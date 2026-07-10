# Application Load Balancer (ALB)

## Introduction

An **Application Load Balancer (ALB)** is a Layer 7 load balancer provided by AWS Elastic Load Balancing (ELB).

It distributes incoming HTTP and HTTPS traffic across multiple targets, such as:

- Amazon EC2 instances
- Containers (Amazon ECS)
- IP addresses
- AWS Lambda functions

By spreading traffic across multiple resources, an ALB improves:

- High availability
- Scalability
- Fault tolerance
- Application performance

---

# Why Use an Application Load Balancer?

Without a Load Balancer:

```
Users
   │
   ▼
Single EC2 Instance
```

If the EC2 instance fails, the application becomes unavailable.

With an ALB:

```
Users
   │
   ▼
Application Load Balancer
   │
   ├─────────────┐
   ▼             ▼
EC2 Instance 1  EC2 Instance 2
```

Traffic is automatically distributed between healthy instances.

---

# How ALB Works

```
Internet
      │
      ▼
Application Load Balancer
      │
      ├───────────────┐
      ▼               ▼
EC2 Instance 1   EC2 Instance 2
```

The ALB receives requests from users and forwards them to healthy targets.

---

# Layer 7 Load Balancer

The Application Load Balancer operates at **Layer 7 (Application Layer)** of the OSI model.

It understands:

- HTTP
- HTTPS
- URLs
- Host names
- HTTP headers
- Query strings

Because it understands application traffic, it can make intelligent routing decisions.

---

# ALB Features

Amazon ALB provides:

- Layer 7 routing
- HTTPS support
- SSL/TLS termination
- Path-based routing
- Host-based routing
- Health checks
- WebSocket support
- HTTP/2 support
- Integration with Auto Scaling

---

# Listener

A **Listener** checks for incoming connection requests.

Example:

```
HTTP
Port 80

HTTPS
Port 443
```

When traffic arrives, the listener evaluates its rules and forwards requests to the appropriate Target Group.

---

# Listener Rules

Listener rules define how traffic is routed.

Example:

```
URL

/app/*

↓

Application Servers
```

```
URL

/images/*

↓

Image Servers
```

Rules can be based on:

- URL path
- Host name
- HTTP headers
- Query parameters

---

# Target Groups

An ALB forwards requests to **Target Groups**.

Example:

```
Application Load Balancer

        │

        ▼

Target Group

        │

        ├──────────────┐

        ▼              ▼

EC2-1          EC2-2
```

Each Target Group contains one or more registered targets.

---

# Health Checks

The ALB continuously checks the health of registered targets.

Healthy:

```
EC2 Instance

Status

Healthy
```

Unhealthy:

```
EC2 Instance

Status

Unhealthy
```

Traffic is automatically routed only to healthy targets.

---

# Path-Based Routing

Different URLs can be routed to different applications.

Example:

```
example.com/app

↓

Application Servers
```

```
example.com/api

↓

API Servers
```

This allows multiple applications to share one ALB.

---

# Host-Based Routing

Traffic can also be routed using domain names.

Example:

```
app.example.com

↓

Application Servers
```

```
admin.example.com

↓

Admin Servers
```

---

# HTTPS Support

The ALB supports SSL/TLS encryption.

```
Client

HTTPS

↓

Application Load Balancer

↓

HTTP or HTTPS

↓

EC2 Instance
```

AWS Certificate Manager (ACM) can be used to manage SSL certificates.

---

# Integration with Auto Scaling

```
Users

      │

      ▼

Application Load Balancer

      │

      ▼

Auto Scaling Group

      │

      ├─────────────┐

      ▼             ▼

EC2-1         EC2-2
```

As new EC2 instances are launched, they are automatically registered with the ALB.

---

# Real-World DevOps Example

An e-commerce website:

```
                Internet
                    │
                    ▼
        Application Load Balancer
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
 Web Server 1             Web Server 2
        │                       │
        └───────────┬───────────┘
                    ▼
              Amazon RDS
```

Users are automatically distributed across multiple web servers, improving availability and scalability.

---

# Best Practices

- Deploy the ALB across multiple Availability Zones.
- Enable HTTPS using AWS Certificate Manager.
- Configure health checks correctly.
- Use Target Groups to organize backend services.
- Combine the ALB with Auto Scaling for dynamic scaling.
- Monitor ALB metrics using Amazon CloudWatch.

---

# Common Mistakes

- Registering unhealthy targets.
- Forgetting to configure health checks.
- Exposing backend EC2 instances directly to the internet.
- Not enabling HTTPS.
- Using one Target Group for unrelated applications.

---

# Interview Questions

### What is an Application Load Balancer?

An Application Load Balancer is a Layer 7 load balancer that distributes HTTP and HTTPS traffic across multiple targets.

---

### Which OSI layer does an ALB operate on?

Layer 7 (Application Layer).

---

### What is the purpose of a Target Group?

A Target Group contains one or more backend resources that receive traffic from the ALB.

---

### What are Health Checks?

Health Checks monitor backend targets and ensure traffic is sent only to healthy resources.

---

### Can an ALB perform path-based routing?

Yes. An ALB supports path-based and host-based routing.

---

# Key Takeaways

- ALB operates at Layer 7 of the OSI model.
- It distributes HTTP and HTTPS traffic.
- Supports path-based and host-based routing.
- Uses Target Groups to route requests.
- Performs automatic health checks.
- Integrates seamlessly with Auto Scaling for highly available applications.