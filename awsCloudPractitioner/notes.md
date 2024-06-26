# Cloud Computing

## What is cloud Computing

> Cloud Computing is the delivery of computational resources like servers, databases, networking software, analytics and intelligence over internet to offer faster inovation, flexible resources and economies of scale.

## Types of Cloud Computing

### Infrastructure as a Service (IaaS)
Provides networking computers, data storage
Highest level of flexibility
Easily parallel with traditional infrastructure.

### Platform as a Service (PaaS)
Don't need to manage infrastructure.
Focus on deployment and management of app

### Software as a Service (SaaS)
Complete product that is run and managed by service provider

# IAM 

IAM = Identity And Access Management 
Global Service
Root account created by default, shouldn't be shared or used
Groups only contain user's not other groups
Users don't belong to a group can be in different groups
Users and groups can be assigned JSON documents called policies
These policies define permissions to users
Use least privilige principle: 
- Don't give more permissions than a person needed

Inline Policy: A policy that attach to a user only

## IAM Policies Structure

Version: "2012-10-17"
id: An identifier (Optional)
Statement: One or more individual statements
> Sid: Statement id
Effect: Whatever the statements aloow or denies access
Principal: account/user/role to which this policy applied to
Action: List of actions policy allows or denies
Resource: List of resources which the actions applied to. 
Condition: Conditions for when the policy in effect (optional)

### Admin Policy

{
    "Version": "2012-10-17",
    "Statements": [
        {
            "Effect": "Allow",
            "Action": "*",
            "Resource": "*"
        }
    ]
}

You can create a policy from policies tab in IAM Console. 
In AWS you can setup password policy to a IAM user
#### Usage of MFA highly recommended
> MFA: password + mfa key = login

## Types of MFA Devices

Virtual MFA Device (Phone, Authy)
Universal 2nd Factor U2F Security Key (An actual Device)
Hardware Key Fab MFA Device 
Hardware Key Fab MFA Device for AWS GovCloud

## How can users access AWS?

There is 3 ways to access AWS Services:
> AWS Management Console
AWS CLI
AWS SDK

## What is AWS SDK 

Language specific API's (set of libraries)
Enables you to access AWS Services programmatically
Embedded within your application
Supports:
- SDK's (Java, Python, Go, Nodejs)
- Mobile SDK's (Android, IOS, ...)
- IoT Device SDK's (Embedded c, Arduino, ...)

Example: AWS CLI is a program built in AWS Python SDK.
#### For CLI and SDK access you must configure a secret key. 
Every file you created in AWS Cloud Shell will exist in next uses. Stays forever. 

## IAM Roles for Services

Some AWS services will need to perform actions on your behalf(As your permission)
To do so, we will assign permissions to AWS Services with IAM Roles
IAM Roles will be given to services not users
Common Roles:
- EC2 Instance Roles
- Lambda Function Roles
- Roles for Cloud Formation

## IAM Security Tools

IAM Credential Report(account level):
- A report that lists all your accounts users and the staatus of their various credentials

IAM Access Advisor 
- Shows the service permission granted to a user and when those services last accessed
- You can use this information to revise your policies.

## IAM Best Practices

Don't use root accout accept AWS account setup.
Create an IAM Users for each people who need to access to console in your organization
Assign users to groups and assign permission to groups
Create a strong password policy
Use access keys for programmatic access
Audit permissions of your account using IAM Credential Report and IAM Access Advisor

## Shared Responsibility Model for IAM

### AWS:
Infrastructure
Configuration and vulnerability analysis
Compliance Validation

### User:
Users, Groups, Roles, policies management and monitoring
Enable MFA on all accounts
Rotate all your keys often 
Use IAM tools to apply appropriate permissions
Analyze access patterns and permissions

## IAM Summary

Users: Real people who has a password for console
Groups: contains users only, define permission to individuals in the group
Policies: JSON documents for defining permissions to users or groups
Roles: Permissions for AWS Services
Security: MFA + Password policies
AWS CLI: Use AWS Services via CLI
AWS SDK: Use AWS Services via programming 
Audit: IAM Credentials Report and IAM Access Advisor

# EC2 (Elastic Compute Cloud)

EC2: Infrastructure as a Service
Ity mainly consists in the capability of:
- Renting virtual Machines (EC2)
- Storing data and Vitual MAchines (EBS)
- Disturbuting Load Accross Machines (ELB)
- Scaling the services with auto scaling group(ASG)

#### Knowing EC2 is fundemental to understand how cloud works.

## EC2 User Data

It is possible bootstrap our instances using EC2 User Data Script.
Bootstraping means launching commands when machine starts
The script only run once at instance first start 
EC2 User Data Automates:
- Installing Updates
- Installing Software 
- Downloading Common Files

EC2 User Data Runs as Root User 

## EC2 Instance Types

You can use different types of EC2 instances
They are optimized for different use cases
There are 8 class of them 

1. General Purpose
2. Compute Optimized
3. Memory Optimized
4. Accelerated Computing
5. Storage Optimized
6. HPC(High Performance Computing) Optimized 
7. Instance Features
8. Measuring Instance Performance

- m5.2xlarge
> m: Instance class
5: Instance generation 
2xlarge: size within the instance class 

1. General Purpose

Great for diversity of workloads such as web servers or code repositories
Balance between: 
- Compute 
- Memory
- Networking

2. Compute Optimized

Great for compute intensive tasks that require high performance processor such as: 
- Batch Processing workloads
- Media Trasnscoding
- High Performance Web Servers
- High :Performance Computing (HPC)
- Scientific Modelling and Machine Learning
- Dedicated Gaming Servers

3. Memory Optimized

Fast Performance Workloads that process large data sets in memory:
- High Performance relational and non relational databases
- Distrubuted web scale cache stores
- In-Memory Databases optimized for BI(Bussiness Inteligence)
- Application performing real-time processing of big unstructured data 

4. Storage Optimized

Great for storage-insentive tasks that require high, sequential, read and write access to large data sets on local storage.
- High Frequency Online Transaction Processing(OLTP) systems
- Relational or No-SQL Databases
- Cache for in memory databases
- Data Warehousing Applications
- Distrubuted File Systems

## Security Groups 

Security Groups are fundemental of networking security in AWS
They control how traffic allowed in to or out of our EC2 instance
Security groups only contain allow rules
Security group rules can reference by IP or by security group
Inbound Traffic: Traffic to inside our EC2 instance
Outbound Traffic: Traffic from our EC2 instance.

#### Security Groups Deep Dive

Security groups are acting as a firewall on EC2 instance
They Regulate:
- Access to ports
- Authorized IP ranges 
- Control Inbound Traffic (To EC2)
- Control Outbound Traffic (From EC2)

Can be attached multiple instances
Locked down to region/VPC combination
Does live outside the EC2 - If traffic is blocked EC2 instance won't see it
Maintaining a seperate security group for ssh access is a good practice
If your application is not accesable(time out), than it is a security group issue
If your application gives a connection refused error, it's an application error it's not launched
All inbound traffic blocked by default 
All outbound traffic is authorised by default

## Classic Ports to know

22 = SSH(Secure Shell) - Log in to Linux Shell
21 = FTP(File Transfer Protocol) - uploads files into a file share ü
22 = SFTP(Secure File Tranfer Protocol) - uploads files using SSH
80 = HTTP(Hyper Text Transfer Protocol) - access unsecured websites
443 = HTTPS(Secure Hyper Text Tranfer Protocol) - Access Secure Websites
3389 = RDP(Remote Desktop Protocol) - Login to a Windows Instance

## SSH 

SSH is one of the most important function. It allows you to control a remote machine, all using the command line

- ssh -i key.pem ec2-user@MachineIP

#### You must make your key unwritable with above command. 

- chmod 0400 key.pem

#### You can make ssh connection to a remote machine using your browser without an access key using ec2-instance-connect.
Right click to your ec2 instance and choose connect from dropdown. Default user is ec2-user. 
There is an AWS CLI exist every ec2 instance but this CLI is not configured. 
#### Configuring an EC2 instance with your credentials is a bad idea you need to use IAM roles.

## EC2 Instance Purchasing Options

On-Demand Instances:
- For short workloads, predictable pricing, pay by second

Reserved Instances
- Reserved Instances for long workloads
- It's convertable you can change the instance type

Savings Plan(1 and 3 Years)

Spot Instances
- For short workloads 
- It is cheap
- Can loose instance(less reliable)

Dedicated Hosts
- Book an entire physical server and control instance placement

Dedicated Instrances 
- No other costumers will share your hardware

Capacity Reservations
- Reserve capacity in a specific AZ for any duration

## EC2 On-Demand

Pay for what you use
- Linux or Windows - billing per second, after first minute
- All other OS billing per hour

Has the highest cost but no upfront payment
No Longterm commitment
Recommended for short term uninterrupted workloads, where you can't predict how the application will behave.

## EC2 Reserved Instances

A lot cheaer then On-Demand
You reserved specific instance attributes(Instance Type, OS, Region, Tenancy)
Reservation Period (1 or 3 years)
Payment Options:
- No Upfront(+Discount)
- Partial Upfront(++ Discount)
- All Upfront(+++ Discount)

Reserved Instances Scope:
- Regional or Zonal(Reserve capacity in an AZ)

Recommended for steady state usage applicastion like a database.
You can buy or sell in the reserved instance marketplace

The Convertable Reserved Instance: 
- Can change the instance type, instance family, OS, Scope and Tenancy.
- Less Discount for a reserved instance because of it's flexibility.

## EC2 Savings Plan

Get a discount based on long term usage
Commit a certain type of usage ($10/hour)
Usage beyond EC2 Savings Plan is billed at the On-Demand Price
Locked to a specific instance family and AWS Region (m5 in eu-west-1)
Flexible across:
- Instance Size 
- OS 
- Tenancy(Host, Dedicated, Default)

## EC2 Spot Instances

Can get a discount up to %90 compared to On-Demand
Insatances that you can lose any time if your max price is less then the current spot price
The most cost efficient instances in AWS.
Usefull for workloads that are resillient to fail:
- Batch jobs
- Data analysis
- Image Processing
- Any distrubuted workloads
- Workloads with a flexible start and end

#### Not suitable for critical jobs and databases.

## EC2 Dedicated Hosts

A physical server with EC2 instance capacity fully dedicated to your use
Allows you to address compliance requirements and use your existing server-bound software licenses(per socket, per core, VM Softvare Licenses)
The most expensive option 
Purchasing Options:
- On-Demand (Pay per second)
- Reserved 1 or 3 Years (No Upfront, Paretial Upfront, All Upfront)

Usefull for software that have complicated license model(BYOL - Bring Your Own License)
Or for companies taht have strong regulatory and compliance needs

## EC2 Dedicated Instances

Instances that run on hardware dedicated to you 
May share hardware with other instances in same account
No control over instance placement(Can move hardware after start/stop)

## EC2 Capacity Reservations

Reserve On Demand instances capacity in a specific AZ for any duration
You always have access to EC2 capacity when you need it
You're charged On Demand price whether you run instances or not. 
No time commitment, No billing Discounts.
Combine with Regional Reserved Instances and Savings Plan to benefit from billing discount.
Suitable for short term uninterrupted workloads that needs to be in a specific AZ.

## Shared Responsibility Model for EC2

### AWS

Infrastructure (Global Network Security)
Isolation on Physical Host
Replacing faulty hardware
Compliance Validation

### User

Security Groups Rule
OS patches and updates
Software and utilities
IAM Roles assigned to EC2
Data security on your instance

## EC2 Summary

EC2 instance: AMI(OS) + Instance Size(RAM, CPU) + Storage + Security Groups + EC2 User Data
Security Groups: Firewall for EC2 Instances
EC2 User Data: Script that run once at the start 
SSH: Secure Shell cvonnection to EC2 Instance (Port: 22)
EC2 Instance Role: Link to IAM Roles 
Purchasing Options: On-Demand, Spot, Reserved, Dedicated Host, Dedicated Instance

# EBS Elastic Block Store

A EBS(Elastic Block Store) volume is a network drive you can attach to your instances while they run
It allows your instances to persist data even after termination
They can only be mounted by one instance (CCP Level)
They are bound to a specific AZ

## EBS Volume

It's a network drive(not physical drive)
- It uses network to communicate with instance, which means there can be a latency
- It can be detached from an EC2 instance and attached another one pretty quickly

It locked to an AZ
- An EBS volume in eu-east-1a can't be attached to an instance in eu-east-1b
- To move a volume across, you first need to snapshot it.

