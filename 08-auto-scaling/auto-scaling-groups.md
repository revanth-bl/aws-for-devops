# Amazon EC2 Auto Scaling Groups (ASG)

## Introduction

**Amazon EC2 Auto Scaling** is an AWS service that automatically launches or terminates EC2 instances based on application demand.

The core component of this service is the **Auto Scaling Group (ASG)**.

An Auto Scaling Group manages a collection of EC2 instances to ensure that:

- The desired number of instances is always running.
- Failed instances are automatically replaced.
- Capacity increases during high traffic.
- Capacity decreases during low traffic.

This helps improve application availability while optimizing infrastructure costs.

---

# Why Use Auto Scaling?

Without Auto Scaling:

```
Users
   │
   ▼
Single EC2 Instance

High Traffic

↓

Slow Performance
```

The application may become overloaded during traffic spikes.

With Auto Scaling:

```
Users
   │
   ▼
Application Load Balancer
   │
   ▼
Auto Scaling Group
   │
 ┌─┼──────────────┐
 ▼ ▼              ▼
EC2-1          EC2-2          EC2-3
```

Additional EC2 instances are launched automatically when demand increases.

---

# How Auto Scaling Works

```
Users
     │
     ▼
Application Load Balancer
     │
     ▼
Auto Scaling Group
     │
 ┌───┴───────────┐
 ▼               ▼
EC2 Instance   EC2 Instance
```

The Auto Scaling Group monitors the application and adjusts the number of EC2 instances based on configured scaling policies.

---

# Auto Scaling Group Components

An Auto Scaling Group consists of:

- Launch Template (or Launch Configuration)
- Minimum Capacity
- Desired Capacity
- Maximum Capacity
- Scaling Policies
- Health Checks

Together, these define how the group behaves.

---

# Launch Template

A **Launch Template** defines how new EC2 instances should be created.

It includes:

- Amazon Machine Image (AMI)
- Instance Type
- Security Groups
- Key Pair
- Storage Configuration
- IAM Role
- User Data

Every new instance launched by the ASG uses this template.

---

# Capacity Settings

Every Auto Scaling Group has three capacity values.

## Minimum Capacity

The smallest number of EC2 instances that must always be running.

Example:

```
Minimum = 2
```

Even during low traffic, at least two instances remain active.

---

## Desired Capacity

The preferred number of running instances.

Example:

```
Desired = 4
```

The ASG attempts to maintain four running instances.

---

## Maximum Capacity

The maximum number of instances the ASG can launch.

Example:

```
Maximum = 10
```

The group will never scale beyond ten instances.

---

# Health Checks

The ASG continuously monitors the health of EC2 instances.

Healthy:

```
EC2 Instance

Healthy
```

Unhealthy:

```
EC2 Instance

Unhealthy

↓

Terminate

↓

Launch Replacement
```

Failed instances are automatically replaced to maintain the desired capacity.

---

# Integration with Load Balancer

```
Internet
      │
      ▼
Application Load Balancer
      │
      ▼
Auto Scaling Group
      │
 ┌────┴────┐
 ▼         ▼
EC2-1   EC2-2
```

As new instances are launched, they are automatically registered with the Load Balancer's Target Group.

---

# Automatic Scaling

Example:

```
CPU Usage

20%

↓

2 Instances

--------------------

CPU Usage

80%

↓

6 Instances

--------------------

CPU Usage

15%

↓

2 Instances
```

The Auto Scaling Group adjusts capacity automatically based on demand.

---

# High Availability

Deploy the Auto Scaling Group across multiple Availability Zones.

```
AWS Region

├── AZ-A
│     ├── EC2
│     └── EC2
│
└── AZ-B
      ├── EC2
      └── EC2
```

If one Availability Zone becomes unavailable, instances in the other zone continue serving traffic.

---

# Benefits

- Automatic scaling
- High availability
- Fault tolerance
- Reduced operational effort
- Lower infrastructure costs
- Automatic replacement of failed instances

---

# Common Use Cases

Auto Scaling Groups are commonly used for:

- Web applications
- APIs
- E-commerce platforms
- Microservices
- Gaming backends
- Enterprise applications

---

# Best Practices

- Use Launch Templates instead of Launch Configurations.
- Deploy across multiple Availability Zones.
- Configure appropriate minimum, desired, and maximum capacities.
- Combine Auto Scaling with an Application Load Balancer.
- Monitor scaling activities using Amazon CloudWatch.
- Test scaling behavior before production deployment.

---

# Common Mistakes

- Setting the maximum capacity too low.
- Using only one Availability Zone.
- Forgetting to configure health checks.
- Not attaching the Auto Scaling Group to a Target Group.
- Ignoring scaling limits during peak traffic.

---

# Real-World DevOps Example

An online shopping platform experiences high traffic during a sale.

```
Customers
     │
     ▼
Application Load Balancer
     │
     ▼
Auto Scaling Group
     │
 ┌───┼──────────────┐
 ▼   ▼              ▼
EC2 EC2          EC2
```

As customer traffic increases, additional EC2 instances are launched automatically. After the sale ends, unnecessary instances are terminated, reducing costs.

---

# Interview Questions

### What is an Auto Scaling Group?

An Auto Scaling Group is a logical collection of EC2 instances that automatically maintains, scales, and replaces instances based on configured policies.

---

### What is the difference between Minimum, Desired, and Maximum Capacity?

- **Minimum Capacity:** Lowest number of running instances.
- **Desired Capacity:** Target number of running instances.
- **Maximum Capacity:** Highest number of instances the group can launch.

---

### What happens if an EC2 instance fails?

The Auto Scaling Group automatically terminates the unhealthy instance and launches a replacement.

---

### Can an Auto Scaling Group work with a Load Balancer?

Yes. Auto Scaling Groups integrate with Application and Network Load Balancers using Target Groups.

---

### Why deploy an Auto Scaling Group across multiple Availability Zones?

To improve high availability and fault tolerance if one Availability Zone becomes unavailable.

---

# Key Takeaways

- Auto Scaling Groups automatically manage EC2 capacity.
- They maintain the desired number of running instances.
- Failed instances are automatically replaced.
- ASGs work seamlessly with Load Balancers and Target Groups.
- Deploy across multiple Availability Zones for high availability.
- Auto Scaling helps balance performance, reliability, and cost.