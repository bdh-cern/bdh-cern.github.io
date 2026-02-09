
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

The programmed current is displayed because this relies on `OnCycleForewarning`, which is indeed in the StandalonePipeline.

**ToDo**: implement `OnCycleMeasured` in the `StandalonePipeline`.
 






