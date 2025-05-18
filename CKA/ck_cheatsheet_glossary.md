## 📘 CKA Keyword Glossary (Simplified)

### ☸️ Core Concepts

* **Cluster**: A set of machines (nodes) running Kubernetes, consisting of a control plane and worker nodes.
* **Node**: A physical or virtual machine in a Kubernetes cluster.
* **Pod**: The smallest deployable unit; wraps one or more containers.
* **Namespace**: A way to divide cluster resources between multiple users.
* **Container**: A lightweight, portable unit that runs applications inside Pods.

### ⚙️ Workload & Scheduling

* **Deployment**: Ensures the desired number of pods are running and updates them.
* **ReplicaSet**: Maintains a stable set of replica Pods.
* **DaemonSet**: Ensures a pod runs on all (or some) nodes.
* **StatefulSet**: Like Deployment, but for apps needing stable identity/storage.
* **Job**: A one-time task that runs to completion.
* **CronJob**: Schedules jobs to run periodically.
* **Taints**: Prevent pods from being scheduled on nodes unless they tolerate the taint.
* **Tolerations**: Allow pods to be scheduled on nodes with matching taints.
* **Node Affinity**: Rules that influence pod placement on nodes.

### 🧱 Storage

* **Persistent Volume (PV)**: A piece of storage provisioned in the cluster.
* **Persistent Volume Claim (PVC)**: A request for storage by a user.
* **StorageClass**: Describes storage "classes" like SSD, HDD, or network-based.
* **Access Modes**:

  * `ReadWriteOnce` (RWO): One node read/write
  * `ReadOnlyMany` (ROX): Many nodes read-only
  * `ReadWriteMany` (RWX): Many nodes read/write
* **Reclaim Policies**:

  * `Retain`: Keeps the PV even after PVC is deleted
  * `Delete`: Deletes PV automatically
  * `Recycle`: Deprecated, clears data and reuses

### 📡 Networking

* **Service**: Exposes a set of Pods as a network service.
* **ClusterIP**: Default, accessible within cluster only.
* **NodePort**: Exposes service on static port on each node.
* **LoadBalancer**: Creates external load balancer (usually in cloud).
* **Ingress**: Manages external access to services, usually HTTP.
* **Ingress Controller**: Implements the Ingress rules.
* **CoreDNS**: Cluster DNS service for service discovery.
* **CNI (Container Network Interface)**: Plugin that provides networking between pods.
* **NetworkPolicy**: Rules to allow/deny traffic to/from pods.

### 🔒 Security & RBAC

* **RBAC**: Role-Based Access Control, defines who can do what.
* **Role**: Set of permissions within a namespace.
* **ClusterRole**: Permissions cluster-wide.
* **RoleBinding**: Grants Role to a user or group.
* **ServiceAccount**: Provides identity for processes in pods.

### 🧩 Extensibility

* **CRI (Container Runtime Interface)**: Lets K8s talk to container runtimes like containerd or CRI-O.
* **CSI (Container Storage Interface)**: Lets K8s talk to storage providers.
* **CNI (Container Network Interface)**: Lets K8s talk to network providers.
* **CRD (Custom Resource Definition)**: Define your own resource types.
* **Operator**: A controller for managing custom resources (CRDs).

### 🛠️ Misc

* **kubeadm**: CLI to set up clusters.
* **kubelet**: Agent that runs on nodes and manages pods.
* **kube-proxy**: Manages network rules on nodes.
* **Helm**: Package manager for Kubernetes.
* **Kustomize**: Template-free way to customize YAML configs.

> 🧠 Learn the keywords well—they are the vocabulary of all exam questions and real-world debugging.
