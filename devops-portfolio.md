# 100 Days of Advanced DevOps Engineering
**Engineer:** RAMACHANDIRAN S | **Status:** Active Practice | **Target Position:** DevOps / Infrastructure Engineer

> **Daily update:** After completing a module, update its status, add the commands/configuration you used, record the result, and place screenshots in `screenshots/` using the matching day filename.

---

## 📊 Phase-Wise Progress Dashboard

| Phase  | Modules & Core Technologies                 | Target Horizon | Status                          |
| :---   | :---                                        | :---           | :---                            |
| **01** | Linux Systems & Host Hardening              | Days 01 - 20   | 🔄 In Progress (Days 1-2 Done) |
| **02** | Git Version Control & Distributed Workflows | Days 21 - 34   | ⏳ Pending                     |
| **03** | Docker Containerization & Microservices     | Days 35 - 47   | ⏳ Pending                     |
| **04** | Kubernetes Cluster Orchestration            | Days 48 - 67   | ⏳ Pending                     |
| **05** | Jenkins CI/CD Automation Pipelines 	       | Days 68 - 81   | ⏳ Pending                     |
| **06** | Advanced Ansible Configuration Management   | Days 82 - 93   | ⏳ Pending                     |
| **07** | Infrastructure as Code (IaC) via Terraform  | Days 94 - 100  | ⏳ Pending                     |

---

## 💻 Technical Execution Log

### 🛡️ Phase 1: Linux Systems & Host Hardening (Days 1 - 20)

#### Day 1: Linux User Setup with Non-Interactive Shell
- **Objective:** Provision an automation service account blocked from interactive terminal access.
- **Execution:**
  ```bash
  sudo useradd -s /usr/sbin/nologin deploy_user
  ```
- **Security Value:** Prevents interactive command-line hijacking if service credentials leak.
- **Verification:** ![Day 1 Verification](./screenshots/devops-day01.png)

#### Day 2: Temporary User Setup with Expiry
- **Objective:** Provision a time-bound contractor user account configured to auto-expire.
- **Execution:**
  ```bash
  sudo useradd -e 2026-11-10 contractor_user
  ```
- **Security Value:** Automatically mitigates compliance risks linked to stale, orphaned, or forgotten accounts.
- **Verification:** ![Day 2 Verification](./screenshots/devops-day02.png)

#### Day 3: Secure Root SSH Access
- **Objective:** Disable direct root user login over SSH to prevent automated brute-force entry attempts.
- **Execution:**
1. Open the SSH configuration file
 ```bash
sudo vi /etc/ssh/sshd_config
 ```
2. Uncomment and update the line to:text
PermitRootLogin no
3. Restart the SSH service to apply changes
 ```bash
sudo systemctl restart sshd
 ```
- **Security Value:** Enforces the use of standard users with explicit escalation privileges, shielding administrative vectors.
- **Verification:** ![Day 3 Verification](./screenshots/devops-day03.png)

#### Day 4: Script Execution Permissions
- **Objective:** Securely assign appropriate filesystem execution bits to automated infrastructure scripts.
- **Execution:**
  ```bash
  sudo chmod 755 /tmp/xfusioncorp.sh
  ```
- **Security Value:** Restricts administrative file execution privileges exclusively to authorized identity contexts.
- **Verification:** ![Day 4 Verification](./screenshots/devops-day04.png)

#### Day 5: SELinux Installation and Configuration
- **Objective:** Deploy and enforce host-level Mandatory Access Control (MAC) security boundaries.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Confines rogue process interactions even if underlying web applications are compromised.
- **Verification:** ![Day 5 Verification](./screenshots/devops-day05.png)

#### Day 6: Create a Cron Job
- **Objective:** Configure recurring automated background runtime operations using the crontab scheduler.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Standardizes regular host execution patterns for updates, log rotations, and cleanups.
- **Verification:** ![Day 6 Verification](./screenshots/devops-day06.png)

#### Day 7: Linux SSH Authentication
- **Objective:** Replace legacy password access with robust, asymmetric cryptographic key authentication.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Eliminates the possibility of password cracking vectors across exposed network interfaces.
- **Verification:** ![Day 7 Verification](./screenshots/devops-day07.png)

#### Day 8: Install Ansible
- **Objective:** Deploy the agentless orchestration and configuration engine on a centralized control node.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Enables declarative system configuration validation and uniform fleet state parity.
- **Verification:** ![Day 8 Verification](./screenshots/devops-day08.png)

