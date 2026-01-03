# Domain 2 – Design Resilient Architectures

## API creation and management (for example, Amazon API Gateway, REST API)
- 📌 Giải thích ngắn: Thiết kế cổng vào cho dịch vụ backend, tách client khỏi server.
- 🛠 AWS Services / Ví dụ: Amazon API Gateway, Lambda, ECS, ALB. Ví dụ: API Gateway nhận request REST, gọi Lambda xử lý.
- 📝 Exam Tip: Từ khóa: "rate limiting", "API key", "REST/HTTP API" → nghiêng về API Gateway.
- 🧠 Mẹo nhớ: Nhớ: API Gateway là cửa chính vào microservice.

## AWS managed services with appropriate use cases (for example, AWS Transfer Family, Amazon Simple Queue Service [Amazon SQS], Secrets Manager)
- 📌 Giải thích ngắn: Giao việc hạ tầng (patch, scale cơ bản) cho AWS, mình tập trung logic.
- 🛠 AWS Services / Ví dụ: SQS, SNS, Secrets Manager, Transfer Family. Ví dụ: dùng SQS thay vì tự dựng hàng đợi RabbitMQ.
- 📝 Exam Tip: Câu hỏi muốn ít quản trị, scale dễ, HA cao → ưu tiên managed service.
- 🧠 Mẹo nhớ: Nhớ: Managed = AWS lo, mình dùng.

## Caching strategies
- 📌 Giải thích ngắn: Lưu tạm dữ liệu hay truy cập để giảm load backend, tăng tốc.
- 🛠 AWS Services / Ví dụ: ElastiCache (Redis/Memcached), CloudFront, API Gateway cache.
- 📝 Exam Tip: Từ khóa: "low latency reads", "frequent reads" → dùng cache trước khi scale DB.
- 🧠 Mẹo nhớ: Nhớ: Cache như tủ lạnh mini bên cạnh, khỏi chạy ra kho.

## Design principles for microservices (for example, stateless workloads compared with stateful workloads)
- 📌 Giải thích ngắn: Stateless không giữ trạng thái trên instance, dễ scale. Stateful giữ state, khó scale ngang.
- 🛠 AWS Services / Ví dụ: Lambda, ECS/Fargate, DynamoDB, RDS.
- 📝 Exam Tip: Thấy yêu cầu scale nhanh, HA cao → thiết kế stateless, state đưa vào DB/queue.
- 🧠 Mẹo nhớ: Nhớ: Service không giữ đồ, gửi hết vào kho chung.

## Event-driven architectures
- 📌 Giải thích ngắn: Thành phần giao tiếp qua sự kiện, không gọi trực tiếp. Dễ tách và scale độc lập.
- 🛠 AWS Services / Ví dụ: EventBridge, SNS, SQS, Kinesis, Lambda.
- 📝 Exam Tip: Từ khóa: "decoupled", "event", "asynchronous" → dùng SNS/SQS/EventBridge + Lambda.
- 🧠 Mẹo nhớ: Nhớ: Ai xong việc thì bắn tín hiệu, người cần nghe sẽ tự nghe.

## Horizontal scaling and vertical scaling
- 📌 Giải thích ngắn: Scale ngang: thêm instance. Scale dọc: tăng cấu hình một instance.
- 🛠 AWS Services / Ví dụ: EC2 Auto Scaling, RDS instance size, ECS tasks.
- 📝 Exam Tip: Ưu tiên scale ngang để HA; scale dọc chỉ là tạm thời hoặc giới hạn.
- 🧠 Mẹo nhớ: Nhớ: Nhiều xe nhỏ (ngang) an toàn hơn một xe tải khổng lồ (dọc).

## How to appropriately use edge accelerators (for example, content delivery network [CDN])
- 📌 Giải thích ngắn: Đặt nội dung/giao tiếp gần user để giảm latency, tăng độ tin cậy.
- 🛠 AWS Services / Ví dụ: CloudFront, AWS Global Accelerator.
- 📝 Exam Tip: Tĩnh/content web → CloudFront; TCP/UDP, multi-Region active-active → Global Accelerator.
- 🧠 Mẹo nhớ: Nhớ: CloudFront cho file/web, GA cho traffic tới app.

