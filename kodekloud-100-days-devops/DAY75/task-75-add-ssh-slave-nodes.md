# Day 75: Add SSH Slave Nodes

| | |
|---|---|
| **Day** | 75 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Add `stapp01/02/03` as SSH agent nodes named `App_server_1/2/3` with labels `stapp01/02/03`.

## ✅ Solution (copy and paste)

```bash
# Each app server needs Java first
ssh tony@stapp01  "sudo yum install -y java-17-openjdk"
ssh steve@stapp02 "sudo yum install -y java-17-openjdk"
ssh banner@stapp03 "sudo yum install -y java-17-openjdk"
```
1. **Manage Jenkins > Credentials > Global > Add**: one entry per server (Username with password: `tony`, `steve`, `banner`; IDs `stapp01-cred` etc.).
2. **Manage Jenkins > Nodes > New Node**
   - Name `App_server_1`, type **Permanent Agent**
   - Remote root directory: `/home/tony/jenkins` (a folder the user can write)
   - Labels: `stapp01`
   - Usage: Use this node as much as possible
   - Launch method: **Launch agents via SSH**, Host `stapp01`, Credentials `stapp01-cred`
   - Host Key Verification Strategy: **Non verifying Verification Strategy**
   - Save
3. Repeat for `App_server_2` (`stapp02`, steve) and `App_server_3` (`stapp03`, banner).

## 🧪 Verification

**Nodes** page shows all three online (no red cross). Click a node > **Log** says "Agent successfully connected".

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Agent offline | Install Java on the server and check the credentials and remote directory. |
| Host key error | Choose **Non verifying Verification Strategy**. |
| Permission denied on the remote directory | Use a directory the user owns, for example `/home/tony/jenkins`. |

## 📸 Screenshot

![Day 75 verification](./screenshots/day75.png)

---
[⬅️ Day 74](../DAY74/task-74-database-backup-job.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 76 ➡️](../DAY76/task-76-project-based-matrix-authorization-on-a-job.md)
