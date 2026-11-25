# Day 79: Auto-Deploy on Every Gitea Push

| | |
|---|---|
| **Day** | 79 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Job `nautilus-app-deployment`: poll Gitea `master` and copy the code to `/var/www/html` on the Storage Server. Apache runs on port 8080 on all app servers.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<GITEA_REPO_URL>`

## ✅ Solution (copy and paste)

### 1. Apache on all app servers
```bash
# Repeat on stapp01, stapp02, stapp03
sudo yum install -y httpd
sudo sed -i 's/^Listen .*/Listen 8080/' /etc/httpd/conf/httpd.conf
sudo systemctl enable --now httpd
```
### 2. Job (runs on the Storage Server node, label `ststor01`)
1. **New Item** > `nautilus-app-deployment` > Freestyle.
2. **General > Restrict where this project can be run** > Label `ststor01`.
3. **Source Code Management > Git** > Repository URL: `<GITEA_REPO_URL>` (e.g. `http://git.stratos.xfusioncorp.com/sarah/web.git`), add Gitea credentials, Branch `*/master`.
4. **Build Triggers > Poll SCM** > `* * * * *`
5. **Build Steps > Execute shell**:
```bash
sudo chown -R sarah:sarah /var/www/html 2>/dev/null || true
rm -rf /var/www/html/*
cp -r $WORKSPACE/* /var/www/html/
```
6. Save > **Build Now**.

## 🧪 Verification

LBR URL shows the page. Push a change in Gitea (edit `index.html`) and watch a new build start within a minute.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Polling does not trigger | Set the schedule `* * * * *` and the branch `*/master`. |
| Files are not copied | The node label must be `ststor01`. Check permissions of `/var/www/html`. |
| The LBR page fails | Apache must listen on 8080 on all app servers. |

## 💡 Notes

adjust ownership and paths to what the task says.

## 📸 Screenshot

![Day 79 verification](./screenshots/day79.png)

---
[⬅️ Day 78](../DAY78/task-78-conditional-pipeline-branch-parameter.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 80 ➡️](../DAY80/task-80-chained-builds-upstream-then-downstream.md)