## How to migrate applications into containers
- 📌 Giải thích ngắn: Đóng gói ứng dụng thành container để chạy đồng nhất mọi môi trường.
- 🛠 AWS Services / Ví dụ: ECS, EKS, Fargate, ECR.
- 📝 Exam Tip: Từ khóa: "lift-and-shift", "containerized" → ECS/EKS; muốn không quản EC2 → Fargate.
- 🧠 Mẹo nhớ: Nhớ: Container = hộp đóng gói app + phụ thuộc.

## Load balancing concepts (for example, Application Load Balancer)
- 📌 Giải thích ngắn: Phân phối traffic tới nhiều instance để tránh quá tải, tăng HA.
- 🛠 AWS Services / Ví dụ: ALB, NLB, CLB, Gateway Load Balancer.
- 📝 Exam Tip: HTTP/HTTPS, path-based → ALB; TCP tốc độ cao → NLB; firewall appliances → GWLB.
- 🧠 Mẹo nhớ: Nhớ: ALB hiểu HTTP, NLB chỉ quan tâm port/IP.

## Multi-tier architectures
- 📌 Giải thích ngắn: Chia ứng dụng thành các tầng: web, app, DB để dễ quản và bảo mật.
- 🛠 AWS Services / Ví dụ: EC2/ALB (web), ECS/Lambda (app), RDS/DynamoDB (DB).
- 📝 Exam Tip: Câu hỏi mẫu 3-tier web app luôn: ALB → EC2/ECS/Lambda → RDS/DynamoDB trong private subnet.
- 🧠 Mẹo nhớ: Nhớ: Web nói chuyện App, App nói chuyện DB.

## Queuing and messaging concepts (for example, publish/subscribe)
- 📌 Giải thích ngắn: Hàng đợi và pub/sub giúp tách rời producer-consumer, chống mất message.
- 🛠 AWS Services / Ví dụ: SQS (queue), SNS (pub/sub), EventBridge.
- 📝 Exam Tip: Cần đảm bảo mỗi message xử lý một lần → SQS; broadcast nhiều subscriber → SNS.
- 🧠 Mẹo nhớ: Nhớ: SNS = phát loa, SQS = hàng xếp chờ.

## Serverless technologies and patterns (for example, AWS Fargate, AWS Lambda)
- 📌 Giải thích ngắn: Chạy code mà không quản EC2, trả tiền theo request/thời gian chạy. Scale tự động.
- 🛠 AWS Services / Ví dụ: Lambda, Fargate, DynamoDB, API Gateway.
- 📝 Exam Tip: Cần scale mạnh, workload gián đoạn, traffic không ổn định → ưu tiên serverless.
- 🧠 Mẹo nhớ: Nhớ: Không thuê nhà (server), chỉ thuê theo giờ dùng.

## Storage types with associated characteristics (for example, object, file, block)
- 📌 Giải thích ngắn: Mỗi kiểu lưu trữ phù hợp một use case: file lớn, share file, gắn vào instance.
- 🛠 AWS Services / Ví dụ: S3 (object), EFS/FSx (file), EBS (block).
- 📝 Exam Tip: Backup, log, media → S3; share file giữa server → EFS/FSx; disk cho EC2 → EBS.
- 🧠 Mẹo nhớ: Nhớ: S3 = kho đồ; EFS = thư mục dùng chung; EBS = ổ cứng máy.

## The orchestration of containers (for example, Amazon Elastic Container Service [Amazon ECS], Amazon Elastic Kubernetes Service [Amazon EKS])
- 📌 Giải thích ngắn: Điều phối container: scheduling, scale, healthcheck. ECS/AWS native, EKS/Kubernetes.
- 🛠 AWS Services / Ví dụ: Amazon ECS, EKS, Fargate.
- 📝 Exam Tip: Muốn đơn giản, AWS-native → ECS; có kinh nghiệm K8s hoặc multi-cloud → EKS.
- 🧠 Mẹo nhớ: Nhớ: ECS = AWS lái xe; EKS = bạn lái xe với xe Kubernetes.

