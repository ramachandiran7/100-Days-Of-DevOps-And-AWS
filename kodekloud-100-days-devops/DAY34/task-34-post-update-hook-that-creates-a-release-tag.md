# Day 34: post-update Hook that Creates a Release Tag

| | |
|---|---|
| **Day** | 34 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

Merge `feature` into `master` in `/usr/src/kodekloudrepos/<REPO>`; create a `post-update` hook in `/opt/<REPO>.git` that tags `release-YYYY-MM-DD`; test; push. Use natasha; don't change permissions.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<REPO>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01

# 1. Merge
cd /usr/src/kodekloudrepos/<REPO>
git checkout master
git merge feature

# 2. Create the hook in the BARE repo
vi /opt/<REPO>.git/hooks/post-update
```
Hook content:
```bash
#!/bin/bash
# Create a release tag whenever master is pushed
for ref in "$@"; do
  if [ "$ref" = "refs/heads/master" ]; then
    TAG="release-$(date +%F)"
    git tag -f "$TAG" refs/heads/master
  fi
done
exit 0
```
```bash
chmod +x /opt/<REPO>.git/hooks/post-update

# 3. Push (this triggers the hook)
cd /usr/src/kodekloudrepos/<REPO>
git push origin master
```

## 🧪 Verification

```bash
git --git-dir=/opt/<REPO>.git tag      # release-<today's date>
git fetch --tags && git tag
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| The tag is not created | The hook must be named exactly `post-update` and be executable (`chmod +x`). |
| Nothing happened on merge | The hook only fires on `git push` to the bare repo. |
| Wrong tag name | Use the exact format from the task: `release-YYYY-MM-DD`. |

## 💡 Notes

the hook only fires on a push to the bare repo, not on a local merge. If the tag name has a required format, follow the task exactly.

## 📸 Screenshot

![Day 34 verification](./screenshots/day34.png)

---
[⬅️ Day 33](../DAY33/task-33-fix-a-rejected-push-typo-rebase-conflict.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 35 ➡️](../DAY35/task-35-install-docker-ce-and-the-compose-plugin.md)
