---
title: "Deployment Verification"
teaching: 15
exercises: 0
questions:
- "How to verify deployment metadata in the Database?"
objectives:
- "Understand the Deployment Verification workflow"
- "Learn how to use the `verification_notebooks\Deployment Verification` notebook"
- "Learn some known issues and troubleshooting tips "
keypoints:
- "Review the Gitlab ticket and run the Deployment Verification notebook"
---

After deployment metadata is loaded the Gitlab ticket will be assigned to a **different** person for verification.
Below is an example of the last step in the ticket to be completed.
- Note: `verification_notebooks\Deployment Verification` notebook automates verification_scripts/`deploy-4 verification script` 
which is still available in case of programing error or notebook/browser becomes unresponsive. 

~~~
Tag Metadata

...
- [ ] - NAME check for double reporting (`deploy-4 verification script`)

**tag metadata txt file**
~~~
{: .language-plaintext .example}


# The Deployment Verification Workflow 
When a Deployment (often with Detections) verification ticket is assigned to you follow below steps to complete the tasks.  

### Assess the Ticket

Things to check:

1. Have all the previous steps been completed?  
1. Any unresolved issues linked to this ticket or in the comments?
1. Take note of the project code and the OTN or partner node.   


### Run the Tag Verification Notebook

The `Tag Verification` notebook can be found under `verification_notebooks`
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

#### Re-run moorings verification from IPython cell
- This cell runs the same checks as in the `deploy` notebook.
- Review any unfolded warning or error messages.

#### Run double reporting checks cell
- This step ensures no duplicates of the receiver metadata (in terms of serial number, location and date time) within and across all OTN and partner nodes.
- The know issue for this and all other cross-node checks is: Brazil node is offline thus 
there will be error about connection time out with BRZ node.   

#### Report and fix found issues
- Copy all warnings and errors (excluding the above known issues) to the comments of the Gitlab ticket.
- Try to resolve/fix issues as listed below:

| Issue                                            | Cause / Explaination                                          | Solution/Fix                                        |
|--------------------------------------------------|---------------------------------------------------------------|-----------------------------------------------------|
| Missing vendor specs for the following receivers | The product specification has not been loaded into OTN database | Remind DAQ team to require and load the missing spec later |
| Missing tag vendor specs for the following TRANSMITTERs |The product specification has not been loaded into OTN database | Remind DAQ team to require and load the missing spec later |


- For other issues message or assign the ticket to the data team for support. 

#### Complete Gitlab tasks 

- If no issues found or all issues are resolved check-off the checkbox and close the Gitlab ticket.  
