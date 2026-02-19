---
title: "Near Real Time (NRT) Animal Movement Location Data Quality Control (QC) Process"
teaching: 120
exercises: 0
questions:
- "What are NRT data and NRT data sources/vendors?"
- "Why NRT data needs QC?"
- "What is ArgosQC package?"
- "ArgosQC's workflow/features"
- "Satellite vendors: SMRU and WildlifeComputers"
- "How to configure ArgosQC (aniMotum) model parameters for various species?"
- "What are the mandatory import files for ArgosQC?"
- "What are the output files and how to interpreate ArgosQC results and diagnoses?"
- "What are the signs, and how do you fine-tune model parameters?"
---


#### below topics can be on a separate lesson.

- "How to access researchers' NRT data?"
- "How to match satellite tags from "
- "Satellite data providers, programs, PTTs and UUIDs"



objectives:
- "Understand near-real-time animal location data"
- "Understand satillite tags and vendors"
- "Understand the purpose of ArgosQC and configuration parameters"

keypoints:
- "ArgosQC for near-real-time data"
---

ArgosQC for near-real-time data is an essential automated process that uses state-space models (calling the underneath aniMotum R package) to filter noisy Argos satellite location data from vendors like SMRU and Wildlife Computers. Its effectiveness relies on configuring species-specific movement parameters and interpreting diagnostic outputs to produce reliable animal movement tracks for ecological research.

## NRT data and NRT data sources
1. Near Real-Time data are transmitted by satellite-linked electronic tags, when animals are at the ocean surface, via the Argos satellite constellation. 
2. Currently, the ArgosQC R package can access & download NRT data from two animal tag manufacturers - SMRU (Sea Mammal Research Unit, St Andrews, UK) and Wildlife Computers. Typically, NRT data are downloaded & QC'd once every 24 hours until tag deployments have ended (e.g., due to tag battery failure, or animal recapture). SMRU tag data are made available on a server with a Web Application Firewall (https://www.smru.st-andrews.ac.uk/protected/technical.html), which requires a user ID and password (provided to the tag owner) to access the tag data files (stored in a `.mdb` file). Once a node manager has access to a tag owner's user ID and password, SMRU tag `.mdb` files can be download via ArgosQC. Wildlife Computers tag data are accessed via a Data Portal (https://my.wildlifecomputers.com/), which requires both a user account (with user ID and password) to access the Portal AND explicit consent by tag owner(s) to share their tag data (set up by the tag owner on the Data Portal). Details on accessing tag data via the Wildlife Computers Portal are here: https://static.wildlifecomputers.com/Portal-and-Tag-Agent-User-Guide-2.pdf. Once a user account is set up by the node manager and explicit data sharing is set up by the tag owner, data can be downloaded by ArgosQC via the Wildlife Computers API.

## Quality Control for NRT data
1. With the Argos satellite system, tag location is measured by tag transmissions received by polar-orbiting Argos-Kinéis satellites as they pass overhead, and relayed to a base in France. The Doppler shift in tag transmission frequency is used to triangulate position of the tag. These calculations are conducted in real-time by the French organization Collecte Localisation Satellites (CLS). This positioning technology is less precise than GPS and requires a statistical quality control process (provided by the ArgosQC R package) to obtain more reliable locations and estimates of their uncertainty. 
2. At a minimum, satellite tags transmit their location but, depending on their programming and on-board sensor capabilities, may also transmit summaries of behavioural data such as dive profiles or diving and surfacing activity summaries, and physical observations of water temperature, salinity and/or fluorimetry at depth (CTD/FTD profiles) as animal dive through the water column. Tag owners can obtain records of their tag(s) locations through time from CLS, but CLS also provides the location data and all tag transmission messages to the tag manufacturers in near real-time. The tag manufacturers decompress and organize these messages (typically) into distinct tag data files (e.g., one file per sensor data stream or behavioural activity) and make them available to the tag owners.
3. Typically, the behavioural and physical observations data files either have crudely interpolated locations or no locations associated with each record. The ArgosQC R package uses a statistically robust interpolation to append a location and its uncertainty to each record in these data files. This both provides more accurate locations for each observation and eliminates the need for subsequent users of the data to geolocate tag-observed events or physical observations.


## ArgosQC workflow and features
1. Place holder for this topic
2. ace holder for this topic


## Configuring ArgosQC

## ArgosQC Key Features
https://github.com/ianjonsen/ArgosQC


1. Comprehensive Automated Workflow: ArgosQC now provides a fully automated, end-to-end process. It handles everything from accessing and organizing complex multi-file data structures from vendors (SMRU and Wildlife Computers), to fitting state-space models (SSMs) and finally writing out appended, quality-controlled data.

2. Simplified Execution with New Functions: The process can be run easily with manufacturer-specific functions like smru_qc() and wc_qc(). These functions use a simple configuration file (e.g., test_conf.json) to manage project settings, making the QC process repeatable and easier to manage.

3. Enhanced Data Integration: A key new feature is the ability to collate tag data with associated deployment metadata. The output is then enriched by appending SSM-estimated locations to every tag-measured event record (like CTD profiles, dives, haulouts, and raw Argos/GPS locations) into a single, comprehensive .csv file.

4. Refined Data Filtering: Recent updates (February 2026) include a practical fix to remove erroneous locations originating from the manufacturer's headquarters (e.g., SMRU HQ), a common issue in raw data streams.

5. Improved Data Handling: Recent commits have focused on robustness, including fixes for Wildlife Computers (WC) UUID parsing issues (January 2026) and the implementation of checks to ensure data integrity.

6. Expanded Documentation and Vignettes: The package now features detailed vignettes that guide users through the config file structures and specific workflows for both SMRU and Wildlife Computers data, making it easier to get started and customize the process.


## Feature Request and Bug Report

As an open-source tool under active development (with the last commit on February 12, 2026), user feedback is essential for improving ArgosQC. If you encounter problems or have ideas for new features, you are encouraged to contribute through the following channels:

Report Bugs via GitHub Issues: If you find a bug (e.g., a workflow error, data parsing problem, or unexpected crash), please submit a report through the repository's Issues tab. When reporting, include:

A clear and descriptive title.

A step-by-step description of how to reproduce the issue.

Your session information (output of sessionInfo() in R) and the version of ArgosQC you are using.

Any relevant error messages or log outputs.

Suggest Enhancements: For new feature requests or ideas to improve existing workflows (like support for additional tag vendors or new diagnostic plots), you can also use the Issues tab. Please tag your issue with an "enhancement" label if possible, and clearly explain the proposed feature and its potential use case.

Review Current Priorities: Before submitting, it is helpful to review the Issues page to see if the bug or feature has already been reported or is currently being addressed.

Code Contributions: If you are interested in fixing a bug or adding a feature yourself, please consult the repository's Contributing guidelines (linked on the main page). The standard practice is to fork the repository, create a branch for your changes, and submit a Pull Request for review by the maintainer.

{% include links.md %}
