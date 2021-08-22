# AWS Management Concepts

> Arav Budhiraja | 19th August 2021

Course Link: https://my.ine.com/Cloud/courses/756bf216/aws-management-concepts

### AWS - Amazon Web Services

## Topics

1. AWS Support Plans
2. Tagging best practices
3. Billing
4. Well Architected Framework(WAF)
5. Logging
6. Infrastructure as Code
7. AWS Organizations

## Learning Objectives

1. Describe AWS support plans in general and the special plans
2. Tagging in AWS and the best practices for tagging resources
3. Billing in AWS - Billing Console and Calculator 
4. Well Architected Framework- Tool and Lenses
5. Infrastructure as Code with AWS CloudFormation
6. AWS Organization

## AWS Support Plans

A workload is a collection of resources and code that can deliver a profit.

* Determine the support plan needed
* Support options - Basic, Developer, Business and Enterprise

To determine which support plan we have to see what we will be doing in the Cloud

What we can be doing can be from just learning to mission critical workload 

Mission critical workload - Something in the cloud which is generating profit, which a business depends on. THIS IS NOT A PERSONAL PROJECT. 

### Basic Support 

Aimed at when you are learning about AWS and experimenting and gaining knowledge
 
 Included in ALL AWS ACCOUNTS
 
 - 24/7 access to customer service - Email/Text support. Not gonna get a fast result. Used when asking questions which do not require an immediate results. The support provides documentations, whitepapers and a support forum. 
 - AWS Trusted Advisor - Provide recommendations that help you follow best practices in AWS. Checks for ways to improve your infrastructure, security, performance, reduce costs and monitor service quotas. 7 checks only.
 - AWS Personal Health Dashboard: Shows you what is going on their infrastructure at the moment. 
 - BASIC SUPPORT IS FREE

### Developer Support

Aimed at when a person is working on a project that is going to become a large and real world project. Used when you are testing your project. 

- Response times: For general problem response time is less than 24 hours and for impaired problems it is less than 12 hours. Note: The response time is during business hours. When setting up your AWS account, you have to indicate your region. That regions sets your business hours. 
- Cost: There are two options when it comes to developer support. You will pay the greater of the following 2 options
	-  $29 per month 
	-  3% of the bill
	
	If the 3% of your bill is $50, then you would pay $50 and not $29. If the 3% of your bill is $10, then you would pay $29. 
	
### Business Support 

Aimed at a business which is ready to put a large project into AWS

- Full set of checks with AWS Trusted Advisor
- 24/7 phone, email, chat access to Cloud Support Engineers
- Response times: For impaired problems response time is less than 4 hours and if the project is down, then the response time is less than 1 hour.
- Cost: There are 3 options when it comes to business support. You will pay the greatest of the following 3 options
	-  $100 per month 
	-  10% of the bill, if the bill is less than $10K
	-  10% of $10K + 7% of the bill which is greater than $10K and less than $80K
	
	We will get a greater discount if we use more resources
		
### Enterprise Support

Aimed at large projects whose profit can be measured in seconds

- Response time: If the business is down, response time is less than 15 minutes
- Designated Technical Account Manager who will help when their is a problem in your organization and they can give you ideas
- Cost: There are 3 options when it comes to enterprise support. You will pay the greatest of the following 3 options
	-  $15,000 per month 
	-  10% of the bill, if the bill is less than $150K
	-  10% of $150K + 7% of the bill which is greater than $150K and less than $500K

	We will get a greater discount if we use more resources

### Summary

1. Basic: Free and great if you're just starting out
2. Developer: Experimenting with workloads. Little better response time and more access to the systems
3. Business: Running a workload which will generate a profit
4. Enterprise: Run a workload which has to be running and is essential for a business

![support-plans](support-plans.png)

### Quiz

1. For someone learning AWS for the first time and not needing to build complex infrastructures, what would be the appropriate support level?

```txt
Basic Support
```

2. Which AWS Support Option gives you a designated technical account manager?

```txt
Enterprise Support
```


## AWS Tagging Best Practices

* What is tagging?
* How to use tags
* Determine required tags 
* Areas for best practice in tagging 
* Resource for tagging

Tagging is a way of adding metadata to identify, categorize and secure AWS resources

When creating a tag, we have to specify a key and it's value

If we are creating an S3 Bucket for a customer, we add a tag such as 'Owner' and it's value would be an email such as 'test@test.com'. So when a person is going through the resources and wants to know who owns this bucket, the person can see the tag which gives them the email. Another tag is to specify whether a bucket can be deleted. We can give the key as 'CanBeDeleted' and value as 'Yes' or 'No'. 

