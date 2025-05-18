# 📦 Implement Storage Classes & Dynamic Volume Provisioning

## 🔧 View Existing StorageClasses
```bash
kubectl get storageclass
```

## 🧱 Create a StorageClass (e.g., using local-path)

**sc-local.yaml**

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: local-sc
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
```

```bash
kubectl apply -f sc-local.yaml
```

## 🚀 PVC for Dynamic Provisioning (e.g., Minikube uses standard)

**pvc.yaml**

```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: dynamic-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  storageClassName: standard
```

Run the following command

```bash
kubectl apply -f pvc.yaml
```

## 🔍 Check dynamic PV creation

```bash
kubectl get pv
```

# 📁 Configure Volume Types, Access Modes & Reclaim Policies
## 📂 Static PV Example (hostPath)


**pv.yaml**

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: host-pv
spec:
  capacity:
    storage: 1Gi
  accessModes:
    - ReadWriteOnce
  persistentVolumeReclaimPolicy: Retain
  hostPath:
    path: /mnt/data
```

```bash
kubectl apply -f pv.yaml
```

## 🧾 Access Modes
| Mode          | Description                          |
| ------------- | ------------------------------------ |
| ReadWriteOnce | Mounted once, read-write by one node |
| ReadOnlyMany  | Mounted many times, read-only        |
| ReadWriteMany | Mounted many times, read-write       |

## ♻️ Reclaim Policies
| Policy  | Behavior when PVC is deleted         |
| ------- | ------------------------------------ |
| Retain  | Keeps the PV for manual cleanup      |
| Delete  | Deletes the PV and associated data   |
| Recycle | Performs basic `rm -rf` (deprecated) |


# 🛠 Manage PV and PVC

## 🔍 View PVs and PVCs

```bash
kubectl get pv
kubectl get pvc
```

## 🔄 Bind Static PV + PVC

```yaml
# pvc.yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: static-pvc
spec:
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
  volumeName: host-pv        # Bind to specific PV
```
## ❌ Delete PVC and Observe Behavior

```bash
kubectl delete pvc static-pvc
kubectl get pv               # Check PV status (e.g., Released)
```

## 🧹 Cleanup
```bash
kubectl delete pv host-pv
```

## 🔎 Bonus Troubleshooting

```bash
kubectl describe pv <pv-name>
kubectl describe pvc <pvc-name>
kubectl get events
```