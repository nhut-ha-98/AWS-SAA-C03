# Domain 1 – Design Secure Architectures

## Access controls and management across multiple accounts
- 📌 Giải thích ngắn: Quản lý ai được vào tài nguyên khi có nhiều AWS account. Giúp tách môi trường dev/test/prod nhưng vẫn kiểm soát tập trung.
- 🛠 AWS Services / Ví dụ: AWS Organizations, IAM, SCPs. Ví dụ: dùng Organizations + SCP chặn tạo tài nguyên đắt tiền ở account dev.
- 📝 Exam Tip: Thấy "multi-account" nghĩ ngay đến Organizations + SCP + IAM role. Không dùng share root user giữa các account.
- 🧠 Mẹo nhớ: Nhớ: Nhiều nhà (account), một quản lý chung (Organizations + SCP).

## AWS federated access and identity services (for example, AWS Identity and Access Management [IAM], AWS IAM Identity Center [AWS Single Sign-On])
- 📌 Giải thích ngắn: Cho user đăng nhập từ IdP (AD, Okta, Google) vào AWS mà không tạo IAM user riêng.
- 🛠 AWS Services / Ví dụ: IAM, IAM Identity Center (SSO), AWS STS, SAML/OIDC. Ví dụ: nhân viên dùng tài khoản công ty đăng nhập console AWS qua SSO.
- 📝 Exam Tip: Từ khóa: "federation", "SSO", "corporate directory" → dùng IAM Identity Center + IAM role, không dùng IAM user.
- 🧠 Mẹo nhớ: Nhớ: User ở ngoài, role ở trong, STS cấp vé tạm.

## AWS global infrastructure (for example, Availability Zones, AWS Regions)
- 📌 Giải thích ngắn: Region là khu vực, trong đó có nhiều Availability Zone (AZ) để chịu lỗi. Chọn đúng Region/AZ ảnh hưởng bảo mật, HA và latency.
- 🛠 AWS Services / Ví dụ: EC2, RDS, S3 (Region-based), Route 53 (global). Ví dụ: triển khai app đa AZ để tránh một AZ hỏng.
- 📝 Exam Tip: Thấy yêu cầu "multi-AZ", "multi-Region" → nghĩ về HA, DR. Không trộn AZ trong cùng subnet.
- 🧠 Mẹo nhớ: Nhớ: Region = quốc gia, AZ = quận trong thành phố.

## AWS security best practices (for example, the principle of least privilege)
- 📌 Giải thích ngắn: Cho user/service đúng quyền cần, không hơn. Giảm rủi ro lộ hoặc lạm dụng quyền.
- 🛠 AWS Services / Ví dụ: IAM policies, SCPs, IAM Access Analyzer. Ví dụ: chỉ cho EC2 quyền read S3 theo bucket cụ thể.
- 📝 Exam Tip: Từ khóa: "least privilege", "need-to-know" → policy càng hẹp càng đúng. Tránh dùng `AdministratorAccess` trừ khi thật cần.
- 🧠 Mẹo nhớ: Nhớ: Chìa khoá mở đúng một cửa, không mở cả tòa nhà.

## The AWS shared responsibility model
- 📌 Giải thích ngắn: AWS chịu trách nhiệm "security OF the cloud"; khách hàng chịu "security IN the cloud". Biết cái gì AWS lo, cái gì mình phải lo.
- 🛠 AWS Services / Ví dụ: EC2 (khách hàng quản OS, patch), RDS (AWS quản engine, khách hàng quản data, access).
- 📝 Exam Tip: Câu hỏi lý thuyết: lớp nào do AWS, lớp nào do bạn. Với dịch vụ managed càng cao (Lambda, S3) thì AWS làm nhiều hơn.
- 🧠 Mẹo nhớ: Nhớ: AWS lo phần cứng & nền tảng, bạn lo dữ liệu & cấu hình.

## Applying AWS security best practices to IAM users and root users (for example, multi-factor authentication [MFA])
- 📌 Giải thích ngắn: Root user quyền tối đa, chỉ dùng cho việc đặc biệt. Tất cả user khác dùng IAM user/role với MFA.
- 🛠 AWS Services / Ví dụ: IAM, MFA, IAM password policy. Ví dụ: bật MFA cho root, khóa access key của root.
- 📝 Exam Tip: Nếu đề nói "root user" → luôn: bật MFA, không dùng access key, dùng role thay vì root cho tác vụ hàng ngày.
- 🧠 Mẹo nhớ: Nhớ: Root = chìa khoá két sắt, chỉ mở khi bất đắc dĩ.

