# Day 27: Revert the Latest Commit

| | |
|---|---|
| **Day** | 27 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

Revert HEAD in `/usr/src/kodekloudrepos/<REPO>`, with the revert commit message `<MESSAGE>` (e.g. `revert games`).

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<MESSAGE>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>
git log --oneline                       # note the current HEAD

git revert --no-commit HEAD             # stage the undo, don't commit yet
git commit -m "<MESSAGE>"               # exact text from the task
```

## 🧪 Verification

```bash
git log --oneline                       # new top commit "<MESSAGE>"
git show --stat HEAD
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| An editor opens during revert | Use `git revert --no-commit HEAD`, then `git commit -m "<MESSAGE>"`. |
| Wrong revert message | Before pushing, fix it with `git commit --amend -m "<MESSAGE>"`. |
| Revert reports a conflict | Resolve the files, `git add`, then `git revert --continue`. |

## 💡 Notes

`revert` keeps history and adds a new commit, unlike `reset`.

## 📸 Screenshot

![Day 27 verification](./screenshots/day27.png)

---
[⬅️ Day 26](../DAY26/task-26-add-a-new-git-remote-and-push.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 28 ➡️](../DAY28/task-28-cherry-pick-one-commit.md)
