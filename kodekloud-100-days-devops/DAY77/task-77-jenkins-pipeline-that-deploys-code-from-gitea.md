# Day 77: Jenkins Pipeline that Deploys Code from Gitea

| | |
|---|---|
| **Day** | 77 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Pipeline job that updates `/var/www/html` on the Storage Server from the Gitea repo, live through the LBR.

## ✅ Solution (copy and paste)

### Prep on the storage server
```bash
ssh natasha@ststor01
sudo yum install -y java-17-openjdk git
sudo chown -R natasha:natasha /var/www/html      # (or the user the task names)
cd /var/www/html && git remote -v && git branch  # repo is already cloned here
git config --global --add safe.directory /var/www/html
```
### Add the node
1. Credentials: add `natasha` (username/password) with ID `ststor01`.
2. **Manage Jenkins > Nodes > New Node**: Name `Storage Server`, Remote root `/var/www/html` (or `/home/natasha/jenkins`), Label `ststor01`, Launch via SSH to `ststor01`, non-verifying host key.

### Create the pipeline
1. **New Item** > name from the task > **Pipeline** > OK.
2. **Pipeline > Definition: Pipeline script**:
```groovy
pipeline {
    agent { label 'ststor01' }
    stages {
        stage('Deploy') {
            steps {
                sh '''
                    cd /var/www/html
                    git pull origin master
                '''
            }
        }
    }
}
```
3. Save > **Build Now**.

## 🧪 Verification

open the LBR URL (lab website button): your latest content shows with no sub-folder.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `git pull` fails with an ownership error | `git config --global --add safe.directory /var/www/html`. |
| Agent offline | Check Java and the node credentials. |
| Permission denied in `/var/www/html` | `chown` the folder to the agent user. |

## 💡 Notes

if `git pull` asks for credentials, set the remote URL with the Gitea user's login or a token.

## 📸 Screenshot

![Day 77 verification](./screenshots/day77.png)

---
[⬅️ Day 76](../DAY76/task-76-project-based-matrix-authorization-on-a-job.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 78 ➡️](../DAY78/task-78-conditional-pipeline-branch-parameter.md)
