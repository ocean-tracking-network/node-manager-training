Welcome to OTN's Node Manager Training Curriculum.

This OTN-hosted training will provide OTN-style Node Managers with an overview of the processes and tools to use to 
    1) ensure data is formatted correctly and free form errors, 
    2) ingest data into the Database Node and 
    3) create any relevant data products for members of their Node.

Attendees should be detail oriented, in-tune with their local telemetry communities, and not afraid to ask questions!

The website rendering is available here https://ocean-tracking-network.github.io/node-manager-training/index.html

## General Node Manager Training Agenda
The next scheduled training is December 2nd - 6th, 2024 in Halifax, NS, at the Steele Ocean Sciences Building (OTN Headquarters). Invitees from new and existing nodes will explore the OTN Node curriculum with the [OTNDC team](https://oceantrackingnetwork.org/staff/). A draft agenda (subject to update or amendment) for the week's proceedings:

### Day 1
*Welcome*


* **Presentation:** Introduction to Nodes (virtual connections available)
    * The Ocean Tracking Network's Data Centre, the Care of Animal Tracking Data, and the Database Node concept - Jon Pye

*AM Break*

* **OTN System, Structure, and Outputs**
    * Schema structure and data workflows

* **Software Setup and Installation**
    * Python
    * Git
    * Nodebooks

*Lunch*

* **The Data Loading Workflow**
    * How data is received
    * Documenting data loading tasks
    * Accessing and querying your database

* **Data Loading - Project Metadata**
    * Practical - register metadata about new projects to the Node

### Day 2

* **Data Loading - Tagging Metadata**
    * Practical - load records of deployed tags to a project in the Node
    * Validation - internally consistent data 
    * Verification - data consistent across the database

*AM Break*

* **Data Loading - Deployment Metadata**
    * Practical - load records of deployed listening equipment to a project in the Node
    * Validation - internally consistent data
    * Verification - data consistent across the database

*Lunch*

* **Detection Loading**
    * Practical - **load** detection files from the listening instruments to a project in the Node
    * **Validation** - unedited files created by the instrument or client software for the instrument
    * **Verification** - proper formatting of serials, models, dates
    * Recorded Events data loaded from instrument
        * tilt, temperature, etc.
        
*PM Break*

* Detection Loading cont.
    * **Verification** - detections not previously loaded
    * **Correction** - time drift calculations
    * **Verification** - no missing metadata
    * Events - **create** receiver configuration record from Event data
        * listening scheme (OP, NexTrak, MAP-114, etc.)
    * **Match** detections to animal tags registered to any project within the Database Node

### Day 3

* Moving Platforms
    * Loading Detections and Mobile Receiver Deployments

*AM Break*
* Moving Platforms cont.
    * Gliders

*Lunch*
* Moving Platforms cont.
    * Satellite-tagged animals
    * Manual Sampling

*PM Break*
* Visualization Notebooks
    * Node summaries of counting statistics
    * Project-by-project reporting
    * Other

* Evening: Dinner - venue TBD

### Day 4

* Supplementary Notebooks
    * scientific_name_check
    * Registering new instrument models
    * vendor tag and sales sheets
    * Health reporting
    * Contacts updates
    * DB-Fix Notebooks

*Lunch*

* The Data Push
    * Rationale, Process, Schedule
    * Creating detection extracts for researchers

*PM Break*
* Fixing Data errors
* OTN All-Hands meeting

### Day 5

* Upholding the Data Policy
* Nodebook Development and Improvements
* Tandem real data loading w/ OTNDC *or* DB-Fix notebooks
*Lunch*
* Tandem real data loading w/ OTNDC *or* DB-Fix notebooks cont.