Have a provisioned capacity(size in GB's and IOPS)
- You get billed for provisioned capacity.
- You can increase capacity over time

## EBS Delete on Termination

Control EBS volume behaviour when an EC2 instance is terminated.
- For root volume it's enabled by default.
- For any other volume that attached to EC2 instance this attribute is disabled

This behaviour can be controlled by Console and CLI
Use Case: preserve root volume when instance is terminated 

## EBS Snapshots

Make a backup(snapshot) of your EBS volume at a pointy in time. 
Not necessary to detach volume to do a snapshot but recommended
Can copy snapshots across AZ or Regions.

### Snapshot Features

EBS Snapshot Archive
- Move a Snapshoty to Archive Tier that is a lot cheaper 
- Takes within 24 to 723 hours to restore

Recycle Bin for EBS Snapshots
- Setup Rules to retain deleted snapshots so you can recover after an accidental deletion 
- Specify retention(from 1 day to 1 year)

# AMI

AMI = Amazon Machine Image
AMI are a customization of an EC2 instance 
- You add your own software, configuration, OS, monitoring
- Faster boot/configuration time because all software pre-packaged

AMI are built for a specific region (can be copied accross the regions)
You can launch EC2 instances from: 
- A public AMI: AWS provided
- Your own AMI You make and maintain yourself
- An AWS Marketplace AMI: An AMI someone else is made and potentially sells

## AMI Process

Start an EC2 instance and customize it
Stop the instance (for data integrity)
Build an AMI - This will also creates an EBS Snapshot
Launch instances from other AMI's. 

## EC2 Image Builder 

Used to automate thwe creation of VM's or Container images. 
- Automate the creation, maintain, validate and test EC2 instance

Can be run on a schedule(weakly, whenever packages updated, etc)
Free service(Only pay for underlying resources)

## EC2 Instance Store

EBS volumes are network drives with good but limited performance
If you need a high performance hardware disk, use EC2 Instance Store
- Better IO performance
- EC2 instance Store loose their storage if they're stopped(ephemeral)
- Good for buffer/cache/scratch data/temporary content
- Risk of data loss if hardware fails
- Backups and replications are your responsibility

# EFS Elastic File System

Managed NFS(Network File System) that can be mounted on hundreds of EC2 instances
EFS works with Linux EC2 instances in multi AZ
Highly available, scalable, expensive(3x gp2), pay per use, no capacity planning

## EFS Infraquent Access(EFS-IA)

Storage class that is cost-optimized for files not accessed every day
Up to %92 lower cost compared to EFS Standard
EFS will automatically move your files to EFS-IA based on last time they accessed
Enable EFS-IA with a lifecycle policy
Example: move files that are not accesed for 60 days to EFS-IA
Transparent to the applications accessing EFS.

## Shared Responsibility Model for EC2 Storage

### AWS

Infrastructure 
Replication for data, for EBS volumes, EFS drives
Replacing faulty hardware
Ensuring their employees can't access to your data

### User

Setting up backup/snapshot procedures
Setting up data encryption
Responsibility of any data on the drives
Understanding the risk of using using EC2 Instance Store. 

## Amazon FSx

Launch 3'rd party high performance file system on AWS
Fully managed service:
- FSx for Lustre
- FSx for Windows File Server
- FSx for NetApp ONTAP

## Amazon FSx for Windows File Server 

A fully managed, highly reliable and scalable Windows Native shared file system 
Built on Windows File Server
Supports SMB protocol and Windowes NTFS 
Integrated with Microsoft Active Directory
Can be accessed from AWS or your on-premise infrastructure

## Amazon FSx for Lustre

A fully managed, high performance, scalable file storage for High Performance Computing(HPC)
The name lustre is derived from linux and cluster 
Machine Learning, Analytics, Video Processing, Financial Modelling
Scales up to hudreds of GB/s, millions of IOPS, sub-ms latencies

## EC2 Instance Storage Summary

EBS volumes: 
- Network drives that is attached to one EC2 instance at a time
- Mapped to an AZ
- Can use EBS Snapshots for Backups, tranferring EBS volumes across AZ

AMI: create ready to use EC2 instances with our costumizations
EC2 Image Builder: automatically build test and distrubute AMIs
EC2 Instance Store:
- High performance hardware disk attached to our EC2 instance 
- Lost if our instance stopped/terminated 

EFS: Network File System Can be attached hudreds of instances in a region
EFS-IA: Cost optimization for not frequently accessed files. 
FSx for Windows: Network file system for Windows Servers
FSx for Lustre: High Performance Computing Linux file system. 

# ELB Elastic Load Balancing

## Scalability and High Availability

### Scalability

Scalability möeans that an application/system can handle loads by adopting.
There are two kinds of scalability:
- Vertical Scalability
- Horizontal Scalability

Scalability is linked but different to  High availability.

### Vertical Scalability

Vertical scalability means increasing the machine size of the instance.
For example app runs in t2.micro we can scale vertically to t2.large.
Vertical scalability very common for non-distrubuted systems such as databases
There's usually a limit how much you scale(hardware limit)

### Horizontal Scalability

Horizontal scalability means increasing the number of instances/systems for your application
Horizontal scaling implies distrubuted systems This is very common for web applications/ modern applications
It's easy to horizontally scale thanks to cloud offerings such as Amazon EC2

### High Availability

High availability usually goes hand in hand with hortizontal scaling
High availability means running your application/system inb at least 2 AZ
The goal of high availability is survive a data center loss(disaster)

## High Availability and Scalability for EC2

Vertical SCaling: Increase Instance size(scale up/down)
- From t2.nano - 0.5 GB RAM, 1 vCVPU
- To u-12tb1.metal - 12.3 TB RAM, 448 vCPU

Horizontal Scaling: Increase number of instances(scale out/in)
- Auto Scaling Group 
- Load Balancer

High Availability:Run instances for the same application across multi AZ
- Auto Scaling Group Multi AZ
- Load Balancer Multi AZ

## Scalability vs Elasticity (vs Agility)

Scalability: ability to accomodate a larger load by making the hardware atronger(scale up), or by adding nodes(scale out)
Elasticity: Once a system is scalable, elasticity means that there will be some auto-scaling so that system can scale based on the load. This is cloud friendly: pay-per-use, match demand, optimize costs
Agility(not related to scalability is a distractor): New IT resources only a click away, Which means that you reduce the time to make those resources available to your developers from weeks to just minutes.

## ELB Overview 

Load Balancers are servers that forward internet traffic to multiple servers(EC2 instances) downstream.

### Why use a Load Balancer

spread load across multiple downstream instances
Expose a single point of access (DNS) to your application
Seamlessly handle failures of downstream instances
Do regular health checks to your instances

Provide SSL Termination(HTTPS) to your website. 
Highly available across zones
An ELB(Elastic Load Balancer) is managed Load Balancer:
- AWS guarantee that it will be working 
- AWS takes of upgrades, maintenance, high availability
- AWS provides only a few configuration knobs

It cost less to setup your own load balancer but it will be a lot more effort on your end(maintenance, integration)
4 kind of Load Balancers offered by AWS:
- Application Load Balancer (HTTP/HTTPS) - Layer 7
- Network Load Balancer (Ultra high performance allows TCP) Layer 4
- Gateway Load Balancer (GENEVA) Layer 3
- Classic Load Balancer (retired in 2023) - Layer 4 and 7

### Application Load Balancer

HTTP/HTTPS/gRPC protocols Layer 7
HTTP Routing Features
Static DNS

### Network Load Balancer

TCP/UDP Protocols (layer 4)
High Performance: millions of requests per second
Static IP through Elastic IP

### Gateway Load Balancer

GENEVE Protocol on IP Packages(Layer 3)
Route Traffic to a Firewall that you managed on EC2 Instances
Intrusion Detection

## Auto Scaling Group(ASG) Overview

In real life, the load on your websites and application can change over time
In cloud you can create and get rid of servers very quickly
The goal of Auto Scaling Group(ASG) is:
- Scale out(add EC2 instances) to match an increasing load
- Scale in(remove EC2 instances) to match a decreasing load
- Ensure we have minimum and maximum number of machines running
- Automatically register new instances to a load balancer
- Replace unhealty instances

Cost savings: only run at an optimal capacity(principle of cloud)

## Scaling Strategies

Manual Scaling: Upgrade the size of ASG manually
Dynamic Scaling: Respond to changing Demand 
- Simple/Step Scaling
- - When a CloudWatch alarm is triggered(CPU > %70), then add 2 units
- - When a CloudWatch alarm is triggered(CPU < %30), then remove 1 units
- Target Tracking Scaling:
- - Example: I want the avrage ASG CPU to stay at aroun %40
- Scheduled Scaling 
- - Anticipate a scaling based on known usage patterns
- - Example: Increase the min capacity to 10 at 5 pm on Fridays
- Predictive Scaling 
- - Uses machine learning to predict future trafic ahead of the time
- - Automatically provisions right number of EC2 instances in advance
- - Usefull when your load has predictable time based patterns

## ELB and ASG Summary

High availability vs Scalability(vertical and horizontal) vs Elasticity vs Agility in the Cloud
Elastic Load Balancer(ELB):
- Distrubute traffic across backend EC2 instances can be multi AZ
- Supports health checks
- 4 types of ELB exis:
- - Classic(old)
- - Application(HTTP - L7)
- - Network(TCP - L4)
- - Gateway(GENEVA - L3)
Auto Scaling Groups(ASG):
- Implement elasticity for your application across multi AZ
- Scale EC2 instances based on the demand on your system replace unhealty 
- Integrated with the ELB

# Amazon S3

Amazon S3 stands for Simple Storage Service
Amazon S3 is one of the main bulding blocks of AWS
It's advertised as infinitely scaling storage
Many websites use Amazon S3 as a backbone
Many AWS services use Amazon S3 as an integration as well

## S3 Use Cases

Backup and storage
Disaster Recovery
Archive
Hybrid Cloud Storage
Application Hosting
Media Hosting
Data lakes and big data analytics
Software Delivery 
Static Website

## Amazon S3 Buckets

Amazon S3 allows people to store objects(files) in "buckets"
Buckets must have globally unique name (across all regions all accounts)
Buckets are defined at region level
S3 looks like a global service but buckets bnound to a specific region
Naming Conventions:
- No uppercase, No Underscore
- 3-63 characters
- Not an IPü
- Must start weith lower case letter or number

## s3 Objects

Objects(files) has a key
The key is the full path:
- s3://my-bucket/my-folder/my-file.txt

The key is composed of prefix + object name
There is no concept of directories within buckets
Just keys with very long name just contain slashes(/)
Objects values are content of the body
- Max object size is 5 TB
- If uploading more then 5 GB must use multi-part upload

Metadata(list of key/value pairs - sytstem or user metadata)
Tags(Unicode key/value pairs - up to 10) - usefull for security and lifecycle
Version ID (If version enabled)

## S3 Seurity

User based:
- IAM policies - which API calls should be allowed for a specific user from AMI

Resource Based 
- Bucket Policies: Bucket wise rule from s3 console - allows cross account
- Object Access Control List(ACL): finer grain(can be disabled)
- Bucket Access Control List(ACL): less common (can be disabled)

Note: An IAM principal can access S3 object if :
- The user IAM permissions Allow it or the resource policy allows it
- AND there is no explicit DENY

Encryption: encrypt objects in S3 using encryption keys

## S3 Bucket policies

JSON based policies
- Resources: buckets and objects
- Effect: Allow or Deny
- Actions: Set of API calls Allow or Deny
- Principal: The account or user to apply the policy to

Use S3 bucket for policy to:
- Grant public asccess
- Force objects encrypted at upload
- Grant access to another account

## Bucket settings for Block Public Access

These setting were created for prevent company data leaks
If you know your bucket should never be public, leave these on
Can be set at the account level

## Amazon S3 Satic Webdsite Hosting

S3 can host static website and make them accesable on the internet.
The website URL will be:
- http://bucket-name.s3-website-region.amazonaws.com

If you get a 403 Forbidden error öake sure bucket policy allows public read

## Amazon S3 Versioning

You can version objects in S3
It is enabled at the bucket level
Same key overwrite weill change the version
It is best practice to version your buckets
- Protects against unintended deletion
- Easy roll back to preevious version

Notes:
- Any file that is not versioned prior to enabling versioning will have version "null"
- Suspending the versioning does not delete the previous version

## Amazon S3 Replication (CRR and SRR)

Must enable versioning in source and destination buckets
Cross region Replication(CRR)
Same Region Replication(SRR)
Buckets can be in different AWS accounts
Copying is asynchronous
Must give proper IAM permissions to S3
Use Cases:
- CRR - compliance, lower latency access, replication across accounts
- SRR - log aggregation live replication between production and test accounts

## S3 Storage Classes

Amazon S3 Standaerd - General Purpose
Amazon S3 Standard- Infrequent Access
Amazon S3 One Zone - Infrequent Access
Amazon S3 Glacier Instant Retrieval
Amazon S3 Glacier Flexible Retrieval
Amazon S3 Glacier Deep Archive
Amazon S3 Intelligent Tiering

Can move between classes manually or using S3 lifecycle configurations.

## S3 Durability and Availability

Durability:
- It has %99 durability
- Same for all storage classes

Availability:
- Measures how readily available a service is
- Varies depending on the bstorage class

### S3 Standard - General Purpose 

%99.99 Availability
Used for frequently accesed data
Low latency and high throughput
Sustain 2 concurrent facility failures
Use Cases:
- Big Data Analytics
- Mobile and Gaming Apps
- Content Distrubution

### S3 Infrequent Access

For data is less frequently accessed but requires rapid access when needed
Lower cost then S3 standard
Amazon S3 Standard-Infrequent Access(S3 Standard IA)
- %99.9 availability
- USe Cases:
- - Disaster Recovery
- - Backups

Amazon S3 One Zone - Infrequent Access(One Zone - IA)
- High Durability in a single AZ data loss when AZ is destroyed
- %99.5 Availability
- Use Cases:
- - Storing secondary backups copies of on premise data
- - Or data you can recreate

### S3 Glacier Storage Classes

low cost obj storage meant for archieving/backups
Pricing: Price for obj storage + obj retrieval cost
Amazon S3 Glacier Instant Retrieval
- Milliseconds retrieval, great for data accessed once a quarter
- Minimum storage duration of 90 days

Amazon S3 Glacier Flexible Retrieval(formerly Amazon S3 Glacier)
- Expedited (1 to 5 minutes)
- Standard (3 to 5 hours)
- Bulk (5 to 12 hours)

Amazon S3 Glacier Deep Archive - for long term storage:
- standard(12 hours)
- Bulk (48 hours)
- Minimum storage duration of 180 days

### S3 Intelligence Tiering

Small monthly monitoring and auto tiering fee
Moves objects automatically between Access Ties based on usage
There are no retrieval charges in S3 Intelligen Tiering
Frequently Accessed Tier(automatic): default Tier
Infrequent Accessed Tier(automatic): object not accessed for 30 days
Archive Instant Access Tie(automatic): objects not accesed for 90 days
Archive Access Tier(optional): configurable 90 days to 700+ days
Deep Archive Access Tier(optional): configurable from 180 days to 700+ days

## S3 Encryption

Server-side encrytion(default)
- User uploads file; file encrypted in the bucket

Client Side Encryption
- Encrypts the file before uploading it

## IAM Access Analyzer for S3

Ensures that only intended people have access to your bucket
Example:
- Publicly available bucket
- Bucket that has shared with other aws account

Evaluates S3 bucket policies,S3 ACLs, S3 Access Point Policies
Powered by IAM Access Analyzer

## Shared Responsibility Model for S3

### AWS

Infrastructure(global security, durability, availability, sustain concurrent loss of data in two facilities)
Configurastion and vulnurebilaty analysis
Compliance valdation

### User

S3 Versionning
S3 Bucket Policies
S3 Replication Setup
Logging and monitoring
S3 Storage Classes
Data Encryption at rest and in transit

# AWS Snow Family

Highly secure portable devices to collect and process data at the edge, and migrate into and out of the aws
Data Migration:
- Snowcone
- Snowball Edge
- Snowmobile

Edge Computing
- Snowcone
- Snowball Edge

## Data Migration with AWS Snow Family

Challanges:
- Limited connectivity
- Limited bandwidth
- High Network cost
- Shared Bandwidth
- Connection stability

AWS Snow Family: Offline devices torm data migration and edge computing
If it takes more then 1 week to tranfer data you should use Snowball Devices

## Snowball Edge (for data transfer)

Physical data trasnsport solution move TBs or PBs data in or out of AWS
Alternative to moving data over the network(and paying the network fees)
Pay per data tranfer job
Provide block storage and Amazon S3 Compatible object storage

Snowball Edge Storage Optimized:
- 80 TB of HDD capacity for block volume and S3 compatible object storage

Snowball Edge Compute optimized:
- 42 TB HDD or 28 TB NVMe capacity for block volume and S3 compatible object stotrage

Use Cases:
- Large Cloud Dasta Migration
- DC Decommission
- Disaster Recovery

## AWS Snowcone and Sonwcone SSD

Small, portable Computing anywhere rugged and secure withstands harsh environments.
Light (4.5 pounds, 2.1 kg)
Device used for edge computing, storage and data transfer
Snowcone 8 TB of HDD Storage
Snowcone 14 TB of SSD Storage
Use Snowcone where snowball does not fit the environment
Must provide your own battery and cables
Can be send to AWS offline, or connect it to the internet and use AWS DataSync to send data

## AWS Snowmobile

Transfer exabytes of data(1 EB = 1000 TB)
Each Snowmobile has 100 PB of capacity (use multiple in parallel)
High security: temperature controlled, GPS, 24/7 Video Surveilance
Better then snowball if you transfer more then 10 PB

## Snow Family Usage Process

1. Request Snowball devices from the AWS Console for delivery.
2. Install the Snowball Client / AWS OpsHub on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you are done
5. Data will be loaded in to s3 bucket 
6. Snowball is completaly wiped

## What is Edge Computing

Process data while it's being created on an edge location
- A truck on the road, a ship on the sea, a minnig station underground

These location may have 
- Limited or no internet access
- Limited or no computing Power

We setup a Snowball Edge/Snowcone device to do edge computing
Use Cases Edge Computing:
- Preprocess Data 
- Machine learning at the edge
- Transcoding media streams 

Eventually (if need be) we can ship back the device to AWS(for data transfer)

## Snow Family Edge Computing

Snowcone and Snowcone SSD Smaller
- 2 CPU, 4 GB RAM wired and wireless access 
- USB-C power using a cord or optional batteries

Snowball Edge - Compute Optimized
- 104 vCPU, 416 GiB of RAM
- Optional GPU (video processing, machine learning)
- 28 TB NVMe or 42 TB HDD usable storage
- Storage clustring available (up to 16 nodes)

Snowball Edge Storage Optimized
- Up to 40 vCPU, 80 GiB of RAM, 80 TB of storage

All: can run EC2 Instances and AWS Lambda functions(using AWS IoT Greengrass)
Long term deployment options: 1 and 3 years discounted price

## AWS OpsHub

Historically, to use Snow Family Services, you need a CLI 
Today you can use AWS OpsHub(GUI) to manage your snow family devices
- Unlocking and configuring single or clustered devices
- TYransferring files
- Launching and managing instances running on Snow Family Devices
- Monitor Device Metrics 
- Launch compatible AWS Services on your devices (ex: EC2, AWS DataSync, Network File System(NFS))

## Snowball Edge Pricing

You pay for device usage and data transfer out of AWS 
Data Transfer IN to Amazon S3 is free. 
On-Demand:
- Includes a one time service free per job which includes
- - 10 days of usage for Snowball Edge Storage Optimized 80 TB
- - 15 days of usage for Snowball Edge Storage Optimized 210 TB
- Shipping days are not count
- Pay per day for additional costs

Commited Upfront
- Pay in advance for monthly, 1 year or 3 years
- Up to %62 discount

## Hybrid Cloud for Storage

AWS pushing for hybrid cloud 
- Part of your infrtastructure is on-premises
- Part of your infrastructure is on the cloud 

this can be due to:
- Long cloud migrations 
- Security requirements
- Compliance requirements
- IT Strategy

S3 is proprietary storage technology (unlike EFS/NFS) so how do you expose the s3 data to on premise?
AWS Storage Gateway!

## AWS Storage Cloud Native Options

Block 
- Amazon EBS
- EC2 Instance Store

File
- Amazon Elastic File System

Object 
- Amazon S3 
- Glacier

## Amazon Storage Gateway

Bridge between on-premise data and cloud data in S3
Hybrid storage service to allow on-premnise to seamlessly use the AWS Cloud
Use Cases:
- Disaster Recovery
- Backup and Restore

Types of Storage Gateway
- File Gateway 
- Volume Gateway
- Tape Gateway

## Amazon S3 Summary

Buckets and Objects: global unique name, tied to a region
S3 Security: IAM policies, S3 Bucket policies, S3 encryption
S3 Websites: host a static website on Amazon S3
S3 Versioning: multiple versions for files, prevent accidental deletes
S3 Replication: Same-Region or cross Region, must enable versioning
S3 Storage Classes: Standard, IA, Intelligent Glacier(Instant Flexible Deep)
Snow Family: import data onto S3 through a physical device, edge computing
OpsHub: Desktop application to manage Snow Family Devices
Storage Gateway: Hybrid Solution to extend on-premises storage to S3

# Databases

Storing data on a disk (EFS, EBS, EC2 Instance Store, S3) can have its limits.
Sometimes you want to store data in a database. 
You can structure data in a database.
You build indexes to efficiently query/search through data
You define relatioshps between your datasets
Databases are optimized for a purpose and come with a different features, shapes and constraints

## Relational Databases

Looks like excel sheet with links between them
Can use the SQL language to perform queries and lookups.

## NoSQL Databases 

NoSQL = nonSQL == non relational database
NoSQL databases purpose build for specific data modelsd and have flexible schemas for building modern applications
Benefits:
- Flexibility: easy to evolve data models
- Scalability: Designed to scale out by distrubuted clusters
- High Performance: Optimized for a specific data model
- Highly functional: types optimnized for the data model

Examples: key-value, document, graph, in memory, search databases

## NoSQL Data Example

JSON = Javascript Object Notation
JSON is a common form of data that fits into NoSQL model
Data can be nested
Fields can change over time
Supports new types like Arrays

## Data Bases and SRM on AWS

AWS offers use to manage different databases
Benefits include:
- Quick provisioning, High Availability, Vertical and horizontal scaling
- Automated Backups and restore, Operations and upgrades
- OS patching handled by AWS
- Monitoring and Alerting

Note: Many Database technology could be run on EC2, but you must handle yourself the resillience, backups, patching, high availability, fault tolerance, scaling.

## Amazon RDS Overwiev

RDS stands for relational database service
It's managed DB service for DB use SQL query language
It allows you to create databases inb the cloud that are managed by AWS
- PostgreSQL
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- IBM DB2
- Aurora(AWS Proprietary Database)

## Advantages of using RDS instead of DB on EC2

RDS is managed service:
- Automated provisioning
- Continous backups, Restore to a specific timestamp(Point in time Restore!)
- Monitoring Dashboards
- Read replicas for improved read performance
- Multi AZ setup for disaster recovery
- Scaling capability(vertical and horizontal)
- Storage backed by EBS

But you can't SSH to your instances

### Amazon Aurora

Aurora is a proprietary database technology from AWS
PostgreSQL and MySQL both supported
Aurora is AWS Clud Optimized and claims 5x performance improvement over MySQL RDS, over 3x more performance then PostgreSQL RDS.
Aurora storage automatically grows in increments of 10 GB, up to 128 TB.
Aurora cost more then RDS (%20 more) - but it's much more efficient
Not in the free tier

### Amazon Aurora Serverless

Automate database instantiation and auto scaling based on actual usage.
PostgreSQL and MySQL both supported
No capacity planning needed.
Least management overhead
Pay per second, can be more cost effective
Use cases: Good for infrequent intermittent or unpredictable workloads

### RDS Deployments

Read Replicas:
- Scale the read workloads of your DB.
- Can create up to 15 read replicas
- Data is only written to the main DB

Multi AZ
- Failover in case of AZ outage(high availability)
- Data is onlly read / written to the main DB
- Can have 1 other AZ as a failover

Multi Region(Read Replicas)
- Disaster Recovery in case of region issue
- Local performance for global needs
- Replication costs

### ElastiCache

Elasticache is to get manmaged by Redis or Memcache
Caches are in-memory databases with high performance, low latency
Helps reduce load of databases for read intensive workloads
AWS takes care of OS maintenance, patching, optimization setup configurtation, monitoring, failure recovery.

### Dynamo DB

Fully managed highly available with replication across 3 AZ
NoSQL database - not a relational database
Scales to massive workloads, distributed serverless database
Millions of requests per second, trillions of row, 100s of TB storage
Fast and consistent in performance
Single-digit millisecond latency - low latency retrieval
Integrated with IAM for security, authorization and administration
Low cost and auto scaling capabilities
Standard and Infrequent Access(IA) Table class

### DynamoDB Type of Data 

DynamoDB is a key value database
There is primary keys and atributes
Schema defined for each item

### DynamoDB Accelerator

Fully managed in-memory cache for DynamoDB
Caches most frequently accessed data in memory
10x increased performance microseconds latency
Secure, highly available, and highly scalable
Difference in between ElastiCache is DAX integrated into DynamoDB, in other hand ElastiCache can be used for other DBs

It's a serverless service you start with creating a table not a database
Every item has its own schema very flexible database
All data lives in one giant table there is noı join with other tables 

### DynamoDB Global Tables

Make a Dynamo DB table accesible with low latency in multiple regions
Active-Active replication (read/write to any AWS region) - 2 way replica

### Redshift

Redshift is based on PostgreSQL, but it's not used for OLTP(Online Transaction Processing)
It's OLAP - online analytical processing(analytics and data warehousing)
Load data once every hour not every second
10x better performance then other data warehouses, scale PBs of Data
Columnar storage of data(instead of rows)
Massively parallel query execution(MPP), highly available
Pay as you go based on the instances provided
Has a SQL interrface for performing queries
You can integrate BI tools such as AWS Quicksight or Tableau

### Redshift Serverless

Automatically provisions and scales data warehouse underlying capacity
Run analytics workloads without provisioning underlying infrastructure
Pay only what you use (save costs)
Cost efficient then standard
UseCases: Reporting, dashboarding applications, real time analytics

### Amazon EMR

EMR stands for Elastic MapReduce
EMR helps creating Hadoop clusters(Big Data) to analyze and process vast amount of data 
The Clusters can be made of 100s of EC2 instances
Also supports Apache Spark, Hbase, Presta, Flink
EMR takes care of all provisioning and configuration
Auto scaling and integrated with spot instances 
Use cases: Data processing, machine learning, Web indexing

### Amazon Athena

Serverless query service to perform analytics against S3 objects
Uses standard SQL language to query files
Supports CSV, JSON, ORC, Avro, and parquet(built on Presto)
Pricing is 5$ per TB data scanned
Use compressed or columnar data for cost savings
Use Cases:
- BI
- Analytics
- Reporting
- Analyze and Query VPC flowlogs
- Analyze ELB logs

## Exam Tip: Analyze data in S3 using serverless SQL, use Athena

### Amazon Quicksight

Serverless machine learning powered BI service to create interactive dashboards
Fast automatically scalable embeddable with per session pricibg
Use Cases:
- Business Analytics
- Building Visualizations
- Perfgorm ad-hoc analysis
- Get business insişghts using data 

Integrated with RDS, Aurora, Athena, Redshift, S3...

### DocumentDB

Aurora is an AWS implemantation of MySQL/PopstgreSQL
Document DB is the same forMongDB(NoSQL)
MongoDB used to store, query and index JSON data
Smimlar deployment concepr as Aurora
Fully managed highly available with replication across 3 AZ
DocumentDB storage automatically grows in increments of 10 GB 
Automatically scales to workloads with millions of requests per seconds

### Amazon Neptune 

Fully managed graph database
A popular graph datasaet would be a social network
- Users have friends
- Posts have comments
- Comments have likes from users
- Users share and like posts

Highly available across 3 AZ, with up to 15 replicas
Build and run applications working with highly connected datasets
Great for knowlerdge graphs(wikipedia), fraud detection, recommandation engine, social networking

### Amazon Timestream 

Fully managed, fast, scalable, serverless time series database
Automatically scales up and down to adjust capacity
Store and analyze trillions of events per day
1000s times faster and 1/10th the cost Relational Databases
Built in time series analytics functions(helps you identify patterns in your data in real time)

### Amazon Quantum Ledger Database

QLDB is an abroviation for Quantum Ledger Database
A ledger is a book recording finasncial transactions
Fully managed, Serverless, Highly Available, Replications across 3 AZ
Used to review history of all the changes made to your application data over time
Immutable system: no entry can be removed or change over time
Cryptyographically verified
Better performance then common ledger block-chain frameworks, manipulate data using SQL
Difference with Amazon Block Chain: no decentralization over data 
In accordance with financial regulations

### Amazon Managed BlockChain

Blockchain makes it possible to build applications where multiple parties can execute transactions without the need for a trusted, central authority
Amazon Managed Blockchain Service can:
- Join public blockchain Networks
- Or create your own scalable private network

Compatible with frameworks Hyperledger Public and Etherium

### AWS Glue

Managed ETL service
Easily create Extract, Transform and Load pipelines
USefull to prepare and transform data for analytics
Fully serverless service

### DMS - Database Migration Service

Quickly and securely migrate your databases to AWS
Its resillient and self healing
The source remain available during the data transfer
Supports:
- Homogeneous Migrations: Oracle to Oracle
- Heterogeneous Migrations: Microsoft to Aurora

## Databases adn Analytics Summary

RDS(Relational Databse Servbice)'es are good in OLTP(Online Transaction Processing)
There does exist some differences between fo0llowing concepts: Multi AZ, Read Replicas, Multi Region
ElastiCache: Inmemory Database
DynamoDB is a serverless key/value database
There is a cache for DynamoDB it's called DAX(DynamoDB Accelerator)
Redshift is an online Data Warehouse(SQL)(OLAP - Online Analytical Processing NOT OLTP - Online Transaction Processing)
EMR manages Hadoop Clusters
Athena: Query data on Amazon S3(Uses SQL with serverless fashion)
QuickSight: BI service for creating dashboards for data.(Serverless)
DocumentDB: Aurora for MongoDB(JSON - NoSQL)
Amazon QLDB stands for Quantum Ledger Database. It's a Financial Transaction Ledger(immutable, cryptographically verified)
Amazon Managed Block Chain: Managed Hyperledger Fabric and Etherium Blockchains
Glue: Managed ETL and Data Catalog Service
DMS: Database Migration Service 
Timestream: Time series Database

# Deployment and Function as a Service

### What is a Docker Container

Docker is a software development platform to deploy applications.
Apps are packaged in containers that can be run any OS
Apps run the same regardless of where they run
- Any machine
- No compatibility Issues
- Predictable behaviour
- less work
- Easier to maintain and deploy 
- Works with any language, any OS

Scale containers up and down very quickly
Docker images are stored in Docker Repositories
Public: DockerHUB
- Find base images for many techgnologies and OS
- Ubuntu, MySQL, NodeJS

Private: Amazon ECR(Elastic Container Registery)

### Docker vs VM

Docker is a virtualization technology
Resources are shared with the host (many containers on one server)

## ECS(Elastic Container Service)

Launch Docker Containers on AWS
You must provision and maintain the infrastructure(EC2 instances)
AWS takes care of starting and stopping the containers
Has integration with thye Application Load Balancer

## Fargate

Launch Docker Containers on AWS
You don't provision the infrastructure
It's simpler then ECS
It is serverless
AWS just run the containers based on the CPU and RAM you need

## ECR

Stands for Elastic Container Registery
Private Docker Registery on AWS
This is where you store your docker images so they can run on ECS or Fargate

### Serverless

Serverless is a new paradigm in which the developers don't have to manage the servers anymore
They just deploy the code
They just deploy the functions
Initially Serverless == FaaS(Function as a Service)
Serverless pioneered by AWS Lambda but now also includes anything that managed "Databases, messaging Storage"
Serverless does not mean there is no servers
It means that you don't provision and manage or even see them

### Why AWS Lambda

#### EC2

Virtual servers in the cloud 
Limited by thge RAM and CPU
Continously running
Scaling means intervention to add or remove servers

#### Lambda

Virtual Servers no servers to manage 
Limited by time - short executions 
Run on-demand
Scaling is automated

### Benefits of AWS Lambda

Easy pricing:
- Pay per rquest and comnpute time
- Free tier of 1 000 000 lambda requests and 400 000 GB's of compute time

Integrated with whole AWS suite
Event Driven: Functions invoked when needed.
Integrated with many programming languages
Easy monitoring through AWS CloudWatch
Easy to get more resources for functions(Up to 10 GB of RAM)
Increasing RAM will also improve CPU and Networking

### Lambda Language Support 

NodeJS
Python
Java
C#
Go
Ruby
Lambda Container Image: 
- The container image must implement the Lambda Runtime API
- ECS/Fargate is preffered for running arbitrary Docker Images

Use Case:
- You can create a thumbnail and metadata in DB with an event trigger like saving a photograph
- You can run CRON jobs periodically

### Lambda Pricing

Pay per calls:
- First 1000000 requests are free
- 0.20$ per 1 million requests there after

Pay per duration:
- 400 000 GB-second of compute time per month is free
- == 400 000 GBs if function is 1 GB RAM 
- == 3200000 GBs if function is 128 MB RAM
- After that $1.00 for 600000 GBs

It is usually very cheap to run lambda so it's very popular

## Amazon API Gateway

Example: Building a serverless API
Fully managed service for developers to easily create, publish, maintain, monitor and secure API'S
Serverless and scalable
Supports RESTfull APIs and WebSocket API's
Support for security user authentication, API throtling API keys

## AWS Batch

Fully managed batch processing at any scale
Efficiently run 100000s of computing batch jobs on AWS
A batch job is a job that has a start and end point(opposed to continous)
Batch will dynamically launch EC2 or Spot instances
AWS Batch provisions right amount of compute memory
You submit or schedule and AWS does the rest 
Batch jobs are defined as Docker images and run on ECS
Helpfull for cost optimizations and focusing less on the infrastructure

### Batch vs Lambda

#### Lambda

Time limit
limited runtime
Limited and temporary disk space
Serverless

#### Batch

No time limit
Any runtime as l0ng as its packaged as a Docker Image
Rely on EBS / instance store for disk storage
Relies on EC2 can be managed by console

## Amazon LightSail

Virtual servers, storage, databases and networking
Low and predictable pricing
Its a simpler alternative to other AWS services
Great for people with less cloud cloud experience
Can setup notifications and monitoring of your lightSail resources
Use Cases:
- Simple Web Applications(has templates for LAMP, Nginx, MEAN, Nodejs)
- WEbsites (Templates for Wordpress, Magenta, Plesk)
- Dev/TEst environments

Has high availability but no auto scaling

### Other Compute Summary 

Docker: Container technology to run applications
ECS: run Docker containers on EC2 instances 
Fargate: 
- Run Docker containers without provisioning infrastructure
- Serverless offering

ECR: Private Docker Images Registery
Batch: run Batch Jobs on managed EC2 instances
Lightsail: Predictable, low pricing for simple apps and database stacks

### Lambda Summary 

Lambda is a Function as a Service, serverless, seamless scaling, reactive
Lambda Billing:
- By the time run X by the RAM provisioned
- By the number of invocations

Supports many programming language
Invocation time up to 15 minutes
API Gateway: Expose Lambda functions as a HTTP API.

# Deploying And Monitoring Infrastructure

## CloudFormation

Cloudformation isd a declerative way of outlining your AWS infrastructure, for any resources(most of them are supprted)
For example with Cloudformation Template:
- I want a security group
- I want a S3 bucket
- I want a Load Balancer(ALB) in front of these machines

Then Cloudformation create those resources for you, in the right order, with the exact configuration you specify

### Benefits of Cloudformation

Infrastructure as Code:
- No resources are monually created
- Changes to the infrastructure reviewed through code

Cost:
- Each resources within the stack is tagged with an identifier so you can easily see how much a stack costs you
- You can estimate the costs of your resources using the Cloudformation Template
- Savings Strategy: In development you can automatically delete and recreate templates

Productivity: 
- Ability to destroy and recreate infrastructure on the fly
- Automated generation of Diagram for your template
- Declerative Programming(no need to figure out ordering and orchestration)

Don't re-invent the wheel:
- Leverage existing templates on the web
- Leverage the documentation

Supports almost all AWS resources:
- Every technology that exist in this document is supported
- You can use "custom resources" for resources that are not supported

We can see all the resources
We can see the realations between the components

## AWS Cloud Development Kit(CDK)

Define your cloud infrastructure using a programming language
supports:
- Python
- Java
- Javascript
- C#

The code compiled to a Cloudformation Template(JSON/YAML)
You can therefore deploy your infrastructure application runtime together
- Great for Lambda Functions
- Great for Docker Containers in ECS/EKS

### Developer Problems on AWS

Managing Infrastructure
Deploying Code
Configuring Database, Loud Balancers etc.
Scaling Concerns
Most of Web Apps have the same architecture (ALB + ASG)
All the developers want is fıor their code is to run
Possibly consistently across different apps and environments

## AWS Elastic Beanstalk

Elastic Beanstalk is a developer centric way of deploying an application
It uses components:
- EC2
- ELB
- RDS
- ASG

But it's all in one view easy to make sense of
We still havbe full control over the configuration
Beanstalk == Platform as a Service(PaaS)
Beanstalk is free you only pay for underlying resources
Managed Service:
- Instance configuration and OS handled by AWS
- Deployment Strategy is configurable but performed by Elastic Beanstalk
- Capacity provisioning
- Load Balancing and Auto Scaling
- Application Health - monitoring and responsiveness

Just the application code is the responsibility
Three architecture Model:
- Single instance deployment: Good for Dev
- ALB + ASG: Great for production or pre-production web applications
- ASG only: great for non-web applkications in production(workers etc)

Supports many platform:
- Go
- Java Tomcat
- NodeJS
- PHP
- Python
- Package Builder
- Single Container Docker
- Multi Container Docker
- Pre-configured Docker

### Beanstalk - Health Monitoring

Health agent pushes metrics to CloudWatch
Checks for app health, publishes health events

## AWS Code Deploy 

We want to deploy our application automatically 
Works with EC2 instances
Works with on-premises servers
Hybrid service
Servers / Instances must be provisioned and configured ahead of time with the CodeDeploy Agent

## AWS Code Commit 

Before pushing the code to servers it needs to store somewhere
Dev's store code using Git
Github is a famous public offering, CodeCommit is the competing product of AWS
Code commit:
- Source control service that hosts Git-based repos
- Makes it easy to collabrate other on code
- The code changes are automatically versioned

Benefits:
- Fully managed
- Scalable and highly available 
- Private, secure, Integrated with AWS

## AWS CodeBuild

Code building service in the cloud
Compiles source code, run tests and produces a packege that ready to deploy
Benefits:
- Fully managed, Serverless
- Continously scaling and highly available
- Secure
- Pay as you go - only paid for build time

## AWS CodePipeline

Orchestrate the different steps to have the code automatically pushed to production
- Code -> Build -> Test -> Provision -> Deploy
- Basis for CI/CD

Benefits:
- Fully managed compatible with CodeCommit, CodeBuild, CodeDeploy, Beanstalk, Github, 3rd Parties etc
- Fast delivery, rapid updates

## AWS CodeArtifact

Software packages often depends on each other to build(often called dependencies) and new ones are created
Storing and retrieving these dependecies is called artifact management 
Traditionally you need to setup your own artifact management system
CodeArtifact is a secure, scalable and cost-effective way of artifact management for software development 
Works with common dependency management softwares such as Maven, Gradle, npm, yarn, pip, etc.
Developers and CodeBuild can then retrieve dependencies straight from CodeArtifact 

## AWS Cloud9

AWS Cloud9 is a Cloud IDE(Integrated Development Environment) for writing running and debugging the code
Classic IDE downloaded on a computer before being used
AWS Cloud9 also allows you to collabration in real-time(pair programming)

## AWS System Manager(SSM)

Helps you manage your EC2 and On-Premises systems at scale
Another Hybrid AWS Service
Get operational insights about the state of your infrastructure
Suite of 10+ products
Most important features are:
- Patching automation for enhanced compliance 
- Run commands across an entire fleet of servers
- Store parameter configuration with the SSM Parameter Store

Works for Linux, Windows, MacOS and RsberryPi OS(Raspbian)

### How System Manager(SSM) Works

We needf to install SSM Agent onto the systems we control
Installed by default on Amazon Linux AMI and some Ubuntu AMI
If an instance can't be controlled with SSM, it is probably an issue with SSM Agent
Thanks to the SSM Agent we can run commands, patch and configure our servers

### SSM Session Manager

Allows you to start SSH on your EC2 and on-premises servers
No SSH access, bastion hosts, or SSH keys needed
No Port 22 needed(Better security)
Supporets Linux, MacOS, Windows
Send session log data to S3 or CloudWatch logs
You need to assign SSM Core Access Role to your EC2 instance

For SSH you need:
- A key pair SSH access on port 22 for manual connection
- You can use EC2 connect without a key but you still need port 22 opened
- With SSM SessionMAnager you can start SSH Connection without a key with closed port 22

### SSM Parameter Store

Secure storage for configuration and secrets
API keys, passwords, configurations
Serverless, scalable, durable, easy SDK
Control access permissions via IAM
Version Tracking and encryption(optional)

### Deployment Summary

CloudFormation(AWS only):
- Infrastructure as Code, works with almost all AWS resources
- Repeat across Regions and accounts

Beanstalk(AWS only):
- Platform as a Service(PaaS), Limited to certain programming languages and Docker
- Deploy code consistently with a known architecture(ex ALB + EC2 + RDS)

CodeDeploy(Hybrid):
- Deploy and upgrade any application on servers

System Manager:
- Patch, configure and run commands at scale

### Developer Services Summary

CodeCommit: Private Repositories in AWS
CodeBuild: Build and Test Code in AWS
CodeDeploy: Deploy Code onto servers
CodePipeline: Orchestration of Pipeline(CI/CD)
CodeArtifact: Store software packages/dependencies on AWS
CodeStar: Unified view for developers to do CI/CD
Cloud9: CloudIDE with collab
AWS CDK: Define your infrastructure using a programming language.

# Global Infrastructure

A global application is an application deployed in multiple geographies
On AWS this could be Regions or Edge Locations
Decreased Latency:
- Latency is the time it takes for a network packet to reach a server
- It takes time for a packet from Asia to reach the US
- Deploy your application closer to your users to decrease latency, better experience

Disaster Recovery:
- If an AWS region goes down(earthquake, Storm, Power shutdown, etc)
- You can failover to another region and have your application still working
- A Disaster Recovery Plan is important to increase availability at your application

Attack Protection
- Distrubuted global infrastructure is harder to attack

### Global AWS Infrastructure

Regions: For deploying application and infrastructure
Availability Zone: Made of multiple data centers
Edge Locations(Point of Presence): For content delivery as close as possible to users

### Global Applications in AWS

Global DNS: Route 53
- Great to route users to the closest deployment with least latency
- Great for disaster recovery strategies

Global Content Delivery Network(CDN): CloudFront
- Replicate part of your applications in an edge location - decrease latency
- Cache common requests - improved user experience and decrease latency

S3 Transfer Acceleration
- Accelerate global uploads and downloads into Amazon S3

AWS Global Accelerator
- Improve global application availability and performance using AWS global network 

## Amazon Route53

Route53 is a managed DNS(Domain Name Server)
DNS is a collection of rules on records which helps clients understand how to reach a server through URL
In AWS most commnon records are:
- www.google.com -> 12.34.56.78 == A record(IPv4)
- IPv6
- CNAME: hostname to hostname
- Alias

## AWS CloudFront

Content Delivery Network(CDN)
Improves read performance, content is cached at the edge locations
Improves User Experience
216 Point of Presence globally(Edge Locations)
DDoS Protection(because worldwide): Integration with Shield, AWS Web application Firewall

### CloudFront Origins

S3 Bucket:
- For distrubuting files and storing them in the edge locations
- Enhanced security with CloudFront Origin Access Control(OAC)
- OAC is replacing Origin Access Identity(OAI)
- Cloudfront cache is used as an ingress(to upload files to S3)

Custom Origin(HTTP):
- Applicaiton Load Balancer
- EC2 Instance
- S3 Web Site
- Any HTTP backend you want

### CloudFront vs S3 Cross Region Replication 

CloudFront:
- Global Edge Network
- Files are cached for a TTL(maybe a day)
- Great for static content that must be available everywhere

S3 Cross Region Replication
- Must be setup for each region you want replication to happen
- Files are uploaded in near real-time
- Read only
- Great for dynamic content that needs to be available at low-latency in few regions

## S3 Transfer acceleration

Increase transfer speed by transferring file to an AWS edge location 
Which will forward the data to S3 bucket in target region through AWS private network.

## AWS Global Accelerator

Improve global application availability and performance using the AWS Global Network
Leverage the AWS internal network to optimize the route to your application
2 Anycast IP are created for your application and traffic sent through edge locations
The Edge Locations: Send the traffic to your application

### Global Acclerator vs CloudFront

They both use the AWS global network and its edge lopcations around the world
Both services integrated with AWS Shield for DDoS protection

CloudFront(Content Delivery Network)
- Improves performance for your cacheable content(such as images and videos)
- Content is served at the edge

Global Accelerator:
- No caching, proxiying packets at the edge to applications running in one or more AWS regions
- Improves performance for as wide range of applications over TCP or UDP
- Good for HTTP use cases that require static IP address
- Good for HTTP use cases that required deterministic, fast regional failover

## AWS Outposts

Hybrid Cloud: Bussinesses that keep an on-premises infrastructure alongside a cloud infrastructure
Therefore two ways of dealing with IT systems:
- One for the AWS Cloud (using AWS Console, CLI, SDK)
- One for their on-premises infrastructure

AWS Outposts are server racks that offers the same AWS Infrastructure,
Services APIs and tools to build your own applications on-premises just as in the cloud
AWS will setup and manage "Outposts Racks" within your on-premises infrastructure and you can start leveraging AWS services on-premises

You are responsible for the Outpost Racks physical security

Benefits:
- Low-latency across the on-premises servers
- Local data processing
- Data residency
- Easier Migration from on-premises to the cloud 
- Fully managed service

Some services that works on Outposts:
- EC2 (Elastic Compute Cloud)
- EBS (Elastic Block Store)
- S3 (Simple Storage Service)
- EKS (Elastic Kubernetes Service)
- ECS (Elastic Container Service)
- RDS (Relational Database Service)
- EMR (Elastic MapReduce)

## AWS WaweLength

WaweLength zones are infrastructure deployments embedded within the telecommunication providers datacenters at the edge of the 5G Networks
Brings AWS services top the edge of the 5G Networks
Example: EC2, EBS, VPC, ...
Ultra low-latency applications through 5G networks
Traffic doesn't leave the Communication Service Provider'S(CSP) network
High bandwidth and secure connection to the parent AWS Region
No additional charges and service agreements

Use Cases:
- Smart Cities
- ML-assisted diagnostics
- Connected Vehicles
- Interactive Live Video Streams
- AR/VR
- Real-Time Gaming

## AWS Local Zones

Places AWS compute, storage, database and other selected AWS services closer to end users to run latency-sensitive applications.
Extends your VPC to more locations - "Extension of an AWS Region"
Compatible with EC2, RDS, ECS, EBS, ElastiCache, Direct Connect, ...
Example:
- AWS Region: N. Virginia(us-east-1)
- AWS Local Zones: Boston, Chicago, Dallas, Houston, Miami, ...

### Global Application Architecture 

Single Region, Single AZ 
- No High Availability
- High Global Latency
- Very easy to build

Single Region, Multi AZ
- High Availability exists
- High Global Latency
- Easy to build

Multi Region, Active - Passive
- Good Global Read Latency
- Bad Global Write Latency
- Difficulty: Medium

Multi Region, Active - Active
- Good Write Latency
- Good Read Latency
- Difficulty: Hard

### Global Applications in AWS - Summary

Global DNS(Domain Name Server): Route 53
- Great to route users to the closest deployment with least latency
- Great for disaster recovery strategies

Global Content Delivery Network(CDN): CloudFront
- Replicate part of your applications to AWS Edge Locations - decrease latency
- Cache Common Requests - improved user experience and decreased latency

S3 Tranfer Accelerator
- Accelerate global uploads and downloads into Amazon S3 using Edge locations

AWS Global Accelerator
- Improve global application availability and performance using the AWS global network

AWS Outposts
- Deploy Outpost Racks in your own Data Center to extend AWS Services

AWS WaveLength
- Brings AWS Serices to the edge of the 5G Network
- Ultra low-latency applications

AWS Local Zones
- Bring AWS resources(compute, database, storage) closer to your users
- Good for latency sensitive applications

# Cloud Integrations

## Introduction

When we start deploying multiple applications they will inevitably communicate with one another
There are two patterns of communication 
1. Synchronous Communications(application to application)
2. Asynchronous Communications / Event Based (application to queue to applicaiton)

Synchronous communication between applicaitons can be problematic if there are sudden spikes of traffic
What if you need to suddenly encode 1000 videos but usually it's 10?
In that case it is better to decouple your application
- Using SQS: queue model
- using SNS: pub/sub model
- using Kinesis: real-time data streaming model 

These services can scale independently from our application.

## Amazon SQS (Simple Queue Service)

Oldest AWS offering (over 10 years)
Fully managed service(serverless), use to decouple applications
Scales from 1 message per second to 10000s per second
Default retention of messages: 4 days, maximum of 14 days
Messages are deleted after they're read by consumers
Low-Latency (<10 ms on publish and receive)
Consumers share the work to read messages and scale horizontally

## Amazon SQS - FIFO Queue

FIFO = First In First Out (ordering of messages in the queue)
Messages are processed in order by the consumer 

## Amazon Kinesis

Kinesis = real-time big data streaming 
Manbaged service to collect, process and analyze real-time streaming data at any scale
Types of Kinesis:
- Kinesis Data Streams: low-latency streaming to ingest data at scale from thousands of resources
- Kinesis Data FireHouse: Load streams into S3, RedShift, ElasticSearch, etc...
- Kinesis Data Analytics: Perform real-time analytics on streams using SQL
- Kinesis Video Streams: Monitor Real-Time video streams for analytics and ML

## Amazon SNS(Simple Notification Service)

The "event publishers" only sends message to one SNS topic 
As many "event subscribers" as we want to listen to the SNS topic notifications
Each subscriber to the topic will get all the messages 
Up to 12 500 000 subscriptions per topic, 100000 topics limit

## Amazon MQ

SQS, SNS are cloud native services proprietary protocols from AWS
Traditional applications running from on-premises servers may use open protocals such as: MQTT, AMQP, STOMP, Openwire, WSS
When migrating to the cloud, instead of re-engineering the applications to use SQS, SNS we can use Amazon MQ
Amazon MQ is a managed message broker service for RabbitMQ and ActiveMQ
Amazon MQ doesn't scale as much as SQS / SNS
Amazon MQ runs on servers, can run on Multi AZ with Failover
Amazon MQ has both queue feature (SQS) and topic features (SNS)

## Integration Section - Summary

SQS:
- Queue service in AWS 
- Multiple producers, messages kept up to 14 days 
- Multiple consumers share the read and delete messages when done
- Used to decouple applications in AWS 

SNS:
- Notiffication Service in AWS
- Subscribers: Email, Lambda, SQS, HTTP, Mobile, ...
- Multiple Subscribers, send all messages all of them 
- No message retention 

Kinesis:
- Real-time data streaming, persistence, and analysis

Amazon MQ
- Managed message broker for ActiveMQ and RabbitMQ in the cloud (MQTT, AMQP protocols)

# Cloud Monitoring 

## Amazon CloudWatch Metrics

CloudWatch provides metrics for every service in AWS
Metric is a variable to monitor(CPU Utilization, NetworkIN, ...)
Can create cloudWatch Dashboards from metrics

### Important Metrics

EC2 Metrics: CPU Utilization, Status Checks, Network(not RAM)
- Default metrics every 5 minutes
- Option for detailed monitoring($$$): Metrics every 1 minute

EBS Volumes:
- Disk Read/Write

S3 Buckets:
- Bucket size Bytes
- Number of Objects 
- All Requests

Billing:
- Total Estimated Charge

Service Limits:
- How much you've been using a service API

Custom Metrics:
- Push your own metrics

## Amazon CloudWatch Alarms

Alarms used to trigger notifications for any metric
Alarm Action:
- Auto Scaling: increase or decrease EC2 instances
- EC2 actions: stop, terminate, reboot, recover an EC2 instance
- SNS notifications: send a nbotification into an SNS Topic

Various Options(sampling, %, max, min, etc...)
Can choose the period on which to evaluate an alarm
Examnple: Create a billing alarm on the CloudWatch Billingt metric
Alarm States:
- OK
- INSUFFICIENT_DATA
- ALARM 

## Amazon CloudWatch Logs

CloudWatch logs can collect logs from:
- Elastic Beanstalk: collection of logs from application
- ECS: collection from containers
- AWS Lambda: collection from function logs
- CloudTrail based on filter
- CloudWatch Log Agents: on EC2 machgines or on-premises servers
- Route 53: Log DNS queries

Enables real-time monitoring of logs
Adjustable CloudWatch logs retention

### CloudWatch Logs for EC2

By default no logs from your EC2 instance will go to CloudWatch
You need to run a CloudWatch Agent on EC2 to push the log files you want
Make sure IAM permissions are correct
The CloudWatch Log Agent can be setup on-premises too.

## Amazon EventBridge

Use Cases: 
- Schedule CRON Jobs
- Event Pattern: Event rules to react to a service doing something
- Trigger Lambda functions, send SNS/SQS messages

There are 3 types of Event Bus:
- Default Event Bus: Takes events from AWS resources
- Partner Event Bus: Can take events from AWS partners(Zendesk, DataDog)
- Custom Event Bus: You can configure your custom application to trigger an event

Schema Registery: MÖodel event schema
You can archive events (all/filter) sent to an event bus (indefinitely or set period)
Ability to replay archived events

## AWS CloudTrail

Provides governance, compliance, and audit for your AWS account
CloudTrail is enabled by default 
Get an history of events/API calls made within your AWS account by:
- Console
- CLI
- SDK
- AWS Services

Can put logs from CloudTrail into CloudWatch Logs or S3
A Trail can be applied to all regions (default) or a single region

If a resource is deleted look at CloudTrail first!

## AWS X-Ray

Debugging in production, good old way:
- Test locally
- Add log statements everywhere
- Re-Deploy in production

Log format differs across applications and log analysis is hard
Debugging: One big monolith is easy, distrubuted services hard
No common views of your entire architecture

X-RAY gives a Visual Analysis of all your architecture

AWS X-Ray Advantages:
- Troubleshooting performance (bottlenecks)
- Understand dependencies in a microservice architecture
- Pinpoint service issues
- Review request behaviour
- Find errors and exceptions
- Are we meeting time SLA?
- Where i am throttled?
- Identify users that are impacted

## Amazon CodeGuru

An ML powered service fgor automated code reviews and application performance recommendations
Provides two functionalities:
- CodeGuru Reviewer: Automated Code Reviewsfor staticv code analysis
- CodeGuru Profiler: Visibility/Recommendations about application performance during runtime(production)

### Amazon CodeGru Reviewer

Identify criticall issues, security vulnurabilities and hard to find bugs
Example: common coding best practices, resource leaks, security detection input validations
Uese ML and automated reasoning
Hard learned lessons across millions of code reviews on 1000s of open source and Amazon Repositories
Supports Java and Python
Integrates with Github, Bitbucket and AWS CodeCommit

### Amazon Code Gure Profiler

Helps understand runtimne behaviour of your application 
Example: Identify if your application is consuming excessive CPU capacity on a logging routine
Features:
- Identify and remove code inefficiencies
- Improve application performance(e.g. reduce CPU Utilization)
- Decrease compute costs
- Provides Heap Summary(identify which object using up memory)
- Anomaly Detection

Supports applications running on AWS or on-premise
Minimal overhead on application

## AWS Health Dashboard

Shows all regions, all services health 
Shows historical information for each day 
Has an RSS feed you can subscribe to 
Previously called AWS Service Health Dashboard

## AWS Account Health Dashboard

Previously called AWS Personal Health Dashboard(PHD)
AWS Account Health Dashboard alerts and remediation guidance when AWS experiencing events that may impact you 
While Service Health Dashboard display general status of AWS services, Account Health Dashboard gives you a personalized view into the performance and availability of AWS services underlying your AWS resources
The dashboard displays relevant anbd timely information to help you manage events in progress and provides proactive notifications to help you plan for scheduled activities
Can aggregate data from an entire AWS Organization 
Global Service 
Shows how AWS outages directly impact you and your AWS resources
Alert, remedition, proactive, scheduled activities

## Cloud Monbitoring - Summary

CloudWatch:
- Metrics: Monitor the performance of AWS Services and billing metrics
- Alarms: Automate notifications, perform EC2 action, notify to SNS based on metric
- Logs: Collect log files from EC2 instances, servers, lambda functions...

EventBridge:
- React to events in AWS, or trigger a rule on a schedule

CloudTrail:
- Audit API calls made within your AWS Account 

CloudTrail Insights
- Automated Analysis of your CloudTrail Events

X-Ray:
- Trace requests made through your distrubuted application 

AWS Health Dashboard:ü
- Status of all AWS Services across all regions 

AWS Account Health Dashboards
- AWS events that impact your infrastructure 

Amazon CodeGuru:
- Automated code reviews and application performance recommendations

# VPC and Networking

## VPC

At the AWS CCP Level you should know about:
- VPC, Subnets, Internet Gateway and NAT Gateways
- Security Groups, Network ACL(NACL), VPC Flow Logs
- VPC Peering, VPC Endpoints
- Site to Site VPN and Direct Connection(DX)
- Transit Gateway

## IP Addresses in AWS

IPv4 - Internet Protocol Version 4(4.3 Billion Addresses)
- Public IPv4 - Can be used on the internet 
- EC2 instances gets a new public IP address every time you stop it then start it again(default)
- Private IPv4 - Can be used on private networks such as Local Area Network(LAN) or internal AWS network(e.g. 192.168.1.1)
- Private IPv4 is fixed for EC2 instances even if you start/stop them

ElasticIP - allows you to attach a fixed public IPv4 address to EC2 instance
Note: All public IPv4 addresses on AWS will be charged $0.005 per hour(including EIP)
- Free Tier: 750 hours usage per month 

IPv6 - Internet Protocol Version 6(3.4 x 10^38 Addresses)
- Every IP address is public in AWS(no private range)
- IPv6 is FREE!

## VPC and Subnets Primer 

VPC - Virtual Private Cloud: Private Network to deploy your resources(regional resources)
Subnets: allow you to partition your network inside your VPC (AZ resource)
A public subnet is a subnet that is accesible from the internet
A private subnet is a subnet that is not accesible from the internet 
To define access to the internet and between subnets, we use Route Tables 

## Internet Gateways and NAT Gateways

Internet Gateways helps our VPC instances connect with the internet 
Public Subnets have a route to the internet gateways
NAT Gateways(AWS managed) and NAT Instances(self managed) allow your instances in your private subnets to access the internet while remaining private 

## Network ACL(NACL) and Security Groups

NACL: 
- A firewall that control traffic from and to subnet 
- Can have allow and deny rules
- Are attached at subnet level
- Rules only include IP addresses 

Security Groups:
- A firewall that controls traffic to and from ENI/an EC2 Instance 
- Can have only allow rule
- Rules include IP addressesand other security groups 

## NACL vs Security Groups

### Security Group

Operates at the instance level
Supports allow rule only
Is Stateful: Return traffic is automatically allowed regardles of any rules 
We evaluate all rules before deciding whether to allow traffic
Applies to an instance only if someone specifies the security group when launching the instance or associates the security group with instance later on

### NACL(Network Access Control List)

Operates at the subnet level
Supports allow rules and deny rules
Is Stateless: Return traffic must be explicitly allowed by rules
We process rules in number order when deciding whether to allow traffic
Automatically applies to all instances in the subnets it's associated with(therefore you don't have to rely on users to specify the security group)

