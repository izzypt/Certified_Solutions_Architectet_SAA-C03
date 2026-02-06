 # Certified_Solutions_Architectet_SAA-C03

# 1 - What's AWS

- AWS - Cloud Provider
- Provide us with servers and services that we can use on <i>**demand**</i> and <u>**scale easily**</u>


# 2 - What services we are going to learn :

- Amazon EC2
- Amazon ECR
- Amazon ECS
- AWS Elastic Beanstalk
- AWS Lambda
- Auto Scaling
- IAM
- AWS KMS
- Amazon S3
- Amazon SES
- Amazon RDS
- Amazon Aurora
- Amazon DynamoDB
- Amazon ElastiCache
- Amazon SQS
- Amazon SQS
- Amazon SNS
- AWS Step Functions
- Amazon CloudWatch
- AWS CloudFormation
- AWS CloudTrail
- Amazon API Gateway
- Elastic Load Balancing
- Amazon CloudFront
- Amazon Kinesis
- Amazon Route 53

# 3 - Creating AWS account

Follow the step at to create an account :

https://aws.amazon.com/

# 4 - AWS Cloud History

2002: Launched internally at amazon because they realized the IT department could be externalized.

2003: Amazon infrastructure is one of their core strenght. Idea to market.

2004: Launched publicly with SQS.

2006: Re-launched publicly with SQS, S3 & EC2.

2007: Launched in EU

# 5 - AWS Global Infrastructure

- AWS Regions
- AWS Availability Zones
- AWS Data Centers
- AWS Edge Locations / Points of Presence

### AWS Regions

AWS Regions are spread across the globe (us-east1, eu-ewst3 etc...) and regions are connected to each other via a network (a private network of AWS).

An AWS region is a cluster of data centers

Most AWS services are region-scoped.

### How to choose an AWS Region

When launching a new application, selecting the right AWS Region is a key architectural decision. Consider the following factors:

### Compliance & data residency
Data governance, legal, and regulatory requirements may dictate where data can be stored and processed.
Example: sensitive data must not leave a specific region without explicit authorization.

Proximity to customers
 - Choosing a region close to your users reduces network latency and improves application performance.

Service availability
 - Not all AWS services, features, or instance types are available in every region. New services are often released in a subset of regions first.

Pricing
 - AWS pricing varies by region. Costs are transparent and published on each service’s pricing page, so regional cost differences should be factored into your decision.

### AWS Availability Zones (AZs)

Each AWS Region consists of multiple Availability Zones (typically 3 to 6).

An Availability Zone is one or more physically separate data centers with:

- Independent power

- Independent networking

- Redundant connectivity

Availability Zones are isolated from one another to reduce the impact of failures, natural disasters, or other incidents, while still being close enough to provide low-latency connectivity.

Designing applications across multiple AZs increases high availability and fault tolerance.

### AWS Points of Presence (Edge Locations)

AWS operates 400+ Points of Presence, including:

- 400+ Edge Locations

- 10+ Regional Edge Caches

These are distributed across 90+ cities in 40+ countries.

Edge Locations are used primarily by services like Amazon CloudFront, AWS WAF, Shield, and Route 53 to:

- Cache content closer to end users

- Reduce latency

- Improve global performance and resilience

# 6 -  IAM (Identity and access management) & AWS CLI

It's a global service.

We can manage users, create them and assign them to groups.

The root account is used to refer to the account you initial create, shouldn't be used or shared.

You should create user.. people within your organization which can be grouped.

Groups can only contain users, not other groups. 

A user can belong to multiple groups.

By creating groups we can manage permissions  

### IAM : permissions

- Users or Groups can be assigned JSON documents called policies, which describe what a user/group is allowed to do.
- Best practice is to follow the least privileged principle, which basically tells you to not give more permission than what the user needs.
- Users with wrong permissions might accidently cost you a lot of money...

### IAM : policies

***In-line policy*** : a policty that is only attached to a user.

***Policy structure***: 