## When to use read replicas
- 📌 Giải thích ngắn: Tạo bản sao chỉ-read để giảm tải DB chính, scale đọc.
- 🛠 AWS Services / Ví dụ: RDS Read Replicas, Aurora Replicas, DynamoDB DAX (cache).
- 📝 Exam Tip: Từ khóa: "read-heavy", "reporting" → dùng read replica; không dùng để HA chính thay cho Multi-AZ.
- 🧠 Mẹo nhớ: Nhớ: Master ghi, replica đọc.

## Workflow orchestration (for example, AWS Step Functions)
- 📌 Giải thích ngắn: Điều phối nhiều bước Lambda/service theo flow, có retry, trạng thái.
- 🛠 AWS Services / Ví dụ: AWS Step Functions, Lambda, ECS.
- 📝 Exam Tip: Từ khóa: "state machine", "long-running workflow" → Step Functions + Lambda.
- 🧠 Mẹo nhớ: Nhớ: Step Functions = sơ đồ công việc có từng bước rõ ràng.

## Designing event-driven, microservice, and/or multi-tier architectures based on requirements
- 📌 Giải thích ngắn: Kết hợp các pattern để tăng độ linh hoạt, chịu lỗi và scale độc lập.
- 🛠 AWS Services / Ví dụ: API Gateway, Lambda, ECS, EventBridge, SQS, RDS/DynamoDB.
- 📝 Exam Tip: Đề bài nói "loosely coupled", "independent scaling" → chọn microservice + event + queue.
- 🧠 Mẹo nhớ: Nhớ: Mỗi dịch vụ làm một việc, nói chuyện qua sự kiện.

## Determining scaling strategies for components used in an architecture design
- 📌 Giải thích ngắn: Mỗi phần (web, app, DB, cache) scale khác nhau tùy workload.
- 🛠 AWS Services / Ví dụ: EC2 Auto Scaling, Aurora Auto Scaling, DynamoDB Auto Scaling, Lambda concurrency.
- 📝 Exam Tip: Chú ý metric: CPU cho EC2, RCU/WCU cho DynamoDB, concurrency cho Lambda.
- 🧠 Mẹo nhớ: Nhớ: Đo đúng chỉ số, mới scale đúng chỗ.

## Determining the AWS services required to achieve loose coupling based on requirements
- 📌 Giải thích ngắn: Tách thành phần để một bên lỗi không kéo sập cả hệ thống.
- 🛠 AWS Services / Ví dụ: SQS, SNS, EventBridge, S3 (as buffer).
- 📝 Exam Tip: Cần retry, chống burst, không mất message → dùng queue/topic/event bus.
- 🧠 Mẹo nhớ: Nhớ: Đặt hộp thư (queue/topic) giữa các dịch vụ.

## Determining when to use containers
- 📌 Giải thích ngắn: Ứng dụng lâu chạy, nhiều phụ thuộc, cần kiểm soát runtime hơn Lambda.
- 🛠 AWS Services / Ví dụ: ECS/EKS trên EC2 hoặc Fargate.
- 📝 Exam Tip: Di chuyển app từ on-prem (microservice, web) → container; batch ngắn, event nhỏ → cân nhắc Lambda.
- 🧠 Mẹo nhớ: Nhớ: App quá to/đặc biệt so với Lambda thì bỏ vào container.

## Determining when to use serverless technologies and patterns
- 📌 Giải thích ngắn: Workload ngắn, không liên tục, không muốn quản server, traffic khó đoán.
- 🛠 AWS Services / Ví dụ: Lambda, Fargate, DynamoDB, API Gateway.
- 📝 Exam Tip: Thấy "unpredictable traffic", "spiky", "pay per use" → serverless là ứng viên số 1.
- 🧠 Mẹo nhớ: Nhớ: Không traffic thì gần như không tốn tiền.

## Recommending appropriate compute, storage, networking, and database technologies based on requirements
- 📌 Giải thích ngắn: Dựa vào pattern đọc/ghi, latency, throughput, chi phí để chọn kết hợp dịch vụ.
- 🛠 AWS Services / Ví dụ: EC2/ECS/Lambda, S3/EFS/EBS, RDS/DynamoDB, CloudFront, ALB.
- 📝 Exam Tip: Đọc kỹ yêu cầu: transaction vs analytics, burst vs steady, size data, RPO/RTO.
- 🧠 Mẹo nhớ: Nhớ: Không có one-size-fits-all, luôn là "it depends" nhưng có pattern rõ.

