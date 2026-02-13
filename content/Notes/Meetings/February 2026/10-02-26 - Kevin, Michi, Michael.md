
- Updating parameter type will necessitate updating the make rule definition
- New make rule to add B and BHYS
- BHYS added to database but now appearing in LSA next suite
- Incorporation rule:
	- PlateauIR to perform the little linear interpolation at the start of the flat-top
	- Also could use decay IR to decay the interpolation backwards from the flat-top
- Parameters
	- Beam energy
	- RF freq
	- Orbit
	- B field
- Radial loop - maintains RF to whatever keeps you on central orbit
- Synchro loop - maintains RF to programmed; always off for FT
	- Used for LHC beams becuase the SPS needs to match the LHC's frequency
	- FT never needs to match anyones orbit so the SL is never used
- Past transition -> small freq change causes undetermined orbit
- Extraction depends on orbit so correcting when
- If phase loop corrects phase, only time the SL **would** fire is when phase loop fires to correct phase can (probably) not 
- How do we correct the ramp? Because this is subject to hysteresis, but the flat-top correction cannot simply be linearly interpolated
- SE corrections today are purely flat-top based, but how?
- [ ] Ask magnets team about the correction on the ramp
- Incorporate with constant decay IR with 60ms on ramp
- Why doesn't SL itself solve the hysteresis issue?
- trim settings: `propagate=False`
- Ask about the delta Q = R relation
- K = bending angle for dipole, gradient for quadrupole
- Values of B required for e.g. chroma corrections are energy dependent, so more convenient to calacluate via normalised optical parameters. Dipole corrections are not so sensitive.
- Decide when to push the new hierarchy and make rule to next/lsa. Can only do both at once.

1. SPS uses RL, but this is switched off at FT
2. If on RL, any change in B will change E
3. If on SL, any change in B will change orbit, not E
4. If on no L, will change orbit
5. Only sending a FT trim -> make sure RL is **still on** so it can correct for the orbit difference (as this is important for the slow extraction)

Maybe be can use the SL to simply correct the hysteresis by correcting B and altering orbit. If the orbit correction is <1mm, then this may be suitable.


