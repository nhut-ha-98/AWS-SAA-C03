# Domain 4 – Design Cost-Optimized Architectures

### Access options (for example, an S3 bucket with Requester Pays object storage)
- 📌 Giải thích ngắn: Cho phép bên đọc dữ liệu trả tiền data transfer thay vì chủ bucket.
- 🛠 AWS Services / Ví dụ: S3 với Requester Pays. Ví dụ: dataset public, ai tải thì tự trả chi phí.
- 📝 Exam Tip: Từ khóa: "Requester Pays" → bật flag ở S3 bucket; dùng khi nhiều bên ngoài tải data.
- 🧠 Mẹo nhớ: Nhớ: Ai dùng thì người đó trả tiền.

### AWS cost management service features (for example, cost allocation tags, multi-account billing)
- 📌 Giải thích ngắn: Tag resource để phân bổ chi phí theo team/project, gom bill nhiều account.
- 🛠 AWS Services / Ví dụ: Cost allocation tags, AWS Organizations consolidated billing.
- 📝 Exam Tip: Câu hỏi về show cost theo team/dept → bật cost allocation tags + dùng Organizations.
- 🧠 Mẹo nhớ: Nhớ: Mọi thứ phải được gắn nhãn để biết tiền của ai.

### AWS cost management tools with appropriate use cases (for example, AWS Cost Explorer, AWS Budgets, AWS Cost and Usage Report)
- 📌 Giải thích ngắn: Theo dõi, phân tích và cảnh báo chi phí chi tiết.
- 🛠 AWS Services / Ví dụ: Cost Explorer (phân tích), AWS Budgets (cảnh báo), Cost and Usage Report (file chi tiết).
- 📝 Exam Tip: Thấy "detailed billing", "hourly cost" → CUR; "alert when over budget" → Budgets; "view trend" → Cost Explorer.
- 🧠 Mẹo nhớ: Nhớ: Explorer để xem, Budgets để cảnh báo, CUR để phân tích sâu.

### AWS storage services with appropriate use cases (for example, Amazon FSx, Amazon EFS, Amazon S3, Amazon EBS)
- 📌 Giải thích ngắn: Mỗi loại storage có giá khác, phải chọn phù hợp workload.
- 🛠 AWS Services / Ví dụ: FSx, EFS, S3, EBS, Glacier.
- 📝 Exam Tip: File share Windows → FSx; share Linux → EFS; object/archive → S3/Glacier; disk EC2 → EBS.
- 🧠 Mẹo nhớ: Nhớ: Lưu càng sâu (Glacier) càng rẻ nhưng càng chậm.

### Backup strategies
- 📌 Giải thích ngắn: Chọn tần suất, độ lâu, loại storage backup hợp lý để không tốn quá nhiều.
- 🛠 AWS Services / Ví dụ: AWS Backup, RDS snapshot, EBS snapshot, S3 Glacier.
- 📝 Exam Tip: Không cần restore nhanh → đưa backup sang Glacier Deep Archive; chỉ giữ một số phiên bản gần nhất.
- 🧠 Mẹo nhớ: Nhớ: Backup cũ ít khi dùng thì đẩy sang tier rẻ.

### Block storage options (for example, hard disk drive [HDD] volume types, solid state drive [SSD] volume types)
- 📌 Giải thích ngắn: SSD cho IOPS cao, HDD rẻ cho throughput/ sequential IO.
- 🛠 AWS Services / Ví dụ: EBS gp3/io1/io2 (SSD), st1/sc1 (HDD).
- 📝 Exam Tip: General → gp3; IO cao, latency thấp → io1/io2; big data scan, log → st1/sc1.
- 🧠 Mẹo nhớ: Nhớ: SSD cho tốc độ, HDD cho dung lượng rẻ.

### Data lifecycles
- 📌 Giải thích ngắn: Tự động chuyển data từ tier đắt sang rẻ khi ít dùng hơn.
- 🛠 AWS Services / Ví dụ: S3 Lifecycle, EFS Lifecycle, Backup lifecycle.
- 📝 Exam Tip: Thấy "move old objects" → dùng S3 Lifecycle sang IA/Glacier; giảm chi phí data lâu năm.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu càng già càng được đưa vào kho lạnh.

### Hybrid storage options (for example, DataSync, Transfer Family, Storage Gateway)
- 📌 Giải thích ngắn: Kết hợp lưu trữ local với cloud để giảm chi phí và latency.
- 🛠 AWS Services / Ví dụ: Storage Gateway, DataSync, FSx on AWS, Snowball Edge.
- 📝 Exam Tip: Cần cache local truy cập S3 → File/Volume Gateway; sync khối lượng lớn theo lịch → DataSync.
- 🧠 Mẹo nhớ: Nhớ: Lưu một bản gần app, một bản rẻ ở cloud.

