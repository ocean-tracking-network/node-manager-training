---
title: "Detections"
teaching: 0
exercises: 0
questions:
- "What is the workflow for loading detection data?"
- "What do I need to look out for as a node manager when looking for detections?"
objectives:
- "Understand the workflow for detction data in the OTN system"
- "Learn common errors and pitfalls that come up when loading detections"
keypoints:
- "Its important to handle errors when they come up as they can have implications on detections"
- "OTN finsihes off detections tickets running Matching and sensor tag processing"
---

## Create gitlab issue

When you recieve new detection detection metadata you should create a new Gitlab Issue using the detection meta data template below.

```
- [ ] - NODE MANAGER load raw detections and events (detections-1 notebook, events-1 notebook) (put_table_names_in_ticket) 
- [ ] - NODE MANAGER verify raw detections table (detections-1 notebook)
- [ ] - NODE MANAGER load to detections_yyyy (detections-2 notebook) (put detection years that were affected here)
- [ ] - NODE MANAGER verify detections_yyyy (looking for duplicates) (detections-2 notebook)
- [ ] - NODE MANAGER load to sensor_match_yyyy (detections-2 notebook)(put sensor_match years that were affected here)
- [ ] - NODE MANAGER timedrift correction (detections-2b notebook)
- [ ] - NODE MANAGER verify timedrift corrections (detections-2b notebook)
- [ ] - NODE MANAGER check for open unverified receiver metadata (put issue number here) (manual check)
- [ ] - NODE MANAGER load to otn_detections_yyyy (detections-3 notebook)
- [ ] - NODE MANAGER verify otn_detections_yyyy (detections-3 notebook)
- [ ] - NODE MANAGER load sentinel records (detections-3 notebook)
- [ ] - NODE MANAGER check for missing receiver metadata (detections-3b notebook)
- [ ] - NODE MANAGER load download records (events-2 notebook)
- [ ] - NODE MANAGER verify download records (events-2 notebook)
- [ ] - NODE MANAGER pass issue to analyst for final steps
- [ ] - OTN check for double reporting (detections verification script)
- [ ] - OTN match tags to animals (detections-4 notebook)
- [ ] - OTN mark test/transceiver tags (detections verification script)
- [ ] - OTN do sensor tag processing (only done by OTN as it requires vendor specifications)
- [ ] - OTN update detection extract table
```

## detections - 1 - load csv detections

Detections 1 loads a raw CSV detection file into a new database table.

## Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. You will also want to insert the path of your auth file into `engine = get_engine()` so you will be able to connect to the database.

## User input

Cell two requires input from you. This information will be used to get the raw detections CSV and to be able to create a new raw table in the database.

You will need to input: 
- `file_or_folder_path`: This is the path to the you detection input file
- `table_suffix`: The  table suffix used to create in the raw tables in the form YYYY_MM
- `schema`: This database schema that you want to load detections to 
- `load_detections`: a true or false value using the table suffix you supplied
- `stacked`: this is for Fathom exports only and is a way to know how to parse them

## Verify detection file and loading into a database table

Cell three allows you to review and verify the detection file’s format. Upon successful verification, you can then run cell four which will  load the degtections  into a new raw table.

## Verify Raw Detection Table

You will now need to verify the newly loaded raw detection table. After verification if no major issues are found you are ready to move on to events - 1 - load events into c_events_yyyy.

## events - 1 - load events into c_events_yyyy

Events 1 is responsible for loading receiver events files into raw tables.

## Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. You will also want to insert the path of your auth file into `engine = get_engine()` so you will be able to connect to the database.

## User inputs 

To load the events, the notebook will require information from you about the events file and table you need to load to. 

You will need to input:
- `filepath`: This is the path to the you events csv
- `table_name`: The raw table to load the events file into 'c_events_YYYY'
- `schema`: This database schema that you want to load detections to 
- `file_encoding`: The file_encoding: ISO-8859-1 in the event export. The  default encoding used in VUE's event export

## Verifying the events file

Before attempting to load the event files to  a raw table the notebook will verify the file to make sure there are no major issues. This will be done by running the Verify events file cell. Barring no major issues you will be able to run the second last cell to load the events file.


 ## Load the events file into the c_events_yyyy table

The second last cell loads the events file into a raw table. It depends on successful verification from the last step. Upon successful loading and can dispose of the engine then move on to the next notebook.

## detections - 2 - c_table into detections_yyyy

This notebook takes the raw detection data from detections - 1 - load csv detections and places it into the next level detection_yyyy tables.

## Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. You will also want to insert the path of your auth file into `engine = get_engine()` so you will be able to connect to the database.

## User inputs 

To load the to the detection_yyyy tables the notebook will require information about the schema you are working in and the raw table that you created in detections 1.

You will need to input:
- `c_table`: The raw table that you created in detections 1 (c_detections_yyyy)
- `schema`: This database schema that you want to load detections to 


## Create missing tables

With detections you only get tables based on the years that you need. So these cells will detect any tables you are missing and create them as needed  based on the years covered in the raw detection tables (c_table). This will cover all tables such as detections_yyyy, sensor_match_yyyy and otn_detections_yyyy. 

## Create Detection Sequence

