# AWS & Networking Keywords Reference
*Tài liệu tham khảo từ khóa AWS & Mạng*

## AWS SAA-C03 Exam Categories
*Các danh mục chứng chỉ AWS SAA-C03*

**🏗️ Design Resilient Architectures** - Thiết kế kiến trúc đàn hồi
**⚡ Design High-Performing Architectures** - Thiết kế kiến trúc hiệu suất cao  
**🔒 Design Secure Applications** - Thiết kế ứng dụng bảo mật
**💰 Design Cost-Optimized Architectures** - Thiết kế kiến trúc tối ưu chi phí

---

## 1. AWS Core Services
*Các dịch vụ cốt lõi AWS*

### 1.1 Compute Services
*Dịch vụ tính toán*

**1.1.1 EC2 (Elastic Compute Cloud)** 🏗️⚡💰
- EN: Virtual servers in the cloud with scalable computing capacity
- VN: Máy chủ ảo trên cloud với khả năng mở rộng tính toán
- **Purpose:** Host applications, websites, databases
- **Use Case:** Web servers, application backends, batch processing

**1.1.2 Lambda** 🏗️⚡💰
- EN: Serverless compute service that runs code without managing servers
- VN: Dịch vụ tính toán không máy chủ chạy code mà không cần quản lý server
- **Purpose:** Event-driven code execution without server management
- **Use Case:** API backends, file processing, scheduled tasks

**1.1.3 ECS (Elastic Container Service)** 🏗️⚡
- EN: Container orchestration service for Docker containers
- VN: Dịch vụ điều phối container cho Docker containers
- **Purpose:** Manage and scale containerized applications
- **Use Case:** Microservices, container orchestration, CI/CD pipelines

**1.1.4 EKS (Elastic Kubernetes Service)** 🏗️⚡
- EN: Managed Kubernetes service for container orchestration
- VN: Dịch vụ Kubernetes được quản lý cho điều phối container
- **Purpose:** Run Kubernetes without managing control plane
- **Use Case:** Complex microservices, enterprise container workloads

### 1.2 Storage Services
*Dịch vụ lưu trữ*

**1.2.1 S3 (Simple Storage Service)** 🏗️⚡🔒💰
- EN: Object storage service with unlimited scalability
- VN: Dịch vụ lưu trữ đối tượng với khả năng mở rộng không giới hạn
- **Purpose:** Store and retrieve any amount of data from anywhere
- **Use Case:** Static websites, backups, data lakes, content distribution

**1.2.2 EBS (Elastic Block Store)** 🏗️⚡💰
- EN: Block-level storage volumes for EC2 instances
- VN: Ổ đĩa lưu trữ khối cho các EC2 instances
- **Purpose:** Persistent block storage for EC2 instances
- **Use Case:** Database storage, file systems, boot volumes

**1.2.3 EFS (Elastic File System)** 🏗️⚡💰
- EN: Fully managed NFS file system for EC2
- VN: Hệ thống file NFS được quản lý hoàn toàn cho EC2
- **Purpose:** Shared file storage across multiple EC2 instances
- **Use Case:** Content repositories, web serving, data analytics

**1.2.4 Glacier** 🏗️💰
- EN: Low-cost archive storage for long-term backup
- VN: Lưu trữ lưu trữ chi phí thấp cho sao lưu dài hạn
- **Purpose:** Long-term archival and backup at low cost
- **Use Case:** Data archiving, compliance, disaster recovery

**1.2.5 Storage Gateway** 🏗️💰
- EN: Hybrid cloud storage service connecting on-premises to AWS
- VN: Dịch vụ lưu trữ hybrid cloud kết nối on-premises với AWS
- **Purpose:** Seamlessly connect on-premises to cloud storage
- **Use Case:** Hybrid cloud storage, backup to cloud, migration

### 1.3 Database Services
*Dịch vụ cơ sở dữ liệu*

**1.3.1 RDS (Relational Database Service)** 🏗️⚡💰
- EN: Managed relational database service (MySQL, PostgreSQL, etc.)
- VN: Dịch vụ cơ sở dữ liệu quan hệ được quản lý
- **Purpose:** Managed relational databases without infrastructure management
- **Use Case:** Web applications, enterprise apps, OLTP workloads

**1.3.2 DynamoDB** 🏗️⚡💰
- EN: NoSQL database service with single-digit millisecond performance
- VN: Dịch vụ cơ sở dữ liệu NoSQL với hiệu suất millisecond
- **Purpose:** Fast, scalable NoSQL database for any scale
- **Use Case:** Mobile apps, gaming, IoT, real-time analytics

**1.3.3 Aurora** 🏗️⚡💰
- EN: MySQL and PostgreSQL compatible relational database
- VN: Cơ sở dữ liệu quan hệ tương thích MySQL và PostgreSQL
- **Purpose:** High-performance cloud-native relational database
- **Use Case:** Enterprise applications, SaaS applications, web services

**1.3.4 ElastiCache** ⚡💰
- EN: In-memory caching service (Redis/Memcached)
- VN: Dịch vụ cache trong bộ nhớ
- **Purpose:** Improve application performance with sub-millisecond latency
- **Use Case:** Session storage, database caching, real-time analytics

**1.3.5 Redshift** ⚡💰
- EN: Data warehouse service for analytics
- VN: Dịch vụ kho dữ liệu cho phân tích
- **Purpose:** Fast, scalable data warehouse for analytics
- **Use Case:** Business intelligence, data analytics, reporting

### 1.4 Analytics Services
*Dịch vụ phân tích dữ liệu*