### Storage access patterns
- 📌 Giải thích ngắn: Thói quen đọc/ghi quyết định chọn tier (Standard/IA/Glacier, One Zone…).
- 🛠 AWS Services / Ví dụ: S3 Standard, Standard-IA, One Zone-IA, Glacier, EFS-IA.
- 📝 Exam Tip: Ít truy cập nhưng cần multi-AZ → Standard-IA; chấp nhận mất một AZ → One Zone-IA rẻ hơn.
- 🧠 Mẹo nhớ: Nhớ: Truy cập càng ít → tier càng rẻ.

### Storage tiering (for example, cold tiering for object storage)
- 📌 Giải thích ngắn: Tách nóng/ấm/lạnh cho object để giảm bill.
- 🛠 AWS Services / Ví dụ: S3 Standard, IA, Intelligent-Tiering, Glacier, Deep Archive.
- 📝 Exam Tip: Không biết pattern → dùng Intelligent-Tiering; dữ liệu archive lâu năm → Glacier Deep Archive.
- 🧠 Mẹo nhớ: Nhớ: Intelligent-Tiering cho AWS tự chọn dùm.

### Designing appropriate storage strategies (for example, batch uploads to Amazon S3 compared with individual uploads)
- 📌 Giải thích ngắn: Chọn cách put/get hợp lý (batch vs từng file) và kết hợp tiering.
- 🛠 AWS Services / Ví dụ: S3 multipart upload, batch upload, lifecycle.
- 📝 Exam Tip: Nhiều file nhỏ → gom batch để giảm overhead; log cũ → chuyển Glacier.
- 🧠 Mẹo nhớ: Nhớ: Gửi hàng theo lô rẻ hơn gửi từng cái.

### Determining the correct storage size for a workload
- 📌 Giải thích ngắn: Dự đoán vừa đủ để tránh under/over-provision, dùng auto scaling nơi có thể.
- 🛠 AWS Services / Ví dụ: EBS size + auto-grow, EFS/S3 (scale tự động).
- 📝 Exam Tip: DB on EBS nên bật CloudWatch alarm để scale up khi gần đầy; EFS/S3 không cần provision capacity.
- 🧠 Mẹo nhớ: Nhớ: Chỉ provision cho thứ không auto-scale.

### Determining the lowest cost method of transferring data for a workload to AWS storage
- 📌 Giải thích ngắn: So sánh online vs offline, region vs AZ, direct vs internet.
- 🛠 AWS Services / Ví dụ: Direct Connect, VPN, Snowball, DataSync, S3 Transfer Acceleration.
- 📝 Exam Tip: Cross-Region data transfer khá đắt, so với dùng CDN/edge cache; volume lớn qua Internet chậm → Snowball có thể rẻ hơn.
- 🧠 Mẹo nhớ: Nhớ: Đi xa nhiều thì tìm đường chuyên dụng hoặc xe tải.

### Determining when storage auto scaling is required
- 📌 Giải thích ngắn: Một số storage (EBS) cần quản dung lượng; số khác auto-scale (S3/EFS).
- 🛠 AWS Services / Ví dụ: EBS size, Aurora storage auto-scaling, DynamoDB auto scaling.
- 📝 Exam Tip: Cần scale dung lượng DB thời gian thực → Aurora với storage auto-scaling; DynamoDB auto-scaling WCU/RCU.
- 🧠 Mẹo nhớ: Nhớ: Chọn dịch vụ biết tự co giãn giúp đỡ quản lý.

### Managing S3 object lifecycles
- 📌 Giải thích ngắn: Đặt rule tự chuyển/xóa object theo tuổi để giảm chi phí.
- 🛠 AWS Services / Ví dụ: S3 Lifecycle rules, Expiration, Transition.
- 📝 Exam Tip: Câu hỏi về log quá nhiều, bill S3 tăng → thiết lập lifecycle: 30 ngày sang IA, 90 ngày sang Glacier, 365 ngày delete.
- 🧠 Mẹo nhớ: Nhớ: Tự động dọn kho hàng theo ngày.

### Selecting the appropriate backup and/or archival solution
- 📌 Giải thích ngắn: Backup cần restore nhanh; archive có thể chậm nhưng rẻ.
- 🛠 AWS Services / Ví dụ: AWS Backup, S3 Glacier, RDS snapshot, EBS snapshot, Tape Gateway.
- 📝 Exam Tip: Audit/compliance lâu năm → Glacier/Tape Gateway; backup vận hành hàng ngày → snapshot/Backup.
- 🧠 Mẹo nhớ: Nhớ: Backup cho hôm nay, archive cho năm sau.

