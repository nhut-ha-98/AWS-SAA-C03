# 🏗️ AWS Solutions Architect Associate (SAA-C03) - Complete Study Guide

> **Exam Overview**: 130 phút | 65 câu hỏi | Điểm đậu: 720/1000 | $150 USD  
> **Domains**: Design Secure Architectures (30%) | Design Resilient Architectures (26%) | Design High-Performing Architectures (24%) | Design Cost-Optimized Architectures (20%)

## � Exam Domains & Weightings

| Domain | Percentage | Key Focus Areas |
|--------|------------|-----------------|
| **Domain 1**: Design Secure Architectures | 30% | Access controls, data protection, security services |
| **Domain 2**: Design Resilient Architectures | 26% | Multi-tier architectures, disaster recovery, scalability |
| **Domain 3**: Design High-Performing Architectures | 24% | Caching, database optimization, compute solutions |
| **Domain 4**: Design Cost-Optimized Architectures | 20% | Storage tiers, compute optimization, monitoring |

📖 **Official Exam Guide**: [AWS SAA-C03 Exam Guide](https://d1.awsstatic.com/training-and-certification/docs-sa-assoc/AWS-Certified-Solutions-Architect-Associate_Exam-Guide.pdf)

---

# 📋 Complete AWS Services Checklist

**Priority Levels**:
- 🔥 **CRITICAL** - Must know thoroughly (appear in 80%+ questions)
- ⭐ **HIGH** - Important for exam success (appear in 50%+ questions) 
- ➕ **MEDIUM** - Good to know (appear in 20%+ questions)
- 💡 **BASIC** - Conceptual understanding needed

---

## 1. 💻 Compute Services

### 🔥 **Amazon EC2** (Elastic Compute Cloud)

**Core Concepts**:
- **Instance Types**: T4g (burstable), M6i (general), C6i (compute), R6i (memory), I4i (storage)
- **Pricing Models**: On-Demand, Reserved (1-3 year), Spot (up to 90% savings), Savings Plans, Dedicated Hosts
- **Instance Metadata**: 169.254.169.254/latest/meta-data/
- **User Data**: Bootstrap scripts, runs at first boot only

**Storage Options**:
- **EBS Types**: gp3 (general SSD), io1/io2 (provisioned IOPS), st1 (throughput HDD), sc1 (cold HDD)
- **Snapshots**: Point-in-time backups, incremental, cross-region copy
- **Encryption**: At rest + in transit, KMS integration

**Placement Groups**:
- **Cluster**: Same AZ, 10 Gbps network, low latency
- **Spread**: Different hardware, max 7 instances per AZ  
- **Partition**: Up to 7 partitions per AZ, big data workloads

**Key Exam Points**:
- ✅ Spot instances for fault-tolerant workloads
- ✅ Reserved instances for predictable workloads  
- ✅ EBS-optimized instances for storage performance
- ✅ Enhanced networking (SR-IOV, ENA) for HPC

📖 **Documentation**: [EC2 User Guide](https://docs.aws.amazon.com/ec2/) | [Instance Types](https://aws.amazon.com/ec2/instance-types/) | [EBS Documentation](https://docs.aws.amazon.com/ebs/)

---

### 🔥 **Elastic Load Balancing (ELB) & Auto Scaling**

**Load Balancer Types**:
- **ALB** (Application): Layer 7, HTTP/HTTPS, WebSocket, path/host routing, sticky sessions
- **NLB** (Network): Layer 4, TCP/UDP, extreme performance, static IP, preserves source IP
- **GLB** (Gateway): Layer 3, GENEVE protocol, third-party appliances
- **CLB** (Classic): Legacy, avoid for new deployments

**Auto Scaling Groups (ASG)**:
- **Scaling Policies**: Simple, Step, Target Tracking, Predictive
- **Health Checks**: EC2 vs ELB health checks
- **Lifecycle Hooks**: Custom actions during launch/terminate
- **Multiple Instance Types**: Mixed instance types and purchase options

**Advanced Features**:
- **Cross-Zone Load Balancing**: Distribute evenly across AZs
- **Connection Draining**: Graceful shutdown (CLB) / Deregistration Delay (ALB/NLB)
- **SSL Termination**: Offload SSL processing to load balancer

**Key Exam Points**:
- ✅ ALB for HTTP/HTTPS applications with advanced routing
- ✅ NLB for extreme performance and static IP requirements
- ✅ Target tracking scaling for automatic CPU/request management
- ✅ Health check grace period during ASG scaling

📖 **Documentation**: [ELB User Guide](https://docs.aws.amazon.com/elasticloadbalancing/) | [Auto Scaling User Guide](https://docs.aws.amazon.com/autoscaling/)

---

### 🔥 **AWS Lambda** (Serverless Compute)

**Core Features**:
- **Runtime Support**: Python, Node.js, Java, C#, Go, Ruby, Custom runtimes
- **Execution Limits**: 15 min timeout, 10 GB memory, 512 MB `/tmp` storage
- **Concurrency**: 1000 concurrent executions (default), reserved/provisioned concurrency
- **Cold Starts**: Initialization delay, use provisioned concurrency for latency-sensitive apps

**Integration Patterns**:
- **Event Sources**: S3, DynamoDB, Kinesis, SQS, SNS, API Gateway, EventBridge
- **Destinations**: Success/failure routing to SQS, SNS, Lambda, EventBridge
- **Layers**: Shared libraries, up to 5 layers per function

**Monitoring & Debugging**:
- **CloudWatch**: Automatic logging, custom metrics
- **X-Ray**: Distributed tracing, performance analysis
- **Dead Letter Queues**: Failed execution handling

**Key Exam Points**:
- ✅ Event-driven architectures and serverless patterns
- ✅ Cost optimization compared to EC2 for sporadic workloads
- ✅ VPC configuration for database access
- ✅ Environment variables and parameter store integration

📖 **Documentation**: [Lambda Developer Guide](https://docs.aws.amazon.com/lambda/) | [Serverless Application Lens](https://docs.aws.amazon.com/wellarchitected/latest/serverless-applications-lens/)

---

### ⭐ **Amazon ECS & EKS** (Container Services)

**ECS (Elastic Container Service)**:
- **Launch Types**: EC2 (manage instances) vs Fargate (serverless)
- **Task Definitions**: Container specifications, CPU/memory, networking
- **Services**: Desired count, load balancer integration, auto scaling
- **Service Discovery**: DNS-based service discovery within VPC

**EKS (Elastic Kubernetes Service)**:
- **Managed Control Plane**: AWS-managed Kubernetes masters
- **Worker Nodes**: EC2 instances or Fargate for pods
- **Add-ons**: VPC CNI, CoreDNS, kube-proxy
- **IRSA**: IAM Roles for Service Accounts

**Key Exam Points**:
- ✅ Fargate for serverless containers without EC2 management
- ✅ ECS for simpler container orchestration, EKS for Kubernetes expertise
- ✅ Task placement constraints and strategies
- ✅ Integration with ALB for container load balancing

📖 **Documentation**: [ECS Developer Guide](https://docs.aws.amazon.com/ecs/) | [EKS User Guide](https://docs.aws.amazon.com/eks/)

---

### ➕ **AWS Batch** (Managed Batch Computing)

**Core Components**:
- **Job Definitions**: Container images, vCPU, memory requirements
- **Job Queues**: Priority-based job scheduling
- **Compute Environments**: Managed/unmanaged EC2 instances
- **Array Jobs**: Parallel processing of large datasets

**Use Cases**: Scientific computing, image processing, financial risk modeling

📖 **Documentation**: [AWS Batch User Guide](https://docs.aws.amazon.com/batch/)

---

### ➕ **Elastic Beanstalk** (Platform as a Service)

**Supported Platforms**:
- **Languages**: Java, .NET, PHP, Node.js, Python, Ruby, Go
- **Containers**: Docker single/multi-container
- **Infrastructure**: Auto-managed EC2, ELB, Auto Scaling, monitoring

**Deployment Options**:
- **All at once**: Fastest, brief downtime
- **Rolling**: No downtime, reduced capacity during deployment  
- **Rolling with additional batch**: No downtime, maintains full capacity
- **Immutable**: Zero downtime, full replacement deployment
- **Blue/Green**: Manual, complete environment swap

**Key Exam Points**:
- ✅ Quick deployment for standard web applications
- ✅ Underlying infrastructure still accessible for customization
- ✅ Integration with RDS, ElastiCache, and other AWS services

📖 **Documentation**: [Elastic Beanstalk Developer Guide](https://docs.aws.amazon.com/elasticbeanstalk/)

---

## 2. 🗄️ Storage Services

### 🔥 **Amazon S3** (Simple Storage Service)

**Storage Classes & Pricing**:
- **Standard**: Frequent access, 99.999999999% (11 9's) durability
- **Standard-IA**: Infrequent access, lower cost, retrieval fees
- **One Zone-IA**: Single AZ, 20% less cost than Standard-IA
- **Glacier Instant Retrieval**: Archive with millisecond access
- **Glacier Flexible Retrieval**: 1-12 hours retrieval (formerly Glacier)
- **Glacier Deep Archive**: Cheapest, 12+ hours retrieval
- **Intelligent Tiering**: Automatic cost optimization

**Advanced Features**:
- **Versioning**: Multiple versions of objects, delete protection
- **MFA Delete**: Extra security for versioned objects
- **Lifecycle Policies**: Automatic transitions between storage classes
- **Cross-Region Replication (CRR)**: Different regions, compliance
- **Same-Region Replication (SRR)**: Within region, log aggregation
- **Transfer Acceleration**: CloudFront edge locations for uploads
- **Multipart Upload**: Large files >5GB, parallel uploads

**Security & Access Control**:
- **Bucket Policies**: JSON-based, resource-level permissions
- **ACLs**: Legacy, object/bucket level (avoid for new deployments)
- **Pre-signed URLs**: Temporary access to private objects
- **VPC Endpoints**: Private access without internet gateway
- **Access Points**: Simplified access management for complex buckets

**Encryption Options**:
- **SSE-S3**: AWS managed keys (AES-256)
- **SSE-KMS**: Customer managed keys, audit trail
- **SSE-C**: Customer provided keys
- **Client-side**: Encrypt before upload

**Performance Optimization**:
- **Request Patterns**: Avoid sequential naming (timestamps, alphabetical)
- **Prefix Distribution**: Spread across multiple prefixes
- **CloudFront**: Global content delivery network
- **S3 Select**: Retrieve subset of object data using SQL

**Key Exam Points**:
- ✅ Storage class selection based on access patterns and cost requirements
- ✅ Lifecycle policies for automated cost optimization  
- ✅ Cross-region replication for disaster recovery and compliance
- ✅ Pre-signed URLs for temporary access without AWS credentials
- ✅ VPC endpoints for secure, private access from VPC

📖 **Documentation**: [S3 User Guide](https://docs.aws.amazon.com/s3/) | [S3 Storage Classes](https://aws.amazon.com/s3/storage-classes/) | [S3 Performance Guidelines](https://docs.aws.amazon.com/s3/latest/userguide/optimizing-performance.html)

---

### 🔥 **Amazon EBS** (Elastic Block Store)

**Volume Types**:
- **gp3** (General Purpose SSD): 3,000-16,000 IOPS, independent throughput/IOPS scaling
- **gp2** (General Purpose SSD): Burstable IOPS, baseline 3 IOPS/GB
- **io1/io2** (Provisioned IOPS SSD): Up to 64,000 IOPS, database workloads
- **st1** (Throughput Optimized HDD): Big data, data warehouses, log processing  
- **sc1** (Cold HDD): Less frequently accessed, lowest cost

**Advanced Features**:
- **Snapshots**: Point-in-time backups, incremental, stored in S3
- **Fast Snapshot Restore (FSR)**: Instantly restore from snapshots
- **Multi-Attach**: Attach single volume to multiple instances (io1/io2 only)
- **Encryption**: At rest and in transit, KMS integration, boot volume encryption
- **Elastic Volumes**: Modify size, performance, and type without downtime

**Performance Considerations**:
- **IOPS vs Throughput**: Match to application requirements
- **Pre-warming**: Initialize volumes from snapshots for consistent performance
- **EBS-Optimized**: Dedicated bandwidth between EC2 and EBS
- **Placement Groups**: Cluster placement for networked storage workloads

**Key Exam Points**:
- ✅ gp3 as default choice for most workloads due to independent scaling
- ✅ io1/io2 for databases requiring consistent high IOPS (>16,000)
- ✅ EBS snapshots for backup and disaster recovery strategies
- ✅ Encryption for sensitive data compliance requirements

📖 **Documentation**: [EBS User Guide](https://docs.aws.amazon.com/ebs/) | [EBS Volume Types](https://docs.aws.amazon.com/ebs/latest/userguide/ebs-volume-types.html)

---

### ⭐ **Amazon EFS** (Elastic File System)

**File System Features**:
- **POSIX-compliant**: Standard file system semantics
- **Scalability**: Petabyte scale, auto-scaling capacity
- **Availability**: Multi-AZ by default, 99.999999999% durability
- **Access**: NFSv4.1 protocol, concurrent access from multiple instances

**Performance Modes**:
- **General Purpose**: Lowest latency, up to 7,000 file operations/sec
- **Max I/O**: Higher latency, >7,000 file operations/sec

**Throughput Modes**:
- **Bursting**: Baseline + burst based on file system size
- **Provisioned**: Independent of storage amount, consistent performance

**Storage Classes**:
- **Standard**: Frequent access, multi-AZ storage
- **Infrequent Access (IA)**: Lower cost, retrieval fees
- **Archive**: Lowest cost, rarely accessed files

**Key Exam Points**:
- ✅ Shared storage across multiple EC2 instances and AZs
- ✅ POSIX compliance for applications requiring standard file system
- ✅ Auto-scaling eliminates capacity planning
- ✅ Lifecycle management for automatic cost optimization

📖 **Documentation**: [EFS User Guide](https://docs.aws.amazon.com/efs/) | [EFS Performance](https://docs.aws.amazon.com/efs/latest/ug/performance.html)

---

### ⭐ **AWS FSx** (Fully Managed File Systems)

**FSx for Windows File Server**:
- **Active Directory**: Native Windows features, DFS namespaces
- **Performance**: Up to 2 GB/s throughput, submillisecond latency
- **Backup**: Automatic daily backups, point-in-time recovery

**FSx for Lustre**:
- **HPC Workloads**: Machine learning, high performance computing
- **S3 Integration**: Process data directly from S3 buckets
- **Performance**: Up to hundreds of GB/s throughput

**FSx for NetApp ONTAP**:
- **NFS/SMB**: Multi-protocol access, data deduplication
- **SnapMirror**: Replication to on-premises NetApp systems

**FSx for OpenZFS**:
- **High Performance**: Up to 4 GB/s throughput, millions of IOPS
- **Snapshots**: Point-in-time copies, space-efficient

📖 **Documentation**: [FSx User Guide](https://docs.aws.amazon.com/fsx/)

---

### ➕ **Storage Gateway** (Hybrid Storage)

**Gateway Types**:
- **File Gateway**: NFS/SMB access to S3 objects as files
- **Volume Gateway**: iSCSI block storage with S3 backing
  - **Stored Volumes**: Primary on-premises, async backup to S3
  - **Cached Volumes**: Primary on S3, cache frequently accessed data
- **Tape Gateway**: Virtual Tape Library (VTL) for backup applications

**Use Cases**: Hybrid cloud storage, backup to cloud, disaster recovery

📖 **Documentation**: [Storage Gateway User Guide](https://docs.aws.amazon.com/storagegateway/)

---

### 💡 **Instance Store** (Ephemeral Storage)

**Characteristics**:
- **Temporary**: Data lost on instance stop/terminate/failure
- **Performance**: Very high IOPS and throughput, NVMe SSD
- **Use Cases**: Temporary processing, caches, buffers, scratch data
- **Instance Types**: I3, I4i, D2, D3, R5d, M5d, C5d families

**Key Exam Points**:
- ✅ Highest storage performance but temporary
- ✅ Good for distributed systems with replication
- ✅ Cannot be detached/attached like EBS volumes

📖 **Documentation**: [Instance Store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html)

---

## 3. 🌐 Networking & Content Delivery

### 🔥 **Amazon VPC** (Virtual Private Cloud)

**Core Components**:
- **CIDR Blocks**: IPv4 (10.0.0.0/16) and IPv6, non-overlapping ranges
- **Subnets**: Public (IGW route), private (no direct internet), isolated
- **Route Tables**: Control traffic routing, associated with subnets
- **Internet Gateway (IGW)**: Bi-directional internet access for public subnets
- **NAT Gateway/Instance**: Outbound internet for private subnets (AZ-specific)

**Advanced Networking**:
- **VPC Peering**: Direct network connection between VPCs (no transitive routing)
- **Transit Gateway**: Central hub for multiple VPC connections, supports transitive routing
- **VPN Gateway**: Site-to-site VPN connections to on-premises
- **Direct Connect**: Dedicated network connection, consistent bandwidth/latency
- **VPC Endpoints**: Private connectivity to AWS services without internet

**Endpoint Types**:
- **Gateway Endpoints**: S3 and DynamoDB, route table entries
- **Interface Endpoints**: Private IP addresses, powered by PrivateLink
- **VPC Lattice**: Service mesh for service-to-service communication

**Security Groups vs NACLs**:
- **Security Groups**: Instance-level, stateful, allow rules only
- **NACLs**: Subnet-level, stateless, allow/deny rules, processed in order

**DNS and DHCP**:
- **DNS Resolution**: VPC DNS resolver, custom DNS via DHCP options
- **DNS Hostnames**: Public DNS names for public IP addresses
- **DHCP Options Sets**: Custom DNS servers, domain names, NTP servers

**Key Exam Points**:
- ✅ Public subnet requires IGW route (0.0.0.0/0 → igw-xxx)
- ✅ Private subnet uses NAT Gateway for outbound internet access
- ✅ VPC Peering does not support transitive routing between VPCs
- ✅ VPC Endpoints eliminate data transfer charges for AWS service access
- ✅ Security Groups are stateful; NACLs are stateless

📖 **Documentation**: [VPC User Guide](https://docs.aws.amazon.com/vpc/) | [VPC Networking](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html) | [AWS PrivateLink](https://docs.aws.amazon.com/vpc/latest/privatelink/)

---

### 🔥 **Route 53** (DNS & Domain Registration)

**Record Types**:
- **A**: IPv4 address mapping (example.com → 192.0.2.1)
- **AAAA**: IPv6 address mapping
- **CNAME**: Canonical name for another domain (www.example.com → example.com)
- **Alias**: AWS-specific, points to AWS resources (ELB, CloudFront, S3)
- **MX**: Mail exchange servers for email routing
- **TXT**: Text records for verification and SPF/DKIM

**Routing Policies**:
- **Simple**: Single resource, no health checks
- **Weighted**: Traffic distribution by percentages (A/B testing, gradual deployments)
- **Latency-based**: Route to lowest latency region for user
- **Failover**: Active/passive setup with health checks
- **Geolocation**: Route based on user's geographic location
- **Geoproximity**: Route based on location with bias adjustment
- **Multi-value Answer**: Multiple IP addresses with health checks

**Health Checks**:
- **Endpoint Monitoring**: HTTP/HTTPS/TCP health checks
- **Calculated Health Checks**: Combine multiple health checks with AND/OR/NOT
- **CloudWatch Alarms**: Health checks based on CloudWatch metrics
- **String Matching**: Check for specific text in response

**Advanced Features**:
- **Private Hosted Zones**: DNS resolution within VPC
- **Resolver**: Hybrid DNS between on-premises and AWS
- **Traffic Flow**: Visual editor for complex routing policies
- **Domain Registration**: Register and transfer domains

**Key Exam Points**:
- ✅ Alias records for AWS resources (no charge for queries)
- ✅ Weighted routing for gradual deployments and A/B testing
- ✅ Latency-based routing for global applications with multiple regions
- ✅ Health checks for automatic failover to healthy resources
- ✅ Private hosted zones for internal DNS resolution

📖 **Documentation**: [Route 53 Developer Guide](https://docs.aws.amazon.com/route53/) | [Routing Policies](https://docs.aws.amazon.com/route53/latest/developerguide/routing-policy.html)

---

### 🔥 **CloudFront** (Content Delivery Network)

**Core Features**:
- **Global Edge Locations**: 400+ locations worldwide for low latency
- **Origin Types**: S3 buckets, ELB, EC2, on-premises servers
- **Caching**: TTL-based, cache behaviors, query string/header forwarding
- **Compression**: Automatic gzip compression for better performance

**Distribution Types**:
- **Web Distribution**: Static/dynamic content, streaming media
- **RTMP Distribution**: Adobe Flash media streaming (legacy)

**Security Features**:
- **OAI (Origin Access Identity)**: Restrict S3 bucket access to CloudFront only
- **OAC (Origin Access Control)**: Next-generation OAI with additional features
- **Signed URLs**: Time-limited access to individual files
- **Signed Cookies**: Access to multiple files, user sessions
- **Geographic Restrictions**: Block/allow content by country
- **AWS WAF Integration**: Web application firewall protection

**Performance Optimization**:
- **Cache Behaviors**: Different caching rules for different paths
- **Origin Request Policies**: Control headers/cookies sent to origin
- **Response Headers Policies**: Add security headers to responses
- **Field-Level Encryption**: Encrypt sensitive form data

**Advanced Features**:
- **Lambda@Edge**: Run code at edge locations for content customization
- **CloudFront Functions**: Lightweight JavaScript for simple transformations
- **Origin Shield**: Additional caching layer to reduce origin load
- **Real-time Logs**: Detailed request logs for analysis

**Key Exam Points**:
- ✅ Use OAI/OAC to restrict S3 bucket access to CloudFront only
- ✅ Signed URLs for individual file access control
- ✅ Geographic restrictions for content licensing compliance
- ✅ Multiple origins and cache behaviors for complex applications
- ✅ Lambda@Edge for dynamic content generation at edge

📖 **Documentation**: [CloudFront Developer Guide](https://docs.aws.amazon.com/cloudfront/) | [CloudFront Security](https://docs.aws.amazon.com/cloudfront/latest/developerguide/SecurityAndPrivacyFeatures.html)

---

### ⭐ **AWS Global Accelerator**

**Core Features**:
- **Anycast IP Addresses**: Static IPs that route to optimal AWS edge location
- **Traffic Dials**: Control traffic percentage to endpoint groups
- **Endpoint Weights**: Distribute traffic within endpoint group
- **Health Checks**: Automatic failover to healthy endpoints

**Use Cases**:
- **Gaming Applications**: Consistent, low-latency connections
- **IoT Applications**: Reliable connectivity for global devices
- **VoIP Applications**: Improved call quality and reliability

**vs CloudFront**:
- Global Accelerator: TCP/UDP traffic, static IP addresses, improve performance
- CloudFront: HTTP/HTTPS content, dynamic IP addresses, cache content

📖 **Documentation**: [Global Accelerator Developer Guide](https://docs.aws.amazon.com/global-accelerator/)

---

### ⭐ **API Gateway**

**Gateway Types**:
- **REST API**: Full-featured, supports caching, custom domain names
- **HTTP API**: Lower cost, faster, OpenAPI 3.0 support
- **WebSocket API**: Bi-directional communication, real-time applications

**Integration Types**:
- **Lambda Function**: Invoke Lambda functions
- **HTTP Endpoint**: Proxy to HTTP endpoints
- **AWS Service**: Direct integration with AWS services
- **Mock Integration**: Return static responses

**Security Features**:
- **API Keys**: Simple API access control
- **Usage Plans**: Throttling and quota management
- **Authorizers**: Lambda authorizers, Cognito User Pools
- **Resource Policies**: IAM-based access control
- **WAF Integration**: Web application firewall protection

**Key Exam Points**:
- ✅ REST API for full features, HTTP API for simple use cases and cost optimization
- ✅ Lambda authorizers for custom authentication logic
- ✅ Usage plans and API keys for third-party developer access control
- ✅ Caching to reduce backend load and improve performance

📖 **Documentation**: [API Gateway Developer Guide](https://docs.aws.amazon.com/apigateway/)

---

### ➕ **Elastic Load Balancing Advanced Features**

**ALB Advanced Routing**:
- **Host-based**: Route based on Host header (api.example.com, www.example.com)
- **Path-based**: Route based on URL path (/api/*, /images/*)
- **HTTP Header**: Route based on custom headers
- **HTTP Method**: Route based on HTTP method (GET, POST)
- **Query String**: Route based on query parameters
- **Source IP**: Route based on client IP address

**NLB Advanced Features**:
- **Preserve Source IP**: Maintain original client IP address
- **Static IP**: Fixed IP addresses for whitelisting
- **PrivateLink**: VPC endpoint service integration
- **Cross-Zone Load Balancing**: Distribute evenly across AZs

**Target Types**:
- **Instance**: Route to EC2 instance IDs
- **IP**: Route to specific IP addresses (on-premises, containers)
- **Lambda**: Route to Lambda functions (ALB only)

📖 **Documentation**: [Application Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/application/) | [Network Load Balancer](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/)

---

## 4. 🗃️ Database Services

### 🔥 **Amazon RDS** (Relational Database Service)

**Supported Engines**:
- **MySQL**: Popular open-source, web applications
- **PostgreSQL**: Advanced features, JSON support, enterprise
- **MariaDB**: MySQL-compatible, enhanced performance
- **Oracle**: Enterprise database, bring-your-own-license (BYOL)
- **SQL Server**: Microsoft database, various editions
- **Aurora**: AWS-native, MySQL/PostgreSQL compatible

**High Availability & Scaling**:
- **Multi-AZ Deployments**: Synchronous replication, automatic failover (1-2 minutes)
- **Read Replicas**: Asynchronous replication, read scaling (up to 15 replicas)
- **Cross-Region Read Replicas**: Disaster recovery, local reads
- **Aurora Auto Scaling**: Automatic read replica scaling based on metrics

**Backup & Recovery**:
- **Automated Backups**: Point-in-time recovery (1-35 days), transaction logs
- **Manual Snapshots**: User-initiated, retained until manually deleted
- **Cross-Region Snapshots**: Disaster recovery, compliance
- **Snapshot Sharing**: Share encrypted snapshots across accounts

**Performance Optimization**:
- **Performance Insights**: Database performance monitoring and tuning
- **Parameter Groups**: Database configuration management
- **Option Groups**: Additional database features (Oracle/SQL Server)
- **Enhanced Monitoring**: OS-level metrics collection

**Security Features**:
- **Encryption**: At rest (KMS) and in transit (SSL/TLS)
- **Network Isolation**: VPC deployment, security groups
- **IAM Authentication**: Database authentication using IAM
- **Database Activity Streams**: Real-time monitoring of database activity

**Key Exam Points**:
- ✅ Multi-AZ for high availability, Read Replicas for read scaling
- ✅ Automated backups vs manual snapshots for different retention needs
- ✅ Aurora for cloud-native applications requiring high performance
- ✅ Cross-region read replicas for disaster recovery strategies

📖 **Documentation**: [RDS User Guide](https://docs.aws.amazon.com/rds/) | [Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/) | [RDS Performance Insights](https://docs.aws.amazon.com/AmazonRDS/latest/UserGuide/USER_PerfInsights.html)

---

### 🔥 **Amazon Aurora** (Cloud-Native Relational Database)

**Architecture**:
- **Storage**: Distributed, auto-scaling (10GB - 128TB), 6 copies across 3 AZs
- **Compute**: Separate from storage, fast failover (<30 seconds)
- **Endpoints**: Writer, reader, custom endpoints for different workloads
- **Aurora Serverless**: On-demand, auto-scaling compute capacity

**Performance Features**:
- **Performance**: 5x faster than MySQL, 3x faster than PostgreSQL
- **Parallel Query**: Parallel processing for analytical queries (MySQL)
- **Backtrack**: Rewind database to specific point in time (MySQL)
- **Fast Cloning**: Copy-on-write cloning for development/testing

**Global Features**:
- **Aurora Global Database**: Cross-region replication (<1 second lag)
- **Global Write Forwarding**: Write to any region, forwarded to primary
- **Aurora Multi-Master**: Multiple write nodes (MySQL only)

**Machine Learning**:
- **Aurora ML**: Native integration with SageMaker and Comprehend
- **Predictive Scaling**: ML-powered capacity planning

**Key Exam Points**:
- ✅ Aurora for applications requiring highest performance and availability
- ✅ Aurora Serverless for variable workloads and cost optimization
- ✅ Aurora Global Database for global applications with disaster recovery
- ✅ Fast cloning for development environments without storage duplication

📖 **Documentation**: [Aurora User Guide](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/) | [Aurora Serverless](https://docs.aws.amazon.com/AmazonRDS/latest/AuroraUserGuide/aurora-serverless.html)

---

### 🔥 **Amazon DynamoDB** (NoSQL Database)

**Data Model**:
- **Tables**: Schema-less collections of items
- **Primary Key**: Partition Key (required) + Sort Key (optional)
- **Attributes**: Name-value pairs, flexible data types
- **Item Size**: Maximum 400 KB per item

**Capacity Modes**:
- **On-Demand**: Pay per request, automatic scaling, unpredictable workloads
- **Provisioned**: Fixed capacity, predictable workloads, auto-scaling available
- **Reserved Capacity**: Cost savings for predictable workloads

**Indexes**:
- **Global Secondary Index (GSI)**: Different partition/sort key, eventually consistent
- **Local Secondary Index (LSI)**: Same partition key, different sort key, strongly consistent
- **Sparse Indexes**: Only items with index attributes are included

**Advanced Features**:
- **DynamoDB Streams**: Capture data modification events, Lambda triggers
- **Global Tables**: Multi-region, multi-master replication
- **Point-in-Time Recovery (PITR)**: Continuous backups, restore to any second in last 35 days
- **On-Demand Backup**: Manual snapshots, long-term retention

**Performance & Caching**:
- **DAX (DynamoDB Accelerator)**: In-memory cache, microsecond latency
- **Adaptive Capacity**: Isolate frequently accessed partitions
- **Burst Capacity**: Handle occasional spikes in traffic
- **Auto Scaling**: Automatically adjust provisioned capacity

**Security**:
- **Encryption**: At rest and in transit by default
- **Fine-Grained Access Control**: Item and attribute-level permissions
- **VPC Endpoints**: Private access from VPC
- **AWS Backup**: Centralized backup across AWS services

**Key Exam Points**:
- ✅ Choose partition key for even distribution of data and requests
- ✅ GSI for queries on non-key attributes, LSI for different sort order
- ✅ DAX for read-heavy applications requiring microsecond latency
- ✅ DynamoDB Streams for real-time processing of data changes
- ✅ Global Tables for global applications with local read/write access

📖 **Documentation**: [DynamoDB Developer Guide](https://docs.aws.amazon.com/dynamodb/) | [DynamoDB Best Practices](https://docs.aws.amazon.com/dynamodb/latest/developerguide/best-practices.html) | [DAX Developer Guide](https://docs.aws.amazon.com/amazondynamodb/latest/developerguide/DAX.html)

---

### ⭐ **ElastiCache** (In-Memory Caching)

**Engine Comparison**:
| Feature | Redis | Memcached |
|---------|-------|-----------|
| **Data Types** | Strings, Lists, Sets, Hashes, etc. | Simple key-value strings |
| **Persistence** | Backup/restore, snapshots | No persistence |
| **Replication** | Master-slave, cluster mode | No replication |
| **Multi-threading** | Single-threaded | Multi-threaded |
| **Partitioning** | Hash slots, cluster mode | Client-side |
| **Lua Scripts** | Supported | Not supported |
| **Pub/Sub** | Supported | Not supported |

**Redis Features**:
- **Cluster Mode**: Automatic partitioning across multiple nodes
- **Replication Groups**: Primary node with read replicas
- **Backup/Restore**: Automatic and manual snapshots
- **Auth**: Redis AUTH command, encryption in transit/at rest
- **Multi-AZ**: Automatic failover with replica promotion

**Use Cases**:
- **Database Caching**: Reduce database load, improve response times
- **Session Store**: Shared session data across application servers
- **Gaming Leaderboards**: Sorted sets for real-time rankings
- **Real-time Analytics**: In-memory data processing
- **Message Queues**: Pub/sub messaging patterns (Redis)

**Performance Optimization**:
- **Node Types**: Memory-optimized instances (R6g, R5, R4)
- **Reserved Nodes**: Cost savings for predictable workloads
- **CloudWatch Metrics**: Monitor CPU, memory, connections, cache hits

**Key Exam Points**:
- ✅ Redis for complex data structures and persistence requirements
- ✅ Memcached for simple caching with multi-threading
- ✅ Cluster mode for horizontal scaling and partitioning
- ✅ Multi-AZ for high availability and automatic failover

📖 **Documentation**: [ElastiCache User Guide](https://docs.aws.amazon.com/elasticache/) | [Redis User Guide](https://docs.aws.amazon.com/elasticache/latest/red-ug/) | [Memcached User Guide](https://docs.aws.amazon.com/elasticache/latest/mem-ug/)

---

### ⭐ **Amazon Redshift** (Data Warehouse)

**Architecture**:
- **Leader Node**: Query planning, result aggregation
- **Compute Nodes**: Data storage and processing
- **Node Types**: RA3 (managed storage), DC2 (SSD storage)
- **Columnar Storage**: Optimized for analytical workloads

**Performance Features**:
- **Massively Parallel Processing (MPP)**: Parallel query execution
- **Compression**: Automatic compression reduces storage costs
- **Distribution Styles**: EVEN, KEY, ALL for data distribution
- **Sort Keys**: Improve query performance for filtered/sorted data
- **Zone Maps**: Skip unnecessary data blocks during scans

**Data Loading**:
- **COPY Command**: Bulk data loading from S3, DynamoDB, EMR
- **Redshift Spectrum**: Query S3 data without loading into Redshift
- **AWS Glue**: ETL service for data preparation
- **Data Pipeline**: Orchestrate data workflows

**Scaling & Availability**:
- **Elastic Resize**: Add/remove nodes in minutes
- **Concurrency Scaling**: Additional clusters for concurrent queries
- **Multi-AZ**: Available in select regions
- **Cross-Region Snapshots**: Disaster recovery

**Key Exam Points**:
- ✅ Redshift for OLAP workloads and business intelligence
- ✅ Redshift Spectrum for querying data lake without loading
- ✅ Columnar storage and compression for analytical performance
- ✅ COPY command for efficient bulk data loading from S3

📖 **Documentation**: [Redshift Database Developer Guide](https://docs.aws.amazon.com/redshift/) | [Redshift Spectrum](https://docs.aws.amazon.com/redshift/latest/dg/c-using-spectrum.html)

---

### ➕ **Database Migration Service (DMS)**

**Migration Types**:
- **Homogeneous**: Same database engine (Oracle to Oracle)
- **Heterogeneous**: Different engines (Oracle to PostgreSQL)
- **One-time**: Full load migration
- **Continuous**: Ongoing replication (CDC - Change Data Capture)

**Schema Conversion Tool (SCT)**:
- **Convert Schema**: Database objects, stored procedures, functions
- **Assessment Report**: Compatibility analysis and conversion effort
- **Code Conversion**: Application code that interacts with database

**Supported Sources/Targets**:
- **Sources**: On-premises, EC2, RDS, S3, Azure SQL, Google Cloud SQL
- **Targets**: RDS, Aurora, Redshift, DynamoDB, ElastiCache, Kinesis, S3

📖 **Documentation**: [DMS User Guide](https://docs.aws.amazon.com/dms/) | [Schema Conversion Tool](https://docs.aws.amazon.com/SchemaConversionTool/)

---

### 💡 **Other Database Services**

**Amazon DocumentDB** (MongoDB-compatible):
- **Use Cases**: Content management, catalogs, user profiles
- **Features**: JSON document storage, MongoDB API compatibility
- **Scaling**: Compute and storage scale independently

**Amazon Neptune** (Graph Database):
- **Use Cases**: Social networks, recommendation engines, fraud detection
- **Query Languages**: Gremlin (Apache TinkerPop), SPARQL (RDF)
- **Performance**: Optimized for graph traversals

**Amazon Keyspaces** (Cassandra-compatible):
- **Use Cases**: Time-series data, IoT applications, real-time personalization
- **Features**: Serverless, CQL (Cassandra Query Language) API
- **Scaling**: Automatic scaling based on traffic

**Amazon Timestream** (Time-series Database):
- **Use Cases**: IoT sensor data, application monitoring, industrial telemetry
- **Features**: Built-in analytics, automatic data lifecycle management
- **Performance**: Optimized for time-series data patterns

📖 **Documentation**: [DocumentDB Developer Guide](https://docs.aws.amazon.com/documentdb/) | [Neptune User Guide](https://docs.aws.amazon.com/neptune/) | [Keyspaces Developer Guide](https://docs.aws.amazon.com/keyspaces/) | [Timestream Developer Guide](https://docs.aws.amazon.com/timestream/)

---

## 5. 🔄 Application Integration & Messaging

### 🔥 **Amazon SQS** (Simple Queue Service)

**Queue Types**:
- **Standard Queues**: At-least-once delivery, best-effort ordering, unlimited throughput
- **FIFO Queues**: Exactly-once processing, strict ordering, up to 300 TPS (3,000 with batching)

**Core Features**:
- **Message Retention**: 1 minute to 14 days (default 4 days)
- **Message Size**: Up to 256 KB, larger messages via S3 (SQS Extended Client Library)
- **Visibility Timeout**: Hide message during processing (0 seconds to 12 hours)
- **Receive Message Wait Time**: Long polling (0-20 seconds) vs short polling

**Advanced Features**:
- **Dead Letter Queues (DLQ)**: Handle failed message processing
- **Message Attributes**: Metadata for filtering and routing
- **Delay Queues**: Postpone message delivery (0-15 minutes)
- **Content-Based Deduplication**: FIFO queues, automatic deduplication based on message body
- **Message Groups**: FIFO queues, preserve ordering within groups

**Integration Patterns**:
- **Decoupling**: Microservices communication
- **Load Leveling**: Buffer between components with different processing rates
- **Fan-out**: Combine with SNS for multiple consumers
- **Batch Processing**: Accumulate messages for efficient processing

**Key Exam Points**:
- ✅ Standard queues for high throughput, FIFO for ordering requirements
- ✅ Dead letter queues for handling message processing failures
- ✅ Long polling to reduce costs and improve message delivery efficiency
- ✅ Visibility timeout configuration based on processing time requirements
- ✅ Message deduplication for exactly-once processing in FIFO queues

📖 **Documentation**: [SQS Developer Guide](https://docs.aws.amazon.com/sqs/) | [SQS Best Practices](https://docs.aws.amazon.com/sqs/latest/dg/sqs-best-practices.html)

---

### 🔥 **Amazon SNS** (Simple Notification Service)

**Core Features**:
- **Topics**: Communication channels for pub/sub messaging
- **Subscriptions**: Endpoints that receive topic messages
- **Message Attributes**: Key-value pairs for filtering and routing
- **Message Filtering**: Subscribe to subset of messages based on attributes

**Supported Protocols**:
- **HTTP/HTTPS**: Webhooks, API endpoints
- **Email/Email-JSON**: Direct email delivery
- **SMS**: Text messages to phone numbers
- **SQS**: Queue integration for reliable delivery
- **Lambda**: Direct function invocation
- **Application**: Mobile push notifications (iOS, Android, Fire OS)
- **Platform Endpoints**: Device-specific push notifications

**Advanced Features**:
- **FIFO Topics**: Strict message ordering and exactly-once delivery
- **Message Deduplication**: Prevent duplicate messages in FIFO topics
- **Delivery Status Logging**: CloudWatch Logs integration
- **Large Message Payloads**: Store large messages in S3, send reference via SNS
- **Cross-Region Delivery**: Subscribe endpoints in different regions

**Fan-out Pattern**:
- **SNS + SQS**: Reliable, scalable message distribution
- **Multiple Subscribers**: Each gets copy of message
- **Decoupled Processing**: Independent processing by different services

**Key Exam Points**:
- ✅ Pub/sub pattern for broadcasting messages to multiple subscribers
- ✅ Message filtering to deliver relevant messages to specific subscribers
- ✅ SNS+SQS fan-out pattern for reliable message distribution
- ✅ FIFO topics when strict ordering is required across subscribers
- ✅ Cross-region subscriptions for global applications

📖 **Documentation**: [SNS Developer Guide](https://docs.aws.amazon.com/sns/) | [Message Filtering](https://docs.aws.amazon.com/sns/latest/dg/sns-message-filtering.html)

---

### ⭐ **Amazon EventBridge** (Event-Driven Architecture)

**Core Components**:
- **Event Buses**: Custom event buses for different applications/teams
- **Rules**: Route events based on event patterns
- **Targets**: Destinations for matched events (Lambda, SQS, SNS, etc.)
- **Event Patterns**: JSON-based filtering of events

**Event Sources**:
- **AWS Services**: 90+ AWS services publish events
- **Custom Applications**: Custom events via PutEvents API
- **SaaS Partners**: Direct integration with third-party services
- **EventBridge Pipes**: Point-to-point integration between sources and targets

**Advanced Features**:
- **Schema Registry**: Centralized event schema management
- **Event Replay**: Replay historical events for debugging/recovery
- **Archive**: Long-term storage of events for compliance
- **Cross-Account Events**: Share events across AWS accounts
- **Global Endpoints**: Multi-region event replication

**Integration Capabilities**:
- **API Destinations**: HTTP endpoints as targets
- **Dead Letter Queues**: Handle failed event delivery
- **Retry Policies**: Configurable retry behavior
- **Input Transformers**: Modify event data before delivery

**Key Exam Points**:
- ✅ Event-driven architectures with loose coupling between services
- ✅ Custom event buses for multi-tenant applications
- ✅ Schema registry for event contract management
- ✅ Cross-account event sharing for organization-wide integration
- ✅ API destinations for integrating with external systems

📖 **Documentation**: [EventBridge User Guide](https://docs.aws.amazon.com/eventbridge/) | [EventBridge Patterns](https://docs.aws.amazon.com/eventbridge/latest/userguide/eb-event-patterns.html)

---

### ⭐ **AWS Step Functions** (Workflow Orchestration)

**State Machine Types**:
- **Standard Workflows**: Long-running (up to 1 year), exactly-once execution
- **Express Workflows**: Short-duration (<5 minutes), high-volume, at-least-once execution
  - **Synchronous**: Wait for completion, return result
  - **Asynchronous**: Don't wait for completion, fire-and-forget

**State Types**:
- **Task**: Execute work using Lambda, ECS, SNS, SQS, etc.
- **Choice**: Branch based on conditions
- **Wait**: Delay execution for specified time
- **Succeed/Fail**: Terminal states
- **Pass**: Transform input/output or add fixed data
- **Map**: Process array of items in parallel
- **Parallel**: Execute branches in parallel

**Integration Patterns**:
- **Request-Response**: Synchronous execution (default)
- **Run Job (.sync)**: Wait for job completion (Batch, ECS, Glue)
- **Wait for Callback (.waitForCallback)**: Wait for external task completion

**Error Handling**:
- **Retry**: Automatic retry with exponential backoff
- **Catch**: Handle specific error types
- **Timeouts**: Prevent infinite execution
- **Dead Letter Queues**: Handle failed executions

**Monitoring & Observability**:
- **CloudWatch**: Execution metrics and logs
- **X-Ray**: Distributed tracing integration
- **EventBridge**: State change events
- **CloudTrail**: API call logging

**Key Exam Points**:
- ✅ Coordinate distributed applications and microservices
- ✅ Visual workflow editor for complex business logic
- ✅ Built-in error handling and retry mechanisms
- ✅ Integration with 200+ AWS services via optimized connectors
- ✅ Express workflows for high-volume, short-duration processes

📖 **Documentation**: [Step Functions Developer Guide](https://docs.aws.amazon.com/step-functions/) | [AWS Service Integrations](https://docs.aws.amazon.com/step-functions/latest/dg/concepts-service-integrations.html)

---

### ➕ **Amazon Kinesis** (Real-time Data Streaming)

**Service Types**:
- **Kinesis Data Streams**: Real-time data streaming, custom applications
- **Kinesis Data Firehose**: Load streaming data to destinations (S3, Redshift, etc.)
- **Kinesis Analytics**: SQL queries on streaming data
- **Kinesis Video Streams**: Video streaming from connected devices

**Data Streams Features**:
- **Shards**: Units of capacity, 1MB/sec or 1,000 records/sec per shard
- **Retention**: 1-365 days (default 24 hours)
- **Partition Key**: Determines which shard receives the record
- **Sequence Number**: Unique identifier within shard

**Firehose Features**:
- **Delivery**: Near real-time (60 seconds minimum)
- **Transformation**: Lambda functions for data processing
- **Compression**: GZIP, ZIP, SNAPPY for S3 delivery
- **Error Handling**: Failed records to separate S3 bucket

**Key Exam Points**:
- ✅ Real-time analytics on streaming data
- ✅ Kinesis Data Streams for custom processing applications
- ✅ Kinesis Data Firehose for managed delivery to data stores
- ✅ Shard scaling based on throughput requirements

📖 **Documentation**: [Kinesis Developer Guide](https://docs.aws.amazon.com/kinesis/)

---

### 💡 **Amazon MQ** (Managed Message Broker)

**Supported Brokers**:
- **Apache ActiveMQ**: JMS API, traditional enterprise messaging
- **RabbitMQ**: AMQP protocol, flexible routing, clustering

**Use Cases**:
- **Migration**: Lift-and-shift from on-premises message brokers
- **Enterprise Integration**: Existing applications using JMS/AMQP
- **Hybrid Architectures**: Bridge between cloud and on-premises

**vs SQS/SNS**: MQ for compatibility, SQS/SNS for cloud-native applications

📖 **Documentation**: [Amazon MQ User Guide](https://docs.aws.amazon.com/amazon-mq/)

---

## 6. 🔐 Security, Identity & Compliance

### 🔥 **AWS IAM** (Identity and Access Management)

**Core Components**:
- **Users**: Individual identities, long-term credentials, access keys/passwords
- **Groups**: Collections of users, simplified permission management
- **Roles**: Temporary credentials, assumed by users/services/applications
- **Policies**: JSON documents defining permissions (identity-based vs resource-based)

**Policy Types**:
- **AWS Managed**: Created and maintained by AWS (PowerUserAccess, ReadOnlyAccess)
- **Customer Managed**: Custom policies created by customers
- **Inline Policies**: Directly attached to single user/group/role

**Advanced Features**:
- **Policy Conditions**: Context-based access control (IP, MFA, time, etc.)
- **Resource-based Policies**: Attached to resources (S3 bucket policies, Lambda resource policies)
- **Permission Boundaries**: Maximum permissions for IAM entities
- **Service-Linked Roles**: Predefined roles for AWS services
- **Cross-Account Access**: AssumeRole for accessing resources in other accounts

**AWS STS (Security Token Service)**:
- **Temporary Credentials**: Short-term access (15 minutes to 12 hours)
- **AssumeRole**: Cross-account access, role switching
- **GetSessionToken**: MFA-protected API calls
- **GetFederationToken**: Federated user access

**Best Practices**:
- **Least Privilege**: Grant minimum required permissions
- **MFA**: Multi-factor authentication for sensitive operations
- **Access Keys Rotation**: Regular key rotation, avoid embedding in code
- **IAM Access Analyzer**: Analyze resource policies for unintended access
- **CloudTrail Integration**: Monitor IAM API calls

**Policy Evaluation Logic**:
1. **Explicit Deny**: Always takes precedence
2. **Explicit Allow**: Required for access
3. **Default Deny**: No explicit allow results in deny

**Key Exam Points**:
- ✅ Roles for applications and services, users for human identities
- ✅ Policy conditions for context-based access control
- ✅ Cross-account access patterns using roles and external IDs
- ✅ Permission boundaries to delegate permission management
- ✅ Service-linked roles for AWS service integration

📖 **Documentation**: [IAM User Guide](https://docs.aws.amazon.com/iam/) | [IAM Best Practices](https://docs.aws.amazon.com/iam/latest/userguide/best-practices.html) | [Policy Evaluation Logic](https://docs.aws.amazon.com/iam/latest/userguide/reference_policies_evaluation-logic.html)

---

### 🔥 **AWS KMS** (Key Management Service)

**Key Types**:
- **Customer Managed Keys (CMK)**: Full control, key policies, rotation
- **AWS Managed Keys**: Created by AWS services, limited customer control
- **AWS Owned Keys**: Used by AWS services, no customer visibility

**Key Specifications**:
- **Symmetric Keys**: Single key for encrypt/decrypt (default, most common)
- **Asymmetric Keys**: Key pairs for encrypt/decrypt or sign/verify
- **HMAC Keys**: Hash-based message authentication codes

**Key Management**:
- **Key Policies**: Resource-based policies controlling key access
- **Grants**: Temporary, programmatic access delegation
- **Key Rotation**: Automatic annual rotation for customer managed keys
- **Multi-Region Keys**: Replicated keys across regions

**Encryption Context**:
- **Additional Authenticated Data (AAD)**: Non-secret data for encryption context
- **Logging**: CloudTrail logs show encryption context
- **Access Control**: Policies can require specific encryption context

**Integration with AWS Services**:
- **S3**: Server-side encryption with KMS keys (SSE-KMS)
- **EBS**: Volume encryption using KMS keys
- **RDS**: Database encryption at rest
- **Lambda**: Environment variable encryption
- **Parameter Store**: Secure parameter encryption

**Key Exam Points**:
- ✅ Customer managed keys for full control and compliance requirements
- ✅ Key policies control access to keys, separate from IAM policies
- ✅ Encryption context for additional security and audit trails
- ✅ Multi-region keys for global applications with local encryption
- ✅ Automatic key rotation for security best practices

📖 **Documentation**: [KMS Developer Guide](https://docs.aws.amazon.com/kms/) | [KMS Best Practices](https://docs.aws.amazon.com/kms/latest/developerguide/best-practices.html)

---

### ⭐ **AWS Secrets Manager vs Systems Manager Parameter Store**

| Feature | Secrets Manager | Parameter Store (SSM) |
|---------|----------------|----------------------|
| **Cost** | $0.40/secret/month + API calls | Free tier (10,000 params), $0.05/10,000 advanced |
| **Automatic Rotation** | Built-in rotation for RDS, Redshift, DocumentDB | Manual rotation only |
| **Value Size** | Up to 64 KB | Standard: 4 KB, Advanced: 8 KB |
| **Hierarchical Storage** | No | Yes (/app/db/username) |
| **Cross-Region Replication** | Yes | Manual cross-region access |
| **Fine-grained Access Control** | Resource policies | IAM policies only |
| **Versioning** | Automatic | Manual (advanced parameters) |
| **Integration** | Native AWS service integration | Broader integration options |

**Secrets Manager Use Cases**:
- **Database Credentials**: Automatic rotation with RDS integration
- **API Keys**: Third-party service credentials
- **Sensitive Configuration**: Application secrets requiring rotation
- **Cross-Region Secrets**: Replicated secrets for disaster recovery

**Parameter Store Use Cases**:
- **Configuration Management**: Application settings, feature flags
- **Hierarchical Organization**: Environment-specific parameters
- **Cost-Sensitive**: Large number of parameters with budget constraints
- **Integration Flexibility**: EC2, Lambda, ECS, CodeBuild integration

**Key Exam Points**:
- ✅ Secrets Manager for automatic rotation of database credentials
- ✅ Parameter Store for configuration management and cost optimization
- ✅ Hierarchical parameter organization for environment separation
- ✅ SecureString parameters with KMS encryption for sensitive data
- ✅ Cross-region replication strategy for disaster recovery

📖 **Documentation**: [Secrets Manager User Guide](https://docs.aws.amazon.com/secretsmanager/) | [Parameter Store User Guide](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)

---

### ⭐ **Amazon Cognito** (User Identity and Access Management)

**Service Components**:
- **User Pools**: User directory, authentication, user management
- **Identity Pools (Federated Identities)**: AWS credential provision for federated users

**User Pools Features**:
- **Authentication**: Sign-up, sign-in, password reset, MFA
- **User Attributes**: Standard (email, phone) and custom attributes
- **Groups**: Organize users, assign IAM roles to groups
- **Lambda Triggers**: Customize authentication flow with Lambda functions
- **Hosted UI**: Pre-built authentication pages
- **Social Identity Providers**: Facebook, Google, Apple, Amazon, SAML, OIDC

**Identity Pools Features**:
- **Temporary AWS Credentials**: STS tokens for AWS resource access
- **Authenticated vs Unauthenticated**: Different IAM roles for different user types
- **Identity Providers**: Cognito User Pools, SAML, OIDC, social providers
- **Role Mapping**: Map federated identities to IAM roles

**Advanced Features**:
- **Advanced Security**: Risk-based authentication, device tracking, geolocation
- **App Clients**: Different authentication flows for web/mobile applications
- **Custom Domains**: Branded authentication pages
- **Analytics**: User behavior and authentication metrics

**Integration Patterns**:
- **Web Applications**: User Pools + Identity Pools for complete solution
- **Mobile Applications**: SDK integration with offline sync
- **API Gateway**: Cognito User Pools as authorizer
- **ALB**: Native Cognito integration for authentication

**Key Exam Points**:
- ✅ User Pools for user authentication and management
- ✅ Identity Pools for providing AWS credentials to federated users
- ✅ Social identity providers for external authentication integration
- ✅ Lambda triggers for customizing authentication workflows
- ✅ Integration with API Gateway and ALB for web application authentication

📖 **Documentation**: [Cognito Developer Guide](https://docs.aws.amazon.com/cognito/) | [User Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-user-identity-pools.html) | [Identity Pools](https://docs.aws.amazon.com/cognito/latest/developerguide/cognito-identity.html)

---

### ⭐ **AWS WAF & Shield** (Web Application Security)

**AWS WAF (Web Application Firewall)**:
- **Rule Actions**: Allow, Block, Count (monitoring)
- **Rule Conditions**: IP addresses, HTTP headers, HTTP body, URI strings, SQL injection, XSS
- **Web ACLs**: Collections of rules applied to CloudFront, ALB, API Gateway, AppSync
- **Managed Rules**: AWS and AWS Marketplace pre-configured rule sets
- **Rate-Based Rules**: Block IPs exceeding request rate limits

**AWS Shield**:
- **Shield Standard**: Free DDoS protection for all AWS customers
- **Shield Advanced**: $3,000/month, enhanced protection, 24/7 DRP support, cost protection

**Integration Points**:
- **CloudFront**: Global edge protection
- **Application Load Balancer**: Regional application protection
- **API Gateway**: API endpoint protection
- **AWS Global Accelerator**: Enhanced DDoS protection

**Key Exam Points**:
- ✅ WAF for application-layer protection against common attacks
- ✅ Shield Advanced for enhanced DDoS protection and financial guarantees
- ✅ Managed rules for quick deployment of security protections
- ✅ Rate-based rules for preventing abuse and API rate limiting

📖 **Documentation**: [WAF Developer Guide](https://docs.aws.amazon.com/waf/) | [Shield Advanced Guide](https://docs.aws.amazon.com/waf/latest/developerguide/shield-advanced.html)

---

### ➕ **Additional Security Services**

**AWS Certificate Manager (ACM)**:
- **SSL/TLS Certificates**: Free certificates for AWS services
- **Automatic Renewal**: Managed certificate lifecycle
- **Integration**: CloudFront, ELB, API Gateway, CloudFormation

**Amazon GuardDuty** (Threat Detection):
- **Machine Learning**: Behavioral analysis for threat detection
- **Data Sources**: VPC Flow Logs, DNS logs, CloudTrail events
- **Threat Intelligence**: AWS security intelligence and third-party feeds
- **Integration**: Security Hub, EventBridge for automated response

**AWS Inspector** (Vulnerability Assessment):
- **EC2 Assessment**: Operating system and application vulnerabilities
- **Container Assessment**: ECR image scanning
- **Lambda Assessment**: Function code and dependencies
- **Findings**: Common vulnerabilities and exposures (CVEs)

**AWS Security Hub** (Security Posture Management):
- **Centralized Dashboard**: Multi-account security findings
- **Compliance Standards**: CIS, PCI DSS, AWS Foundational Security Standard
- **Integration**: 40+ AWS and partner security services
- **Custom Insights**: Queries for specific security concerns

📖 **Documentation**: [ACM User Guide](https://docs.aws.amazon.com/acm/) | [GuardDuty User Guide](https://docs.aws.amazon.com/guardduty/) | [Inspector User Guide](https://docs.aws.amazon.com/inspector/) | [Security Hub User Guide](https://docs.aws.amazon.com/securityhub/)

---

## 7. 📊 Monitoring, Logging & Management

### 🔥 **Amazon CloudWatch** (Monitoring and Observability)

**Core Components**:
- **Metrics**: Numerical data points over time (CPU utilization, request count)
- **Logs**: Text-based log data from applications and AWS services
- **Alarms**: Automated actions based on metric thresholds
- **Dashboards**: Visual representation of metrics and logs
- **Events (EventBridge)**: Respond to state changes in AWS resources

**Metrics Features**:
- **Standard Metrics**: AWS services provide default metrics (5-minute intervals)
- **Detailed Monitoring**: 1-minute intervals for EC2 (additional cost)
- **Custom Metrics**: Application-specific metrics via API/SDK
- **High-Resolution Metrics**: Up to 1-second intervals
- **Metric Filters**: Extract metrics from log data

**Logs Features**:
- **Log Groups**: Containers for log streams with retention settings
- **Log Streams**: Sequence of log events from single source
- **CloudWatch Insights**: SQL-like queries for log analysis
- **Log Retention**: 1 day to 10 years, indefinite retention
- **Real-time Processing**: Kinesis Data Streams/Firehose integration

**Alarms and Actions**:
- **Alarm States**: OK, ALARM, INSUFFICIENT_DATA
- **Alarm Actions**: SNS notifications, Auto Scaling actions, EC2 actions, Systems Manager actions
- **Composite Alarms**: Combine multiple alarms with AND/OR logic
- **Anomaly Detection**: Machine learning-based threshold detection

**Advanced Features**:
- **CloudWatch Agent**: Enhanced monitoring for EC2 and on-premises
- **Container Insights**: ECS, EKS, Kubernetes monitoring
- **Lambda Insights**: Enhanced Lambda function monitoring
- **Application Insights**: Application performance monitoring
- **Synthetics**: Monitor application endpoints with canaries

**Key Exam Points**:
- ✅ Custom metrics for application-specific monitoring requirements
- ✅ CloudWatch Logs Insights for complex log analysis and troubleshooting
- ✅ Composite alarms for sophisticated alerting scenarios
- ✅ CloudWatch Agent for detailed system-level monitoring
- ✅ Cross-account log sharing for centralized logging strategies

📖 **Documentation**: [CloudWatch User Guide](https://docs.aws.amazon.com/cloudwatch/) | [CloudWatch Logs](https://docs.aws.amazon.com/cloudwatch/latest/logs/) | [CloudWatch Agent](https://docs.aws.amazon.com/cloudwatch/latest/monitoring/Install-CloudWatch-Agent.html)

---

### 🔥 **AWS CloudTrail** (API Auditing and Compliance)

**Core Features**:
- **API Call Logging**: Record all API calls across AWS services
- **Event History**: 90-day history available in console (free)
- **Management Events**: Control plane operations (resource creation/deletion)
- **Data Events**: Data plane operations (S3 object access, Lambda function execution)
- **Insight Events**: Unusual activity patterns detected by machine learning

**Trail Configuration**:
- **Single Region**: Events from one region only
- **All Regions**: Events from all current and future regions
- **Organization Trail**: Multi-account logging for AWS Organizations
- **Global Service Events**: IAM, CloudFront, Route 53 events (us-east-1)

**Advanced Features**:
- **Log File Integrity Validation**: Cryptographic verification of log files
- **CloudWatch Logs Integration**: Real-time monitoring and alerting
- **Event Filtering**: Reduce costs by logging specific events only
- **Multi-Region Trail**: Single trail across all regions
- **Cross-Account Log Delivery**: Centralized logging to security account

**Integration and Analysis**:
- **AWS Config**: Compliance monitoring with configuration changes
- **Amazon Athena**: Query CloudTrail logs using SQL
- **Amazon QuickSight**: Visualize API usage patterns
- **Third-party SIEM**: Export to security information and event management systems

**Security Considerations**:
- **S3 Bucket Policies**: Secure CloudTrail log storage
- **KMS Encryption**: Encrypt log files at rest
- **Log File Validation**: Detect tampering attempts
- **Access Logging**: Monitor who accesses CloudTrail logs

**Key Exam Points**:
- ✅ Enable CloudTrail in all regions for comprehensive audit coverage
- ✅ Data events for detailed S3 and Lambda access logging
- ✅ CloudWatch Logs integration for real-time security monitoring
- ✅ Organization trails for multi-account compliance requirements
- ✅ Log file integrity validation for forensic investigations

📖 **Documentation**: [CloudTrail User Guide](https://docs.aws.amazon.com/cloudtrail/) | [CloudTrail Best Practices](https://docs.aws.amazon.com/cloudtrail/latest/userguide/best-practices-security.html)

---

### ⭐ **AWS Config** (Configuration Management and Compliance)

**Core Functions**:
- **Configuration Items (CIs)**: Point-in-time snapshots of resource configurations
- **Configuration Recorder**: Captures resource configuration changes
- **Delivery Channel**: Delivers configuration data to S3 bucket
- **Configuration Timeline**: History of configuration changes over time

**Rules and Compliance**:
- **AWS Managed Rules**: Pre-built rules for common compliance requirements
- **Custom Rules**: Lambda-based rules for organization-specific requirements
- **Compliance Timeline**: Track compliance status changes over time
- **Remediation**: Automatic or manual actions to fix non-compliant resources

**Advanced Features**:
- **Multi-Account, Multi-Region**: Aggregate configuration data across accounts/regions
- **Organization Config**: Centralized management for AWS Organizations
- **Conformance Packs**: Collections of rules and remediation actions
- **Resource Relationships**: Understand dependencies between resources

**Integration Capabilities**:
- **CloudTrail**: Correlate configuration changes with API calls
- **CloudWatch**: Metrics and alarms for compliance monitoring
- **Security Hub**: Centralized security findings management
- **Systems Manager**: Automated remediation actions

**Common Use Cases**:
- **Security Analysis**: Identify security group misconfigurations
- **Change Management**: Track who changed what and when
- **Compliance Reporting**: Demonstrate adherence to standards (CIS, PCI, SOX)
- **Troubleshooting**: Understand resource state at specific points in time

**Key Exam Points**:
- ✅ Enable Config in all regions for comprehensive configuration tracking
- ✅ Use conformance packs for standardized compliance across accounts
- ✅ Remediation configurations for automatic compliance enforcement
- ✅ Multi-account aggregation for organization-wide visibility
- ✅ Integration with Security Hub for centralized compliance dashboard

📖 **Documentation**: [Config Developer Guide](https://docs.aws.amazon.com/config/) | [Config Rules](https://docs.aws.amazon.com/config/latest/developerguide/evaluate-config.html) | [Conformance Packs](https://docs.aws.amazon.com/config/latest/developerguide/conformance-packs.html)

---

### ⭐ **AWS Systems Manager** (Operational Management)

**Core Capabilities**:
- **Session Manager**: Secure shell access without SSH/RDP, bastion hosts, or key pairs
- **Run Command**: Execute commands remotely on managed instances
- **Patch Manager**: Automate OS and application patching
- **State Manager**: Maintain consistent configuration state
- **Parameter Store**: Centralized configuration and secrets management

**Instance Management**:
- **SSM Agent**: Required on instances for Systems Manager functionality
- **Managed Instances**: EC2 instances and on-premises servers
- **Hybrid Environments**: Manage on-premises infrastructure with cloud tools
- **Fleet Manager**: Web-based interface for remote management

**Automation and Operations**:
- **Automation Documents**: Predefined workflows for common tasks
- **Maintenance Windows**: Schedule operational tasks during defined periods
- **OpsCenter**: Centralized operational issue management
- **Explorer**: Operational dashboard with resource grouping

**Application Management**:
- **Application Manager**: Organize resources by application
- **AppConfig**: Feature flag and configuration deployment
- **Distributor**: Package distribution to managed instances

**Key Exam Points**:
- ✅ Session Manager eliminates need for bastion hosts and SSH key management
- ✅ Parameter Store for secure configuration management across environments
- ✅ Patch Manager for automated, compliant patching strategies
- ✅ Hybrid environment management connecting cloud and on-premises
- ✅ Automation documents for repeatable operational procedures

📖 **Documentation**: [Systems Manager User Guide](https://docs.aws.amazon.com/systems-manager/) | [Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) | [Parameter Store](https://docs.aws.amazon.com/systems-manager/latest/userguide/systems-manager-parameter-store.html)

---

### ➕ **AWS Trusted Advisor** (Best Practice Recommendations)

**Check Categories**:
- **Cost Optimization**: Underutilized resources, Reserved Instance recommendations
- **Performance**: Service limits, throughput optimization recommendations
- **Security**: Security group configurations, IAM usage, MFA enablement
- **Fault Tolerance**: Auto Scaling, Multi-AZ deployments, backup configurations
- **Service Limits**: Current usage vs. service limits across AWS services

**Support Plans**:
- **Basic/Developer**: 7 core checks (security groups, service limits, etc.)
- **Business/Enterprise**: Full check suite, API access, CloudWatch integration
- **Enterprise**: Business support case management, infrastructure event management

**Automation and Integration**:
- **Trusted Advisor API**: Programmatic access to check results
- **CloudWatch Events**: Automated responses to check status changes
- **AWS Support API**: Integrate with ticketing and monitoring systems
- **Refresh Frequency**: Business/Enterprise support automatic refresh every 24 hours

**Common Recommendations**:
- **Idle Resources**: EC2 instances with low utilization
- **Storage Optimization**: EBS volumes, S3 lifecycle policies
- **Security Groups**: Overly permissive rules, unused security groups
- **Reserved Instances**: Cost savings opportunities for predictable workloads

**Key Exam Points**:
- ✅ Business/Enterprise support required for full Trusted Advisor features
- ✅ API access enables automated cost optimization workflows
- ✅ Regular review of recommendations drives operational excellence
- ✅ Integration with CloudWatch for proactive monitoring of recommendations

📖 **Documentation**: [Trusted Advisor](https://docs.aws.amazon.com/awssupport/latest/user/trusted-advisor.html) | [Support Plans](https://aws.amazon.com/premiumsupport/plans/)

---

### 💡 **Additional Management Tools**

**AWS Organizations** (Multi-Account Management):
- **Organizational Units (OUs)**: Hierarchical account organization
- **Service Control Policies (SCPs)**: Preventive guardrails across accounts
- **Consolidated Billing**: Centralized payment and cost management
- **Account Factory**: Automated account creation and configuration

**AWS Control Tower** (Multi-Account Governance):
- **Landing Zone**: Pre-configured multi-account environment
- **Guardrails**: Preventive and detective controls
- **Account Factory**: Standardized account provisioning
- **Dashboard**: Compliance and governance overview

**AWS License Manager**:
- **License Tracking**: Monitor software license usage across AWS and on-premises
- **License Rules**: Enforce compliance with licensing agreements
- **Integration**: EC2, Systems Manager, Organizations integration

**Amazon CloudFormation** (Infrastructure as Code):
- **Templates**: JSON/YAML infrastructure definitions
- **Stacks**: Deployed collections of resources
- **Change Sets**: Preview changes before deployment
- **StackSets**: Deploy stacks across multiple accounts and regions

📖 **Documentation**: [Organizations User Guide](https://docs.aws.amazon.com/organizations/) | [Control Tower User Guide](https://docs.aws.amazon.com/controltower/) | [License Manager User Guide](https://docs.aws.amazon.com/license-manager/) | [CloudFormation User Guide](https://docs.aws.amazon.com/cloudformation/)

---

## 8. Deployment & Automation

### ⭐ **CloudFormation**

* Infrastructure as Code (YAML/JSON templates).
* Stacks, change sets, drift detection.
  📖 [CloudFormation Docs](https://docs.aws.amazon.com/cloudformation/)

---

### ➕ **Systems Manager**

* Session Manager (secure shell without SSH).
* Patch Manager, Parameter Store.
  📖 [Systems Manager Docs](https://docs.aws.amazon.com/systems-manager/)

---

# 🔑 Tóm tắt

* **🔥 Bắt buộc nắm vững**: EC2, ELB/ASG, S3, VPC, IAM, RDS, DynamoDB, Route 53, CloudFront, Lambda, SQS/SNS, CloudWatch.
* **⭐ Quan trọng**: ElastiCache, Aurora, EventBridge, Step Functions, KMS, Config, CloudTrail, CloudFormation.
* **➕ Biết qua**: Beanstalk, Glacier, Cognito, Trusted Advisor, Systems Manager.

---

👉 Bạn có muốn mình chuyển checklist này thành **bảng flashcard PDF** (mỗi dịch vụ 1 card) để bạn in ra hoặc học kiểu “flip card” cho dễ nhớ không?
