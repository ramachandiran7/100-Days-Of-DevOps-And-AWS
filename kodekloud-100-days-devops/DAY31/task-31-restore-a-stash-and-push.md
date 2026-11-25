# Day 31: Restore a Stash and Push

| | |
|---|---|
| **Day** | 31 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

Restore `stash@{<N>}` in `/usr/src/kodekloudrepos/<REPO>`, commit, push to `origin/master`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<N>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>

git stash list                          # see all stashes
git stash apply stash@{<N>}             # e.g. stash@{1}
git status

git add .
git commit -m "Restore stashed changes"
git push origin master
```

## 🧪 Verification

```bash
git log --oneline -2
git status
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `stash@{N}` not found | `git stash list` and use the correct index. |
| Conflict on apply | Resolve it, `git add`, then commit. |
| Change missing on the remote | You must commit and also run `git push origin master`. |

## 💡 Notes

`apply` keeps the stash in the list; `pop` removes it. Use the one the task implies, `apply` is the safe default.

## 📸 Screenshot

![Day 31 verification](./screenshots/day31.png)

---
[⬅️ Day 30](../DAY30/task-30-hard-reset-to-a-commit-and-force-push.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 32 ➡️](../DAY32/task-32-rebase-a-feature-branch-onto-master.md)
