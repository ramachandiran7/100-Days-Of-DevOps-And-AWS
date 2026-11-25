# Day 88: Deploy httpd with blockinfile

| | |
|---|---|
| **Day** | 88 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Install and start httpd on all app servers; create `/var/www/html/index.html` with 3 lines via `blockinfile`; owner/group `apache`, mode `0744`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APACHE_PORT>`

## ✅ Solution (copy and paste)

```yaml
- name: Deploy httpd with a sample page
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

    - name: Create index.html using blockinfile
      ansible.builtin.blockinfile:
        path: /var/www/html/index.html
        create: yes
        owner: apache
        group: apache
        mode: '0744'
        block: |
          Welcome to XfusionCorp!
          This is Nautilus sample file, created using Ansible!
          Please do not modify this file manually!
```
Use the exact three lines from your task.
```bash
ansible-playbook -i inventory playbook.yml
curl http://stapp01:<APACHE_PORT>
```

## 🧪 Verification

```bash
ansible -i inventory all -a "cat /var/www/html/index.html"
curl http://stapp01:<APACHE_PORT>
```
The three lines from the task are shown.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `index.html` contains marker comments | Normal for `blockinfile`. It adds BEGIN and END ANSIBLE MANAGED BLOCK lines. |
| httpd is not running | Add the service task with `state: started`. |
| Wrong permissions | `owner` and `group` are `apache`, `mode: '0744'`. |

## 📸 Screenshot

![Day 88 verification](./screenshots/day88.png)

---
[⬅️ Day 87](../DAY87/task-87-install-a-package-on-all-app-servers.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 89 ➡️](../DAY89/task-89-install-start-and-enable-httpd.md)
