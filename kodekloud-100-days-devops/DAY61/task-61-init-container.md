# Day 61: Init Container

| | |
|---|---|
| **Day** | 61 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Create deployment `ic-deploy-datacenter` with an init container that writes a message to a shared volume, and a main container that reads it.

## ✅ Solution (copy and paste)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: ic-deploy-datacenter
  labels:
    app: ic-datacenter
spec:
  replicas: 1
  selector:
    matchLabels:
      app: ic-datacenter
  template:
    metadata:
      labels:
        app: ic-datacenter
    spec:
      volumes:
        - name: ic-volume-datacenter
          emptyDir: {}
      initContainers:
        - name: ic-msg-datacenter
          image: debian:latest
          command: ["/bin/bash", "-c", "echo Init Done - Welcome to xFusionCorp Industries > /ic/beta"]
          volumeMounts:
            - name: ic-volume-datacenter
              mountPath: /ic
      containers:
        - name: ic-main-datacenter
          image: debian:latest
          command: ["/bin/bash", "-c", "while true; do cat /ic/beta; sleep 5; done"]
          volumeMounts:
            - name: ic-volume-datacenter
              mountPath: /ic
```
```bash
kubectl apply -f ic-deploy.yaml
kubectl get pods
kubectl logs -f deployment/ic-deploy-datacenter -c ic-main-datacenter
# Init Done - Welcome to xFusionCorp Industries
```

## 🧪 Verification

```bash
kubectl logs -f deployment/ic-deploy-datacenter -c ic-main-datacenter
```
The log prints the init message again and again.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Cannot read logs | Add `-c ic-main-datacenter`. |
| Pod stuck at `Init:` | `kubectl describe pod` and check the init command syntax. |
| File missing in the main container | Both containers must mount the same volume path. |

## 📸 Screenshot

![Day 61 verification](./screenshots/day61.png)

---
[⬅️ Day 60](../DAY60/task-60-pv-pvc-pod-nodeport-service.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 62 ➡️](../DAY62/task-62-secret-from-a-file-mounted-in-a-pod.md)
