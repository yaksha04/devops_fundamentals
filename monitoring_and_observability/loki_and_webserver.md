Loki + Web Server (Nginx) Monitoring Setup using Docker
Introduction

In this setup, we will monitor a web server (Nginx) using:

Grafana Loki → Log aggregation
Promtail → Log collector
Grafana → Visualization dashboard
Docker Compose → Container orchestration

This setup simulates a real-world DevOps logging pipeline.

Architecture Overview
Nginx (Web Server)
        ↓
   Log Files (/var/log/nginx)
        ↓
     Promtail
        ↓
       Loki
        ↓
     Grafana
Prerequisites

Make sure you have:

Docker installed
Docker Compose installed
Basic Linux knowledge

Check installation:

docker --version
docker-compose --version
Project Structure

Create a project folder:

mkdir loki-monitoring
cd loki-monitoring

Create files:

touch docker-compose.yml
touch promtail-config.yml
touch loki-config.yml
Step 1: Docker Compose File

Create docker-compose.yml

version: "3.8"

services:
  nginx:
    image: nginx:latest
    container_name: nginx
    ports:
      - "8080:80"
    volumes:
      - ./nginx_logs:/var/log/nginx

  loki:
    image: grafana/loki:2.9.0
    container_name: loki
    ports:
      - "3100:3100"
    command: -config.file=/etc/loki/local-config.yaml
    volumes:
      - ./loki-config.yml:/etc/loki/local-config.yaml

  promtail:
    image: grafana/promtail:2.9.0
    container_name: promtail
    volumes:
      - ./promtail-config.yml:/etc/promtail/config.yml
      - ./nginx_logs:/var/log/nginx
    command: -config.file=/etc/promtail/config.yml

  grafana:
    image: grafana/grafana:latest
    container_name: grafana
    ports:
      - "3000:3000"
Step 2: Loki Configuration

Create loki-config.yml

auth_enabled: false

server:
  http_listen_port: 3100

common:
  path_prefix: /loki
  storage:
    filesystem:
      chunks_directory: /loki/chunks
      rules_directory: /loki/rules

schema_config:
  configs:
    - from: 2020-10-24
      store: boltdb-shipper
      object_store: filesystem
      schema: v11
      index:
        prefix: index_
        period: 24h

limits_config:
  allow_structured_metadata: false
Step 3: Promtail Configuration

Create promtail-config.yml

server:
  http_listen_port: 9080

positions:
  filename: /tmp/positions.yaml

clients:
  - url: http://loki:3100/loki/api/v1/push

scrape_configs:
  - job_name: nginx_logs
    static_configs:
      - targets:
          - localhost
        labels:
          job: nginx
          __path__: /var/log/nginx/*.log
Step 4: Run the Setup

Start everything:

docker-compose up -d

Check running containers:

docker ps
Step 5: Generate Logs

Open browser:

http://localhost:8080

Refresh multiple times to generate logs.

Step 6: Access Grafana

Open:

http://localhost:3000

Default login:

Username: admin
Password: admin
Step 7: Add Loki Data Source

In Grafana:

Go to Settings → Data Sources
Click Add Data Source
Select Loki
URL:
http://loki:3100
Click Save & Test
Step 8: View Logs in Grafana

Go to Explore → Loki

Run query:

{job="nginx"}

You will see live logs from Nginx.

Step 9: Advanced Log Query (LogQL)

Find errors:

{job="nginx"} |= "error"

Find HTTP 404:

{job="nginx"} |= "404"
