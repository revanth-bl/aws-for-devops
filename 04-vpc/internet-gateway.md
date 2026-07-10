# Amazon Virtual Private Cloud (VPC)

## Introduction

**Amazon Virtual Private Cloud (VPC)** is a service that allows you to create a logically isolated virtual network within AWS.

A VPC gives you complete control over your network configuration, including:

- IP address ranges
- Subnets
- Route tables
- Internet connectivity
- Security settings

Think of a VPC as your own private data center inside AWS.

---

# Why Use a VPC?

Without a VPC, all resources would exist in a shared network.

A VPC allows you to:

- Isolate resources
- Improve security
- Control network traffic
- Design scalable architectures
- Connect securely to on-premises networks

---

# How a VPC Works

```
                    AWS Region
                        │
                        ▼
              Amazon VPC (10.0.0.0/16)
                        │
        ┌───────────────┴───────────────┐
        ▼                               ▼
 Public Subnet                  Private Subnet
        │                               │
        ▼                               ▼
    EC2 Instance                  Database
```

The VPC acts as the network boundary for your AWS resources.

---

# Components of a VPC

A VPC typically contains:

- CIDR Block
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- Network ACLs

---

# CIDR Block

Every VPC requires an IP address range.

Example:

```
10.0.0.0/16
```

This range determines the private IP addresses available inside the VPC.

Examples:

```
10.0.0.0/16
172.31.0.0/16
192.168.0.0/16
```

---

# VPC Features

- Logical isolation
- Custom IP address ranges
- Public and private subnets
- Internet connectivity
- Secure communication
- Scalability
- High availability

---

# Default VPC

AWS automatically creates a **Default VPC** in each Region.

Features:

- Ready to use
- Public subnets
- Internet Gateway attached
- Route table configured

Suitable for:

- Learning
- Testing
- Small workloads

---

# Custom VPC

A Custom VPC is created manually by the user.

Benefits:

- Full control
- Better security
- Flexible network design
- Production-ready architecture

Most production workloads use Custom VPCs.

---

# Public vs Private VPC Resources

### Public Resources

Examples:

- Web servers
- Load Balancers
- Bastion Hosts

Can communicate with the internet.

---

### Private Resources

Examples:

- Databases
- Internal APIs
- Application servers

Cannot communicate directly with the internet.

---

# VPC Architecture Example

```
                  Internet
                      │
                      ▼
            Internet Gateway
                      │
          ┌───────────┴───────────┐
          ▼                       ▼
   Public Subnet           Private Subnet

 Web Server EC2            Database
 Load Balancer             Application Server
```

---

# VPC Best Practices

- Use a Custom VPC for production.
- Plan CIDR ranges carefully.
- Separate public and private resources.
- Use multiple Availability Zones.
- Apply least-privilege network access.
- Enable VPC Flow Logs for monitoring.
- Use Security Groups and Network ACLs together.

---

# Real-World Example

An e-commerce application:

```
Internet
    │
    ▼
Application Load Balancer
    │
    ▼
Public Subnet
    │
    ▼
Application Servers
    │
    ▼
Private Subnet
    │
    ▼
Amazon RDS
```

The database remains protected inside the private subnet while users access the application through the public layer.

---

# Interview Questions

### What is a VPC?

A VPC is a logically isolated virtual network in AWS where you launch and manage cloud resources.

---

### What is the difference between a Default VPC and a Custom VPC?

A Default VPC is automatically created and ready to use, while a Custom VPC is manually created and offers greater control over networking.

---

### Can multiple VPCs exist in one AWS Region?

Yes. You can create multiple VPCs within the same AWS Region.

---

### Why are VPCs important?

They provide network isolation, security, and complete control over AWS networking.

---

# Key Takeaways

- A VPC is your private virtual network in AWS.
- Every VPC uses a CIDR block.
- VPCs contain subnets, route tables, gateways, and security controls.
- Custom VPCs are recommended for production workloads.
- Proper VPC design is the foundation of secure AWS architectures.