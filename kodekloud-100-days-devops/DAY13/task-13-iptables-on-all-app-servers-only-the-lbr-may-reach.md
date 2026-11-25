# Day 13: iptables on All App Servers (only the LBR may reach Apache)

| | |
|---|---|
| **Day** | 13 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

Install iptables on all app servers. Block `<PORT>` for everyone except the load balancer `<LBR_IP>`. Rules must survive reboot.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<LBR_IP>` `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# Find the LBR IP (from jump host)
getent hosts stlb01

# On EACH app server (stapp01, stapp02, stapp03)
ssh <SUDO_USER>@<STAPP>
sudo su -
yum install -y iptables iptables-services
systemctl enable --now iptables

# Order matters: ACCEPT first, DROP second
iptables -I INPUT 1 -p tcp -s <LBR_IP> --dport <PORT> -j ACCEPT
iptables -I INPUT 2 -p tcp --dport <PORT> -j DROP

# Persist
service iptables save || iptables-save > /etc/sysconfig/iptables
```

## 🧪 Verification

```bash
iptables -L INPUT -n --line-numbers        # ACCEPT on line 1, DROP on line 2
cat /etc/sysconfig/iptables | grep <PORT>
# From jump host (not the LBR): should hang / fail
curl -m 5 http://<STAPP>:<PORT>
# From the LBR: should work
ssh loki@stlb01 "curl -m 5 http://<STAPP>:<PORT>"
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Rules are gone after reboot | They were not saved. Run `service iptables save`. |
| The load balancer is blocked too | ACCEPT must sit above DROP. Check `iptables -L INPUT -n --line-numbers`. |
| `iptables: command not found` | `yum install -y iptables iptables-services`. |

## 💡 Notes

do not touch the SSH rule or you will lock yourself out.

## 📸 Screenshot

![Day 13 verification](./screenshots/day13.png)

---
[⬅️ Day 12](../DAY12/task-12-fix-apache-not-reachable-on-a-port-network.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 14 ➡️](../DAY14/task-14-fix-apache-on-the-faulty-app-server-same-port-on-all.md)
