---
title: Setup
---

### In order to work efficiently as a Node Manager, the following programs are necessary and/or useful.

To standardize the verification and quality control process that all contributing data is subjected to, OTN has built custom quality control workflows and tools for Node Managers, often referred to as the OTN Nodebooks. The underlying functions are written in `Python` and workflows that rely on them can be undertaken through the use of `Jupyter` Notebooks. In order to use these tools, and interact with your database, you will need to install a few different applications and packages. All installation instructions are also available on our GitLab [here](https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/wikis/home). 

This lesson will give attendees a chance to install all the relevant software, under the supervision of OTN staff.

# Python/Anaconda

`Python` is a popular general-purpose programming language that can be used for a wide variety of applications. It is the main language used by OTN and our data processing pipeline.

`Anaconda` is a python distribution and a package manager. When you install `Anaconda` you get a `python` interpreter, and many of the core python libraries. Managing your Python installation with Anaconda allows you to be able to install and update all the packages needed to run the Nodebooks with one command rather than having to install each one individually. 

There is a smaller version of `Anaconda` with fewer, more essential packages which we recommend installing to save computer memory, called `miniconda`.

 **Install Miniconda** - [https://docs.conda.io/en/latest/miniconda.html](https://docs.conda.io/en/latest/miniconda.html)
  - Select the option to `add to PATH environment variable` (during install steps)!


# Git

`Git` is a version-control system, it helps people to work collaboratively and maintains a complete history of all changes made to a project. We use `Git` at OTN to track changes to the Nodebooks made by our developer team, and occasionally you will need to update your Nodebooks to include those changes.

**Install Git** 

- **Windows**- [https://git-scm.com/download/win](https://git-scm.com/download/win)

- **Mac**- [https://git-scm.com/download](https://git-scm.com/download)


# Nodebooks - iPython Utilities 
The `ipython-utilities` project contains the collection of Nodebooks used to load data into the OTN data system.

**Create an Account**

First, you will need a GitLab account. Please fill out this [signup form for an account on GitLab](https://gitlab.oceantrack.org/users/sign_up).

Then, OTN staff will give you access to the relevant Projects containing the code we will use.

**Install iPython Utilities** 

1. Determine the folder in which you wish to keep the iPython Utilities Nodebooks.
1. Open your `terminal` or `command prompt` app. 
   * Type `cd` then `space`. 
   * You then need to get the filepath to the folder in which you wish to keep the iPython Utilities Nodebooks. You can either drag the folder into the `terminal` or `command prompt` app or hit `shift/option` while right clicking and select `copy as path` from the menu.
   * Then paste the filepath in the `terminal` or `command prompt` and hit `enter`
   * In summary, you should type `cd /path/to/desired/folder` before pressing enter.
1. You are now able to run commands in that folder. Now run: `git clone https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities.git`. This will get the latest version iPython Utilities from our GitLab
1. Navigate to the ipython-utilities subdirectory that was created by running `cd ipython-utilities`.
1. Now to install all required python packages, run the following: `conda env update -n root -f environment.yml`. Confirm there is a success message produced.

**To open and use the OTN Nodebooks:**
- **MAC**: Open your terminal, and navigate to your ipython-utilities directory, using `cd /path/to/ipython-utilities`. Then, run the command: `jupyter notebook --config="nb_config.py" "0. Home.ipynb"` to open the Nodebooks in a browser window.
- **WINDOWS**: Double-click the `start-jupyter.bat` file in your ipython-utlities folder, which will open the Nodebooks in a browser window.
- **DO NOT CLOSE** your terminal/CMD instance that opens! This will need to remain open in the background in order for the Nodebooks to be operational.

More operating system-specific instructions and troubleshooting tips can be found at: [https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/wikis/New-Install-of-Ipython-Utilities](https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/wikis/New-Install-of-Ipython-Utilities)

![OTN Nodebooks - home page](/fig/home_page.JPG)

# Database Console Viewer

There are database administration applications to assist with interacting directly with your database. There are many options available but `DBeaver` and `DataGrip` are the most popular options at OTN. 

* [https://dbeaver.io/](https://dbeaver.io/) (free and open access - **recommended**)
* [https://www.jetbrains.com/datagrip](https://www.jetbrains.com/datagrip) (free institutional/student access options - another option)

# More Useful Programs

In order to work efficiently as a Node Manager, the following programs are necessary and/or useful.

## For WINDOWS users

**Path Copy Copy** - For copying path links from your file browser.
* [https://pathcopycopy.github.io/](https://pathcopycopy.github.io/)

**Notepad ++** - For reading and editing code, csv files etc. without altering the formatting.
* [https://notepad-plus-plus.org/downloads/](https://notepad-plus-plus.org/downloads/)

**Tortoise Git** - For managing git, avoiding command line.
* [https://tortoisegit.org/download/](https://tortoisegit.org/download/)

## For MAC users

**VS Code** - For reading and editing code, csv files etc. without altering the formatting.
* [https://code.visualstudio.com/](https://code.visualstudio.com/)

**Source Tree** - For managing git, avoiding command line.
* [https://www.sourcetreeapp.com](https://www.sourcetreeapp.com)

# Node Training Datasets

We have created test datasets to use for this workshop. Each attendee has their own files, available at this link: [https://members.oceantrack.org/data/repository/fntp/nmt-files/](https://members.oceantrack.org/data/repository/fntp/nmt-files/)


Please find the folder with your name and download. Save these somewhere on your computer, and **UNZIP** all files.
{% include links.md %}
