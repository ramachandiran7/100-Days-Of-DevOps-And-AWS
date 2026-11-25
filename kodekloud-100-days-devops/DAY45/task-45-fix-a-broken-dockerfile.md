# Day 45: Fix a Broken Dockerfile

| | |
|---|---|
| **Day** | 45 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

The Dockerfile in `/opt/docker` fails to build. Fix it without changing the base image or data files, then build.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<TAG>`

## ✅ Solution (copy and paste)

```bash
ssh steve@stapp02
sudo su -
cd /opt/docker
ls -R                                    # what files actually exist?
cat Dockerfile
docker build -t test-image . 2>&1 | tail -20     # READ the error
```

### Fix checklist (do whichever the error says)
```text
1. COPY path wrong      -> make it match `ls -R`   (e.g. COPY html/index.html ..., COPY certs/server.crt ...)
2. sed with "/" in text -> escape slashes:  modules\/mod_ssl.so   (or use a different delimiter)
3. Missing space / bad RUN syntax
4. Wrong config path    -> httpd image uses /usr/local/apache2/conf/httpd.conf
5. File referenced but not in the build folder
```
```bash
vi Dockerfile                            # apply the fix
docker build -t <TAG> .
```

## 🧪 Verification

```bash
docker images | grep <TAG>               # build succeeded
docker run -d --name t1 -p 8080:8080 <TAG>; curl -I http://localhost:8080; docker rm -f t1
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Build stops at `COPY` | The path does not exist. Compare with `ls -R`. |
| `sed` error with slashes | Escape `/` as `\/` or use another delimiter. |
| The build works but the container exits | `docker logs <ID>` shows the error. |

## 💡 Notes

change only what is broken, keep `FROM` as it is.

## 📸 Screenshot

![Day 45 verification](./screenshots/day45.png)

---
[⬅️ Day 44](../DAY44/task-44-docker-compose-for-httpd-with-a-bind-mount.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 46 ➡️](../DAY46/task-46-docker-compose-multi-service-stack-php-mariadb.md)