**1.4.1 Athena** ⚡💰
- EN: Serverless interactive query service for S3 data
- VN: Dịch vụ truy vấn tương tác không máy chủ cho dữ liệu S3
- **Purpose:** Run SQL queries directly on S3 data without infrastructure
- **Use Case:** Ad-hoc analysis, log analysis, data lake queries

**1.4.2 AWS Glue** ⚡💰
- EN: Serverless ETL service for data preparation
- VN: Dịch vụ ETL không máy chủ để chuẩn bị dữ liệu
- **Purpose:** Extract, transform, and load data between data stores
- **Use Case:** Data cataloging, ETL jobs, schema discovery

**1.4.3 EMR (Elastic MapReduce)** ⚡💰
- EN: Big data processing platform using Hadoop/Spark
- VN: Nền tảng xử lý big data sử dụng Hadoop/Spark
- **Purpose:** Process large datasets using distributed computing
- **Use Case:** Big data analytics, machine learning, data science

**1.4.4 Kinesis Data Analytics** ⚡
- EN: Real-time stream processing with SQL
- VN: Xử lý luồng dữ liệu thời gian thực với SQL
- **Purpose:** Analyze streaming data in real-time
- **Use Case:** Real-time dashboards, anomaly detection, live metrics

**1.4.5 QuickSight** 🏗️💰
- EN: Business intelligence and data visualization service
- VN: Dịch vụ business intelligence và trực quan hóa dữ liệu
- **Purpose:** Create interactive dashboards and reports
- **Use Case:** Executive dashboards, self-service BI, embedded analytics

### 1.5 Data Transfer Services
*Dịch vụ truyền tải dữ liệu*

**1.5.1 Snowball Edge** 🏗️💰
- EN: Edge computing device with 80TB storage and compute capacity
- VN: Thiết bị edge computing với dung lượng 80TB và khả năng tính toán
- **Purpose:** Data transfer and edge computing in remote locations
- **Use Case:** Large data migrations, edge processing, offline environments

**1.5.2 Snowcone** 🏗️💰
- EN: Small, portable edge computing device (8TB storage)
- VN: Thiết bị edge computing nhỏ gọn, di động (8TB)
- **Purpose:** Edge computing in space-constrained environments
- **Use Case:** Drones, vehicles, remote locations, IoT edge processing

**1.5.3 Snowmobile** 🏗️💰
- EN: Exabyte-scale data transfer truck (100PB capacity)
- VN: Xe tải truyền dữ liệu quy mô exabyte (100PB)
- **Purpose:** Massive data center migrations
- **Use Case:** Entire data center moves, legacy system consolidation

**1.5.4 DataSync** 🏗️💰
- EN: Online data transfer service for moving data between locations
- VN: Dịch vụ truyền dữ liệu online để di chuyển dữ liệu giữa các vị trí
- **Purpose:** Automated, secure data transfer over network
- **Use Case:** Hybrid cloud sync, data lake ingestion, backup to cloud

**1.5.5 Transfer Family** 🏗️💰
- EN: Managed FTP, FTPS, and SFTP service
- VN: Dịch vụ FTP, FTPS và SFTP được quản lý
- **Purpose:** Secure file transfer protocols as managed service
- **Use Case:** B2B file exchange, application integration, legacy system support

---

## 2. AWS Networking Services
*Dịch vụ mạng AWS*

### 2.1 Core Networking
*Mạng cốt lõi*

**2.1.1 VPC (Virtual Private Cloud)** 🏗️🔒
- EN: Isolated virtual network within AWS cloud
- VN: Mạng ảo biệt lập trong AWS cloud
- **Purpose:** Create isolated network environment in AWS
- **Use Case:** Secure application hosting, network isolation, hybrid connectivity

**2.1.2 Route 53** 🏗️⚡
- EN: Scalable DNS web service and domain registration
- VN: Dịch vụ DNS có thể mở rộng và đăng ký tên miền
- **Purpose:** Route end users to internet applications reliably
- **Use Case:** Domain registration, DNS routing, health checks, failover

**2.1.3 CloudFront** 🏗️⚡🔒💰
- EN: Content Delivery Network (CDN) for fast content delivery
- VN: Mạng phân phối nội dung để phân phối nội dung nhanh
- **Purpose:** Deliver content with low latency and high transfer speeds
- **Use Case:** Website acceleration, video streaming, API acceleration

**2.1.4 ELB (Elastic Load Balancer)** 🏗️⚡
- EN: Distributes incoming traffic across multiple targets
- VN: Phân phối lưu lượng truy cập đến nhiều mục tiêu
- **Purpose:** Distribute incoming application traffic across multiple targets
- **Use Case:** High availability, fault tolerance, traffic distribution

**2.1.5 API Gateway** 🏗️⚡🔒💰
- EN: Service for creating, publishing, and managing APIs
- VN: Dịch vụ tạo, xuất bản và quản lý APIs
- **Purpose:** Create, publish, maintain, monitor, and secure APIs
- **Use Case:** RESTful APIs, WebSocket APIs, serverless backends

### 2.2 VPC Components
*Thành phần VPC*

**2.2.1 Subnet** 🏗️🔒
- EN: Range of IP addresses in VPC, can be public or private
- VN: Dải địa chỉ IP trong VPC, có thể là công khai hoặc riêng tư
- **Purpose:** Segment VPC into smaller network ranges
- **Use Case:** Network isolation, availability zones, security layers

**2.2.2 Internet Gateway (IGW)** 🏗️
- EN: Allows communication between VPC and internet
- VN: Cho phép giao tiếp giữa VPC và internet
- **Purpose:** Enable internet access for VPC resources
- **Use Case:** Public subnet connectivity, web applications, public APIs

