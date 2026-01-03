# Domain 3 – Design High-Performing Architectures

### Hybrid storage solutions to meet business requirements
- 📌 Giải thích ngắn: Kết hợp on-prem và cloud để tối ưu hiệu năng, latency và chi phí.
- 🛠 AWS Services / Ví dụ: Storage Gateway, DataSync, Direct Connect, S3, EFS. Ví dụ: app on-prem truy cập file lưu trên S3 qua File Gateway.
- 📝 Exam Tip: Từ khóa: "low latency access from on-prem" → Storage Gateway hoặc local cache; nhiều data cần migrate → DataSync.
- 🧠 Mẹo nhớ: Nhớ: Một chân ở datacenter, một chân ở S3.

### Storage services with appropriate use cases (for example, Amazon S3, Amazon Elastic File System [Amazon EFS], Amazon Elastic Block Store [Amazon EBS])
- 📌 Giải thích ngắn: Mỗi dịch vụ lưu trữ tối ưu cho kiểu workload khác nhau.
- 🛠 AWS Services / Ví dụ: S3 (object), EFS (file share), EBS (block), FSx (Windows/Lustre).
- 📝 Exam Tip: Ứng dụng cần disk gắn vào EC2 → EBS; nhiều instance share file → EFS/FSx; backup/log/media → S3.
- 🧠 Mẹo nhớ: Nhớ: EBS cho 1 máy, EFS cho nhiều máy, S3 cho object.

### Storage types with associated characteristics (for example, object, file, block)
- 📌 Giải thích ngắn: Object: metadata + key. File: cấu trúc thư mục. Block: block thô. Hiểu để đoán performance/giới hạn.
- 🛠 AWS Services / Ví dụ: S3 (object), EFS/FSx (file), EBS (block).
- 📝 Exam Tip: Performance cao, IO random → block (EBS); POSIX, share file → file; scale lớn, rẻ → object.
- 🧠 Mẹo nhớ: Nhớ: Object = file + metadata; block = viên gạch; file = thư mục.

### Determining storage services and configurations that meet performance demands
- 📌 Giải thích ngắn: Điều chỉnh loại volume, IOPS, throughput để đáp ứng workload.
- 🛠 AWS Services / Ví dụ: EBS gp3/io1/io2, EFS throughput mode, S3 Transfer Acceleration.
- 📝 Exam Tip: DB production, IO cao → io1/io2 Provisioned IOPS; general → gp3; throughput file share → cấu hình EFS.
- 🧠 Mẹo nhớ: Nhớ: IOPS cao thì chọn io1/io2, còn lại gp3.

### Determining storage services that can scale to accommodate future needs
- 📌 Giải thích ngắn: Chọn dịch vụ tự scale hoặc dễ mở rộng khi data tăng nhiều.
- 🛠 AWS Services / Ví dụ: S3, EFS, Aurora, DynamoDB, FSx Lustre.
- 📝 Exam Tip: Cần petabyte, scale gần vô hạn → S3; file share tăng dần → EFS; DB scale read tự động → Aurora.
- 🧠 Mẹo nhớ: Nhớ: Dùng dịch vụ "serverless-like" thì scale đỡ đau đầu.

### AWS compute services with appropriate use cases (for example, AWS Batch, Amazon EMR, Fargate)
- 📌 Giải thích ngắn: Mỗi dịch vụ compute phù hợp kiểu workload: batch, big data, API, container…
- 🛠 AWS Services / Ví dụ: EC2, Lambda, Fargate, AWS Batch, EMR, ECS, EKS.
- 📝 Exam Tip: Batch ít phụ thuộc → AWS Batch; big data Hadoop/Spark → EMR; event nhỏ → Lambda; container app → ECS/EKS.
- 🧠 Mẹo nhớ: Nhớ: EMR cho big data; Batch cho job theo lô; Lambda cho event nhỏ.

### Distributed computing concepts supported by AWS global infrastructure and edge services
- 📌 Giải thích ngắn: Chia việc cho nhiều node và edge location để tăng performance, giảm latency.
- 🛠 AWS Services / Ví dụ: CloudFront, Global Accelerator, EMR, Kinesis, SQS.
- 📝 Exam Tip: Đề nhắc "edge", "global users" → dùng CloudFront/GA; xử lý song song → EMR/AWS Batch.
- 🧠 Mẹo nhớ: Nhớ: Chia việc cho nhiều người làm nhanh hơn một người.

