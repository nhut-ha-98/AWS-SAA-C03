# Flashcards – AWS SAA-C03

## Domain 1 – Design Secure Architectures

**Q1:** Nguyên tắc “least privilege” nghĩa là gì trên AWS?  
**A1:** Chỉ cấp đúng quyền cần dùng (IAM policy càng hẹp càng tốt), tránh quyền admin rộng.

**Q2:** Khi nào nên dùng AWS Organizations + SCP?  
**A2:** Khi có nhiều account và cần áp chính sách/guardrail tập trung cho toàn bộ tổ chức.

**Q3:** Truy cập cross-account an toàn nên dùng gì?  
**A3:** IAM Role + STS assume role, không chia sẻ access key hoặc dùng root.

**Q4:** Khi nào nên dùng IAM Identity Center (SSO) thay vì IAM user?  
**A4:** Khi muốn dùng tài khoản công ty/AD/IdP để login AWS, quản lý user tập trung.

**Q5:** Root user nên dùng cho việc gì?  
**A5:** Chỉ cho tác vụ đặc biệt (ví dụ bật MFA, đổi thông tin thanh toán), luôn bật MFA, không dùng access key.

**Q6:** Khác nhau chính giữa IAM policy và resource policy là gì?  
**A6:** IAM policy gán cho identity (user/role); resource policy gán cho resource (S3, KMS, SQS) để control cross-account/public.

**Q7:** Khi nào nên dùng S3 bucket policy thay vì chỉ IAM policy?  
**A7:** Khi cần cho account khác hoặc public truy cập bucket, hoặc muốn chặn/cho phép theo điều kiện IP, VPC Endpoint.

**Q8:** VPC Endpoint giúp giải quyết vấn đề gì?  
**A8:** Cho EC2 private subnet truy cập dịch vụ AWS (S3, DynamoDB…) mà không cần ra Internet/NAT.

**Q9:** Security Group khác Network ACL ở điểm chính nào?  
**A9:** SG stateful, áp cho ENI/instance; NACL stateless, áp cho subnet, thường dùng để chặn/allow theo IP rộng.

**Q10:** Dùng dịch vụ nào để quản lý mật khẩu, API key an toàn?  
**A10:** AWS Secrets Manager hoặc SSM Parameter Store (SecureString) + IAM role.

**Q11:** Muốn user sign-in vào ứng dụng với Facebook/Google hoặc tài khoản riêng, chọn dịch vụ nào?  
**A11:** Amazon Cognito (User Pool + Identity Pool nếu cần credential AWS).

**Q12:** Bảo vệ ứng dụng web khỏi SQL injection, XSS nên dùng gì?  
**A12:** AWS WAF đặt trước ALB/API Gateway/CloudFront, dùng rule OWASP.

**Q13:** Bảo vệ khỏi DDoS Layer 3/4 trên AWS như thế nào?  
**A13:** AWS Shield (Standard miễn phí, Advanced có thêm tính năng + hỗ trợ), kết hợp CloudFront/Route 53.

**Q14:** Mã hóa dữ liệu “at rest” thường dùng dịch vụ nào?  
**A14:** Kích hoạt encryption với AWS KMS trên S3, EBS, RDS, EFS… (SSE-KMS, EBS encrypted).

**Q15:** Mã hóa dữ liệu “in transit” cho web/app trên AWS dùng gì?  
**A15:** HTTPS/TLS với certificate từ AWS Certificate Manager (ACM) trên ALB/CloudFront/API Gateway.

**Q16:** KMS key policy có vai trò gì?  
**A16:** Là policy gốc quyết định ai có thể dùng/ quản trị key; nếu deny ở đây thì IAM cũng không override được.

**Q17:** Để đáp ứng yêu cầu audit/compliance (PCI, GDPR), 2 dịch vụ log/cấu hình quan trọng là gì?  
**A17:** AWS CloudTrail (log API) và AWS Config (theo dõi, đánh giá cấu hình resource).

