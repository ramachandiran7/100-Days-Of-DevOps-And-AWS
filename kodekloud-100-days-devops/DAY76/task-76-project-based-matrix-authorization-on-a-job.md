# Day 76: Project-Based Matrix Authorization on a Job

| | |
|---|---|
| **Day** | 76 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

For job `Packages`, give users `sam` and `rohan` specific permissions with inheritance.

## ✅ Solution (copy and paste)

1. Make sure the users exist (**Manage Jenkins > Users**) and the **Matrix Authorization Strategy** plugin is installed.
2. **Manage Jenkins > Security > Authorization** > **Project-based Matrix Authorization Strategy**.
   - admin: all permissions. `sam`, `rohan`: **Overall > Read**. Save.
3. Open job **Packages** > **Configure** > tick **Enable project-based security**.
4. **Inheritance Strategy**: **Inherit permissions from parent ACL**.
5. Add users and tick permissions:

| User | Permissions |
|---|---|
| sam | Job: Build, Configure, Read |
| rohan | Job: Build, Cancel, Configure, Read, Update; SCM: Tag |

6. Save.

## 🧪 Verification

log in as `sam` and `rohan` separately and confirm the buttons match.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The user cannot see the job | They need **Overall > Read** and **Job > Read**. |
| Permissions are not applied | Enable **project-based security** on the job. |
| Locked out | Keep admin with full rights. |

## 📸 Screenshot

![Day 76 verification](./screenshots/day76.png)

---
[⬅️ Day 75](../DAY75/task-75-add-ssh-slave-nodes.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 77 ➡️](../DAY77/task-77-jenkins-pipeline-that-deploys-code-from-gitea.md)