### Queuing and messaging concepts (for example, publish/subscribe)
- 📌 Giải thích ngắn: Dùng hàng đợi để hấp thụ burst traffic, scale worker phía sau theo độ dài hàng.
- 🛠 AWS Services / Ví dụ: SQS, SNS, EventBridge + Lambda/ECS.
- 📝 Exam Tip: Scale theo queue depth: CloudWatch alarm → tăng worker; chống quá tải backend.
- 🧠 Mẹo nhớ: Nhớ: Hàng dài thì gọi thêm nhân viên.

### Scalability capabilities with appropriate use cases (for example, Amazon EC2 Auto Scaling, AWS Auto Scaling)
- 📌 Giải thích ngắn: Tự động tăng/giảm số lượng resource theo metric hoặc schedule.
- 🛠 AWS Services / Ví dụ: EC2 Auto Scaling, DynamoDB Auto Scaling, Application Auto Scaling.
- 📝 Exam Tip: Từ khóa: "handle traffic spike", "scale automatically" → Auto Scaling Group / dịch vụ auto scaling tương ứng.
- 🧠 Mẹo nhớ: Nhớ: Hệ thống tự co giãn như dây thun.

### Serverless technologies and patterns (for example, Lambda, Fargate)
- 📌 Giải thích ngắn: Chạy code event-driven, không quản server, auto scale đến hàng nghìn request.
- 🛠 AWS Services / Ví dụ: Lambda, Fargate, Step Functions, API Gateway.
- 📝 Exam Tip: Workload unpredictable → serverless; nhớ giới hạn timeout, memory, package size.
- 🧠 Mẹo nhớ: Nhớ: Không user thì gần như không tốn instance.

### The orchestration of containers (for example, Amazon ECS, Amazon EKS)
- 📌 Giải thích ngắn: Quản lý số lượng task/pod, placement, scaling để đạt performance mong muốn.
- 🛠 AWS Services / Ví dụ: ECS, EKS, Fargate, EC2.
- 📝 Exam Tip: Yêu cầu "portable across clouds" → EKS; đơn giản AWS-only → ECS; không muốn quản node → Fargate.
- 🧠 Mẹo nhớ: Nhớ: ECS/EKS là bộ điều phối, EC2/Fargate là chỗ chạy.

### Decoupling workloads so that components can scale independently
- 📌 Giải thích ngắn: Tách các thành phần heavy (CPU, IO, DB) để mỗi phần scale theo metric riêng.
- 🛠 AWS Services / Ví dụ: Microservices trên ECS/Lambda, SQS, SNS, EventBridge.
- 📝 Exam Tip: Thành phần nào nghẽn nhiều nhất → tách ra thành service riêng + queue.
- 🧠 Mẹo nhớ: Nhớ: Đừng bắt cả hệ thống scale chỉ vì một chức năng nặng.

### Identifying metrics and conditions to perform scaling actions
- 📌 Giải thích ngắn: Dùng đúng metric (CPU, latency, queue length, RCU/WCU) để trigger scale in/out.
- 🛠 AWS Services / Ví dụ: CloudWatch, Auto Scaling policies, target tracking.
- 📝 Exam Tip: Sử dụng target tracking cho đơn giản: ví dụ giữ CPU ~50% hoặc queue length ổn định.
- 🧠 Mẹo nhớ: Nhớ: Chỉ số đúng → scale mượt, chỉ số sai → scale lung tung.

### Selecting the appropriate compute options and features (for example, EC2 instance types) to meet business requirements
- 📌 Giải thích ngắn: Tùy workload mà chọn general, compute, memory, storage optimized.
- 🛠 AWS Services / Ví dụ: EC2 (M, C, R, I, P…), Fargate CPU/memory config.
- 📝 Exam Tip: CPU-bound → C family; RAM nhiều → R/X; IO nhiều → I; GPU → P/G.
- 🧠 Mẹo nhớ: Nhớ: C=Compute, R=RAM, I=IO, P=GPU.

