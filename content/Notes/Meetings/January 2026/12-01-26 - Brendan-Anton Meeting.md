# Summary

## ML stuff

- TransformerTF contains the training scripts
- sps-app-hysteresis contains the actual program. Download on the TN.
## SoTA

- Static effects: working with TFT. App exists to deploy this. Has not been tested live.
- Dynamic effects: Works in app, but not by default. Uses a similar NN. Less well-developed.
- Chroma stuff: we don't know why the chroma changes after switching to RMD1.  If the $\Delta\xi$ is consistent, then we can mitigate it with settings.
## Goals

- We need to see if the chroma change $\Delta\xi$ from switch to [[Depowered MD1]] is consistent across different supercycles
	- This will let us know if we can correct it using settings tag, or if something more complex is needed
- Adopt a low priority for static effects
	- However, further work on this new, simpler method of Anton's is interesting
- Work out how we can flatten MD1 before beam commissioning. 
- Define a spill quality factor as a KPI
## Actionables

- Play the functions from [[01-12-25 MD - Cancelled Chroma Scans]] in the lab with Carlo and Alberto. Analyse sextupolar component from dipoles.
- MD to replace [[01-12-25 MD - Cancelled Chroma Scans]] 
- Bug fixes and verification of existing NN-based hysteresis compensation app
	- Especially important to verify untested framework to run this live
- Investigation of Anton's new, simpler scheme (could be deployed on Geoff). Possible development of this by me.
- In general, work with magnets lab to resolve the discrepancy in the machine vs lab eddies.
	- Eddies are low-priority because they are not needed for switch to [[Depowered MD1]]

# Meeting notes

Notebook: https://quartz.haochen.lu/

To discuss:

- Which MDs last year were related to the chroma measurements?
	- Noticing problems in July
	- [[22-08-25 MD - Dipole chroma scans]] - 
	- [[19-11-25 MD - Messy chroma analysis]] - 
	- The quick parallel one - SFTION, SFTION, LHCION
		- main dipole field altered
		- validates the idea that LHCION causes hyst. in the SFTION (0.1GeV range)
	- 1st Dec - get more complete view of chroma changes based on various scenarios (failed because of no protons)
- What were the goals/progress of last year?
	- Finding the origin of the sextupolar field with MD1 is removed?
	- Dynamic effects (eddy currents?)
	- Effort was mostly on control using surrogate model
	- Late -> realised need modular approach for
		1. dynamic (injection)
		2. chroma
		3. flat-top
	- Problem encountered: precision (drift on B-train and lab quadrupoles) not sufficient
	- Dynamic effects different in lab --- just look at static effects (quads)
		- taking out vacuum chamber was an issue because it was the supporting structure for the measurement coils
		- issues with power converter causing noise which caused drift of the measurement coils (fluxmeter)
		- NMR only locks in clean dipole field
	- Difficult to do integration correction because it will wash out hysteresis effects
	- injection plateau is meant to be flat - programmed as a slight increase to counter the slight decrease from eddy currents. result is approximately flat
- What is the 'state of the art' of the hysteresis compensation scheme?
	- TFT to predict static effect
		- Where does this work? Flat-top only?
	- What about eddies - exponential convolution, analytical model; works the same as TFT, corrects with respect to a reference value
	- Both can be enabled by ticking a box in the GUI somewhere
- What are we trying to do immediately in the new year?
	- Prioritising chroma
		- to see if our chroma is consistent; can we make two different set of settings for the FT that we switch between (one for normal MD1 and one for flat MD1)
		- want to make sure $\Delta\xi$ is similar no matter what the super cycle is - this will allow us to simply have some settings to compensate for it
	- What's the plan for the eddies?
		- Not actually needed for flattening MD1
		- Talk with Kevin to see what he wants to flatten MD1
		- Flatten MD1 during beam commissioning
	- What do we need to do next on static effects? Priority?
		- BO with ten in one out (low priority) - flat top field only
-  Actionables in new year:
	1. re-do the cancelled MD 
	2. perform the hand-over 
		- Me to run GUI, training 
	3. analyse the function from the cancelled MD in the lab with C&A
		- analyse the sextupolar component 
	4. online hysteresis compensation - running this in the GUI
		- fixing bugs, testing, monitoring, etc
		- set up on ccc computers - currently running on VPC which is ssh'd into
		- ucap node running - verify
		- framework to run this online exists, but this is untested
		- ...or write a package to run the BO version on Geoff?
	5. take a look at the dynamic effects
- Longer-term goals:
	1. flatten, then remove MD1
	2. Resolve lab-MD conflict (eddies)
	3. Define the spill quality factor as a KPI


- Smaller questions:
	- In [[22-08-25 MD - Dipole chroma scans]], was the quadrupole MD1 on or off? - on, unlikely that the quads would contribute strong 6pole, due to symmetry in their function
	- In each MD, what was 'MD1 off' - zeros? Flat? What energy? yes for 19/11.
		- 'our MD1' = 0 on dipole, quads, pulse on 6,8'
		- zeros = 0 on everything
		- for the set of md1 off in nov, on actual 0
		- Could characterise difference between 'FMD1' and zero
	- Why N=100 for nafflib? More resolution for the clustering?
	- Could we just use estimatedH/V for the chroma instead of nafflib
		- nafflib doesn't use FFT, estimatedH/V uses FFT which is less precise
		- works better for low amount of data

Notes
- generic optimisation framework (GEOFF)

Running the Predictors:
- gitlab:
	- sps-app-hysteresis - the app, on acc-py
	- sps-mlp-hysteresis-compensation - the actual predictors, on gitlab too
- transformertf - contains training 
- clearml for monitoring???

