# Amazon CloudWatch Alarms

## Introduction

An **Amazon CloudWatch Alarm** continuously monitors a CloudWatch metric and performs an action when the metric reaches a specified threshold.

CloudWatch Alarms help automate monitoring by:

- Detecting problems
- Sending notifications
- Triggering Auto Scaling
- Improving application reliability

Instead of manually checking metrics, CloudWatch Alarms automatically notify administrators or perform predefined actions.

---

# Why Use CloudWatch Alarms?

Without an Alarm:

```
High CPU Usage

↓

Nobody Notices

↓

Application Performance Degrades
```

With an Alarm:

```
High CPU Usage

↓

CloudWatch Alarm

↓

Send Notification

↓

Take Action
```

This helps identify and respond to issues quickly.

---

# How CloudWatch Alarms Work

```
Application

↓

CloudWatch Metric

↓

CloudWatch Alarm

↓

Action
```

The alarm continuously evaluates the selected metric.

If the configured condition is met, the alarm changes state and performs the configured action.

---

# Alarm States

A CloudWatch Alarm has three possible states.

## OK

```
Metric

↓

Normal

↓

OK
```

The monitored metric is operating within the defined threshold.

---

## ALARM

```
Metric

↓

Threshold Exceeded

↓

ALARM
```

The threshold has been breached and the configured action is executed.

---

## INSUFFICIENT_DATA

```
No Metric Data

↓

INSUFFICIENT_DATA
```

CloudWatch does not have enough data to determine the alarm state.

---

# Alarm Components

A CloudWatch Alarm consists of:

- Metric
- Threshold
- Evaluation Period
- Comparison Operator
- Alarm Action

Example:

```
CPU Utilization

Threshold: 80%

Evaluation: 5 Minutes

Action: Send Notification
```

---

# Example Alarm

```
CPU Utilization

75%

↓

No Action

--------------------

CPU Utilization

85%

↓

CloudWatch Alarm

↓

Amazon SNS Notification
```

---

# Alarm Actions

CloudWatch Alarms can perform several actions.

Examples include:

- Send an Amazon SNS notification
- Launch EC2 instances through Auto Scaling
- Terminate EC2 instances through Auto Scaling
- Recover an EC2 instance (supported instance types)
- Stop an EC2 instance
- Reboot an EC2 instance

---

# Integration with Amazon SNS

A common use case is sending notifications through Amazon SNS.

```
CloudWatch Alarm

↓

Amazon SNS

↓

Email

SMS

Lambda
```

This allows administrators to receive alerts immediately.

---

# Integration with Auto Scaling

```
CPU > 70%

↓

CloudWatch Alarm

↓

Scaling Policy

↓

Launch New EC2 Instance
```

CloudWatch Alarms work closely with Auto Scaling Groups to automatically adjust capacity.

---

# Common Metrics

CloudWatch Alarms can monitor metrics such as:

- CPU Utilization
- Memory Utilization (using CloudWatch Agent)
- Network In
- Network Out
- Disk Read Operations
- Disk Write Operations
- Request Count
- Status Check Failed

---

# Real-World DevOps Example

A production web application:

```
Users

↓

Application

↓

CPU = 85%

↓

CloudWatch Alarm

↓

Amazon SNS

↓

DevOps Engineer

↓

Investigate Issue
```

If traffic continues increasing, another alarm can trigger an Auto Scaling policy to launch additional EC2 instances.

---

# Best Practices

- Set realistic alarm thresholds.
- Enable notifications using Amazon SNS.
- Avoid unnecessary alarms that generate alert fatigue.
- Monitor business-critical metrics.
- Test alarms regularly.
- Integrate alarms with Auto Scaling when appropriate.

---

# Common Mistakes

- Setting thresholds too low.
- Ignoring INSUFFICIENT_DATA state.
- Creating too many alarms.
- Forgetting to configure notifications.
- Never testing alarm actions.

---

# Interview Questions

### What is a CloudWatch Alarm?

A CloudWatch Alarm monitors a metric and performs an action when the configured threshold is reached.

---

### What are the three alarm states?

- OK
- ALARM
- INSUFFICIENT_DATA

---

### Which AWS service is commonly used to send CloudWatch Alarm notifications?

Amazon SNS.

---

### Can CloudWatch Alarms trigger Auto Scaling?

Yes. They can trigger Auto Scaling policies to launch or terminate EC2 instances.

---

### Can CloudWatch Alarms monitor CPU utilization?

Yes. CPU utilization is one of the most commonly monitored CloudWatch metrics.

---

# Key Takeaways

- CloudWatch Alarms monitor AWS resource metrics.
- They automatically respond when thresholds are exceeded.
- Alarm states are OK, ALARM, and INSUFFICIENT_DATA.
- CloudWatch Alarms integrate with Amazon SNS and Auto Scaling.
- Proper alarm configuration improves reliability and reduces downtime.
- Monitoring and alerting are essential parts of production AWS environments.