## VPC Flow Logs

Capture information about IP traffic going into you interfaces:
- VPC Flow Logs
- Subnet Flow Logs
- Elastic Network Interface(ENI) Flow Logs

Helps to monitor and troubleshoot connectivity issues
Example: 
- Subnets to Internet
- Subnets to Subnets
- Internet to Subnets

Captures network informationfrom AWS managed interfaces too: Elastic Loud Balancer, ElastiCache, RDS, Aurora, etc...
VPC Flow Logs data can go to S3, CloudWatch Logs and Kinesis Data Firehose

## VPC Peering

Connect to VPC, privately using AWS network
Make them bvehave as if they were in the same network
Must not have overlapping CIDR(IP address Range)
VPC Pearing connection is not transitive(must be established for each VPC that need to communicate with one another)

## VPC Endpoints

Endpoints allow you to connect AWS Services using a private network instead of public www network
This gives you enhanced security and lower latency to AWS Services
VPC Endpoint Gateway: S3 and DynamoDB
VPC Endpoint Interface: the rest

## AWS PrivateLink(VPC Endpoint Service)

Most secure and scalable way to expose a service to 1000s ofn VPCs 
Does not require VPC Peering, internet gateway, NAT, Route Tables
Requires a network Load BAlancer(Service VPC) and Elactic Network Interface(ENI) (Costumer VPC)

