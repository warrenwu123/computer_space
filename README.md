# Lab 1

## AWS Accounts and Log In

### Step 1 Log into an IAM user account created for you on AWS.

First, i get to the website `[https://489389878001.signin.aws.amazon.com/console]`

### output:
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


# Lab 2

## Create an EC2 instance using awscli
### Step 1 : Create an EC2 instance using awscli

Code:
```
aws ec2 create-security-group --group-name 24372276-sg --description "security group for development environment"
```
explaination:
```
-Group-name:  the name of the group
-Description: to demonstrate what does this use for
-vpc—id: This is an optional choice, to define which vpc to use. If I don’t set this parameter, it will set the default vpc. 
For this project, we don’t need to set the vpc-id
```
then, we wull get the response including groupid and securitygrouparn
<img width="865" height="81" alt="image" src="https://github.com/user-attachments/assets/0cda75ef-e51d-4830-ad9d-ac87333f0bb9" />

### Step 2 : Authorise inbound traffic for ssh

In this part, we need to set the policy for inbound traffic
code:

```
aws ec2 authorize-security-group-ingress --group-name 24372276-sg --protocol tcp --port 22 --cidr 0.0.0.0/0
```

parameter:
```
--group-name
 confirm the group name that is fitting for this inbound rule. In this case, we put it as 24372276-sg
--protocol tcp
 Defines the protocol for incoming traffic. we set it to tcp, which is the common protocol 
--port 22
 This parameter are used to defines the port number that is being opened.
 22 is the default port for SSH access, which means this rule allows SSH connections to the EC2 instance.
--cidr 0.0.0.0/0
 CIDR (Classless Inter-Domain Routing) specifies which IPs are allowed to get access. 
 0.0.0.0/0 means allow the requests from all IPv4 addresses.
```

The output is like this below, it will show the securitygrouprules we just set 

<img width="865" height="229" alt="image" src="https://github.com/user-attachments/assets/57f3fcac-1c47-471f-9695-e1dedff1c566" />

### Step 3 Create a key pair

we need to create a key pair to let AWS verify identification from users, it will generate a public key on ec2 and private on our local machine.

code: 
```
aws ec2 create-key-pair --key-name <student number>-key --query 'KeyMaterial' --output text > <student number>-key.pem
```
We will use 24372276 to replace all the <student number> placeholder. 

Explaination:

```
--key-name <student number>-key
 This parameter is used to specifies the name of the key pair.


--query 'KeyMaterial'
 AWS returns a lot of information when creating a key pair, but the actual private key is under the field KeyMaterial.

 Using --query 'KeyMaterial' tells AWS only return the private key content.

--output text
 Ensures the private key is returned as plain text, not in JSON format.

> <student number>-key.pem

 The > redirects the output (the private key content) into a file
 <student number>-key.pem is the file name where the private key will be saved locally.
```

### Step 4: Set the permission for this 
By running this code, we set the private key to only-read mode.
```
chmod 400 24372276-key.pem
```

### Step 5: Launch a new  instance 

In this step, we launch the ec2 instance on AWS 

Code:
```
aws ec2 run-instances --image-id ami-010876b9ddd38475e --security-group-ids 24372276-sg --count 1 --instance-type t3.micro --key-name 24372276-key --query 'Instances[0].InstanceId'
```

Explaination:
```
--image-id <ami id>
Specifies the AMI (Amazon Machine Image) ID to use for the instance.
This can be found at the region table according to the region 

--security-group-ids <student number>-sg
Attaches your security group that just are defined before to the instance.
Security group defines the firewall rules for inbound/outbound traffic.

--count 1
The number of instances to launch.
Here it’s 1, meaning launch a single EC2 instance.

--instance-type t3.micro
Defines the instance type, which determines CPU, memory, and other resources.
t3.micro is a small, cost-efficient instance, often used for learning or testing.

--key-name 24372276-key
Associates the key pair I just created earlier with the instance.
This key is used for SSH access to the instance.

--query 'Instances[0].InstanceId'
Like we did before, this parameter limit the output of the console, Specifically, Filters the AWS CLI output to only return the ID of the first instance created.
InstanceId is a unique identifier for your EC2 instance (like i-0abcd1234ef56789).
```

This will return the output of instance id
<img width="865" height="43" alt="image" src="https://github.com/user-attachments/assets/f8badb20-9f35-4309-b9f8-86bc0a64e06a" />

### Step 6 Add a tag to your Instance
In this part, we would like to assign the name for our instance 
Code:
```
aws ec2 create-tags --resources <Instance Id from above> --tags Key=Name,Value=<Instance Name>
```
Explanation:
```
--resources <Instance Id from above>
Specifies the resource(s) we want to tag.
<Instance Id from above> should be replaced with the EC2 instance ID returned from the previous run-instances command 


--tags Key=Name,Value=<Instance Name>
Defines the tag key and value.
Key=Name is a common convention in AWS to give a human-readable name to an instance.
Value=<Instance Name> is the actual name you want to assign (e.g., MyEC2Instance). As The tutorial provided, I need to set the name of the tags as 24372276-vm
```

