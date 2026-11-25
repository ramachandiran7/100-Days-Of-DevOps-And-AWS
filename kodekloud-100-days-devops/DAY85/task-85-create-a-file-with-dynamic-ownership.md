# Day 85: Create a File with Dynamic Ownership

| | |
|---|---|
| **Day** | 85 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Create `/opt/app.txt` (mode 0655) on all app servers, owned by each server's own sudo user (tony, steve, banner).

## ✅ Solution (copy and paste)

```yaml
- name: Create file with per-host ownership
  hosts: all
  become: yes
  tasks:
    - name: Create /opt/app.txt
      ansible.builtin.file:
        path: /opt/app.txt
        state: touch
        mode: '0655'
        owner: "{{ ansible_user }}"
        group: "{{ ansible_user }}"
```
`ansible_user` comes from the inventory line of each host, so ownership differs per server automatically.
```bash
ansible-playbook -i inventory playbook.yml
ansible -i inventory all -a "ls -l /opt/app.txt"
```

## 🧪 Verification

```bash
ansible -i inventory all -a "ls -l /opt/app.txt"
```
Each server shows its own owner (tony, steve, banner) and mode `-rw-r-xr-x`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The mode is ignored | Quote it: `'0655'`. |
| Same owner everywhere | Use `"{{ ansible_user }}"`, which comes from each inventory line. |
| Permission denied | Add `become: yes`. |

## 📸 Screenshot

![Day 85 verification](./screenshots/day85.png)

---
[⬅️ Day 84](../DAY84/task-84-copy-a-file-to-all-app-servers.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 86 ➡️](../DAY86/task-86-passwordless-ssh-for-ansible.md)
