# Day 02: Create a Temporary User with an Expiry Date

| | |
|---|---|
| **Day** | 2 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Create user `<USER>` (lowercase) on `<APP_SERVER>` expiring on `<YYYY-MM-DD>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<STAPP>` `<SUDO_USER>` `<USER>`

## ✅ Solution (copy and paste)

```bash
ssh <SUDO_USER>@<STAPP>
sudo su -
useradd -e <YYYY-MM-DD> <USER>       # e.g. useradd -e 2024-03-28 ravi
```

## 🧪 Verification

```bash
chage -l <USER>                      # "Account expires" must show your date
id <USER>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `invalid date` | Use the format YYYY-MM-DD, for example `2024-03-28`. |
| `chage -l` shows `Account expires: never` | `-e` was missed. Fix: `chage -E <YYYY-MM-DD> <USER>`. |
| User created on the wrong server | Check `hostname` before you start. The task names the server. |

## 💡 Notes

the date format is always YYYY-MM-DD. `-e` sets account expiry; `chage -E` can change it later.

## 📸 Screenshot

![Day 02 verification](./screenshots/day02.png)

---
[⬅️ Day 01](../DAY01/task-1-create-a-user-with-a-non-interactive-shell.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 03 ➡️](../DAY03/task-3-disable-direct-root-ssh-login-all-app-servers.md)
