# Day 80: Chained Builds (upstream then downstream)

| | |
|---|---|
| **Day** | 80 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Job 1 `nautilus-app-deployment` deploys code. Job 2 `manage-services` restarts Apache on all app servers only if Job 1 is stable.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<BANNER_PASSWORD>` `<STEVE_PASSWORD>` `<TONY_PASSWORD>`

## ✅ Solution (copy and paste)

1. Build Job 1 exactly as in Day 79.
2. **New Item** > `manage-services` > Freestyle.
3. **Build Triggers > Build after other projects are built** > Projects to watch: `nautilus-app-deployment` > select **Trigger only if build is stable**.
4. **Build Steps > Execute shell** (on the Jenkins server; install `sshpass` first: `sudo yum install -y epel-release sshpass`):
```bash
sshpass -p '<TONY_PASSWORD>'   ssh -o StrictHostKeyChecking=no tony@stapp01   "sudo systemctl restart httpd"
sshpass -p '<STEVE_PASSWORD>'  ssh -o StrictHostKeyChecking=no steve@stapp02  "sudo systemctl restart httpd"
sshpass -p '<BANNER_PASSWORD>' ssh -o StrictHostKeyChecking=no banner@stapp03 "sudo systemctl restart httpd"
```
5. Save. In Job 1 you can also tick **Build other projects** > `manage-services` > **Trigger only if build is stable**.

## 🧪 Verification

run Job 1 and watch Job 2 start by itself. Console Output of Job 2 shows three successful restarts.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Job 2 never starts | Job 1 must be stable (not unstable or failed). |
| `sshpass: command not found` | Install EPEL and sshpass on the Jenkins server. |
| Restart fails | The SSH user needs sudo rights. |

## 📸 Screenshot

![Day 80 verification](./screenshots/day80.png)

---
[⬅️ Day 79](../DAY79/task-79-auto-deploy-on-every-gitea-push.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 81 ➡️](../DAY81/task-81-multistage-pipeline-deploy-test.md)
