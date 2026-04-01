---
title: "Near Real Time (NRT) Animal Tagging Location Data Quality Control (QC) Process: SMRU"
teaching: 120
exercises: 0
questions:
- "How to receive metadata & data access from a researcher to set up satellite data harvesting"
- "How to use the metadata to create a config file"
- "How to push that config file somewhere so it can be processed regularly by the RT process"
- "How to process a dataset that is no longer real-time - delayed-mode"
---


## How to receive metadata & data access from a researcher to set up satellite data harvesting for SMRU tags
### Metadata
The minimum metadata required by the QC process is: 1. species common name; 2. species scientific name; 3. release site (e.g., Sable Island); 4. release country; 5. SMRU campaign id(s) (e.g., ct190). Use whatever method for obtaining these metadata from the researcher works for you.

### Data access
Ensure you have the researcher's username and password to access the data on the [SMRU server](https://www.smru.st-andrews.ac.uk/protected/technical.html). The server page is accessible to anyone to view SMRU tag deployments by registered project, but access to data within individual deployment "campaigns" are behind a WAF. 

Once you have the researcher's username and password, these can be entered in the config file `harvest` block.

## How to use the metadata to create a config file
All details for constructing `ArgosQC` config files are in this [Jupyter notebook](https://github.com/ocean-tracking-network/rt-sat-to-obis/blob/add_conda_env/ArgosQC_SMRU_Project_Config.ipynb)

## How to push that config file somewhere so it can be processed regularly by the RT process
Details on how to do this are in this [Jupyter notebook](https://github.com/ocean-tracking-network/rt-sat-to-obis/blob/add_conda_env/ArgosQC_SMRU_Project_Config.ipynb)

## How to process a dataset that is no longer real-time - delayed-mode
Tag datasets that are no longer real-time (deployments have ended) may be processed in the same manner as real-time datasets, except that the QC process only needs to be run once.

