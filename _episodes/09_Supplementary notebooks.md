---
title: "Supplementary notebooks"
teaching: 15
exercises: 0
questions:
- "What are other Nodebooks are there that could be usefull for me to know as a Node Manager?"
objectives:
- "Learn about Nodebooks that are useful for Node Managers outside the core data loading notebooks"
keypoints:
- "ipython-utilities has many useful notebooks for Node Managers to help them"
---

OTN maintains several additional Nodebooks that fall outside the core `tag`, `deployment` and `detection` tools. These may be useful to Node managers who also deal with these particular scenarios.

## Check Environment 

This notebook checks your system Python environment against our `environment.yml`. This is to see if the Python packages and libraries you have installed are in line with what is required to run the ipython Notebooks. This will assist you with updating your packages if they become out-of-date, or if OTN develops and publishes new tools which rely on new packages.
 
## scientific_name_check

This notebook uses [WoRMS](https://www.marinespecies.org/index.php) to check animal common and scientific names. It is used to add new species names to `obis.scientificnames` table for use each project. The instructions for using this notebook are the same as the `Adding Scientific Names` section in the `Create and Update Projects` notebook
 
## Add Instrument Models to Database  

This notebook is used to add an instrument model to the `obis.instrument_models` table.

## insert_vendor_sheet
 
Used to load manufacturer specifications for tags or receivers into the `vendor` tables.  
 
## convert - Fathom (vdat) Export - VRL to CSV
 
Convert VRLs or VDATs into CSV files using command-line Fathom software. Can also be done using the Fathom app.  
 
## Active Tracking
 
Handles active tracking data - detections collected by using a VR100 hydrophone (or similar) during "mobile" tracking activities. 

## Slocum Telemetry Notebook 

This notebook will process and load detection data collected by a `slocum` glider mission. Information required includes `glider telemetry`, `glider metadata`, and `detection files`.
 
## Load Health Report 

This notebook will load "health reports" collected by `LiquidRobotics WaveGliders` while remotely offloading `VR4` receivers.
  
## Telemetry Processing for Wave Gliders and Animals 

This notebook will process and load detection data collected by a `WaveGlider` mission. Information required includes `glider telemetry`, `glider metadata`, and `detection files`.

## create and update contacts' notebook

This notebook can be used to add new contacts to a project and update existing contacts in the database. Note: you cannot change someone's email address using this tool.

## Active Tags and IUCN Status

Located in the `vis` subfolder. This creates a summary report of Tag Life, Tags, Detections, Stations. Tailored for OTN's reporting requirements and data policy.

## Generate Receiver Map

Located in the `vis` subfolder. This creates a map to show receivers from Nodes. Tailored for OTN's reporting requirements and data policy.

##  Receiver Operator Report

Located in the `vis` subfolder. This notebook generates a summary report for receiver operators to describe what animals have been seen and when. Tailored for OTN's reporting requirements and data policy.

## DB-Fix Notebooks

These are a series of notebooks for fixing common issues found in the database. These notebooks are beyond the scope of the current training but eventually Data Managers who wish to learn more will be able to take further training. In the meantime, if you see notes in the notebooks such as "Use the DB Fix notebook called XXXX to correct this error", please contact OTN for assistance.