### Selecting the appropriate service for data migration to storage services
- 📌 Giải thích ngắn: Tùy volume và mạng mà chọn online/offline tool.
- 🛠 AWS Services / Ví dụ: DataSync, Snowball, Storage Gateway, S3 Transfer Acceleration.
- 📝 Exam Tip: Nhiều TB/PB, mạng yếu → Snowball; liên tục sync → DataSync; muốn tăng speed upload global → Transfer Acceleration.
- 🧠 Mẹo nhớ: Nhớ: DataSync = sync nhiều lần; Snowball = chuyển một cục lớn.

### Selecting the appropriate storage tier
- 📌 Giải thích ngắn: Cân bằng giữa chi phí, độ truy cập, durability để chọn Standard/IA/Glacier…
- 🛠 AWS Services / Ví dụ: S3 storage classes, EFS-IA, RDS storage type.
- 📝 Exam Tip: Câu hỏi cho dữ liệu ít dùng nhưng phải giữ lâu → IA/Glacier; file hay đọc/ghi → Standard/EFS.
- 🧠 Mẹo nhớ: Nhớ: Đọc thường xuyên → tier nóng, đọc hiếm → tier lạnh.

### Selecting the correct data lifecycle for storage
- 📌 Giải thích ngắn: Toàn bộ vòng đời: ingest → dùng nhiều → dùng ít → archive → xóa, được tự động hóa.
- 🛠 AWS Services / Ví dụ: S3 Lifecycle, Backup plans, retention policies.
- 📝 Exam Tip: Ràng buộc xóa sau N năm → retention policy; cần giữ file không được xóa → Object Lock.
- 🧠 Mẹo nhớ: Nhớ: Mỗi file có ngày sinh và ngày "nghỉ hưu".

### Selecting the most cost-effective storage service for a workload
- 📌 Giải thích ngắn: Dựa vào pattern và durability để chọn dịch vụ phù hợp thay vì luôn dùng S3/IOPS cao.
- 🛠 AWS Services / Ví dụ: S3, Glacier, EFS, EBS HDD, FSx.
- 📝 Exam Tip: Logs nhiều nhưng ít đọc → S3 IA/Glacier; DB test → smaller EBS/HDD; không dùng EBS io1 nếu không cần.
- 🧠 Mẹo nhớ: Nhớ: Dùng vũ khí vừa đủ, không đem đại bác bắn chim.

### AWS cost management service features (for example, cost allocation tags, multi-account billing)
- 📌 Giải thích ngắn: Gắn tag cho EC2/RDS/Lambda… để track chi phí theo project; gom bill nhiều account để dễ tối ưu.
- 🛠 AWS Services / Ví dụ: Cost allocation tags, Organizations.
- 📝 Exam Tip: Compute cost tăng khó giải thích → nhìn tag; không tag thì khó tối ưu.
- 🧠 Mẹo nhớ: Nhớ: Không tag = không nhìn thấy ai đang xài.

### AWS cost management tools with appropriate use cases (for example, Cost Explorer, AWS Budgets, AWS Cost and Usage Report)
- 📌 Giải thích ngắn: Xem chi tiết chi phí compute, đặt cảnh báo, tìm resource rảnh.
- 🛠 AWS Services / Ví dụ: Cost Explorer, Budgets, CUR, Compute Optimizer.
- 📝 Exam Tip: Khuyến nghị size EC2/RDS → AWS Compute Optimizer; alert chi phí vượt ngưỡng → Budgets.
- 🧠 Mẹo nhớ: Nhớ: Compute Optimizer là "cố vấn" cho EC2/RDS.

### AWS global infrastructure (for example, Availability Zones, AWS Regions)
- 📌 Giải thích ngắn: Chọn Region ảnh hưởng giá, data transfer, latency.
- 🛠 AWS Services / Ví dụ: So sánh giá Region, Reserved Instances/Savings Plans multi-Region.
- 📝 Exam Tip: Region khác giá khác; cross-Region traffic tốn thêm tiền; cân bằng giữa latency và cost.
- 🧠 Mẹo nhớ: Nhớ: Region gần có thể rẻ, nhưng không phải lúc nào cũng rẻ nhất.

### AWS purchasing options (for example, Spot Instances, Reserved Instances, Savings Plans)
- 📌 Giải thích ngắn: Chọn mô hình giá phù hợp với mức độ ổn định của workload.
- 🛠 AWS Services / Ví dụ: EC2 On-Demand, Spot, Reserved Instances, Compute/Savings Plans.
- 📝 Exam Tip: Prod ổn định 24/7 → Reserved/Savings Plans; job linh hoạt, chịu được hủy → Spot; mới bắt đầu → On-Demand.
- 🧠 Mẹo nhớ: Nhớ: Ổn định thì ký hợp đồng, linh hoạt thì mua spot.

