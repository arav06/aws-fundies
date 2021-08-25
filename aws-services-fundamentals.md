# AWS Services Fundamentals 

> Arav Budhiraja | 20th August 2021

Course Link: https://my.ine.com/Cloud/courses/7160c9f4/aws-services-fundamentals

## Topics

1. Setup an AWS account 
2. Infrastructure 
3. Networking 
4. Compute
5. Storage 
6. Additional Services

## Learning Objectives 

1. Create a secure AWS account with billing alarms 
2. Define the fundamental resources of AWS 
3. Confident having general conversations about AWS infrastructure and services 
	- Virtual Private Clouds(VPC)
	- Networking in AWS
	- Compute
	- Storage

## Creating an AWS Account 

* Create an AWS Account 
	-	Support options 
* Understand the root account 
	* Best practice: Limit use of root
* Create a user account 
* Enable Multi Factor Authentication(MFA)
* Create a billing alarm 
	* Best practice: Multiple billing alarms
* Homework

### Create an AWS Account 

#### What you need to get started

* Valid Email Address. If the AWS account will be a business one, use a restricted organization email. Make sure more than 1 person has access to the business email. For experimenting with AWS we will use a personal email
* Valid Credit Card 

#### Support Options 

![support-plans](support-plans.png)

#### Understanding the root account 

If we are logging in with an email, we are logging into the root user

NOT an everyday login. We should not always be logging into the root. Root account has unlimited capabilities 

Setup MFA for root account 

We should not setup programmatic access keys for the root user 

Programmatic access keys are pieces of security credentials which can be used to run scripts in our AWS Console. Scripts should not be run as root as we can break our environment 

In most cases, only root has access to billing and cost 

GovCloud is needed when our organization wishes to work with the Government of USA

We need to use root when changing account settings, restoring IAM user permissions, activate IAM access to billing and cost, signing up for GovCloud and closing our account

In this case, we have to create an IAM User. IAM users will be the users which we will login into everyday. These users can be used by the operations team, security team, database team and developer team. We have to setup MFA for the IAM users

To setup MFA, we can use Google Authenticator(software), RSA Tokens(hardware) or Gemalto(hardware)

#### Creating an IAM User

1. Search for 'IAM' and click on 'IAM'
2. On the left hand side, click on 'Users' below 'Access Management'
3. Click on the blue button which says 'Add user'
4. Provide a username and give it 'AWS Management Console access'. 'Programmatic Access' can be enabled if we wish to run scripts in the console and use the CLI
5. Now select custom password and enter a strong password. Deselect 'Require password reset'. Click on next
6. Give the required permissions. Here, we can give this user the 'AdministrativeAccess' permission. This will give us access to all services and resources. We can also create a group such as 'adminGroup' and add the user to that group
7. Specify a tag and click on next 
8. Click on 'Create User' at the bottom left 
9. Now, a custom URL will be displayed. 
10. Go to the custom URL and provide the username and password 
11. Now we can access the management console for the new IAM user

#### Enabling MFA

1. Search for 'IAM' and click on 'IAM'
2. On the left hand side, click on 'Users' below 'Access Management'
3. Click on the user 
4. Click on the 'Security credentials' tab 
5. There, the assigned MFA device will be not assigned 
6. Click on 'Manage'
7. We will be using Google Authenticator. So click on 'Virtual MFA device' and click on continue 
8. Download Google Authenticator from the Google Play Store/App Store
9. Open the app and click on + in the bottom right corner 
10. Select 'Scan QR Code'
11. In AWS, click on show QR code 
12. Scan the QR Code using Google Authenticator 
13. Now we have to fill out 2 MFA codes. These codes will be the numbers which will be shown in the app. New codes are generated every 30 seconds
14. Click on assign MFA and now we have setup MFA 

#### Billing alarms 

IMPORTANT THING WE CAN ADD TO OUR ACCOUNT 

We should not start a service and leave it running. This will cause the bill to keep on increasing 

Billing alarms watch our account and if we reach a certain spending limit, it will alert us 

An alarm can be created using CloudWatch. The alarm which we will create is a part of the Simple Notification System(SNS). 

Billing alarms are basically sending a value on which we can keep an eye on to CloudWatch to monitor the value

SNS will take the email we supply and immediately send an email to us. The email will ask if we wish to use CloudWatch to send us alerts. If we click on confirm, then we will start receiving email for alarms. If we do not click on confirm, then CloudWatch will not send emails. Check the Spam folder for the confirmation email

Billing alarms are rule based alerts which are based on the AWS bill

CREATE MORE THAN ONE ALARM 

If our max allowable bill is $10, we should send alarms at $5, $7 and $9

If our bill reaches that limit, CloudWatch will alert us via an email

##### Creating billing alarms 

1. Search for CloudWatch in the services 
2. In the left bar, click on 'Billing' which is below 'Alarms'
3. Here, we can create an alarm by clicking on the orange button 
4. By default, it gives us exactly what we want 
5. At the bottom we can select if the estimated charge should be Greater/Greater or Equal/Lower or Equal/Lower and then specify the amount. If we select Greater and specify the amount as $10, then CloudWatch would alert us when our bill exceeds $10. Once we have specified the amount, click next
6. Now we can select the alarm trigger. Select 'In alarm' and 'Create a new topic'. Give a name for the topic and type in the email to which the alert will be sent
7. Go to the bottom and click on next 
8. Now we have to specify an alarm name and alarm description and click on next
9. And finally click on 'Create alarm'

#### Homework 

* Create another IAM user 
	* Give the user admin permission 
	* Setup MFA
* Create another billing alarm with CloudWatch
	* Set the alarm to trigger at 90% of the budget 

### Quiz

1. When setting the billing alarm why is it a best practice to set more than one alarm?

```txt
If the initial message is missed or no action is taken subsequent alarms at higher limits will fire. This helps ensure that action will be taken when spending limits are being approached.
```

2. What is one step you should take to protect your AWS root account?

```txt
Enable MFA for the root account
```

## AWS Infrastructure 

Elementary pieces of AWS

* AWS Data Centers 
* AWS Availability Zones(AZs)
* AWS Regions
	* Basic principles for selecting an AWS Region
