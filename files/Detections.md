Detections
- [ ] - NAME add label *'loading records'*
- [ ] - NAME load raw detections and events `(detections-1` notebook and `events-1` notebook **OR** `Batch Fathom Export` notebook and `detections-1` notebook) **:fish:(put table names here)**
- [ ] - NAME upload raw detections to project folder (OTN members.oceantrack.org, FACT RW etc) if needed
- [ ] - NAME verify raw detections table (`detections-1` notebook)
- [ ] - NAME load raw events to events table (`events-2` notebook)
- [ ] - NAME load to detections_yyyy (`detections-2` notebook) **:fish:(put detection years that were loaded here)**
- [ ] - NAME verify detections_yyyy (looking for duplicates) (`detections-2` notebook)
- [ ] - NAME load to sensor_match_yyyy (`detections-2` notebook) **:fish:(put sensor years that were loaded here)**
- [ ] - NAME timedrift correction for affected detection and sensor years (`detections-2b` notebook)
- [ ] - NAME verify timedrift corrections (`detections-2b` notebook)
- [ ] - NAME manually check for open, unverified receiver metadata, **STOP** if it exists! **(put Gitlab issue number here)**
------
- [ ] - NAME load to otn_detections_yyyy (`detections-3` notebook) **:fish:(put affected years here)**
- [ ] - NAME verify otn_detections_yyyy (`detections-3` notebook)
- [ ] - NAME load sentinel records (`detections-3` notebook) 
- [ ] - NAME check for missing receiver metadata (`detections-3b` notebook)
- [ ] - NAME check for missing data records (`detections-3c` notebook)
- [ ] - NAME load download records (`events-3` notebook)
- [ ] - NAME verify download records (`events-3` notebook)
- [ ] - NAME process receiver configuration (`events-4` notebook)
- [ ] - NAME label issue with *'Verify'*, removed label *'loading records'*
- [ ] - NAME pass issue to analyst for final steps
- [ ] - NAME check for double reporting (`detections verification script`)
- [ ] - NAME match tags to animals (`detections-4` notebook)
- [ ] - NAME do sensor tag processing (`detections-5` notebook) - only done if vendor specifications are available
- [ ] - NAME update detection extract table

**detections files/path:**
