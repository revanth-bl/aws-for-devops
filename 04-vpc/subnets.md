# Subnets

## Introduction

A **Subnet** is a smaller network created from the IP address range of a VPC.

Subnets help organize and isolate AWS resources by dividing a VPC into multiple logical sections.

Every AWS resource, such as an EC2 instance, RDS database, or NAT Gateway, must be launched inside a subnet.

---

# Why Do We Need Subnets?

Instead of placing every resource in one large network, subnets allow you to:

- Organize resources
- Improve security
- Separate public and private workloads
- Increase availability
- Simplify network management

Example:

```
VPC (10.0.0.0/16)

├── Public Subnet
│
├── Private Subnet
│
└── Database Subnet
```

---

# How Subnets Work

```
AWS Region
     │
     ▼
    VPC
     │
     ├──────────────┐
     ▼              ▼
Public Subnet   Private Subnet
     │              │
     ▼              ▼
Web Server      Database
```

Each subnet uses a portion of the VPC's CIDR block.

---

# CIDR Allocation

Suppose the VPC CIDR block is:

```
10.0.0.0/16
```

It can be divided into smaller subnets:

```
10.0.1.0/24
10.0.2.0/24
10.0.3.0/24
10.0.4.0/24
```

Each subnet has its own IP address range.

---

# Types of Subnets

AWS commonly uses two subnet types:

- Public Subnet
- Private Subnet

---

# Public Subnet

A **Public Subnet** is a subnet that has a route to an **Internet Gateway (IGW)**.

Resources inside a public subnet can communicate with the internet if they also have public IP addresses.

Common resources:

- Web Servers
- Bastion Hosts
- NAT Gateways
- Application Load Balancers

Example:

```
Internet
     │
     ▼
Internet Gateway
     │
     ▼
Public Subnet
     │
     ▼
EC2 Web Server
```

---

# Private Subnet

A **Private Subnet** does **not** have a direct route to an Internet Gateway.

Resources in a private subnet are protected from direct internet access.

They can still access the internet for outbound connections through a NAT Gateway.

Common resources:

- Amazon RDS
- Application Servers
- Internal APIs
- Backend Services

Example:

```
Private EC2
      │
      ▼
Private Subnet
      │
      ▼
NAT Gateway
      │
      ▼
Internet
```

---

# Public vs Private Subnet

| Public Subnet | Private Subnet |
|---------------|----------------|
| Route to Internet Gateway | No direct route to Internet Gateway |
| Can have public IPs | Uses private IPs only |
| Internet accessible (if allowed) | Not directly accessible from the internet |
| Hosts web-facing resources | Hosts internal resources |

---

# Availability Zones and Subnets

A subnet exists in **one Availability Zone (AZ)** only.

Example:

```
AWS Region

├── Availability Zone A
│      ├── Public Subnet A
│      └── Private Subnet A
│
└── Availability Zone B
       ├── Public Subnet B
       └── Private Subnet B
```

For high availability, deploy resources across multiple Availability Zones.

---

# Subnet Route Tables

Each subnet must be associated with a route table.

Example:

```
Public Subnet
      │
      ▼
Public Route Table
      │
      ▼
Internet Gateway
```

```
Private Subnet
      │
      ▼
Private Route Table
      │
      ▼
NAT Gateway
```

The route table determines how network traffic is forwarded.

---

# Creating a Subnet

Steps:

1. Open the VPC Dashboard.
2. Select **Subnets**.
3. Click **Create subnet**.
4. Choose the VPC.
5. Select an Availability Zone.
6. Specify the subnet CIDR block.
7. Create the subnet.

---

# Subnet Best Practices

- Separate public and private resources.
- Use multiple Availability Zones.
- Plan CIDR ranges carefully to allow future growth.
- Keep databases in private subnets.
- Avoid exposing unnecessary resources to the internet.
- Use descriptive names and tags.

---

# Common Mistakes

- Placing databases in public subnets.
- Creating only one subnet for production workloads.
- Overlapping CIDR ranges.
- Forgetting to associate the correct route table.
- Assuming a public subnet automatically gives internet access without a route to an Internet Gateway and a public IP.

---

# Real-World DevOps Example

A highly available web application:

```
                     Internet
                         │
                         ▼
                 Internet Gateway
                         │
        ┌────────────────┴────────────────┐
        ▼                                 ▼
 Public Subnet A                   Public Subnet B
        │                                 │
        ▼                                 ▼
 Application Load Balancer (Multi-AZ)
        │
        ▼
 ┌───────────────┬────────────────┐
 ▼                               ▼
Private Subnet A           Private Subnet B
Application Server         Application Server
        │                               │
        └───────────────┬───────────────┘
                        ▼
                  Amazon RDS
```

This design improves availability, scalability, and security.

---

# Interview Questions

### What is a subnet?

A subnet is a smaller network created from a VPC's CIDR block that hosts AWS resources.

---

### What is the difference between a public subnet and a private subnet?

A public subnet has a route to an Internet Gateway, while a private subnet does not.

---

### Can a subnet span multiple Availability Zones?

No. A subnet belongs to a single Availability Zone.

---

### Can a private subnet access the internet?

Yes, by using a NAT Gateway for outbound internet access.

---

### Why should databases be placed in private subnets?

Private subnets prevent direct internet access, improving security for sensitive resources.

---

# Key Takeaways

- A subnet is a subdivision of a VPC.
- Every AWS resource must be launched inside a subnet.
- Public subnets use an Internet Gateway.
- Private subnets typically use a NAT Gateway for outbound internet access.
- A subnet belongs to only one Availability Zone.
- Using multiple public and private subnets across Availability Zones improves availability and security.