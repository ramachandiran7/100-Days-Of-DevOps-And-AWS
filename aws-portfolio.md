# 100 Days of AWS Cloud Architecture

**Engineer:** [Your Name] | **Status:** In Progress | **Target Position:** Cloud Architect / DevOps Specialist

> **Daily update:** After completing a module, update its status, add the commands/configuration you used, record the result, and place screenshots in `screenshots/` using the matching day filename.

---

## 📊 Infrastructure Track Dashboard

| Domain | Core Focus Areas | Target Range | Status |
| :--- | :--- | :--- | :--- |
| **01** | Compute & Storage Foundations | Days 01 - 15 | 🔄 In Progress (Day 1 Done) |
| **02** | Identity & Access Management (IAM) | Days 16 - 20 | ⏳ Pending |
| **03** | Advanced Networking & VPC Security | Days 21 - 30 | ⏳ Pending |
| **04** | Managed Database Architectures | Days 31 - 32 | ⏳ Pending |
| **05** | Serverless & Container Solutions | Days 33 - 39 | ⏳ Pending |
| **06** | High Availability & Infrastructure Automation | Days 40 - 50 | ⏳ Pending |

---

## 💻 Technical Execution Log

### 🖥️ Phase 1: Compute & Storage Foundations (Days 1 - 15)

#### Day 1: Create Key Pair
- **Objective:** Generate a secure cryptographic RSA key pair via the AWS console for secure SSH handshakes.
- **Execution:**
  ```bash
  chmod 400 dev-ssh-key.pem
- **Architecture Value:** Setting local file permissions to `400` restricts read access exclusively to the owner, fulfilling structural OpenSSH client handshakes before opening connection buffers.
- **Verification:** ![Day 1 Verification](./screenshots/aws-day01.png)

#### Day 2: Create Security Group
- **Objective:** Provision a stateful firewall boundary defining explicit network ingress and egress limitations.
- **Execution:**
  ```text
  
- **Architecture Value:** Drops all unsolicited traffic at the AWS infrastructure edge before it reaches internal compute workloads.
- **Verification:** ![Day 2 Verification](./screenshots/aws-day02.png)

#### Day 3: Create Subnet
- **Objective:** Partition the VPC IP network space into isolated, distinct availability segments.
- **Execution:**
  ```text
  
- **Architecture Value:** Groups compute resources by access needs, separating public web paths from private data layers.
- **Verification:** ![Day 3 Verification](./screenshots/aws-day03.png)

#### Day 4: Enable Versioning for S3 Bucket
- **Objective:** Turn on history tracking for your object storage bucket to keep multiple variants of objects over time.
- **Execution:**
  ```text
  
- **Architecture Value:** Protects critical data stores from accidental deletion or malicious ransomware changes.
- **Verification:** ![Day 4 Verification](./screenshots/aws-day04.png)

#### Day 5: Create GP3 Volume
- **Objective:** Provision high-performance Elastic Block Store (EBS) volumes with independent IOPS allocations.
- **Execution:**
  ```text
  
- **Architecture Value:** Provides scalable, predictable storage IOPS performance independent of volume capacity sizes.
- **Verification:** ![Day 5 Verification](./screenshots/aws-day05.png)

#### Day 6: Launch EC2 Instance
- **Objective:** Spin up a virtual Linux server instance within an isolated target subnet boundary.
- **Execution:**
  ```text
  
- **Architecture Value:** Deploys raw computing capacity aligned with defined corporate base configurations.
- **Verification:** ![Day 6 Verification](./screenshots/aws-day06.png)

#### Day 7: Change EC2 Instance Type
- **Objective:** Adjust instance sizing scales to alter underlying CPU and memory resource allocations.
- **Execution:**
  ```text
  
- **Architecture Value:** Provides vertical scaling capabilities to handle changing application resource demands.
- **Verification:** ![Day 7 Verification](./screenshots/aws-day07.png)

#### Day 8: Enable Stop Protection for EC2 Instance
- **Objective:** Lock down the instance state properties to prevent accidental or unauthorized server shutdowns.
- **Execution:**
  ```text
  
