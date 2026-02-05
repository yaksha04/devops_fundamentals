# Introduction to Kubernetes (Container Orchestration)

## Why Kubernetes Exists

Docker solved one big problem:
> “It runs the same everywhere.”

But the moment you move beyond **one container on one server**, new problems appear:

- ❌ What if a container crashes?
- ❌ How do you scale containers up/down?
- ❌ How do containers talk to each other?
- ❌ How do you deploy updates without downtime?
- ❌ How do you manage hundreds of containers across many machines?

Managing containers **manually** does not scale.  
This operational nightmare is why Kubernetes exists.

---

## What is Kubernetes?

**:contentReference[oaicite:1]{index=1}** (also called **K8s**) is an open-source **container orchestration platform** that automates:

- Deployment
- Scaling
- Networking
- Self-healing
- Load balancing
- Configuration & secrets management

In simple words:
> **Docker runs containers. Kubernetes runs Docker at scale.**

---

## From Containers to Orchestration

Running containers manually:
```bash
docker run
docker stop
docker restart
Works for:

Learning

Small demos

Fails badly for:

Production

High traffic

Multiple services

Zero-downtime deployments

Kubernetes replaces manual container management with declarative automation.

Core Kubernetes Idea (Mental Model)

You don’t tell Kubernetes how to do things.
You tell it what you want.

Example:

“I want 3 replicas of this app running at all times.”

Kubernetes figures out:

Where to run them

How to restart them

How to replace failed ones

Kubernetes Architecture Overview
High-Level Architecture
Kubernetes Cluster
│
├── Control Plane (Master Node)
│   ├── API Server
│   ├── Scheduler
│   ├── Controller Manager
│   └── etcd (cluster state)
│
└── Worker Nodes
    ├── kubelet
    ├── container runtime (Docker / containerd)
    └── Pods (running containers)

Control Plane Components
1. API Server

Entry point to the cluster

All commands go through it (kubectl)

Validates and processes requests

2. Scheduler

Decides which pod runs on which node

Based on CPU, memory, constraints, policies

3. Controller Manager

Ensures desired state = actual state

Example:

If 3 pods are required and 1 dies → creates a new one

4. etcd

Distributed key-value store

Stores entire cluster state

If etcd dies → cluster memory loss (very bad)

Worker Node Components
kubelet

Agent running on each node

Talks to API server

Ensures containers are running as instructed

Container Runtime

Runs the containers

Examples:

Docker

containerd

CRI-O

What is a Pod?

A Pod is the smallest deployable unit in Kubernetes.

A pod can contain:

One container (most common)

Multiple tightly-coupled containers

Key points:

Containers in a pod share:

Network

Storage

Pods are ephemeral (they can die anytime)

You don’t scale containers.
You scale pods.

Important Kubernetes Objects
Object	Purpose
Pod	Runs containers
Deployment	Manages replicas & updates
Service	Exposes pods to network
ReplicaSet	Ensures desired pod count
ConfigMap	Non-secret configuration
Secret	Sensitive data
Namespace	Logical isolation
Ingress	HTTP/HTTPS routing
Kubernetes vs Docker Swarm vs VMs
Feature	Virtual Machines	Docker Swarm	Kubernetes
Scaling	Manual	Limited	Advanced
Self-healing	❌	Basic	✅
Networking	OS-level	Simple	Powerful
Industry Adoption	High	Low	Massive
Complexity	Medium	Low	High
Production Grade	✅	⚠️	✅✅
