## Data Access Overview
* * *

## 1. Send credentials and get welcome email
* * *
<h3>Send SSH Key and Oauth to Gen3 commons team.</h3>

To access the VPC, users will need to send their public ssh key (or "pubkey") and an email that supports Oauth (often gmail) to <Gen3-support@datacommons.io>.   

> NOTE:   Do not send your private ssh key.   This is confidential and should never be shared with anyone.  

The pubkey will be used to access the login node and any VMs setup for the user.    The email will be used to permit access to:

* [Bionimbus](http://bionimbus-pdc.opensciencedatacloud.org/storage/) to receive s3 data storage credentials
* [data.Gen3.org](https://data.Gen3.org/) for browser based querying of metadata.

>NOTE:  for Gen3 members that were also their organization's contact for data submission, you already have access to your s3 credentials and the commons metadata API <data.Gen3.org>.   Just send your pubkey.  

<h4> I'm not familiar with SSH - how do I generate a keypair? </h4>

Github has a very nice [ssh tutorial](https://help.github.com/articles/connecting-to-github-with-ssh/) with step-by-step instructions for Mac, Windows (users with gitbash installed), and Linux users.   If you're new to using SSH we'd recommend reviewing the links:

* [About SSH](https://help.github.com/articles/about-ssh/)
* [Checking for Existing SSH Keys](https://help.github.com/articles/checking-for-existing-ssh-keys/)
* [Generating a new SSH key and adding it to the SSH Agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

>NOTE:  For Windows users, we recommend installing [Git for Windows](https://git-for-windows.github.io/) and using the Git Bash feature to interact on the command line, manage ssh keys, and s3 credentials.   

<h3>Receive a welcome email</h3>

Gen3 members with the appropriate signed legal documents will be sent an email that gives the following unique information:

* username (this is used to ssh to the VPC login node) - eg:  `ssh -A <username>@34.197.164.18`
* an IP associated with your new VM

* * *
## 2. SSH to Virtual Machine: config
* * *

<h3>How will I access the Login Node and my Virtual Machine (VM)?</h3>

Gen3 Commons users will login to the Virtual Private Cloud (VPC) headnode, then hop over to their analysis VM.   For more information on the [VPC architecture](../appendices/architecture/).

In your [welcome email](#1-send-credentials-and-get-welcome-email) you received your username and your vm.   In order to access your VM, you first must access the VPC login node.   This configuration helps ensure the security of the Gen3 commons by having your VM in a private subnet.   Using the credentials from your welcome email this can be done in the following order:

1.   SSH to login node:   `ssh -A <username>@34.197.164.18`
2.   SSH from login node to your VM:  `ssh -A ubuntu@<my_VM_ip>`

>NOTE 1:   `34.197.164.18` is the IP for the login node.   This is unlikely to change.   

>NOTE 2:  the `-A` flag forwards all the keys in your key chain.   For more details on managing SSH keys, check the guides linked in the [previous step](#1-send-credentials-and-get-welcome-email).

>NOTE 3:   You can't login to your analysis VM (in the private subnet) without first logging in to the login node (in the public subnet).  

Advanced users can manage these connections however they see fit.   For other users, we recommend updating your SSH config file so you can setup a 'multihop' ssh tunnel.  To 'multihop' in this context is to use a single command to get to your VM.    What follows are instructions for updating your `.ssh/config` file to get to your VM in a single command.

* * *
## 3. Setting up an ssh config for 'multihop'
* * *

To start, go to your .ssh directory in your laptop home directory.

```
cd ~/.ssh
```

If this directory does not exist, make one.

```
mkdir -p ~/.ssh
cd ~/.ssh
```

Within this directory create a file named "config" [Note: I use vim here but any text editor will do]:

```
vim config
```

In this file you can specify various hosts for access via ssh. Your host for the head login node should look something like this:

```
Host login-node
    Hostname <ip.address.of.login.node>
    User <YOUR_USERNAME>
    IdentityFile </path/to/YOUR_CREDFILE>
    ForwardAgent yes
```

Where /path/to/YOUR_CREDFILE might be, e.g., `~/.ssh/id_rsa`

The username will be provided to you by the Gen3 support team and will be tied to the credential file that you provide us when setting up the account. Save this file and exit. Back in the command line terminal you should now be able to log in to the Gen3 head-node using this host:

```
ssh login-node
```
Exit the head login node and return to your local machine. Back in your config file, add a new host for your analysis VM:

```
Host analysis
    Hostname <YOUR_VM_IP>
    User ubuntu
    ProxyCommand ssh -q -AXY login-node -W %h:%p
```

Once again you will receive the Hostname IP from the Gen3 support team in step 4.  This host will route you through the head login node and take you directly to your personal Gen3 analysis VM. Once again save the file and exit. In the terminal, try and log in to the submission VM:

```
ssh analysis
```

If you've done everything correctly, you should now be in the analysis VM.  

* * *
## 4. Access "raw" data storage from Virtual Machine
* * *

<h3> Add s3 'raw' data storage credentials to your VM </h3>
Now you'll need to add your storage credentials to your analysis VM.   Details on getting your credentials from the [Bionimbus storage portal](https://bionimbus-pdc.opensciencedatacloud.org/storage/) are outlined in the [data contribution section](/user-guide/data-contribution/) of this documentation.   If you are only accessing data and did not contribute, please follow those directions to acquire your keys using the Oauth you provided in [Step 1](#1-send-credentials-and-get-welcome-email) of the Data Access section.   

If you did contribute data you should use an existing key.   They will still have "read/write" permission to your project folder, but will also have permission to "read" other data in the Gen3 commons.   If you submitted multiple projects and have multiple keys, all will have the same "read" permissions for data - it only matters which one you pick if you still intend to write data to your project folder from your VM.  

As a reminder, the command to setup a profile is:
`aws configure --profile <CREATE YOUR PROFILE NAME>`

<h4> Example:  Configure an s3 profile in your VM </h4>
![Configure s3 Profile](/img/configure-S3.gif)

<h3>Review contents of the Gen3 Commons</h3>

You can now review the 'raw' data folders in the Gen3 object storage.   

`aws s3 ls s3://commons-data/ --profile <profilename>`

To peek inside a folder:

`aws s3 ls s3://commons-data/<foldername>/ --profile <profilename>`

You can use other commands to pull files from the s3 object storage into your VM. If you're not familiar with AWScli commands, we recommend reviewing the [high-level docs](http://docs.aws.amazon.com/cli/latest/userguide/using-s3-commands.html) or the [complete documentation](http://docs.aws.amazon.com/cli/latest/reference/s3/).

>NOTE:   Remember, that since your access is read only (except any projects you've submitted associated with your keys), you will only be able to read, not write to the project folders in the commons.   
>NOTE2:   If you are using keys with write access to your project folders in the commons, be VERY CAREFUL.   Don't delete any data you'll have to resubmit later.      

<h3> Ready to work! </h3>

You're ready to use whatever tools you wish to analyze data in the commons within your VM.   For requests for alternative configurations, analysis storage, or other needs please contact <gen3-support@datacommons.io>.

For an example of how you could use a Jupyter Notebook to run analysis in the browser on your local computer, please continue on to the [next section](/user-guide/demo/).    There are lots of good examples that may be useful to you.    
