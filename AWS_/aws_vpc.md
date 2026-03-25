# AWS VPC (Virtual Private Cloud)

## Introduction

**AWS VPC (Virtual Private Cloud)** allows you to create a logically isolated network within AWS where you can launch and manage resources like EC2 instances.

It gives you full control over:

* IP address range
* Subnets
* Routing
* Security

---

## Why VPC is Important

Without VPC:

* No control over networking
* Resources exposed to public internet
* Poor security

With VPC:

* Secure and isolated environment
* Custom networking configuration
* Controlled access

---

## Key Components of VPC

### 1. VPC

A VPC is your private network in AWS.

Example:

* CIDR Block: 10.0.0.0/16

---

### 2. Subnets

Subnets divide a VPC into smaller networks.

Types:

#### Public Subnet

* Has access to internet
* Used for web servers

#### Private Subnet

* No direct internet access
* Used for databases and backend services

---

### 3. Internet Gateway (IGW)

Allows communication between VPC and the internet.

* Required for public subnets
* Enables inbound and outbound traffic

---

### 4. Route Table

Defines how traffic is routed inside the VPC.

Example:

| Destination | Target           |
| ----------- | ---------------- |
| 0.0.0.0/0   | Internet Gateway |

---

### 5. NAT Gateway

Allows private subnet resources to access the internet **without exposing them**.

Use case:

* Download updates
* Access external APIs

---

### 6. Security Groups

Acts as a **firewall at instance level**.

* Stateful
* Controls inbound and outbound traffic

---

### 7. Network ACL (NACL)

Acts as a **firewall at subnet level**.

* Stateless
* Controls traffic entering and leaving subnets

---

## Public vs Private Architecture

### Public Subnet:

* Connected to Internet Gateway
* Used for frontend servers

### Private Subnet:

* Uses NAT Gateway for internet access
* Used for backend systems

---

## Basic VPC Architecture

* VPC (10.0.0.0/16)

  * Public Subnet (10.0.1.0/24)

    * Web Server (EC2)
  * Private Subnet (10.0.2.0/24)

    * Database Server

---

## Steps to Create a VPC

1. Create VPC with CIDR block
2. Create subnets (public and private)
3. Attach Internet Gateway
4. Create route tables
5. Configure NAT Gateway
6. Launch EC2 instances

---

## VPC in DevOps

VPC is essential for:

* Designing secure cloud architecture
* Deploying microservices
* Hosting applications with proper isolation
* Setting up production environments

---

## Advantages of VPC

* Network isolation
* High security
* Flexible configuration
* Scalable architecture

---

## Conclusion

AWS VPC allows you to build secure and scalable networking environments in the cloud. It is a fundamental service for deploying real-world applications on AWS.
