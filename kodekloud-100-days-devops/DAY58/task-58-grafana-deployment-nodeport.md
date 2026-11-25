# Day 58: Grafana Deployment + NodePort

| | |
|---|---|
| **Day** | 58 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deployment `grafana-deployment-nautilus` and a NodePort service on `<NODEPORT>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NODEPORT>`

## ✅ Solution (copy and paste)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: grafana-deployment-nautilus
spec:
  replicas: 1
  selector:
    matchLabels:
      app: grafana
  template:
    metadata:
      labels:
        app: grafana
    spec:
      containers:
        - name: grafana
          image: grafana/grafana:latest
          ports:
            - containerPort: 3000
apiVersion: v1
kind: Service
metadata:
  name: grafana-service-nautilus
spec:
  type: NodePort
  selector:
    app: grafana
  ports:
    - port: 3000
      targetPort: 3000
      nodePort: 32000
```
```bash
kubectl apply -f grafana.yaml
kubectl get pods,svc
```

## 🧪 Verification

the Grafana login page opens via the lab's website button.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Service not reachable | The `nodePort` must match the task. `kubectl get svc`. |
| `ImagePullBackOff` | Check the spelling of `grafana/grafana:latest`. |
| Selector mismatch | The deployment and service must share the same label. |

## 📸 Screenshot

![Day 58 verification](./screenshots/day58.png)

---
[⬅️ Day 57](../DAY57/task-57-pod-with-environment-variables.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 59 ➡️](../DAY59/task-59-fix-a-redis-deployment.md)
