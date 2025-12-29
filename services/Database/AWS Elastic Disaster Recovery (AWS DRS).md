# **AWS Elastic Disaster Recovery (AWS DRS)**

⚡⚡⚡

## ⚡ STAGE 1 — ULTRA-FAST READ (30–60s)

==============================

### 🧠 MEMORY ANCHORS (VERY IMPORTANT)

**AWS Elastic Disaster Recovery là gì?**

* 🔁 **Continuous block-level replication** từ on-prem / EC2 lên AWS
* 🕯️ **Pilot light DR**: chỉ chạy tối thiểu, bật full khi có sự cố
* ⏱️ **RPO seconds**, **RTO minutes**
* 💸 **Low-cost DR** cho VM-based workloads

**🌍 Real-world analogy**

> Giống như **ghi hình camera liên tục** ở nhà kho: bình thường không dùng, nhưng khi có sự cố thì mở lại toàn bộ cảnh để phục hồi.

**🔑 Must-remember keywords (English)**

* Elastic Disaster Recovery
* Continuous replication
* Pilot light
* RPO seconds
* RTO minutes

---

## 📝 STAGE 2 — PRE-EXAM READ

==============================

### 1️⃣ 🔍 SERVICE OVERVIEW

**What is AWS Elastic Disaster Recovery?**

* Managed service giúp **replicate liên tục VM** (OS + app + data) vào AWS để phục vụ **Disaster Recovery**

**WHY it exists**

* Thay thế giải pháp DR truyền thống **đắt đỏ, phức tạp**

**Key value proposition**

* ✅ RPO rất thấp (seconds)
* ✅ RTO nhanh (minutes–<1h)
* ✅ Trả tiền thấp khi chưa failover

🧠 **Keywords**: Elastic Disaster Recovery, Continuous replication, Pilot light

---

### 2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

**Risks addressed**

* 💥 Datacenter outage
* 🔥 Hardware failure
* 🌊 Natural disaster
* ⚡ Ransomware (khôi phục sang clean point-in-time)

**If NOT using this service**

* ❌ RPO cao (backup theo giờ/ngày)
* ❌ RTO dài (rebuild infra + restore)
* ❌ DR không test thường xuyên

🧠 **Keywords**: Threat, Risk, Disaster recovery

---

### 3️⃣ 📦 USE CASES (REAL-WORLD)

**Common scenarios**

* On-prem **VMware / Hyper-V** cần DR lên AWS
* EC2 workload cần **cross-Region DR**
* Legacy app (SAP, SQL Server, Oracle trên VM)

**Who should use it**

* 🏢 Enterprise (legacy workload)
* 🧑‍💻 IT Ops / Infra team

**BEST choice when**

* App chạy trên **VM**
* Cần **RPO seconds**, **RTO < 1 hour**
* Muốn **tiết kiệm chi phí**

🧠 **Keywords**: Use case, Best fit

---

### 4️⃣ 🧠 EXAM COVERAGE & TRAPS

**Exam must-know**

* AWS Elastic Disaster Recovery ≠ Backup
* Replicate **entire VM**, không chỉ database
* Default pattern: **Pilot light**

**Common traps**

* ❌ Nhầm với AWS Backup
* ❌ Nhầm với Multi-AZ / Active-Active HA

**NOT used for**

* ❌ High availability (HA)
* ❌ Zero-downtime

🧠 **Keywords**: Exam tip, Anti-pattern

---

## 📚 STAGE 3 — FULL UNDERSTANDING

==============================

### 5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* 🧠 **AWS DRS Service**: quản lý replication & recovery
* 🧩 **Replication Agent** 🖥️: cài trên source server
* 🗄️ **Staging Area (Low-cost EC2 + EBS)**: nhận block changes
* 🚀 **Recovery EC2**: chỉ launch khi failover

**High-level flow**
Source VM ➝ Replication Agent ➝ Staging Area ➝ Launch Recovery Instance

---

### 6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* 🧱 **Amazon EC2**: recovery instances
* 💾 **Amazon EBS**: replicated volumes
* 🔐 **IAM**: permissions
* 📊 **Amazon CloudWatch**: monitoring
* 🧪 **AWS Fault Injection Simulator** (gián tiếp): DR test

🧠 **Keywords**: Integration, Automation

---

### 7️⃣ ⚖️ PROS & LIMITATIONS

**Benefits**

* 💰 Low cost (pay small until failover)
* ⏱️ Very low RPO
* 🔄 Automated recovery

**Limitations**

* ❌ Not application-aware (DB-level)
* ❌ Not zero-downtime
* ❌ Recovery still needs manual trigger/plan

🧠 **Keywords**: Benefit, Limitation

---

### 8️⃣ 🧪 SCENARIOS & DECISION GUIDE

**Choose AWS Elastic Disaster Recovery when**

* VM-based workload
* Tight RPO/RTO
* Cost-sensitive DR

**Compare quickly**

* vs **AWS Backup** → Backup = hours RPO
* vs **Multi-AZ** → HA, not DR
* vs **Active/Active** → Expensive, complex

🧠 **Keywords**: Choose when, Compare

---

## ❓ Q&A (EXAM-FOCUSED)

**Q1:** RPO 30s, SQL Server on VM, low cost → chọn gì?
➡️ AWS Elastic Disaster Recovery

**Q2:** AWS DRS có thay thế backup không?
➡️ ❌ Không, chỉ dùng cho DR

**Q3:** AWS DRS có phải HA không?
➡️ ❌ Không, là DR

---

## 🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

* 🕯️ **Pilot Light DR**

  * On-prem VM ➝ AWS DRS ➝ Launch EC2 khi disaster

* 🌍 **Cross-Region DR**

  * EC2 Region A ➝ replicate ➝ Region B

* 🏢 **Datacenter to AWS DR**

  * VMware ➝ AWS Elastic Disaster Recovery ➝ AWS

* 🔐 **Ransomware Recovery**

  * Continuous replication ➝ recover to clean point

---

🎯 **FINAL MEMORY HOOK**

> AWS Elastic Disaster Recovery = **VM-level, continuous replication, low-cost pilot light DR**
