# Cloud Practitioner

# What is Cloud Computing

Cloud Computing refers to on demand delivery of IT resources with pay-as-you-go pricing model.

<br>

# Six Advantages of Cloud Computing

* Trade capital expense for variable expense
* Benefit from massive economies of scale
* Stop guessing capacity
* Increase speed and agility
* Stop spending money running and maintaining data centers
* Go global in minutes

<br>

# AWS Global Infrastructure

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

<br>

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

## Elastic Load Balancing

is the AWS service that acts as a single point of contact for all incoming application traffic and automatically distributes traffic across multiple resources, such as Amazon EC2 instances.

Elastic Load Balancing is a regional construct and automatically scalable and highly-avilable.

ELB works in combination with Auto-Scaling group. 
When your EC2 fleet **auto-scales out**, as each instance comes online, the auto-scaling service just lets the Elastic Load Balancing service know that it's ready to handle the traffic, and off it goes. 
Once the **fleet scales in**, ELB first stops all new traffic, and waits for the existing requests to complete, to drain out. Once they do that, then the auto-scaling engine can terminate the instances without disruption to existing customers.

<br>

# AWS VPC (Virtual Private Cloud)

* **VPC**, or Virtual Private Cloud, is essentially your own private network in AWS, an isolated boundary from other customers in same AWS Cloud. VPC allows you to define your **private IP range** for your resources to be deployed.

### Structuring VPC

* **Subnets**. Within a virtual private cloud (VPC), you can **organize** your resources into subnets. Subnets are **chunks** of IP addresses in your VPC that allow you to group resources together.

You deploy Public and Private Subnets. 
* Public subnets contain resources that need to be accessible by the public over the internet, such as an online store’s website.
* Private subnets contain resources that should be accessible only through your private network, such as a APIs / Database that contains customers’ personal information and order histories.

### Connecting to VPC

* VPC is private by default with no doors opened yet. So you can deploy resources in there, but cannot access them from anywhere.
* So you need to open-up the doors, lets see how.

#### Public resources and Internet Gateway

In order to allow traffic from the public internet to flow into and out of your VPC, you must attach what is called an **internet gateway**, or IGW, to your VPC. 
Internet Gateway is like Front-Door of your Coffee-Shop which is open for all customers.

#### Private resources and Virtual Private Gateway

Create VPN Connection (Encyrpted, Protected) between your internal corporate network (data center) and VPC.

* VPC deploys some private resources which we do not want anyone to access from public internet, but we want to allow **few trusted people** like employees, partners, software-programs to be able to access them.
* The virtual private gateway is the component that allows **protected internet traffic** to enter into the VPC, only if they are coming from approved network in an encrypted manner.
* It allows you to create a VPN connection between a private network, like your on-premises data center or internal corporate network to your VPC. This VPN connection is over internet but **encrypted**.
* Jump Host should also be deployed and accessed using these Private Connection and not using Public IPs.

#### AWS Direct Connect

Create **completely private, dedicated fiber connection** from your data center to AWS. So traffic does not go over internet and you get lowest possible latency with needed security compliance and no bandwidth issues.

### Securing VPC resources

#### NACL

A network ACL is a virtual firewall that controls inbound and outbound traffic at the subnet level.

* Each AWS account includes a default network ACL which allows all inbound and outbound traffic, but you can modify it by adding your own rules.
* When configuring your VPC, you can use your account’s default network ACL or create custom network ACLs (recommended).
* Custom NACL creation is recomendded and it will by default have an explicit deny rule (like app NACLs). So all inbound and outbound traffic is denied until you add rules to specify which traffic to allow.
* Network ACLs perform stateless packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound.

#### Security groups

A security group is a virtual firewall that controls inbound and outbound traffic to Amazon EC2 instance.

https://aws.amazon.com/products/networking/

<br>

# AWS Storage


