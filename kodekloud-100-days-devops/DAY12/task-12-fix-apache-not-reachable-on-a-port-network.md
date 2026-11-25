# Day 12: Fix Apache Not Reachable on a Port (network troubleshooting)

| | |
|---|---|
| **Day** | 12 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Apache on `<APP_SERVER>` is not reachable on port `<PORT>`. Find and fix it, without weakening security.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>` `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# 1. From jump host: confirm the symptom
curl -I http://<STAPP>:<PORT>
telnet <STAPP> <PORT>                # (or: nc -zv <STAPP> <PORT>)

# 2. On the server
ssh <SUDO_USER>@<STAPP>
sudo su -
systemctl status httpd
grep -n '^Listen' /etc/httpd/conf/httpd.conf     # must be: Listen <PORT>
httpd -t                                          # config syntax OK?
ss -tulnp | grep <PORT>                           # who holds the port?
```

### Fix whichever applies
```bash
# A) Another service holds the port (often sendmail/postfix)
systemctl stop sendmail && systemctl disable sendmail

# B) Wrong Listen line
sed -i 's/^Listen .*/Listen <PORT>/' /etc/httpd/conf/httpd.conf

# C) Apache simply stopped
systemctl enable --now httpd

# D) Firewall blocks the port: ADD a rule, do not flush the firewall
iptables -L INPUT -n --line-numbers
iptables -I INPUT -p tcp --dport <PORT> -j ACCEPT
iptables-save > /etc/sysconfig/iptables    # make it persistent
```

## 🧪 Verification

**from jump host:**

```bash
curl -I http://<STAPP>:<PORT>              # HTTP/1.1 200 OK
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `Connection refused` | Apache is stopped. `systemctl enable --now httpd`. |
| httpd fails with `Address already in use` | Another service owns the port. Stop and disable it (often sendmail). |
| Works on the server, fails from the jump host | Firewall. Insert an ACCEPT rule for the port and save the rules. |

## 💡 Notes

`-I` inserts at the top so the rule lands above any REJECT rule.

## 📸 Screenshot

![Day 12 verification](./screenshots/day12.png)

---
[⬅️ Day 11](../DAY11/task-11-install-tomcat-and-deploy-root-war-on-a-custom-port.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 13 ➡️](../DAY13/task-13-iptables-on-all-app-servers-only-the-lbr-may-reach.md)
