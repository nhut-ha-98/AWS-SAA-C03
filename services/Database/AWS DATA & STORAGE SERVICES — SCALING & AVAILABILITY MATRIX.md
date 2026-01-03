
## 🧱 AWS DATA & STORAGE SERVICES — SCALING & GLOBAL WRITE MATRIX

> **Global Write = can write data in multiple regions simultaneously**

---

## 🟦 RELATIONAL DATABASES

| Service                       | Storage Scaling | Compute Scaling | Read Replicas | Multi-AZ | Cross-Region    | 🌍 Global Write |
| ----------------------------- | --------------- | --------------- | ------------- | -------- | --------------- | --------------- |
| **RDS (MySQL/Postgres/etc.)** | ✅ Manual / Auto | ❌ Manual        | ✅ Yes         | ✅ Yes    | ✅ Read Replicas | ❌ No            |
| **Aurora Provisioned**        | ✅ Auto          | ❌ Manual        | ✅ Up to 15    | ✅ Yes    | ✅ Global DB     | ❌ No (1 writer) |
| **Aurora Serverless v1/v2**   | ✅ Auto          | ✅ Auto          | ✅ Readers     | ✅ Yes    | ✅ Global DB     | ❌ No (1 writer) |

📌 **Key exam trap**

> *Aurora Global Database = global reads, **single-region write***

---

## 🟨 NoSQL / KEY-VALUE

| Service                   | Storage Scaling | Compute Scaling | Read Replicas | Multi-AZ | Cross-Region    | 🌍 Global Write |
| ------------------------- | --------------- | --------------- | ------------- | -------- | --------------- | --------------- |
| **DynamoDB**              | ✅ Auto          | ✅ Auto          | ❌ N/A         | ✅ Yes    | ✅ Global Tables | ✅ **YES**       |
| **ElastiCache Redis**     | ❌ Manual        | ❌ Manual        | ✅ Yes         | ✅ Yes    | ❌ No            | ❌ No            |
| **ElastiCache Memcached** | ❌ Manual        | ❌ Manual        | ❌ No          | ❌ No     | ❌ No            | ❌ No            |

📌 **Only DynamoDB supports true multi-region writes**

---

## 🟧 DATA WAREHOUSE / ANALYTICS

| Service                  | Storage Scaling | Compute Scaling | Read Replicas | Multi-AZ | Cross-Region | 🌍 Global Write |
| ------------------------ | --------------- | --------------- | ------------- | -------- | ------------ | --------------- |
| **Redshift Provisioned** | ❌ Node-based    | ❌ Manual        | ❌ No          | ❌ No     | ❌ No         | ❌ No            |
| **Redshift Serverless**  | ✅ Auto          | ✅ Auto          | ❌ No          | ✅ Yes    | ❌ No         | ❌ No            |
| **Athena**               | ✅ Auto          | ✅ Auto          | ❌ No          | ✅ Yes    | ❌ No         | ❌ No            |

---

## 🟩 OBJECT / FILE STORAGE

| Service | Storage Scaling | Compute Scaling | Replication | Multi-AZ | Cross-Region | 🌍 Global Write            |
| ------- | --------------- | --------------- | ----------- | -------- | ------------ | -------------------------- |
| **S3**  | ✅ Auto          | N/A             | ✅ CRR / SRR | ✅ Yes    | ✅ Yes        | ⚠️ *Eventually consistent* |
| **EFS** | ✅ Auto          | N/A             | ❌ No        | ✅ Yes    | ❌ No         | ❌ No                       |
| **FSx** | ❌ Manual        | ❌ Manual        | ❌ No        | ❌ No     | ❌ No         | ❌ No                       |

📌 **S3 note (important)**

* Multiple regions **can write**, but:

  * No conflict resolution
  * Not transactional
  * Not considered “true global write” in exams

---

## 🧠 EXAM-LEVEL TRUTHS (MEMORIZE)

### ✅ TRUE Global Write (multi-region active-active)

* **DynamoDB Global Tables**

### ❌ NOT Global Write

* Aurora Global Database (single writer)
* RDS Cross-Region Read Replicas
* S3 CRR (async, eventual)

---

## 🧩 Killer exam shortcut

> **“Global write” → DynamoDB Global Tables**
> **“Global read” → Aurora Global DB / RDS read replicas**
> **“Object replication” → S3 CRR**

