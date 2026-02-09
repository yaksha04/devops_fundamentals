# Docker Image vs Docker Container

## Why This Comparison Matters

“Image” and “Container” are often used interchangeably by beginners —  
and that’s **wrong**.

Interviewers love this topic because:
- It looks simple
- It exposes shallow understanding instantly

If you can explain this clearly, you already sound like a DevOps engineer.

---

## What is a Docker Image?

A **Docker Image** is a **read-only blueprint** used to create containers.

Think of it as:
- A template
- A snapshot
- A class (OOP analogy)

### Key Characteristics of an Image

- Immutable (cannot be changed once built)
- Built using a `Dockerfile`
- Stored in a registry
- Consists of multiple **layers**
- Does **not** run by itself

Example:
```bash
docker build -t myapp:1.0 .
docker pull nginx
Image = what should be run

What is a Docker Container?
A Docker Container is a running instance of an image.

Think of it as:

A live process

An object created from a class

A running application

Key Characteristics of a Container
Created from an image

Has a writable layer

Can be started, stopped, restarted, deleted

Uses host OS kernel

Is ephemeral by default

Example:

docker run -d nginx
docker start mycontainer
docker stop mycontainer
Container = the actual running thing

Image vs Container (Side-by-Side Comparison)
Feature	Docker Image	Docker Container
Nature	Blueprint / Template	Running instance
State	Static	Dynamic
Mutability	Read-only	Writable layer
Purpose	Used to create containers	Runs applications
Storage	Stored in registry	Exists on host
Execution	Cannot execute	Actively running
Lifecycle	Build → Store	Create → Run → Stop → Delete
Layered Architecture (The Real Difference)
Image Layers
An image is made of read-only layers:

Base OS Layer
Dependency Layer
Application Layer
These layers are:

Cached

Reused

Shared across containers

Container Writable Layer
When a container starts:

Docker adds a thin writable layer on top of the image

Writable Container Layer  ← changes go here
------------------------
Read-only Image Layers
Key rule:

Any data written inside a container is lost when the container is deleted
(unless volumes are used).

One Image → Multiple Containers
This is important.

From one image, you can create many containers:

Image: nginx
 ├── Container 1
 ├── Container 2
 └── Container 3
All containers:

Share the same image

Have separate runtime state

Are isolated from each other

Lifecycle Difference (Exam + Interview Gold)
Image Lifecycle
Dockerfile → Image → Registry
Container Lifecycle
Image → Container → Running → Stopped → Deleted
Analogy (Use This in Interviews)
Image = Recipe 📘

Container = Dish 🍽️

You can cook many dishes from one recipe,
but changing the dish doesn’t change the recipe.

Common Beginner Mistakes (Be Honest With Yourself)
❌ “Image is running”
❌ “Container is stored in Docker Hub”
❌ “Image has data persistence”

Correct thinking:

Images don’t run

Containers don’t get stored in registries

Persistence requires volumes

When Do You Use What?
You build images when:

Packaging applications

Versioning software

Sharing apps

You run containers when:

Executing applications

Scaling services

Deploying to production

Image vs Container vs VM (Quick Context)
Feature	Image	Container	Virtual Machine
OS	❌	Shared	Full OS
Runtime	❌	✅	✅
Weight	Very Light	Light	Heavy
Purpose	Template	Execution	Full system
Conclusion
If you remember only one line, remember this:

Docker Image = Blueprint
Docker Container = Running Instance
