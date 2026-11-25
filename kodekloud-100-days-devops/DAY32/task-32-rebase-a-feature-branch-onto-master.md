# Day 32: Rebase a Feature Branch onto master

| | |
|---|---|
| **Day** | 32 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

Rebase `feature` onto `master` (no merge commits) and push `feature`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>

git checkout master
git pull origin master                  # make sure master is current
git checkout feature
git rebase master

git push origin feature --force         # history was rewritten
```

### If there are conflicts
```bash
# edit the conflicted file(s), then:
git add <file>
git rebase --continue
```

## 🧪 Verification

```bash
git log --oneline --graph --all         # straight line, no merge commits
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Conflicts during rebase | Fix the files, `git add`, then `git rebase --continue`. |
| Push rejected | Rebase rewrites history. Use `git push origin feature --force`. |
| Merge commits still present | You merged instead of rebasing. Redo with `git rebase master`. |

## 📸 Screenshot

![Day 32 verification](./screenshots/day32.png)

---
[⬅️ Day 31](../DAY31/task-31-restore-a-stash-and-push.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 33 ➡️](../DAY33/task-33-fix-a-rejected-push-typo-rebase-conflict.md)