* Amazon Virtual Private Cloud(VPC)
	* Amazon VPCs and Fault Tolerance 
* Amazon CloudFront

### AWS Data Centers

There is no magic involved

AWS uses traditional servers, storage and networking equipment 

They bring all of the above together and put it in a building. These buildings are known as data centers

In AWS, the data layer is the place in which users put information into AWS

#### Features of AWS Data Centers

- Multiple layers of PHYSICAL SECURITY
- Making sure there is great backup power, HVAC and fire suppression
- Making sure the data layer is restricted and includes threat detection devices
- When selecting a location for a data center, the environmental issues of the location are taken into consideration

Even if we are going to build a simple web app, we automatically inherit all of the above features, even though we may not need them 

### AWS Availability Zones(AZs)

DATA CENTERS GO INTO AVAILABILITY ZONES

One or more data centers collected together which maybe close to each other 

Lets us build a fault tolerant and highly available service 

Best practice would be to use more than one AZ

We should put our app into many AZs giving us high bandwidth and low latency such that it feels they are all in 1 data center. If 1 AZ is down, our app will be still be running as the other AZ is up

Examples: us-east-1a and us-east-1b. us-east-1 is a region and a,b and are the AZs

#### Features of AZs

* Interconnected by high bandwidth, low latency and redundant networks
* All network traffic between AZs are encrypted 
* AZs are physically separated from one another, but are within 60 miles of each other 

As of 2021, there are 80 Availability Zones in the entire world(approx), not in each region

### AWS Regions 

AVAILABILITY ZONES GO INTO REGIONS 

 Made up of multiple, isolated and physically separated availability zones 

SELECT THE REGION WHICH IS CLOSEST TO OUR END USERS 

Allows developers to use the infrastructure that complies with data regulations from a certain part of the word and/or is closest to end user

As of 2021, there are 25 regions(approx). Examples: ap-south-1, us-east-1

Our region is displayed in the top right corner, next to the username 

Upon clicking on it, we can see the other regions and their short forms 

If we see that something such as EC2 instance is missing, we should check if we are in the correct region 

Some services can only be found in specific regions such as RDS. There are some services such as IAM and S3 whose region is set to 'Global' which means that it can be accessed from all regions, be it Mumbai/Virginia/South Africa

S3 as a service is global but the buckets can be setup in different regions 

#### Selecting an AWS Region

1. Data Regulations:We have to check if there are regulatory considerations for the data which will be processed
2. AWS Services: Are the required AWS services available in that region? AWS DOES NOT PUSH OUT NEW SERVICES TO REGIONS SIMULTANEOUSLY. It tends to roll out services from 1 region to the next and normally starts from Virginia 
3. Geographic Location: Is the region geographically near your intended end users? We should not select the region as Australia if we want our end users to be people from USA/South America/Europe
4. Fault Tolerance: Do we need the highest levels of fault tolerance from the infrastructure? We may setup our infrastructure in another region to ensure high availability

### Amazon Virtual Private Cloud(VPC)

A private cloud for our organization within AWS

A VPC consists of an Availability Zone which is running many services

We should setup more than 1 AZ in our VPC, so that if 1 goes down, the other one is still up and running 

For high levels of fault tolerance, we can setup our VPC in another region and setup the exact same infrastructure

### Amazon CloudFront 

Helps in getting closer to the end user

To get low latency to the end users, we will use a content distribution network(CDN) known as Amazon CloudFront 

* 255+ sites in the world
* Speeds up delivery of websites and speeds up live and on-demand video streaming
* Automatically routes traffic to the most performant AWS edge locations 

The places where CloudFront sites are located are known as edge locations

We have an app in Ohio but our user is in Rio. The first time a user accesses the website, a request is sent to the CloudFront site in Rio. The site checks if it already has the required contents in its cache. If it does not, the request is then sent from the site at Rio to the site in Ohio. The site in Ohio then sends the contents of the website to the site in Rio. The site in Rio stores the website contents in it's cache and then forwards the contents to the user in Rio. At the same time, if another user also accesses the website, then a request is sent to the site in Rio which instantly forwards the website contents to the user. It does not request the site in Ohio for the website since it has stored the contents in it's cache. This will offer much lower latency and quicker response time.

### Quiz

1. What is the correct order of infrastructure at AWS as it relates to data centers, availability zones, and regions?

```txt
Data centers go into availability zones, availability zones go into regions
```

2. What are some considerations when choosing an AWS Region?

```txt
Regulatory restrictions concerning data processing
```

## Amazon Elastic Cloud Compute (EC2)

* What is Amazon EC2
* Amazon Machine Image(AMI) 
* Instance Types 
* Storage 
* Security Groups
* Purchasing Options 
* Dedicated Instances and Dedicated Hosts

### What is Amazon EC2

Virtualization is running an operating system within another operating system

* Virtual servers in the cloud which can support workloads
* Can scale in or out in minutes. 10 years ago, when we had to add more servers to our infrastructure, it would cost a lot of money. As user demand goes up, we can scale out and when user demand starts decreasing, we can scale in 
* Has many operating systems and server sizes 
* Flexible options to optimize cost

An EC2 instance is made up of an amazon machine image and instance type

Once an EC2 virtual machine is up and running, it is known as an EC2 instance

To connect to an EC2 instance via SSH/RDP, we will have to generate a connection key

By default, when connecting to a linux instance, we connect over SSH and when connecting to a windows instance, we connect over RDP

### Amazon Machine Image(AMI)

The software of our virtual server 

Contains the operating system, applications and utilities. Example: We can buy an AMI which already has WordPress setup and run our website instantly 

Offer launch permissions to configure security 

AMIs have storage options to attach to the EC2 instance 

AMI partners up with the instance type

AMIs which are free have 'Free tier eligible' mentioned below

* 'Quick Start' consists of AMIs which can be spun up instantly without much configuration
* 'My AMIs' has AMIs which we have spun up and taken a snapshot 
* 'AWS Marketplace' is the place where vendors are selling their AMIs such as WordPress  
* 'Community AMIs' are AMIs which are supported by the community

### Instance Types

The virtual hardware of our server

