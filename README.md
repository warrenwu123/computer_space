# Lab 1

## AWS Accounts and Log In

### Step 1 Log into an IAM user account created for you on AWS.

First, i get to the website `[https://489389878001.signin.aws.amazon.com/console]`

### output:
<img width="1857" height="966" alt="ee" src="https://github.com/user-attachments/assets/dd230773-922d-4b1c-9cc6-9450930caf27" />

then, I used the username `24372276@student.uwa.edu.au` and password to login in to console, it will show this page below

### output:
<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/2714d19a-7865-4166-a7fb-9acc812d9ff3" />

### Step 2 Search and open Identity Access Management

I clicked the IAM-Security Credential part, entering into this page below 

### output:
<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/a7f6f74b-d6e9-4a74-82da-76d20e61818c" />


then, i clicked `create access key` to create access key 

First, we need to choose use case. As we would like to use this access key to access AWS in the command interface, so we choose CLI as use case.

### output:
<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/57de8538-dae1-4eb7-97ce-689783902224" />


Second is the description for this key. I set it to " Connect to AWS service from Linux

### output:
<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/d6e15f22-490e-4a0d-b1df-d281918e731d" />


Then, click access key, we can get our access key, which has access key and secret access key. 

### output:
<img width="865" height="427" alt="image" src="https://github.com/user-attachments/assets/2a0dc0e1-058c-4c2a-a602-5078a3897bdc" />


## Set up recent Unix-like OSes

I'm the Windows Users. when I input wsl to my poershell, it will go into wsl 
### output:
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

### Step 1 Install Docker

Code:
```
sudo apt install docker.io -y
```

Explaination:
```
This command is used for downloading the docker package
```

<img width="865" height="366" alt="image" src="https://github.com/user-attachments/assets/5bff8ddb-cfd1-4ea5-9d72-0a9a99266089" />

### Step 2 start and enable docker 

running those two code lines to start and enable docker, then we could use it to get image or create image later

```
sudo systemctl start docker
sudo systemctl enable docker
```

### Step 3 check the version 

Code:
```
docker –version
```

<img width="865" height="42" alt="image" src="https://github.com/user-attachments/assets/8d597ef3-446a-4fda-8ad2-6a56025b6542" />


## Build and run an httpd container

### Step 1 create html file and Dockerfile

First, I created a new directory html by inputting code

```
mkdir html
```
Then, go into this directory and create a file html.
```
cd ./html
touch index.html
```
touch is the command that is used to create the new file

then, I added the basic html code into it.

Output:
<img width="1329" height="345" alt="image" src="https://github.com/user-attachments/assets/b327890f-b3aa-4e51-b5c5-9df563cd5488" />


then, go back to root directory and create a new file Dockerfile 

```
cd ..
touch Dockerfile
```

then, edit the Dockerfile to add the code below 

Code: 
```
FROM httpd:2.4
COPY ./html/ /usr/local/apache2/htdocs/
```

Explanation:
```
FROM is used to tell Docker which base image to start from.
Httpd:2.4 : it represents the official Apache HTTP Server (httpd)

COPY ./html/ /usr/local/apache2/htdocs/
This piece of code is used to copy files from your computer (build context) into the image.
./html/ : this locates the local folder html 
/usr/local/apache2/htdocs/: this is the default folder of image
```

<img width="1317" height="219" alt="image" src="https://github.com/user-attachments/assets/d79a7dbb-314b-4fb2-9a47-32a089549cee" />

### Step 2 Build a docker image

In this step, we would like to build an image.

Code:
```
docker build -t my-apache2 .
```

Explaination:

```
-t (or --tag) assigns a name (and optionally a tag) to the image.

In this case, the image will be called my-apache2.

After my-apache2, it will be the path, which tells Docker where to look for the Dockerfile and any files referenced inside it.In this case, it will be current path,so it will be .
```

<img width="865" height="406" alt="image" src="https://github.com/user-attachments/assets/49fe354b-cc3b-4a69-854c-9650ca148843" />

### Step 3 run docker 

Code:
```
docker run -p 80:80 -dit --name my-app my-apache2
```

Explaination:
```
-p 80:80
Maps host port 80 to container port 80.
Apache inside the container listens on port 80.

For dit, it will be split into three parameters: 
-d
Run the container in detached mode (in the background).
Without -d, Docker would attach logs to your terminal.

-i
Keep STDIN (input stream) open, even if not attached.
Often used together with -t.

-t
Allocate a pseudo-TTY (a terminal).
Makes the container behave like it has a real terminal.

--name my-app
Assigns a custom name (my-app) to the container.
```
After running this code, get access to the url http://localhost. It will show the hello world successfully.

<img width="658" height="368" alt="image" src="https://github.com/user-attachments/assets/f6fe78df-a6e7-482f-954b-74a8d0baf58a" />

### Step 4 remove docker

First, showing all the current running docker

Code:
```
docker ps -a
```

<img width="1713" height="141" alt="image" src="https://github.com/user-attachments/assets/8ae983d2-c9a5-4726-bebc-6780da9c274f" />

Second, stop the current running docker my-app
```
docker stop my-app
```

<img width="948" height="69" alt="image" src="https://github.com/user-attachments/assets/dece645c-70d9-4351-9d07-1022f79b75b3" />

Then, remove it and list it again, it will show no docker is running 

