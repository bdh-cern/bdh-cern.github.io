
| Date       | 1st December 2025 |
| ---------- | ----------------- |
| Start time | 15:00 + 02:00     |
| End time   | 17:30 + 02:00     |
| User       | -/-               |
| LSA cycle  | -/-               |
| Purpose    | Chroma analysis   |

The idea of this MD was to explore the chroma changes brought about by removing MD1 in a couple difference scenarios. However, due to septum and kicker issues in the PSB, there were no protons available and the MD was cancelled.

Logbook entry: https://logbook.cern.ch/elogbook-server/GET/showEventInLogbook/4466049

# Plan:

## Cycles:

| LSA name                               | Purpose                                                            | Nickname         |
| -------------------------------------- | ------------------------------------------------------------------ | ---------------- |
| LHC_PILOT_Q20_2025_V1                  | Standard proton cycle                                              | LHCPILOT         |
| LHC_ION_1inj_Q26_Pb82_2025_V1          | Ion cycle at 400GeV dynamic economy to emulate SFT-like hysteresis | LHCION2 (DynEco) |
| MD_26_L60_Q20_2022_V1_Clone_MD_to_flat | MD1-like cycle at 26GeV (flat) and 200GeV                          | MD1              |
| SFT_PRO_MD_aperture_2025_V3            | measurement cycle                                                  | MEAS             |
|                                        |                                                                    |                  |
## Supercycles 

(Ranked by priority):

1. LHCPILOT + MD1 (26 GeV, flat) + MEAS   
2. LHCPILOT + MEAS  
3. LHCION2 (DynEco) + MD1 (200 GeV) + MEAS  
4. LHCION2 (DynEco) + MD1 (26 GeV, flat)  + MEAS      
5. LHCION2 (DynEco) + MEAS  
6. LHCPILOT + MD1 (200 GeV) + MEAS (already have data but good for reference)

The dynamic economy is meant to replicate SFTPRO hysteresis, so this is equivalent to: 

1. LHCPILOT + MD1 (26 GeV, flat) + MEAS   
2. LHCPILOT + MEAS  
3. SFTPRO + MD1 (200 GeV) + MEAS  
4. SFTPRO + MD1 (26 GeV, flat)  + MEAS      
5. SFTPRO + MEAS  
6. LHCPILOT + MD1 (200 GeV) + MEAS (already have data but good for reference)

# Download

- **LHC_ION_1inj_Q26_Pb82_2025_V1** - used most recent trim, dated 20-11-2025. This doesn't account for the DynEco
- **LHC_PILOT_Q20_2025_V1** - used most recent trim, dated 29-08-2025
- **MD_26_L60_Q20_2022_V1_Clone_MD_to_flat** - used the appropriate tags
- **SFT_PRO_MD_aperture_2025_V3** - used most recent trim, dated 27-11-2025