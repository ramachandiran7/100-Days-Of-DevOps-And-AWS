# Day 05: Install SELinux Packages and Disable It Permanently

| | |
|---|---|
| **Day** | 5 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Install SELinux packages and set it to disabled (no reboot needed). Ignore the live `sestatus` output.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
ssh <SUDO_USER>@<STAPP>
sudo su -

yum install -y selinux-policy selinux-policy-targeted policycoreutils policycoreutils-python-utils libselinux-utils

# Package install creates /etc/selinux/config. Set the mode:
sed -i 's/^SELINUX=.*/SELINUX=disabled/' /etc/selinux/config
```

## 🧪 Verification

```bash
grep ^SELINUX= /etc/selinux/config   # SELINUX=disabled
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `/etc/selinux/config: No such file` | Install the packages first, then edit the file. |
| `sestatus` still shows enforcing or permissive | Expected: the config applies after a reboot. Do not reboot unless the task says so. |
| `sed` changed nothing | Spacing differs. Open `vi /etc/selinux/config` and set `SELINUX=disabled` by hand. |

## 💡 Notes

the change takes effect only after a reboot. Do not reboot unless the task says so. Use `dnf` instead of `yum` if `yum` is missing.

## 📸 Screenshot

![Day 05 verification](./screenshots/day05.png)

---
[⬅️ Day 04](../DAY04/task-4-give-a-script-executable-permission.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 06 ➡️](../DAY06/task-6-install-cronie-and-create-a-cron-job-all-app-servers.md)
