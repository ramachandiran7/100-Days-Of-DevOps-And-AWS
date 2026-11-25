# Day 30: Hard Reset to a Commit and Force-Push

| | |
|---|---|
| **Day** | 30 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

Reset `/usr/src/kodekloudrepos/<REPO>` so only the initial commit and `<COMMIT_MESSAGE>` remain.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<COMMIT_MESSAGE>` `<HASH>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>

git log --oneline                       # find the hash of "<COMMIT_MESSAGE>"
git reset --hard <HASH>
git log --oneline                       # only the 2 wanted commits remain

git push origin master --force
```

## 🧪 Verification

```bash
git log --oneline
git status
git ls-remote origin                    # remote master == your <HASH>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Push rejected (non-fast-forward) | History was rewritten. Use `git push origin master --force`. |
| Wrong commits remain | `git reflog` finds the old HEAD. Run `git reset --hard <HASH>` again. |
| `dubious ownership` | Use `safe.directory`. |

## 💡 Notes

`--hard` deletes later commits and working changes. Force-push rewrites remote history.

## 📸 Screenshot

![Day 30 verification](./screenshots/day30.png)

---
[⬅️ Day 29](../DAY29/task-29-pull-request-workflow-in-gitea-ui-task.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 31 ➡️](../DAY31/task-31-restore-a-stash-and-push.md)
