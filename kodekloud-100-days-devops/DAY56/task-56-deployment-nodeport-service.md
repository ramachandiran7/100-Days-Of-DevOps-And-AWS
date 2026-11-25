# Day 56: Deployment + NodePort Service

| | |
|---|---|
| **Day** | 56 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deployment `nginx-deployment` (3 replicas, `nginx:latest`, container `nginx-container`, label `app: nginx`) and NodePort service `nginx-service` on `<NODEPORT>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NODEPORT>`

## ✅ Solution (copy and paste)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
        - name: nginx-container
          image: nginx:latest
          ports:
            - containerPort: 80
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  type: NodePort
  selector:
    app: nginx
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30011
```
```bash
kubectl apply -f nginx.yaml
kubectl get deploy,pods,svc
```

## 🧪 Verification

lab **App** button shows the Nginx welcome page.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `nodePort` out of range | The allowed range is 30000 to 32767. |
| The service has no endpoints | The selector must match the pod labels (`app: nginx`). |
| Port already allocated | Use the task's nodePort and delete any old service. |

## 📸 Screenshot

![Day 56 verification](./screenshots/day56.png)

---
[⬅️ Day 55](../DAY55/task-55-sidecar-container-for-logs.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 57 ➡️](../DAY57/task-57-pod-with-environment-variables.md)