## Site to Site VPN and Direct Connect

Site to Site VPN:
- Connect an on-premises VPN to AWS
- The connection is automatically encrypted
- Goes over the public internet

Direct Connect(DX):
- Establish a physical connection between on-premises and AWS
- The connection is private, secure and fast
- Goes over a private network 
- Takes at least a month to establish

Site to Site VPN:
- On-premises must use a Customer Gateway(CGW)
- AWS must use a Virtual Private Gateway(VGW)

## AWS Client VPN

Connect from your computer using OpenVPN to your private network in AWS and on-premises
Allows you to connect to your EC2 insatances over a private IP(just as if you were in the VPC Network)
Goes over public network

## Transit Gateway

For having transitive peering between 1000s of VPCs and on-premises, hub-and-spoke(star) connection
It simplfies the Network Topology
One single Gateway to provide this functionality
Works with Direct Connect, Gateway, VPN connections

## VPC - Summary

VPC = Virtual Private Cloud
Subnets: Tied to an AZ, network partition of the VPC
Internet Gateways: at the VPC Level provide internet access
NAT Gateweay/Instances: give internet access to private subnets
NACL: Stateless, subnet rules for inbound and outbound traffic
Security Groups: Stateful, operates at the EC2 level or ENI
VPC Peering: Connect two VPC with non-overlapping IP address renges, non transitive
Elastic IP: Fixed public IPv4, ongoing cost if not used 
VPC Endpoints: Provide private access to AWS Services within VPC
PrivateLink: Privately connect to a service in a 3rd party VPC
VPC Flow Logs: Network Traffic Logs
Site top Site VPN: VPN over public internet between on-premises Data Center and AWS
Client VPN: Open VPN connetion from your computer into your VPC 
Direct Connect: Direct Private connection to AWS(physical connection)
Transit Gateway: Connect 1000s of VPC and on-premises networks together

