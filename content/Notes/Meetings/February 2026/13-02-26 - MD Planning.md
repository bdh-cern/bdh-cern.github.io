
We want to redo [[01-12-25 MD - Cancelled Chroma Scans]] on 17th, 18th Feb.

Supercycles to play:

LHCPILOT + MD1 (200 GeV) + MEAS   
LHCPILOT + MD1 (26 GeV, flat) + MEAS
LHCPILOT + MEAS  
SFTPRO + MD1 (200 GeV) + MEAS
SFTPRO + MD1 (26 GeV, flat)  + MEAS
SFTPRO + MEAS 

Key:

| LSA name                                  | Purpose                                                              | Nickname         |
| ----------------------------------------- | -------------------------------------------------------------------- | ---------------- |
| LHC_PILOT_Q20_2025_V1                     | Standard proton cycle                                                | LHCPILOT         |
| SFT_PRO_MTE_East_Extraction_L4780_2025_V1 | Standard SFTPRO cycle                                                | SFTPRO           |
| LHC_ION_1inj_Q26_Pb82_2025_V1             | Can be used at 400GeV dynamic economy to emulate SFT-like hysteresis | LHCION2 (DynEco) |
| MD_26_L60_Q20_2022_V1_Clone_MD_to_flat    | MD1-like cycle at 26GeV (flat) and 200GeV                            | MD1              |
| SFT_PRO_MD_aperture_2025_V3               | Measurement cycle                                                    | MEAS             |

- Tuesday - implementing a few things before the chroma measurements can start
	- BST pre-beam delay (?)
	- Removing the injection bump with Francesco; the bumper moves the orbit out before the kicker kicks it into the (ring?/transfer function?)
	- Changing to new optics with new chromaticity 'knobs'
	- Arrive at 9-10am, probably starting at 11am
	- SFT-MD1-MEAS, LHC-MD1-MEAS on the weekend
	- Depowering MD1 will require tune and momentum trims
	- Will then have to trim chroma to return to with-MD1 values on without-MD1 supercycles 
- Could do some chroma measurements on the weekend in order to have a control for the before/after the optics
- Going from -4e-3 to +4e-3 dp/p (ish) with steps of 5e-4, 3-5 measurements per point
- 'Core beam'?
- Damper off?
- MD1 is 3BP
- MD cycles have been reduced to 4BP (from 6BP)
- How is chroma of the ramp effected? Can possibly measure on the initial part of the ramp
- Start from the aperture cycle that the SPS is currently using but on the cycle name SFT_PRO_MD_aperture_2025_V3

Plan: 

- On the weekend:
- Prepare SFT_PRO_MD_aperture_2025_V3, with 19-11 tag ('200GeV MD1') , verify damper is off
- Copy settings from SFT_PRO_MD_aperture_2025_V3 : Energy matching, Orbit correction, Check the tune, Rf injection phases, Stable phase offset
- Measure in two configurations:
	- LHCINDIV - MD1 - SFT_PRO_MD_aperture_2025_V3
	- SFTPRO - MD1 - SFT_PRO_MD_aperture_2025_V3
- Chroma measurement configs:
	- Aim for +- 6e-3 dp/p with step 0.5e-3 and 3 shots per point
	- Measurement along flat-bottom to beyond transition (aim for beyond 50GeV)

For next week:

- Redo one of the weekend measurements (LHCINDIV - MD1 - SFT_PRO_MD_aperture_2025_V3 or SFTPRO - MD1 - SFT_PRO_MD_aperture_2025_V3)
- Then:
	- SFTPRO - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- LHCINDIV - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- (All flat on 2,4,6,8-poles)
- Establish settings set to switch between with 200 GeV MD1/flat 26 GeV  MD1 on SFT_PRO_MD_aperture_2025_V3 to recover linear chroma in beam domain, then repeat - work out which settings need to be changed
- Repeat:
	- SFTPRO - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- LHCINDIV - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- (All flat on 2,4,6,8-poles)
- ...to make sure chromaticity has been restored.