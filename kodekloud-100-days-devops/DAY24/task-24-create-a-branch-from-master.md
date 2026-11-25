# Day 24: Create a Branch from master

| | |
|---|---|
| **Day** | 24 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

In `/usr/src/kodekloudrepos/<REPO>` create branch `<NEW_BRANCH>` from `master`. No code changes.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NEW_BRANCH>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>
git status
git checkout master
git branch <NEW_BRANCH>                # creates it WITHOUT switching
```

## 🧪 Verification

```bash
git branch -a
git log --oneline -1 master
git log --oneline -1 <NEW_BRANCH>      # same commit hash as master
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `branch already exists` | It exists already. `git branch -a` to confirm. |
| The new branch does not match master | It was created from another branch. Run `git checkout master` first, then `git branch <NEW_BRANCH>`. |
| `dubious ownership` | Use the `safe.directory` command from the top of this phase. |

## 📸 Screenshot

![Day 24 verification](./screenshots/day24.png)

---
[⬅️ Day 23](../DAY23/task-23-fork-a-repository-in-gitea-ui-task.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 25 ➡️](../DAY25/task-25-branch-commit-merge-and-push.md)