- **Architecture Value:** Adds a protection step that blocks accidental administrative commands from taking critical servers offline.
- **Verification:** ![Day 8 Verification](./screenshots/aws-day08.png)

#### Day 9: Enable Termination Protection for EC2 Instance
- **Objective:** Block instances from being completely deleted through accidental console clicks or script errors.
- **Execution:**
  ```text
  
- **Architecture Value:** Prevents permanent data and service loss caused by human error or automated pipeline mistakes.
- **Verification:** ![Day 9 Verification](./screenshots/aws-day09.png)

#### Day 10: Attach Elastic IP to EC2 Instance
- **Objective:** Bind a permanent, static public IPv4 address to your virtual server endpoint.
- **Execution:**
  ```text
  
- **Architecture Value:** Ensures external clients have a steady, predictable entry route that persists across instance restarts.
- **Verification:** ![Day 10 Verification](./screenshots/aws-day10.png)

#### Day 11: Attach Elastic Network Interface to EC2 Instance
- **Objective:** Add secondary virtual network cards to an instance to enable multi-homed routing paths.
- **Execution:**
  ```text
  
- **Architecture Value:** Separates standard public client traffic routes cleanly from internal management networks.
- **Verification:** ![Day 11 Verification](./screenshots/aws-day11.png)

#### Day 12: Attach Volume to EC2 Instance
- **Objective:** Connect a separate block storage drive block to a running instance to expand its local storage capacity.
- **Execution:**
  ```text
  
- **Architecture Value:** Separates critical application data storage cleanly away from the volatile primary OS boot drive.
- **Verification:** ![Day 12 Verification](./screenshots/aws-day12.png)

#### Day 13: Create AMI from EC2 Instance
- **Objective:** Capture a running server's exact configuration state into a reusable gold standard template image.
- **Execution:**
  ```text
  
- **Architecture Value:** Creates a clear blueprint for spinning up matching, identical server backups or scale replicas.
- **Verification:** ![Day 13 Verification](./screenshots/aws-day13.png)

#### Day 14: Terminate EC2 Instance
- **Objective:** Decommission and completely wipe unneeded compute instances to optimize cloud spending.
- **Execution:**
  ```text
  
- **Architecture Value:** Follows clean lifecycle management rules by purging stale, unused resources from your cloud account.
- **Verification:** ![Day 14 Verification](./screenshots/aws-day14.png)

#### Day 15: Create Volume Snapshot
- **Objective:** Capture an point-in-time backup copy of a block storage drive and store it securely in S3.
- **Execution:**
  ```text
  
- **Architecture Value:** Provides a durable backup state, allowing rapid recovery if a block drive encounters data corruption.
- **Verification:** ![Day 15 Verification](./screenshots/aws-day15.png)

---

### 🔑 Phase 2: Identity & Access Management (Days 16 - 20)

#### Day 16: Create IAM User
- **Objective:** Provision unique identity credentials for a human operator accessing the cloud platform.
- **Execution:**
  ```text
  
- **Architecture Value:** Ends account sharing practices by giving every team member distinct, traceable credentials.
- **Verification:** ![Day 16 Verification](./screenshots/aws-day16.png)

#### Day 17: Create IAM Group
- **Objective:** Group individual cloud user accounts together under unified management categories.
- **Execution:**
  ```text
  
- **Architecture Value:** Simplifies user access management, ensuring permissions are updated across entire teams simultaneously.
- **Verification:** ![Day 17 Verification](./screenshots/aws-day17.png)

#### Day 18: Create Read-Only IAM Policy for EC2 Console Access
- **Objective:** Codify a granular permission rule that grants inspection access while blocking modification changes.
- **Execution:**
  ```json
  
- **Architecture Value:** Follows strict least-privilege access rules, preventing audit users from accidentally changing production settings.
- **Verification:** ![Day 18 Verification](./screenshots/aws-day18.png)