AWS gives us categories for the type of hardware we need: general, compute, memory, accelerated, storage 

Offers various amounts of virtual CPUs and memory 

The way AWS offers the the purpose of the server and the various amounts of CPUs and memory is by 'Purpose.Size'

Purpose - Category and generation of the server.
Size - Lets you know how big/small the server is 

Examples: M5.large(General, 2vCPUs, 8GiB Memory) and M5.xlarge(General,4vCPUs,16 GiB  Memory)

As we go up by one size such as .large to .xlarge, the amounts of CPU and memory will double

Definitions for instance types can be found <a href="https://aws.amazon.com/ec2/instance-types/">here</a>

.metal - Physical machine designated for us 

### Storage 

#### Instance Store

VERY IMPORTANT: IT IS TEMPORARY. NOT A PLACE TO SET UP A DATABASE/STORE LONG TERM INFORMATION 

Physical disks which are attached to the hardware of the virtual machine 

If the physical components fail or if the EC2 instance is stopped/hibernated/terminated, then you will lose the data in the storage 

GREAT FOR TEMPORARY STORAGE 

#### Elastic Block Storage(EBS)

PERSISTENT STORAGE 

2 flavors: SSDs and Spinning drives aka HDs(Have a good purpose in cloud architecture)

EBS is a great place to store databases and other long term information 

SSDs are great if you are constantly going to be writing to the disk

If you are not sure about which storage, go for SSD

Spinning drives are great for storing large files and if you want to store files which you do not access frequently 

CONSIDER THE WORKLOAD BEFORE SELECTING STORAGE TYPE

### Security Groups 

FIREWALL WHICH WRAPS AROUND OUR EC2 INSTANCE 

We can specify rules for inbound/outbound traffic 

We can name our security groups

In security groups, rules are stateful

Lets say that we have a website running on port 443(HTTPS) and using our security group, we allow all inbound traffic to port 443. Now, we have a device connected to the internet which visits our website. Once it does so, it hits the security group which allows it to access port 443. During this negotiation, the device provides a high port number(port higher than 1024) such as 48923, to which the contents of the website should be sent back. Now, the security group realizes that the traffic on port 443 is legitimate and the client wants the website contents on port 48923. So, the security groups automatically allows outbound traffic on port 48923

The rules of a security group such as 'SG-1' can be applied to more than one EC2 instance. If we allow inbound traffic on port 22(SSH) for 'SG-1',  then all the instances whose security group is 'SG-1' will follow that rule and allow inbound connection on port 22

### Purchasing Options 

How we pay for EC2 

#### On Demand 

Pay as you go

You are charged by the hour/second, depending on the OS. 

Most open-source operating systems such as linux are charged by the second, for a minimum of 1 minute. Windows is charged by the hour

There is no long term commitment, capacity planning  or purchasing required 

#### Reserved Instances(RI)

For a server which will be running for a long time such as 1 year or 3 years 

Changes the billing model to a complete/partial/none up front 

There are two types: Standard and Convertible 

In an RI, if we purchase a system, then IT WILL BE A PERMANENT ACTION

Convertible RI will let us upgrade our instance from something such as M5 to M6 or to a new version

RI IS A BILLING MODEL 

AWS offers Standard RIs for 1-year or 3-year terms

AWS has finite hardware and with so many customers they may not have the hardware you require. If this system is for a mission critical workload, then you need a zonal RI which require us to pick an availability zone in our VPC. Once this is done, it becomes a capacity reservation which lets us start up the server which is defined in the RI

|   	Topic		| Standard RI |  Convertible RI| 
| ----------- | ----------- | ----------- | 
| % off On-Demand| Up to 72%|Up to 54%  | 
| Change attributes of the RI|No| Yes if the exchanged results in the RI are greater of equal | 
| Capacity Reservation|Yes if an AZ is specified| Yes if an AZ is specified | 

#### Spot 

Allows us to not spend a tremendous amount of money by bidding on spare Amazon EC2 instances

Up to 90% off compared to On-Demand 

We can only use stateless workloads i.e. we can shutdown the workload and bring it back up and it will not affect the way the workload is running. The data for it is being stored in a database and the workload can make calls to the database to get the data 

These servers can be reclaimed within a 2 minute warning 

Lets say that we are bidding $5 for a server which costs $10. Gradually the price comes down to $5 and now we own that server and we run our workload. As more and more people start using the AWS infrastructure, the price for the server starts coming back up and once it passes $5, we get a 2 minute warning and after 2 minutes our server will be taken away from us 

### Dedicated Instances and Dedicated Hosts

We have a situation where our workload needs an environment in which the app on the server does not want other servers in the system to access it's hardware, due to regulatory concerns

Dedicated instances and hosts let us say 'this physical system is my machine and no one else can access its resources' 

Dedicated Instances - Instances which are running on a single server which are dedicated for one customer. But if one customer shuts down their instance, their hardware maybe changed but they will be the only one using that hardware. Helps in isolating workload 

Shared tenancy - Different customers are sharing the same hardware but are separated by a barrier so that they cannot access each other's data

Dedicated Hosts - Dedicated physical servers for a single customer whose hardware will not be changed

In dedicated hosts, a customer is the first and only one on the server and there will be no interchanging of hardware. YOU WILL BE THE ONLY ONE ON THAT SERVER. Helps in ensuring workload isolation and that you will always be on the same physical server

### Setting up and running an EC2 instance 

* Amazon Linux AMI
* t2.micro 
* Add a 5GiB SSD drive 
* Allow inbound traffic to port 443(HTTPS)
* Tag the instance with CanBeDeleted
* Generate a connection key 
* Terminating the instance 

