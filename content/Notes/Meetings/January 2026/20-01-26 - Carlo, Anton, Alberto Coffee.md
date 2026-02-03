
- Can't access UCAP because I don't have access to the test node
- Can't access sps-app-hysteresis because I don't have RBAC
	- Got PO-user from Raul, but this doesn't seem to have fixed anything
- Can try out AqFlow
- Can do reading on:
	- Preisach model, hysteresis predictors
	- Particle accelerators book

# Actions

- [ ] Ask Michi Hostettler or Georges Trad for permissions to pubish the new device to LSA
- [x] Put Carlo, Alberto bi-weekly in the meeting with Alex and Francesco
- [x] Make a new meeting with Carlo, Alberto, bi-weekly, Tuesday 3-4pm, somewhere near CCC
- [ ] Change app-hysteresis so that RBAC LbL is not required (rather, 'explicit' RBAC)
- [x] Create a new branch and start making changes
- [ ] Set up Claude to interpret the gitlab

# Meeting

- RBAC requires login-by-location
- Need to change the app so that it logs in 'explicitly'
- Anton has been refactoring the UCAP node via genai to be more up to date
- Anton may be absent for all of Feb, then back for 4 months (until end of June)
- Is the PS ramp-up parameterised or not?
	- Anton thinks that the power converters would already have tripped in the SPS case if the ramp-up was not altered by the propagating back the flat-top correction
	- SPS is parameterised, but B correction is linearly interpolated from 0 (at beginning of injection) to flat top (hence does not introduce discrete jump)
	- Interpolation begins at start of ramp-up
- Organise biweekly Alex, Francesco, Carlo, Alberto
- Organise biweekly C&A 3-4
- Anton is setting up a LSA virtual device which contains LSA settings related to the hysteresis compensation
	- Class is HystCompFlags
	- e.g. enabled, trim time start, end, etc.
	- UCAP node will subscribe to this, and e.g. B main, and publish BHYST after transform
	- How is BHYST sent to the actual machine?
	- This will have to be PPM (e.g. changing to enabled for SFTPRO and disabled for everything else)
	- Device name: SPS.HYSTCOMP.MBI.FLAGS (https://ccde.cern.ch/devices/2400688)
	- Device class: HystCompFlags https://ccde.cern.ch/devices/classes/46106/version/47330/properties
	- Will still need to publish the device to LSA
		- Lacking permissions
	- These should be RBAC protected, ultimately
	- Ask Michi Hostettler or Georges Trad for the necessary permissions to publish to LSA
	- Otherwise Kevin probably has the permissions to do this

