# Day 92: Ansible Role with a Jinja2 Template

| | |
|---|---|
| **Day** | 92 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Run the `httpd` role on `stapp02`. Template `index.html.j2` with the dynamic hostname, deployed to `/var/www/html/index.html`, owner = sudo user, mode `0644`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APACHE_PORT>`

## ✅ Solution (copy and paste)

```bash
cd ~/ansible
ls role/httpd                            # tasks/ templates/ ... already exists
vi role/httpd/templates/index.html.j2
```
`templates/index.html.j2`:
```jinja
This file was created using Ansible on {{ inventory_hostname }}
```
`role/httpd/tasks/main.yml` (append this task, keep the existing install/start tasks):
```yaml
- name: Deploy index.html from template
  ansible.builtin.template:
    src: index.html.j2
    dest: /var/www/html/index.html
    owner: "{{ ansible_user }}"
    group: "{{ ansible_user }}"
    mode: '0644'
```
`playbook.yml`:
```yaml
- hosts: stapp02
  become: yes
  roles:
    - role/httpd
```
```bash
ansible-playbook -i inventory playbook.yml
curl http://stapp02:<APACHE_PORT>        # shows the hostname text
```
Use the exact sentence from your task for the template content.

## 🧪 Verification

```bash
curl http://stapp02:<APACHE_PORT>
```
The page shows the template text with the host name filled in.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `role not found` | Run from `~/ansible`. The role path is `role/httpd`. |
| `Could not find or access index.html.j2` | The file goes in `templates/` inside the role. |
| The hostname is not shown | Use `{{ inventory_hostname }}` in the template. |

## 📸 Screenshot

![Day 92 verification](./screenshots/day92.png)

---
[⬅️ Day 91](../DAY91/task-91-httpd-lineinfile-prepend-a-line.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 93 ➡️](../DAY93/task-93-conditionals-when.md)
