# Day 91: httpd + lineinfile (prepend a line)

| | |
|---|---|
| **Day** | 91 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Install and start httpd; `index.html` contains `This is a Nautilus sample file, created using Ansible!`; **prepend** `Welcome to xFusionCorp Industries!` with `lineinfile`; owner/group `apache`, mode `0744`.

## ✅ Solution (copy and paste)

```yaml
- name: httpd with lineinfile
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

    - name: Create index.html
      ansible.builtin.copy:
        dest: /var/www/html/index.html
        content: "This is a Nautilus sample file, created using Ansible!\n"
        owner: apache
        group: apache
        mode: '0744'

    - name: Prepend a line
      ansible.builtin.lineinfile:
        path: /var/www/html/index.html
        insertbefore: BOF
        line: "Welcome to xFusionCorp Industries!"
```
```bash
ansible-playbook -i inventory playbook.yml
ansible -i inventory all -a "cat /var/www/html/index.html"
```

## 🧪 Verification

the "Welcome..." line is first, the "This is..." line second.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The line is added at the end | Use `insertbefore: BOF`. |
| Wrong ownership | Set `owner` and `group` to `apache` and `mode: '0744'` on the copy task. |
| A duplicate line appears | `lineinfile` is idempotent, so a re-run is safe. |

## 📸 Screenshot

![Day 91 verification](./screenshots/day91.png)

---
[⬅️ Day 90](../DAY90/task-90-files-with-acls.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 92 ➡️](../DAY92/task-92-ansible-role-with-a-jinja2-template.md)