### Distributed compute strategies (for example, edge processing)
- 📌 Giải thích ngắn: Xử lý sớm ở gần nguồn dữ liệu để giảm traffic về Region (tiết kiệm cost).
- 🛠 AWS Services / Ví dụ: Lambda@Edge, Greengrass, Snowball Edge, Local Zones.
- 📝 Exam Tip: IoT, video analytics ở biên → Greengrass/Snowball Edge; personalization gần user → Lambda@Edge.
- 🧠 Mẹo nhớ: Nhớ: Xử lý gần nguồn, gửi về trung tâm ít hơn.

### Hybrid compute options (for example, AWS Outposts, AWS Snowball Edge)
- 📌 Giải thích ngắn: Chạy compute AWS tại on-prem để thỏa compliance/latency mà vẫn dùng API AWS.
- 🛠 AWS Services / Ví dụ: AWS Outposts, Snowball Edge.
- 📝 Exam Tip: Cần API AWS, low latency local → Outposts; cần compute tạm thời nơi không có DC/Internet tốt → Snowball Edge.
- 🧠 Mẹo nhớ: Nhớ: Mang một "miếng Region" về nhà.

### Instance types, families, and sizes (for example, memory optimized, compute optimized, virtualization)
- 📌 Giải thích ngắn: Chọn đúng loại instance giúp đạt hiệu năng với chi phí tối ưu.
- 🛠 AWS Services / Ví dụ: EC2 M/C/R/X/I/T/P/G, burstable vs non-burst.
- 📝 Exam Tip: Idle nhiều → t3/t4g burstable; CPU gắt → C; RAM nặng → R; IO nặng → I.
- 🧠 Mẹo nhớ: Nhớ: Dùng đúng chữ cái theo bottleneck chính.

### Optimization of compute utilization (for example, containers, serverless computing, microservices)
- 📌 Giải thích ngắn: Gom workload vào container/serverless để tránh over-provision nhiều VM rảnh.
- 🛠 AWS Services / Ví dụ: ECS/EKS, Fargate, Lambda, microservices.
- 📝 Exam Tip: Nhiều app chạy nhẹ trên nhiều EC2 riêng → chuyển vào container/Fargate/Lambda.
- 🧠 Mẹo nhớ: Nhớ: Gom chung lên một tàu lớn thay vì nhiều tàu nhỏ trống.

### Scaling strategies (for example, auto scaling, hibernation)
- 📌 Giải thích ngắn: Scale out/in tự động theo nhu cầu để không chạy dư.
- 🛠 AWS Services / Ví dụ: Auto Scaling Group, scheduled scaling, dynamic scaling.
- 📝 Exam Tip: Workload theo giờ làm việc → scheduled scaling; traffic bất thường → dynamic theo metric.
- 🧠 Mẹo nhớ: Nhớ: Ban ngày đông xe, tối ít xe; scale theo giờ.

### Determining an appropriate load balancing strategy (for example, Application Load Balancer [Layer 7] compared with Network Load Balancer [Layer 4] compared with Gateway Load Balancer)
- 📌 Giải thích ngắn: Chọn LB đủ tính năng, không dùng loại đắt nếu không cần.
- 🛠 AWS Services / Ví dụ: ALB, NLB, Gateway Load Balancer.
- 📝 Exam Tip: Chỉ cần TCP đơn giản → NLB có thể rẻ hơn; không cần LB riêng thì cân nhắc dùng ALB share nhiều service.
- 🧠 Mẹo nhớ: Nhớ: Dùng một LB cho nhiều service khi phù hợp.

### Determining appropriate scaling methods and strategies for elastic workloads (for example, horizontal compared with vertical, EC2 hibernation)
- 📌 Giải thích ngắn: Kết hợp horizontal/vertical, Spot/Mixed instances, hibernation để tiết kiệm.
- 🛠 AWS Services / Ví dụ: ASG mixed instances, EC2 hibernate, Spot Fleet.
- 📝 Exam Tip: Dev/test → Spot + schedule off; batch linh hoạt → Spot; prod core → On-Demand + RI/SP.
- 🧠 Mẹo nhớ: Nhớ: Việc không gấp thì giao cho Spot.

### Determining cost-effective AWS compute services with appropriate use cases (for example, Lambda, Amazon EC2, Fargate)
- 📌 Giải thích ngắn: Dùng dịch vụ phù hợp để tránh overkill (ví dụ dùng EC2 lâu chạy cho việc nhỏ có thể dùng Lambda).
- 🛠 AWS Services / Ví dụ: Lambda, EC2, Fargate, Batch.
- 📝 Exam Tip: Traffic thấp, thưa → Lambda; web constant → EC2/containers; batch → Batch trên Spot.
- 🧠 Mẹo nhớ: Nhớ: Ít request → Lambda; nhiều request ổn định → EC2/ECS.

