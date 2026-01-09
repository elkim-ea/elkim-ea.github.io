---
layout: post
title: " SAA Error Notebook - 1 "
date: 2026-01-10
categories:
  - "Error Notebook/SAA" 
tags: [SAA] 
---

# Q2.
A company wants to use NAt gateways in its AWS environment. The company's Amazon EC2 instances in private subnets must be able to connect to the public internet through the NAT gateway. Which solution will meet these requirements?

### My Choice :
Create public NAT gateways in the same private subnets as the EC2 instances
### Correct Answer : 
Create public NAT gateways in public subnets in the same VPCs as the EC2 instances

### Explanation:
NAT Gateways must be deployed in a **public subnet** to access the internet via an **internet gateway**.  
Private subnets **route outbound traffic** to the NAT Gateway. If placed in a private subnet, the NAT Gateway won't function correctly.

### Key Concepts & Analysis:
NAT Gateway is used to allow **instances in private subnets** to **initiate outbound** internet connections (e.g., for updates, API calls).                      
It **does not allow inbound connections**.
- A **NAT Gateway deployed in a Public Subnet**
- An **Elastic IP** attached to the NAT Gateway
- A **route in the private subnet’s route table**:
  - `0.0.0.0/0` -> NAT Gateway
- The public subnet containing the NAT must have a route to the **Internet Gateway**

### Exam Strategy & Cheat Sheet:

| Requirement                             | Placement / Configuration         |
|----------------------------------------|-----------------------------------|
| NAT Gateway                            | Public Subnet                     |
| EC2 instances needing outbound access  | Private Subnet                    |
| Private subnet route                   | `0.0.0.0/0` -> NAT Gateway         |
| NAT Gateway route                      | `0.0.0.0/0` -> Internet Gateway    |

# Q3.
