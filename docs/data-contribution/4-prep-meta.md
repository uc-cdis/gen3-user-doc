# 4. Prepare metadata that fits the data model

## Overview
Gen3 data contributors will need to prepare metadata for their submission in tab-separated value (tsv) files, login to a portal provided for submission, and upload and validate their metadata submission.   This is simultaneously the most challenging and crucial part of contributing data to a Gen3 commons.   This page details the preparation and ordering of the tsvs that will be submitted.   The next two pages cover submission virtual machine (VM) access and uploading and validating your metadata tsv submission.   

## Review and understand the data model
Now that you have your project name, you can begin building out the rest of your metadata. Reference the most recent graph model of your commons at https://www.Gen3.org/data-group/ to help guide you on the necessary components in your submission. As you can see, from project you build up to experiment then to case and so on. For the properties that are allowed within this submission, please take some time to read through the dictionary schemas.   The raw schema can be found at: <link.to.schemas.Gen3.org>. Descriptions for each property as well as the valid submission values can be found in those schemas.
&nbsp;
Once you have [access to submission portal, link to submission portal doc](https://www.synapse.org/#!Synapse:syn8011461/wiki/413159), we recommend using the [Data Dictionary Viewer, link to dict viewer](https://www.synapse.org/#!Synapse:syn8011461/wiki/424047) to review the schema and determine which properties best describe your submission.   This tool will help you understand the field types, requirements, and node dependencies for your submission.

## Create your TSVs
&nbsp;
It may be helpful to think of each TSV as a node in the graph of the data model.   Each node can have multiple components, for example a project could have multiple experiments in a node.  
&nbsp;
* Blank TSV templates can be found at https://www.synapse.org/#!Synapse:syn10268802
    * Note there are wiki pages associated with each potential tsv or node in the templates.   They show example fields and information about data provenance.  
    * Field types and limitations can be cleaned from a careful read of the associated yaml files at:  https://github.com/occ-data/bpadictionary/tree/develop/gdcdictionary/schemas  

## Determine Submission Order
Before we discuss the actual submission process, we must first mention that the files must be submitted in a specific order. Once again referring back to the graph model at https://www.bloodpac.org/data-group, you cannot submit a node without submitting the nodes to which it points. 
&nbsp;
If you submit a file out of order, the validator will reject the submission on the basis that the dependency you point to (e.g. the read_groups.submitter_id in assay_result.tsv will be pointing to a node that doesn’t exist) is not present.   The Data Dictionary viewer can help you determine these dependencies.

## Sample Diagram of TSV Submission Order
While this diagram represents an earlier version of the BloodPAC data model, the required submission logic for current versions of the model will be very similar.
${image?fileName=blood%5Fatlas%5F010617%5Fmarkup%2Epng&align=None&responsive=true}
