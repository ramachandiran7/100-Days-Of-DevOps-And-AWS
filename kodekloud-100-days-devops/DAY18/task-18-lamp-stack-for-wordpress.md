# Day 18: LAMP Stack for WordPress

| | |
|---|---|
| **Day** | 18 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Apache + PHP on all app servers (port `<PORT>`), MariaDB on the DB server with database `<DB_NAME>` and user `<DB_USER>`. `/var/www/html` is a shared mount.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<DB_NAME>` `<DB_PASS>` `<DB_USER>` `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# A) On EACH app server (stapp01, stapp02, stapp03)
ssh <SUDO_USER>@<STAPP>
sudo su -
yum install -y httpd php php-mysqlnd php-gd php-xml php-mbstring
sed -i 's/^Listen .*/Listen <PORT>/' /etc/httpd/conf/httpd.conf
systemctl enable --now httpd
systemctl restart httpd
ss -tlnp | grep <PORT>
exit; exit

# B) On the DB server
ssh peter@stdb01
sudo su -
yum install -y mariadb-server
systemctl enable --now mariadb
mysql
```
```sql
CREATE DATABASE <DB_NAME>;
CREATE USER '<DB_USER>'@'%' IDENTIFIED BY '<DB_PASS>';
GRANT ALL PRIVILEGES ON <DB_NAME>.* TO '<DB_USER>'@'%';
FLUSH PRIVILEGES;
EXIT;
```

## 🧪 Verification

open the LBR's **App** button: it should show a database connection success message with the username.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| App page says database connection failed | The user or host is wrong. Create it as `'<DB_USER>'@'%'` and run `FLUSH PRIVILEGES;`. |
| Apache does not listen on the new port | Edit `Listen`, then `systemctl restart httpd`. |
| `Access denied for user` | Password mismatch. Re-create the user with the task's password. |

## 💡 Notes

the user host must be `'%'` (or the app servers' IPs) because connections come from other machines.

## 📸 Screenshot

![Day 18 verification](./screenshots/day18.png)

---
[⬅️ Day 17](../DAY17/task-17-postgresql-user-and-database.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 19 ➡️](../DAY19/task-19-apache-serving-two-static-sites-on-a-custom-port.md)