### Selecting the appropriate resource type and size (for example, the amount of Lambda memory) to meet business requirements
- 📌 Giải thích ngắn: Size quá nhỏ → chậm; quá lớn → phí tiền. Tuning để đạt balance performance/cost.
- 🛠 AWS Services / Ví dụ: Lambda memory setting, EC2 t3/t4g/m5…, RDS instance size.
- 📝 Exam Tip: Lambda nhiều CPU hơn khi tăng memory; test để tìm sweet spot; EC2 thử burstable vs non-burst.
- 🧠 Mẹo nhớ: Nhớ: Đủ to để chạy mượt, không quá to để đốt tiền.

### AWS global infrastructure (for example, Availability Zones, AWS Regions)
- 📌 Giải thích ngắn: Chọn AZ/Region gần app và user để giảm latency DB.
- 🛠 AWS Services / Ví dụ: RDS Multi-AZ, Aurora Global Database, DynamoDB global tables.
- 📝 Exam Tip: Multi-AZ tăng HA, không giảm latency; multi-Region replica để user global đọc nhanh hơn.
- 🧠 Mẹo nhớ: Nhớ: Đưa bản đọc đến gần người dùng.

### Caching strategies and services (for example, Amazon ElastiCache)
- 📌 Giải thích ngắn: Lưu kết quả truy vấn hay dùng vào cache để giảm tải DB và tăng tốc.
- 🛠 AWS Services / Ví dụ: ElastiCache Redis/Memcached, DynamoDB DAX.
- 📝 Exam Tip: Thấy "read-intensive", "millisecond latency" → dùng cache; không thay thế backup/DR.
- 🧠 Mẹo nhớ: Nhớ: Cache là đệm giữa app và DB.

### Data access patterns (for example, read-intensive compared with write-intensive)
- 📌 Giải thích ngắn: Read-heavy cần replica/cache; write-heavy cần scale ghi, sharding hoặc NoSQL.
- 🛠 AWS Services / Ví dụ: RDS read replicas, Aurora, DynamoDB partitioning, Kinesis.
- 📝 Exam Tip: Read nhiều → read replica + cache; write nhiều → cân nhắc DynamoDB/Kinesis + worker.
- 🧠 Mẹo nhớ: Nhớ: Đọc thì nhân bản, ghi thì chia nhỏ hàng.

### Database capacity planning (for example, capacity units, instance types, Provisioned IOPS)
- 📌 Giải thích ngắn: Xác định TPS, IOPS, RCU/WCU để chọn cấu hình đủ chịu tải.
- 🛠 AWS Services / Ví dụ: DynamoDB RCU/WCU, Aurora/RDS instance class, EBS Provisioned IOPS.
- 📝 Exam Tip: Thấy DynamoDB → nhớ RCU/WCU; thiếu capacity → throttling. Cần auto-scale → bật auto scaling.
- 🧠 Mẹo nhớ: Nhớ: Đơn vị capacity giống số nhân viên quầy thu ngân.

### Database connections and proxies
- 📌 Giải thích ngắn: Kết nối quá nhiều có thể làm DB nghẽn; dùng proxy để pool và reuse.
- 🛠 AWS Services / Ví dụ: RDS Proxy, PgBouncer trên EC2, NLB.
- 📝 Exam Tip: Lambda/Serverless + RDS → giải pháp chuẩn là RDS Proxy để không mở quá nhiều connection.
- 🧠 Mẹo nhớ: Nhớ: Proxy giữ sẵn nhiều kết nối, app chỉ mượn tạm.

### Database engines with appropriate use cases (for example, heterogeneous migrations, homogeneous migrations)
- 📌 Giải thích ngắn: MySQL/PostgreSQL/Oracle/SQL Server/Aurora… có ưu/nhược riêng.
- 🛠 AWS Services / Ví dụ: RDS MySQL/PostgreSQL/Oracle/SQL Server, Aurora MySQL/PostgreSQL.
- 📝 Exam Tip: Homogeneous migration → DMS + RDS cùng engine; heterogeneous → DMS + Schema Conversion Tool (SCT).
- 🧠 Mẹo nhớ: Nhớ: Cùng họ dễ chuyển hơn khác họ.

