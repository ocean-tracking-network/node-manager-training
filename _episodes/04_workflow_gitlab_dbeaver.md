---
title: "Data Loading Workflow"
teaching: 30
exercises: 15
questions:
- "How does a Node Manager receive data?"
- "How does a Node Manager track their To-Do list?"
- "How can a Node Manager interact with their database directly?"
objectives:
- "Understand the data-loading workflow"
- "Understand how to create and use GitLab Issues"
- "Understand how to access and query your database tables"
- "Understand how to use the `AUTH - Create and Update` notebook to maintain your database credentials file"
keypoints:
- "Node-members cannot access the database, you are the liason"
- "Data submissions and QC processes should be trackable and archived"
- "OTN is always here to help with any step of the process"
---

Data Managers receive data from a researcher and then begin a several-step process of QA/QC and matching of data.

1. Records are received, and immediately a GitLab Issue is created.
1. Data are QA/QC'd using the OTN Nodebook tools (covered in detail later in the curriculum), and all progress is tracked in GitLab. Feedback between Data Manager and researchers happens at this stage, until data is clean and all GitLab tasks are completed.
1. The successful processing of records can be evaluated by checking the database tables using DBeaver, and SQL queries.

The process flow is as follows:
```mermaid
flowchart LR
    data_start(( )) --> get_data(Receive metadata
from researchers)
    style data_start fill:#00FF00,stroke:#00FF00,stroke-width:4px
    get_data --> gitlab(Create Gitlab issue
with template)
    gitlab --> viz{Visually inspect,
does metadata have errors?}
    viz -- yes --> req(Request corrected data
from researchers)
    req --> end1(( ))
    style end1 fill:#FF0000,stroke:#FF0000
    viz --no --> run_checklist(Run data through checklist)
    run_checklist --> otn_part(Pass to OTN for
final verification)
    otn_part --> end2(( ))
    style end2 fill:#FF0000,stroke:#FF0000
	```

## Researcher data submission

There are many ways to receive data from researchers in your community/group. Find and make official the way that works for your community and ensure that that becomes standard practice for reporting to your Node.

### File management website

The most common way to receive data and metadata from a researcher is through some type of file management website. This will require either an email notification system for the Node Manager or **constant** checking to look for new submissions.

OTN-managed Nodes can always use the same Plone file management portal software that OTN itself uses to create and maintain private-access data repository folders into which researchers can deposit their data and metadata. These private folders also serve as the location where Detection Extracts are distributed to users, when available.

The FACT Network currently uses a custom instance of Research Workspace for the same purpose.

The ACT and GLATOS Networks use a custom data-submission form managed through their networks' web sites.

Its common for groups of researchers to use DropBox, Google Drive, or something similar to share data/metadata when the Network is still small. This can be a great, accessible option but the caveat is that is is much more difficult to control access to each individual folder to protect the Data Policy, and it may be difficult to determine when new data has been submitted.

### Email-only submission

Generally, each Node Manager has an email address for communicating with their network's data submitters (ex: Data @ TheFACTNetwork . org). This is a great way to ensure all Node-related emails are contained in the same account in the case of multiple Node Managers or the succession of a new Node Manager. With proper email management, this can be a very successful way to ask Node-users to submit their data/metadata to your Node.

It is **not** recommended to use a personal email account for this, since all the files and history of the project's data submissions will be lost if that Manager ever moves away from the role. If the account is hosted at an institution, it may be advisable to submit requests to raise institutional limits on things like email storage in advance.

# Documenting data submission

Using one of the suggested means above, a user has submitted data and metadata to the Node Manager. Now what?

OTN uses GitLab Issues with templates of task-lists to ensure we NEVER forget a step in data loading, and that no file is ever lost/forgotten in an inbox.

Immediately upon receipt of a data file, you are advised to login to OTN's GitLab (https://gitlab.oceantrack.org). You will have a project for your Node named <YOURNODE-DAQ>. This is where you will navigate to. You may want to bookmark this webpage!

Once on the GitLab project page, you should navigate to the **Issues** menu option, on the left side. Think of your GitLab issues as your running "TODO List"! You will want to create a new Issue for each piece of data that is submitted.

*NOTE: GitLab Issues are often referred to as "tickets"*

### Creating GitLab issues

By choosing the **New Issue** button in the top-right of your screen, you will be taken to a new, blank, issue form. To fill out the fields you will need to do the following:

- Title: Write the project name/code, the type of data submitted, and the submission date, this makes the ticket searchable in the future (eg: `HFX tag metadata 2022-02`)
- Type: No need to edit this field, should be type `Issue`.
- Description: **1)** There are pre-made *Templates* to choose from here, using the drop down menu. Ensure you choose the relevant checklist for the type of data
 that was submitted (eg: `Tag_metadata`). This will populate the large description field! **2)** Ensure you include the link to the submitted data file
