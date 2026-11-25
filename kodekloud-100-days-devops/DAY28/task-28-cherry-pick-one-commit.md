# Day 28: Cherry-Pick One Commit

| | |
|---|---|
| **Day** | 28 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

Apply only the commit "<COMMIT_MESSAGE>" from `feature` onto `master`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<COMMIT_MESSAGE>` `<HASH>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>

git log feature --oneline               # find the hash of "<COMMIT_MESSAGE>"
git checkout master
git cherry-pick <HASH>
git push origin master
```

## 🧪 Verification

```bash
git log --oneline -3                    # cherry-picked commit is on master
git status
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Cannot find the commit hash | `git log feature --oneline` and look for the message. |
| Cherry-pick conflict | Edit the file, `git add`, then `git cherry-pick --continue`. |
| Change is not on the remote | `git push origin master`. |

## 💡 Notes

if there is a conflict: edit the file, `git add <file>`, `git cherry-pick --continue`.

## 📸 Screenshot

![Day 28 verification](./screenshots/day28.png)

---
[⬅️ Day 27](../DAY27/task-27-revert-the-latest-commit.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 29 ➡️](../DAY29/task-29-pull-request-workflow-in-gitea-ui-task.md)