#### Day 19: Attach IAM Policy to IAM User
- **Objective:** Bind specific authorization rules directly to an identity account to define what they can access.
- **Execution:**
  ```text
  
- **Architecture Value:** Implements clear access permissions tailored explicitly to a user's day-to-day job duties.
- **Verification:** ![Day 19 Verification](./screenshots/aws-day19.png)

#### Day 20: Create IAM Role for EC2 with Policy Attachment
- **Objective:** Build an application identity token that allows virtual servers to interact securely with other cloud systems.
- **Execution:**
  ```json
  
- **Architecture Value:** Eliminates the insecure practice of hardcoding access password strings directly into application source code.
- **Verification:** ![Day 20 Verification](./screenshots/aws-day20.png)

---

### 🌐 Phase 3: Advanced Networking & VPC Security (Days 21 - 30)

#### Day 21: Setting Up an EC2 Instance with an Elastic IP for Application Hosting
- Objective: Deploy a public web server using static IP mapping to ensure steady external client connections.
- Execution:
  ```text
- Architecture Value: Guarantees external networks always see a fixed entry route, independent of backend restarts.
- Verification: ![Day 21 Verification](./screenshots/aws-day21.png)
#### Day 22: Configuring Secure SSH Access to an EC2 Instance

- Objective: Lock down remote administration channels to accept connections exclusively from specific corporate IP blocks.
- Execution:
  ```text
- Architecture Value: Shields management terminal ports from open internet scanning attempts and brute force attacks.
- Verification: ![Day 22 Verification](./screenshots/aws-day22.png)
#### Day 23: Data Migration Between S3 Buckets Using AWS CLI

- Objective: Run high-speed, secure object copies directly across different cloud storage paths using the CLI tool.
- Execution:
  ```bash
- Architecture Value: Implements secure cloud transfer paths without forcing data downloads out to unsafe local networks.
- Verification: ![Day 23 Verification](./screenshots/aws-day23.png)
#### Day 24: Setting Up an Application Load Balancer for an EC2 Instance

- Objective: Deploy a smart traffic proxy layer to distribute application requests evenly across backend nodes.
- Execution:
  ```text
- Architecture Value: Shields internal application server configurations safely from direct public exposure.
- Verification: ![Day 24 Verification](./screenshots/aws-day24.png)
#### Day 25: Setting Up an EC2 Instance and CloudWatch Alarm

- Objective: Link a virtual compute node to an automated monitoring monitor to flag excessive resource spikes.
- Execution:
  ```text
- Architecture Value: Gives immediate visibility into system stress spikes, alerting teams to potential performance or security incidents.
- Verification: ![Day 25 Verification](./screenshots/aws-day25.png)
#### Day 26: Configuring an EC2 Instance as a Web Server with Nginx

- Objective: Install and optimize an engineering proxy server to manage application web delivery.
- Execution:
  ```bash
- Architecture Value: Standardizes the public presentation layer, keeping backend compute services secure and separate.
- Verification: ![Day 26 Verification](./screenshots/aws-day26.png)
#### Day 27: Configuring a Public VPC with an EC2 Instance for Internet Access

- Objective: Design an internet-facing network layout complete with clear internet gateway routing paths.
- Execution:
  ```text
- Architecture Value: Establishes a clean, secure network edge environment to manage public application delivery pipelines.
- Verification: ![Day 27 Verification](./screenshots/aws-day27.png)
#### Day 28: Creating a Private ECR Repository

- Objective: Provision a private, secure storage vault to house your production Docker image files.
- Execution:
  ```text
- Architecture Value: Encrypts and shields application code images, protecting them from public visibility or unsanctioned access.
- Verification: ![Day 28 Verification](./screenshots/aws-day28.png)
#### Day 29: Establishing Secure Communication Between Public and Private VPCs via VPC Peering

