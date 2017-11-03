# 6. Submit and validate project metadata tsvs

## Begin your submission

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

## Troubleshooting and finishing your submission

If, against all odds, your submission is perfect on the first try, you are finished with submission of that node, and you can move on to the next node. However, if the submission throws errors or claims your submission to be invalid, you will need to fix your submission.
&nbsp;
The best first step is to go through the outputs from the individual entities. In the errors field will be a rough description of what tripped our validation check. The most common problems are simple issues such as spelling errors or mislabeled fields. 
&nbsp;
Other errors include the one I mentioned earlier about submitting out of order and errors from not adhering to valid values as defined in our dictionary.
&nbsp;
If you don't receive any output it usually means your TSV is invalid and must be edited.
&nbsp;

### Submission Failure Example
![Submission Failure Example](http://g.recordit.co/Q9mb2wNCN8.gif)

### ALTERNATIVE in BETA:  Form submission
Using tsvs allows users to bulk submit their metadata.   This is ultimately a much faster process for users with larger datasets.   If you wish, you can also use form submission to insert properties into a node.   

NOTE:   if you use the same submitter ID, and submit again to the same node, it will overwrite properties.   Be sure to change it should you choose to use form submission multiple times on a given node.   

NOTE2:   it is not currently possible to remove values submitted in error using the form submission method.

${image?fileName=formSubmission%2Egif&align=None&scale=100&responsive=true}

### Query the API

If helpful you can use query the API in the submission portal to confirm or correct your submission, to delete nodes, or to submit json queries to learn more about your submission or all the data in the commons.   To learn more visit the API section of the wiki:  
https://www.synapse.org/#!Synapse:syn8011461/wiki/415875

### Check the commons matrices

Read ["What's an example of the API at work?"](https://www.synapse.org/#!Synapse:syn8011461/wiki/415875) to learn more about how the [data matrices](https://www.bloodpac.org/data-group/) work.   Suffice to say, you can check them hourly to see relevant metadata you submit appear!

### Provide feedback
You may receive errors for what you think is a valid submission. If you feel what you have provided for a particular entity is valid, please contact the Gen3 support team at gen3-support@occ-data.org. We will be happy to accommodate any necessary changes. We can always add new nodes, properties, or values.

### Let us know submission is complete
Please contact the Gen3 support team to let us know when your submission is complete. 

### Submission FAQ

#### How do I know my submission was accepted? 
You will see this within the json output: 
```
'message': 'Transaction successful.',
'success': True,
```

#### How can I learn more about the elements of my existing submission?
When you are viewing a project, there is a "browse nodes" feature.   From here you can download, view, or completely delete the tsvs associated with any project you have write access to.

#### What happens if i need to resubmit a tsv that was already accepted?
When you resubmit (aka submit to a node with the same submitter id), you will update the existing node. 
&nbsp;
For example, if you submit a sample with `sample_type`, `composition`, and `tube_type`, and you later realize that the tube type was wrong for that submission, if you were to resubmit a tsv that has just the `submitter_id` and `tube_type` it will overwrite ONLY the tube type. The `sample_type` and composition from the previous submission will still be in the database.  What this means is that if you had previously submitted something you DON'T want, like say you realize that you accidentally submitted the `tube_type` as `method_of_sample_procurement`, simply renaming the header in your TSV would not overwrite the existing data in the node.  You would need to submit null/empty values for `method_of_sample_procurement` to get rid of it.

#### I was part of the very first submission group, in Nov/Dec 2016 when we added TSVs directly into an object store.   Where is the `project.submitter_id` field?

`projects.submitter_id` has become `projects.code` now.   SO:

EXAMPLE:
* `program.name` = 'bpa'
* `project.code` ='MyOrg_P0001_T1'
* `project_id` = `program.name` + '-' + `project.code` = 'bpa-MyOrg_P0001_T1'

