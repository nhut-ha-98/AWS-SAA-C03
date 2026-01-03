# AWS Systems Manager

🎯 OBJECTIVE
Cung cấp cái nhìn TOÀN DIỆN nhưng DỄ NHỚ về AWS Systems Manager (SSM).
Thiết kế cho 3 giai đoạn đọc: Cực nhanh → Trước exam → Hiểu sâu.
Tập trung vào hiểu bản chất, coverage, và khả năng ghi nhớ lâu dài.


⚡ STAGE 1 — ULTRA-FAST READ (30–60s)
====================================

🧠 MEMORY ANCHORS (RẤT QUAN TRỌNG)

🔹 AWS Systems Manager là gì? (tóm gọn < 5 bullet)

* 🛠️ Công cụ **central management** cho EC2 & on‑prem servers
* 🤖 Cho phép **automation**, **patching**, **remote command** KHÔNG cần SSH
* 🔐 Quản lý cấu hình & secrets an toàn qua IAM

🔹 Real‑world analogy
👉 AWS Systems Manager giống như **IT Admin Dashboard**: bạn update, cấu hình, sửa lỗi hàng trăm server từ 1 chỗ, không cần login từng máy.

🔹 Must‑remember keywords (<7)
**Systems Manager**, **SSM Agent**, **Run Command**, **Patch Manager**, **Parameter Store**, **Automation**


📝 STAGE 2 — PRE-EXAM READ
==========================

1️⃣ 🔍 SERVICE OVERVIEW

* AWS Systems Manager là dịch vụ giúp **manage, configure, automate** hạ tầng AWS
* WHY: giảm việc SSH/RDP thủ công, giảm lỗi con người
* Value:

  * Quản lý tập trung
  * Không cần mở port SSH
  * Tích hợp IAM & automation mạnh

🧠 Keywords: **Centralized management**, **Automation**, **IAM**

---

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Server drift (mỗi máy mỗi cấu hình)
* Quên patch → lỗ hổng bảo mật
* SSH keys rải rác → rủi ro security

❌ Nếu KHÔNG dùng SSM:

* Quản lý thủ công
* Khó audit
* Dễ misconfiguration

🧠 Keywords: **Threat**, **Risk**, **Misconfiguration**

---

3️⃣ 📦 USE CASES (REAL‑WORLD)

* Chạy command hàng loạt (restart service, clear disk)
* Patch OS tự động cho EC2
* Lưu secrets/config an toàn
* Automation runbook (scale, recover, setup)

👥 Ai nên dùng?

* Startup: giảm ops
* Enterprise: compliance, audit
* Security team: hardening

🧠 Keywords: **Use case**, **Best fit**

---

4️⃣ 🧠 EXAM COVERAGE & TRAPS

✅ Exam hay hỏi:

* Remote management **không cần SSH**
* Parameter Store vs Secrets Manager
* Patch automation

⚠️ Traps:

* SSM ≠ monitoring (đó là CloudWatch)
* SSM ≠ configuration management tool như Ansible (nâng cao hơn)

🧠 Keywords: **Exam tip**, **Anti‑pattern**


📚 STAGE 3 — FULL UNDERSTANDING
===============================

5️⃣ 🧩 CORE COMPONENTS, FEATURES & CONFIG (TECH-FOCUSED)

🔹 **SSM Agent** 🤖

* Cài trên EC2, On-Prem, Hybrid
* Giao tiếp outbound HTTPS (443)
* Yêu cầu **IAM Role** gắn cho EC2
* Cho phép nhận command, patch, automation

🔹 **Managed Instances** 🖥️

* EC2 hoặc on-prem đã cài agent + role
* Hiển thị trong Systems Manager console
* Không phân biệt EC2 hay on-prem

🔹 **Run Command** ▶️

* Chạy shell / PowerShell command từ xa
* Không cần SSH/RDP
* Target theo:

  * Instance ID
  * Tag
  * Resource Group
* Output lưu vào:

  * S3
  * CloudWatch Logs

🔹 **Documents (SSM Documents)** 📄

* JSON/YAML định nghĩa hành động
* Types:

  * Command
  * Automation
  * Policy
* AWS cung cấp sẵn + custom

🔹 **Patch Manager** 🩹

* Quản lý OS patching
* Patch baseline:

  * Approve/Reject patches
  * Severity level
* Maintenance Window để schedule
* Báo cáo compliance

🔹 **Maintenance Window** ⏰

* Lên lịch task (patch, command)
* Chạy theo cron-like schedule
* Giảm downtime giờ cao điểm

🔹 **Automation** ⚙️

* Runbook (SSM Document type Automation)
* Thực hiện multi-step workflow
* Rollback khi lỗi
* Dùng cho:

  * AMI creation
  * EC2 recovery
  * Auto remediation

🔹 **State Manager** 🔄

* Đảm bảo server luôn đúng trạng thái
* Ví dụ:

  * Service luôn running
  * Package luôn installed
* Chạy định kỳ

🔹 **Parameter Store** 🔐

* Lưu:

  * Config values
  * Secrets
* Types:

  * String
  * StringList
  * SecureString
* Encryption bằng **KMS**
* IAM-based access

🔹 **Session Manager** 🧑‍💻

* SSH-like access qua AWS Console/CLI
* Không cần mở port 22
* Không cần key pair
* Log session (CloudWatch / S3)

---

6️⃣ 🔄 CONFIGURATION & SECURITY CONTROLS

🔹 **IAM Configuration** 🔑

* EC2 cần IAM Role với policy:

  * AmazonSSMManagedInstanceCore
* User cần quyền gọi SSM APIs

🔹 **Network Requirements** 🌐

* EC2 cần outbound access đến SSM endpoints
* Private subnet dùng VPC Endpoint (Interface):

  * ssm
  * ec2messages
  * ssmmessages

🔹 **Logging & Auditing** 📜

* CloudTrail: API calls
* CloudWatch Logs: command/session output
* S3: long-term storage

---

7️⃣ ⚖️ FEATURE SUMMARY (EXAM-ORIENTED)

* Remote management **không SSH**
* Automation native AWS
* Patch & compliance
* Secure secret storage
* Hybrid (cloud + on-prem)

---

8️⃣ 🧪 COMMON EXAM SCENARIOS (TECH)

* Không mở SSH → dùng **Session Manager**
* Auto patch EC2 → **Patch Manager + Maintenance Window**
* Chạy command hàng loạt → **Run Command**
* Lưu DB password → **Parameter Store (SecureString)**
* Drift config → **State Manager**


📌 TECH ONE-LINER
==============================
👉 AWS Systems Manager = **Agent-based, IAM-controlled, centralized operations platform for EC2 & hybrid servers**
