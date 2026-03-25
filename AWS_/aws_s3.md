# AWS S3 (Simple Storage Service)

## Introduction

**Amazon S3 (Simple Storage Service)** is an object storage service used to store and retrieve any amount of data from anywhere on the internet.

S3 stores data in the form of **objects** inside **buckets**.

---

## Key Concepts

### Bucket

* A container for storing objects
* Globally unique name

### Object

* File + metadata stored in S3

---

## Features of S3

### 1. Scalability

* Unlimited storage capacity

### 2. Durability

* 99.999999999% (11 9’s durability)

### 3. Availability

* Highly available across regions

### 4. Security

* Bucket policies
* IAM integration
* Encryption (at rest & in transit)

---

## Storage Classes

| Class                | Use Case                 |
| -------------------- | ------------------------ |
| S3 Standard          | Frequently accessed data |
| S3 IA                | Infrequent access        |
| Glacier              | Archival storage         |
| Glacier Deep Archive | Long-term backup         |

---

## Versioning

* Keeps multiple versions of objects
* Protects against accidental deletion

---

## Use Cases

* Static website hosting
* Backup and restore
* Data lakes
* Log storage

---

## S3 in DevOps

* Store build artifacts
* Backup CI/CD pipelines
* Store logs and monitoring data

---

## Advantages

* Highly durable
* Scalable
* Cost-effective
* Easy integration

---

## Conclusion

S3 is a highly reliable and scalable object storage service widely used for storing data, backups, and static content.
