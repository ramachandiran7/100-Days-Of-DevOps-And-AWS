# Day 36: Run an Nginx Container

| | |
|---|---|
| **Day** | 36 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

On `<APP_SERVER>` create container `<NAME>` from `nginx:alpine`, running.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<NAME>`

## ✅ Solution (copy and paste)

```bash
ssh tony@stapp01
sudo su -
docker run -d --name <NAME> nginx:alpine
```

## 🧪 Verification

```bash
docker ps                               # STATUS shows "Up"
docker ps -a --filter name=<NAME>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `container name already in use` | Remove the old one with `docker rm -f <NAME>`, then run again. |
| Image pull fails | Check the tag spelling `nginx:alpine`. |
| The container exited | Read `docker logs <NAME>`. |

## 📸 Screenshot

![Day 36 verification](./screenshots/day36.png)

---
[⬅️ Day 35](../DAY35/task-35-install-docker-ce-and-the-compose-plugin.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 37 ➡️](../DAY37/task-37-copy-a-file-into-a-running-container.md)
