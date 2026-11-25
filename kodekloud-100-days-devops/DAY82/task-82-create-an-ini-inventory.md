# Day 82: Create an INI Inventory

| | |
|---|---|
| **Day** | 82 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

`/home/thor/playbook/inventory` with App Server 3 and the variables `ansible_host`, `ansible_user`, `ansible_ssh_pass`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<PASSWORD>`

## ✅ Solution (copy and paste)

```bash
cd /home/thor/playbook
getent hosts stapp03                              # IP, if you want it
vi inventory
```
```ini
stapp03 ansible_host=<IP_OR_stapp03> ansible_user=banner ansible_ssh_pass=<PASSWORD> ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```

## 🧪 Verification

```bash
ansible -i inventory stapp03 -m ping             # "pong"
```
If a playbook exists there: `ansible-playbook -i inventory playbook.yml`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `UNREACHABLE` | Check `ansible_host`, `ansible_user` and the password. |
| Host key error | Add `ansible_ssh_common_args='-o StrictHostKeyChecking=no'`. |
| `No inventory` warning | Pass `-i inventory`. |

## 📸 Screenshot

![Day 82 verification](./screenshots/day82.png)

---
[⬅️ Day 81](../DAY81/task-81-multistage-pipeline-deploy-test.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 83 ➡️](../DAY83/task-83-fix-the-inventory-and-create-a-playbook-create-a-file.md)
