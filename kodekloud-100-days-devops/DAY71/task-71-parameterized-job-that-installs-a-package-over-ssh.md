# Day 71: Parameterized Job that Installs a Package over SSH

| | |
|---|---|
| **Day** | 71 of 100 |
| **Phase** | 5 · Jenkins |

## 📌 Task

Freestyle job `install-packages`, string parameter `PACKAGE`, installs `$PACKAGE` on `ststor01`. Test with `nginx` and `git`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<NATASHA_PASSWORD>`

## ✅ Solution (copy and paste)

```bash
# Prep: make sure natasha can run sudo with the lab password, and note the password
```
1. **Manage Jenkins > Plugins**: install **SSH** (or **Publish Over SSH**) and **SSH Credentials**. Restart.
2. **Manage Jenkins > Credentials > System > Global > Add Credentials**
   - Kind: Username with password (or SSH private key)
   - Username: `natasha`, Password: from the lab page, ID: `ststor01-ssh`
3. **New Item** > name `install-packages` > **Freestyle project** > OK.
4. Tick **This project is parameterized** > Add Parameter > **String Parameter**
   - Name: `PACKAGE`
5. **Build Steps > Add build step > Execute shell script on remote host using ssh**
   - SSH site: `natasha@ststor01:22` (add the host in **Manage Jenkins > System > SSH remote hosts** if it is not listed; Credentials = `ststor01-ssh`)
   - Command:
```bash
echo '<NATASHA_PASSWORD>' | sudo -S yum install -y $PACKAGE
```
6. Save. **Build with Parameters** > `nginx`, then again with `git`.

## 🧪 Verification

Console Output ends with `Finished: SUCCESS`; on the server run `rpm -q nginx git`.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `$PACKAGE` is empty | The parameter name must be exactly `PACKAGE`. |
| SSH authentication fails | Check the credentials username and password, and test the host in System settings. |
| `sudo` asks for a password | Feed it to `sudo -S` as shown in the solution. |

## 📸 Screenshot

![Day 71 verification](./screenshots/day71.png)

---
[⬅️ Day 70](../DAY70/task-70-create-a-jenkins-user-and-set-matrix-authorization.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 72 ➡️](../DAY72/task-72-parameterized-job-string-choice.md)