#### Day 9: MariaDB Troubleshooting
- **Objective:** Diagnose and rectify operational blocks, query deadlocks, and relational connection errors.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Restores business high availability models and protects local database storage engines under load stress.
- **Verification:** ![Day 9 Verification](./screenshots/devops-day09.png)

#### Day 10: Linux Bash Scripts
- **Objective:** Construct functional shell programs containing explicit logic handling and error capturing mechanisms.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Minimizes human administrative mistakes during cluster operations via rule-based automation scripts.
- **Verification:** ![Day 10 Verification](./screenshots/devops-day10.png)

#### Day 11: Install and Configure Tomcat Server
- **Objective:** Deploy, secure, and optimize the Java servlet web application execution runtime.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Implements minimum necessary privilege structures for production application container environments.
- **Verification:** ![Day 11 Verification](./screenshots/devops-day11.png)

#### Day 12: Linux Network Services
- **Objective:** Interrogate, monitor, and isolate core host networking interface parameters and route ports.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Surfaces active network processing listeners to rapidly block hidden, unapproved communication backdoors.
- **Verification:** ![Day 12 Verification](./screenshots/devops-day12.png)

#### Day 13: IPtables Installation And Configuration
- **Objective:** Implement stateful firewall rule matrices at the host level to filter unexpected network traffic.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Anchors an initial defense-in-depth perimeter directly inside the operating system kernel.
- **Verification:** ![Day 13 Verification](./screenshots/devops-day13.png)

#### Day 14: Linux Process Troubleshooting
- **Objective:** Analyze system calls, trace runaway computations, and mitigate Out-Of-Memory (OOM) crashing events.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Sustains host system availability parameters against computing resource starvation metrics.
- **Verification:** ![Day 14 Verification](./screenshots/devops-day14.png)

#### Day 15: Setup SSL for Nginx
- **Objective:** Bind Transport Layer Security (TLS/SSL) certificates to active web reverse proxy engines.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Encrypts external client-to-server traffic streams, protecting sensitive payload records from network sniffing.
- **Verification:** ![Day 15 Verification](./screenshots/devops-day15.png)

#### Day 16: Install and Configure Nginx as an LBR
- **Objective:** Deploy an application proxy layer optimized to distribute operational load patterns across clusters.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Masks upstream app server infrastructure configurations cleanly from direct internet connections.
- **Verification:** ![Day 16 Verification](./screenshots/devops-day16.png)

#### Day 17: Install and Configure PostgreSQL
- **Objective:** Deploy, secure, and validate a relational object database server topology.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Hardens corporate data backends using strict access access control matching at the engine layer.
- **Verification:** ![Day 17 Verification](./screenshots/devops-day17.png)

#### Day 18: Install and Configure DB Server
- **Objective:** Apply secure foundational database access controls to lock down administrative connections.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Assures granular local socket access configurations are rigorously enforced across environments.
- **Verification:** ![Day 18 Verification](./screenshots/devops-day18.png)

#### Day 19: Install and Configure Web Application
- **Objective:** Orchestrate multi-tier application stacks across defined network and file dependencies.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Confirms least-privilege matrix controls function cleanly across interconnected software layers.
- **Verification:** ![Day 19 Verification](./screenshots/devops-day19.png)

#### Day 20: Configure Nginx + PHP-FPM Using Unix Sock
- **Objective:** Link processing runtimes together using Unix Domain Sockets rather than standard TCP loopback paths.
- **Execution:**
  ```bash
  
  ```
- **Security Value:** Restricts application inter-process communications entirely to internal, localized host boundaries.
- **Verification:** ![Day 20 Verification](./screenshots/devops-day20.png)

---

### 🌿 Phase 2: Git Version Control & Distributed Workflows (Days 21 - 34)

#### Day 21: Set Up Git Repository on Storage Server
- **Objective:** Initialize central version tracking frameworks to record architectural changes securely.
- Execution:
  ```bash
  ```
- Security Value: Establishes an unalterable version history log for infrastructure configuration auditing.
- Verification: ![Day 21 Verification](./screenshots/devops-day21.png)
#### Day 22: Clone Git Repository on Storage Server

- Objective: Distribute tracking workspaces downward to individual engineering execution environments.
- Execution:
  ```bash
  ```
- Security Value: Guarantees cryptographic tracing of code state differences via distinct, historical commit logs.
- Verification: ![Day 22 Verification](./screenshots/devops-day22.png)
#### Day 23: Fork a Git Repository

- Objective: Clone upstream application paths into isolated sandboxes for modifications.
- Execution:
  ```bash
  ```