# Security and Compliance

## AWS Shared Responsibility Model

AWS resposibility - Security of the Cloud
- Protecting infrastructure(hardware, software, facilities, and networking) that runs all the AWS Services
- Managed services like S3, DynamoDB, RDS, etc...

Customers Responbsibility - Security in the Cloud
- For EC2 instance, customer responsible for management of the guest OS(including patches and updates), firewall and Network Configurations, IAM, etc...
- Ecrypting application Data

Shared Controls:
- Patch management, Configurastion management, Awareness and Training

### Example for RDS

AWS responsibility:
- MAnage underlying EC2 instance, disable SSH access, 
- Automated Database patching
- Automated OS Patching
- Audit underlying instance and disk, guarantee it functions

Your Responsibility:
- Check the ports, IP, security group inbound rules
- In Database user creation and permissions
- Creating a database with or without public access
- Ensure parameter groups or DB is configured to only allow SSL connection
- Database encryption settings

### Example for S3

AWS Responsibility:
- Guarantee you get unlimited storage
- Guarantee you get encryption
- Ensure seperation of the Data between different customers
- Ensure AWS employees can't accesss your data

Your Responsibility:
- Bucket configuration
- Bucket policy/public settings
- IAM user and roles
- Enabling encryption

### What is a DDoS Attack?

