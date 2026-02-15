# Important Docker Commands (Beyond Basics)

This guide covers essential Docker commands you must know for:
- DevOps roles
- Real-world debugging
- Interviews
- Production environments

If you only know `docker ps` and `docker run`, you're not ready yet.

---

# 1️⃣ Container Lifecycle Commands

## Run a Container

```bash
docker run nginx
Common flags:

docker run -d -p 8080:80 --name web nginx
Flag	Meaning
-d	Run in detached mode (background)
-p	Port mapping (host:container)
--name	Assign custom container name
Start / Stop Container
docker start <container>
docker stop <container>
Difference:

run → Create + Start

start → Start existing container

Restart Container
docker restart <container>
Remove Container
docker rm <container>
Force remove running container:

docker rm -f <container>
2️⃣ Image Management Commands
Build Image
docker build -t myapp:1.0 .
Flag	Meaning
-t	Tag image
.	Current directory as build context
Remove Image
docker rmi <image_id>
Force remove:

docker rmi -f <image_id>
Pull Image
docker pull nginx
Push Image
docker push username/myapp:1.0
Requires login:

docker login
3️⃣ Debugging & Inspection Commands (VERY IMPORTANT)
View Logs
docker logs <container>
Live logs:

docker logs -f <container>
Execute Command Inside Container
docker exec -it <container> sh
Or bash:

docker exec -it <container> bash
Used for:

Debugging

Checking config

Installing packages (not recommended in prod)

Inspect Container or Image
docker inspect <container_or_image>
Shows:

IP address

Mounts

Environment variables

Network info

4️⃣ Volume Commands
List Volumes
docker volume ls
Create Volume
docker volume create myvolume
Remove Volume
docker volume rm myvolume
5️⃣ Network Commands
List Networks
docker network ls
Create Network
docker network create mynetwork
Inspect Network
docker network inspect mynetwork
6️⃣ Cleanup Commands (Production Useful)
Remove Stopped Containers
docker container prune
Remove Unused Images
docker image prune
Remove Everything Unused
docker system prune
Remove everything including volumes:

docker system prune -a --volumes
⚠ Be careful — this deletes unused resources.

7️⃣ System Information Commands
Docker Info
docker info
Shows:

Storage driver

Number of containers

Number of images

Docker root directory

Docker Version
docker version
Shows:

Client version

Server version

API version

🔥 Common Interview Questions
Q: What is the difference between docker run and docker start?
run creates a new container and starts it

start starts an existing stopped container

Q: How do you debug a crashing container?
docker ps -a

docker logs <container>

docker inspect <container>

docker exec -it <container> sh

🧠 Recommended Command Mastery Order
run / stop / start / rm

build / pull / push

logs / exec / inspect

volumes

networking

prune & cleanup

🎯 Final Advice
If you cannot confidently use:

docker logs

docker exec

docker inspect

docker system prune

You are not production-ready yet.

These commands separate:

Docker beginners
from
DevOps engineers

Next Topics
Dockerfile deep dive

Multi-container setup with Docker Compose

Image optimization techniques

Docker security basics


---

If you want next, I suggest:

- 🔥 `docker run` deep internal explanation  
- 🔥 Docker Compose full guide  
- 🔥 30 most asked Docker interview questions  
- 🔥 Advanced image optimization & multi-stage builds  

Pick one. We go serious from here 🚀
