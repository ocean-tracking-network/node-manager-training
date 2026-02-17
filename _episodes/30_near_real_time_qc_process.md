---
title: "Near Real Time (NRT) Animal Movement Location Data Quality Control (QC) Process"
teaching: 120
exercises: 0
questions:
- "What are NRT data and NRT data sources/vendors?"
- "Why NRT data needs QC?
- "What is ArgosQC package?"
- "ArgosQC's workflow/features"
- "Satellite vendors: SMRU and WildlifeComputers"
- "How to configure ArgosQC (aniMotum) model parameters for various species?"
- "What are the mandatory import files for ArgosQC?"
- "What are the output files and how to interpreate ArgosQC results and diagnoses?"
- "What are the signs, and how do you fine-tune model parameters?"



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

ArgosQC for near-real-time data is an essential automated process that uses state-space models (calling the underneath aniMotum package) to filter noisy satellite location data from vendors like SMRU and Wildlife Computers. Its effectiveness relies on configuring species-specific movement parameters and interpreting diagnostic outputs to produce reliable animal movement tracks for ecological research.

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