CLOUD IS NOT AN IT OPERATION, IT IS A BUSINESS STRATEGY 

  A cross functional team should be organized to identify the tag requirements. The IT Team should not only create tags, they should ask people such as HR and Finance Team.
  
  TAGS CAN BE FREELY NAMED
  
  The IT team can organize a tag requirements workshop so contributors can work together to identify the required tags
  
  Areas where tagging can be implemented:
  
  - AWS Console: In the console, we can do grouping in the resource manager which can be used to show everything owned by group 'abcd' or show everything which can handle 'abcd'
  - Cost allocation: As we get deeper in the cost, the financial operations team should be able to create a detailed report. Instead of the team saying that 'this group is using this much', they should be able to say 'this group is using this much for this project in this region'. Tagging will be helpful for this
  - Automation: When using Infrastructure as Code
  - Operations Support: When the Operations needs to find a particular report, tags will be extremely useful for them to find the resource
  - Access control: To specify which people can access a particular resource
  - Security risk management:  To determine which type of actions can be performed on a resource
  
  ### Quiz
  
  1. When creating a list of tags that an organization will use, what is the best approach?
  
```txt
Create a cross functional team to organize and identify tag requirements.
```

  2. What are some areas of interest for tagging resources in AWS? (Select all that apply)

```txt
Automation,Operations support,Cost allocation,Access Control
```

  ## Billing in AWS
  
  * Reality of cloud cost
  * Billing Dashboard
  * AWS Cost Explorer 
  * AWS Pricing Calculator 
  * AWS Trusted Advisor
  * Top 3 ways to lower an AWS bill

Variable expense - Pay for resources as and when you use them

Capital expense - Pay an upfront cost for all resources at one time

CLOUD COSTS NEED MANAGEMENT 

A financial operations team would help in managing cloud costs

### Billing Dashboard

Billing Dashboard gives an immediate view of the cost, quick access to the billing details and a cost explorer 

The Billing Dashboard shows the costs for EC2, Route53, DataTransfer, CloudTrail and OtherServices

Once we see an extra cost for something such as EC2, we immediately know we have a running EC2 instance which we have to stop. The process is extremely quick and easy

If we click on 'Bill Details', it shows a breakdown of the costs

### Cost Explorer 

Cost explorer is an advanced tool where filters and tags can be used to check all the details about the costs in AWS

In the cost explorer, we can dive deep into the costs and trends. It shows the % by which costs have gone up, costs overtime which will help to find trends and monthly and daily costs of services

### AWS Pricing Calculator

<a href="https://calculator.aws">AWS Pricing Calculator</a> helps determine the cost of services which we wish to use on AWS. We can select the service, configure the service and include the support costs, and then it shows the total cost.

THIS IS VERY IMPORTANT FOR A PROPOSAL. 

We have to first search and select the service we wish to use and then provide a brief description, region to run the server in, pricing model, etc.

If we have to specify information such as 'Processed bytes' or 'Average number of connections', we can ask the IT team for this information

Once all the information has been specified, we can scroll to the bottom and check the cost per month. We can now add this to our estimate. In our estimate, the total and annual and monthly cost and monthly cost per service are displayed

Snapshots - Backups

The estimate can also be exported so that it can be used in a document or presentation

### AWS Trusted Advisor 

The AWS Trusted Advisor check all your services and gives recommendations about performance, security, fault tolerance, service limits and cost optimization

The advisor looks at all our costs, find out where our money is being spent and lets us know where we can do a better job

It can detect something such as an EC2 instance which is running and is not being used and is sitting idle 

The number of checks is limited as is determined by the chosen support plan

Higher level support will help in finding more and better ways to reduce costs

It can be found by search for trusted advisor in AWS services

### Top 3 ways to lower an AWS Bill

* Terminating underutilized EC2 instances
* Terminating underutilized EBS instances
* In S3 Buckets, you can use intelligent tiering which will make it easy to get into the bucket. We can change it to in-frequent access tiering. It will cost more to get to it but costs less to store. In an average business, only 20% of data in a bucket is regularly used.

  ### Quiz
  
 1. What is one of the three top ways to lower an AWS bill?

```txt
Implement tiered storage in Amazon S3
```

2. You've been asked to project the cost of a proposed project in AWS. Which tool would help you determine the cost?

```txt
AWS Pricing Calculator
```

## AWS Well-Architected

SECRET WEAPON OF PEOPLE WHO ARE BEST AT AWS

* Well-Architected Framework
* Well-Architected Tool
* Well-Architected Lenses

### Well-Architected Framwork(WAF)

Started as a single whitepaper but has grown to several tools and whitepapers

It is a list of questions which ask if 'abcd' is the best architecture

### Well-Architected Pillars

* Operational Excellence: Focuses on providing insights into status, efficient and effective operations and if we are improving. Asks if we are efficiently running our workload and are we improving. How to structure our organization and support business outcomes? How to design the workload so that it's state can be understood? The Well-Architected Framework will stop you and ask what has to be added to the workload to understand what is happening 
* Security: Describes how to use services in AWS to protect systems, data and assets and improve the security of our architecture. Asks if we are following best security practices. How do you detect and investigate security events? How do you classify your data?What criteria makes data important?
* Reliability: Focuses on building an architecture that has strong foundations, is resilient, can recover from failures and is maintained with best practices. Asks how we can build a reliable architecture. If something breaks, we have a way to quickly bring more architecture to support it. How do you monitor workload resources? How do you use fault isolation to protect the workload?
* Performance Efficiency: Focuses on efficient use of services in the architecture to meet customer demands and business requirmenets. Asks how do you evolve the workload to take advantage of new releases. 
* Cost Optimization: Helps in understanding and controlling where money is being spent and avoiding unnecessary costs. How do you use pricing models to reduce costs? How do you monitor costs and usage?

