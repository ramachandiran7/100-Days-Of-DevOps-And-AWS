# Day 60: PV + PVC + Pod + NodePort Service

| | |
|---|---|
| **Day** | 60 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Create PV `pv-nautilus`, PVC `pvc-nautilus`, pod `pod-nautilus` and NodePort service `web-nautilus` so the web app serves its content from persistent storage.

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-nautilus
spec:
  storageClassName: manual
  capacity:
    storage: 3Gi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/devops
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pvc-nautilus
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 1Gi
apiVersion: v1
kind: Pod
metadata:
  name: pod-nautilus
  labels:
    app: web-nautilus
spec:
  volumes:
    - name: storage
      persistentVolumeClaim:
        claimName: pvc-nautilus
  containers:
    - name: container-nautilus
      image: httpd:latest
      volumeMounts:
        - name: storage
          mountPath: /usr/local/apache2/htdocs
apiVersion: v1
kind: Service
metadata:
  name: web-nautilus
spec:
  type: NodePort
  selector:
    app: web-nautilus
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```
```bash
kubectl apply -f web-app.yaml
kubectl get pv,pvc,pod,svc              # PVC STATUS = Bound
```

## 🧪 Verification

```bash
kubectl get pv,pvc,pod,svc
```
The PVC shows `Bound`, the pod is `Running`, and the app opens from the lab's website button.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| PVC stays `Pending` | StorageClass or size does not match the PV. |
| Pod `Pending` | The PVC is not bound yet. `kubectl describe pvc`. |
| Service unreachable | Pod labels must match the service selector. |

## 📸 Screenshot

![Day 60 verification](./screenshots/day60.png)

---
[⬅️ Day 59](../DAY59/task-59-fix-a-redis-deployment.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 61 ➡️](../DAY61/task-61-init-container.md)
