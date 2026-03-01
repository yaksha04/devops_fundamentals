# Minikube Setup Guide (Local Kubernetes Cluster)

Minikube allows you to run a single-node Kubernetes cluster locally for learning and development purposes.

It is ideal for:
- Beginners learning Kubernetes
- Testing deployments locally
- Practicing kubectl commands
- CI/CD experimentation

---

# 1. System Requirements

Minimum:

- 2 CPU cores
- 4 GB RAM
- 20 GB free disk space
- Virtualization enabled (BIOS/UEFI)

Check virtualization (Linux):


egrep -c '(vmx|svm)' /proc/cpuinfo


If output is `0`, virtualization is not enabled.

---

# 2. Install kubectl

Kubectl is the Kubernetes CLI tool used to interact with the cluster.

### Linux


curl -LO "https://dl.k8s.io/release/$(curl
 -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl
"
chmod +x kubectl
sudo mv kubectl /usr/local/bin/


Verify:


kubectl version --client


---

# 3. Install Minikube

### Linux


curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64

sudo install minikube-linux-amd64 /usr/local/bin/minikube


Verify:


minikube version


---

# 4. Install a Container Runtime (Driver)

Minikube needs a driver to create the cluster.

Recommended:

- Docker (most common)
- VirtualBox
- KVM

If Docker is installed:


docker --version


---

# 5. Start Minikube Cluster

Basic start:


minikube start


With specific driver:


minikube start --driver=docker


With resource allocation:


minikube start --cpus=2 --memory=4096


---

# 6. Verify Cluster

Check nodes:


kubectl get nodes


Expected output:


NAME STATUS ROLES AGE VERSION
minikube Ready control-plane 2m v1.xx.x


Check system pods:


kubectl get pods -A


---

# 7. Enable Dashboard (Optional)


minikube dashboard


This opens Kubernetes web UI in browser.

---

# 8. Basic Test Deployment

Create test deployment:


kubectl create deployment nginx --image=nginx


Expose it:


kubectl expose deployment nginx --type=NodePort --port=80


Get service:


kubectl get service


Access in browser:


minikube service nginx


---

# 9. Stop and Delete Cluster

Stop cluster:


minikube stop


Delete cluster:


minikube delete


---

# 10. Common Troubleshooting

### If cluster fails to start

Try:


minikube delete
minikube start --driver=docker


### If kubectl cannot connect

Check context:


kubectl config current-context


Set context:


kubectl config use-context minikube


---

# 11. Important Minikube Commands


minikube status
minikube ip
minikube logs
minikube ssh
minikube addons list
