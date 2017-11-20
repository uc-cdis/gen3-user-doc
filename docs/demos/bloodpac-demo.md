# BloodPAC DEMO: Using a Jupyter notebook for analysis
* * *

The bioinformatics team at the Center for Data Intensive Science (CDIS) at University of Chicago has put together a starting python library and a sample analysis notebook to help jumpstart commons analyses.    Both can be found in your VM in the analysis folder.    They can also be found at: [https://github.com/occ-data/bpa-functions](https://github.com/occ-data/bpa-functions).    The Gen3 community is encouraged to add to the functions library or improve the notebook.  

> NOTE:   As the Gen3 community updates repositories, you can keep them up to date using `git pull origin master` in the `functions` folder.   It has already been initialized to sync with this repository.
> NOTE2: If you receive an error when trying to do `git pull`, you may need to set proxies and/or either save or drop any changes you've made:

* set proxies:
export http_proxy="http://cloud-proxy.internal.io:3128";
export https_proxy="http://cloud-proxy.internal.io:3128"
(`cat /etc/environment` to see proxy settings)

* to drop changes:
 `git stash save --keep-index`
 `git stash drop`

* or save changes
`git commit .`

* Update CDIS utils python libraries:
`git clone https://github.com/uc-cdis/cdis-python-utils.git`
`cd cdis-python-utils`
`sudo -E python setup.py install`

* unset proxies to get juypter notebook to work again
`unset http_proxy;`
`unset https_proxy;`



What follows in this wiki is a guide to setting up this Jupyter notebook so that you can run everything in your browser.   In the notebook, you'll learn about basic Gen3 commons operations like:  

* Querying the API for metadata associated with submissions
* Pulling data into your VM for analysis
* Running a simple analysis over a file and collection of files
* Plotting the results

In the Jupyter notebook, many of the calls rely on more complex functions described in the [analysis_functions file](https://github.com/occ-data/bpa-functions/blob/master/analysis_functions_v2.py).   It is worth taking the time to understand how this file works so you can use and customize it or build your own tools.    
&nbsp;
We would gladly publish and share any tools, Docker images, function libraries, notebooks, etc via Github or via this Sage Synapse profile.   Just contact Gen3-support@datacommons.io for more information.

## Running the notebook in your VM

After we're logged in to our analysis VM and in the functions directory (from home: `cd functions`), run the jupyter notebook server.  
&nbsp;
Run the notebook server: ```jupyter notebook --no-browser --port=8889```

>NOTE:   You can stop a Juptyer server at anytime via `ctrl + c`

## Port forwarding to your VM

Next you'll want to set up a connection so that you can access the notebook being served from the VM to a browser in your local machine.   On a terminal session from your local machine (not in the VM) setup the connection.   
&nbsp;
Setup connection:   `ssh -N -L localhost:8888:localhost:8889 analysis`

> NOTE:   In the example above "analysis" is the name of the ssh shortcut we [setup back in step 2](https://www.synapse.org/#!Synapse:syn8011461/wiki/414184).

## Access the notebook in via browser

In your preferred browser and enter http://localhost:8888/;   Then from the VM terminal session, copy and paste the token from the notebook server into the requested spot in your browser.

#### Example:   Run Server, port forward, access notebook in browser
${image?fileName=jupyter%2Egif&align=Center&responsive=true}

## Review and follow the notebook

#### Credentials

The notebook makes use of both a [.secrets file](https://www.synapse.org/#!Synapse:syn8011461/wiki/415875) that came preloaded in your VM in the home directory that lets you query the metadata API from the VM, and the s3 profile you created back in [step 3](https://www.synapse.org/#!Synapse:syn8011461/wiki/415865) to pull 'raw' data into your VM for analysis.
&nbsp;
The first thing you'll want to do is update the "profile" variable in the first cell to whatever the name of your s3 profile is.       

>NOTE:  If you have forgotten what you called your profile, you can always take a look at the credential file to review.  From the VM run:  `vi ~/.aws/credentials`.  

#### Jupyter Basics
If you're not familiar with Jupyter notebooks, you have a few options to run the commands inside.   You can review line by line (select cell - `Shift+Enter`) or you can run all from the "Kernel" menu at the top of the browser.   

#### Shutting Down your Server
When you're done working, we encourage you to shut down your Jupyter server via `ctrl + c` in the VM that's running it.  You don't have to do this every time, but you should do it when you don't need it any more.   

#### VM Termination
At this point in the Gen3 commons development, you should contact Gen3-support@datacommons.io when you no longer need your VM active.   Active VMs accrue hourly charges (currently paid for by the Consortium and grants), so it's important to not waste valuable resources.   
