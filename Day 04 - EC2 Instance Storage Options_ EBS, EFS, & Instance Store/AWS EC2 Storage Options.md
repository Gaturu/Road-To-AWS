# ☁️ Day 4: Understanding EC2 Storage – EBS, EFS & Instance Store

Welcome to Day 4 of the **Road to AWS Cloud & Certification** series!  
Today, we're turning our focus to the **storage layer of EC2**, the unsung hero behind reliability, speed, and data durability in the cloud.

AWS provides **three main storage types** for EC2:

- **Elastic Block Store (EBS)** – for block-level, persistent data
- **Elastic File System (EFS)** – for shared access across instances
- **Instance Store** – for fast, temporary storage that lives with the EC2 host

---

## 🟦 Amazon Elastic Block Store (EBS)

**EBS** is network-attached storage designed for use with a single EC2 instance at a time (unless using Multi-Attach with specific volume types). It allows your applications to store data even when the instance is stopped or rebooted.

### 🔍 EBS Highlights:
- Bound to a single AZ, but can be copied via snapshots
- Supports volume resizing and type changes without downtime
- Backup via **EBS Snapshots** (stored in S3)
- Can be encrypted at rest and in transit using **AWS KMS**
- **Delete on termination** can be toggled for root volumes

### 📦 Volume Types:
| Type     | Description                             |
|----------|-----------------------------------------|
| gp3/gp2  | General purpose, balanced performance   |
| io1/io2  | High-performance, provisioned IOPS      |
| st1      | Optimized for large, sequential workloads |
| sc1      | Cold storage, low cost, rare access     |

### 🔐 Extra Features:
- **Snapshots**: Used for backup and cross-AZ/Region restores
- **Multi-Attach (io1/io2)**: Allows sharing a volume with multiple EC2s
- **Fast Snapshot Restore**: Instant-ready volumes on restore
- **Snapshot Archive**: Low-cost archival backups

---

## 🟧 Amazon Elastic File System (EFS)

**EFS** provides a managed file storage solution that can be mounted across multiple EC2 instances simultaneously, making it ideal for shared access patterns and Linux-based workloads.

### 🔍 Key Traits:
- Scales automatically (no provisioning needed)
- Supports multiple AZs (high availability)
- POSIX-compliant file system
- Uses **NFSv4.1 protocol**
- Works only with **Linux** EC2 instances

### 🧊 Storage Classes:
| Tier              | When to Use                      |
|-------------------|----------------------------------|
| Standard          | Frequent access workloads        |
| Infrequent Access | Archive or cold data             |
| One-Zone IA       | Cheaper, less resilient storage  |

Lifecycle management can transition files across tiers based on age.

### 🛡️ Security:
- Data encryption using KMS
- Access control with **Security Groups & IAM**

---

## 🔘 EC2 Instance Store

**Instance Store** volumes are **physically attached** to the EC2 host. They offer exceptional performance but are **non-persistent** — meaning all data is lost when the instance is stopped or terminated.

### ⚙️ Characteristics:
- **Temporary storage**, bound to the EC2 lifecycle
- **Very high IOPS**, ideal for caching or temp data
- No snapshots or backups available
- Included at no cost with supported instance types (e.g., `i3`, `d2`, `c5d`)

### ⚡ Best Use Cases:
- Ephemeral compute tasks
- ETL buffer layers
- Scratch data or local cache

---

## 📊 Storage Comparison

| Feature              | EBS            | EFS                 | Instance Store        |
|----------------------|----------------|----------------------|------------------------|
| Durability           | Yes            | Yes                 | No (ephemeral)         |
| AZ/Region Scope      | AZ-bound       | Multi-AZ            | Tied to instance host  |
| Multi-Instance Access| No (except io1/2) | Yes              | No                    |
| Backup Support       | Snapshots      | N/A                 | Not available          |
| OS Support           | Linux & Windows| Linux only          | Instance-dependent     |
| Cost Model           | Per GB provisioned | Pay-per-usage   | Included in instance   |

---

## 🧠 Choosing the Right Storage

| Use Case                              | Recommended Option   |
|---------------------------------------|-----------------------|
| Boot volumes                          | EBS (gp3/gp2)         |
| Application data                      | EBS                   |
| Shared website content                | EFS                   |
| Linux-only file system sharing        | EFS                   |
| High IOPS for databases               | EBS (io2/io1)         |
| Temporary scratch or buffer space     | Instance Store        |
| Automatic scaling shared storage      | EFS                   |

---

## 🧩 Final Thoughts

Each of these storage solutions plays a distinct role in AWS architecture. Whether you're building for performance, durability, or speed, AWS lets you tailor your infrastructure to fit your needs — and that’s what cloud-native design is all about.

---

🎯 **Next Up – Day 5:**  
We’ll explore **Elastic Load Balancing (ELB)** and **Auto Scaling** — the magic that powers dynamic scaling and fault tolerance in the AWS cloud.

📖 **Blog version available here:** [Read on Medium](https://medium.com/@gaturugaturu/unlocking-aws-ec2-storage-a-complete-guide-to-ebs-efs-instance-store-526e74e8e06d)

📂 **Explore more or contribute:**  
[🔗 GitHub Repository: Road to AWS Cloud](https://github.com/Gaturu/Road-To-AWS)

