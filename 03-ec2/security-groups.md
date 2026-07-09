# EC2 Security Groups

## Introduction

An **Amazon EC2 Security Group** is a virtual firewall that controls inbound and outbound traffic for EC2 instances.

Security Groups determine:

- Who can connect to an EC2 instance.
- Which ports are accessible.
- Which protocols are allowed.
- What outbound connections are permitted.

Security Groups operate at the instance level and are one of the primary security mechanisms in AWS networking.

---

# How Security Groups Work

```
                Internet
                   │
                   ▼
            Security Group
                   │
                   ▼
             EC2 Instance
```

When traffic reaches an EC2 instance, AWS checks the Security Group rules before allowing or denying access.

---

# Security Group Rules

Security Groups contain two types of rules:

1. Inbound Rules
2. Outbound Rules

---

# Inbound Rules

Inbound rules control incoming traffic to an EC2 instance.

Examples:

Allow SSH:

```
Type: SSH
Port: 22
Protocol: TCP
Source: Your IP Address
```

Allow Web Traffic:

```
Type: HTTP
Port: 80
Protocol: TCP
Source: 0.0.0.0/0
```

Allow HTTPS:

```
Type: HTTPS
Port: 443
Protocol: TCP
Source: 0.0.0.0/0
```

---

# Outbound Rules

Outbound rules control traffic leaving the EC2 instance.

By default:

```
Allow All Outbound Traffic
```

Example:

An EC2 instance can:

- Download software updates.
- Connect to external APIs.
- Access AWS services.

---

# Security Group Characteristics

## 1. Stateful Firewall

Security Groups are stateful.

This means:

If inbound traffic is allowed, the response traffic is automatically allowed.

Example:

```
User
 │
 ▼
EC2 Server
 │
 ▼
Response
```

No separate outbound rule is required for the response.

---

## 2. Allow Rules Only

Security Groups support:

- Allow rules

They do not support:

- Explicit deny rules

If traffic does not match an allow rule, it is automatically denied.

---

## 3. Attached to EC2 Instances

A Security Group is associated with network interfaces (ENIs) attached to EC2 instances.

---

## 4. Multiple Security Groups

An EC2 instance can have multiple Security Groups.

Example:

```
EC2 Instance

├── Web Security Group
│
└── Monitoring Security Group
```

All rules from attached Security Groups are combined.

---

# Common Security Group Ports

| Service | Port | Protocol |
|---------|------|----------|
| SSH | 22 | TCP |
| HTTP | 80 | TCP |
| HTTPS | 443 | TCP |
| RDP | 3389 | TCP |
| MySQL | 3306 | TCP |
| PostgreSQL | 5432 | TCP |

---

# Security Group Example

A web server architecture:

```
              Users
                │
                ▼
        Security Group

        Allow:
        HTTP  : 80
        HTTPS : 443

                │
                ▼

             EC2 Web Server
```

Only web traffic is allowed.

SSH access can be restricted:

```
SSH Port 22
Source:
Administrator IP only
```

---

# Security Group vs Network ACL

Security Groups and Network ACLs both control network traffic, but they work differently.

| Security Group | Network ACL |
|----------------|-------------|
| Instance level | Subnet level |
| Stateful | Stateless |
| Allow rules only | Allow and Deny rules |
| Evaluated at instance | Evaluated at subnet boundary |
| No rule numbering | Rules evaluated by priority |

---

# Creating a Security Group

Steps:

1. Open EC2 Dashboard.
2. Select Security Groups.
3. Click Create Security Group.
4. Provide:
   - Security group name
   - Description
   - VPC
5. Add inbound rules.
6. Add outbound rules.
7. Attach it to EC2 instances.

---

# Security Group Best Practices

## 1. Restrict SSH Access

Bad:

```
SSH
Port: 22
Source: 0.0.0.0/0
```

Anyone on the internet can attempt access.

Better:

```
SSH
Port: 22
Source: Your IP Address
```

---

## 2. Use Least Privilege

Only open required ports.

Example:

A database server should not allow public internet access.

---

## 3. Separate Security Groups

Use different Security Groups for different layers.

Example:

```
Web Layer Security Group

Allow:
80,443


Application Layer Security Group

Allow:
8080


Database Layer Security Group

Allow:
3306
```

---

## 4. Avoid Unnecessary Rules

Remove:

- Unused ports
- Old IP addresses
- Temporary access rules

---

## 5. Use Security Group References

Instead of allowing IP addresses, allow communication between Security Groups.

Example:

```
Application SG
        │
        ▼
Database SG
```

Only application servers can access the database.

---

# Real-World DevOps Example

Three-tier application:

```
Internet
   │
   ▼
Load Balancer
   │
   ▼
Web Servers
   │
   ▼
Application Servers
   │
   ▼
Database
```

Security Groups:

```
Load Balancer SG
Allow:
80,443


Web Server SG
Allow:
Traffic from Load Balancer SG


Database SG
Allow:
Traffic from Application SG
```

This creates a secure layered architecture.

---

# Common Mistakes

- Opening SSH (22) to everyone.
- Allowing database ports publicly.
- Using overly broad rules.
- Forgetting to remove temporary access.
- Using the default Security Group for everything.

---

# Interview Questions

### What is an EC2 Security Group?

A Security Group is a virtual firewall that controls inbound and outbound traffic for EC2 instances.

---

### Are Security Groups stateful or stateless?

Security Groups are stateful.

---

### Can Security Groups deny traffic?

No. Security Groups only support allow rules. Anything not allowed is automatically denied.

---

### What happens if an inbound rule allows SSH?

The EC2 instance can accept SSH connections on port 22 from the specified source.

---

### Difference between Security Groups and Network ACLs?

Security Groups work at the instance level and are stateful, while Network ACLs work at the subnet level and are stateless.

---

# Key Takeaways

- Security Groups act as virtual firewalls for EC2 instances.
- They control inbound and outbound traffic.
- Security Groups are stateful.
- Only allow rules can be created.
- Restrict access using the Principle of Least Privilege.
- Never expose sensitive ports publicly.
- Security Groups are essential for securing AWS workloads.