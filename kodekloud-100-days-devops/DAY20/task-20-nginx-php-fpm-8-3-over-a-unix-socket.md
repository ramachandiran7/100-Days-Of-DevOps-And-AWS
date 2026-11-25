# Day 20: Nginx + PHP-FPM 8.3 over a Unix Socket

| | |
|---|---|
| **Day** | 20 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On `<APP_SERVER>`: Nginx on port `<PORT>` with root `/var/www/html`, PHP-FPM 8.3 on socket `/var/run/php-fpm/default.sock`, test `curl http://<STAPP>:<PORT>/index.php`. Do not modify `index.php` / `info.php`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
ssh <SUDO_USER>@<STAPP>
sudo su -
cat /etc/os-release                           # note the major version (8 / 9)

# 1. Install Nginx
yum install -y nginx

# 2. Install PHP 8.3 from the Remi repo (replace 9 with your OS major version)
dnf install -y epel-release
dnf install -y https://rpms.remirepo.net/enterprise/remi-release-9.rpm
dnf module reset php -y
dnf module enable php:remi-8.3 -y
dnf install -y php-fpm php-cli php-mysqlnd php-mbstring php-xml

php -v                                        # 8.3.x
```

### Configure PHP-FPM
```bash
vi /etc/php-fpm.d/www.conf
```
Set these lines (find and replace the existing ones):
```ini
user = nginx
group = nginx
listen = /var/run/php-fpm/default.sock
listen.owner = nginx
listen.group = nginx
listen.mode = 0660
```
```bash
mkdir -p /var/run/php-fpm
chown nginx:nginx /var/run/php-fpm
```

### Configure Nginx
```bash
vi /etc/nginx/nginx.conf
```
Inside the `server { ... }` block:
```nginx
    listen       <PORT>;
    listen       [::]:<PORT>;
    root         /var/www/html;
    index        index.php index.html;

    location ~ \.php$ {
        fastcgi_pass   unix:/var/run/php-fpm/default.sock;
        fastcgi_index  index.php;
        fastcgi_param  SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include        fastcgi_params;
    }
```
```bash
nginx -t
systemctl enable --now php-fpm
systemctl enable --now nginx
systemctl restart php-fpm nginx
ls -l /var/run/php-fpm/default.sock           # socket exists
```

## 🧪 Verification

**from jump host:**

```bash
curl http://<STAPP>:<PORT>/index.php
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| 502 Bad Gateway | Socket path or permissions are wrong. `/var/run/php-fpm/default.sock` must exist and be owned by nginx. |
| `File not found.` | `root` or `SCRIPT_FILENAME` is wrong in the Nginx PHP block. |
| `php-fpm` will not start | `mkdir -p /var/run/php-fpm`, then read `journalctl -xeu php-fpm`. |

## 💡 Notes

a 502 error usually means the socket path or owner/group is wrong, or php-fpm is not running. Check `journalctl -xeu php-fpm`.

## 📸 Screenshot

![Day 20 verification](./screenshots/day20.png)

---
[⬅️ Day 19](../DAY19/task-19-apache-serving-two-static-sites-on-a-custom-port.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 21 ➡️](../DAY21/task-21-create-a-bare-git-repository.md)
