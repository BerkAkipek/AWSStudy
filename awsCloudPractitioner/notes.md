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

