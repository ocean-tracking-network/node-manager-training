---
title: "Database Fix Notebooks"
teaching: 15
exercises: 0
questions:
- "What should I do if the database values require a change?"
objectives:
- "Learn about Database Fix Notebooks that are useful for changes to the database"
keypoints:
- "database-fix-notebooks has many useful notebooks for Node Managers to help them make changes to the database"
---

### General Description

When a researcher conveys that database values are incorrect, we can use the [Database fix notebooks](https://gitlab.oceantrack.org/otn-partner-nodes/database-fix-notebooks) to correct these values. These notebooks are also used to fix errors that come up from the verifications. The instructions to use them will be shown in the verification instructions. This suite of notebooks, however, should be used as a last option. If an error comes up from the verification notebooks, human eyes and critical thinking should be used to check if the database fix notebooks should be used.

### Installation
The installation steps for the database fix notebooks are similar to the installation steps for ipython-utilities:
1. Determine the folder in which you wish to keep the Database Fix Notebooks.
1. Open your `terminal` or `command prompt` app. 
   * Type `cd` then `space`. 
   * You then need to get the filepath to the folder in which you wish to keep the Database Fix Notebooks. You can either drag the folder into the `terminal` or `command prompt` app or hit `shift/option` while right clicking and select `copy as path` from the menu.
   * Then paste the filepath in the `terminal` or `command prompt` and hit `enter`
   * In summary, you should type `cd /path/to/desired/folder` before pressing enter.
1. Create and activate the "nodebook" python enviornment. The creation process will only need to happen once.
   * In your terminal, run the command `conda create -n nodebook python=3.9`
   * Activate the nodebook environment using `conda activate nodebook`
1. You are now able to run commands in that folder. Now run: `git clone https://gitlab.oceantrack.org/otn-partner-nodes/database-fix-notebooks.git`. This will get the latest version Database Fix Notebooks from our GitLab
1. Navigate to the database-fix-notebooks subdirectory that was created by running `cd database-fix-notebooks`.
1. Now to install all required python packages by running the following: `mamba env update -n nodebook -f environment.yml`

**To open and use the Database Fix Notebooks:**
- **MAC/WINDOWS**: Open your terminal, and navigate to your database-fix-notebooks directory, using `cd /paht/to/database-fix-notebooks`. Then, run the commands: 
   * `conda activate nodebook` to activate the nodebook python environment
   * `jupyter notebook --config="nb_config.py" "0. Home.ipynb"` to open the Nodebooks in a browser window.
- **DO NOT CLOSE** your terminal/CMD instance that opens! This will need to remain open in the background in order for the Nodebooks to be operational.

More operating system-specific instructions and troubleshooting tips can be found at: [https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/wikis/New-Install-of-Ipython-Utilities](https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/wikis/New-Install-of-Ipython-Utilities)

### Gitlab KDBX integration
One interesting part of the Database Fix Notebooks is that if you add a Gitlab token to your kdbx file, it will automatically add the results from the notebook to the created Gitlab issue. Otherwise, you will have to copy and paste the displayed results manualyl into the comments (as directed by the notebook).

To integrate the Gitlab token into your kdbx file, please use the instructions in the [AUTH - Create and Update](https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/blob/master/AUTH%20-%20Create%20and%20Update.ipynb) notebook in ipython-utilities.

### Issue Creation

The **first** step when a researcher tell you about an incorrect database value is to create a new Gitlab Issue with the `DB Fix` Issue checklist template.

Here is the Issue checklist, for reference:

~~~
# **DB Fix Issue**

## Related gitlab issue:
- **[paste link to issue]**

## CSV of information needed for each record that needs fixing (look at `0. Home` notebook for column headers):
- **[link file here]**

## Task list
- [ ] NAME label issue `DB Fix`
- [ ] NAME create a CSV of changes 
- [ ] NAME assign to @diniangela to make the change
- [ ] Angela make database change
~~~
{: .language-plaintext .example}

There are a few helpful explanation notebooks inside this suite of notebook.
- [0. Home](https://gitlab.oceantrack.org/otn-partner-nodes/database-fix-notebooks/-/blob/master/0.%20Home.ipynb): This notebook will provide a brief explanation of what each notebook does, as well as helpful hints to show what is needed to run the notebook.
- [0. Which notebook should I use](https://gitlab.oceantrack.org/otn-partner-nodes/database-fix-notebooks/-/blob/master/0.%20Which%20notebook%20should%20I%20use.ipynb): This notebook has a form which will help node managers determine which database fix notebook is appropriate for their change. It shows a list of the types of metadata we offer (project, tag, deployment, and detection) and, based on the selection, shows a list of columns from the raw metadata sheets. Based on this selection, it will display a result of which notebook to use.

### Spreadsheet Creation

Some of the database fix notebooks require a spreadsheet of the changes. These will be evident by the notebook top description or the description on `0. Home.ipynb`. 

The required columns will be shown in the description. If there are missing required columns, the notebook will display an error with which columns are missing. 

The spreadsheet should be created and added to the created Gitlab issue, either in the description or in a comment.

### Next Steps
Once you know which notebook to use and have created the spreadsheet (if needed), you can open the notebook which will consist of a single cell to run.

The notebooks have similar formats so three examples will be demonstrated below.

### Example 1: Change receiver serial
Let's say for the first example, a researcher has emailed saying that they made a typo in the receiver metadata.

### Example 2: Change tag end date
Let's say for the second example, a researcher has emailed saying that they were missing a harvest date, which should be used instead of the estimated tag life.

#### Example 3: Fix the_geom
Let's say for the third example, you are verifying tag metadata and an error comes up from ipython-utilities saying that the_geom is incorrect and the instructions direct you to the 'fix the_geom' database fix notebooks.

#### Example 4: Fix duplicate downloads
Let's say for the fourth example, you are verifying event data and an error pops up from ipython-utilites saying that there are duplicate downloads and the instructions direct you to the 'fix duplicate downloads' database fix notebooks.

The first step would be to create an issue with the collection code and linking the detections Gitlab issue that you were working on when this error popped up.

After this, you would open up the 'Fix duplicate downloads' notebook in database-fix-notebooks, notice there's no spreadsheet needed, and run the single cell.

This prompts you for your engine with a 'Browse File' button. Once you click this, your file explorer opens up and you can search for your KDBX (with the Gitlab token). Once you have selected this, the dialog box closes and a 'Next' button appears.