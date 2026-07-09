# AWS Basics - Quick Notes

## AWS Overview

- AWS stands for **Amazon Web Services**.
- Launched in **2006** by Amazon.
- World's leading cloud computing platform.
- Provides 200+ cloud services.
- Uses a **Pay-As-You-Go** pricing model.

---

# Cloud Computing

Cloud computing is the delivery of computing resources over the internet instead of using physical hardware.

Examples of cloud services:

- Compute
- Storage
- Networking
- Databases
- Security
- Monitoring
- AI & Machine Learning

---

# Cloud Service Models

| Model | Responsibility |
|--------|----------------|
| IaaS | Infrastructure |
| PaaS | Platform |
| SaaS | Software |

AWS mainly provides **Infrastructure as a Service (IaaS)** but also offers many Platform as a Service (PaaS) solutions.

---

# AWS Global Infrastructure

AWS Global Infrastructure consists of:

- Regions
- Availability Zones (AZs)
- Edge Locations
- Regional Edge Caches
- Local Zones
- Wavelength Zones

---

# Region

- Geographic location.
- Contains multiple Availability Zones.
- Completely isolated from other Regions.
- Example: Mumbai (`ap-south-1`).

---

# Availability Zone (AZ)

- One or more physically separate data centers.
- Independent power, cooling, and networking.
- Connected with high-speed private links.
- Designed for high availability and fault tolerance.

---

# Edge Location

Used by:

- CloudFront
- Route 53
- AWS Shield
- AWS WAF

Purpose:

- Reduce latency
- Deliver cached content closer to users

---

# Advantages of AWS

- Pay only for what you use.
- Highly scalable.
- Global infrastructure.
- Secure by design.
- Highly available.
- Reliable.
- Elastic resources.
- Fast deployment.

---

# Popular AWS Services

| Service | Purpose |
|----------|---------|
| EC2 | Virtual servers |
| S3 | Object storage |
| IAM | Identity and Access Management |
| VPC | Virtual network |
| RDS | Managed relational database |
| Route 53 | DNS service |
| CloudWatch | Monitoring and logging |
| CloudFormation | Infrastructure as Code |
| Lambda | Serverless computing |

---

# Shared Responsibility Model

AWS is responsible for:

- Physical security
- Hardware
- Networking infrastructure
- Data centers

Customers are responsible for:

- IAM users and permissions
- Applications
- Operating system (for EC2)
- Data
- Security Groups
- Encryption configuration

---

# Common Interview Questions

**Q:** What is AWS?

**A:** AWS is Amazon's cloud computing platform that provides on-demand IT services over the internet.

---

**Q:** What is a Region?

**A:** A geographic area that contains multiple Availability Zones.

---

**Q:** What is an Availability Zone?

**A:** One or more isolated data centers within a Region.

---

**Q:** Why use multiple Availability Zones?

**A:** To improve high availability and fault tolerance.

---

**Q:** What is an Edge Location?

**A:** A location that caches and delivers content closer to users, reducing latency.

---

# Key Terms

- Cloud Computing
- Region
- Availability Zone (AZ)
- Edge Location
- Scalability
- Elasticity
- High Availability
- Fault Tolerance
- Pay-As-You-Go
- Shared Responsibility Model

---

# Remember

> **Region = Geographic Area**

> **Availability Zone = Data Center(s)**

> **Edge Location = Content Delivery**

> **Multi-AZ = High Availability**

> **Multi-Region = Disaster Recovery**

> **AWS = Cloud Infrastructure**