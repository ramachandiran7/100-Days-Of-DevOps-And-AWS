# Day 11: Install Tomcat and Deploy ROOT.war on a Custom Port

| | |
|---|---|
| **Day** | 11 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Install Tomcat on `<APP_SERVER>`, run on port `<PORT>`, deploy `/tmp/ROOT.war` from the jump host, test `http://<STAPP>:<PORT>`.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# 1. FROM JUMP HOST: copy the WAR
scp /tmp/ROOT.war <SUDO_USER>@<STAPP>:/tmp/

# 2. On the app server
ssh <SUDO_USER>@<STAPP>
sudo su -
yum install -y tomcat

# 3. Change the HTTP connector port (the AJP connector 8009 stays untouched)
grep -n 'Connector port' /etc/tomcat/server.xml
sed -i 's/Connector port="8080"/Connector port="<PORT>"/' /etc/tomcat/server.xml

# 4. Deploy as the root app
rm -rf /usr/share/tomcat/webapps/ROOT*
cp /tmp/ROOT.war /usr/share/tomcat/webapps/ROOT.war

# 5. Start
systemctl enable --now tomcat
sleep 10
ls /usr/share/tomcat/webapps         # a ROOT/ folder appears = deployed
```

## 🧪 Verification

**from jump host:**

```bash
curl http://<STAPP>:<PORT>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Blank page or 404 | The old `ROOT` folder is still there. Remove `/usr/share/tomcat/webapps/ROOT*`, copy the WAR again, restart Tomcat. |
| Still answers on 8080 | `sed` did not match. Run `grep -n 'Connector port' /etc/tomcat/server.xml` and edit by hand. |
| `Connection refused` | `systemctl status tomcat`, then `ss -tlnp` to confirm the port. |

## 💡 Notes

if curl fails, check `systemctl status tomcat` and `ss -tlnp | grep <PORT>`.

## 📸 Screenshot

![Day 11 verification](./screenshots/day11.png)

---
[⬅️ Day 10](../DAY10/task-10-bash-backup-script-zip-scp-with-no-password.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 12 ➡️](../DAY12/task-12-fix-apache-not-reachable-on-a-port-network.md)
