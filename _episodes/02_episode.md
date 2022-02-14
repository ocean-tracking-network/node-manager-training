---
title: "OTN system and structure and outputs"
teaching: 20-30
exercises: 0
questions:
- "What does an OTN style database look like?"
- "What is the gerneal path data takes in the OTN data system"
- "What does the OTN Data system output?"
objectives:
- "Understand the OTN Database sturcture on a high level"
- "Understand the general path of data of data through the OTN System"
- "Understand what the OTN System can output"
keypoints:
- "All OTN database have the same structure"
- "Databases are divided into project schemas which get certain tables based on the data they submit"
- "Data in the OTN system goes from the the raw tables to the intermediate tables to the upper tables and lastly aggregate tables"
---

## The OTN Data System 

The OTN data system is an aggregator of telemetry data made up of interconnected node databases and data processing tools. These work together to connect researchers with relevant and reliable data. At the heart of this system are nodes and their OTN style node databases.

An OTN node style database is just a database that follows a certain structure. Each OTN node has its own database that follows the same structure as all the others. This structure allows nodes to use the OTN data loading process, produce OTN data products, and share data across other nodes. 

## Basic Structure:

The basic structure of an OTN style database is that a node's projects get subdivided into their own schemas. These schemas contain only the relevant tables and data to that project. The tables included in each schema are created based on which type of data the project is reporting. 

Projects can have the type tracker, deployment or data projects. Tracker projects submit data related to tags and animals. They get tables based on the tags, animals, and detections of those tags. Deployment projects submit data related to receivers and detections. These projects get tables related to receiver deployments and detections on their receivers. Data projects which are projects that do both tracking and deployments will submit all data related tags, animals, receivers, and detections and will get all the related tables. For each type of metadata, there will be raw tables, intermediate tables, and final tables.

In addition to the project schemas, there are some important common schemas in the database that node managers should be aware of. These additional schemas include the obis, erddap, geoserver, vendor, and discovery schemas. These schemas are found across all nodes and are important to end data products and processing. The obis schema holds data about a node's projects as well as the aggregated data from those projects. When data goes into the final table of the project schema it will be inherited into a table in obis generally with a similar name. The erddap schema holds data formatted to be used for ERDDAP instances. The geoserver schema holds data formatted to be used for Geoserver layers. The vendor schema holds specification data about tag and receiver instruments from vendors. The discovery schema holds summaries of data across the OTN ecosystem. There is a lot of information being shared and put into different places but this can be adjusted based on sharing and reporting requirements.

## The Path of Data:

The OTN data system takes 4 types of data: project, tag, deploy, and detections. Any data that comes in should be processed in the above order because the later data types depend on the earlier ones (e.g. detections relies on deployment metadata). Most data has a similar flow through the OTN system even though each type has different notebooks and processes for loading. The exception to this is project data which have a more unique journey because it impacts the project schema.

## Project Data:

Project data has a unique journey because it is used to create a new schema for a project and it dictates what type of data a project will be reporting. This influences the loading tools and processes that will be used. The general journey of project data is that when a  researcher submits a new project they fill out a project metadata sheet and submit it to the node manager. The node manager does some quick visual QC's to catch any obvious errors then puts the data through the notebook responsible for creating and updating projects(Create and Update Projects). The Create and Update Projects notebook will make a new schema in the database for that project, and fill it with the needed tables for the data that project will be reporting. After this, OTN will verify the project one last time to make sure everything is good.

## Tag, Deployment, and Detections Data:

Even though tag, deployment, and detections data all have their own loading tools and process, their general path through the database is the same. These data types start out with a submission from the researcher. The node manager then puts the data into the document management website of the node's choice if it was not submitted through there, and does some quick visual QC to catch any obvious errors. The data is then processed through the notebooks that correspond to its type and is processed through the system. This process is dictated by the task list associated with the issue made for this processing. The data will first be loaded into the raw tables. This is the table that holds the raw data as submitted by the researcher (raw tables always have the prefix c_ and will have a suffix indicating the date it was loaded, typically YYYY_MM). After the raw table is verified, the data will move to the intermediate tables which is where the data has had some processing done to it but it is not in its final form. Then after the intermediate table is verified, it will move to the upper tables, where the data is finished being processed and is in its final form. This is the data that will be used for aggregation tables such as obis and for outputs such as detection extracts.

## Outputs of the OTN Data System 

Besides just taking in data, the OTN data system can output data as well. Every three months the OTN system goes through what we call ‘The Push’. This is where we take what data we have, verify it, and update our records. This is also the time when we do cross node matching, where we look for detection matches between nodes.  Once cross node matching is done, detection extracts are ready to be sent out. Detection extracts are files that contain relevant detection data.  There are multiple types of detection extracts OTN creates: 'qualified' which contain detections matched to animals of other projects, 'unqualified' which contain the project's unmatched or mystery detections which are not associated with any deployed tag, 'sentinel' which contain the detections matched to test or transceiver tags, and 'tracker' which contain animal metadata that have been matched to detections. Detection extracts are ready for use in many analysis packages, such as glatos and resonate. Additionally during the push, data is pulled into the OTN database from node discovery tables and updated for use in summary tables and output tables such as discovery, erddap, and geoserver.