### Determining the required availability for different classes of workloads (for example, production workloads, non-production workloads)
- 📌 Giải thích ngắn: Không phải workload nào cũng cần multi-AZ/multi-Region; chọn đúng để tiết kiệm.
- 🛠 AWS Services / Ví dụ: Single-AZ vs Multi-AZ RDS/EC2, backup-only cho non-prod.
- 📝 Exam Tip: Dev/test thường 1 AZ, ít HA; prod critical → Multi-AZ, DR; internal tool → có thể chịu downtime.
- 🧠 Mẹo nhớ: Nhớ: Không phải app nào cũng là "mission critical".

### Selecting the appropriate instance family for a workload
- 📌 Giải thích ngắn: Chọn family theo bottleneck chính để không phải overprovision tài nguyên khác.
- 🛠 AWS Services / Ví dụ: C5/C7 (CPU), R5/R6 (RAM), I3/I4 (IO), G/P (GPU).
- 📝 Exam Tip: CPU-bound → C; in-memory cache → R; analytics IO nặng → I; ML/inference → G/P.
- 🧠 Mẹo nhớ: Nhớ: Đặt tên theo chữ cái dễ nhớ bottleneck.

### Selecting the appropriate instance size for a workload
- 📌 Giải thích ngắn: Resize lên/xuống dựa trên sử dụng thực tế để tránh lãng phí.
- 🛠 AWS Services / Ví dụ: t3.small vs t3.large, m5.large vs m5.xlarge, RDS size change.
- 📝 Exam Tip: Compute Optimizer thường đề xuất nhỏ lại 1-2 bậc nếu underutilized; nhớ test trước khi áp.
- 🧠 Mẹo nhớ: Nhớ: Nếu CPU/RAM < 20% liên tục → nghĩ đến việc thu nhỏ.

### AWS cost management service features (for example, cost allocation tags, multi-account billing)
- 📌 Giải thích ngắn: Quy định bao lâu snapshot, giữ bao lâu, chuyển sang storage rẻ khi cần.
- 🛠 AWS Services / Ví dụ: RDS backup window & retention, Aurora backup, Backup service.
- 📝 Exam Tip: Không cần giữ snapshot quá lâu; có thể export ra S3 (Glacier) cho archive thay vì giữ snapshot đắt.
- 🧠 Mẹo nhớ: Nhớ: Snapshot lâu năm nên nằm trên S3/Glacier, không nằm mãi trong RDS.

### AWS cost management tools with appropriate use cases (for example, Cost Explorer, AWS Budgets, AWS Cost and Usage Report)
- 📌 Giải thích ngắn: Aurora/DynamoDB serverless có thể rẻ hơn nếu workload dao động.
- 🛠 AWS Services / Ví dụ: Aurora Serverless v2, DynamoDB on-demand/provisioned với auto scaling.
- 📝 Exam Tip: Workload không steady → DB serverless/on-demand; steady → provisioned + RI.
- 🧠 Mẹo nhớ: Nhớ: Dao động thì trả tiền theo dùng, ổn định thì đặt trước.

### Caching strategies
- 📌 Giải thích ngắn: Columnar/time series tối ưu query analytics, rẻ hơn so với RDS cho khối lượng lớn.
- 🛠 AWS Services / Ví dụ: Redshift (columnar), Timestream (time series), OpenSearch.
- 📝 Exam Tip: Analytics nặng → Redshift; time series metric/log → Timestream/OpenSearch thay vì RDS.
- 🧠 Mẹo nhớ: Nhớ: Analytics thì dùng "kho" chuyên dụng, không dùng DB giao dịch.

### Data retention policies

- 📌 Giải thích ngắn: Định nghĩa giữ dữ liệu bao lâu (ngày/tháng/năm) cho từng loại để vừa đủ compliance vừa không tốn phí lưu trữ.
- 🛠 AWS Services / Ví dụ: S3 Lifecycle + Expiration, Backup retention, CloudWatch Logs retention.
- 📝 Exam Tip: Thấy yêu cầu "log giữ 90 ngày", "xóa sau 7 năm" → dùng retention/lifecycle thay vì giữ vô hạn.
- 🧠 Mẹo nhớ: Nhớ: Không có dữ liệu nào nên sống mãi nếu luật không bắt buộc.

### Database capacity planning (for example, capacity units)

- 📌 Giải thích ngắn: Ước lượng trước TPS/IOPS/RCU/WCU để không mua dư (tốn tiền) hay thiếu (throttle).
- 🛠 AWS Services / Ví dụ: DynamoDB RCU/WCU, Aurora/RDS instance class + IOPS, Compute Optimizer.
- 📝 Exam Tip: DynamoDB ít traffic → on-demand; traffic ổn định, dự đoán được → provisioned + auto scaling để tối ưu chi phí.
- 🧠 Mẹo nhớ: Nhớ: Dành đủ quầy thu ngân cho giờ cao điểm, không xây siêu thị to cho vài khách.

### Database connections and proxies