## Designing a flexible authorization model that includes IAM users, groups, roles, and policies
- 📌 Giải thích ngắn: Gom user vào group, gán policy cho group/role thay vì từng user. Role cho service hoặc user tạm mượn quyền.
- 🛠 AWS Services / Ví dụ: IAM users, groups, roles, managed policies. Ví dụ: group "Developers" có quyền read S3, assume role "Admin" khi cần.
- 📝 Exam Tip: Thấy nhu cầu "tạm thời tăng quyền", "ứng dụng truy cập S3" → dùng IAM role, không dùng access key cố định.
- 🧠 Mẹo nhớ: Nhớ: User mặc áo (role) để đổi quyền, áo cởi ra thì hết quyền.

## Designing a role-based access control strategy (for example, AWS Security Token Service [AWS STS], role switching, cross-account access)
- 📌 Giải thích ngắn: Role-based access control: user/ứng dụng được gán role tương ứng nhiệm vụ. STS cấp token tạm khi assume role, kể cả qua account khác.
- 🛠 AWS Services / Ví dụ: AWS STS, IAM role, external ID. Ví dụ: account A assume role ở account B để deploy.
- 📝 Exam Tip: Từ khóa: "cross-account", "temporary credentials" → IAM role + STS, không share access key giữa account.
- 🧠 Mẹo nhớ: Nhớ: Đi thăm nhà hàng xóm phải mượn thẻ (role) do nhà đó cấp.

## Designing a security strategy for multiple AWS accounts (for example, AWS Control Tower, service control policies [SCPs])
- 📌 Giải thích ngắn: Quản lý hàng loạt account với guardrail chuẩn, policy áp từ trên xuống. Dùng để chuẩn hóa bảo mật và compliance.
- 🛠 AWS Services / Ví dụ: AWS Organizations, AWS Control Tower, SCPs, AWS Config. Ví dụ: chặn tạo resource ngoài Region cho phép bằng SCP.
- 📝 Exam Tip: Thấy "landing zone", "multi-account governance" → nghĩ Control Tower + Organizations + SCP.
- 🧠 Mẹo nhớ: Nhớ: Tòa nhà (Organization) đặt nội quy chung (SCP) cho tất cả căn hộ (account).

## Determining the appropriate use of resource policies for AWS services
- 📌 Giải thích ngắn: Resource policy gắn trực tiếp vào resource (S3 bucket, KMS key, SQS). Cho phép/deny truy cập từ account khác hoặc public.
- 🛠 AWS Services / Ví dụ: S3 bucket policy, KMS key policy, SQS/SNS resource policy. Ví dụ: cho account B đọc bucket của account A qua bucket policy.
- 📝 Exam Tip: Thấy truy cập cross-account vào S3, KMS, SQS, SNS → dùng resource policy thay vì chỉ IAM policy.
- 🧠 Mẹo nhớ: Nhớ: Nhà (resource) tự dán bảng nội quy ở cửa (resource policy).

## Determining when to federate a directory service with IAM roles
- 📌 Giải thích ngắn: Dùng AD/IdP hiện có cho user đăng nhập AWS, map nhóm AD sang IAM role. Giảm công tạo user trùng lặp.
- 🛠 AWS Services / Ví dụ: IAM Identity Center, AWS Directory Service, SAML, AD Connector. Ví dụ: nhóm AD "Finance" assume role chỉ xem báo cáo billing.
- 📝 Exam Tip: Từ khóa: "use existing corporate identity", "Active Directory" → dùng federation + IAM role, không tạo IAM user riêng lẻ.
- 🧠 Mẹo nhớ: Nhớ: Một tài khoản công ty, nhiều hệ thống, vào AWS qua role.

