# Day 35: Install Docker CE and the Compose Plugin

| | |
|---|---|
| **Day** | 35 of 100 |
| **Phase** | 3 · Docker |

## 📌 Task

On `<APP_SERVER>` install Docker CE and the Compose plugin; start and enable Docker.

## 🔁 Values to change before you run

Replace each of these with the value from **your** task: `<APP_SERVER>`

## ✅ Solution (copy and paste)

```bash
ssh banner@stapp03
sudo su -

yum install -y yum-utils
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
# (on dnf systems: dnf config-manager --add-repo <same URL>)

yum install -y docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
systemctl enable --now docker
```

## 🧪 Verification

```bash
docker --version
docker compose version
systemctl status docker                # active (running)
docker run --rm hello-world
```

## 🛠️ Common Issues & Fixes

| Issue you may see | Fix |
|---|---|
| `yum-config-manager: command not found` | `yum install -y yum-utils`. |
| Package conflict with runc or podman | Add `--allowerasing` to the install command. |
| `permission denied` on the docker socket | Use `sudo` or run as root. |

## 📸 Screenshot

![Day 35 verification](./screenshots/day35.png)

---
[⬅️ Day 34](../DAY34/task-34-post-update-hook-that-creates-a-release-tag.md) &nbsp;|&nbsp; [🏠 Home](../README.md) &nbsp;|&nbsp; [Day 36 ➡️](../DAY36/task-36-run-an-nginx-container.md)
