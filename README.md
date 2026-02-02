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

# How can user access AWS

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

### About the AWS SDK

- AWS Software Development Kit
- Language-specific APIs
- Enables you to access and manage AWS services programmatically
- Embedded within your application
- Support JavaScript, Python, PHP, Ruby, Java, GO, Node.JS, C++....
