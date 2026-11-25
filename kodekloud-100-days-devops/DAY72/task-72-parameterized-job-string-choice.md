# Day 72: Parameterized Job (string + choice)

| | |
|---|---|
| **Day** | 72 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Job `parameterized-job`: string `Stage` (default `Build`), choice `env` (`Development`, `Staging`, `Production`), echo both, build once with `env=Staging`.

## ✅ Solution (copy and paste)

1. **New Item** > `parameterized-job` > Freestyle > OK.
2. **This project is parameterized**:
   - **String Parameter**: Name `Stage`, Default `Build`.
   - **Choice Parameter**: Name `env`, Choices (one per line): `Development`, `Staging`, `Production`.
3. **Build Steps > Execute shell**:
```bash
echo "Stage is: $Stage"
echo "Environment is: $env"
```
4. Save > **Build with Parameters** > `env=Staging` > Build.

## 🧪 Verification

Console Output shows both values.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Build with Parameters is missing | Tick **This project is parameterized**. |
| Values are empty in the console | Parameter names are case-sensitive. |
| The choice list is wrong | Put one choice per line. |

## 📸 Screenshot

![Day 72 verification](./screenshots/day72.png)

---
[⬅️ Day 71](../DAY71/task-71-parameterized-job-that-installs-a-package-over-ssh.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 73 ➡️](../DAY73/task-73-scheduled-job-that-copies-apache-logs.md)
