
# ☁️ Phân loại AWS Services: SaaS – PaaS – IaaS

---

## 🧱 IaaS – *Infrastructure as a Service*

👉 AWS lo **hạ tầng vật lý**, bạn quản lý **OS → App**

| Dịch vụ               | Vai trò         | Ghi chú                |
| --------------------- | --------------- | ---------------------- |
| EC2                   | Virtual Machine | Full control OS        |
| EBS                   | Block storage   | Gắn vào EC2            |
| S3                    | Object storage  | Durable, không phải DB |
| Elastic Load Balancer | Load balancing  | L4/L7                  |
| VPC                   | Network         | Subnet, route          |
| Direct Connect        | Kết nối on-prem | Private link           |
| Route 53              | DNS             | Global                 |
| Elastic IP            | IP tĩnh         | Cho EC2                |
| AWS Outposts          | AWS on-prem     | Hybrid                 |

📌 **Keyword thi:** *you manage OS, patching*

---

## 🧰 PaaS – *Platform as a Service*

👉 AWS lo **infra + OS + runtime**, bạn lo **code & data**

### 🔹 Compute / App Platform

| Dịch vụ           | Use case                    |
| ----------------- | --------------------------- |
| Elastic Beanstalk | Deploy app nhanh            |
| App Runner        | App container               |
| Lambda            | Serverless                  |
| ECS / EKS         | Container                   |
| Fargate           | Container không quản server |

---

### 🔹 Database (Managed)

| Dịch vụ     | Loại                    |
| ----------- | ----------------------- |
| RDS         | Relational              |
| Aurora      | Relational (AWS-native) |
| DynamoDB    | NoSQL key-value         |
| ElastiCache | In-memory               |
| MemoryDB    | Redis durable           |
| Neptune     | Graph                   |
| DocumentDB  | Mongo-compatible        |
| Timestream  | Time-series             |
| Keyspaces   | Cassandra               |

📌 Bạn **không ssh**, không patch DB engine

---

### 🔹 Integration & Backend

| Dịch vụ        | Vai trò               |
| -------------- | --------------------- |
| API Gateway    | API                   |
| AppSync        | GraphQL               |
| SQS            | Queue                 |
| SNS            | Pub/Sub               |
| EventBridge    | Event bus             |
| Step Functions | Workflow              |
| AppFlow        | SaaS data integration |

---

### 🔹 DevOps & App Support

| Dịch vụ                               |                |
| ------------------------------------- | -------------- |
| CodeBuild / CodeDeploy / CodePipeline | CI/CD          |
| CloudWatch                            | Logs / Metrics |
| X-Ray                                 | Tracing        |
| Secrets Manager                       | Secret         |
| Parameter Store                       | Config         |

📌 **Keyword:** *no server management*

---

## ☁️ SaaS – *Software as a Service*

👉 AWS lo **mọi thứ**, bạn **chỉ cấu hình & dùng**

### 🔹 Business / End-user SaaS

| Dịch vụ           | Use case        |
| ----------------- | --------------- |
| Amazon WorkMail   | Email           |
| Amazon Chime      | Meeting         |
| Amazon Connect    | Call center     |
| Amazon WorkDocs   | Document        |
| Amazon WorkSpaces | Virtual desktop |

---

### 🔹 Analytics & Monitoring (SaaS-like)

| Dịch vụ                |           |
| ---------------------- | --------- |
| Amazon QuickSight      | BI        |
| AWS Managed Grafana    | Dashboard |
| AWS Managed Prometheus | Metrics   |

---

### 🔹 AI & ML SaaS

| Dịch vụ            |                   |
| ------------------ | ----------------- |
| Amazon Rekognition | Image/Video AI    |
| Amazon Textract    | OCR               |
| Amazon Comprehend  | NLP               |
| Amazon Translate   | Translate         |
| Amazon Polly       | Text-to-speech    |
| Amazon Lex         | Chatbot           |
| Amazon Bedrock     | GenAI (API-first) |

📌 **Keyword:** *consume via API/UI*

---

## 🧠 Bảng nhớ nhanh (1 dòng ăn điểm thi)

| Mô hình | Bạn làm gì         |
| ------- | ------------------ |
| IaaS    | Manage OS + app    |
| PaaS    | Manage code + data |
| SaaS    | Just use           |

---

## 🎯 Mapping cực nhanh (hay ra đề)

* **EC2 = IaaS**
* **RDS / Lambda = PaaS**
* **QuickSight / WorkMail = SaaS**

    