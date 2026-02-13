
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