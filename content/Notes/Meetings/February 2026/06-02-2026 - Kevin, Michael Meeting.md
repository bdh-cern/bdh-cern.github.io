
- Incorporation rule: how to incorporate a new value into existing LSA settings
	- Defined by BP and parameter type
	- No name
- LSA: value=target+correction
- BHYST
	- parameter type B
	- Make a note of BP name
	- Probably need to change the parameter type to avoid messing with the incorporation rules for important settings
	- Created new parameter type BHYS
- InCA - LSA for the injectors
- Transient - trim that's only valid for a week
- PyDA_LSA - anton's package to send trims to LSA
	- Update to new version and use Michael's code to send the incorporated trim (relative delta)
	- clone latest release from gitlabs specifically
- Figure out where the BHYS parameter type went
- Want to get a relative delta in the incorporation
- K - optics parameter corresponding to magnetic field strength
- Make rules...
	- Currently B->BHSYT->I
	- But we might want two branches:
		- B---->I
		- BHYS---->I
		- ... such that B and BHYS are combined to give I
	- Why does it work for the chroma? 
	- Core question: how do we make BHYS an additive quantity that adds to the I which is set by B?
	- What is a knob/knob make rule

- Currently BHYS is 'B with corrections for hysteresis'. But rather it should be 'the correction on top of B to account for hysteresis'
- How do I get on to NEXT?: CCM->CO->Lsa next
- How do I get to the parameter type application? -> Link from Michael

Existing make structure for chromaticity is what we roughly want to replicate: 

![[Pasted image 20260206141152.png]]

