Fathom Live Buoy Data
- [ ] - NAME add label *'loading records'*
- [ ] - NAME load deployment metadata in a receiver ticket (**issue link here**)
- [ ] - NAME load raw files to c_tables [detections, diagnostics, environmental] (`Live Buoy Processing` notebook)(**:fish: put raw table names here)** 
:stop_sign: Stop at Create buoy locations table cell
- [ ] - NAME upload raw detections to project folder (OTN members.oceantrack.org, FACT RW etc) if needed
- [ ] - NAME assign to OTN 
- [ ] - NAME create raw live_buoy_locations table and load locations (`Live Buoy Processing` notebook)
- [ ] - NAME load to detections_YYYY (`Live Buoy Processing` notebook) **:fish: put years affected here**
- [ ] - NAME verify detections_yyyy (looking for duplicates)(`Live Buoy Processing` notebook)
- [ ] - NAME load to sensor_match_yyyy (`Live Buoy Processing` notebook) **:fish: put sensor_match years that were affected here**
- [ ] - NAME manually check for open, unverified receiver metadata, STOP if it exists! (**put Gitlab issue number here**)
-----
- [ ] - NAME load to otn_detections_yyyy (`Live Buoy Processing` notebook)
- [ ] - NAME update live buoy detection locations (`Live Buoy Processing` notebook)
- [ ] - NAME verify otn_detections_yyyy and load sentinel records (`Live Buoy Processing` notebook)
- [ ] - NAME load hub locations to otn_detections_yyyy (`Live Buoy Processing` notebook)
- [ ] - NAME check for missing receiver metadata (`detections-3b` notebook)
- [ ] - NAME check for missing data records (`detections-3c` notebook)
- [ ] - NAME label issue with *'Verify'*
- [ ] - NAME pass issue to analyst for final steps
- [ ] - NAME check for double reporting (`detections verification script`)
- [ ] - NAME match tags to animals (`detections-4 notebook`)
- [ ] - NAME do sensor tag processing (only done by OTN as it requires vendor specifications)
- [ ] - NAME update detection extract table


metadata: **(link deployment metadata issue here)**

detections: **(link detectons CSV here)**

diagnostics: **(link diagnostics CSV here)**

environmental: **(link environmental CSV here)**


Steps to obtain files:
1. access Fathom Central Portal
1. go to Download tab
1. select region
1. select csv file type
1. select **detections**, including date range
1. name and download file
1. select **diagnostics**, same date range, download
1. select **environmental**, same date range, download
