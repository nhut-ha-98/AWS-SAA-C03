# **AWS DMS (Database Migration Service)**

# ⚡ STAGE 1 — ULTRA-FAST READ

🧠 MEMORY ANCHORS

* Migrates **databases** to AWS with minimal downtime ⏱️

* Supports **homogeneous** & **heterogeneous** migrations 🔄

* Can **replicate ongoing changes** (CDC) to keep target in sync 🔗

* Analogy: DMS giống như **"dịch vụ chuyển nhà cho dữ liệu"**, giúp chuyển từ nhà cũ (database cũ) sang nhà mới (AWS) mà không làm gián đoạn cuộc sống hàng ngày.

* Keywords: **Migration, Replication, Minimal Downtime**

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **AWS DMS** giúp chuyển đổi dữ liệu từ nguồn này sang đích AWS database một cách an toàn và liên tục.
* **Core purpose:** Giảm downtime và rủi ro khi di chuyển dữ liệu.
* **Key value proposition:** Hỗ trợ di chuyển nhiều loại database, từ on-premises hoặc cloud khác sang AWS.
* 🧠 Keywords: **Migration, Replication, Continuous**

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Giảm rủi ro **downtime** và mất dữ liệu trong migration.
* Xử lý các **schema differences** khi di chuyển giữa các loại database khác nhau.
* Nếu không dùng DMS: migration thủ công, downtime dài, mất dữ liệu.
* 🧠 Keywords: **Threat, Risk, Data Loss**

3️⃣ 📦 USE CASES (REAL-WORLD)

* Di chuyển **Oracle -> Aurora PostgreSQL**, **SQL Server -> RDS MySQL**.
* Replicate dữ liệu từ on-premises DB sang AWS để làm **analytics hoặc DR**.
* **Best fit:** Enterprise, DevOps teams, startups cần cloud migration.
* 🧠 Keywords: **Use case, Migration, DR**

4️⃣ 🧠 EXAM COVERAGE & TRAPS

* **Key concepts:** Homogeneous vs Heterogeneous, CDC (Change Data Capture), replication tasks.
* **Common traps:** Không nhầm với **AWS Glue** (DMS chỉ di chuyển DB, Glue ETL dữ liệu)
* **Not used for:** ETL phức tạp, big data transformation.
* 🧠 Keywords: **Exam tip, Anti-pattern, CDC**

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* **Replication Instance** 🖥️: Thực hiện data migration & replication.
* **Source Endpoint** 🏠: Database nguồn.
* **Target Endpoint** 🎯: Database đích.
* **Replication Task** 🔄: Cấu hình chi tiết migration (full load, CDC, or both).
* **Flow:** Source DB ➡ Replication Instance ➡ Target DB
* 🧠 Keywords: **Replication Instance, Endpoint, Task**

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **Amazon RDS, Aurora, Redshift, S3**: làm target hoặc source.
* **CloudWatch**: monitor replication.
* **SNS**: thông báo trạng thái migration.
* 🧠 Keywords: **Integration, Monitoring, Notification**

7️⃣ ⚖️ PROS & LIMITATIONS

* **Pros:** Minimal downtime, supports heterogeneous migrations, easy to set up.
* **Limitations:** Không thay thế ETL tool, performance phụ thuộc vào replication instance, schema conversion may need SCT.
* 🧠 Keywords: **Benefit, Limitation**

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

* **Choose DMS:** DB migration or replication, minimal downtime.
* **Not DMS:** Complex ETL, batch transformations (use Glue).
* Short comparison:

  * DMS vs Glue: DMS = migrate/replicate, Glue = transform & ETL.
* 🧠 Keywords: **Choose when, Compare**

❓ Q&A

* **Q:** Có thể dùng DMS để replicate dữ liệu liên tục không?
  **A:** ✅ Yes, dùng **CDC**.
* **Q:** DMS có thể di chuyển dữ liệu giữa MySQL và PostgreSQL không?
  **A:** ✅ Yes, **heterogeneous migration**.
* **Q:** DMS thay thế ETL tool được không?
  **A:** ❌ No, DMS mainly migration.
* **Q:** DMS có downtime dài không?
  **A:** ❌ Minimal downtime, support full load + CDC.

🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

* On-premises DB 🏠 ➡ Replication Instance 🖥️ ➡ Amazon RDS 🎯 (Full load + CDC)
* Source DB 🏠 ➡ DMS ➡ Redshift 🎯 (ETL simple replication, analytics)
* Multiple sources 🏠🏠 ➡ DMS 🖥️ ➡ S3 🎯 ➡ Athena (analytics pipeline)



# cần dùng AWS SCT (Schema Conversion Tool) để chuyển schema trước, sau đó DMS mới migrate dữ liệu.