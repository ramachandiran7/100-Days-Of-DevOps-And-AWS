# Day 16: Nginx as a Load Balancer (LBR)

| | |
|---|---|
| **Day** | 16 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On `stlb01` install Nginx and load balance across all three app servers in `/etc/nginx/nginx.conf`. Do not change Apache's port.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APACHE_PORT>`

## ✅ Solution (copy and paste)

```bash
# 1. Find Apache's port and make sure Apache runs on every app server
ssh tony@stapp01 'grep ^Listen /etc/httpd/conf/httpd.conf; systemctl is-active httpd'
ssh steve@stapp02 'grep ^Listen /etc/httpd/conf/httpd.conf; systemctl is-active httpd'
ssh banner@stapp03 'grep ^Listen /etc/httpd/conf/httpd.conf; systemctl is-active httpd'
# Start any that are inactive:  sudo systemctl enable --now httpd

# 2. On the LBR
ssh loki@stlb01
sudo su -
yum install -y nginx
vi /etc/nginx/nginx.conf
```

### Inside the `http { ... }` block add the upstream, and point the existing `server` block at it
```nginx
http {
    upstream app_servers {
        server stapp01:<APACHE_PORT>;
        server stapp02:<APACHE_PORT>;
        server stapp03:<APACHE_PORT>;
    }

    server {
        listen 80;
        server_name stlb01;

        location / {
            proxy_pass http://app_servers;
        }
    }
}
```
Remove or replace the default `location / { }` so there is only one.

```bash
nginx -t
systemctl enable --now nginx
systemctl restart nginx
```

## 🧪 Verification

`curl http://stlb01` from the jump host, and click the lab's **StaticApp** button.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| 502 Bad Gateway | An app server's Apache is down or the port is wrong. Check `systemctl is-active httpd` and the Listen port on each server. |
| Default Nginx page still shows | The default `server` block was not changed. Make `location /` use `proxy_pass`. |
| `nginx -t`: upstream directive not allowed here | `upstream` must be inside the `http { }` block. |

## 📸 Screenshot

![Day 16 verification](./screenshots/day16.png)

---
[⬅️ Day 15](../DAY15/task-15-nginx-with-a-self-signed-ssl-certificate.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 17 ➡️](../DAY17/task-17-postgresql-user-and-database.md)
