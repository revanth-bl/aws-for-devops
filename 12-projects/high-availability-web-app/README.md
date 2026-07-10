# High Availability Web Application on AWS

## Project Overview

This project demonstrates how to build a highly available and fault-tolerant web application using AWS best practices.

The application remains available even if an Availability Zone or EC2 instance fails.

---

# Architecture

```
Users

     │

     ▼

Route 53

     │

     ▼

Application Load Balancer

     │

     ▼

Auto Scaling Group

 ┌───────────────┐
 ▼               ▼

AZ-A           AZ-B

EC2            EC2

     │

     ▼

Amazon RDS (Multi-AZ)
```

---

# AWS Services Used

- Route 53
- VPC
- EC2
- ALB
- Auto Scaling
- Amazon RDS
- CloudWatch
- IAM

---

# High Availability Features

- Multi-AZ
- Auto Scaling
- Load Balancer
- Health Checks
- Route 53
- CloudWatch Monitoring

---

# Implementation Steps

1. Create VPC
2. Configure Public Subnets
3. Configure Private Subnets
4. Launch EC2 Instances
5. Configure Auto Scaling
6. Configure ALB
7. Configure RDS Multi-AZ
8. Configure Route 53
9. Configure CloudWatch
10. Perform Failover Testing

---

# Failure Scenario

```
AZ-A Failure

↓

Traffic

↓

ALB

↓

AZ-B

↓

Healthy EC2
```

---

# Expected Result

Application remains online during instance or Availability Zone failures.

---

# Skills Demonstrated

- High Availability
- Disaster Recovery
- Fault Tolerance
- Monitoring
- Networking
- Scaling

---

# Future Improvements

- AWS WAF
- CloudFront
- CloudFormation
- CI/CD
- Blue/Green Deployment