**2.2.3 NAT Gateway** 🏗️🔒💰
- EN: Enables private subnet instances to access internet
- VN: Cho phép các instance trong subnet riêng truy cập internet
- **Purpose:** Provide outbound internet access for private resources
- **Use Case:** Software updates, API calls from private instances

**2.2.4 Route Table** 🏗️🔒
- EN: Contains rules (routes) that determine network traffic direction
- VN: Chứa các quy tắc xác định hướng lưu lượng mạng
- **Purpose:** Control traffic routing within VPC and to external networks
- **Use Case:** Traffic routing, subnet associations, custom routing

**2.2.5 Security Group** 🔒
- EN: Virtual firewall controlling inbound/outbound traffic
- VN: Tường lửa ảo kiểm soát lưu lượng vào/ra
- **Purpose:** Control traffic at instance level with stateful rules
- **Use Case:** Instance-level security, application access control

**2.2.6 NACL (Network Access Control List)** 🔒
- EN: Subnet-level firewall with allow/deny rules
- VN: Tường lửa cấp subnet với quy tắc cho phép/từ chối
- **Purpose:** Control traffic at subnet level with stateless rules
- **Use Case:** Subnet-level security, defense in depth, compliance

### 2.3 Messaging & Eventing Services
*Dịch vụ nhắn tin và sự kiện*

**2.3.1 SQS (Simple Queue Service)** 🏗️⚡💰
- EN: Fully managed message queuing service
- VN: Dịch vụ hàng đợi tin nhắn được quản lý hoàn toàn
- **Purpose:** Decouple application components with reliable messaging
- **Use Case:** Job queues, order processing, microservices communication

**2.3.2 SNS (Simple Notification Service)** 🏗️⚡🔒
- EN: Fully managed pub/sub messaging service
- VN: Dịch vụ nhắn tin pub/sub được quản lý hoàn toàn
- **Purpose:** Send notifications to multiple subscribers simultaneously
- **Use Case:** Push notifications, email alerts, fan-out messaging

**2.3.3 EventBridge** 🏗️⚡🔒
- EN: Serverless event bus for application integration
- VN: Event bus không máy chủ để tích hợp ứng dụng
- **Purpose:** Route events between AWS services and SaaS applications
- **Use Case:** Event-driven architectures, SaaS integration, microservices

**2.3.4 Kinesis Data Streams** 🏗️⚡
- EN: Real-time data streaming service
- VN: Dịch vụ streaming dữ liệu thời gian thực
- **Purpose:** Collect and process streaming data in real-time
- **Use Case:** Real-time analytics, log processing, IoT data ingestion

**2.3.5 Step Functions** 🏗️⚡
- EN: Visual workflow service for coordinating distributed applications
- VN: Dịch vụ quy trình làm việc trực quan để điều phối ứng dụng phân tán
- **Purpose:** Orchestrate multiple AWS services into workflows
- **Use Case:** Business processes, data pipelines, error handling workflows

### 2.4 Connectivity Services
*Dịch vụ kết nối*

**2.4.1 VPN Gateway** 🏗️🔒💰
- EN: Connects on-premises networks to VPC via VPN
- VN: Kết nối mạng on-premises với VPC qua VPN
- **Purpose:** Secure connection between on-premises and AWS
- **Use Case:** Hybrid cloud, secure remote access, site-to-site connectivity

**2.4.2 Direct Connect** 🏗️⚡💰
- EN: Dedicated network connection from premises to AWS
- VN: Kết nối mạng chuyên dụng từ cơ sở hạ tầng đến AWS
- **Purpose:** High-bandwidth, low-latency connection to AWS
- **Use Case:** Large data transfers, consistent network performance

**2.4.3 Transit Gateway** 🏗️💰
- EN: Network hub connecting VPCs and on-premises networks
- VN: Hub mạng kết nối các VPC và mạng on-premises
- **Purpose:** Simplify network connectivity between multiple VPCs
- **Use Case:** Multi-VPC architectures, complex network topologies

**2.4.4 VPC Peering** 🏗️🔒
- EN: Network connection between two VPCs
- VN: Kết nối mạng giữa hai VPC
- **Purpose:** Enable direct communication between VPCs
- **Use Case:** Cross-VPC communication, shared services, multi-region

**2.4.5 Global Accelerator** 🏗️⚡💰
- EN: Network service that improves global application performance
- VN: Dịch vụ mạng cải thiện hiệu suất ứng dụng toàn cầu
- **Purpose:** Optimize global network performance using AWS backbone
- **Use Case:** Gaming applications, IoT, real-time APIs, global load balancing

---

## 3. AWS Security & Identity
*Bảo mật & Danh tính AWS*

### 3.1 Identity Services
*Dịch vụ danh tính*

**3.1.1 IAM (Identity and Access Management)** 🔒
- EN: Service for managing users, groups, and permissions
- VN: Dịch vụ quản lý người dùng, nhóm và quyền
- **Purpose:** Control access to AWS services and resources
- **Use Case:** User management, role-based access, service permissions

**3.1.2 Cognito** 🔒
- EN: User identity and authentication service for web/mobile apps
- VN: Dịch vụ danh tính và xác thực người dùng cho ứng dụng web/mobile
- **Purpose:** Add user sign-up, sign-in, and access control to apps
- **Use Case:** Mobile apps, web applications, user pools, identity federation

**3.1.3 SSO (Single Sign-On)** 🔒💰
- EN: Centrally manage access to multiple AWS accounts
- VN: Quản lý truy cập tập trung đến nhiều tài khoản AWS
- **Purpose:** Simplify access management across multiple AWS accounts
- **Use Case:** Enterprise authentication, multi-account management

