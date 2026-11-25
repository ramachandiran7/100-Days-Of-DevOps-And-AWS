# Day 73: Scheduled Job that Copies Apache Logs

| | |
|---|---|
| **Day** | 73 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Job `copy-logs` every 10 minutes: copy `/var/log/httpd/*_log` from `stapp02` to `/usr/src/sysops` on `ststor01`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NATASHA_PASSWORD>`

## ✅ Solution (copy and paste)

1. Install **SSH Credentials**, **Publish Over SSH**. Restart.
2. **Manage Jenkins > System > Publish over SSH > SSH Servers > Add**
   - Name `stapp02`, Hostname `stapp02`, Username `steve`, tick **Use password authentication**, enter the password. **Test Configuration** = Success.
3. Prep on `stapp02` (sshpass lets scp run without a prompt):
```bash
ssh steve@stapp02
sudo yum install -y epel-release && sudo yum install -y sshpass
```
4. Prep on `ststor01`: `ssh natasha@ststor01 "ls -ld /usr/src/sysops"` (must exist and be writable by natasha).
5. **New Item** > `copy-logs` > Freestyle.
6. **Build Triggers > Build periodically** > Schedule: `*/10 * * * *`
7. **Build Steps > Send files or execute commands over SSH** > SSH Server `stapp02` > **Exec command**:
```bash
sudo sshpass -p '<NATASHA_PASSWORD>' scp -o StrictHostKeyChecking=no /var/log/httpd/access_log /var/log/httpd/error_log natasha@ststor01:/usr/src/sysops/
```
8. Save > **Build Now**.

## 🧪 Verification

`ssh natasha@ststor01 "ls -l /usr/src/sysops"` shows both logs. Wait 10 minutes and the next scheduled run appears.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `sshpass: command not found` | Install it on stapp02 (EPEL). |
| Permission denied reading the logs | Use `sudo` in the exec command. |
| The schedule does not fire | Use `*/10 * * * *` under Build periodically. |

## 📸 Screenshot

![Day 73 verification](./screenshots/day73.png)

---
[⬅️ Day 72](../DAY72/task-72-parameterized-job-string-choice.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 74 ➡️](../DAY74/task-74-database-backup-job.md)
