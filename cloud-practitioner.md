# Cloud Practitioner

<br>

# What is Cloud Computing

Cloud Computing refers to on demand delivery of IT resources with pay-as-you-go pricing model.

<br><br>

# Six Advantages of Cloud Computing

* Trade capital expense for variable expense
* Benefit from massive economies of scale
* Stop guessing capacity
* Increase speed and agility
* Stop spending money running and maintaining data centers
* Go global in minutes

<br><br>

# AWS Global Infrastructure

### Overview

* AWS Cloud infrastructure is built around AWS Regions and Availability Zones.
* An AWS Region is a physical location in the world. Each Amazon Region is designed to be completely isolated from the other Amazon Regions.
* AWS Region has multiple Availability Zones.
* Availability Zone consist of one or more discrete data centers, each with redundant power, networking, and connectivity, housed in separate facilities.
* Each Availability Zone is isolated, but the Availability Zones in a Region are connected through low-latency links.

### Choosing AWS Region based on 4 business factors

1. **Complaince with data governance and legal requirements** - For example, if your company requires all of its data to reside within the boundaries of the UK, you would choose the London Region. 
2. **Proximity to your customers** - Select region that is close to your customers. If most of your customers live in Singapore, consider running out of the Singapore Region.
3. **Feature Availability** - Let's say your developers wanted to play with our new quantum computing platform. Well then, they have to run in the Regions that already have the hardware installed.
4. **Pricing** - Even when the hardware is equal in all regions, some locations are just more expensive to operate in.

### Avalability Zones

An Availability Zone is a single data center or a group of data centers within a Region. Availability Zones are located tens of miles apart from each other. This is close enough to have low latency (the time between when content requested and received) between Availability Zones. However, if a disaster occurs in one part of the Region, they are distant enough to reduce the chance that multiple Availability Zones are affected.

The Northern California Region is called us-west-1, and this Region contains three AZs (1a, 1b, and 1c). Then, within each AZ there are three data centers.

<br><br>

# Amazon EC2

Secure and resizable compute capacity for virtually any workload in AWS cloud.

## Amazon EC2 instance types

### General purpose instances 

provide a **balance** of compute, memory, and networking resources. You can use them for a variety of workloads, such as:

* Web servers
* Application servers
* Gaming servers
* Backend servers for enterprise applications
* Small and medium databases

### Compute optimized instances 

are ideal for **compute-bound applications** that benefit from **high-performance processors**.

* Batch processing workloads
* High performance web/app/gaming servers

### Memory optimized instances 

are designed to deliver fast performance for workloads that process **large datasets in memory**. 

* High-performance database (redis)
* Workload that involves performing real-time processing of a large amount of unstructured data.

### Accelerated computing instances 

use **hardware accelerators**

* Floating-point number calculations
* Graphics processing
* Data pattern matching.

### Storage optimized instances 

are designed for workloads that require **high, sequential read and write access to large datasets on local storage**. High IOPS requirement.

* Distributed file systems
* Data warehousing applications
* High-frequency online transaction processing (OLTP) systems.

<br>

## Amazon EC2 pricing

### On-Demand Instances

are ideal for short-term, irregular workloads that **cannot be interrupted**. Developing and testing applications.

### Reserved Instances 

are a **billing discount** applied to the use of On-Demand Instances in your account, for **1-year or 3-year term**.

**Standard Reserved Instances**: Good when you know exact **Number** of EC2 instnaces needed, Instance family type (M5), size (M5.xlarge), OS, Region
**Convertible Reserved Instances**: When you need to change AZ, Instance type, size etc.

### EC2 Instance Savings Plans 

reduce your EC2 instance costs when you make an **hourly spend commitment to an instance family (Ex: M5) and Region for a 1-year or 3-year term**. This term commitment results in savings of up to 72 percent compared to On-Demand rates.

You have the benefit of saving costs on running any EC2 instance within an EC2 instance family in a chosen Region (for example, M5 usage in N. Virginia) regardless of Availability Zone, instance size, OS, or tenancy. 

### Spot Instances 

are ideal for workloads with flexible start and end times, or that can **withstand interruptions** like background processing job. Spot Instances use unused Amazon EC2 computing capacity and offer you cost savings at up to 90% off of On-Demand prices.

### Dedicated Hosts 

are physical servers with Amazon EC2 instance capacity that is fully dedicated to your use. You can use existing software licenses.

<br>

## Amazon EC2 Auto Scaling 

Enables you to automatically add or remove Amazon EC2 instances in response to changing application demand.
This helps to scale-out to handle high traffic OR scale-in to save costs.
When you create an Auto Scaling group, you can set the **minimum, desired and maximum** number of Amazon EC2 instances

<br>

