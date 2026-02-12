
Issue: main window does not show simulated B-train, although in the prediction history window, the program claims to be retrieving the measured field (but not showing the measured field with respect to the reference).

![[Pasted image 20260209131319.png]]

![[Pasted image 20260209131345.png]]

Anton's thoughts:

> in principle, the operational and spare b-train switches to simulated B field when sources is missing
> 
> I noticed last time I ran the bug there was a bug with saving measured field into the CycleData, maybe? so that'd be the reason the blue line in the scrolling plot is missing and the bottom middle plot
> 
> but the white line delta is expected. as previously mentioned, the reference is the first prediction. so the dB is the B_ref - B_pred

Confirmation unclear on 'so it should actually already use the simulated B-train'...

The fact that the prediction always seems to be at zero (even when the supercycle is changed?) makes me think there's something wrong here --- not just a visual/display bug.

# Finding the data

1. plotModel: `_handle_new_measured` <--connected-- `OnCycleMeasured`
2. RemotePipeline: `_handle_cycle_measured` --calls--> `OnCycleMeasured.emit`
3. RemotePipeline: `_setup_subscriptions` estabilishes endpoints according to `remote_params`
4. These come from `app_context.REMOTE_PARAMS` (not in [[Online & Offline Modes|offline]] mode... must be something else)
5. ... static variables in `app_context` seem to define which parameters the app is looking for
6. these are set by the 'recipes' in the application contexts ``__init__``

`_handle_cycle_measured`--calls-->So OnCycleMeasured--emits-->`_handle_new_measured`

There doesn't seem to be any version of `_handle_cycle_measured` anywhere in the standalone (non-UCAP) version of the app.

The programmed current is displayed because this relies on `OnCycleForewarning`, which is indeed in the StandalonePipeline. (???)

**ToDo**: implement `OnCycleMeasured` in the `StandalonePipeline`.

Looking at the programmed current:

1. Variable in the plot is called `model.current_prog_source`
2. This is set in `PlotModel._handle_new_programmed` from `cycle_data.current_prog`
3. `_handle_new_programmed` is connected to `onCycleForewarning`
4. `onCycleForewarning` actually returns `QtEventBuilderAdapter.cycleDataAvailable`, in hystcomp_event_builder so it is **actually** connected to this.
5. This indeed emits (via a chain of connections) when the `_correction_core` of `StandalonePipeline` fires its `cycle_data_available`

Back to measured B (sticking to standalone):

1. `model._field_meas_source` has its value set in `_handle_new_measured`
2. `onCycleMeasured` actually points to `_add_measurement_ref.cycleDataAvailable`. `_add_measurement_ref` ultimately comes from `SynchronousOrchestrator`
3. `cycleDataAvailable` is in QtEventBuilderAdapter, which implies it is generic but really seems to be quite specific to cycle data acquisition. Emits when `_builder.cycle_data_available` emits[^1]
4. `_builder.cycle_data_available` emits when `AddMeasurementReferencesEventBuilder.on_new_cycle_data` fires --- and this **does not** fire
5. This seems to perculate back to `_add_measurement_post` in `_synchronous`, which is an instantiation of `CycleStampedAddMeasurementsEventBuilder`
6. `CycleStampedAddMeasurementsEventBuilder` has a method `on_cycle_stamp_group_triggered` which looks like it should update the B and I values
7. There seems to be a check failing in `_cycle_stamp_grouped` called `_check_ready` which seemingly makes sure all the buffered data is available before it calls `on_cycle_stamp_group_triggered`
8. This check fails because the correct cyclestamp isn't in the buffer





 

[^1]: At first glance, this seems to emit everywhere (because it is a method of QtEventBuilderAdapter), but in fact this particular instantiation of it in AddMeasurementReferencesEventBuilder only emits as described in the following step.
