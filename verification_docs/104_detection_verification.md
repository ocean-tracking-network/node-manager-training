---
title: "Detection Verification"
teaching: 30
exercises: 0
questions:
- "How to verify detection in the Database?"
- "How to match tags to animals?"
- "How to process sensor tag?"
- 
objectives:
- "Understand the Detection Verification workflow"
- "Learn how to use the `verification_notebooks\Detection Verification` notebook"
- "Learn how to match tags to animals using the `detections - 4 - match otn_detections to tagging specifications` notebook"
- "Learn sensor tag processing using the `detections - 5 - sensor tag processing` notebook"
- "Learn some known issues and troubleshooting tips "

- keypoints:
- "Review the Gitlab ticket and run the Deployment Verification notebook"
- "Run `detections - 4 - match otn_detections to tagging specifications` notebook"
- "Run `detections - 5 - sensor tag processing` notebook"
---

After deployment metadata and detections are loaded the Gitlab the ticket will be assigned to a **different** person for verification.
Below is an example of the steps in the ticket to be completed.
- Note: `verification_notebooks\Detection Verification` notebook automates verification_scripts/`detections verification script` 
which is still available in case of programing error or notebook/browser becomes unresponsive. 

~~~
Detections

...
- [ ] - NAME check for double reporting (`detections verification script`)
- [ ] - NAME match tags to animals (`detections-4` notebook)
- [ ] - NAME do sensor tag processing (only done if vendor specifications are available)
- [ ] - NAME update detection extract table

**detections files/path:**
~~~
{: .language-plaintext .example}


# The Detection Verification Workflow 
When a Detection (often with Detections) verification ticket is assigned to you follow below steps to complete the tasks.  

### Assess the Ticket

Things to check:

1. Have all the previous steps been completed?  
1. Any unresolved issues linked to this ticket or in the comments?
1. Take note of the project code and the OTN or partner node.   


### Run the Detection Verification Notebook

The `Detection Verification` notebook can be found under `verification_notebooks`
folder in ipython-utilities project.

#### Imports cell
This section will be common for most Nodebooks: it is a cell at the top of the notebook where you will import any required packages and functions to use throughout the notebook. It must be run first, every time.

#### Enter engine connection cell
You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

#### Specify schema cell
- Replace the placeholder string: `'schema'` with the lowercase project code (can be found in the title or project metadata form).

#### Re-verify the detection metadata cell
- This cell runs the same checks as in the `detections` and `events`notebooks .
- Review any unfolded warning or error messages.
- Ask DB team about large detection count difference in the `Check detection counts:` section.
Note: if `Check detection counts:` or `Check if schema.c_events_yyyy have been loaded into events table:` freeze your browser
run the `verification_scripts\detection_verification.sql`: `--Check if all download records have been loaded` 
and `--replace <yyyy> and <next_yyyy> with years, do for each year that has detections_yyyy` section respectively.

#### Run double reporting checks cell
- This step ensures no duplicated detections within and across all OTN and partner nodes.
- The know issue for this and all other cross-node checks is: Brazil node is offline thus 
there will be error about connection time out with BRZ node.   

#### Report and fix found issues
- Copy all warnings and errors (excluding the above known issues) to the comments of the Gitlab ticket.
- Try to resolve/fix issues as listed below:

| Issue                                            | Cause / Explaination                                          | Solution/Fix                                        |
|--------------------------------------------------|---------------------------------------------------------------|-----------------------------------------------------|
|  |   |
|  | |  |

- For other issues message or assign the ticket to the data team for support. 


### Run the detections - 4 - match otn_detections to tagging specifications Notebook

The `detections - 4 - match otn_detections to tagging specifications` notebook can be found in ipython-utilities project.

#### Imports cell
This section will be common for most Nodebooks: it is a cell at the top of the notebook where you will import any required packages and functions to use throughout the notebook. It must be run first, every time.

#### Enter engine connection cell
You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

#### Specify schema cell
- Replace the placeholder string: `'schema'` with the lowercase project code (can be found in the title or project metadata form).

#### # Year of the detection table to match cell
- Specify one year at a time as noted in the `comment in issue what detection years were loaded` step of this ticket.  

#### # Summary of tags to be matched, with extended enddate (detailed report) cell
- List candidates to be matched including project (trackercode), tags, animals and dates.

#### # Simplified report cell
- Summarize the detection counts by project (trackercode).

#### # Choose whether to exclude or include the list of codes (in below cells) and the next two cells
- Prompt with `include` and `exclude` options for the projects (trackercodes) to be matched.
- Display `Codes to include:` or `Codes to exclude:` depends on the previous selection.
- Before making selection go to Gitlab to search each project (trackercode). Record open `tag` tickets for the detection year 
and ask DB team if the code should be excluded. 
- Select projects (trackercodes) and run the next `codes_to_use=` cell.

#### # Months to extend and the next cell
- Prompt user with the `Months to extend by` number picker.
- Inout the number of months (usually set to 3) months as the extension to enddate of a tag.
- Run the next cell to save above selection as a variable `months_to_extend_enddate_for_update`. 

#### # Match the tags to the detection records cell
- Will match the selected projects (trackercodes) for the year.


#### # #Add to detection extract list cell
- Update the `gitlab_issue_url` (to current Gitlab ticket) and `push_date` (as DB team) variables.
- Run the cell to generate detection extracts.




#### Complete Gitlab tasks 

- If no issues found or all issues are resolved check-off the checkbox and close the Gitlab ticket.  
