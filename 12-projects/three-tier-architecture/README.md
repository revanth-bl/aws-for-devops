# Three-Tier Web Application Architecture

## Project Overview

This project demonstrates a production-style three-tier architecture on AWS.

The application is divided into:

- Presentation Tier
- Application Tier
- Database Tier

---

# Architecture

```
Internet

      │

      ▼

Route 53

      │

      ▼

Application Load Balancer

      │

      ▼

Auto Scaling Group

      │

      ▼

EC2 Instances

      │

      ▼

Amazon RDS
```

---

# AWS Services Used

- VPC
- EC2
- RDS
- Auto Scaling
- Application Load Balancer
- Route 53
- IAM
- CloudWatch

---

# Objectives

- Build a secure VPC
- Create Public and Private Subnets
- Deploy EC2 Instances
- Deploy Amazon RDS
- Configure Security Groups
- Configure Load Balancer
- Configure Auto Scaling

---

# Network Design

Public Subnets

- Load Balancer

Private Subnets

- EC2
- RDS

---

# Implementation Steps

1. Create VPC
2. Create Public Subnets
3. Create Private Subnets
4. Configure Internet Gateway
5. Configure NAT Gateway
6. Configure Route Tables
7. Launch EC2 Instances
8. Create RDS
9. Configure ALB
10. Configure Auto Scaling
11. Configure Route 53
12. Configure CloudWatch

---

# Expected Result

Highly available three-tier application.

---

# Skills Demonstrated

- Networking
- Compute
- Database
- Monitoring
- High Availability
- Security

---

# Future Improvements

- WAF
- CloudFront
- CI/CD
- Infrastructure as Code