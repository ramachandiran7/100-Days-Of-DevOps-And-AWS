# Day 03: Disable Direct Root SSH Login (all app servers)

| | |
|---|---|
| **Day** | 3 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Disable root SSH login on ALL app servers. Repeat on stapp01, stapp02, stapp03.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# Repeat this block for each server
ssh <SUDO_USER>@<STAPP>
sudo su -

# Back up, then change the setting
cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak
sed -i 's/^#\?PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config

# Check syntax BEFORE restarting (a typo can lock you out)
sshd -t

systemctl restart sshd
grep -i '^PermitRootLogin' /etc/ssh/sshd_config
exit; exit
```

## 🧪 Verification

**from jump host:**

```bash
ssh root@stapp01                     # must say: Permission denied
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `sshd` fails to restart | Typo in the config. `sshd -t` shows the line. Restore with `cp /etc/ssh/sshd_config.bak /etc/ssh/sshd_config`. |
| Root can still log in | Two `PermitRootLogin` lines, or sshd was not restarted. Keep one line `PermitRootLogin no`, then `systemctl restart sshd`. |
| Only one server fixed | The task says all app servers. Repeat on stapp01, stapp02 and stapp03. |

## 💡 Notes

if `grep` shows two PermitRootLogin lines, edit the file with `vi` so only `PermitRootLogin no` is active.

## 📸 Screenshot

![Day 03 verification](./screenshots/day03.png)

---
[⬅️ Day 02](../DAY02/task-2-create-a-temporary-user-with-an-expiry-date.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 04 ➡️](../DAY04/task-4-give-a-script-executable-permission.md)
