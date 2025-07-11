# Day 5: EC2 Auto Scaling & Load Balancing – Deep Dive

In today’s entry of our "Road to AWS Cloud" journey, we shift gears toward two of the most powerful components in AWS compute: **Elastic Load Balancing (ELB)** and **Auto Scaling Groups (ASG)**. These services are essential when it comes to distributing traffic intelligently and adapting automatically to changes in load.

Let’s break them down clearly and practically.

---

## What is Elastic Load Balancing?

**Elastic Load Balancing** is an AWS service that automatically routes incoming application traffic to multiple targets. These targets could be:
- EC2 instances
- ECS containers
- Lambda functions
- IP addresses

By spreading the load and managing unhealthy targets, ELB ensures that applications remain reliable and responsive.

---

## Why ELB Matters

Elastic Load Balancers are designed to:
- Evenly distribute traffic across compute resources
- Remove unresponsive targets using health checks
- Terminate SSL/TLS sessions securely
- Act as a single entry point using DNS
- Work across multiple Availability Zones
- Integrate easily with Auto Scaling Groups

This service eliminates the need to manually manage traffic flow or worry about single points of failure.

---

## Health Checks

Health checks are critical to ELB functionality. They continuously monitor each target using specified protocols and paths. If a target fails its checks, traffic is paused until it recovers. ELB supports checks using HTTP, HTTPS, or TCP depending on the balancer type.

---

## Load Balancer Types in AWS

### 1. Classic Load Balancer (CLB)
- Operates at the request and connection level
- Suitable for basic HTTP/HTTPS workloads
- Simple but lacks advanced routing features

### 2. Application Load Balancer (ALB)
- Works at Layer 7 (HTTP/HTTPS)
- Supports routing based on paths, hosts, headers, and more
- Ideal for web apps and microservices
- Integrates with ECS and Lambda

### 3. Network Load Balancer (NLB)
- Operates at Layer 4 (TCP/UDP/TLS)
- High performance for low latency applications
- Supports static IPs and preserves source IPs

### 4. Gateway Load Balancer (GWLB)
- Distributes traffic to third-party appliances
- Useful for firewalls and inspection tools
- Uses GENEVE protocol

---

## Target Groups & Listeners

**Listeners** are responsible for receiving incoming traffic. Each one is tied to a protocol and port. 

**Target Groups** define where that traffic goes. Targets can be instances, Lambda functions, containers, or IP addresses. Each group has its own health check configuration.

---

## Sticky Sessions

Sometimes, it's necessary for a user to always hit the same backend—especially when using in-memory sessions. ELB supports this with sticky sessions:
- Cookie or IP-based
- Session persistence with controlled expiration
- Available in CLB, ALB, and NLB

---

## Cross-Zone Load Balancing

When enabled, cross-zone balancing evenly distributes requests across all targets in all zones. Without it, requests are routed only to targets in the same AZ as the incoming request.

- On by default in ALB and CLB
- Optional (and configurable) in NLB

---

## SSL/TLS Support

ELB supports secure communications using SSL/TLS:
- Terminate SSL at the load balancer
- Manage certificates with AWS Certificate Manager (ACM)
- Host multiple HTTPS apps with SNI (Server Name Indication)

---

## Connection Draining (Deregistration Delay)

When targets are removed—during scale-down or maintenance—ELB allows in-flight requests to complete. This is called:
- **Connection Draining** in CLB
- **Deregistration Delay** in ALB and NLB

This helps ensure a smooth user experience without dropped connections.

---

## Practical Scenarios

1. **Web Frontend with Path Routing**  
   ALB sends `/api` requests to ECS and `/app` requests to EC2 instances.

2. **Real-time Traffic Handling**  
   NLB handles massive TCP/UDP flows with low latency.

3. **Security Appliance Integration**  
   GWLB routes outbound traffic through firewall appliances.

4. **Multi-Region or Hybrid Access**  
   Use ALB/NLB with IP targets to route across cloud and on-prem resources.

---

## Wrapping Up

Elastic Load Balancing is the backbone of reliable and responsive applications on AWS. It not only handles traffic, but also simplifies scaling, failure recovery, and secure access. When combined with Auto Scaling Groups, it becomes a powerful automation duo.

In our next post, we’ll move into the networking layer as we explore **Amazon VPC: Subnets, CIDR Blocks, and Route Tables**.

---

### 🔗 Resources

- **Join the Journey on GitHub**: [https://github.com/Road-to-AWS](https://github.com/Gaturu/Road-To-AWS)
- **Read Previous Day (EC2 Pricing & Templates)**: [Link to Day 4 Medium Post](https://medium.com/aws-tip/unlocking-aws-ec2-storage-a-complete-guide-to-ebs-efs-instance-store-526e74e8e06d)
- **Let’s Connect on LinkedIn**: [https://linkedin.com/](https://www.linkedin.com/in/duncangaturu/)

Stay tuned. More AWS discoveries ahead!