- Security Value: Completely shields the primary target production codebase from experimental script drift.
- Verification: ![Day 23 Verification](./screenshots/devops-day23.png)
#### Day 24: Git Create Branches

- Objective: Isolate software development streams using decoupled branch workspaces.
- Execution:
  ```bash
  ```
- Security Value: Separates stable, production-ready code paths from active feature engineering work.
- Verification: ![Day 24 Verification](./screenshots/devops-day24.png)
#### Day 25: Git Merge Branches

- Objective: Integrate verified modification pathways back into the parent application workspace.
- Execution:
  ```bash
  ```
- Security Value: Ensures strict code gating checks are completed before merging scripts into deployment lines.
- Verification: ![Day 25 Verification](./screenshots/devops-day25.png)
#### Day 26: Git Manage Remotes

- Objective: Configure multi-tenant upstream and downstream target definitions for deployment synchronization.
- Execution:
  ```bash
  ```
- Security Value: Prevents misconfigurations from pushing sensitive code modules to unapproved public hosts.
- Verification: ![Day 26 Verification](./screenshots/devops-day26.png)
#### Day 27: Git Revert Some Changes

- Objective: Undo previous configurations safely by committing an automated inverse rollback state.
- Execution:
  ```bash
  ```
- Security Value: Provides a zero-downtime path to quickly fix production system errors.
- Verification: ![Day 27 Verification](./screenshots/devops-day27.png)
#### Day 28: Git Cherry Pick

- Objective: Extract target architectural commits across divergent configuration states with high precision.
- Execution:
  ```bash
  ```
- Security Value: Accelerates targeted patch management procedures into live target environments.
- Verification: ![Day 28 Verification](./screenshots/devops-day28.png)
#### Day 29: Manage Git Pull Requests

- Objective: Execute full peer review code gates regulating integration patterns into main tracks.
- Execution:
  ```bash
  ```
- Security Value: Enforces dual-authorization review models preventing single-point insider threats.
- Verification: ![Day 29 Verification](./screenshots/devops-day29.png)
#### Day 30: Git hard reset

- Objective: Clean configuration corruption states immediately back to a known-good index point.
- Execution:
  ```bash
  ```
- Security Value: Purges unsanctioned code configurations rapidly from active staging nodes.
- Verification: ![Day 30 Verification](./screenshots/devops-day30.png)
#### Day 31: Git Stash

- Objective: Temporarily shelf incomplete local changes to rapidly handle priority system context switches.
- Execution:
  ```bash
  ```
- Security Value: Preserves unstable internal scripts without muddying formal system log states.
- Verification: ![Day 31 Verification](./screenshots/devops-day31.png)
#### Day 32: Git Rebase

- Objective: Linearly restructure development history tracks to maintain clean tracking trails.
- Execution:
  ```bash
  ```
- Security Value: Simplifies audit histories, allowing clear tracking of individual engineering changes.
- Verification: ![Day 32 Verification](./screenshots/devops-day32.png)
#### Day 33: Resolve Git Merge Conflicts

- Objective: Mitigate overlapping source configuration blocks using logical evaluation frameworks.
- Execution:
  ```bash
  ```
- Security Value: Guarantees application definition integrity is maintained over competing modification pipelines.
- Verification: ![Day 33 Verification](./screenshots/devops-day33.png)
#### Day 34: Git Hook

- Objective: Construct client/server automation boundaries that trigger code analysis checks before commits occur.
- Execution:
  ```bash
  ```
- Security Value: Enforces programmatic credential scanning and formatting checks automatically before code leaves the host.
- Verification: ![Day 34 Verification](./screenshots/devops-day34.png)

### Phase 3: Docker Containerization & Microservices (Days 35 - 47)
#### Day 35: Install Docker Packages and Start Docker Service

- Objective: Initialize isolated high-performance host kernel container engine dependencies.
- Execution:
  ```bash
  ```
- Security Value: Sets system boundaries segregating execution contexts safely away from core OS kernels.
- Verification: ![Day 35 Verification](./screenshots/devops-day35.png)
#### Day 36: Deploy Nginx Container on Application Server

- Objective: Spin up an ephemeral web endpoint encapsulated inside structured namespace controls.
- Execution:
  ```bash
  ```
- Security Value: Restricts internet-facing application runtimes within controlled container sandboxes.
- Verification: ![Day 36 Verification](./screenshots/devops-day36.png)
#### Day 37: Copy File to Docker Container