## Using purpose-built AWS services for workloads
- 📌 Giải thích ngắn: Mỗi dịch vụ được tối ưu cho một kiểu workload: key-value, time series, data warehouse...
- 🛠 AWS Services / Ví dụ: DynamoDB, Timestream, Redshift, ElastiCache, S3.
- 📝 Exam Tip: Từ khóa: "time series" → Timestream; "data warehouse" → Redshift; "key-value" → DynamoDB.
- 🧠 Mẹo nhớ: Nhớ: Dùng búa cho đinh, dùng kìm cho ốc.

## AWS global infrastructure (for example, Availability Zones, AWS Regions, Amazon Route 53)
- 📌 Giải thích ngắn: Thiết kế app chạy được khi một AZ hoặc cả Region gặp sự cố.
- 🛠 AWS Services / Ví dụ: Multi-AZ EC2/RDS, Multi-Region S3/Route 53, Global Accelerator.
- 📝 Exam Tip: "Multi-AZ" cho lỗi hạ tầng nhỏ; "multi-Region" cho DR lớn; Route 53 health check để failover.
- 🧠 Mẹo nhớ: Nhớ: AZ để chống lỗi nhỏ, Region để chống thảm họa.

## AWS managed services with appropriate use cases (for example, Amazon Comprehend, Amazon Polly)
- 📌 Giải thích ngắn: Các dịch vụ như Comprehend, Polly… là fully managed, scale sẵn, ít lo HA.
- 🛠 AWS Services / Ví dụ: Amazon Comprehend, Polly, Rekognition, Transcribe.
- 📝 Exam Tip: Câu hỏi về NLP, text analysis, text-to-speech mà không nói ML model → chọn dịch vụ managed.
- 🧠 Mẹo nhớ: Nhớ: Đã có dịch vụ làm sẵn, không cần tự xây.

## Basic networking concepts (for example, route tables)
- 📌 Giải thích ngắn: Route table quyết định traffic từ subnet đi đâu. Sai route có thể làm mất kết nối.
- 🛠 AWS Services / Ví dụ: VPC, Route Table, IGW, NAT, TGW.
- 📝 Exam Tip: Internet access cần default route 0.0.0.0/0 tới IGW; private outbound cần route tới NAT.
- 🧠 Mẹo nhớ: Nhớ: Route table = bản đồ đường đi trong VPC.

## Disaster recovery (DR) strategies (for example, backup and restore, pilot light, warm standby, active-active failover, recovery point objective [RPO], recovery time objective [RTO])
- 📌 Giải thích ngắn: Nhiều chiến lược DR với chi phí vs RPO/RTO khác nhau.
- 🛠 AWS Services / Ví dụ: Backup & Restore, Pilot Light, Warm Standby, Multi-Region Active-Active.
- 📝 Exam Tip: RPO/RTO thấp → warm standby/active-active; chi phí thấp → backup/restore hoặc pilot light.
- 🧠 Mẹo nhớ: Nhớ: Giá càng cao thì downtime càng ít.

## Distributed design patterns
- 📌 Giải thích ngắn: Thiết kế hệ thống phân tán, không phụ thuộc vào một điểm, tự phục hồi.
- 🛠 AWS Services / Ví dụ: ALB, Auto Scaling, SQS, SNS, multi-AZ, caching.
- 📝 Exam Tip: Tập trung tránh single point of failure, thêm retry, backoff, idempotency.
- 🧠 Mẹo nhớ: Nhớ: Không để cả đội ngồi trên một chiếc ghế.

## Failover strategies
- 📌 Giải thích ngắn: Tự động chuyển traffic sang hệ thống dự phòng khi hệ chính lỗi.
- 🛠 AWS Services / Ví dụ: Route 53 failover, Multi-AZ RDS, Global Accelerator, health checks.
- 📝 Exam Tip: Từ khóa: "automatic failover" → Route 53 + health check, Multi-AZ DB.
- 🧠 Mẹo nhớ: Nhớ: Luôn có sân phụ chờ sẵn.

