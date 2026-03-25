# AWS EBS (Elastic Block Store)

## Introduction

**Amazon EBS (Elastic Block Store)** provides block-level storage that can be attached to EC2 instances.

It is mainly used as a **disk for virtual servers**.

---

## Key Features

### 1. Persistent Storage

* Data remains even after instance stops

### 2. High Performance

* SSD and HDD options

### 3. Backup Support

* Snapshots stored in S3

---

## Volume Types

| Type      | Use Case             |
| --------- | -------------------- |
| gp3 / gp2 | General purpose      |
| io1 / io2 | High-performance     |
| st1       | Throughput optimized |
| sc1       | Cold storage         |

---

## EBS vs S3

| Feature    | EBS           | S3             |
| ---------- | ------------- | -------------- |
| Type       | Block storage | Object storage |
| Use        | OS, databases | Files, backups |
| Attachment | EC2 only      | Anywhere       |

---

## Snapshots

* Backup of EBS volumes
* Stored in S3
* Used for recovery

---

## Use Cases

* Database storage
* OS boot volume
* Application data storage

---

## EBS in DevOps

* Persistent storage for applications
* Backup strategy using snapshots
* Database hosting

---

## Conclusion

EBS provides reliable and high-performance block storage for EC2 instances, making it essential for running stateful applications.