## Elastic Load Balancing

is the AWS service that acts as a single point of contact for all incoming application traffic and automatically distributes traffic across multiple resources, such as Amazon EC2 instances.

Elastic Load Balancing is a regional construct and automatically scalable and highly-avilable.

ELB works in combination with Auto-Scaling group. 
When your EC2 fleet **auto-scales out**, as each instance comes online, the auto-scaling service just lets the Elastic Load Balancing service know that it's ready to handle the traffic, and off it goes. 
Once the **fleet scales in**, ELB first stops all new traffic, and waits for the existing requests to complete, to drain out. Once they do that, then the auto-scaling engine can terminate the instances without disruption to existing customers.

<br><br>

# AWS VPC (Virtual Private Cloud)

* **VPC**, or Virtual Private Cloud, is essentially your own private network in AWS, an isolated boundary from other customers in same AWS Cloud. VPC allows you to define your **private IP range** for your resources to be deployed.

## Structuring VPC

* **Subnets**. Within a virtual private cloud (VPC), you can **organize** your resources into subnets. Subnets are **chunks** of IP addresses in your VPC that allow you to group resources together.

You deploy Public and Private Subnets. 
* Public subnets contain resources that need to be accessible by the public over the internet, such as an online store’s website.
* Private subnets contain resources that should be accessible only through your private network, such as a APIs / Database that contains customers’ personal information and order histories.

## Connecting to VPC

* VPC is private by default with no doors opened yet. So you can deploy resources in there, but cannot access them from anywhere.
* So you need to open-up the doors, lets see how.

### Public resources and Internet Gateway

In order to allow traffic from the public internet to flow into and out of your VPC, you must attach what is called an **internet gateway**, or IGW, to your VPC. 
Internet Gateway is like Front-Door of your Coffee-Shop which is open for all customers.

### Private resources and Virtual Private Gateway

Create VPN Connection (Encyrpted, Protected) between your internal corporate network (data center) and VPC.

* VPC deploys some private resources which we do not want anyone to access from public internet, but we want to allow **few trusted people** like employees, partners, software-programs to be able to access them.
* The virtual private gateway is the component that allows **protected internet traffic** to enter into the VPC, only if they are coming from approved network in an encrypted manner.
* It allows you to create a VPN connection between a private network, like your on-premises data center or internal corporate network to your VPC. This VPN connection is over internet but **encrypted**.
* Jump Host should also be deployed and accessed using these Private Connection and not using Public IPs.

### AWS Direct Connect

Create **completely private, dedicated fiber connection** from your data center to AWS. So traffic does not go over internet and you get lowest possible latency with needed security compliance and no bandwidth issues.

## Securing VPC resources

### NACL

A network ACL is a virtual firewall that controls inbound and outbound traffic at the subnet level.

* Each AWS account includes a default network ACL which allows all inbound and outbound traffic, but you can modify it by adding your own rules.
* When configuring your VPC, you can use your account’s default network ACL or create custom network ACLs (recommended).
* Custom NACL creation is recomendded and it will by default have an explicit deny rule (like app NACLs). So all inbound and outbound traffic is denied until you add rules to specify which traffic to allow.
* Network ACLs perform stateless packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound.

### Security groups

A security group is a virtual firewall that controls inbound and outbound traffic to Amazon EC2 instance.

https://aws.amazon.com/products/networking/

<br><br>

# AWS Storage

## AWS EBS

* Amazon EBS volumes are attached to EC2 instances.
* EBS is Avalability Zone level resource. EBS stores data in single Avalability Zone.
* To attach Amazon EC2 instances to an EBS volumme, both must reside in same Avalability Zone.
* It's a hard drive.
* You can save files on it. 
* You can also run a **database** on top of it. 
* Or store applications on it. 
* If you provision a two terabyte EBS volume and fill it up, it doesn't automatically scale to give you more storage.

<br>

## AWS EFS

EFS is a scalable file system used with AWS Cloud services and on-premises resources.

* It is a true file system not just Hard-Drive that you attach to EC2.
* Multiple clients / applications / EC2 instances can read/write data stored in shared file system through file paths.
* Its a regional resource. It stores data across multiple Avlability Zones.
* As you add and remove files, Amazon EFS grows and shrinks automatically. It can scale on demand to petabytes without disrupting applications. No need to provision any more volumes.

EBS VS EFS

https://aws.amazon.com/efs/when-to-choose-efs/
https://cloudnativenow.com/topics/cloudnativenetworking/using-ebs-and-efs-as-persistent-volume-in-kubernetes/#:~:text=EBS%20vs.,EFS&text=Amazon%20EFS%20provides%20a%20shared,to%20a%20dedicated%20storage%20volume.

## AWS S3

