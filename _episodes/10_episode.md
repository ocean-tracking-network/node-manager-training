---
title: "The Push"
teaching: 60
exercises: 0
questions:
- "What it the Push?"
- "What do I need to do as a node manager for the push?"
- "What are the end products of the push?"
objectives:
- "Understand a basic overview of the push"
- "Understand what a node managers responsibilities are during the push"
- "Understand what detection extracts are
keypoints:
- "The Push is when we verify all the data in the system, fix any issue, and then send it out to researchers so they can use it"
- "As node managers its your responsibility to get the data into the system so OTN can verify and get it ready to be sent out"
- "Detection extracts are the main end product of the push"
---

## What it the Push?

The Push is when the OTN data system is reverified and any new relevant information is sent to researchers. New data being brought in is cut off so that what's in the system can be reliably verified. This way any issues found can be fixed and the data can be in the best form based on the information available at that moment. Once verification is done detections are matched across nodes and detection extracts are sent out to researchers. This is also the time when publication tables such as discovery, erddap, and geoserver are updated.

## When is the Push 

Push events happen three times a year. They start on the third Thursday of the push month which are February, June, and October. This date would be the date that OTN would like to cut off all data coming into the system. We have this schedule to ensure dates are known well in advance so everyone can better prepare and schedule in advance. 

Push schedule for till 2023:
June 23, 2022
October 20, 2022
February 16, 2023
June 15, 2023
October 19, 2023

## What do I need to do as a node manager for the push?

Node managers have two main jobs during The Push. The first job is to get the node’s data loaded in time for the push. Data will be coming to you throughout all times so we do encourage you to try and continuously load data throughout the year. Closer to push dates you will get a larger amount of data coming in so it is good to get ahead and avoid a backlog. The second job node managers have is to create and send out detection extracts when OTN gives the go ahead that they are ready to be made. This will be done using the detections - create detection extracts notebook.

## Detection extracts

Detection extracts are the main output of the push. They are files that contain relevant detection data. There are multiple types of detection extracts OTN creates: 'qualified' which contain detections matched to animals of other projects, 'unqualified' which contain the project's unmatched or mystery detections which are not associated with any deployed tag, 'sentinel' which contain the detections matched to test or transceiver tags, and 'tracker' which contain animal metadata that have been matched to detections. Detection extracts are ready for use in many analysis packages, such as glatos and resonate. 