**Q18:** Cần bảo vệ dữ liệu S3 chứa PII, nên nghĩ đến dịch vụ nào?  
**A18:** Amazon Macie (phát hiện PII) + KMS + S3 encryption + IAM/bucket policy chặt.

---

## Domain 2 – Design Resilient Architectures

**Q1:** Khi nào nên dùng API Gateway thay vì ALB làm API entry?  
**A1:** Khi cần throttling, API key, usage plan, integration với Lambda, stage/version.

**Q2:** Dịch vụ nào dùng cho pub/sub và dịch vụ nào cho queue điểm-điểm?  
**A2:** SNS cho pub/sub (fan-out), SQS cho queue (mỗi message cho 1 consumer).

**Q3:** Kiến trúc event-driven thường kết hợp các dịch vụ nào?  
**A3:** SNS/SQS/EventBridge + Lambda/ECS để xử lý async, loose coupling.

**Q4:** Ưu điểm chính của stateless service là gì?  
**A4:** Dễ scale ngang, thay instance không mất state (state để ở DB/queue/cache).

**Q5:** Multi-AZ và Multi-Region khác nhau về mục tiêu gì?  
**A5:** Multi-AZ cho HA trong một Region; Multi-Region cho DR/thảm họa cả Region.

**Q6:** Dịch vụ nào giúp load balancing HTTP/HTTPS và routing theo path/host?  
**A6:** Application Load Balancer (ALB).

**Q7:** Pattern DR rẻ nhất nhưng RTO cao là gì?  
**A7:** Backup & Restore (backup S3/snapshot, restore khi sự cố).

**Q8:** Pattern DR có RTO thấp nhất nhưng tốn nhất là gì?  
**A8:** Multi-Region Active-Active (nhiều Region cùng phục vụ).

**Q9:** Immutable infrastructure nghĩa là gì?  
**A9:** Không SSH chỉnh server đang chạy; thay đổi bằng cách tạo image/version mới và rollout (blue/green, ASG).

**Q10:** Dùng dịch vụ nào để điều phối workflow nhiều bước giữa Lambda/ECS?  
**A10:** AWS Step Functions (state machine, retry, branch).

**Q11:** Khi workload có burst traffic và cần buffer, nên thêm dịch vụ nào?  
**A11:** SQS hoặc Kinesis để hàng đợi/stream, sau đó worker scale theo queue depth.

**Q12:** Muốn HA cho RDS trong một Region nên dùng cấu hình nào?  
**A12:** RDS Multi-AZ (synchronous replica, automatic failover) – không phải read replica.

**Q13:** Khi nào dùng DynamoDB thay vì RDS cho resilience/scale?  
**A13:** Khi cần scale read/write rất lớn, low-latency, multi-Region dễ dàng (global tables).

**Q14:** Route 53 có thể dùng làm cơ chế gì cho HA?  
**A14:** DNS failover với health check, chuyển traffic qua endpoint dự phòng.

**Q15:** Dùng dịch vụ nào để tăng độ tin cậy kết nối DB khi nhiều Lambda/EC2?  
**A15:** Amazon RDS Proxy (connection pooling, ổn định).

**Q16:** Service quotas/throttling nên xử lý như thế nào trong design?  
**A16:** Thiết kế retry với exponential backoff, monitor CloudWatch, xin tăng quota khi cần.

**Q17:** Khi nào nên dùng AWS Global Accelerator thay vì CloudFront?  
**A17:** Khi tối ưu TCP/UDP traffic đến ALB/NLB/EC2 ở nhiều Region (anycast IP, health-based routing), không phải content caching.

**Q18:** Tại sao managed services thường resilient hơn tự host trên EC2?  
**A18:** Đã built-in multi-AZ, self-healing, patching, scaling; mình chỉ cấu hình.

---

## Domain 3 – Design High-Performing Architectures

**Q1:** S3, EFS, EBS khác nhau chính về use case gì?  
**A1:** S3 cho object lớn/backup/log, EFS cho share file POSIX giữa nhiều instance, EBS cho disk gắn 1 instance/AZ.

