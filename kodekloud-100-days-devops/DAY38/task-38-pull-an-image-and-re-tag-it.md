# Day 38: Pull an Image and Re-tag It

| | |
|---|---|
| **Day** | 38 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

Pull `busybox:musl` and create tag `busybox:media`.

## ✅ Solution (copy and paste)

```bash
ssh banner@stapp03
sudo su -
docker pull busybox:musl
docker tag busybox:musl busybox:media
```

## 🧪 Verification

```bash
docker images | grep busybox            # both tags, same IMAGE ID
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `pull access denied` | Check the spelling of `busybox:musl`. |
| The new tag is missing | `docker images`, then repeat `docker tag`. |
| Done on the wrong server | The task names the app server. Check `hostname`. |

## 📸 Screenshot

![Day 38 verification](./screenshots/day38.png)

---
[⬅️ Day 37](../DAY37/task-37-copy-a-file-into-a-running-container.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 39 ➡️](../DAY39/task-39-create-an-image-from-a-container.md)
