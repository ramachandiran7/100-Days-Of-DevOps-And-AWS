# Day 48: Create a Pod

| | |
|---|---|
| **Day** | 48 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Pod `pod-httpd`, image `httpd:latest`, container `httpd-container`, label `app: httpd_app`.

## ✅ Solution (copy and paste)

```yaml
# pod-httpd.yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-httpd
  labels:
    app: httpd_app
spec:
  containers:
    - name: httpd-container
      image: httpd:latest
```
```bash
kubectl apply -f pod-httpd.yaml
kubectl get pods --show-labels         # STATUS Running
```

## 🧪 Verification

```bash
kubectl get pods --show-labels
```
STATUS is `Running` and the label `app=httpd_app` is shown.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `ImagePullBackOff` | Image name typo. `kubectl describe pod pod-httpd`. |
| Cannot find the pod by label | The label must be `app: httpd_app`. |
| `error converting YAML` | Indentation. Use 2 spaces and no tabs. |

## 📸 Screenshot

![Day 48 verification](./screenshots/day48.png)

---
[⬅️ Day 47](../DAY47/task-47-dockerize-a-python-app.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 49 ➡️](../DAY49/task-49-create-a-deployment.md)