## Immutable infrastructure
- 📌 Giải thích ngắn: Không chỉnh sửa server đang chạy; cập nhật bằng cách tạo instance mới từ AMI mới.
- 🛠 AWS Services / Ví dụ: EC2 Auto Scaling + Launch Template, CodeDeploy blue/green.
- 📝 Exam Tip: Từ khóa: "immutable", "blue/green" → tạo môi trường mới rồi chuyển traffic, không SSH sửa tay.
- 🧠 Mẹo nhớ: Nhớ: Server như đĩa CD, ghi xong là chỉ đọc.

## Load balancing concepts (for example, Application Load Balancer)
- 📌 Giải thích ngắn: LB gửi traffic tới nhiều target ở nhiều AZ, nếu một target/AZ chết thì traffic chuyển nơi khác.
- 🛠 AWS Services / Ví dụ: ALB, NLB, Target Group, Auto Scaling.
- 📝 Exam Tip: Đảm bảo target ở ít nhất 2 AZ; health check quan trọng để failover.
- 🧠 Mẹo nhớ: Nhớ: LB như người điều phối xe bus ra nhiều tuyến.

## Proxy concepts (for example, Amazon RDS Proxy)
- 📌 Giải thích ngắn: Proxy giúp quản lý pool connection, tăng độ ổn định, che DB khỏi client.
- 🛠 AWS Services / Ví dụ: RDS Proxy, NLB/ALB làm reverse proxy.
- 📝 Exam Tip: Serverless (Lambda) kết nối RDS → dùng RDS Proxy để tránh quá nhiều connection.
- 🧠 Mẹo nhớ: Nhớ: Proxy là người gác cổng cho DB.

## Service quotas and throttling (for example, how to configure the service quotas for a workload in a standby environment)
- 📌 Giải thích ngắn: Mỗi dịch vụ có giới hạn (quota). Vượt quá sẽ bị throttling, có thể gây lỗi.
- 🛠 AWS Services / Ví dụ: Service Quotas, CloudWatch, exponential backoff.
- 📝 Exam Tip: Thấy lỗi ThrottlingException → implement retry + backoff hoặc xin tăng quota.
- 🧠 Mẹo nhớ: Nhớ: Đường ống có đường kính giới hạn, bơm quá mạnh sẽ bị nghẽn.

## Storage options and characteristics (for example, durability, replication)
- 📌 Giải thích ngắn: Mỗi loại lưu trữ có durability, độ replicate khác nhau, ảnh hưởng đến HA.
- 🛠 AWS Services / Ví dụ: S3 (11x9), EBS, EFS, RDS Multi-AZ, Aurora.
- 📝 Exam Tip: Cần durability rất cao, multi-AZ → S3/Aurora; EBS là volume AZ-level, cần snapshot để bảo vệ.
- 🧠 Mẹo nhớ: Nhớ: S3 gần như không mất dữ liệu, EBS thì vẫn có rủi ro.

## Workload visibility (for example, AWS X-Ray)
- 📌 Giải thích ngắn: Theo dõi request, log, metric để phát hiện lỗi và bottleneck.
- 🛠 AWS Services / Ví dụ: CloudWatch, X-Ray, CloudTrail, OpenSearch.
- 📝 Exam Tip: Microservices khó debug → dùng X-Ray để trace end-to-end.
- 🧠 Mẹo nhớ: Nhớ: X-Ray như chụp phim toàn bộ đường đi request.

## Determining automation strategies to ensure infrastructure integrity
- 📌 Giải thích ngắn: Dùng IaC/automation để tạo lại hạ tầng chuẩn, tránh cấu hình tay lệch chuẩn.
- 🛠 AWS Services / Ví dụ: CloudFormation, CDK, Terraform, Config, Systems Manager.
- 📝 Exam Tip: Từ khóa: "consistent environment", "repeatable" → IaC, không click tay.
- 🧠 Mẹo nhớ: Nhớ: Hạ tầng là code, không phải tài liệu Word.