```
docker rm my-app
docker ps -a
```

<img width="1095" height="126" alt="image" src="https://github.com/user-attachments/assets/b7f76864-cc59-4101-85b4-ea423eab1136" />


# Lab 3

## Preparation 

### Step1 Create a directory rootdir

Execute the code below to create a directory rootdir

```
Mkdir rootdir
```

And then input the code below to create file rootdir.txt 

```
cd ./rootdir
touch rootfile.txt
```

then, create a subdir directory and subdir.txt as the same way
```
Mkdir subdir
touch subdir.txt
```

and write some contents that are required in them

<img width="940" height="536" alt="image" src="https://github.com/user-attachments/assets/23c73dcc-a038-4e42-89c0-05d0e9c5445b" />

### Step2 Save files to S3 bucket

I changed the cloudstorage.py like this below. This piece of code helps us create s3 bucket with the name that I defined and find the rootdir directory and all the files inside it, then put them all into s3 bucket

```
import os
import boto3
import botocore

# ------------------------------
# CITS5503
#
# cloudstorage.py
#
# Copies local files to S3
#
# Given a root local directory, will return files in each level and
# copy to same path on S3
# ------------------------------

# Change these values as needed
ROOT_DIR = 'rootdir'                       # root local directory
STUDENT_ID = '24372276'                 # set the student id
ROOT_S3_DIR = f'24372276-cloudstorage'  # use my id to name S3 bucket
REGION_NAME = 'ap-southeast-2'             # region name 

# Create S3 client
s3 = boto3.client('s3', region_name=REGION_NAME)

# Create S3 bucket if it does not exist
try:
    # Bucket creation is region-dependent
    if REGION_NAME == 'us-east-1':
        response = s3.create_bucket(Bucket=ROOT_S3_DIR)
    else:
        response = s3.create_bucket(
            Bucket=ROOT_S3_DIR,
            CreateBucketConfiguration={'LocationConstraint': REGION_NAME}
        )
    print(f"Bucket '{ROOT_S3_DIR}' created successfully.")
except botocore.exceptions.ClientError as error:
    if error.response['Error']['Code'] == 'BucketAlreadyOwnedByYou':
        print(f"Bucket '{ROOT_S3_DIR}' already exists and is owned by you.")
    else:
        raise

def upload_file(folder_name, local_file_path, file_name):
    """
    Upload a file to the S3 bucket, preserving the folder structure.
    folder_name: path inside S3 (e.g., subdir/)
    local_file_path: local file path
    file_name: just the file name
    """
    # Compose key (path inside bucket)
    if folder_name:
        s3_key = f"{folder_name}/{file_name}".replace('//', '/')
    else:
        s3_key = file_name

    print(f"Uploading '{local_file_path}' to 's3://{ROOT_S3_DIR}/{s3_key}' ...")
    s3.upload_file(local_file_path, ROOT_S3_DIR, s3_key)

# Traverse directory and upload files
for dir_name, subdir_list, file_list in os.walk(ROOT_DIR, topdown=True):
    relative_dir = os.path.relpath(dir_name, ROOT_DIR)
    if relative_dir == '.':
        relative_dir = ''     # root level, no prefix
    for fname in file_list:
        local_path = os.path.join(dir_name, fname)
        upload_file(relative_dir, local_path, fname)

print("All files uploaded successfully.")
```

When I ran this code, it will show that we already put the all the files into the corresponded folder. 

<img width="940" height="104" alt="image" src="https://github.com/user-attachments/assets/7cdc71e0-99a9-4e71-bbf5-5b0222d70ba0" />


### Step 3 Restore from S3

I created the python script called restorefromcloud.py to Restore files from S3 and make the local directory and file keep the same structure and content.
Specifically, I created a new directory called restored_rootdir as the rootdir, then copy the file as corresponded path. 

```
import os
import boto3

# ------------------------------
# CITS5503
#
# restorefromcloud.py
#
# Restores files from S3 bucket to local directory,
# recreating the same structure as originally uploaded.
# ------------------------------

STUDENT_ID = '24372276'                  # <-- Replace with your real student ID
ROOT_S3_DIR = f'24372276-cloudstorage'  # Your S3 bucket name
RESTORE_DIR = 'restored_rootdir'            # Local directory where files will be restored
REGION_NAME = 'ap-southeast-2'              # Replace with your AWS region

# Create S3 client
s3 = boto3.client('s3', region_name=REGION_NAME)

# Ensure restore directory exists
if not os.path.exists(RESTORE_DIR):
    os.makedirs(RESTORE_DIR)

# List objects in the bucket
response = s3.list_objects_v2(Bucket=ROOT_S3_DIR)

if 'Contents' not in response:
    print(f"No files found in bucket '{ROOT_S3_DIR}'.")
else:
    for obj in response['Contents']:
        key = obj['Key']          # S3 object key (path in bucket)
        local_path = os.path.join(RESTORE_DIR, key)

        # Ensure local directory exists
        os.makedirs(os.path.dirname(local_path), exist_ok=True)

        # Download file
        print(f"Downloading 's3://{ROOT_S3_DIR}/{key}' to '{local_path}' ...")
        s3.download_file(ROOT_S3_DIR, key, local_path)

print("All files restored successfully.")
```
When I ran the code, it will show all files restored successfully. 
<img width="940" height="72" alt="image" src="https://github.com/user-attachments/assets/eb3ee8c5-5b9b-4ad3-a6d7-4d49c06e4244" />