### 3.2 Security Services
*Dịch vụ bảo mật*

**3.2.1 WAF (Web Application Firewall)** 🔒
- EN: Protects web applications from common exploits
- VN: Bảo vệ ứng dụng web khỏi các cuộc tấn công phổ biến
- **Purpose:** Filter malicious web traffic before it reaches applications
- **Use Case:** SQL injection protection, XSS prevention, rate limiting

**3.2.2 Shield** 🔒💰
- EN: DDoS protection service for AWS applications
- VN: Dịch vụ bảo vệ DDoS cho ứng dụng AWS
- **Purpose:** Protect against DDoS attacks
- **Use Case:** DDoS mitigation, always-on protection, advanced threat protection

**3.2.3 GuardDuty** 🔒
- EN: Threat detection service using machine learning
- VN: Dịch vụ phát hiện mối đe dọa sử dụng machine learning
- **Purpose:** Detect malicious activity and unauthorized behavior
- **Use Case:** Security monitoring, threat intelligence, incident response

**3.2.4 KMS (Key Management Service)** 🔒
- EN: Managed service for creating and controlling encryption keys
- VN: Dịch vụ được quản lý để tạo và kiểm soát khóa mã hóa
- **Purpose:** Create and manage cryptographic keys for encryption
- **Use Case:** Data encryption, key rotation, compliance requirements

**3.2.5 Network Firewall** 🔒
- EN: Managed network firewall service with IPS capabilities
- VN: Dịch vụ tường lửa mạng được quản lý với khả năng IPS
- **Purpose:** Protect VPCs with managed firewall and intrusion prevention
- **Use Case:** Network security, deep packet inspection, compliance

**3.2.6 Firewall Manager** 🔒💰
- EN: Centralized security policy management across accounts
- VN: Quản lý chính sách bảo mật tập trung qua các tài khoản
- **Purpose:** Manage security policies across multiple AWS accounts
- **Use Case:** Multi-account governance, compliance enforcement, policy automation

**3.2.7 Traffic Mirroring** 🔒
- EN: Copy network traffic for analysis and security monitoring
- VN: Sao chép lưu lượng mạng để phân tích và giám sát bảo mật
- **Purpose:** Mirror VPC traffic to security analysis tools
- **Use Case:** Network forensics, IDS/IPS, compliance monitoring

**3.2.8 Macie** 🔒💰
- EN: ML-powered data security service for discovering sensitive data
- VN: Dịch vụ bảo mật dữ liệu được hỗ trợ ML để khám phá dữ liệu nhạy cảm
- **Purpose:** Discover, classify, and protect sensitive data in S3
- **Use Case:** PII discovery, data classification, compliance monitoring

**3.2.9 Secrets Manager** 🔒💰
- EN: Centralized secrets management with automatic rotation
- VN: Quản lý bí mật tập trung với xoay vòng tự động
- **Purpose:** Store, retrieve, and rotate application secrets
- **Use Case:** Database credentials, API keys, application secrets

**3.2.10 IAM Access Analyzer** 🔒
- EN: Analyze resource policies to identify security risks
- VN: Phân tích chính sách tài nguyên để xác định rủi ro bảo mật
- **Purpose:** Identify overly permissive resource access policies
- **Use Case:** Security assessment, policy validation, compliance auditing

---

## 4. AWS Management & Monitoring
*Quản lý & Giám sát AWS*

### 4.1 Monitoring Services
*Dịch vụ giám sát*

**4.1.1 CloudWatch** 🏗️⚡🔒💰
- EN: Monitoring service for AWS resources and applications
- VN: Dịch vụ giám sát cho tài nguyên và ứng dụng AWS
- **Purpose:** Monitor resources, collect metrics, set alarms
- **Use Case:** Performance monitoring, alerting, log analysis, auto scaling

**4.1.2 CloudTrail** 🔒
- EN: Service for logging and monitoring API calls
- VN: Dịch vụ ghi log và giám sát các lời gọi API
- **Purpose:** Track user activity and API usage across AWS
- **Use Case:** Compliance auditing, security analysis, troubleshooting

**4.1.3 Config** 🔒💰
- EN: Service for assessing and auditing AWS resource configurations
- VN: Dịch vụ đánh giá và kiểm toán cấu hình tài nguyên AWS
- **Purpose:** Track resource configurations and compliance
- **Use Case:** Configuration compliance, change management, auditing

### 4.2 Deployment Services
*Dịch vụ triển khai*

**4.2.1 CloudFormation** 🏗️💰
- EN: Infrastructure as Code service using templates
- VN: Dịch vụ Infrastructure as Code sử dụng templates
- **Purpose:** Model and provision AWS resources using code
- **Use Case:** Infrastructure automation, consistent deployments, version control

**4.2.2 CodeDeploy** 🏗️
- EN: Automated application deployment service
- VN: Dịch vụ triển khai ứng dụng tự động
- **Purpose:** Automate code deployments to compute services
- **Use Case:** Blue/green deployments, rolling deployments, CI/CD pipelines

**4.2.3 Elastic Beanstalk** 🏗️💰
- EN: Platform service for deploying web applications
- VN: Dịch vụ nền tảng để triển khai ứng dụng web
- **Purpose:** Deploy and manage applications without infrastructure complexity
- **Use Case:** Web applications, API backends, development environments

---

## 5. Networking Fundamentals
*Kiến thức mạng cơ bản*

### 5.1 Network Protocols
*Giao thức mạng*

