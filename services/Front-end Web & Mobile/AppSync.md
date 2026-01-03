# **AWS AppSync**

# ⚡ STAGE 1 — ULTRA-FAST READ (30–60s)

🧠 MEMORY ANCHORS (VERY IMPORTANT)

* **Managed GraphQL service** để query/mutate data từ **nhiều backend** (DynamoDB, Lambda, RDS, HTTP) trong **1 API duy nhất**
* **Client chỉ nói CẦN GÌ**, AppSync tự lo **fetch, aggregate, auth, cache**
* Tối ưu cho **serverless + real-time + mobile/web**

🔎 **Real-world analogy**

* AppSync giống như **nhân viên lễ tân thông minh**: bạn hỏi 1 câu, lễ tân tự đi hỏi nhiều phòng ban rồi trả về đúng thứ bạn cần 📞🏢

🧠 **Must-remember keywords (English only)**

* GraphQL
* Pipeline Resolver
* Data Source
* Real-time
* Authorization

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **AWS AppSync** là **fully managed GraphQL API service**
* **WHY**: Giải quyết bài toán **aggregate data từ nhiều backend** với latency thấp
* **Value**:

  * Single endpoint
  * Fine-grained data fetching
  * Serverless, auto-scale
* 🧠 Keywords: **GraphQL**, **Resolver**, **Data Source**, **Schema**

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* Vấn đề:

  * Client phải gọi **nhiều API** → chậm, phức tạp
  * Over-fetch / Under-fetch data
* Nếu KHÔNG dùng AppSync:

  * Phải tự viết aggregation logic trong Lambda
  * Khó maintain, tăng latency
* 🧠 Keywords: **Risk**, **Latency**, **Over-fetching**

3️⃣ 📦 USE CASES (REAL-WORLD)

* Mobile / Web app cần data từ **nhiều DynamoDB tables**
* Real-time app (chat, dashboard, collaboration)
* Backend for frontend (BFF)
* Best fit cho:

  * **Startup**: nhanh, ít ops
  * **Enterprise**: scale, security
* 🧠 Keywords: **Use case**, **Best fit**

4️⃣ 🧠 EXAM COVERAGE & TRAPS

* Exam hay hỏi:

  * Aggregate data từ **multiple data sources**
  * Cần **no impact on baseline performance**
* Traps:

  * Dùng API Gateway + Lambda thay vì AppSync
* AppSync **NOT used for**:

  * REST-only API
  * Batch / analytics query
* 🧠 Keywords: **Exam tip**, **Anti-pattern**

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* 📄 **GraphQL Schema**: định nghĩa type, query, mutation, subscription
* 🔀 **Resolver**: mapping GraphQL field → backend
* 🧵 **Pipeline Resolver**: nhiều bước resolver liên tiếp
* 🗄️ **Data Source**: DynamoDB, Lambda, RDS, OpenSearch, HTTP
* 🔐 **Authorization**: IAM, Cognito, API Key, OIDC

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **DynamoDB**: direct resolver, low latency
* **AWS Lambda**: custom logic
* **Amazon Cognito**: user authentication
* **Amazon OpenSearch**: search
* 🧠 Keywords: **Integration**, **Event-driven**

7️⃣ ⚖️ PROS & LIMITATIONS

* ✅ Pros:

  * Aggregate data dễ dàng
  * Fine-grained access
  * Real-time subscription built-in
* ❌ Limitations:

  * Không phù hợp REST-only mindset
  * Learning curve với GraphQL
* 🧠 Keywords: **Benefit**, **Limitation**

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

* Chọn **AppSync khi**:

  * Nhiều data source
  * Mobile/Web app
  * Real-time needed
* So sánh nhanh:

  * AppSync vs API Gateway: **GraphQL vs REST**
  * AppSync vs Lambda: **orchestration vs compute**
* 🧠 Keywords: **Choose when**, **Compare**

❓ Q&A (EXAM-FOCUSED)

* Q: App cần đọc nhiều DynamoDB tables, ít ops?

  * A: **AppSync Pipeline Resolver**
* Q: Real-time update cho client?

  * A: **Subscription**
* Q: REST API đơn giản?

  * A: **API Gateway (not AppSync)**

🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

* 📱 Mobile/Web ➝ AppSync ➝ DynamoDB (direct resolver)
* 🧠 AppSync ➝ Pipeline Resolver ➝ multiple DynamoDB tables
* 🔔 AppSync Subscription ➝ Real-time update to clients
* 🔐 AppSync + Cognito ➝ user-based access control


```
Client (GraphQL Query / Mutation / Subscription)
│
▼
AppSync
├──▶ DynamoDB (Direct Resolver)
│
├──▶ HTTP Data Source (NO Lambda)
│ └─▶ REST APIs / Microservices / SaaS
│
├──▶ AWS Lambda
│ ├─▶ RDS / Aurora (SQL JOIN)
│ ├─▶ External APIs (complex logic)
│ └─▶ Other AWS services
│
├──▶ OpenSearch
│
└──▶ Pipeline Resolver (ORCHESTRATION)
├─▶ DynamoDB (Table A)
├─▶ DynamoDB (Table B)
├─▶ HTTP API
└─▶ Merge result → GraphQL Response
```