- Objective: Inject asset configuration structures directly across container storage namespaces.
- Execution:
  ```bash
  ```
- Security Value: Facilitates predictable content configuration injection without widening host attack surfaces.
- Verification: ![Day 37 Verification](./screenshots/devops-day37.png)
#### Day 38: Pull Docker Image

- Objective: Securely retrieve cryptographically hash-verified application base templates from trusted repositories.
- Execution:
  ```bash
  ```
- Security Value: Guarantees baseline layer integrity against corrupted file systems or supply chain attacks.
- Verification: ![Day 38 Verification](./screenshots/devops-day38.png)
#### Day 39: Create a Docker Image From Container

- Objective: Capture active operational execution variations into reproducible gold standard container images.
- Execution:
  ```bash
  ```
- Security Value: Locks verified running software profiles into standardized immutable distribution templates.
- Verification: ![Day 39 Verification](./screenshots/devops-day39.png)
#### Day 40: Docker EXEC Operations

- Objective: Instantiate active diagnostic terminal channels directly inside encapsulated operating networks.
- Execution:
  ```bash
  ```
- Security Value: Permits system auditing and tracing without forcing permanent service down states.
- Verification: ![Day 40 Verification](./screenshots/devops-day40.png)
#### Day 41: Write a Docker File

- Objective: Construct clean, layered blueprint definitions that build applications under clear step guides.
- Execution:
  ```dockerfile
  ```
- Security Value: Prevents container image bloat and drops unnecessary root privileges using multi-stage builds.
- Verification: ![Day 41 Verification](./screenshots/devops-day41.png)
#### Day 42: Create a Docker Network

- Objective: Deploy isolated network subnets that separate container communications from adjacent workloads.
- Execution:
  ```bash
  ```
- Security Value: Implements micro-segmentation, ensuring compromised applications cannot sniff adjacent internal networks.
- Verification: ![Day 42 Verification](./screenshots/devops-day42.png)
#### Day 43: Docker Ports Mapping

- Objective: Explicitly bind target internal container application ports to defined host networking interfaces.
- Execution:
  ```bash
  ```
- Security Value: Prevents unintended mass port exposures onto untrusted external internet routes.
- Verification: ![Day 43 Verification](./screenshots/devops-day43.png)
#### Day 44: Write a Docker Compose File

- Objective: Declare multi-container architecture setups using structured YAML infrastructure definitions.
- Execution:
  ```yaml
  ```
- Security Value: Documents and unifies environment setup expectations in an auditable declarative format.
- Verification: ![Day 44 Verification](./screenshots/devops-day44.png)
#### Day 45: Resolve Dockerfile Issues

- Objective: Debug failing container compilation steps, fix broken environment structures, and remove security hazards.
- Execution:
  ```bash
  ```
- Security Value: Purges vulnerabilities like cleartext secrets or elevated root permissions from image build records.
- Verification: ![Day 45 Verification](./screenshots/devops-day45.png)
#### Day 46: Deploy an App on Docker Containers

- Objective: Launch interconnected application stacks with external persistent volume mappings.
- Execution:
  ```bash
  ```
- Security Value: Segregates mutable system state data safely away from ephemeral compute application processes.
- Verification: ![Day 46 Verification](./screenshots/devops-day46.png)
#### Day 47: Docker Python App

- Objective: Package a custom Python runtime stack with explicit non-root service account isolation.
- Execution:
  ```bash
  ```
- Security Value: Blocks malicious code execution attempts from breaking out onto the parent host kernel.
- Verification: ![Day 47 Verification](./screenshots/devops-day47.png)

### Phase 4: Kubernetes Cluster Orchestration (Days 48 - 67)
#### Day 48: Deploy Pods in Kubernetes Cluster

- Objective: Instantiate bare application computing units inside the managed cluster network.
- Execution:
  ```bash
  ```
- Security Value: Leverages granular container namespace isolation boundaries at the orchestration layer.
- Verification: ![Day 48 Verification](./screenshots/devops-day48.png)
#### Day 49: Deploy Applications with Kubernetes Deployments

- Objective: Establish declarative replication controllers to manage application updates and self-healing targets.
- Execution:
  ```yaml
  ```
- Security Value: Ensures continuous application availability states match defined cluster standards.
- Verification: ![Day 49 Verification](./screenshots/devops-day49.png)
#### Day 50: Set Resource Limits in Kubernetes Pods

- Objective: Impose explicit maximum CPU and memory resource consumption bounds on application containers.
- Execution:
  ```yaml
  ```