### Step 7 get the public ip address 
In this step, we are getting the ip address that ec2 opens for external users to get access to it 
Code: 
```
aws ec2 describe-instances --instance-ids <Instance Id from above> --query 'Reservations[0].Instances[0].PublicIpAddress'
```
This command is used to retrieve information about your EC2 instance, specifically its public IP address.

Explaination:
```
--instance-ids <Instance Id from above>
 Specifies the ID of the instance 

--query 'Reservations[0].Instances[0].PublicIpAddress'
 AWS CLI returns a large JSON object with all instance information.
 This query filters the output to return only the public IP address of the first instance in the first reservation.
```
This will return the output of ip address,which is `13.239.39.99`
<img width="865" height="38" alt="image" src="https://github.com/user-attachments/assets/a70cfa30-e6d7-434b-a679-0cfe5da41ec1" />

### Step 8 List the created instance using the AWS console
Then we use this ip address to connect the instance 

**Code:**

```
ssh -i 24372276-key.pem ubuntu@13.239.39.99
```
**Explaination:**

```
-i <student number>-key.pem
The -i option specifies the private key file to use for authentication.
-ubuntu@<IP Address from above>
ubuntu is the username for the EC2 instance.
  For Ubuntu AMIs, the default user is ubuntu.
  For Amazon Linux, it is usually ec2-user.
<IP Address from above> is the public IP I retrieved from the instance in step 7.
```
Then, after putting code, I connected the instance successfully. 

<img width="865" height="601" alt="image" src="https://github.com/user-attachments/assets/21f9c973-15e6-44e1-aeba-e8b023869a33" />

### Step 9: check the instance in AWS console

When I check the region ap-southeast-2, I can find the instance that is named by my id. 

<img width="865" height="109" alt="image" src="https://github.com/user-attachments/assets/b07f0a04-b793-43a2-b1a2-0e5d8de52679" />

## Create a python script 
In this part, we are going to use python script to create a new instance. For the new instance that we are going to create, we are going to set different key name, security group name and instance name 

following the steps like we just did before, I created the python script to create new instance
```
import boto3
import time

# ---------------------------
# User Configurations
# ---------------------------
student_number = "24372276"               
region_name = "ap-southeast-2"           
ami_id = "ami-010876b9ddd38475e"          
instance_type = "t3.micro"           
key_name = f"{student_number}-key2"  # set a different key_name
security_group_name = f"{student_number}-sg2"  # set a different security_group_name
instance_name = f"{student_number}-vm2" # set a different instance_name


# ---------------------------
# Create EC2 Client
# ---------------------------
ec2 = boto3.client("ec2", region_name=region_name)

# ---------------------------
# Step 1: Create Security Group
# ---------------------------
response_sg = ec2.create_security_group(
    GroupName=security_group_name,
    Description="Security group for development environment"
)
security_group_id = response_sg['GroupId']
print(f"Created security group {security_group_name} with ID: {security_group_id}")

# ---------------------------
# Step 2: Authorize SSH inbound traffic
# ---------------------------
ec2.authorize_security_group_ingress(
    GroupId=security_group_id,
    IpPermissions=[
        {
            'IpProtocol': 'tcp',
            'FromPort': 22,
            'ToPort': 22,
            'IpRanges': [{'CidrIp': '0.0.0.0/0'}]
        }
    ]
)
print(f"Authorized SSH inbound traffic for security group {security_group_name}")

# ---------------------------
# Step 3: Create Key Pair
# ---------------------------
key_pair = ec2.create_key_pair(KeyName=key_name)
key_file = f"{key_name}.pem"
with open(key_file, "w") as f:
    f.write(key_pair['KeyMaterial'])
print(f"Created key pair {key_name} and saved to {key_file}")

# Optionally, set file permissions to 400 (Linux/Mac)
# import os
# os.chmod(key_file, 0o400)

# ---------------------------
# Step 4: Launch EC2 Instance
# ---------------------------
response_instance = ec2.run_instances(
    ImageId=ami_id,
    InstanceType=instance_type,
    KeyName=key_name,
    SecurityGroupIds=[security_group_id],
    MinCount=1,
    MaxCount=1
)
instance_id = response_instance['Instances'][0]['InstanceId']
print(f"Launched EC2 instance with ID: {instance_id}")

# ---------------------------
# Step 5: Add Name Tag to Instance
# ---------------------------
ec2.create_tags(
    Resources=[instance_id],
    Tags=[{'Key': 'Name', 'Value': instance_name}]
)
print(f"Tagged instance {instance_id} with Name: {instance_name}")

# ---------------------------
# Step 6: Get Public IP Address
# ---------------------------
# Wait a few seconds for the public IP to be assigned
time.sleep(5)

response_desc = ec2.describe_instances(InstanceIds=[instance_id])
public_ip = response_desc['Reservations'][0]['Instances'][0].get('PublicIpAddress')
print(f"Public IP address of instance {instance_id}: {public_ip}")
```

When I ran the python script, it will return the ip address finally. 

**Output:**

<img width="865" height="94" alt="image" src="https://github.com/user-attachments/assets/943adbb9-7a24-4fd2-91f9-dee194aa329c" />


## Install Docker

## Step 1 Install Docker






