- Objective: Bridge two separate networks with an encrypted tunnel, allowing instances to pass traffic privately without using the open internet.
- Execution:
  ```text
- Architecture Value: Keeps cross-application network traffic off the open public web, minimizing exposure hazards.
- Verification: ![Day 29 Verification](./screenshots/aws-day29.png)
#### Day 30: Enable Internet Access for Private EC2 using NAT Instance

- Objective: Design a unidirectional route path that lets private instances download updates safely without exposing them to direct incoming public connections.
- Execution:
  ```text
- Architecture Value: Protects internal servers from inbound attacks while permitting necessary outbound outbound update checks.
- Verification: ![Day 30 Verification](./screenshots/aws-day30.png)

### Phase 4: Managed Database Architectures (Days 31 - 32)
#### Day 31: Configuring a Private RDS Instance for Application Development

- Objective: Provision a managed relational database instance completely within a hidden private subnet segment.
- Execution:
  ```text
- Architecture Value: Completely blocks database engines from direct open internet paths, securing core application records.
- Verification: ![Day 31 Verification](./screenshots/aws-day31.png)
#### Day 32: Snapshot and Restoration of an RDS Instance

- Objective: Run a full database snapshot copy and validate the process by restoring it to a new active instance.
- Execution:
  ```text
- Architecture Value: Proves disaster recovery playbooks work, ensuring business continuity against database corruption.
- Verification: ![Day 32 Verification](./screenshots/aws-day32.png)

### Phase 5: Serverless & Container Solutions (Days 33 - 39)
#### Day 33: Create a Lambda Function

- Objective: Deploy an event-driven serverless code script via the cloud console dashboard.
- Execution:
  ```text
- Architecture Value: Lowers the attack surface by running code only on demand, eliminating long-running server instances.
- Verification: ![Day 33 Verification](./screenshots/aws-day33.png)
#### Day 34: Create a Lambda Function Using CLI

- Objective: Deploy and update a serverless code bundle using the command line toolkit.
- Execution:
  ```bash
- Architecture Value: Sets up predictable script deployment pathways suitable for CI/CD automation pipelines.
- Verification: ![Day 34 Verification](./screenshots/aws-day34.png)
#### Day 35: Deploying and Managing Applications on AWS

- Objective: Group cloud application elements systematically into structured runtime sets.
- Execution:
  ```text
- Architecture Value: Streamlines cross-resource management visibility, ensuring uniform resource tagging.
- Verification: ![Day 35 Verification](./screenshots/aws-day35.png)
#### Day 36: Load Balancing EC2 Instances with Application Load Balancer

- Objective: Route web traffic dynamically across multiple server targets using path-based health monitoring.
- Execution:
  ```text
- Architecture Value: Ensures system availability by dynamically routing traffic away from failing servers.
- Verification: ![Day 36 Verification](./screenshots/aws-day36.png)
#### Day 37: Managing EC2 Access with S3 Role-based Permissions

- Objective: Bind an IAM privilege profile directly to a server instance to permit access to an encrypted S3 bucket.
- Execution:
  ```text
- Architecture Value: Avoids saving permanent access keys onto local server disks, blocking data leaks if systems are compromised.
- Verification: ![Day 37 Verification](./screenshots/aws-day37.png)
#### Day 38: Deploying Containerized Applications with Amazon ECS

- Objective: Deploy a production docker container stack inside a fully managed cloud container orchestration engine.
- Execution:
  ```text
- Architecture Value: Optimizes infrastructure use by running microservices inside strict container sandboxes.
- Verification: ![Day 38 Verification](./screenshots/aws-day38.png)
#### Day 39: Hosting a Static Website on AWS S3

- Objective: Configure an object storage bucket to deliver public web content directly without running virtual servers.
- Execution:
  ```text
- Architecture Value: Lowers overhead and maintenance costs by replacing traditional server hosts with serverless web hosting.
- Verification: ![Day 39 Verification](./screenshots/aws-day39.png)

### Phase 6: High Availability & Infrastructure Automation (Days 40 - 50)
#### Day 40: Troubleshooting Internet Accessibility for an EC2-Hosted Application

- Objective: Use system tracing tools to fix broken internet gateway routing maps and missing firewall access lines.
- Execution:
  ```text
