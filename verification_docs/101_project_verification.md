---
title: "New Project Verification"
teaching: 15
exercises: 0
questions:
- "How to verify a newly created project in the Database?"
objectives:
- "Understand the New Project Verification workflow"
- "Learn how to use the `verification_notebooks\Project Verification` notebook"
- "Learn some known issues and troubleshooting tips "
keypoints:
- "Review the Gitlab ticket and run the Project Verification notebook"
---

After a new project is created the Gitlab ticket will be assigned to a **different** person for verification.
Below is an example of the last steps in the ticket to be completed.
~~~
Project Metadata

...
- [ ] - NAME verify project in database
- [ ] - NAME pass issue to OTN daq staff
...

**project metadata txt file**
~~~
{: .language-plaintext .example}


# The New Project Verification Workflow 
When a project verification ticket is assigned to you follow below steps to complete the tasks.  

### Assess the Ticket

Things to check:

1. Have all the previous steps been completed?  
1. Any unresolved issues linked to this ticket or in the comments?
1. Which OTN or partner node was the project created in.   


### Run the Project Verification Notebook

The `Project Verification` notebook can be found under `verification_notebooks`
folder in ipython-utilities project.

#### Imports cell
This section will be common for most Nodebooks: it is a cell at the top of the notebook where you will import any required packages and functions to use throughout the notebook. It must be run first, every time.
zz
#### Enter engine connection cell
You will have to edit one section: `engine = get_engine()`
- Within the open brackets you need to open quotations and paste the path to your database `.kdbx` file which contains your login credentials.
- On MacOS computers, you can usually find and copy the path to your database `.kdbx` file by right-clicking on the file and holding down the "option" key. On Windows, we recommend using the installed software Path Copy Copy, so you can copy a unix-style path by right-clicking.
- The path should look like `engine = get_engine('C:/Users/username/Desktop/Auth files/database_conn_string.kdbx')`.

#### Specify schema cell
- Replace the placeholder string: `'schema'` with the lowercase project code (can be found in the title or project metadata form).

#### Re-run project verification from IPython cell
- This cell runs the same checks as in the `Create and Update Projects` notebook.
- Review any unfolded warning or error messages.
- Some common known issues (no actions required):
1. In Database match check section ignore errors about not-matching below not matching pairs:
   1. otnunit vs. otn 
   2. OTN vs. OTN-Global
   
2. In DB location and host check ignore errors about below not-matching pair:
   1. db.oceantrack.org vs. db.load.oceantrack.org
3. Verify information in Checking contacts section: any missing or mal-formatted fields. Ask DAQ team if not sure.
4. Verify scientific names on https://www.marinespecies.org/ 

#### Run double reporting checks cell
- This step ensures the project code is unique across all OTN and partner nodes.
- The know issue for this and all other cross-node checks is: Brazil node is offline thus 
there will be error about connection time out with BRZ node.   

#### Complete Gitlab tasks 
- Document and report issues found:
  1. Copy all warnings and errors (excluding the above known issues) to the comments of the Gitlab ticket.
  2. Message or assign the ticket to the data team for support. 

- If no issues found check-off two checkboxes Gitlab ticket. Close or assign the ticket to DAQ team as in the ticket's checklist. 
