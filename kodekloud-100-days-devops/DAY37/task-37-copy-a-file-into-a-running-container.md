# Day 37: Copy a File into a Running Container

| | |
|---|---|
| **Day** | 37 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

Copy `/tmp/nautilus.txt.gpg` from the Docker host to `/opt/` in container `<CONTAINER>`, unmodified.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<CONTAINER>`

## ✅ Solution (copy and paste)

```bash
ssh tony@stapp01
sudo su -
docker ps                               # confirm the container is running
docker cp /tmp/nautilus.txt.gpg <CONTAINER>:/opt/
```

## 🧪 Verification

```bash
docker exec <CONTAINER> ls -l /opt/
md5sum /tmp/nautilus.txt.gpg
docker exec <CONTAINER> md5sum /opt/nautilus.txt.gpg    # checksums match
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `No such container` | `docker ps -a` for the real name. Start it if stopped. |
| Source file not found | The file is on the Docker host. Check `ls -l /tmp/`. |
| Checksums differ | Copy again and do not edit the file. |

## 📸 Screenshot

![Day 37 verification](./screenshots/day37.png)

---
[⬅️ Day 36](../DAY36/task-36-run-an-nginx-container.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 38 ➡️](../DAY38/task-38-pull-an-image-and-re-tag-it.md)