- version
- id (optional)
- statement : one or more individual statements (required)
  - SID (statement identifier - optional)
  - **Effect** : wether the statement allows or denies the access (Allow, Deny)
  - **Principal** : which account/user/role the policy is applied to ( the WHO - who's the target of the policy)
  - **Action** : list of actions this policy allows or denies (the WHAT - what is allowed or denied)
  - **Resource** : list of resources to which the actions will be applied to.
  - Condition : conditions for when this policy is in effect (optional)

### IAM - MFA Overview

Password Policy:

- strong passwords: You can setup a password policy
 - Set a minimum password length
 - Require specific character types
 - Allow IAM users to change their own password
 - Require users to change their password after some time (pw expiration)
 - Prevent password re-use


### MFA - Multi Factor Authentication

It's a must on AWS:

- Users have access to your account and can possibly change configurations or delete resource in your AWS account.
- You want to protect your root Account and IAM users:
 - MFA = password you know + security device you own

MFA app Options:
- Google Authenticator
- Authy

The above are VIRTUAL MFA device.

You can also use HARDWARE optionsm like hardware Key Fovv MFA Device


#### Defining a password policy :

IAM > Account Settings > Edit password policy

### How can user access AWS

3 options:
- AWS Management Console (password + MFA)
- AWS Command Line (CLI; protected by access keys)
- AWS Software Developer Kit (SDK) - for code; protected by access keys

***Acess Keys*** ARE generated through the AWS console !
Users manage their own access key
***Acess kEYS*** ARE SECRET, just like a password. DON'T share them.

- Access Key ID ~= username
- Secret Access Key ~= password

### About the AWS CLI

- A tool that enables you to interact with AWS services using commands in your command-line shell
- Direct access to the public APIs of AWS services
- You can develop scripts to manage your resources

### About the AWS SDK (Software Development Kit)

- AWS Software Development Kit
- Language-specific APIs
- Enables you to access and manage AWS services programmatically
- Embedded within your application
- Support JavaScript, Python, PHP, Ruby, Java, GO, Node.JS, C++....

### AWS CLI Setup

 1 - Search on google "aws CLI install windows" - aws documentation should appear
 2 - Download the Windows installer
 3 - Run the Installer


### Creating AWS ACCESS key

- IAM -> Users -> simao_admin (the user you want to create a key for) -> Create access key
- <img width="786" height="479" alt="image" src="https://github.com/user-attachments/assets/c3b49d05-0c1f-4736-a831-85c65e379ff0" />
- from the terminal run aws configure


### IAM Roles for Services.

- Some AWS services will need to perform actions on your behalf
- To do so, we will assign permissions to AWS services with IAM roles
- We need to allow that service to perform certain actions like we do with some user(s)

***Common roles:***
- EC2 Instance Roles
- Lambda functionn roles
- Roles for CloudFormation

### Iam Roles Hands On
An IAM Role is an identity in AWS that does not belong to a person.
Instead of being “logged into,” it is assumed by something (or someone) temporarily.

Think of it like:

```🎟️ A temporary access badge that gives specific permissions for a specific job. ```

No passwords. No long-lived access keys.


### Iam Security tools

- IAM Credentials Report (account-level)
  - A report that lists all your account's users and the status of their various credentials
 
- IAM Access Advisor (user-level)
  - Access advisor shows the service permissions granted to a usar and when those services were last accessed.

# 7 -  EC2 Fundamentals

- EC2 is one of the most popular of AWS offering
- EC2 = Elastic Compute Cloud = Infrastructure as a service
- It mainly consists on the capability of
  - Renting a virtual machine (EC2) 
  - Storing data on virtual drives (EBS)
  - Distributing load across machine (ELB)
  - Scaling the services usin an auto-sclaing (ASG)
 
 Knowing EC2 is fundamental to understand how the Cloud works


 ### EC2 sizing & configuration options

 - Operating System:
   - Windows
   - Linux
   - Mac OS
- How much compute power & cores (CPU)
- How much random-access memory (RAM)
- How much storage space:
  - Network-attached (EBS & EFS)
  - Hardware (EC2 Instance Store)
- Network card: speed of the card, Public IP address
- Firewall rules: security group
- Bootstrap script (configure at first launch): EC2 User Data

### EC2 User Data

- It is possible to bottstrap our instances using an ***EC2 User data script***.
- ***bootstrapping*** means launching commands when a machine starts.
- The script is ***only run once*** at the instance ***first start***
- EC2 user data is used to automate boot tasks such as :
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything you can think of
- The ***EC2 User Data Script*** runs with the root user

### Hands-On : Launching an EC2 Instance running Linux

We'll be launching our first virutal server using the AWS console.
We'll get a first high-level approach to the various parameters.
We'll see that our web server is launched using EC2 user data.
And learn how to start / stop / terminate our instance.

### EC2 Instance Types - Overview

You can use different types of EC2 instanceshat are optimized for different  use cases (https://aws.amazon.com/ec2/instance-types/)

- ***General Purpose***
  - Great for a diversity of workloads such as web servers or code repositories
  - Balance between compute, memory, networking
 
- ***Compute Optimized (c5 , c6 c6g, c6gn)***
  - Great for compute-intensive tasks that require high performance processors:
    - batch processing workloads
    - Media transcoding
    - High performance web servers
    - High performance computing (HPC)
    - Scientific modeling & machine learning 

- ***Memory Optimized (r5,r5a, r5b, r6, r6a, r6b)***
  - Fast performance for workloads that process large data sets in memory
  - Use cases:
    - high performance , relational/non-relational databases
    - Distributed web scale cache stores
    - In.memory databases optimized for BI (business Intelligence)
    - Applications performing real-time processing of big unstructured data

- ***Accelerated Computing***
- ***Instance Features***
- ***Storage Optimized (D2, D3, D3en, H1)***
  - Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
  - Use cases:
    - High frequency online transaction processing (OLTP) systems
    - Relational & NoSQL databases
    - Cache for in-memory databases (for example, Redis)
    - Data warehousing applications
    - Distributed file systems
  
  AWS has the following naming convention :
  ```m5.2xlarge```

  - m : instance class
  - 5 : generation/version (AWS improves them over time)
  - 2xlarge : size within the instance class

### Security Groups & Classic Ports Overview

- Security Groups are the fundamental of network security in AWS
- They control how traffic is allowed into or out of our EC2 instance.

- Security groups only contain allow rules.
- Security groups rules can reference by IP or by security group

Securty groups are acting as a "firewall" on EC2 instances

They regulate:
- Access to Ports
- Authorized IP ranges - IPv4 and IPv6
- Control of Inbound Network (from other to the instance)
- Control of Outbound Network (from the instance to other)

<img width="1897" height="269" alt="image" src="https://github.com/user-attachments/assets/6bf2b7e5-bb1d-443b-be03-f9ffe6e31667" />

<img width="957" height="471" alt="image" src="https://github.com/user-attachments/assets/c62d9024-125c-42a4-aaef-5504c180febc" />
<img width="957" height="471" alt="image" src="https://github.com/user-attachments/assets/c62d9024-125c-42a4-aaef-5504c180febc" />