- Security Value: Protects the cluster infrastructure from internal resource starvation or DoS side-effects from leaky applications.
- Verification: ![Day 50 Verification](./screenshots/devops-day50.png)
#### Day 51: Execute Rolling Updates in Kubernetes

- Objective: Push software updates to live systems incrementally, keeping the application online throughout the update.
- Execution:
  ```bash
  ```
- Security Value: Eliminates service down times and validates the health of new code before fully removing old ones.
- Verification: ![Day 51 Verification](./screenshots/devops-day51.png)
#### Day 52: Revert Deployment to Previous Version in Kubernetes

- Objective: Initiate immediate programmatic rollbacks to a known good deployment revision if issues arise.
- Execution:
  ```bash
  ```
- Security Value: Drastically limits the impact of problematic code deployments on production users.
- Verification: ![Day 52 Verification](./screenshots/devops-day52.png)
#### Day 53: Resolve VolumeMounts Issue in Kubernetes

- Objective: Diagnose and correct misconfigured directory attachment points within container pods.
- Execution:
  ```bash
  ```
- Security Value: Enforces correct file permissions, preventing read-write errors on sensitive data drives.
- Verification: ![Day 53 Verification](./screenshots/devops-day53.png)
#### Day 54: Kubernetes Shared Volumes

- Objective: Configure high-performance local directories that allow containers within the same pod to pass data back and forth.
- Execution:
  ```yaml
  ```
- Security Value: Limits inter-process communications directly to local pod boundaries rather than exposing data over the broader network.
- Verification: ![Day 54 Verification](./screenshots/devops-day54.png)
#### Day 55: Kubernetes Sidecar Containers

- Objective: Inject helper containers into existing pods to offload tasks like automated log shipping or security proxies.
- Execution:
  ```yaml
  ```
- Security Value: Separates primary business logic cleanly from supporting infrastructure processes like log collection.
- Verification: ![Day 55 Verification](./screenshots/devops-day55.png)
#### Day 56: Deploy Nginx Web Server on Kubernetes Cluster

- Objective: Spin up a scalable, public-facing load balancer setup to manage traffic entry into your cluster.
- Execution:
  ```bash
  ```
- Security Value: Standardizes the entry path for client traffic, screening internal microservices from direct exposure.
- Verification: ![Day 56 Verification](./screenshots/devops-day56.png)
#### Day 57: Print Environment Variables

- Objective: Extract and inspect configuration values passed directly into container runtime states.
- Execution:
  ```bash
  ```
- Security Value: Verifies that no cleartext secrets or passwords have leaked into plain environment strings.
- Verification: ![Day 57 Verification](./screenshots/devops-day57.png)
#### Day 58: Deploy Grafana on Kubernetes Cluster

- Objective: Set up an advanced visualization dashboard platform to track cluster metrics and activities.
- Execution:
  ```bash
  ```
- Security Value: Boosts overall infrastructure visibility, allowing teams to spot abnormal usage anomalies early.
- Verification: ![Day 58 Verification](./screenshots/devops-day58.png)
#### Day 59: Troubleshoot Deployment issues in Kubernetes

- Objective: Use system logs and pod state tools to fix containers stuck in loops like CrashLoopBackOff.
- Execution:
  ```bash
  ```
- Security Value: Speeds up incident response and restores cluster configurations back to stable, secure parameters.
- Verification: ![Day 59 Verification](./screenshots/devops-day59.png)
#### Day 60: Persistent Volumes in Kubernetes

- Objective: Configure durable external storage volumes that keep your data intact even if application pods restart or fail.
- Execution:
  ```yaml
  ```
- Security Value: Protects critical company records from accidental deletion or loss during container lifecycles.
- Verification: ![Day 60 Verification](./screenshots/devops-day60.png)
#### Day 61: Init Containers in Kubernetes

- Objective: Deploy startup containers that run setup scripts and database checks completely before main applications boot up.
- Execution:
  ```yaml
  ```
- Security Value: Eliminates the need to grant administrative setup privileges to long-running application pods.
- Verification: ![Day 61 Verification](./screenshots/devops-day61.png)
#### Day 62: Manage Secrets in Kubernetes

- Objective: Securely encode and inject sensitive data like API tokens or certificates into application pods.
- Execution:
  ```yaml
  ```
- Security Value: Prevents plain-text passwords from being accidentally committed to public Git repositories.
- Verification: ![Day 62 Verification](./screenshots/devops-day62.png)
#### Day 63: Deploy Iron Gallery App on Kubernetes

