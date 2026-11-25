# Day 67: Guestbook App (Redis master, Redis slave, frontend)

| | |
|---|---|
| **Day** | 67 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deploy the Guestbook app: a Redis master, Redis slaves and a PHP frontend, each exposed through its own service.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<DIGEST_FROM_TASK>`

## ✅ Solution (copy and paste)

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-master
  labels:
    app: redis-master
spec:
  replicas: 1
  selector:
    matchLabels:
      app: redis-master
  template:
    metadata:
      labels:
        app: redis-master
    spec:
      containers:
        - name: master-redis-xfusion
          image: redis
          ports:
            - containerPort: 6379
          resources:
            requests:
              cpu: 100m
              memory: 100Mi
apiVersion: v1
kind: Service
metadata:
  name: redis-master
spec:
  selector:
    app: redis-master
  ports:
    - port: 6379
      targetPort: 6379
apiVersion: apps/v1
kind: Deployment
metadata:
  name: redis-slave
  labels:
    app: redis-slave
spec:
  replicas: 2
  selector:
    matchLabels:
      app: redis-slave
  template:
    metadata:
      labels:
        app: redis-slave
    spec:
      containers:
        - name: slave-redis-xfusion
          image: gcr.io/google_samples/gb-redisslave:v3
          ports:
            - containerPort: 6379
          resources:
            requests:
              cpu: 100m
              memory: 100Mi
          env:
            - name: GET_HOSTS_FROM
              value: dns
apiVersion: v1
kind: Service
metadata:
  name: redis-slave
spec:
  selector:
    app: redis-slave
  ports:
    - port: 6379
      targetPort: 6379
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend
  labels:
    app: frontend
spec:
  replicas: 3
  selector:
    matchLabels:
      app: frontend
  template:
    metadata:
      labels:
        app: frontend
    spec:
      containers:
        - name: php-redis-xfusion
          image: gcr.io/google-samples/gb-frontend@sha256:<DIGEST_FROM_TASK>
          ports:
            - containerPort: 80
          resources:
            requests:
              cpu: 100m
              memory: 100Mi
          env:
            - name: GET_HOSTS_FROM
              value: dns
apiVersion: v1
kind: Service
metadata:
  name: frontend
spec:
  type: NodePort
  selector:
    app: frontend
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30009
```
```bash
kubectl apply -f guestbook.yaml
kubectl get deploy,pods,svc             # 1 master, 2 slaves, 3 frontends Running
```

## 🧪 Verification

App button shows the Guestbook page. Copy the frontend image digest exactly from your task.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Frontend cannot reach Redis | Service names must be `redis-master` and `redis-slave`. |
| `InvalidImageName` | Copy the image digest exactly from the task. |
| Pods `Pending` | `kubectl describe pod`. Resource requests may be too high. |

## 📸 Screenshot

![Day 67 verification](./screenshots/day67.png)

---
[⬅️ Day 66](../DAY66/task-66-mysql-with-pv-pvc-secrets-and-nodeport.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 68 ➡️](../DAY68/task-68-set-up-a-jenkins-server.md)
