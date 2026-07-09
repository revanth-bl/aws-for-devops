# Launching an EC2 Instance

## Introduction

Amazon Elastic Compute Cloud (**EC2**) is an AWS service that provides resizable virtual servers in the cloud.

Launching an EC2 instance means creating a virtual machine with:

- Operating system
- CPU
- Memory
- Storage
- Network configuration
- Security settings

EC2 allows organizations to deploy applications without purchasing or maintaining physical servers.

---

# EC2 Launch Process Overview

The process of launching an EC2 instance includes:

```
Choose AMI
    │
    ▼
Choose Instance Type
    │
    ▼
Configure Network
    │
    ▼
Configure Storage
    │
    ▼
Configure Security Group
    │
    ▼
Select Key Pair
    │
    ▼
Launch Instance
```

---

# Step 1: Choose an AMI

An **Amazon Machine Image (AMI)** defines the operating system and initial configuration of the instance.

Examples:

- Amazon Linux
- Ubuntu
- Red Hat Enterprise Linux
- Windows Server

Example:

```
Ubuntu Server 24.04 LTS
```

The AMI acts as the blueprint for the EC2 instance.

---

# Step 2: Choose Instance Type

An EC2 instance type defines the hardware configuration.

It determines:

- CPU
- Memory
- Network performance
- Storage options

Example:

```
t2.micro
t3.medium
m7i.large
```

---

# EC2 Instance Families

## General Purpose

Balanced CPU, memory, and networking.

Examples:

- T series
- M series

Use cases:

- Web servers
- Development environments

---

## Compute Optimized

High CPU performance.

Examples:

- C series

Use cases:

- Batch processing
- Gaming servers
- High-performance applications

---

## Memory Optimized

Designed for large memory workloads.

Examples:

- R series

Use cases:

- Databases
- Analytics

---

## Storage Optimized

Designed for high local storage performance.

Examples:

- I series
- D series

Use cases:

- Big data
- Data processing

---

# Step 3: Configure Network Settings

Network configuration includes:

- VPC
- Subnet
- Availability Zone
- Public IP
- Security Group

Example:

```
Region
   │
   ▼
VPC
   │
   ▼
Subnet
   │
   ▼
EC2 Instance
```

---

# Step 4: Configure Storage

EC2 instances use storage volumes.

Common options:

- EBS volumes
- Instance Store

Example:

```
EC2 Instance

├── Root Volume
│       └── Operating System
│
└── Additional Volume
        └── Application Data
```

Storage settings include:

- Volume size
- Volume type
- Encryption
- Delete on termination

---

# Step 5: Configure Security Group

A Security Group acts as a virtual firewall for the EC2 instance.

It controls:

- Incoming traffic (Inbound)
- Outgoing traffic (Outbound)

Example:

Allow SSH:

```
Port: 22
Protocol: TCP
Source: Your IP
```

Allow Web Traffic:

```
Port: 80
Protocol: HTTP
Source: Anywhere
```

---

# Step 6: Select Key Pair

A Key Pair is used to securely access the EC2 instance.

For Linux:

```
SSH + Private Key
```

Example:

```bash
ssh -i server-key.pem ubuntu@public-ip
```

---

# Step 7: Launch Instance

After reviewing all settings:

1. Click **Launch Instance**.
2. AWS creates the virtual machine.
3. The instance receives:
   - Private IP address
   - Public IP (if enabled)
   - Security configuration

The instance enters the running state.

---

# EC2 Instance States

An EC2 instance can have different states:

| State | Description |
|-------|-------------|
| Pending | Instance is starting |
| Running | Instance is active |
| Stopping | Instance is shutting down |
| Stopped | Instance is powered off |
| Terminated | Instance is permanently deleted |

---

# Connecting to an EC2 Instance

## Linux Instance

Using SSH:

```bash
ssh -i key.pem username@public-ip
```

Examples:

Amazon Linux:

```bash
ssh -i key.pem ec2-user@public-ip
```

Ubuntu:

```bash
ssh -i key.pem ubuntu@public-ip
```

---

## Windows Instance

Connection method:

- Remote Desktop Protocol (RDP)

Requires:

- Administrator password
- Public IP address
- RDP access in Security Group

---

# User Data

EC2 supports **User Data**, which allows automatic execution of scripts during instance startup.

Example:

```bash
#!/bin/bash

yum update -y
yum install httpd -y
systemctl start httpd
```

Common uses:

- Installing software
- Configuring applications
- Automating server setup

---

# Terminating an EC2 Instance

Termination permanently deletes the instance.

Before terminating:

- Backup important data.
- Create snapshots if needed.
- Verify Delete on Termination settings.

---

# Launching Multiple Instances

For production environments:

- Use Launch Templates.
- Use Auto Scaling Groups.
- Use Load Balancers.

Example:

```
             Load Balancer

          /       |       \

       EC2      EC2      EC2
```

---

# Best Practices

- Use IAM Roles instead of storing access keys.
- Choose the correct instance type.
- Restrict SSH access to trusted IP addresses.
- Enable EBS encryption.
- Apply security patches regularly.
- Monitor instances using CloudWatch.
- Use Auto Scaling for production workloads.
- Tag resources properly.

---

# Real-World DevOps Example

A company deploys a web application:

```
User
 │
 ▼
Application Load Balancer
 │
 ▼
EC2 Instances
 │
 ▼
EBS Storage
 │
 ▼
Database
```

EC2 provides the compute layer where the application runs.

---

# Interview Questions

### What is EC2?

EC2 is an AWS service that provides scalable virtual servers in the cloud.

---

### What are the steps to launch an EC2 instance?

1. Select AMI.
2. Choose instance type.
3. Configure network.
4. Configure storage.
5. Configure security group.
6. Select key pair.
7. Launch instance.

---

### What is User Data in EC2?

User Data allows scripts to automatically run when an EC2 instance starts.

---

### What is an Instance Type?

An instance type defines the CPU, memory, storage, and networking capacity of an EC2 instance.

---

### Difference between Stop and Terminate?

- Stop: Instance is shut down but can be started again.
- Terminate: Instance is permanently deleted.

---

# Key Takeaways

- EC2 provides virtual servers in AWS.
- AMIs define the operating system and configuration.
- Instance types determine hardware capacity.
- Security Groups control network access.
- Key Pairs provide secure authentication.
- User Data enables automatic configuration.
- EC2 is one of the most important AWS services for DevOps engineers.