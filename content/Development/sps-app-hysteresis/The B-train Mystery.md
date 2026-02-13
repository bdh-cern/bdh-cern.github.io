
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


# Fixing UCAP

- It looked like the problem was that the relevant data could not be downloaded from the HYSTCOMP node
- This was because the node was relying on a deprecated timing device (see [[12-02-26 - Anton Debugging]])
- After fixing the node (sps-ucap-hysteresis-compensation 0.3.5.dev1) the app still isn't displaying the measured B

# Fixing the buffer

- The `_check_ready` function in `_cycle_stamp_grouped` is repeatedly returning false
- The specific check is 
```
            if cycle_stamp not in buffer[selector]:
                return False
```
- ...this means that the data for the cyclestamp for the cycle which has **just played** has not been downloaded into the buffer.
- Based on the following log breakpoint, the cyclestamp has not yet been added to the buffer:
  ```
  1770912464535000000 not in buffer for SPS.USER.SFTPRO1. Stamp in buffer: {1770911236935000000: 0, 1770911276535000000: 1, 1770911316135000000: 2, 1770911355735000000: 3, 1770911395335000000: 4, 1770911434935000000: 5, 1770911474535000000: 6, 1770911514135000000: 7, 1770911553735000000: 8, 1770911593335000000: 9, 1770911632935000000: 9, 1770911672535000000: 9, 1770911712135000000: 9, 1770911751735000000: 9, 1770911791335000000: 9, 1770911830935000000: 9, 1770911870535000000: 9, 1770911910135000000: 9, 1770911949735000000: 9, 1770911989335000000: 9, 1770912028935000000: 9, 1770912068535000000: 9, 1770912108135000000: 9, 1770912147735000000: 9, 1770912187335000000: 9, 1770912226935000000: 9, 1770912266535000000: 9, 1770912306135000000: 9, 1770912345735000000: 9, 1770912385335000000: 9, 1770912424935000000: 9}
  ```
- ... however, an earlier log message is looking for 1770912424935000000, which is indeed in the buffer by the time of the log above

[^1]: At first glance, this seems to emit everywhere (because it is a method of QtEventBuilderAdapter), but in fact this particular instantiation of it in AddMeasurementReferencesEventBuilder only emits as described in the following step.