### Well-Architected Tool

Provides a list of questions with regards to the pillars. It provides guidance based on established best practices

Lets you create a workload and you have to fill up details about it 

Once a workload is created, the security team can come and handle the security workload, the operations team can deal with the operational excellence and the finance team can deal with the cost optimization 

### Well-Architected Lenses

Part of Well-Architected Framework which provides whitepapers about analytics, IoT, financial services, etc. 

### Quiz

  1. How many pillars, or areas of focus, are part of Well-Architected?
  
```txt
5
```

  2. Which of the following is not a pillar, or area of focus, in Well-Architected?

```txt
Service Selection Optimization
```

## Amazon CloudWatch & Amazon CloudTrail

Used for logging in AWS

* Amazon CloudWatch: Purpose, Main points
* Amazon CloudTrail: Purpose

### Amazon CloudWatch

Used to watch or keep an eye on our AWS resources

Lets you observe activity on an AWS resource

Monitors various aspects of performance such as EC2 instance CPU and read or writes to an RDS DB 

It monitors every 5 minutes by default but it can be changed, but it may cost more

Triggers can be created, such that when a particular value such as CPU Utilization exceeds a limit, then you can configure it to send an email/message letting you know that the condition has turned true

Applications written in a language such as python can be used to write to CloudWatch

If we are using CloudWatch to monitor an EC2 instance, we can click on the Instance ID and navigate to 'Monitoring' in the popup window

With CloudWatch, AWS cannot tell statistics such as memory usage because if it were measuring the memory usage, it means that they were in your memory and can read the memory. 

CloudWatch can be extended with various scripts. ENSURE THAT THESE SCRIPTS ARE FROM TRUSTED SOURCES

### Amazon CloudTrail

Stores logs of everything in an S3 Bucket 

Keeps track of every API call

Everything in AWS is an API(Application Programming Interface) call, and everything is logged by CloudTrail

Critical for auditing resources for compliance

Helps in security analysis and automation 

Trails can be delivered to CloudWatch when suspicious logs are detected and then  a trigger can be setup to alert the person via email/text

### Quiz

  1. What is the purpose of Amazon CloudWatch?
  
```txt
Provide monitoring and observability into an AWS infrastructure
```

  2. When Amazon CloudTrail creates logs, by default, where is the information stored?

```txt
Amazon S3
```

## Infrastructure as Code(Iac)

VERY IMPORTANT TO BE GREAT IN THE CLOUD

* What is IaC
* Reason for using IaC
* AWS CloudFormation

Gives us a way to declare our resources in code and we get exactly what we want

Following instructions to build infrastructure is full of potential errors 

To solve this problem, we need a way to declare our infrastructure. Instead of installing a web server, we have code which does it. It gives a declarative language and we say to build 'abcd', 'efgh' and 'ijkl'

If we create an infrastructure using IaC, in a development environment we can easily move the code to the test environment, we get the same infrastructure without configuring additional settings. It is exactly the same

Once in production, most apps fail. IaC can fix this. There is a one to one relation. It offers reproducibility such that the state in dev environment is the same as the one in the test and production environments 

A collection of resources created with IaC is known as a stack

### AWS CloudFormation

Once we have the code, we can use CloudFormation to model what we wish to create in AWS. It lets us create, update and delete resources

All of the resources, combined are known as a stack. CloudFormation easily lets us take down the infrastructure for sometime and we can bring it back up easily

CloudFormation is the definitive source for our AWS architecture

### Quiz

  1. What is a collection of resources created with IaC called?
  
```txt
A stack
```

  2. Which AWS services is used to implement infrastructure as code?

```txt
AWS CloudFormation
```

## AWS Organizations

Great utility in AWS that lets us take many AWS accounts and bring them under one 'umbrella'

* AWS Organizations - Basics, Management, Billing 

We have a company which is growing. The company has many departments which is creating many accounts for their environments such as dev, testing and production 

To handle this growth, we will use AWS organizations which will let us centrally manage all the accounts. You can create and apply policies and it will apply it across the entire infrastructure. It gives central security and we can audit all the organizations from one place

We can create a policy such as the IT Team cannot use the billing environment, then the policy would flow down to all the organizations

Thus, from once organization, we can manage all the other organizations 

AWS Organizations brings all the costs of all accounts into one bill

Since AWS gives greater discounts for the more resources we use, and since we are having so many organizations running services and using more resources, then when they are all combined together, we have a greater discount

### Quiz 

  1. How can AWS Organizations help lower your AWS bill?
  
```txt
A consolidated bill will reflect higher consumption, and possibly lower cost, for resources used in AWS.
```

  2. What is the name of the service that allows you to centrally organize separate AWS accounts?

```txt
AWS Organizations
```

****
