# Kubernetes Ingress

Ingress is a Kubernetes API object used to manage external access to services in a cluster.

It allows you to expose multiple services using a single external IP through HTTP/HTTPS routing.

Ingress acts as a smart router for incoming traffic.

---

# 1. Why Ingress is Needed

Problem without Ingress:

Each service exposed externally requires a separate LoadBalancer.

Example:

Service A → LoadBalancer  
Service B → LoadBalancer  
Service C → LoadBalancer  

This leads to:

- High cloud cost
- Complex networking
- Difficult routing management

Solution:

Ingress allows routing multiple services through a single entry point.

---

# 2. How Ingress Works

Traffic Flow:

User → Ingress → Service → Pods

Ingress receives incoming requests and routes them to the correct service based on rules.

Example routing:


example.com/app1 → service-app1
example.com/app2 → service-app2


Or path-based routing:


example.com/api → api-service
example.com/web → web-service


---

# 3. Important Components

## Ingress Resource

Defines routing rules for incoming traffic.

---

## Ingress Controller

Actual component that implements the routing rules.

Examples:

- NGINX Ingress Controller
- Traefik
- HAProxy
- AWS ALB Ingress Controller

Without an Ingress Controller, Ingress will not work.

---

# 4. Basic Ingress YAML

Example:

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example-ingress
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /app1
        pathType: Prefix
        backend:
          service:
            name: app1-service
            port:
              number: 80

Apply:

kubectl apply -f ingress.yaml
5. Path-Based Routing

Example:

apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: app-routing
spec:
  rules:
  - host: example.com
    http:
      paths:
      - path: /frontend
        pathType: Prefix
        backend:
          service:
            name: frontend-service
            port:
              number: 80

      - path: /backend
        pathType: Prefix
        backend:
          service:
            name: backend-service
            port:
              number: 80

Traffic Routing:

example.com/frontend → frontend-service
example.com/backend → backend-service
6. Host-Based Routing

Example:

rules:
- host: api.example.com
  http:
    paths:
    - path: /
      pathType: Prefix
      backend:
        service:
          name: api-service
          port:
            number: 80

- host: web.example.com
  http:
    paths:
    - path: /
      pathType: Prefix
      backend:
        service:
          name: web-service
          port:
            number: 80
7. TLS Configuration (HTTPS)

Ingress supports HTTPS using TLS.

Example:

tls:
- hosts:
  - example.com
  secretName: tls-secret

TLS certificates are stored in Kubernetes Secrets.

8. Enable Ingress in Minikube

Enable addon:

minikube addons enable ingress

Check controller:

kubectl get pods -n ingress-nginx
9. Inspecting Ingress

List ingress:

kubectl get ingress

Detailed info:

kubectl describe ingress example-ingress

Check services:

kubectl get services
10. Example Architecture

Typical setup:

User
  ↓
Ingress Controller
  ↓
Ingress Rules
  ↓
Services
  ↓
Pods

Ingress acts as the entry point for external HTTP/HTTPS traffic.

11. Advantages of Ingress

Single entry point for multiple services

Cost-efficient compared to multiple LoadBalancers

Supports path-based routing

Supports host-based routing

Enables SSL/TLS termination

Centralized traffic management

12. Ingress vs Service
Feature	Service	Ingress
Internal communication	Yes	No
External access	Limited	Yes
Routing rules	No	Yes
SSL termination	No	Yes
Load balancing	Basic	Advanced

Service exposes applications.
Ingress manages routing to those services.

13. Common Issues
Ingress controller not installed

Ingress resource alone does nothing.

Controller must be running.

Incorrect service name

If service name is wrong, traffic will fail.

Check:

kubectl get svc
DNS configuration missing

Host-based routing requires proper DNS mapping.

14. Interview-Level Understanding

Important points:

Ingress manages external HTTP/HTTPS access

Requires an Ingress Controller

Supports host-based and path-based routing

Enables SSL termination

Reduces number of LoadBalancers
