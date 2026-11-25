# Day 63: Iron Gallery App (namespace, 2 deployments, 2 services)

| | |
|---|---|
| **Day** | 63 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deploy the Iron Gallery app in its own namespace: a gallery deployment, a MariaDB deployment, a ClusterIP service for the database and a NodePort service for the app.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<DB_USER>` `<NODEPORT>` `<ROOT_PASSWORD>` `<USER_PASSWORD>`

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: iron-namespace-datacenter
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-gallery-deployment-datacenter
  namespace: iron-namespace-datacenter
  labels:
    run: iron-gallery
spec:
  replicas: 1
  selector:
    matchLabels:
      run: iron-gallery
  template:
    metadata:
      labels:
        run: iron-gallery
    spec:
      volumes:
        - name: config
          emptyDir: {}
        - name: images
          emptyDir: {}
      containers:
        - name: iron-gallery-container-datacenter
          image: kodekloud/irongallery:2.0
          resources:
            limits:
              memory: "100Mi"
              cpu: "50m"
          volumeMounts:
            - name: config
              mountPath: /usr/share/nginx/html/data
            - name: images
              mountPath: /usr/share/nginx/html/uploads
apiVersion: apps/v1
kind: Deployment
metadata:
  name: iron-db-deployment-datacenter
  namespace: iron-namespace-datacenter
  labels:
    db: mariadb
spec:
  replicas: 1
  selector:
    matchLabels:
      db: mariadb
  template:
    metadata:
      labels:
        db: mariadb
    spec:
      volumes:
        - name: db
          emptyDir: {}
      containers:
        - name: iron-db-container-datacenter
          image: kodekloud/irondb:2.0
          env:
            - name: MYSQL_DATABASE
              value: database_web
            - name: MYSQL_ROOT_PASSWORD
              value: "<ROOT_PASSWORD>"
            - name: MYSQL_PASSWORD
              value: "<USER_PASSWORD>"
            - name: MYSQL_USER
              value: "<DB_USER>"
          volumeMounts:
            - name: db
              mountPath: /var/lib/mysql
apiVersion: v1
kind: Service
metadata:
  name: iron-db-service-datacenter
  namespace: iron-namespace-datacenter
spec:
  type: ClusterIP
  selector:
    db: mariadb
  ports:
    - protocol: TCP
      port: 3306
      targetPort: 3306
apiVersion: v1
kind: Service
metadata:
  name: iron-gallery-service-datacenter
  namespace: iron-namespace-datacenter
spec:
  type: NodePort
  selector:
    run: iron-gallery
  ports:
    - port: 80
      targetPort: 80
      nodePort: <NODEPORT>               # from your task
```
```bash
kubectl apply -f iron-gallery.yaml
kubectl get all -n iron-namespace-datacenter
```

## 🧪 Verification

lab website button shows the Iron Gallery installer page.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Resources not found | Add `-n iron-namespace-datacenter` to kubectl. |
| DB pod `CrashLoopBackOff` | Environment values missing. Read `kubectl logs`. |
| App page not reachable | The `nodePort` must match the task's value. |

## 📸 Screenshot

![Day 63 verification](./screenshots/day63.png)

---
[⬅️ Day 62](../DAY62/task-62-secret-from-a-file-mounted-in-a-pod.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 64 ➡️](../DAY64/task-64-fix-a-python-flask-deployment-and-service.md)
