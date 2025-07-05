# 🔐 IAM – Identity and Access Management

Welcome to Day 3 of the **Road to AWS Cloud and Certification** Journey. Today, we dive deep into one of the most critical services in the AWS ecosystem: **Amazon EC2 (Elastic Compute Cloud)**. This powerful service forms the compute layer of AWS and allows you to provision **virtual servers** to run your applications seamlessly.


## DAY 3: AWS EC2 Instance Types and Use Cases
---

## What is AWS EC2?
**Amazon EC2** is a web service that provides secure, resizable compute capacity in the cloud. With this service, you can provision virtual servers called EC2 instances
In simpler terms an EC2 instance is a virtual machine (VM) that runs in the AWS Cloud.
These instances can run everything from simple web apps to complex, distributed, high-performance systems.

# EC2 Instance Types
---

When working with EC2, one of the most important decisions you'll make is choosing the right instance type. Think of it as picking the perfect engine for your vehicle — some engines are designed for speed, others for hauling data, and some strike a balance between all.

EC2 instance types are grouped into instance families, each tailored to meet specific performance needs. 

Let’s explore the main families:

## General Purpose Instances
These instances are your go-to for most day-to-day workloads. They offer a balanced mix of **compute**, **memory**, and **networking**, making them versatile for a wide range of applications.

📌 Best For:

* Web servers

* Development environments

* Microservices

**Tip**: If you're unsure where to start, general purpose instances (like t3, t4g, or m6g) are a safe and flexible choice.

## Compute Optimized Instances
These are designed for applications that need a **high-performance CPU**. If your workload is compute-bound — meaning it heavily relies on processing power — this is where you’ll want to look.

📌 Best For:

Scientific modeling

* High-performance computing (HPC)

* Batch processing

*  Media transcoding

* Ad serving and game servers

**Example Instances**: Belong to the c family (e.g., c6g, c7i)


## Memory Optimized Instances
Memory optimized instances are built to handle large datasets in-memory with blazing speed. They’re perfect for applications that need more RAM than compute power.

📌 Best For:

* In-memory databases like Redis or Memcached

* Real-time big data analytics

* High-performance relational databases


**Instances**: Typically fall under r, x, or u families.

# Storage Optimized Instances 
These instances are ideal when dealing with massive volumes of data that need to be written or read quickly and sequentially from local storage.

📌 Best For:

* Data warehousing

* Large transactional databases

* Log processing and analytics

* Distributed file systems

**Instances**: Fall under i, d, and h families. Known for delivering tens of thousands of low-latency IOPS.


## Accelerated Computing Instances
When CPUs aren’t enough, these instances bring in hardware accelerators like GPUs and FPGAs to handle graphics rendering, machine learning inference, and complex mathematical computations with lightning speed.

📌 Best For:

* Machine learning training and inference

* 3D rendering and video encoding

* Genomics and computational finance

* Pattern recognition

**Instances**: Include families like g, p, and f.


# EC2 Pricing Options – Paying Smart in the Cloud
---

One of the things that sets AWS apart is the **flexibility** of how you pay for the resources you use. With Amazon EC2, you’re not locked into a single model — instead, AWS offers multiple pricing options, each designed to match your workload patterns, business needs, and budget.

**Let’s break them down so you can make informed decisions as you build in the cloud**.

## On-Demand Instances – Pay As You Go
This is the simplest pricing model — perfect for when your workload is **short-term, unpredictable, or still in development**.

🔹 No long-term commitment
🔹 No upfront payment
🔹 Billed per second, which means you're only paying for exactly what you use

**Use Case**: Testing environments, temporary workloads, or when you're unsure how your application will behave under load.

**Pro Tip**: Great for agility, not for cost savings. If your workload is long-running or predictable, consider Reserved Instances or Savings Plans.

# Reserved Instances (RIs) – Commit to Save
**Reserved Instances** are all about planning ahead. You commit to using a specific instance type in a specific region for **1 or 3 years**, and in return, AWS gives you with up to **72% discount** compared to **On-Demand prices**.

💳 You can choose from:

No Upfront – Pay monthly, no upfront cost

Partial Upfront – Pay some upfront, get better savings

All Upfront – Pay it all at once for the biggest discount

**Use Case**: Production workloads running 24/7, predictable usage patterns


# Convertible Reserved Instances – Flex with Certainty
Convertible RIs are like regular Reserved Instances, but more flexible. They allow you to change instance attributes — such as instance type, family, OS, tenancy, or scope — while still benefiting from long-term pricing.

📉 Discount: Up to 66% off compared to On-Demand

✅ Use Case: Long-running workloads that may evolve over time (e.g., migrate from Intel to Graviton, or Linux to Windows)

# Savings Plans – Commit by Dollar, Not Instance
This is one of the most modern and flexible pricing models. Instead of committing to a specific instance type, you commit to a specific amount of **compute usage in dollars per hour (e.g., $10/hour) for 1 or 3 years**.

**In return, you can run any EC2 instance type — even across families or regions — and still enjoy savings of up to 72%.**

✅ Use Case: Dynamic environments using a mix of instance types, or those using multiple compute services like EC2, Fargate, and Lambda.

# Spot Instances – Deep Discounts, but Risky
Spot Instances let you tap into **AWS’s unused capacity** — at discounts of up to **90% compared to On-Demand**.

**But there’s a catch**: you can **lose** the instance at any moment when **AWS reclaims capacity**. Think of it like a bidding war — if your bid falls below the current spot price, the instance disappears.

⚠️ Not ideal for critical, long-running apps.

**Use Case**: Fault-tolerant jobs like big data processing, CI/CD pipelines, batch jobs, or dev/test environments.

**Tip**: Use Spot Fleet or Auto Scaling with mixed instance types for better reliability.

# Dedicated Hosts – Full Control, Full Compliance
**Need physical isolation for licensing or compliance reasons?** A Dedicated Host gives you an entire physical server — reserved just for you.

You control instance placement and can bring your own server-bound software licenses.

💸 It’s the most expensive EC2 pricing option.

**Use Case**: Compliance-heavy workloads, strict licensing requirements, or regulated industries

**Purchase Options**: Available as On-Demand or Reserved

# Dedicated Instances – Isolation Without Full Host Control
Unlike Dedicated Hosts, Dedicated Instances still run on hardware that’s exclusive to you, but you don’t control where they’re placed on the host.

**Use Case**: When you need instance-level isolation without managing the underlying host.

