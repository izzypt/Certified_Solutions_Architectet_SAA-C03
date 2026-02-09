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


### Security Grups - Good to know

- Can be attached to multiple instances
- Locked down to a regen /VPC combination
- Does live "outside" the EC2 - if traffic is blocked the EC2 instance won't see it
- ***It's good to maintain one separate security group for SSH access***
- If your application is not accessible (time out), then it's security group issue
- If your group application gives a "connection refused" error, then it's an application error or it's not launched
- All inbound traffic is blocked by default
- All outbound traggic is authorised by default

### Referencing other security groups

<img width="854" height="454" alt="image" src="https://github.com/user-attachments/assets/571293bd-9784-4aaf-90a3-7218c19cf7e6" />

This diagram illustrates a fundamental concept in AWS networking: **Security Group Referencing** (also known as "chaining").

Instead of opening a port to a specific IP address or a wide range (like `0.0.0.0/0`), you tell a Security Group to allow traffic from **any resource that has a specific Security Group ID attached to it.**

---

In the diagram, **Security Group 1** acts as a gatekeeper for the EC2 instance on the left.

* It has rules that say: "I trust **SG 1** and **SG 2**."
* Because the top two instances have those groups attached, their traffic (green arrows) is allowed through on Port 123.
* The bottom instance has **SG 3**, which isn't on the "VIP list," so its traffic (red arrow) is blocked.

---

## Key Advantages

### 1. Dynamic Scalability (Auto-Scaling Friendly)

In a cloud environment, IP addresses are often temporary. If you scale from 2 web servers to 200, you don't want to manually update your database's security group with 198 new IP addresses.

* **With Referencing:** As soon as a new instance launches with the "Web-Server-SG," it automatically has permission to talk to the database. No manual updates required.

### 2. Reduced Maintenance & "Blast Radius"

If you rely on IP addresses, you end up with a "wall of text" in your firewall rules that is hard to audit.

* **With Referencing:** You only need one rule per tier (e.g., "Allow App Tier to talk to DB Tier"). This makes your security posture much easier to read and less prone to human error.

### 3. Security Across Subnets

IP-based rules often force you to open up entire CIDR blocks (e.g., `10.0.1.0/24`). This is risky because *any* resource in that subnet—even one that shouldn't have access—could potentially reach your target.

* **With Referencing:** Traffic is restricted by **identity**, not location. Only instances with the specific "key" (the SG ID) can enter, regardless of which subnet they live in.

### 4. Self-Referencing for Clusters

Notice in the diagram that **Security Group 1** is referencing **itself**. This is a common pattern for clusters (like ElasticSearch or MongoDB). It allows all nodes within that same group to communicate with each other for heartbeats or data replication without needing to know each other's individual IPs.

---

> **Pro Tip:** When you use referencing, the traffic is filtered at the ENI (Elastic Network Interface) level, meaning the blocked traffic (like that from SG 3) never even touches your instance's OS, saving CPU cycles and increasing security.

### Classic Ports to know

- 22 -> SSH
- 21 -> FTP
- 22 -> SFTP
- 80 -> HTTP
- 443 -> HTTPS
- 3389 -> RDP (Remote Desktop Protocol) - log in into a Windows Instnce


### EC2 Instances Purchasing Options

- On-Demand Instance : short workload, predictable pricing, pay by second
- Server (1 & 3 years) 
  - Reserved Instances - long workloads
  - Convertible Reserved Instances - long workloads with flexible instances
- Saving Plans (1 & 3 years) - commitment to an amount of usage, long workload
- Spot instances - short workloads, cheap, can lose instances (less reliable)
- Dedicated hosts - book an entire physical server, control instance placement
- Dedicated instances - no other customers will share your hardware
- Capacity Instances - no other customers will share your hardware
- Capacity Rsercations - reserve capacity in a specific AZ for any duration

### EC2 on Demanad

- Pay what you use:
  - Linux or Windows - billing per second, after the first minute
  - All other operating systems - billing per hour
- Has the highest cost but no upfront payment
- No long-term commitment

