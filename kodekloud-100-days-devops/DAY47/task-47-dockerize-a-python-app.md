# Day 47: Dockerize a Python App

| | |
|---|---|
| **Day** | 47 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

On `<APP_SERVER>` build `<IMAGE>` from a Dockerfile in `/python_app` (deps in `/python_app/src/requirements.txt`, expose `<APP_PORT>`, run `server.py`), then run it.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_PORT>` `<APP_SERVER>` `<CONTAINER>` `<HOST_PORT>` `<IMAGE>`

## ✅ Solution (copy and paste)

```bash
ssh banner@stapp03
sudo su -
cd /python_app
ls -R
cat src/requirements.txt

vi Dockerfile
```
```dockerfile
FROM python:3.11-slim
WORKDIR /app
COPY src/requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt
COPY src/ .
EXPOSE <APP_PORT>
CMD ["python", "server.py"]
```
```bash
docker build -t <IMAGE> .                # e.g. nautilus/python-app
docker run -d --name <CONTAINER> -p <HOST_PORT>:<APP_PORT> <IMAGE>
```

## 🧪 Verification

```bash
docker ps
curl http://localhost:<HOST_PORT>
docker logs <CONTAINER>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `ModuleNotFoundError` | `requirements.txt` was not installed. Check the `COPY` and `pip install` lines. |
| `server.py` not found | Adjust `COPY` to where `server.py` lives. |
| curl fails | Check `-p <HOST_PORT>:<APP_PORT>` and `docker logs`. |

## 💡 Notes

if `server.py` is not under `src/`, adjust the `COPY`. Use the container name and host port from the task.

## 📸 Screenshot

![Day 47 verification](./screenshots/day47.png)

---
[⬅️ Day 46](../DAY46/task-46-docker-compose-multi-service-stack-php-mariadb.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 48 ➡️](../DAY48/task-48-create-a-pod.md)