### Database replication (for example, read replicas)
- 📌 Giải thích ngắn: Relational cho transaction, join. NoSQL cho scale lớn, schema linh hoạt. In-memory cho tốc độ cực nhanh.
- 🛠 AWS Services / Ví dụ: Aurora/RDS (relational), DynamoDB (NoSQL), ElastiCache (in-memory).
- 📝 Exam Tip: Transaction ACID → relational; key-value, scale lớn → DynamoDB; cache/session → ElastiCache.
- 🧠 Mẹo nhớ: Nhớ: SQL cho quan hệ phức tạp, NoSQL cho tốc độ và scale.

### Database types and services (for example, serverless, relational compared with non-relational, in-memory)
- 📌 Giải thích ngắn: Tạo đúng số replica, đúng Region để đáp ứng traffic đọc và HA.
- 🛠 AWS Services / Ví dụ: RDS Read Replicas, Aurora Replicas, cross-Region replica.
- 📝 Exam Tip: Analytic/report không ảnh hưởng DB chính → dùng replica; cần DR Region khác → cross-Region replica.
- 🧠 Mẹo nhớ: Nhớ: Đọc luôn hướng về replica khi có thể.

### Configuring read replicas to meet business requirements
- 📌 Giải thích ngắn: Kết hợp partition, index, sharding, cache, replica để đạt throughput mong muốn.
- 🛠 AWS Services / Ví dụ: Aurora, DynamoDB, ElastiCache, read replicas, DAX.
- 📝 Exam Tip: Đề bài nhắc throughput cao, latency thấp, global users → kết hợp replica + cache + multi-Region.
- 🧠 Mẹo nhớ: Nhớ: DB khỏe nhờ chia nhỏ việc và đẩy bớt ra cache.

### Designing database architectures
- 📌 Giải thích ngắn: Dùng cache front DB/API để đạt latency ms và tiết kiệm cost DB.
- 🛠 AWS Services / Ví dụ: ElastiCache, DynamoDB DAX, API Gateway cache, CloudFront.
- 📝 Exam Tip: Hot data, top items, config ít đổi → nên đưa vào cache.
- 🧠 Mẹo nhớ: Nhớ: Những gì hay dùng nên để gần app.

### Determining an appropriate database engine (for example, MySQL compared with PostgreSQL)
- 📌 Giải thích ngắn: Đưa nội dung và endpoint gần user trên toàn cầu.
- 🛠 AWS Services / Ví dụ: CloudFront, AWS Global Accelerator, Route 53.
- 📝 Exam Tip: Static content → CloudFront; nhiều Region active-active cho TCP/UDP → Global Accelerator.
- 🧠 Mẹo nhớ: Nhớ: CloudFront cho nội dung, GA cho kết nối.

### Determining an appropriate database type (for example, Amazon Aurora, Amazon DynamoDB)
- 📌 Giải thích ngắn: Chia subnet theo tầng (web/app/db), gán route và CIDR hợp lý để scale và an toàn.
- 🛠 AWS Services / Ví dụ: VPC, Subnet, Route Table, IGW, NAT, TGW.
- 📝 Exam Tip: Subnet phải nằm trọn trong một AZ; private tier không có route trực tiếp ra IGW.
- 🧠 Mẹo nhớ: Nhớ: Mỗi tầng app là một lớp subnet riêng.

### Integrating caching to meet business requirements
- 📌 Giải thích ngắn: LB là thành phần trung tâm phân phối traffic, giúp scale app dễ hơn.
- 🛠 AWS Services / Ví dụ: ALB, NLB, Gateway Load Balancer.
- 📝 Exam Tip: HTTP/HTTPS + routing theo path/host → ALB; TCP/UDP hiệu năng cao → NLB.
- 🧠 Mẹo nhớ: Nhớ: Chọn LB theo Layer: L7=ALB, L4=NLB.

### Edge networking services with appropriate use cases (for example, Amazon CloudFront, AWS Global Accelerator)
- 📌 Giải thích ngắn: Kết nối an toàn từ on-prem và giữa VPC với dịch vụ AWS.
- 🛠 AWS Services / Ví dụ: Site-to-Site VPN, Direct Connect, VPC Peering, PrivateLink.
- 📝 Exam Tip: PrivateLink để private access tới dịch vụ/endpoint; DX khi cần băng thông ổn định/latency thấp; VPN để bắt đầu nhanh.
- 🧠 Mẹo nhớ: Nhớ: PrivateLink = cổng riêng, DX = dây cáp riêng.

