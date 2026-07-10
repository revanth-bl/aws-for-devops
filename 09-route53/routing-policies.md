# Amazon Route 53 Routing Policies

## Introduction

A **Routing Policy** defines how Amazon Route 53 responds to DNS queries and determines which resource receives user traffic.

Different routing policies are designed for different use cases, such as:

- Simple routing
- Load balancing
- High availability
- Disaster recovery
- Low latency
- Geographic traffic distribution

Choosing the correct routing policy helps improve application performance, reliability, and user experience.

---

# Why Use Routing Policies?

Without a routing policy:

```
Users

↓

Route 53

↓

Single Server
```

All traffic is sent to one destination.

With routing policies:

```
Users

↓

Route 53

↓

Different AWS Resources
```

Traffic can be distributed intelligently based on your requirements.

---

# Types of Routing Policies

Amazon Route 53 supports the following routing policies:

- Simple Routing
- Weighted Routing
- Latency Routing
- Failover Routing
- Geolocation Routing
- Geoproximity Routing
- Multivalue Answer Routing

---

# 1. Simple Routing

Simple Routing directs traffic to a single resource.

Example:

```
Users

↓

Route 53

↓

Application Load Balancer
```

Use cases:

- Single web server
- Single Load Balancer
- Small applications

---

# 2. Weighted Routing

Weighted Routing distributes traffic based on assigned percentages.

Example:

```
Users

↓

Route 53

↓

80% → Server A

20% → Server B
```

Common use cases:

- A/B testing
- Gradual deployments
- Blue/Green deployments

---

# 3. Latency Routing

Latency Routing sends users to the AWS Region with the lowest network latency.

Example:

```
User (India)

↓

Mumbai Region

----------------

User (Germany)

↓

Frankfurt Region
```

Benefits:

- Faster response times
- Better user experience

---

# 4. Failover Routing

Failover Routing supports disaster recovery.

Example:

```
Primary Server

↓

Health Check

↓

Healthy

↓

Serve Traffic

----------------

Primary Fails

↓

Secondary Server
```

If the primary endpoint becomes unhealthy, Route 53 automatically routes traffic to the secondary endpoint.

---

# 5. Geolocation Routing

Geolocation Routing sends traffic based on the user's geographic location.

Example:

```
Users in India

↓

India Website

----------------

Users in USA

↓

USA Website
```

Typical use cases:

- Country-specific websites
- Localized content
- Regional legal requirements

---

# 6. Geoproximity Routing

Geoproximity Routing routes traffic based on the geographic location of AWS resources and users.

It can also shift traffic using **bias** values.

Example:

```
User

↓

Nearest AWS Region

↓

Application
```

This policy requires **Route 53 Traffic Flow**.

---

# 7. Multivalue Answer Routing

Multivalue Answer Routing returns multiple healthy IP addresses in response to a DNS query.

Example:

```
Users

↓

Route 53

↓

EC2-1

EC2-2

EC2-3
```

If one endpoint becomes unhealthy, it is removed from the response.

---

# Health Checks

Several routing policies work with Route 53 Health Checks.

```
Application

↓

Health Check

↓

Healthy

↓

Return DNS Record
```

If the endpoint is unhealthy, Route 53 can route traffic to another healthy resource.

Health Checks are commonly used with:

- Failover Routing
- Multivalue Answer Routing
- Weighted Routing (optional)

---

# Routing Policy Comparison

| Routing Policy | Primary Purpose |
|----------------|-----------------|
| Simple | Single resource |
| Weighted | Traffic distribution by percentage |
| Latency | Lowest network latency |
| Failover | Disaster recovery |
| Geolocation | Route by user location |
| Geoproximity | Route based on user and resource proximity |
| Multivalue Answer | Return multiple healthy endpoints |

---

# Real-World DevOps Example

A global e-commerce platform:

```
                    Users
                       │
                       ▼
                  Amazon Route 53
                       │
      ┌────────────────┼────────────────┐
      ▼                ▼                ▼
 Mumbai Region   Frankfurt Region   Virginia Region
```

Users are automatically directed to the most appropriate region, reducing latency and improving availability.

---

# Best Practices

- Use Latency Routing for global applications.
- Use Failover Routing for disaster recovery.
- Use Weighted Routing for canary or blue/green deployments.
- Enable Health Checks for production environments.
- Choose the routing policy that matches your application's requirements.
- Monitor DNS performance using Amazon CloudWatch.

---

# Common Mistakes

- Using Simple Routing for highly available applications.
- Forgetting to configure Health Checks with Failover Routing.
- Confusing Geolocation Routing with Latency Routing.
- Misconfiguring traffic weights.
- Ignoring DNS failover testing.

---

# Interview Questions

### What is a Routing Policy in Route 53?

A Routing Policy determines how Route 53 responds to DNS queries and routes user traffic to resources.

---

### Which routing policy is best for disaster recovery?

Failover Routing.

---

### Which routing policy sends users to the nearest AWS Region?

Latency Routing sends users to the region with the lowest network latency.

---

### Which routing policy is commonly used for A/B testing?

Weighted Routing.

---

### What is the difference between Geolocation and Latency Routing?

**Geolocation Routing** uses the user's geographic location (such as country or continent).

**Latency Routing** uses network latency and sends users to the AWS Region with the fastest response time.

---

# Key Takeaways

- Routing Policies determine how Route 53 directs user traffic.
- Simple Routing sends traffic to a single resource.
- Weighted Routing distributes traffic by percentage.
- Latency Routing improves user experience by reducing response times.
- Failover Routing supports disaster recovery with Health Checks.
- Geolocation and Geoproximity Routing provide location-based traffic management.
- Multivalue Answer Routing returns multiple healthy endpoints for improved availability.