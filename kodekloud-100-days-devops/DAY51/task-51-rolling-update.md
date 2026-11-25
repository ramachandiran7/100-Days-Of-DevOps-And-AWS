# Day 51: Rolling Update

| | |
|---|---|
| **Day** | 51 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Update `nginx-deployment` to `nginx:1.19`; container name `nginx-container`.

## ✅ Solution (copy and paste)

```bash
kubectl get deployment nginx-deployment -o wide                       # note container name
kubectl set image deployment/nginx-deployment nginx-container=nginx:1.19
kubectl rollout status deployment/nginx-deployment
kubectl get pods
kubectl describe deployment nginx-deployment | grep -i image
```

## 🧪 Verification

```bash
kubectl rollout status deployment/nginx-deployment
kubectl describe deployment nginx-deployment
```
The image shows `nginx:1.19` and every pod is `Running`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `unable to find container named` | Wrong container name. `kubectl get deploy nginx-deployment -o wide`. |
| Rollout stuck | `kubectl describe pods` and check the image tag exists. |
| Old image still shown | Wait for `kubectl rollout status`, then describe again. |

## 📸 Screenshot

![Day 51 verification](./screenshots/day51.png)

---
[⬅️ Day 50](../DAY50/task-50-pod-with-resource-requests-and-limits.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 52 ➡️](../DAY52/task-52-roll-back-a-deployment.md)
