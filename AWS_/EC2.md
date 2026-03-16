# Amazon EC2 (Elastic Compute Cloud)

## Introduction

**Amazon EC2 (Elastic Compute Cloud)** is a core compute service provided by **Amazon Web Services (AWS)** that allows users to run virtual servers in the cloud.

EC2 enables developers and organizations to launch and manage virtual machines without purchasing physical hardware. These virtual machines are known as **EC2 instances**.

With EC2, users can choose the operating system, CPU, memory, storage, and networking configuration according to their application requirements.

---

## Why EC2 is Important

Before cloud services like EC2, companies had to purchase and maintain physical servers. This required:

* High upfront hardware costs
* Data center maintenance
* Manual server scaling
* Hardware replacement and upgrades

EC2 eliminates these problems by providing **on-demand virtual servers** that can be launched, resized, and terminated easily.

---

## Key Features of EC2

### 1. Scalability

EC2 allows users to scale computing resources according to application demand. Instances can be added or removed automatically using **Auto Scaling**.

### 2. Flexible Instance Types

AWS provides multiple EC2 instance types optimized for different workloads such as:

* General purpose
* Compute optimized
* Memory optimized
* Storage optimized

### 3. Pay-as-you-go Pricing

Users only pay for the compute time they consume. There is no need to purchase hardware in advance.

### 4. Security

EC2 provides security through features such as:

* Security Groups
* Key Pairs (SSH authentication)
* Integration with IAM

### 5. High Availability

EC2 instances can be deployed across multiple **Availability Zones** to improve fault tolerance.

---

## EC2 Components

### AMI (Amazon Machine Image)

An **AMI** is a pre-configured template used to launch EC2 instances. It contains:

* Operating system
* Application server
* Required software

Example AMIs:

* Amazon Linux
* Ubuntu
* Red Hat Enterprise Linux
* Windows Server

---

### Instance

An **instance** is a virtual server created from an AMI. It runs applications and workloads.

Each instance has:

* CPU
* Memory
* Network configuration
* Storage

---

### Instance Types

Instance types determine the hardware resources allocated to the instance.

Examples:

| Instance Type | Use Case                       |
| ------------- | ------------------------------ |
| t2 / t3       | General purpose workloads      |
| c5            | Compute-intensive applications |
| r5            | Memory-intensive workloads     |
| i3            | Storage-intensive workloads    |

---

### Key Pair

A **key pair** is used to securely connect to an EC2 instance using SSH.

It consists of:

* Public Key (stored in AWS)
* Private Key (.pem file used by the user)

Example SSH connection:

```
ssh -i mykey.pem ec2-user@public-ip
```

---

### Security Groups

Security Groups act as **virtual firewalls** for EC2 instances.

They control inbound and outbound traffic.

Example rules:

| Protocol | Port | Purpose            |
| -------- | ---- | ------------------ |
| SSH      | 22   | Remote access      |
| HTTP     | 80   | Web traffic        |
| HTTPS    | 443  | Secure web traffic |

---

### Elastic IP

An **Elastic IP** is a static public IP address that can be associated with an EC2 instance.

It helps maintain a fixed IP address even if the instance stops or restarts.

---

## EC2 Storage Options

### 1. EBS (Elastic Block Store)

Persistent storage attached to EC2 instances.

Features:

* Data persists even after instance termination (if configured)
* Used for operating system and application storage

### 2. Instance Store

Temporary storage attached to the physical host machine.

Features:

* High performance
* Data is lost if instance stops or terminates

---

## Steps to Launch an EC2 Instance

1. Login to AWS Console
2. Navigate to EC2 Dashboard
3. Click **Launch Instance**
4. Select an AMI
5. Choose instance type
6. Configure instance settings
7. Add storage
8. Configure security group
9. Create or select key pair
10. Launch instance

---

## EC2 in DevOps

EC2 is widely used in DevOps workflows for:

* Hosting applications
* Running CI/CD pipelines
* Deploying microservices
* Testing environments
* Container orchestration platforms

EC2 integrates with many AWS services such as:

* S3
* CloudWatch
* IAM
* Auto Scaling
* Elastic Load Balancer

---

## Advantages of EC2

* Flexible and scalable infrastructure
* Full control over operating system
* Pay-per-use pricing
* Highly secure environment
* Global availability

---

## Conclusion

Amazon EC2 is one of the most important services in AWS. It provides scalable and flexible compute capacity in the cloud, allowing developers and organizations to run applications without managing physical servers.