- Recommended for short-tem and un-interrupted workloads, where you can't predict how the application will behave 

### EC2 Reserved Instances
- up to 72% discount compared to On-demand (AWS MAY CHANGES DISCOUNTS OVER TIME , not fixed...)
- You reserve a specific instance attributes (Instance Type, Region, Tenancy, OS)
- Reservation Period - 1 year (+discount) or 3 years (+++discount)
- Payment Options - No Upfront (+), Partial Upfront (++), All Upfront (+++)


Whether you choose On-Demand or Reserved, you are getting the exact same virtual server (the same CPU, RAM, and performance).

The difference lies entirely in the **billing model** and the **level of commitment** you make to AWS. Think of it like a car: On-Demand is like a short-term rental or a ride-share, while Reserved is more like a long-term lease.

---

## 1. EC2 On-Demand

This is the most flexible way to use AWS. You pay for compute capacity by the second or the hour (depending on the OS) with no long-term commitment.

* **How it works:** You start an instance, use it, and then terminate it. You only pay for what you used.
* **Best for:** * Short-term, unpredictable workloads.
* Testing and prototyping.
* Applications that cannot be interrupted but don't run 24/7.


* **Cost:** This is the most expensive "per hour" rate because you are paying for the luxury of flexibility.

---

## 2. EC2 Reserved Instances (RIs)

This isn't actually an "instance" you launch; it’s a **billing discount** applied to an On-Demand instance in your account.

* **How it works:** You commit to using a specific instance type in a specific region for a term of **1 or 3 years**.
* **The Discount:** In exchange for this commitment, AWS gives you a massive discount (up to **72%**) compared to On-Demand pricing.
* **Payment Options:** You can pay **All Upfront**, **Partial Upfront**, or **No Upfront** (monthly).
* **Best for:** * Applications with "steady-state" usage (servers that stay on 24/7).
* Budgeting for long-term projects where you know exactly what hardware you need.



---

## Key Differences at a Glance

| Feature | On-Demand | Reserved Instances |
| --- | --- | --- |
| **Commitment** | None (Pay-as-you-go) | 1 or 3 Years |
| **Cost** | Highest hourly rate | Significant discount (up to 72%) |
| **Flexibility** | High (Spin up/down anytime) | Low (Committed to the term) |
| **Ideal Use Case** | Spiky, unpredictable traffic | Predictable, constant traffic |

---

### A Simple Analogy

Imagine you are staying at a hotel:

* **On-Demand:** You walk in off the street and ask for a room for one night. It’s expensive, but you can leave whenever you want.
* **Reserved:** You sign a contract promising the hotel you will stay in that room for the next year. Because they are guaranteed your business, they cut your nightly rate in half.

**Would you like me to help you calculate which option makes more sense for a specific project you have in mind?**

### EC2 Saving Plans

If **Reserved Instances** are a rigid contract, **Savings Plans** are the modern, flexible upgrade.

AWS introduced Savings Plans because customers found Reserved Instances too restrictive—if you committed to a specific "M5" instance but later realized your code ran better on a "C6," you were often stuck with the bill for the wrong hardware.

---

## What is a Savings Plan?

A Savings Plan is a flexible pricing model that offers the same deep discounts as Reserved Instances (up to 72%), but instead of committing to a **specific instance type**, you commit to a **consistent amount of hourly spend** (e.g., "$10/hour") for a 1 or 3-year term.

### How it works:

* **The Commitment:** You promise to spend, for example, $5.00 every hour on AWS compute services.
* **The Discount:** Anything you use up to that $5.00 is billed at a heavily discounted rate.
* **The Overflow:** If you use $7.00 worth of compute in an hour, the first $5.00 is covered by the plan, and the remaining $2.00 is billed at the standard (higher) On-Demand rate.

---

## Types of Savings Plans

