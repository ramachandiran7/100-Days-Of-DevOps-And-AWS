# Day 81: Multistage Pipeline (Deploy + Test)

| | |
|---|---|
| **Day** | 81 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Pipeline `deploy-job` with stages **Deploy** and **Test** (case-sensitive names). Test checks the LBR URL content and fails fast.

## ✅ Solution (copy and paste)

### Prep
in Gitea, edit `index.html` in `sarah/web` to `Welcome to xFusionCorp Industries` and commit to master. Node and repo as in Day 77.

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
        stage('Test') {
            steps {
                sh '''
                    curl -sf http://stlb01:8091 | grep "Welcome to xFusionCorp Industries"
                '''
            }
        }
    }
}
```
Job type = **Pipeline** (not Multibranch). Save > **Build Now**.

## 🧪 Verification

the Stage View shows two green stages. `curl http://stlb01:8091` prints the welcome text.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The Test stage fails | The page text does not match. Check `curl http://stlb01:8091`. |
| Stage names are wrong | Use exactly `Deploy` and `Test`. |
| Wrong job type | Use **Pipeline**, not Multibranch. |

## 💡 Notes

`curl -f` plus `grep` returns non-zero when the page is missing or wrong, which fails the stage.

## 📸 Screenshot

![Day 81 verification](./screenshots/day81.png)

---
[⬅️ Day 80](../DAY80/task-80-chained-builds-upstream-then-downstream.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 82 ➡️](../DAY82/task-82-create-an-ini-inventory.md)