And when I check my directory,  the restored_rootdir has been created and keep the same structure and file content.
<img width="504" height="141" alt="image" src="https://github.com/user-attachments/assets/913eb347-8967-44cf-af0b-568bbc05df65" />


### Step 4: Write information about files to DynamoDB

First, create the dynamodb directory and get into it. 
```
mkdir dynamodb
```

Then, we need to get the dynamodb running in the local machine. 
To get this, we need to install the jre package first, which allows your system to run Java programs

```
sudo apt-get install default-jre
```

then we get the dynamodb_local_latest.tar.gz from remote repository. 
```
wget https://s3-ap-northeast-1.amazonaws.com/dynamodb-local-tokyo/dynamodb_local_latest.tar.gz
```
we will get the dynamodb_local_latest.tar.gz file, which is a compiled file for all tar files for local 

<img width="408" height="42" alt="image" src="https://github.com/user-attachments/assets/8a415b5f-4ea7-4125-9ac8-f3dc56668fda" />


then, we extract files from dynamodb_local_latest.tar.gz

```
tar -zxvf dynamodb_local_latest.tar.gz
```

<img width="940" height="593" alt="image" src="https://github.com/user-attachments/assets/a0b9889d-ada5-4f54-a337-279196f87ff0" />

it will retreive all the files that initialized the DynamnoDB
<img width="462" height="303" alt="image" src="https://github.com/user-attachments/assets/219702d3-19b6-4fd4-aabd-3b882df5c256" />

then we run the code below to activate local DynamoDB

```
java -Djava.library.path=./DynamoDBLocal_lib -jar DynamoDBLocal.jar -sharedDb
```

From the wsl, we can see the DynamoDB is running now 

<img width="940" height="164" alt="image" src="https://github.com/user-attachments/assets/e6efded8-b7b8-4b5e-ab9c-4a987481e231" />


Next, we need to create table on our local database. So first, we create python script to finish the logic. The python script we created is as below.

```
import boto3
import os
from datetime import datetime

# -----------------------------
# 1. Connect to local DynamoDB
# -----------------------------
dynamodb = boto3.resource(
    "dynamodb",
    region_name="ap-southeast-2",
    endpoint_url="http://localhost:8000"  # Local DynamoDB endpoint
)

# -----------------------------
# 2. Create the table if not exists
# -----------------------------
table_name = "CloudFiles"

existing_tables = dynamodb.meta.client.list_tables()["TableNames"]
if table_name not in existing_tables:
    table = dynamodb.create_table(
        TableName=table_name,
        KeySchema=[
            {"AttributeName": "userId", "KeyType": "HASH"},  # Partition key
            {"AttributeName": "fileName", "KeyType": "RANGE"},  # Sort key
        ],
        AttributeDefinitions=[
            {"AttributeName": "userId", "AttributeType": "S"},
            {"AttributeName": "fileName", "AttributeType": "S"},
        ],
        ProvisionedThroughput={
            "ReadCapacityUnits": 5,
            "WriteCapacityUnits": 5
        }
    )
    table.wait_until_exists()
    print(f"✅ Table '{table_name}' created successfully.")
else:
    table = dynamodb.Table(table_name)
    print(f"ℹ️ Table '{table_name}' already exists.")

# -----------------------------
# 3. Connect to S3
# -----------------------------
s3 = boto3.client("s3")
bucket_name = "24372276-cloudstorage"  # 🔴 Replace with your S3 bucket name

# -----------------------------
# 4. List all files in S3 bucket
# -----------------------------
response = s3.list_objects_v2(Bucket=bucket_name)
if "Contents" not in response:
    print("⚠️ No files found in S3 bucket.")
    exit()

# -----------------------------
# 5. Insert file attributes into DynamoDB
# -----------------------------
for obj in response["Contents"]:
    file_name = os.path.basename(obj["Key"])
    path = obj["Key"]
    last_updated = obj["LastModified"].isoformat()

    acl_owner = s3.get_bucket_acl(Bucket=bucket_name)["Owner"]

    # userId must be the owner ID
    user_id = acl_owner.get("ID")

    # owner = DisplayName if available, otherwise fallback to ID
    owner = acl_owner.get("DisplayName") or acl_owner.get("ID")

    # Permissions can be derived from ACL grants
    acl = s3.get_object_acl(Bucket=bucket_name, Key=path)
    permissions = [grant["Permission"] for grant in acl["Grants"]]

    # Write item to DynamoDB
    table.put_item(
        Item={
            "userId": user_id,
            "fileName": file_name,
            "path": path,
            "lastUpdated": last_updated,
            "owner": owner,
            "permissions": str(permissions)  # Store as string
        }
    )
    print(f"✅ Inserted {file_name} into DynamoDB")

print("🎉 All S3 file attributes inserted into DynamoDB successfully.")
```

Explaination:

```
we need to create table from the s3 bucket, so we use the same s3 bucket name that we created before. And set the end_point to localhost:8000, which is the default port for local db program.
And as the requirements, we extract all the attributes from the response that is returned by the S3 bucket and put them into the local DynamoDB
```

