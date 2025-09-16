<img width="865" height="383" alt="image" src="https://github.com/user-attachments/assets/f26abcbc-b002-4e74-9fd7-2cf3dcce7905" />## AWS Accounts and Log In

### Step 1 Log into an IAM user account created for you on AWS.

First, i get to the website `[https://489389878001.signin.aws.amazon.com/console]`


<img width="1857" height="966" alt="ee" src="https://github.com/user-attachments/assets/dd230773-922d-4b1c-9cc6-9450930caf27" />

then, I used the username `24372276@student.uwa.edu.au` and password to login in to console, it will show this page below

<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/2714d19a-7865-4166-a7fb-9acc812d9ff3" />

### Step 2 Search and open Identity Access Management

I clicked the IAM-Security Credential part, entering into this page below 

<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/a7f6f74b-d6e9-4a74-82da-76d20e61818c" />

then, i clicked `create access key` to create access key 

First, we need to choose use case. As we would like to use this access key to access AWS in the command interface, so we choose CLI as use case.

<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/57de8538-dae1-4eb7-97ce-689783902224" />

Second is the description for this key. I set it to " Connect to AWS service from Linux

<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/d6e15f22-490e-4a0d-b1df-d281918e731d" />

Then, click access key, we can get our access key, which has access key and secret access key. 

<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/2a0dc0e1-058c-4c2a-a602-5078a3897bdc" />


## Set up recent Unix-like OSes

I'm the Windows Users. when I input wsl to my poershell, it will go into wsl 
<img width="1644" height="174" alt="image" src="https://github.com/user-attachments/assets/624010ec-384d-439a-adca-3b21c9a11453" />

then, i would like to check the version of my wsl, i input the code below
```
wsl -l -v
```
we can see the version of wsl, which is ubuntu 24.04
<img width="615" height="105" alt="image" src="https://github.com/user-attachments/assets/104397da-ffc2-40b9-b48f-5905fea4b847" />

## Install Linux packages

### step 1 Install Python

First, I updated all the packages to the lastest version by putting the code below 

```
sudo apt update
sudo apt -y upgrade

```

Then, check the version of python by putting the code below, showing that i have the lastest version python 

```
python3 -V

```

<img width="865" height="65" alt="image" src="https://github.com/user-attachments/assets/5e077159-d270-4aee-acfb-648ec3760c79" />


Then, I install the pip3 packages 

```
sudo apt install -y python3-pip

```

<img width="865" height="564" alt="image" src="https://github.com/user-attachments/assets/acd43a87-208a-4710-a2b9-74c07a5f8358" />

### step 2 Install awscli

we use the code below to install awscli, which is the package that allows us to configure aws and get access to aws service 

```
sudo apt install awscli

```
but it shows the package seems to be obsolete 
<img width="865" height="194" alt="image" src="https://github.com/user-attachments/assets/6bd790c3-38b8-4d7d-81d1-3ffcf435518b" />

So, i changed another way to install this package by running this code below 

```
sudo snap install aws-cli --classic

```
```
--snap: a package management tool shop for wsl, like apt

--classic: classic confinemen mode, allowing aws-cli to get access to system file and resource.

```

After doing this, it will be installed successfully 
<img width="865" height="62" alt="image" src="https://github.com/user-attachments/assets/07876c1a-a848-4861-be84-64e4543a018f" />

### step 3 Configure AWS

put the code below to configure aws 

```
aws configure

```
it will activate the configure interface 

<img width="865" height="127" alt="image" src="https://github.com/user-attachments/assets/a4ccb44b-3df7-47a7-87cc-83589be0db38" />

we will be required to input four types of information `AWS access key ID`, `AWS Secret Access Key`, `Default Region name`, `Default output format`

the first two information can be found at the last step of creating access key. 
From the region table, i can find the region name is `ap-southeast-2` according to my student id
And the default output format is json 

<img width="865" height="127" alt="image" src="https://github.com/user-attachments/assets/23bc4275-6003-4ef0-9c0a-479fb8305b85" />

### step 4 Install boto3

boto3 is the root package to use all the services and resources in AWS, so we need to install it by putting the code below 

```
sudo apt install python3-boto3

```
instead of usin `pip3`, I use `sudo apt install` to get package from the remote package shop directly. 

And we successfully installed it 

<img width="865" height="383" alt="image" src="https://github.com/user-attachments/assets/5fb65d27-7795-4f86-8ad6-5f971a8dcc43" />


## Test the installed environment


### step 1 Test the AWS environment

For this part, we need to test if AWS is configured successfully and if we can get access to its service and resources.

First, we 

```
aws ec2 describe-regions --output table

```
```
--ec2:define the service as ec2

```
```
describe-regions: describe all the available regions that can be used
```
```
--output table: define the format of output to table
```

So, we will get the table including all the available regions in AWS
<img width="865" height="493" alt="image" src="https://github.com/user-attachments/assets/61e123f5-ec96-46ff-b277-9c9f95315043" />


### step 2 Test the python environment

Second, we need to test if the python works

So,we run `python3` to activate python edit page

then, we put the code below in console

```
import boto3
ec2 = boto3.client('ec2')
response = ec2.describe_regions()
print(response)

```
```
ec2 = boto3.client('ec2') : create a ec2 object to allow you to use ec2 service by this object
```
```
response = ec2.describe_regions(): retreive all regions and return to response
```
then, i will get the json file including all regions 

<img width="865" height="418" alt="image" src="https://github.com/user-attachments/assets/bb3b9f38-12f7-423a-a0fc-378d8a41b338" />

### Step 3 Write a Python script
In this part, we would like to show region table by usin python script

in order to show the endpoint and regionname table, we need to install tabulate first, which is a library that can make data as a table 

So we put this code below

```
pip install tabulate --break-system-packages

```

```

--break-system-packages: pass the external envrionment notice

```
<img width="865" height="135" alt="image" src="https://github.com/user-attachments/assets/8b19ebe1-2cf4-403a-a23f-d7975b31abc1" />

Then, we put the code below into console to create a region table 

```
import boto3
from tabulate import tabulate
ec2 = boto3.client("ec2")

response = ec2.describe_regions()

data = []
for region in response["Regions"]:
data.append([region["Endpoint"], region["RegionName"]])

print(tabulate(data, headers=["Endpoint", "RegionName"]))
```
For response, it will be a key called Regions that includes all the regions, so I retrieve them all and put it into list one by one, then display them as table by usin tabulate

The output is just like this, from this table, we can see all the endpoints and region name 

<img width="865" height="367" alt="image" src="https://github.com/user-attachments/assets/a26708fb-1ad3-4016-91e4-ebb46b59316c" />























