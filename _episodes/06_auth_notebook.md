---
title: "Connecting to the Database from the Nodebooks"
teaching: 30
exercises: 15
questions:
- "How can a Node Manager connect with their database in the Nodebooks?"
- "How can a Node Manager connect with other Nodes for matching?"
- "How can a Node Manager use Gitlab Automation in the Database Fix Nodebooks?"
objectives:
- "Understand how to use the `AUTH - Create and Update` notebook to maintain your database credentials file"
keypoints:
- "Node-members cannot access the database, you are the liason"
- "Data submissions and QC processes should be trackable and archived"
- "OTN is always here to help with any step of the process"
---


# Connecting to your Database from the Nodebooks

Now that we have explored and set up some of the tools needed to work as a Node Manager, we can begin preparing our Nodebook connection files. To enhance security, OTN uses encrypted, password-protected `.kdbx` files to store login credentials for your database. To create these, we have developed an interactive `AUTH - Create and Update` Nodebook.

1. Open the OTN Nodebooks
	* Open your terminal, and navigate to your ipython-utilities directory, using `cd /path/to/ipython-utilities.` Then, run the commands:
        * `conda activate nodebook` to activate the nodebook python environment
        * `jupyter notebook --config="nb_config.py" "0. Home.ipynb"` to open the Nodebooks in a browser window.
2. Your Nodebooks should open in a new browser window, showing the `Home` page.
3. Open the `AUTH - Create and Update` Nodebook

### Imports cell

This section will be common for most Nodebooks: it is a cell at the top of the notebook where you will import any required packages and functions to use throughout the notebook. It must be run first, every time.

### Path to file

This cell needs to be edited. Between the quotes you will type the filepath to the `.kdbx` file you would like to create, *or* one which already exists that you would like to edit. The format should look like:

~~~
file_location = 'C:/Users/path/to/node_auth.kdbx'
~~~
{: .language-plaintext .example}

Run this cell to save the input.

### Create Password

Run this cell. You will be prompted to create a password for the file (if it is a new file) or to enter the existing password if you are accessing an existing file. **Ensure that you remember this master password**, as you will be using it every time you connect to the database through the Nodebooks.

### Create or Update Main Connections

Run this cell. This section will have an editable form. If it is a new file, all fields will be blank. If it is an existing file, the previously-entered information will display. You may now edit the information, pressing the blue button when you are finished to save your results.

- Conn Name: this is customizable - what is the name of this connection? We recommend choosing something like "OTN Database" to help you remember.
- Host: this will be something like `matos.asascience.com` for your DB, but for training purposes we will use the IP of our Node Training DB: `129.173.48.161`.
- Port: this is specified in your `.auth` file and will be four digits. Use `5432` for Node Training.
- DB Name: this will be your database name, something like `pathnode`. For training, it will be `node_training`.
- User/Password: your personal username and password, as found on your `.auth` file.

### Create or Update DBLink Connections

In order to match detections across databases, you will need to establish `DBLink` connections to other OTN Nodes. This information can be stored in your `.kdbx` file, and will give you limited access to information required to match detections and create detection extracts.

Run this cell. This section will have an editable form. If it is a new file, all fields will be blank, and you can choose `Add Connection`. If it is an existing file, the previously-entered information will display for each DBLink Connection you've specified. You may now edit the information, pressing the update or save button when you are finished to save your results.

Please contact OTN if you need any of the following information:

- Conn Name: this is customizable - what is the name of this connection? Something like `fact-link-to-migramar` is informative.
- Host: this will be something like `matos.asascience.com` for the DB you are trying to connect to (i.e. not your own Node db host).
- Port: this will be the port required to connect to the remote DB (not your Node db).
- DB Name: this will be the name of the database you are trying to connect to (not your Node db), something like `otnunit`.
- User/Password: the username and password of the DBLink user for your database. Not your own node admin's connection information.

Once you have saved your new DBLink connection, you can create another. Continue until you have established connections to all remote Nodes. Currently, you will require DBLinks to 7 Nodes, but this is rapidly expanding.

### Test Connections

The next two cells will test the connection information you entered. Success messages will look like this for your main connection:

~~~
Auth password:········
Connection Notes: None
Database connection established
Connection Type:postgresql Host:db.your.org Database:your_db User:node_admin Node: Node
~~~
{: .language-plaintext .example}

and like this for your DBLink connections:

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

This will be relevant for users of the `Database Fix` suite of Nodebooks only. If you are not going to use these tools, you can skip this cell in the Nodebooks.

A Gitlab Access Token will allow Nodebooks to access your GitLab account and insert comments into an Issue directly, as you are working on it. This has been developed for the Database Fix Notebooks to ensure all changes made within the notebooks are documented in GitLab properly. The automation is part of the `OTNGitlabAutomation` package.

Instructions to create a Personal Access Token are found on our wiki [here](https://gitlab.oceantrack.org/otn-partner-nodes/otngitlabautomation/-/wikis/How-to-create-an-personal-access-token)

You can create one by following the steps below:
1. In the top-right corner of gitlab, click your avatar.
1. Select Edit profile.
1. On the left sidebar, select Access Tokens. Enter a name for your token and optionally set expiry date for the token.
1. Under 'Select scopes' select 'api'.
1. Select Create personal access token.
1. A new token will be created at the top of the page. Make sure you save it somewhere as you won't be able to access it again. Treat this token like a password as it can be used to access GitLab under your user.

Once you have created your access token, run this cell. 

You will need to enter your personal access token.

Press `Add Token` to insert the token into your `.kdbx`. 

Re-running this cell will allow you to update your access token any time it expires.

{% include links.md %}
