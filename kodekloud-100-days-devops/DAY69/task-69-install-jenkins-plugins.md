# Day 69: Install Jenkins Plugins

| | |
|---|---|
| **Day** | 69 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Install the Git and GitLab plugins.

## ✅ Solution (copy and paste)

1. Log in as admin.
2. **Manage Jenkins > Plugins > Available plugins**.
3. Search `Git`, tick **Git**. Search `GitLab`, tick **GitLab**.
4. Click **Install**, then tick **Restart Jenkins when installation is complete and no jobs are running**.
5. When Jenkins is back, log in again.

## 🧪 Verification

**Plugins > Installed plugins**, search `Git` and `GitLab`: both listed.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Plugin not found | Search under Available plugins. Refresh the plugin index if the list is empty. |
| The plugin shows pending restart | Restart Jenkins from Manage Jenkins. |
| Install fails | Check the Jenkins server has internet access. |

## 📸 Screenshot

![Day 69 verification](./screenshots/day69.png)

---
[⬅️ Day 68](../DAY68/task-68-set-up-a-jenkins-server.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 70 ➡️](../DAY70/task-70-create-a-jenkins-user-and-set-matrix-authorization.md)
