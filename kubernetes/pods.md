# Kubernetes Pods

A Pod is the smallest deployable unit in Kubernetes.

You NEVER deploy containers directly in Kubernetes.
You deploy Pods.

---

# 1. What is a Pod?

A Pod is:

- A wrapper around one or more containers
- A shared network namespace
- A shared storage environment
- A single logical host for containers

Think of it like:

Container = App  
Pod = Mini machine running that app  

---

# 2. Why Pods Exist

Containers are isolated by default.

Kubernetes groups tightly coupled containers into a Pod so they can:

- Share the same IP address
- Share localhost communication
- Share storage volumes
- Start and stop together

Without Pods, multi-container communication would be complex.

---

# 3. Pod Characteristics

- Each Pod gets a unique IP
- Containers inside a Pod share:
  - Same IP
  - Same port space
  - Same volumes
- Pods are ephemeral (temporary)
- Pods are not self-healing by default (ReplicaSet handles that)

---

# 4. Single Container Pod

Most common type.

Example YAML:

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx-pod
spec:
  containers:
  - name: nginx
    image: nginx
    ports:
    - containerPort: 80

Apply:

kubectl apply -f pod.yaml
5. Multi-Container Pod (Sidecar Pattern)

Used when containers must run together.

Example:

Main app container

Logging sidecar container

Example YAML:

apiVersion: v1
kind: Pod
metadata:
  name: multi-container-pod
spec:
  containers:
  - name: app
    image: nginx
  - name: sidecar
    image: busybox
    command: ["sh", "-c", "while true; do echo logging; sleep 5; done"]

Use case:

Logging

Monitoring

Proxy injection

6. Pod Lifecycle

Phases:

Pending

Running

Succeeded

Failed

Unknown

Check status:

kubectl get pods

Detailed info:

kubectl describe pod <pod-name>
7. Pod Restart Policy

Defined in spec:

Always (default)

OnFailure

Never

Example:

restartPolicy: OnFailure
8. Pod Networking

Every Pod gets its own IP

Containers inside Pod communicate via localhost

Pods communicate using Pod IP or Service

Important:
Pod IP changes if Pod is recreated.

That’s why Services exist.

9. Pod Storage (Volumes)

Containers in a Pod can share volumes.

Example:

volumes:
- name: shared-volume
  emptyDir: {}

containers:
- name: app
  image: nginx
  volumeMounts:
  - mountPath: /data
    name: shared-volume

Common volume types:

emptyDir

hostPath

PersistentVolumeClaim

10. Debugging Pods

Get logs:

kubectl logs <pod-name>

Exec into container:

kubectl exec -it <pod-name> -- /bin/bash

Check events:

kubectl describe pod <pod-name>
11. Important Pod Commands
kubectl get pods
kubectl get pods -o wide
kubectl delete pod <name>
kubectl edit pod <name>
kubectl explain pod
12. Key Interview Points

Pod is the smallest deployable unit.

Pods are ephemeral.

Pods share network namespace.

Pods are not meant to be created directly in production.

Deployments manage Pods.

If a Pod dies, IP changes.

Services provide stable networking.

If someone says they deploy Pods directly in production,
they don’t understand Kubernetes properly.

Conclusion

Pods are the foundation of Kubernetes.

But in real-world production:

You almost never create Pods directly.
You use Deployments, StatefulSets, or DaemonSets.

Master Pods first.
Then move to ReplicaSets and Deployments.