## Application configuration and credentials security
- 📌 Giải thích ngắn: Không hard-code mật khẩu/API key trong code. Lưu ở nơi bảo mật, xoay vòng được.
- 🛠 AWS Services / Ví dụ: AWS Secrets Manager, Systems Manager Parameter Store, IAM role. Ví dụ: Lambda đọc DB password từ Secrets Manager.
- 📝 Exam Tip: Thấy từ "secrets", "DB password" → dùng Secrets Manager/Parameter Store; tránh lưu trong S3/plain text/code.
- 🧠 Mẹo nhớ: Nhớ: Mật khẩu ở két (Secrets), app chỉ mượn lúc cần.

## AWS service endpoints
- 📌 Giải thích ngắn: Endpoint là URL/điểm kết nối tới dịch vụ. Có thể dùng VPC endpoint để không đi Internet.
- 🛠 AWS Services / Ví dụ: VPC Gateway/Interface Endpoints, S3, DynamoDB. Ví dụ: EC2 private subnet truy cập S3 qua Gateway Endpoint.
- 📝 Exam Tip: Từ khóa: "no public internet", "private access" → dùng VPC endpoint. Không cần NAT cho S3/DynamoDB nếu có endpoint.
- 🧠 Mẹo nhớ: Nhớ: Cửa riêng trong nội bộ VPC dẫn thẳng tới dịch vụ.

## Control ports, protocols, and network traffic on AWS
- 📌 Giải thích ngắn: Dùng SG, NACL, route table để cho/ chặn traffic theo port, protocol, CIDR. Bảo vệ lớp network.
- 🛠 AWS Services / Ví dụ: Security Group, Network ACL, Route Table, NLB. Ví dụ: chỉ mở TCP 443 từ Internet tới ALB.
- 📝 Exam Tip: SG là stateful, NACL stateless. Thấy chặn IP cụ thể ở subnet → dùng NACL; chặn ở instance → dùng SG.
- 🧠 Mẹo nhớ: Nhớ: SG = tường nhà, NACL = cổng khu dân cư.

## Secure application access
- 📌 Giải thích ngắn: Đảm bảo user truy cập app qua HTTPS, auth, và kiểm soát session an toàn.
- 🛠 AWS Services / Ví dụ: ALB (HTTPS), Cognito, CloudFront, ACM, WAF. Ví dụ: ALB terminate TLS với cert từ ACM.
- 📝 Exam Tip: Từ khóa: "HTTPS only", "user sign-in", "OAuth" → nghĩ Cognito + ALB/CloudFront + ACM.
- 🧠 Mẹo nhớ: Nhớ: Đường vào app luôn là https + đăng nhập.

## Security services with appropriate use cases (for example, Amazon Cognito, Amazon GuardDuty, Amazon Macie)
- 📌 Giải thích ngắn: Mỗi dịch vụ giải một bài toán bảo mật riêng: identity, phát hiện đe dọa, bảo vệ dữ liệu nhạy cảm.
- 🛠 AWS Services / Ví dụ: Cognito (user pool), GuardDuty (threat detection), Macie (PII in S3).
- 📝 Exam Tip: Map từ khóa: user sign-in → Cognito; threat detection → GuardDuty; PII in S3 → Macie.
- 🧠 Mẹo nhớ: Nhớ: Cognito = login, GuardDuty = bảo vệ nhà, Macie = bảo vệ dữ liệu nhạy cảm.

## Threat vectors external to AWS (for example, DDoS, SQL injection)
- 📌 Giải thích ngắn: Hiểu các tấn công web phổ biến để chọn đúng dịch vụ bảo vệ.
- 🛠 AWS Services / Ví dụ: AWS Shield, AWS WAF, CloudFront, ALB. Ví dụ: WAF rule chặn SQL injection.
- 📝 Exam Tip: Từ khóa: "DDoS" → Shield/CloudFront; "OWASP", "SQL injection" → WAF.
- 🧠 Mẹo nhớ: Nhớ: Shield chống DDoS, WAF lọc request xấu.

## Designing VPC architectures with security components (for example, security groups, route tables, network ACLs, NAT gateways)
- 📌 Giải thích ngắn: VPC gồm subnet, route, SG, NACL, NAT, Internet Gateway để phân tách và bảo vệ mạng.
- 🛠 AWS Services / Ví dụ: VPC, Subnet, IGW, NAT Gateway, SG, NACL. Ví dụ: web ở public subnet, DB ở private subnet.
- 📝 Exam Tip: Thấy kiến trúc 3-tier web/app/db → web public, app+db private, NAT cho outbound, SG chặt.
- 🧠 Mẹo nhớ: Nhớ: Public cho front-end, private cho data.

