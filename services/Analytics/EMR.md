# **AWS EMR (Elastic MapReduce)**

# ⚡ STAGE 1 — ULTRA-FAST READ

🧠 MEMORY ANCHORS

* 🏗️ Managed big data platform chạy **Apache Spark, Hadoop** trên AWS
* ⚡ Xử lý **big data at scale** nhanh, linh hoạt, trả tiền theo mức dùng
* 🔄 Phân tích batch & streaming từ **S3, HDFS, DynamoDB**

📖 Analogy (Real-world)

* AWS EMR giống như **thuê một nhà máy xử lý dữ liệu khổng lồ theo giờ**: cần thì bật, xong việc thì tắt

🔑 Must-remember keywords

* **Spark**, **Hadoop**, **Big Data**, **Cluster**, **S3**

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **AWS EMR** là dịch vụ **managed cluster** để xử lý **Big Data frameworks**
* WHY: Giảm công sức tự setup & vận hành Hadoop/Spark
* Value:

  * Scale nhanh ⚡
  * Pay-as-you-go 💰
  * Tích hợp chặt với **Amazon S3**
* 🧠 Keywords: **Big Data**, **Cluster**, **Spark**, **Hadoop**

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Vấn đề:

  * Xử lý data lớn quá sức EC2 đơn lẻ
  * On-prem Hadoop phức tạp, khó scale
* Scenario:

  * Batch job chạy hàng TB dữ liệu
  * Log processing, ETL
* Không dùng EMR:

  * Tốn công quản trị cluster
  * Khó tối ưu chi phí & scale
* 🧠 Keywords: **Scalability**, **Throughput**, **Cost**

3️⃣ 📦 USE CASES (REAL-WORLD)

* ETL data pipeline
* Log & clickstream analysis
* Machine Learning preprocessing
* Data transformation trước khi đưa vào **Redshift**
* Best fit:

  * Startup & Enterprise có **Big Data workload**
* 🧠 Keywords: **ETL**, **Analytics**, **Batch processing**

4️⃣ 🧠 EXAM COVERAGE & TRAPS

* Exam nhớ:

  * EMR = Big Data processing, **NOT database**
  * Storage tách rời compute (S3)
* Trap thường gặp:

  * Dùng EMR thay cho **Redshift** (sai)
  * Dùng EMR cho low-latency OLTP (sai)
* 🧠 Keywords: **Exam tip**, **Anti-pattern**

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* 🧠 **Cluster**

  * Master node 🧠: quản lý
  * Core node ⚙️: xử lý + lưu HDFS
  * Task node 🚀: xử lý mở rộng
* 📥 Input

  * **Amazon S3**, **HDFS**, **DynamoDB**
* 📤 Output

  * **S3**, **Redshift**, **OpenSearch**
* Frameworks:

  * **Apache Spark** ⚡
  * **Hadoop MapReduce** 🗺️
  * **Hive**, **Presto**, **HBase**

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **Amazon S3**: data lake chính
* **IAM**: quyền truy cập cluster
* **CloudWatch**: monitoring
* **AWS Glue**: metadata catalog
* **Step Functions**: orchestration
* 🧠 Keywords: **Integration**, **Automation**

7️⃣ ⚖️ PROS & LIMITATIONS

* ✅ Pros:

  * Scale lớn
  * Flexible framework
  * Cost-efficient cho batch job
* ⚠️ Limitations:

  * Không phù hợp real-time OLTP
  * Cần hiểu Big Data concept
  * Startup time có độ trễ
* 🧠 Keywords: **Benefit**, **Limitation**

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

* Choose **EMR** khi:

  * Xử lý Big Data batch
  * Cần Spark/Hadoop
* Compare nhanh:

  * EMR vs **Redshift**: processing vs analytics DB
  * EMR vs **Glue**: flexible cluster vs serverless ETL
  * EMR vs **Athena**: compute-heavy vs SQL query
* 🧠 Keywords: **Choose when**, **Compare**
