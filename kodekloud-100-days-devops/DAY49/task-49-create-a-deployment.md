# Day 49: Create a Deployment

| | |
|---|---|
| **Day** | 49 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deployment `nginx`, image `nginx:latest` (tag explicit).

## ✅ Solution (copy and paste)

```bash
kubectl create deployment nginx --image=nginx:latest
kubectl get deployments
kubectl get pods
```
YAML alternative:
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx
          image: nginx:latest
```

## 🧪 Verification

```bash
kubectl get deployments
kubectl get pods
```
The deployment `nginx` shows READY `1/1` and its pod is `Running`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `ImagePullBackOff` | Use exactly `nginx:latest`. |
| Wrong object name | The deployment is named `nginx`. |
| `AlreadyExists` | `kubectl delete deployment nginx`, then recreate. |

## 📸 Screenshot

![Day 49 verification](./screenshots/day49.png)

---
[⬅️ Day 48](../DAY48/task-48-create-a-pod.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 50 ➡️](../DAY50/task-50-pod-with-resource-requests-and-limits.md)
