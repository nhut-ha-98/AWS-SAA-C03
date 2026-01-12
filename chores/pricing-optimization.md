# 💰 AWS Pricing & Cost Optimization Guide

> **Complete cost management strategies** cho SAA-C03 exam và real-world scenarios

---

## 📊 **AWS Pricing Models Overview**

### **Core Pricing Concepts**
- **Pay-as-you-go**: Chỉ trả cho resources đã sử dụng
- **Pay less when you reserve**: Reserved Instances discounts
- **Pay less with volume**: Volume discounts cho large usage
- **Pay less as AWS grows**: AWS giảm giá theo thời gian

### **Billing & Cost Management Tools**
- 🔍 **AWS Cost Explorer**: Analyze và visualize costs
- 📊 **AWS Budgets**: Set cost và usage budgets
- 🚨 **AWS Cost Anomaly Detection**: Detect unusual spending
- 📈 **AWS Cost and Usage Report**: Detailed billing data
- 💳 **AWS Billing Dashboard**: Overview spending summary
- 🏷️ **Cost Allocation Tags**: Track costs by project/department

---

## 🖥️ **EC2 Pricing Strategies**

### **Instance Purchasing Options**

#### **🔥 On-Demand Instances**
```
Pricing: $0.0116/hour (t3.micro us-east-1)
Use Cases:
✅ Development và testing
✅ Unpredictable workloads  
✅ Applications với short-term spiky usage
❌ Long-running production workloads (expensive)
```

#### **⭐ Reserved Instances (RI)**
```
Standard RI: Up to 75% discount vs On-Demand
Convertible RI: Up to 66% discount + flexibility to change
Scheduled RI: For predictable recurring schedules

Terms: 1 year or 3 years
Payment: No Upfront, Partial Upfront, All Upfront

Example Savings:
t3.medium On-Demand: $0.0416/hour × 8760 hours = $364/year
t3.medium RI (3-year All Upfront): $182/year = 50% savings
```

#### **💡 Savings Plans**
```
Compute Savings Plans: Up to 66% discount
- Flexible across instance family, size, OS, tenancy, region
- Applies to EC2, Lambda, Fargate

EC2 Instance Savings Plans: Up to 72% discount  
- Specific to instance family in chosen region
- Flexible across size, OS, tenancy
```

#### **🏃 Spot Instances**
```
Discount: Up to 90% vs On-Demand
Best for:
✅ Fault-tolerant workloads
✅ Batch processing
✅ CI/CD pipelines
✅ Big data analytics
❌ Critical production databases
❌ Real-time applications

Spot Fleet Strategy:
- Mix multiple instance types và AZs
- Use Spot Instance interruption notices
- Implement graceful shutdown handling
```

### **Cost Optimization Techniques**

#### **Right-Sizing Instances**
```bash
# Use CloudWatch metrics để identify under-utilized instances
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
  --start-time 2024-09-01T00:00:00Z \
  --end-time 2024-09-25T23:59:59Z \
  --period 86400 \
  --statistics Average

# Recommendations:
CPU < 20% consistently → Downsize instance type
Memory < 50% consistently → Choose memory-optimized instance
Network utilization low → Choose smaller instance
```

#### **Auto Scaling Cost Benefits**
```
Traditional Fixed Capacity: 4 × t3.medium = $1,460/year
Auto Scaling (2-6 instances): Average 3 instances = $1,095/year
Savings: $365/year (25% reduction)

Best Practices:
- Set appropriate min/max limits
- Use predictive scaling cho known patterns
- Implement warm-up periods
- Monitor scaling metrics regularly
```

---

## 🗄️ **S3 Storage Cost Optimization**

### **Storage Classes Pricing (us-east-1)**
```
S3 Standard: $0.023/GB/month
S3 Standard-IA: $0.0125/GB/month + retrieval fees
S3 One Zone-IA: $0.01/GB/month + retrieval fees
S3 Glacier Instant Retrieval: $0.004/GB/month
S3 Glacier Flexible Retrieval: $0.0036/GB/month
S3 Glacier Deep Archive: $0.00099/GB/month
S3 Intelligent Tiering: $0.0125/GB/month + monitoring fees
```

### **Lifecycle Policy Examples**

