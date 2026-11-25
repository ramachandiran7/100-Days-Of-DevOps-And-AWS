# Day 78: Conditional Pipeline (branch parameter)

| | |
|---|---|
| **Day** | 78 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Pipeline with a `BRANCH` choice parameter (`master` or `feature`) that deploys only that branch.

## ✅ Solution (copy and paste)

Prep: same node and repo as Day 77.

```groovy
pipeline {
    agent { label 'ststor01' }
    parameters {
        choice(name: 'BRANCH', choices: ['master', 'feature'], description: 'Branch to deploy')
    }
    stages {
        stage('Deploy') {
            steps {
                sh """
                    cd /var/www/html
                    git fetch --all
                    git checkout ${params.BRANCH}
                    git pull origin ${params.BRANCH}
                """
            }
        }
    }
}
```
### Run
Build with Parameters > `master`, check the LBR page; then `feature`, check again.

## 🧪 Verification

Run **Build with Parameters** once with `master` and once with `feature`. After each run:
```bash
curl http://stlb01
```
The page changes to match the branch you deployed, and the console ends with `Finished: SUCCESS`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `checkout` fails because of local changes | `git stash` or `git checkout -- .` first. |
| Branch not found | `git fetch --all` before the checkout. |
| The parameter is not used | Use `${params.BRANCH}` inside a double-quoted shell string. |

## 📸 Screenshot

![Day 78 verification](./screenshots/day78.png)

---
[⬅️ Day 77](../DAY77/task-77-jenkins-pipeline-that-deploys-code-from-gitea.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 79 ➡️](../DAY79/task-79-auto-deploy-on-every-gitea-push.md)
