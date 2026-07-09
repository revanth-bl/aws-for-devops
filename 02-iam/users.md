# IAM Users

## Introduction

An **IAM User** is an identity created in AWS that represents a person, application, or service that needs access to AWS resources.

Each IAM User can have its own:

- Username
- Password (for AWS Console access)
- Access keys (for AWS CLI/API access)
- Permissions

IAM Users are used to securely control who can access AWS resources and what actions they can perform.

---

# Why Use IAM Users?

IAM Users allow organizations to provide individual access to AWS without sharing credentials.

Example:

Instead of multiple developers using one AWS account password:

```
Developer A → IAM User
Developer B → IAM User
Developer C → IAM User
```

Each user has separate credentials and permissions.

---

# IAM User Components

An IAM User can have:

## 1. Username

A unique identifier for the user.

Example:

```
john-devops
```

---

## 2. Password

Used for signing into the AWS Management Console.

Example:

```
AWS Console Login
        │
        ▼
Username + Password
```

---

## 3. Access Keys

Used for programmatic access through:

- AWS CLI
- AWS SDK
- APIs
- Automation scripts

Access keys contain:

- Access Key ID
- Secret Access Key

Example:

```
AWS CLI
   │
   ▼
Access Keys
   │
   ▼
AWS Services
```

---

# IAM User Permissions

By default, a new IAM User has **no permissions**.

Permissions must be granted using IAM Policies.

Permissions can be assigned through:

- User Policies
- Group Policies
- Role Assumption

Example:

```
IAM User
    │
    ▼
IAM Group
    │
    ▼
IAM Policy
    │
    ▼
AWS Resource Access
```

---

# IAM Users and Groups

The recommended approach is to assign permissions through groups.

Example:

```
Developers Group

├── Alice
├── Bob
└── Charlie

Policies:
- EC2 Access
- S3 Access
- CloudWatch Access
```

When a new developer joins, simply add them to the Developers group.

---

# IAM User Authentication

IAM Users can authenticate using:

## AWS Management Console

Uses:

- Username
- Password
- MFA

Example:

```
Browser
   │
   ▼
AWS Console Login
```

---

## AWS CLI / SDK

Uses:

- Access Key ID
- Secret Access Key

Example:

```
Terminal
    │
    ▼
AWS CLI
    │
    ▼
AWS API
```

---

# Creating an IAM User

Using AWS Console:

1. Open the IAM service.
2. Select **Users**.
3. Click **Create user**.
4. Enter the username.
5. Select access type:
   - Console access
   - Programmatic access
6. Attach permissions.
7. Enable MFA.
8. Create the user.

---

# IAM User vs Root User

| Root User | IAM User |
|-----------|----------|
| Created when AWS account is created | Created by administrators |
| Has complete account access | Limited permissions |
| Uses account email address | Uses assigned username |
| Should rarely be used | Used for daily operations |

---

# IAM User vs IAM Role

| IAM User | IAM Role |
|----------|----------|
| Permanent identity | Temporary identity |
| Has credentials | No permanent credentials |
| Represents a person/application | Represents permissions |
| Used by humans mainly | Used by AWS services and applications |

---

# Best Practices

## 1. Avoid Using Root User

Use the root account only for:

- Account setup
- Billing changes
- Account recovery

Do normal work using IAM Users.

---

## 2. Enable MFA

Enable MFA for:

- Root User
- Administrator Users
- Privileged Accounts

---

## 3. Follow Least Privilege

Give users only the permissions they need.

Example:

A developer who only needs S3 access should not receive full administrator permissions.

---

## 4. Do Not Share Credentials

Each person should have their own IAM User.

Avoid:

```
admin@example.com
SharedPassword123
```

---

## 5. Rotate Access Keys

Regularly review and rotate access keys.

Remove unused credentials.

---

# Real-World Example

A company has:

- Developers
- DevOps Engineers
- Security Engineers

Each employee receives an IAM User.

Example:

```
Developer:
- EC2 access
- S3 access

DevOps Engineer:
- EC2
- VPC
- CloudFormation

Security Engineer:
- IAM
- CloudTrail
- Security services
```

Each user gets only the required permissions.

---

# Common Mistakes

- Using the root account for daily tasks.
- Sharing IAM credentials.
- Giving AdministratorAccess to everyone.
- Creating unnecessary access keys.
- Not enabling MFA.
- Keeping unused users active.

---

# Interview Questions

### What is an IAM User?

An IAM User is an identity created in AWS that represents a person or application requiring access to AWS resources.

---

### Does a new IAM User have permissions by default?

No. A new IAM User has no permissions until policies are attached.

---

### What are IAM User access keys used for?

Access keys are used for programmatic access through AWS CLI, SDKs, and APIs.

---

### Why should we avoid using the root user?

The root user has unrestricted access to the entire AWS account. Using it daily increases security risk.

---

### What is the best way to assign permissions to IAM Users?

Assign users to IAM Groups and attach policies to groups.

---

# Key Takeaways

- IAM Users represent people or applications in AWS.
- Users can access AWS through Console or CLI/API.
- New users have no permissions by default.
- Permissions are controlled using IAM Policies.
- Use Groups to manage permissions efficiently.
- Enable MFA and follow the Principle of Least Privilege.
- Avoid using the root user for daily activities.