### How to design network architecture (for example, subnet tiers, routing, IP addressing)
- 📌 Giải thích ngắn: Thiết kế mạng cho global, hybrid, multi-tier với độ phức tạp vừa đủ.
- 🛠 AWS Services / Ví dụ: VPC, TGW, VPC peering, DX, VPN, CloudFront, GA.
- 📝 Exam Tip: Nhiều VPC cần hub-and-spoke → Transit Gateway; ít VPC → peering.
- 🧠 Mẹo nhớ: Nhớ: TGW như bến xe trung tâm nối nhiều tuyến.

### Load balancing concepts (for example, Application Load Balancer)
- 📌 Giải thích ngắn: Chọn mô hình có thể thêm subnet, VPC, Region mà không phải phá lại hết.
- 🛠 AWS Services / Ví dụ: Transit Gateway, CIDR plan rộng, segmentation rõ.
- 📝 Exam Tip: Plan CIDR lớn ngay từ đầu; domain nhiều VPC/Region → dùng TGW.
- 🧠 Mẹo nhớ: Nhớ: Chừa đường dự phòng cho tương lai mở rộng.

### Network connection options (for example, AWS VPN, Direct Connect, AWS PrivateLink)
- 📌 Giải thích ngắn: Đặt app gần dữ liệu và user để giảm latency, giảm chi phí chuyển vùng.
- 🛠 AWS Services / Ví dụ: AZ placement, Region choice, Local Zones, Wavelength, Outposts.
- 📝 Exam Tip: Analytics engine nên cùng Region với S3 data; không đặt DB một Region, app Region khác nếu không cần thiết.
- 🧠 Mẹo nhớ: Nhớ: Đưa ứng dụng đến gần nơi dữ liệu ở.

### Creating a network topology for various architectures (for example, global, hybrid, multi-tier)
- 📌 Giải thích ngắn: Tùy loại traffic (HTTP, TCP, gateway) mà chọn LB đúng để đạt hiệu năng tốt.
- 🛠 AWS Services / Ví dụ: ALB, NLB, Gateway Load Balancer, Route 53.
- 📝 Exam Tip: HTTP + routing nâng cao → ALB; gói nhỏ, yêu cầu siêu nhanh → NLB; inbound appliances → GWLB.
- 🧠 Mẹo nhớ: Nhớ: Đúng LB = hiệu năng tốt + dễ mở rộng.

### Determining network configurations that can scale to accommodate future needs
- 📌 Giải thích ngắn: Phân tích dữ liệu và vẽ dashboard nhanh từ data lake/warehouse.
- 🛠 AWS Services / Ví dụ: Athena, Lake Formation, Glue Data Catalog, QuickSight.
- 📝 Exam Tip: Ad-hoc query trên S3 → Athena; BI dashboard → QuickSight; data lake permission → Lake Formation.
- 🧠 Mẹo nhớ: Nhớ: Athena = SQL trên S3, QuickSight = dashboard.

### Determining the appropriate placement of resources to meet business requirements
- 📌 Giải thích ngắn: Tùy tần suất (real-time, mini-batch, batch) mà chọn pipeline.
- 🛠 AWS Services / Ví dụ: Kinesis Data Streams/Firehose, S3 batch upload, DataSync.
- 📝 Exam Tip: Real-time → Kinesis; hourly/daily file → S3 batch/DataSync.
- 🧠 Mẹo nhớ: Nhớ: Dòng chảy liên tục thì stream, từng đợt thì batch.

### Selecting the appropriate load balancing strategy
- 📌 Giải thích ngắn: Tự động copy, sync dữ liệu giữa on-prem và AWS với tối ưu băng thông.
- 🛠 AWS Services / Ví dụ: DataSync, Storage Gateway, Snowball.
- 📝 Exam Tip: Di chuyển nhiều TB qua mạng → DataSync; cần cache local truy cập S3 → Storage Gateway.
- 🧠 Mẹo nhớ: Nhớ: DataSync để di chuyển, Gateway để truy cập.

