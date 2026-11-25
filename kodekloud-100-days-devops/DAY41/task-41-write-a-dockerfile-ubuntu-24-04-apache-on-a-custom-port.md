# Day 41: Write a Dockerfile (Ubuntu 24.04 + Apache on a custom port)

| | |
|---|---|
| **Day** | 41 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

`/opt/docker/Dockerfile` (capital D) based on `ubuntu:24.04`, installs apache2, listens on `<PORT>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<PORT>`

## ✅ Solution (copy and paste)

```bash
ssh banner@stapp03
sudo su -
mkdir -p /opt/docker
vi /opt/docker/Dockerfile
```
```dockerfile
FROM ubuntu:24.04

ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get update && \
    apt-get install -y apache2 && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

# Change the listening port
RUN sed -i 's/^Listen 80$/Listen <PORT>/' /etc/apache2/ports.conf && \
    sed -i 's/<VirtualHost \*:80>/<VirtualHost *:<PORT>>/' /etc/apache2/sites-available/000-default.conf

EXPOSE <PORT>
CMD ["apache2ctl", "-D", "FOREGROUND"]
```
```bash
cd /opt/docker
docker build -t apache-ubuntu .
```

## 🧪 Verification

```bash
docker images | grep apache-ubuntu
docker run -d --name apache-test -p <PORT>:<PORT> apache-ubuntu
curl -I http://localhost:<PORT>
docker rm -f apache-test                # clean up the test
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The build asks questions or hangs | Add `ENV DEBIAN_FRONTEND=noninteractive` before `apt-get`. |
| `Dockerfile: no such file` | The name is case-sensitive: `Dockerfile` with a capital D. |
| Port did not change | The `sed` patterns did not match. Check the files inside a test container. |

## 📸 Screenshot

![Day 41 verification](./screenshots/day41.png)

---
[⬅️ Day 40](../DAY40/task-40-install-and-configure-apache-inside-a-container.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 42 ➡️](../DAY42/task-42-create-a-docker-macvlan-network.md)
