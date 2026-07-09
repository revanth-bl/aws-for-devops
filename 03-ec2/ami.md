# Amazon Machine Image (AMI)

## Introduction

An **Amazon Machine Image (AMI)** is a template used to create EC2 instances in AWS.

An AMI contains the information required to launch a virtual server, including:

- Operating system
- Application server
- Software packages
- Configuration settings
- Permissions
- Storage mappings

When launching an EC2 instance, AWS uses an AMI as the blueprint for the server.

---

# How AMI Works

```
        AMI
         │
         ▼
  Launch EC2 Instance
         │
         ▼
 Virtual Server Created
         │
         ▼
 OS + Software + Configuration
```

An AMI can be used repeatedly to create identical EC2 instances.

---

# Components of an AMI

An AMI contains three main components:

## 1. Root Volume Template

Contains the operating system and boot files.

Examples:

- Amazon Linux
- Ubuntu
- Windows Server
- Red Hat Enterprise Linux

---

## 2. Block Device Mapping

Defines the storage volumes attached to the instance.

It specifies:

- Volume type
- Volume size
- Device name
- Delete-on-termination settings

---

## 3. Launch Permissions

Controls who can use the AMI.

Options:

- Private
- Shared with specific AWS accounts
- Public

---

# Types of AMIs

## 1. AWS Provided AMIs

Created and maintained by AWS.

Examples:

- Amazon Linux AMI
- Windows Server AMI

Advantages:

- Officially supported
- Regular updates
- Secure baseline

---

## 2. Community AMIs

Created and shared by AWS users and organizations.

Examples:

- Custom Linux distributions
- Pre-configured applications

Before using community AMIs, verify:

- Publisher trust
- Security settings
- Software included

---

## 3. Marketplace AMIs

Provided by third-party vendors through AWS Marketplace.

Examples:

- Security appliances
- Enterprise software
- Database platforms

Some Marketplace AMIs require additional licensing fees.

---

## 4. Custom AMIs

Created by customers from existing EC2 instances.

Used when organizations need:

- Standardized server configurations
- Faster deployments
- Consistent environments

---

# Creating a Custom AMI

Steps:

1. Launch and configure an EC2 instance.
2. Install required software.
3. Configure the operating system.
4. Stop the instance (recommended).
5. Create an AMI from the instance.
6. Launch new instances using the AMI.

Example:

```
Configured EC2 Server
          │
          ▼
     Create AMI
          │
          ▼
 Multiple Identical Servers
```

---

# Why Use Custom AMIs?

Custom AMIs help organizations:

- Deploy servers quickly.
- Maintain consistent configurations.
- Reduce manual setup.
- Automate infrastructure deployment.
- Create repeatable environments.

---

# AMI and Auto Scaling

Auto Scaling Groups commonly use AMIs to launch new instances automatically.

Example:

```
Auto Scaling Group
          │
          ▼
       AMI Template
          │
          ▼
New EC2 Instances Created
```

When demand increases, AWS launches new EC2 instances from the configured AMI.

---

# AMI Lifecycle

The AMI lifecycle:

```
Create Instance
       │
       ▼
Configure Software
       │
       ▼
Create AMI
       │
       ▼
Launch New Instances
       │
       ▼
Deregister AMI When No Longer Needed
```

---

# AMI Sharing

AMIs can be shared with:

- Other AWS accounts
- Specific users
- Public AWS community

Common use cases:

- Enterprise deployments
- Multi-account environments
- Disaster recovery

---

# AMI vs Snapshot

| AMI | Snapshot |
|-----|----------|
| Template for launching EC2 instances | Backup of an EBS volume |
| Contains OS and configuration | Contains only volume data |
| Used to create new EC2 instances | Used to restore storage |
| Includes launch permissions | Does not launch instances directly |

---

# AMI Best Practices

- Use trusted AMIs from AWS or verified publishers.
- Keep AMIs updated with security patches.
- Remove unnecessary software before creating AMIs.
- Use naming conventions and version numbers.
- Encrypt AMIs containing sensitive data.
- Regularly remove outdated AMIs.
- Test AMIs before production use.

---

# Real-World DevOps Example

A company needs to deploy 100 web servers.

Without AMI:

- Install OS manually.
- Install packages manually.
- Configure each server individually.

With AMI:

```
Golden AMI
     │
     ▼
Auto Scaling Group
     │
     ▼
100 Identical Web Servers
```

All servers have the same configuration and can be deployed quickly.

---

# Interview Questions

### What is an AMI in AWS?

An AMI is a template used to launch EC2 instances containing the operating system, software, and configuration.

---

### What information does an AMI contain?

An AMI contains:

- Root volume template
- Block device mappings
- Launch permissions

---

### What is a Custom AMI?

A custom AMI is an AMI created by a user from a configured EC2 instance.

---

### Difference between AMI and Snapshot?

An AMI is used to launch EC2 instances, while a snapshot is a backup of an EBS volume.

---

### Why are AMIs useful in Auto Scaling?

Auto Scaling uses AMIs to automatically create identical EC2 instances when scaling out.

---

# Key Takeaways

- AMI is the blueprint for an EC2 instance.
- It contains the OS, software, and configuration.
- AWS provides public AMIs, and users can create custom AMIs.
- Custom AMIs improve automation and consistency.
- Auto Scaling Groups use AMIs to launch new instances.
- AMIs are essential for production deployments and DevOps automation.