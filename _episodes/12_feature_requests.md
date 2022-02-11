---
title: "Nodebook Improvement and Development"
teaching: 10
exercises: 0
questions:
- "How do I request new features?"
- "How do I report bugs to OTN?"
- "What is my role in Nodebook develeopment?"
objectives:
- "Understand the process for developing the Nodebooks"
- "Understand the process for testing new Nodebook changes"
keypoints:
- "The Nodebooks are for you - OTN wants to ensure they remain useful"
---

Once you begin using the OTN Nodebooks, you will likely discover tools that are missing, or features which have code-bugs in them. OTN developers are here to help ensure the Nodebooks meet your needs. We are constantly changing our processes and are always open to suggestions to improve! These tools are for you, and we want to ensure they are useful.

## New Features

If there is a feature that you'd like to see, you can bring this to OTN's attention in this way:

1. Ask in our Slack channels to see if there is a tool that already exists that will fit your needs. Discuss your ideal-feature with OTN developers to help them understand what you need.
2. Once the new feature is properly scoped, create a new Gitlab Issue here https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/issues, using the `new_feature` template. You should assign to one of the OTN developers, who can begin to work on the request.

Here is the "new_feature" template, for your information:


            Note that this template is **ONLY** used for tracking new features. Bugs should be filed separately using the Bug template.

            The new feature should be proposed, scoped, and approved **before** you fill out this template.

            ## Summary
            **Provide a general summary of the feature to be built.**

            ## Rationale
            **Why do we want this?**

            ## End Users
            **Who is expected to use this functionality most?**

            ## Scope
            **What are the expected qualities and functionality of this new feature? One per line.**

            ## Minimum viable product
            **What subset of the above functionality is necessary before the feature is considered finished?**

            ## Timeline
            **Give a brief, ballpark estimate on when you would want this done.**


## Bug-fixes

If you encounter an error in your Nodebooks, its possible there is an issue with your dataset. Sometime, however, the case is that the Nodebook is not functioning as expected! If you believe a certain Nodebook is malfunctioning, you will want to identify this bug to OTN developers as soon as possible.

To identify a bug, here are the steps to take:
1. Ask in our Slack channels to see if the error is caused by your dataset. This can include posting an error message, or just describing the output from the Nodebook, and why it is not as expected.
2. If OTN developers identify that the problem is not your dataset, the next step will be to create a Gitlab Issue here https://gitlab.oceantrack.org/otn-partner-nodes/ipython-utilities/-/issues, using the `bug` template. You should assign to one of the OTN developers, and use the label `bugfix`.

Here is the "bug" template, for your information:


            Note that this template is **ONLY** used for reporting bugs. New features must be vetted and filed separately using the New Feature template.

            As such, before you continue, ask yourself:
            **Does this ticket concern existing functionality that is broken? Or is it a deficiency in the system as-designed that needs net new work to complete?**
            If it's the former, then use this template, otherwise, use the New Feature template.

            ## Summary
            **Provide a general summary of the problem.**

            ## Expected Behavior
            **What should be happening?**

            ## Current Behavior
            **What is actually happening?**

            ## Steps to Reproduce
            **How can I see this bug happening? Where does it happen? Provide links to specific pages where the bug is visible, along with steps to reproduce it.**

            ## Priority
            **On a scale from 1 to 5, approximate the severity of the issue. Be honest.**


## Testing Features/Fixes

Once OTN developers have attempted to build your new feature, or fix your bug, they will publish their code into the `integration` branch of our ipython-utilities Nodebooks. You will be asked to test these changes, to ensure the end-product is satisfactory. This branch is used for development and testing only, and should not be used for data-loading outside of testing.

Here are instructions for changing branches:

(Replace anything in <> with the sensible value for your installation/situation)

Open git bash or terminal.

From your git bash window, type:

```
cd "/path/to/your/ipython-utilities"
```
This will put your terminal or git bash terminal in the folder where this codebase lives on your computer. Now we're going to 
* reset any changes you have made locally (save anything you might want to keep with `git stash`), 
* switch to the new branch
* update that branch with any new code

```
git reset --hard
git checkout <branch you are moving to ie:integration>
git pull
```

Resolve python libraries by using the mamba command:

```
mamba env update -n root -f environment.yml
```

You will then be able to test the new code. When you are finished, follow the same steps to switch back to the `master` branch to continue your work. The `master` branch contains all the production-quality tools.

{% include links.md %}
