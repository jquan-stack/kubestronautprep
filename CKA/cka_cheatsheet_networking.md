## 🌐 Services & Networking

### Pod-to-Pod Connectivity

* Handled by CNI plugin (e.g., Flannel, Calico)

```bash
kubectl exec -it <pod1> -- ping <pod2-ip>                # Test connectivity
kubectl get pods -o wide                                # View Pod IPs
```

### Network Policies

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-frontend
spec:
  podSelector:
    matchLabels:
      role: db
  ingress:
  - from:
    - podSelector:
        matchLabels:
          role: frontend
```

```bash
kubectl apply -f netpol.yaml                            # Apply NetworkPolicy
```

### Service Types (ClusterIP, NodePort, LoadBalancer)

```bash
kubectl expose deployment web --port=80 --target-port=80 --type=ClusterIP       # Internal only
kubectl expose deployment web --type=NodePort                                   # Exposes on <NodeIP>:<Port>
kubectl expose deployment web --type=LoadBalancer                               # For cloud only (ELB)
kubectl get svc                                                                  # See service IP and port
```

### Gateway API and Ingress

```bash
kubectl apply -f https://github.com/kubernetes-sigs/gateway-api/releases/latest/download/standard-install.yaml  # Install Gateway API CRDs
kubectl get gatewayclass                                                                                         # View GatewayClasses
```

### Ingress Controller and Resources

```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.9.1/deploy/static/provider/baremetal/deploy.yaml   # Install NGINX Ingress Controller
```

```yaml
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: test-ingress
spec:
  rules:
  - host: myapp.example.com
    http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: web
            port:
              number: 80
```

```bash
kubectl apply -f ingress.yaml                  # Deploy Ingress rule
```

### CoreDNS

```bash
kubectl get pods -n kube-system -l k8s-app=kube-dns        # Check CoreDNS pods
kubectl exec -it <pod> -- nslookup <svc-name>              # Test DNS resolution
```