| Plan Type | What it covers | Flexibility Level |
| --- | --- | --- |
| **EC2 Instance Savings Plan** | Only specific instance families (e.g., all M5s) in a specific region. | **Medium:** You can switch sizes (M5.large to M5.xlarge) or OS, but must stay in the M5 family. |
| **Compute Savings Plan** | **Any** EC2 instance, plus AWS Lambda and AWS Fargate. | **Highest:** You can switch regions, instance families, OS, and even move from EC2 to Fargate (Serverless). |
| **SageMaker Savings Plan** | Specifically for Amazon SageMaker (Machine Learning) usage. | **Specific:** Only applies to SageMaker costs. |

---

## Why choose Savings Plans over Reserved Instances?

Most users are moving toward Savings Plans because they handle the "real world" better:

1. **Hardware Upgrades:** If AWS releases a newer, faster, cheaper instance type (e.g., moving from  to ), a **Compute Savings Plan** automatically applies its discount to the new hardware.
2. **Less Management:** You don't have to manage "floating" RI credits or perform manual exchanges.
3. **Modern Architecture:** If you decide to migrate your app from a virtual server (EC2) to a container (Fargate) or a function (Lambda), the **Compute Savings Plan** follows you.

> **Note:** Just like Reserved Instances, these are **billing constructs**. Your servers don't reboot or change when you buy a plan; your bill just gets smaller.

---

### Comparison: RI vs. Savings Plan

* **Reserved Instances:** Best if you want to "reserve" capacity (ensure a server is physically available for you in a specific data center) or if you use older, niche instance types.
* **Savings Plans:** Best for almost everyone else because they offer the same discount with much less administrative headache.

### EC2 Spot Instances

- Can get discount of up to 90% compared to On-demand
- Instance that you can "lose" at any point of time if your max price is less than the current spot price.
- The MOST cost-efficient instances in AWS
- Useful for workloads that are RESILIENT TO failure
 - Batch jobs
 - Data analysis
 - Image processing
 - Any distribued workloads
 - Workloads with a flexible start and end time


NOT SUITABLE for critical jobs or databases.

### EC2 Dedicated Hosts

- A physical server with EC2 instance capacity fully dedicated to your use case.
- Allows your address compliance requirements and use your existing server-bound software licenses (per-socker, per-core, pe --VM Software licenses)
- Purchasing Options:
  -  On-Demand - pay per secnd active Dedicated Host;
  -  Reserved - 1 or 3 years (No Upfront, Partial, All Upfront)
 
- The ***most expensive*** option
- Useful for software that have complicated licensing model (BYOLD - Bring Your Own License)
- Or for companies that have strong regulatory or compliance needs


### EC2 Capacity Reservations

- Reserve On-Demand instances capacity in a specific AZ for any duration
- You always have access to EC2 capacity when you need it
- No time commitment (create/cancel anytime), no billing discounts
- Combine with Regional Reserved Instances and Saving Plans to benefit from billing discounts
- You're charget at On-Demand rate wether you run instances or not
- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ


<img width="959" height="485" alt="image" src="https://github.com/user-attachments/assets/e22d065b-bfdb-44ac-ab1c-ad275f2431d2" />

<img width="898" height="454" alt="image" src="https://github.com/user-attachments/assets/37aebc09-e176-4d35-b361-a7a64fbb5966" />

### Spot Instances & Spot Fleet

- Can get a discount of up to 90% compared to On-demand
- Define max spot price and get the instance while current spot price < max
  - The hourly spot price varies based on offer and capacity
  - If the current spot price > your max price you can choose to stop or terminate your instance with a 2 minutes grace period
- Other stategy : ***Spot Block***
  -  "block" spot instance during a specified time grame (1 to 6 hours) without interruptions
  -  in rare situations the intance may be reclaimed

<img width="1480" height="894" alt="image" src="https://github.com/user-attachments/assets/07bf5f9c-7baf-4a49-8c03-8c5aa7210323" />

- Used for batch jobs, data analysis or workloads that are resilient to failure
- Not great for critical jobs or databases

- A spot price is the current market value of an asset, commodity, or currency for immediate purchase, payment, and delivery.
- It represents the "on-the-spot" cash price determined by real-time supply and demand, distinct from futures prices that set delivery for a future date.

A Spot Instance request can be in one of the following states:

- open – The request is waiting to be fulfilled.

- active – The request is fulfilled and has an associated Spot Instance.