**5.1.1 TCP (Transmission Control Protocol)** 🏗️⚡
- EN: Reliable, connection-oriented protocol for data transmission
- VN: Giao thức kết nối đáng tin cậy để truyền dữ liệu
- **Purpose:** Ensure reliable, ordered data delivery
- **Use Case:** Web browsing, email, file transfer, database connections

**5.1.2 UDP (User Datagram Protocol)** ⚡
- EN: Fast, connectionless protocol for data transmission
- VN: Giao thức không kết nối nhanh để truyền dữ liệu
- **Purpose:** Fast data transmission without reliability guarantees
- **Use Case:** Video streaming, gaming, DNS queries, real-time applications

**5.1.3 HTTP/HTTPS** 🔒
- EN: Web protocols for transferring web content (secure version)
- VN: Giao thức web để truyền nội dung web (phiên bản bảo mật)
- **Purpose:** Transfer web content securely over the internet
- **Use Case:** Web applications, APIs, secure communications

**5.1.4 DNS (Domain Name System)** 🏗️⚡
- EN: System that translates domain names to IP addresses
- VN: Hệ thống chuyển đổi tên miền thành địa chỉ IP
- **Purpose:** Resolve human-readable names to IP addresses
- **Use Case:** Domain resolution, load balancing, service discovery

### 5.2 Network Architecture
*Kiến trúc mạng*

**5.2.1 CIDR (Classless Inter-Domain Routing)** 🏗️🔒
- EN: Method for allocating IP addresses and routing
- VN: Phương pháp phân bổ địa chỉ IP và định tuyến
- **Purpose:** Efficiently allocate IP addresses and enable flexible subnetting
- **Use Case:** VPC design, subnet planning, network segmentation

**5.2.2 BGP (Border Gateway Protocol)** 🏗️⚡
- EN: Protocol for routing between autonomous systems
- VN: Giao thức định tuyến giữa các hệ thống tự trị
- **Purpose:** Route traffic between different networks on the internet
- **Use Case:** Internet routing, multi-homed networks, traffic engineering

**5.2.3 VPN (Virtual Private Network)** 🔒💰
- EN: Secure tunnel over public networks
- VN: Đường hầm bảo mật qua mạng công cộng
- **Purpose:** Create secure connections over untrusted networks
- **Use Case:** Remote access, site-to-site connectivity, secure communications

**5.2.4 CDN (Content Delivery Network)** ⚡💰
- EN: Geographically distributed servers for content delivery
- VN: Máy chủ phân tán địa lý để phân phối nội dung
- **Purpose:** Deliver content faster by caching near users
- **Use Case:** Website acceleration, video streaming, global content distribution

### 5.3 Load Balancing
*Cân bằng tải*

**5.3.1 Application Load Balancer (ALB)** 🏗️⚡💰
- EN: Layer 7 load balancer for HTTP/HTTPS traffic
- VN: Cân bằng tải lớp 7 cho lưu lượng HTTP/HTTPS
- **Purpose:** Distribute HTTP/HTTPS requests with advanced routing
- **Use Case:** Web applications, microservices, content-based routing

**5.3.2 Network Load Balancer (NLB)** 🏗️⚡
- EN: Layer 4 load balancer for TCP/UDP traffic
- VN: Cân bằng tải lớp 4 cho lưu lượng TCP/UDP
- **Purpose:** High-performance load balancing for TCP/UDP traffic
- **Use Case:** Gaming applications, IoT, ultra-low latency requirements

**5.3.3 Gateway Load Balancer (GLB)** 🏗️🔒
- EN: Layer 3 load balancer for third-party appliances
- VN: Cân bằng tải lớp 3 cho thiết bị bên thứ ba
- **Purpose:** Deploy and scale third-party network virtual appliances
- **Use Case:** Firewalls, intrusion detection, deep packet inspection

### 5.4 Advanced Networking Concepts
*Khái niệm mạng nâng cao*

**5.4.1 SPICE (QuickSight)** ⚡💰
- EN: Super-fast, Parallel, In-memory Calculation Engine
- VN: Công cụ tính toán siêu nhanh, song song, trong bộ nhớ
- **Purpose:** High-performance in-memory analytics engine for QuickSight
- **Use Case:** Fast dashboard queries, interactive analytics, large dataset processing

**5.4.2 NFS (Network File System)** 🏗️🔒
- EN: Protocol for accessing files over network as if local
- VN: Giao thức truy cập file qua mạng như file cục bộ
- **Purpose:** Mount remote file systems as local drives
- **Use Case:** Shared storage, Snowball Edge data transfer, EFS access

**5.4.3 SMB (Server Message Block)** 🏗️🔒
- EN: Network file sharing protocol used primarily in Windows environments
- VN: Giao thức chia sẻ file mạng chủ yếu dùng trong môi trường Windows
- **Purpose:** Share files, printers, and resources over network
- **Use Case:** Windows file sharing, Storage Gateway, cross-platform access

**5.4.4 GENEVE Protocol** 🔒
- EN: Generic Network Virtualization Encapsulation protocol
- VN: Giao thức đóng gói ảo hóa mạng chung
- **Purpose:** Network overlay protocol for Gateway Load Balancer
- **Use Case:** Traffic mirroring, security appliance integration, network virtualization

**5.4.5 Anycast IP** ⚡🔒
- EN: Network addressing where single IP is advertised from multiple locations
- VN: Địa chỉ mạng nơi một IP được quảng cáo từ nhiều vị trí
- **Purpose:** Route traffic to nearest/best performing location
- **Use Case:** Global Accelerator, DNS, DDoS mitigation

---