<img width="940" height="138" alt="image" src="https://github.com/user-attachments/assets/93d48d4a-5283-472d-8a4f-5f52198a4f91" />

### Step 5: scan the table

We use the code to scan the local tables 
```
aws dynamodb scan \
    --table-name CloudFiles \
--endpoint-url http://localhost:8000
```

```
--table-name CloudFiles: choose which table we want to scan
--endpoint-url
```

Then, we can see the output on the console
```
{
    "Items": [
        {
            "owner": {
                "S": "zhi.zhang"
            },
            "path": {
                "S": "rootfile.txt"
            },
            "lastUpdated": {
                "S": "2025-09-15T12:38:27+00:00"
            },
            "fileName": {
                "S": "rootfile.txt"
            },
            "userId": {
                "S": "2a5fac7aada1ad2caa48c9ab08cc4e2428d4eb596108daa3b59f1204ae96482e"
            },
            "permissions": {
                "S": "['FULL_CONTROL']"
            }
        },
        {
            "owner": {
                "S": "zhi.zhang"
            },
            "path": {
                "S": "subdir/subfile.txt"
            },
            "lastUpdated": {
                "S": "2025-09-15T12:38:28+00:00"
            },
            "fileName": {
                "S": "subfile.txt"
            },
            "userId": {
                "S": "2a5fac7aada1ad2caa48c9ab08cc4e2428d4eb596108daa3b59f1204ae96482e"
            },
            "permissions": {
                "S": "['FULL_CONTROL']"
            }
        }
    ],
    "Count": 2,
    "ScannedCount": 2,
    "ConsumedCapacity": null
}
```

### Step 6 delete the table

Code:
```
aws dynamodb delete-table \
    --table-name CloudFiles \
--endpoint-url http://localhost:8000
```

Then we get the outcome in the console

```
{
    "TableDescription": {
        "AttributeDefinitions": [
            {
                "AttributeName": "userId",
                "AttributeType": "S"
            },
            {
                "AttributeName": "fileName",
                "AttributeType": "S"
            }
        ],
        "TableName": "CloudFiles",
        "KeySchema": [
            {
                "AttributeName": "userId",
                "KeyType": "HASH"
            },
            {
                "AttributeName": "fileName",
                "KeyType": "RANGE"
            }
        ],
        "TableStatus": "ACTIVE",
        "CreationDateTime": 1757949512.3,
        "ProvisionedThroughput": {
            "LastIncreaseDateTime": 0.0,
            "LastDecreaseDateTime": 0.0,
            "NumberOfDecreasesToday": 0,
            "ReadCapacityUnits": 5,
            "WriteCapacityUnits": 5
        },
        "TableSizeBytes": 371,
        "ItemCount": 2,
        "TableArn": "arn:aws:dynamodb:ddblocal:000000000000:table/CloudFiles",
        "DeletionProtectionEnabled": false
    }
}
```

# Lab 4 

## Apply a policy to restrict permissions on the bucket
### Step 1 Apply policy to my S3 bucket

First, I created a new S3 bucket with the same name and region name

<img width="865" height="58" alt="image" src="https://github.com/user-attachments/assets/2ed0cdfa-6405-47e7-ade4-aabbabdc65c2" />

Second, I wrote a python script to set policy to my bucket.

```
import boto3
import json

# -----------------------------
# 1. Define your variables
# -----------------------------
bucket_name = "24372276-cloudstorage"       
student_number = "24372276"      
username = f"{student_number}@student.uwa.edu.au"

# -----------------------------
# 2. Create S3 client
# -----------------------------
s3 = boto3.client("s3")

# -----------------------------
# 3. Define the bucket policy
# -----------------------------
policy = {
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "AllowAllS3ActionsInUserFolderForUserOnly",
            "Effect": "DENY",
            "Principal": "*",
            "Action": "s3:*",
            "Resource": [
                f"arn:aws:s3:::{bucket_name}",                     # Bucket itself
                f"arn:aws:s3:::{bucket_name}/folder1/folder2/*"   # Objects inside folder
            ],
            "Condition": {
                "StringNotLike": {
                    "aws:username": username
                }
            }
        }
    ]
}

# Convert policy to JSON string
policy_json = json.dumps(policy)

# -----------------------------
# 4. Apply the policy to the bucket
# -----------------------------
response = s3.put_bucket_policy(
    Bucket=bucket_name,
    Policy=policy_json
)

print("✅ Bucket policy applied successfully!")
```
This code will set the limit to my bucket, allowing no one to connect except me.

Explaination for policy set:
```
Effect : DENY. This rule denies access to matching users and resources.
Principal :"*", means that applies to all users.
Action :"s3:*" Denies all S3 actions (read, write, delete, etc.).
Resource means List of resources this rule applies to:
1.	arn:aws:s3:::{bucket_name} : the bucket itself.
2.	arn:aws:s3:::{bucket_name}/folder1/folder2/* : all objects inside folder1/folder2.
```

The condition part means there are some conditions can limit the deny

```
"StringNotLike" : applies the DENY only if the user’s AWS username does NOT match the username I set.
```

Then, we run this python script.

<img width="865" height="50" alt="image" src="https://github.com/user-attachments/assets/c7e42eec-78db-4fcc-8879-43b413155460" />


### Step 2 Check whether the script works
We use the command below to list all the policies within my bucket. 