Before loading detections a detection sequence is created. The sequence is used to populate the det_key value. The det_key value is an unique ID for that detection to help ensure there are no duplicates. Duplicate detections are then checked for and will not be inserted into the detections_yyyy tables. After all this the raw detection records are ready to be loaded into the detection_yyyy tables.

## Verify Detections YYYY Tables

After the records are successfully loaded into the  detections_yyyy  you will now run the verification and fix any major issues that come up. As you may have noticed there are a lot of verification and checks in loading. It is important to keep in mind that all these verifications are being done to try and catch issues as early as possible when they are easiest to fix. OTN is alway available to help if you have any questions with verifications.

##  Load sensors_match Tables by Year

For the last part of this notebook you will need to load the sensors_match tables. This loads sensor detections into a project's sensor_match_yyyy tables. Later, these tables will aid in matching vendor specifications to resolve sensor tag values. After this you are ready to dispose of the database connection and move to detections-2b.

## detections - 2b - timedrift calculations

This notebook calculates time drift factors and applies the corrections to the detection_yyyy tables

## Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. You will also want to insert the path of your auth file into `engine = get_engine()` so you will be able to connect to the database.

## Calculating and adding the time_drift_factors

For this notebook you just need to provide the schema you are working in. After that you can run `create_tbl_time_drift_factors`. This function will create the time_drift_factors table in the schema if it doesn't exist.

The next step is to run `check_time_drifts`. Which gives a display of the time drift factor values that will be added to the time_drift_factors table given an events table.

If everything looks good `add_time_drift_factors` is ready to be run which adds new time drift factors to the time_drift_factors table from the events file.

You will then run `create_time_drift_views` which creates the time drift views used to calculate drift values for both the detections and sensor_match tables

Finally,  `update_detection_time`  is ready to be run. This function updates both the detections and sensor_match tables with corrected time values using the vw_time_drift_cor view. You will need to provide the years you want to be adjusted. 

## Verify Detections After Time Drift Calculations

After running the above cells you will then verify the time drift corrections on the detections_yyyy and sensor_match_yyyy tables. Pending no major issue coming from the verification you are ready to dispose of the engine and move on to the next notebook.


## detections - 3 - detections_yyyy into otn_detections

The detections - 3 notebook moves the detections from detection_yyyy and sensor_match_yyyy tables into the final otn_detections_yyyy tables.

## Imports and user inputs

Like in the notebooks before it you will need to run the import cells, fill in your auth string for the database, and provide some user input. The input in this case is the schema you wish to work in. Before moving on from this you will need to confirm 2 things:

1) Confirm that NO push is currently ongoing 

2) confirm rcvr_locations for this schema have been verified.

 If a push is ongoing, or if verification has not yet occured, you must wait for it to be completed before processing beyond this point.


 ## Creating detection veiws and loading in otn_detections

Once you are clear to continue loading you can run `create_detection_views`. This function as its name implies creates views for detection data. These are then used to run the function in the next cell `load_into_otn_detections_new`, which loads the detections from those views into otn_detections.

 ##  Syncing Corrected Times

The next two cells are used only if you have loaded detections through to the otn_detections_yyyy without first running the detections - 2b - timedrift calculations. You will need to provide the date of the current push and the link of the issue you are loading. You will then be able to correct the times and if  a node's detection times are updated the node's obis.detection_extract list will also be updated.

## Verify OTN Detections

After running your needed cells you will then verify otn_detection_yyyy detections. Pending no major issue coming from the verification you are ready to dispose of the engine and move on to the next notebook.


## detections - 3b - missing_metadata_check

This notebook is for checking detections that have not been inserted into otn_detections_yyyy, and will show potentially missing receiver metadata. 


The user will be able to set a threshold for the minimum number of detections to look at (default is 100). It will also separate animal detections from transceiver detections in a graph.At the end, it will show a SQL command to run so that the missing metadata can be seen in table format.

## Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. You will also want to insert the path of your auth file into `engine = get_engine()` so you will be able to connect to the database.

## User inputs


For this notebook you will need to provide: 
- `schema`: This database schema that you want to load detections to 
- `years`: A comma-separated list of detection table years for detections_yyyy, should be in form [yyyy] or [yyyy,yyyy,'early']

##  Check for Missing Metadata in Detections_yyyy

This step will perform the check for missing metadata in detections_yyyy. Based on an acceptable threshold (e.g. 100) of number of detections without metadata. You will then get a query and visualization of the missing metadata. One note with the visualization is that you will see receivers with less than this threshold but they will not be given in the query that comes up. There are also two cells at the end that allow you create  reports for researchers in CSV or HTML form.

## events - 2 - move c_events into events table

## Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. You will also want to insert the path of your auth file into `engine = get_engine()` so you will be able to connect to the database.

# User input

The second cell of this notebook is where you input the required information move events c_events tables into the events table:
- `c_events_table`: This is the path to the you detection input file
- `schema`: This database schema that you want to load detections to 

 # Verify a table format

You will then verify that the c_events events table you put in exists and then verify that it meets the required format specifications. You will also see a `datecreated` variable which you can leave as none so it uses the current date as the date created value. Pending nothing comes up in the verification you run the load cell and when it loads successfully you have finished your position of detections. You can now pass it to OTN who will finish the rest of the task list.

