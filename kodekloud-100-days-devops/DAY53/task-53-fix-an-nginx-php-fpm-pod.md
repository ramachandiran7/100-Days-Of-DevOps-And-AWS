# Day 53: Fix an Nginx + PHP-FPM Pod

| | |
|---|---|
| **Day** | 53 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Pod `nginx-phpfpm` with ConfigMap `nginx-config` is broken. Fix it, then copy `/home/thor/index.php` into nginx's document root.

## ✅ Solution (copy and paste)

```bash
# 1. Investigate
kubectl get pod nginx-phpfpm -o yaml > /tmp/pod.yaml
kubectl get configmap nginx-config -o yaml        # note: root /var/www/html;
grep -n -B2 -A3 mountPath /tmp/pod.yaml
```
### Typical problem
nginx-container mounts the shared volume at `/usr/share/nginx/html`, but the config says `root /var/www/html;`. The two must match.

```bash
# 2. Fix: change the nginx-container mountPath to /var/www/html
vi /tmp/pod.yaml
kubectl delete pod nginx-phpfpm
kubectl apply -f /tmp/pod.yaml
kubectl get pod nginx-phpfpm

# 3. Copy the PHP file into nginx's root
kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html/index.php -c nginx-container
```

## 🧪 Verification

click the lab's **Website** button: the PHP page shows.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `pod updates may not change fields` | Pods are immutable. Delete the pod and apply the edited YAML. |
| Blank page or 404 | The nginx-container `mountPath` must equal the `root` in the config. |
| PHP file not served | Copy it again with `kubectl cp ... -c nginx-container`. |

## 💡 Notes

most pod fields cannot be edited in place, so delete and re-apply.

## 📸 Screenshot

![Day 53 verification](./screenshots/day53.png)

---
[⬅️ Day 52](../DAY52/task-52-roll-back-a-deployment.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 54 ➡️](../DAY54/task-54-two-containers-sharing-a-volume.md)
