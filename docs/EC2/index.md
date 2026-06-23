---
title: EC2 Instance
parent: AWS Notes
nav_order: 1
---

# EC2 Basics

## What is EC2?

**EC2 (Elastic Compute Cloud)** is a web service that provides resizable compute capacity in the cloud. It's essentially a virtual computer/server that runs on AWS infrastructure.

### Why Use EC2?

- **Scalability**: Easily add or remove compute capacity based on demand
- **Cost-effective**: Pay only for what you use (pay-as-you-go model)
- **Flexibility**: Choose OS, software, and configurations
- **Reliability**: High availability with multiple regions/zones
- **Control**: Full admin/root access to instances
- **Speed**: Launch instances in minutes vs. physical servers in weeks

## EC2 Instance Basics

### What is an Instance?

An EC2 instance is a virtual server running on AWS. You can:
- Choose CPU, memory, and storage capacity
- Select operating system (Amazon Linux, Ubuntu, Windows, etc.)
- Install and run any software/applications
- Connect via SSH (Linux) or RDP (Windows)

### Instance Types

EC2 offers different instance families for various use cases:

| Type | Use Case | Examples |
|------|----------|----------|
| **T3/T4g** | General purpose, low-traffic apps | Web servers, development |
| **M5/M6** | Balanced compute/memory/network | Medium workloads, databases |
| **C5/C6** | Compute optimized | High-performance apps, batch processing |
| **R5/R6** | Memory optimized | In-memory databases, caching |
| **P3/G4** | GPU/ML | Machine learning, graphics rendering |

### Pricing Models

- **On-Demand**: Pay per hour/second. Most flexible, highest cost
- **Reserved Instances**: Commit 1-3 years, up to 72% discount
- **Spot Instances**: Unused capacity at 90% discount, can be interrupted
- **Savings Plans**: Flexible discount commitment

## Key Concepts

### AMI (Amazon Machine Image)
A template containing OS, software, and configurations. Think of it as a "snapshot" you use to launch instances.

### Security Groups
Virtual firewalls controlling inbound/outbound traffic to instances.

### Key Pairs
SSH key pairs (private/public) for secure access to instances.

### Elastic IPs
Static public IP addresses that persist when instances stop/start.

### Volumes
Storage attached to instances (EBS volumes for persistent storage, instance store for temporary).

## Typical Workflow

1. **Choose AMI** - Select OS and software template
2. **Select Instance Type** - Pick CPU/memory specs
3. **Configure Details** - Set network, storage, tags
4. **Add Storage** - Attach volumes
5. **Security Group** - Define firewall rules
6. **Review & Launch** - Create key pair and launch
7. **Connect** - Use SSH/RDP to access instance
8. **Install/Configure** - Set up your applications
9. **Monitor** - Use CloudWatch for metrics
10. **Stop/Terminate** - When done, manage costs

## Common Use Cases

- **Web Hosting**: Host websites and web applications
- **Development/Testing**: Cheap sandbox environments
- **Databases**: Run MySQL, PostgreSQL, MongoDB, etc.
- **Machine Learning**: GPU instances for training models
- **Big Data**: Process large datasets with multiple instances
- **Batch Processing**: Run computational jobs

## Getting Started Tips

1. **Use Free Tier**: AWS offers 750 hours/month of t2.micro for 12 months
2. **Always Use Security Groups**: Restrict access to needed ports only
3. **Tag Instances**: Use tags to organize and track costs
4. **Monitor Costs**: Use AWS Cost Explorer to track spending
5. **Automate Backups**: Use AMIs and snapshots for disaster recovery
6. **Stop vs. Terminate**: Stop to pause (keep charges), terminate to delete
7. **Use CloudWatch**: Monitor CPU, network, and disk metrics

## Common Mistakes to Avoid

- ❌ Leaving instances running unnecessarily (high costs)
- ❌ Using overly permissive security groups (security risk)
- ❌ Not backing up data/configurations
- ❌ Choosing wrong instance type (wasted resources)
- ❌ Ignoring auto-scaling for variable workloads

---

**Next Steps**: Create your first EC2 instance, connect to it, and run a simple web server to understand the basics hands-on.
