# Day 93: Conditionals (`when`)

| | |
|---|---|
| **Day** | 93 of 100 |
| **Phase** | 6 · Ansible |

## 📌 Task

One play on all hosts. Copy a different file to each server's `/opt/data/` using `when: inventory_hostname == ...`.

## ✅ Solution (copy and paste)

| Server | Source | Destination | Owner |
|---|---|---|---|
| stapp01 | /usr/src/data/blog.txt | /opt/data/blog.txt | tony |
| stapp02 | /usr/src/data/story.txt | /opt/data/story.txt | steve |
| stapp03 | /usr/src/data/media.txt | /opt/data/media.txt | banner |

```yaml
- name: Copy host-specific files
  hosts: all
  become: yes
  tasks:
    - name: Copy blog.txt to stapp01
      ansible.builtin.copy:
        src: /usr/src/data/blog.txt
        dest: /opt/data/blog.txt
        owner: tony
        group: tony
        mode: '0744'
      when: inventory_hostname == "stapp01"

    - name: Copy story.txt to stapp02
      ansible.builtin.copy:
        src: /usr/src/data/story.txt
        dest: /opt/data/story.txt
        owner: steve
        group: steve
        mode: '0744'
      when: inventory_hostname == "stapp02"

    - name: Copy media.txt to stapp03
      ansible.builtin.copy:
        src: /usr/src/data/media.txt
        dest: /opt/data/media.txt
        owner: banner
        group: banner
        mode: '0744'
      when: inventory_hostname == "stapp03"
```
```bash
ansible-playbook -i inventory playbook.yml
ansible -i inventory all -a "ls -l /opt/data"
```

## 🧪 Verification

```bash
ansible -i inventory all -a "ls -l /opt/data"
```
Each server shows only its own file with the right owner.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Every task is skipped | The `when` string must match the inventory name exactly. |
| The destination folder is missing | Create `/opt/data` with a `file` task. |
| Invalid owner | Make sure the users exist on the target servers. |

## 💡 Notes

the string in `when:` must match the inventory name exactly.

## 📸 Screenshot

![Day 93 verification](./screenshots/day93.png)

---
[⬅️ Day 92](../DAY92/task-92-ansible-role-with-a-jinja2-template.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 94 ➡️](../DAY94/task-94-create-a-vpc.md)
