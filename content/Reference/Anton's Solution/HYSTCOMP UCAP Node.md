- Node is UCAP-NODE-SPS-HYSTCOMP
- Main device of import is presumably SPS.HYSTCOMP.MBI
	- "Prediction for SPS Hysteresis Compensation on Main Bending Magnet"
	- This has 12 transformers, all currently stopped
	- Most interesting is probably sps-ucap-hystcomp-predict-next-cycle ("Prediction for SPS Hysteresis Compensation on Main Bending Magnet")
	- No actors on this node, so is it actually capable of applying trims at the moment?
- Package is called [sps-ucap-hysteresis-compensation](https://acc-py-repo.cern.ch/browse/project/sps-ucap-hysteresis-compensation).
- Also [sps_mlp_hystcomp](https://acc-py-repo.cern.ch/browse/project/sps-mlp-hysteresis-compensation) which contains the actual TFT predictor (and others)

# Prediction pipeline

The pipeline works between the two packages. Most of the logic is in sps_mlp_hystcomp, under several layers of abstraction.

1. sps-ucap-hysteresis-compensation contains sps_ucap_hystcomp/predict_next_cycle/\_converter.py
2. \_converter.py imports TFTPredictor from sps_mlp_hystcomp, sets it up, and calls predictor.predict_cycle()
3. In sps_mlp_hystcomp, Predictor.predict_cycle() calls the abstract method Predictor.\_predict_impl
4. EncoderDecoderPredictor inherits from Predictor and implements \_predict_impl. Most logic is in this method and \_predict_dataset
5. TFTTransformer inherits from EncoderDecoderPredictor and only overrides the method to load the model weights

In summary:
1. converter.py -> predictor.predict_cycle()
2. predict_cycle() -> \_predict_cycle_impl()
3.  \_predict_cycle_impl() -> EncoderDecoderPredictor. \_predict_cycle_impl() *(override)*
4. EncoderDecoderPredictor.\_predict_cycle_impl() -> \_base_predictor.predictl()
5. predict ->EncoderDecoderPredictor.\_predict_impl()
6. \_predict_impl() -> \_predict_dataset()
# Devices

Devices on this node: 

![[Pasted image 20260129122341.png]]