#### **Standard → IA → Glacier Strategy**
```json
{
  "Rules": [{
    "ID": "CostOptimizedLifecycle",
    "Status": "Enabled",
    "Filter": {"Prefix": "logs/"},
    "Transitions": [
      {
        "Days": 30,
        "StorageClass": "STANDARD_IA"
      },
      {
        "Days": 90, 
        "StorageClass": "GLACIER"
      },
      {
        "Days": 365,
        "StorageClass": "DEEP_ARCHIVE"
      }
    ],
    "Expiration": {
      "Days": 2555
    }
  }]
}

Cost Analysis (1TB data):
Month 1-30: $23/month (Standard)
Month 31-90: $12.50/month (IA) 
Month 91-365: $3.60/month (Glacier)
Year 2+: $0.99/month (Deep Archive)
Total Year 1: $183 vs $276 (Standard only) = 34% savings
```

#### **Intelligent Tiering ROI**
```
Scenario: 10TB mixed access patterns
Standard only: $230/month
Intelligent Tiering: $125/month + $1.25 monitoring = $126.25/month
Monthly savings: $103.75 (45% reduction)
Break-even point: ~1,000 objects minimum
```

### **S3 Cost Optimization Best Practices**
```bash
# 1. Enable S3 Analytics để understand access patterns
aws s3api put-bucket-analytics-configuration \
  --bucket my-bucket \
  --id analytics-config \
  --analytics-configuration Id=analytics-config,StorageClassAnalysis={}

# 2. Use S3 Inventory để track object metadata
aws s3api put-bucket-inventory-configuration \
  --bucket my-bucket \
  --id inventory-config \
  --inventory-configuration file://inventory-config.json

# 3. Implement request optimization
- Use multipart uploads cho files > 100MB
- Enable Transfer Acceleration cho global users
- Use CloudFront để reduce S3 requests
- Batch operations với S3 Batch Operations
```

---

## 🗃️ **Database Cost Optimization**

### **RDS Pricing Strategies**

#### **Instance Types vs Workloads**
```
General Purpose (db.t3/db.m5):
- Dev/test environments: db.t3.micro ($13/month)
- Small production: db.t3.small ($26/month)
- Medium workloads: db.m5.large ($140/month)

Memory Optimized (db.r5/db.x1e):
- In-memory databases: db.r5.large ($175/month)
- Large analytical workloads: db.r5.xlarge ($350/month)

Compute Optimized (db.c5):
- CPU-intensive applications: db.c5.large ($85/month)
```

#### **Reserved Instance Savings**
```
RDS RI Discounts:
1-year term: ~30-40% savings
3-year term: ~50-60% savings

Example (db.r5.xlarge):
On-Demand: $350/month × 12 = $4,200/year
1-year RI: $2,940/year (30% savings)
3-year RI: $1,890/year (55% savings)
```

### **Aurora vs RDS Cost Comparison**
```
RDS MySQL (Multi-AZ): 
- db.r5.large: $350/month
- Storage (1TB): $115/month
- Backup storage: $50/month
Total: $515/month

Aurora MySQL:
- 2 instances: $290/month  
- Storage (1TB): $100/month (pay for what you use)
- Backup: Included
Total: $390/month (24% savings)

Aurora Serverless v2:
- Variable compute: $87-$580/month based on usage
- Perfect for variable workloads
```

### **DynamoDB Cost Optimization**

#### **Pricing Models Comparison**
```
On-Demand:
- Write: $1.25 per million WRU
- Read: $0.25 per million RRU
- Best for: Unpredictable traffic

Provisioned:
- Write: $0.65 per WCU/month
- Read: $0.13 per RCU/month  
- Auto Scaling: Adjust capacity automatically
- Best for: Predictable traffic patterns

Example (1M reads, 200K writes/month):
On-Demand: $250 + $250 = $500/month
Provisioned: $39 + $195 = $234/month (53% savings)
```

#### **DynamoDB Optimization Techniques**
```bash
# 1. Use efficient data modeling
- Single table design
- Composite sort keys
- GSI projection optimization

# 2. Enable compression
aws dynamodb update-table \
  --table-name MyTable \
  --attribute-definitions AttributeName=PK,AttributeType=S \
  --table-class STANDARD_INFREQUENT_ACCESS

# 3. Monitor consumed capacity
aws dynamodb describe-table --table-name MyTable \
  --query 'Table.ProvisionedThroughput'
```

---

## 🌐 **Networking Cost Optimization**