- Objective: Set up a complete multi-tier web application stack inside the cluster environment.
- Execution:
  ```bash
  ```
- Security Value: Confirms network isolation and service interaction rules are working properly across application tiers.
- Verification: ![Day 63 Verification](./screenshots/devops-day63.png)
#### Day 64: Fix Python App Deployed on Kubernetes Cluster

- Objective: Debug runtime permission blocks and resolve failing connection strings in a custom application pod.
- Execution:
  ```bash
  ```
- Security Value: Reinforces strict application boundaries by resolving code errors without opening up massive security holes.
- Verification: ![Day 64 Verification](./screenshots/devops-day64.png)
#### Day 65: Deploy Redis Deployment on Kubernetes

- Objective: Deploy a secure, high-performance in-memory caching database service within the cluster network.
- Execution:
  ```yaml
  ```
- Security Value: Implements localized network authentication to secure rapid-access data stores from external sniffing.
- Verification: ![Day 65 Verification](./screenshots/devops-day65.png)
#### Day 66: Deploy MySQL on Kubernetes

- Objective: Set up a stateful relational database container, complete with persistent storage attachments.
- Execution:
  ```yaml
  ```
- Security Value: Implements access isolation rules to restrict database access exclusively to authorized backend components.
- Verification: ![Day 66 Verification](./screenshots/devops-day66.png)
#### Day 67: Deploy Guest Book App on Kubernetes

- Objective: Launch a full-stack, multi-tier web architecture featuring distinct microservices for frontend and backend tiers.
- Execution:
  ```bash
  ```
- Security Value: Demonstrates how to design secure network paths that isolate different application tiers from one another.
- Verification: ![Day 67 Verification](./screenshots/devops-day67.png)

### Phase 5: Jenkins CI/CD Automation Pipelines (Days 68 - 81)
#### Day 68: Set Up Jenkins Server

- Objective: Deploy and configure a centralized automation server engine to handle build workflows.
- Execution:
  ```bash
  ```
- Security Value: Establishes a protected environment for running software builds and deployments automatically.
- Verification: ![Day 68 Verification](./screenshots/devops-day68.png)
#### Day 69: Install Jenkins Plugins

- Objective: Extend your build engine's capabilities by installing tools for Git tracking, Docker usage, and Pipeline orchestration.
- Execution:
  ```text
  ```
- Security Value: Keeps the build platform updated with the latest security patches and community ecosystem tools.
- Verification: ![Day 69 Verification](./screenshots/devops-day69.png)
#### Day 70: Configure Jenkins User Access

- Objective: Set up strict Role-Based Access Controls (RBAC) to limit who can trigger builds or edit pipelines.
- Execution:
  ```text
  ```
- Security Value: Follows the principle of least privilege, blocking unauthorized users from triggering production builds.
- Verification: ![Day 70 Verification](./screenshots/devops-day70.png)
#### Day 71: Configure Jenkins Job for Package Installation

- Objective: Build an automated pipeline task to compile and package production code cleanly.
- Execution:
  ```groovy
  ```
- Security Value: Standardizes build routines to ensure human error doesn't introduce bad code variations into production.
- Verification: ![Day 71 Verification](./screenshots/devops-day71.png)
#### Day 72: Jenkins Parameterized Builds

- Objective: Design dynamic pipelines that accept user inputs, allowing flexible and controlled deployments.
- Execution:
  ```groovy
  ```
- Security Value: Prevents hardcoding specific environment variables directly inside the core build scripts.
- Verification: ![Day 72 Verification](./screenshots/devops-day72.png)
#### Day 73: Jenkins Scheduled Jobs

- Objective: Create automated triggers to run security scans and clean build environments at specific times.
- Execution:
  ```text
  ```
- Security Value: Automates system maintenance tasks, ensuring security audits happen consistently on a schedule.
- Verification: ![Day 73 Verification](./screenshots/devops-day73.png)
#### Day 74: Jenkins Database Backup Job

- Objective: Automate database dump scripts and securely ship the backup files to remote storage locations.
- Execution:
  ```bash
  ```
- Security Value: Provides a reliable way to recover data quickly if a production database encounters issues or corrupts.
- Verification: ![Day 74 Verification](./screenshots/devops-day74.png)
#### Day 75: Jenkins Slave Nodes

- Objective: Connect secondary worker machines to distribute the load of running heavy software builds.
- Execution:
  ```bash
  ```
