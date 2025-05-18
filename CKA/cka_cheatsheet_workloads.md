## ⚙️ Workloads & Scheduling

### Understand Application Deployments (Rolling Updates & Rollbacks)

```bash
kubectl create deployment web --image=nginx             # Create a deployment
kubectl set image deployment/web nginx=nginx:1.25        # Trigger rolling update
kubectl rollout status deployment/web                    # Watch rollout progress
kubectl rollout history deployment/web                   # View rollout history
kubectl rollout undo deployment/web                      # Roll back to previous version
```

### Use ConfigMaps and Secrets to Configure Applications

```bash
kubectl create configmap app-config --from-literal=MODE=prod         # ConfigMap from literal
kubectl create secret generic app-secret --from-literal=DB_PASS=123   # Secret from literal
kubectl describe configmap app-config                                 # View configmap
kubectl get secret app-secret -o yaml                                 # View secret
```

YAML Snippet to inject into a Pod:

```yaml
envFrom:
  - configMapRef:
      name: app-config
  - secretRef:
      name: app-secret
```

### Configure Workload Autoscaling

```bash
kubectl autoscale deployment web --min=2 --max=5 --cpu-percent=70     # Create HPA
kubectl get hpa                                                       # Check autoscaler
```

### Create Robust, Self-Healing Deployments

```yaml
livenessProbe:
  httpGet:
    path: /healthz
    port: 8080
  initialDelaySeconds: 10
  periodSeconds: 5

readinessProbe:
  exec:
    command:
    - cat
    - /tmp/ready

restartPolicy: Always     # Ensures pod restart if it fails (default)
```

### Configure Pod Admission & Scheduling

**Resource Limits:**

```yaml
resources:
  requests:
    cpu: "100m"
    memory: "128Mi"
  limits:
    cpu: "500m"
    memory: "256Mi"
```

**Node Affinity:**

```yaml
affinity:
  nodeAffinity:
    requiredDuringSchedulingIgnoredDuringExecution:
      nodeSelectorTerms:
      - matchExpressions:
        - key: disktype
          operator: In
          values:
          - ssd
```

**Tolerations and Taints:**

```yaml
tolerations:
- key: "key1"
  operator: "Equal"
  value: "value1"
  effect: "NoSchedule"
```

```bash
kubectl taint nodes <node> key1=value1:NoSchedule    # Prevent pods without matching toleration
```

### Bonus Commands

```bash
kubectl explain pod.spec.affinity                    # Show syntax for affinity
kubectl describe pod <pod>                           # Debug scheduling issues
kubectl get deployment web -o yaml                   # Full deployment config
```