### **Data Transfer Pricing**
```
Internet Data Transfer Out:
First 1 GB/month: FREE
Next 9.999 TB/month: $0.09/GB
Next 40 TB/month: $0.085/GB
Next 100 TB/month: $0.07/GB
Greater than 150 TB/month: $0.05/GB

Regional Data Transfer:
Same AZ: FREE
Cross-AZ: $0.01/GB each direction
Cross-Region: $0.02/GB
```

### **CloudFront Cost Benefits**
```
Direct S3 Access (1TB/month):
Data transfer: $90
Request charges: $0.40
Total: $90.40

Via CloudFront:
CloudFront data transfer: $85
CloudFront requests: $0.75
S3 origin requests: $0.40
Total: $86.15
Savings: $4.25 + improved performance

Additional benefits:
- Edge caching reduces S3 requests
- HTTPS termination
- Global performance improvement
```

### **VPC Cost Considerations**
```
NAT Gateway: $45/month + $0.045/GB processed
NAT Instance (t3.nano): $4/month + data transfer

Cost Break-even Analysis:
NAT Gateway fixed cost: $45
NAT Instance cost for 1TB: $4 + $10 = $14
Break-even: ~900GB/month

VPC Endpoints:
- $7.20/month per endpoint
- Saves data transfer costs to AWS services
- Break-even: ~720GB S3 access/month
```

---

## ⚡ **Serverless Cost Optimization**

### **Lambda Pricing Strategy**
```
Free Tier:
- 1M requests/month
- 400,000 GB-seconds compute/month

Pricing (after free tier):
- Requests: $0.20 per 1M requests  
- Compute: $0.0000166667 per GB-second
- Provisioned Concurrency: $0.0000097222 per GB-second

Cost Optimization Tips:
1. Right-size memory allocation (impacts CPU)
2. Minimize cold starts với provisioned concurrency
3. Use ARM-based Graviton2 processors (20% cheaper)
4. Optimize code execution time
```

### **Lambda vs EC2 Cost Comparison**
```
Scenario: API với 1M requests/month, 500ms avg duration

Lambda:
- Requests: $0.20
- Compute (128MB): $10.40  
Total: $10.60/month

EC2 (t3.nano):
- Instance: $3.80/month
- 24/7 availability required
Total: $3.80/month (cheaper for consistent load)

Break-even: ~500K requests/month
```

### **API Gateway Optimization**
```
REST API: $3.50 per million API calls
HTTP API: $1.00 per million API calls (71% cheaper)

Caching Benefits:
- $0.02/hour for 0.5GB cache
- Reduces backend calls
- Improves response times

Example (1M calls with 50% cache hit):
Without cache: $3.50
With cache: $1.75 + $14.40 = $16.15
Break-even: >4M calls/month
```

---

## 📊 **Cost Monitoring & Alerting**

### **AWS Budgets Setup**
```bash
# Create cost budget
aws budgets create-budget \
  --account-id 123456789012 \
  --budget '{
    "BudgetName": "Monthly-Cost-Budget",
    "BudgetLimit": {
      "Amount": "100",
      "Unit": "USD"
    },
    "TimeUnit": "MONTHLY",
    "BudgetType": "COST"
  }' \
  --notifications-with-subscribers file://budget-notifications.json
```

**budget-notifications.json**:
```json
[{
  "Notification": {
    "NotificationType": "ACTUAL", 
    "ComparisonOperator": "GREATER_THAN",
    "Threshold": 80,
    "ThresholdType": "PERCENTAGE"
  },
  "Subscribers": [{
    "SubscriptionType": "EMAIL",
    "Address": "admin@company.com"
  }]
}]
```

### **Cost Allocation Tags Strategy**
```bash
# Tag resources for cost tracking
aws ec2 create-tags \
  --resources i-1234567890abcdef0 \
  --tags Key=Environment,Value=Production \
         Key=Project,Value=WebApp \
         Key=Owner,Value=TeamA \
         Key=CostCenter,Value=Engineering

# Activate cost allocation tags
aws ce activate-cost-allocation-tags \
  --tag-keys Environment Project Owner CostCenter
```

### **Cost Explorer Queries**
```bash
# Get monthly costs by service
aws ce get-cost-and-usage \
  --time-period Start=2024-09-01,End=2024-09-30 \
  --granularity MONTHLY \
  --metrics UnblendedCost \
  --group-by Type=DIMENSION,Key=SERVICE

# Get costs by tag
aws ce get-cost-and-usage \
  --time-period Start=2024-09-01,End=2024-09-30 \
  --granularity MONTHLY \
  --metrics UnblendedCost \
  --group-by Type=TAG,Key=Project
```

