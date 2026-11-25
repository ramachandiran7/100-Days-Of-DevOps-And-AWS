# Day 04: Give a Script Executable Permission

| | |
|---|---|
| **Day** | 4 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Make `/tmp/xfusioncorp.sh` executable for everyone on `<APP_SERVER>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
ssh <SUDO_USER>@<STAPP>
ls -l /tmp/xfusioncorp.sh            # before
sudo chmod a+x /tmp/xfusioncorp.sh   # adds execute for user, group, others
ls -l /tmp/xfusioncorp.sh            # after
```

## 🧪 Verification

the permission string shows `x` three times, e.g. `-rwxr-xr-x`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Operation not permitted` | Use `sudo chmod ...`. |
| Others still cannot run the script | Only the owner bit was set. Use `chmod a+x` or `755`. |
| Changed on the wrong server | The task names the app server. Check `hostname`. |

## 💡 Notes

`chmod 755` also works. `a+x` leaves other bits untouched.

## 📸 Screenshot

![Day 04 verification](./screenshots/day04.png)

---
[⬅️ Day 03](../DAY03/task-3-disable-direct-root-ssh-login-all-app-servers.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 05 ➡️](../DAY05/task-5-install-selinux-packages-and-disable-it-permanently.md)