OR use the `Attach a file` option to attach a copy of the submitted data file to the issue.
- Assignee: Assign to yourself if this is a task for you, or to anyone else who you would like to delegate to
- Milestone: These are the upcoming Data Push dates. You should choose the nearest future PUSH date as the Milestone for this issue.
- Labels: This is for your reference - choose a label that will help you remember what stage of processing this issue is in. Some common examples include `Needs QC`, `Waiting for Metadata`, `Waiting for VRLs`, `Request PI Clarification` etc. You can create new labels at any time to help sort your tickets.

Now, with all information completed, you can select **Create Issue**.

### Using GitLab to track progress

As you approach the deadline for data-loading, before a data PUSH, you should begin to work on your Issues which fall under that Milestone. When you open an issue, you will be able to see the remaining tasks to properly load/process that data along with the name of the OTN Nodebook you should use to complete each task.

Keep GitLab open in your browser as you work through the relevant Nodebooks. You should check-off the tasks as you complete them, and insert any comments you have into the bottom of the ticket. Comments can include error messages from the Nodebook, questions you have for the researcher, any re-formatting required, etc. At any time you can change the `Labels` on the issue, to help you remember the issue's status at-a-glance.

Once you are done for the day, you'll be able to come back and see exactly where you left off, thanks to the checklist!

You can tag anyone from the OTN Data Team in your GitLab issue (using the `@NAME` syntax). We will be notified via email to come and check out the Issue and answer any questions that have been commented.

Once you have completed all the tasks in the template, you can edit the `Assignee` value in the top-right corner, and assign to someone from OTN's Database team (currently, Angela or Yinghuan). They will complete the final verification of the data, and close the issue when completed. At this time, you can change to the `Verify` issue label, or something similar, to help visually "mark it off" your issue list on the main page.

## GitLab practice

At this time we will take a moment to practice making GitLab Issues, and explore other pages on our GitLab like, `Milestones`, `Repository`, `Snippets`, and `Wiki`.

## Database access

As part of the OTN workflow, once we have used the OTN Nodebooks, it may be prudent to use a database client like DBeaver to view the contents of your database Node directly, and be sure the data was indeed loaded as expected.

DBeaver is an open-source application for interacting directly with databases. There are lots of built-in tools for quick query-writing, and data exploration. We will assume that workshop attendees are novices in using this application.

### Connecting to your database

For this training we will connect to a Node Training test database, as practice. Once you open DBeaver, you will need to click on the `Database` menu item, and choose `New Database Connection`. A popup will appear, and you will choose the `PostreSQL` logo (the elephant) then click Next. Using the `.auth` file provided to you by OTNDC you will complete the following fields:

- Host: this will be something like `matos.asascience.com` for your DB, but we will use the IP address: `129.173.48.161` for our Node Training DB.
- Database: this will be your database name, something like `pathnode`. For training, it will be `node_training`.
- Port: this is specified in your `.auth` file and will be four digits. For training, this port will be set to `5432`.
- Username/Password: your personal username and password, as found on your `.auth` file.

Next you choose `Test Connection` and see if it passes the tests. If so, you can choose `Finish` and you're now connected to your database!

On the left-side you should now see a `Database Navigator` tab, and a list of all your active database connections. You can use the drop down menu to explore all the `schemas` aka: collections stored in your database. You can even view each individual table, to confirm the creation steps in the Nodebooks were successful!

### Writing a query in DBeaver

If you wish to write an SQL query to see a specific portion of your already-loaded data, you should first open a new SQL console. Choose `SQL Editor` from the top menu, then `New SQL Script`. A blank form should appear.

While writing SQL is out of the scope of this course, there are many great SQL resources available online. The general premise involves creating conditional `select` statements to specify the data you're interested in. ex: `select * from hfx.rcvr_locations where rcv_serial_no = '12345';` will select all records from the HFX schema's rcvr_locations table, where the serial number is 12345.

To run a query, you ensure your cursor is on the line you want to run, then you can either 1) right-click, and choose Execute, or 2) press CTRL-ENTER (CMD-ENTER for Mac). The results of your query will be displayed in the window below the SQL console.

OTN is here to support you as you begin to experiment with SQL queries, and the OTN database structure, and can help you build a library of helpful custom queries that you may want or need.

# Database Practice

Let's take a moment to explore some of the tables in the Node Training database, and write some example SQL queries.

# Connecting to your Database from the Nodebooks

