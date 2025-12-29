# **AWS Outposts**

# ⚡ STAGE 1 — ULTRA-FAST READ (30–60s)

🧠 MEMORY ANCHORS (VERY IMPORTANT)

* 🏢 **AWS Outposts** = AWS **đặt hạ tầng vật lý ngay on-premises** của khách hàng
* ☁️ Chạy **AWS services locally** nhưng quản lý như AWS Region
* 🔒 Dùng khi **data residency / latency / on-prem requirement** bắt buộc

**Real-world analogy**:

* AWS Region = **data center AWS** ☁️
* AWS Outposts = **AWS mang data center tới nhà bạn** 🏠

**Must-remember keywords**:

* **On-premises**
* **AWS-managed hardware**
* **Hybrid cloud**
* **Low latency**
* **Data residency**

---

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **AWS Outposts** là **AWS-managed infrastructure** được **deploy tại on-premises** hoặc colocation
* Control plane vẫn ở **AWS Region**, data plane chạy local
* Mục tiêu: mang **AWS experience & services** về on-prem

🧠 Keywords:

* **Hybrid**, **On-prem**, **AWS-managed**

---

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Quy định **data residency** không cho dữ liệu ra ngoài
* Ứng dụng cần **ultra-low latency** với hệ thống on-prem
* Không đồng nhất tool giữa cloud & on-prem

❌ Không dùng Outposts:

* Phải tự quản lý hạ tầng
* Tooling & API không đồng nhất

🧠 Keywords:

* **Compliance risk**, **Latency**, **Operational risk**

---

3️⃣ 📦 USE CASES (REAL-WORLD)

* 🏦 Banking / Finance (data locality)
* 🏥 Healthcare (PHI, compliance)
* 🏭 Manufacturing (factory systems)
* 🛫 Telco core systems

**Best fit**:

* Enterprise
* Regulated industries
* Hybrid-cloud strategy

🧠 Keywords:

* **Use case**, **Best fit**, **Regulated**

---

4️⃣ 🧠 EXAM COVERAGE & TRAPS

✅ Exam tips:

* Outposts = **AWS on your data center**
* AWS chịu trách nhiệm **hardware & patching**

❌ Common traps:

* Không phải edge service như CloudFront
* Không phải multi-region
* Không phải purely on-prem DIY

🧠 Keywords:

* **Exam tip**, **Anti-pattern**

---

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* 🧱 **Outposts Rack / Server**: AWS hardware tại site
* 🌍 **Parent Region**: control plane
* 🖥️ **EC2**: compute local
* 💾 **EBS**: local persistent storage
* 🌐 **VPC Extension**: network integration

**High-level flow**:
User/App → Outposts → AWS Region (control)

🧠 Keywords:

* **Local data plane**, **Regional control plane**

---

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **Amazon EC2** 🖥️
* **Amazon EBS** 💾
* **Amazon ECS / EKS** 📦
* **Application Load Balancer** ⚖️
* **AWS Direct Connect / VPN** 🔗

🧠 Keywords:

* **Integration**, **Hybrid networking**, **Consistency**

---

7️⃣ ⚖️ PROS & LIMITATIONS

✅ Benefits:

* Consistent AWS APIs & tooling
* Meet **data residency** requirements
* Low latency with on-prem systems

⚠️ Limitations:

* **High cost**
* Limited service availability
* Capacity planning required

🧠 Keywords:

* **Benefit**, **Limitation**

---

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

✅ Choose **AWS Outposts** when:

* Dữ liệu **phải ở on-prem**
* Cần AWS services local

🔁 Compare:

* **Outposts vs Local Zones**: on-prem vs city edge
* **Outposts vs Snow Family**: persistent vs temporary
* **Outposts vs Wavelength**: enterprise vs 5G

🧠 Keywords:

* **Choose when**, **Compare**

---

❓ Q&A (EXAM FOCUS)

1️⃣ App không được phép đưa data ra cloud?
→ **AWS Outposts**

2️⃣ Cần latency thấp cho city users?
→ ❌ Không phải Outposts → Local Zones

3️⃣ Di chuyển data ngắn hạn?
→ **AWS Snowball**

---

🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

1️⃣ 🏦 Regulated App
On-prem App → Outposts EC2 → Local EBS

2️⃣ 🏭 Factory System
Machines → Outposts → Analytics Region

3️⃣ ☁️ Hybrid App
Outposts (core) → Region (scale)

---

🎯 **FINAL MEMORY HOOK**

> AWS Outposts = **AWS mang cloud vào data center của bạn** ☁️➡️🏢
