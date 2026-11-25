# Day 59: Fix a Redis Deployment

| | |
|---|---|
| **Day** | 59 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

`redis-deployment` is down: wrong image tag (`redis:alpin`) and wrong ConfigMap name (`redis-cofig`).

## ✅ Solution (copy and paste)

```bash
kubectl get pods
kubectl describe pod <redis-pod> | tail -20       # ImagePullBackOff / ConfigMap not found
kubectl get configmap                              # real ConfigMap name

kubectl edit deployment redis-deployment
#   image: redis:alpine
#   configMap: name: redis-config

kubectl rollout status deployment/redis-deployment
kubectl get pods                                   # Running
```

## 🧪 Verification

```bash
kubectl get pods
kubectl rollout status deployment/redis-deployment
```
The Redis pod is `Running` and the rollout completes.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Pod `ImagePullBackOff` | Fix the image tag (`redis:alpine`). |
| `configmap not found` | `kubectl get configmap` and use the real name. |
| The edit was not applied | After `kubectl edit`, check `kubectl rollout status`. |

## 📸 Screenshot

![Day 59 verification](./screenshots/day59.png)

---
[⬅️ Day 58](../DAY58/task-58-grafana-deployment-nodeport.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 60 ➡️](../DAY60/task-60-pv-pvc-pod-nodeport-service.md)
