# Cloud Practitioner

# What is Cloud Computing

Cloud Computing refers to on demand delivery of IT resources with pay-as-you-go pricing model.

# Six Advantages of Cloud Computing

* Trade capital expense for variable expense
* Benefit from massive economies of scale
* Stop guessing capacity
* Increase speed and agility
* Stop spending money running and maintaining data centers
* Go global in minutes

# Global Infrastructure

* AWS Cloud infrastructure is built around AWS Regions and Availability Zones.
* An AWS Region is a physical location in the world. Each Amazon Region is designed to be completely isolated from the other Amazon Regions.
* AWS Region has multiple Availability Zones.
* Availability Zone consist of one or more discrete data centers, each with redundant power, networking, and connectivity, housed in separate facilities.
* Each Availability Zone is isolated, but the Availability Zones in a Region are connected through low-latency links.

# Amazon EC2 instance types

## General purpose instances 

provide a **balance** of compute, memory, and networking resources. You can use them for a variety of workloads, such as:

* Web servers
* Application servers
* Gaming servers
* Backend servers for enterprise applications
* Small and medium databases

## Compute optimized instances 

are ideal for **compute-bound applications** that benefit from **high-performance processors**.

* Batch processing workloads
* High performance web/app/gaming servers

## Memory optimized instances 

are designed to deliver fast performance for workloads that process **large datasets in memory**. 

* High-performance database (redis)
* Workload that involves performing real-time processing of a large amount of unstructured data.

## Accelerated computing instances 

use **hardware accelerators**

* Floating-point number calculations
* Graphics processing
* Data pattern matching.

## Storage optimized instances 

are designed for workloads that require **high, sequential read and write access to large datasets on local storage**. High IOPS requirement.

* Distributed file systems
* Data warehousing applications
* High-frequency online transaction processing (OLTP) systems.

# Amazon EC2 pricing

## On-Demand Instances

are ideal for short-term, irregular workloads that **cannot be interrupted**. Developing and testing applications.

## Reserved Instances 

are a **billing discount** applied to the use of On-Demand Instances in your account, for **1-year or 3-year term**.

**Standard Reserved Instances**: Good when you know exact **Number** of EC2 instnaces needed, Instance family type (M5), size (M5.xlarge), OS, Region
**Convertible Reserved Instances**: When you need to change AZ, Instance type, size etc.

## EC2 Instance Savings Plans 

reduce your EC2 instance costs when you make an **hourly spend commitment to an instance family (Ex: M5) and Region for a 1-year or 3-year term**. This term commitment results in savings of up to 72 percent compared to On-Demand rates.

You have the benefit of saving costs on running any EC2 instance within an EC2 instance family in a chosen Region (for example, M5 usage in N. Virginia) regardless of Availability Zone, instance size, OS, or tenancy. 

## Spot Instances 

are ideal for workloads with flexible start and end times, or that can **withstand interruptions** like background processing job. Spot Instances use unused Amazon EC2 computing capacity and offer you cost savings at up to 90% off of On-Demand prices.

## Dedicated Hosts 

are physical servers with Amazon EC2 instance capacity that is fully dedicated to your use. You can use existing software licenses.

# Amazon EC2 Auto Scaling 

Enables you to automatically add or remove Amazon EC2 instances in response to changing application demand.
This helps to scale-out to handle high traffic OR scale-in to save costs.
When you create an Auto Scaling group, you can set the **minimum, desired and maximum** number of Amazon EC2 instances

# Elastic Load Balancing

is the AWS service that acts as a single point of contact for all incoming application traffic and automatically distributes traffic across multiple resources, such as Amazon EC2 instances.

Elastic Load Balancing is a regional construct and automatically scalable and highly-avilable.

ELB works in combination with Auto-Scaling group. 
When your EC2 fleet **auto-scales out**, as each instance comes online, the auto-scaling service just lets the Elastic Load Balancing service know that it's ready to handle the traffic, and off it goes. 
Once the **fleet scales in**, ELB first stops all new traffic, and waits for the existing requests to complete, to drain out. Once they do that, then the auto-scaling engine can terminate the instances without disruption to existing customers.
