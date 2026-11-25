# Day 29: Pull Request Workflow in Gitea (UI task)

| | |
|---|---|
| **Day** | 29 of 100 |
| **Phase** | 2 · Git |

## 📌 Task

A PR is needed for `<BRANCH>` into `master`. Assign `<REVIEWER>` as reviewer, review and merge via the UI.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<BRANCH>` `<NAME>` `<REVIEWER>`

## ✅ Solution (copy and paste)

1. Gitea UI > log in as the **author** (e.g. `max`).
2. Open the repo > **Pull Requests** > **New Pull Request**.
3. Base = `master`, Compare = `<BRANCH>`.
4. Title exactly as the task states, e.g. `Added story-<NAME>`. Click **Create Pull Request**.
5. On the PR page: **Reviewers** (right side) > select `<REVIEWER>` (e.g. `tom`).
6. Sign out. Log in as the **reviewer** (e.g. `tom`).
7. Open the PR > **Files Changed** > **Review** > Approve > Submit.
8. Click **Merge Pull Request** > confirm.

## 🧪 Verification

📸 Screenshot: the merged PR page.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Cannot pick a reviewer | The reviewer needs access to the repo in Gitea. |
| The author cannot approve | Log out and approve as the reviewer. |
| Wrong PR title | Edit it with the exact text from the task. |

## 📸 Screenshot

![Day 29 verification](./screenshots/day29.png)

---
[⬅️ Day 28](../DAY28/task-28-cherry-pick-one-commit.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 30 ➡️](../DAY30/task-30-hard-reset-to-a-commit-and-force-push.md)
