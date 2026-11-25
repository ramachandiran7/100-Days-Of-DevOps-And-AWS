# Day 33: Fix a Rejected Push (typo + rebase conflict)

| | |
|---|---|
| **Day** | 33 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

As `max`, fix a typo in `story-index.txt` in `/home/max/story-blog`, resolve the conflict, push, verify in Gitea.

## ✅ Solution (copy and paste)

```bash
ssh max@ststor01
cd /home/max/story-blog
git status
git log --oneline -5
cat story-index.txt                     # find the typo

# 1. Fix the typo
vi story-index.txt
git add story-index.txt
git commit -m "Fix typo in story-index.txt"

# 2. Push is rejected (remote has new commits). Rebase onto them:
git push origin master                  # ! [rejected] ...
git pull --rebase origin master

# 3. Conflict in story-index.txt. Open it, remove the <<<<<<< ======= >>>>>>> markers,
#    keep the correct lines (both writers' stories + the typo fix)
vi story-index.txt
git add story-index.txt
git rebase --continue

# 4. Push
git push origin master
```

## 🧪 Verification

open Gitea, repo `story-blog`, open `story-index.txt`. The typo is fixed and both authors' lines are present. Screenshot it.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Conflict markers left in the file | Delete every `<<<<<<<`, `=======` and `>>>>>>>` line. |
| Stuck in the middle of a rebase | `git status` shows the next step: `git add`, then `git rebase --continue`. |
| Push still rejected | Run `git pull --rebase origin master` again, then push. |

## 💡 Notes

run `git status` any time to see which step you are in.

## 📸 Screenshot

![Day 33 verification](./screenshots/day33.png)

---
[⬅️ Day 32](../DAY32/task-32-rebase-a-feature-branch-onto-master.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 34 ➡️](../DAY34/task-34-post-update-hook-that-creates-a-release-tag.md)
