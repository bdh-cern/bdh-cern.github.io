- Cloned the app to local\_home in /opt and installed with `pip install -e .` 

Getting the following error when running `app-hysteresis -d MBI --logdir /tmp/logs` :

```
2026-01-16 12:03:47 ERROR    Failed to login with RBAC.                                                                                                                                   application.py:192
                             Traceback (most recent call last):                                                                                                                                             
                               File "/opt/home/brendana/sps-app-hysteresis/sps_app_hysteresis/application.py", line 182, in setup_rbac_authentication                                                       
                                 token = pyrbac.AuthenticationClient().login_location()                                                                                                                     
                                         ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^                                                                                                                     
                             pyrbac._rbac_bindings.AuthenticationError: LOCATION authentication failure: Unable to authenticate.                                                                            
                    WARNING  No RBAC by location, you will have to login manually.  
```

Lacking login-by-location?

This is followed by:

```
File "pyarrow/_dataset.pyx", line 1477, in pyarrow._dataset.Fragment.physical_schema.__get__ File "pyarrow/error.pxi", line 155, in pyarrow.lib.pyarrow_internal_check_status File "pyarrow/error.pxi", line 92, in pyarrow.lib.check_status pyarrow.lib.ArrowInvalid: Could not open Parquet input source '<Buffer>': Parquet magic bytes not found in footer. Either the file is corrupted or this is not a parquet file.
```

... makes me think that the LBL fails, this isn't accounted for, then the buffer pyarrow is trying to read here is actually just a 404 rather than a valid parquet, causing this issue.

**21-01-26:** SPS login-by-location is used for the hysteresis app, even though the VPC is not based in the SPS island. Need to change the app to use explicit RBAC.