1. In AWS instances, search for 'ec2' and click on 'EC2'
2. Before you begin, select the appropriate region 
3. Scroll down and click on 'Launch instance'
4. Here, we can select  'Amazon Linux 2 AMI' which is free tier eligible 
5. Now, for the instance type we will select 't2.micro' since it is free tier eligible and click on 'Next:Configure Instance Details'
6. We can scale out/in by specifying the number of instances. If we want to request for spot billing, we check 'Request Spot instances'. We can enable the option to auto-assign a public IP. 'IAM role' can be be used to define the things which the server can do. We can create a role allowing the server to communicate with a Microsoft instance and then add the role. For now we will not do it. Click on 'Add storage'
7. Here, we can add additional storage. We can also specify if we wish to encrypted the drive and delete the drive if we delete the instance. If we want the data in the drive to be persistent, do not enable 'Delete on Termination'. 'Delete on Termination' means that if we terminate our instance, then the drive will also be deleted. If we do not check that, the drive will exist after we terminate the instance. Click on 'Next: Add Tags'
8. Here, we can add tags such as 'CanBeDeleted' or 'Owner'. Once you have specified the tags, click on 'Next: Configure Security Group'
9. Now, we can configure the settings for inbound/outbound connections. Since this instance will be a web server, we can add a rule whose type is 'HTTPS', the protocol is 'TCP', the port is '443' and the source can be from anywhere
10. Finally click on 'Review and Launch' and here we can check all the settings. If we want this to be a private instance and a message appears saying that the security group is available to the world, then we should check the settings in the security group
11. Now you click on 'Launch'. Here you will be prompted for a key pair. The key pair is used to connect to the instance via SSH/RDP
12. In this case, we can select 'Create a new key pair', provide it a name and then click on 'Download Key Pair'. Once it is download, click on 'Launch Instances'
13. We can now go check our running instance by click on the instance id which should be something like 'i-37bvd2942', below the green text which says 'Your instances are now launching'
14. Below 'Instance state' we can see if the instance is pending/running/stopped. If we click on the instance id and pull up the window at the bottom, we can see information about the instance 
15. We will now terminate the instance. Stopping at instance means that it is shutdown and we can bring it back up later. Terminating an instance is obliterating everything. To terminate it, right click on the instance id and click on 'Terminate instance'

### Quiz

1. When purchasing a reserved EC2 instance, what are the two time period options?

```txt
1 year and 3 years
```

2. When configuring an Amazon EC2 instance, when is the key pair selected for programmatic access?

```txt
Immediately before launching the instance
```

## Storage in AWS

The best options for storage are EBS and S3

* Amazon Elastic Block Storage(EBS)
* Amazon Simple Storage Service(S3)

### Amazon Elastic Block Storage(EBS)

The hard drives of EC2 instances

Used to store blocks 

Two flavors: SSDs and Spinning Drives(HDs)

SSDs are great for general purpose and great for storing a database or a file system which is constantly being written to/read from 

Spinning Drives are great for infrequent access and can be used to store files which are infrequently used 

IOPS - Unit of measure representing input/output operations per second 

Throughput - Measure of the amount of data transferred from/to a storage device per second 

Two types of SSDs: General Purpose and Provisioned IOPS

General Purpose - gp3 and gp2 - Difference is in the throughput, for gp3 it is 1000 MiB/s and for gp2 it is 250 MiB/s. These are great for general computing, when we are developing our app and testing it. Size can be from 1 GiB to 16 TiB and they offer 16000 Max IOPS/Volume 

For databases and file systems which are constantly being read from/written to, Provisioned IOPS are used. There are 2 types Io2 and Io1. Size can be from 4 GiB to 16 TiB and the throughput is 1000 MiB/s and they offer 64000 IOPS/Volume

Two types of HDs: Throughput Optimized and Cold

To store big data/large files, we use spinning drives. The best type for this is 'Throughput Optimized' or st1. Size can be from 125 GiB to 16 TiB and the throughput is 500 MiB/s

The other type is known as 'Cold' or sc1. Much less expensive but we should not writing to/reading from them frequently. Used to store data which is not accessed frequently. Size can be from 125 GiB to 16 TiB and the throughput is 250 MiB/s

If a drive is not attached to an EC2 instance, it's status will be 'available' and if it is attached, the status will be 'in-use'

### Amazon Simple Storage Service(S3)

Used to store objects 

With a large file in EBS, we can change a part of a file without having to completely rewrite it. IN S3 WE HAVE TO COMPLETELY REWRITE THE FILE 

* Scalable object storage with virtually not limit 
* Designed for 99.999% durability
* Cost effective storage clases 
* Provides storage for AWS resources and assets which will be read from the internet
* Can be used to host static websites and other static resources such as pictures/videos

S3 is used by game companies when they wish to roll out a new update as it is extremely easy to put the file in the bucket and then we can simply push the update via a URL 
 
In S3, the place where objects are stored are known as buckets 

#### Storage classes 

* S3 Standard: Low latency and high throughput. Default location where S3 buckets are setup
* S3 Infrequent Access: Used to store objects which will not be frequently accessed. Cost for storage will decrease but the cost for accessing the objects will increase
* S3 Intelligent-Tiering: We can create a rule in our S3 standard class such that if an object has not been accessed for more than a month, then automatically move it to S3 Infrequent Access but if someone does access it, then move it back up to the standard level. Storage cost will increase but cost to access the object will decrease 
* S3 Glacier: Used to store long term archives. We can store backups of objects and to retrieve objects from Glacier, it can take as long as 12 hours 

### Creating and attaching an EBS volume

1. In the console, we will search for 'ec2' since EBS is related to EC2
2. In the left bar, scroll down and find 'Elastic Block Store'. Ensure that we are in the right region
3. Click on 'Volumes' and then in the top left we will click on 'Create volume'
4. In the volume type we can select if we wish to use gp2, gp3, io1, io2, st1 or sc1. gp2 is great for general computing so we will use that. Then provide a size
5. We will then specify the availability zone and we can also encrypt the drive by checking 'Encrypt this volume'
6. Now click on 'Create Volume' in the bottom right. We can then click on 'Close' and now we can see the drive we have created. 
7. Select the drive and click on 'Actions' and click on 'Attach volume'. Here we get a dropdown which will provide the EC2 instances to which we can attach the drive. After a few minutes, it's status should change from 'available' to 'in-use'

### Quiz

1. Which storage service is considered to be scalable object storage?

```txt
Amazon S3
```

2. What is a feature of Amazon S3?

```txt
Host static websites and other static resources
```

## Amazon Virtual Private Cloud (VPC)

Our private cloud within AWS 