## 6. AWS Architecture Patterns
*Mẫu kiến trúc AWS*

### 6.1 High Availability
*Tính khả dụng cao*

**6.1.1 Auto Scaling** 🏗️⚡💰
- EN: Automatically adjusts capacity based on demand
- VN: Tự động điều chỉnh dung lượng dựa trên nhu cầu
- **Purpose:** Maintain application availability and manage costs
- **Use Case:** Traffic spikes, cost optimization, maintaining performance

**6.1.2 Multi-AZ (Availability Zone)** 🏗️
- EN: Deploying resources across multiple data centers
- VN: Triển khai tài nguyên qua nhiều trung tâm dữ liệu
- **Purpose:** Achieve high availability and fault tolerance
- **Use Case:** Database failover, disaster recovery, eliminating single points of failure

**6.1.3 Fault Tolerance** 🏗️
- EN: System's ability to continue operating despite failures
- VN: Khả năng hệ thống tiếp tục hoạt động dù có lỗi
- **Purpose:** Maintain service availability during component failures
- **Use Case:** Mission-critical applications, always-on services, redundant systems

### 6.2 Performance & Scalability
*Hiệu suất & Khả năng mở rộng*

**6.2.1 Elastic** ⚡💰
- EN: Ability to scale resources up/down automatically
- VN: Khả năng tự động mở rộng/thu hẹp tài nguyên
- **Purpose:** Adapt to changing demand while optimizing costs
- **Use Case:** Variable workloads, cost optimization, handling traffic spikes

**6.2.2 Caching** ⚡💰
- EN: Storing frequently accessed data for faster retrieval
- VN: Lưu trữ dữ liệu thường truy cập để truy xuất nhanh hơn
- **Purpose:** Improve application performance and reduce backend load
- **Use Case:** Database query optimization, API response caching, session storage

**6.2.3 Edge Location** ⚡💰
- EN: AWS data centers for content caching worldwide
- VN: Trung tâm dữ liệu AWS để cache nội dung toàn cầu
- **Purpose:** Deliver content closer to end users for better performance
- **Use Case:** Global content delivery, reduced latency, improved user experience

**6.2.4 IOPS (Input/Output Operations Per Second)** ⚡💰
- EN: Measurement of how many read/write operations a storage system can perform each second
- VN: Thước đo số lượng thao tác đọc/ghi một hệ thống lưu trữ thực hiện mỗi giây
- **Purpose:** Benchmark and provision storage performance to meet workload latency and throughput needs
- **Use Case:** Selecting EBS gp3/io1/io2 volumes, sizing Provisioned IOPS for databases, performance tuning for high-transaction systems

---

## 7. AWS Pricing & Cost Optimization
*Định giá & Tối ưu chi phí AWS*

### 7.1 Pricing Models
*Mô hình định giá*

**7.1.1 On-Demand** 💰
- EN: Pay-as-you-use pricing with no commitments
- VN: Định giá trả theo sử dụng không cam kết
- **Purpose:** Flexible computing with no upfront costs or commitments
- **Use Case:** Development, testing, unpredictable workloads, short-term needs

**7.1.2 Reserved Instances** 💰
- EN: Discounted pricing for committed usage terms
- VN: Định giá giảm giá cho cam kết sử dụng
- **Purpose:** Significant cost savings for steady-state workloads
- **Use Case:** Production environments, predictable usage, long-term applications

**7.1.3 Spot Instances** 💰
- EN: Bid-based pricing for unused EC2 capacity
- VN: Định giá đấu thầu cho dung lượng EC2 không sử dụng
- **Purpose:** Access spare compute capacity at reduced costs
- **Use Case:** Batch processing, fault-tolerant workloads, flexible applications

### 7.2 Cost Management
*Quản lý chi phí*

**7.2.1 Cost Explorer** 💰
- EN: Tool for visualizing and analyzing AWS costs
- VN: Công cụ trực quan hóa và phân tích chi phí AWS
- **Purpose:** Understand spending patterns and identify cost optimization opportunities
- **Use Case:** Cost analysis, budget planning, spending trends, resource optimization

**7.2.2 Budgets** 💰
- EN: Service for setting cost and usage budgets
- VN: Dịch vụ thiết lập ngân sách chi phí và sử dụng
- **Purpose:** Monitor costs and usage against defined budgets
- **Use Case:** Cost control, spending alerts, budget management, cost governance

**7.2.3 Trusted Advisor** 🏗️⚡🔒💰
- EN: Service providing optimization recommendations
- VN: Dịch vụ cung cấp khuyến nghị tối ưu hóa
- **Purpose:** Provide best practice recommendations across multiple categories
- **Use Case:** Cost optimization, security improvements, performance tuning, fault tolerance

---

---

## 8. Data Analytics & Business Intelligence
*Phân tích dữ liệu & Business Intelligence*

### 8.1 Data Processing Concepts
*Khái niệm xử lý dữ liệu*

**8.1.1 ETL (Extract, Transform, Load)** ⚡💰
- EN: Process of extracting data from sources, transforming it, and loading into target
- VN: Quy trình trích xuất dữ liệu từ nguồn, chuyển đổi và tải vào đích
- **Purpose:** Prepare and integrate data from multiple sources
- **Use Case:** Data warehousing, data lake preparation, system integration

**8.1.2 ELT (Extract, Load, Transform)** ⚡💰
- EN: Process of extracting data, loading into target, then transforming
- VN: Quy trình trích xuất dữ liệu, tải vào đích, sau đó chuyển đổi
- **Purpose:** Leverage target system's processing power for transformations
- **Use Case:** Cloud data warehouses, big data platforms, modern analytics

