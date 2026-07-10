# Static Website Hosting on AWS

## Project Overview

This project demonstrates how to host a static website using Amazon S3.

The website is publicly accessible over the internet and can optionally be integrated with Amazon Route 53 and Amazon CloudFront for custom domains, HTTPS, and global content delivery.

---

# Architecture

```
User
   │
   ▼
Route 53 (Optional)
   │
   ▼
CloudFront (Optional)
   │
   ▼
Amazon S3 Bucket
```

---

# AWS Services Used

- Amazon S3
- Route 53 (Optional)
- CloudFront (Optional)
- IAM

---

# Objectives

- Create an S3 bucket
- Enable Static Website Hosting
- Upload website files
- Configure bucket policy
- Access the website
- (Optional) Configure CloudFront
- (Optional) Configure Route 53

---

# Implementation Steps

## Step 1

Create an S3 Bucket.

## Step 2

Disable Block Public Access (for this demo).

## Step 3

Enable Static Website Hosting.

## Step 4

Upload HTML, CSS, and JavaScript files.

## Step 5

Configure Bucket Policy.

## Step 6

Access the Website Endpoint.

## Step 7 (Optional)

Configure CloudFront.

## Step 8 (Optional)

Configure Route 53.

---

# Folder Structure

```
static-website-hosting/

├── README.md
├── screenshots/
├── index.html
└── assets/
```

---

# Expected Result

A publicly accessible static website hosted on Amazon S3.

---

# Skills Demonstrated

- Amazon S3
- IAM
- Bucket Policies
- Static Website Hosting
- CloudFront
- Route 53

---

# Future Improvements

- HTTPS using CloudFront
- Custom Domain
- CI/CD Deployment
- Versioning