- failed – The request has one or more bad parameters.

- closed – The Spot Instance was interrupted or terminated.

- disabled – You stopped the Spot Instance.

- cancelled – You canceled the request, or the request expired.

The following illustration represents the transitions between the request states. Notice that the transitions depend on the request type (one-time or persistent).

<img width="778" height="840" alt="image" src="https://github.com/user-attachments/assets/c26f8a22-0bf8-495b-8733-3c5d075632c4" />


Spot Instance request states.

- A one-time Spot Instance request remains active until Amazon EC2 launches the Spot Instance, the request expires, or you cancel the request. If capacity is not available, your Spot Instance is terminated and the Spot Instance request is closed.

> A persistent Spot Instance request remains active until it expires or you cancel it, even if the request is fulfilled. If capacity is not available, your Spot Instance is interrupted. After your instance is interrupted, when capacity becomes available again, the Spot Instance is started if stopped or resumed if hibernated. You can stop a Spot Instance and start it again if capacity is available. If the Spot Instance is terminated (irrespective of whether the Spot Instance is in a stopped or running state), the Spot Instance request is opened again and Amazon EC2 launches a new Spot Instance. For more information, see Stop a Spot Instance, Start a Spot Instance, and Terminate a Spot Instance.

You can track the status of your Spot Instance requests, as well as the status of the Spot Instances launched, through the status. For more information, see Get the status of a Spot Instance request.

### Spot Fleets

A Spot Fleet is like a “pool manager” for EC2 instances. You tell it how many servers you want, what types are okay, and how much you’re willing to pay. It then automatically launches Spot Instances (and optional On-Demand ones) from the options you allowed.

It keeps adding instances until it reaches your target capacity or max budget.

You can tell it to pick the cheapest instances (lowestPrice) or spread them out for reliability (diversified).

Basically, it helps run lots of servers cheaply and flexibly without you managing each one.

- Spot Fleets = set of Spot Instances + (optional) On-Demand Instances
- The Spot fleet will try to meet the target capacity with price constraints
  - Define possible launch pools: instance type, OS , Availability Zone
  - Can have multiple pools, so tart the the fleet can choose
  - Splot fleet stops launching instances when reaching capacity or max cost.
 
- Strategies to allocate Spot Instances:
  - lowestPrice: from the pool with the lowest price ( cost optimization, short workload)
  - diversified: distributed across all pools (great for availability, long workloads) 

# EC2 - Solutions Architect Associate Level

### Private vs Public vs Elastic IP

- Network has 2 types of IP : Ipv4 and Ipv6
  - IPv4 : 1.92.80.6
  - IPv6 : 1900:4545:3:200:f8ff:f821:67cf


To master the AWS Solutions Architect Associate exam, you need to understand how EC2 addresses work not just in isolation, but how they interact within a VPC.

Here is a streamlined summary of the three IP types you'll encounter on the exam.

---

# ☁️ EC2 IP Address Comparison

### 1. Private IP

Every EC2 instance has at least one Private IP. This is the "internal" address used for communication within the AWS network.

* **Scope:** Reachable only within the VPC or via VPN/Direct Connect.
* **Persistence:** Remains the same when the instance is stopped and restarted.
* **Cost:** Free.
* **Exam Tip:** Use Private IPs for communication between instances in the same VPC to save on data transfer costs and keep traffic off the public internet.

### 2. Public IP

Used for communication between your instance and the internet.

* **Persistence:** **Lost when the instance is stopped.** When you restart the instance, it receives a *new* Public IP from the AWS pool.
* **Assignment:** You can't "own" these; they are assigned dynamically by AWS.
* **DNS:** Usually comes with a public DNS name that resolves to the IP.

### 3. Elastic IP (EIP)

A static, public IPv4 address designed for dynamic cloud computing.

* **Persistence:** It is "masked" to your AWS account. You can stop/start the instance, and the IP **stays the same**.
* **Flexibility:** You can rapidly remapped an EIP to another instance in your account to mask instance failures.
* **Cost Logic:** AWS actually charges you if the EIP is **not** attached to a running instance (to prevent IP squatting).
* **Exam Tip:** Generally, for modern architectures, AWS recommends using a **Load Balancer** or **Route 53** alias instead of a fleet of Elastic IPs.

