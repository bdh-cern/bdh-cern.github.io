
For [[Hysteresis App]]

Current error:

```
Traceback (most recent call last):  
 File "/opt/home/brendana/sps-app-hysteresis/sps_app_hysteresis/widgets/trim_widget/_view.py", line 208, in onEnableTrim  
   self.model.settings.trim_enabled[self.model.cycle] = (  
   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^  
 File "/opt/home/brendana/sps-app-hysteresis/.venv/lib/python3.11/site-packages/hystcomp_actions/correction/_settings.py", line 124, in __setitem__  
   self.parent.trimEnabledChanged.emit(cycle_name, value)  
   ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^  
AttributeError: 'PyQt6.QtCore.pyqtSignal' object has no attribute 'emit'
```

GPT guess:

Summary
	.emit() only exists on bound signals
	You are calling it on a signal descriptor
Ensure:
	Signal is declared on a QObject subclass
	You are using an instance, not the class
	The signal is not reassigned
	This is a structural issue, not a runtime edge case.

Moved:

self.trimEnabledChanged = QtCore.Signal(str, bool)
(etc.)

from `__init__` to the class declaration for both QtTrimSettings and OnlineTrimSettings

... Can't tell if the issue is actually fixed but the app no longer complains when I turn the trims on.

**Fixed:** implemented in [v0.3.1](https://gitlab.cern.ch/dsb/applications/op-app-context/-/commit/bed174fa5dd4ca7d2d5a78fc35cef6a45ce3fea4)
