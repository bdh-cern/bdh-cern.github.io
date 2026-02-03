# General Notes

- The SPS typically uses beam/injection time (not cycle time)
# Energy/Momentum Points

Idle current (ZERO): 13.5 GeV / 155A
MD1: 200 GeV
SFTPRO injection: 14 GeV 
LHC injection: 26 GeV
# Constants

| Variable                       | Symbol      | Value                 | Unit | Note |
| ------------------------------ | ----------- | --------------------- | ---- | ---- |
| Momentum compaction            | $\alpha$    | 0.001853974296        |      |      |
| Slip factor (14GeV)            | $\eta$      | 0.002614964637129285  |      |      |
| Slip factor (26GeV)            | $\eta$      | 0.0005533576515251234 |      |      |
| Standard  revolution frequency | $F_{rev,0}$ | ~43.279               | kHz  |      |
|                                |             |                       |      |      |

# Useful Variables


| Description          | Variable name                               | Notes                                                            |
| -------------------- | ------------------------------------------- | ---------------------------------------------------------------- |
| B field              | SR.BMEAS-OP-B-SD:SamplesFromTrigger:samples |                                                                  |
| Programmed I         | QD.LOG.I.REF                                | Measured I is not logged.<br>Can't actually find this on timber. |
| Revolution frequency | SA.RevFreq.ACQ-D                            |                                                                  |

# Control

- The SPS does not use B-train for magnetic feedback control, unlike the PS.
- During ramping, the SPS uses the 'radial loop' to maintain the centred beam position