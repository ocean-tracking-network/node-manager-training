
---
title: "Moving Platform: Mission Metadata, Telemetry and Detection Loading"
teaching: 60
exercises: 0
questions:
- "How do I load moving platform missings, telemetry data, and detections into the Database?"
  
objectives:
- "Understand how to use the GitLab checklist"
- "Understand the workflow for detection data in the OTN system"
- "Learn common errors and pitfalls that come up when loading detections"
keypoints:
- "Its important to handle errors when they come up as they can have implications on detections"
- "OTN finishes off detections Issues by running Matching and sensor tag processing"
---

Once `deployment metadata` has been processed for a project, the related detections may now be processed. Detection data should be reported to the Node as a collection of raw, **unedited** files. These can be in the form of a zipped folder of `.VRLs`, a database from Thelma Biotel or any other raw data product from any manufacturer. The files contain only transmitter numbers and the datetimes at which they were recorded at a specific receiver. The `tag metadata` and `deployment metadata` will provide the associated geographic and biological context to this data.

# Submitted Records

Immediately, upon receipt of the data files, a new GitLab Issue should be created. Please use the `Detections` Issue checklist template.

Here is the Issue checklist, for reference:

~~~
