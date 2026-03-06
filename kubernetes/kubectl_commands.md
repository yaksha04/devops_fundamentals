# kubectl Commands Guide

kubectl is the command-line tool used to interact with Kubernetes clusters.

It allows you to:
- Deploy applications
- Inspect cluster resources
- Debug running workloads
- Manage configurations

---

# 1. Cluster Information Commands

Check cluster information:


kubectl cluster-info


Check nodes in the cluster:


kubectl get nodes


Detailed node information:


kubectl describe node <node-name>


---

# 2. Pod Management Commands

List pods:


kubectl get pods


List pods with additional details:


kubectl get pods -o wide


Describe a pod:


kubectl describe pod <pod-name>


Delete a pod:


kubectl delete pod <pod-name>


View pod logs:


kubectl logs <pod-name>


Execute commands inside a pod:


kubectl exec -it <pod-name> -- /bin/bash


---

# 3. Deployment Commands

List deployments:


kubectl get deployments


Create deployment:


kubectl create deployment nginx --image=nginx


Update image:


kubectl set image deployment/nginx nginx=nginx:latest


Scale deployment:


kubectl scale deployment nginx --replicas=5


Check rollout status:


kubectl rollout status deployment nginx


Rollback deployment:


kubectl rollout undo deployment nginx


---

# 4. ReplicaSet Commands

List ReplicaSets:


kubectl get rs


Describe ReplicaSet:


kubectl describe rs <replicaset-name>


Scale ReplicaSet:


kubectl scale rs <replicaset-name> --replicas=4


---

# 5. Service Commands

List services:


kubectl get services


Describe service:


kubectl describe service <service-name>


Expose deployment as service:


kubectl expose deployment nginx --port=80 --type=NodePort


---

# 6. Namespace Commands

List namespaces:


kubectl get namespaces


Create namespace:


kubectl create namespace dev


Run command in specific namespace:


kubectl get pods -n dev


Delete namespace:


kubectl delete namespace dev


---

# 7. Configuration Commands

Apply configuration file:


kubectl apply -f file.yaml


Create resource from YAML:


kubectl create -f file.yaml


Delete resource from YAML:


kubectl delete -f file.yaml


View resource YAML:


kubectl get pod <pod-name> -o yaml


---

# 8. Debugging Commands

Check events in cluster:


kubectl get events


Watch resources continuously:


kubectl get pods -w


Check resource usage:


kubectl top pods
kubectl top nodes


---

# 9. Config and Context Commands

View current context:


kubectl config current-context


List contexts:


kubectl config get-contexts


Switch context:


kubectl config use-context <context-name>


---

# 10. Resource Exploration Commands

List all resources:


kubectl get all


Explain Kubernetes resource:


kubectl explain pod


Explain specific field:


kubectl explain deployment.spec


---

# 11. Port Forwarding

Access service locally:


kubectl port-forward pod/<pod-name> 8080:80


Example:


kubectl port-forward deployment/nginx 8080:80


Access application via:


http://localhost:8080


---

# 12. Copy Files to and from Pods

Copy file from local machine to pod:


kubectl cp file.txt <pod-name>:/tmp/


Copy file from pod to local machine:


kubectl cp <pod-name>:/tmp/file.txt .


---

# 13. Label Management

Add label to resource:


kubectl label pod <pod-name> env=production


View labels:


kubectl get pods --show-labels


---

# 14. Annotating Resources

Add annotation:


kubectl annotate pod <pod-name> description="test pod"


---

# 15. Delete Resources

Delete pod:


kubectl delete pod <pod-name>


Delete deployment:


kubectl delete deployment <deployment-name>


Delete service:


kubectl delete service <service-name>


---

# 16. Important Shortcuts


kubectl get pods -A
kubectl get pods -o wide
kubectl get pods --watch
kubectl get svc
kubectl get deploy
kubectl get rs


---

# 17. Common kubectl Aliases (Recommended)

Many DevOps engineers use:


alias k=kubectl


Then commands become shorter:


k get pods
k get svc
k describe pod nginx


---

# Conclusion

kubectl is the primary interface for interacting with Kubernetes clusters.

Mastering kubectl helps with:

- Application deployment
- Cluster debugging
- Resource monitoring
- DevOps automation

Daily Kubernetes work heavily relies on kubectl commands.
