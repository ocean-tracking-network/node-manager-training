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

This Nodebook checks your system Python environment against our `environment.yml`. This is to see if the Python packages and libraries you have installed are in line with what is required to run the Nodebooks. This will assist you with updating your packages if they become out-of-date, or if OTN develops and publishes new tools which rely on new packages.
 
## scientific_name_check

This Nodebook uses [WoRMS](https://www.marinespecies.org/index.php) to check animal common and scientific names. It is used to add new species names to `obis.scientificnames` table for use each project. The instructions for using this Nodebook are the same as the `Adding Scientific Names` section in the `Create and Update Projects` Nodebook.

Occasionally, you may have to add a new species to the WoRMS data system. The specifics of doing so are laid out on the [WoRMS Contribution page](https://marinespecies.org/contribute.php) but they amount to: email info@marinespecies.org with a literature record describing the taxa that needs to be added. Traditionally WoRMS was not a register of freshwater species but in recent years they have extended their scope to account for and track marine, brackish, and fresh habitat designations for their supported taxa. So don't hesitate to reach out to them and help them add new species!
 
## Add Instrument Models to Database  

This Nodebook is used to add an instrument model to the `obis.instrument_models` table.

## insert_vendor_sheet
 
Used to load manufacturer specifications for tags or receivers into the `vendor` tables.  
 
## [convert - Fathom (vdat) Export - VRL to CSV](https://ocean-tracking-network.github.io/node-manager-training/08_Detections/index.html#convertToCSV)
 
Convert VRLs or VDATs into CSV files using command-line Fathom software. Can also be done using the Fathom app.  

## Load Health Report 

This notebook will load "health reports" collected by `LiquidRobotics WaveGliders` while remotely offloading `VR4` receivers.

## Create and Update Contacts Nodebook

This Nodebook can be used to add new contacts to a project and update existing contacts in the database. Note: you cannot change someone's email address using this tool.

## DB-Fix Notebooks

These are a series of notebooks for fixing common issues found in the database. These notebooks are beyond the scope of the current training but eventually Data Managers who wish to learn more will be able to take further training. In the meantime, if you see notes in the notebooks such as "Use the DB Fix notebook called XXXX to correct this error", please contact OTN for assistance.

# Outdated / old workflows:

## Active Tracking
 
Handles active tracking data - detections collected by using a VR100 hydrophone (or similar) during "mobile" tracking activities. **(Superceded by Movers workflow)**

## Slocum Telemetry Notebook 

This notebook will process and load detection data collected by a `slocum` glider mission. Information required includes `glider telemetry`, `glider metadata`, and `detection files`. **(Superceded by Movers workflow)**  

## Telemetry Processing for Wave Gliders and Animals 

This notebook will process and load detection data collected by a `WaveGlider` mission. Information required includes `glider telemetry`, `glider metadata`, and `detection files`. **(Superceded by Movers workflow)**
