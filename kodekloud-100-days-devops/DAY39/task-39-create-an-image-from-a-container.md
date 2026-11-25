# Day 39: Create an Image from a Container

| | |
|---|---|
| **Day** | 39 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

Commit running container `<CONTAINER>` to a new image `<NAME>:<TAG>` (e.g. `beta:datacenter`).

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<CONTAINER>` `<NAME>` `<TAG>`

## ✅ Solution (copy and paste)

```bash
ssh tony@stapp01
sudo su -
docker commit <CONTAINER> <NAME>:<TAG>
```

## 🧪 Verification

```bash
docker images | grep <NAME>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `No such container` | `docker ps -a` for the exact name. |
| The image is not listed | Check the `<NAME>:<TAG>` format and run `docker images`. |
| Wrong image name | The task sets the name and tag. Match them exactly. |

## 📸 Screenshot

![Day 39 verification](./screenshots/day39.png)

---
[⬅️ Day 38](../DAY38/task-38-pull-an-image-and-re-tag-it.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 40 ➡️](../DAY40/task-40-install-and-configure-apache-inside-a-container.md)