* VPC 
* IP Addressing 
* Availability Zones in the VPC
* Connecting to outside resources from the VPC
* Connecting to AWS Resources that are addressed with a URL 
* Proper use of the default VPC 

When creating a VPC, we set a base IP Address range

VPCs define the base network 

We can create AZs in our VPC to create subnets and deploying resources in the subnet and to create resilient architectures

When building VPCs from scratch, VPCs are not allowed to connect to outside resources. To connect it to outside resources we can add gateways. These are the internet gateway and VPN gateway. Internet gateways let us connect to the internet. Internet gateways allow connections to URLs or IP addresses which are outside the VPC's range. We can define special routing rules and setup VPN gateways which can be used to connect our VPC network to another network such as an on prem one 

Public subnets are the subnets which are connected to the internet

Private subnets are the subnets which are not connected to the internet. If they are connected to another network such as an on prem one, they are still known as private subnets

When we connect to certain resources in AWS, we use URLs. Examples: S3 and Dynamo DB. By default, when a resource in our VPC connects to an S3 bucket, it is addressed by the URL. Connections to these URLs, by default, go through the internet connection. We have to setup AWS endpoints which can be used to avoid routing over the internet. Once we setup these endpoints, connections to these URLs will flow through the endpoints and not the internet gateway. 

All AWS accounts have default VPCs in each AWS Region. Default VPCs are configured the same for all accounts and they do not use actual workloads. These default VPCs are great for beginners you are experimenting with AWS

DO NOT PUT MISSION CRITICAL/BUSINESS RESOURCES IN THE DEFAULT VPC SINCE THE NETWORK OF THE DEFAULT VPC IS THE SAME FOR EVERYONE

### Quiz

1. What services allows resources in your Amazon VPC to connect to the internet?

```txt
Internet gateway
```

2. With default settings, when a resources in a VPC connect to Amazon S3, how is the bucket addressed?

```txt
By the buckets URL
```

## Amazon Elastic File System (EFS)

Great way to share files to our clients who are outside/within our infrastructure 

* Elastic File System
	* Clients 
	* EFS - Infrequent Access
* Creating and sharing an EFS share 

Managed data store that automatically scales up and down 

We do not have to worry about provisioning more storage in an EFS share as it is automatic

Automatically copies the data across multiple AZs

Lets say we have 2 AZs in our infrastructure, AZ1 and AZ2. These AZs have one or more data centers. If our EFS share is copied across 2 AZs and if 1 AZ is down, then our data will still be accessible

Using EFS, we can share files inside/outside the cloud, such as sharing the data to a client who is on prem 

Multiple AZs and VPCs can access the same EFS share/shares 

We can also share files between different clients. An EFS share can be used as a central repository for resources which are required by clients

EFS IS NOT SUPPORTED BY WINDOWS, IT ONLY WORKS WITH LINUX 

Lets say that in our VPC we have 2 AZs, AZ1 and AZ2. Clients in an AZ do not directly connect to an EFS share. Each AZ gets a mount target, and the clients connect to the mount target which would give us access to the data in the EFS share. If we had only 1 mount target and that would go down, we would not be able to access the data. If we lost connection to the mount target from AZ1, we can still connect to the mount target in AZ2

Mount targets are used to connect to an EFS share from one or more AZs, such that if 1 mount target is down, we can still access the share from the other AZ

EC2 instances and containers can connect to EFS shares

Machines which are not in our VPC can also connect to an EFS share in our VPC, via a VPN Gateway

EFS has 2 tierings - Standard and Infrequent Access 

In most organizations, only 20% of data is actively used and the other 80% is infrequently accessed. To store this data we will use EFS - Infrequent Access Tiering. It is little more expensive to access, but the cost for storage is less

Approximately, if we store 1 TB of data in EFS - Standard, it will cost $300/month . But if we store only 200GB of data in EFS - Standard which will cost $60/month  and 800GB of data in EFS - Infrequent Access, which will cost $20/month, the total would be only $80/month 

EFS has 2 modes: Regional and One Zone 

EFS Regional automatically copies data across all AZs

EFS One Zone is used in the case where we can recreate the data we uploaded, if the AZ is down. It will not copy data across AZs but One Zone does save money 

We can create EFS shares with the same name as the id of the shares is what matters 

We connect to an EFS share by using the NFS(Network File Sharing) protocol

If we are not being able to connect to our share, we can click on the share, click on 'Attach' and in the bottom we can click on 'User guide'

### Creating and sharing an EFS share 

1. In the services, search for 'efs' and click on 'EFS'
2. On the right, click on 'Create file system'
3. Provide a name for the share, provide the VPC where it should exist and click on 'Create' 
4. Click on the EFS share and in the top right corner click on 'Attach' 
5. Here, we can see the commands which we can use to the mount the share 
6. You may see a message saying we do not have any mount targets. To run a mount target, click on 'Manage mount targets'
7. To delete the EFS share, in the top right corner click on 'Delete' and provide the id of the share and click on 'Confirm'

### Quiz

1. How do you increase the amount of storage available in an EFS share?

```txt
EFS automatically scales up and down
```

2. You are helping with a new architecture for both Linux and Windows servers. The EC2 instances will need to share storage. It has been suggested that EFS should be used. Will this work and why or why not?

```txt
EFS will not work because it only supports Linux
```

## Amazon Elastic Beanstalk(EB)