Now that we have explored and set up some of the tools needed to work as a Node Manager, we can begin preparing our Nodebook connection files. To enhance security, OTN uses encrypted, password-protected `.kdbx` files to store login credentials for your database. To create these, we have developed an interactive `AUTH - Create and Update` Nodebook.

1. Open the OTN Nodebooks
	* **MAC**: Open your terminal, and navigate to your ipython-utilities directory, using `cd /paht/to/ipython-utilities`. Then, run the command: `jupyter notebook --config="nb_config.py" "0. Home.ipynb"` to open the Nodebooks
	* **WINDOWS**: Double-click the `start-jupyter.bat` file in your ipython-utlities folder, which will open the Nodebooks.
2. Your Nodebooks should open in a new browser window, showing the `Home` page.
3. Open the `AUTH - Create and Update` notebook

### Imports cell

This section will be common for most Nodebooks: it is a cell at the top of the notebook where you will import any required packages and functions to use throughout the notebook. It must be run first, every time.

### Path to file

This cell needs to be edited. Between the quotes you will type the filepath to the `.kdbx` file you would like to create, or one which already exists that you would like to edit. The format should look like:

~~~
file_location = 'C:/Users/path/to/node_auth.kdbx'
~~~
{: .language-plaintext .example}

Run this cell to save the input.

### Create Password

Run this cell. You will be prompted to create a password for the file (if it is a new file) or to enter the existing password if you are accessing an existing file. **Ensure that you remember this password**, as you will be using it every time you connect to the database through the Nodebooks.

### Create or Update Main Connections

Run this cell. This section will have an editable form. If it is a new file, all fields will be blank. If it is an existing file, the previously-entered information will display. You may now edit the information, pressing the blue button when you are finished to save your results.

- Conn Name: this is customizable - what is the name of this connection? Something like "OTN Database" to help you remember.
- Host: this will be something like `matos.asascience.com` for your DB, but is just an IP address for our Node Training DB `129.173.48.161`
- Port: this is specified in your `.auth` file and will be four digits. Use `5432` for Node Training.
- DB Name: this will be your database name, something like `pathnode`. For training, it will be `node_training`.
- User/Password: your personal username and password, as found on your `.auth` file.

### Create or Update DBLink Connections

In order to match detections across databases, you will need to establish `DBLink` connections to other OTN Nodes. This information can be stored in your `.kdbx` file, and will give you limited access to information required to match detections and create detection extracts.

Run this cell. This section will have an editable form. If it is a new file, all fields will be blank, and you can choose `Add Connection`. If it is an existing file, the previously-entered information will display, for each DBLink Connection you've specified. You may now edit the information, pressing the update or save button when you are finished to save your results.

Please contact OTN if you need any of the following information:

- Conn Name: this is customizable - what is the name of this connection? Something like `fact-link-to-migramar` is informative.
- Host: this will be something like `matos.asascience.com` for the DB you are trying to connect to (i.e. not your own Node db host).
- Port: this will be the port required to connect to the remote DB (not your Node db).
- DB Name: this will be the name of the database you are trying to connect to (not your Node db), something like `otnunit`.
- User/Password: the username and password of the DBLink user for your database. Not your own node admin's connection information.

Once you have saved your new DBLink connection, you can create another. Continue until you have established connections to all remote Nodes. Currently, you will require DBLinks to 7 Nodes.

### Test Connections

The next two cells will test the connection information you entered. Success messages will look like:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.your.org Database:your_db User:node_admin Node: Node
~~~
{: .language-plaintext .example}

and also like:

~~~
Testing dblink connections:
	fact-link-to-Node1: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE1
	fact-link-to-Node2: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE2
	fact-link-to-Node3: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE3
	fact-link-to-Node4: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE4
	fact-link-to-Node5: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE5
	fact-link-to-Node6: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE6
	fact-link-to-Node7: DBLink established on user@db.load.oceantrack.org:5432 - Node: NODE7
~~~
{: .language-plaintext .example}

You are now able to use the filepath to your `.kdbx` file to run all the Nodebooks.

### Change KDBX password

If you have been passed a template `.kdbx` file from OTNDC with prefilled information, you should use this section to change the password to ensure your privacy is protected.

You will need to enter:
- Current Password (provided by OTNDC) for your template file
- New Password (of your choosing)

Press `Save` to change the password of your `.kdbx`. **Ensure that you remember this password**, as you will be using it every time you connect to the database through the Nodebooks.

### Add a Git Access Token

This will be relevant for users of the `DB Fix` and `Verification` suite of Nodebooks only. If you have questions about this section please reach out to OTNDC.

{% include links.md %}
