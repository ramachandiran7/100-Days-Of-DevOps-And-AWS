# Day 10: Bash Backup Script (zip + scp with no password)

| | |
|---|---|
| **Day** | 10 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On App Server 1 create `ecommerce_backup.sh` that zips `/var/www/html/ecommerce` to `/backup/xfusioncorp_ecommerce.zip`, copies it to `stbkp01:/backup/`, without prompting for a password, no `sudo` inside the script.

## ✅ Solution (copy and paste)

```bash
# 1. Log in
ssh tony@stapp01

# 2. Install zip (manual, as the task says)
sudo yum install -y zip

# 3. Make sure tony can write to /backup and run from a scripts folder
ls -ld /backup
sudo chown tony:tony /backup
sudo mkdir -p /scripts && sudo chown tony:tony /scripts   # use the path from your task if given

# 4. Passwordless SSH from tony to the backup server user (clint)
ssh-keygen -t rsa                    # Enter x3
ssh-copy-id clint@stbkp01            # lab password for clint
ssh clint@stbkp01 "ls -ld /backup"   # no password prompt = success

# 5. Create the script
cat > /scripts/ecommerce_backup.sh << 'SCRIPT'
#!/bin/bash
# Zip the site
zip -rq /backup/xfusioncorp_ecommerce.zip /var/www/html/ecommerce

# Copy to the backup server (key-based, no password, no sudo)
scp /backup/xfusioncorp_ecommerce.zip clint@stbkp01:/backup/
SCRIPT

# 6. Make executable and run it as tony
chmod +x /scripts/ecommerce_backup.sh
/scripts/ecommerce_backup.sh
```

## 🧪 Verification

```bash
ls -l /backup/xfusioncorp_ecommerce.zip
ssh clint@stbkp01 "ls -l /backup/xfusioncorp_ecommerce.zip"
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `zip: command not found` | `sudo yum install -y zip`. |
| `scp` asks for a password | Key not set up. Run `ssh-copy-id clint@stbkp01` as tony on stapp01. |
| `Permission denied` writing `/backup` | `sudo chown tony:tony /backup`. Never put `sudo` inside the script. |

## 💡 Notes

if the zip step says "Permission denied" reading the site, check the folder's permissions. Do not add `sudo` to the script.

## 📸 Screenshot

![Day 10 verification](./screenshots/day10.png)

---
[⬅️ Day 09](../DAY09/task-9-fix-mariadb-service-down.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 11 ➡️](../DAY11/task-11-install-tomcat-and-deploy-root-war-on-a-custom-port.md)
