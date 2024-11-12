---
title: "Moving Platform: Mission Metadata, Telemetry and Detection Loading"
teaching: 150
exercises: 0
questions:
- "What are considered moving platforms. What are the use cases?"
- "How do I load moving platform metadata, telemetry data, and detections into the Database?"
objectives:
- "Understand the workflow for moving platform workflow in the OTN system"
- "Learn how to use the `Movers` notebooks"
- "Known issues and shooting tips"
keypoints:
- "OTN supports processing of slocum and wave glider detections, detections from other mobile platforms (ship-board receivers, animal-mounted receivers, etc.), and active tracking (reference https://oceantrackingnetwork.org/gliders/)."
- "OTN is able to match detections collected by moving platforms as long as geolocation data is provided."
- "`mission metadata`, `telemetry data` and `detection data` should be submitted prior to the Moving platform data loading process."
---

Here is the issue checklist in the OTN Gitlab `Moving Platforms` template, for reference:

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

metadata: **(put metadata repository link here)**

data: **(put data repository link here)**

telemetry: **(put telemetry repository link here)**

~~~

# Loading Mission Metadata

Moving platform missing metadata should be reported to the Node in the template provided here: [Moving Platforms Metadata](https://members.oceantrack.org/data/data-collection). 
This spreadsheet file will contain one or more missions (rows) of the moving platform: identifiers, instruments used, and deployment/recovery times.

1. Quality control the `MOVING PLATFORMS METADATA` spreadsheet. If any modification save revised version as `_QCed.xlsx`
   
1.1 Visually check for any missing information and inconsistant or formatting issues in the **essential** columns (in dark-green backgroup color)? Column names and example data are shown as below:
 * PLATFORM_ID: e.g. `OTN-GL-1` (recommand in uppercase alphanumerics).
 * OTN_MISSION_ID: e.g. `OTN-GL-1-20231003T1456` (Note: otn_mission_id is an iternal unique identifier which can be constructed as `platform_id + deploy_date_time`).
 * INS_MODEL_NO: e.g. `VMT`
 * INS_SERIAL_NO: e.g. `130000`
 * DEPLOY_DATE_TIME: e.g. `2023-10-03T14:56:00`
 * DEPLOY_LAT: e.g. `16.7428`
 * DEPLOY_LONG: e.g. `-24.7889`
 * RECOVER_DATE_TIME: e.g. `2023-12-03T12:00:00`
 * RECOVERED: (y/n/l)
 * RECOVER_LAT:  e.g. `16.9251`
 * RECOVER_LONG: e.g. `-25.4713`
 * DATA_DOWNLOADED: (y/n)
 * DOWNLOAD_DATE_TIME: e.g. `2024-06-11T00:00:00`
 * FILENAME: e.g. `VMT_130000_20240616_133100.vrl` (Note: prefer original downloads).

1.2 Optional but nice to have columns:  
* TRANSMITTER and TRANSMIT_MODEL to reduce self-detections.

   
2. Run through the [`movers - 1 - Load Mission Metadata` notebook] (http://localhost:8888/notebooks/movers%20-%201%20-%20Load%20Mission%20Metadata.ipynb) to load the spreadsheet into the `mission_table`:



### User Input
Cell three requires input from you. This information will be used to get the raw mission CSV and to be able to create a new raw mission table in the database.

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

1. Visually check if any missing information, inconsistant or formatting issues in the four **essential** columns? Column names and example data are shown as below:
 * Timestamp: e.g. `2023-12-13T13:10:12` (Note: the column name maybe different)
 * lat: e.g. `28.33517` (Note: the column name maybe different)
 * lon: e.g. `-80.33734833` (Note: the column name maybe different)
 * vehicleName: e.g. `1234567202310031456` (Note: the column name maybe different.Ensure the values match the `mission_table`.`platform_id` in the **Loading Mission Metadata** step)
 * otn_mission_id: e.g. `1234567202310031456` (Note: this column needs to be added in a spreadsheet application. And populate the values to match the values in the `mission_table`.`otn_mission_id` in the **Loading Mission Metadata** step)


2. Launch [`movers - 2 - Load telemetry` notebook] (http://localhost:8888/notebooks/movers%20-%202%20-%20Load%20telemetry.ipynb) and fill in
   
### User Input
Cell three requires input from you. This information will be used to get the telemetry CSV and to be able to create a new raw telemetry table in the database.

1. `table_suffix`: e.g. `2024_03` 
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar.

1. `schema`:  'collectioncode'
    * please edit to include the relevant project code, in lowercase, between the quotes.

1. `telemetry_file`: '/path/to/telem_file'
    * paste a filepath to the relevant CSV file. The filepath will be added between the provided quotation marks.

![image](https://github.com/ocean-tracking-network/node-manager-training/assets/68606079/4bd40123-23d1-4816-9c44-a64f391b93de)

3. Run the `Prepare the telemetry file to be upload` cell to map the spreadsheet comlumns to Database columns.
![image](https://github.com/ocean-tracking-network/node-manager-training/assets/68606079/d03c04da-194c-4d8e-9808-b7d7c7afc687)

   
4. Run the `verify_telemetry_file` and `load_csv` cells to load the telemetry data (.csv) file into the `raw_telemetry` table, `telemetry` table and joined with `mission_table` as the `moving_platform_mission_telemetry` table:
 

5. Check off the step and record the `c_moving_platform_telemetry` name in the Gitlab ticket.

`- [ ] - NAME load raw telemetry files (movers-2 notebook) **(:fish: table name: c_moving_platform_telemetry_yyyy**)`


6. Run the `movers - 2 - Load telemetry` notebook: `create_telemetry_table` and `verify_telemetry_table` cells to create the telemtry table for joining to missions:

7. Check off the step and record the `moving_platform_telemetry` name in the Gitlab ticket.

`- [ ] - NAME create telemetry table from raw table (movers-2 notebook) **(:fish: table name: moving_platform_telemetry_yyyy**)`


8. Run the `movers - 2 - Load telemetry` notebook: `verify_missions_table`, `create_joined_table`, and `verify_joined_table` cells to create the mission and telemetry joined table:

9. Check off the step and record the `moving_platform_mission_telemetry` name in the Gitlab ticket.

`- [ ] - NAME combine mission metadata with telemetry (movers-2 notebook) **(:fish: table name: moving_platform_mission_telemetry_yyyy)**`


# Loading Raw Detections and Events

These detailed steps and explanations are the same as https://github.com/ocean-tracking-network/node-manager-training/blob/gh-pages/_episodes/08_Detections.md `Convert to CSV` section, `detections - 1 - load csv detections` section, `events - 1 - load events into c_events_yyyy` section and `events - 2 - move c_events into events table` section. Please use the above Detection Loading process as reference.

- The related detections may now be processed. Detection data should be reported to the Node as a collection of raw, **unedited** files. These can be in the form of a zipped folder of `.VRLs`, a database from Thelma Biotel or any other raw data product from any manufacturer. The files contain only transmitter numbers and the datetimes at which they were recorded at a specific receiver. The `tag metadata` and `deployment metadata` will provide the associated geographic and biological context to this data.

Visual Inspection

Once the files are received from a researcher, the Data Manager should first complete a visual check for formatting and accuracy.

Things to visually check:

- Do the files appear edited? Look for `_edited` in file name.
- Is the file format the same as expected for that manufacturer? Ex. `.vrl` for Innovasea - not `.csv` or `rld` formats.
- Is there data for each of the instrument recoveries that was reported in the `deployment metadata`?

# Convert to CSV

Once the raw files are obtained, the data must be converted to `csv` format. There are several ways this can be done, depending on the manufacturer.

For Innovasea
- VUE
    - Open a new `database`
    - Import all the `VRL` files
    - Select `export detections` and choose the location you want to save the files
    - Select `export events` and choose the location you want to save the files
- Fathom Connect App
    - choose "export data"
    - select the relevant files and import into the Fathom Connect application
    - export all data types, and choose the location you want to save the files
- `convert - Fathom (vdat) Export - VRL to CSV` Nodebook
    - this will use the `vdat.exe` executable to export from VRL/VDAT to CSV
    - select the folder containing the relevant files and the location you'd like the CSVs saved
    - run the cells to `convert`

For Thelma Biotel
- use the `ComPort` software to open the `.tbdb` file and export as CSV

For Lotek
- exporting to CSV is more complicated, please reach out to OTN for specific steps

Other manufacturers: contact OTN staff.


# detections - 1 - load csv detections

Detections-1 loads CSV detections files into a new database table. If detections were exported using `Fathom` or the `convert - Fathom (vdat) Export - VRL to CSV` notebook, the `events` records will also be loaded at this stage. This is because these applications combine the detections and events data in one CSV file.
### Import cells and Database Connections

As in all notebooks, run the import cell to get the packages and functions needed throughout the notebook. This cell can be run without any edits.

The second cell will set your database connection. You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

Once you have added your information, you can run the cell. Successful login is indicated with the following output:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.for.your.org Database:your_db_name User:your_node_admin Node:Node
~~~
{: .language-plaintext .example}


### User Input

Cell three requires input from you. This information will be used to get the raw detections CSV and to be able to create a new raw table in the database.

1. `file_or_folder_path = r'C:/Users/path/to/detections_CSVs/'`
    * paste a filepath to the relevant CSV file(s). The filepath will be added between the provided quotation marks.
    * this can be a path to a single CSV file, or a folder of multiple CSVs.
1. `table_suffix = 'YYYY_mm'`
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar, to indicate the most-recently downloaded instrument.
1. `schema = 'collectioncode'`
	  * please edit to include the relevant project code, in lowercase, between the quotes.

There are also some optional inputs:
- `load_detections`: a true or false value using the table suffix you supplied
- `stacked`: this is for Fathom exports only and is a way to know how to parse them

Once you have added your information, you can run the cell.

### Verify Detection File and Load to Raw Table

Next, the notebook will review and verify the detection file(s) format, and report any error. Upon successful verification, you can then run the cell below which will attempt to load the detections into a new raw table.

The notebook will indicate the success of the table-creation with a message such as this:

~~~
Reading fathom files...
Loading Files...
7/7
~~~
{: .language-plaintext .example}


#### Task list checkpoint

In GitLab, this task can be completed at this stage:

`- [ ] - NAME load to raw detections (detections-1 notebook) **(:fish: table name: c_detections_yyyy)**`

Ensure you paste the table name (ex: c_detections_YYYY_mm) into the section indicated, before you check the box.

### Verify Raw Detection Table

This cell will now complete the Quality Control checks of the raw table. This is to ensure the Nodebook loaded the records correctly from the CSVs.

The output will have useful information:
- Are there any duplicates?
- Are the serial numbers formatted correctly?
- Are the models formatted correctly?

The notebook will indicate the sheet had passed quality control by adding a ✔️**green checkmark** beside each section.

If there are any errors, contact OTN for next steps.

#### Task list checkpoint

In GitLab, these tasks can be completed at this stage:

`- [ ] - NAME verify raw detections table (detections-1 notebook)`

# events - 1 - load events into c_events_yyyy

Events-1 is responsible for loading receiver events files into raw tables. This is only relevant for CSVs that were **NOT** exported using `Fathom` or the `convert - Fathom (vdat) Export - VRL to CSV` notebook.

### Import cell

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. This cell can be run without any edits.

### User Inputs

Cell two requires input from you. This information will be used to get the raw events CSV and to be able to create a new raw table in the database.

1. `filepath = r'C:/Users/path/to/events.csv'`
    * paste a filepath to the relevant CSV file. The filepath will be added between the provided quotation marks.
1. `table_name = 'c_events_YYYY_mm'`
	  * Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar, to indicate the most-recently downloaded instrument.
1. `schema = 'collectioncode'`
	  * please edit to include the relevant project code, in lowercase, between the quotes.

There are also some optional inputs:
- `file_encoding`: The file_encoding: ISO-8859-1 in the event export. The  default encoding used in VUE's event export

Once you have added your information, you can run the cell.

### Verifying the events file

Before attempting to load the event files to a raw table the notebook will verify the file to make sure there are no major issues. This will be done by running the Verify events file cell. Barring no errors, you will be able to continue.

The notebook will indicate the success of the file verification with a message such as this:

~~~
Reading file 'events.csv' as CSV.
Verifying the file.
Format: VUE 2.6+
Mandatory Columns: OK
date_and_time datetime:OK
Initialization(s): XX
Data Upload(s): XX
Reset(s): XX
~~~
{: .language-plaintext .example}


### Database Connection

You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

Once you have added your information, you can run the cell. Successful login is indicated with the following output:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.for.your.org Database:your_db_name User:your_node_admin Node:Node
~~~
{: .language-plaintext .example}


### Load the events file into the c_events_yyyy table

The second last cell loads the events file into a raw table. It depends on successful verification from the last step. Upon successful loading and can dispose of the engine then move on to the next notebook.

The notebook will indicate the success of the table-creation with the following message:

~~~
File loaded with XXXXX records.
100%
~~~
{: .language-plaintext .example}


#### Task list checkpoint

In GitLab, these tasks can be completed at this stage:

`- [ ] - NAME load raw events (`events-1` notebook) **(:fish: table name: c_events_yyyy )**`

Ensure you paste the table name (ex: c_events_YYYY_mm) into the section indicated, before you check the box.

# events - 2 - move c_events into events table

This notebook will move the `raw` events records in the `intermediate` events table.

### Import cell

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. This cell can be run without any edits.

### User input

This cell requires input from you. This information will be used to get the raw events CSV and to be able to create a new raw table in the database.

1. `c_events_table = 'c_events_YYYY_mm'`
	  * Within the quotes, please add your custom table suffix, which you have just loaded in either `detections-1` or `events-1`.
1. `schema = 'collectioncode'`
	  * please edit to include the relevant project code, in lowercase, between the quotes.

### Database Connection

You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

Once you have added your information, you can run the cell. Successful login is indicated with the following output:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.for.your.org Database:your_db_name User:your_node_admin Node:Node
~~~
{: .language-plaintext .example}


### Verify table format

You will then verify that the c_events events table you put in exists and then verify that it meets the required format specifications.

The notebook will indicate the success of the table verification with a message such as this:

~~~
Checking table name format... OK
Checking if schema collectioncode exists... OK!
Checking collectioncode schema for c_events_YYYY_mm table... OK!
collectioncode.c_events_YYYY_mm table found.
~~~
{: .language-plaintext .example}

If there are any errors in this section, please contact OTN.

### Load to Events table

Pending nothing comes up in the verification cells, you run the `loading` cell.

The notebook will indicate the success of the processing with a message such as this:

~~~
Checking for the collectioncode.events table... OK!
Loading events... OK!
Loaded XX rows into collectioncode.events table.
~~~
{: .language-plaintext .example}


#### Task list checkpoint

In GitLab, these tasks can be completed at this stage:
   
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

- Note: if not detections were promoted into detections_yyyy_movers please assign the ticket to OTN for trouble shooting.
  
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
- Note: if not detections were promoted into detections_yyyy_movers please assign the ticket to OTN for trouble shooting.

5. Run the `verify_otn_detections` cell to verify the `otn_detections_yyyy` tables. Check off the step in the Gitlab ticket.

`- [ ] - NAME verify otn_detections_yyyy (movers-4 notebook)`

6. Run the `load_platforms_to_moorings` cell to verify the `moorings` tables. Check off the step in the Gitlab ticket.

`- [ ] - NAME create mission and receiver records in moorings (movers-4 notebook)`

# events - 3 - create download records

This notebook will promote the events records from the intermediate `events` table to the final `moorings` records. Only use this notebook after adding the receiver records to the moorings table as this process is dependant on receiver records.

### Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. This cell can be run without any edits.

The second cell will set your database connection. You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

Once you have added your information, you can run the cell. Successful login is indicated with the following output:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.for.your.org Database:your_db_name User:your_node_admin Node:Node
~~~
{: .language-plaintext .example}


### User Inputs

Information regarding the tables we want to check against is required. Please complete `schema = 'collectioncode'`, edited to include the relevant project code, in lowercase, between the quotes.

Once you have edited the value, you can run the cell.

### Detecting Download Records

The next cell will scan the `events` table looking for data download events, and attempt to match them to their corresponding receiver deployment.

You should see output like this:

~~~
Found XXX download records to add to the moorings table
~~~
{: .language-plaintext .example}


The next cell will print out all the identified download records, in a dataframe for you to view.

### Loading Download Records

Before moving on from this you will need to confirm 2 things:

1) Confirm that **NO Push** is currently ongoing

2) confirm `rcvr_locations` for this schema have been verified.

If a Push is ongoing, or if verification has not yet occurred, you **must** wait for it to be completed before processing beyond this point.

If everything is OK, you can run the cell. The notebook will indicate success with a message like:

~~~
Added XXX records to the moorings table
~~~
{: .language-plaintext .example}


#### Task list checkpoint

In GitLab, this task can be completed at this stage:

`- [ ] - NAME load download records ("events-3" notebook)`

### Verify Download Records

This cell will have useful information:
- Are the instrument models formatted correctly?
- Are receiver serial numbers formatting correctly?
- Are there any other outstanding download records which haven't been loaded?

The notebook will indicate the table has passed verification by the presence of ✔️**green checkmarks**.

If there are any errors, contact OTN for next steps.


#### Task list checkpoint

In GitLab, this task can be completed at this stage:

`- [ ] - NAME verify download records ("events-3" notebook)`

# events-4 - process receiver configuration

This notebook will process the receiver configurations (such as MAP code) from the events table and load them into the schema's `receiver_config` table. This is a new initiative by OTN to document and store this information, to provide better feedback to researchers regarding the detectability of their tag-programming through time and space.

### Import cells and Database connections

As in all notebooks run the import cell to get the packages and functions needed throughout the notebook. This cell can be run without any edits.

The second cell will set your database connection. You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

Once you have added your information, you can run the cell. Successful login is indicated with the following output:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.for.your.org Database:your_db_name User:your_node_admin Node:Node
~~~
{: .language-plaintext .example}


### User Inputs

Information regarding the tables we want to check against is required. Please complete `schema = 'collectioncode'`, edited to include the relevant project code, in lowercase, between the quotes.

Once you have edited the value, you can run the cell.

### Get Receiver Configuration

Using the receiver deployment records, and the information found in the `events` table, this cell will identify and important configuration information for each deployment. A dataframe will be displayed.

The following cell will extrapolate further to populate all the required columns from the `receiver_config` table. A dataframe will be displayed.

### Load Configuration to Database

Finally, the notebook will insert the identified records into the `receiver_config` table. You should see the following success message, followed by a dataframe:

~~~
The following XX receiver configurations are new and have been inserted:
~~~
{: .language-plaintext .example}


#### Task list checkpoint

In GitLab, this task can be completed at this stage:

`- [ ] - NAME process receiver configuration ("events-4" notebook)`


# Final Steps

The remaining steps in the GitLab Checklist are completed outside the notebooks.

First: you should access the Repository folder in your browser and ensure the raw detections are posted in the `Data and Metadata` folder.

Finally, the Issue can be passed off to an OTN-analyst for final verification in the database.
