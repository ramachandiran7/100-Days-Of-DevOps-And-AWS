# Day 89: Install, Start and Enable httpd

| | |
|---|---|
| **Day** | 89 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Install, start and enable `httpd` on all app servers using one Ansible playbook.

## ✅ Solution (copy and paste)

```yaml
- name: Install and enable httpd
  hosts: all
  become: yes
  tasks:
    - name: Install httpd
      ansible.builtin.yum:
        name: httpd
        state: present

    - name: Start and enable httpd
      ansible.builtin.service:
        name: httpd
        state: started
        enabled: yes
```
```bash
ansible-playbook -i inventory playbook.yml
ansible -i inventory all -a "systemctl is-active httpd"
ansible -i inventory all -a "systemctl is-enabled httpd"
```

## 🧪 Verification

```bash
ansible -i inventory all -a "systemctl is-active httpd"
ansible -i inventory all -a "systemctl is-enabled httpd"
```
Both commands print `active` and `enabled` for every server.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Could not find the requested service` | Install httpd first. The yum task must run before the service task. |
| Permission denied | Add `become: yes`. |
| Starts but is not enabled | Add `enabled: yes`. |

## 📸 Screenshot

![Day 89 verification](./screenshots/day89.png)

---
[⬅️ Day 88](../DAY88/task-88-deploy-httpd-with-blockinfile.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 90 ➡️](../DAY90/task-90-files-with-acls.md)