- 📌 Giải thích ngắn: Quản lý connection pool tốt giúp giảm số connection DB (license/cost) mà vẫn đảm bảo hiệu năng.
- 🛠 AWS Services / Ví dụ: RDS Proxy, connection pooling, Aurora Serverless v2.
- 📝 Exam Tip: Serverless/Lambda bắn nhiều connection nhỏ → dùng RDS Proxy để gom, tránh phải scale DB quá to chỉ vì connection.
- 🧠 Mẹo nhớ: Nhớ: Proxy đứng giữa gom nhiều kết nối lẻ thành ít kết nối bền.

### Database engines with appropriate use cases (for example, heterogeneous migrations, homogeneous migrations)

- 📌 Giải thích ngắn: Chọn engine phù hợp (Aurora, MySQL, PostgreSQL, DynamoDB…) để giảm license và chi phí vận hành.
- 🛠 AWS Services / Ví dụ: RDS MySQL/PostgreSQL, Aurora, DynamoDB.
- 📝 Exam Tip: Giảm chi phí license Oracle/SQL Server → migrate sang Aurora/MySQL/PostgreSQL bằng DMS + SCT.
- 🧠 Mẹo nhớ: Nhớ: Dùng mã nguồn mở/Aurora thường rẻ hơn DB thương mại.

### Database replication (for example, read replicas)

- 📌 Giải thích ngắn: Tạo replica đúng nhu cầu để scale đọc, tránh over-replication gây tốn chi phí không cần.
- 🛠 AWS Services / Ví dụ: RDS Read Replicas, Aurora Replicas, cross-Region replica.
- 📝 Exam Tip: Read không quá nặng → 1–2 replica là đủ; nhiều replica mà ít traffic → xem xét giảm số replica để tiết kiệm.
- 🧠 Mẹo nhớ: Nhớ: Bản sao chỉ nên đủ dùng, không phải mỗi user một DB.

### Database types and services (for example, relational compared with non-relational, Aurora, DynamoDB)

- 📌 Giải thích ngắn: Dùng đúng loại DB giúp tránh overkill: NoSQL/serverless cho scale lớn, relational cho transaction.
- 🛠 AWS Services / Ví dụ: Aurora (relational tối ưu chi phí), DynamoDB (NoSQL pay-per-request), RDS chuẩn.
- 📝 Exam Tip: Key-value, traffic lớn, không join phức tạp → DynamoDB (on-demand có thể rẻ hơn so với RDS luôn-on).
- 🧠 Mẹo nhớ: Nhớ: Không phải cái gì cũng nhét vào RDS.

### Designing appropriate backup and retention policies (for example, snapshot frequency)

- 📌 Giải thích ngắn: Đặt tần suất snapshot và thời gian giữ hợp lý để vừa đáp ứng RPO vừa không phình bill storage.
- 🛠 AWS Services / Ví dụ: RDS automated backups, AWS Backup plans, snapshot schedules.
- 📝 Exam Tip: Prod critical → snapshot thường xuyên, retention vừa phải; môi trường dev/test → snapshot thưa hơn, retention ngắn.
- 🧠 Mẹo nhớ: Nhớ: Backup nhiều cho cái quan trọng, ít cho cái rẻ tiền.

### Determining an appropriate database engine (for example, MySQL compared with PostgreSQL)

- 📌 Giải thích ngắn: So sánh tính năng, ecosystem và chi phí vận hành giữa các engine để chọn cái đủ dùng.
- 🛠 AWS Services / Ví dụ: RDS MySQL, PostgreSQL, Aurora các phiên bản.
- 📝 Exam Tip: Nếu không yêu cầu đặc thù, MySQL/PostgreSQL trên Aurora thường rẻ và hiệu quả hơn commercial engine.
- 🧠 Mẹo nhớ: Nhớ: Chọn engine phổ biến giúp dễ thuê người, dễ tối ưu chi phí.

### Determining cost-effective AWS database services with appropriate use cases (for example, DynamoDB compared with Amazon RDS, serverless)

- 📌 Giải thích ngắn: Dùng DynamoDB/Aurora serverless cho workload dao động để tránh phải trả tiền DB idle.
- 🛠 AWS Services / Ví dụ: DynamoDB on-demand, Aurora Serverless v2, RDS standard.
- 📝 Exam Tip: Workload không chạy 24/7, traffic biến động → DB serverless/on-demand thường rẻ hơn RDS provisioned.
- 🧠 Mẹo nhớ: Nhớ: Không chạy thường xuyên thì đừng thuê nhà nguyên tháng.

### Determining cost-effective AWS database types (for example, time series format, columnar format)

- 📌 Giải thích ngắn: Lưu dữ liệu đúng định dạng (columnar/time series) để query ít dữ liệu hơn, giảm cost.
- 🛠 AWS Services / Ví dụ: Redshift (columnar), Timestream (time series), Parquet/ORC trên S3.
- 📝 Exam Tip: Analytics log lớn → Parquet/Redshift/Timestream rẻ hơn nhiều so với query trực tiếp trên RDS.
- 🧠 Mẹo nhớ: Nhớ: Đứng từ trên nhìn cột (columnar) rẻ hơn đào từng dòng.

