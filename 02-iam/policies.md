# IAM Policies

## Introduction

An **IAM Policy** is a JSON document that defines what actions are allowed or denied on AWS resources.

Policies are attached to:

- IAM Users
- IAM Groups
- IAM Roles

Instead of granting permissions directly, AWS evaluates the policies attached to an identity to determine whether a requested action is allowed.

---

# Why IAM Policies are Important

IAM Policies help organizations:

- Control access to AWS resources.
- Follow the Principle of Least Privilege.
- Improve security.
- Simplify permission management.
- Meet compliance requirements.

Without IAM Policies, every user would either have full access or no access at all.

---

# How IAM Policies Work

```
User / Group / Role
        │
        ▼
 IAM Policy (JSON)
        │
        ▼
 Allow or Deny Access
        │
        ▼
 AWS Resource
```

When a user makes a request, AWS evaluates all applicable policies before allowing or denying the action.

---

# Structure of an IAM Policy

An IAM policy is written in **JSON (JavaScript Object Notation)**.

A simple example:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListBucket",
      "Resource": "*"
    }
  ]
}
```

---

# Main Elements of an IAM Policy

## Version

Specifies the policy language version.

Example:

```json
"Version": "2012-10-17"
```

---

## Statement

Contains one or more permission rules.

```json
"Statement": [ ]
```

---

## Effect

Determines whether the action is allowed or denied.

Possible values:

- Allow
- Deny

Example:

```json
"Effect": "Allow"
```

---

## Action

Specifies the AWS API actions that are allowed or denied.

Examples:

- ec2:StartInstances
- ec2:StopInstances
- s3:GetObject
- s3:PutObject

---

## Resource

Specifies which AWS resource the policy applies to.

Examples:

```text
*
```

or

```text
arn:aws:s3:::my-bucket
```

---

# Types of IAM Policies

## 1. AWS Managed Policies

Policies created and maintained by AWS.

Examples:

- AmazonS3ReadOnlyAccess
- AmazonEC2FullAccess
- ReadOnlyAccess
- AdministratorAccess

**Advantages**

- Easy to use.
- Automatically updated by AWS.
- Suitable for common use cases.

---

## 2. Customer Managed Policies

Policies created and managed by your organization.

Advantages:

- Custom permissions.
- Reusable across multiple users, groups, or roles.
- Full control over updates.

---

## 3. Inline Policies

Policies embedded directly into a single user, group, or role.

Characteristics:

- One-to-one relationship.
- Cannot be shared.
- Deleted automatically when the identity is deleted.

---

# Managed Policy vs Inline Policy

| Managed Policy | Inline Policy |
|----------------|---------------|
| Reusable | Not reusable |
| Can be attached to multiple identities | Attached to only one identity |
| Easier to maintain | Best for unique permissions |

---

# Policy Evaluation Logic

When an AWS request is made:

1. AWS authenticates the identity.
2. AWS collects all applicable policies.
3. AWS evaluates the policies.
4. An explicit **Deny** always overrides an **Allow**.
5. If no policy allows the action, access is denied by default.

---

# Explicit Deny vs Implicit Deny

### Implicit Deny

If no policy allows an action, AWS denies it automatically.

### Explicit Deny

If any policy explicitly denies an action, access is denied even if another policy allows it.

Example:

```
Policy A → Allow S3 Access

Policy B → Deny S3 Access

Result → Access Denied
```

---

# Principle of Least Privilege

Grant only the permissions required to perform a specific task.

Instead of:

```
AdministratorAccess
```

Prefer:

```
AmazonS3ReadOnlyAccess
```

This reduces security risks.

---

# Best Practices

- Follow the Principle of Least Privilege.
- Use AWS Managed Policies when appropriate.
- Create Customer Managed Policies for custom requirements.
- Avoid attaching permissions directly to users.
- Attach policies to groups or roles whenever possible.
- Regularly review and remove unused permissions.
- Test policies before using them in production.

---

# Real-World Example

A company has three teams:

**Developers**

- Read and write to S3.
- Launch EC2 instances.

**Finance**

- Read billing reports only.

**Security Team**

- Manage IAM users and policies.

Each team receives different IAM policies based on its responsibilities.

---

# Interview Questions

### What is an IAM Policy?

An IAM Policy is a JSON document that defines permissions for AWS resources.

---

### What is the difference between AWS Managed Policies and Customer Managed Policies?

- **AWS Managed Policies:** Created and maintained by AWS.
- **Customer Managed Policies:** Created and maintained by the customer.

---

### What is an Inline Policy?

An Inline Policy is embedded directly into a single IAM user, group, or role and cannot be reused.

---

### What happens if no policy allows an action?

AWS applies an **Implicit Deny**, and the request is rejected.

---

### Which takes precedence: Allow or Explicit Deny?

**Explicit Deny** always overrides **Allow**.

---

# Key Takeaways

- IAM Policies define permissions in AWS.
- Policies are written in JSON.
- Policies can be attached to users, groups, and roles.
- AWS supports Managed Policies, Customer Managed Policies, and Inline Policies.
- AWS follows the **Implicit Deny** model by default.
- **Explicit Deny** always overrides **Allow**.
- Follow the **Principle of Least Privilege** to improve security.