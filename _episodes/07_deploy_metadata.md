---
title: "Deployment Metadata"
teaching:30
exercises: 0
questions:
- "How do I load new deployments into the Database?"
objectives:
- "Understand the proper template-completion"
- "Understand how to use the Gitlab checklist"
- "Learn how to use the `Deploy` notebook"
keypoints:
- "Loading receiver metadata requires judgement from the Data Manager"
- "Communication with the researcher is essential when errors are found"
---
Once a project has been registered, the next step (for `Deployment` and `Data` project types) is to quality control and load the instrument deployment metadata into the database. Deployment metadata should be reported to the Node in the template provided [here](https://members.oceantrack.org/data/data-collection). This file will contain information about the deployment of any instruments used to detect tagged subjects or collect related data. This includes stationary test tags, range test instruments, non-acoustic environmental sensors etc. Geographic location, as well as the duration of the deployment for each instrument, is recorded. The locations of these listening stations are used to fix detections geographically.

Remembering our previous lessons, there are multiple levels of data-tables in the database for deployment records: `raw tables`, `rcvr_locations`, `stations` and `moorings`. The process for loading instrument metadata reflects this, as does the Gitlab task list.

# Submitted Metadata

Immediately, upon receipt of the metadata, a new Gitlab Issue should be created. Please use the `Receiver_metadata` Issue checklist template.

Here is the Issue checklist, for reference:

```markdown
Receiver Metadata
- [ ] - NAME add label *'loading records'*
- [ ] - NAME load raw receiver metadata (`deploy` notebook) **put_table_name_in_ticket**
- [ ] - NAME check that station locations have not changed station "NAMES" since last submission (manual check)
- [ ] - NAME verify raw table (`deploy` notebook)
- [ ] - NAME post updated metadata file to project repository (OTN members.oceantrack.org, FACT RW etc)
- [ ] - NAME load station records (`deploy` notebook)
- [ ] - NAME verify stations (`deploy` notebook)
- [ ] - NAME load to rcvr_locations (`deploy` notebook)
- [ ] - NAME verify rcvr_locations (`deploy` notebook)
- [ ] - NAME add transmitter records receivers with integral pingers (`deploy` notebook)
- [ ] - NAME load to moorings (`deploy` notebook)
- [ ] - NAME verify moorings (`deploy` notebook)
- [ ] - NAME label issue with *'Verify'*
- [ ] - NAME pass issue to OTN daq for reassignment to analyst
- [ ] - NAME check if project is OTN loan, if yes, check for lost indicator in recovery column, list receiver serial numbers for OTN inventory updating.
- [ ] - NAME pass issue to OTN analyst for final verification
- [ ] - NAME check for double reporting (`deploy-4 verification script`)

```
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
1. If any of the above mandatory fields are blank, follow-up with the researcher will be required if:
	* you cannot discern the values yourself.
	* you do not have access to the Tag or Receiver Specifications from the manufacturer (relevant for the columns containing `transmitter` information).
1. Are all lat/longs in the correct sign? Are they in the correct format (decimal degrees)?
1. Do all transceivers/test tags have their transmitters provided?
1. Are all recoveries from previous years recorded?
1. Do comments suggest anything was lost or damaged, where recovery indicator doesn't say "lost" or "failed"?

In general, most commonly formatting errors occur in records where there are >1 instrument deployed at a station, or if the receiver was deployed and recovered from the same site.

The metadata template [available here](https://members.oceantrack.org/data/data-collection) has a `Data Dictionary` sheet which contains detailed expectations for each column. Refer back to these definitions often. We have also included some recommendations on our [FAQ page](https://members.oceantrack.org/faq). Here are some guidelines:

- Deployment, download, and recovery information for each station is entered on a single line.
-  When more than one instrument is deployed, downloaded, or recovered at the same station, enter each one on a separate line using the same `OTN_ARRAY`, `STATION_NO`.
- When sentinel tags are co-deployed with receivers, their information can be added to `TRANSMITTER` and `TRANSMIT_MODEL` columns, on the same line as the receiver deployment.
- If a sentinel tag is deployed alone then a new line for that station, with as much information as possible, is added. 
- When an instrument is deemed lost, a value of `l` or `lost` should be entered in the "recovered" field; if the instrument is found, this can be updated by changing the recovery field to `f` or `found` and resubmitting the metadata sheet.
- Every time an instrument is brought to the surface, enter "y" to indicate it was successfully recovered, even if only for downloading and redeployment. A new line for the redeployment is required.

# Quality Control - Deploy Notebook

Each step in the Issue checklist will be discussed here, along with other important notes required to use the Nodebook.

### Imports cell

This section will be common for most Nodebooks: it is a cell at the top of the notebook where you will import any required packages and functions to use throughout the notebook. It must be run first, every time. 

There are **no** values here which need to be edited.

## Path to File

In this cell, you need to paste a filepath to the relevant Deployment Metadata file. The filepath will be added between the provided quotation marks.

Correct formatting looks something like this:

```
# Shortfrom metadata path (xls, csv)
filepath = r'C:/Users/path/to/deployment_metadata.xlsx'
```

You also must select the format of the Deployment metadata. Currently, only the FACT Network uses a slightly different format than the template [available here](https://members.oceantrack.org/data/data-collection). If its relevant for your Node, you can edit the `excel_fmt` section.

Correct formatting looks something like this:

```
excel_fmt = 'otn' # Deployment metadata format 'otn' or 'fact'
```

Once you have added your filepath and chosen your template format, you can run the cell.

Next, you must choose which *sheet* you would like to quality control. Generally, it will be names `Deployment` but is often customized by researchers. Once you have selected the sheet name, **do not** re-run the cell to save the output - simply ensure the correct sheet is highlighted and move onto the next cell.

### Table Name and Database Connection

You will have to edit **three** sections: 

1. `schema = 'collectioncode'`
	* please edit to include the relevant project code, in lowercase, between the quotes.
1. `table_name = 'c_shortform_YYYY_mm'`
	* Within the quotes, please add your custom table suffix. We recommend using `year_month` or similar, to indicate the most-recently deployed/recovered instrument in the metadata sheet.
1. `engine = get_engine()` 
	* Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
	* On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
	* The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`. 

Once you have added your information, you can run the cell. Successful login is indicated with the following output:

``` 
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.load.oceantrack.org Database:otnunit User:admin Node:OTN
```

### Verification of File Contents

This cell will now complete the first round of Quality Control checks.

The output will have useful information:
- Is the sheet formatted correctly? Correct column names, datatypes in each column etc.
- Compared to the `stations` table in the database, are the station names correct? Have stations "moved" location? Are the reported bottom_depths significantly different (check for possible `ft` vs `m` vs `ftm` errors).
- Are all recovery dates after the deployment dates?
- Are all the provided `ins_model_no` values present in the `obis.instrument_models` table? If not, please check the records in the `obis.instrument_models` and the source file to confirm there are no typos. If this is a new model which has never been used before, follow the link to the `add instrument_models` notebook to add the new instrument model. 
- Do all transceivers/test tags have their transmitters provided? Do these match any manufacturer Specifications we have in in the database?
- Are there any overlapping deployments (one serial number deployed at multiple locations for a period of time)? 
- Are all the deployments within the Bounding Box of the project. If the bounding box needs to be expanded to include the stations, you can use the `Square Draw Tool` to re-draw the bounding box until you are happy with it. Once all stations are drawn inside the bounding box, press the `Adjust Bounding Box` button to save the results.
- Are there possible gaps in the metadata, based on previously-loaded `detections` files?

The notebook will indicate the sheet had passed quality control by adding a ✔️**green checkmark** beside each section. There should also be an interactive plot generated, summarizing the instruments deployed over time for you to explore, and a map of the deployments.

Using the map, please confirm the following:
1. the instrument deployment locations are in the part of the world expected based on the project abstract. Ex: lat/long have correct +/- signs
1. the instrument deployments do not occur on land 

If there is information which is not passing quality control, you should fix the source-file (potentially speaking to the researcher) and try again.

### Loading the Raw Table

**ONLY** once the source file has successfully passed ALL quality control checks can you load the raw table to the database.

You have already named the table above, so there are no edits needed in this cell.

The notebook will indicate the success of the table-creation with the following message:

```
Reading file 'deployment_metadata.xlsx' as otn formatted Excel.
Table Loading Complete: 
 Loaded XXX records into table schema.c_shortform_YYYY_mm
```
#### Task list checkpoint

In Gitlab, these tasks can be completed at this stage:

```markdown
- [ ] - NAME load raw receiver metadata ("deploy" notebook) **put_table_name_in_ticket**
- [ ] - NAME check that station locations have not changed station "NAMES" since last submission (manual check)
```

Ensure you paste the table name (ex: c_shortform_YYYY_mm) into the section indicated, before you check the box.


### Verify Raw Table 

This cell will now complete the Quality Control checks of the raw table. This is to ensure the Nodebook loaded the records correctly from the Excel sheet.

The output will have useful information:
- Are there any duplicate records?
- Is there missing information in the `ar_model_no` and `ar_serial_no` columns? If so, ensure that it makes sense for receivers to be deployed without Acoustic Releases in this location (ex: diver deployed).
- Do all transceivers/test tags have their transmitters provided? Do these match any manufacturer Specifications we have in in the database?
- Are there any non-numeric serial numbers? Do these makes sense (ex: environmental sensors)?
- Are the deployments within the bounding box?
- Is the `recovered` column completed correctly, based on the `comments` and the `recovery_date` columns?
- Are there blank strings that need to be set to NULL? If so, press the `Set to NULL` button in that cell.

The notebook will indicate the sheet had passed quality control by adding a :heavy_check_mark:**green checkmark** beside each section.

If there are any errors go into database and fix the `raw` table directly, or contact the researcher, and re-run.


#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - NAME verify raw table ("deploy" notebook)`

### Loading Stations Records

**STOP** - confirm there is no Push currently ongoing. If a Push is ongoing, you must wait for it to be completed before processing beyond this point

Only once the raw table has successfully passed ALL quality control checks can you load the stations information to the database `stations` table.

Running this cell will first check for any new stations to add, then confirm the records in the `stations` table matches the records in the `moorings` table where `basisofrecord = 'STATION'`.

If new stations are identified:
- Compare these station names to existing stations in the `stations` table in the database. Are they truly new, or is there a typo in the raw table? Did the station change names, but is in the same location as a previous station?
- If there are fixes to be made, change the records in the `raw` table, or contact the researcher.
- If all stations are truly new, you should review the information in the editable form, then select `Add New Stations`.

The success message will look like:

```
TODO ---- whats the success message?
```

If the `stations` and `moorings` tables are not in-sync, the difference between the two will need to be compared and possibly updated.

#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - load station records ("deploy" notebook)`

### Verify Stations Table

This cell will now complete the Quality Control checks of the stations records contained in the entire schema. We are no longer checking our newly-loaded records only, but also each previously-loaded record.

The output will have useful information:

- Were all the stations from our `raw` table promoted to the `stations` table, and the `moorings` table?
- Are all stations in unique locations?
- Are all stations within the project's bounding box?
- Are there blank strings that need to be set to NULL? If so, press the `Set to NULL` button in that cell.
- Are any of the dates in the future?

The notebook will indicate the sheet had passed quality control by adding a ✔️**green checkmark** beside each section.

If there are any errors go into database and fix the `raw` table directly, or contact the researcher, and re-run. If there are problems with the `stations` or `moorings` table, you will need to contact an OTN database staff member to resolve these.

#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - verify stations("deploy" notebook)`

### Load to rcvr_locations
Once the `station` table is verified, the receiver deployment records can now be promoted to the `intermediate` rcvr_locations table.

The cell will identify any new deployments to add, and any previously-loaded deployments which need updating (ex: they have been recovered).

If new deployments are identified:
- Compare these deployments to existing deployments in the `rcvr_locations` table in the database. Are they truly new, or is there a typo in the raw table? Did the station change names, but is in the same location as before? Did the serial number change, but the deployment location and date are the same?
- If there are fixes to be made, change the records in the `raw` table, or contact the researcher.
- If all deployments are truly new, you can then select `Add Deployments`.

If deployment updates are identified:
- Review the suggested changes: **do not** select changes which remove information (ex: release 590023 --> `None` is not a good change to accept).
- Use the check boxes to select only the appropriate changes
- Once you are sure the changes are correct, you can then select `Update Deployments`.

Each instance will give a success message such as:

```
XX deployments load to rcvr_locations
```
#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - load to rcvr_locations ("deploy" notebook)`


### Verify rcvr_locations

This cell will now complete the Quality Control checks of the rcvr_locations records contained in the entire schema. We are no longer checking our newly-loaded records only, but also each previously-loaded record.

The output will have useful information:
- Have all deployments been loaded from the raw table? Please note that instruments where a sentinel tag is deployed alone at a station will not be loaded to rcvr_locations, and so these will likely be flagged in this section for your review.
- Are there blank strings that need to be set to NULL? If so, press the `Set to NULL` button in that cell.
- Based on comments, are there any instances where a receiver's status should be changed to "lost"?
- Are all instruments in the `obis.instrument_models` table?
- Are there any overlapping deployments?
- Is the geom, serial number and catalognumber formatted correctly?

The notebook will indicate the table has passed quality control by adding a ✔️**green checkmark** beside each section. 

If there are any errors contact OTN, or contact the researcher, to resolve. 

#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - verify rcvr_locations ("deploy" notebook)`

### Load Transmitter Records to Moorings

The `transmitter` values associated with transceivers, co-deployed sentinel tags or stand-alone test tags will be loaded to the `moorings` table in this section. Existing transmitter records will also be updated if relevant.

If new transmitters are identified:
- Review for accuracy then select `Add Transmitters`.

If transmitter updates are identified:
- Review the suggested changes: **do not** select changes which remove information (ex: release 590023 --> `None` is not a good change to accept).
- Use the check boxes to select only the appropriate changes
- Once you are sure the changes are correct, you can then select `Update Transmitters`.

#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - load transmitter records receivers with integral pingers ("deploy" notebook)`

### Load Receivers to Moorings

The final, highest-level table for instrument deployments is `moorings`.

The cell will identify any new deployments to add, and any previously-loaded deployments which need updating (ex: they have been recovered).

Please review all new deployments and deployment update for accuracy, then press the associated buttons to make the changes. At this stage, the updates are not editable: any updated chosen from the `rcvr_locations` section will be processed here.

You may be asked to select an `instrumenttype` for certain receivers. Use the drop-down menu to select before adding the deployment.

#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - load to moorings ("deploy" notebook)`

### Verify Moorings

This cell will now complete the Quality Control checks of the moorings records contained in the entire schema. We are no longer checking our newly-loaded records only, but also each previously-loaded record.

The output will have useful information:
- Have all deployments been loaded from rcvr_locations? 
- Do we have manufacturer specifications for the receivers or tags deployed?
- Are there blank strings that need to be set to NULL? If so, press the `Set to NULL` button in that cell.
- Do the `STATIONS` records match the information in the `stations` table?
- Are all instruments in the `obis.instrument_models` table?
- Are there any overlapping deployments or receivers or tags?
- Are there duplicate download records?
- Is the lat/long, geom, serial number and catalognumber formatted correctly?

The notebook will indicate the table has passed quality control by adding a ✔️ **green checkmark** beside each section. 

If there are any errors contact OTN to resolve. 

#### Task list checkpoint

In Gitlab, this task can be completed at this stage:

`- [ ] - verify moorings ("deploy" notebook)`

# Final Steps

The remaining steps in the Gitlab Checklist are completed outside the notebooks.

First: you should access the Repository folder in your browser and add the cleaned Deployment Metadata `.xlsx` file into the "Data and Metadata" folder.

Finally, the Issue can be passed off to an OTN-analyst for final verification in the database.

{% include links.md %}
