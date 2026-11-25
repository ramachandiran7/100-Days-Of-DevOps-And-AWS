# Day 54: Two Containers Sharing a Volume

| | |
|---|---|
| **Day** | 54 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Pod `volume-share-nautilus`, emptyDir `volume-share`, container 1 mounts `/tmp/blog`, container 2 mounts `/tmp/games`.

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: volume-share-nautilus
spec:
  volumes:
    - name: volume-share
      emptyDir: {}
  containers:
    - name: volume-container-nautilus-1
      image: ubuntu:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/blog
    - name: volume-container-nautilus-2
      image: ubuntu:latest
      command: ["sleep", "3600"]
      volumeMounts:
        - name: volume-share
          mountPath: /tmp/games
```
```bash
kubectl apply -f volume-share.yaml
kubectl exec volume-share-nautilus -c volume-container-nautilus-1 -- sh -c 'echo "hello from 1" > /tmp/blog/blog.txt'
kubectl exec volume-share-nautilus -c volume-container-nautilus-2 -- cat /tmp/games/blog.txt
```

## 🧪 Verification

```bash
kubectl exec volume-share-nautilus -c volume-container-nautilus-2 -- cat /tmp/games/blog.txt
```
Container 2 prints the text that container 1 wrote.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| File not visible in container 2 | Both mounts must use the same volume name. |
| `container not found` | Add `-c <container-name>`. |
| Pod not Ready | `kubectl describe pod volume-share-nautilus`. |

## 📸 Screenshot

![Day 54 verification](./screenshots/day54.png)

---
[⬅️ Day 53](../DAY53/task-53-fix-an-nginx-php-fpm-pod.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 55 ➡️](../DAY55/task-55-sidecar-container-for-logs.md)