- Architecture Value: Restores secure traffic access paths without opening up excessive permission settings.
- Verification: ![Day 40 Verification](./screenshots/aws-day40.png)
#### Day 41: Securing Data with AWS KMS

- Objective: Deploy and use custom cryptographic keys to encrypt sensitive file stores at rest.
- Execution:
  ```text
- Architecture Value: Secures sensitive corporate records from theft, aligning infrastructure directly with data compliance laws.
- Verification: ![Day 41 Verification](./screenshots/aws-day41.png)
#### Day 42: Building and Managing NoSQL Databases with AWS DynamoDB

- Objective: Deploy a scalable, key-value NoSQL database service featuring microsecond performance limits.
- Execution:
  ```text
- Architecture Value: Provides structural database horizontal scaling, eliminating traditional database patching work.
- Verification: ![Day 42 Verification](./screenshots/aws-day42.png)
#### Day 43: Scaling and Managing Kubernetes Clusters with Amazon EKS

- Objective: Provision a production-ready Kubernetes management engine across multiple availability zone segments.
- Execution:
  ```text
- Architecture Value: Delivers a uniform container control landscape featuring built-in AWS network security alignments.
- Verification: ![Day 43 Verification](./screenshots/aws-day43.png)
#### Day 44: Implementing Auto Scaling for High Availability in AWS

- Objective: Configure an Auto Scaling group to adjust server numbers automatically based on live system load trends.
- Execution:
  ```text
- Architecture Value: Maintains application stability during sudden traffic surges while cutting costs when demand drops.
- Verification: ![Day 44 Verification](./screenshots/aws-day44.png)
#### Day 45: Configure NAT Gateway for Internet Access in a Private VPC

- Objective: Deploy a highly available managed network bridge to handle secure outbound update routes from private subnets.
- Execution:
  ```text
- Architecture Value: Replaces manual NAT configurations with a fully scalable, enterprise-grade outbound network shield.
- Verification: ![Day 45 Verification](./screenshots/aws-day45.png)
#### Day 46: Event-Driven Processing with Amazon S3 and Lambda

- Objective: Build a pipeline that runs serverless scripts automatically the moment new files land in an S3 bucket.
- Execution:
  ```text
- Architecture Value: Automates asset parsing tasks instantly without needing continuous server processing power.
- Verification: ![Day 46 Verification](./screenshots/aws-day46.png)
#### Day 47: Integrating AWS SQS and SNS for Reliable Messaging

- Objective: Connect a pub/sub notification topic to a secure message queue to safely decouple app communications.
- Execution:
  ```text
- Architecture Value: Prevents data dropouts during high traffic spikes by buffering communications between application modules.
- Verification: ![Day 47 Verification](./screenshots/aws-day47.png)
#### Day 48: Automating Infrastructure Deployment with AWS CloudFormation

- Objective: Codify a multi-tier infrastructure setup inside a single declarative JSON/YAML template file.
- Execution:
  ```yaml
- Architecture Value: Enables repeatable, audited infrastructure rollouts, eliminating manual console click mistakes.
- Verification: ![Day 48 Verification](./screenshots/aws-day48.png)
#### Day 49: Centralized Audit Logging with VPC Peering

- Objective: Route internal log shipping traffic securely across private network peers to a master logging bucket.
- Execution:
  ```text
- Architecture Value: Concentrates audit trails into a single secure vault, protecting records from tampering.
- Verification: ![Day 49 Verification](./screenshots/aws-day49.png)
#### Day 50: Expanding EC2 Instance Storage for Development Needs

- Objective: Automate online storage adjustments on live block volumes without taking applications offline.
- Execution:
  ```bash
- Architecture Value: Prevents storage space failures on active development servers with zero user downtime.
- Verification: ![Day 50 Verification](./screenshots/aws-day50.png)
