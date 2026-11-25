# Day 86: Passwordless SSH for Ansible

| | |
|---|---|
| **Day** | 86 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Make `ansible stapp03 -i /home/thor/ansible/inventory -m ping` work without a password.

## ✅ Solution (copy and paste)

```bash
ssh-keygen -t rsa                       # Enter x3 (skip if a key exists)
ssh-copy-id banner@stapp03              # lab password once
ssh banner@stapp03 hostname             # no prompt
vi /home/thor/ansible/inventory
```
Inventory line without any password:
```ini
stapp03 ansible_host=<IP_OR_stapp03> ansible_user=banner
```
```bash
ansible stapp03 -i /home/thor/ansible/inventory -m ping     # SUCCESS "pong"
```

## 🧪 Verification

```bash
ansible stapp03 -i /home/thor/ansible/inventory -m ping
```
The result is `SUCCESS` with `"ping": "pong"` and no password prompt.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Still prompts for a password | Remove `ansible_ssh_pass` and re-run `ssh-copy-id`. |
| `Permission denied (publickey)` | Check `~/.ssh` permissions on the server. |
| Wrong user | The inventory user must be `banner` for stapp03. |

## 📸 Screenshot

![Day 86 verification](./screenshots/day86.png)

---
[⬅️ Day 85](../DAY85/task-85-create-a-file-with-dynamic-ownership.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 87 ➡️](../DAY87/task-87-install-a-package-on-all-app-servers.md)
