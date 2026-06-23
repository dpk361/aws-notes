---
title: AWS Notes
nav_order: 1
---

# AWS Server-End Learning Roadmap for Backend Engineers

When diving into Amazon Web Services (AWS) from a backend and infrastructure engineering perspective, the sheer volume of services can be overwhelming. This guide outlines the essential "server-end" primitives you must master first, structured from core virtual machines to networking, scaling, and modern container-based deployments.

---

## Roadmap Overview
1. **Core Compute (EC2)**: Virtual machines and underlying storage.
2. **Access & Security (IAM & Security Groups)**: The gatekeepers of cloud infrastructure.
3. **Cloud Networking (VPC Essentials)**: Isolating and connecting your servers.
4. **Availability & Scaling (ELB & ASG)**: Handling traffic and high availability.
5. **Modern Container Infrastructure (ECS & Fargate)**: Shifting from VMs to microservices.

---

## 1. Core Compute: Amazon EC2 (Elastic Compute Cloud)
EC2 is the fundamental building block of AWS infrastructure. Understanding how EC2 operates teaches you the basics of cloud virtualization, lifecycle states, and resource allocation.

### Key Concepts to Master:
* **AMI (Amazon Machine Image):** Pre-configured templates containing the Operating System (e.g., Amazon Linux, Ubuntu) and initial software packages.
* **Instance Types:** Understanding the naming conventions (e.g., `t2.micro`, `m5.large`). For learning, stick to the **Free Tier** burstable performance instances (`t2.micro` or `t3.micro`).
* **EBS (Elastic Block Store):** The virtual hard drives attached to your EC2 instances. Learn the difference between:
  * **Root Volumes:** Where the operating system is installed (cleared on instance termination unless configured otherwise).
  * **Data Volumes:** Persistent block storage mounted for application data, logs, or databases.
* **Key Pairs:** Using asymmetric cryptography (SSH `.pem` or `.ppk` files) to securely connect to your Linux backend servers.

---

## 2. Cloud Security & Infrastructure Access
A server is only as good as its security posture. AWS follows a *Zero Trust* philosophy where everything is locked down by default.

### Key Concepts to Master:
* **Security Groups (Stateful Firewalls):** These operate at the instance level. You must learn how to configure:
  * **Inbound Rules:** Allowing traffic from specific ports and IP ranges. 
    * *Example:* Port `22` (SSH) restricted to your personal IP, Port `80`/`443` (HTTP/HTTPS) open to the world, and Port `8080` (Java/Spring Boot default) open for application testing.
  * **Outbound Rules:** Controlling what traffic your server can send out (default is wide open).
* **IAM (Identity and Access Management) Roles for EC2:** **Never** hardcode AWS access keys inside your backend application properties or codebase. Instead, master **IAM Roles**. You attach a role directly to the EC2 instance, allowing your running application code to seamlessly and securely communicate with other AWS services (like Amazon S3 or Parameter Store) using temporary tokens.

---

## 3. Basic Cloud Networking: VPC (Virtual Private Cloud) Essentials
You do not need to become a network engineer immediately, but you must understand how backend components are isolated.

| Component | Purpose | Target Use Case |
| :--- | :--- | :--- |
| **Public Subnet** | Has a direct route to an Internet Gateway. Accessible from the outside world. | Application Load Balancers, Public Web API Gateways. |
| **Private Subnet** | No direct inbound route from the internet. Completely isolated internally. | Backend Microservices, Core Databases (RDS), Cache Clusters. |
| **Elastic IP (EIP)** | A static, public IPv4 address allocated to your AWS account. | Keeping a fixed IP for a server that needs to survive stops, starts, or re-allocations. |

---

## 4. High Availability & Horizontal Scaling
Once you can run a single server, you must learn how production applications distribute traffic and scale elastically.

* **Application Load Balancers (ALB):** Operates at Layer 7 (Application Layer) of the OSI model. It acts as a reverse proxy, inspecting incoming HTTP/HTTPS traffic and routing it across a pool of target EC2 instances based on path routing rules (e.g., `/api/v1/users` goes to Server Group A).
* **Auto Scaling Groups (ASG):** Eliminates manual capacity provisioning. You define a *Launch Template* (which AMI, instance type, and security group to use) and scaling policies (e.g., *"If average CPU utilization exceeds 70%, spin up 2 additional instances"*).

---

## 5. Next Steps: Modern Deployment Infrastructure
Once you are completely comfortable SSHing into an EC2 server and running a manual deployment, transition away from managing individual virtual machines:

* **Docker on EC2:** Learn how to containerize your application and run it on a virtual machine.
* **Amazon ECS (Elastic Container Service) with AWS Fargate:** This is a key inflection point for modern backend developers. Fargate provides a **serverless compute engine** for containers. You no longer provision or manage underlying EC2 instances; you simply provide your Docker image, set CPU/Memory limits, and AWS runs the infrastructure for you.

---

## Recommended Practical Milestone Project

The best way to solidify this knowledge is to build a simple, realistic milestone architecture. 

### Step 1: Manual Single-Server Deployment
1. **Spin up** a Single Linux EC2 Instance (`t2.micro`).
2. **Configure the Security Group** to allow SSH (`22`) from your IP and custom TCP traffic on port `8080`.
3. **SSH into the instance** via your terminal using your Key Pair:
   ```bash
   ssh -i "your-key.pem" ec2-user@your-instance-public-dns.amazonaws.com