
This is a re-do of [[01-12-25 MD - Cancelled Chroma Scans]]. The plan was dicussed in [[13-02-26 - MD Planning]].

- Good trim with nice flat orbit saved as LHC+MD1
- Logbook: https://logbook.cern.ch/elogbook-server/#/logbook?logbookId=3121&dateFrom=2026-02-17T00%3A00%3A00&dateTo=2026-02-18T00%3A00%3A00&eventToHighlight=4466049
- MD1 flat on dipoles, quads, octupoles, but small degauss playing on sextupoles
- Time interval on NavPy: 0.023255814ns -> Downsampled acquisition is 5.95ms
# LHC+MD1+MD5 measurement no.1

- Started 15:40:47
- coeffs_H = -6.31411836e+04, 5.98474933e+02, -1.02618952e+00, 2.66203951e+01
-   coeffs_V = 26017.892712477467, 94.44696821331691, -2.4655244171882305, 26.580125709718622
- Log:   **1) 15:40:47 - 16:21:48:** with suboptimal acquisition settings (2K turns, with 10 ms interval); no excitation; HANN; but final analysis still looks decent. Chroma settings **0.655 (QPH) / -0.52 (QPV)**.


![[Pasted image 20260217162406.png]]
![[Pasted image 20260217162506.png]]



# LHC+MD1+MD5 measurement no.2

- Start 16:52:00 - end 17:33:04
- Chroma settings **0.655 (QPH) / -0.644 (QPV)**
-  Log: **2)** Repeat measurement 1), but with optimised acq settings (2K turns, with 23 ms interval); no excitation, RECT; and with a QPV trim to match that of SFTPRO1. Chroma settings **0.655 (QPH) / -0.644 (QPV)**
- New chroma value was made to match the injection of SFTPRO
![[Pasted image 20260217175144.png]]

![[Pasted image 20260217175203.png]]

# SFTPRO+MD1+MD5 measurement no.1

- Start 18:03:25 - end  18:44:46
- Full SC is SFT + MD1 + Meas Cycle + LHCPILOT + MD1

H coefficients: -6.44836892e+04  5.78308922e+02 -1.24162142e+00  2.66115947e+01
V coefficients:  3.38753232e+04  7.85797303e+01 -5.32878133e+00  2.65730411e+01

![[Pasted image 20260218100456.png]]

![[Pasted image 20260218100531.png]]
# LHCINDIV + MD1 + MD5 no. 3

- Switched on the 50Hz correction
- Start 18:50:12 - End: 19:31:12
-
H -5.46919961e+04  5.42048126e+02 -1.54119482e+00  2.66199541e+01
V  2.71283309e+04  9.47367808e+01 -5.16331778e+00  2.65805803e+01

![[Pasted image 20260219103526.png]]

![[Pasted image 20260219104620.png]]

# Plan sent to group:  

## Summary:

1. Weekend: take measurements with 200 GeV MD1
2. Tuesday: redo one of the weekend measurements to make sure the optics changes haven't greatly effected results 
3. Take measurements 26 GeV flat MD1
4. Work out the settings we need to restore the chroma back to what it was while we had 200 GeV MD1
5. Redo measurements with flat 26 GeV MD1 and new settings 
## Relevant cycles:
- SFT_PRO_MD_aperture_2025_V3 (measurement cycle)
- LHC_INDIV_1inj_Q20_2026_V1 (LHCINDIV)
- SFT_PRO_MTE_East_extraction_L4780_2026_V1 (SFTPRO)
- MD_26_L60_Q20_2022_V1 (200 GeV MD1)
- MD_26_L1685_Q20_2026_V1 (flat 26 GeV MD1)
## Measurement procedure:
- General recipe: SFTPRO or LHCINDIV -> 26 or 200 GeV MD1 -> SFT_PRO_MD_aperture_2025_V3
- We will perform measurements on SFT_PRO_MD_aperture_2025_V3. This cycle will have to be re-prepared for each set of measurements so that beam losses don't interfere with taking the chroma. We will need to make a tag for each version so we can track what has changed.
- Measure in range -6e-3 to +6e-3 dp/p
- Step of 0.5e-3
- 3 shots per point
- Measure along flat-bottom and as far as possible into ramp (aim for beyond transition; beyond 50 GeV)
## Weekend measurements:
- Load SFT_PRO_MD_aperture_2025_V3 with 19th Nov tag ('with 200 GeV MD1')
- Verify that the damper is off
- Copy relevant settings from ​present aperture cycle:  energy matching, orbit correction, check the tune, rf injection phases, stable phase offset (etc)
- Save as tag named 'with 200 GeV MD1 - Feb MD'
- Measure in two configurations:
	- LHCINDIV - 200 GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- SFTPRO - 200 GeV MD1 - SFT_PRO_MD_aperture_2025_V3
## Tuesday/Wednesday measurements:
- Redo one of the weekend measurements from above
- Verify that we get comparable results (so we can check that the optics change hasn't effected us too much)
- Prepare SFT_PRO_MD_aperture_2025_V3 to minimise beam losses after flat 26 GeV MD1 - store in tag named 'after flat 26 GeV'
- Measure in two configurations:
	- SFTPRO - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- LHCINDIV - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
- While playing flat 26 GeV MD1, restore the chroma to match that of the 200 GeV measurements. Formulate a group of settings adjustments which will allow us to switch between 26 GeV and 200 GeV MD1 at will. 
- Prepare SFT_PRO_MD_aperture_2025_V3 to minimise beam losses after flat 26 GeV MD1 and new settings - store in tag named 'after flat 26 GeV + new settings'
- Using these settings, repeat:
	- SFTPRO - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
	- LHCINDIV - flat 26GeV MD1 - SFT_PRO_MD_aperture_2025_V3
- Verify that the chromaticity with flat 26 GeV MD1 and new settings matches that measured whilst using the 200 GeV MD1 