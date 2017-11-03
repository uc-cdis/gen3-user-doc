# 1. Send credentials and get welcome email

## Send SSH Key and Oauth to Gen3 commons team.

To access the VPC, users will need to send their public ssh key (or "pubkey") and an email that supports Oauth (often gmail) to Gen3-support@datacommons.io.   

> NOTE:   Do not send your private ssh key.   This is confidential and should never be shared with anyone.  

The pubkey will be used to access the login node and any VMs setup for the user.    The email will be used to permit access to:

* [Bionimbus](http://bionimbus-pdc.opensciencedatacloud.org/storage/) to receive s3 data storage credentials
* [data.Gen3.org]( https://data.Gen3.org/) for browser based querying of metadata. 

>NOTE:  for Gen3 members that were also their organization's contact for data submission, you already have access to your s3 credentials and data.Gen3.org.   Just send your pubkey.  

### I'm not familiar with SSH - how do I generate a keypair? 
[Github has a very nice tutorial](https://help.github.com/articles/connecting-to-github-with-ssh/) with step by step instructions for Mac, Windows (users with gitbash installed), and Linux users.   If you're new to using SSH we'd recommend reviewing the links:
* [About SSH](https://help.github.com/articles/about-ssh/)
* [Checking for Existing SSH Keys](https://help.github.com/articles/checking-for-existing-ssh-keys/)
* [Generating a new SSH key and adding it to the SSH Agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)
&nbsp;
>NOTE:  For Windows users, we recommend installing [Git for Windows](https://git-for-windows.github.io/) and using the Git Bash feature to interact on the command line, manage ssh keys, and s3 credentials.   

## Receive a welcome email
Gen3 members with the appropriate signed legal documents will be sent an email that gives the following unique information: 

* username (this is used to ssh to the VPC login node) - eg:  `ssh -A <username>@34.197.164.18`
* an IP associated with your new VM


