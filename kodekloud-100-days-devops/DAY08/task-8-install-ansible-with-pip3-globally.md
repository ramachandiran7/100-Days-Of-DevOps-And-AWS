# Day 08: Install Ansible with pip3 (globally)

| | |
|---|---|
| **Day** | 8 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Install Ansible `<VERSION>` on the jump host using pip3 only, available to all users.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<VERSION>`

## ✅ Solution (copy and paste)

```bash
pip3 --version
sudo pip3 install ansible==<VERSION>   # e.g. 4.7.0 ; sudo = system-wide
```

## 🧪 Verification

```bash
ansible --version
which ansible                        # normally /usr/local/bin/ansible
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `pip3: command not found` | `sudo yum install -y python3-pip`. |
| `ansible: command not found` for another user | It was installed with `--user`. Reinstall with `sudo pip3 install ...` or add a symlink in `/usr/bin`. |
| Wrong version installed | Pin it: `sudo pip3 install ansible==<VERSION>`, then check `ansible --version`. |

## 💡 Notes

### If other users cannot run it
```bash
sudo ln -s /usr/local/bin/ansible /usr/bin/ansible
```
### Notes
`pip3 install --user` is NOT global. Use `sudo`.

## 📸 Screenshot

![Day 08 verification](./screenshots/day08.png)

---
[⬅️ Day 07](../DAY07/task-7-passwordless-ssh-from-thor-jump-host-to-all-app-servers.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 09 ➡️](../DAY09/task-9-fix-mariadb-service-down.md)
