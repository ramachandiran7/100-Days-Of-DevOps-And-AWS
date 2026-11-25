# 100 Days of DevOps: KodeKloud Engineer Practice

![Days](https://img.shields.io/badge/Days-100-blue) ![Linux](https://img.shields.io/badge/Linux-FCC624?logo=linux&logoColor=black) ![Git](https://img.shields.io/badge/Git-F05032?logo=git&logoColor=white) ![Docker](https://img.shields.io/badge/Docker-2496ED?logo=docker&logoColor=white) ![Kubernetes](https://img.shields.io/badge/Kubernetes-326CE5?logo=kubernetes&logoColor=white) ![Jenkins](https://img.shields.io/badge/Jenkins-D24939?logo=jenkins&logoColor=white) ![Ansible](https://img.shields.io/badge/Ansible-EE0000?logo=ansible&logoColor=white) ![Terraform](https://img.shields.io/badge/Terraform-7B42BC?logo=terraform&logoColor=white)

**Author:** RAMACHANDIRAN S

One folder per day, one file per task. Each file shows **the task, the solution to copy, how to verify it, and the common issues with their fixes**, so you can find a problem and its fix quickly.

## 📖 How to use a day file

| Section | What it gives you |
|---|---|
| 📌 Task | What the lab asks for |
| 🔁 Values to change | The `<PLACEHOLDERS>` to replace with the values from your own task |
| ✅ Solution | Commands or YAML to copy and paste, in order |
| 🧪 Verification | How to prove it worked (take your screenshot here) |
| 🛠️ Common Issues & Fixes | The errors people hit and what fixes each one |
| 📸 Screenshot | Save your image as `DAYxx/screenshots/dayxx.png` and it appears here |

> **Lab values** (server names, users, ports, file names) change between KodeKloud accounts. Always check the values against your own task. Passwords are never stored in this repo: take them from the lab's "Details of all Users and Servers" page.

## 📊 Progress

**15 / 100 days completed.** Change a row from ⬜ Pending to ✅ Done after you finish and verify that day in your lab.

| Phase | Topic | Days |
|:--:|:--|:--:|
| 1 | Linux Systems & Host Hardening | 1 - 20 |
| 2 | Git Version Control | 21 - 34 |
| 3 | Docker | 35 - 47 |
| 4 | Kubernetes | 48 - 67 |
| 5 | Jenkins CI/CD | 68 - 81 |
| 6 | Ansible | 82 - 93 |
| 7 | Terraform on AWS | 94 - 100 |

## 🗂️ Repository structure

```text
kodekloud-100-days-devops/
├── README.md
├── LICENSE
├── .gitignore
├── DAY01/
│   ├── task-1-create-a-user-with-a-non-interactive-shell.md
│   └── screenshots/
├── DAY02/
│   └── ...
└── DAY100/
    └── task-100-....md
```

## 🗓️ All 100 days

### 🐧 Phase 1: Linux (Days 1 to 20)

| Day | Task | Status |
|:--:|:--|:--:|
| 1 | [Create a User with a Non-Interactive Shell](./DAY01/task-1-create-a-user-with-a-non-interactive-shell.md) | ✅ Done |
| 2 | [Create a Temporary User with an Expiry Date](./DAY02/task-2-create-a-temporary-user-with-an-expiry-date.md) | ✅ Done |
| 3 | [Disable Direct Root SSH Login (all app servers)](./DAY03/task-3-disable-direct-root-ssh-login-all-app-servers.md) | ✅ Done |
| 4 | [Give a Script Executable Permission](./DAY04/task-4-give-a-script-executable-permission.md) | ✅ Done |
| 5 | [Install SELinux Packages and Disable It Permanently](./DAY05/task-5-install-selinux-packages-and-disable-it-permanently.md) | ✅ Done |
| 6 | [Install cronie and Create a Cron Job (all app servers)](./DAY06/task-6-install-cronie-and-create-a-cron-job-all-app-servers.md) | ✅ Done |
| 7 | [Passwordless SSH from thor (jump host) to all app servers](./DAY07/task-7-passwordless-ssh-from-thor-jump-host-to-all-app-servers.md) | ✅ Done |
| 8 | [Install Ansible with pip3 (globally)](./DAY08/task-8-install-ansible-with-pip3-globally.md) | ✅ Done |
| 9 | [Fix MariaDB Service Down](./DAY09/task-9-fix-mariadb-service-down.md) | ✅ Done |
| 10 | [Bash Backup Script (zip + scp with no password)](./DAY10/task-10-bash-backup-script-zip-scp-with-no-password.md) | ✅ Done |
| 11 | [Install Tomcat and Deploy ROOT.war on a Custom Port](./DAY11/task-11-install-tomcat-and-deploy-root-war-on-a-custom-port.md) | ✅ Done |
| 12 | [Fix Apache Not Reachable on a Port (network troubleshooting)](./DAY12/task-12-fix-apache-not-reachable-on-a-port-network.md) | ✅ Done |
| 13 | [iptables on All App Servers (only the LBR may reach Apache)](./DAY13/task-13-iptables-on-all-app-servers-only-the-lbr-may-reach.md) | ✅ Done |
| 14 | [Fix Apache on the Faulty App Server (same port on all)](./DAY14/task-14-fix-apache-on-the-faulty-app-server-same-port-on-all.md) | ✅ Done |
| 15 | [Nginx with a Self-Signed SSL Certificate](./DAY15/task-15-nginx-with-a-self-signed-ssl-certificate.md) | ✅ Done |
| 16 | [Nginx as a Load Balancer (LBR)](./DAY16/task-16-nginx-as-a-load-balancer-lbr.md) | ⬜ Pending |
| 17 | [PostgreSQL User and Database](./DAY17/task-17-postgresql-user-and-database.md) | ⬜ Pending |
| 18 | [LAMP Stack for WordPress](./DAY18/task-18-lamp-stack-for-wordpress.md) | ⬜ Pending |
| 19 | [Apache Serving Two Static Sites on a Custom Port](./DAY19/task-19-apache-serving-two-static-sites-on-a-custom-port.md) | ⬜ Pending |
| 20 | [Nginx + PHP-FPM 8.3 over a Unix Socket](./DAY20/task-20-nginx-php-fpm-8-3-over-a-unix-socket.md) | ⬜ Pending |

### 🔀 Phase 2: Git (Days 21 to 34)

| Day | Task | Status |
|:--:|:--|:--:|
| 21 | [Create a Bare Git Repository](./DAY21/task-21-create-a-bare-git-repository.md) | ⬜ Pending |
| 22 | [Clone a Repository to a Specific Directory](./DAY22/task-22-clone-a-repository-to-a-specific-directory.md) | ⬜ Pending |
| 23 | [Fork a Repository in Gitea (UI task)](./DAY23/task-23-fork-a-repository-in-gitea-ui-task.md) | ⬜ Pending |
| 24 | [Create a Branch from master](./DAY24/task-24-create-a-branch-from-master.md) | ⬜ Pending |
| 25 | [Branch, Commit, Merge and Push](./DAY25/task-25-branch-commit-merge-and-push.md) | ⬜ Pending |
| 26 | [Add a New Git Remote and Push](./DAY26/task-26-add-a-new-git-remote-and-push.md) | ⬜ Pending |
| 27 | [Revert the Latest Commit](./DAY27/task-27-revert-the-latest-commit.md) | ⬜ Pending |
| 28 | [Cherry-Pick One Commit](./DAY28/task-28-cherry-pick-one-commit.md) | ⬜ Pending |
| 29 | [Pull Request Workflow in Gitea (UI task)](./DAY29/task-29-pull-request-workflow-in-gitea-ui-task.md) | ⬜ Pending |
| 30 | [Hard Reset to a Commit and Force-Push](./DAY30/task-30-hard-reset-to-a-commit-and-force-push.md) | ⬜ Pending |
| 31 | [Restore a Stash and Push](./DAY31/task-31-restore-a-stash-and-push.md) | ⬜ Pending |
| 32 | [Rebase a Feature Branch onto master](./DAY32/task-32-rebase-a-feature-branch-onto-master.md) | ⬜ Pending |
| 33 | [Fix a Rejected Push (typo + rebase conflict)](./DAY33/task-33-fix-a-rejected-push-typo-rebase-conflict.md) | ⬜ Pending |
| 34 | [post-update Hook that Creates a Release Tag](./DAY34/task-34-post-update-hook-that-creates-a-release-tag.md) | ⬜ Pending |

### 🐳 Phase 3: Docker (Days 35 to 47)

| Day | Task | Status |
|:--:|:--|:--:|
| 35 | [Install Docker CE and the Compose Plugin](./DAY35/task-35-install-docker-ce-and-the-compose-plugin.md) | ⬜ Pending |
| 36 | [Run an Nginx Container](./DAY36/task-36-run-an-nginx-container.md) | ⬜ Pending |
| 37 | [Copy a File into a Running Container](./DAY37/task-37-copy-a-file-into-a-running-container.md) | ⬜ Pending |
| 38 | [Pull an Image and Re-tag It](./DAY38/task-38-pull-an-image-and-re-tag-it.md) | ⬜ Pending |
| 39 | [Create an Image from a Container](./DAY39/task-39-create-an-image-from-a-container.md) | ⬜ Pending |
| 40 | [Install and Configure Apache Inside a Container](./DAY40/task-40-install-and-configure-apache-inside-a-container.md) | ⬜ Pending |
| 41 | [Write a Dockerfile (Ubuntu 24.04 + Apache on a custom port)](./DAY41/task-41-write-a-dockerfile-ubuntu-24-04-apache-on-a-custom-port.md) | ⬜ Pending |
| 42 | [Create a Docker macvlan Network](./DAY42/task-42-create-a-docker-macvlan-network.md) | ⬜ Pending |
| 43 | [Container with Port Mapping](./DAY43/task-43-container-with-port-mapping.md) | ⬜ Pending |
| 44 | [Docker Compose for httpd with a Bind Mount](./DAY44/task-44-docker-compose-for-httpd-with-a-bind-mount.md) | ⬜ Pending |
| 45 | [Fix a Broken Dockerfile](./DAY45/task-45-fix-a-broken-dockerfile.md) | ⬜ Pending |
| 46 | [Docker Compose Multi-Service Stack (PHP + MariaDB)](./DAY46/task-46-docker-compose-multi-service-stack-php-mariadb.md) | ⬜ Pending |
| 47 | [Dockerize a Python App](./DAY47/task-47-dockerize-a-python-app.md) | ⬜ Pending |

### ☸️ Phase 4: Kubernetes (Days 48 to 67)

| Day | Task | Status |
|:--:|:--|:--:|
| 48 | [Create a Pod](./DAY48/task-48-create-a-pod.md) | ⬜ Pending |
| 49 | [Create a Deployment](./DAY49/task-49-create-a-deployment.md) | ⬜ Pending |
| 50 | [Pod with Resource Requests and Limits](./DAY50/task-50-pod-with-resource-requests-and-limits.md) | ⬜ Pending |
| 51 | [Rolling Update](./DAY51/task-51-rolling-update.md) | ⬜ Pending |
| 52 | [Roll Back a Deployment](./DAY52/task-52-roll-back-a-deployment.md) | ⬜ Pending |
| 53 | [Fix an Nginx + PHP-FPM Pod](./DAY53/task-53-fix-an-nginx-php-fpm-pod.md) | ⬜ Pending |
| 54 | [Two Containers Sharing a Volume](./DAY54/task-54-two-containers-sharing-a-volume.md) | ⬜ Pending |
| 55 | [Sidecar Container for Logs](./DAY55/task-55-sidecar-container-for-logs.md) | ⬜ Pending |
| 56 | [Deployment + NodePort Service](./DAY56/task-56-deployment-nodeport-service.md) | ⬜ Pending |
| 57 | [Pod with Environment Variables](./DAY57/task-57-pod-with-environment-variables.md) | ⬜ Pending |
| 58 | [Grafana Deployment + NodePort](./DAY58/task-58-grafana-deployment-nodeport.md) | ⬜ Pending |
| 59 | [Fix a Redis Deployment](./DAY59/task-59-fix-a-redis-deployment.md) | ⬜ Pending |
| 60 | [PV + PVC + Pod + NodePort Service](./DAY60/task-60-pv-pvc-pod-nodeport-service.md) | ⬜ Pending |
| 61 | [Init Container](./DAY61/task-61-init-container.md) | ⬜ Pending |
| 62 | [Secret from a File Mounted in a Pod](./DAY62/task-62-secret-from-a-file-mounted-in-a-pod.md) | ⬜ Pending |
| 63 | [Iron Gallery App (namespace, 2 deployments, 2 services)](./DAY63/task-63-iron-gallery-app-namespace-2-deployments-2-services.md) | ⬜ Pending |
| 64 | [Fix a Python Flask Deployment and Service](./DAY64/task-64-fix-a-python-flask-deployment-and-service.md) | ⬜ Pending |
| 65 | [Redis with a ConfigMap and Volumes](./DAY65/task-65-redis-with-a-configmap-and-volumes.md) | ⬜ Pending |
| 66 | [MySQL with PV, PVC, Secrets and NodePort](./DAY66/task-66-mysql-with-pv-pvc-secrets-and-nodeport.md) | ⬜ Pending |
| 67 | [Guestbook App (Redis master, Redis slave, frontend)](./DAY67/task-67-guestbook-app-redis-master-redis-slave-frontend.md) | ⬜ Pending |

### 🔧 Phase 5: Jenkins (Days 68 to 81)

| Day | Task | Status |
|:--:|:--|:--:|
| 68 | [Set Up a Jenkins Server](./DAY68/task-68-set-up-a-jenkins-server.md) | ⬜ Pending |
| 69 | [Install Jenkins Plugins](./DAY69/task-69-install-jenkins-plugins.md) | ⬜ Pending |
| 70 | [Create a Jenkins User and Set Matrix Authorization](./DAY70/task-70-create-a-jenkins-user-and-set-matrix-authorization.md) | ⬜ Pending |
| 71 | [Parameterized Job that Installs a Package over SSH](./DAY71/task-71-parameterized-job-that-installs-a-package-over-ssh.md) | ⬜ Pending |
| 72 | [Parameterized Job (string + choice)](./DAY72/task-72-parameterized-job-string-choice.md) | ⬜ Pending |
| 73 | [Scheduled Job that Copies Apache Logs](./DAY73/task-73-scheduled-job-that-copies-apache-logs.md) | ⬜ Pending |
| 74 | [Database Backup Job](./DAY74/task-74-database-backup-job.md) | ⬜ Pending |
| 75 | [Add SSH Slave Nodes](./DAY75/task-75-add-ssh-slave-nodes.md) | ⬜ Pending |
| 76 | [Project-Based Matrix Authorization on a Job](./DAY76/task-76-project-based-matrix-authorization-on-a-job.md) | ⬜ Pending |
| 77 | [Jenkins Pipeline that Deploys Code from Gitea](./DAY77/task-77-jenkins-pipeline-that-deploys-code-from-gitea.md) | ⬜ Pending |
| 78 | [Conditional Pipeline (branch parameter)](./DAY78/task-78-conditional-pipeline-branch-parameter.md) | ⬜ Pending |
| 79 | [Auto-Deploy on Every Gitea Push](./DAY79/task-79-auto-deploy-on-every-gitea-push.md) | ⬜ Pending |
| 80 | [Chained Builds (upstream then downstream)](./DAY80/task-80-chained-builds-upstream-then-downstream.md) | ⬜ Pending |
| 81 | [Multistage Pipeline (Deploy + Test)](./DAY81/task-81-multistage-pipeline-deploy-test.md) | ⬜ Pending |

### 📦 Phase 6: Ansible (Days 82 to 93)

| Day | Task | Status |
|:--:|:--|:--:|
| 82 | [Create an INI Inventory](./DAY82/task-82-create-an-ini-inventory.md) | ⬜ Pending |
| 83 | [Fix the Inventory and Create a Playbook (create a file)](./DAY83/task-83-fix-the-inventory-and-create-a-playbook-create-a-file.md) | ⬜ Pending |
| 84 | [Copy a File to All App Servers](./DAY84/task-84-copy-a-file-to-all-app-servers.md) | ⬜ Pending |
| 85 | [Create a File with Dynamic Ownership](./DAY85/task-85-create-a-file-with-dynamic-ownership.md) | ⬜ Pending |
| 86 | [Passwordless SSH for Ansible](./DAY86/task-86-passwordless-ssh-for-ansible.md) | ⬜ Pending |
| 87 | [Install a Package on All App Servers](./DAY87/task-87-install-a-package-on-all-app-servers.md) | ⬜ Pending |
| 88 | [Deploy httpd with blockinfile](./DAY88/task-88-deploy-httpd-with-blockinfile.md) | ⬜ Pending |
| 89 | [Install, Start and Enable httpd](./DAY89/task-89-install-start-and-enable-httpd.md) | ⬜ Pending |
| 90 | [Files with ACLs](./DAY90/task-90-files-with-acls.md) | ⬜ Pending |
| 91 | [httpd + lineinfile (prepend a line)](./DAY91/task-91-httpd-lineinfile-prepend-a-line.md) | ⬜ Pending |
| 92 | [Ansible Role with a Jinja2 Template](./DAY92/task-92-ansible-role-with-a-jinja2-template.md) | ⬜ Pending |
| 93 | [Conditionals (`when`)](./DAY93/task-93-conditionals-when.md) | ⬜ Pending |

### ☁️ Phase 7: Terraform (Days 94 to 100)

| Day | Task | Status |
|:--:|:--|:--:|
| 94 | [Create a VPC](./DAY94/task-94-create-a-vpc.md) | ⬜ Pending |
| 95 | [Create a Security Group in the Default VPC](./DAY95/task-95-create-a-security-group-in-the-default-vpc.md) | ⬜ Pending |
| 96 | [EC2 Instance with an RSA Key Pair](./DAY96/task-96-ec2-instance-with-an-rsa-key-pair.md) | ⬜ Pending |
| 97 | [IAM Read-Only Policy for EC2](./DAY97/task-97-iam-read-only-policy-for-ec2.md) | ⬜ Pending |
| 98 | [EC2 in a Private VPC Subnet (variables, tfvars, outputs)](./DAY98/task-98-ec2-in-a-private-vpc-subnet-variables-tfvars-outputs.md) | ⬜ Pending |
| 99 | [DynamoDB Table + IAM Role + Read-Only Policy](./DAY99/task-99-dynamodb-table-iam-role-read-only-policy.md) | ⬜ Pending |
| 100 | [EC2 + CloudWatch CPU Alarm to an Existing SNS Topic](./DAY100/task-100-ec2-cloudwatch-cpu-alarm-to-an-existing-sns-topic.md) | ⬜ Pending |

## 🙏 Credits

- Labs and tasks: [KodeKloud Engineer](https://kodekloud.com/)
- Folder layout inspired by [MiqdadProjects/kodekloud-eng-100-days-devops](https://github.com/MiqdadProjects/kodekloud-eng-100-days-devops) (MIT). The write-ups in this repo are my own.

## 📄 License

MIT. See [LICENSE](./LICENSE).
