---
title: "Supplementary notebooks"
teaching: 0
exercises: 0
questions:
- "What are other notebooks are there that could be usefull for me to know as a node manager?"
objectives:
- "Learn about notebooks that are useful for node managers but not part of the data loading notebooks"
keypoints:
- "ipython utilities has many useful notebooks for node managers to help them"
---

## Supplementary notebooks:

 ## Check Environment: 

 This notebook checks your system python environment against our environment.yml. This is to see if the packages and libraies you have installed are what is inline with what is needed to run the ipython.
 
## scientific_name_check:

This notebook uses [WoRMs](https://www.marinespecies.org/index.php) to check animal common and scientific names. It also allows you to add names to obis.scientificnames table for use in projects.
 
 ## Add Instrument Models to Database :  

Notebook adds an instrument model to the obis.instrument_models table.

 ## insert_vendor_sheet: 
 
Used to load vendor specifications for tags or receivers into the vendor tables.  
 
 ## convert - Fathom (vdat) Export - VRL to CSV: 
 
Convert VRLs or VDATs into CSV files using command-line Fathom software. Can also be done using the Fathom app.  
 
 ## Active Tracking:
 
Handles active tracking data  


## Slocum Telemetry Notebook: 

Handles telemetry metadata and data from slocum gliders  
 
## Load Health Report: 

Load Glider Health records.
  
## Telemetry Processing for Wave Gliders and Animals: 

Handles telemetry metadata and data from wave gliders

## create and update contacts' notebook

This notebooks can be used to add new contacts and update contacts information in the database

## Active Tags and IUCN Status
OTN-flavoured reporting of Tag Life, Tags, Detections, Stations

## Generate Receiver Map
Map to show recivers from nodes

##  Receiver Operator Report
This notebook generates a summary report for receiver operators to describe what animals have been seen and when. 

## dbfix notebooks

These are a seris of notebooks for fixing common issues that come up in the database. These notebooks are out of scope for the current training but eveventually do wish to learn more we will have further training available in future on them.