### Data analytics and visualization services with appropriate use cases (for example, Amazon Athena, AWS Lake Formation, Amazon QuickSight)
- 📌 Giải thích ngắn: Dọn dẹp, đổi định dạng, chuẩn hóa dữ liệu cho analytics.
- 🛠 AWS Services / Ví dụ: AWS Glue ETL, Glue Studio, Glue Jobs.
- 📝 Exam Tip: Từ khóa: "serverless ETL", "schema discovery" → Glue crawler + Glue job.
- 🧠 Mẹo nhớ: Nhớ: Glue là keo dán các nguồn dữ liệu lại với nhau.

### Data ingestion patterns (for example, frequency)
- 📌 Giải thích ngắn: Hạn chế ai/ứng dụng nào có thể gửi dữ liệu, dùng encryption, private endpoint.
- 🛠 AWS Services / Ví dụ: IAM, KMS, VPC endpoint, PrivateLink, ACL bucket, API keys.
- 📝 Exam Tip: Endpoint ingest (Kinesis, S3, API GW) cần IAM policy, key, TLS, hạn chế source IP.
- 🧠 Mẹo nhớ: Nhớ: Cửa nhận dữ liệu phải khóa kỹ hơn cửa thường.

### Data transfer services with appropriate use cases (for example, AWS DataSync, AWS Storage Gateway)
- 📌 Giải thích ngắn: Chọn pipe đủ lớn cho volume và velocity dữ liệu.
- 🛠 AWS Services / Ví dụ: Kinesis shard, Firehose throughput, DataSync task, Snowball.
- 📝 Exam Tip: Real-time volume lớn → tăng shard Kinesis; offline vài chục TB → Snowball.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu càng nhiều, ống phải càng to.

### Data transformation services with appropriate use cases (for example, AWS Glue)
- 📌 Giải thích ngắn: Xử lý dòng dữ liệu liên tục (log, clickstream, IoT) theo gần real-time.
- 🛠 AWS Services / Ví dụ: Kinesis Data Streams/Firehose/Data Analytics, MSK (Kafka).
- 📝 Exam Tip: Analytics real-time → Kinesis Data Analytics; load vào S3/Redshift → Firehose.
- 🧠 Mẹo nhớ: Nhớ: Kinesis = băng chuyền liên tục chở event.

### Secure access to ingestion access points
- 📌 Giải thích ngắn: Data lake lưu dữ liệu raw trên S3, phân quyền, catalog để nhiều công cụ đọc được.
- 🛠 AWS Services / Ví dụ: S3, Lake Formation, Glue Data Catalog, KMS, CloudTrail.
- 📝 Exam Tip: Từ khóa: "central data lake" → S3 + Lake Formation + Glue + Athena/Redshift Spectrum.
- 🧠 Mẹo nhớ: Nhớ: Hồ dữ liệu là S3 + lớp quản lý và phân quyền.

### Sizes and speeds needed to meet business requirements
- 📌 Giải thích ngắn: Ingest → buffer → process → store → visualize, tất cả theo dòng liên tục.
- 🛠 AWS Services / Ví dụ: Kinesis, MSK, Lambda, Firehose, S3, Redshift, QuickSight.
- 📝 Exam Tip: Luồng log/click cần dashboard real-time → Kinesis + Analytics + Firehose + S3/Redshift + QuickSight.
- 🧠 Mẹo nhớ: Nhớ: Chuỗi 5 bước: nhận, đệm, xử lý, lưu, xem.

### Streaming data services with appropriate use cases (for example, Amazon Kinesis)
- 📌 Giải thích ngắn: Kết hợp online (DataSync/VPN/DX) và offline (Snowball) tùy băng thông và thời gian.
- 🛠 AWS Services / Ví dụ: DataSync, Snowball/Snowmobile, Storage Gateway, S3 Transfer Acceleration.
- 📝 Exam Tip: Nhiều PB → Snowmobile; vài chục TB, mạng chậm → Snowball; sync thường xuyên → DataSync.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu càng to, càng nên dùng xe tải (Snow).

