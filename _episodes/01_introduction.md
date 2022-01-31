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
- "Understand the relationship between OTN and its Nodes"
- "Ensure attendees have required background information"
keypoints:
- "Your Node is fully compatible with all other like it"
- "A well-connected Node Manager is essential"
- "OTN staff are always availble to support Node Managers"
---

## What is a Node?

OTN has partnered with several regional acoustic telemetry networks around the world to enable detection-matching across our communities. An OTN Node is a copy of OTN's database structure which allows for direct cross-referencing between every one of these affiliated groups. You can see the list of OTN Nodes here: https://members.oceantrack.org. You only need to report your data to one Node in order for your tags/detections to matched to all Nodes.

### What is the benefit to users?

OTN and affiliated networks provide automated cross-referencing of your detection data with other tags in the system to help resolve "mystery detections" and provide detection data to taggers in other regions. OTN's Data Managers will also extensively quality-control your submitted metadata for errors to ensure the most accurate records possible are stored in the database. OTN's database and Data Portal website are excellent places to archive your datasets for future use and sharing with collaborators. We offer pathways to publish your datasets with OBIS, and via open data portals like ERDDAP, GeoServer etc. The data-product format returned by OTN is directly ingestible by analysis packages such as glatos and resonATe for ease of analysis. OTN offers support for the use of these packages and tools.

Below is a presentation from current Node Managers, decribing the relationship between OTN and its Nodes. The content will include comments about the benefits of the Node system as well as a realistic understanding of the work involded in hosting/maintaining the Node.

**link the presentation here when its available**

## Node Managers

OTN has found great success in apointing local on-the-ground Node Managers for each affilated Node. These local data wranglers have been esstential to building and maintaining trust in the telemetry communities in which they serve.

In order to be successful as a Node Manager in your region, there are a few tips and guidelines:

1. ensure you set aside time each week to wear your "Node Manager hat"
2. familiarize yourself with the metadata reporting templates, and pay great detail to the formats required for each variable
3. ensure you have consistent communications with OTN's data team so you are able to align your detection matching with all other Nodes, and keep your local toolbox up to date.
4. ensure you have consistent communication with your local telemetry community - knowing who's who is important for relationship building.
5. be willing to learn and ask questions - we are always trying to improve our tools and processes!

No previous coding or management experience is required! Anyone who is willing to put in the work to become a Data Manager will be successful. Being involded in the telemtry community as a researcher (or affilate) will be enough to get you started with " data wrangling" in your region.

## Node Training

Each year OTN hosts a training session for Node Managers. This session is not only for new Node Managers, but also a refresher for current Node Managers on our updated tools and processes.

This is a hands-on course: you will be expected to practice loading data with us, using a Training Node we have built for this purpose. This means you will need to install all required software and devote full attention for the next several days.

In general, here are the topics to be covered:
- OTN Node structure and database maintenance
- OTN's data loading workflow: from metadata to detection extracts, and how we track progress in Gitlab
- Practice interfacing with a Node-style database in DBeaver, using SQL scripts
- Practice using OTN's jupyter Nodebooks to QC, load, and process data/metadata
- Overview of OTN's Data Push process, and your roll in that
- Data Policy guidelines as a Node Manager

If you do not intend on being involved in loading data to an OTN-style Node (and would prefer to be a spectator) please let us know, so we can identify who our hands-on learners will be.

A great resource for Node Managers as they get started will be OTN's FAQ page - https://members.oceantrack.org/faq. Your local telemetry community will likely have many questions about the Node and how it works, which may include some of these questions.

{% include links.md %}
