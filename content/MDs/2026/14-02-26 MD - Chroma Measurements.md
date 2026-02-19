
Measuring two configurations:

LHCINDIV - 200 GeV MD1 - MD_14GeV_CHROMA_2026_V1
SFTPRO - 200 GeV MD1 - MD_14GeV_CHROMA_2026_V1

Tried to accelerate beyond transition and analyse chroma over the whole thing.

# AutoQ run1 (SFTPRO):

start: 2026-02-15 05:08:19
end: 2026-02-15 05:35:01

f0_start_index = 4
f0_stop_index = 8

## For flat-bottom:

measurement_start_index = 200
measurement_stop_index = 600 
## For ramp:

measurement_start_index = 650
measurement_stop_index = 800 

## Comments

The beam position was not zeroed for this measurement (orbit offset before kick was ~-1mm). This means there isn't a good zero-point to use as reference for dp/p=0). Also, the beams during the lower dpps seem to have deteriorated. It will be hard to use this data.

![[Pasted image 20260216173639.png]]

![[Pasted image 20260216173941.png]]

Seems to hold up fairly well maybe -4e-3 dpp? Could salvage.

Could we somehow work out the dp/p corresponding to a 1mm offset from r=0 and add this to the reported dp/ps?

Need to override the f0 calculation with the approximate f0 expected of the SPS since it can't be adequately captured from the measurements.
# AutoQ run2 (LHCINDIV and SFTPRO?):

Looking at the cycles played in timber shows 792s of LHCINDIV and 86.4s if SFTPRO

start: 2026-02-15 05:38:03
end: 2026-02-15 06:35:30

f0_start_index = 4
f0_stop_index = 8

## For flat-bottom

measurement_start_index =
measurement_stop_index = 

## For ramp:

# AutoQ run3 (LHCINDIV):

start: 2026-02-15 06:06:35
end: 2026-02-15 06:35:30

f0_start_index = 4
f0_stop_index = 8

## For flat-bottom:

measurement_start_index =
measurement_stop_index = 

## For ramp:


# AutoQ run4 (Mix, LHCINDIV):

Looking at B-train shows MD1-MEAS-LHCINDIV

Seems to play this until 06:56:27, then zeros and SFTPRO are played as well and MEAS disappears.

start: 2026-02-15 06:35:30
end: 2026-02-15 07:12:03

Likely not to use as the 06:35 - 06:56 looks like: 

![[Pasted image 20260216114424.png]]

# AutoQ run5 (Mix):

Looking at B-train:
MD1-SFTPRO-ZERO-LHCINDIV-MD1-SFTPRO

No MD_14GeV_CHROMA_2026_V1 in this one, so likely irrelevant.

start: 2026-02-15 07:12:03
end: 2026-02-15 07:44:03

f0_start_index = 4
f0_stop_index = 8

## For flat-bottom:

measurement_start_index =
measurement_stop_index = 

## For ramp:



