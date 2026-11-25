# Day 25: Branch, Commit, Merge and Push

| | |
|---|---|
| **Day** | 25 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

In `/usr/src/kodekloudrepos/<REPO>` create branch `<BRANCH>` from master, add `/tmp/index.html`, commit, merge into master, push both branches to origin.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<BRANCH>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>

git checkout master
git checkout -b <BRANCH>               # create + switch

cp /tmp/index.html .
git add index.html
git commit -m "Add index.html"

git checkout master
git merge <BRANCH>

git push origin <BRANCH>
git push origin master
```

## 🧪 Verification

```bash
git log --oneline --graph --all
git status                              # "up to date with origin/master"
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Please tell me who you are` | Set `git config --global user.name` and `git config --global user.email`. |
| Push rejected | `git pull origin <branch>` first, then push again. |
| Master is not updated on the remote | Push both: the branch and master. |

## 📸 Screenshot

![Day 25 verification](./screenshots/day25.png)

---
[⬅️ Day 24](../DAY24/task-24-create-a-branch-from-master.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 26 ➡️](../DAY26/task-26-add-a-new-git-remote-and-push.md)
