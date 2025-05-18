## 🏗 Cluster Architecture, Installation & Configuration

### RBAC - Manage Role Based Access Control

```bash
kubectl create role pod-reader --verb=get,list --resource=pods --namespace=dev   # Create Role
kubectl create rolebinding read-pods --role=pod-reader --user=devuser --namespace=dev  # Bind role
kubectl get roles,rolebindings -n dev                                                 # Check
```

### Prepare Infrastructure for kubeadm

* OS: Linux, 2+ nodes
* Disable swap: `swapoff -a`
* Enable modules:

```bash
modprobe overlay
modprobe br_netfilter
```

* Install container runtime (containerd recommended)

### Create and Manage Kubernetes Clusters Using kubeadm

```bash
kubeadm init --pod-network-cidr=10.244.0.0/16           # Initialize control plane
mkdir -p $HOME/.kube
cp /etc/kubernetes/admin.conf $HOME/.kube/config       # Setup kubeconfig
kubeadm join <IP>:6443 --token <token> --discovery-token-ca-cert-hash sha256:<hash>  # Join node
```

### Cluster Lifecycle Management

```bash
kubeadm reset                  # Reset cluster state
kubectl drain <node> --delete-local-data --force --ignore-daemonsets  # Safely drain node
kubectl delete node <node>     # Remove node
```

### Highly-Available Control Plane

* Use external etcd and HAProxy/load balancer
* Pass `--control-plane-endpoint` to `kubeadm init`

### Use Helm and Kustomize to Install Components

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami     # Add repo
helm install nginx bitnami/nginx                             # Install with Helm

kustomize build . | kubectl apply -f -                        # Apply with Kustomize
```

### Understand Extension Interfaces (CNI, CSI, CRI)

* **CNI**: Networking (e.g., Calico, Flannel)
* **CSI**: Storage (e.g., hostPath driver)
* **CRI**: Container runtime (e.g., containerd, cri-o)

### CRDs and Operators

```bash
kubectl get crd                                # List custom resource definitions
kubectl apply -f <operator-install.yaml>       # Install operator
kubectl get <custom-resource>                  # Check operator's CRs
```
