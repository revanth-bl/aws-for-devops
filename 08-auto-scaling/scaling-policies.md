# Amazon EC2 Auto Scaling Policies

## Introduction

A **Scaling Policy** defines the rules that an Auto Scaling Group (ASG) uses to automatically increase or decrease the number of EC2 instances.

Scaling policies help ensure that applications:

- Handle traffic spikes efficiently
- Maintain performance
- Optimize infrastructure costs
- Avoid unnecessary resource usage

Scaling decisions are typically based on Amazon CloudWatch metrics such as CPU utilization, network traffic, or request count.

---

# Why Use Scaling Policies?

Without a scaling policy:

```
Users

↓

High Traffic

↓

2 EC2 Instances

↓

Slow Application
```

The application cannot respond to increased demand.

With a scaling policy:

```
Users

↓

High Traffic

↓

Auto Scaling Group

↓

2 → 4 → 6 EC2 Instances
```

The application automatically scales to meet demand.

---

# How Scaling Policies Work

```
CloudWatch Metric

        │

        ▼

Scaling Policy

        │

        ▼

Auto Scaling Group

        │

        ▼

Launch or Terminate EC2 Instances
```

CloudWatch continuously monitors application metrics. When a configured threshold is reached, the scaling policy instructs the Auto Scaling Group to add or remove instances.

---

# Types of Scaling Policies

Amazon EC2 Auto Scaling supports several scaling policy types:

- Target Tracking Scaling
- Simple Scaling
- Step Scaling
- Scheduled Scaling

---

# 1. Target Tracking Scaling

Target Tracking maintains a specific metric value automatically.

Example:

```
Target CPU Utilization

50%
```

If CPU usage rises above the target:

```
CPU = 70%

↓

Launch Additional Instances
```

If CPU usage falls below the target:

```
CPU = 20%

↓

Terminate Extra Instances
```

This is the most commonly used and recommended scaling policy.

---

# 2. Simple Scaling

Simple Scaling performs one scaling action when a CloudWatch alarm is triggered.

Example:

```
CPU > 70%

↓

Add 2 Instances
```

After scaling, the ASG waits for a cooldown period before another scaling action.

---

# 3. Step Scaling

Step Scaling adjusts capacity based on how much the metric exceeds the threshold.

Example:

```
CPU 60–70%

↓

Add 1 Instance

--------------------

CPU 70–85%

↓

Add 2 Instances

--------------------

CPU > 85%

↓

Add 4 Instances
```

This provides more flexible scaling than Simple Scaling.

---

# 4. Scheduled Scaling

Scheduled Scaling launches or terminates instances at specific times.

Example:

```
Every Monday

08:00 AM

↓

Launch 6 Instances

--------------------

06:00 PM

↓

Reduce to 2 Instances
```

Useful for predictable traffic patterns.

---

# Scale Out vs Scale In

## Scale Out

Adds EC2 instances.

```
2 Instances

↓

4 Instances

↓

6 Instances
```

Used during high demand.

---

## Scale In

Removes EC2 instances.

```
6 Instances

↓

4 Instances

↓

2 Instances
```

Used during low demand to reduce costs.

---

# CloudWatch Metrics

Common metrics used for scaling include:

- CPU Utilization
- Network In
- Network Out
- Request Count (ALB)
- Memory Utilization (with CloudWatch Agent)
- Custom CloudWatch Metrics

---

# Cooldown Period

A cooldown period prevents continuous scaling actions.

Example:

```
Scale Out

↓

Wait 300 Seconds

↓

Evaluate Metrics Again
```

This allows new instances to become fully operational before making additional scaling decisions.

---

# Scaling Policy Example

```
CPU Utilization

25%

↓

2 EC2 Instances

--------------------

CPU Utilization

75%

↓

4 EC2 Instances

--------------------

CPU Utilization

90%

↓

6 EC2 Instances

--------------------

CPU Utilization

20%

↓

2 EC2 Instances
```

The ASG adjusts capacity based on the configured scaling policy.

---

# Best Practices

- Prefer Target Tracking Scaling for most workloads.
- Use Step Scaling for variable traffic patterns.
- Use Scheduled Scaling for predictable workloads.
- Monitor metrics with Amazon CloudWatch.
- Configure sensible minimum and maximum capacities.
- Test scaling behavior before production deployment.

---

# Common Mistakes

- Setting thresholds too low or too high.
- Ignoring cooldown periods.
- Using Scheduled Scaling for unpredictable workloads.
- Not monitoring scaling events.
- Configuring maximum capacity too low for peak traffic.

---

# Real-World DevOps Example

An online ticket booking application experiences high traffic during event launches.

```
Users

      │

      ▼

CloudWatch

CPU > 70%

      │

      ▼

Scaling Policy

      │

      ▼

Auto Scaling Group

      │

      ▼

Launch Additional EC2 Instances
```

Once traffic decreases, the ASG removes unnecessary instances to reduce infrastructure costs.

---

# Interview Questions

### What is a Scaling Policy?

A Scaling Policy defines when and how an Auto Scaling Group launches or terminates EC2 instances based on configured metrics or schedules.

---

### Which scaling policy is recommended for most workloads?

Target Tracking Scaling because it automatically maintains a target metric value.

---

### What is the difference between Scale Out and Scale In?

- **Scale Out:** Adds EC2 instances.
- **Scale In:** Removes EC2 instances.

---

### What is the purpose of a cooldown period?

It prevents repeated scaling actions while new instances initialize and application metrics stabilize.

---

### Which AWS service provides the metrics used by Scaling Policies?

Amazon CloudWatch.

---

# Key Takeaways

- Scaling Policies control how an Auto Scaling Group responds to changing demand.
- CloudWatch metrics trigger scaling actions.
- Target Tracking is the recommended policy for most applications.
- Step Scaling offers more granular control than Simple Scaling.
- Scheduled Scaling is ideal for predictable traffic patterns.
- Proper scaling policies improve application performance while minimizing infrastructure costs.