Distrubuted Denial-of-Service
A hacker launch bunch of master servers
Each master server launch bunch of bots
These bots start sending many requests to your application
Your server become down under this load 

### DDoS Protection in AWS

AWS Shield Standard: Protect against DDoS attacks for your websites and application, for all customers at no additional costs
AWS Shield Advaced: 24/7 Premium DDoS protection 
AWS WAF(Web Application Firewall): Filter specific requests based on the rules
CloudFront and Route53: 
- Availability protection using global edge network 
- Combined with AWS Shield, provides attack migration at the edge

Be ready to leverage and scale AWS Auto Scaling

## AWS Shield

AWS Shield Standard:
- Free service that activated for every customer
- Provides protection from attacks such as SYN/UDP Floods, Reflection Attacks and other Layer 3/4 attacks

AWS Shield Advanced:
- Optional DDoS mitigation Service ($3000 per month per organization)
- Protect against attacks on Amazon EC2, ELB, AWS CloudFront, AWS Global Accelerator, Route53
- 24/7 access to AWS DDoS response team(DRP)
- Protect against higher fees during usage spikes due to DDoS

## AWS WAF - Web Application Firewall

Protects your web application from common web exploits(Layer 7)
Layer 7 is HTTP (vs Layer 4 is TCP)
Deploy on ALB, API Gaateway, CloudFront
Define Web ACL(Application Control List):
- Rules can include IP addresses, HTTP headers, HTTP body or URI strings
- Protects from common attacks - SQL Injections and Cross Site scripting(XSS)
- Size constraints, geo-match(block countries)
- Rate-based rules(to count occurences of events) - for DDoS protection

## AWS Network Firewall

Protect your entire VPC
From Layer 3 to Layer 7 protection
Any direction, you can inspect:
- VPC to VPC traffic
- Outbound to Internet
- Inbound from Internet
- To/from Direct Connect and Site to Site VPN

## AWS Firewall MAnager

Manage security rules in all accounts of an AWS Organization
Security policy: common set of security rules
- VPC security Groups for EC2, ALB, etc...
- WAF Rules
- AWS Shield Advanced
- AWS Network Firewall

Rules are applied to new resources as they are created(good for compliance) across all and feature accounts in your organization

### Penetration Testing in AWS Cloud

AWS costumers welcome to carry out security assessments or penetration tests against their AWS infrastructure without prior approval for these services:
- Amazon EC2 instances, NAT Gateways and ELB
- Amazon RDS
- Amazon CloudFront
- Amazon Aurora
- Amazon API Gateway
- AWS Lambda and Lambda Edge functions
- Amazon LightSail resources
- Amazon Elastic Beanstalk environments

List can increase over time

Prohibited activities:
- DNS Zone walking via Amazon Route53 Hosted Zones
- Denial of Service(DoS), Distrubuted Denial of Service(DDoS), Simulated DoS and Simulated DDoS
- Port flooding
- Protocol Flooding
- Request flooding(login request flooding, API request flooding)

For any other simulated events contact AWS Security Team

### Encryption at AWS

Data at Rest: Data stored or archived on a device 
- On a Harddisk, on a RDS instance, in S3 Glacier Deep Archive, etc...

Data in Transit(in motion): Data being moved from one location to another
- Transfer from on-premises to AWS, EC2, DynamoDB etc...
- Means data transferred on the network

We want to encrypt data in both states!
For this we leverage encryption keys.

## AWS KMS(Key Management Service)

Anytime you hear "encryption" for an AWS Service, it's most likely KMS
KMS: AWS manages the encryption keys for us
Encryption Opt-In:
- EBS volumes: encrypt volumes
- S3 Buckets: Server-Side encryption of objects
- Redshift DB: encryption of data
- RDS Database: encryption of data
- EFS drives: encryption of data

Encryption automatically enabled:
- CloudTrail Logs
- S3 Glacier
- Storage Gateways

## CloudHSM

KMS -> AWS manages the software for encryption
CloudHSM -> AWS provisions encryption hardware 
Dedicated Hardware(HSM = Hardware Security Module)
You manage your own encryption keys entirely(not AWS)
HSM device is tamper resistant, FIPS 140-2 Level 3 compliance which is a security standard

### Types of KMS Keys

Customer Managed Keys:
- Create, manage and used by customer, can enable or disable
- Possibility of Rotation Policy(new key generated every year, old keys preserved)

