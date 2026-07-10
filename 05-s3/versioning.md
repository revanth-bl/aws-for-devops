# Amazon S3 Versioning

## Introduction

**Amazon S3 Versioning** is a feature that keeps multiple versions of an object in the same bucket.

When versioning is enabled:

- Overwriting an object does not replace the existing object.
- Deleting an object does not permanently remove it.
- Every version of an object is preserved with a unique Version ID.

Versioning helps protect against accidental deletion, data corruption, and unintended overwrites.

---

# Why Use Versioning?

Without versioning:

```
Upload report.pdf
        │
        ▼
Overwrite report.pdf
        │
        ▼
Old Version Lost
```

With versioning:

```
Upload report.pdf
        │
        ▼
Version 1
        │
        ▼
Update report.pdf
        │
        ▼
Version 2
        │
        ▼
Update report.pdf
        │
        ▼
Version 3
```

All previous versions remain available until they are deleted.

---

# How Versioning Works

Every object receives a unique **Version ID**.

Example:

```
Bucket

report.pdf

├── Version 1
├── Version 2
└── Version 3 (Current)
```

The latest version becomes the current version, while older versions remain stored.

---

# Version IDs

Each object version has its own identifier.

Example:

```
report.pdf

Version ID:
A1B2C3

Version ID:
D4E5F6

Version ID:
G7H8I9
```

AWS uses these Version IDs to retrieve or restore specific versions.

---

# Enabling Versioning

Steps:

1. Open the Amazon S3 Console.
2. Select the bucket.
3. Open the **Properties** tab.
4. Find **Bucket Versioning**.
5. Click **Enable**.
6. Save the changes.

Once enabled, all new object uploads are versioned.

---

# Object Updates

Suppose you upload:

```
resume.pdf
```

Later you upload another file with the same name.

Instead of replacing the original:

```
resume.pdf

├── Version 1
└── Version 2
```

Both versions are stored.

---

# Object Deletion

Without versioning:

```
Delete File
      │
      ▼
File Removed
```

With versioning:

```
Delete File
      │
      ▼
Delete Marker Created
      │
      ▼
Older Versions Still Exist
```

Deleting an object creates a **Delete Marker**, making the object appear deleted while preserving previous versions.

---

# Restoring Deleted Objects

If an object was accidentally deleted:

```
Current Version

Delete Marker
```

Remove the Delete Marker to make the most recent object version accessible again.

This allows quick recovery from accidental deletions.

---

# Versioning States

Amazon S3 supports three versioning states.

## 1. Unversioned

```
Bucket

Object
```

Only one version exists.

---

## 2. Versioning Enabled

```
Bucket

Object

├── Version 1
├── Version 2
└── Version 3
```

Every update creates a new version.

---

## 3. Versioning Suspended

No new versions are created, but existing versions remain stored.

Existing object versions are not deleted automatically.

---

# Versioning and Lifecycle Policies

Lifecycle Policies can manage object versions automatically.

Example:

```
Current Version

↓

Previous Versions

↓

Delete after 180 Days
```

This helps reduce storage costs while retaining recent versions.

---

# Benefits of Versioning

- Protects against accidental deletion.
- Protects against accidental overwrites.
- Supports data recovery.
- Simplifies rollback to previous versions.
- Improves backup strategies.
- Works with Lifecycle Policies and Cross-Region Replication.

---

# Best Practices

- Enable versioning on important buckets.
- Combine versioning with Lifecycle Policies.
- Enable server-side encryption for sensitive data.
- Regularly review storage costs, as multiple versions consume additional storage.
- Use IAM policies to control who can delete object versions.

---

# Common Mistakes

- Assuming deleted objects are permanently removed.
- Forgetting that every version consumes storage.
- Not using Lifecycle Policies to clean up old versions.
- Disabling versioning without understanding its impact.
- Ignoring storage costs for buckets with many object versions.

---

# Real-World DevOps Example

A CI/CD pipeline stores deployment packages.

```
Application Build

      │

      ▼

app.zip

Version 1

      │

New Deployment

      ▼

Version 2

      │

Deployment Issue

      ▼

Rollback to Version 1
```

Versioning allows teams to recover previous deployment artifacts quickly.

---

# Interview Questions

### What is Amazon S3 Versioning?

Amazon S3 Versioning is a feature that stores multiple versions of an object within the same bucket.

---

### What happens when you overwrite an object?

A new version of the object is created, while previous versions remain stored.

---

### What happens when you delete an object in a versioned bucket?

Amazon S3 creates a Delete Marker. Previous object versions remain available until they are permanently deleted.

---

### Can Versioning be disabled?

Versioning can be **suspended**, but it cannot be completely disabled after it has been enabled. Existing versions remain in the bucket.

---

### Why is Versioning important?

It protects against accidental deletion, overwrites, and data loss while enabling easy recovery of previous object versions.

---

# Key Takeaways

- Versioning stores multiple versions of the same object.
- Every object version has a unique Version ID.
- Deleting an object creates a Delete Marker instead of immediately removing previous versions.
- Versioning enables rollback and recovery.
- Lifecycle Policies can automatically manage old versions.
- Versioning is a recommended best practice for production S3 buckets.