## Determining the AWS services required to provide a highly available and/or fault-tolerant architecture across AWS Regions or Availability Zones
- 📌 Giải thích ngắn: Kết hợp LB, Auto Scaling, Multi-AZ, Multi-Region để vẫn chạy khi có lỗi.
- 🛠 AWS Services / Ví dụ: ALB + ASG, RDS Multi-AZ, Aurora Global Database, S3 CRR, Route 53.
- 📝 Exam Tip: Đề bài nhắc "HA" nhưng không quá khắt khe → Multi-AZ; nhắc "Region failure" → Multi-Region với Route 53.
- 🧠 Mẹo nhớ: Nhớ: AZ cho high availability, Region cho disaster recovery.

## Identifying metrics based on business requirements to deliver a highly available solution
- 📌 Giải thích ngắn: Chọn metric phù hợp để alarm & scale: lỗi, latency, CPU, queue depth…
- 🛠 AWS Services / Ví dụ: CloudWatch metrics/alarms, SLO/SLA.
- 📝 Exam Tip: Đừng chỉ nhìn CPU; web app nên nhìn 5xx, latency, queue length.
- 🧠 Mẹo nhớ: Nhớ: Đo đúng cái đang đau, không phải cái dễ đo.

## Implementing designs to mitigate single points of failure
- 📌 Giải thích ngắn: Bất kỳ thành phần nào nếu hỏng làm sập cả hệ thống thì phải có dự phòng.
- 🛠 AWS Services / Ví dụ: Multi-AZ, multiple instances, redundant NAT, Route 53 failover.
- 📝 Exam Tip: Một NAT Gateway cho cả Region → có thể là SPOF trong một AZ; tốt hơn mỗi AZ một NAT nếu HA ưu tiên hơn chi phí.
- 🧠 Mẹo nhớ: Nhớ: Không để một mắt xích quyết định cả dây chuyền.

## Implementing strategies to ensure the durability and availability of data (for example, backups)
- 📌 Giải thích ngắn: Kết hợp backup, replication, multi-AZ/Region để dữ liệu luôn có và không mất.
- 🛠 AWS Services / Ví dụ: S3 versioning + CRR, RDS/Aurora Multi-AZ + backup, DynamoDB global tables.
- 📝 Exam Tip: Bài toán RPO=0 gần như → synchronous replication (Multi-AZ); RPO>0 → async replication/backup.
- 🧠 Mẹo nhớ: Nhớ: Một bản hiện tại, một bản ở chỗ khác, thêm bản snapshot.

## Selecting an appropriate DR strategy to meet business requirements
- 📌 Giải thích ngắn: Match chiến lược DR với RPO/RTO và ngân sách.
- 🛠 AWS Services / Ví dụ: Backup/Restore, Pilot Light, Warm Standby, Multi-Region Active-Active.
- 📝 Exam Tip: Câu hỏi so sánh nhiều lựa chọn DR → nhớ thứ tự: rẻ/slow (backup) → trung bình (pilot/warm) → đắt/nhanh (active-active).
- 🧠 Mẹo nhớ: Nhớ: RTO càng nhỏ, tiền càng nhiều.

## Using AWS services that improve the reliability of legacy applications and applications not built for the cloud (for example, when application changes are not possible)
- 📌 Giải thích ngắn: Dùng LB, ASG, managed DB… bọc quanh app cũ mà không cần sửa code lớn.
- 🛠 AWS Services / Ví dụ: ALB + Auto Scaling EC2, RDS thay tự host DB, FSx/EFS share file.
- 📝 Exam Tip: Nếu không đổi code được, hãy đổi hạ tầng xung quanh để có HA/backup.
- 🧠 Mẹo nhớ: Nhớ: Không sửa máy, nhưng có thể thay khung và bánh xe.

## Using purpose-built AWS services for workloads
- 📌 Giải thích ngắn: Chọn dịch vụ vốn được thiết kế để chịu lỗi tốt (multi-AZ, self-healing).
- 🛠 AWS Services / Ví dụ: Aurora, DynamoDB, S3, Lambda, SQS.
- 📝 Exam Tip: Fully managed, multi-AZ by default thường là đáp án tốt cho reliability.
- 🧠 Mẹo nhớ: Nhớ: Dịch vụ serverless/managed thường mặc định bền và sẵn sàng cao.
