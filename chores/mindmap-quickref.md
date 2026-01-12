# 🧠 AWS SAA-C03 Mind Map & Quick Reference

## 🗺️ **Service Categories Mind Map**

```
AWS SAA-C03
│
├── 💻 COMPUTE
│   ├── 🔥 EC2 (Instance Types, Pricing, Placement Groups)
│   ├── 🔥 Auto Scaling + ELB (ALB, NLB, Scaling Policies)
│   ├── 🔥 Lambda (Serverless, Event-driven)
│   ├── ⭐ ECS/EKS (Containers, Fargate)
│   └── ➕ Elastic Beanstalk (PaaS)
│
├── 🗄️ STORAGE
│   ├── 🔥 S3 (Storage Classes, Lifecycle, Security)
│   ├── 🔥 EBS (Volume Types, Snapshots, Encryption)
│   ├── ⭐ EFS (Shared File System, Multi-AZ)
│   ├── ⭐ FSx (Windows, Lustre, NetApp, OpenZFS)
│   └── ➕ Storage Gateway (Hybrid)
│
├── 🗃️ DATABASE
│   ├── 🔥 RDS (Multi-AZ, Read Replicas, Engines)
│   ├── 🔥 Aurora (Performance, Global DB, Serverless)
│   ├── 🔥 DynamoDB (NoSQL, GSI/LSI, Streams, DAX)
│   ├── ⭐ ElastiCache (Redis vs Memcached)
│   ├── ⭐ Redshift (Data Warehouse, Spectrum)
│   └── 💡 Specialized (DocumentDB, Neptune, Timestream)
│
├── 🌐 NETWORKING
│   ├── 🔥 VPC (Subnets, NAT, IGW, Peering, Endpoints)
│   ├── 🔥 Route 53 (DNS, Routing Policies, Health Checks)
│   ├── 🔥 CloudFront (CDN, Edge Locations, OAI/OAC)
│   ├── ⭐ API Gateway (REST, HTTP, WebSocket APIs)
│   └── ⭐ Global Accelerator (Anycast IP, Performance)
│
├── 🔄 INTEGRATION
│   ├── 🔥 SQS (Standard, FIFO, DLQ, Polling)
│   ├── 🔥 SNS (Pub/Sub, Topics, Filtering, Fanout)
│   ├── ⭐ EventBridge (Event Bus, Rules, Schema Registry)
│   ├── ⭐ Step Functions (Workflows, State Machines)
│   └── ➕ Kinesis (Streams, Firehose, Analytics)
│
├── 🔐 SECURITY
│   ├── 🔥 IAM (Users, Roles, Policies, STS)
│   ├── ⭐ KMS (Keys, Encryption Context, Rotation)
│   ├── ⭐ Secrets Manager vs Parameter Store
│   ├── ⭐ Cognito (User Pools, Identity Pools)
│   ├── ⭐ WAF & Shield (Web Protection, DDoS)
│   └── ➕ Security Services (GuardDuty, Inspector)
│
├── 📊 MONITORING
│   ├── 🔥 CloudWatch (Metrics, Logs, Alarms, Dashboards)
│   ├── 🔥 CloudTrail (API Auditing, Multi-region)
│   ├── ⭐ Config (Compliance, Rules, Remediation)
│   ├── ⭐ Systems Manager (Session Manager, Parameter Store)
│   └── ➕ Trusted Advisor (Best Practices, Cost)
│
├── 🚀 DEPLOYMENT
│   ├── ⭐ CloudFormation (IaC, Stacks, StackSets)
│   ├── ⭐ CodeDeploy (Blue/Green, Rolling, Canary)
│   └── ➕ Code Services (CodeCommit, CodeBuild, CodePipeline)
│
└── 📈 ANALYTICS
    ├── ⭐ EMR (Hadoop, Spark, Big Data)
    ├── ⭐ Athena (Serverless Query, S3 Data)
    ├── ➕ Glue (ETL, Catalog, DataBrew)
    └── 💡 QuickSight (BI, Visualization)
```

---

## 📋 **Service Decision Matrix**

### **Compute Services Decision Tree**

```
Need Compute? 
├── Serverless? → Lambda (event-driven, <15min)
├── Containers?
│   ├── Managed Kubernetes → EKS
│   ├── Simple Container → ECS
│   └── No Server Management → Fargate
├── Traditional Server?
│   ├── Full Control → EC2
│   └── Simple Deployment → Elastic Beanstalk
└── High Performance Computing → EC2 (Cluster Placement Groups)
```

### **Storage Services Decision Tree**

```
Need Storage?
├── Object Storage?
│   ├── Web/Mobile → S3 (with CloudFront)
│   ├── Backup/Archive → S3 (Glacier classes)
│   └── Data Lake → S3 (with Athena/Glue)
├── Block Storage?
│   ├── High IOPS → EBS io1/io2
│   ├── General Purpose → EBS gp3
│   └── Throughput Optimized → EBS st1
├── File Storage?
│   ├── POSIX Compliant → EFS
│   ├── Windows → FSx for Windows
│   ├── HPC → FSx for Lustre
│   └── Shared across instances → EFS
└── Hybrid Storage → Storage Gateway
```

### **Database Services Decision Tree**

```
Need Database?
├── Relational?
│   ├── AWS Managed → RDS (Multi-AZ, Read Replicas)
│   ├── Cloud Native → Aurora (better performance)
│   └── Data Warehouse → Redshift
├── NoSQL?
│   ├── Key-Value → DynamoDB
│   ├── Document → DocumentDB
│   ├── Graph → Neptune
│   └── Wide Column → Keyspaces
├── Cache?
│   ├── Simple Cache → ElastiCache Memcached
│   ├── Advanced Features → ElastiCache Redis
│   └── DynamoDB Cache → DAX
└── Time Series → Timestream
```

