
# Questions from [[14-01-26 - WP4 Meeting]]:

- What is Marco's idea about this dipole feedback thing?
	- He was talking about implementing B-train feedback control on the SPS, similar to what is used on the PS currently.
- What was the discussion about the number of BPs in the MD? Talking about going from 6 to 3 BPs, but isn't MD1 already 3 BPs?
	- Was talking about a 6-BP MD cycle, **not** MD1
	- Discussion was that maybe we could do beam stuff in MD1, which would probably require 4 BPs
		- Alex, Francesco disagree that it would take as many as 4 BPs - might only take 1.
		- This would require the MD1 to be on 26 GeV (not idle) so beam can be injected
		- Doing so would effectively double the parallel MD capacity
- What is this nuance about having to make momentum modifications when MD1 is removed? This apparently causes a loss of 'ppm-ness' --- why?
	- They were worried about the effect that removing MD1 would have on SFTPRO after an proper MD cycle was played.
	- This might cause problems with injection because the MD cycles sometimes use high energies in high-order components.
- What is the plan with the modification of the ramp (seemingly separately from the flat top)?
	- The flat-top shape does not propagate back to the ramp shape, so there can be a discrete continuity (which LSA will linearly interpolate over)
	- SPS works on 'tables' --- i.e. array of (time, field) pairs which define the magnetic shape.
	- In contrast, the PS has pre-defined parameterised definition of the whole shape, so if one point in e.g. the flat-top is moved, the ramp will automatically be adjusted accordingly.
- What about this old idea of thinking of a spill quality factor (from Nov)?
	- Spill quality factor is already logged, we should start using it.
	- We should also work out precisely how this logged quantity is defined.

## Actions:

- [ ] Work with Anton on the app bug fixes
- [x] Also ask for the magnetic functions for the magnets lab
	- [x] export from LSA, get from trim history, export historic one
	- [ ] RBAC error stopping me from accessing the tags on MD1 clone
- [ ] Reading on hysteresis predictors, particle accelerators book
- [ ] See if I can train the TFT on a point-wise prediction with 10in 1 out
- [ ] Interface with UCAP

# Miscellanea 
- Important to centre during ramp
- Radial loop - erf, feedback loop looking at this one bpm which estimates the error in energy and changes the frequency to keep the beam centred during the ramp (start_ramp to start_flattop)
