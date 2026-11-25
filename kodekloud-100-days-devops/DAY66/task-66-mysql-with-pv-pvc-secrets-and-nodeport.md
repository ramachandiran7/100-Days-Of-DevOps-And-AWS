# Day 66: MySQL with PV, PVC, Secrets and NodePort

| | |
|---|---|
| **Day** | 66 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Deploy MySQL with PV and PVC storage, three Secrets for the credentials, and a NodePort service.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<DB_NAME>` `<PASS>` `<ROOT_PASS>` `<USER>`

## ✅ Solution (copy and paste)

```bash
kubectl create secret generic mysql-root-pass --from-literal=password=<ROOT_PASS>
kubectl create secret generic mysql-user-pass --from-literal=username=<USER> --from-literal=password=<PASS>
kubectl create secret generic mysql-db-url --from-literal=database=<DB_NAME>
kubectl get secrets
```
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: mysql-pv
spec:
  storageClassName: manual
  capacity:
    storage: 250Mi
  accessModes:
    - ReadWriteOnce
  hostPath:
    path: /mnt/data
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mysql-pv-claim
spec:
  storageClassName: manual
  accessModes:
    - ReadWriteOnce
  resources:
    requests:
      storage: 250Mi
apiVersion: apps/v1
kind: Deployment
metadata:
  name: mysql-deployment
  labels:
    app: mysql
spec:
  replicas: 1
  selector:
    matchLabels:
      app: mysql
  template:
    metadata:
      labels:
        app: mysql
    spec:
      volumes:
        - name: mysql-storage
          persistentVolumeClaim:
            claimName: mysql-pv-claim
      containers:
        - name: mysql-container
          image: mysql:5.7
          ports:
            - containerPort: 3306
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-root-pass
                  key: password
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  name: mysql-db-url
                  key: database
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: username
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  name: mysql-user-pass
                  key: password
          volumeMounts:
            - name: mysql-storage
              mountPath: /var/lib/mysql
apiVersion: v1
kind: Service
metadata:
  name: mysql
spec:
  type: NodePort
  selector:
    app: mysql
  ports:
    - port: 3306
      targetPort: 3306
      nodePort: 30007
```
```bash
kubectl apply -f mysql.yaml
kubectl get pv,pvc,pods,svc             # PVC Bound, pod Running
```

## 🧪 Verification

```bash
kubectl get pv,pvc,pods,svc
```
The PVC is `Bound` and the MySQL pod is `Running`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Pod `CrashLoopBackOff` | Secrets are wrong. `kubectl logs <pod>`. |
| PVC `Pending` | StorageClass `manual` must match the PV. |
| Service not reachable | NodePort 30007 must match the task. |

## 📸 Screenshot

![Day 66 verification](./screenshots/day66.png)

---
[⬅️ Day 65](../DAY65/task-65-redis-with-a-configmap-and-volumes.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 67 ➡️](../DAY67/task-67-guestbook-app-redis-master-redis-slave-frontend.md)
