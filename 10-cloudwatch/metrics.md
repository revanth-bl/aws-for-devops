# Amazon CloudWatch Metrics

## Introduction

**Amazon CloudWatch Metrics** are numerical data points that represent the performance and health of AWS resources and applications over time.

CloudWatch automatically collects metrics from many AWS services, allowing you to monitor system performance, detect issues, and automate responses.

Metrics help answer questions such as:

- Is CPU usage too high?
- Is the application receiving more traffic?
- Is storage running out?
- Are instances healthy?

---

# Why Use CloudWatch Metrics?

Without monitoring:

```
Application

↓

Performance Problems

↓

Nobody Notices
```

With CloudWatch Metrics:

```
Application

↓

CloudWatch Metrics

↓

Performance Monitoring

↓

Take Action
```

Metrics provide visibility into the health and performance of your infrastructure.

---

# How CloudWatch Metrics Work

```
AWS Resource

↓

CloudWatch Metric

↓

CloudWatch

↓

Dashboard / Alarm / Auto Scaling
```

AWS resources publish metric data to CloudWatch, where it can be visualized, monitored, and used for automation.

---

# What is a Metric?

A **Metric** is a time-ordered collection of numerical values.

Example:

```
Time        CPU

10:00       25%

10:05       40%

10:10       65%

10:15       80%
```

Each metric contains data points recorded over time.

---

# Metric Components

A metric includes:

- Metric Name
- Namespace
- Dimensions
- Timestamp
- Value
- Unit

Example:

```
Metric Name

CPUUtilization

Namespace

AWS/EC2

Value

65%

Unit

Percent
```

---

# Namespaces

A **Namespace** groups related metrics.

Examples:

```
AWS/EC2

AWS/S3

AWS/RDS

AWS/Lambda

AWS/ApplicationELB
```

Namespaces help organize metrics by AWS service.

---

# Dimensions

**Dimensions** identify a specific resource for a metric.

Example:

```
Metric

CPUUtilization

↓

InstanceId = i-123456789
```

This allows CloudWatch to monitor individual resources separately.

---

# Common EC2 Metrics

CloudWatch automatically provides metrics such as:

- CPU Utilization
- Network In
- Network Out
- Disk Read Bytes
- Disk Write Bytes
- Status Check Failed

Example:

```
EC2 Instance

↓

CPU Utilization

↓

45%
```

---

# Common RDS Metrics

Amazon RDS publishes metrics including:

- CPU Utilization
- Free Storage Space
- Database Connections
- Read IOPS
- Write IOPS
- Freeable Memory

---

# Common Load Balancer Metrics

Application and Network Load Balancers publish metrics such as:

- Request Count
- Active Connections
- Target Response Time
- Healthy Host Count
- UnHealthy Host Count

---

# CloudWatch Dashboards

Metrics can be displayed using CloudWatch Dashboards.

Example:

```
CloudWatch Dashboard

------------------------

CPU Utilization

Memory Usage

Network Traffic

Disk Usage
```

Dashboards provide a centralized view of system performance.

---

# Custom Metrics

Applications can publish their own metrics to CloudWatch.

Examples:

- Active Users
- Orders Per Minute
- Failed Login Attempts
- API Response Time

Custom metrics allow monitoring of business-specific data.

---

# Integration with CloudWatch Alarms

```
CPU Utilization

↓

CloudWatch Metric

↓

CloudWatch Alarm

↓

Amazon SNS
```

Metrics are the foundation for CloudWatch Alarms.

---

# Integration with Auto Scaling

```
CPU > 70%

↓

CloudWatch Metric

↓

Scaling Policy

↓

Launch New EC2 Instance
```

CloudWatch Metrics can automatically trigger Auto Scaling actions.

---

# Real-World DevOps Example

An online shopping application:

```
Customers

↓

EC2 Instances

↓

CloudWatch Metrics

↓

CPU = 85%

↓

CloudWatch Alarm

↓

Auto Scaling

↓

Launch Additional EC2 Instances
```

As traffic increases, CloudWatch Metrics detect higher CPU utilization and trigger scaling actions.

---

# Benefits

- Real-time performance monitoring
- Automatic metric collection
- Easy visualization
- Integration with Alarms
- Supports Auto Scaling
- Enables proactive monitoring
- Supports custom business metrics

---

# Best Practices

- Monitor business-critical metrics.
- Create CloudWatch Dashboards.
- Use CloudWatch Alarms for important metrics.
- Publish Custom Metrics when necessary.
- Monitor trends instead of single data points.
- Review metrics regularly to optimize performance.

---

# Common Mistakes

- Monitoring too few metrics.
- Ignoring long-term performance trends.
- Creating alarms without understanding normal behavior.
- Forgetting to monitor custom applications.
- Confusing metrics with logs.

---

# Interview Questions

### What is an Amazon CloudWatch Metric?

A CloudWatch Metric is a numerical measurement collected over time that represents the performance or health of an AWS resource or application.

---

### What is a Namespace?

A Namespace is a container that groups related CloudWatch Metrics for an AWS service or application.

---

### What is a Dimension?

A Dimension identifies a specific resource associated with a metric, such as an EC2 Instance ID.

---

### Can CloudWatch collect custom metrics?

Yes. Applications can publish custom metrics to CloudWatch using the AWS SDK or API.

---

### How do CloudWatch Metrics work with Auto Scaling?

CloudWatch Metrics provide the data used by scaling policies to automatically launch or terminate EC2 instances.

---

# Key Takeaways

- CloudWatch Metrics measure AWS resource performance over time.
- Metrics include Namespaces, Dimensions, timestamps, and values.
- AWS automatically publishes metrics for many services.
- Applications can publish Custom Metrics.
- Metrics integrate with Dashboards, Alarms, and Auto Scaling.
- Effective monitoring helps improve reliability, performance, and operational efficiency.