* AWS S3 is a service that provides object-level storage. Amazon S3 stores data as objects in buckets.
* You can upload any type of file to Amazon S3, such as images, videos, text files, and so on. 
* Amazon S3 offers unlimited storage space. 
* The maximum file size for an object in Amazon S3 is 5 TB.

S3 Standard has a 99.999999999 percent avilability.
Data is stored in 3 AZs.

### S3 General Purpose Storage

#### S3 Standard

* Designed for frequently accessed data
* Stores data in a minimum of three Availability Zones
* Websites, content distribution, and data analytics
* Higher Cost

#### S3 Standard-Infrequent Access or S3 Standard-IA

* Ideal for infrequently accessed data but requires rapid access
* Stores data in a minimum of three Availability Zones
* Perfect place to store backups, disaster recovery files, or any object that requires long-term storage. 
* Similar to Amazon S3 Standard but has a lower storage price and higher retrieval price

#### S3 OneZone-Infrequent Access or S3 OneZone-IA

* Stores data in a single Availability Zone
* Has a lower storage price than Amazon S3 Standard-IA

Compared to S3 Standard and S3 Standard-IA, which store data in a minimum of three Availability Zones, S3 One Zone-IA stores data in a single Availability Zone. 

This makes it a good storage class to consider if the following conditions apply:
* You want to save costs on storage.
* You can easily reproduce your data in the event of an Availability Zone failure.


#### S3 Intelligent-Tiering

* Ideal for data with unknown or changing access patterns
* Requires a small monthly monitoring and automation fee per object

In the S3 Intelligent-Tiering storage class, Amazon S3 monitors objects’ access patterns. If you haven’t accessed an object for 30 consecutive days, Amazon S3 automatically moves it to the infrequent access tier, S3 Standard-IA. If you access an object in the infrequent access tier, Amazon S3 automatically moves it to the frequent access tier, S3 Standard.

<br>

### S3 Glacier

Archive data for Auditing purpose for several years.

#### S3 Glacier Instant Retrieval

* Works well for archived data that requires immediate access
* Can retrieve objects within a **few milliseconds**
  
#### S3 Glacier Flexible Retrieval

* Low-cost storage designed for data archiving
* Able to retrieve objects within a **few minutes to hours**
* low-cost storage solution for archival

Upload objects directly to S3 Glacier Flexible Retrieval or using S3 Lifecycle policies.

#### S3 Glacier Instant Deep Archive

* Lowest-cost object storage class ideal for archiving
* Data retrieval from **12 to 48 hours.**

## 3S3 Outposts

Creates S3 buckets on Amazon S3 Outposts

#### S3 Lifecycle Policies

Policies that you can create to move data automatically between tiers. For example, say we need to keep an object in S3 Standard for 90 days, and then we want to move it to S3 Standard-IA for the next 30 days. Then after 120 days total, we want to move it to S3 Glacier Flexible Retrieval. With Lifecycle policies, you create that configuration without changing your application code, and it will perform those moves for you automatically. It's another example of a managed AWS service, helping take that burden off you, so you can focus more on your business needs. 

<br><br>

# Amazon RDS

Automated patching, backups, redundancy, failover, disaster recovery, encryption at rest and in transit.

### HA, Automatic fail-over, Multi-AZ deployments and scalability

There are 2 types of deployment possible in RDS.

**Multi-AZ DB instance deployment** - has **one** standby DB instance that provides failover support, but doesn't serve read traffic.

In a Multi-AZ DB instance deployment, Amazon RDS automatically provisions and maintains a synchronous standby replica in a different Availability Zone.
The primary DB instance is synchronously replicated across Availability Zones to a standby replica to provide data redundancy and minimize latency spikes during system backups. 

**Multi-AZ DB cluster deployment** has **two** standby DB instances that provide failover support and can also serve read traffic.

A Multi-AZ DB cluster deployment is a **semisynchronous**, high availability deployment mode of Amazon RDS with two readable standby DB instances.

A Multi-AZ DB cluster has **1 writer DB instance and 2 reader DB instances** in three separate Availability Zones in the same AWS Region.

With a Multi-AZ DB cluster, Amazon RDS replicates data from the writer DB instance to both of the reader DB instances using the DB engine's native replication capabilities.

https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/multi-az-db-clusters-concepts.html
https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PIOPS.StorageTypes.html#USER_PIOPS.UpgradeFileSystem

https://aws.amazon.com/getting-started/decision-guides/

https://aws.amazon.com/architecture


# AWS Monitoring

### Mintoring Overview

* Collecting metrics, evaluating those metrics over time, and then using them to make decisions or take actions, is what we call monitoring. 
* Gain visibility across your applications, infrastructure, and services.

