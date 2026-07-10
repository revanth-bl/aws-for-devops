# Amazon S3 Buckets

## Introduction

**Amazon Simple Storage Service (Amazon S3)** is a highly scalable object storage service provided by AWS.

It is designed to store and retrieve virtually unlimited amounts of data from anywhere over the internet.

Unlike Amazon EBS, which provides block storage, Amazon S3 stores data as **objects** inside **buckets**.

Amazon S3 is widely used for:

- Backup and recovery
- Static website hosting
- Storing application assets
- Log storage
- Data lakes
- CI/CD artifacts
- Disaster recovery

---

# What is an S3 Bucket?

A **Bucket** is a container used to store objects in Amazon S3.

Think of it like a folder on your computer, except it exists in AWS and can store billions of objects.

Example:

```
my-company-storage

├── images/
├── videos/
├── documents/
├── backups/
└── logs/
```

Every object belongs to exactly one bucket.

---

# What is an Object?

An **Object** is the basic unit of storage in Amazon S3.

Each object consists of:

- Data (the file)
- Object Key (filename/path)
- Metadata
- Version ID (if versioning is enabled)

Example:

```
Bucket

images/

└── logo.png
```

Here:

- Bucket = `my-company-storage`
- Object Key = `images/logo.png`

---

# Bucket Naming Rules

Bucket names must:

- Be globally unique.
- Contain 3 to 63 characters.
- Use lowercase letters, numbers, and hyphens (`-`).
- Start and end with a letter or number.
- Not contain spaces or uppercase letters.

Examples:

```
company-backups
project-assets
devops-storage
```

Invalid examples:

```
MyBucket
My Bucket
bucket_01
```

---

# S3 Bucket Architecture

```
Amazon S3

└── Bucket
      │
      ├── image.png
      ├── backup.zip
      ├── logs.txt
      └── videos/
```

A bucket stores objects and organizes them using object keys.

---

# Bucket Regions

Every bucket is created in a specific AWS Region.

Example:

```
Bucket

Region:
ap-south-1 (Mumbai)
```

Although the bucket belongs to one Region, it can be accessed from anywhere if permissions allow.

---

# Bucket Permissions

Access to buckets is controlled using:

- IAM Policies
- Bucket Policies
- Access Control Lists (ACLs)
- AWS Organizations (optional)

By default, new buckets are private.

---

# Public vs Private Buckets

## Private Bucket

```
Internet
    │
    ▼
 Access Denied
```

Only authorized users or applications can access the data.

---

## Public Bucket

```
Internet
    │
    ▼
Public Bucket
    │
    ▼
Images
Videos
Documents
```

Public buckets are commonly used for:

- Static website assets
- Public images
- Downloadable files

Avoid making buckets public unless required.

---

# Common Bucket Operations

Amazon S3 supports:

- Create bucket
- Upload objects
- Download objects
- Copy objects
- Move objects
- Delete objects
- List objects

---

# Bucket Features

Amazon S3 provides:

- High durability (11 nines)
- High availability
- Automatic scaling
- Strong read-after-write consistency
- Encryption support
- Versioning
- Lifecycle management
- Cross-Region Replication (optional)

---

# S3 Storage Model

```
Bucket

├── image.jpg
├── report.pdf
├── backup.sql
├── app.zip
└── logs/
```

Unlike a traditional file system, folders are created by object key prefixes.

---

# Real-World DevOps Example

A CI/CD pipeline stores build artifacts.

```
Developer
     │
     ▼
Git Repository
     │
     ▼
CI/CD Pipeline
     │
     ▼
Amazon S3 Bucket
     │
     ▼
Deployment
```

The pipeline uploads application packages to S3 before deploying them to EC2 or other AWS services.

---

# Best Practices

- Use meaningful bucket names.
- Enable versioning for important data.
- Block public access unless necessary.
- Encrypt sensitive objects.
- Organize objects using prefixes.
- Apply lifecycle rules to reduce storage costs.
- Enable logging and monitoring.

---

# Common Mistakes

- Making buckets publicly accessible without need.
- Using weak bucket naming conventions.
- Storing sensitive data without encryption.
- Deleting objects without versioning enabled.
- Ignoring lifecycle policies for old data.

---

# Interview Questions

### What is Amazon S3?

Amazon S3 is an object storage service that stores data as objects inside buckets.

---

### What is an S3 Bucket?

An S3 Bucket is a container used to store objects.

---

### What is an Object in Amazon S3?

An object consists of the file, metadata, and an object key that uniquely identifies it within a bucket.

---

### Are bucket names unique?

Yes. Bucket names must be globally unique across all AWS accounts.

---

### Is an S3 bucket public by default?

No. New S3 buckets are private by default.

---

# Key Takeaways

- Amazon S3 is AWS's object storage service.
- Buckets store objects.
- Every object belongs to one bucket.
- Bucket names must be globally unique.
- New buckets are private by default.
- S3 is highly durable, scalable, and widely used for backups, websites, logs, and CI/CD pipelines.