**Q2:** Khi workload DB cần IOPS rất cao, nên chọn loại EBS nào?  
**A2:** io1/io2 (Provisioned IOPS SSD); còn general purpose → gp3.

**Q3:** Dịch vụ nào phù hợp nhất cho big data Hadoop/Spark?  
**A3:** Amazon EMR (cluster big data managed).

**Q4:** Workload event-driven, gián đoạn, traffic khó đoán, compute nên là gì?  
**A4:** AWS Lambda (serverless), có thể kèm API Gateway/SQS.

**Q5:** ECS và EKS khác gì về mức độ “AWS native”?  
**A5:** ECS là native AWS đơn giản hơn; EKS là Kubernetes managed, hợp khi đã dùng K8s/multi-cloud.

**Q6:** Để autoscale EC2 theo CPU, nên dùng thành phần nào?  
**A6:** Auto Scaling Group + CloudWatch metric (target tracking hoặc step scaling).

**Q7:** Dịch vụ nào dùng để cache trước DB/API để tăng tốc read?  
**A7:** Amazon ElastiCache (Redis/Memcached), hoặc DAX cho DynamoDB.

**Q8:** Read-heavy workload trên RDS nên tối ưu bằng gì trước khi scale vertical?  
**A8:** Thêm read replicas + cache (ElastiCache) cho truy vấn hay đọc.

**Q9:** Khi nào nên dùng DynamoDB thay vì RDS về mặt hiệu năng?  
**A9:** Khi cần low-latency ms, scale đọc/ghi cực lớn, schema key-value.

**Q10:** Để phân tích dữ liệu trên S3 bằng SQL mà không dựng cluster, chọn gì?  
**A10:** Amazon Athena (serverless query trên S3).

**Q11:** Định dạng nào giúp truy vấn analytic trên S3 nhanh và rẻ hơn CSV?  
**A11:** Parquet (columnar) hoặc ORC (ít đọc disk hơn).

**Q12:** Chức năng chính của AWS Glue trong pipeline dữ liệu là gì?  
**A12:** ETL serverless (discover schema, transform, convert format, catalog).

**Q13:** Khác biệt chính giữa batch ingest và streaming ingest?  
**A13:** Batch theo đợt (phút/giờ/ngày), streaming near real-time; streaming dùng Kinesis/MSK.

**Q14:** Khi nào dùng Kinesis Firehose thay vì Kinesis Data Streams?  
**A14:** Khi chỉ cần đưa dữ liệu liên tục vào S3/Redshift/OpenSearch mà không cần app tự đọc stream.

**Q15:** QuickSight dùng để làm gì?  
**A15:** BI/dashboards trực quan cho business user, đọc từ RDS, Athena, Redshift, S3…

**Q16:** Vì sao nên đặt compute gần dữ liệu?  
**A16:** Giảm latency, giảm data transfer, tăng throughput (ví dụ EMR cùng Region với S3 data lake).

**Q17:** Global users xem nội dung tĩnh, dịch vụ nào giúp tăng tốc tốt nhất?  
**A17:** Amazon CloudFront (CDN, edge cache).

**Q18:** Để tối ưu chi phí nhưng vẫn high-performance cho DynamoDB, nên chú ý gì?  
**A18:** Chọn RCU/WCU phù hợp, dùng auto scaling hoặc on-demand, thiết kế partition key tốt.

**Q19:** Metric chính để scale Lambda là gì?  
**A19:** Concurrency (số request đang xử lý) + duration; có thể giới hạn concurrency để bảo vệ backend.

**Q20:** Khi thiết kế network high-performance, cần lưu ý gì về AZ/Region?  
**A20:** Đặt app, DB, storage trong cùng Region/và thường cùng AZ khi cần latency thấp, tránh cross-Region/AZ nếu không cần.

---

## Domain 4 – Design Cost-Optimized Architectures

**Q1:** S3 Requester Pays dùng cho tình huống nào?  
**A1:** Khi nhiều bên ngoài tải dữ liệu và bạn muốn họ tự trả tiền data transfer.

