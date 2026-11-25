# Day 26: Add a New Git Remote and Push

| | |
|---|---|
| **Day** | 26 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

In `/usr/src/kodekloudrepos/<REPO>` add remote `<REMOTE_NAME>` pointing at `/opt/<NEW_REPO>.git`, commit `/tmp/index.html` on master, push master to the new remote.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NEW_REPO>` `<REMOTE_NAME>` `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
cd /usr/src/kodekloudrepos/<REPO>

git remote add <REMOTE_NAME> /opt/<NEW_REPO>.git
git remote -v

cp /tmp/index.html .
git add index.html
git commit -m "Add index.html"
git push <REMOTE_NAME> master
```

## 🧪 Verification

```bash
git remote -v
git ls-remote <REMOTE_NAME>             # shows refs/heads/master with your commit
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `remote already exists` | `git remote set-url <REMOTE_NAME> /opt/<NEW_REPO>.git`. |
| Push fails with no such repository | Check the path with `ls -d /opt/*.git`. |
| `nothing to commit` | The file is already tracked or `cp` failed. Run `git status`. |

## 📸 Screenshot

![Day 26 verification](./screenshots/day26.png)

---
[⬅️ Day 25](../DAY25/task-25-branch-commit-merge-and-push.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 27 ➡️](../DAY27/task-27-revert-the-latest-commit.md)
