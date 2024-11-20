---
title: "Fixing Data Errors"
teaching: 10
exercises: 0
questions:
- "How do I identify data errors?"
- "How do I correct data errors?"
objectives:
- "Understand the workflow for faxing data errors."
keypoints:
- "OTN is developing tools to support this."
---

# Identifying Errors

During the process of loading data it is possible to uncover errors with previously-loaded datasets. Generally, there a few ways Node Managers will identify errors:
- By using the `Verification` cells in the Nodebooks
- When new QA/QC updates are released for the Nodebooks
- When a researcher identifies an error explicitly
- When a researcher submits data that does not match previously-loaded records

In the latter case, full comparison between the records is required, followed by a discussion with the researcher to identify if the previously-loaded records or the new records are correct. Often, the outcome is that the data in the DB needs correction.

In other cases, if the [DB Fix Notebooks](https://ocean-tracking-network.github.io/node-manager-training/10_Database%20fix%20notebooks/index.html) covered in the previous lesson do not cover your issue, then you will have to reach out to OTN's data center with a GitLab ticket.


# Scoping the Required Correction

Once an error has been identified, the correction needs to be scoped. This includes: which tables are affected by the error, which catalognumbers, etc. Please use the `DB Fix Issue` GitLab template.

Here is the template for reference:

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


Once fully scoped, you may assign the Issue to OTN Staff to complete the correction. If it is a simple process, they may provide instructions to the Node Manager to complete. **Do not** attempt to correct the issue yourself without consultation with OTN.

{% include links.md %}