* AWS Elastic Beanstalk
* Capabilities of  Elastic Beanstalk
* Deploying an app using code provided in Elastic Beanstalk

 Elastic Beanstalk lets us deploy functionalities such as databases, loading balancing, scaling with little AWS knowledge
 
 Automates deployment of apps 
 
 We supply code and it takes care of the rest. We can write the code in python, ruby, php, java, go and even docker containers. Once we have our code, we specify the architecture to Elastic Beanstalk and it takes care of the rest. It can be used to run web servers such as IIS, Apache, Nginx
 
 Using Elastic Beanstalk, we can create the following infrastructure: scaling and load balancing, monitoring, logging and tracing, health status and database instances 
 
 A collection of resources created with EB is known as a stack
 
 When we build using EB, we build an environment and if we do not want something, we can tear it down. The advantage is that we will not have resources for which we will be charged, even after it has been terminated. The disadvantage is that if we have a database which has important data and we delete the environment, then we lose all the data. We can backup the data or build the database separately and link to it with our code
 
 Many security professionals do not allow the use of EB in their organization. They understand the idea of EB but are troubled with the fact that EB is building our infrastructure. To check if EB is alright to use for our organization, we should check the Services in Scope website. If we are going to be processing cards, we should check if EB is PCI compliant and if we are working with the Federal Government, we should if it is FedRAMP compliant
 
 If the name of an EB environment has '(terminated)' at it's end, it means it is being deleted/has been deleted 
 
 IN ELASTIC BEANSTALK, APPS RUN IN AN ENVIRONMENT 
 
 It takes 10-15 minutes for an environment to be completely deleted 
 
 EB supports Apache, IIS, Node, Docker, etc
 
  ### Deploying an app using code provided in Elastic Beanstalk
 
 1. In services, search for 'elastic beanstalk' and click on 'Elastic Beanstalk'
 2. First we will have to create a test app so that we can create an environment and click on 'Create a new app' and provide a name, tags and the platform to use
 3. Now we will have the place where we can create our environment. 
 4. Click on 'Create a new environment'. We can select 'Web server environment' to deploy a web server and then click on 'Next'
 5. Specify an environment name and the application name. We can also specify a domain and it will be appended by '.region.elasticbeans' where 'region' is the region we are in such as 'us-east-1' and 'ap-south-1'. We can also give a description
 6. Scroll down and provide the platform, branch and version. You can also upload our own code or let AWS create a sample app
 7.  In 'Configure more options', we can use a single instance, single spot instance, high availability(load balancer and scaling groups) and custom(set the presets). We can also select the instance type, security settings, notifications, network, tags for the resources, database. For now we will not mess around with the advanced settings
 8. Click on 'Create environment'. It will take some time for an environment to be created. After sometime, we can see the health status and the platform. The URL is also displayed
 9. If we scroll down, we can see the recent version
 10. If we visit the website, we can see the sample app
 11. To delete all the resources, we will click on 'Actions' , scroll down and click on 'Terminate environment'. We will have to specify the environment name and then click on 'Terminate'

### Quiz

1. You are helping with an AWS Elastic Beanstalk deployment that includes a database resources that was created in Elastic Beanstalk. What special consideration should be made before deleting the environment created by Elastic Beanstalk?

```txt
The database will be deleted when the environment is deleted. If there is any data in the database that needs to be preserved it must be backed up before deleting the environment.
```

2. You are helping with a new architecture for both Linux and Windows servers. The EC2 instances will need to share storage. It has been suggested that EFS should be used. Will this work and why or why not?

```txt
Node,Apache,Microsoft IIS,Docker
```

## AWS Lambda, Amazon Elastic Container Service (ECS) & AWS Fargate

Other ways to execute code in AWS

* AWS Lambda - Architecture and implementation 
* Understanding containers 
* AWS Elastic Container Service 
* AWS Fargate

### AWS Lambda 

Used to run code without needing a server

No administration is required 

Can handle both frontend and backend code 

Automatic scaling and fault tolerance 

Supports many runtimes and languages 

We have our code which is read to go and we upload it to lambda. Once we upload it to lambda it sits there and does nothing. It waits for a trigger to occur that tells it to run. Best way to trigger code would be by using an 'S3 Create Object'. We can have a 'Create Object' happen when we upload files to a bucket. The bucket can be configured to create a trigger such that if files are uploaded, call the lambda and let the lambda know the names of the files. You can also create another lambda function 

Many lambda functions can be chained such that instead of having one code base, we can have the code broke up into many lambdas 

In the free tier, we get 1 million free requests. When lambda runs, it has an execution role which limits the permissions of the function 

Cold start - When first starting lamba. To prevent this, we can call the lamba function every 15 minutes to make sure that it is running 

* If we are running an app on lambda, it has to use less than 10 GiB or memory
* Lambda can only run for 15 minutes
* Lambda's cold start takes a lot of time and it will reset after 15 minutes of inactivity 
* Functions have to be well written and tightly defined 
* We have to understand monitoring in AWS using services such as CloudTrail and CloudWatch. Monitoring is important when we have many lambdas
* Stateless or can re-engineered as stateless

If we want to use more than 10 GiB of memory and run the code for more than 15 minutes, we can use containers

### Containers 

Lets say that we run code for the first time and it works. When we run it on another machine, it does not work. We move it to production and it does not work and it also does not work on the customer's machine. In most cases, the problem is because the code was being run on different machines. The customer machine, production machine and development machine are different. This is known as inconsistent environments. To solve this we will use containers

Isolated environments to run our code

The most famous is Docker 

Docker gives us a consistent runtime environment such that if I run a container on my machine, it will work the same on another machine 

Docker works across platforms and it is highly efficient. Instead of running one service on an EC2 instance, we can have 10 containers in our instance, running 10 different services making it more efficient 

Docker works in private data centers and cloud environments 

### AWS Elastic Container Service(ECS)

Automates building EC2 instances that the containers run on 

We have to specify the containers which we want to run and ECS deploys the containers on the servers 

ECS clusters are groups of EC2 instances that are running containers 

ECS can monitor EC2 instances for free capacity to run containers

Elastic Container Registry(ECR) is a repository from where we can pull containers

We have a container and we register it in the ECR and now ECS can pull the container from the ECR. ECS gets indicated what we expect to run and it can push out the number of containers which we indicate to the ECS cluster of servers that it has setup. ECS manages the above. We can put our containers in ECR, ECS pulls the containers and then pushes the containers on to the EC2 instances and runs the number of containers we want to 

If we do not want to run our container on a server, we will use Fargate 

### AWS Fargate

Can be used to run containers without servers 

Removes the need for provisioning and managing 

We have to pay for the resources which are being used by our containers 

We run tasks(pods) in an isolated environment, improving security and isolation 

When using Fargate we have to take into consideration, the costs for the vCPU used, memory used and the supported services used

Carefully monitor your bill when using Fargate by using billing alarms 

### Quiz

1. Which service would you use if you wanted to use containers without creating virtual servers?

```txt
Amazon Fargate
```

