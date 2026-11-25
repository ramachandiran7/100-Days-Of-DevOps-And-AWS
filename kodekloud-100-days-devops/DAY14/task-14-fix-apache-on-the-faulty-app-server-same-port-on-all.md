# Day 14: Fix Apache on the Faulty App Server (same port on all)

| | |
|---|---|
| **Day** | 14 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

One app server's Apache is down. Make Apache run on port `<PORT>` on all app servers.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<PORT>` `<STAPP>` `<SUDO_USER>`

## ✅ Solution (copy and paste)

```bash
# 1. From jump host: find the broken one
curl -I http://stapp01:<PORT>
curl -I http://stapp02:<PORT>
curl -I http://stapp03:<PORT>

# 2. On the failing server
ssh <SUDO_USER>@<STAPP>
sudo su -
systemctl status httpd
journalctl -xeu httpd | tail -30
httpd -t                                           # config errors
grep -n '^Listen' /etc/httpd/conf/httpd.conf
ss -tlnp | grep <PORT>                             # port conflict?

# 3. Fixes
sed -i 's/^Listen .*/Listen <PORT>/' /etc/httpd/conf/httpd.conf
systemctl stop sendmail 2>/dev/null; systemctl disable sendmail 2>/dev/null   # if it holds the port
systemctl enable --now httpd
systemctl restart httpd
```

## 🧪 Verification

```bash
curl -I http://stapp01:<PORT>; curl -I http://stapp02:<PORT>; curl -I http://stapp03:<PORT>
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `httpd -t` reports a syntax error | Fix the line it names, then restart. |
| `Address already in use` | Stop the conflicting service. Avoid `kill -9` on managed services. |
| Other servers use a different port | Check `grep ^Listen /etc/httpd/conf/httpd.conf` on all three. |

## 💡 Notes

prefer `systemctl stop <service>` over `kill -9`. Check the other two servers also listen on `<PORT>`.

## 📸 Screenshot

![Day 14 verification](./screenshots/day14.png)

---
[⬅️ Day 13](../DAY13/task-13-iptables-on-all-app-servers-only-the-lbr-may-reach.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 15 ➡️](../DAY15/task-15-nginx-with-a-self-signed-ssl-certificate.md)
