
# Summary

1. Generate the project and device with acc-py run app aqflow --wizard \[project-name\]
2. Implement the converter logic in \[project-name\]/\[project_name\]/pipelines/\[transformation_name\]/{converter.py, pipeline.py}
3. Use moks to test with mock data. This is done by running converter.py (?)
4. Publish the device
# Pipelines

```
class AqFlowPipeline(AqFlowOnline):
    def __init__(self, ucap_converter: OneToOneConverter | None = None):
        super().__init__(
            ucap_converter=ucap_converter,
            device_name=device.name,
            transformation=publish_user,
        )

    @aq_node(
        inputs="input_value",
        outputs="data1",
        name="func_1",
    )
    def func_1(self, input_value: FailSafeParameterValue) -> bool:
        logger.info("Processing event in func_1")
        return True

    @aq_node(
        inputs="data1",
        outputs="output_to_fspv",
        name="func_2",
    )
    def func_2(self, data: bool) -> OutputProperties:
        logger.info("Processing data in func_2")
        publications.user.field_name = True
        return publications
```   

- The @aq_flow decorators denote the functions as pipeline steps
- In this example, step 1 is func1 (which outputs data1) and step 2 is func2 (the output of which is converted to a FailSafeParameterValue by the magic work 'output_to_fspv').
	- Schematically: inputs_value -> \[func_1\] -> data1 -> \[func_2\] -> publications
- One defines the publications by inheriting from aqflow's OutputProperties class (see below).
- The logic for the transformation goes in the functions (func_1 and func_2 in this case).
- The input and output types are both FailSafeParameterValue

## Node example

This is an example from the docs of a node which computes an anomaly score for an event based on some sort of position data:

```
@aq_node(
    inputs=["position_data", "intensity"],
    outputs="anomaly_score",
    name="compute_anomaly_score",
)
def compute_anomaly_score(self, position_data: np.ndarray, intensity: float) -> float:
    """Compute anomaly score using statistical analysis."""
    logger.info("Computing anomaly score")

    # Simple anomaly detection using standard deviation
    mean_position = np.mean(position_data)
    std_position = np.std(position_data)

    # Combine position stability and intensity
    position_anomaly = abs(mean_position) / (std_position + 1e-6)
    intensity_anomaly = abs(intensity - 1.0)  # Assuming normalized intensity

    score = position_anomaly + intensity_anomaly
    logger.debug(f"Computed anomaly score: {score}")

    return score
```

# Converter <-> Pipeline interaction

1. In converter.py, the pipeline (AqFlowPipeline) is imported from pipeline.py.
2. In converter.py, a class 'UcapConverter' is defined with a class variable aqflow_pipeline
3. This aqflow_pipline is set to AqFlowPipeline(ucap_converter=self)
	- I.e. the converter stores a reference to the custom pipeline. It's unclear what purpose ucap_converter=self serves.
4. The body of the convert method is simply:
	`return self.aqflow_pipeline.ucap_one_to_one_convert(input_value)`
	... i.e. the converter passes the FSPV input value to the pipeline's inherited convert method (the details of which are probably not important).

The file converter.py just contains the code to run the pipeline  (and testing with mock values):

```
class UcapConverter(OneToOneConverter):
    def __init__(self):
        super().__init__()
        self.aqflow_pipeline = AqFlowPipeline(ucap_converter=self)

    def convert(
        self, input_value: FailSafeParameterValue
    ) -> FailSafeParameterValue | None:

        return self.aqflow_pipeline.ucap_one_to_one_convert(input_value) 
        
if __name__ == "__main__":
	# test code using moks   
```

# Publications and Properties

The pipeline returns 'publications' by default. This is an instantiation of the Properties class, which itself inherits from OutputProperties:

```
from aqflow import (
	...
    OutputProperties,
	...
)

class user(BaseProperty):
    property_name: str = "user"
    lsa_user: str | None = None

class Properties(OutputProperties):
    user: user # I am only publishing the user of the PS here

publications = Properties()
```

So:
- publications is an instatiation of properties
- properties contains the BaseProperty(s) 
- Each BaseProperty defines one of the properies you want to publish.
	- You can define completely custom fields under these properties

Example from [docs](https://acc-py.web.cern.ch/gitlab/epa-wp8-automate-equipment/project-astra/aqflow/docs/stable/examples/step4_implement_pipeline.html#output-properties-setup): 

```
# Define output properties matching device publications
class AnomalyAlert(BaseProperty):
    property_name: str = "AnomalyAlert"
    anomaly_score: Optional[float] = None
    is_anomaly: Optional[bool] = None
    timestamp: Optional[int] = None

class LoggerBeamAnomaly(BaseProperty):
    property_name: str = "logger_beam_anomaly"
    beam_data: Optional[list[float]] = None
    message: Optional[str] = None
    score: Optional[float] = None

class Properties(OutputProperties):
    AnomalyAlert: AnomalyAlert
    LoggerBeamAnomaly: LoggerBeamAnomaly
```
