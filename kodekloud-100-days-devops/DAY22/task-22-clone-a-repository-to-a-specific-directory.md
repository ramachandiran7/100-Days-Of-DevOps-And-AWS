# Day 22: Clone a Repository to a Specific Directory

| | |
|---|---|
| **Day** | 22 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

As `natasha`, clone `/opt/<REPO>.git` into `/usr/src/kodekloudrepos/<REPO>` without changing permissions.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01                   # stay as natasha. Do NOT use root.
cd /usr/src/kodekloudrepos
git clone /opt/<REPO>.git /usr/src/kodekloudrepos/<REPO>
```

## 🧪 Verification

```bash
cd /usr/src/kodekloudrepos/<REPO>
git status
git remote -v
ls -la
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `dubious ownership` | `git config --global --add safe.directory '*'`. |
| `Permission denied` | Stay as natasha and do not change permissions. |
| `destination path already exists` | The folder already has content. Check `ls -la` and clone into the exact path from the task. |

## 💡 Notes

if you get "dubious ownership", use the `safe.directory` command at the top. Do not `chmod`/`chown` anything.

## 📸 Screenshot

![Day 22 verification](./screenshots/day22.png)

---
[⬅️ Day 21](../DAY21/task-21-create-a-bare-git-repository.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 23 ➡️](../DAY23/task-23-fork-a-repository-in-gitea-ui-task.md)
