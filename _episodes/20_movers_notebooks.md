
---
title: "Moving Platform: Mission Metadata, Telemetry and Detection Loading"
teaching: 60
exercises: 0
questions:
- "What are considered moving platforms. What are the use cases?"
- "How do I load moving platform metadata, telemetry data, and detections into the Database?"
---
objectives:
- "Understand the workflow for moving platform workflow in the OTN system"
- "Learn how to use the `Movers` notebooks"
---
keypoints:
- TODO: a list of technologies are supported by the Moving Platform workflow such as Liquid Robotics Wave glider, Teledyne Webb Research Slocum glider, short deployments (hours) down a line of traps, etc. https://oceantrackingnetwork.org/gliders/
- TODO: "OTN finishes off detection issues by running matching and sensor tag processing"
---

`mission metadata`, `telemetry data` and `detection data` should be submitted prior to the Moving platform data loading process. 
Here is the Issue checklist in the OTN Gitlab `Moving Platforms` template, for reference:

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

# Loading Mission Metadata

Moving platform missing metadata should be reported to the Node in the template provided [here](https://members.oceantrack.org/data/data-collection). 
This spreadsheet file will contain one or more missions (rows) of the moving platform: identifiers, instruments used, and deployment/recovery times.

1. Visually check for any missing information and inconsistant or formatting issues in the **essential** columns? Column names and example data are shown as below:
 * platform_id: e.g. `1234567`
 * otn_mission_id: e.g. `1234567202310031456` (Note: otn_mission_id is an internal unique identifier which can be constructed as `platform_id + deploy_date_time digits`).
 * ins_model_no: e.g. `VMT`
 * ins_serial_no: e.g. `130000`
 * deploy_date_time: e.g. `2023-10-03T14:56:00`
 * recover_date_time: e.g. `2023-12-03T12:00:00`



   
2. Run through the `movers - 1 - Load Mission Metadata` notebook to load the spreadsheet into the `mission_table`:

### User Input
Cell three requires input from you. This information will be used to get the raw detections CSV and to be able to create a new raw table in the database.

1. `schema`:  'collectioncode'
    * please edit to include the relevant project code, in lowercase, between the quotes.
      
1. `table_suffix`: e.g. `2024_03` - should be the same as in the `movers - 1 - Load Mission Metadata` notebook.
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar, to indicate the most-recently downloaded instrument.
     
1. `mission_file`: '/path/to/mission_file'
    * paste a filepath to the relevant XLSX file. The filepath will be added between the provided quotation marks.


![image](https://github.com/ocean-tracking-network/node-manager-training/assets/68606079/da7c6919-e1c8-4016-bfb5-06a11840f4e7)


3. Check off the step and record the `mission_table` name in the Gitlab ticket.

`- [ ] - NAME load raw metadata file (movers-1 notebook)**(:fish: table name: c_moving_platform_missions_yyyy)**`

# Loading Telemetry Data

1. Visually check for any missing information and inconsistant or formatting issues in the **essential** columns? Column names and example data are shown as below:
 * date_time_utc: e.g. `2023-12-13T13:10:12`
 * lat: e.g. `28.33517`
 * lon: e.g. `-80.33734833`.
 * mission_id: e.g. `1234567202310031456` (Note: the value should match the `mission_table`.`otn_mission_id` in the **Loading Mission Metadata** step)
 * platform_id: e.g. `1234567` (Note: the value should match the `mission_table`.`platform_id` in the **Loading Mission Metadata** step)


2. Run the `movers - 2 - Load telemetry` notebook: `verify_telemetry_file` and `load_csv` cells to load the telemetry data (.csv) file into the `raw_telemetry` table, `telemetry` table and joined with `mission_table` as the `moving_platform_mission_telemetry` table:
 * table_suffix: e.g. `2024_03` (should be the same as in the `movers - 1 - Load Mission Metadata` notebook)

### User Input
Cell three requires input from you. This information will be used to get the raw detections CSV and to be able to create a new raw table in the database.

1. `table_suffix`: e.g. `2024_03` - should be the same as in the `movers - 1 - Load Mission Metadata` notebook.
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar.
     
1. `schema`:  'collectioncode'
    * please edit to include the relevant project code, in lowercase, between the quotes.

1. `telemetry_file`: '/path/to/telem_file'
    * paste a filepath to the relevant CSV file. The filepath will be added between the provided quotation marks.

![image](https://github.com/ocean-tracking-network/node-manager-training/assets/68606079/4bd40123-23d1-4816-9c44-a64f391b93de)


3. Check off the step and record the `c_moving_platform_telemetry` name in the Gitlab ticket.

`- [ ] - NAME load raw telemetry files (movers-2 notebook) **(:fish: table name: c_moving_platform_telemetry_yyyy**)`


4. Run the `movers - 2 - Load telemetry` notebook: `create_telemetry_table` and `verify_telemetry_table` cells to create the telemtry table for joining to missions:

5. Check off the step and record the `moving_platform_telemetry` name in the Gitlab ticket.

`- [ ] - NAME create telemetry table from raw table (movers-2 notebook) **(:fish: table name: moving_platform_telemetry_yyyy**)`


6. Run the `movers - 2 - Load telemetry` notebook: `verify_missions_table`, `create_joined_table`, and `verify_joined_table` cells to create the mission and telemetry joined table:

7. Check off the step and record the `moving_platform_mission_telemetry` name in the Gitlab ticket.

`- [ ] - NAME combine mission metadata with telemetry (movers-2 notebook) **(:fish: table name: moving_platform_mission_telemetry_yyyy)**`


# Loading Raw Detections and Events


1. Load raw detections via `detections - 1 - load csv detections` notebook: check off the steps and record the `c_detections` name in the Gitlab ticket.

`- [ ] - NAME load to raw detections (detections-1 notebook) **(:fish: table name: c_detections_yyyy)**`

`- [ ] - NAME verify raw detections table (detections-1 notebook)`

2. Load raw events by the `events - 1 - load events into c_events_yyyy` notebook: check off the step and record the `c_events` name in the Gitlab ticket.

`- [ ] - NAME load raw events (`events-1` notebook) **(:fish: table name: c_events_yyyy )**`

3. Run the `events - 2 - move c_events into events table` notebook to promote the raw events into to the `events` table.
   
`- [ ] - NAME load raw events to events table (events-2 notebook)`

# Loading Detections for Moving Platforms

- With the telemetry and mission table, we can now upload the raw detections and promote them to the detections_yyyy_movers tables. 
- This notebook has the functionalities of `detections - 2 - c_table into detections_yyyy` and `detections - 2b - timedrift calculations` notebooks. The difference is it handles `_movers` tables. 
1. Run `movers - 3 - Load Detections` notebook till `Load raw dets into detections_yyyy_movers` cell to populate `detections_yyyy_movers` tables and load raw detections into them.

### User Input
Cell three requires input from you. This information will be used to get the raw detections CSV and to be able to create a new raw table in the database.

1. `table_suffix`: e.g. `2024_03` - should be the same as in the `movers - 1 - Load Mission Metadata` notebook.
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar.
     
1. `schema`:  'collectioncode'
    * please edit to include the relevant project code, in lowercase, between the quotes.

![image](https://github.com/ocean-tracking-network/node-manager-training/assets/68606079/9e5f8bc8-d0f6-4ab8-91fa-8d932a3ca78d)

2. Check off the step and record affected years (which detections_yyyy_movers tables were updated) in the Gitlab ticket.

`- [ ] - NAME load to detections_yyyy_movers (`movers-2` notebook) **(:fish: put affected years here)**`

- TODO: add troubleshooting tips here: raw detections were note promoted into detections_yyyy_movers.
  
3. Run the next six cells to load timedrift factors (into time_drift_factors), apply time adjustment to detections_yyyy_movers and verify the timedrift corrections. Check off the steps in the Gitlab ticket.
   
`- [ ] - NAME timedrift correction for affected detection (`movers-3` notebook)`

`- [ ] - NAME verify timedrift corrections (movers-3 notebook)`

4. Run the next two cells to verify the detections_yyyy_movers tables. Check off the step in the Gitlab ticket.

`- [ ] - NAME verify detections_yyyy_movers (looking for duplicates) (movers-3 notebook)`

5. Run the last cell to create and load sensor match tables for movers. Check off the step and record affected years in the Gitlab ticket.

`- [ ] - NAME load to sensor match (`movers-3` notebook) **(:fish: put affected years here)**`

# Loading OTN Detections

### User Input
Cell three requires input from you. This information will be used to get the raw detections CSV and to be able to create a new raw table in the database.

1. `table_suffix`: e.g. `2024_03` - should be the same as in the `movers - 1 - Load Mission Metadata` notebook.
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar.
     
1. `schema`:  'collectioncode'
    * Please edit to include the relevant project code, in lowercase, between the quotes.

1. `years`:  e.g. `[2022, 2023]`
	  * Enter the affected years from `movers - 3 - Load Detections`

![image](https://github.com/ocean-tracking-network/node-manager-training/assets/68606079/ca5360c7-b9fd-44a9-9c4f-84d5f194f63f)


1. Run the `create_moving_platforms_full_telemetry` cell to load to formatted telemetry table. Check off the step and record the affected years in the Gitlab ticket.
   
`- [ ] - NAME load formatted telemetry tables (movers-4 notebook) **(:fish: put affected years here)**`


2. Run the `create_reduced_telemetry_tables` cell to reduced telemetry tables. Check off the step and record the affected years in the Gitlab ticket.
   
`- [ ] - NAME load reduced telemetry tables (movers-4 notebook) **(:fish: put affected years here)**`


3. Run the `create_platform_as_receiver_tables` cell to load glider as receiver tables. Check off the step and record the affected years in the Gitlab ticket.
   
`- [ ] - NAME load glider as receiver tables (movers-4 notebook) **(:fish: put affected years here)**`

4. Run the `create_detections_view` and `load_view_into_otn_dets` cells to load view detections into otn_detections_yyyy tables. Check off the step and record the affected years in the Gitlab ticket.

`- [ ] - NAME load into vw_detections_yyyy_movers (`movers-4` notebook) **(:fish: put affected years here)**`

`- [ ] - NAME load view detections into otn_detections_yyyy (movers-4 notebook) **(:fish: put affected years here)**`

5. Run the `verify_otn_detections` cell to verify the `otn_detections_yyyy` tables. Check off the step in the Gitlab ticket.

`- [ ] - NAME verify otn_detections_yyyy (movers-4 notebook)`

6. Run the `load_platforms_to_moorings` cell to verify the `moorings` tables. Check off the step in the Gitlab ticket.

`- [ ] - NAME create mission and receiver records in moorings (movers-4 notebook)`

# Creating Download Records and Processing Receiver Configuration

1. Create and verify download records via `events - 3 - create download records` notebook: check off the steps in the Gitlab ticket.


`- [ ] - NAME load download records (events-3 notebook)`

`- [ ] - NAME verify download records (events-3 notebook)`

2. Run through the `events - 4 - process receiver configuration` notebook to process receiver configuration: check off the step in the Gitlab ticket.
   
`- [ ] - NAME process receiver configuration (events-4 notebook)`

# Final Steps

The remaining steps in the GitLab Checklist are completed outside the notebooks.

First: you should access the Repository folder in your browser and ensure the raw detections are posted in the `Data and Metadata` folder.

Finally, the Issue can be passed off to an OTN-analyst for final verification in the database.
