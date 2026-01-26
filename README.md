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

### how to choose an AWS Region ?

 If you need to launch a new app, where to do it ? Take into account:

 - Compliance (data governance and legal requirements: f.example: data must never leave a region without explicit permission)

 - Proximity to customers : reduced latency

 - Available services within a Region: new services and new features aren't available in every Region.

 - Pricing: prices varies from region to region and is transparent in the service pricing page.


### AWS Availability Zones

Each region has many availability zones ( min : 3, max : 6)

Each Availability Zone (AZ) is one or more discrete data center with redudant power, networking and connectivity.

They are separated from each other, so that they're isolated from disasters.


### AWS Point of Presence (Edge Locations)

- Amazon has 400+ points of presence (400+ Edge locations & 10+ Regional Caches) in 90+ cities across 40+ countries.

- 
