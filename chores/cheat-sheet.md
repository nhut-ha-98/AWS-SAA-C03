# ⚡ AWS SAA-C03 Cheat Sheet

> **1-page reference** cho exam day - In ra và mang theo khi thi!

---

## 🔥 **Critical Services Quick Reference**

### **EC2 Instance Types**
```
T4g: Burstable (web servers, small DBs)
M6i: General purpose (web apps, microservices) 
C6i: Compute optimized (HPC, gaming)
R6i: Memory optimized (databases, caches)
I4i: Storage optimized (NoSQL, data warehouses)
```

### **EBS Volume Types**
```
gp3: General SSD (3K-16K IOPS) - DEFAULT choice
io1/io2: Provisioned IOPS SSD (up to 64K IOPS)
st1: Throughput HDD (big data, logs)
sc1: Cold HDD (infrequent access)
```

### **S3 Storage Classes**
```
Standard → Standard-IA (30+ days) → Glacier IR (90+ days)
→ Glacier Flexible (90+ days, 1-12h retrieval)  
→ Glacier Deep Archive (180+ days, 12h+ retrieval)
Intelligent Tiering: Unknown access patterns
```

### **Load Balancer Selection**
```
ALB: HTTP/HTTPS, Layer 7 routing, WAF integration
NLB: TCP/UDP, ultra-high performance, static IP
CLB: Legacy, avoid for new deployments
```

---

## 🗄️ **Database Decision Matrix**

| Need | Solution | When to Use |
|------|----------|-------------|
| **RDBMS** | RDS Multi-AZ | Traditional apps, ACID |
| **Cloud Native** | Aurora | 5x MySQL perf, global apps |
| **NoSQL** | DynamoDB | Web/mobile, millisecond latency |
| **Cache** | ElastiCache | Session store, read acceleration |
| **Data Warehouse** | Redshift | OLAP, business intelligence |
| **Search** | OpenSearch | Log analytics, full-text search |

---

## 🌐 **Networking Essentials**

### **VPC Components**
```
Internet Gateway (IGW): Public subnet internet access
NAT Gateway: Private subnet outbound internet  
VPC Peering: Direct VPC-to-VPC (no transitive)
Transit Gateway: Hub-and-spoke, supports transitive
VPC Endpoints: Private AWS service access
```

### **Route 53 Routing Policies**
```
Simple: Single resource, no health check
Weighted: A/B testing, gradual rollout
Latency: Route to lowest latency region
Failover: Active/passive with health checks
Geolocation: Route by user location
```

---

## 🔐 **Security Quick Checks**

### **IAM Best Practices**
- ✅ Roles for applications, Users for humans
- ✅ Least privilege principle
- ✅ MFA for privileged access
- ✅ Rotate access keys regularly
- ✅ Use policy conditions for context

### **Encryption Options**
```
S3: SSE-S3 (AWS keys) | SSE-KMS (customer keys) | SSE-C (customer provided)
EBS: KMS encryption (at rest + transit)
RDS: KMS encryption + SSL/TLS
DynamoDB: Encryption at rest (default)
```

---

## 📊 **Monitoring & Management**

### **CloudWatch vs CloudTrail vs Config**
```
CloudWatch: Metrics, logs, alarms (performance monitoring)
CloudTrail: API calls, who did what (security auditing)
Config: Resource configuration changes (compliance)
```

### **Auto Scaling Policies**
```
Target Tracking: Maintain metric target (CPU 70%)
Step Scaling: Scale based on alarm breach size
Simple Scaling: Scale by fixed amount
Predictive: ML-based proactive scaling
```

---

## 🔄 **Integration Patterns**

### **SQS vs SNS vs EventBridge**
```
SQS: Point-to-point messaging, decoupling
SNS: Pub/Sub, fan-out to multiple subscribers  
EventBridge: Event routing, SaaS integration
```

### **Lambda Triggers**
```
API Gateway: REST/HTTP APIs
S3: Object events (create, delete)
DynamoDB: Streams for data changes
EventBridge: Scheduled or event-driven
SQS: Queue message processing
```

---

## 💰 **Cost Optimization Cheat**

### **Pricing Models**
```
On-Demand: Variable workloads, testing
Reserved: Predictable 24/7 (up to 75% savings)
Spot: Fault-tolerant batch (up to 90% savings)
Savings Plans: Flexible usage commitment
```

### **Storage Cost Optimization**
```
S3 Lifecycle: Auto-transition to cheaper classes
EBS: gp3 vs gp2 (better price/performance)
Snapshots: Incremental, cross-region for DR
EFS: IA storage class for infrequent access
```

---

## 🏗️ **Architecture Patterns**

### **High Availability**
```
Multi-AZ: RDS, ELB, Auto Scaling across AZs
Health Checks: Route 53, ELB target health
Auto Recovery: Auto Scaling, RDS failover
Backup: Automated backups, cross-region copy
```

### **Disaster Recovery**
```
Backup & Restore: Cheapest, higher RTO/RPO
Pilot Light: Core systems, scale when needed
Warm Standby: Scaled-down production copy
Multi-Site: Active-active, lowest RTO/RPO
```

---

## ⚡ **Performance Optimization**

### **Caching Strategy**
```
CloudFront: Global edge caching (static content)
ElastiCache: Database query caching
DAX: DynamoDB microsecond caching
S3 Transfer Acceleration: Global uploads
```

### **Database Performance**
```
RDS: Read replicas, Multi-AZ, parameter groups
DynamoDB: Partition key design, GSI, DAX
Aurora: Auto scaling, parallel query, global DB
Redshift: Columnar storage, distribution keys
```

---

## 🎯 **Exam Strategy Reminders**

### **Question Analysis Steps**
1. **Identify requirement keywords**: cost-effective, highly available, scalable
2. **Eliminate obviously wrong answers**: Over/under-engineered solutions  
3. **Apply Well-Architected principles**: Security, reliability, performance
4. **Choose simplest solution**: That meets all requirements

### **Time Management**  
```
130 minutes ÷ 65 questions = 2 min/question
First pass (90 min): Answer confident questions
Second pass (30 min): Review flagged questions  
Final check (10 min): Verify answers
```

### **Common Traps to Avoid**
- ❌ Reserved Instances for unpredictable workloads
- ❌ Public subnets for databases
- ❌ Single AZ for HA requirements
- ❌ Over-permissive security groups
- ❌ Ignoring cost optimization opportunities

---

## 🚨 **Last-Minute Memory Aids**

### **Service Limits (Key Ones)**
```
VPC: 5 per region (soft limit)
Security Groups: 2,500 per VPC
Lambda: 15 min timeout, 10GB memory
S3: Unlimited objects, 5TB per object
DynamoDB: 400KB item size limit
```

### **Multi-AZ vs Read Replicas**
```
Multi-AZ: HA (synchronous, same region, auto failover)
Read Replicas: Scaling (asynchronous, can be cross-region)
```

### **IAM Policy Evaluation**
```
1. Explicit DENY (always wins)
2. Explicit ALLOW (required for access)  
3. Default DENY (no allow = deny)
```

---

## 📋 **Final Checklist Before Exam**

- [ ] **ID and confirmation ready**
- [ ] **Quiet environment set up** (for online exam)
- [ ] **This cheat sheet reviewed** 
- [ ] **Well-rested and confident**
- [ ] **Practice exam score 85%+**

---

**🎓 Remember: Think like a cloud architect, not just a service user. Consider the big picture, integrations, and long-term implications. You've got this! 🚀**

**Print this page and keep it handy for last-minute review! Good luck! 🍀**