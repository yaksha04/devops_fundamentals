# Kubernetes Services

A Service in Kubernetes is used to expose Pods and provide stable networking.

Pods are ephemeral and their IP addresses change when they are recreated.  
A Service provides a stable IP and DNS name that routes traffic to the correct Pods.

---

# 1. Why Services Are Needed

Problem:

- Pods get dynamic IP addresses
- Pods can be destroyed and recreated anytime
- Clients cannot rely on Pod IPs

Solution:

Service provides:
- Stable IP
- DNS name
- Load balancing
- Service discovery

---

# 2. How Services Work

Services use **labels and selectors** to identify Pods.

Example:

Pods:


app: nginx


Service selector:


selector:
app: nginx


The Service automatically forwards traffic to all matching Pods.

---

# 3. Basic Service YAML

Example:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP

Apply:

kubectl apply -f service.yaml
4. Important Fields
selector

Identifies which Pods receive traffic.

selector:
  app: nginx
port

Port exposed by the Service.

port: 80
targetPort

Port on the container inside the Pod.

targetPort: 80
type

Defines how the Service is exposed.

Common types:

ClusterIP

NodePort

LoadBalancer

ExternalName

5. Types of Kubernetes Services
1. ClusterIP (Default)

Accessible only inside the cluster.

Used for internal communication between microservices.

Example:

type: ClusterIP

Access:

http://service-name
2. NodePort

Exposes service on each node's IP at a specific port.

Port range:

30000–32767

Example:

type: NodePort
ports:
  - port: 80
    targetPort: 80
    nodePort: 30007

Access:

http://NodeIP:30007

Used mostly for development and testing.

3. LoadBalancer

Creates an external cloud load balancer.

Supported in:

AWS

GCP

Azure

Example:

type: LoadBalancer

Kubernetes automatically provisions a cloud load balancer.

4. ExternalName

Maps a service to an external DNS name.

Example:

type: ExternalName
externalName: example.com

Used for connecting to external services.

6. Service Discovery

Kubernetes automatically creates DNS entries.

Example:

http://nginx-service

Inside cluster:

http://nginx-service.default.svc.cluster.local

Pods can communicate using service names.

7. Load Balancing

When multiple Pods match a Service selector:

Service automatically distributes traffic across Pods.

Example:

3 Pods behind Service:

Pod1
Pod2
Pod3

Incoming traffic is balanced automatically.

8. Inspecting Services

List services:

kubectl get services

Detailed info:

kubectl describe service nginx-service

Check endpoints:

kubectl get endpoints
9. Testing Service

Create deployment:

kubectl create deployment nginx --image=nginx

Expose deployment:

kubectl expose deployment nginx --port=80 --type=NodePort

Get service:

kubectl get service

Access via:

minikube service nginx
10. Service vs Pod Networking
Feature	Pod	Service
IP stability	❌	✅
Load balancing	❌	✅
DNS name	❌	✅
External access	❌	✅
11. Real Production Architecture

Typical setup:

User
  ↓
LoadBalancer Service
  ↓
Deployment
  ↓
ReplicaSet
  ↓
Pods
  ↓
Containers

Service acts as the networking layer between users and Pods.
