# Main things

- How can we correctly categorise BHYS under the BHYS parameter type?
- How can we change the make rule structure such that B BHYS are used additively to calculate I
	- A similar structure is already used to calculate QF mains from multiple additive sources 
- Why does the tune control run through K, whilst the B (or BHYS) control does not?

# Meeting notes

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
	- BHYS has a make rule which goes directly to I, but other quantities have one that influences K first. Why?
	- Core question: how do we make BHYS an additive quantity that adds to the I which is set by B?
	- What is a knob/knob make rule

- When trimming BHYS start of flattop BP, need to make sure that there is a node with value 0 in the previous BP from which to linearly interpolate up to positive value of BHYS
	- This can't be too fast or the make rule for IMAINs will fail
	- 20ms before trim is sufficient 

- We think that it's fine to trim correction. Doesn't seem to make a difference to what we want to do at the moment.

- Currently BHYS is 'B with corrections for hysteresis'. But rather it should be 'the correction on top of B to account for hysteresis'
- How do I get on to NEXT?: CCM->CO->Lsa next
- How do I get to the parameter type application? -> Link from Michael


# Figures

Existing make structure for chromaticity is what we roughly want to replicate: 

![[Pasted image 20260206141152.png]]

Incorporation rule (highlighted):

![[Pasted image 20260206152904.png]]