### Migrating database schemas and data to different locations and/or different database engines
- 📌 Giải thích ngắn: Dùng DMS và SCT để migrate ít downtime, tránh phải build tool riêng.
- 🛠 AWS Services / Ví dụ: Database Migration Service (DMS), Schema Conversion Tool (SCT), S3 intermediate.
- 📝 Exam Tip: Heterogeneous migration (Oracle → Aurora) → DMS + SCT; giảm license cost bằng chuyển từ commercial sang open source/Aurora.
- 🧠 Mẹo nhớ: Nhớ: DMS là cầu nối giữa DB cũ và DB mới.

### AWS cost management service features (for example, cost allocation tags, multi-account billing)
- 📌 Giải thích ngắn: NAT Gateway tính tiền theo giờ + data, nhiều NAT tốn nhiều.
- 🛠 AWS Services / Ví dụ: NAT Gateway, NAT Instance (ít dùng, tự quản).
- 📝 Exam Tip: Muốn rẻ: một NAT Gateway shared cho nhiều private subnet nhưng trade-off HA; HA hơn → mỗi AZ một NAT, chi phí cao hơn.
- 🧠 Mẹo nhớ: Nhớ: Ít NAT rẻ hơn, nhiều NAT an toàn hơn.

### AWS cost management tools with appropriate use cases (for example, Cost Explorer, AWS Budgets, AWS Cost and Usage Report)
- 📌 Giải thích ngắn: Đường riêng (DX) đắt hơn nhưng băng thông tốt; VPN rẻ hơn nhưng phụ thuộc Internet.
- 🛠 AWS Services / Ví dụ: Direct Connect, VPN, DX + VPN backup.
- 📝 Exam Tip: Traffic ổn định, lớn → DX có thể rẻ hơn về lâu dài; traffic nhỏ/thử nghiệm → VPN.
- 🧠 Mẹo nhớ: Nhớ: DX như thuê đường cáp riêng, VPN là đi chung quốc lộ.

### Load balancing concepts (for example, Application Load Balancer)
- 📌 Giải thích ngắn: Cấu trúc mạng tốt giúp giảm hop, giảm phí transfer không cần thiết.
- 🛠 AWS Services / Ví dụ: Transit Gateway, VPC peering, inter-Region peering.
- 📝 Exam Tip: Cross-Region peering tốn tiền; nếu không cần multi-Region thì giữ trong cùng Region để rẻ hơn.
- 🧠 Mẹo nhớ: Nhớ: Mỗi lần đi qua biên giới (Region) là thêm phí.

### NAT gateways (for example, NAT instance costs compared with NAT gateway costs)
- 📌 Giải thích ngắn: DNS like Route 53 rẻ và scale tốt, ít khi là bottleneck chi phí.
- 🛠 AWS Services / Ví dụ: Route 53, Private Hosted Zones.
- 📝 Exam Tip: Route 53 được dùng nhiều vì rẻ, global, HA cao; chỉ chú ý số hosted zone/record.
- 🧠 Mẹo nhớ: Nhớ: DNS rẻ, ít khi là chỗ cần tối ưu đầu tiên.

### Network connectivity (for example, private lines, dedicated lines, VPNs)
- 📌 Giải thích ngắn: Dùng 1 NAT shared rẻ hơn, nhưng ít HA hơn; nhiều NAT tốn hơn nhưng bền hơn.
- 🛠 AWS Services / Ví dụ: NAT Gateway theo AZ, route table thiết kế phù hợp.
- 📝 Exam Tip: Workload non-critical → có thể dùng 1 NAT GW/Region; critical → mỗi AZ một NAT GW.
- 🧠 Mẹo nhớ: Nhớ: Tiền vs HA, phải chọn ưu tiên.

### Network routing, topology, and peering (for example, AWS Transit Gateway, VPC peering)
- 📌 Giải thích ngắn: Kết nối riêng đắt nhưng ổn định; VPN rẻ nhưng phụ thuộc Internet; Internet public rẻ nhất nhưng ít bảo mật.
- 🛠 AWS Services / Ví dụ: Direct Connect, Site-to-Site VPN, Internet Gateway.
- 📝 Exam Tip: Compliance yêu cầu dedicated line → DX; POC nhỏ → VPN; public web → Internet + ALB.
- 🧠 Mẹo nhớ: Nhớ: Quan trọng/nhạy cảm thì đi đường riêng.

