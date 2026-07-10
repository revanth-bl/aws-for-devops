# Amazon ELB Target Groups

## Introduction

A **Target Group** is a logical collection of backend resources that receive traffic from an AWS Load Balancer.

Instead of sending requests directly to EC2 instances, the Load Balancer forwards requests to a Target Group. The Target Group then distributes traffic to its registered targets.

Target Groups are used by:

- Application Load Balancer (ALB)
- Network Load Balancer (NLB)
- Gateway Load Balancer (GWLB)

---

# Why Use Target Groups?

Without a Target Group:

```
Users
   │
   ▼
Load Balancer
   │
   ▼
Single Server
```

If the server fails, the application becomes unavailable.

With a Target Group:

```
Users
   │
   ▼
Load Balancer
   │
   ▼
Target Group
   │
 ┌─┴────────────┐
 ▼              ▼
EC2-1        EC2-2
```

Traffic is automatically distributed among healthy targets.

---

# How Target Groups Work

```
Internet
     │
     ▼
Load Balancer
     │
     ▼
Target Group
     │
 ┌───┴───────────┐
 ▼               ▼
Server 1     Server 2
```

The Load Balancer sends requests to the Target Group, which routes traffic only to healthy targets.

---

# Supported Target Types

A Target Group can contain different types of backend resources.

Supported target types include:

- Amazon EC2 Instances
- IP Addresses
- AWS Lambda Functions (ALB only)

Example:

```
Target Group

├── EC2 Instance
├── EC2 Instance
└── EC2 Instance
```

---

# Health Checks

Target Groups continuously monitor the health of registered targets.

Healthy:

```
EC2-1

Status

Healthy
```

Unhealthy:

```
EC2-2

Status

Unhealthy
```

Traffic is automatically routed only to healthy targets.

Health checks can use:

- HTTP
- HTTPS
- TCP

Depending on the type of Load Balancer.

---

# Listener and Target Group Relationship

```
Client

      │

      ▼

Listener (Port 80 / 443)

      │

      ▼

Target Group

      │

      ├─────────────┐

      ▼             ▼

EC2-1         EC2-2
```

The Listener receives incoming traffic, evaluates its rules, and forwards requests to the appropriate Target Group.

---

# Multiple Target Groups

A single Load Balancer can use multiple Target Groups.

Example:

```
Application Load Balancer

        │

 ┌──────┴──────────┐

 ▼                 ▼

Target Group A   Target Group B

 ▼                 ▼

App Servers     API Servers
```

This allows one Load Balancer to serve multiple applications or services.

---

# Target Registration

Targets can be registered:

- Automatically through Auto Scaling Groups
- Manually using the AWS Console
- Using the AWS CLI
- Using Infrastructure as Code (CloudFormation, Terraform)

As new EC2 instances are launched, they can automatically join the Target Group.

---

# Deregistration

When an instance is no longer needed:

```
EC2 Instance

↓

Deregister

↓

Stops Receiving Traffic
```

Existing connections can be completed before the instance is removed (connection draining/deregistration delay).

---

# Target Group Attributes

Common Target Group settings include:

- Health check path
- Health check interval
- Healthy threshold
- Unhealthy threshold
- Port
- Protocol
- Deregistration delay
- Stickiness (for ALB)

These settings help control traffic routing and application behavior.

---

# Real-World DevOps Example

An e-commerce application:

```
                    Internet
                        │
                        ▼
          Application Load Balancer
                        │
            ┌───────────┴───────────┐
            ▼                       ▼
      Web Target Group        API Target Group
            │                       │
      ┌─────┴─────┐           ┌─────┴─────┐
      ▼           ▼           ▼           ▼
   EC2-1       EC2-2       EC2-3       EC2-4
```

The ALB routes web traffic and API requests to separate Target Groups, improving scalability and organization.

---

# Best Practices

- Configure accurate health checks.
- Register multiple targets for high availability.
- Use Auto Scaling with Target Groups.
- Separate applications into different Target Groups.
- Monitor target health using Amazon CloudWatch.
- Remove unhealthy or unused targets promptly.

---

# Common Mistakes

- Registering unhealthy instances.
- Using one Target Group for unrelated applications.
- Misconfiguring health check paths.
- Forgetting to deregister terminated instances (when not using Auto Scaling).
- Ignoring health check failures.

---

# Interview Questions

### What is a Target Group?

A Target Group is a collection of backend resources that receive traffic from an AWS Load Balancer.

---

### Which Load Balancers use Target Groups?

Application Load Balancers (ALB), Network Load Balancers (NLB), and Gateway Load Balancers (GWLB).

---

### What is the purpose of Health Checks?

Health Checks determine whether a target is healthy. The Load Balancer sends traffic only to healthy targets.

---

### Can one Load Balancer use multiple Target Groups?

Yes. A single Load Balancer can forward traffic to multiple Target Groups based on listener rules.

---

### Can Target Groups automatically register EC2 instances?

Yes. When used with Auto Scaling Groups, new EC2 instances can be automatically registered and deregistered.

---

# Key Takeaways

- Target Groups connect Load Balancers to backend resources.
- They support EC2 instances, IP addresses, and AWS Lambda (ALB).
- Health Checks ensure traffic is routed only to healthy targets.
- Multiple Target Groups allow one Load Balancer to support multiple applications.
- Target Groups integrate seamlessly with Auto Scaling for dynamic environments.
- Proper Target Group configuration is essential for high availability and reliable traffic distribution.