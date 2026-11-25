# Day 52: Roll Back a Deployment

| | |
|---|---|
| **Day** | 52 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Revert `nginx-deployment` to its previous revision.

## ✅ Solution (copy and paste)

```bash
kubectl rollout history deployment/nginx-deployment
kubectl rollout undo deployment/nginx-deployment
kubectl rollout status deployment/nginx-deployment
kubectl get pods
kubectl describe deployment nginx-deployment | grep -i image          # previous image back
```

## 🧪 Verification

```bash
kubectl rollout status deployment/nginx-deployment
kubectl describe deployment nginx-deployment
```
The previous image is back and the rollout reports success.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `no rollout history found` | Only one revision exists. Update first. |
| Same image after undo | `kubectl rollout history`, then use `--to-revision=<N>`. |
| Pods still terminating | Wait for `kubectl rollout status`. |

## 💡 Notes

to go to a specific revision: `kubectl rollout undo deployment/nginx-deployment --to-revision=<N>`.

## 📸 Screenshot

![Day 52 verification](./screenshots/day52.png)

---
[⬅️ Day 51](../DAY51/task-51-rolling-update.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 53 ➡️](../DAY53/task-53-fix-an-nginx-php-fpm-pod.md)