---

## 📊 Quick Reference Table

| Feature | Private IP | Public IP | Elastic IP |
| --- | --- | --- | --- |
| **Reachability** | Internal (VPC) | Internet | Internet |
| **Survives Stop/Start?** | Yes | No | Yes |
| **Survives Termination?** | No | No | Yes (stays in account) |
| **Changeable?** | No | Yes (on restart) | No (Static) |

---

## 💡 Exam "Gotchas" to Remember

* **Max Limit:** By default, you are limited to **5 Elastic IPs** per region. If an exam question asks how to scale to 50 instances using individual EIPs, the answer is usually "Use a Load Balancer" instead.
* **Public IP Requirement:** An instance can only have a Public IP if it is launched in a **Public Subnet** (a subnet with a route to an Internet Gateway).
* **DNS Behavior:** In a VPC, the Public DNS of an instance resolves to the Public IP from outside the network, but resolves to the Private IP from *inside* the network (to save money and improve speed).

---

# 🏗️ The 3 Types of Placement Groups

<img width="1208" height="634" alt="image" src="https://github.com/user-attachments/assets/c753921f-043c-4591-8399-1b7f03461d89" />

Placement Groups in AWS are a way to **control how EC2 instances are physically placed in AWS data centers** so you can optimize for **performance, latency, or fault tolerance**.

Three types, one-liners each:

* **Cluster** → instances are **packed close together** in the same AZ
  - ✅ ultra-low latency, high throughput (HPC, big data)
  - ❌ higher blast radius if hardware fails

* **Spread** → instances are **kept on separate hardware**
  - ✅ maximum fault isolation (critical small workloads)
  - ❌ limited number of instances
  - ✅ Can span multiple AZs
  - ✅ Each instance is placed on distinct underlying hardware
  - ✅ Designed for maximum fault isolation
  - ❌ Limited to a small number of instances per AZ

* **Partition** → instances are **grouped into partitions**, each on isolated hardware
  - ✅ balance between scale and fault isolation (Kafka, HDFS)
  - ✅ Instances are divided into partitions, and each partition is isolated from the others
  
Think of it as telling AWS *“how close or how far apart should my EC2s live?”*
Quick mental model:

- Cluster → “close together, same AZ”

- Spread → “far apart, even across AZs”

- Partition → “groups isolated, can cross AZs”

### 1. Cluster Placement Groups

All instances are packed into a **single Availability Zone** on the same physical rack.

* **Best for:** Low network latency and high network throughput.
* **Use Case:** High-Performance Computing (HPC), Big Data (Hadoop/Spark), or applications that need lightning-fast node-to-node communication.
* **The Risk:** If the rack or hardware fails, all instances fail (Single Point of Failure).
* **Exam Tip:** If the question mentions "low latency" or "10 Gbps/25 Gbps networking," think **Cluster**.

### 2. Spread Placement Groups

Each instance is placed on **distinct hardware** (different racks, each with its own network and power source).

* **Best for:** Maximizing availability and reducing correlated failures.
* **Capacity:** Limited to **7 instances per AZ** per placement group.
* **Use Case:** Critical individual instances that must be kept separate (e.g., a small cluster of critical SQL nodes).
* **The Risk:** You hit the 7-instance limit quickly.
* **Exam Tip:** If the goal is "strict isolation" or "minimizing simultaneous failure," think **Spread**.

### 3. Partition Placement Groups

Instances are divided into logical segments called "partitions." Each partition has its own set of racks.

* **How it works:** AWS ensures that no two partitions share the same racks.
* **Capacity:** Can scale to hundreds of instances.
* **Use Case:** Large distributed workloads like HDFS, Cassandra, or Kafka.
* **The Risk:** One partition failure affects all instances *within* that partition, but other partitions remain safe.
* **Exam Tip:** If you see "topology-aware" workloads or large-scale distributed databases, think **Partition**.

