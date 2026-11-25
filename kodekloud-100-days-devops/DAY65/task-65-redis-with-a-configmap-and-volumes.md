# Day 65: Redis with a ConfigMap and Volumes

| | |
|---|---|
| **Day** | 65 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deploy Redis as `redis-deployment` with a ConfigMap-based config, an emptyDir data volume and a CPU request.

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: my-redis-config
data:
  redis-config: |
    maxmemory 2mb
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-deployment
  labels:
    app: redis
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis
  template:
    metadata:
      labels:
        app: redis
    spec:
      volumes:
        - name: data
          emptyDir: {}
        - name: redis-config
          configMap:
            name: my-redis-config
      containers:
        - name: redis-container
          image: redis:alpine
          ports:
            - containerPort: 6379
          resources:
            requests:
              cpu: "1"
          volumeMounts:
            - name: data
              mountPath: /redis-master-data
            - name: redis-config
              mountPath: /redis-master
```
```bash
kubectl apply -f redis.yaml
kubectl get pods                        # Running
kubectl exec deploy/redis-deployment -- ls /redis-master
```

## 🧪 Verification

```bash
kubectl get pods
kubectl exec deploy/redis-deployment -- ls /redis-master
```
The pod is `Running` and the config file is listed.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `configmap not found` | Create the ConfigMap first or keep it in the same file. |
| Pod `Pending` | The CPU request of `1` may exceed the node. Use the task's value. |
| Config not mounted | `mountPath: /redis-master`. |

## 📸 Screenshot

![Day 65 verification](./screenshots/day65.png)

---
[⬅️ Day 64](../DAY64/task-64-fix-a-python-flask-deployment-and-service.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 66 ➡️](../DAY66/task-66-mysql-with-pv-pvc-secrets-and-nodeport.md)
