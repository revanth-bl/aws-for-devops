# EC2 Key Pairs

## Introduction

An **EC2 Key Pair** is a security mechanism used to securely connect to an Amazon EC2 instance.

Key pairs use **public key cryptography** to authenticate users without sending passwords over the network.

A key pair consists of:

- Public Key
- Private Key

AWS stores the public key, while the user keeps the private key securely.

---

# How EC2 Key Pairs Work

```
        User
         │
         │  Private Key
         ▼
   Authentication Request
         │
         ▼
     EC2 Instance
         │
         │  Public Key
         ▼
   Access Granted
```

The private key proves that the user owns the matching public key stored on the EC2 instance.

---

# Components of a Key Pair

## 1. Public Key

- Stored inside the EC2 instance.
- Can be shared safely.
- Used to verify authentication.

Example:

```
~/.ssh/authorized_keys
```

---

## 2. Private Key

- Downloaded by the user when creating the key pair.
- Must be kept secret.
- Used to connect to the EC2 instance.

Common file formats:

```
.pem
.ppk
```

Example:

```
my-server-key.pem
```

---

# Why Use Key Pairs?

Key pairs provide:

- Secure authentication
- Passwordless login
- Protection against brute-force password attacks
- Automated server access
- Better security for cloud environments

---

# Creating an EC2 Key Pair

Steps:

1. Open AWS Management Console.
2. Navigate to EC2.
3. Select **Key Pairs**.
4. Click **Create Key Pair**.
5. Enter a key pair name.
6. Choose key type:
   - RSA
   - ED25519
7. Choose private key format:
   - `.pem` for OpenSSH
   - `.ppk` for PuTTY
8. Download the private key.

Example:

```
devops-key.pem
```

---

# Connecting to a Linux EC2 Instance Using SSH

Example command:

```bash
ssh -i devops-key.pem ec2-user@<public-ip>
```

For Ubuntu:

```bash
ssh -i devops-key.pem ubuntu@<public-ip>
```

---

# Private Key Permissions

The private key file must have restricted permissions.

Linux/macOS:

```bash
chmod 400 devops-key.pem
```

This prevents unauthorized users from reading the key.

---

# Windows SSH Access

Windows supports SSH through:

- Windows Terminal
- PowerShell
- OpenSSH Client
- PuTTY

Example:

```powershell
ssh -i devops-key.pem ec2-user@<public-ip>
```

---

# Key Pair During EC2 Launch

When creating an EC2 instance:

```
Launch Instance
        │
        ▼
Choose AMI
        │
        ▼
Choose Instance Type
        │
        ▼
Select Key Pair
        │
        ▼
Launch Instance
```

The selected key pair allows secure access to the instance.

---

# Lost Private Key

AWS does not store your private key.

If the private key is lost:

- You cannot download it again.
- You cannot connect using that key.

Possible recovery methods:

- Create a new key pair.
- Attach the EBS volume to another instance.
- Modify the SSH authorized keys.
- Use AWS Systems Manager Session Manager.

---

# Key Pair Best Practices

- Never share private keys.
- Store private keys securely.
- Do not upload `.pem` files to GitHub.
- Use different keys for different environments.
- Rotate keys when required.
- Remove unused keys.
- Enable additional security controls like MFA.

---

# Key Pair Security Example

Bad practice:

```
GitHub Repository

├── application-code
└── production-server.pem  ❌
```

Anyone who obtains the key could potentially access the server.

Good practice:

```
GitHub Repository

├── application-code
└── .gitignore
        │
        └── *.pem
```

Private keys should never be committed.

---

# EC2 Key Pair vs Password Authentication

| Key Pair | Password |
|----------|----------|
| Uses cryptographic authentication | Uses password authentication |
| More secure | Easier to attack |
| No password sharing | Password can be leaked |
| Standard for cloud servers | Usually disabled in production |

---

# Real-World DevOps Example

A DevOps engineer needs to manage production EC2 servers.

Instead of sharing passwords:

```
Engineer
    │
    ▼
Private Key
    │
    ▼
SSH Connection
    │
    ▼
EC2 Instance
```

Each engineer receives controlled access using secure authentication methods.

---

# Interview Questions

### What is an EC2 Key Pair?

An EC2 Key Pair is a public-private key combination used to securely access EC2 instances.

---

### Where is the private key stored?

The private key is downloaded by the user and must be stored securely.

---

### Does AWS keep a copy of the private key?

No. AWS only stores the public key.

---

### What happens if you lose the private key?

You cannot directly connect using that key. You must use recovery methods such as replacing the SSH key.

---

### Why should private keys not be uploaded to GitHub?

Anyone with access to the private key could potentially gain unauthorized access to the EC2 instance.

---

# Key Takeaways

- EC2 Key Pairs provide secure instance authentication.
- Public keys are stored on EC2; private keys are kept by users.
- Private keys must never be shared or exposed.
- SSH access to Linux EC2 instances commonly uses key pairs.
- Losing a private key requires recovery steps because AWS cannot restore it.