---
title: "Introduction to Nodes"
teaching: 30
exercises: 0
questions:
- "What is an OTN-style Database Node?"
- "What is expected from a Node Manager?"
- "Who is this training for?"
- "What is the schedule for the next several days?"
objectives:
- "Understand the relationship between OTN and its Nodes."
- "Ensure attendees have required background information."
keypoints:
- "Your Node is fully compatible with all others like it."
- "A well-connected Node Manager is essential."
- "OTN staff are always availble to support Node Managers."
---

## What is a Node?

OTN partners with regional acoustic telemetry networks around the world to enable detection-matching across our communities. An OTN Node is an exact copy of OTN's acoustic telemetry database structure, which allows for direct cross-referencing between the data holdings of each regional telemetry sharing community. The list of OTN Nodes is available here: https://members.oceantrack.org. Data only needs to be reported to one Node in order for tags/detections to be matched across all.

### How does a Node benefit its users?

OTN and affiliated networks provide automated cross-referencing of your detection data with other tags in the system to help resolve "mystery detections" and provide detection data to taggers in other regions. OTN Data Managers extensively quality-control submitted metadata to ensure the most accurate records possible are stored in the database. OTN's database and Data Portal website are well suited for archiving datasets for future use and sharing with collaborators. The OTN system includes pathways to publish datasets with OBIS, and for sharing via open data portals such as ERDDAP and GeoServer. The data-product format returned by OTN is directly ingestible by analysis packages including glatos and resonATe. OTN offers continuous support for the use of these packages and tools.

Below is a presentation from current Node Managers, describing the relationship between OTN and its Nodes, the benefits of the Node system as a community outgrows more organic person-to-person sharing, as well as a realistic understanding of the work involved in hosting/maintaining a Node.

[PDF](../Resources/Pye - OTNDC, OTN Nodes and Data Partners.pptx)

## Node Managers

To date, the greatest successes in organizing telemetry communities has come from identifying and working with local on-the-ground Node Managers for each affiliated Node. The trusted and connected 'data wranglers' have been essential to building and maintaining the culture and sense of trust in each telemetry group.

In order to be successful as a Node Manager in your region, here are a few tips and guidelines:

1. Ensure you set aside time each week to wear your 'Node Manager hat'.
2. Familiarize yourself with the metadata reporting templates, and follow carefully the formats required for each variable.
3. Ensure you have continuous communication with the OTN data team so you are able to align your detection matching with all other Nodes, and keep your local toolbox up to date.
4. Ensure you have consistent communication with your local telemetry community - knowing who's who is important for relationship building.
5. Be willing to learn and ask questions - we are always trying to improve our tools and processes!

No previous coding or data management experience is required! Anyone who is willing to put in the work to become a Data Manager can be successful. Being involved in the telemetry community as a researcher (or affiliate) is enough to get you started with 'data wrangling' in your region.

## Node Training

Each year OTN hosts a training session for Node Managers. This session is not only for new Node Managers, but also a refresher for current Node Managers on our updated tools and processes.

This is a hands-on course, participants will be using the tools to practice loading telemetry data with us, using a Training Node we have built for this purpose. This means you will need to install all required software and devote full attention for the next several days.

Here are the general topics that will be covered:
- OTN Node structure and database maintenance
- Data loading workflow: from metadata to detection extracts, and how we track progress in GitLab
- Practice interfacing with an OTN Node database in DBeaver, using SQL scripts
- Practice using OTN's Nodebooks to quality control, process and verify records, using python and jupyter notebooks
- Overview of OTN's Data Push process, and how Node Managers are involved
- Data Policy guidelines as a Node Manager

If you do not intend on learning how to load data to an OTN-style Node (and would prefer to be a spectator) please let us know, so we can identify who our hands-on learners will be.

A great resource for Node Managers as they get started will be OTN's FAQ page - https://members.oceantrack.org/faq. Your local telemetry community will likely have many questions about the Node and how it works, and the FAQs can help answer some of these questions.

{% include links.md %}
