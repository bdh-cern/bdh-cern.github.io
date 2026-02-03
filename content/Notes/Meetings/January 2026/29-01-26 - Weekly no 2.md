
- [ ] What is the AqFlow workflow?
- [ ] How do I choose a converter in the wizard if the converter is not yet created?
	- [ ] What about choosing a convertor that already exists on acc-py? Can converters be used independently of the devices in this scheme?
- [ ] How do I actually deploy?

- When I install my package on the note I get:
```
Installing Python package ucap_test_bdh ...  
Installation of ucap_test_bdh:null was successful:  
Using Python 3.11.11 environment at: venv  
Resolved 148 packages in 3.85s  
Audited 148 packages in 1ms
```

- Why ucap_test_bdh:**null**?
# Notes

- Quality factor aka duty factor (unitless or %) aka effective spill length (time) extracted from BSI - aluminium foil which produces secondaries, picked up by PMT,
	- Fabio Follin, BE-OP-SPS: ask how this is defined, frequency
	- Low frequency = easy, high = hard
	- So spill quality factor is sampling frequency-dependent
	- Or using the BCT?
		- 5ms simulation time
	- Ask which device is being used to calculate SPSQC:EFF_SPILL_LENGHT \[sic\]
- 108 QDs have one power converter
- QF2 is something to do with the split power converter for the QFs
- B3 to chroma done 'by simulations'
	- Pre-existing model which we can use to do this
	- Two definitions for 6poles: defined in series expansion, definition is whether one does/does not take the coefficient before 6pole term
- ucap python client
- Make new chroma curves for different windows in the injection plateau
	- Original window is something like 200-1000
	- Make new ones at 200-400, 400-600, 600-800, 800-1000 etc.
- Xuite SPS model
	- K2 - is the B3 normalised to beam rigidity is MADEX terms, the normalised gradient
	- Spit out chromaticity information - evolution of the optics functions along the ring, along with the global parameters
	- We want to try two different K2s to see the predicted chromaticity gradient
	- Want to find out the OoM of the B3 we need to be able to see in the lab (and if possible) 
	- 1e-6T is noise level in lab
	- Take whatever chroma we get out of xsuite, look at the B3, apply the difference observed in the MDs,  look at the new B3, get the $\Delta B3$ (or K2)