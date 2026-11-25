# Day 17: PostgreSQL User and Database

| | |
|---|---|
| **Day** | 17 of 100 |
| **Phase** | 1 · Linux |

## 📌 Task

On `stdb01` create database user `<DB_USER>` / password `<DB_PASS>`, create `<DB_NAME>`, grant all privileges. Do not restart PostgreSQL.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<DB_NAME>` `<DB_PASS>` `<DB_USER>`

## ✅ Solution (copy and paste)

```bash
ssh peter@stdb01
sudo su -
sudo -u postgres psql
```
```sql
CREATE USER <DB_USER> WITH PASSWORD '<DB_PASS>';
CREATE DATABASE <DB_NAME>;
GRANT ALL PRIVILEGES ON DATABASE <DB_NAME> TO <DB_USER>;
\l
\du
\q
```

## 🧪 Verification

`\l` lists the database; `\du` lists the user.

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| Cannot connect with `psql` | Use `sudo -u postgres psql`. |
| `role already exists` | It exists. Use `ALTER USER <DB_USER> WITH PASSWORD '<DB_PASS>';`. |
| SQL syntax error | Every statement ends with `;` and the password is in single quotes. |

## 💡 Notes

do not restart the service. Quote the password with single quotes.

## 📸 Screenshot

![Day 17 verification](./screenshots/day17.png)

---
[⬅️ Day 16](../DAY16/task-16-nginx-as-a-load-balancer-lbr.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 18 ➡️](../DAY18/task-18-lamp-stack-for-wordpress.md)
