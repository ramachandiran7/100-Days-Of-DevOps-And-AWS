# Day 57: Pod with Environment Variables

| | |
|---|---|
| **Day** | 57 of 100 |
| **Phase** | 4 · Kubernetes |

## 📌 Task

Pod `print-envars-greeting`, container `print-env-container` (image `bash`), env `GREETING`, `COMPANY`, `GROUP`, prints them.

## ✅ Solution (copy and paste)

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: print-envars-greeting
spec:
  restartPolicy: Never
  containers:
    - name: print-env-container
      image: bash
      command: ["/bin/sh", "-c", 'echo "$(GREETING) $(COMPANY) $(GROUP)"']
      env:
        - name: GREETING
          value: "Welcome to"
        - name: COMPANY
          value: "DevOps"
        - name: GROUP
          value: "Industries"
```
```bash
kubectl apply -f print-env.yaml
kubectl logs print-envars-greeting     # Welcome to DevOps Industries
```

## 🧪 Verification

```bash
kubectl logs print-envars-greeting
```
The three variables are printed on one line. The pod status `Completed` is normal.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `$(GREETING)` printed literally | Check the `env` names and use the exact `$(VAR)` syntax. |
| Pod shows `Completed` | Normal for a one-shot pod. Read `kubectl logs`. |
| `CrashLoopBackOff` | Set `restartPolicy: Never`. |

## 💡 Notes

use the exact env values from your task. The pod ends in `Completed`; that is normal.

## 📸 Screenshot

![Day 57 verification](./screenshots/day57.png)

---
[⬅️ Day 56](../DAY56/task-56-deployment-nodeport-service.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 58 ➡️](../DAY58/task-58-grafana-deployment-nodeport.md)