### Building and securing data lakes
- 📌 Giải thích ngắn: Xây dashboard, báo cáo cho business user, tự động refresh.
- 🛠 AWS Services / Ví dụ: QuickSight, Athena, Redshift, OpenSearch Dashboards.
- 📝 Exam Tip: Business friendly BI → QuickSight; log search → OpenSearch.
- 🧠 Mẹo nhớ: Nhớ: QuickSight là Power BI phiên bản AWS.

### Designing data streaming architectures
- 📌 Giải thích ngắn: ETL, batch, Spark/Hadoop mỗi loại cần compute khác nhau.
- 🛠 AWS Services / Ví dụ: EMR, Glue, AWS Batch, Lambda, Fargate.
- 📝 Exam Tip: Big data Spark/Hadoop → EMR; ETL serverless → Glue; batch CPU-bound → AWS Batch trên EC2.
- 🧠 Mẹo nhớ: Nhớ: EMR = cluster big data, Glue = ETL serverless.

### Designing data transfer solutions
- 📌 Giải thích ngắn: Điều chỉnh batch size, interval, shard, buffer để cân bằng latency và cost.
- 🛠 AWS Services / Ví dụ: Kinesis shards/buffer, Firehose buffer size/time, DataSync schedule.
- 📝 Exam Tip: Latency thấp → buffer nhỏ; cost thấp → buffer lớn hơn, ít batch hơn.
- 🧠 Mẹo nhớ: Nhớ: Nhanh thì tốn hơn, rẻ thì chậm hơn.

### Implementing visualization strategies

- 📌 Giải thích ngắn: Trình bày dữ liệu thành dashboard, biểu đồ rõ ràng để người dùng business hiểu nhanh và ra quyết định.
- 🛠 AWS Services / Ví dụ: QuickSight, Athena + QuickSight, OpenSearch Dashboards. Ví dụ: query data lake bằng Athena rồi build dashboard QuickSight.
- 📝 Exam Tip: Từ khóa: "BI dashboard", "business visualization" → ưu tiên QuickSight; log search/metrics kỹ thuật → OpenSearch Dashboards.
- 🧠 Mẹo nhớ: Nhớ: Athena/Redshift xử lý, QuickSight vẽ hình.

### Selecting appropriate compute options for data processing (for example, Amazon EMR)

- 📌 Giải thích ngắn: Chọn nền tảng compute phù hợp (cluster, serverless, container) để xử lý dữ liệu hiệu quả và mở rộng được.
- 🛠 AWS Services / Ví dụ: EMR (Hadoop/Spark), Glue (ETL serverless), AWS Batch, Lambda/Fargate. Ví dụ: ETL big data → EMR, ETL nhẹ theo batch → Glue.
- 📝 Exam Tip: Big data, Spark/Hadoop, cần fine-tune cluster → EMR; ETL serverless ít quản lý hạ tầng → Glue; batch compute thuần túy → AWS Batch.
- 🧠 Mẹo nhớ: Nhớ: EMR cho cluster lớn, Glue cho ETL gọn, Batch cho job tính toán.

### Selecting appropriate configurations for ingestion

- 📌 Giải thích ngắn: Cấu hình tần suất, kích thước batch, số shard/partition để ingest dữ liệu mà không nghẽn hoặc tốn kém.
- 🛠 AWS Services / Ví dụ: Kinesis shard count, Firehose buffer size/time, S3 batch upload, DataSync schedule.
- 📝 Exam Tip: Real-time gần như tức thời → nhiều shard, buffer nhỏ; chấp nhận trễ vài phút/giờ → ít shard hơn, batch lớn để tiết kiệm chi phí.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu đến càng gấp thì phải chia nhiều làn đường.

### Transforming data between formats (for example, .csv to .parquet)
- 📌 Giải thích ngắn: Đổi sang định dạng columnar giúp query big data nhanh và rẻ hơn.
- 🛠 AWS Services / Ví dụ: AWS Glue, EMR, Athena (read Parquet), Firehose data transformation.
- 📝 Exam Tip: Từ khóa: "optimize query cost", "columnar" → dùng Parquet/ORC + Glue/EMR để convert.
- 🧠 Mẹo nhớ: Nhớ: Parquet giúp đọc ít dữ liệu hơn nên query nhanh và rẻ.