```
aws s3api get-bucket-policy --bucket <s3_bucket_name>
```
Explaination:
```
aws s3api : Uses the low-level S3 API commands in AWS CLI. The low-level S3 api has more control to s3 bucket. 
get-bucket-policy : Retrieves the policy JSON currently applied to the bucket.
bucket <s3_bucket_name>: Replace <s3_bucket_name> with our own bucket name.
```
it will show the policy we just set 
<img width="1704" height="180" alt="image" src="https://github.com/user-attachments/assets/ce92cc1c-33ea-4388-8cea-20ff0b80d330" />

## AES Encryption using KMS

### Step 1 Create a KMS key

I will create a python script to create KMS key and set the alias name for the KMS key 

```
import boto3

kms = boto3.client('kms', region_name='ap-southeast-2')

# Create a KMS key
response = kms.create_key(
    Description='Lab KMS key',
    KeyUsage='ENCRYPT_DECRYPT',
    CustomerMasterKeySpec='SYMMETRIC_DEFAULT'
)

key_id = response['KeyMetadata']['KeyId']

# Create alias for your key using student number
alias_name = f'alias/24372276'
kms.create_alias(
    AliasName=alias_name,
    TargetKeyId=key_id
)

print(f"KMS key created with ID: {key_id} and alias: {alias_name}")
```
Explaination:

```
Description='Lab KMS key' : Description

KeyUsage='ENCRYPT_DECRYPT' : allows this key to encrypt and decrypt data.

CustomerMasterKeySpec='SYMMETRIC_DEFAULT' :
creates a symmetric key (same key is used for encryption and decryption).
This is the common choice for data encryption (AES-256).
```


Step 2: Attach a policy to the created KMS key

To  attach the policy to the created KMS key, I created a new script set_policy_to_kms.py. By getting key id from alias, we can set the policy into kms successfully. 

```
import boto3
import json

kms = boto3.client('kms', region_name='ap-southeast-2')

alias_name = 'alias/24372276'

response = kms.list_aliases()  # list all the alias 
key_id = None
for alias in response['Aliases']:
    if alias['AliasName'] == alias_name:
        key_id = alias['TargetKeyId']
        break

if key_id:
    print(f"Found key ID: {key_id}")
else:
    print("Alias not found")

key_policy = {
  "Version": "2012-10-17",
  "Id": "key-consolepolicy-3",
  "Statement": [
    {
      "Sid": "Enable IAM User Permissions",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::489389878001:root"
      },
      "Action": "kms:*",
      "Resource": "*"
    },
    {
      "Sid": "Allow access for Key Administrators",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::489389878001:user/24372276@student.uwa.edu.au"
      },
      "Action": [
        "kms:Create*",
        "kms:Describe*",
        "kms:Enable*",
        "kms:List*",
        "kms:Put*",
        "kms:Update*",
        "kms:Revoke*",
        "kms:Disable*",
        "kms:Get*",
        "kms:Delete*",
        "kms:TagResource",
        "kms:UntagResource",
        "kms:ScheduleKeyDeletion",
        "kms:CancelKeyDeletion"
      ],
      "Resource": "*"
    },
    {
      "Sid": "Allow use of the key",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::489389878001:user/24372276@student.uwa.edu.au"
      },
      "Action": [
        "kms:Encrypt",
        "kms:Decrypt",
        "kms:ReEncrypt*",
        "kms:GenerateDataKey*",
        "kms:DescribeKey"
      ],
      "Resource": "*"
    },
    {
      "Sid": "Allow attachment of persistent resources",
      "Effect": "Allow",
      "Principal": {
        "AWS": "arn:aws:iam::489389878001:user/24372276@student.uwa.edu.au"
      },
      "Action": [
        "kms:CreateGrant",
        "kms:ListGrants",
        "kms:RevokeGrant"
      ],
      "Resource": "*",
      "Condition": {
        "Bool": {
          "kms:GrantIsForAWSResource": "true"
        }
      }
    }
  ]
}

kms.put_key_policy(
    KeyId=key_id,
    Policy=json.dumps(key_policy),
    PolicyName='default'
)

print("Key policy set successfully.")
```
Use the put_key_policy method to put the policy into a specific key id

when we run this code, we can see

<img width="865" height="74" alt="image" src="https://github.com/user-attachments/assets/b8358415-9d65-4729-bc89-db44da734c2e" />

### Step 3 Check whether the script works

In the AWS KMS console, I clicked the alias named 24372276 that I just set, and we can see the policy showing that I’m the only key administrator and user
<img width="865" height="212" alt="image" src="https://github.com/user-attachments/assets/63488c5b-99bd-4af8-b41a-e80774228ea1" />
<img width="865" height="429" alt="image" src="https://github.com/user-attachments/assets/cb6bc5c1-098b-49b7-b8c6-befaa72800c2" />

### Step 4: encrypt and decrypt file from s3

First, we created a new folder called kmsfile to store the outcome.
```
mkdir kmsfile
```

