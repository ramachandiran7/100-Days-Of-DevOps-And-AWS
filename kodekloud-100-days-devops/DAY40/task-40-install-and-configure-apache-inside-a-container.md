# Day 40: Install and Configure Apache Inside a Container

| | |
|---|---|
| **Day** | 40 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

In container `<CONTAINER>` on `<APP_SERVER>`: install Apache2 (apt), listen on `<PORT>` (no IP/hostname restriction), keep Apache running and the container running.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<CONTAINER>` `<PORT>`

## ✅ Solution (copy and paste)

```bash
ssh steve@stapp02
sudo su -
docker exec -it <CONTAINER> bash
```
Inside the container:
```bash
apt update
apt install -y apache2 curl

# Listen on the new port
sed -i 's/^Listen 80$/Listen <PORT>/' /etc/apache2/ports.conf
grep -n '^Listen' /etc/apache2/ports.conf

# (If a default VirtualHost is pinned to :80, update it too)
sed -i 's/<VirtualHost \*:80>/<VirtualHost *:<PORT>>/' /etc/apache2/sites-available/000-default.conf

service apache2 start
service apache2 status
curl -I http://localhost:<PORT>
exit
```

## 🧪 Verification

**on the host:**

```bash
docker ps                               # container still Up
docker exec <CONTAINER> service apache2 status
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `apt update` fails | Run it again and check network access inside the container. |
| Apache: `Address already in use` | Port clash. Run `ss -tlnp` inside the container. |
| Apache stops when you leave | Start it with `service apache2 start` inside the container. It keeps running while the container runs. |

## 💡 Notes

containers have no systemd, so use `service apache2 start`. Never use `127.0.0.1:<PORT>` in `Listen`.

## 📸 Screenshot

![Day 40 verification](./screenshots/day40.png)

---
[⬅️ Day 39](../DAY39/task-39-create-an-image-from-a-container.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 41 ➡️](../DAY41/task-41-write-a-dockerfile-ubuntu-24-04-apache-on-a-custom-port.md)
