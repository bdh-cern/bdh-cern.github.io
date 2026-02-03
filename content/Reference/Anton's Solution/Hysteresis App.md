
- Project repo: https://gitlab.cern.ch/dsb/applications/sps-app-hysteresis

To run:

```
# Run for main dipole magnets
app-hysteresis -d MBI --logdir /tmp/logs
# Run for focusing quadrupoles
app-hysteresis -d QF --logdir /tmp/logs
# Run for defocusing quadrupoles
app-hysteresis -d QD --logdir /tmp/logs
```

![[Pasted image 20260129154424.png]]

- Checkpoint TFTMBI_50 (?)
- TFLSTM-47 operational
- Clear reference after each model change
- Reference is the reference B which is from the predictor
	- Could be from the B-train, but has drift
	- Could be from programmed B, but there will be a systematic difference with actual
	- Reference B is reset automatically when B is trimmed by an operator

Checkpoints:
- TFLSTM-47 is compatible (transformer LSTM)
- TFTMBI-50-v0.13 is newer architecture and seems to work (TFT)
- TFLSTM-18 for when MD1 is off (transformer LSTM)
- MLP utility in sps-mlp-hysteresis-compensation (cli.py) 
- NFS - TN file storage

Panels:
- Lower panel shows live data from SPS
- Upper panel shows difference from reference
- Right panel is purely display options

Trims window
- Gain: coefficient on the B correction
- Trim T min, trim T max: time minimum and maximum cycle time
	- trim start 4460 for flat top
	- trim end is already flattop end (9240)
- LSA Server: next - this means that the trim is being applied on the LSA test server
	- --lsa-server sps to switch to the actual SPS trimming

History Window
- Shows info, nothing operational

Feb Plan

- CLI args --lsa-server sps
- Use TFLSTM-18 when MD1 is off
- Gain to low 0.9, then raise (?)
- Trim time start to 4460 for flattop of SFTPRO1
- Tools-> prediction mode-> hysteresis only
	- Eddy prediction should also work, hypothetically. Probably not very relevant though.
- Autoregressive on if no other choice
	- i.e. if B-train is not performing well
	- 'Reset state' grounds autoregressive