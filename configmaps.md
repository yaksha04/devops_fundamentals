# Kubernetes ConfigMaps and Secrets

ConfigMaps and Secrets are used to manage configuration data in Kubernetes.

They allow separation of:
- Application code
- Configuration data

This follows the best practice:
"Build once, configure everywhere"

---

# 1. Why ConfigMaps and Secrets Are Needed

Problem:

Hardcoding configuration inside application:
- Not flexible
- Not secure
- Difficult to change across environments

Example:


DB_HOST=localhost
DB_PASSWORD=123456


Solution:

- ConfigMaps → Store non-sensitive data
- Secrets → Store sensitive data

---

# 2. ConfigMap

ConfigMap stores non-sensitive configuration data.

Examples:
- Environment variables
- Config files
- Application settings

---

## Create ConfigMap

### From literal values:


kubectl create configmap app-config
--from-literal=ENV=production
--from-literal=DEBUG=false


---

### From file:


kubectl create configmap app-config --from-file=config.properties


---

## ConfigMap YAML Example

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
  ENV: production
  DEBUG: "false"

Apply:

kubectl apply -f configmap.yaml
Use ConfigMap in Pod
As environment variables:
env:
- name: ENV
  valueFrom:
    configMapKeyRef:
      name: app-config
      key: ENV
Load entire ConfigMap:
envFrom:
- configMapRef:
    name: app-config
As volume:
volumes:
- name: config-volume
  configMap:
    name: app-config

Mount:

volumeMounts:
- name: config-volume
  mountPath: /etc/config
3. Secrets

Secrets store sensitive data such as:

Passwords
API keys
Tokens
Certificates
Important Note

Secrets are:

Base64 encoded (NOT encrypted by default)
Require RBAC for access control

Do NOT assume Secrets are fully secure.

Create Secret
From literal:
kubectl create secret generic db-secret \
  --from-literal=username=admin \
  --from-literal=password=123456
Secret YAML Example
apiVersion: v1
kind: Secret
metadata:
  name: db-secret
type: Opaque
data:
  username: YWRtaW4=
  password: MTIzNDU2

(Base64 encoded values)

Encode Value
echo -n "admin" | base64
Use Secret in Pod
As environment variable:
env:
- name: DB_PASSWORD
  valueFrom:
    secretKeyRef:
      name: db-secret
      key: password
As volume:
volumes:
- name: secret-volume
  secret:
    secretName: db-secret

Mount:

volumeMounts:
- name: secret-volume
  mountPath: /etc/secret
4. ConfigMap vs Secret
Feature	ConfigMap	Secret
Data type	Non-sensitive	Sensitive
Encoding	Plain text	Base64
Security	Low	Better (with RBAC)
Use case	App config	Credentials
5. Best Practices
Never hardcode credentials in code
Use Secrets for passwords, tokens
Use ConfigMaps for environment configs
Use RBAC to restrict access
Enable encryption at rest for Secrets
Avoid committing secrets to GitHub
6. Updating ConfigMaps and Secrets

After updating:

Pods DO NOT automatically restart.

You must:

kubectl rollout restart deployment <deployment-name>
7. Inspecting ConfigMaps and Secrets

List:

kubectl get configmaps
kubectl get secrets

Describe:

kubectl describe configmap app-config
kubectl describe secret db-secret
8. Real Production Example

Example:

Application needs:

DB_HOST → ConfigMap
DB_PASSWORD → Secret

Deployment uses both:

ConfigMap for environment
Secret for credentials
9. Common Mistakes

❌ Hardcoding secrets in YAML
❌ Storing plain passwords in ConfigMap
❌ Committing secrets to Git
❌ Assuming base64 = secure

10. Interview-Level Understanding

Key points:

ConfigMaps store non-sensitive data
Secrets store sensitive data
Secrets are base64 encoded (not encrypted by default)
Used via environment variables or volumes
Pods need restart after update
Conclusion

ConfigMaps and Secrets help separate configuration from application code.

They are essential for:

Secure deployments
Flexible environments
Scalable DevOps workflows
