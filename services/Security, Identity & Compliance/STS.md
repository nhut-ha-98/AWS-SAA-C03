# **AWS STS (Security Token Service)**

# ⚡ STAGE 1 — ULTRA-FAST READ

🧠 MEMORY ANCHORS (VERY IMPORTANT)

🔑 STS là gì (nhớ nhanh):

* 🎟️ Cấp **temporary credentials** (có thời hạn)
* 🔄 Cho phép **AssumeRole** (cross-account / same-account)
* 🌐 Hỗ trợ **Federation** (SAML, OIDC, external IdP)

🌍 Real-world analogy:

* STS giống như **thẻ ra vào tạm thời** trong công ty: dùng đúng phạm vi, hết hạn tự thu hồi.

🧠 Must-remember keywords:

* **Temporary credentials**, **AssumeRole**, **Federation**, **Trust policy**, **Expiration**

---

# 📝 STAGE 2 — PRE-EXAM READ

1️⃣ 🔍 SERVICE OVERVIEW

* **What is STS?**
  AWS STS là dịch vụ cấp **temporary security credentials** để truy cập AWS resources.

* **WHY tồn tại**
  Giải quyết vấn đề **không dùng long-term access key**, giảm rủi ro bảo mật.

* **Key value proposition**

  * Không cần hard-code credentials ❌
  * Credentials **tự động hết hạn** ⏳
  * Áp dụng **least privilege** qua IAM Role 🎯

* 🧠 Keywords: **Temporary credentials**, **IAM Role**, **Trust relationship**

---

2️⃣ 🛡️ THREATS / PROBLEMS IT SOLVES

* 🔓 Lộ **access key / secret key** dài hạn
* 👤 Người dùng bên ngoài cần truy cập AWS (SSO, partner)
* 🧑‍💻 Truy cập **cross-account** không an toàn nếu chia sẻ key

🚨 Nếu KHÔNG dùng STS:

* Phải tạo IAM User cho mọi đối tượng

* Credential khó xoay vòng (rotation)

* Blast radius lớn khi bị lộ key

* 🧠 Keywords: **Credential leak**, **Least privilege**, **Risk**

---

3️⃣ 📦 USE CASES (REAL-WORLD)

* 🏢 Enterprise: cross-account admin / audit access
* 🌐 SSO: login bằng Azure AD, Google (SAML / OIDC)
* 📱 Mobile / Web app: cấp quyền AWS tạm thời
* 🤝 Partner access: không cần tạo IAM User

✅ BEST choice khi:

* Quyền truy cập **tạm thời**

* Identity **external hoặc dynamic**

* 🧠 Keywords: **Use case**, **Federation**, **Best fit**

---

4️⃣ 🧠 EXAM COVERAGE & TRAPS

✅ Những điểm hay ra đề:

* STS chỉ cấp **temporary credentials**
* Permission đến từ **IAM Role policy**, không phải STS
* **Trust policy** quyết định AI được AssumeRole

❌ Trap thường gặp:

* STS ❌ không tạo user

* STS ❌ không authenticate end-user

* STS ❌ không lưu credentials

* 🧠 Keywords: **Exam tip**, **AssumeRole**, **Anti-pattern**

---

# 📚 STAGE 3 — FULL UNDERSTANDING

5️⃣ 🧩 CORE COMPONENTS & ARCHITECTURE

🧑‍🚀 **IAM Role**

* Chứa permission policy (được làm gì)

🤝 **Trust Policy**

* Ai được AssumeRole (AWS account, service, IdP)

🎟️ **Temporary Credentials** ⏳

* Access Key ID
* Secret Access Key
* Session Token
* Có **Expiration**

🔄 High-level flow:

1. Identity gửi request AssumeRole
2. STS kiểm tra Trust policy
3. STS cấp temporary credentials
4. AWS services xác thực credentials

* 🧠 Keywords: **AssumeRole**, **Trust policy**, **Expiration**

---

6️⃣ 🔄 INTEGRATIONS & RELATED SERVICES

* **IAM**: role, permission policy

* **AWS Organizations**: cross-account access

* **Amazon Cognito**: user authentication → STS credentials

* **External IdP**: SAML, OIDC (Azure AD, Google)

* **AWS CLI / SDK**: assume role programmatically

* 🧠 Keywords: **Integration**, **Federation**, **Automation**

---

7️⃣ ⚖️ PROS & LIMITATIONS

✅ Benefits:

* Bảo mật cao (no long-term key)
* Dễ audit, dễ revoke
* Phù hợp zero-trust

⚠️ Limitations:

* Luôn có thời hạn

* Cần cấu hình Trust policy đúng

* Hơi khó hiểu với người mới

* 🧠 Keywords: **Benefit**, **Limitation**

---

8️⃣ 🧪 SCENARIOS & DECISION GUIDE

✅ Chọn STS khi:

* Cần **temporary access**
* Cần **cross-account access**
* Có **federated users**

🔄 So sánh nhanh:

* STS vs IAM User → STS = temporary, IAM User = permanent

* STS vs Cognito → Cognito authenticate, STS authorize AWS access

* STS vs Resource policy → STS là identity-based access

* 🧠 Keywords: **Choose when**, **Compare**

---

🎯 FINAL TAKEAWAY

Hễ đề thi nhắc đến:

* Temporary access
* Cross-account
* Federation
* Không dùng long-term access key

👉 Chọn ngay **AWS STS** ⚡🧠

🧪 Các API STS quan trọng (hay ra thi)
1️⃣ AssumeRole ⭐⭐⭐

Cross-account access

Case phổ biến nhất

2️⃣ AssumeRoleWithWebIdentity

Login bằng:

Cognito

Google

Facebook

Web / Mobile app

3️⃣ GetSessionToken

MFA cho IAM User

4️⃣ AssumeRoleWithSAML

SSO với AD / Okta