## Determining network segmentation strategies (for example, using public subnets and private subnets)
- 📌 Giải thích ngắn: Chia mạng thành vùng public (có Internet) và private (không public IP) để giảm tấn công.
- 🛠 AWS Services / Ví dụ: VPC, Public/Private Subnet, NAT Gateway, Route Table. Ví dụ: EC2 backend chỉ ra Internet qua NAT.
- 📝 Exam Tip: Từ khóa: "no inbound from Internet" → private subnet + NAT. Không gán public IP cho DB.
- 🧠 Mẹo nhớ: Nhớ: Mặt tiền (public), kho hàng (private).

## Integrating AWS services to secure applications (for example, AWS Shield, AWS WAF, IAM Identity Center, AWS Secrets Manager)
- 📌 Giải thích ngắn: Kết hợp nhiều dịch vụ (WAF, Shield, Secrets, IAM) để tạo lớp bảo vệ nhiều tầng.
- 🛠 AWS Services / Ví dụ: AWS Shield, WAF, IAM Identity Center, Secrets Manager, CloudTrail.
- 📝 Exam Tip: Đề bài nói solution end-to-end security → chọn combo: WAF+Shield+CloudFront+Secrets+IAM role.
- 🧠 Mẹo nhớ: Nhớ: Nhiều lớp áo giáp tốt hơn một.

## Securing external network connections to and from the AWS Cloud (for example, VPN, AWS Direct Connect)
- 📌 Giải thích ngắn: Kết nối on-premises với AWS an toàn bằng VPN (IPsec) hoặc đường riêng Direct Connect.
- 🛠 AWS Services / Ví dụ: Site-to-Site VPN, AWS Direct Connect, Transit Gateway. Ví dụ: site-to-site VPN kết nối VPC với datacenter.
- 📝 Exam Tip: Từ khóa: "consistent bandwidth", "low latency" → Direct Connect; "quick, cheap" → VPN.
- 🧠 Mẹo nhớ: Nhớ: VPN = đường hầm Internet; DX = đường cáp riêng.

## Data access and governance
- 📌 Giải thích ngắn: Xác định ai được truy cập data nào, ở đâu, log lại đầy đủ. Liên quan đến compliance.
- 🛠 AWS Services / Ví dụ: IAM, Lake Formation, S3 bucket policy, KMS, CloudTrail.
- 📝 Exam Tip: Từ khóa: "data governance", "access control" → nghĩ IAM + S3 policy + Lake Formation/KMS.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu quý như vàng, phải có sổ ra vào.

## Data recovery
- 📌 Giải thích ngắn: Khả năng lấy lại dữ liệu sau khi xóa nhầm, hỏng, ransomware.
- 🛠 AWS Services / Ví dụ: RDS snapshots, S3 Versioning, Backup, Cross-Region Replication.
- 📝 Exam Tip: Từ khóa: "RPO/RTO", "restore" → dùng backup, snapshot, replica, multi-AZ.
- 🧠 Mẹo nhớ: Nhớ: Luôn có bản sao để quay ngược thời gian.

## Data retention and classification
- 📌 Giải thích ngắn: Chia dữ liệu theo độ quan trọng, thời gian lưu (ngắn, dài, archive) để tối ưu chi phí và tuân thủ.
- 🛠 AWS Services / Ví dụ: S3 Standard/IA/Glacier, S3 Lifecycle, Backup, RDS backup retention.
- 📝 Exam Tip: Thấy yêu cầu "compliance 7 years", "archive" → dùng Glacier + lifecycle.
- 🧠 Mẹo nhớ: Nhớ: Nóng (Standard), ấm (IA), lạnh (Glacier).

## Encryption and appropriate key management
- 📌 Giải thích ngắn: Mã hóa data bằng key, quản lý key an toàn, xoay vòng và kiểm soát ai dùng được.
- 🛠 AWS Services / Ví dụ: AWS KMS, CloudHSM, CMK, key policy.
- 📝 Exam Tip: Từ khóa: "customer managed keys", "FIPS" → KMS/CloudHSM. Không hard-code key trong app.
- 🧠 Mẹo nhớ: Nhớ: Chìa khoá của chìa khoá nằm ở KMS.