- Security Value: Keeps the main Jenkins control node secure by offloading untrusted code execution tasks to isolated worker instances.
- Verification: ![Day 75 Verification](./screenshots/devops-day75.png)
#### Day 76: Jenkins Project Security

- Objective: Implement project-level access controls to isolate different development team spaces from each other.
- Execution:
  ```text
  ```
- Security Value: Prevents team members from accidentally modifying or viewing pipelines belonging to other business departments.
- Verification: ![Day 76 Verification](./screenshots/devops-day76.png)
#### Day 77: Jenkins Deploy Pipeline

- Objective: Create a full continuous deployment pipeline that automatically pushes verified code out to staging nodes.
- Execution:
  ```groovy
  ```
- Security Value: Removes the risk of human configuration mistakes by automating the deployment path from end to end.
- Verification: ![Day 77 Verification](./screenshots/devops-day77.png)
#### Day 78: Jenkins Conditional Pipeline

- Objective: Design smart pipelines that run specific stages only if previous automated tests pass successfully.
- Execution:
  ```groovy
  ```
- Security Value: Automatically stops broken or unverified code from moving forward into production environments.
- Verification: ![Day 78 Verification](./screenshots/devops-day78.png)
#### Day 79: Jenkins Deployment Job

- Objective: Build a deployment routine featuring an explicit confirmation gate for production releases.
- Execution:
  ```groovy
  ```
- Security Value: Enforces a final manual review step before code changes are applied to the live production site.
- Verification: ![Day 79 Verification](./screenshots/devops-day79.png)
#### Day 80: Jenkins Chained Builds

- Objective: Connect multiple pipeline jobs together so that completing a code build automatically kicks off the security scanning phase.
- Execution:
  ```text
  ```
- Security Value: Ensures code always undergoes rigorous testing and scanning sequences before it is ready for deployment.
- Verification: ![Day 80 Verification](./screenshots/devops-day80.png)
#### Day 81: Jenkins Multistage Pipeline

- Objective: Construct a complete, visible pipeline mapping the entire lifecycle from compilation to final live deployment.
- Execution:
  ```groovy
  ```
- Security Value: Provides clear visibility over every deployment step, making it easy to see exactly where a build failed.
- Verification: ![Day 81 Verification](./screenshots/devops-day81.png)

### Phase 6: Advanced Ansible Configuration Management (Days 82 - 93)
#### Day 82: Create Ansible Inventory for App Server Testing

- Objective: Define and group your target servers systematically within structured inventory configuration files.
- Execution:
  ```ini
  ```
- Security Value: Ensures configuration updates are applied only to target hosts, preventing accidental modifications elsewhere.
- Verification: ![Day 82 Verification](./screenshots/devops-day82.png)
#### Day 83: Troubleshoot and Create Ansible Playbook

- Objective: Debug failing automation scripts and build clean, predictable deployment routines.
- Execution:
  ```yaml
  ```
- Security Value: Standardizes how servers are configured, eliminating manual adjustments that create security inconsistencies.
- Verification: ![Day 83 Verification](./screenshots/devops-day83.png)
#### Day 84: Copy Data to App Servers using Ansible

- Objective: Use automated playbooks to securely distribute configuration assets out to server clusters.
- Execution:
  ```yaml
  ```
- Security Value: Eliminates the need to copy files manually over unverified, ad-hoc terminal connections.
- Verification: ![Day 84 Verification](./screenshots/devops-day84.png)
#### Day 85: Create Files on App Servers using Ansible

- Objective: Automate the provisioning of key configuration files with precise ownership and access permissions.
- Execution:
  ```yaml
  ```
- Security Value: Guarantees that target files are locked down with the correct, secure access permissions right at creation.
- Verification: ![Day 85 Verification](./screenshots/devops-day85.png)
#### Day 86: Ansible Ping Module Usage

- Objective: Run quick, ad-hoc connectivity checks across your infrastructure node groupings.
- Execution:
  ```bash
  ```
- Security Value: Confirms management connections are healthy without needing to open up full interactive login shells.
- Verification: ![Day 86 Verification](./screenshots/devops-day86.png)
#### Day 87: Ansible Install Package

- Objective: Automate software package deployment across server clusters using built-in system managers.
- Execution:
  ```yaml
  ```
- Security Value: Ensures all servers run uniform, approved versions of required operational software.
- Verification: ![Day 87 Verification](./screenshots/devops-day87.png)
#### Day 88: Ansible Blockinfile Module

- Objective: Insert or update distinct, marked code configuration blocks within system layout files.
- Execution:
  ```yaml
  ```
