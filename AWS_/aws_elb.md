# AWS Elastic Load Balancer (ELB)

## Introduction

**AWS Elastic Load Balancer (ELB)** distributes incoming traffic across multiple EC2 instances.

It improves:

* Availability
* Fault tolerance
* Performance

---

## Types of Load Balancers

### 1. Application Load Balancer (ALB)

* Layer 7 (HTTP/HTTPS)
* Best for web applications

### 2. Network Load Balancer (NLB)

* Layer 4 (TCP/UDP)
* High performance

### 3. Gateway Load Balancer

* Used for security appliances

---

## How It Works

* User sends request
* Load balancer receives it
* Distributes to healthy instances

---

## Key Features

### Health Checks

* Detects unhealthy instances

### SSL Termination

* Handles HTTPS traffic

### Sticky Sessions

* Sends user to same instance

---

## ELB + Auto Scaling

* ELB distributes traffic
* Auto Scaling adds/removes instances

👉 Together they create a **highly available system**

---

## Use Cases

* Web applications
* Microservices architecture
* High-traffic systems

---

## Advantages

* Improved reliability
* Better performance
* Automatic failover

---

## Conclusion

Elastic Load Balancer ensures efficient traffic distribution and high availability of applications running on AWS.
