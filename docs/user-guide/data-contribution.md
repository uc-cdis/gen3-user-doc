* * *
## Project Submission Overview
* * *

* Sign documents, fill out forms, get credentials
* Prepare and submit metadata to commons API
* Prepare and submit full dataset (w/o metadata tsvs) to object storage.

<h3>Steps to Contribute a Project to the Gen3 Commons</h3>

1. [Review and sign legal](data-contribution/#1-review-and-sign-legal-agreement)
2. [Complete the data inventory form](data-contribution/#2-complete-the-data-inventory-form)
3. [Receive project name and access credentials](data-contribution/#3-receive-project-name-api-credentials_1)
4. [Prepare metadata that fits the data model](data-contribution/#4-prepare-metadata-that-fits-the-data-model)
5. [Access metadata submission portal](data-contribution/#5-access-metadata-that-fits-the-data-model)
6. [Submit and validate project metadata tsvs](data-contribution/#6-submit-and-validate-project-metadata-tsvs)
7. [Get and configure s3 data storage credentials](data-contribution/#7-get-and-configure-s3-data-storage-credentials)
8. [Upload "raw" data to object storage](data-contribution/#8-upload-raw-data-to-object-storage)

\* NOTE:  Gen3 members are encouraged to submit multiple projects to the commons.   To do so, repeat steps 2-8 above.

* * *

<h3>Why Do Gen3 Commons Use a Data Model?</h3>
* Having all participating members use the same data model:
    * Allows for standardized metadata elements across a commons.
    * Permits flexible and scaleable API generation based on data commons software that reads the data model schema.   
    * Lets users query the commons API so that an ecosystem of applications can be built.
    * Helps automate the validation of submitted data.   


Here is the most [current data model](https://github.com/occ-data/gen3dictionary).

Here is the most current [graph of the model](https://www.gen3.org/data-group/).

If you have an submission element that you believe can't be described in the model, we'd be glad to work with you to find a home for the element or update the model.   

<h3> Questions? </h3>
Contact:

* For Legal:  gen3-legal@occ-data.org

* For Submission/Access Questions:   gen3-support@datacommons.io

* * *
## 1. Review and sign legal agreement
* * *

To use the Gen3 commons, please review and sign the following agreements and return them to info@gen3.org.   The most current versions (and past versions for transparency) of all of the below documents can be found at:  
[https://www.gen3.org/data-governance/](https://www.gen3.org/data-governance/)
&nbsp;
* Data Contributor Agreement (DCA)
* Data Services/Use Agreement (DUA)

&nbsp;
If you only wish to contribute data, you do not need to sign the DUA.  
&nbsp;
* * *

These documents may also reference the:
* Privacy and Security Agreement
* Intellectual Property Rights (IPR) Policy


* * *
## 2. Complete the data inventory form
* * *
Prepare a pre-submission [data inventory form](https://goo.gl/forms/)

Having this information helps the Gen3 submission team prepare for your project and setup your storage access credentials using the authentication method you provide in the form.  

* * *
## 3. Receive project name / API credentials
* * *
&nbsp;
Once you have completed the [data inventory form, link to step](link), you will receive an email with your project name (associated with project data), username (used to login to Virtual Private Cloud (VPC) headnode), and instructions to access the metadata submission portal and an object storage for your project.  
&nbsp;
The project name will be used to create the project node from which you can build out the rest of your submission and is an essential identifier. For example, the project name will need to be provided when you [submit the metadata, link to metadata submission](https://www.synapse.org/#!Synapse:syn8011461/wiki/413154) for your experiment nodes.

<h3>Project name example</h3>

```
<mycompanyname>_P0001_T1
<mycompanyname>_P0002_T1
<mycompanyname>_P0001_T2
```
<h3>Breakdown:</h3>
* "<mycompanyname>" identifies the submitter organization
* "P000x" identifies the submission number for said organization in said train
* "Tx" identifies the train number
&nbsp;
NOTE:  the Gen3 data submission calendar is broken up into different trains.
NOTE2:   Your project folder will have a prefix appended to it to identify the commons.  eg - BloodPAC (BPA):
```
"BPA_<mycompanyname>_P0001_T1"
```
* * *
## 4. Prepare metadata that fits the data model
* * *
<h3> Overview </h3>
Gen3 data contributors will need to prepare metadata for their submission in tab-separated value (tsv) files, login to a portal provided for submission, and upload and validate their metadata submission.   This is simultaneously the most challenging and crucial part of contributing data to a Gen3 commons.   This page details the preparation and ordering of the tsvs that will be submitted.   The next two pages cover submission virtual machine (VM) access and uploading and validating your metadata tsv submission.   

<h3> Review and understand the data model</h3>
Now that you have your project name, you can begin building out the rest of your metadata. Reference the most recent graph model of your commons at https://www.Gen3.org/data-group/ to help guide you on the necessary components in your submission. As you can see, from project you build up to experiment then to case and so on. For the properties that are allowed within this submission, please take some time to read through the dictionary schemas.   The raw schema can be found at: <link.to.schemas.Gen3.org>. Descriptions for each property as well as the valid submission values can be found in those schemas.
&nbsp;
Once you have [access to submission portal, link to submission portal doc](https://www.synapse.org/#!Synapse:syn8011461/wiki/413159), we recommend using the [Data Dictionary Viewer, link to dict viewer](https://www.synapse.org/#!Synapse:syn8011461/wiki/424047) to review the schema and determine which properties best describe your submission.   This tool will help you understand the field types, requirements, and node dependencies for your submission.

<h3>Create your TSVs</h3>
&nbsp;
It may be helpful to think of each TSV as a node in the graph of the data model.   Each node can have multiple components, for example a project could have multiple experiments in a node.  
&nbsp;
* Blank TSV templates can be found at https://www.synapse.org/#!Synapse:syn10268802
    * Note there are wiki pages associated with each potential tsv or node in the templates.   They show example fields and information about data provenance.  
    * Field types and limitations can be cleaned from a careful read of the associated yaml files at:  https://github.com/occ-data/bpadictionary/tree/develop/gdcdictionary/schemas  

<h3>Determine Submission Order</h3>
Before we discuss the actual submission process, we must first mention that the files must be submitted in a specific order. Once again referring back to the graph model at https://www.bloodpac.org/data-group, you cannot submit a node without submitting the nodes to which it points.
&nbsp;
If you submit a file out of order, the validator will reject the submission on the basis that the dependency you point to (e.g. the read_groups.submitter_id in assay_result.tsv will be pointing to a node that doesn’t exist) is not present.   The Data Dictionary viewer can help you determine these dependencies.

<h3>Sample Diagram of TSV Submission Order</h3>
While this diagram represents an earlier version of the BloodPAC data model, the required submission logic for current versions of the model will be very similar.
${image?fileName=blood%5Fatlas%5F010617%5Fmarkup%2Epng&align=None&responsive=true}

* * *
## 5. Access metadata that fits the data model
* * *

<h3>What is the metadata submission portal?</h3>

The metadata submission portal is secure environment for submitting the tsv metadata files associated with your project submission, querying the metadata associated with your project and others, and using the Data Dictionary Viewer to understand fields.   You will be able to login with your OAuth and you will have access update or edit the metadata associated with your submission by adding tsv files or "nodes" to the graph.   

<h3>Where is the metadata submission portal?</h3>

Links to Gen3 Commons Submission portals:

[BloodPAC](https://data.bloodpac.org/)


* * *
## 6. Submit and validate project metadata tsvs
* * *

<h3> Begin your submission</h3>

From the submission portal select the project for which you wish to submit metadata.   Remembering the order in which you need to submit your tsvs (see [step 5, Determine Submission Order](https://www.synapse.org/#!Synapse:syn8011461/wiki/413155) for details) begin your submission by uploading or copying in your first tsv (likely "experiment.tsv").   NOTE:   If you would prefer submitting nodes in json to tsv the submission portal also accepts json.  

>   To get you started, the first node - "project" has already been created for you.

Now you should see a lot of details about the submission process. At the very bottom, you should be able to immediately get a grasp of how the submission went with the following fields:

```
{'entity_error_count': 0,
'message': 'Transaction successful.',
'success': True,
'transaction_id': 403,
'transactional_error_count': 0,
'transactional_errors': [],
'updated_entity_count': 40}
```

Specifically, the message and success fields should provide you with whether your submission was valid and went through. If you see anything other than success, check the other fields for any information on what went wrong with the submission. The most descriptive information will be found in the individual entity transaction logs. Each line in the TSV will have its own output with the following attributes:

```
{'action': 'update',
 'errors': [],
 'id': 'asdf21as-2q4a-2563-213k-8dn4kg8dsb3j',
 'related_cases': [],
 'type': 'case',
 'unique_keys': [{'project_id': 'bpa-MyGroup_P0001_T1'
   'submitter_id': u'BPA_MG_P0001_EX1_C1'}],
 'valid': True,
 'warnings': []},
```

On a successful submission, the API will return something like above. The action can be used to identify if the node was created new or just updated. Other useful information includes the id for the node. This is the UUID for the submission and is unique for the node throughout the entirety of the Gen3 Commons. The other unique_key provided is the tuple project_id and submitter_id; another way of saying that the submitter_id combined with the project_id is a universal identifier for this node.

<h3> Troubleshooting and finishing your submission</h3>

If, against all odds, your submission is perfect on the first try, you are finished with submission of that node, and you can move on to the next node. However, if the submission throws errors or claims your submission to be invalid, you will need to fix your submission.
&nbsp;
The best first step is to go through the outputs from the individual entities. In the errors field will be a rough description of what tripped our validation check. The most common problems are simple issues such as spelling errors or mislabeled fields.
&nbsp;
Other errors include the one I mentioned earlier about submitting out of order and errors from not adhering to valid values as defined in our dictionary.
&nbsp;
If you don't receive any output it usually means your TSV is invalid and must be edited.
&nbsp;

<h4> Submission Failure Example </h4>
![Submission Failure Example](http://g.recordit.co/Q9mb2wNCN8.gif)

<h4> ALTERNATIVE in BETA:  Form submission </h4>
Using tsvs allows users to bulk submit their metadata.   This is ultimately a much faster process for users with larger datasets.   If you wish, you can also use form submission to insert properties into a node.   

NOTE:   if you use the same submitter ID, and submit again to the same node, it will overwrite properties.   Be sure to change it should you choose to use form submission multiple times on a given node.   

NOTE2:   it is not currently possible to remove values submitted in error using the form submission method.

${image?fileName=formSubmission%2Egif&align=None&scale=100&responsive=true}

<h4> Query the API </h4>

If helpful you can use query the API in the submission portal to confirm or correct your submission, to delete nodes, or to submit json queries to learn more about your submission or all the data in the commons.   To learn more visit the API section of the wiki:  
https://www.synapse.org/#!Synapse:syn8011461/wiki/415875

<h4>Check the commons matrices</h4>

Read ["What's an example of the API at work?"](https://www.synapse.org/#!Synapse:syn8011461/wiki/415875) to learn more about how the [data matrices](https://www.bloodpac.org/data-group/) work.   Suffice to say, you can check them hourly to see relevant metadata you submit appear!

<h4>Provide feedback</h4>
You may receive errors for what you think is a valid submission. If you feel what you have provided for a particular entity is valid, please contact the Gen3 support team at gen3-support@occ-data.org. We will be happy to accommodate any necessary changes. We can always add new nodes, properties, or values.

<h4>Let us know submission is complete</h4>
Please contact the Gen3 support team to let us know when your submission is complete.

<h3>Submission FAQ</h3>

<h4> How do I know my submission was accepted? </h4>
You will see this within the json output:
```
'message': 'Transaction successful.',
'success': True,
```

<h4>How can I learn more about the elements of my existing submission?</h4>
When you are viewing a project, there is a "browse nodes" feature.   From here you can download, view, or completely delete the tsvs associated with any project you have write access to.

<h4>What happens if i need to resubmit a tsv that was already accepted?</h4>
When you resubmit (aka submit to a node with the same submitter id), you will update the existing node.

&nbsp;
For example, if you submit a sample with `sample_type`, `composition`, and `tube_type`, and you later realize that the tube type was wrong for that submission, if you were to resubmit a tsv that has just the `submitter_id` and `tube_type` it will overwrite ONLY the tube type. The `sample_type` and composition from the previous submission will still be in the database.  What this means is that if you had previously submitted something you DON'T want, like say you realize that you accidentally submitted the `tube_type` as `method_of_sample_procurement`, simply renaming the header in your TSV would not overwrite the existing data in the node.  You would need to submit null/empty values for `method_of_sample_procurement` to get rid of it.

<h4> I was part of the very first submission group, in Nov/Dec 2016 when we added TSVs directly into an object store.   Where is the `project.submitter_id` field? </h4>

`projects.submitter_id` has become `projects.code` now.   SO:

EXAMPLE:
* `program.name` = 'bpa'
* `project.code` ='MyOrg_P0001_T1'
* `project_id` = `program.name` + '-' + `project.code` = 'bpa-MyOrg_P0001_T1'

* * *

## 7. Get and configure s3 data storage credentials

* * *

<h3>Overview</h3>
Now that you've successfully submitted and validated your project metadata, it's time to upload your 'raw' data to the Gen3 Commons.   The Gen3 commons utilize [object storage](https://en.wikipedia.org/wiki/Object_storage).   
&nbsp;
This page details how users gain and manage the credentials to access a project folder.   The [following page](https://www.synapse.org/#!Synapse:syn8011461/wiki/413158) will detail submitting data to the project folder.   

> Why should we use command line to submit data instead of some kind of website?
>> Because for transfer of large files or many files, there can be time-out issues, encryption issues, or corruption issues.   Using the command line ensures secure and complete transfer.

> NOTE:  if you only have small files and are uncomfortable operating on the command line, you may want to try using a GUI tool like [Cyberduck](https://cyberduck.io/) to connect to S3 and manage your upload instead.  

<h3> Obtain S3 credentials </h3>
1.	Go to https://bionimbus-pdc.opensciencedatacloud.org/storage/ Select and use the authentication method you gave in the [data inventory form](https://www.synapse.org/#!Synapse:syn8011461/wiki/413153)
2.	Download access keys by selecting the appropriate button next to the information for your username, e.g., under "Available BPA Datasets". The button is labeled “Generate S3 credential.” See Figure 1.
3.	Credentials appear as comma-separated values including an access key and a secret key. The secret key should remain secret.  Do not share these keys.

> NOTE:   Do not share the s3 credentials you gain below with anyone.  

> If you need to obtain new credentials, repeat steps (2.a) through (2.c). The button will now say “Rotate key” button, which will deactivate previous credentials and provide new ones.

<h4> Figure 1 </h4>
${image?fileName=bionimbussubmit%2Epng&align=None&responsive=true}

>KNOWN ISSUE: Safari will not provide S3 credentials on the first try. After generating keys once, press the “Rotate key” button.

<h3> Install AWS CLI </h3>
<h4> Mac OSX or Linux/Unix</h4>
Open your “Terminal” application and type the following command:
```
sudo apt-get install awscli
```
or
```
sudo easy_install awscli
```
If prompted, enter your device’s password.

<h4> Windows </h4>
Download and run one of the windows installers at: https://aws.amazon.com/cli/

<h3> Configure AWS CLI with the downloaded project credentials </h3>

In your “Terminal” application, type the line below, replacing “CREATE YOUR PROFILE NAME” with a profile name you create.

```
aws configure --profile <CREATE YOUR PROFILE NAME>
```

> **Pro-tip:**  Profile management will be very important as groups submit multiple projects.   Your downloaded s3 credentials only give you access to the project folder for which they are created.   If you are only submitting one project, you don't need profiles.   If you are submitting multiple, you will want to carefully pick project names for each project.   eg - P0001_T1 and P0002_T1.
>> Some good sources on managing multiple profiles:
>> * OSX/Linux: http://docs.aws.amazon.com/cli/latest/userguide/cli-chap-getting-started.html#cli-multiple-profiles
>> * Windows powershell: http://docs.aws.amazon.com/powershell/latest/userguide/specifying-your-aws-credentials.html

After pressing Enter/Return, you will be prompted for your Access Key ID and Secret Access Key. These are the S3 credentials you downloaded earlier. Enter keys as prompted, pressing Enter/Return after each step.

```
AWS Access Key ID [****************]:
AWS Secret Access Key [****************]:
```
Enter a default region name, as prompted - us-east-1. Press Enter/Return.

```
Default region name [None]: us-east-1
```
Press return at the final prompt.
```
Default output format [None]:
```
You should now be able to see the folder names in the bpa-data bucket.   

```
aws s3 ls s3://bpa-data/ --profile <profilename>
```

* * *

## 8. Upload "raw" data to object storage

* * *

<h3> Preparing your data </h3>
Data files such as BAMs, FASTQs, or PDFs should be uploaded directly to the object store.  The metadata TSVs you prepared should not be submitted to the object store, as they have already been submitted via the API.
&nbsp;
Please prepare a single folder with all of submission files in the same directory.   No sub directories.   

<h3> Uploading your data </h3>
You can now upload all the files in the prepared folder on your local computer using the AWS CLI and the profiles you configured in [step 7](https://www.synapse.org/#!Synapse:syn8011461/wiki/413157). Below is the command to copy a folder filled with all your submission files on your local computer to your project folder in a commons. You need to change the name of /path/folder/ to the name of the path of the folder you want to upload.
&nbsp;

```
aws s3 cp --sse AES256 [/path/folder/] s3://bpa-data/[foldername] --recursive --profile [profilename]
```
> EXTRA:  In an object store, a "folder" or "dir" can't exist with nothing in it.   Thus, if you were to 'ls' before moving any files into it, you wouldn't see the project folder you have access to.   In the example above you're essentially uploading all your data and "creating a folder" in a single step.   

Other useful commands and AWS CLI documentation can be found at: https://www.opensciencedatacloud.org/support/pdc.html and https://aws.amazon.com/cli/

* * *
## Appendix: Data Dictionary Viewer
* * *
&nbsp;
The Data Dictionary Viewer is designed to make it easier to understand the data model, the field types associated with each node, and the potential values associated with each field.   Gen3 members can use it through the 'dictionary' icon at data.Gen3.org or directly at: <https://data.Gen3.org/dd/>
&nbsp;
The Data Dictionary Viewer lets you browse and understand the available fields in a node and review the dependencies a given node has to the existence of a prior node.  This is an invaluable tool for both the submission of data and later analysis of the entire commons.   
&nbsp;
In addition to drilling down on the properties of each node, the Data Dictionary Viewer will also let you toggle views and browse the nodes as a graph and as tables.  
&nbsp;

${image?fileName=datadictionary%5Fv2%2Egif&align=None&scale=100&responsive=true}

* * *
## Appendix: Managing timepoints in a submission
* * *

<br>
Some elements of submitted datasets could be related to each other in time.   To stay in compliance with HIPAA, Gen3 commons create timelines without using real dates.   Every other date field is anchored by the "index_date" in the "case" node.  
<br>
In this field you can have things like "Study Enrollment" or "Diagnosis".   Study the case node in the dictionary for more information on the index_date field:  https://data.Gen3.org/dd/case

<h3> Examples of submissions using multiple date times</h3>

Patient A enrolls in a study on July 1, and has a blood sample taken on July 10. For patient A you would report:
* case.index_date = "Study Enrollment"
* biospecimen.days_to_procurement = July 10 - July 1 = 9
<br>
Alternatively if they were diagnosed 2 years before the study began and you wanted to use that as the index_date nothing is stopping you:
* case.index_date = "Diagnosis"
* biospecimen.days_to_procurment = July 10, 2017 - July 1, 2015 =  739

<h3> Negative Dates </h3>

Days to values can also be negative. If you have an index_date event that occurs after the event, you would present those days_to values as negative. If Patient A had a biospecimen taken when they were initially diagnosed:
* case.index_date = "Study Enrollment"
* biospecimen.days_to_procurement = July 10, 2015 - July 1, 2017 = -721

<h3> No Time Series </h3>

The days_to_procurement and days_to_collection are required fields. If you do not have any data for these, we allow escape values of "Unknown" and "Not Applicable". Please use "Unknown" in the instances where you have established a time series but are unable to pin down the date of the event. Use "Not Applicable" if you do not have a time series at all.

## Appendix: Minimum Technical Data Elements

&nbsp;
To facilitate cross analysis and improve the usability of the Gen3 commons, all data contributors should submit what are considered the “Minimum Technical Data Elements” (MTDE).   These pre-analytic fields were determined through an iterative series of conversations with data contributors and the “Data Experience” Gen3 group.  

[Biospecimen Node](https://data.bloodpac.org/dd/biospecimen)
&nbsp;
* Blood Tube Type
* Procurement Temperature
* Shipment Temperature

[Sample Node](https://data.bloodpac.org/dd/sample)
* Composition
* Blood Fractionation Method
* Hours to Fractionation Upper/Lower
   * From blood draw to completion of fractionation

[Aliquot Node](https://data.bloodpac.org/dd/aliquot)
* Clinical or Contrived
* Hours to Freezer Upper/Lower
   * From completion of fractionation to freezing
* Storage Temperature

<h4> [Analyte Node](https://data.bloodpac.org/dd/analyte) </h4>
* Analyte Isolation Method

[Quantification Assay Node](https://data.bloodpac.org/dd/quantification_assay)
* Assay Method
  * DNA quantification method