2. What is the timeout limit for AWS Lambda?

```txt
15 minutes
```

## Amazon Simple Notification Service(SNS) & Amazon Simple Queue Service(SQS)

### Amazon Simple Notification Service(SNS)

Way of sending messages for app-app or app-person communications 

Enables decoupling of apps. Normally 1 app(a) maybe talking to another(b). If something happens such that b can no longer communicate, then a does not know what to do. With SNS, a can send the message b and its on SNS to get it to b

Managed service and is reliable and offers automatic scaling 

We can send messages to millions of users

When sending a message via SNS, the message is sent to a topic in SNS which sends it to the destination such as SQS, email or phone. The way destinations are defined are by using subscriptions. Subscriptions refer to the destination such as phone/email

SNS IS A FIRE AND FORGOT MESSAGING SYSTEM. When SNS sends a message from the topic via the subscription to the email, it will simply send it and if there is an error on the other end, there is no check for that and the message is gone 

SNS is used a lot by operations team 

### Amazon Simple Queue Service(SQS)

Allows us to retain and replay the message if there is a problem

Gives us a managed queue service 

Messages are stored until they are grabbed by the person/app to which we are sending the message 

Enables decoupling of micro-service architecture 

Sends, stores and moves messages between software components 

Two flavors Standard(Messages go on and the message is grabbed) and FIFO(Ordered messaged, such as if we specify the order a-b-c, then the messages are sent in that order)

### Quiz

1. What are the two options for Amazon SQS queues?

```txt
Standard and FIFO
```

2. Amazon SNS was designed to send messages between which type of entities?

```txt
Application to application & application to person
```

## Amazon Kinesis

* Overview of Kinesis 
* Kinesis Data Streams
* Kinesis Data Firehouse
* Kinesis Data Analytics 
* Kinesis Video Streams

### Overview of Kinesis 

We all have used an app which is a realtime app which is grabbing data and bringing data back. Example: Find a friend app which shows a friend's location on a map

Creating realtime processors on prem is expensive and hard

Amazon Kinesis allows for the collection, processing and analysis of data in realtime 

The data can be videos, audio, app logs, website clicks, IoT, etc

Fully managed and scalable 

Service specific offering for each Kinesis solution 

* Data Streams: Involves large amounts of realtime data and is coming from many sources. Scalable, durable and realtime streaming of gigabytes of data per second coming from thousands of sources
* Data Firehouse: Involves loading of realtime data and can transform data. Capture, load and transform data streams for near real-time analytics
* Data Analytics: Execute SQL queries against real-time data 
* Video Streams: Securely stream from video devices for analytics processing like machine learning 

### Quiz

1. What is the purpose of Amazon Kinesis Data Firehouse?

```txt
Capture, load, and transform data streams for near real-time analytics
```

2. Which of the following is not one of the Kinesis services?

```txt
Kinesis Information Flow
```

## Amazon CloudFront

Get content to users in a faster way

* What is Amazon CloudFront
* Understanding CDNs
* Topology of CloudFront 
* Creating a CloudFront Distribution

CloudFront is a content delivery network to securely deliver data, videos, apps, APIs globally at a high speed and low latency

We are running a website whose server in New York and aimed that this website will only be used by people in USA. However it gains popularity and people from Africa, Australia, Asia and Europe also visit our website. These people will have extremely slow connections, lot of latency and slow delivery of the data, as the server is not close to them

To solve this problem, we can use caching servers. These are servers all over the world where we can put copies of our data and thus get rid of the high latency and slow connections. When a customer make a call to the content, the request goes to the server. The server checks if it has the required data. If it does not it makes a call to the original server in New York. The original server then sends the data to the caching server which will forward it to the user. At the same time, the caching server stores the contents in its cache. Anyone close to that caching server will get low latency. If another person also requests for that data, then the request is sent to the server which sees that it already has the required data and immediately delivers it

These caching servers are known as content delivery network(CDN) servers

Used to roll out updates for games 

CloudFront has 255+ sites 

CloudFront has multiple layers of caching which increases the chance of finding the required content in that caching server

Can pull data from S3 buckets, EC2 instances, Load Balancers and from media 

CloudFront is a global service 

Lets say that we have a user filling out a form on our website and this form is identified using the 'Field-level Encryption' tool. Once this form data is sent to the CloudFront server, it will encrypt the form data at this server. As the content comes back, we have encrypted data

In AWS, an S3 bucket can be used as a source for a CloudFront distribution 

We can create a CloudFront Distribution to share content from a server in say Mumbai to people in USA/Europe/South America, with low latency and fast delivery 

### Creating a CloudFront Distribution

1. In services search for 'cloud front' and click on 'CloudFront'
2. Click on 'Create a CloudFront distribution'
3. Specify the origin domain name. It is a textbox and a dropdown. This is the location from where content will be pulled. Lets specify an S3 bucket
4. If there is a folder inside that location, you can specify that. This will only share that folder. Origin Shield is a new caching ability giving better performance 
5. We do not know where our content will be pulled from. For the price class we should leave it as 'Use All Edge Locations'. But if we want caching in only certain areas, we can do that as well. 
6. When using cloudfront, the URL for the distribution is something like 'd11fj1221321bnndw.cloudfront.net'. In 'Alternate Domain Names', we can specify a different domain name such as 'www.example.com'. Now it will not use the cloudfront domain name 
7. 'Default Root Object' can be used to redirect users to what they have to see. If the URL for our cloudfront distribution is 'www.example.com', and we want to redirect users to 'test.html' when they visit the website, then we can specify the 'Default Root Object' as 'https://example.com/test.html'
8. Now we can scroll to the bottom and click on 'Create distribution'

### Quiz

1. Which of the following can be a source for a CloudFront distribution?

```txt
Amazon S3
```

2. What is the purpose of Amazon CloudFront?

```txt
CloudFront is a content delivery system in AWS
```

## Databases on AWS

* Customer managed databases on AWS 
* AWS Relational Database Service(RDS) 
* Amazon DynamoDB 
* Amazon Redshift 
* AWS Database Migration Service(DMS)

### Customer managed databases on AWS

We are going to run our own database in an EC2 instance 

