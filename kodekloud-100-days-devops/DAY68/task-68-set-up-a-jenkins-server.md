# Day 68: Set Up a Jenkins Server

| | |
|---|---|
| **Day** | 68 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Install Jenkins with yum only, start it, create the admin user from the task.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<USER>`

## ✅ Solution (copy and paste)

```bash
# On the Jenkins server
ssh <USER>@jenkins
sudo su -

# Jenkins needs a current Java
yum install -y java-17-openjdk fontconfig

# Add the Jenkins repo and install
wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
yum install -y jenkins

systemctl enable --now jenkins
systemctl status jenkins
cat /var/lib/jenkins/secrets/initialAdminPassword      # first-login password
```
### UI setup
1. Open Jenkins (lab button, port 8080) and paste the initial admin password.
2. **Install suggested plugins** and wait.
3. **Create First Admin User** with the username, password, full name and email from the task.
4. Save and Finish, then **Start using Jenkins**.

## 🧪 Verification

log in with the new admin user.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `java: command not found` | `yum install -y java-17-openjdk`. |
| Cannot find the unlock password | `cat /var/lib/jenkins/secrets/initialAdminPassword`. |
| Jenkins will not start | `journalctl -xeu jenkins`. Usually Java is missing. |

## 💡 Notes

if the repo in your lab differs, follow the task. "yum only" means no manual RPM downloads or tarballs.

## 📸 Screenshot

![Day 68 verification](./screenshots/day68.png)

---
[⬅️ Day 67](../DAY67/task-67-guestbook-app-redis-master-redis-slave-frontend.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 69 ➡️](../DAY69/task-69-install-jenkins-plugins.md)
