# 🃏 AWS SAA-C03 Flashcards

> **Cách sử dụng**: Đọc câu hỏi, suy nghĩ câu trả lời, sau đó xem đáp án bên dưới

---

## 🔥 **CRITICAL Services Flashcards**

### **EC2 - Elastic Compute Cloud**

**Q: Khi nào nên sử dụng Spot Instances?**
<details>
<summary>Đáp án</summary>

- **Workloads có thể bị interrupt**: Batch processing, data analysis, image rendering
- **Flexible start/end times**: Không cần chạy liên tục
- **Cost-sensitive applications**: Tiết kiệm đến 90% chi phí
- **Fault-tolerant systems**: Có khả năng recovery khi instance bị terminate
- **Không phù hợp**: Production databases, web servers cần uptime cao

</details>

**Q: Phân biệt giữa Security Groups và NACLs?**
<details>
<summary>Đáp án</summary>

| Đặc điểm | Security Groups | NACLs |
|----------|----------------|-------|
| **Level** | Instance level | Subnet level |
| **State** | Stateful | Stateless |
| **Rules** | Allow only | Allow + Deny |
| **Rule evaluation** | All rules | Numbered order |
| **Default** | Deny all inbound | Allow all |

</details>

---

### **S3 - Simple Storage Service**

**Q: Khi nào nên sử dụng từng S3 Storage Class?**
<details>
<summary>Đáp án</summary>

- **Standard**: Frequent access, millisecond latency
- **Standard-IA**: Infrequent access (>30 days), retrieval fee
- **One Zone-IA**: Single AZ, 20% cheaper than Standard-IA
- **Glacier Instant Retrieval**: Archive with instant access (90+ days)
- **Glacier Flexible**: 1-12 hours retrieval (archive 90+ days)
- **Glacier Deep Archive**: 12+ hours, cheapest (180+ days)
- **Intelligent Tiering**: Unknown/changing access patterns

</details>

**Q: Pre-signed URLs hoạt động như thế nào?**
<details>
<summary>Đáp án</summary>

- **Mục đích**: Temporary access to private S3 objects
- **Thời gian**: Configurable expiration (15 minutes to 7 days)
- **Quyền hạn**: Inherit permissions of the user who created URL
- **Use cases**: Secure file uploads, downloads, temporary sharing
- **Security**: URL contains signature, cannot be modified

</details>

---

### **VPC - Virtual Private Cloud**

**Q: Làm thế nào để private subnet access Internet?**
<details>
<summary>Đáp án</summary>

**NAT Gateway/Instance**:
- Đặt trong public subnet
- Route table private subnet: 0.0.0.0/0 → NAT Gateway
- Chỉ outbound traffic (no inbound từ Internet)
- NAT Gateway: Managed, high availability, no maintenance
- NAT Instance: Self-managed, cost-effective, can be bastion host

</details>

**Q: VPC Peering vs Transit Gateway?**
<details>
<summary>Đáp án</summary>

| Feature | VPC Peering | Transit Gateway |
|---------|-------------|-----------------|
| **Transitive routing** | No | Yes |
| **Scalability** | N×(N-1)/2 connections | Hub-and-spoke |
| **Cross-region** | Yes | Yes |
| **Bandwidth** | No limits | 50 Gbps per AZ |
| **Cost** | Free (data transfer charges) | Hourly + data processing |
| **Use case** | Simple 1:1 connections | Complex multi-VPC |

</details>

---

### **RDS & Aurora**

**Q: Multi-AZ vs Read Replicas khác gì?**
<details>
<summary>Đáp án</summary>

| Feature | Multi-AZ | Read Replicas |
|---------|----------|---------------|
| **Purpose** | High Availability | Read Scaling |
| **Replication** | Synchronous | Asynchronous |
| **Failover** | Automatic (1-2 min) | Manual promotion |
| **Readable** | Standby not accessible | Yes, read-only |
| **Cross-region** | Same region only | Yes |
| **Number** | 1 standby | Up to 15 replicas |

</details>

**Q: Khi nào chọn Aurora thay vì RDS?**
<details>
<summary>Đáp án</summary>

**Chọn Aurora khi**:
- Need better performance (5x MySQL, 3x PostgreSQL)
- Global applications (Aurora Global Database)
- Serverless workloads (Aurora Serverless)
- Advanced features (Backtrack, Parallel Query, ML integration)
- Cloud-native applications

**Chọn RDS khi**:
- Specific engine versions not in Aurora
- Simple workloads
- Budget constraints
- Oracle/SQL Server requirements

</details>

---

### **DynamoDB**

**Q: Khi nào sử dụng GSI vs LSI?**
<details>
<summary>Đáp án</summary>

| Feature | GSI | LSI |
|---------|-----|-----|
| **Partition Key** | Different | Same as table |
| **Sort Key** | Different | Different |
| **Consistency** | Eventually consistent | Strongly consistent |
| **Creation** | Anytime | Only at table creation |
| **Item collection size** | No limit | 10 GB limit |
| **Capacity** | Separate RCU/WCU | Shares with table |

</details>

**Q: On-Demand vs Provisioned capacity?**
<details>
<summary>Đáp án</summary>

**On-Demand**:
- Unpredictable workloads
- New applications
- Spiky traffic patterns
- Pay per request
- No capacity planning

**Provisioned**:
- Predictable workloads
- Consistent traffic
- Cost optimization with Reserved Capacity
- Auto Scaling available
- Lower cost for steady workloads

</details>

---

## ⭐ **HIGH Priority Flashcards**

### **Lambda**

**Q: Lambda cold starts và cách optimize?**
<details>
<summary>Đáp án</summary>