---

## 📊 Summary Table

| Strategy | Latency | Reliability | Max Instances | Best For |
| --- | --- | --- | --- | --- |
| **Cluster** | Ultra-Low | Lower (Single Rack) | No specific limit | HPC / Video Encoding |
| **Spread** | Normal | Maximum | 7 per AZ | Critical redundancy |
| **Partition** | Low | High (Isolated) | Hundreds | Big Data / Cassandra |

---

## 💡 Important "Rule of Thumb" for the Exam

* **Moving Instances:** You cannot move an *existing* instance into a placement group. You must create an Image (AMI) of the instance and then launch a new instance into the group.
* **Instance Types:** For Cluster placement groups, AWS recommends using the **same instance type** for all instances in the group to ensure the best performance.
* **Capacity Errors:** If you get an "Insufficient Capacity" error when launching a Cluster placement group, it means the rack is full. You’ll have to stop/start the instances or try a different AZ.

---

### 🧠 Quick Check

**Scenario:** You are designing a system for a genomic research firm that needs to process massive datasets across 50 nodes with the lowest possible latency between them. Which placement group do you choose?

**Answer:** **Cluster Placement Group.** Even though there are many nodes, the "lowest possible latency" requirement is the "Cluster" keyword.

---

## 🛠️ Key Attributes of an ENI

An **ENI (Elastic Network Interface)** is a logical networking component in a VPC that represents a virtual network card. 

Think of it as the "virtual NIC" you plug into your EC2 instance to give it a presence in the network.

An **ENI (Elastic Network Interface)** is a **virtual network card** in AWS that you attach to EC2 instances.

What it does:

* Provides **network connectivity** to an instance inside a VPC
* Has its own **private IP**, optional **public IP / Elastic IP**
* Has **security groups** attached to it (not to the instance directly)
* Can be **attached, detached, and moved** between EC2 instances

What it’s used for:

* **Multiple network interfaces** on one instance (multi-homed apps, firewalls)
* **High availability / failover** (move the ENI to another instance)
* **Traffic separation** (e.g. public vs private traffic)
* **Stable IP address** that survives instance replacement

Mental model:
**EC2 = server**, **ENI = network card you can unplug and move** 🔌


When you create an ENI, it includes:

* A **Primary Private IPv4** address from the IPv4 address range of your VPC.
* One or more **Secondary Private IPv4** addresses.
* One **Elastic IP (IPv4)** per private IPv4 address (optional).
* One **Public IPv4** address (optional).
* One or more **Security Groups**.
* A **MAC address**.

---

## 🚀 Why do we use ENIs? (Exam Use Cases)

### 1. Management Networks

You can create a dual-homed instance by attaching two ENIs from different subnets.

* **Use Case:** One ENI for public-facing traffic and a second "management" ENI in a private subnet for logging or administrative access.

### 2. Low-Budget High Availability (Failover)

Since an ENI is "elastic," you can detach it from one instance and attach it to another.

