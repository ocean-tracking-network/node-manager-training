
---
title: "Moving Platform: Mission Metadata, Telemetry and Detection Loading"
teaching: 60
exercises: 0
questions:
- "What are considered of moving platforms. What are the use cases?"
- "How do I load moving platform missing metadata, telemetry data, and detections into the Database?"
---
objectives:
- "Understand the workflow for moving platform workflow in the OTN system"
- "Learn how to use the `Movers` notebooks"
---
keypoints:
- TODO: a list of technologies are supported by the Moving Platform workflow such as Liquid Robotics Wave glider, Teledyne Webb Research Slocum glider, short deployments (hours) down a line of traps, etc. https://oceantrackingnetwork.org/gliders/
- TODO "OTN finishes off detections Issues by running Matching and sensor tag processing"
---

`mssion metadata`, `telemetry data` and `` has been processed for a project, the related detections may now be processed. Detection data should be reported to the Node as a collection of raw, **unedited** files. These can be in the form of a zipped folder of `.VRLs`, a database from Thelma Biotel or any other raw data product from any manufacturer. The files contain only transmitter numbers and the datetimes at which they were recorded at a specific receiver. The `tag metadata` and `deployment metadata` will provide the associated geographic and biological context to this data.
Here is the Issue checklist, for reference:

~~~
Moving platform
- [ ] - NAME load raw metadata file (`movers-1` notebook)**(:fish: table name: c_moving_platform_missions_yyyy)**
- [ ] - NAME load raw telemetry files (`movers-2` notebook) **(:fish: table name: c_moving_platform_telemetry_yyyy**)
- [ ] - NAME create telemetry table from raw table (`movers-2` notebook) **(:fish: table name: moving_platform_telemetry_yyyy**)
- [ ] - NAME combine mission metadata with telemetry (`movers-2` notebook) **(:fish: table name: moving_platform_mission_telemetry_yyyy)**
- [ ] - NAME load to raw detections (`detections-1` notebook) **(:fish: table name: c_detections_yyyy)**
- [ ] - NAME verify raw detections table (`detections-1` notebook)
- [ ] - NAME load raw events (`events-1` notebook) **(:fish: table name: c_events_yyyy )**
- [ ] - NAME load raw events to events table (`events-2` notebook)
- [ ] - NAME load to detections_yyyy_movers (`movers-2` notebook) **(:fish: put affected years here)**
- [ ] - NAME delete self detections (`movers-3` notebook)
- [ ] - NAME timedrift correction for affected detection (`movers-3` notebook)
- [ ] - NAME verify timedrift corrections (`movers-3` notebook)
- [ ] - NAME verify detections_yyyy_movers (looking for duplicates) (`movers-3` notebook)
- [ ] - NAME load to sensor match (`movers-3` notebook) **(:fish: put affected years here)**
- [ ] - NAME load formatted telemetry tables (`movers-4` notebook) **(:fish: put affected years here)**
- [ ] - NAME load reduced telemetry tables (`movers-4` notebook) **(:fish: put affected years here)**
- [ ] - NAME load glider as receiver tables (`movers-4` notebook) **(:fish: put affected years here)**
- [ ] - NAME load into vw_detections_yyyy_movers (`movers-4` notebook) **(:fish: put affected years here)**
- [ ] - NAME load view detections into otn_detections_yyyy (`movers-4` notebook) **(:fish: put affected years here)**
- [ ] - NAME verify otn_detections_yyyy (`movers-4` notebook)
- [ ] - NAME create mission and receiver records in moorings (`movers-4` notebook)
- [ ] - NAME load download records (`events-3` notebook)
- [ ] - NAME verify download records (`events-3` notebook)
- [ ] - NAME process receiver configuration (`events-4` notebook)
- [ ] - NAME label issue with *'Verify'*
- [ ] - NAME pass issue to analyst for final steps
- [ ] - NAME match tags to animals (`detections-4` notebook)
- [ ] - NAME update detection extract table

metadata: **(put metadata plone link here)**

data: **(put data plone link here)**

telemetry: **(put telemetry plone link here)**

~~~

# Load Mission Metadata

Moving platform missing metadata should be reported to the Node in the template provided [here](https://members.oceantrack.org/data/data-collection). 
This file will contain information about the deployment of any instruments used

### Visual Inspection

Once the completed file is received from a researcher, the Data Manager should first complete a visual check for formatting and accuracy.

In general, the deployment metadata contains information on the instrument, the deployment location, and the deployment/recovery times.

Things to visually check in the metadata:

1. Is there any information missing from the **essential** columns? These are:
	* otn_array
	* station_no
	* deploy_date
	* deploy_lat
	* deploy_long
	* ins_model_no
	* ins_serial_no
	* recovered
	* recover_date
 * 