Then, we write a script to get all files from s3 bucket and encrypt and decrypt them one by one. 
Code:
```
import boto3
import os

# ----------------- Config -----------------
bucket_name = "24372276-cloudstorage"
kms_key_id = "7b7d2e3e-05ba-4f18-bc7a-62deac73a34d"  # e.g., from alias or KeyId
local_folder = "./kmsfile"  # local folder for downloaded/encrypted/decrypted files

# Initialize clients
s3 = boto3.client("s3")
kms = boto3.client("kms")

# Ensure local folder exists
os.makedirs(local_folder, exist_ok=True)

# ----------------- List files in S3 -----------------
response = s3.list_objects_v2(Bucket=bucket_name)
if "Contents" not in response:
    print("No files found in the bucket.")
    exit()

for obj in response["Contents"]:
    file_name = obj["Key"]
    local_file_path = os.path.join(local_folder, file_name.replace("/", "_"))

    # ----------------- Download the file -----------------
    s3.download_file(bucket_name, file_name, local_file_path)
    print(f"Downloaded {file_name} -> {local_file_path}")

    # ----------------- Encrypt the file using KMS -----------------
    with open(local_file_path, "rb") as f:
        plaintext = f.read()

    encrypt_response = kms.encrypt(
        KeyId=kms_key_id,
        Plaintext=plaintext
    )
    encrypted_data = encrypt_response["CiphertextBlob"]

    encrypted_file_path = local_file_path + ".enc"
    with open(encrypted_file_path, "wb") as f_enc:
        f_enc.write(encrypted_data)
    print(f"Encrypted {file_name} -> {encrypted_file_path}")

    # ----------------- Decrypt the file using KMS -----------------
    with open(encrypted_file_path, "rb") as f_enc:
        ciphertext = f_enc.read()

    decrypt_response = kms.decrypt(
        CiphertextBlob=ciphertext
    )
    decrypted_data = decrypt_response["Plaintext"]

    decrypted_file_path = local_file_path + ".dec"
    with open(decrypted_file_path, "wb") as f_dec:
        f_dec.write(decrypted_data)
    print(f"Decrypted {file_name} -> {decrypted_file_path}")
```


<img width="865" height="186" alt="image" src="https://github.com/user-attachments/assets/b4cbe976-165c-43ce-b41b-85a35c5b35c2" />

### Step 5 Apply pycryptodome for encryption/decryption

In this step, we use a new method pycryptodome to encrypt and decrypt files 

First we need to install the pycryptodome package. 
```
Pip3 install pycryptodome
```

Then, we create a script to encrypt and decrypt all the files from s3 as the way of example script. This time we used a new directory ./pycryptodome_files to store the encrypted and decrypted files 

```
import os
import struct
import hashlib
from Crypto.Cipher import AES
from Crypto import Random
import boto3

BLOCK_SIZE = 16
CHUNK_SIZE = 64 * 1024

# -----------------------------
# Encryption / Decryption funcs
# -----------------------------
def encrypt_file(password, in_filename, out_filename):
    """Encrypt file with AES CBC"""
    key = hashlib.sha256(password.encode("utf-8")).digest()
    iv = Random.new().read(AES.block_size)
    encryptor = AES.new(key, AES.MODE_CBC, iv)
    filesize = os.path.getsize(in_filename)

    with open(in_filename, "rb") as infile:
        with open(out_filename, "wb") as outfile:
            outfile.write(struct.pack("<Q", filesize))
            outfile.write(iv)

            while True:
                chunk = infile.read(CHUNK_SIZE)
                if len(chunk) == 0:
                    break
                elif len(chunk) % BLOCK_SIZE != 0:
                    chunk += b" " * (BLOCK_SIZE - len(chunk) % BLOCK_SIZE)

                outfile.write(encryptor.encrypt(chunk))


def decrypt_file(password, in_filename, out_filename):
    """Decrypt file with AES CBC"""
    key = hashlib.sha256(password.encode("utf-8")).digest()

    with open(in_filename, "rb") as infile:
        origsize = struct.unpack("<Q", infile.read(struct.calcsize("Q")))[0]
        iv = infile.read(16)
        decryptor = AES.new(key, AES.MODE_CBC, iv)

        with open(out_filename, "wb") as outfile:
            while True:
                chunk = infile.read(CHUNK_SIZE)
                if len(chunk) == 0:
                    break
                outfile.write(decryptor.decrypt(chunk))
            outfile.truncate(origsize)

# -----------------------------
# Main Program with S3
# -----------------------------
bucket_name = "24372276-cloudstorage"   # 
local_folder = "./pycryptodome_files"  # create a new folder
password = "kitty and the kat"        # reuse same pw as your example

s3 = boto3.client("s3")
os.makedirs(local_folder, exist_ok=True)

# List objects in S3 bucket
response = s3.list_objects_v2(Bucket=bucket_name)
if "Contents" not in response:
    print("No files found in bucket.")
    exit()

for obj in response["Contents"]:
    s3_key = obj["Key"]
    local_file = os.path.join(local_folder, s3_key.replace("/", "_"))

    # Download file
    s3.download_file(bucket_name, s3_key, local_file)
    print(f"Downloaded: {s3_key} -> {local_file}")

    # Encrypt
    encrypted_file = local_file + ".enc"
    encrypt_file(password, local_file, encrypted_file)
    print(f"Encrypted -> {encrypted_file}")

    # Decrypt
    base_name, _ = os.path.splitext(local_file)
    decrypted_file = base_name + "_decrypted.txt"
    decrypt_file(password, encrypted_file, decrypted_file)
    dec_size = os.path.getsize(decrypted_file)
    print(f"Decrypted (restored to txt) -> {decrypted_file} (size: {dec_size} bytes)")
```

