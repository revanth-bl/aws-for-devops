# Amazon RDS Backups

## Introduction

Amazon RDS provides built-in backup features that help protect your database from accidental deletion, corruption, or hardware failures.

RDS backups enable you to:

- Recover lost data
- Restore databases after failures
- Create copies before upgrades
- Meet disaster recovery requirements

AWS manages much of the backup process automatically, reducing administrative effort.

---

# Types of RDS Backups

Amazon RDS supports two primary backup methods:

- Automated Backups
- Manual Snapshots

```
Amazon RDS

├── Automated Backups
│
└── Manual Snapshots
```

---

# Automated Backups

Automated Backups are enabled when you create an RDS instance.

They include:

- Daily database snapshots
- Transaction logs

These allow **Point-in-Time Recovery (PITR)** within the configured backup retention period.

Example:

```
Daily Snapshot

Day 1
Day 2
Day 3
Day 4
```

Transaction logs are continuously captured between snapshots.

---

# Backup Retention Period

You can configure the backup retention period.

Typical range:

```
1 – 35 Days
```

Example:

```
Retention: 7 Days

Today
│
├── Day 1
├── Day 2
├── Day 3
├── Day 4
├── Day 5
├── Day 6
└── Day 7
```

Older automated backups are deleted automatically after the retention period expires.

---

# Point-in-Time Recovery (PITR)

Point-in-Time Recovery allows you to restore a database to a specific second within the backup retention period.

Example:

```
09:00 Database Running

10:30 User Error

Restore Database

10:29:59
```

Instead of restoring only the latest backup, you can recover to just before the problem occurred.

---

# Manual Snapshots

Manual Snapshots are created by the user.

Characteristics:

- Never expire automatically
- Remain until deleted
- Can be shared with other AWS accounts (where supported)
- Can be copied to another Region

Example:

```
Before Major Upgrade

Create Snapshot

↓

Upgrade Database

↓

Rollback if Needed
```

---

# Automated Backup vs Manual Snapshot

| Automated Backup | Manual Snapshot |
|------------------|-----------------|
| Created automatically | Created manually |
| Uses retention period | Retained until deleted |
| Supports Point-in-Time Recovery | Restores to the snapshot only |
| Deleted automatically after retention period | Must be deleted manually |

---

# Backup Window

Amazon RDS performs automated backups during a configurable backup window.

Example:

```
Backup Window

02:00 AM

↓

02:30 AM
```

Choose a period with low database activity to minimize performance impact.

---

# Restoring an RDS Database

You cannot restore directly over an existing DB instance.

Instead:

1. Select the backup or snapshot.
2. Choose **Restore**.
3. AWS creates a **new DB instance**.
4. Update your application to use the new endpoint if needed.

---

# Cross-Region Backup

Manual snapshots can be copied to another AWS Region.

Example:

```
Mumbai Region

↓

Snapshot

↓

Singapore Region
```

This improves disaster recovery preparedness.

---

# Backup Storage

Backup storage is managed separately from the database storage.

Key points:

- Automated backups consume backup storage.
- Manual snapshots consume storage until deleted.
- Storage usage depends on database size and changes.

---

# Best Practices

- Enable automated backups.
- Configure an appropriate retention period.
- Create manual snapshots before major upgrades.
- Test database restores regularly.
- Copy important snapshots to another Region.
- Encrypt backups for sensitive data.
- Monitor backup status using Amazon CloudWatch.

---

# Common Mistakes

- Disabling automated backups.
- Not testing database recovery.
- Forgetting to delete unused manual snapshots.
- Assuming snapshots automatically update.
- Using a very short retention period for production databases.

---

# Real-World DevOps Example

Before deploying a new application version:

```
Production Database

      │

      ▼

Create Manual Snapshot

      │

Deploy Application

      │

Problem Detected

      │

Restore Snapshot
```

This minimizes downtime and data loss during deployments.

---

# Interview Questions

### What types of backups does Amazon RDS support?

Amazon RDS supports Automated Backups and Manual Snapshots.

---

### What is Point-in-Time Recovery (PITR)?

Point-in-Time Recovery restores a database to a specific moment within the configured backup retention period.

---

### How long are automated backups retained?

The retention period is configurable from **1 to 35 days**.

---

### Do manual snapshots expire automatically?

No. Manual snapshots remain until they are deleted.

---

### Can an RDS database be restored over the existing instance?

No. Restoring creates a new DB instance.

---

# Key Takeaways

- Amazon RDS provides Automated Backups and Manual Snapshots.
- Automated Backups support Point-in-Time Recovery.
- Manual Snapshots never expire unless deleted.
- Configure an appropriate backup retention period.
- Always create a manual snapshot before major upgrades.
- Regularly test backup restoration as part of a disaster recovery strategy.