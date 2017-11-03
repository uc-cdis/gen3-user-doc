# 7. Get and configure s3 data storage credentials

## Overview

Now that you've successfully submitted and validated your project metadata, it's time to upload your 'raw' data to the Gen3 Commons.   The Gen3 commons utilize [object storage](https://en.wikipedia.org/wiki/Object_storage).   
&nbsp;
This page details how users gain and manage the credentials to access a project folder.   The [following page](https://www.synapse.org/#!Synapse:syn8011461/wiki/413158) will detail submitting data to the project folder.   

> Why should we use command line to submit data instead of some kind of website?
>> Because for transfer of large files or many files, there can be time-out issues, encryption issues, or corruption issues.   Using the command line ensures secure and complete transfer.

> NOTE:  if you only have small files and are uncomfortable operating on the command line, you may want to try using a GUI tool like [Cyberduck](https://cyberduck.io/) to connect to S3 and manage your upload instead.  

### Obtain S3 credentials
1.	Go to https://bionimbus-pdc.opensciencedatacloud.org/storage/ Select and use the authentication method you gave in the [data inventory form](https://www.synapse.org/#!Synapse:syn8011461/wiki/413153)
2.	Download access keys by selecting the appropriate button next to the information for your username, e.g., under "Available BPA Datasets". The button is labeled “Generate S3 credential.” See Figure 1.
3.	Credentials appear as comma-separated values including an access key and a secret key. The secret key should remain secret.  Do not share these keys.

> NOTE:   Do not share the s3 credentials you gain below with anyone.  

> If you need to obtain new credentials, repeat steps (2.a) through (2.c). The button will now say “Rotate key” button, which will deactivate previous credentials and provide new ones.

### Figure 1
${image?fileName=bionimbussubmit%2Epng&align=None&responsive=true}

>KNOWN ISSUE: Safari will not provide S3 credentials on the first try. After generating keys once, press the “Rotate key” button.

### Install AWS CLI

#### Mac OSX or Linux/Unix
Open your “Terminal” application and type the following command:
```
sudo apt-get install awscli
```
or
```
sudo easy_install awscli
```
If prompted, enter your device’s password.

#### Windows
Download and run one of the windows installers at: https://aws.amazon.com/cli/

### Configure AWS CLI with the downloaded project credentials

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





