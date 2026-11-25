# Day 64: Fix a Python Flask Deployment and Service

| | |
|---|---|
| **Day** | 64 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Image should be `poroko/flask-demo-app`; service port/targetPort `5000`; keep nodePort.

## ✅ Solution (copy and paste)

```bash
kubectl get deploy,pods,svc
kubectl describe pod <python-pod> | tail -15                 # ImagePullBackOff = wrong image

kubectl edit deployment python-deployment-devops
#   image: poroko/flask-demo-app

kubectl edit svc python-service-devops
#   port: 5000
#   targetPort: 5000
#   nodePort: 32345  (leave unchanged)

kubectl rollout status deployment/python-deployment-devops
kubectl get pods,svc
```

## 🧪 Verification

App button shows `Hello World ...`. Use the real names from `kubectl get`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `ImagePullBackOff` | Use `poroko/flask-demo-app`. |
| Service not reachable | `port` and `targetPort` must both be 5000. |
| Editing the wrong object | Take the names from `kubectl get deploy,svc`. |

## 📸 Screenshot

![Day 64 verification](./screenshots/day64.png)

---
[⬅️ Day 63](../DAY63/task-63-iron-gallery-app-namespace-2-deployments-2-services.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 65 ➡️](../DAY65/task-65-redis-with-a-configmap-and-volumes.md)
