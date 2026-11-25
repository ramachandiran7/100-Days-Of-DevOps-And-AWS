# Day 42: Create a Docker macvlan Network

| | |
|---|---|
| **Day** | 42 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

Network `<NAME>`, driver `macvlan`, subnet and ip-range `<SUBNET>`, gateway `<GATEWAY>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<GATEWAY>` `<NAME>` `<SUBNET>`

## ✅ Solution (copy and paste)

```bash
ssh steve@stapp02
sudo su -
docker network create -d macvlan \
  --subnet=<SUBNET> \
  --ip-range=<SUBNET> \
  --gateway=<GATEWAY> \
  <NAME>
```
Example: `--subnet=192.168.30.0/24 --ip-range=192.168.30.0/24 --gateway=192.168.30.1 official`

## 🧪 Verification

```bash
docker network ls | grep <NAME>
docker network inspect <NAME>           # driver macvlan, subnet, gateway correct
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Pool overlaps` | The subnet is in use. `docker network ls`, then `docker network inspect`. |
| Network already exists | `docker network rm <NAME>`, then create it again. |
| Wrong driver | Make sure `-d macvlan` is set. |

## 💡 Notes

if Docker asks for a parent interface, add `-o parent=eth0`.

## 📸 Screenshot

![Day 42 verification](./screenshots/day42.png)

---
[⬅️ Day 41](../DAY41/task-41-write-a-dockerfile-ubuntu-24-04-apache-on-a-custom-port.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 43 ➡️](../DAY43/task-43-container-with-port-mapping.md)
