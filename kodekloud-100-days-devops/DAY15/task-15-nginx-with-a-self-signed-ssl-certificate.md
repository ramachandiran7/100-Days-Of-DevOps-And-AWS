# Day 15: Nginx with a Self-Signed SSL Certificate

| | |
|---|---|
| **Day** | 15 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On `<APP_SERVER>` install Nginx, use `/tmp/nautilus.crt` and `/tmp/nautilus.key`, serve `index.html` containing `Welcome!`, test with `curl -Ik https://<APP_IP>/`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_IP>` `<APP_SERVER>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
ssh <SUDO_USER>@<STAPP>
sudo su -
yum install -y nginx

# 1. Put the cert and key in a proper place
mkdir -p /etc/nginx/ssl
mv /tmp/nautilus.crt /etc/nginx/ssl/
mv /tmp/nautilus.key /etc/nginx/ssl/
chmod 600 /etc/nginx/ssl/nautilus.key

# 2. Find the document root
grep -n 'root' /etc/nginx/nginx.conf          # usually /usr/share/nginx/html

# 3. Create the page
echo "Welcome!" > /usr/share/nginx/html/index.html

# 4. SSL server block
cat > /etc/nginx/conf.d/ssl.conf << 'CONF'
server {
    listen 443 ssl;
    server_name _;
    ssl_certificate     /etc/nginx/ssl/nautilus.crt;
    ssl_certificate_key /etc/nginx/ssl/nautilus.key;
    root  /usr/share/nginx/html;
    index index.html;
}
CONF

# 5. Test the config, then start
nginx -t
systemctl enable --now nginx
systemctl restart nginx
```

## 🧪 Verification

**from jump host:**

```bash
curl -Ik https://<APP_IP>/                   # HTTP/1.1 200 OK   (-k = accept self-signed)
curl -k https://<APP_IP>/                    # Welcome!
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `nginx -t`: cannot load certificate | Wrong path or file name. `ls -l /etc/nginx/ssl/` and fix the config. |
| `Connection refused` on 443 | Not listening. `ss -tlnp` must show 443. Check the `listen 443 ssl;` line. |
| curl: certificate problem | The certificate is self-signed. Use `curl -k` (or `-Ik`). |

## 💡 Notes

get the IP with `getent hosts <STAPP>` on the jump host. `nginx -t` must say "syntax is ok".

## 📸 Screenshot

![Day 15 verification](./screenshots/day15.png)

---
[⬅️ Day 14](../DAY14/task-14-fix-apache-on-the-faulty-app-server-same-port-on-all.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 16 ➡️](../DAY16/task-16-nginx-as-a-load-balancer-lbr.md)
