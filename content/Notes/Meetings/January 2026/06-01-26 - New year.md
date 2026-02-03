
Before the break: working on the chroma analysis, focusing most recently on that of the 19th Nov MD (the rushed one with limited data).

# Related MDs
- [[19-11-25 MD - Messy chroma analysis]]
# From notebook

- Have a look at cycle of interest at 17:02:15 (CH)  on 19-11-26
	- QC FFT suggests $Q_{H}^{frac} \sim 0.61$ with secondary peak around 0.64.
	- Different windowing gives different results:
		- FFT window length 1 $\rightarrow$ 0.61. 0.62 peaks retrieved 
		- FFT window length 2 $\rightarrow$ 0.64 peak retrieved
		- The latter is probably more correct as the 0.61 peak is likely $Q_V^{frac}$ (generally  $Q_{H}^{frac} > Q_{V}^{frac}$)
- Contrive some way of comparing  $Q_{H}^{frac}$ and $Q_{V}^{frac}$ signals and programmatically weighting down the former where the latter peaks.
- Work out what's wrong with the dp/p=0 measurements

Write up to Alex (?):
- Averaging over the windows vastly changes results
- V$\iff$H coupling ruins $Q_{H}^{frac}$ results at dp/p=-4e-3
- One can essentially interpret whether one wants to see linear or non-linear behaviour

# Chroma Plots

Window = 1:
![[win1.png]]
- Appears non-linear in H although this is certainly due to bad data.

Window=2:
![[win2.png]]
- Appears roughly as expected in both H and V.
- Still a bad -4e-3 point for H
- 0 point is split for V

Window=3:
![[win3.png]]
- H still roughly fine, although one can see greater splitting around 0.
- V is much worse. Splitting around 0 and -1e-3 have caused the fitting to break from the obvious linearity

# Plan

So seems like a window of 2 is best. Over larger timescales, Q may deviate too much for the FFT to make adequate use of the information
- [x] Check this visually on QC
	- [x] Check in notebook if needed
**Generally, this should not make a difference as Q should not vary much over 1-3 chunks. It's likely only an issue because of the noisiness of the data.**

Anton used a k means approach to find the Q values. 
 - [x] Find how out this works.
 **Discussed in: [[Fixing chromaticity_helpers.py]]. Improved clustering by comparing modal frequencies instead of centroid positions.**

One of the dp/p= +2e-3 points is an outlier (MD on). I think the issue may be that some chunks are reporting a very high Q and others are reporting the correct one. Using a small window fixes this.
- [x] Find out why the window makes a difference here.
- [x] Fix this.
**Not required**

Contrive some way of comparing $Q_{H}^{frac}$ and $Q_{V}^{frac}$ signals and programmatically weighting down the former where the latter peaks. Could do this buy comparing the H and V peaks in parallel and weighing each down where the other exists.
- [x] Implement 
**Not required**

Put these notes up as a quartz website (like those of Anton):
- [ ] Up on quartz
# Questions

- Is it better to calculate the chromaticity using the measured $Q_0$ or to use the $Q_0$ as implied by the fit? - use fit
- Beam/cycletime distinction in QC vs BBQ data, etc - SPS is injection/beam time (PS uses cycletime)
- What to prepare for next week? - below

# To do:

- [x] Create a few slides for the meeting on 14-01-26 ([[14-01-26 - WP4 Meeting]]) summarising:
	- [x] What we have done
	- [x] Goals we missed
	- [x] Immediate future
	- [x] Longer term
	- [x] Table of tune and chroma results (Q', Q'')

- [x] Add other MDs to this notebook
- [x] Spruce up plots and add necessary labels
- [x] Access B data to determine what magnets were playing MD1 during [[22-08-25 MD - Dipole chroma scans]]
- [x] Refactor get_peaks to work in chromaticity_helpers.py