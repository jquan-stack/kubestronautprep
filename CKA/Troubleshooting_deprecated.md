# main topics

    Troubleshoot clusters and nodes
    Troubleshoot cluster components
    Monitor cluster and application resource usage
    Manage and evaluate container output streams
    Troubleshoot services and networking

# 🔧Troubleshoot Clusters and Nodes

```bash
kubectl get nodes -o wide                         # View all nodes
kubectl describe node <node-name>                # Inspect node details
kubectl get events --sort-by=.metadata.creationTimestamp  # Recent events
kubectl get componentstatus                      # Check cluster health (deprecated, but still asked)
kubectl get cs                                   # Shortcut for above
kubectl logs -n kube-system <pod>                # Check logs of core components
```

# ⚙️ Troubleshoot Cluster Components

```bash
kubectl -n kube-system get pods                  # List system components
kubectl -n kube-system describe pod <pod-name>   # Describe system pod
kubectl -n kube-system logs <pod-name>           # View logs (API server, controller-manager, etc.)
kubectl get endpoints                            # Check API server endpoint
```

## 🔍 Check kubelet status (on node):

```bash
systemctl status kubelet
journalctl -u kubelet
```

# 📊 Monitor Cluster and Application Resource Usage

```bash
kubectl top nodes                                # CPU and memory usage per node
kubectl top pods --all-namespaces                # Resource usage for all pods
kubectl describe pod <pod-name>                  # Check resource requests/limits
```

# 📤 Manage and Evaluate Container Output Streams

```bash
kubectl logs <pod-name>                          # View stdout logs
kubectl logs <pod-name> -c <container-name>      # Logs from a specific container
kubectl logs -f <pod-name>                       # Follow logs (tail -f)
kubectl exec -it <pod-name> -- /bin/sh           # Shell into a container
```
## For crashlooping pods

```bash
kubectl logs <pod> --previous
```

# 🌐 Troubleshoot Services and Networking

```bash
kubectl get svc -o wide                          # View services and cluster IPs
kubectl describe svc <service-name>              # Inspect a service
kubectl get endpoints                            # Show service-to-pod mapping
kubectl get pods -o wide                         # Check pod IPs

# DNS check from within pod:
kubectl run test --image=busybox --rm -it -- /bin/sh
> nslookup <svc-name>                            # Inside the busybox pod

# Port-forward to test service:
kubectl port-forward svc/<svc-name> 8080:80
curl localhost:8080                              # Test access to service
```

# 🛠 Bonus Utilities

```bash
kubectl get all --all-namespaces                 # Overview of all resources
kubectl describe <resource> <name>               # Deep dive into any object
kubectl explain <resource>                       # See resource structure
```

# 📌 Exam Tip

    Know how to navigate /etc/kubernetes/manifests/ (static pods like kube-apiserver)

    Use kubectl edit to quickly change config (e.g., deployments, resources)

    Use -n for namespaces (e.g., kube-system, default, custom apps)

    Timebox: Use kubectl get and describe before going deep