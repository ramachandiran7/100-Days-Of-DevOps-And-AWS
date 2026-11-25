# Day 01: Create a User with a Non-Interactive Shell

| | |
|---|---|
| **Day** | 1 of 100 |
| **Phase** | 1 · Linux |
| **Where** | the app server named in the task (App Server 2 = stapp02, user steve). |

## 📌 Task

Create user `<USER>` with a non-interactive shell on `<APP_SERVER>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<STAPP>` `<SUDO_USER>` `<USER>`

## ✅ Solution (copy and paste)

```bash
# 1. From jump host, log in to the server
ssh <SUDO_USER>@<STAPP>             # e.g. ssh steve@stapp02

# 2. Become root
sudo su -

# 3. Confirm the user does not already exist (no output = good)
grep <USER> /etc/passwd

# 4. Check which nologin path this OS uses
which nologin                        # /sbin/nologin or /usr/sbin/nologin

# 5. Create the user
useradd <USER> -s /sbin/nologin
```

## 🧪 Verification

```bash
getent passwd <USER>                 # last field must be the nologin path
id <USER>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `useradd: user already exists` | Check with `grep <USER> /etc/passwd`. If only the shell is wrong, fix it: `usermod -s /sbin/nologin <USER>`. |
| `command not found` / `Permission denied` | You are not root. Run `sudo su -` first. |
| Shell column still shows `/bin/bash` | Wrong flag or path. Check `which nologin` and re-apply with `usermod -s`. |

## 💡 Notes

a non-interactive shell stops anyone logging in as this account, which suits service/backup accounts.

## 📸 Screenshot

![Day 01 verification](./screenshots/day01.png)

---
[🏠 Home](../README.md) &nbsp;|&nbsp; [Day 02 ➡️](../DAY02/task-2-create-a-temporary-user-with-an-expiry-date.md)