**Cold Start causes**:
- First invocation
- Scaling up
- Code/configuration changes
- Long idle time

**Optimization strategies**:
- **Provisioned Concurrency**: Pre-warm execution environments
- **Keep connections warm**: Reuse database connections
- **Reduce package size**: Minimize deployment package
- **Use layers**: Share common code/libraries
- **Choose runtime wisely**: Compiled languages faster than interpreted

</details>

### **ELB - Elastic Load Balancing**

**Q: Khi nào chọn ALB vs NLB vs CLB?**
<details>
<summary>Đáp án</summary>

**ALB (Application Load Balancer)**:
- HTTP/HTTPS traffic
- Layer 7 routing (path, host, headers)
- WebSocket support
- Integration with WAF
- Container support

**NLB (Network Load Balancer)**:
- TCP/UDP traffic
- Ultra-high performance
- Static IP addresses
- Preserve source IP
- Extreme low latency

**CLB (Classic Load Balancer)**:
- Legacy applications
- Layer 4 and Layer 7
- Avoid for new deployments

</details>

### **CloudWatch**

**Q: Metrics vs Logs vs Events (EventBridge)?**
<details>
<summary>Đáp án</summary>

**CloudWatch Metrics**:
- Numerical time-series data
- CPU, memory, disk I/O
- Custom application metrics
- Alarms and dashboards

**CloudWatch Logs**:
- Text-based log data
- Application logs, system logs
- Log Insights for querying
- Real-time monitoring

**EventBridge (CloudWatch Events)**:
- Event-driven architecture
- State changes in AWS resources
- Rule-based routing
- Integration with SaaS applications

</details>

---

## 🎯 **Scenario-Based Flashcards**

### **Scenario 1: High Availability Web Application**

**Q: Thiết kế web application 3-tier highly available?**
<details>
<summary>Đáp án</summary>

**Web Tier**:
- ALB across multiple AZs
- Auto Scaling Group with EC2 instances
- CloudFront for global distribution

**Application Tier**:
- Private subnets across multiple AZs
- Auto Scaling Group for app servers
- Application Load Balancer internal

**Database Tier**:
- RDS Multi-AZ for HA
- Read Replicas for read scaling
- ElastiCache for caching

**Additional**:
- Route 53 for DNS with health checks
- S3 for static content
- CloudWatch for monitoring

</details>

### **Scenario 2: Cost Optimization**

**Q: Optimize costs cho predictable workload chạy 24/7?**
<details>
<summary>Đáp án</summary>

**Compute**:
- Reserved Instances (1-3 year terms)
- Savings Plans for flexible usage
- Right-sizing instances

**Storage**:
- S3 Intelligent Tiering
- EBS gp3 thay vì gp2
- Lifecycle policies

**Database**:
- Reserved DB Instances
- Aurora Serverless for variable loads

**Monitoring**:
- AWS Cost Explorer
- Budgets and alerts
- Trusted Advisor recommendations

</details>

### **Scenario 3: Disaster Recovery**

**Q: Thiết kế DR strategy với RTO 4 hours, RPO 1 hour?**
<details>
<summary>Đáp án</summary>

**Warm Standby approach**:
- **Primary**: Full production in us-east-1
- **DR**: Scaled-down version in us-west-2
- **Database**: RDS Cross-Region Read Replica
- **DNS**: Route 53 health check failover
- **Storage**: S3 Cross-Region Replication
- **Recovery**: Scale up DR environment when needed

**Backup strategy**:
- Automated RDS backups
- EBS snapshots every hour
- Application data backup to S3

</details>

---

## 🔐 **Security Flashcards**

### **IAM Best Practices**

**Q: IAM security best practices?**
<details>
<summary>Đáp án</summary>

1. **Least Privilege**: Grant minimum required permissions
2. **Use Roles**: For applications and cross-account access
3. **MFA**: Enable for privileged users
4. **Rotate Keys**: Regular access key rotation
5. **Policy Conditions**: Use conditions for context-based access
6. **No Root**: Avoid using root account for daily tasks
7. **Access Analyzer**: Review resource policies
8. **CloudTrail**: Monitor API calls

</details>

### **Data Encryption**

**Q: Encryption options cho S3, EBS, RDS?**
<details>
<summary>Đáp án</summary>

**S3**:
- SSE-S3: AWS managed keys
- SSE-KMS: Customer managed keys, audit trail
- SSE-C: Customer provided keys
- Client-side: Encrypt before upload

**EBS**:
- KMS encryption at rest
- All data, snapshots, volumes encrypted
- Boot volumes supported

**RDS**:
- KMS encryption at rest
- SSL/TLS in transit
- Transparent Data Encryption (TDE) for Oracle/SQL Server

</details>

---

# 💡 **Quick Reference Cards**

## **Exam Day Reminders**

### **Read Questions Carefully**
- ✅ Identify keywords: "most cost-effective", "highest performance", "most secure"
- ✅ Note constraints: budget, timeline, compliance requirements
- ✅ Consider operational overhead and management complexity

### **Common Distractors**
- ❌ Over-engineered solutions for simple problems
- ❌ On-premises solutions when cloud-native exists
- ❌ More expensive options when cheaper alternatives work
- ❌ Complex architectures when simple ones suffice

### **Architecture Principles**
- 🏗️ **Design for failure**: Assume components will fail
- 📈 **Scale horizontally**: Add more instances vs bigger instances
- 🔄 **Decouple components**: Use queues, load balancers, microservices
- 💰 **Optimize costs**: Right-size, use appropriate storage classes
- 🔐 **Implement security**: Defense in depth, least privilege

---

**🎓 Use these flashcards for active recall practice. Cover the answers and try to explain concepts in your own words!**