# Day 6: Building Secure AWS Networks with VPC, Subnets, and Firewalls

## Introduction

In the world of AWS, every great application starts with a strong network foundation. On Day 6 of our journey, we take a step back from compute and storage and dig into what truly connects everything — the **Virtual Private Cloud (VPC)**. If you've ever wondered how data moves through AWS or how services stay secure, this is your answer.

Let's break it down from the ground up — from CIDRs and subnets to route tables and access controls — and by the end of this guide, you'll know how to build a secure, well-structured network inside AWS.

---

## What Is an Amazon VPC?

A **VPC** is a logically isolated virtual network in AWS that mimics a traditional data center but with cloud-native flexibility and scalability.

You can:
- Set your own IP address range
- Create public and private subnets
- Define custom routing
- Control traffic flow in and out of your resources

It's your cloud infrastructure's neighborhood — and you're the city planner.

---

## Understanding CIDR Blocks

CIDR (Classless Inter-Domain Routing) lets you define your VPC's IP space. Here's a quick primer:

- `10.0.0.0/16` gives you 65,536 IP addresses
- `10.0.1.0/24` gives you 256 IP addresses (used in subnets)

| CIDR Block | Number of IPs | Notes                   |
|------------|----------------|--------------------------|
| /28        | 16             | Small use cases or tests |
| /24        | 256            | Common subnet size       |
| /16        | 65,536         | Entire VPC address space |

*Reminder: AWS reserves 5 IPs in each subnet for internal use.*

---

## Subnets: Dividing Your Network

Subnets are chunks of your VPC's IP range that segment your infrastructure. You typically divide them by purpose and accessibility:

- **Public Subnet**: Connected to the internet
- **Private Subnet**: No direct internet access (used for databases, app servers, etc.)

Each subnet lives in one Availability Zone and must be tied to a route table.

---

## Route Tables: Navigating the Cloud Highway

A route table controls how traffic is routed within your VPC.

For example:
- A public subnet will route `0.0.0.0/0` traffic to the **Internet Gateway**
- A private subnet may route traffic to a NAT Gateway or stay isolated

You can customize routing behavior subnet by subnet, offering fine-grained control.

---

## Internet Gateway (IGW)

An **Internet Gateway** provides a path between your VPC and the public internet. It's:
- Horizontally scaled
- Highly available
- Required for internet-bound traffic

But alone, it doesn’t grant access — you must also configure routing and permissions properly.

---

## Security Groups: Instance-Level Shields

**Security Groups (SGs)** act like mini-firewalls attached to your EC2 instances.

- **Stateful**: Responses are allowed automatically
- Allow inbound/outbound rules only
- Cannot explicitly deny traffic

Typical SG rule:
- Allow SSH (TCP port 22) from a specific IP range
- Allow HTTP (TCP port 80) from anywhere

---

## Network ACLs (NACLs): Subnet-Level Guardians

**NACLs** provide a broader net of protection at the subnet level.

- **Stateless**: Return traffic must be explicitly allowed
- Allow and Deny rules available
- Rules evaluated in order (lowest number first)

| Feature         | Security Group | NACL          |
|----------------|----------------|---------------|
| Scope           | Instance       | Subnet        |
| Stateful        | Yes            | No            |
| Rule Types      | Allow only     | Allow & Deny  |

Best practice: don’t modify the default NACL — create a new one when you need custom rules.

---

## Bastion Host: Secure Access to Private Subnets

A **Bastion Host** is a secure EC2 instance in a public subnet that allows SSH access into private subnets.

Configuration:
- Security Group allows port 22 access from trusted IPs
- Private EC2 instances allow traffic from the Bastion’s SG or IP

---

## VPC Endpoints: Private Access to AWS Services

VPC Endpoints allow private connectivity to AWS services like S3 or DynamoDB without using the public internet.

- **Gateway Endpoints**: For S3 and DynamoDB
- **Interface Endpoints**: For other services, using ENIs in your subnet

Benefits:
- Enhanced security
- Reduced latency
- Lower data transfer costs

---

## VPC Peering: VPC-to-VPC Communication

VPC Peering connects two VPCs, enabling private IP communication.

- CIDR blocks must not overlap
- No transitive routing (A ↔ B and B ↔ C doesn’t imply A ↔ C)
- Manual route table updates are required

Great for inter-department or cross-account communication.

---

## VPC Flow Logs: Observe and Analyze

Flow Logs capture metadata about network traffic for analysis and auditing.

- Destination: S3 or CloudWatch
- Use tools like Athena or QuickSight for analytics
- Helps troubleshoot dropped packets or blocked connections

---

## Transit Gateway: Scalable VPC Interconnection

When you have many VPCs and on-prem environments to connect, **Transit Gateway** simplifies things with a hub-and-spoke model.

- Scales better than VPC Peering
- Centralized routing and management

---

## Conclusion

Today, you’ve laid the foundation for cloud security and traffic flow by mastering Amazon VPC. You've learned how to slice your IP space with CIDR, partition workloads with subnets, manage traffic using route tables, and protect your assets with SGs and NACLs.

But this is just the beginning. Good networking design is critical for resilience, security, and scalability.

---

### 🚀 Up Next: Day 7 – Amazon S3
We move from networking to **object storage** as we explore Amazon S3. You'll learn about storage classes, buckets, access permissions, and real-world use cases.

---

### 🔗 Useful Links

**📁 GitHub Repo — Join the Challenge**  
👉 [Road-to-AWS](https://github.com/Gaturu/Road-To-AWS)

**📖 Read Day 5 – ELB and Auto Scaling: Building for Scale and Resilience**  
👉 [Catch up on Day 5](https://awstip.com/load-balancing-and-auto-scaling-in-aws-building-for-scale-and-resilience-205232a79d36)

**👥 Let’s Connect on LinkedIn**  
🔗 [Duncan Gaturu](https://www.linkedin.com/in/duncangaturu/)

Stay inspired. Stay building. See you tomorrow!
