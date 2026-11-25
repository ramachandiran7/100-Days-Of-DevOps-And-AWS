# Day 44: Docker Compose for httpd with a Bind Mount

| | |
|---|---|
| **Day** | 44 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

`/opt/docker/docker-compose.yml`, image `httpd:latest`, container name `<NAME>`, host `<HOST_PORT>` to container 80, mount `/opt/itadmin` to `/usr/local/apache2/htdocs`. Do not change `/opt/itadmin`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<HOST_PORT>` `<NAME>`

## ✅ Solution (copy and paste)

```bash
ssh steve@stapp02
sudo su -
vi /opt/docker/docker-compose.yml
```
```yaml
services:
  httpd:
    image: httpd:latest
    container_name: httpd
    ports:
      - "6400:80"
    volumes:
      - /opt/itadmin:/usr/local/apache2/htdocs
```
```bash
docker compose -f /opt/docker/docker-compose.yml up -d
```

## 🧪 Verification

```bash
docker ps
curl http://localhost:6400              # shows /opt/itadmin content
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Page shows the default `It works!` | The bind mount path is wrong. Check `/opt/itadmin`. |
| Port already in use | `docker ps` and stop the old container. |
| `docker compose` not found | Older installs use `docker-compose`. |

## 💡 Notes

older Compose may need `version: "3"` at the top and `docker-compose` (with a hyphen).

## 📸 Screenshot

![Day 44 verification](./screenshots/day44.png)

---
[⬅️ Day 43](../DAY43/task-43-container-with-port-mapping.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 45 ➡️](../DAY45/task-45-fix-a-broken-dockerfile.md)