**8.1.3 Data Lake** 🏗️💰
- EN: Centralized repository storing structured and unstructured data at scale
- VN: Kho lưu trữ tập trung chứa dữ liệu có cấu trúc và phi cấu trúc ở quy mô lớn
- **Purpose:** Store raw data in native format for future analysis
- **Use Case:** Big data analytics, ML training data, exploratory analysis

**8.1.4 Data Warehouse** ⚡💰
- EN: Optimized database system for analytical queries and reporting
- VN: Hệ thống cơ sở dữ liệu được tối ưu hóa cho truy vấn phân tích và báo cáo
- **Purpose:** Structured data storage optimized for business intelligence
- **Use Case:** Business reporting, OLAP, executive dashboards

**8.1.5 OLAP (Online Analytical Processing)** ⚡
- EN: Technology for fast analysis of multidimensional data
- VN: Công nghệ phân tích nhanh dữ liệu đa chiều
- **Purpose:** Enable complex analytical queries on large datasets
- **Use Case:** Business intelligence, data mining, financial analysis

**8.1.6 OLTP (Online Transaction Processing)** ⚡
- EN: Class of systems optimized for fast, reliable processing of numerous short, atomic transactions
- VN: Hệ thống được tối ưu để xử lý nhanh, tin cậy nhiều giao dịch ngắn và nguyên tử
- **Purpose:** Maintain data integrity and low-latency response for high-volume transactional workloads
- **Use Case:** E-commerce orders, banking systems, inventory management on RDS/Aurora, DynamoDB transactional APIs

### 8.2 Streaming & Real-time Processing
*Xử lý streaming và thời gian thực*

**8.2.1 Stream Processing** ⚡
- EN: Processing data in real-time as it flows through the system
- VN: Xử lý dữ liệu thời gian thực khi nó chảy qua hệ thống
- **Purpose:** Analyze data immediately as it arrives
- **Use Case:** Real-time analytics, fraud detection, IoT monitoring

**8.2.2 Batch Processing** 💰
- EN: Processing data in discrete chunks or batches
- VN: Xử lý dữ liệu theo từng khối hoặc lô riêng biệt
- **Purpose:** Process large volumes of data efficiently
- **Use Case:** Daily reports, data warehouse loading, historical analysis

**8.2.3 Sharding** ⚡
- EN: Distributing data across multiple machines for parallel processing
- VN: Phân phối dữ liệu qua nhiều máy để xử lý song song
- **Purpose:** Scale processing power by distributing workload
- **Use Case:** Kinesis data streams, database scaling, distributed computing

**8.2.4 Partition Key** ⚡
- EN: Key used to determine which shard or partition data belongs to
- VN: Khóa dùng để xác định dữ liệu thuộc shard hoặc phân vùng nào
- **Purpose:** Ensure related data is processed together
- **Use Case:** Kinesis streams, DynamoDB, distributed databases

### 8.3 Business Intelligence Concepts
*Khái niệm Business Intelligence*

**8.3.1 KPI (Key Performance Indicator)** 📊
- EN: Measurable value demonstrating how effectively objectives are achieved
- VN: Giá trị có thể đo lường chứng minh mức độ đạt được mục tiêu
- **Purpose:** Track business performance against strategic goals
- **Use Case:** Executive dashboards, performance monitoring, business reviews

**8.3.2 Drill Down** 📊
- EN: Navigation from summary to detailed level in data analysis
- VN: Điều hướng từ mức tóm tắt đến mức chi tiết trong phân tích dữ liệu
- **Purpose:** Explore data at different levels of granularity
- **Use Case:** Interactive dashboards, root cause analysis, data exploration

**8.3.3 Cross-filtering** 📊
- EN: Selecting data in one visualization affects others on the same dashboard
- VN: Chọn dữ liệu trong một biểu đồ ảnh hưởng đến các biểu đồ khác cùng dashboard
- **Purpose:** Enable interactive exploration across related visuals
- **Use Case:** Interactive dashboards, data discovery, contextual analysis

**8.3.4 Row-Level Security (RLS)** 🔒
- EN: Security model that restricts data access based on user characteristics
- VN: Mô hình bảo mật hạn chế truy cập dữ liệu dựa trên đặc điểm người dùng
- **Purpose:** Ensure users only see data they're authorized to access
- **Use Case:** Multi-tenant dashboards, departmental reporting, data privacy

**8.3.5 Embedded Analytics** 📊💰
- EN: Integration of BI capabilities directly into business applications
- VN: Tích hợp khả năng BI trực tiếp vào ứng dụng kinh doanh
- **Purpose:** Provide analytics within existing user workflows
- **Use Case:** Customer portals, SaaS applications, internal tools

### 8.4 Data Formats & Storage
*Định dạng dữ liệu và lưu trữ*

**8.4.1 Parquet** ⚡💰
- EN: Columnar storage file format optimized for analytics
- VN: Định dạng file lưu trữ cột được tối ưu hóa cho phân tích
- **Purpose:** Efficient storage and querying of analytical data
- **Use Case:** Data lakes, Athena queries, Spark processing

**8.4.2 ORC (Optimized Row Columnar)** ⚡💰
- EN: Columnar storage format with compression and indexing
- VN: Định dạng lưu trữ cột với nén và lập chỉ mục
- **Purpose:** High-performance storage for Hive-based analytics
- **Use Case:** EMR processing, Hive queries, big data analytics

**8.4.3 Avro** ⚡
- EN: Schema evolution-friendly serialization format
- VN: Định dạng serialization thân thiện với sự phát triển schema
- **Purpose:** Flexible data serialization with schema evolution support
- **Use Case:** Streaming data, schema evolution, Kafka messages

