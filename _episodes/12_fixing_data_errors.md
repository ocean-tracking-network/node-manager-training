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

During the process of loading data it is possible to uncover errors with previously-loaded datasets. OTN is constantly improving our QA/QC tools, which means we are identifying and correcting more and more historical errors.

Generally, there a few ways Node Managers will identify errors:
- By using the `Verification` cells in the Nodebooks
- When new QA/QC updates are released for the Nodebooks
- When a researcher identifies an error explicitly
- When a researcher submits data that does not match previously-loaded records

In the latter case, full comparison between the records is required, followed by a discussion with the researcher to identify if the previously-loaded records or the new records are correct. Often, the outcome is that the data in the DB needs correction.

# Scoping the Required Correction

Once an error has been identified, the correction needs to be scoped. This includes: which tables are affected by the error, which catalognumbers, etc. Please use the `DB Fix Issue` GitLab template.

Here is the template for reference:

~~~
# **DB Fix Issue**

__This issue title should include schema name, year of record affected__
- eg "HFX 2020 receiver lat/long change"

__add DB fix label to issue__

## Related gitlab issue:
- eg #1234, [paste link to issue]

## Schema:
- eg HFX

## DB table name:
- eg HFX.moorings

### information needed for each record that needs fixing (repeat for each catalog number):
1. unique identifier:
1. original value:
1. new value:

- [ ] NAME - label issue `db fix`
- [ ] NAME - tag OTNDC staff for assistance with request (@diniangela etc)
~~~
{: .language-plaintext .example}


Once fully scoped, you may assign the Issue to OTN Staff to complete the correction. If it is a simple process, they may provide instructions to the Node Manager to complete. **Do not** attempt to correct the issue yourself without consultation with OTN.

# Database Fix Notebooks

Currently, the OTN Database Team is working on a suite of notebooks for fixing common issues found in the database. These are the tools that the OTN Team will be using to correct the identified errors, if the tool to do so already exists.

These notebooks are beyond the scope of the current training but eventually Data Managers who wish to learn more will be able to take further training. In the meantime, if you see notes in the notebooks such as "Use the DB Fix notebook called XXXX to correct this error", please create a `DB Fix Issue` ticket and pass it off to OTN.

{% include links.md %}