Run an EC2 instance --> Download the software --> Run it on to the machine 

Similar to what is used on prem

This is an example of undifferentiated lifting 

Used in the case where we want full control of our database or there maybe features in this database, provided by the vendor, that are not available in AWS

When our app starts blowing up, we have to deal with patching, replication, backups, tuning, monitoring and high availability, with regards to the database. To solve this problem, we can use a managed database. 

Managed databases are databases which do not require the user to handle most of the fundamental operations such as patching, backups, monitoring, etc

### AWS Relational Database Service(RDS)

Managed database. Patching, replication, backups, tuning, monitoring and high availability are handled by AWS

Many management tasks are handled by AWS such as checking if the hardware is alright 

The time we spend setting up and configuring a traditional database is taken by RDS

RDS supports MySQL, MariaDB, Oracle, MS SQL Serer, Amazon Aurora and PostgreSQL

Aurora is Amazon's purpose built, cloud focused database 

Query Editor is used to execute queries on our database 

RDS LETS US RUN A DATABASE ON AN EC2 INSTANCE, WITHOUT US NEEDING TO CONFIGURE MUCH NOR TAKE CARE OF THE DATABASE

We should create our database in more than 1 AZ

Cannot automatically scale in/out

#### Launching a MySQL database using RDS

1. In the services, search for 'rds' and click on 'RDS'
2. Click on 'Create database'
3. The first option is used to select a Standard or Easy create. In Standard, we will configure the settings of our database but in Easy, AWS configures most of the setting, based on the best practices. If you are using RDS for the first time, select 'Easy create'. 90% of the time, we use 'Standard create' when we are in production 
4. Next we can choose the type of database. Select 'MySQL' and we get the MySQL Community Edition and a note from AWS, letting us know about the issues/limitations of using MySQL
5. We can then select the database version
6. Templates are a way to choose the basic configurations that are needed for the place where the database will be setup, such as production/development/test We will select 'Free tier'. Note: Some databases such as Aurora do not have a free option
7. Now we can provide a name for the database and the username and password for the administrator. Use a strong password
8. Then we can select the instance type of the server on which the databases will be running. Select 'db.t2.micro' as it is the free option
9. We can allocate the needed storage. Turn off 'Enable storage autoscaling'. It is a way to increase storage once a limit is exceeded 
10. Select the VPC and disable 'Public access'
11. Now provide a security group for the database server and the AZ
12. We can scroll to the bottom and it would show us the costs, if we were not using free tier. Click on 'Create database'
13. After a few minutes, we should see that our database has been created. Click on the database name and now we can see the statistics 
14. To delete the database, go back and click on the circle next to the database name and then click on 'Actions'
15. Click on 'Delete'. When deleting the database, RDS asks us if we want a backup of our database. For now we will not create a backup. So deselect 'Create final snapshot' and type 'delete me' in the text box. Check the option which says 'I acknowledge....' and click on 'Delete'

### Amazon Aurora 

Most databases such as Oracle and MS SQL are databases which were built for on prem 

Aurora is Amazon's relational database which is the built for the cloud

Compatible with MySQL and PostgreSQL

Gives improved performance. Up to 3x higher throughput than stock PostgreSQL and up to 5x higher throughput than standard MySQL

Aurora is used in enterprise apps, online/inventory catalogs and web and mobile gaming

Can automatically scale in/out

AURORA IS AN ENTERPRISE CLASS DATABASE 

### Amazon DynamoDB

High performance key-value database

Great performance. Capable of single digit millisecond read latency. The more pressure we put on it, the more queries continue, the faster it is 

It can be made faster using DynamoDB Accelerator(DAX). It is a caching server that sits in front of DynamoDB which has sub millisecond read latency

DynamoDB can be used in realtime games which need to update player scores

IT IS A NoSQL DATABASE

In SQL, we are creating 100s of tables to store a lot of data

In NoSQL we can create a single table and we can repeat the data over and over again and we can make faster queries

By using NoSQL, we are trading complex data design to conserve space for cheap storage and fast, simple queries 

### Amazon Redshift 

Managed database

Redshift is a data warehouse which will store data which is supposed to be stored for a long time

We have structured and semi-structured data in an S3 bucket. Redshift will grab the data and bring it in. 

When querying an S3 Data Lake, we have tons of data. Instead of storing the data in S3, we can store it in Redshift 

Designed to work with other analytic servers/services. It can grab data from an S3 bucket and send the data to Amazon QuickSight 

Amazon QuickSight is used to create beautiful reports about data 

### AWS Database Migration Service(DMS)

WAY OF MIGRATING DATABASES FROM ON PREM TO THE CLOUD

Can move a majority of objects, views, stored procedures and functions 

We can use different source and target databases such as shifting data from an expensive on prem database to something such as MySQL in the cloud 

DMS CAN BE USED TO MIGRATE DATABASES TO/FROM THE CLOUD

Lets say we have a database on prem which we want to shift to the cloud using DMS. If people are constantly writing to that database, DMS will still continue to push data to the cloud

### Quiz

1. Which database is supported by the AWS Relational Database Service (RDS)?

```txt
MySQL
```

2. Amazon Aurora is compatible with which database technologies?

```txt
MySQL and PostgreSQL
```

## Load Balancers 

Lets say that our business has a website which is running on a server. 100s of clients are visiting the website and everything is going great. After sometime, our clients increase and now 1000s of clients are visiting the website, which is causing the CPUs and RAMs to crash. We need another server and so we buy another server to handle the load. But this will not work and people are still hitting the 1st server. To tell people to not go to the 1st server all the time and to evenly distribute the load, we will use a load balancer. We'll setup a rule such that when people are visiting our website, go to the load balancer and not the 1st server. The load balancer will ensure that when people are visiting our website, that the load between the 2 servers are being distributed evenly 

In AWS, load balancing is known as Elastic Load Balancing(ELB)

It is a managed service

3 types of load balancers: classic(old, v1), application(new, v2) and network(new, v2). Amazon recommends using v2 load balancers 

AWS guarantees that the load balancer will be working and takes care of the updates, maintenance and high availability 

Costs less to setup your own load balancer but will require more effort from us 

***