---

## 🎯 **Cost Optimization Action Plan**

### **Week 1: Assessment**
- [ ] **Enable Cost Explorer**: Analyze current spending patterns
- [ ] **Set up Budgets**: Create alerts for cost thresholds
- [ ] **Implement Tagging**: Tag all resources for cost allocation
- [ ] **Review Right-sizing**: Identify oversized EC2 instances
- [ ] **Audit Storage**: Find unused EBS volumes và snapshots

### **Week 2: Quick Wins**
- [ ] **Delete unused resources**: Unattached EBS, unused AMIs
- [ ] **Convert to Reserved Instances**: For predictable workloads
- [ ] **Implement S3 Lifecycle**: Move old data to cheaper storage
- [ ] **Enable S3 Intelligent Tiering**: For mixed access patterns  
- [ ] **Review data transfer**: Optimize cross-AZ communication

### **Week 3: Advanced Optimization**
- [ ] **Evaluate Spot Instances**: For fault-tolerant workloads
- [ ] **Implement Auto Scaling**: Match capacity to demand
- [ ] **Optimize Lambda**: Right-size memory và reduce duration
- [ ] **Review RDS**: Consider Aurora, enable Performance Insights
- [ ] **CloudFront implementation**: Reduce origin requests

### **Week 4: Monitoring & Governance**
- [ ] **Set up anomaly detection**: Catch unexpected spending
- [ ] **Create cost dashboards**: Visual spending tracking
- [ ] **Implement approval workflows**: For expensive resources
- [ ] **Regular cost reviews**: Monthly team meetings
- [ ] **Optimization automation**: Scripts for common tasks

---

## 💡 **SAA-C03 Exam Focus Areas**

### **Key Cost Concepts for Exam**
1. **Reserved Instances**: Standard vs Convertible vs Scheduled
2. **Savings Plans**: Compute vs EC2 Instance plans
3. **Spot Instances**: Best practices và use cases
4. **S3 Storage Classes**: Cost-effective data lifecycle
5. **Data Transfer**: Understanding egress charges
6. **Right-sizing**: Matching resources to workload needs

### **Common Exam Scenarios**
```
Scenario 1: "Reduce costs for predictable workloads"
Answer: Reserved Instances or Savings Plans

Scenario 2: "Fault-tolerant batch processing cost optimization"  
Answer: Spot Instances với Spot Fleets

Scenario 3: "Reduce S3 costs for infrequently accessed data"
Answer: S3 Intelligent Tiering or Lifecycle policies

Scenario 4: "Lower data transfer costs for global users"
Answer: CloudFront CDN implementation

Scenario 5: "Optimize costs for variable serverless workload"
Answer: Lambda với appropriate memory sizing
```

### **Cost Optimization Decision Tree**
```
Workload Type?
├── Predictable → Reserved Instances/Savings Plans
├── Variable → Auto Scaling + On-Demand
├── Fault-tolerant → Spot Instances
├── Serverless → Lambda optimization
└── Storage → Lifecycle policies + Intelligent Tiering

Access Pattern?  
├── Frequent → S3 Standard
├── Infrequent → S3 IA or Intelligent Tiering
├── Archive → S3 Glacier/Deep Archive
└── Unknown → S3 Intelligent Tiering

Performance Requirements?
├── High → On-Demand/Reserved
├── Flexible → Spot Instances  
├── Burst → T3 burstable instances
└── Consistent → Fixed instance types
```

---

## 📈 **ROI Calculation Examples**

### **Reserved Instance ROI**
```
Current On-Demand Cost: $5,000/month
3-year RI Cost: $1,800/year = $150/month
Monthly Savings: $4,850
3-year Total Savings: $174,600
ROI: 970% over 3 years
```

### **Auto Scaling ROI**
```
Fixed 10 instances: $500/month
Auto Scaling (avg 6 instances): $300/month
Implementation cost: $2,000 (one-time)
Break-even: 10 months
Annual savings: $2,400 (after break-even)
```

### **S3 Lifecycle ROI**
```
100TB data in S3 Standard: $2,300/month
With lifecycle to Glacier: $600/month
Implementation effort: 40 hours
Monthly savings: $1,700
Annual savings: $20,400
```

---

**💰 Implementing these cost optimization strategies will significantly reduce AWS spending while maintaining performance và reliability! 🎯**