AWS Managed Keys:
- Created, managed and used on customers behalf by AWS 
- Used by AWS Services(aws/s3, aws/ebs, aws/redshift)
- Collection of CMKs that an AWS Service owns and manages to use in multiple accounts
- AWS can use those to protect resources in your account(but you can't view keys)

CloudHSM Keys(Custom Keystore):
- Keys generated from your own CloudHSM Hardware device
- Cryptographic operations are performed within the CloudHSM cluster

## AWS Certificate MAnager

Let's you easily provision, manage and deploy SSL/TLS Certificates
Used to provide in-flight encryption for websites(HTTPS)
Supports both public and private SSL certificates
Automatic certificate renewal
Integration with(load TLS certificates on):
- ELB
- CloudFront Distrubutions
- APIs and API Gateway

## AWS Secret Manager

Newer service, meant for storing secrets
Capability to force rotation of secrets every X days
Automatic ge neration of secrets on rotation(uses Lambda)
Integration with Amazon RDS(MySQL, PostgreSQL, Aurora)
Secrets are encrypted using KMS
Mostly meant for RDS integration 

## AWS Artifact (not really a Service)

Portal that provides customers with on-demand access to AWS compliance documentation and AWS Aggrements
Artifact Reports: Allows you to download AWS Security and Compliance Documents from 3rdf party auditors like AWS ISO certifications, Payment Card Industry(PCI) and System and Organization Control(SOC)reports
Artifact Aggrements: Allows you to review, accept and track the status of AWS agreements such as the Business Associate Addendum(BAA) or the Health Insurance Portability and Accountability Act(HIPAA) for an individual account or in your organization
Can be used to support internal audit or compliance

## Amazon Guard Duty

Intelligent Thread discovery to protect AWS account 
Uses ML algorithms, anbomaly dsetection, 3rd party data
One click to enable(30 days trial), no need to install software
Input data includes: 
- CloudTrail Events Logs: unusual API calls, unauthorized deployments
- - CloudTrail Management Events: Create VPC subnet, create trail
- - CloudTrail S3 Data Events: get object, list objects, delete object, ...
- VPC Flow Logs: unusual internet traffic, unusual IP addresses
- DNS logs: compromised EC2 instances, sending encoded data within DNS queries
- Optional Features: EKS Audit Logs, RDS and Aurora, EBS, Lambda, S3 Data Events, ...

Can setup EventBridge rules to be notified in case of findings
EventBridge rules can target Lambda or SNS
Can protect against CryptoCurrency attacks(has a dedicated finding for it)

## Amazon Inspector

Automated Security Assessments
For EC2 Instances:
- Leveraging AWS System Manager(SSM) agent
- Analyze against unintended Network Accesibility
- Analyze running OS against known vulnerabilities

For Container images pushed to Amazon ECR:
- Assessment of container images as they are pushed

For Lambda Functions:
- Identifies software vulnerabilities in function code and package
- Assessment of functions as they are deployed 

Reporting and Integration with AWS Security Hub
Send findings to Amazon EventBridge

### What does Amazon Inspector Evaluates?

Remmeber: Only for EC2 instances, Container images in ECS and Lambda functions
Continous scanning of infrastructure, only when needed
Package vulnerabilities(EC2, ECR, Lambda) - database of CVE
Network reachibility(EC2)
A risk score associated with all vulnerabilities for priorization

## AWS Config

Helps with auditing and recording compliance of your AWS resources
Helps record configurations and changes over time
Possibility of storing the configuration data into S3(analyzed by Athena)

Questions that can be solved by AWS Config:
- Is there unrestricted SSH access to my security groups?
- Do my buckets have any public access?
- How has my ALB configuration changed over time?

You can receive alerts(SNS notifications) for any changes
AWS Config is a per-region service
Can be aggregated across regions and accounts
View compliance of a resource over time 
View configuration of a resource over time
View CloudTrail API calls if enabled

## Amazon Macie

Amazon Macie is a fully managed data security and data privacy service that uses ML and pattern matching to discover and protect your sensitive data in AWS.
Macie helps identify and alert you to sensitive data, such as Personally Identifiable Information(PII)

## AWS Security Hub

Central security took to manage security across several AWS accounts and automate security checks 
Integrated dashboards showing current security and compliance status to quickly take actions 
Automatically aggregates in predefined or personal findings from various AWS services and AWS Partner Tools:
- Config
- GuardDuty
- Inspector
- MAcie
- IAM Access Analyzer 
- AWS System MAnager 
- AWS Health
- AWS Partner Network Solutions

Must first enable the AWS Config Service

## Amazon Detective 

GuardDuty, MAcie and Security Hub are used to identify potential security issues or findings
Sometimes security finding require deeper analysis to isolate the root cause and take action - it's a complex process
Amazon Detective analyzes, investigate and quickly identifies the root cause of security issues or suspicious activities
Automatically collects and process events from VPC Flow Logs, CloudTrail, GuardDuty and create a unified view
Produces visualizations with details and context to get the root cause 

## AWS Abuse 

Report suspected AWS resources used for abusive or illegal purposes
Abusive and prohibited behaviours are:
- Spam - receiving undesired emails, from AWS-owned IP address, websites and forums spammed by AWS resource
- Port Scanning: Sending packets to your ports to discover the unsecured ones
- DoS and DDoS Attacks: AWs owned resources try to overwhelm or crash your servers/softwares
- Intrusion Attempts: Logging in on your resources 
- Hosting objectionable or copyrighted content without consent
- Distrubuting Malware: AWS resources distrubuting softwares to harm computers and machines

For any of the above contact with AWS Abuse Team

## Root User Priviliges

Root User == Account Owner(created when account is created)
HAs complete control and access to all AWS services and resources 
Lock away your AWS account root user access keys!
Do not use your root account for every day tasks, even administrative tasks

Actions that can be performed by only root user:
- Change account Settings(account name, email, root user password, rtoot user access keys)
- View certain tax invoices
- Close your AWS Account
- Restore IAM permissions
- Change or cancel your AWS Support Plan
- Register as a Seller in the Reserved Instance Marketplace
- Configure an S3 Bucket to enable MFA 
- Edit or delete an Amazon S3 Bucket policy that includes an invalid VPC ID or VPC Endpoint ID 
- Sign up for GovCloud

## IAM Access Analyzer

Find out which resources shared externally 
- S3 Buckets
- IAM Roles
- KMS Keys
- Lambda functions and layers
- SQS Queries
- Secret MAnager Secrets

Define Zone of Trust: AWS Account or AWS Organization
Access outside zone of trust -> findings

### Security and Compliance - Summary

Shared Responsibility model in AWS
Shield: Automatic DDoS protection + 24/7 support for advanced
WAF: Firewall to filter incoming requests based on the rules 
KMS: Encryption keys managed by AWS
CloudHSM: Hardware encryption, we manage encryption keys
AWS Certificate Manager: Provision, Manage and deploy SSL/TLS Certificates
Artifact: Get access to compliance reports such as PCI, ISO, etc...
GuardDuty: Find malicious behaviour with VPC, DNS and CloudTrail Logs
Inspector: Find software vulnerabilities in EC2 instances, ECR images and lambda functions
NEtwork Firewall: Protect VPC against network attacks
Config: Track config changes and compliance against rules 
Macie: Find sensitive data(ex: PII) in S3 buckets
CloudTrail: Track API calls made by users within account 
AWS Security Hub: gather security findings from multiple accounts
Amazon Detective: Find the root cause of security issues or suspicious activities
AWS Abuse: Report abusive or malicious AWS resources
Root User Priviliges:
- Change account settings
- close your AWS account 
- Change or cancel your AWS Support Plan
- Register as a seller in the reserved Instance Marketplace

IAM Access Analyzer: identify which resources shared externally
Firewall Manager: Manage security rules across an organization(WAF, Shield)

# Machine Learning

## Rekognition

Find objects, people, text, scenes in images and videos using ML.
Facial analysis and facial search to do user verification, people counting 
Create a database of familiar faces or compare against celebrities
Use Cases:
- Labeling
- Content Moderation
- Text Detection
- Face detection and Analysis(gender, age, emotions, ...)
- Face search and verification
- Celebrity Recognition
- Pathing(ex: for sport game analysis)

## Amazon Transcribe

Automatically converts speech to text 
Uses a Deep Learning process called Automatic Speech Recognition(ASR) to convert speech to text quickly and accurately
Automatically remove Personally Identifiable Information(PII) using Redaction
Supports Automatic Language Identification for multi-lingual audio
Use Cases:
- Transcribe costumer service calls
- Automated closed captioning and subtitles 
- Generate metadata for media assets to create a fully searchable archive

## Amazon Polly 

Turn text into life-like speech using deep learning
Allowing you to create applications that can talk

## Amazon Translate

Natural and accurate language translation
Amazon translate allows you to localize content - such as web sites and applications - for international users easily translate large volumes of text efficiently

## Amazon Lex

Same technology that powers Alexa
Automatic Speech Recognition(ASR) to convert speech to text 
Natural Language understanding to recognize the intent of the text, callers
Helps build chatbots, call center bots

## Amazon Connect

Receive calls, create contact flows, cloud based virtual contact center
Can integrate with other CRM systems or AWS 
No upfront payments, %80 cheaper then traditional contact center solutions

## Amazon Comprehend

For Natural Language Processing(NLP)
Fully managed and serverless service
Uses ML to find insights and relationships in text:
- Language of text
- Extract key phrases, places, people, brands or events
- Understands how positive or negative the text is
- Analyzes text using tokenization and parts of speech
- Automatically organizes a collection of text files by topic

Sample Use Case: 
- Analyze customer Interactions(e mail) to find what leads to a positive or negative experience
- Create and group articles by topic that comprehend wil uncover

## Amazon SageMaker

Fully managed service for developers/data scientists to build ML models
Typically difficult to do all the processes in one place + provision servers

## Amazon Forecast

Fully managed service uses ML to deliver highly accurate foreccasts
Example: Predict the future sales of a product
%50 more accurate than looking at the data itself
Reduce forecasting time from months to hours 
Use Cases:
- Product demand planning
- Financial Planning
- Resource Planning

## Amazon Kendra

Fully managed document search service powered by ML
Extract answers from within a document(text, pdf, HTML, PowerPoint, MS Word, ...)
Natural language search capabilities
Learn from user interactions/feedback to promote preferred results(Incremental Learning)
Ability to manually fine-tune search results(importance of data, freshness, custom, ...)

## Amazon Personalize 

Fully managed ML service to build apps with real-time personalized recommendations 
Use Cases:
- Personalized Product Recommendations/re-ranking
- Customized direct marketing

Same technology used by Amazon.com
Integrates into existing websites, applications, SMS, e-mail marketing systems ...
Implement in days not months(You don't need to build, train and deploy ML models)
Example: 
- Retail Stores
- Media and Entertainment

## Amazon Textract

Automatically extract text, handwriting and data from any scanned document using AI and ML
Extract data from forms and tables 
Read and process any type of document(PDFs, images, ...)
Use Cases:
- Financial Services(e.g. invoices, financial reports)
- Healthcare(e.g. medical records, insurance claims )
- Publc Sector(e.g. tax forms, ID, passports)

### AWS Machine Learning - Summary

Rekognition: Face detection, labeling, celebrity recognition
Transcribe: Audio to text(ex: subtitles)
Polly: Text to Audio
Translate: Translations
Lex: Build conversational bots
Connect: Cloud Contact Center
Comprehend: Natural Language Processing
SageMaker: ML for developers and Data Scientists
Forecast: Build highly accurate forecasts
Kendra: ML powered document search engine
Personalize: Real-time personalized recommendations
Textract: Detect Text and Data in documents

# Account and Management, Billing and Support

## AWS Organizations

Global service
Allows to manage multiple accounts
The main account is master account
Cost Benefits:
- Consolidated billing across all accounts - single payment method
- Pricing benefits from aggregated usage(Volume discount for EC2, S3)
- Pooling of reserved EC2 instances for optimal savings

API is available to automatically create AWS Accounts
Restricted account priviliges using Service Control Policies(SCP)

### Multi Account Strategies

Create accounts per department, per cost center
Create an account for each environment dev/test/prod
Create accounts based on regulatory restrictions
To have seperate per-account service limits
For isolated resources
Multi Account vs One Account with Multi VPC
Use tagging standards for billing purposes 
Enable CloudTrail on all accounts, send logs to central S3 account 
Send CloudWatch Logs to central logging account 

## Service Control Policies

Whitelist or Blacklist IAM actions
Applied at the Organizational Unit(OU) or Account Level
Does not apply to MAster Account
SCP applied to sll the Users and Roles of the account including root
The SCP does not affect, service-linked roles 
- Service-linked roles enable other AWS services to integrate with AWS Organizations and can't be restricted by SCPs.

SCP must have an explicit allow(does not allow anything by default)
Use Cases:
- Restrict access to certain services (example: can't use EMR)
- Enforce PCI compliance by explicitly disabling services

OU level > Account Level
If you allow something in OU level even if an account at that OU level has deny SCP on it can access that service.
SCP looks like an IAM policy it's a JSON object

### AWS Organizations - Consoladated Billing

When enabled provides you with:
- Combined usage - combine the usage across all AWS Accounts in the AWS Organiztion to share the volume pricing, Reserved Instances, Savings Plan discounts.
- One Bill - Get one bill for all AWS Accounts in the AWS Organization

The management account can reserve Instances discount sharing for any account in AWS Organization, included itself

## AWS Control Tower

Easy way to setup and govern a secure and compliant multi-account AWS environment based on the best practices.
Benefits:
- Automate the set up of your environment in a few clicks
- Automate ongoing policy management using guardrails 
- Detect policy violations and remediate them
* Monitor compliance through an interactive dashboard

AWS Control Tower runs on top of AWS Organizations:
- It automatically sets up AWS Organizations to organize accounts and implement SCPs(Service Control Policy)

## AWS Resource Manager(AWS RAM)

Sahre AWS Resources that you own with other AWS accounts
Share with any account or within your organization 
Avoid resource duplications!
Supported Resources:
- Aurora
- VPC Subnet
- Transit Gateway
- Route53
- EC2 Dedicated Hosts
- License manager Configurations

## AWS Service Catalog

Users that are new to AWS have too many options, and may create stacks that are not compliant/in line with the rest of the organization.
Some users just want a quick self-service portal to launch a set of authorized products pre-defined by admins.
Includes:
- Virtual MAchines
- Databases
- Storage Options

## Pricing Models In AWS

AWS has 4 pricing models:
- Pay as you go: Pay for what you use, remain agile, responsive, meet scale demands.
- Save when you reserve: minimize risks, predictably manage budgets, comply with long-term requirements.
- - EC2 Reserved Instances
- - DynamoDB Reserved Capacity
- - ElatiCache Reserved Nodes
- - RDS Reserved Instance
- - RedShift Reserved Nodes
- Pay less by using more: Volume based discount
- Pay less as AWS grows

### Free Services and Free Tier in AWS 

Totally free:
- IAM 
- VPC
- Consolidated Billing

Pay for only underlying resources:ü
- Elastic Beanstalk
- CloudFormation
- Auto Scaling Groups

Free Tier:
- EC2 t2.micro insatance for a year
- S3 
- EBS
- ELB
- AWS Data Transfer

### Compute Pricing - EC2

Only Chrged for what you use:
Number of instances
Instance Configuration:
- Physical Capacity
- Region
- OS and Software
- Instance Type
- Instance Size

ELB running time and amount data processed 
Detailed monitoring 

On-Demand Instances:
- Minimum of 60 seconds
- Pay per second(linux/windows) or per hour (Other)

Reserved Instances:
- Up to %75 discount compared to on-demand hourly rate
- 1 or 3 years commitment
- All upfront, Partial upfront, No Upfront

Spot Instances:
- Up to %90 discount compared to on-demand hourly rate
- Bid for unused capacity

Dadicated Hosts:
- On-Demand
- Reservations for 1 year or 3 years commitment

Savings Plan: As an alternative to save on sustained usage.

Lambda:
- Pay per call
- Pay per duration 

ECS:
- EC2 Launch Type Model: No additional fees, you pay for AWS resources created and stored in your application.

Fargate:
- Fargate Launch Type Model: Pay for vCPU and Memory resources allocasted to your applications in your container.

### Storage Pricing

S3:
- Storage Class S3 Standard, S3 Infrequent Access, S3 One-Zone IA, S3 Intelligent Tiering, S3 Glacier or S3 Glacier Deep Archive
- Number and the size of objects: Price can be tiered(based on the volume)
- Number and type of requests
- Data tranfer OUT of the region
- S3 Transfer Acceleration
- Lifecycle Transitions

EFS:
- Pay per use, has infrequent access, lifecycle rules.

EBS:
- Volume type(based on performance)
- Storage volume in GB per month provisioned
- IOPS:
- - General Purpose SSD: Included
- - Provisioned IOPS SSD: Provisioned amount in IOPS
- - Magnetic: Number of requests.
- Snapshots:
- - Added data cost per GB per month
- Data Transfer:
- - Outbound data transfer are tiered for volume discounts
- - Inbound is free.

### Database Pricing

RDS:
- Per hour billing 
- Database characteristics:
- - Engine
- - Size 
- - Memory Class  
- Purchase Type:
- - On-Demand
- - Reserved Instances(1 or 3 years) with required upfront
- Backup storage: There is no additional charge for back up storage up to %100 of your total database storage for a region
- Additional Storage(per GB per month)
- Number of input and output requests per month.
- Deployment Type(Storage and I/O are variable):
- - Single AZ
- - Multiple AZ
- Data Tranfer:
- - Outbound data transfer is tiered for volume discount
- - Inbound is free

### Content Delivery

CloudFront:
- Pricing is different across different geographic regions
- Aggregated for each edge location, then applied to your bill
- Data transfer OUT(Volume discount)
- Number of HTTP/HTTPS requests

### Networking cost in AWS per GB

Use private IP instead of public IP for good savings and better network performance
Use same AZ for maximum savings(at the cost of high availability)

### Savings Plans

Commit a certain $ amount per hour for 1 or 3 years 
Easiest way to setup long-term commitments on AWS 
EC2 Savings Plan:
- Up to %72 discount compared to On-Demand 
- Commit to usage of individual instance families in a region(e.g. c5 or m5)
- Regardless of AZ, size(m5.xl to m5.4xl), OS(Linux/Windows), or tenancy
- All upfront, Partial upfront, No upfront

Compute Savings Plan:
- Up to %66 discount compared to On-Demand
- Regardless of Family, Size, Region, OS, Tenancy, compute options
- Compute Options: EC2, Fargate, Lambda

Machine Learning Savings Plan: Sage Maker, ...

Setup from AWS Cost Explorer Console

## AWS Compute Optimizer

Reduce costs and improve performance by recommending optimal AWS Resources for your workloads
Helps you choose optimal configurations and right size your workloads(over/under provisioned)
Uses ML to analyze your configurations and their utilization CloudWatch metrics
Supported Resources:
- EC2 instances
- EC2 ASG
- EBS Volumes
- Lambda Functions

Lower your costs by up to %25
Recommendations can be exported to S3

## Billing and Costing Tools

Estimate Costs in the Cloud:
- Pricing Calculator

Tracking Costs in the Cloud:
- Billing Dashboard
- Cost Allocation Tags
- Cost and usage Reports
- Cost Explorer

Monitoring Against Costs Plans:
- Billing Alarms
- Budgets

## AWS Pricing Calculator

Estimate the cost of your solution architecture

### Cost Allocation Tags

Use cost allocation tags to track your AWS costs on a detailed level

AWS Generated tags:
- Automatically applied to your resource you create 
- Start with prefix "aws:"

User Generated Tags:
- Defined by User
- Start with prefix "user:"

### Tagging and Resource Groups

Tags are used to organizing resources:
- EC2: instances, images, load balancers, security groups, ...
- RDS, VPC resources, Route 53, IAM users, etc...
- Resources created by CloudFormation are all tagged the same way 

Common Tags are: Name, Environment, Team, ...
Tags can be used to create resource groups:
- Create, maintain and view a collection of resources that share common tags.
- Manage these tags using Tag Editor

## Cost And Usage Reports

Dive deeper into your AWS costs and usage
The AWS Cost and Usage Report contains the most comprehensive set of AWS cost and usage data avilable, including additional metadata about AWS servicing, pricing and reservations.
The AWS Cost and Usage Report lists AWS usage for each service category used by an account and its IAM users in hourly or daily line items, as well as any tags you activated for cost allocation purposes.
Can be integrated with Athena, Redshift or QuickSight.

## Cost Explorer 

Virtualize, understand and manage your AWS costs and usage over time
Create custom reports that analyze cost and usage data 
Analyze your data at high level: Total Costs and usage across all accounts
Or monthly, hourly resource level granularity
Choose an optimal savings plan(to lower prices on your bill)
Forecast usage up to 12 months based on previous usage 

### Billing Alarms in CloudWatch

Billing data metric stored in us-east-1
Billing data are for overall worldwide AWS costs
It's for actual cost, not for projected costs
Intended a simple alarm(not as powerfull as AWS Budgets)

## AWS Budgets

Create budget and send alarms when costs exceeds the budget

4 Types of Budgets:
- Usage 
- Cost
- Reservations
- Savings Plans

For Reserved Instances:
- Track utilization
- Supports EC2, Elasticache, RDS, RedShift

Can filter by Service, Linked Account, Tag, Purchase Option, Instance Type, Region, AZ, API Operations, ...
Same Options as AWS Cost Explorer
2 budgets are free then $0.02 /day/budget

## AWS Cost Anomaly Detection

Continously monitor your cost and usage using ML to detect unusual spends
It learns your unique, historic spend patterns to detect one-time cost spike and/or continously cost increase(you don't need to define threshold)
Monitor AWS Services, member accounts, cost allocation tags or cost categories
Sends you to anomaly detection report with root cause analysis
Get notified with individual alerts or daily/weekly summary(using SNS)

## AWS Service Quotas 

Notify you when you are close to a service quota value threshold
Create CloudWatch Alarms on the Service Quotas Console
Example: Lambda concurrent executions 
Request a quota increase from AWS Service Quotas or shutdown resources before limit is reached

## AWS Trusted Advisor

No need to install anything - high level AWS account assessments
Analyze your AWS Accounts and provides recommendations on 6 categories:
- Cost Optimiztion
- Performance
- Security
- Fault Tolerance
- Service Limits
- Operational Excellence

Business and Enterprise Support Plan:
- Full set of checks
- Programmatic access using AWS Support API

## AWS Support Plans

### AWS Basic Support Plan

Customer Service and communities - 24x7 access to customer service, documentation, white papers and support forums
AWS Trusted Advbisor - Access to 7 core trusted advisor checks and guidance to provision your resources following best practies to increase performance and improve security
AWS Personal Health Dashboard - A personalized view of the health of AWS services and alerts when your resources are impacted.

### AWS Developer Support Plan

All basic Support Plan + 
Business hours email access to Cloud Support Associates 
Unlimited Cases / 1 primary contact
Case Severity / Response Times:
- General Guidance: < 24 business hours
- System Impaired: < 12 business hours

### AWS Business Support Plan (24x7)

Intended to be used if you have production workloads
Trusted Advisor - Full Set of Checks and API access
24x7 phone, email and chat access to Cloud Support Engineers
Unlimited Cases / Unlimited Contacts
Access to Infrastructure Event Management for additionasl fee
Case Severity/Response Times: 
- General Guidance: < 24 business hours
- Systems Impaired: < 12 business hours
- Production System Impaired: < 4 hours
- Production System Down: < 1 hour

### AWS Enterprise On-Ramp Support Plan (24x7)

Intended to be used if you have production or business critical worklods
All of the Business Support Plan +
Access to a pool of Technical Account Managers(TAM)
Cocierge Support Team(for billing and account best practices)
Infrastructure Event Management, Well-Architected and Operations Reviews
Case Severity / Response Times:
- ...
- Production System Impaired: < 4 hours
- Production System Down: < 1 hour
- Business Critical system down: < 30 minutes

### AWS ENterprise Support Plan(24x7)

Intended to be used if you have mission critical workloads
All of the business Support Plan +
Access to a designated Technical Account Manager(TAM)
Concierge Support Team(for billing and account best practices)
Infrastructure Event Manager, Weel-Architected and Operations Team
Case Severity / Response Times:
- ...
- Production System Impaired: < 4 hours
- Production System Down: < 1 hour
- Business Critical system down: < 15 minutes

## Account Best Practices - Summary

Operate multiple accounts using Organizations
Use SCP(Service Control Policy) to restrict account power
Easily setup multiple accounts with best practices with AWS Control Tower
Use Tags and Cost Allocation Tags for easy management and billing
IAM guidelines: MFA, Least-privilige, password policy, password rotation
AWS Config: To record all resources configurations and compliance over time 
CloudFormation: to deploy stacks across accounts and regions
Trusted Advisor: To get insights, Support Plan adopted to your needs 
Send service logs and access logs to S3 or CloudWatch Logs
CloudTrail to record API calls made within your account 
If your account compromised: change the root password, delete and rotate all passwords/keys, contact AWS Support
Allow users to create pre-defined stacks defined by admins using AWS Service Catalog

## Billing and Costing Tools - Summary

Compute Optimizer: Recommends Resources configurations to reduce costs
Pricing Calculator: Calculate cost of services in AWS 
Billing Dashboard: High-level overview + Free Tier Dashboards
Cost Allocation Tags: Tag resources to create detailed reports 
Cost and Usage Reports: Most comprehensive billing dataset
Cost Explorer: View current usage (detailed) and forecast usage
Billinmg Alarms: in us-east-1 track overall and per-servicve usage
Budgets: more advanced - track usage, costs, RI, and get alerts.
Savings Plans: Easy way to save based on long-term usage of AWS
Cost Anomaly Detection: Detect unusual spends using ML
Service Quotas: Notify you when you're close to a service quota Threshold

# Advanced Identity

## AWS STS(Security Token Service)

Enables you to create temporary, limited-priviliges credentials to access your AWS resources
Short-Term credentials: You configure expiration period
Use Cases:
- Identity Federation: Manage our identities in external systems and provide them with STS tokens to access AWS resources
- IAM roles for cross/same account access 
- IAM roles for Amazon EC2: provide temporary credentials for EC2 instances to access AWS resources 

## AWS Cognito

Identify for your web and mobile application Users(Potentially Millions)
Istead of creating an IAM user for them, you create a user in incognito

### What is Microsoft Active Directory(AD)?

Found on any Windows Server with AD Domain Services
Database of objects: User Accounts, Computers, Printers, File Shares, Security Groups
Centralized Security Management, Create Accounts, Assign Permissions

## AWS Directory Services

AWS Managed Microsoft AD:
- Create your own Active Directory in AWS, manage users locally, supports MFA
- Establish trust connections with your on-premises AD

AD Connector:
- Directory Gateway(Proxy) to redirect on-premises AD, supports MFA
- Users are managed on on-premises AD

Simple AD:
- AD-compoatible managed Directory in AWS
- Cannot be joined wit on-premises AD

## AWS IAM Identity Center

It's successor to AWS single sign-on
One Login(Single Sign-on) for all your:
- AWS Accounts in AWS Organization
- Business Cloud Applications(ex: SalesForce, Box, Microsoft 365, ...)
- SAML 2.0 - enabled applications
- EC2 Windows Instances 

Idetity Providers:
- Build in identity store in IAM Identity Center 
- 3rd Party: Active Directory(AD), One Login, Okta, ...

## Advanced Identity - Summary

IAM:
- Identity and Access Management inside in your AWS Account
- For users that you trust and belong to your company 

Organiztions: Manage Multiple accounts
Security Token Service(STS): Temporary limited-priviliges credentials to access AWS resources
Cognito: Create a database of users for your mobile and web application
Directory Services: Integrate Microsoft Active Directory in AWS
IAM Identity Center: One login for multiple AWS accounts and applicaitons

