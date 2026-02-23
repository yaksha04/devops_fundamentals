# Docker Ports & Port Mapping

Understanding Docker ports is essential for:
- Accessing containers from browser
- Connecting services (Frontend ↔ Backend)
- Debugging network issues
- Production deployments

If ports are wrong → your app looks “down” even when it’s running.

---

# 1️⃣ What is a Port?

A port is a communication endpoint.

Examples:
- 80 → HTTP
- 443 → HTTPS
- 3306 → MySQL
- 5432 → PostgreSQL
- 3000 / 8080 → Common app ports

Every container runs services on specific internal ports.

---

# 2️⃣ Internal vs External Ports

Inside a container:
- App runs on internal port (e.g., 3000)

Outside (host machine):
- You access via host port (e.g., 8080)

Port mapping connects them.

---

# 3️⃣ Port Mapping Syntax

```bash
docker run -p <host_port>:<container_port> image

Example:

docker run -p 8080:80 nginx

Meaning:

Host:8080 → Container:80


If you open:

http://localhost:8080

Traffic is forwarded to container's port 80.

---

# 4️⃣ Visual Representation


Browser
|
localhost:8080
|
Host Machine
|
Docker Engine
|
Container (Port 80)


---

# 5️⃣ EXPOSE vs -p (Very Important)

## EXPOSE (Dockerfile)

```dockerfile
EXPOSE 3000

Only documents port

Does NOT publish port

Helps with clarity

-p (docker run)
docker run -p 3000:3000 myapp

Actually publishes port to host.

⚠ Interview Trap:

Q: Does EXPOSE make container accessible?
A: ❌ No. You must use -p or -P.

6️⃣ Publish All Exposed Ports
docker run -P myapp

Docker assigns random host ports automatically.

Check with:

docker ps
7️⃣ Binding to Specific IP
docker run -p 127.0.0.1:8080:80 nginx

Means:

Only accessible locally

Not from external network

Good for:

Development security

8️⃣ Multiple Port Mapping
docker run -p 8080:80 -p 8443:443 nginx

Maps:

8080 → 80

8443 → 443

9️⃣ Port Mapping in Docker Compose
services:
  web:
    image: nginx
    ports:
      - "8080:80"

Same concept as -p.

🔟 Common Beginner Mistakes

❌ Forgetting -p flag
❌ Using wrong container port
❌ Using localhost inside container
❌ Exposing sensitive services publicly

1️⃣1️⃣ Internal Container Communication

If two containers are in same network:

You DO NOT need port mapping.

Example:

Backend connects to database using:

mysql:3306

Not:

localhost:3306

Because:

Port mapping is only for host access

Containers use internal networking

1️⃣2️⃣ Debugging Port Issues

Check running containers:

docker ps

Look at PORTS column.

Inspect container:

docker inspect <container>

Test from inside container:

docker exec -it <container> sh
1️⃣3️⃣ Production Considerations

✔ Do not expose database ports publicly
✔ Use reverse proxy (NGINX, Traefik)
✔ Bind to specific IP if needed
✔ Avoid random high port chaos
✔ Use environment variables for flexibility

1️⃣4️⃣ Docker Ports vs VM Ports
Feature	Docker	VM
Port Isolation	Namespace-based	Full OS
Mapping Required	Yes	Usually direct
Lightweight	Yes	No
1️⃣5️⃣ Real Interview Questions

Q1: What happens if two containers try to use same host port?
→ Error: Port already allocated

Q2: Why can’t I access my container from browser?
→ Missing -p or wrong mapping

Q3: Difference between EXPOSE and -p?
→ EXPOSE documents, -p publishes
