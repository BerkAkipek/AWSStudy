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

