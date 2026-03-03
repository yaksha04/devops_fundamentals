ReplicaSet sits between:

Deployment → ReplicaSet → Pods

---

# 1. What is a ReplicaSet?

A ReplicaSet:

- Ensures a fixed number of Pods are running
- Recreates Pods if they crash or are deleted
- Uses label selectors to identify Pods
- Does NOT handle rolling updates intelligently

ReplicaSet is responsible only for maintaining replica count.

---

# 2. Why ReplicaSet Exists

Pods are ephemeral.
If a Pod crashes, it is gone.

ReplicaSet continuously checks:
“Are the required number of Pods running?”

If not:
- It creates new Pods automatically.

---

# 3. Basic ReplicaSet YAML

Example:

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.25

Apply:

kubectl apply -f replicaset.yaml
4. Important Fields Explained
replicas

Number of Pods to maintain.

replicas: 3

If one Pod is deleted manually,
ReplicaSet creates a new one immediately.

selector

Defines how ReplicaSet identifies Pods.

Must match template labels exactly.

If labels mismatch:
ReplicaSet will create new Pods endlessly.

template

Defines the Pod blueprint.

This is the actual Pod configuration.

5. Testing ReplicaSet Self-Healing

Create ReplicaSet

Run:

kubectl get pods

Delete one Pod:

kubectl delete pod <pod-name>

Observe:

kubectl get pods

A new Pod will automatically be created.

That is self-healing behavior.

6. Scaling ReplicaSet

Manual scaling:

kubectl scale rs nginx-replicaset --replicas=5

Or edit YAML and re-apply.

Check:

kubectl get pods
7. ReplicaSet vs ReplicationController

ReplicaSet is the modern version.

Difference:

Feature	ReplicationController	ReplicaSet
Label selector support	Basic	Advanced
matchExpressions	❌	✅
Production use	Deprecated	Yes

ReplicaSet replaced ReplicationController.

8. Label Selectors

ReplicaSet uses:

selector:
  matchLabels:
    app: nginx

It can also use matchExpressions:

selector:
  matchExpressions:
  - key: app
    operator: In
    values:
    - nginx

This gives more flexible matching.

9. Important Behavior

⚠ ReplicaSet does NOT update Pods automatically when image changes.

If you change image in template:

Old Pods are NOT replaced automatically.

That is why Deployments exist.

10. Inspecting ReplicaSet
kubectl get rs
kubectl describe rs nginx-replicaset
kubectl get pods

Check owner:

kubectl get pods -o wide

If created by Deployment,
Owner reference will show Deployment.

11. Deleting ReplicaSet
kubectl delete rs nginx-replicaset

This deletes:

ReplicaSet

All managed Pods

12. ReplicaSet vs Deployment
Feature	ReplicaSet	Deployment
Maintains replica count	✅	✅
Rolling updates	❌	✅
Rollback	❌	✅
Version management	❌	✅
Production recommended	❌ (Direct use rare)	✅

In real production:
You rarely create ReplicaSet manually.
Deployment manages ReplicaSets for you.

13. Interview-Level Understanding

If asked:

Why don’t we use ReplicaSet directly in production?

Answer:

No rolling update capability

No rollback

No version tracking

Cannot manage multiple revisions safely

Deployment wraps ReplicaSet and provides those features.

Conclusion

ReplicaSet ensures the desired number of Pods are always running.

But it is not a complete application management solution.

In real-world DevOps:
You use Deployments.
Deployments create and manage ReplicaSets.
ReplicaSets manage Pods.