**8.4.4 Delta Lake** ⚡
- EN: Storage layer providing ACID transactions on top of data lakes
- VN: Lớp lưu trữ cung cấp giao dịch ACID trên data lake
- **Purpose:** Reliable data lakes with transactional consistency
- **Use Case:** Data lake reliability, time travel, concurrent access

---

## 9. AWS Media Services
*Dịch vụ truyền thông AWS*

### 9.1 Media Processing Services
*Dịch vụ xử lý truyền thông*

**9.1.1 Elastic Transcoder** 🏗️⚡💰
- EN: Cloud-based media transcoding service for converting video/audio files
- VN: Dịch vụ chuyển đổi định dạng media trên cloud để chuyển đổi file video/audio
- **Purpose:** Convert media files between different formats and resolutions
- **Use Case:** Video streaming preparation, mobile app content, multi-format delivery

**9.1.2 MediaConvert** 🏗️⚡💰
- EN: File-based video transcoding service with broadcast-grade features
- VN: Dịch vụ chuyển đổi video dựa trên file với tính năng cấp phát sóng
- **Purpose:** Professional video processing and format conversion
- **Use Case:** Broadcast workflows, professional video production, content preparation

**9.1.3 MediaLive** 🏗️⚡💰
- EN: Live video processing service for broadcast and streaming
- VN: Dịch vụ xử lý video trực tiếp cho phát sóng và streaming
- **Purpose:** Encode live video streams for broadcast and multiscreen delivery
- **Use Case:** Live streaming, broadcast TV, real-time video processing

**9.1.4 MediaPackage** 🏗️⚡🔒
- EN: Video origination and packaging service for secure delivery
- VN: Dịch vụ tạo nguồn và đóng gói video để phân phối bảo mật
- **Purpose:** Package and deliver video content securely to various devices
- **Use Case:** OTT platforms, video streaming, content protection

**9.1.5 MediaStore** 🏗️⚡💰
- EN: High-performance storage service optimized for media
- VN: Dịch vụ lưu trữ hiệu suất cao được tối ưu hóa cho media
- **Purpose:** Store and deliver video content with high throughput
- **Use Case:** Live streaming origin, media workflows, high-bandwidth content

### 9.2 Media Streaming Concepts
*Khái niệm streaming media*

**9.2.1 Transcoding** ⚡💰
- EN: Process of converting media from one format/codec to another
- VN: Quá trình chuyển đổi media từ định dạng/codec này sang khác
- **Purpose:** Optimize media for different devices and bandwidths
- **Use Case:** Multi-device support, bandwidth optimization, format compatibility

**9.2.2 HLS (HTTP Live Streaming)** ⚡
- EN: Adaptive bitrate streaming protocol developed by Apple
- VN: Giao thức streaming bitrate thích ứng được phát triển bởi Apple
- **Purpose:** Deliver live and on-demand video over HTTP
- **Use Case:** iOS streaming, adaptive video delivery, live broadcasts

**9.2.3 DASH (Dynamic Adaptive Streaming)** ⚡
- EN: Adaptive streaming technique enabling high-quality streaming
- VN: Kỹ thuật streaming thích ứng cho phép streaming chất lượng cao
- **Purpose:** Provide smooth streaming experience across different network conditions
- **Use Case:** Video streaming platforms, bandwidth adaptation, quality optimization

**9.2.4 ABR (Adaptive Bitrate Streaming)** ⚡
- EN: Streaming technique that adjusts video quality based on network conditions
- VN: Kỹ thuật streaming điều chỉnh chất lượng video dựa trên điều kiện mạng
- **Purpose:** Optimize streaming quality based on available bandwidth
- **Use Case:** Video streaming, mobile content delivery, network optimization

**9.2.5 CDN (Content Delivery Network)** ⚡🔒💰
- EN: Geographically distributed servers for content caching and delivery
- VN: Máy chủ phân tán địa lý để cache và phân phối nội dung
- **Purpose:** Deliver media content with low latency globally
- **Use Case:** Video streaming, global content distribution, performance optimization

---

## 10. Machine Learning & AI Services
*Dịch vụ Machine Learning và AI*

### 9.1 ML Platform Services
*Dịch vụ nền tảng ML*

**9.1.1 SageMaker** 🏗️⚡💰
- EN: Fully managed machine learning platform
- VN: Nền tảng machine learning được quản lý hoàn toàn
- **Purpose:** Build, train, and deploy ML models at scale
- **Use Case:** Model development, ML pipelines, model hosting

**9.1.2 Comprehend** ⚡💰
- EN: Natural language processing service for text analysis
- VN: Dịch vụ xử lý ngôn ngữ tự nhiên để phân tích văn bản
- **Purpose:** Extract insights from text using NLP
- **Use Case:** Sentiment analysis, entity extraction, document classification

**9.1.3 Rekognition** ⚡💰
- EN: Image and video analysis service using deep learning
- VN: Dịch vụ phân tích hình ảnh và video sử dụng deep learning
- **Purpose:** Analyze images and videos for objects, faces, and activities
- **Use Case:** Content moderation, facial recognition, object detection

**9.1.4 Textract** ⚡💰
- EN: Extract text and data from documents using OCR and ML
- VN: Trích xuất văn bản và dữ liệu từ tài liệu sử dụng OCR và ML
- **Purpose:** Automatically extract structured data from documents
- **Use Case:** Document processing, form analysis, invoice processing

---

*End of Keywords Reference / Kết thúc tài liệu tham khảo từ khóa*