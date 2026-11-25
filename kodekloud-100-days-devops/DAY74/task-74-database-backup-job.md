# Day 74: Database Backup Job

| | |
|---|---|
| **Day** | 74 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Job `database-backup` every 10 minutes: `mysqldump` of `<DB_NAME>` on `stdb01`, named `db_$(date +%F).sql`, copied to `/home/clint/db_backups` on `stbkp01`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<CLINT_PASSWORD>` `<DB_NAME>` `<DB_PASS>` `<DB_USER>`

## ✅ Solution (copy and paste)

1. Install **Publish Over SSH**; add an SSH server `stdb01` (user from the lab page) under **Manage Jenkins > System > Publish over SSH**.
2. Prep on `stdb01`: `sudo yum install -y epel-release sshpass` (and `mysql` client if missing).
3. **New Item** > `database-backup` > Freestyle.
4. **Build Triggers > Build periodically**: `*/10 * * * *`
5. **Build Steps > Send files or execute commands over SSH** > server `stdb01` > **Exec command**:
```bash
mkdir -p /tmp/db-backup
mysqldump -u <DB_USER> -p'<DB_PASS>' <DB_NAME> > /tmp/db-backup/db_$(date +%F).sql
sshpass -p '<CLINT_PASSWORD>' scp -o StrictHostKeyChecking=no /tmp/db-backup/db_$(date +%F).sql clint@stbkp01:/home/clint/db_backups/
rm -f /tmp/db-backup/db_$(date +%F).sql
```
6. Save > **Build Now**.

## 🧪 Verification

`ssh clint@stbkp01 "ls -l /home/clint/db_backups"` shows `db_YYYY-MM-DD.sql`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Access denied` in mysqldump | Wrong DB user or password. |
| `scp` fails | The destination directory must exist on stbkp01. |
| Wrong file name | Use `db_$(date +%F).sql`. |

## 📸 Screenshot

![Day 74 verification](./screenshots/day74.png)

---
[⬅️ Day 73](../DAY73/task-73-scheduled-job-that-copies-apache-logs.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 75 ➡️](../DAY75/task-75-add-ssh-slave-nodes.md)
