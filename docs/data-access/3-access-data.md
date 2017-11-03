# 3. Access "raw" data storage from Virtual Machine

## Add s3 'raw' data storage credentials to your VM
Now you'll need to add your storage credentials to your analysis VM.   Details on getting your credentials from the [Bionimbus storage portal](https://bionimbus-pdc.opensciencedatacloud.org/storage/) are outlined in the [data contribution section](https://www.synapse.org/#!Synapse:syn8011461/wiki/413157) of the wiki.   If you are only accessing data and did not contribute, please follow those directions to acquire your keys using the Oauth you provided in [Step 1](https://www.synapse.org/#!Synapse:syn8011461/wiki/414183) of the Data Access section.   

If you did contribute data you should use an existing key.   They will still have "read/write" permission to your project folder, but will also have permission to "read" other data in the BloodPAC commons.   If you submitted multiple projects and have multiple keys, all will have the same "read" permissions for data - it only matters which one you pick if you still intend to write data to your project folder from your VM.  

As a reminder, the command to setup a profile is: `aws configure --profile <CREATE YOUR PROFILE NAME>`
### Example:  Configure an S3 profile in your VM
${image?fileName=S3%5FVM%5FprofileLoop%2Egif&align=Center&responsive=true}

## Review contents of the Gen3 Commons

You can now review the 'raw' data folders in the Gen3 object storage.   
`aws s3 ls s3://commons-data/ --profile <profilename>`

To peek inside a folder:
`aws s3 ls s3://commons-data/<foldername>/ --profile <profilename>`

You can use other commands to pull files from the s3 object storage into your VM.    If you're not familiar with AWScli commands, we recommend reviewing the [high-level docs](http://docs.aws.amazon.com/cli/latest/userguide/using-s3-commands.html) or the [complete documentation](http://docs.aws.amazon.com/cli/latest/reference/s3/).

>NOTE:   Remember, that since your access is read only (except any projects you've submitted associated with your keys), you will only be able to read, not write to the project folders in the commons.   
>NOTE2:   If you are using keys with write access to your project folders in the commons, be VERY CAREFUL.   Don't delete any data you'll have to resubmit later.      

### Ready to work!

You're ready to use whatever tools you wish to analyze data in the commons within your VM.   For requests for alternative configurations, analysis storage, or other needs please contact gen3-support@datacommons.io.

For an example of how you could use a Jupyter Notebook to run analysis in the browser on your local computer, please continue on to the [next section](/demos/bloodpac-demo.md).    There are lots of good examples that may be useful to you.    
