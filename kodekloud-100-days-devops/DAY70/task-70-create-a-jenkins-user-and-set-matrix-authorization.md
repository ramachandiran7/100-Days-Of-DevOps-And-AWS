# Day 70: Create a Jenkins User and Set Matrix Authorization

| | |
|---|---|
| **Day** | 70 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Create user `<USER>`, install Matrix Authorization Strategy, give the user the permissions in the task, keep admin with full access.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<USER>`

## ✅ Solution (copy and paste)

1. **Manage Jenkins > Users > Create User**: username, password, full name. Create.
2. **Manage Jenkins > Plugins** > install **Matrix Authorization Strategy**. Restart when done.
3. **Manage Jenkins > Security > Authorization** > select **Project-based Matrix Authorization Strategy**.
4. In the matrix:
   - **admin**: tick every box (Administer / all).
   - **`<USER>`**: tick **Overall > Read** and the other permissions the task lists (e.g. Job > Read).
   - **Authenticated Users**: leave blank unless the task says otherwise.
5. **Save**.

## 🧪 Verification

log out, log in as `<USER>`: you can see Jenkins but only do what you were allowed to. Log back in as admin.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Locked out after enabling matrix | Give admin all permissions before saving. |
| The user cannot log in | Create the user under Manage Jenkins, then Users. |
| Wrong permissions | Tick only what the task lists. |

## 💡 Notes

if you forget to give admin full access, you lock yourself out. Add admin first, then save.

## 📸 Screenshot

![Day 70 verification](./screenshots/day70.png)

---
[⬅️ Day 69](../DAY69/task-69-install-jenkins-plugins.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 71 ➡️](../DAY71/task-71-parameterized-job-that-installs-a-package-over-ssh.md)
