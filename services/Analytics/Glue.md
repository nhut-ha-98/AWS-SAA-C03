# **AWS GLUE**

⚡ Managed ETL & Data Integration Service cho Data Lake trên AWS

---

# ⚡ STAGE 1 — ULTRA-FAST READ

🧠 MEMORY ANCHORS

🔹 AWS Glue là gì? (tóm tắt <5 bullets)

* 🧩 **Serverless ETL** service để **discover, prepare, transform, and load data**
* 📚 Tự động quản lý **Data Catalog** cho Data Lake
* 🔄 Chạy ETL jobs dựa trên **Apache Spark** (managed)
* ⚙️ Tích hợp chặt với **S3, Athena, Redshift**

🏭 Real-world analogy

* AWS Glue giống như **người quản lý kho dữ liệu**: tự đọc nhãn, sắp xếp, làm sạch và chuyển hàng (data) sang đúng kệ để analytics dùng ngay 📦➡️📊

🧠 Must-remember keywords (English)

* **ETL** · **Data Catalog** · **Serverless** · **Apache Spark** · **Crawler**

---

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* AWS Glue là gì?

  * **Fully managed, serverless ETL & data integration service**
* WHY tồn tại?

  * Giảm công sức **build & manage ETL pipelines** cho Data Lake
* Key value proposition

  * ❌ Không quản lý server
  * ⚡ Scale tự động
  * 📚 Metadata tập trung cho analytics
* 🧠 Keywords

  * **ETL**, **Serverless**, **Data Catalog**, **Schema**, **Spark**

---

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Vấn đề thường gặp

  * ETL thủ công, khó scale
  * Schema drift (thay đổi cấu trúc dữ liệu)
  * Metadata phân tán, khó query
* Nếu KHÔNG dùng AWS Glue

  * ETL rời rạc (EC2, scripts)
  * Quản lý schema thủ công
  * Analytics chậm & lỗi
* 🧠 Keywords

  * **Risk**, **Schema drift**, **Data silos**

---

3️⃣ 📦 USE CASES (REAL-WORLD)

* Common scenarios

  * Build **Data Lake on Amazon S3**
  * Prepare data cho **Athena / Redshift / EMR**
  * Ingest data từ **RDS, DynamoDB, logs**
* Ai nên dùng?

  * Startup: nhanh, ít ops
  * Enterprise: chuẩn hóa Data Lake
  * Data team / Analytics team
* Khi là BEST choice

  * Khi cần **serverless ETL + metadata management**
* 🧠 Keywords

  * **Use case**, **Data Lake**, **Best fit**

---

4️⃣ 🧠 EXAM COVERAGE & TRAPS

* Key exam concepts

  * Glue = **ETL + Data Catalog** (KHÔNG phải BI tool)
  * Glue jobs chạy trên **Apache Spark**
  * Athena cần **Glue Data Catalog**
* Common traps

  * ❌ Nhầm Glue với **AWS Data Pipeline**
  * ❌ Dùng Glue cho real-time streaming (Glue chủ yếu batch)
* Glue KHÔNG dùng để

  * Visualization
  * Low-latency OLTP
* 🧠 Keywords

  * **Exam tip**, **Anti-pattern**

---

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* 🕷️ **Crawler**

  * Quét data source → infer schema → update Data Catalog
* 📚 **Data Catalog**

  * Central metadata repository (tables, databases, schema)
* ⚙️ **Glue Job**

  * ETL code (Spark) để transform data
* 🧪 **Glue Studio**

  * Visual ETL (low-code)
* ⏱️ **Trigger / Workflow**

  * Orchestration cho ETL pipeline

High-level flow

* Source ➝ Crawler ➝ Data Catalog ➝ Glue Job ➝ Target

---

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* Amazon S3

  * Primary Data Lake storage
* Amazon Athena

  * Query data dùng Glue Data Catalog
* Amazon Redshift

  * Load curated data vào data warehouse
* AWS Lake Formation

  * Fine-grained access control cho Data Lake
* Amazon EventBridge

  * Trigger Glue jobs theo event
* 🧠 Keywords

  * **Integration**, **Event-driven**, **Automation**

---

7️⃣ ⚖️ PROS & LIMITATIONS

* ✅ Pros

  * Serverless, auto scale
  * Tight integration với analytics stack
  * Centralized metadata
* ⚠️ Limitations

  * Cold start latency
  * Not ideal cho real-time ETL
  * Spark learning curve
* 🧠 Keywords

  * **Benefit**, **Limitation**

---

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

* Choose AWS Glue when

  * Build Data Lake on S3
  * Need batch ETL + schema management
* Compare nhanh

  * Glue vs AWS Data Pipeline

    * Glue = serverless Spark ETL
    * Data Pipeline = orchestration (legacy)
  * Glue vs Amazon EMR

    * Glue = managed ETL
    * EMR = full control big data cluster
* 🧠 Keywords

  * **Choose when**, **Compare**

---

❓ Q&A (EXAM-FOCUSED)

1️⃣ Athena query fail vì không thấy table?

* 👉 Chưa có metadata trong **Glue Data Catalog**

2️⃣ ETL batch cho Data Lake, không muốn manage cluster?

* 👉 **AWS Glue**

3️⃣ Cần stream processing real-time?

* 👉 Không phải Glue → nghĩ đến **Kinesis**

---

🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

1️⃣ 🗄️ S3 Data Lake ETL

* Logs ➝ S3 ➝ Glue Crawler ➝ Glue Job ➝ S3 (curated)

2️⃣ 🔍 Serverless Analytics

* S3 ➝ Glue Data Catalog ➝ Athena query

3️⃣ 🏢 Data Warehouse Load

* S3 ➝ Glue ETL ➝ Amazon Redshift

4️⃣ 🔐 Governed Data Lake

* S3 ➝ Glue + Lake Formation ➝ Controlled access

---

🎯 GHI NHỚ CUỐI

* AWS Glue = **Serverless ETL + Metadata Backbone** cho Data Lake
* Luôn gắn với **S3 + Athena + Redshift** trong exam
