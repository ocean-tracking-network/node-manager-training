---
title: "Setup and Installing Needed Software"
teaching: 10
exercises: 50
questions:
- "What Software do I Need to do my Node Manager Requiremnets?"
- "Why do I need the recomened Software?"
- "How do I install the needed software?"
objectives:
- "Understand how to install needed software and get ready to load to data"
- "Ensure attendees have the needed software installed and are ready to move on to using it"
keypoints:
- "Node manager tasks envolve the use of many different programs"
- "OTN staff are always availble to help when needing to install these programs or if you are having issues with them"
- "There are lots of programs and tools to help Node managers"
---

# In order to work efficiently as a Node Manager, the following programs are necessary and/or useful.


## Python/Anaconda

Python is a popular general-purpose programming language that can be used for a wide variety of applications. It is the main language used by OTN and our data processing pipeline.

Anaconda is a python distribution and a package manager. When you install Anaconda you get python and many of the popular python libraries. Anaconda allows you to be able to install all the packages needed to run the notebooks with one command rather than having to install each one individually. There is a smaller version of Anaconda with only essential packages we recommend installing called miniconda.

 **Install Miniconda** - https://docs.conda.io/en/latest/miniconda.html
  - Select the option to "add to PATH environment variable" (during install steps)!!


## Git

Git is a version control system, it helps people to be able to work collaboratively and maintain a complete history of their work. We use Git at OTN to track changes on data products and on occasion you will need to get those changes to ensure you have the best version of our products.

**Install Git** 

**Windows**- https://git-scm.com/download/win

**Mac**- https://git-scm.com/download


## Database Console Viewer (dBeaver, DataGrip, etc)

There are database administration tools to help make database related tasks easier. There are many options available but dBeaver and DataGrip are the most popular options at OTN. 
<br>
* https://dbeaver.io/ (free and open access - recommended)
* https://www.jetbrains.com/datagrip (free institutional/student access options - another option)

## iPython Utilities 
These are the collection of notebooks used to load data into the OTN datasystem.

**Install iPython Utilities** 

1. Navigate to the folder you wish to keep the iPython Utilities notebooks in
2. Open your terminal or command prompt app. Type `cd` then `space`. You then need to get the path of the folder you will be keeping the notebooks in. You can either drag the folder into the terminal or command prompt app or hit shift/option while right clicking and select copy as path then paste that in the terminal or command prompt and hit `enter`
3. You are now able to run commands in that folder. Now run: 
`git clone https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities.git`
This will get the latest version iPython Utilities from our gitlab
4. To help install all the required packages quickly we use a package called mamba. Install mamba by running the command: `conda install -c conda-forge mamba`
6. Navigate to the ipython-utilities subdirectory that was created by running `cd ipython-utilities`.
7. Now to install all needed packages and run the following: `mamba env update -n root -f environment.yml`
8. In the ipython-utilities directory run the command: `jupyter notebook --config="nb_config.py" "0. Home.ipynb"`

More operating system specific instructions and troubleshooting tips can be found at: https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/wikis/New-Install-of-Ipython-Utilities

---

## Operating Specific Programs
___

## For WINDOWS users

**Path Copy Copy** - For copying path links from your file browser.
* https://pathcopycopy.github.io/

**Notepad ++** - For reading and editing code, csv files etc. without altering the formatting.
* https://notepad-plus-plus.org/downloads/

**Tortoise Git** - For managing git, avoiding command line.
* https://tortoisegit.org/download/
---

## For MAC users

**VS Code** - For reading and editing code, csv files etc. without altering the formatting.
* https://code.visualstudio.com/

**Source Tree** - For managing git, avoiding command line.
* https://www.sourcetreeapp.com

