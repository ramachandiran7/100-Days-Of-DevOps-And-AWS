# Day 43: Container with Port Mapping

| | |
|---|---|
| **Day** | 43 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

Container `<NAME>` from `nginx:alpine`, host port `<HOST_PORT>` to container port 80, running.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<HOST_PORT>` `<NAME>`

## ✅ Solution (copy and paste)

```bash
ssh banner@stapp03
sudo su -
docker run -d --name <NAME> -p <HOST_PORT>:80 nginx:alpine
```

## 🧪 Verification

```bash
docker ps                               # PORTS: 0.0.0.0:<HOST_PORT>->80/tcp
curl -I http://localhost:<HOST_PORT>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `port is already allocated` | Another container uses the port. `docker ps`, then stop it. |
| Name already in use | `docker rm -f <NAME>`. |
| curl fails | Wait a moment and read `docker logs <NAME>`. |

## 📸 Screenshot

![Day 43 verification](./screenshots/day43.png)

---
[⬅️ Day 42](../DAY42/task-42-create-a-docker-macvlan-network.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 44 ➡️](../DAY44/task-44-docker-compose-for-httpd-with-a-bind-mount.md)
