# Day 46: Docker Compose Multi-Service Stack (PHP + MariaDB)

| | |
|---|---|
| **Day** | 46 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

`/opt/devops/docker-compose.yml` with `web` (php:apache, `php_host`) and `db` (mariadb, `mysql_host`). Deploy detached.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<COMPLEX_PASSWORD>` `<COMPLEX_ROOT_PASSWORD>` `<DB_USER>`

## ✅ Solution (copy and paste)

```bash
ssh tony@stapp01
sudo su -
mkdir -p /opt/devops
vi /opt/devops/docker-compose.yml
```
```yaml
services:
  web:
    image: php:apache
    container_name: php_host
    ports:
      - "6100:80"
    volumes:
      - /var/www/html:/var/www/html
    depends_on:
      - db

  db:
    image: mariadb:latest
    container_name: mysql_host
    ports:
      - "3306:3306"
    volumes:
      - /var/lib/mysql:/var/lib/mysql
    environment:
      MYSQL_DATABASE: database_host
      MYSQL_USER: <DB_USER>
      MYSQL_PASSWORD: <COMPLEX_PASSWORD>
      MYSQL_ROOT_PASSWORD: <COMPLEX_ROOT_PASSWORD>
```
```bash
cd /opt/devops
docker compose up -d
```

## 🧪 Verification

```bash
docker ps                                # php_host and mysql_host both Up
curl -I http://localhost:6100
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `port is already allocated` (3306 or 6100) | Stop the container that owns the port. |
| The DB container exits | An environment variable is missing or invalid. `docker logs mysql_host`. |
| Web cannot reach the DB | Use the service name `db` or the container name `mysql_host`. |

## 💡 Notes

replace ports, DB name and image tags with your task's values. Use passwords of your own.

## 📸 Screenshot

![Day 46 verification](./screenshots/day46.png)

---
[⬅️ Day 45](../DAY45/task-45-fix-a-broken-dockerfile.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 47 ➡️](../DAY47/task-47-dockerize-a-python-app.md)
