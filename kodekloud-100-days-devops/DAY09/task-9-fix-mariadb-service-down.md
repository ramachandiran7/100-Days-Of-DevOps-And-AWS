# Day 09: Fix MariaDB Service Down

| | |
|---|---|
| **Day** | 9 of 100 |
| **Phase** | 1 · Linux |
| **Where** | `ssh peter@stdb01`, then `sudo su -`. |

## 📌 Task

MariaDB is down on the DB server (stdb01). Find the cause and restore it.

## ✅ Solution (copy and paste)

```bash
# 1. See the failure
systemctl status mariadb
journalctl -xeu mariadb | tail -40
tail -30 /var/log/mariadb/mariadb.log

# 2. Check the usual suspects
ls -ld /var/lib/mysql /var/run/mariadb /var/log/mariadb
ls -l /var/lib/mysql | head
df -h                                 # full disk?
ss -tlnp | grep 3306                  # port already taken?

# 3. Fix what you found (most common: wrong owner / missing dir)
mkdir -p /var/lib/mysql
chown -R mysql:mysql /var/lib/mysql
chmod 755 /var/lib/mysql
chown -R mysql:mysql /var/log/mariadb /var/run/mariadb 2>/dev/null

# 4. Start and enable
systemctl start mariadb
systemctl enable mariadb
systemctl status mariadb
```

## 🧪 Verification

```bash
mysql -e "SHOW DATABASES;"
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Journal mentions permission denied on `/var/lib/mysql` | `chown -R mysql:mysql /var/lib/mysql`. |
| `Address already in use` | Run `ss -tlnp` and look for 3306. Stop whatever holds the port. |
| Missing directory or `No space left on device` | Create the directory and fix ownership. Check `df -h` for a full disk. |

## 💡 Notes

read the journal first. The fix depends on the error (permissions, missing directory, config typo in `/etc/my.cnf`, disk full).

## 📸 Screenshot

![Day 09 verification](./screenshots/day09.png)

---
[⬅️ Day 08](../DAY08/task-8-install-ansible-with-pip3-globally.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 10 ➡️](../DAY10/task-10-bash-backup-script-zip-scp-with-no-password.md)
