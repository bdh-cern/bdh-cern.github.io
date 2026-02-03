3 pm - 5 pm, Glassbox

Indico: https://indico.cern.ch/event/1621996/

Discussion: 
# Summary 

## Plan

- The chroma MDs will be repeated during beam commissioning on 17th, 18th Feb.
- The TFT approach should be validated and bugs should be fixed.
	- GP approach can be investigated and implemented at a later date.
- Parasitically take data during hardware commissioning to test hysteresis prediction quality
- We should only expect to depower/flatten MD1 in the near/medium term. Removing it would require major overhauls to the hardware
- Work out how to flatten MD1 during commissioning (as well as chroma measurements)
- One dedicated MD slot --- think this is separate to the beam commissioning time
## Hysteresis App

- Currently exists with a GUI and in-built prediction logic.
- The prediction logic also exists on a UCAP GPU node, which does the same thing.
	- Some issues with 'locking down' this GPU node. We don't want other people to be able to break it by accident.
- Correction is flat-top only and gives a constant, once-per-cycle offset
	- I believe it predicts the hysteresis point-by-point over the flat-top, then averages this for a constant offset
	- Offset is the order of 1e-4T
- A once-per-cycle offset protects the power converters against rapid oscillations, but even individual $\Delta B$ could theoretically drift over time and push $I$ into unsafe regions.
	- This should already be protected against in LSA
- Operators will need to make an incorporation rule for the flat-top correction to propagate correctly
	- Although I though this had already been done with BHYST?

## Questions

- What is Marco's idea about this dipole feedback thing?
- What was the discussion about the number of BPs in the MD? 
	- Talking about going from 6 to 3 BPs, but isn't MD1 already 3 BPs?
- What is this nuance about having to make momentum modifications when MD1 is removed?
	- This apparently causes a loss of 'ppm-ness' --- why?
- What is the plan with the modification of the ramp (seemingly separately from the flat top)?
	- I thought that LSA would automatically take care of the interpolation between injection and flat-top?



# Notes

- Can't measure chroma in lab, only 6-pole component
- is 26 GeV MD1 flat or not?
- Anton supposed to be present from Feb onwards to write thesis
- What are the opportunities for MD and during beam commissioning?
	- Redo the cancelled MD?
	- Use an SPS dedicated MD slot for this instead?
- App can run with events published to japc(?)
	- Subscribe to next cycle, then you know future programmed current
	- B-train as input
- UCAP has the same logic running continuously
- GPU needed - UCAP occupies sole GPU node in CCR
- Find the pre-MD1 papers (A)
- Offset is order of 1e-4T
- Correction is to flat-top only
- Risk of breaking the power converters with plus/moin
- Individual $\Delta B$ can add up over time and break converter (with too high I)
	- But this can be caught in LSA (defined by IMAX)
	- And is also protected against in the power converters
- Correction is one-per-cycle ('constant') so this should hopefully be sufficient to protect the power converters
- Hysteresis app to do:
	- bugs
	- integrate with UCAP (make it 'on-line')
	- monitoring GUI
- OP side will have to work on:
	- incorporation rule
	- making sure limits are in place to protect hardware
- App has a hard-coded number which defines the minimum correction; lower corrections will be ignored and not used to trim
- Hardware commissioning: parasitically take data to test the quality of the of the prediction
- Investigate hysteresis in the ramp in the future
	- "would guarantee that the flap-top and the ramp move together" - why wouldn't this be the case, considering the ramp is calculated by LSA as a linear interpolation
		- No it isn't - the correction is linearly interpolated.
		- parallel on SHiP cycle
- One dedicated MD slot
- MD1 flat settings would require a chromaticity and a momentum offset
- Loss of 'ppm-ness' i.e. ability to make pulse-to-pulse modifications
	- Why would this be the case?
- What is beam based alignment?
- Commissioning:
	- do the set-up
	- then we work out exactly what we need to do when we flatten MD1
	- do the set-up as usual with MD1 though
- Can put beam in flat MD1
- MD1 is 3 bp usually
	- What is this discussion about reducing the MD1 from 6 to 3bp
- 16th Feb -- beam based alignment (what exactly is this)
- 17th, 18th test the MD1 (redo the cancelled MD)
- What is Marco's idea?


# Info



| Date                   | SCs                                                                                                                                    | Notes                                           | $Q_H'$ (norm.)                        | $Q_H''$ (norm.)                            | $Q_V'$ (norm.)                            | $Q_V''$ (norm.)                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------- | ------------------------------------- | ------------------------------------------ | ----------------------------------------- | ------------------------------------------ |
| 22nd Aug               | SFTPRO-MD1 (on/off) -meas                                                                                                              | MD1 off only on 2-poles (4,6,8-poles untouched) | ON: -3.18 (-0.12)<br>OFF: 3.71 (0.14) | ON: 377.09 (14.16)<br>OFF: 1297.36 (48.75) | ON: -6.89 (-0.26)<br>OFF:  -12.21 (-0.46) | ON: 132.82 (4.99)<br>OFF: -495.46 (-18.61) |
| 19th Nov               | SFTPRO-LHCPILOT-MD1 (on/off)-meas                                                                                                      | MD1 off everywhere (ZERO on 2,4,6,8-poles)      | ON: -2.60 (-0.10)<br>OFF: 2.49 (0.09) | ON: 509.17 (19.12)<br>OFF: 1606.61 (60.35) | ON: -8.29 (-0.31)<br>OFF: -11.74 (-0.44)  | ON: 216.71 (8.14)<br>OFF: -784.72 (-29.48) |
| 1st Dec<br>(Cancelled) | 1. LHCPILOT-26Gev MD1 (on/off)-meas<br>2. LHCION(dyneco)-200GeV MD1-meas<br>3. LHCION(dyneco)-26GeV MD1-meas<br>4. LHCION(dyneco)-meas | DynEco cycles to replicate SFTPRO hysteresis    |                                       |                                            |                                           |                                            |
|                        |                                                                                                                                        |                                                 |                                       |                                            |                                           |                                            |

![[image(6).png]]

![[image(7).png]]