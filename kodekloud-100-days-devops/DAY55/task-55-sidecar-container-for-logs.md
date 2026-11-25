# Day 55: Sidecar Container for Logs

| | |
|---|---|
| **Day** | 55 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Pod `webserver`, emptyDir `shared-logs`, nginx container + sidecar reading the logs.

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: webserver
spec:
  volumes:
    - name: shared-logs
      emptyDir: {}
  containers:
    - name: nginx-container
      image: nginx:latest
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
    - name: sidecar-container
      image: ubuntu:latest
      command: ["sh", "-c", "while true; do cat /var/log/nginx/access.log /var/log/nginx/error.log; sleep 30; done"]
      volumeMounts:
        - name: shared-logs
          mountPath: /var/log/nginx
```
```bash
kubectl apply -f webserver.yaml
kubectl get pod webserver              # READY 2/2
kubectl logs webserver -c sidecar-container
```

## 🧪 Verification

```bash
kubectl get pod webserver
kubectl logs webserver -c sidecar-container
```
READY shows `2/2` and the sidecar prints the Nginx logs.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Sidecar logs are empty | Nginx logs only after a request. Send one with `kubectl exec` and curl. |
| READY shows 1/2 | A container failed. `kubectl describe pod webserver`. |
| Wrong mount path | Both containers must mount `/var/log/nginx`. |

## 📸 Screenshot

![Day 55 verification](./screenshots/day55.png)

---
[⬅️ Day 54](../DAY54/task-54-two-containers-sharing-a-volume.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 56 ➡️](../DAY56/task-56-deployment-nodeport-service.md)
