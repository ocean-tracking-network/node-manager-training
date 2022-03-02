---
title: "OTN system and structure and outputs"
teaching: 20-30
exercises: 0
questions:
- "What does an OTN style database look like?"
- "What is the general path data takes in the OTN data system"
- "What does the OTN Data system output?"
objectives:
- "Understand the OTN Database structure on a high level"
- "Understand the general path of data of data through the OTN System"
- "Understand what the OTN System can output"
keypoints:
- "All OTN database have the same structure"
- "Databases are divided into project schemas which get certain tables based on the data they submit"
- "Data in the OTN system goes from the the raw tables to the intermediate tables to the upper tables and lastly aggregate tables"
---

## OTN Data system 

The OTN data system is an aggregator of telemetry data made up of interconnected node databases and data processing tools. These work together to connect researchers with relevant and reliable data. At the heart of this system are nodes and their OTN node style databases.

An OTN node style database is just a database that follows a certain structure. Each OTN node has its own database that follows the same structure as all the others. This structure allows nodes to use the OTN data loading process, produce OTN data products, and share data across other nodes. 

## Basic structure:

The basic structure of an OTN style database is that a node's projects get subdivided into their own schemas. These schemas contain only the relevant tables and data to that project. The tables included in each schema are created based on which type of data the project is reporting. 

*Projects can have the type tracker, deployment, or data. Tracker projects submit data related to tags and animals. They get tables based on the tags, animals, and detections of those tags. Deployment projects submit data related to receivers and detections. These projects get tables related to receiver deployments and detections on their receivers. Data projects which are projects that do both tracking and deployments will submit data related tags, animals, receivers, and detections and will get all the related tables.

In addition to the project schemas, there are some important common schemas in the database that node managers should be aware of. These additional schemas include the obis, erddap, geoserver, vendor, and discovery schemas. These schemas are found across all nodes and are important to end data products and processing. The obis schema holds data about a node's projects as well as the aggregated data from those projects. When data goes into a final table of the project schema it will be inherited into a table in obis generally with a similar name in the obis schema. The erddap schema holds data formatted to be used for ERDDAP instances. The geoserver schema holds data formatted to be used for Geoserver layers. The vendor schema holds specification data about tag and receiver instruments from vendors. The discovery schema holds summaries of data across the OTN ecosystem. There is a lot of information being shared and put into different places but this may be able to be adjusted based on sharing and reporting requirements.

## The Path of Data:

*The OTN data system takes 4 types of data: project, tag, deploy, and detections. Most data has a similar flow through the OTN system even though each type has different notebooks and processes for loading. The exception to this is project data which has a more unique journey because it is used to create a project schema.

## Project Data:

Project data has a unique journey because it is used to create a new schema in the database for a project. The data a project will be reporting dictates what type of tables the schema will have. This influences the loading tools and processes that will be used later on. The general journey of project data is that when a researcher submits a new project they fill out a project metadata sheet and submit it to the node manager. The node manager does some quick visual QC's to catch any obvious errors then puts the data through the notebook responsible for creating and updating projects(Create and Update Projects). The Create and Update Projects notebook will make a new schema in the database for that project, and fill it with the needed tables based on the data a project will be reporting. After this, OTN will verify the project one last time to make sure everything is good.

## Tag, deployment and detections data:

Even though tag, deployment, and detections data all have their own loading tools and process, their general path through the database is the same. These data types start out with a submission from the researcher. The node manager gets it from the document management website of the node's choice or puts it there if they got the data through email in order to have an easily findable copy later. They will then do some quick visual QC to catch any obvious errors. The data is then processed through the notebooks that correspond to its type and is processed through the system. This process is dictated by the task list associated with the issue made for this type. The data will first be loaded into the raw tables. This is the table that holds the raw data as submitted by the researcher (raw tables always have the prefix c_ and will have a suffix indicating the date it was loaded, typically YYYY_MM). After the raw table is verified, the data will move to the intermediate tables which is where the data has had some processing done to it but it is not in its final form. Then after the intermediate table is verified, it will move to the upper tables, where the data is finished being processed and is in its final form. This is the data that will be used for aggregation tables such as obis and for outputs such as detection extracts.

## Outputs of the OTN data system 

Besides just taking in data, the OTN data system outputs data as well. Every four months the OTN system goes through what is called ‘The Push’. This is where we take what data we have, verify it, and update our records. This is also the time when cross node matching is done, where detections are matched between nodes. Once cross node matching is done, detection extracts are ready to be sent to researchers with any newly updated data from their projects. Detection extracts are files that contain relevant detection data that are ready for use in many analysis packages, such as glatos and resonate. Additionally during the push, publications like discovery, erddap, and geoserver are updated with the newly verified and updated data.

## Backing up your data

With a OTN node style database you will be storing a lot of data so it is important to make sure that data is protected. To ensure this you want to make sure that your database is being backed up properly in the event that your primary database crashes, is corrupted, is lost, or any other data losing event. 

You will want to talk to the groups or institutions that you are working with for database administration to find out their policies and practices for backups. Backup strategies may vary from group to group but it is a good idea to make sure they are adequately backing up your data daily if not multiple times a day and keeping copies of backups in different locations in the case that something happens at a single location. 
