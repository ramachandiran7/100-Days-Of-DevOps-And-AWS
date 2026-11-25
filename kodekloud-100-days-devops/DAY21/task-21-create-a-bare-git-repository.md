# Day 21: Create a Bare Git Repository

| | |
|---|---|
| **Day** | 21 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

On the storage server install Git and create a bare repo at `/opt/<NAME>.git`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NAME>`

## ✅ Solution (copy and paste)

```bash
ssh natasha@ststor01
sudo su -
yum install -y git
git --version

cd /opt
git init --bare <NAME>.git            # e.g. games.git
```

## 🧪 Verification

```bash
ls -ld /opt/<NAME>.git
git -C /opt/<NAME>.git rev-parse --is-bare-repository      # true
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `git: command not found` | `yum install -y git`. |
| The repo is not bare | Re-create it with `git init --bare <name>.git`. |
| `Permission denied` in `/opt` | Run as root with `sudo su -`. |

## 💡 Notes

a bare repo has no working files. It is the shared "central" repo others push to.

## 📸 Screenshot

![Day 21 verification](./screenshots/day21.png)

---
[⬅️ Day 20](../DAY20/task-20-nginx-php-fpm-8-3-over-a-unix-socket.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 22 ➡️](../DAY22/task-22-clone-a-repository-to-a-specific-directory.md)
