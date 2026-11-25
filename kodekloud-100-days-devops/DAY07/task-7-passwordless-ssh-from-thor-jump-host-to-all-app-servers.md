# Day 07: Passwordless SSH from thor (jump host) to all app servers

| | |
|---|---|
| **Day** | 7 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

User `thor` on the jump host must SSH to every app server's sudo user without a password.

## ✅ Solution (copy and paste)

```bash
# On the jump host as thor
whoami                               # thor
ssh-keygen -t rsa                    # press Enter 3 times (skip if ~/.ssh/id_rsa exists)

ssh-copy-id tony@stapp01             # type "yes", then the lab password
ssh-copy-id steve@stapp02
ssh-copy-id banner@stapp03
```

## 🧪 Verification

```bash
ssh tony@stapp01 hostname            # no password prompt
ssh steve@stapp02 hostname
ssh banner@stapp03 hostname
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Still asked for a password | The key was not copied. Re-run `ssh-copy-id <user>@<server>` with the correct user for that server. |
| `Permission denied (publickey)` | On the server run `chmod 700 ~/.ssh` and `chmod 600 ~/.ssh/authorized_keys`. |
| Key made as the wrong user | Run `whoami`. On the jump host it must be `thor`. |

## 💡 Notes

each server's sudo user is different. Never generate a key on the app server for this task.

## 📸 Screenshot

![Day 07 verification](./screenshots/day07.png)

---
[⬅️ Day 06](../DAY06/task-6-install-cronie-and-create-a-cron-job-all-app-servers.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 08 ➡️](../DAY08/task-8-install-ansible-with-pip3-globally.md)
