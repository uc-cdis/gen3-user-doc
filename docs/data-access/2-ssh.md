# 2. SSH to Virtual Machine: config

## How will I access the Login Node and my Virtual Machine (VM)? 
Gen3 Commons users will login to the Virtual Private Cloud (VPC) headnode, then hop over to their analysis VM.   For more information on the VPC, visit: https://www.synapse.org/#!Synapse:syn8011461/wiki/414186
&nbsp; 

In your [welcome email](https://cgmeyer.github.io/gen3-user-doc/Data%20Access/1sendcred.html) you received your username and your vm.   In order to access your VM, you first must access the VPC login node.   This configuration helps ensure the security of the BloodPAC commons by having your VM in a private subnet.   Using the credentials from your welcome email this can be done in the following order:

1.   SSH to login node:   `ssh -A <username>@34.197.164.18`
2.   SSH from login node to your VM:  `ssh -A ubuntu@<my_VM_ip>`

>NOTE 1:   34.197.164.18 is the IP for the login node.   This is unlikely to change.   
>NOTE 2:  the `-A` flag forwards all the keys in your key chain.   For more details on managing SSH keys, check the guides linked in the [previous step](https://www.synapse.org/#!Synapse:syn8011461/wiki/414183).
>NOTE 3:   You can't login to your analysis VM (in the private subnet) without first logging in to the login node (in the public subnet).  

Advanced users can manage these connections however they see fit.   For other users, we recommend updating your SSH config file so you can setup a 'multihop' ssh tunnel.  To 'multihop' in this context is to use a single command to get to your VM.    What follows are instructions for updating your `.ssh/config` file to get to your VM in a single command.

## Setting up an ssh config for 'multihop'

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

In this file you can specify various hosts for access via ssh. Your host for the BPA head node should look something like this:

```
Host BPA
    Hostname 34.197.164.18
    User YOUR_USERNAME
    IdentityFile /path/to/YOUR_CREDFILE
    ForwardAgent yes
```

The username will be provided to you by the BloodPAC support team and will be tied to the credential file that you provide us when setting up the account. Save this file and exit. Back in the command line terminal you should now be able to log in to the BloodPAC head-node using this host:

```
ssh BPA
```
Exit the BPA head node and return to your local machine. Back in your config file, add a new host for the BPA submission VM:

```
Host analysis
    Hostname YOUR_VM_IP
    User ubuntu
    ProxyCommand ssh -q -AXY BPA -W %h:%p
```

Once again you will receive the Hostname IP from the BloodPAC support team in step 4.  This host will route you through the BPA head node and take you directly to your personal BloodPAC analysis VM. Once again save the file and exit. In the terminal, try and log in to the submission VM:

```
ssh analysis
````

If you've done everything correctly, you should now be in the analysis VM.  