* **The Scenario:** If Instance A fails, you can move its ENI to Instance B.
* **The Result:** The network traffic (sent to the ENI's IP address) is immediately redirected to Instance B without needing to update DNS records.

### 3. Licensing

Some software licenses are tied to a specific MAC address. By using a specific ENI, you can maintain that MAC address even if you terminate and replace the underlying EC2 instance.

---

## 📊 ENI vs. ENA vs. EFA (The "Network" Confusion)

The exam might throw these three similar-sounding acronyms at you. Here is how to keep them straight:

| Feature | **ENI** (Network Interface) | **ENA** (Enhanced Networking) | **EFA** (Fabric Adapter) |
| --- | --- | --- | --- |
| **Best For** | Standard networking / Failover | Higher throughput (up to 100Gbps) | High-Performance Computing (HPC) |
| **Key Attribute** | Basic virtual NIC | Low CPU utilization / Consistent latency | Bypasses the OS kernel for speed |
| **Think of it as...** | A standard plug | A high-speed fiber cable | A direct "teleport" between nodes |

---

## ⚠️ Exam "Gotchas"

* **AZ Binding:** An ENI is tied to a specific **Availability Zone**. You cannot move an ENI from an instance in `us-east-1a` to an instance in `us-east-1b`.
* **The Primary ENI:** Every instance is created with a "Primary" ENI (`eth0`). You **cannot** detach the primary ENI from an instance. You can only attach/detach *secondary* ENIs.
* **Security Groups:** Security Groups are actually attached to the **ENI**, not the EC2 instance itself. This is a subtle but important distinction for troubleshooting.

---

### 🧠 Quick Concept Check

**Scenario:** You have a critical application where the license is tied to a specific IP and MAC address. The underlying hardware of your EC2 instance fails. How do you recover quickly?

**Answer:** Launch a new instance and **attach the existing ENI** from the failed instance to the new one. The new instance will inherit the licensed IP and MAC address.

---

# 🛠️ EBS Volumes

Look at  **EBS (Elastic Block Store)** as a "Network Drive" (like a virtual USB stick) that you can attach to your EC2 instances. Because it’s network-based, it persists independently of the instance's life cycle.

* **Locked to an AZ:** An EBS volume is created in a specific Availability Zone (e.g., `us-east-1a`). To move it to a different AZ, you must take a **Snapshot** and restore it in the new zone.
* **Network Latency:** Since it communicates with the EC2 instance over the network, there is a slight latency compared to "Instance Store" (physical disks).
* **Persistence:** By default, the **Root** volume (where the OS lives) is deleted when the instance is terminated, but you can toggle the "Delete on Termination" attribute to **No** to keep it.

---

## 📊 EBS Volume Types (The "Exam Favorite")

AWS categorizes EBS volumes into two main buckets: **SSD** (for small, fast I/O) and **HDD** (for large, sequential throughput).

| Volume Type | Name | Best For | Max Size / IOPS |
| --- | --- | --- | --- |
| **gp3 / gp2** (SSD) | General Purpose | System boots, virtual desktops, dev/test environments. | 16,000 IOPS |
| **io2 / io1** (SSD) | Provisioned IOPS | High-performance databases (Oracle, SAP HANA). | 64,000+ IOPS |
| **st1** (HDD) | Throughput Optimized | Big Data, Data Warehousing, Log processing. | 500 MB/s |
| **sc1** (HDD) | Cold HDD | Archives, infrequent access, lowest cost. | 250 MB/s |

> **Exam Tip:** You cannot use HDD volumes (**st1** or **sc1**) as **Boot Volumes**. Only SSDs can host the OS.

---

## 📸 Snapshots & Data Management

* **Snapshots:** Incremental backups. Only the blocks changed since the last snapshot are saved.
* **EBS Multi-Attach:** Available only on **io1/io2** volumes. This allows you to attach a single EBS volume to *multiple* instances simultaneously (must be in the same AZ).
* **Encryption:** When you encrypt an EBS volume, data at rest, data in transit (between instance and volume), and all resulting snapshots are automatically encrypted.

---

## ⚖️ EBS vs. Instance Store

This is a classic exam comparison.

* **EBS:** Durable, network-attached, survives instance stops/restarts. Think of it as **Long-term storage**.
* **Instance Store:** Physically attached to the host server. It is **Ephemeral** (if the instance stops, the data is **wiped**).
* **Use Case:** High-speed cache, buffer, or temporary data that is replicated elsewhere.



---

## 💡 Important "Rule of Thumb"

If the exam question mentions **"High performance"** + **"Relational Database,"** look for **Provisioned IOPS (io2)**.
If it mentions **"Lowest cost"** + **"Streaming large files,"** look for **Throughput Optimized (st1)**.

---

### 🧠 Quick Check

**Scenario:** You have a database that requires 20,000 IOPS. Which EBS volume type should you choose?

**Answer:** **io2 or io1 (Provisioned IOPS).** General Purpose (gp3) caps out at 16,000 IOPS, so you must use Provisioned IOPS to hit that higher threshold.

Since EBS is about storage, would you like to compare it to **EFS (Elastic File System)** next? EFS is the "Big Brother" that allows hundreds of instances to connect at once.
