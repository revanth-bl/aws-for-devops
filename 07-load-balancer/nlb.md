# Network Load Balancer (NLB)

## Introduction

A **Network Load Balancer (NLB)** is a Layer 4 load balancer provided by AWS Elastic Load Balancing (ELB).

It distributes incoming network traffic based on **TCP**, **UDP**, and **TLS** protocols.

Unlike an Application Load Balancer (ALB), which makes routing decisions using HTTP requests, URLs, or host names, an NLB routes traffic using IP addresses and ports.

It is designed for:

- Ultra-low latency
- High throughput
- Millions of requests per second
- High availability
- Fault tolerance

---

# Why Use a Network Load Balancer?

Applications such as gaming servers, financial systems, and real-time communication platforms require extremely fast network performance.

Example:

```
Clients

      │

      ▼

Network Load Balancer

      │

      ├──────────────┐

      ▼              ▼

Server 1       Server 2
```

Traffic is distributed efficiently with minimal latency.

---

# How NLB Works

```
Internet
      │
      ▼
Network Load Balancer
      │
      ├───────────────┐
      ▼               ▼
EC2 Instance 1   EC2 Instance 2
```

The NLB forwards traffic directly to healthy targets based on network-level information.

---

# Layer 4 Load Balancer

The Network Load Balancer operates at **Layer 4 (Transport Layer)** of the OSI model.

It understands:

- TCP
- UDP
- TLS

Unlike an ALB, it does **not** inspect:

- URLs
- HTTP headers
- Cookies
- Host names

---

# Supported Protocols

The NLB supports:

- TCP
- UDP
- TLS

This makes it suitable for applications that do not use HTTP or HTTPS.

---

# Key Features

Amazon NLB provides:

- Layer 4 load balancing
- Ultra-low latency
- High throughput
- Static IP addresses
- Elastic IP support
- Health checks
- TLS termination
- Integration with Auto Scaling
- High availability across multiple Availability Zones

---

# Static IP Addresses

Unlike an ALB, a Network Load Balancer can provide static IP addresses.

Example:

```
Client

↓

Static Public IP

↓

Network Load Balancer
```

This is useful when clients or firewalls require fixed IP addresses.

---

# Health Checks

The NLB continuously checks the health of registered targets.

Healthy target:

```
EC2 Instance

Status

Healthy
```

Unhealthy target:

```
EC2 Instance

Status

Unhealthy
```

Traffic is automatically routed only to healthy targets.

---

# Target Groups

Like an ALB, an NLB uses Target Groups.

```
Network Load Balancer

        │

        ▼

Target Group

        │

        ├─────────────┐

        ▼             ▼

EC2-1          EC2-2
```

Each Target Group contains one or more backend resources.

---

# Integration with Auto Scaling

```
Users

      │

      ▼

Network Load Balancer

      │

      ▼

Auto Scaling Group

      │

      ├──────────────┐

      ▼              ▼

EC2-1         EC2-2
```

As Auto Scaling launches new instances, they can automatically register with the Target Group.

---

# ALB vs NLB

| Application Load Balancer (ALB) | Network Load Balancer (NLB) |
|---------------------------------|------------------------------|
| Layer 7 | Layer 4 |
| HTTP / HTTPS | TCP / UDP / TLS |
| Path-based routing | No path-based routing |
| Host-based routing | No host-based routing |
| Understands HTTP requests | Routes using IP addresses and ports |
| Best for web applications | Best for high-performance network applications |

---

# Common Use Cases

Network Load Balancers are commonly used for:

- Gaming servers
- VoIP applications
- Financial trading systems
- IoT platforms
- Real-time messaging
- DNS services
- Database connections

---

# Best Practices

- Deploy the NLB across multiple Availability Zones.
- Configure health checks correctly.
- Use Auto Scaling with backend instances.
- Use TLS listeners when encryption is required.
- Monitor traffic and latency using Amazon CloudWatch.
- Select NLB only when Layer 4 load balancing is required.

---

# Common Mistakes

- Choosing an NLB for applications that require path-based routing.
- Forgetting to configure health checks.
- Assuming an NLB understands HTTP requests.
- Using an ALB when static IP addresses are required.
- Ignoring network latency and throughput metrics.

---

# Real-World DevOps Example

A multiplayer gaming platform:

```
                Players
                    │
                    ▼
        Network Load Balancer
                    │
        ┌───────────┴───────────┐
        ▼                       ▼
   Game Server 1          Game Server 2
```

The NLB distributes player connections with minimal latency while maintaining high performance.

---

# Interview Questions

### What is a Network Load Balancer?

A Network Load Balancer is a Layer 4 load balancer that distributes TCP, UDP, and TLS traffic across multiple targets.

---

### Which OSI layer does an NLB operate on?

Layer 4 (Transport Layer).

---

### Does an NLB support path-based routing?

No. Path-based routing is supported by the Application Load Balancer (ALB), not the Network Load Balancer.

---

### What protocols does an NLB support?

TCP, UDP, and TLS.

---

### Why would you choose an NLB instead of an ALB?

Choose an NLB when you need ultra-low latency, high throughput, static IP addresses, or support for non-HTTP protocols such as TCP and UDP.

---

# Key Takeaways

- NLB operates at Layer 4 of the OSI model.
- Supports TCP, UDP, and TLS traffic.
- Provides ultra-low latency and high throughput.
- Supports static IP addresses and Elastic IPs.
- Uses Target Groups and Health Checks.
- Ideal for high-performance network applications and non-HTTP workloads.