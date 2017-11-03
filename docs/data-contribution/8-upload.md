# 8. Upload "raw" data to object storage

### Preparing your data
Data files such as BAMs, FASTQs, or PDFs should be uploaded directly to the object store.  The metadata TSVs you prepared should not be submitted to the object store, as they have already been submitted via the API.
&nbsp;
Please prepare a single folder with all of submission files in the same directory.   No sub directories.   

### Uploading your data)
You can now upload all the files in the prepared folder on your local computer using the AWS CLI and the profiles you configured in [step 7](https://www.synapse.org/#!Synapse:syn8011461/wiki/413157). Below is the command to copy a folder filled with all your submission files on your local computer to your project folder in a commons. You need to change the name of /path/folder/ to the name of the path of the folder you want to upload.
&nbsp;
```
aws s3 cp --sse AES256 [/path/folder/] s3://bpa-data/[foldername] --recursive --profile [profilename]
```
> EXTRA:  In an object store, a "folder" or "dir" can't exist with nothing in it.   Thus, if you were to 'ls' before moving any files into it, you wouldn't see the project folder you have access to.   In the example above you're essentially uploading all your data and "creating a folder" in a single step.   

Other useful commands and AWS CLI documentation can be found at: https://www.opensciencedatacloud.org/support/pdc.html and https://aws.amazon.com/cli/
