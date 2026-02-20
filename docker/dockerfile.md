# Dockerfile Basics

A Dockerfile is a text file that contains instructions to build a Docker image.

It defines:
- Base image
- Application dependencies
- Environment configuration
- Startup command

Think of it as:
> Blueprint for creating a Docker image.

---

# Basic Structure of a Dockerfile

Example:

```dockerfile
# Base image
FROM node:18

# Set working directory
WORKDIR /app

# Copy files
COPY package.json .

# Install dependencies
RUN npm install

# Copy remaining files
COPY . .

# Expose port
EXPOSE 3000

# Start application
CMD ["node", "app.js"]
Core Dockerfile Instructions (Must Know)
1️⃣ FROM (Mandatory)

Defines the base image.

FROM ubuntu:22.04

Every Dockerfile must start with FROM.

Best practice:

Use official images

Use specific version tags

Avoid latest in production

2️⃣ WORKDIR

Sets working directory inside container.

WORKDIR /app

If directory doesn't exist → Docker creates it.

Better than using RUN cd.

3️⃣ COPY

Copies files from host to image.

COPY . .

Syntax:

COPY <source> <destination>
4️⃣ ADD (Avoid if not needed)

Similar to COPY but can:

Extract tar files

Download URLs

Best practice:

Prefer COPY unless you specifically need ADD features.

5️⃣ RUN

Executes commands while building image.

RUN apt update && apt install -y curl

Important:

Creates a new image layer

Combine commands to reduce layers

6️⃣ EXPOSE

Documents which port app uses.

EXPOSE 8080

Note:

Does NOT publish port

Use docker run -p to map ports

7️⃣ CMD

Defines default command to run container.

CMD ["node", "app.js"]

Only one CMD allowed.
If multiple → last one wins.

8️⃣ ENTRYPOINT

Defines main container executable.

ENTRYPOINT ["node"]

Difference:

ENTRYPOINT = fixed main command

CMD = default arguments

Image Layering Concept

Every instruction creates a new layer.

Example:

Layer 1 → FROM
Layer 2 → RUN
Layer 3 → COPY
Layer 4 → CMD

More layers = larger image.

Goal:

Minimize layers.

Build Image from Dockerfile
docker build -t myapp:1.0 .

-t → tag image

. → current directory (build context)

.dockerignore (Very Important)

Used to exclude files from build context.

Example:

node_modules
.git
.env

Why?

Smaller image

Faster build

Better security

Best Practices (Production Mindset)

✔ Use minimal base images (alpine if possible)
✔ Avoid root user
✔ Use multi-stage builds
✔ Pin versions
✔ Clean package cache
✔ Use .dockerignore
