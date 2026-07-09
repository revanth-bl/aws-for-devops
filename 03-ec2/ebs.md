# Amazon Elastic Block Store (EBS)

## Introduction

**Amazon Elastic Block Store (EBS)** is a block-level storage service designed to be used with Amazon EC2 instances.

EBS provides persistent storage volumes that can be attached to EC2 instances. Unlike temporary instance storage, EBS data remains available even after an EC2 instance is stopped.

---

# What is Block Storage?

Block storage divides data into fixed-size blocks and stores them separately.

Applications interact with block storage like a traditional hard drive.

Examples:

- Operating system files
- Applications
- Databases
- Logs

An EBS volume behaves like a physical hard disk attached to a server.

---

# How EBS Works

```
        EC2 Instance
              │
              ▼
        EBS Volume
              │
              ▼
      Persistent Storage
```

An EC2 instance can have one or more EBS volumes attached.

---

# Features of EBS

## 1. Persistent Storage

EBS volumes are independent from EC2 instance lifecycle.

Example:

```
Stop EC2 Instance
        │
        ▼
Start EC2 Instance
        │
        ▼
Data Still Exists
```

---

## 2. High Availability

EBS volumes are automatically replicated within an Availability Zone to protect against hardware failures.

---

## 3. Scalability

EBS volumes can be modified without replacing the EC2 instance.

You can increase:

- Volume size
- Performance
- IOPS

---

## 4. Backup Support

EBS volumes can be backed up using:

- EBS Snapshots

Snapshots can be used to:

- Restore data
- Create new volumes
- Create AMIs

---

# EBS Volume Types

AWS provides different EBS volume types for different workloads.

---

# 1. General Purpose SSD (gp3/gp2)

Balanced storage for most workloads.

Suitable for:

- Web servers
- Development environments
- Small databases
- Applications

Advantages:

- Good performance
- Cost-effective
- Default choice for many applications

---

# 2. Provisioned IOPS SSD (io2/io1)

Designed for high-performance workloads requiring consistent I/O performance.

Used for:

- Large databases
- Enterprise applications
- Critical workloads

Provides:

- High IOPS
- Low latency
- High durability

---

# 3. Throughput Optimized HDD (st1)

Designed for large sequential workloads.

Used for:

- Big data processing
- Data warehouses
- Log processing

---

# 4. Cold HDD (sc1)

Low-cost HDD storage for infrequently accessed data.

Used for:

- Archives
- Backup data
- Infrequent workloads

---

# EBS Volume Type Comparison

| Volume Type | Best For |
|-------------|----------|
| gp3/gp2 | General workloads |
| io2/io1 | High-performance databases |
| st1 | Big data and streaming workloads |
| sc1 | Infrequent access storage |

---

# EBS Snapshots

An **EBS Snapshot** is a point-in-time backup of an EBS volume.

Snapshots are stored in Amazon S3 internally.

Benefits:

- Backup and recovery
- Migration between Regions
- Creating new EBS volumes
- Creating custom AMIs

---

# Creating an EBS Snapshot

Process:

```
EBS Volume
     │
     ▼
Create Snapshot
     │
     ▼
Stored Backup
     │
     ▼
Restore When Needed
```

---

# EBS Encryption

EBS supports encryption to protect stored data.

Encryption provides:

- Data-at-rest protection
- Secure volume snapshots
- Secure data transfer between EC2 and EBS

AWS Key Management Service (KMS) is used to manage encryption keys.

---

# EBS and EC2 Lifecycle

When launching an EC2 instance:

- Root volume is usually created automatically.
- Additional EBS volumes can be attached later.

Example:

```
EC2 Instance

├── Root EBS Volume
│       └── Operating System
│
└── Data EBS Volume
        └── Application Data
```

---

# Delete on Termination

Each EBS volume has a setting called:

**Delete on Termination**

## Enabled:

When EC2 instance is deleted:

```
EC2 Terminated
       │
       ▼
EBS Volume Deleted
```

## Disabled:

The EBS volume remains after instance termination.

Useful for preserving important data.

---

# EBS vs Instance Store

| EBS | Instance Store |
|-----|----------------|
| Persistent storage | Temporary storage |
| Data survives stop/start | Data lost when instance stops |
| Network-attached storage | Physically attached storage |
| Can create snapshots | No snapshots |

---

# EBS Best Practices

- Choose the correct volume type based on workload.
- Enable encryption for sensitive data.
- Create regular snapshots.
- Delete unused volumes to reduce costs.
- Monitor volume performance.
- Use appropriate volume size.
- Avoid storing critical data without backups.

---

# Real-World DevOps Example

A production web application runs on EC2.

Architecture:

```
              Users
                │
                ▼
             EC2 Server
                │
        ┌───────┴────────┐
        ▼                ▼
   Root EBS          Data EBS
   Volume            Volume

   OS Files          Application Data
```

If the EC2 instance fails:

- Launch a replacement instance.
- Attach the existing EBS volume.
- Restore application data.

---

# Interview Questions

### What is EBS?

EBS is a persistent block storage service used with EC2 instances.

---

### Does EBS data survive when an EC2 instance is stopped?

Yes. EBS volumes persist after stopping an EC2 instance.

---

### What is an EBS Snapshot?

A point-in-time backup of an EBS volume.

---

### Difference between EBS and Instance Store?

EBS provides persistent storage, while Instance Store provides temporary storage that is lost when the instance stops or terminates.

---

### Can an EBS volume be attached to multiple EC2 instances?

Generally, an EBS volume can be attached to one EC2 instance at a time (except supported multi-attach configurations).

---

# Key Takeaways

- EBS provides persistent block storage for EC2.
- EBS volumes behave like virtual hard drives.
- Data remains after stopping an EC2 instance.
- Snapshots provide backup and recovery.
- Different volume types support different workloads.
- Encryption protects stored data.
- EBS is essential for production EC2 workloads.