---

## 🎯 **Common Exam Patterns**

### **High Availability Patterns**

| Requirement | Solution | Key Components |
|-------------|----------|----------------|
| **Web App HA** | Multi-AZ + ALB + ASG | ALB, Auto Scaling, Multi-AZ RDS |
| **DNS Failover** | Route 53 Health Checks | Primary/Secondary routing |
| **Database HA** | RDS Multi-AZ | Synchronous replication, auto failover |
| **Cross-Region HA** | Multi-Region + Route 53 | Global infrastructure, latency routing |

### **Cost Optimization Patterns**

| Scenario | Solution | Savings |
|----------|----------|---------|
| **Predictable Workload** | Reserved Instances | Up to 75% |
| **Fault-Tolerant Batch** | Spot Instances | Up to 90% |
| **Variable Workload** | Auto Scaling + On-Demand | Pay for actual usage |
| **Storage Optimization** | S3 Intelligent Tiering | 30-40% on storage |

### **Security Implementation Patterns**

| Security Layer | AWS Services | Best Practice |
|----------------|--------------|---------------|
| **Identity** | IAM, Cognito | Least privilege, MFA |
| **Network** | VPC, Security Groups, NACLs | Defense in depth |
| **Data** | KMS, S3 encryption | Encrypt at rest + transit |
| **Monitoring** | CloudTrail, GuardDuty | Continuous monitoring |

---

## 🔍 **Service Comparison Charts**

### **Load Balancer Comparison**

| Feature | ALB | NLB | CLB |
|---------|-----|-----|-----|
| **OSI Layer** | Layer 7 (HTTP/HTTPS) | Layer 4 (TCP/UDP) | Layer 4 & 7 |
| **Routing** | Path, Host, Header based | IP hash, flow hash | Round robin |
| **Performance** | High | Ultra-high | Medium |
| **Static IP** | No | Yes | No |
| **WebSocket** | Yes | Yes | No |
| **WAF Integration** | Yes | No | No |
| **Use Case** | Web applications | High performance, gaming | Legacy applications |

### **Database Performance Comparison**

| Database | Best For | Performance | Scalability |
|----------|----------|-------------|-------------|
| **Aurora** | Cloud-native apps | 5x MySQL, 3x PostgreSQL | Auto-scaling storage |
| **RDS** | Traditional apps | Standard MySQL/PostgreSQL | Read replicas |
| **DynamoDB** | Web/mobile apps | Single-digit millisecond | Horizontal scaling |
| **ElastiCache** | Caching layer | Microsecond latency | Cluster mode |
| **Redshift** | Analytics/BI | Columnar storage | Massively parallel |

### **Storage Performance Comparison**

| Storage Type | Latency | Throughput | Use Case |
|--------------|---------|------------|----------|
| **EBS gp3** | Low | Up to 1,000 MiB/s | General purpose |
| **EBS io1/io2** | Ultra-low | Up to 4,000 MiB/s | Databases, critical apps |
| **Instance Store** | Ultra-low | Very high | Temporary, cache |
| **EFS** | Low | Up to 10+ GB/s | Shared file access |
| **S3** | Variable | High (parallel) | Object storage, backup |

---

## 📐 **Architecture Decision Framework**

### **Step 1: Understand Requirements**
- **Functional**: What does the system need to do?
- **Non-functional**: Performance, scalability, availability requirements
- **Constraints**: Budget, timeline, compliance, existing systems

### **Step 2: Apply Well-Architected Principles**
- **Security**: Identity, data protection, network security
- **Reliability**: Multi-AZ, backup, disaster recovery
- **Performance**: Right-sizing, caching, CDN
- **Cost**: Reserved instances, storage classes, monitoring
- **Operational Excellence**: Monitoring, automation, documentation

### **Step 3: Select Services**
- **Start with managed services**: Less operational overhead
- **Consider integration**: How services work together
- **Plan for growth**: Scalability and flexibility
- **Design for failure**: Redundancy and fault tolerance

### **Step 4: Validate Design**
- **Review against requirements**: Does it meet all needs?
- **Check constraints**: Budget, compliance, performance
- **Consider alternatives**: Are there simpler/cheaper options?
- **Plan migration**: How to implement incrementally?

---

## 🚨 **Common Exam Traps**

### **Cost Optimization Traps**
- ❌ Choosing Reserved Instances for unpredictable workloads
- ❌ Using On-Demand for steady, predictable workloads
- ❌ Ignoring S3 storage classes for long-term storage
- ❌ Over-provisioning resources "just in case"

### **Security Traps**
- ❌ Public subnets for database servers
- ❌ Overly permissive security group rules (0.0.0.0/0)
- ❌ Using root account for daily operations
- ❌ Storing credentials in code or AMIs

### **Performance Traps**
- ❌ Single AZ deployments for HA requirements
- ❌ Using CLB instead of ALB for new applications
- ❌ Not using caching for read-heavy workloads
- ❌ Wrong EBS volume type for workload requirements

### **Reliability Traps**
- ❌ No backup strategy or disaster recovery plan
- ❌ Single point of failure in architecture
- ❌ Not testing failover procedures
- ❌ Ignoring health checks and monitoring

---

**🎓 Use this mind map to visualize service relationships and make better architecture decisions during the exam!**