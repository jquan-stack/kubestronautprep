📦 Implement Storage Classes & Dynamic Volume Provisioning

🔧 View Existing StorageClasses

kubectl get storageclass

🧱 Create a StorageClass (e.g., using local-path)

# sc-local.yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: local-sc
provisioner: kubernetes.io/no-provisioner
volumeBindingMode: WaitForFirstConsumer


kubectl apply -f sc-local.yaml

🚀 PVC for Dynamic Provisioning (e.g., Minikube uses standard)
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

  kubectl apply -f pvc.yaml

🔍 Check dynamic PV creation
  kubectl get pv

📁 Configure Volume Types, Access Modes & Reclaim Policies
📂 Static PV Example (hostPath)
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

kubectl apply -f pv.yaml

🧾 Access Modes
Mode	Description
ReadWriteOnce	Mounted once, read-write by one node
ReadOnlyMany	Mounted many times, read-only
ReadWriteMany	Mounted many times, read-write

♻️ Reclaim Policies
Policy	Behavior when PVC is deleted
Retain	Keeps the PV for manual cleanup
Delete	Deletes the PV and associated data
Recycle	Performs basic rm -rf (deprecated)

🛠 Manage PV and PVC
🔍 View PVs and PVCs