## Aligning AWS technologies to meet compliance requirements
- 📌 Giải thích ngắn: Chọn dịch vụ/funk phù hợp để đáp ứng PCI, HIPAA, GDPR... bằng logging, encryption, access control.
- 🛠 AWS Services / Ví dụ: CloudTrail, Config, KMS, Macie, Shield, Artifact (tài liệu compliance).
- 📝 Exam Tip: Thấy đề nói "audit", "compliance" → cần log (CloudTrail), cấu hình chuẩn (Config), mã hóa (KMS).
- 🧠 Mẹo nhớ: Nhớ: Audit = log; compliance = policy + log + encryption.

## Encrypting data at rest (for example, AWS Key Management Service [AWS KMS])
- 📌 Giải thích ngắn: Bật encryption cho các dịch vụ lưu trữ để nếu ổ đĩa bị lộ thì vẫn an toàn.
- 🛠 AWS Services / Ví dụ: KMS, S3 SSE-KMS, EBS encryption, RDS encryption.
- 📝 Exam Tip: Từ khóa: "encryption at rest" → bật SSE/EBS/RDS encryption với KMS CMK.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu ngủ phải được đắp chăn (mã hóa).

## Encrypting data in transit (for example, AWS Certificate Manager [ACM] using TLS)
- 📌 Giải thích ngắn: Dùng TLS/HTTPS để bảo vệ dữ liệu trên đường truyền.
- 🛠 AWS Services / Ví dụ: ACM (TLS cert), ALB/CloudFront HTTPS, API Gateway, TLS cho RDS.
- 📝 Exam Tip: Từ khóa: "SSL/TLS", "HTTPS only" → dùng ACM + ALB/API GW/CloudFront.
- 🧠 Mẹo nhớ: Nhớ: Mọi đường dây ra ngoài đều bọc áo TLS.

## Implementing access policies for encryption keys
- 📌 Giải thích ngắn: Xác định ai được dùng, quản trị, xoay vòng key KMS. Sai policy có thể khóa luôn dữ liệu.
- 🛠 AWS Services / Ví dụ: KMS key policy, IAM policy, Grants.
- 📝 Exam Tip: Luôn nhớ: key policy là gốc; nếu deny ở đây thì IAM cũng bó tay.
- 🧠 Mẹo nhớ: Nhớ: Chủ nhà là key policy, IAM chỉ là giấy giới thiệu.

## Implementing data backups and replications
- 📌 Giải thích ngắn: Giữ nhiều bản sao ở nhiều nơi/AZ/Region để tránh mất mát.
- 🛠 AWS Services / Ví dụ: S3 CRR, RDS Multi-AZ, EFS backup, AWS Backup.
- 📝 Exam Tip: Thấy yêu cầu "durability", "cross-Region" → replication; "restore point" → backup/snapshot.
- 🧠 Mẹo nhớ: Nhớ: Không để dữ liệu chỉ ở một chỗ.

## Implementing policies for data access, lifecycle, and protection
- 📌 Giải thích ngắn: Định nghĩa ai được đọc/ghi, lưu bao lâu, khi nào chuyển tier/xóa.
- 🛠 AWS Services / Ví dụ: S3 Bucket Policy, IAM, S3 Lifecycle, Object Lock, Retention.
- 📝 Exam Tip: Từ khóa: "WORM", "legal hold", "data retention" → S3 Object Lock + Lifecycle.
- 🧠 Mẹo nhớ: Nhớ: Có luật chơi rõ ràng cho từng loại file.

## Rotating encryption keys and renewing certificates
- 📌 Giải thích ngắn: Định kỳ thay key/cert để giảm rủi ro lộ thông tin lâu dài.
- 🛠 AWS Services / Ví dụ: KMS key rotation, ACM certificate renewal, Secrets Manager rotation.
- 📝 Exam Tip: Thấy "automatic rotation" → dùng Secrets Manager/KMS rotation; đừng tự viết script nếu không cần.
- 🧠 Mẹo nhớ: Nhớ: Mật khẩu, key, cert đều phải có hạn dùng.