### Network services with appropriate use cases (for example, DNS)
- 📌 Giải thích ngắn: Chọn đường đi data sao cho ít cross-AZ/Region, tận dụng private link.
- 🛠 AWS Services / Ví dụ: VPC endpoints, PrivateLink, same-AZ routing, Global Accelerator.
- 📝 Exam Tip: Deploy resource trong cùng AZ/VPC để tránh phí cross-AZ; dùng endpoint để tránh đi ra Internet.
- 🧠 Mẹo nhớ: Nhớ: Dữ liệu đi nội bộ luôn rẻ hơn đi vòng ngoài.

### Configuring appropriate NAT gateway types for a network (for example, a single shared NAT gateway compared with NAT gateways for each Availability Zone)
- 📌 Giải thích ngắn: Cache tại edge giúp giảm traffic quay lại origin, tiết kiệm transfer/compute.
- 🛠 AWS Services / Ví dụ: CloudFront, Lambda@Edge, S3 origin, ALB origin.
- 📝 Exam Tip: Nhiều user global tải static content → CloudFront để giảm chi phí Region egress.
- 🧠 Mẹo nhớ: Nhớ: Đưa file ra gần user để server gốc đỡ vất vả.

### Configuring appropriate network connections (for example, Direct Connect compared with VPN compared with internet)
- 📌 Giải thích ngắn: Xem lại flow traffic để giảm hop, bỏ bớt NAT/VPN không cần, gom flow lại.
- 🛠 AWS Services / Ví dụ: VPC Flow Logs, Cost Explorer (data transfer), CloudWatch.
- 📝 Exam Tip: Chi phí data transfer cao bất ngờ → nhìn flow logs để thấy flow cross-AZ/Region dư thừa.
- 🧠 Mẹo nhớ: Nhớ: Muốn giảm tiền mạng phải biết dữ liệu đang đi đâu.

### Configuring appropriate network routes to minimize network transfer costs (for example, Region to Region, Availability Zone to Availability Zone, private to public, Global Accelerator, VPC endpoints)
- 📌 Giải thích ngắn: Giới hạn request để bảo vệ backend, tránh tăng cost đột biến.
- 🛠 AWS Services / Ví dụ: API Gateway throttling, WAF rate-based rules, SQS.
- 📝 Exam Tip: Public API → dùng API Gateway throttling + WAF; tránh tạo quá nhiều Lambda/EC2 tốn tiền.
- 🧠 Mẹo nhớ: Nhớ: Đặt van nước để không ai mở quá mạnh cùng lúc.

### Determining strategic needs for content delivery networks (CDNs) and edge caching

- 📌 Giải thích ngắn: Quyết định khi nào dùng CDN/edge cache để giảm chi phí egress và tải trên origin.
- 🛠 AWS Services / Ví dụ: CloudFront, Global Accelerator, Lambda@Edge.
- 📝 Exam Tip: Nhiều user global, tải static content → CloudFront giúp giảm data transfer từ Region và giảm số EC2 cần chạy.
- 🧠 Mẹo nhớ: Nhớ: Cho user lấy hàng ở kho gần nhà thay vì về tận nhà máy.

### Reviewing existing workloads for network optimizations

- 📌 Giải thích ngắn: Soi lại đường đi traffic để giảm hop, giảm cross-AZ/Region, tìm chỗ có thể dùng endpoint/private link.
- 🛠 AWS Services / Ví dụ: VPC Flow Logs, Cost Explorer (data transfer), CloudWatch dashboards.
- 📝 Exam Tip: Bill data transfer tăng bất thường → xem flow logs, giảm traffic đi qua NAT/cross-AZ không cần thiết.
- 🧠 Mẹo nhớ: Nhớ: Muốn tiết kiệm tiền mạng thì phải vẽ bản đồ đường đi trước.

### Selecting an appropriate throttling strategy

- 📌 Giải thích ngắn: Đặt giới hạn request để bảo vệ backend, tránh bùng nổ chi phí khi có spike hoặc misuse.
- 🛠 AWS Services / Ví dụ: API Gateway throttling, WAF rate-based rules, application-level throttling, SQS buffer.
- 📝 Exam Tip: Public API với chi phí Lambda/EC2 tăng đột biến → dùng throttling ở API Gateway/WAF + queue để san tải.
- 🧠 Mẹo nhớ: Nhớ: Van nước siết vừa phải thì hóa đơn nước mới dễ chịu.

### Selecting the appropriate bandwidth allocation for a network device (for example, a single VPN compared with multiple VPNs, Direct Connect speed)
- 📌 Giải thích ngắn: Chọn số lượng VPN/DX speed phù hợp để không over-provision.
- 🛠 AWS Services / Ví dụ: 1 vs nhiều VPN, DX 1 Gbps vs 10 Gbps.
- 📝 Exam Tip: Bắt đầu nhỏ (1 Gbps/1 VPN) rồi scale out khi cần; DX redundant để HA nhưng cân nhắc chi phí.
- 🧠 Mẹo nhớ: Nhớ: Đường ống nước to gấp đôi không phải lúc nào cũng cần.
