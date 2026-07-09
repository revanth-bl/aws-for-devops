# IAM Groups

## Introduction

An **IAM Group** is a collection of IAM users. Instead of assigning permissions to each user individually, you can assign permissions to a group, and every user in that group automatically inherits those permissions.

Groups make permission management easier, more consistent, and less error-prone.

---

# Why Use IAM Groups?

Managing permissions for each user individually becomes difficult as an organization grows.

For example, imagine a company has 50 developers. Assigning the same permissions to each developer one by one would be time-consuming and difficult to maintain.

Instead, you can:

- Create a **Developers** group.
- Attach the required IAM policies to the group.
- Add all developers to the group.

Now every developer automatically receives the required permissions.

---

# How IAM Groups Work

```
IAM Policy
      │
      ▼
 IAM Group
      │
      ▼
Multiple IAM Users
```

Permissions are attached to the group, not to individual users.

---

# Example

Company structure:

```
Developers Group
├── Alice
├── Bob
└── Charlie

Administrators Group
├── David
└── Emma

Finance Group
├── John
└── Sarah
```

Each group has different permissions based on job responsibilities.

---

# Benefits of IAM Groups

- Easier permission management
- Consistent access control
- Reduces administrative effort
- Simplifies onboarding new employees
- Supports the Principle of Least Privilege

---

# Common IAM Groups

Many organizations create groups such as:

- Administrators
- Developers
- DevOps
- Security
- Database Administrators (DBA)
- Finance
- HR
- ReadOnlyUsers

Each group receives permissions appropriate for its role.

---

# Creating an IAM Group

Using the AWS Management Console:

1. Open the IAM Dashboard.
2. Select **User groups**.
3. Click **Create group**.
4. Enter a group name.
5. Attach one or more IAM policies.
6. Add users to the group.
7. Create the group.

---

# Adding Users to a Group

A user can belong to one or more IAM groups.

Example:

```
User: Alice

Groups:
✔ Developers
✔ CloudWatch-ReadOnly
```

The user receives permissions from all assigned groups.

---

# IAM Groups and Policies

Permissions are granted by attaching IAM policies to groups.

Example:

```
Developers Group
│
├── AmazonEC2ReadOnlyAccess
├── AmazonS3ReadOnlyAccess
└── CloudWatchReadOnlyAccess
```

Every member of the Developers group inherits these permissions.

---

# IAM Groups vs IAM Users

| IAM User | IAM Group |
|----------|-----------|
| Represents one person or application | Represents a collection of users |
| Has individual credentials | Has no credentials |
| Can have policies attached | Can have policies attached |
| Can belong to multiple groups | Contains multiple users |

---

# Best Practices

- Assign permissions to groups instead of individual users whenever possible.
- Organize groups based on job roles.
- Follow the Principle of Least Privilege.
- Regularly review group membership.
- Remove users from groups when responsibilities change.
- Avoid granting unnecessary administrator access.

---

# Limitations of IAM Groups

- Groups cannot contain other groups.
- Groups cannot be used for temporary access.
- Groups do not have login credentials.
- AWS accounts have service quotas for the number of groups and users.

---

# Real-World Example

A software company has:

- 30 Developers
- 10 DevOps Engineers
- 5 Security Engineers

Instead of configuring permissions for all 45 users individually:

- Create a **Developers** group.
- Create a **DevOps** group.
- Create a **Security** group.

Attach the appropriate policies to each group.

When a new developer joins, simply add them to the **Developers** group.

---

# Interview Questions

### What is an IAM Group?

An IAM Group is a collection of IAM users that share the same permissions.

---

### Can an IAM Group have login credentials?

No. Only IAM users have login credentials.

---

### Can a user belong to multiple IAM Groups?

Yes. A user can belong to multiple IAM groups and inherits permissions from all of them.

---

### Can an IAM Group contain another IAM Group?

No. Nested IAM groups are not supported.

---

### Why should permissions be assigned to groups instead of individual users?

Assigning permissions to groups simplifies management, ensures consistency, and reduces administrative overhead.

---

# Key Takeaways

- IAM Groups simplify permission management.
- Permissions are attached to groups through IAM policies.
- Users inherit permissions from the groups they belong to.
- A user can belong to multiple groups.
- Groups have no credentials and cannot be used to sign in.
- Using groups follows AWS security best practices and makes administration more efficient.