- Security Value: Prevents configuration files from being corrupted during automated update routines.
- Verification: ![Day 88 Verification](./screenshots/devops-day88.png)
#### Day 89: Ansible Manage Services

- Objective: Automate state management to ensure core host background processes are running and enabled on boot.
- Execution:
  ```yaml
  ```
- Security Value: Ensures security services remain active and running across all systems at all times.
- Verification: ![Day 89 Verification](./screenshots/devops-day89.png)
#### Day 90: Managing ACLs Using Ansible

- Objective: Set up advanced, granular Access Control Lists (ACLs) to regulate file access on managed nodes.
- Execution:
  ```yaml
  ```
- Security Value: Enforces fine-grained data protection rules beyond standard, broad Linux user permissions.
- Verification: ![Day 90 Verification](./screenshots/devops-day90.png)
#### Day 91: Ansible Lineinfile Module

- Objective: Find and update specific configuration text strings within target system files.
- Execution:
  ```yaml
  ```
- Security Value: Allows precise security updates to system settings without disturbing other configuration variables.
- Verification: ![Day 91 Verification](./screenshots/devops-day91.png)
#### Day 92: Managing Jinja2 Templates Using Ansible

- Objective: Build dynamic, adaptive configuration files using flexible template models.
- Execution:
  ```j2
  ```
- Security Value: Adjusts configuration files dynamically to fit specific target host traits without needing hardcoded values.
- Verification: ![Day 92 Verification](./screenshots/devops-day92.png)
#### Day 93: Using Ansible Conditionals

- Objective: Build smart playbooks that run specific configuration steps only when clear criteria are met.
- Execution:
  ```yaml
  ```
- Security Value: Prevents incompatible configuration updates from running and breaking unrelated operating systems.
- Verification: ![Day 93 Verification](./screenshots/devops-day93.png)

### Phase 7: Infrastructure as Code via Terraform (Days 94 - 100)
#### Day 94: Create VPC Using Terraform

- Objective: Define a custom Virtual Private Cloud (VPC) network perimeter using declarative code configuration files.
- Execution:
  ```hcl
  ```
- Security Value: Establishes a clean, isolated network boundary for company workloads, independent of default public configurations.
- Verification: ![Day 94 Verification](./screenshots/terraform-day94.png)
#### Day 95: Create Security Group Using Terraform

- Objective: Codify stateful firewall rules to tightly regulate allowed traffic into infrastructure components.
- Execution:
  ```hcl
  ```
- Security Value: Follow a zero-trust model, explicitly blocking all network traffic by default unless approved.
- Verification: ![Day 95 Verification](./screenshots/terraform-day95.png)
#### Day 96: Create EC2 Instance Using Terraform

- Objective: Provision scalable cloud virtual machines cleanly using modular resource blueprints.
- Execution:
  ```hcl
  ```
- Security Value: Ensures all deployed virtual servers match approved, uniform baseline security images.
- Verification: ![Day 96 Verification](./screenshots/terraform-day96.png)
#### Day 97: Create IAM Policy Using Terraform

- Objective: Codify precise granular permissions to govern access to cloud service resources.
- Execution:
  ```hcl
  ```
- Security Value: Enforces strict least-privilege boundaries, preventing services from accessing unapproved corporate data stores.
- Verification: ![Day 97 Verification](./screenshots/terraform-day97.png)
#### Day 98: Launch EC2 in Private VPC Subnet Using Terraform

- Objective: Deploy cloud compute workloads inside completely isolated subnets with no direct route to the open internet.
- Execution:
  ```hcl
  ```
- Security Value: Hides critical application backends from public internet exposure, blocking external scanning attempts.
- Verification: ![Day 98 Verification](./screenshots/terraform-day98.png)
#### Day 99: Attach IAM Policy for DynamoDB Access Using Terraform

- Objective: Bind localized access keys to server profiles, allowing them to read and write to specific database tables.
- Execution:
  ```hcl
  ```
- Security Value: Eliminates the risky practice of hardcoding access passwords directly onto server disk drives.
- Verification: ![Day 99 Verification](./screenshots/terraform-day99.png)
#### Day 100: Create and Configure Alarm Using CloudWatch Using Terraform

- Objective: Codify automated alerting rules to instantly flag resource spikes or unusual system usage metrics.
- Execution:
  ```hcl
  ```
- Security Value: Provides immediate notification of security breaches, high traffic stress events, or infrastructure failure states.
- Verification: ![Day 100 Verification](./screenshots/terraform-day100.png)

---
