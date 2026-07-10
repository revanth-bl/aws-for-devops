# Amazon RDS Read Replicas

## Introduction

An **Amazon RDS Read Replica** is a read-only copy of a primary database instance.

Read Replicas are used to improve the performance of applications with heavy read workloads by distributing read requests across multiple database instances.

Applications continue sending write operations to the primary database, while read operations can be directed to one or more Read Replicas.

---

# Why Use Read Replicas?

As applications grow, database read requests increase.

Instead of placing all traffic on one database, Read Replicas distribute read operations.

Example:

```
Users

      │

      ▼

Primary Database

      │

      ├──────────────┐

      ▼              ▼

Read Replica 1   Read Replica 2
```

This reduces the load on the primary database.

---

# How Read Replicas Work

The primary database accepts:

- INSERT
- UPDATE
- DELETE
- WRITE operations

Read Replicas receive changes from the primary using **asynchronous replication**.

```
Application

        │

        ▼

Primary Database

   (Write Operations)

        │

Asynchronous Replication

        ▼

Read Replica
```

Applications send read-only queries to the replica.

---

# Read Operations

Examples of read operations:

- SELECT
- Reports
- Dashboards
- Analytics
- Search queries

These requests can be handled by Read Replicas instead of the primary database.

---

# Write Operations

Write operations always occur on the primary database.

Examples:

```
INSERT
UPDATE
DELETE
CREATE
ALTER
DROP
```

Read Replicas cannot accept write operations.

---

# Replication

Amazon RDS Read Replicas use **asynchronous replication**.

```
Primary Database

        │

        ▼

Changes

        │

        ▼

Read Replica
```

Because replication is asynchronous, there may be a small delay (replication lag) before changes appear on the replica.

---

# Multiple Read Replicas

One primary database can have multiple Read Replicas.

Example:

```
                 Primary Database

           ┌─────────┼─────────┐

           ▼         ▼         ▼

      Replica 1  Replica 2  Replica 3
```

Applications can distribute read traffic across multiple replicas.

---

# Read Replica Promotion

If required, a Read Replica can be promoted to become a standalone database instance.

Example:

```
Primary Database

        │

Read Replica

        │

Promote

        ▼

Standalone Database
```

After promotion, it no longer receives updates from the original primary database.

---

# Read Replica vs Multi-AZ

| Read Replica | Multi-AZ |
|--------------|-----------|
| Improves read performance | Improves high availability |
| Read-only | Standby instance |
| Uses asynchronous replication | Uses synchronous replication |
| Can serve application read traffic | Cannot serve application traffic while acting as standby |
| Can be promoted | Automatic failover managed by AWS |

---

# Supported Database Engines

Read Replicas are supported by:

- MySQL
- PostgreSQL
- MariaDB
- Amazon Aurora

Support varies by engine and version.

---

# Real-World Example

An e-commerce website:

```
Customers

        │

        ▼

Application

        │

        ▼

Primary Database

        │

        ├──────────────┐

        ▼              ▼

Reporting       Product Search

(Read Replica)  (Read Replica)
```

The primary database handles customer purchases, while reporting and search queries run on Read Replicas.

---

# Benefits

- Improves read performance.
- Reduces load on the primary database.
- Supports reporting and analytics.
- Improves scalability.
- Allows multiple read-only database copies.

---

# Limitations

- Read-only access.
- Replication lag may occur.
- Does not replace backups.
- Does not provide automatic failover like Multi-AZ.
- Write operations must always go to the primary database.

---

# Best Practices

- Use Read Replicas for read-heavy workloads.
- Monitor replication lag using Amazon CloudWatch.
- Continue using Multi-AZ for high availability.
- Route reporting and analytics queries to replicas.
- Size replica instances based on expected read traffic.

---

# Common Mistakes

- Assuming Read Replicas provide automatic failover.
- Sending write requests to a Read Replica.
- Ignoring replication lag.
- Using Read Replicas instead of backups.
- Confusing Read Replicas with Multi-AZ deployments.

---

# Interview Questions

### What is an Amazon RDS Read Replica?

A Read Replica is a read-only copy of a primary RDS database used to improve read performance.

---

### Can applications write to a Read Replica?

No. Read Replicas support read-only operations.

---

### What type of replication is used?

Read Replicas use asynchronous replication.

---

### Can a Read Replica become a standalone database?

Yes. It can be promoted to a standalone DB instance.

---

### What is the difference between Read Replicas and Multi-AZ?

Read Replicas improve read scalability using asynchronous replication, while Multi-AZ improves high availability using synchronous replication and automatic failover.

---

# Key Takeaways

- Read Replicas improve read scalability.
- They are read-only database copies.
- Replication is asynchronous, so some lag is possible.
- Write operations always go to the primary database.
- Read Replicas can be promoted to standalone databases.
- Multi-AZ and Read Replicas solve different problems and are often used together in production environments.