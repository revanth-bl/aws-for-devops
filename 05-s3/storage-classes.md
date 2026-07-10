# Amazon S3 Storage Classes

## Introduction

Amazon S3 offers multiple **Storage Classes** designed for different access patterns and cost requirements.

Instead of storing every object in the same type of storage, you can choose the most suitable storage class based on:

- How frequently the data is accessed
- How quickly it needs to be retrieved
- Storage cost
- Retrieval cost
- Availability requirements

Selecting the correct storage class helps optimize performance while reducing storage costs.

---

# Why Storage Classes?

Not all data is accessed equally.

Example:

```
Application Data

Daily Access
▼
Images
Videos
Documents

Monthly Access
▼
Backups

Yearly Access
▼
Archives
```

Keeping archived data in expensive storage wastes money.

Storage Classes solve this problem.

---

# S3 Storage Class Overview

```
Frequently Accessed
        │
        ▼
S3 Standard
        │
        ▼
S3 Intelligent-Tiering
        │
        ▼
S3 Standard-IA
        │
        ▼
S3 One Zone-IA
        │
        ▼
S3 Glacier Instant Retrieval
        │
        ▼
S3 Glacier Flexible Retrieval
        │
        ▼
S3 Glacier Deep Archive
```

As access frequency decreases, storage costs generally decrease.

---

# 1. S3 Standard

Designed for frequently accessed data.

Features:

- Low latency
- High throughput
- Multi-Availability Zone storage
- High availability
- High durability

Common use cases:

- Websites
- Mobile applications
- Frequently accessed files
- Active business data

---

# 2. S3 Intelligent-Tiering

Automatically moves objects between access tiers based on usage patterns.

Suitable for:

- Unknown access patterns
- Long-term storage
- Mixed workloads

Benefits:

- Automatic cost optimization
- No performance impact
- Minimal operational effort

---

# 3. S3 Standard-Infrequent Access (Standard-IA)

Designed for data that is accessed occasionally but must be available quickly when needed.

Examples:

- Backups
- Disaster recovery
- Long-term business files

Benefits:

- Lower storage cost than Standard
- Fast retrieval

---

# 4. S3 One Zone-Infrequent Access (One Zone-IA)

Stores data in a single Availability Zone.

Suitable for:

- Secondary backups
- Re-creatable data
- Non-critical files

Advantages:

- Lower cost than Standard-IA

Limitation:

- Lower resilience because data is stored in one Availability Zone.

---

# 5. S3 Glacier Instant Retrieval

Designed for archive data that still requires immediate access.

Examples:

- Medical records
- Media archives
- Historical documents

Provides:

- Low-cost archival storage
- Millisecond retrieval

---

# 6. S3 Glacier Flexible Retrieval

Designed for archived data that is rarely accessed.

Examples:

- Compliance records
- Archived backups

Retrieval options include:

- Expedited
- Standard
- Bulk

Storage costs are lower than Glacier Instant Retrieval, but retrieval times can be longer depending on the option chosen.

---

# 7. S3 Glacier Deep Archive

The lowest-cost S3 storage class.

Designed for long-term archival data.

Examples:

- Legal records
- Regulatory archives
- Long-term backups

Ideal when data is rarely accessed.

---

# Storage Class Comparison

| Storage Class | Access Pattern | Typical Use Case |
|--------------|----------------|------------------|
| S3 Standard | Frequent | Websites, applications |
| Intelligent-Tiering | Unknown | Mixed workloads |
| Standard-IA | Infrequent | Backups |
| One Zone-IA | Infrequent | Non-critical backups |
| Glacier Instant Retrieval | Rare | Archives requiring immediate access |
| Glacier Flexible Retrieval | Very rare | Archived backups |
| Glacier Deep Archive | Almost never | Long-term compliance archives |

---

# Lifecycle Integration

Storage Classes work together with **Lifecycle Policies**.

Example:

```
Day 0
▼
S3 Standard

Day 30
▼
Standard-IA

Day 90
▼
Glacier Flexible Retrieval

Day 365
▼
Glacier Deep Archive
```

Lifecycle rules automatically move objects between storage classes.

---

# Choosing the Right Storage Class

| Requirement | Recommended Storage Class |
|------------|---------------------------|
| Frequently accessed data | S3 Standard |
| Unknown access pattern | Intelligent-Tiering |
| Occasional access | Standard-IA |
| Low-cost single-AZ storage | One Zone-IA |
| Archive with instant access | Glacier Instant Retrieval |
| Archive with flexible retrieval | Glacier Flexible Retrieval |
| Long-term archival | Glacier Deep Archive |

---

# Best Practices

- Choose storage classes based on actual access patterns.
- Use Intelligent-Tiering when access patterns are unpredictable.
- Use Lifecycle Policies to automate transitions.
- Avoid storing archive data in S3 Standard.
- Review storage usage regularly using AWS Cost Explorer and S3 Storage Class Analysis.

---

# Common Mistakes

- Keeping old backups in S3 Standard.
- Using Glacier for frequently accessed files.
- Ignoring retrieval costs when selecting archive storage.
- Not implementing Lifecycle Policies.
- Storing critical single-copy data in One Zone-IA.

---

# Real-World DevOps Example

A company stores application logs.

```
Application

      │

      ▼

Amazon S3 Standard

      │

30 Days

      ▼

S3 Standard-IA

      │

90 Days

      ▼

Glacier Flexible Retrieval

      │

365 Days

      ▼

Glacier Deep Archive
```

This approach minimizes storage costs while keeping data available when required.

---

# Interview Questions

### What is an S3 Storage Class?

An S3 Storage Class defines how Amazon S3 stores objects based on cost, availability, and access frequency.

---

### Which storage class is best for frequently accessed data?

S3 Standard.

---

### Which storage class automatically optimizes costs?

S3 Intelligent-Tiering.

---

### Which storage class offers the lowest storage cost?

S3 Glacier Deep Archive.

---

### Why use Lifecycle Policies with Storage Classes?

Lifecycle Policies automatically move objects between storage classes based on rules, reducing storage costs.

---

# Key Takeaways

- Amazon S3 provides multiple storage classes for different workloads.
- Frequently accessed data belongs in S3 Standard.
- Intelligent-Tiering automatically optimizes storage costs.
- Glacier storage classes are designed for archival data.
- Lifecycle Policies automate movement between storage classes.
- Selecting the correct storage class is essential for balancing performance and cost.