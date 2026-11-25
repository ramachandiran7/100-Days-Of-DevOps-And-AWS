# Day 90: Files with ACLs

| | |
|---|---|
| **Day** | 90 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

Create files with specific ACLs on each server:

## ✅ Solution (copy and paste)

| Server | File | Owner | ACL |
|---|---|---|---|
| stapp01 | /opt/dba/blog.txt | root:root | group tony: r |
| stapp02 | /opt/dba/story.txt | root:root | user steve: rw |
| stapp03 | /opt/dba/media.txt | root:root | group banner: rw |

```yaml
- name: ACL on stapp01
  hosts: stapp01
  become: yes
  tasks:
    - ansible.builtin.file:
        path: /opt/dba
        state: directory
    - ansible.builtin.file:
        path: /opt/dba/blog.txt
        state: touch
        owner: root
        group: root
    - ansible.posix.acl:
        path: /opt/dba/blog.txt
        entity: tony
        etype: group
        permissions: r
        state: present

- name: ACL on stapp02
  hosts: stapp02
  become: yes
  tasks:
    - ansible.builtin.file:
        path: /opt/dba
        state: directory
    - ansible.builtin.file:
        path: /opt/dba/story.txt
        state: touch
        owner: root
        group: root
    - ansible.posix.acl:
        path: /opt/dba/story.txt
        entity: steve
        etype: user
        permissions: rw
        state: present

- name: ACL on stapp03
  hosts: stapp03
  become: yes
  tasks:
    - ansible.builtin.file:
        path: /opt/dba
        state: directory
    - ansible.builtin.file:
        path: /opt/dba/media.txt
        state: touch
        owner: root
        group: root
    - ansible.posix.acl:
        path: /opt/dba/media.txt
        entity: banner
        etype: group
        permissions: rw
        state: present
```
```bash
ansible-playbook -i inventory playbook.yml
ansible stapp01 -i inventory -b -a "getfacl /opt/dba/blog.txt"
```

## 🧪 Verification

```bash
ansible stapp01 -i inventory -b -a "getfacl /opt/dba/blog.txt"
```
The ACL entry from the task is listed. Repeat for stapp02 and stapp03.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `ansible.posix.acl` not found | `ansible-galaxy collection install ansible.posix`. |
| `setfacl: command not found` | Install the `acl` package on the host. |
| Applied to the wrong host | Each play must target its own host. |

## 💡 Notes

if `ansible.posix` is missing: `ansible-galaxy collection install ansible.posix`.

## 📸 Screenshot

![Day 90 verification](./screenshots/day90.png)

---
[⬅️ Day 89](../DAY89/task-89-install-start-and-enable-httpd.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 91 ➡️](../DAY91/task-91-httpd-lineinfile-prepend-a-line.md)