then, get all the files and encrypt and decrypt

<img width="865" height="123" alt="image" src="https://github.com/user-attachments/assets/0a204fbd-9f63-406b-a58e-bae89971393a" />


### Step 6 upload the files into s3 bucket

We have two folders that need to be uploaded, like we did before, we walk through both folders and upload all the files within folders into s3 bucket. 


```
import os
import boto3

# -----------------------------
# Config
# -----------------------------
bucket_name = "24372276-cloudstorage"  # <-- replace with your bucket
kms_folder = "./kmsfile"
crypto_folder = "./pycryptodome_files"

s3 = boto3.client("s3")

def upload_folder(local_folder, s3_prefix):
    """Upload all files in local_folder to s3://bucket/s3_prefix/"""
    for root, _, files in os.walk(local_folder):
        for file in files:
            local_path = os.path.join(root, file)
            # Preserve relative path inside the S3 prefix
            rel_path = os.path.relpath(local_path, local_folder)
            s3_key = f"{s3_prefix}/{rel_path}"

            print(f"Uploading {local_path} -> s3://{bucket_name}/{s3_key}")
            s3.upload_file(local_path, bucket_name, s3_key)

# -----------------------------
# Upload results
# -----------------------------
upload_folder(kms_folder, "kmsfile")
upload_folder(crypto_folder, "pycryptodome_files")

print("✅ All encrypted and decrypted files uploaded successfully.")
```

it will show all files have been uploaded when we ran this script

<img width="865" height="238" alt="image" src="https://github.com/user-attachments/assets/69370aad-e2ee-4c50-af4e-f8252dd8982b" />


# Lab 5

## Application Load Balancer

### Step 1 Create 2 EC2 instances

We are going to create 2 EC2 instances as requirements, which includes creating a security group and inbound traffic setting. 

The only difference between the ec2 instance we built on in lab2 is we are setting vpc and 2 subnets on this example for load balancer 

```
import boto3
import time

# -------------------------------
# Config
# -------------------------------
student_number = "24372276"
region_name = "ap-southeast-2"
ami_id = "ami-010876b9ddd38475e"
instance_type = "t2.micro"
key_name = f"{student_number}-key"  # You should create/import a key pair with this name
sg_name = f"{student_number}-sg"
vm1_name = f"{student_number}-vm1"
vm2_name = f"{student_number}-vm2"

ec2 = boto3.client("ec2", region_name=region_name)
elb = boto3.client("elbv2", region_name=region_name)

# -------------------------------
# 1. Create Security Group
# -------------------------------
vpcs = ec2.describe_vpcs()
vpc_id = vpcs["Vpcs"][0]["VpcId"]

sg = ec2.create_security_group(
    GroupName=sg_name,
    Description="Allow SSH and HTTP",
    VpcId=vpc_id
)
sg_id = sg["GroupId"]

# Allow inbound SSH (22) and HTTP (80)
ec2.authorize_security_group_ingress(
    GroupId=sg_id,
    IpPermissions=[
        {"IpProtocol": "tcp", "FromPort": 22, "ToPort": 22,
         "IpRanges": [{"CidrIp": "0.0.0.0/0"}]},
        {"IpProtocol": "tcp", "FromPort": 80, "ToPort": 80,
         "IpRanges": [{"CidrIp": "0.0.0.0/0"}]}
    ]
)
print(f"✅ Security group {sg_name} created: {sg_id}")

# -------------------------------
# 2. Launch 2 Instances
# -------------------------------
# Get available subnets in the region
subnets = ec2.describe_subnets(Filters=[{"Name": "vpc-id", "Values": [vpc_id]}])
subnet_ids = [s["SubnetId"] for s in subnets["Subnets"]]

# Pick 2 different AZ subnets
subnet1, subnet2 = subnet_ids[0], subnet_ids[1]

instances = ec2.run_instances(
    ImageId=ami_id,
    InstanceType=instance_type,
    KeyName=key_name,
    MinCount=1,
    MaxCount=2,
    NetworkInterfaces=[
        {
            "SubnetId": subnet1,
            "DeviceIndex": 0,
            "AssociatePublicIpAddress": True,
            "Groups": [sg_id]
        }
    ],
    TagSpecifications=[{
        "ResourceType": "instance",
        "Tags": [{"Key": "Name", "Value": vm1_name}]
    }]
)
instance1_id = instances["Instances"][0]["InstanceId"]

instances2 = ec2.run_instances(
    ImageId=ami_id,
    InstanceType=instance_type,
    KeyName=key_name,
    MinCount=1,
    MaxCount=1,
    NetworkInterfaces=[
        {
            "SubnetId": subnet2,
            "DeviceIndex": 0,
            "AssociatePublicIpAddress": True,
            "Groups": [sg_id]
        }
    ],
    TagSpecifications=[{
        "ResourceType": "instance",
        "Tags": [{"Key": "Name", "Value": vm2_name}]
    }]
)
instance2_id = instances2["Instances"][0]["InstanceId"]

print(f"✅ Instances created: {instance1_id} ({vm1_name}), {instance2_id} ({vm2_name})")

# Wait until running
print("⏳ Waiting for instances to run...")
ec2.get_waiter("instance_running").wait(InstanceIds=[instance1_id, instance2_id])

# Get instance details
instances_desc = ec2.describe_instances(InstanceIds=[instance1_id, instance2_id])
for res in instances_desc["Reservations"]:
    for inst in res["Instances"]:
        print(f"Instance {inst['InstanceId']} is running at {inst['PublicIpAddress']}")
```

