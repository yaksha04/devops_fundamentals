# Docker Architecture

## Overview

Docker follows a **client–server architecture**.

At a high level:
- The **Docker Client** sends commands
- The **Docker Engine (Daemon)** does the heavy lifting
- Containers run on the **host machine**

All communication happens through **REST APIs** (local or remote).

> Docker is not magic.  
> It’s a well-designed client talking to a background service.

---

## Core Components of Docker Architecture

Docker architecture mainly consists of:

1. Docker Client  
2. Docker Daemon (Docker Engine)  
3. Docker Objects  
   - Images  
   - Containers  
   - Volumes  
   - Networks  

---

## High-Level Architecture Diagram

Docker Client
|
| (REST API / CLI commands)
v
Docker Daemon (dockerd)
|
├── Images
├── Containers
├── Volumes
└── Networks
|
Host Operating System
|
Physical Hardware


---

## 1. Docker Client

The **Docker Client** is what users interact with.

Examples:
```bash
docker build
docker pull
docker run
docker ps
Key points:

CLI tool (docker)

Sends commands to Docker Daemon

Can communicate with:

Local daemon

Remote daemon (over TCP)

Client does nothing by itself.
It only requests. The daemon executes.

2. Docker Daemon (Docker Engine)
The Docker Daemon (dockerd) is the brain.

Responsibilities:

Builds images

Runs containers

Manages networking

Manages volumes

Talks to container runtime

Runs as a background service.

Internal Components
Docker Daemon
│
├── REST API
├── Image Manager
├── Container Manager
├── Network Manager
└── Volume Manager
If the daemon stops:

❌ Containers stop

❌ Docker commands fail

3. Docker Images
A Docker Image is a read-only template used to create containers.

Characteristics:

Built using a Dockerfile

Layered architecture

Immutable

Example:

docker build -t myapp .
Image layers:

Base OS Layer
App Dependencies Layer
Application Code Layer
Images don’t run.
Containers do.

4. Docker Containers
A Container is a running instance of an image.

Key traits:

Lightweight

Isolated

Ephemeral (can be destroyed anytime)

Example:

docker run -d nginx
Internally:

Uses Linux namespaces

Uses cgroups for resource limits

Shares host OS kernel

Container ≠ VM
No guest OS inside a container.

5. Container Runtime
The container runtime actually runs containers.

Modern Docker uses:

containerd

runc

Flow:

Docker CLI
 → Docker Daemon
   → containerd
     → runc
       → Linux Kernel
Docker itself does NOT directly talk to the kernel.

6. Docker Registry
A Docker Registry stores images.

Types:

Public Registry

Docker Hub

Private Registry

AWS ECR

Azure ACR

GCP Artifact Registry

Self-hosted

Example:

docker pull nginx
docker push myimage
Image flow:

Registry → Image → Container
7. Docker Networking
Docker provides networking using drivers.

Common drivers:

bridge (default)

host

none

overlay (multi-host)

Each container:

Gets its own IP

Uses virtual ethernet

8. Docker Volumes
Volumes provide persistent storage.

Why volumes?

Containers are temporary

Data must survive restarts

Types:

Volumes

Bind mounts

Example:

docker run -v data:/app/data myapp
Docker Architecture Summary (One Shot)
User
 |
Docker CLI
 |
Docker REST API
 |
Docker Daemon (dockerd)
 |
containerd
 |
runc
 |
Linux Kernel
 |
Hardware
Docker vs Virtual Machines (Architecture View)
Feature	Docker	Virtual Machine
OS	Shared Host Kernel	Full Guest OS
Startup	Seconds	Minutes
Resource Usage	Low	High
Isolation	Process-level	Hardware-level
Why Docker Architecture Matters in DevOps
Understanding architecture helps you:

Debug container issues

Optimize performance

Explain internals in interviews

Transition smoothly to Kubernetes

Interviewers often ask:

“What happens internally when you run docker run?”

If you know this architecture — you’re already ahead.

Conclusion
Docker’s power comes from:

Client–server design

Lightweight containers

Kernel-level isolation

Clean separation of concerns

Docker didn’t remove servers.
It removed painful server management.

