<h2> Data Access Overview </h2>
* * *

The sponsor of a Gen3 data commons typically decides how users will access data in object storage. In some cases, approved users may be allowed to download data directly to their local computer from within an internet browser or with the [cdis-data-client](https://github.com/uc-cdis/cdis-data-client/releases). When more security is required, users may be required to download and analyze data in a protected environment, such as a virtual machine (VM) in a virtual private cloud (VPC).

* * *
## Accessing data from within a browser
* * *

Once data files are [registered](/user-guide/data-contribution/#-register-data-files-with-the-windmill-data-portal/), their address in s3 object storage can be obtained by providing the file's UUID to the following URL:
https://data.gen3.org/index/index/UUID

Data files can be downloaded by providing the file's UUID to the following URL:
https://data.gen3.org/user/data/download/UUID

* * *
## Downloading data with the cdis-data-client
* * *

Data files can also be downloaded using the "cdis-data-client", which provides a simple command-line interface for downloading and uploading data files.

[Download the latest release of the client here.](https://github.com/uc-cdis/cdis-data-client/releases)

Once downloaded and installed, the client can be configured with the API credentials.json downloaded from your Profile in the data portal:
```
./cdis-data-client configure --profile <profile_name> --cred /path/to/api/credentials.json
```

The client will then prompt you for the API. Enter the API of your commons, e.g.:
```
API endpoint: https://gen3.datacommons.io/
```

To download a data file, pass the file's UUID to the client:
```
cdis-data-client download --profile <profile_name> --file ./filename.tsv --uuid d7a5XXXX-XXXX-XXXX-XXXX-XXXX53583014
```

In the above command, `download` mode is specified, the `profile_name` we configured with the API credentails earlier is used, and a filename (`filename.tsv`) was specified for our local copy of the downloaded file.

* * *
## Accessing data from the Virtual Private Cloud
* * *

If additional security is required, the cdis-data-client can be installed on a VM in the VPC to download files. The following instructions detail how to login to a VM.

* * *
<h3>Send public SSH Key and OpenConnectID account to Gen3 commons team.</h3>
* * *
To access the Virtual Private Cloud (VPC), users will need to send their public ssh key (or "pubkey") and an email that supports Oauth (often gmail) to <support@datacommons.io>. Do not send your private ssh key! This is confidential and should never be shared with anyone.  

Github has a very nice [ssh tutorial](https://help.github.com/articles/connecting-to-github-with-ssh/) with step-by-step instructions for Mac, Windows (users with gitbash installed), and Linux users. If you're new to using SSH we'd recommend reviewing the links:

* [About SSH](https://help.github.com/articles/about-ssh/)
* [Checking for Existing SSH Keys](https://help.github.com/articles/checking-for-existing-ssh-keys/)
* [Generating a new SSH key and adding it to the SSH Agent](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/)

Gen3 users with the appropriate signed legal documents will be sent an email that gives the following unique information:

* username (this is used to ssh to the VPC login node) - eg:  `ssh -A <username>@<login-ip-address>`
* an IP associated with your new VM

* * *
<h3>SSH to Virtual Machine</h3>
* * *
In some data commons, you may need to ssh in to a "login" node prior to accessing your personal virtual machine:

1.   SSH to login node:   `ssh -A <username>@3<login-node-IP>`
2.   SSH from login node to your VM:  `ssh -A ubuntu@<my_VM_IP>`

>NOTE:  the `-A` flag forwards all the keys in your key chain.   For more details on managing SSH keys, check the guides linked in the [previous step](#1-send-credentials-and-get-welcome-email).

It is recommended to update the SSH config file to use a 'multihop' ssh tunnel. To 'multihop' in this context is to use a single command to get to your VM. What follows are instructions for updating your `.ssh/config` file to get to your VM in a single command.

Go to your .ssh directory in your laptop home directory: `cd ~/.ssh`

Within this directory, edit the file named "config" (if it doesn't exist, create it first): `vim config`

In this file you can specify various hosts for access via ssh. Your host for the head login node should look something like this:

```
Host login-node
    Hostname <ip.address.of.login.node>
    User <YOUR_USERNAME>
    IdentityFile </path/to/YOUR_CREDFILE>
    ForwardAgent yes
```

Where /path/to/YOUR_CREDFILE might be: `~/.ssh/id_rsa`

The username will be provided to you by the Gen3 support team and will be tied to the credential file that you provide us when setting up the account (your private ssh key). Save this file and exit. Back in the command line terminal you should now be able to log in to the login node using this host:

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

Once again you will receive the Hostname IP from the support team.  This host will route you through the head login node and take you directly to your personal analysis VM. Once again, save the file and exit. In the terminal, try to log in to the submission VM:

```
ssh analysis
```

If you've done everything correctly, you should now be in the analysis VM.  

<h3> Ready to work! </h3>

You're ready to use whatever tools you wish to analyze data in the commons within your VM.   For requests for alternative configurations, analysis storage, or other needs please contact `support@datacommons.io`.

For an example of how to use a Jupyter Notebook for data analyses in a browser window on your local computer, please continue on to the [next section](/user-guide/demo/).     
