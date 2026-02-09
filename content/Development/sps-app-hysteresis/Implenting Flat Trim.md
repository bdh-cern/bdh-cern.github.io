

NB: Might need new name other than 'Flatd Trim'. In any case this is a trim which is applied as a single value across the flat-top.

- Anton's recommendations:

> it's in `hystcomp-actions.trim`
> 
> you need to implement an interface like [https://gitlab.cern.ch/dsb/hysteresis/hysteresis-compensation-actions/-/blob/master/hystcomp_actions/protocols.py?ref_type=heads#L118](https://gitlab.cern.ch/dsb/hysteresis/hysteresis-compensation-actions/-/blob/master/hystcomp_actions/protocols.py?ref_type=heads#L118)
> 
> with an example like
> 
> [https://gitlab.cern.ch/dsb/hysteresis/hysteresis-compensation-actions/-/blob/master/hystcomp_actions/trim/_trim.py?ref_type=heads](https://gitlab.cern.ch/dsb/hysteresis/hysteresis-compensation-actions/-/blob/master/hystcomp_actions/trim/_trim.py?ref_type=heads)
> 
> and just use your new trim class instead of the default one.

First link is to `InferenceProtocol`, which as far as I can see is never implemented once across the project except in `EddyCurrentInferenceProtocol`. There is also a `TrimProtocol` but this inherits from Protocol and is not even in `__all__` i.e. is not even visible when the module is imported.

Second link is to `Trim`, which is indeed used in sps-app-hysteresis. This seems to ingest some settings and maybe contains the actual driving logic.

Discovered `_context_recipes` in application.py which is a mad way of setting the trim settings from the CLI, (but not really from the CLI). This definitely needs a rework so that default profiles can be switched between inside the app.

Ultimately probably need a Trim interface which both pointwise and fixed implement. Then Trim can just have e.g. `.apply_trim()` and the logic can be hidden in the inheritors.

**Need to make changes to `_standalone.py`, which is the only place that handles PointwiseTrim.** <- Resume from here

- `self._trim_core()` is set to a `PointwiseTrim` instance in `StandalonePipeline`
	- Then `self.orchestrator` is set to an `SynchronousOrchestrator` instance which has `trim=self._trim_core` as an argument
	- The pipeline then gets all sorts of instance variables set to QtEventBuilderAdapters which presumably exposes the orchestrator builders to it:

		self._create_cycle = QtEventBuilderAdapter(
		self._orchestrator.create_cycle, parent=parent
		)
		
	- The orchestrator is then started in `_standalone.start()` which only calls `self._orchestrator.start()`
		- The latter method iterates over builders and start them


# Changes

Changed the context given to `_lsa.set` from:

```
            # context=LsaCycleContext(
            #     cycle=cycle,
            #     comment=comment,
            #     flags=TrimFlags(
            #         transient=True,
            #         drive=context.lsa_server not in {"next", "dev"},
            #         propagate_to_children=context.lsa_server not in {"next", "dev"},
            #     ),
            # ),
```

to 

```
 context = pyda_lsa.LsaIncorporationContext(
                cycle=cycle,
                cycle_time=6000.0, # change to trim start time I think
                flags=pyda_lsa.TrimFlags(
                    relative=True,
                    transient=True,
                    drive=context.lsa_server not in {"next", "dev"},
                    propagate_to_children=context.lsa_server not in {"next", "dev"},
                ),
```

which is now using this new LsaIncorporationContext from the newest version of pyDA_lsa. The only difference between it and the old LsaCycleContext is that it stores the cycle time which I guess points towards the BP and thus the incorporation rule.