### Step 2 Create a load banlancer

First, we set the parameters for load balancer

```
lb = elb.create_load_balancer(
    Name=f"{student_number}-alb",
    Subnets=[subnet1, subnet2],
    SecurityGroups=[sg_id],
    Scheme="internet-facing",
    Type="application",
    IpAddressType="ipv4"
)
```

Explaination:

```
Subnets=[subnet1, subnet2]
A load balancer must live inside a VPC
SecurityGroups=[sg_id]
Security groups act as firewalls that control inbound and outbound traffic to load balancer. We set the security groups that we created before for our load balancer

Scheme="internet-facing"
This is the rule defines whether the load balancer is public or private: 

Type="application"
Defines the kind of load balancer. There are also network or gateway options 
```

Then, we get the load balancer arn from lb instance

```
lb_arn = lb["LoadBalancers"][0]["LoadBalancerArn"] 
print(f"✅ Load balancer created: {lb_arn}")
```
Then we create a target group and get the target group arn 
The target group is where the load balancer send its traffic to
```
tg = elb.create_target_group(
    Name=f"{student_number}-tg",
    Protocol="HTTP",
    Port=80,
    VpcId=vpc_id,
    TargetType="instance"
)
tg_arn = tg["TargetGroups"][0]["TargetGroupArn"]
```
For this example, we set protocol as HTTP, since it’s enough for communication between load balancer and ec2 instance. 
And we set the port as 80, which is where the Apache runs
Then load balance must live in the specific vpc
For the targetType, we set it as instance since in this example, the load balancer mainly fits for the ec2 instance.
Finally, we get the targetgroup arn from the same position 

Last, we created the listener as requirements 

```
elb.create_listener(
    LoadBalancerArn=lb_arn,
    Protocol="HTTP",
    Port=80,
    DefaultActions=[{"Type": "forward", "TargetGroupArn": tg_arn}]
)
print("✅ Listener created and attached to load balancer.")
```

When we run this code piece, we will get the outcome below. 
<img width="865" height="125" alt="image" src="https://github.com/user-attachments/assets/1123c520-ea39-42f1-a623-b57551e3a4da" />

### Step 3 test the load balancer

First, we try to use the ssh to get access to ec2 instance 
```
ssh -i 24372276-key.pem ubuntu@13.211.89.236
```
Explaination:
```
-i 24372276-key.pem: specify the private key
ubuntu@13.211.89.236: username and ip address of ec2 instance
```

It shows the permission denied. 
<img width="865" height="296" alt="image" src="https://github.com/user-attachments/assets/1b83dc76-aa44-41a2-836e-4e3b9b23a482" />

I went to the ec2 console and click connect and then click the SSH client, I found that I need to execute the command as the website said. 

<img width="865" height="252" alt="image" src="https://github.com/user-attachments/assets/c48d25a8-d90e-4e5c-80b7-c0d486f4b019" />

First, make sure the private key is not publicly viewed 
```
chmod 400 "24372276-key.pem"
```

but this command doesn’t work in the mnt path, so first I move the key-pem file into the linux home path. 
Run those two code lines on wsl

```
mkdir -p ~/.ssh 
mv 24372276-key.pem ~/.ssh/
```

then, set the pem to only-read

```
chmod 400 ~/.ssh/24372276-key.pem
```
Second, try to connect it by SSH 
```
ssh -i "~/.ssh/24372276-key.pem" ubuntu@ec2-3-25-119-9.ap-southeast-2.compute.amazonaws.com
```
And I get into the ec2 instance successfully
<img width="865" height="406" alt="image" src="https://github.com/user-attachments/assets/db52a185-fad9-44f6-ad31-1d1a2ad2fc6f" />


### Step 4 install apache2 

Then, we run those two lines of code to install apache2 
```
sudo apt-get update
sudo apt install apache2
```

### Step 5 change the title

In the ec2 instance, We run the code to start editing the html page 

```
sudo nano /var/www/html/index.html
```

<img width="865" height="462" alt="image" src="https://github.com/user-attachments/assets/b6291247-bda6-4590-aabe-b10b2fcc8d11" />

the previous title is like this 
<img width="865" height="105" alt="image" src="https://github.com/user-attachments/assets/ca591206-6e4a-4d24-9d10-c1e063ce964d" />

I changed the tile to instance name "24372276-vm1"

<img width="865" height="99" alt="image" src="https://github.com/user-attachments/assets/b4144331-b11b-4880-b27e-356a0b3fb9aa" />

Use Ctrl+O+enter to save and ctrl+x to exit 

### Step 6 Test in the browser 

First, keep the ec2 open, then input http://3.25.119.9/ in the browser, we will see the correct page below 

<img width="865" height="688" alt="image" src="https://github.com/user-attachments/assets/040287d2-c3f6-4cca-83ff-dab78f5d20a0" />

And for vm2, we can get http://13.211.89.236/ to get the page. 

<img width="865" height="708" alt="image" src="https://github.com/user-attachments/assets/3157adcc-2439-4ec3-989a-96b16dd94008" />














































































