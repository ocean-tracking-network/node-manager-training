---
title: "Virtual Machine Specs for OTN Database Node"
teaching: 10
exercises: 0
questions:
- "What does a new Node need to get started?"
objectives:
- "Understand what technical specification are required for a Node"
- "Understand the format of Detection Extracts"
keypoints:
- "There are key requirements for a Node"
---

## Virtual Machine Specs for OTN Database Node

To setup an OTN node, a network first has to create technical space for the database, website, and associated infrastructure. If contracting a cloud-based service, the below breakdown of requirements will be important to keep in mind.

## ## Service-level breakdown

#### PostgreSQL 14+ with PostGIS and dblinks
 - Minimum RAM 1GB 
 - Storage 100MB for installation and 200GB - 1 TB for medium to large data projects.

#### Tomcat Services (Optional) 
 - Geoserver 2.28.x+  (for publication of projects, contacts, and receiver locations)
	 - Minimum RAM required 2GB with 500 MB needed for base installation.  
	 - Recommended RAM from 4-8 GB.
	 - Storage is shared between the PostgreSQL database tables.
 - Erddap 2.23.x+  (for publication of all relevant tracking data for published projects)
	 - Minimum system specs: 2 GB of ram with 500 GB of storage depending on the amount of data stored.
	 - Recommend RAM from 4 - 8 GB based on usage requirements.

#### Plone 6.1.x (file management and content management system)
 - Minimum RAM required 2 GB.
 - Recommended RAM is above 2 GB
 - Diskspace needed for installation 600 MB
 - Maximum Space needed depends on the amount of data loaded to Plone. Roughly equal to the amount of database storage allocated.

## Full installation of the OTN stack - recommended specs
 - RAM: 16GB+
 - Storage: 1TB+ for medium to large data projects. Recommended to use SSD based storage for access speed. 
 - System Backups should be configured / purchased and confirmed to be enabled.
 - Linux operating system (Debian or RedHat based)
 - Containerized (Docker) installs will require additional processing overhead, more resources should be allocated for containerized deployments of the OTN system.

{% include links.md %}

