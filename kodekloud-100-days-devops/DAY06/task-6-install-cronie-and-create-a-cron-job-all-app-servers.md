# Day 06: Install cronie and Create a Cron Job (all app servers)

| | |
|---|---|
| **Day** | 6 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On all app servers install cronie, start crond, and add `*/5 * * * * echo hello > /tmp/cron_text` for root.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# Repeat on stapp01, stapp02, stapp03
ssh <SUDO_USER>@<STAPP>
sudo su -

yum install -y cronie
systemctl enable --now crond

# Add the entry ONCE (keeps existing entries)
(crontab -l 2>/dev/null; echo "*/5 * * * * echo hello > /tmp/cron_text") | crontab -
```

## 🧪 Verification

```bash
systemctl status crond               # active (running)
crontab -l                           # entry listed exactly once
sleep 300; cat /tmp/cron_text        # prints: hello
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `crontab: command not found` | `yum install -y cronie`. |
| The job never runs | `systemctl enable --now crond`, then `systemctl status crond`. |
| The entry appears twice | The add command ran twice. Remove one line with `crontab -e`. |

## 💡 Notes

running the add-line twice creates a duplicate entry. If so, fix it with `crontab -e`.

## 📸 Screenshot

![Day 06 verification](./screenshots/day06.png)

---
[⬅️ Day 05](../DAY05/task-5-install-selinux-packages-and-disable-it-permanently.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 07 ➡️](../DAY07/task-7-passwordless-ssh-from-thor-jump-host-to-all-app-servers.md)
