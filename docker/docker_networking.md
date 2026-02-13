Docker Networking
Why Docker Networking Matters

Running one container is easy.

Running multiple containers that talk to each other is where things get real.

Examples:

Backend ↔ Database

Frontend ↔ Backend

Microservice ↔ Microservice

Container ↔ Host machine

Without networking knowledge:

Containers won’t communicate

Ports won’t expose properly

Debugging becomes painful

How Docker Networking Works (Core Idea)

Every container:

Gets its own network namespace

Gets its own IP address

Can communicate using virtual networking

Docker creates virtual networks internally.

Think of it like:

Mini virtual LANs inside your system.

Default Network Drivers

Docker supports multiple network drivers.

1️⃣ Bridge Network (Default)

When you run:

docker run nginx


Docker automatically attaches it to the bridge network.

What is Bridge?

Default local network

Containers can talk to each other (if on same bridge)

Isolated from host unless ports are exposed

Architecture View
Host Machine
│
├── docker0 (bridge)
│     ├── Container A (172.x.x.x)
│     ├── Container B (172.x.x.x)
│     └── Container C (172.x.x.x)

Important

To access container from browser:

docker run -p 8080:80 nginx


8080 → host port

80 → container port

Without -p, container stays internal.

2️⃣ Host Network
docker run --network host nginx


Container shares host network directly.

Meaning:

No port mapping needed

Container uses host IP

Higher performance

Less isolation

Used in:

Performance-critical apps

Monitoring tools

⚠ Not recommended unless necessary.

3️⃣ None Network
docker run --network none nginx


No internet

No external communication

Fully isolated

Used for:

Security testing

Air-gapped containers

4️⃣ Overlay Network

Used in:

Docker Swarm

Multi-host setups

Allows containers on different machines to communicate.

Think:

Virtual network across multiple servers.

User-Defined Bridge Network (Very Important)

Instead of using default bridge, create custom network:

docker network create mynetwork


Run containers inside it:

docker run -d --name app --network mynetwork myapp
docker run -d --name db --network mynetwork mysql


Now containers can talk using names:

app → db


No need to use IP addresses.

This is best practice.

Networking Commands You Must Know

List networks:

docker network ls


Inspect network:

docker network inspect bridge


Create network:

docker network create mynet


Remove network:

docker network rm mynet

How Containers Communicate
Same Network

Use container name

Docker provides internal DNS

Example:

http://db:3306

Different Networks

Cannot communicate unless connected manually

Port Mapping Explained Properly
docker run -p 3000:80 nginx


Meaning:

Host:3000 → Container:80


Browser hits:

localhost:3000


Docker forwards traffic internally.

Real Interview Scenario

Q: Why can't my backend connect to MySQL container?

Common reasons:

Different networks

Using localhost instead of container name

MySQL not exposing correct port

Correct way:

Use user-defined bridge

Use container names

Avoid hardcoding IPs

Docker Networking vs VM Networking
Feature	Docker	VM
IP	Virtual per container	Full OS IP
Isolation	Namespace-based	Hardware-level
Setup	Easy	Complex
Performance	Lightweight	Heavier
Common Beginner Mistakes

❌ Using localhost inside container
❌ Forgetting -p flag
❌ Not creating user-defined network
❌ Using container IP instead of name

Golden rule:

Inside Docker network, use container names — not localhost.

Debugging Networking Issues

Check container IP:

docker inspect <container_id>


Enter container:

docker exec -it <container_id> sh


Ping another container:

ping db

Real DevOps Insight

In production:

Docker networking concepts extend to

Kubernetes Services

Ingress

Service Mesh

If you understand Docker networking,
Kubernetes networking becomes easier.