Example, if an EC2 instance is being over-utilized, you can trigger a scaling event that automatically would launch another EC2 instance.
If an application starts sending error responses at an unusually high rate, you can alert an employee to go take a look at what's going on.

### CloudWatch

**CloudWatch** is a service that enables you to monitor and manage various metrics and configure alarm actions based on data from those metrics.
**CloudWatch Alarm**: You set a threshold for a metric, and when that threshold is reached CloudWatch can generate an alert and trigger an action.
**CloudWatch Dashboard** enables you to access all the metrics for your resources from a single location.

### CloudTrail

**Cloud Trail** is a service that records API calls for your account. What, Who, When, How.
**CloudTrail Insights**: This optional feature allows CloudTrail to automatically detect unusual API activities in your AWS account. 

### AWS Trusted Advisor

AWS has an automated advisor called AWS Trusted Advisor.

AWS Trusted Advisor is a service inspects resources in your AWS environment against five pillars and provides real-time recommendations in accordance with AWS best practices.
The pillars are cost optimization, performance, security, fault tolerance, and service limits.
Trusted Advisor in real time runs through a series of checks for each pillar in your account, based on AWS best practices, and it compiles categorized items for you to look into, and you can view them directly in the AWS console.

Some checks are free and are included in your AWS account, and others are available depending on the level of your support plan. 

* if you don't have multi-factor authentication turned on for your root user, it's going to let you know.
* If you have underutilized EC2 instances that might be able to be turned off in order to save money.
* If you have EBS volumes that haven't been backed up in a reasonable amount of time, it will let you know that, too.


# AWS Support Plans

### Basic

* Contact AWS for billing questions and service limit increases.
* Limited selection of AWS Trusted Advisor checks.

### Developer

* Best practice guidance
* Client-side diagnostic tools
* Building-block architecture support, which consists of guidance for how to use AWS offerings, features, and services together

### Business

* Use-case guidance to identify AWS offerings, features, and services that can best support your specific needs
* All AWS Trusted Advisor checks
* Limited support for third-party software, such as common operating systems and application stack components

### Enterprise On-Ramp

* A **pool** of Technical Account Managers to provide proactive guidance and coordinate access to programs and AWS experts. Proactive support services, which are provided by a pool of Technical Account Managers.

  * Consultative review and architecture guidance (one per year)
  * Infrastructure Event Management support (one per year)
  * Support automation workflows
  * 30 minutes or less response time for business-critical issues

* A Cost Optimization workshop (one per year)
* A Concierge support team for billing and account assistance
* Tools to monitor costs and performance through Trusted Advisor and Health API/Dashboard

### Enterprise

* A **designated** Technical Account Manager to provide proactive guidance and coordinate access to programs and AWS experts Proactive services, which are provided by a designated Technical Account Manager:

  * Consultative review and architecture guidance
  * Infrastructure Event Management support
  * Cost Optimization Workshop and tools
  * Support automation workflows
  * 15 minutes or less response time for business-critical issues

* Operations Reviews and tools to monitor health
* Training and Game Days to drive innovation
* A Concierge support team for billing and account assistance
* Tools to monitor costs and performance through Trusted Advisor and Health API/Dashboard

# AWS Cloud Adoption Framework

# AWS Cloud Migration Strategies

Six possible options when it comes to enterprise migration to cloud which is known as six R's.
Once you've gone through the discovery phase and know exactly what you have in your existing environment, you decide which option among the six R's is the best fit based on time, cost, priority, criticality. 

### Rehosting

* Rehosting also known as “lift-and-shift” involves moving applications without changes. 
* Customers save cost and can scale quickly.

### Replatforming

* Replatforming, also known as “lift, tinker, and shift,” involves making a **few cloud optimizations** to realize a tangible benefit.
* Optimization is achieved without changing the core architecture of the application.
* Migrate existing MySQL database and replatform it onto RDS MySQL / Aurora, without any code changes at all.

### Refactoring/re-architecting

* Refactoring (also known as re-architecting) involves reimagining how an application is architected and developed by using cloud-native features. 
* Use case is to Innovate faster, add new features, cloud scale, or improve performance, better resiliency.

### Repurchasing

* Repurchasing involves moving from a traditional license to a software-as-a-service model. 
* For example, a business might choose to implement the repurchasing strategy by migrating from a customer relationship management (CRM) system to Salesforce.com.

### Retaining

* Retaining consists of keeping applications that are critical for the business in the source environment. 
* This might include applications that require major refactoring before they can be migrated, or, work that can be postponed until a later time.

### Retiring
Retiring is the process of removing applications that are no longer needed.


<br><br>

# AWS Well-Architected Framework

Operational excellence
Security
Reliability
Performance efficiency
Cost optimization
Sustainability
