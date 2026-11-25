# Day 87: Install a Package on All App Servers

| | |
|---|---|
| **Day** | 87 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Install `samba` using the `yum` module on all app servers.

## ✅ Solution (copy and paste)

```yaml
- name: Install samba
  hosts: all
  become: yes
  tasks:
    - name: Install samba
      ansible.builtin.yum:
        name: samba
        state: present
```
```bash
ansible-playbook -i inventory playbook.yml
ansible -i inventory all -a "rpm -q samba"
```

## 🧪 Verification

```bash
ansible -i inventory all -a "rpm -q samba"
```
Every server prints a samba package version.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `This command has to be run under the root user` | Add `become: yes`. |
| A yum lock error | Wait a moment and run again. |
| Package not found | Check the spelling `samba`. |

## 📸 Screenshot

![Day 87 verification](./screenshots/day87.png)

---
[⬅️ Day 86](../DAY86/task-86-passwordless-ssh-for-ansible.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 88 ➡️](../DAY88/task-88-deploy-httpd-with-blockinfile.md)
