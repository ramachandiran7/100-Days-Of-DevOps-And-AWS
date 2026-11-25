# Day 83: Fix the Inventory and Create a Playbook (create a file)

| | |
|---|---|
| **Day** | 83 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Point the inventory at App Server 2 and create a playbook that creates an empty `/tmp/file.txt` on it.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<PASSWORD>`

## ✅ Solution (copy and paste)

```bash
cd /home/thor/ansible                  # use the folder named in your task
cat inventory                          # fix the host, user, password, IP
vi inventory
```
```ini
stapp02 ansible_host=<IP_OR_stapp02> ansible_user=steve ansible_ssh_pass=<PASSWORD> ansible_ssh_common_args='-o StrictHostKeyChecking=no'
```
```yaml
# playbook.yml
- name: Create an empty file on App Server 2
  hosts: stapp02
  tasks:
    - name: Create /tmp/file.txt
      ansible.builtin.file:
        path: /tmp/file.txt
        state: touch
```
```bash
ansible-playbook -i inventory playbook.yml
```

## 🧪 Verification

`ansible -i inventory stapp02 -a "ls -l /tmp/file.txt"`

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Could not match supplied host pattern` | `hosts:` must match an inventory name. |
| YAML parse error | Use a 2-space indent and no tabs. |
| Module not found | Check the spelling, for example `ansible.builtin.file`. |

## 💡 Notes

### Troubleshooting a "broken" setup
check host names match the inventory, the `hosts:` line matches an inventory name, YAML indentation is 2 spaces, and the module name is spelled correctly.

## 📸 Screenshot

![Day 83 verification](./screenshots/day83.png)

---
[⬅️ Day 82](../DAY82/task-82-create-an-ini-inventory.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 84 ➡️](../DAY84/task-84-copy-a-file-to-all-app-servers.md)
