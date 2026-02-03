To dos:

- [x] Work out the contributions that have been made to ULTIMATE
- [x] Read the relevant parts of the ULTIMATE paper and leave comments if necessary
- [x] Install ULTIMATE and see if the reproducability bug is still there
- [x] Find a time for the MD coordination meeting next week
- [x] Reboot the VPC
	- [x] try to access it with VSCode
	- [x] Write confluence pages to explain this
- [x] Access the UCAP node
	- [x] Try to create a test device and converter and publish some stuff


# ULTIMATE:

- Running with sudo does not properly add LD_LIBRARY_PATH (but running without does not e.g. launch ./test_installation properly)
- Storm is not installing correctly. Compiling the binaries from source.
- Built storm. Test this on Monday.
- ... tested. Storm now working. Automated installer not so much.

## Problems with SMD

Three properties:

- SL1 (the only one in SmartLighting)
- MS1 (the top one, ending with '& detected')
- MS2 (the other one)

Commit 4d3074e2d3426958abdb744f850c9ed4a96ca918

| Order         | SL1         | MS1      | MS2     | Notes                                                                                       |
| ------------- | ----------- | -------- | ------- | ------------------------------------------------------------------------------------------- |
| SL1, MS1, MS2 | 10.16326804 | 0.392    | 0.4     | 0s in MS1 (pLow, pMed), all 0s in MS2, SL1 fine. Repeated this order with identical results |
| MS1, MS2, SL1 | 5.0         | 0.227... | (Error) | 0s in MS1  (pDetected), probabilities sum to -ve in MS2, 1 state only for SL1               |
| SL1, MS2, MS1 | 10.16326804 | 0.392    | 0.4     | 0s in MS2 (pLow, pMed), all 0s in MS1                                                       |
| MS2, MS1, SL1 | 5.0         | (Error)  | 0.4     | NO 0s in MS2, MS1 probabilities sum to -ve, 0s in SL1 (pDetected)                           |

Example of 0s in SL1 (pDetected):
![[Pasted image 20260126152006.png]]