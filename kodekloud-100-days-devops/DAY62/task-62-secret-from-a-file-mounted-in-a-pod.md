# Day 62: Secret from a File Mounted in a Pod

| | |
|---|---|
| **Day** | 62 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Secret `official` from `/opt/official.txt`; pod `secret-devops` mounting it.

## ✅ Solution (copy and paste)

```bash
kubectl create secret generic official --from-file=/opt/official.txt
kubectl get secret official
```
```yaml
apiVersion: v1
kind: Pod
metadata:
  name: secret-devops
spec:
  volumes:
    - name: secret-volume
      secret:
        secretName: official
  containers:
    - name: secret-container-devops
      image: debian:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: secret-volume
          mountPath: /opt/demo           # path from your task
```
```bash
kubectl apply -f secret-pod.yaml
kubectl exec secret-devops -c secret-container-devops -- cat /opt/demo/official.txt
```

## 🧪 Verification

```bash
kubectl exec secret-devops -c secret-container-devops -- cat /opt/demo/official.txt
```
The secret content is printed.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The secret key is not `official.txt` | `--from-file` uses the file name as the key. Keep the file name. |
| `secret not found` | Create the secret before the pod. |
| Mount path is empty | Check `mountPath` and `secretName`. |

## 📸 Screenshot

![Day 62 verification](./screenshots/day62.png)

---
[⬅️ Day 61](../DAY61/task-61-init-container.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 63 ➡️](../DAY63/task-63-iron-gallery-app-namespace-2-deployments-2-services.md)
