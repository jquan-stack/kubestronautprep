## 📦 Storage

### Implement Storage Classes & Dynamic Volume Provisioning

```bash
kubectl get storageclass                           # View existing StorageClasses
```

```yaml
# sc-local.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: local-sc
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer
```

```bash
kubectl apply -f sc-local.yaml                     # Apply a local StorageClass
```

```yaml
# pvc.yaml
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

```bash
kubectl apply -f pvc.yaml                          # Create PVC to trigger dynamic provisioning
kubectl get pv                                     # Check if a PV was created
```

### Configure Volume Types, Access Modes & Reclaim Policies

```yaml
# pv.yaml
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
kubectl apply -f pv.yaml                           # Create a static PersistentVolume
```

Access Modes:

* `ReadWriteOnce`: One node read-write
* `ReadOnlyMany`: Multiple nodes read-only
* `ReadWriteMany`: Multiple nodes read-write

Reclaim Policies:

* `Retain`: Manual cleanup
* `Delete`: Auto-delete
* `Recycle`: Deprecated

### Manage PV and PVC

```bash
kubectl get pv                                     # List PVs
kubectl get pvc                                    # List PVCs
```

```yaml
# pvc-static.yaml
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
  volumeName: host-pv
```

```bash
kubectl apply -f pvc-static.yaml                   # Bind PVC to a static PV
kubectl delete pvc static-pvc                      # Delete PVC
kubectl get pv                                     # PV will show Released status
kubectl delete pv host-pv                          # Clean up PV manually
```
