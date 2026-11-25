# Day 19: Apache Serving Two Static Sites on a Custom Port

| | |
|---|---|
| **Day** | 19 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On `<APP_SERVER>` serve `/home/thor/blog` and `/home/thor/cluster` at `http://localhost:<PORT>/blog/` and `/cluster/`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# 1. FROM JUMP HOST: copy both sites
scp -r /home/thor/blog /home/thor/cluster <SUDO_USER>@<STAPP>:/tmp/

# 2. On the app server
ssh <SUDO_USER>@<STAPP>
sudo su -
yum install -y httpd
sed -i 's/^Listen .*/Listen <PORT>/' /etc/httpd/conf/httpd.conf

# 3. Put the sites under the document root, so the URL paths match
cp -r /tmp/blog    /var/www/html/blog
cp -r /tmp/cluster /var/www/html/cluster
chmod -R 755 /var/www/html/blog /var/www/html/cluster

systemctl enable --now httpd
systemctl restart httpd
```

## 🧪 Verification

**on the server:**

```bash
curl http://localhost:<PORT>/blog/
curl http://localhost:<PORT>/cluster/
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| 404 on `/blog/` | The folder is not under `/var/www/html`. Run `ls /var/www/html`. |
| 403 Forbidden | `chmod -R 755 /var/www/html/blog /var/www/html/cluster`. |
| `Connection refused` | Check the `Listen` line and that httpd is running. |

## 📸 Screenshot

![Day 19 verification](./screenshots/day19.png)

---
[⬅️ Day 18](../DAY18/task-18-lamp-stack-for-wordpress.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 20 ➡️](../DAY20/task-20-nginx-php-fpm-8-3-over-a-unix-socket.md)
