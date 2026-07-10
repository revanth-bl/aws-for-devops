# Route Tables

## Introduction

A **Route Table** is a set of rules (called **routes**) that determines where network traffic from a subnet or gateway is directed.

Every subnet in a VPC must be associated with a route table. Without a route table, AWS resources would not know how to communicate with other networks or the internet.

---

# Why Do We Need Route Tables?

When an EC2 instance sends network traffic, AWS checks the associated route table to determine where the traffic should go.

Example:

```
EC2 Instance
      │
      ▼
 Route Table
      │
      ├── Local Traffic
      ├── Internet Gateway
      └── NAT Gateway
```

The route table acts like a GPS, selecting the correct path for each packet.

---

# How Route Tables Work

```
           EC2 Instance
                 │
                 ▼
          Route Table
                 │
      ┌──────────┼──────────┐
      ▼          ▼          ▼
   Local      Internet    NAT Gateway
  Resources    Gateway
```

AWS compares the destination IP address with the routes in the table and forwards the traffic to the matching target.

---

# Route Table Components

Each route contains:

- **Destination** – The IP range the rule applies to.
- **Target** – Where matching traffic should be sent.

Example:

| Destination | Target |
|-------------|--------|
| 10.0.0.0/16 | Local |
| 0.0.0.0/0 | Internet Gateway |

---

# Local Route

Every VPC automatically includes a **Local Route**.

Example:

```
Destination      Target

10.0.0.0/16      Local
```

This allows communication between resources inside the same VPC.

Without the local route, EC2 instances in different subnets could not communicate.

---

# Default Route

The route:

```
0.0.0.0/0
```

represents **all IPv4 destinations not covered by more specific routes**.

Example:

```
Destination      Target

0.0.0.0/0        Internet Gateway
```

For IPv6, the equivalent default route is:

```
::/0
```

---

# Public Route Table

A public route table includes a route to an Internet Gateway.

Example:

```
Destination      Target

10.0.0.0/16      Local
0.0.0.0/0        Internet Gateway
```

Architecture:

```
Internet
     │
     ▼
Internet Gateway
     │
     ▼
Public Route Table
     │
     ▼
Public Subnet
```

Resources in the public subnet can communicate with the internet if they also have public IP addresses.

---

# Private Route Table

A private route table directs internet-bound traffic to a NAT Gateway instead of an Internet Gateway.

Example:

```
Destination      Target

10.0.0.0/16      Local
0.0.0.0/0        NAT Gateway
```

Architecture:

```
Private EC2
     │
     ▼
Private Route Table
     │
     ▼
NAT Gateway
     │
     ▼
Internet Gateway
     │
     ▼
Internet
```

This allows outbound internet access while preventing direct inbound access.

---

# Route Table Association

Each subnet is associated with one route table.

Example:

```
VPC

├── Public Subnet
│      │
│      ▼
│ Public Route Table
│
└── Private Subnet
       │
       ▼
 Private Route Table
```

Multiple subnets can share the same route table if they require identical routing rules.

---

# Main Route Table

Every VPC has a **Main Route Table**.

Characteristics:

- Automatically created with the VPC.
- Used by subnets that are not explicitly associated with another route table.
- Can be modified or replaced.

---

# Route Table Example

```
Destination         Target

10.0.0.0/16         Local
0.0.0.0/0           Internet Gateway
172.31.0.0/16       VPC Peering
```

AWS evaluates the routes and forwards traffic to the appropriate destination.

---

# Route Tables and Gateways

```
Public Subnet

EC2
 │
 ▼
Route Table
 │
 ▼
Internet Gateway
 │
 ▼
Internet
```

```
Private Subnet

EC2
 │
 ▼
Route Table
 │
 ▼
NAT Gateway
 │
 ▼
Internet Gateway
 │
 ▼
Internet
```

---

# Best Practices

- Use separate route tables for public and private subnets.
- Keep routing simple and well documented.
- Associate subnets with the correct route table.
- Review routes regularly.
- Use descriptive names and tags.
- Avoid unnecessary custom routes.

---

# Common Mistakes

- Forgetting to associate a subnet with the correct route table.
- Missing the `0.0.0.0/0` route for internet access.
- Sending private subnet traffic directly to an Internet Gateway.
- Deleting or modifying the local route.
- Assuming a public subnet automatically has internet access without the correct route.

---

# Real-World DevOps Example

A production application:

```
                     Internet
                         │
                         ▼
                 Internet Gateway
                         │
                Public Route Table
                         │
                         ▼
                 Application Load Balancer
                         │
         ┌───────────────┴───────────────┐
         ▼                               ▼
      Web Server                    NAT Gateway
                                         │
                                         ▼
                               Private Route Table
                                         │
                                         ▼
                               Application Server
                                         │
                                         ▼
                                   Amazon RDS
```

The public resources use the Internet Gateway, while private resources use the NAT Gateway for outbound internet access.

---

# Interview Questions

### What is a Route Table?

A Route Table is a collection of routes that determines where network traffic from a subnet or gateway is directed.

---

### What is the purpose of the Local Route?

The local route allows communication between resources within the same VPC.

---

### What does `0.0.0.0/0` represent?

It is the default IPv4 route and matches all destinations not covered by more specific routes.

---

### Can multiple subnets use the same Route Table?

Yes. Multiple subnets can share a route table if they require the same routing behavior.

---

### What is the difference between a Public Route Table and a Private Route Table?

A public route table routes internet-bound traffic to an Internet Gateway, while a private route table routes internet-bound traffic to a NAT Gateway.

---

# Key Takeaways

- Route Tables determine how network traffic is routed within a VPC.
- Every subnet must be associated with a route table.
- The Local Route enables communication inside the VPC.
- Public Route Tables use an Internet Gateway.
- Private Route Tables use a NAT Gateway for outbound internet access.
- Proper routing is essential for secure and functional AWS network architectures.