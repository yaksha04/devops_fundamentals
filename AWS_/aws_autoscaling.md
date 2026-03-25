# AWS Auto Scaling

## Introduction

**AWS Auto Scaling** automatically adjusts the number of EC2 instances based on traffic demand.

It ensures:

* High availability
* Cost optimization

---

## Why Auto Scaling?

Without Auto Scaling:

* Server overload during traffic spikes
* Wasted resources during low traffic

With Auto Scaling:

* Automatically add/remove instances

---

## Key Concepts

### Auto Scaling Group (ASG)

* Collection of EC2 instances

### Desired Capacity

* Number of instances you want running

### Min / Max Size

* Limits for scaling

---

## Scaling Types

### 1. Dynamic Scaling

* Based on metrics (CPU, memory)

### 2. Scheduled Scaling

* Based on time

### 3. Predictive Scaling

* Based on usage patterns

---

## Scaling Policies

Example:

* Add instance if CPU > 70%
* Remove instance if CPU < 30%

---

## Benefits

* High availability
* Cost efficiency
* Automatic recovery

---

## Auto Scaling in DevOps

* Handles traffic spikes
* Improves system reliability
* Reduces manual intervention

---

## Conclusion

Auto Scaling ensures your application runs smoothly under varying loads while optimizing costs.
