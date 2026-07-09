# IAM Roles

## Introduction

An **IAM Role** is an AWS identity that provides **temporary permissions** to trusted users, applications, or AWS services.

Unlike an IAM User, a role does **not** have permanent credentials such as a password or access keys. Instead, it is **assumed** when needed, and AWS provides temporary security credentials.

IAM Roles are commonly used to allow AWS services or external identities to securely access AWS resources.

---

# Why Use IAM Roles?

Instead of storing long-term AWS credentials inside applications or sharing IAM user credentials, you can assign an IAM Role with the required permissions.

This improves security and simplifies access management.

---

# How IAM Roles Work

```
User / AWS Service / Application
               │
               ▼
         Assume IAM Role
               │
               ▼
Temporary Security Credentials
               │
               ▼
Access AWS Resources
```

The role grants temporary permissions only while it is being used.

---

# IAM User vs IAM Role

| IAM User | IAM Role |
|----------|-----------|
| Permanent identity | Temporary identity |
| Has username and password | No username or password |
| Can have long-term access keys | Uses temporary security credentials |
| Represents a person or application | Represents a set of permissions that can be assumed |

---

# Common Use Cases

## 1. EC2 Instance Access

Instead of storing AWS access keys on an EC2 instance, attach an IAM Role.

Example:

```
EC2 Instance
      │
      ▼
IAM Role
      │
      ▼
Amazon S3 Bucket
```

The EC2 instance automatically receives temporary credentials to access S3.

---

## 2. Lambda Functions

AWS Lambda functions often need to:

- Read from S3
- Write logs to CloudWatch
- Access DynamoDB
- Publish to SNS

An IAM Role provides these permissions securely.

---

## 3. Cross-Account Access

Organizations with multiple AWS accounts can use IAM Roles to grant access between accounts.

Example:

```
AWS Account A
      │
 Assume Role
      │
      ▼
AWS Account B
```

This avoids sharing IAM user credentials across accounts.

---

## 4. Federated Users

Users authenticated through providers such as:

- Microsoft Entra ID (Azure AD)
- Google
- Okta

can assume IAM Roles to access AWS resources without creating IAM users for each person.

---

# Trust Policy

Every IAM Role includes a **Trust Policy**.

A Trust Policy defines **who or what is allowed to assume the role**.

Examples of trusted entities:

- IAM Users
- AWS Services (EC2, Lambda, ECS)
- Another AWS Account
- Federated Identity Providers

Without a valid trust policy, a role cannot be assumed.

---

# Permissions Policy

An IAM Role also has one or more **Permissions Policies** attached.

These policies define **what actions the role can perform** after it has been assumed.

Example:

```
Trust Policy
      │
      ▼
Who can assume the role?

Permissions Policy
      │
      ▼
What can the role do?
```

---

# Creating an IAM Role

Using the AWS Management Console:

1. Open the IAM service.
2. Select **Roles**.
3. Click **Create role**.
4. Choose the trusted entity (AWS service, AWS account, or identity provider).
5. Attach the required IAM policies.
6. Review and create the role.

---

# Benefits of IAM Roles

- No long-term credentials.
- Improved security.
- Supports temporary access.
- Ideal for AWS services.
- Enables cross-account access.
- Simplifies permission management.
- Reduces the risk of credential exposure.

---

# Best Practices

- Use IAM Roles instead of storing access keys in applications.
- Grant only the permissions required (Principle of Least Privilege).
- Regularly review role permissions.
- Use separate roles for different workloads.
- Avoid using overly permissive policies such as `AdministratorAccess` unless absolutely necessary.

---

# Real-World Example

A web application running on an EC2 instance needs to upload images to an S3 bucket.

**Without an IAM Role:**

- Store AWS access keys on the EC2 instance.
- Rotate credentials manually.
- Risk exposing long-term credentials.

**With an IAM Role:**

- Attach an IAM Role to the EC2 instance.
- AWS automatically provides temporary credentials.
- The application uploads images securely without storing access keys.

---

# Interview Questions

### What is an IAM Role?

An IAM Role is an AWS identity that provides temporary permissions to trusted users, applications, or AWS services.

---

### What is the difference between an IAM User and an IAM Role?

An IAM User has permanent credentials, while an IAM Role provides temporary credentials that are assumed when needed.

---

### Why are IAM Roles more secure than storing access keys?

IAM Roles eliminate the need for long-term credentials by using temporary security credentials managed by AWS.

---

### What is a Trust Policy?

A Trust Policy defines who or what is allowed to assume an IAM Role.

---

### What is a common use case for IAM Roles?

Allowing an EC2 instance or Lambda function to securely access AWS services such as S3, DynamoDB, or CloudWatch without storing access keys.

---

# Key Takeaways

- IAM Roles provide temporary permissions.
- Roles do not have usernames, passwords, or long-term access keys.
- AWS services, users, applications, and external identities can assume roles.
- Every role has a **Trust Policy** and one or more **Permissions Policies**.
- IAM Roles are the recommended way to grant AWS services secure access to other AWS resources.