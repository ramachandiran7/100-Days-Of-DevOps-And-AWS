# Day 50: Pod with Resource Requests and Limits

| | |
|---|---|
| **Day** | 50 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Pod `httpd-pod`, container `httpd-container` (`httpd:latest`), requests memory 15Mi / cpu 100m, limits memory 20Mi / cpu 100m.

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: httpd-pod
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
      resources:
        requests:
          memory: "15Mi"
          cpu: "100m"
        limits:
          memory: "20Mi"
          cpu: "100m"
```
```bash
kubectl apply -f httpd-pod.yaml
kubectl describe pod httpd-pod | grep -A6 -i -E 'limits|requests'
```

## 🧪 Verification

```bash
kubectl get pod httpd-pod
kubectl describe pod httpd-pod
```
The pod is `Running` and the describe output shows the requests and limits from the task.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Pod `OOMKilled` | The limit is too low for the image. Keep the values from the task. |
| Pod `Pending` | Requests larger than node capacity. `kubectl describe pod`. |
| Field rejected | Memory units are `Mi` and CPU is `100m`. |

## 📸 Screenshot

![Day 50 verification](./screenshots/day50.png)

---
[⬅️ Day 49](../DAY49/task-49-create-a-deployment.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 51 ➡️](../DAY51/task-51-rolling-update.md)
