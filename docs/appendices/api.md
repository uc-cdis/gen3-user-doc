# Working with the API
* * *

## What does the API do?

The API is created programmatically based on the [BloodPAC commons data model](https://github.com/occ-data/bpadictionary).   All of the work BloodPAC data contributors do to prepare their metadata powers the API (see steps [4-6 in the Data Contribution section](/user-guide/data-contribution/#4-prepare-metadata-that-fits-the-data-model)).   

With the API in place, users can submit queries to find whatever metadata information they might like across the BloodPAC commons.   The API can be queried programmatically or through provided tools like the submission portal.  

We use [GraphQL](http://graphql.org/) to manage the metadata in the BloodPAC commons.  To learn the basics of writing queries in Graph QL, we recommend [this introduction](http://graphql.org/learn/).

## What's an example of the API at work?  

The BloodPAC commons team has created a few matrices to help describe submitted data.   These are linked to from: <https://www.bloodpac.org/data-group/>

These query the API for the desired metadata and return the matrices.   They run on cron jobs that update hourly, so if you're submitting data or adding to the commons, you can watch your entry appear.   If you are a member and would like to view these matrices, contact info@bloodpac.org for a username and password.   

## SECRETS!   Credentials to query

Like your credentials that let you access "raw" data in the object store or your ssh keys that let you access a VM, there is also a credential that lets you query the API.    For users granted data access, these are in a .secrets file in the home directory of your VM.   These are used for every API call.   

For example:   If you're doing the [Jupyter notebook demo](/demos/bloodpac-demo/) from your analysis VM, your secrets file is loaded early in the demo so you can query.   If you're using the submission portal to query, your secrets file is setup in a DB associated with your login credentials.  

Your secrets file helps define what metadata you can read or write to.

## Queries in the submission portal    
You can run queries directly in the submission portal by clicking the magnifying glass or directly at: https://data.bloodpac.org/graphql.    Queries are essential as you begin analysis.   The query portal has been optimized to autocomplete fields based on content, increase speed and responsiveness, and generally make it easier for BloodPAC members to find what they need.

Example templates have been setup [here](/appendices/template-tsvs/).

![GraphQL Query](/img/gQL-query.gif)

### Extra:   Default = first 10 entries
Queries by defult return the first 10 entries.   If you want more than that, you can specify it in the query call: ```(first:1000)```

Updating the example template [`details from experiment`](/assets/details_from_experiment.json/) sample query to call the first 1000, the call becomes:  

```
{
	"query":" query Test {
		experiment (first:1000, submitter_id: "<INSERT submitter_id>") {  
			experimental_intent
			experimental_description
			number_samples_per_experimental_group
			type_of_sample
			type_of_specimen
		}
	} "
}
```

## Browsing by project node    

The metadata submission portal [https://data.gen3.org/](https://data.gen3.org/) can be used to browse an individual submission by node.   Just select a project and then click the "browse nodes" button to the right.    From there, you'll get a screen like below where you can query by node in the dropdown at the left.

<h4> Example:  Browse by node </h4>
![Browse by node](/img/browse-by-node.png)

You can also use this feature to download the tsv associated with the node, or if you have "write" access to the this project, delete existing nodes.   

## Graphing a project

You can also review a graph of an individual project, toggling between views of the completed nodes and the full graph.  

<h5> Example:  Graphing a project </h5>
![Graphing a project](/img/graph-a-project.gif)
