# **Amazon CloudTrail**

# ⚡ STAGE 1 — ULTRA-FAST READ (30–60s)

🧠 MEMORY ANCHORS

* 🕵️ **Tracks EVERYTHING**: Ghi lại mọi **API call / user action** trong AWS account
* 🧾 **Who did What, When, From Where**: Nhật ký audit & compliance
* 🚨 **Security visibility**: Phát hiện hành vi bất thường, điều tra sự cố

🔎 **Real-world analogy**

* CloudTrail giống như **camera + sổ nhật ký** của toàn bộ hệ thống AWS: ai vào, làm gì, lúc nào đều có dấu vết 📹📖

🔑 **Must-remember keywords**

* **API logging**, **Audit**, **Compliance**, **Event history**, **Trail**

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **Amazon CloudTrail** là dịch vụ **record & track API activity** trong AWS
* WHY: Giúp **audit, security, compliance, troubleshooting**
* Value: Biết chính xác **ai làm gì** trong AWS environment
* 🧠 Keywords: **API call**, **Event**, **Trail**, **Audit log**

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* ❌ Không biết ai xóa EC2 / S3 / IAM

* ❌ Không phát hiện truy cập trái phép

* ❌ Không đáp ứng yêu cầu audit / compliance

* Threat scenarios:

  * IAM user bị lộ key ➝ API call bất thường
  * Resource bị delete / modify không rõ lý do

* Không dùng CloudTrail ➝ **Blind security**, không forensics

* 🧠 Keywords: **Threat**, **Detection**, **Risk**

3️⃣ 📦 USE CASES (REAL-WORLD)

* 🏢 Enterprise: Audit & compliance (ISO, SOC, PCI)

* 🔐 Security team: Incident investigation

* 🚀 Startup: Theo dõi thay đổi môi trường prod

* Best when:

  * Cần **full visibility** hành vi người dùng & service

* 🧠 Keywords: **Use case**, **Best fit**

4️⃣ 🧠 EXAM COVERAGE & TRAPS

* CloudTrail = **LOGGING**, không phải monitoring real-time

* Ghi lại **control plane** (API), không phải application log

* KHÔNG thay thế CloudWatch Metrics

* Trap thường gặp:

  * Nhầm CloudTrail với CloudWatch Logs

* 🧠 Keywords: **Exam tip**, **Anti-pattern**

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

* 🧾 **Event**: Mỗi API call (CreateEC2, DeleteS3…)
* 🛤️ **Trail**: Cấu hình nơi lưu log (S3)
* 🗂️ **Event history**: 90 days xem trực tiếp trong console
* 🪣 **S3 bucket**: Lưu trữ log lâu dài
* 📡 **Delivery**: Tự động gửi log

Flow tổng quát:
API call ➝ CloudTrail Event ➝ Event history / S3

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **Amazon S3**: Lưu CloudTrail logs
* **Amazon CloudWatch Logs**: Near real-time alert
* **Amazon EventBridge**: Trigger automation
* **AWS Lambda**: Xử lý event
* **AWS Config**: Kết hợp audit config + activity

🧠 Keywords: **Integration**, **Event-driven**, **Automation**

7️⃣ ⚖️ PROS & LIMITATIONS
✅ Advantages:

* Default enabled (Event history)
* Account-wide visibility
* Required cho security & compliance

⚠️ Limitations:

* Không capture application-level log
* Không phân tích sâu (cần Athena / SIEM)
* Management event chi tiết, data event có phí

🧠 Keywords: **Benefit**, **Limitation**

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

* Chọn **CloudTrail** khi:

  * Cần biết **ai làm gì trong AWS**
  * Audit / forensic / compliance

* So sánh nhanh:

  * CloudTrail vs CloudWatch:

    * Trail = **API activity**
    * Watch = **metrics & logs runtime**

🧠 Keywords: **Choose when**, **Compare**

❓ Q&A (EXAM-FOCUSED)

* Q: EC2 bị terminate, dùng gì để biết ai làm?

  * A: **CloudTrail** (API call TerminateInstances)

* Q: Muốn alert khi ai đó tạo IAM user?

  * A: CloudTrail + CloudWatch Logs/EventBridge

* Q: CloudTrail có log data trong EC2 không?

  * A: ❌ Không (chỉ API)

🏭 MÔ HÌNH / KIẾN TRÚC PHỔ BIẾN

* 🛡️ Security Audit

  * User/API ➝ CloudTrail ➝ S3 ➝ Athena

* 🚨 Real-time Alert

  * CloudTrail ➝ CloudWatch Logs ➝ Alarm

* 🤖 Automation

  * CloudTrail ➝ EventBridge ➝ Lambda

🧠 CHỨC NĂNG ĐẶC BIỆT

* **Management Events**

  * API cho resource control
  * Default enabled

* **Data Events**

  * Log S3 object-level / Lambda invoke
  * Use case: truy cập dữ liệu nhạy cảm
  * Note: có cost

* **Insights**

  * Phát hiện API call bất thường
  * Use case: compromised credentials

---

🎯 GHI NHỚ 1 DÒNG:
**CloudTrail = “AWS activity audit log” — ai làm gì, lúc nào, ở đâu**
