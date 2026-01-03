# **AWS Storage Gateway Overview**

# ⚡ STAGE 1 — ULTRA-FAST READ

🧠 MEMORY ANCHORS

* **Hybrid cloud storage** for on-premises + AWS ✅
* Provides **low-latency local access** + cloud durability ☁️
* Supports **file, volume, and tape gateways** 📂

**Analogy:** Storage Gateway giống như một **cầu nối giữa nhà kho vật lý và kho đám mây AWS** 🌉

**Keywords:** Hybrid, Gateway, NFS/SMB

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **AWS Storage Gateway** là dịch vụ **hybrid cloud** cho phép kết nối môi trường on-premises với AWS.
* **Purpose:** Giúp doanh nghiệp tận dụng AWS Storage mà vẫn giữ dữ liệu local low-latency.
* **Value proposition:** Tích hợp dễ dàng, backup, disaster recovery, archive.
* 🧠 Keywords: Hybrid, On-premises, Cloud Storage

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Giúp **bảo vệ dữ liệu** khi on-premises hardware gặp sự cố.
* Giảm rủi ro mất dữ liệu trong **disaster**.
* Nếu không dùng: dữ liệu có thể **mất**, backup phức tạp, hoặc DR tốn kém.
* 🧠 Keywords: Threat, Risk, Backup, Disaster Recovery

3️⃣ 📦 USE CASES (REAL-WORLD)

* Backup dữ liệu on-premises lên **S3 hoặc Glacier**.
* Migrate files, volumes sang AWS.
* Doanh nghiệp có môi trường hybrid: startups → enterprises.
* 🧠 Keywords: Use case, Best fit, Archive, Backup

4️⃣ 🧠 EXAM COVERAGE & TRAPS

* **Key concepts:** File Gateway, Volume Gateway, Tape Gateway.
* **Traps:** Không dùng để host ứng dụng trực tiếp, không thay thế NAS truyền thống hoàn toàn.
* 🧠 Keywords: Exam tip, Anti-pattern

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* **File Gateway 📂:** expose **NFS/SMB** → store in **S3**.
* **Volume Gateway 💾:** block storage → store in **S3** (cached) hoặc on-premises snapshot → **EBS snapshot**.
* **Tape Gateway 🎟️:** virtual tape library → archive to **Glacier**.
* Flow: On-premises apps → Storage Gateway → AWS Storage (S3/Glacier).
* 🧠 Keywords: File, Volume, Tape, S3, Glacier

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **S3**: storage backend for File/Volume Gateway.
* **Glacier**: long-term archive via Tape Gateway.
* **CloudWatch**: monitoring usage and health.
* **AWS Backup**: centralize backup policies.
* 🧠 Keywords: Integration, CloudWatch, Automation

7️⃣ ⚖️ PROS & LIMITATIONS

* **Pros:** Low-latency access, hybrid integration, DR ready, supports multiple protocols.
* **Limitations:** Not a full replacement for on-premises storage, requires network connectivity, licensing for VTL may apply.
* 🧠 Keywords: Benefit, Limitation

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

* Choose Storage Gateway when **hybrid cloud** storage is needed.
* Compare:

  * File Gateway vs direct S3 upload: File Gateway = low-latency local access.
  * Tape Gateway vs physical tape: Tape Gateway = cloud archive, reduce physical storage.
* 🧠 Keywords: Choose when, Compare

❓Q&A

* Q: Can Storage Gateway replace NAS entirely? A: No, hybrid access only.
* Q: Which gateway supports SMB? A: File Gateway.
* Q: How to archive to Glacier? A: Tape Gateway or S3 lifecycle.

🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

* **Pattern 1:** On-premises server → File Gateway 📂 → S3 (backup)
* **Pattern 2:** On-premises volume → Volume Gateway 💾 → EBS snapshot → S3
* **Pattern 3:** Backup tapes → Tape Gateway 🎟️ → Glacier
* Bối cảnh: Hybrid environment, dịch vụ chính: Storage Gateway, flow tổng quan: Local → Gateway → Cloud


**Volume Gateway** trong **AWS Storage Gateway**
hai chế độ hoạt động chính: **Stored Volumes** và **Cached Volumes**. Mình tóm tắt dễ nhớ cho exam và thực tế:

---

### **1️⃣ Stored Volumes 💾**

* **Mục đích:** Lưu **toàn bộ dữ liệu on-premises** trong local storage và **backup lên AWS (S3) như snapshot**.
* **Dữ liệu chính:** Dữ liệu được **lưu cục bộ** 100% trên server on-premises.
* **Use case:**

  * Cần **low-latency access** cho toàn bộ dữ liệu.
  * Disaster Recovery: dữ liệu local + snapshot AWS.
* **Ưu điểm:**

  * Tất cả dữ liệu có sẵn on-premises → truy cập nhanh.
* **Hạn chế:**

  * Cần **đầy đủ storage** on-premises (tốn disk local).
* **Exam keyword:** Stored = **local primary storage + cloud backup**.

---

### **2️⃣ Cached Volumes 💾**

* **Mục đích:** Lưu **chỉ một phần dữ liệu trên local**, còn phần lớn **cloud (S3) là chính)**.
* **Dữ liệu chính:**

  * **Primary copy** trên **S3**, local chỉ giữ **cache** recent/active blocks.
* **Use case:**

  * On-premises server **không đủ storage** nhưng vẫn cần **low-latency access** dữ liệu gần đây.
  * Disaster Recovery: toàn bộ dữ liệu vẫn trên AWS.
* **Ưu điểm:**

  * Tiết kiệm disk on-premises.
* **Hạn chế:**

  * Nếu dữ liệu chưa cached → tải từ S3 → có latency.
* **Exam keyword:** Cached = **cloud primary storage + local cache**.

---

### **So sánh nhanh**

| Feature                  | Stored Volumes           | Cached Volumes                           |
| ------------------------ | ------------------------ | ---------------------------------------- |
| **Primary copy**         | On-premises              | AWS S3                                   |
| **Local storage needed** | Full dataset             | Small cache only                         |
| **Latency**              | Very low (all local)     | Low for cached, higher if not cached     |
| **Use case**             | Full on-prem access + DR | Hybrid, save local storage, mostly cloud |
| **AWS Snapshot**         | Optional                 | Yes, frequent snapshots to S3            |

---

💡 **Memory hook:**

* **Stored = Local first, cloud backup** 🏠☁️
* **Cached = Cloud first, local cache** ☁️🏠

---
