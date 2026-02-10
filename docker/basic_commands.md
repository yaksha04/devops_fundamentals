Docker Commands: `docker ps` and `docker images`

## Why These Commands Matter

These are **diagnostic commands**.
If Docker is misbehaving, these are usually the **first commands you run**.

Interviewers expect you to know:
- What they show
- When to use them
- Common flags
- Common mistakes

---

## `docker ps` – List Containers

### Purpose
Shows **running containers** by default.


docker ps
What It Displays
Column	Meaning
CONTAINER ID	Short unique ID of the container
IMAGE	Image used to create the container
COMMAND	Command running inside container
CREATED	When container was created
STATUS	Running / Exited / Restarting
PORTS	Port mappings
NAMES	Auto or user-defined container name

Example Output
css
Copy code
CONTAINER ID   IMAGE     COMMAND       STATUS       PORTS     NAMES
a1b2c3d4e5f6   nginx     "nginx -g…"   Up 5 mins    80/tcp   web-server
👉 This means:

Container exists

Container is running

Created from nginx image

docker ps -a – List All Containers
By default, stopped containers are hidden.

bash
Copy code
docker ps -a
Shows:

Running containers

Stopped containers

Exited containers

Very important for debugging.

Common Interview Trap
❌ “My container disappeared”
✅ It’s just stopped — check with docker ps -a

Container States You’ll See
Status	Meaning
Up	Container is running
Exited	Container stopped
Created	Created but never started
Restarting	Crashing and restarting

docker images / docker image ls – List Images
Purpose
Shows locally available Docker images.

bash
Copy code
docker images
# OR (newer, preferred)
docker image ls
What It Displays
Column	Meaning
REPOSITORY	Image name
TAG	Version
IMAGE ID	Unique image identifier
CREATED	When image was built
SIZE	Image size

Example Output
css
Copy code
REPOSITORY   TAG     IMAGE ID       CREATED       SIZE
nginx        latest  605c77e624dd   2 weeks ago   141MB
myapp        v1      a1b2c3d4e5f6   1 hour ago    220MB
👉 This means:

Images exist locally

They may or may not have containers running

Image vs Container Visibility (Very Important)
Command	Shows
docker images	Images stored locally
docker ps	Running containers
docker ps -a	All containers

Images can exist without containers
Containers cannot exist without images

Useful Flags (Know These)
Short Output

docker ps -q
docker images -q
Returns only IDs (used in scripts).

Filter by Image
bash
Copy code
docker ps --filter ancestor=nginx
Format Output (Advanced)
bash
Copy code
docker ps --format "table {{.Names}}\t{{.Status}}"
Common Beginner Mistakes (Be Honest)
❌ Running docker ps and thinking Docker is empty
❌ Deleting images while containers still exist
❌ Confusing image size with container memory usage

Correct mindset:

docker ps → runtime

docker images → storage

Typical Debug Flow (Real World)
1️⃣ Check containers

bash
Copy code
docker ps -a
2️⃣ Check image exists

bash
Copy code
docker images
3️⃣ Remove stopped containers

bash
Copy code
docker rm <container_id>
4️⃣ Remove unused images
docker rmi <image_id>

Quick Interview Q&A
Q: Can docker ps show stopped containers?
A: ❌ No, use docker ps -a

Q: Does docker images show running containers?
A: ❌ No, it shows images only

Q: Can one image have multiple containers?
A: ✅ Yes

Summary (One-Liners)
docker ps → running containers

docker ps -a → all containers

docker images → local images

Containers = runtime

Images = storage
