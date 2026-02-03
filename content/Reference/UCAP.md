UCAP paper: https://cds.cern.ch/record/2809575/files/document.pdf
Quickstart confluence page: https://confluence.cern.ch/spaces/UCAP/pages/413106984/Quick+Start+Guide
Talk on standards https://indico.cern.ch/event/1640923/contributions/6902719/attachments/3209679/5716661/OP%20guidelines%20for%20UCAP%20development.pdf

![[Pasted image 20260116125007.png]]

![[Pasted image 20260120143245.png]]

![[Pasted image 20260120143644.png]]

Users define virtual UCAP 'devices' which take in data, 'transform' it, then output it.

The actual python code which performs the data transformation is called the converter.  

Multiple devices reside on each UCAP 'node', which is essentially the actual physical hardware. The basic structure of one 'UCAP node' is:

1. Acquisition of data
2. Transformation (running the logic on the devices)
3. Publishing this data 

Packages etc. need to be installed to nodes if one wants to use those packages in the device's convertors (i.e. transformations)

# Structure
## Acquisition

The acquisition works by creating 'events' which log the raw data:

![[Pasted image 20260116125452.png]]

- These subscribe to data in the device_name/parameter format (from the 'control system' (CMW))
- timeoutMs defines how long the node should wait for the data, starting from the first subscription being received
	- E.g. if MAGNET_1/Acq publishes something with a new cyclestamp, the acquisition layer will then wait 1000ms for anything from MAGNET_2/Acq before handing the data to the transformation layer.

## Transformation

One defines a `convert` function which acts on the event created by the acquisition layer:

![[Pasted image 20260116125944.png]]

- Transformation of data done in Java or Python (with C/C++ support)

## Publishing

- The results from the transformation layer can then be published to NXCALS or by custom clients.
- Outputs represented as RDA3(?) virtual device properties.
- 

# Actually using it

- ucap-cli: command line tool, seems to be the main UCAP interface, can create/update/delete nodes and interact with 'devices'
- aacp-py app riun ucap-console --expert