**Q2:** Ba công cụ chính để quản lý/giám sát chi phí AWS là gì?  
**A2:** Cost Explorer (phân tích), AWS Budgets (cảnh báo), Cost and Usage Report – CUR (chi tiết sâu).

**Q3:** Dùng gì để phân bổ chi phí theo team/project?  
**A3:** Cost allocation tags + AWS Organizations (consolidated billing).

**Q4:** Dữ liệu ít truy cập nhưng vẫn cần multi-AZ, nên dùng S3 class nào?  
**A4:** S3 Standard-IA (Infrequent Access).

**Q5:** Dữ liệu backup lâu năm, hiếm khi restore, tier nào rẻ nhất?  
**A5:** S3 Glacier Deep Archive (rất rẻ, restore chậm).

**Q6:** HDD-based EBS (st1/sc1) phù hợp dạng workload nào?  
**A6:** Throughput-intensive, sequential IO (big data scan, log), không cần IOPS thấp latency.

**Q7:** Làm sao tự động chuyển log cũ từ S3 Standard sang Glacier để giảm cost?  
**A7:** Cấu hình S3 Lifecycle rule (transition + expiration).

**Q8:** Khi nào nên dùng Intelligent-Tiering cho S3?  
**A8:** Khi không biết rõ pattern truy cập; để AWS tự chuyển tier tối ưu chi phí.

**Q9:** Di chuyển hàng chục TB dữ liệu một lần từ on-prem lên S3 nên chọn gì?  
**A9:** AWS Snowball (offline), thay vì upload liên tục qua Internet.

**Q10:** Sync dữ liệu on-prem ↔ S3 theo lịch định kỳ, dịch vụ phù hợp là?  
**A10:** AWS DataSync (tối ưu băng thông, incremental).

**Q11:** Khi tối ưu compute cost, workload ổn định 24/7 nên dùng pricing nào?  
**A11:** Reserved Instances hoặc Savings Plans (Compute/EC2) để giảm giá so với On-Demand.

**Q12:** Spot Instances phù hợp cho loại workload nào?  
**A12:** Job linh hoạt, batch, test, có thể dừng/gián đoạn mà không ảnh hưởng lớn.

**Q13:** Dev/test environment thường tối ưu cost bằng 2 cách nào?  
**A13:** Dùng Spot + tắt/schedule off giờ không làm việc (EC2/offline environment).

**Q14:** Compute Optimizer giúp việc gì?  
**A14:** Gợi ý thu nhỏ/phóng to EC2/RDS/Auto Scaling để tránh under/over-provision.

**Q15:** Workload ít request, không 24/7, compute rẻ nhất thường là gì?  
**A15:** AWS Lambda (pay-per-request) thay vì EC2 luôn bật.

**Q16:** Không phải workload nào cũng cần Multi-AZ/Multi-Region – ví dụ nào có thể đơn giản hơn để tiết kiệm?  
**A16:** Dev/test, tool nội bộ, hệ thống chấp nhận downtime ngắn → có thể single-AZ + backup thôi.

**Q17:** Để giảm chi phí NAT Gateway nhưng chấp nhận giảm HA, có thể làm gì?  
**A17:** Dùng 1 NAT Gateway shared cho nhiều private subnet thay vì mỗi AZ 1 cái.

**Q18:** Cross-Region data transfer thường có chi phí thế nào so với trong cùng Region?  
**A18:** Đắt hơn; nên giữ traffic trong cùng Region/VPC nếu không có lý do thật sự.

**Q19:** CDN (CloudFront) có giúp giảm chi phí không, ngoài tăng tốc?  
**A19:** Có, vì cache tại edge giảm lượng data egress từ Region và giảm load compute/origin.

**Q20:** Khi nào Direct Connect có thể rẻ hơn VPN về dài hạn?  
**A20:** Khi traffic ổn định, volume lớn; chi phí băng thông Internet/VPN lâu dài có thể cao hơn DX.
