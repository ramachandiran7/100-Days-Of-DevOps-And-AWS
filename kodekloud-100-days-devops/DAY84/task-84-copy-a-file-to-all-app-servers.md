# Day 84: Copy a File to All App Servers

| | |
|---|---|
| **Day** | 84 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Copy `/usr/src/finance/index.html` to `/opt/finance/index.html` on all 3 app servers. Inventory `/home/thor/ansible/inventory`, playbook `/home/thor/ansible/playbook.yml`.

## ✅ Solution (copy and paste)

```bash
mkdir -p /home/thor/ansible && cd /home/thor/ansible
vi inventory                            # three hosts (see skeleton at top)
vi playbook.yml
```
```yaml
- name: Copy index.html to all app servers
  hosts: all
  become: yes
  tasks:
    - name: Make sure the destination folder exists
      ansible.builtin.file:
        path: /opt/finance
        state: directory
        mode: '0755'

    - name: Copy index.html
      ansible.builtin.copy:
        src: /usr/src/finance/index.html
        dest: /opt/finance/index.html
```
```bash
ansible-playbook -i inventory playbook.yml
```

## 🧪 Verification

`ansible -i inventory all -a "ls -l /opt/finance/index.html"`

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Could not find or access` the source | Check the path on the jump host. |
| The destination folder is missing | Create it with a `file` task first. |
| Permission denied | Add `become: yes`. |

## 📸 Screenshot

![Day 84 verification](./screenshots/day84.png)

---
[⬅️ Day 83](../DAY83/task-83-fix-the-inventory-and-create-a-playbook-create-a-file.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 85 ➡️](../DAY85/task-85-create-a-file-with-dynamic-ownership.md)
