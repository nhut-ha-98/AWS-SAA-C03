# 🧪 AWS SAA-C03 Hands-On Lab Guide

> **Practical exercises** để thực hành với AWS services trước khi thi

---

## 🚀 **Lab Setup Prerequisites**

### **AWS Account Requirements**
- ✅ **AWS Free Tier Account**: 12 tháng miễn phí cho new accounts
- ✅ **Billing Alerts**: Set up để avoid unexpected charges
- ✅ **IAM User**: Tạo IAM user thay vì dùng root account
- ✅ **MFA Enabled**: Multi-factor authentication cho security
- ✅ **AWS CLI Installed**: Command line interface cho automation

### **Free Tier Limits**
```bash
EC2: 750 hours/month t2.micro (Linux/Windows)
S3: 5 GB storage, 20,000 GET requests, 2,000 PUT requests
RDS: 750 hours/month db.t2.micro, 20 GB storage
Lambda: 1M requests/month, 400,000 GB-seconds compute
CloudFront: 50 GB data transfer out
```

---

## 🏗️ **Lab 1: 3-Tier Web Application**

### **Architecture Overview**
```
Internet → CloudFront → ALB → Auto Scaling Group → RDS
                              ↓
                          ElastiCache
```

### **Step-by-Step Implementation**

#### **Phase 1: VPC Setup (30 minutes)**
```bash
# 1. Create VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16 --tag-specifications 'ResourceType=vpc,Tags=[{Key=Name,Value=MyVPC}]'

# 2. Create Subnets
# Public Subnets (for ALB)
aws ec2 create-subnet --vpc-id vpc-xxx --cidr-block 10.0.1.0/24 --availability-zone us-east-1a
aws ec2 create-subnet --vpc-id vpc-xxx --cidr-block 10.0.2.0/24 --availability-zone us-east-1b

# Private Subnets (for EC2, RDS)
aws ec2 create-subnet --vpc-id vpc-xxx --cidr-block 10.0.11.0/24 --availability-zone us-east-1a
aws ec2 create-subnet --vpc-id vpc-xxx --cidr-block 10.0.12.0/24 --availability-zone us-east-1b

# 3. Internet Gateway
aws ec2 create-internet-gateway
aws ec2 attach-internet-gateway --internet-gateway-id igw-xxx --vpc-id vpc-xxx

# 4. NAT Gateway
aws ec2 create-nat-gateway --subnet-id subnet-xxx --allocation-id eipalloc-xxx
```

#### **Phase 2: Database Layer (20 minutes)**
```bash
# 1. Create DB Subnet Group
aws rds create-db-subnet-group \
  --db-subnet-group-name myapp-db-subnet-group \
  --db-subnet-group-description "Subnet group for MyApp" \
  --subnet-ids subnet-xxx subnet-yyy

# 2. Create RDS Instance
aws rds create-db-instance \
  --db-instance-identifier myapp-db \
  --db-instance-class db.t3.micro \
  --engine mysql \
  --master-username admin \
  --master-user-password MyPassword123 \
  --allocated-storage 20 \
  --vpc-security-group-ids sg-xxx \
  --db-subnet-group-name myapp-db-subnet-group \
  --multi-az
```

#### **Phase 3: Application Layer (45 minutes)**
```bash
# 1. Create Launch Template
aws ec2 create-launch-template \
  --launch-template-name myapp-template \
  --launch-template-data '{
    "ImageId":"ami-0abcdef1234567890",
    "InstanceType":"t3.micro",
    "SecurityGroupIds":["sg-xxx"],
    "UserData":"IyEvYmluL2Jhc2gKe..."
  }'

# 2. Create Auto Scaling Group
aws autoscaling create-auto-scaling-group \
  --auto-scaling-group-name myapp-asg \
  --launch-template LaunchTemplateName=myapp-template,Version=1 \
  --min-size 2 \
  --max-size 4 \
  --desired-capacity 2 \
  --vpc-zone-identifier "subnet-xxx,subnet-yyy"

# 3. Create Application Load Balancer
aws elbv2 create-load-balancer \
  --name myapp-alb \
  --subnets subnet-xxx subnet-yyy \
  --security-groups sg-xxx
```

#### **Phase 4: Caching Layer (15 minutes)**
```bash
# Create ElastiCache Redis Cluster
aws elasticache create-cache-cluster \
  --cache-cluster-id myapp-cache \
  --cache-node-type cache.t3.micro \
  --engine redis \
  --num-cache-nodes 1 \
  --cache-subnet-group-name myapp-cache-subnet-group
```

### **Testing & Validation**
- [ ] **Web Application**: Access via ALB DNS name
- [ ] **Auto Scaling**: Terminate instance, verify replacement
- [ ] **Database**: Connect from EC2 instances
- [ ] **Caching**: Verify Redis connectivity
- [ ] **Monitoring**: Check CloudWatch metrics

### **Lab Learning Objectives**
- ✅ VPC networking với public/private subnets
- ✅ Multi-AZ RDS deployment cho high availability  
- ✅ Auto Scaling Group với health checks
- ✅ Application Load Balancer configuration
- ✅ ElastiCache integration với application tier

---

## 🗄️ **Lab 2: S3 Data Lake với Analytics**

### **Architecture Overview**
```
Data Sources → S3 Bucket → AWS Glue → Amazon Athena → QuickSight
                    ↓
              Lifecycle Policies → Glacier
```

### **Step-by-Step Implementation**

#### **Phase 1: S3 Setup (20 minutes)**
```bash
# 1. Create S3 Buckets
aws s3 mb s3://myapp-data-lake-raw-data
aws s3 mb s3://myapp-data-lake-processed
aws s3 mb s3://myapp-data-lake-analytics-results

# 2. Enable Versioning
aws s3api put-bucket-versioning \
  --bucket myapp-data-lake-raw-data \
  --versioning-configuration Status=Enabled

# 3. Create Lifecycle Policy
aws s3api put-bucket-lifecycle-configuration \
  --bucket myapp-data-lake-raw-data \
  --lifecycle-configuration file://lifecycle-policy.json
```

**lifecycle-policy.json**:
```json
{
  "Rules": [{
    "ID": "DataLifecycle",
    "Status": "Enabled",
    "Filter": {"Prefix": "logs/"},
    "Transitions": [{
      "Days": 30,
      "StorageClass": "STANDARD_IA"
    }, {
      "Days": 90,
      "StorageClass": "GLACIER"
    }]
  }]
}
```

#### **Phase 2: Data Cataloging với Glue (30 minutes)**
```bash
# 1. Create Glue Database
aws glue create-database \
  --database-input Name=mydatalake,Description="Data lake database"

# 2. Create Glue Crawler
aws glue create-crawler \
  --name mydatalake-crawler \
  --role arn:aws:iam::account:role/GlueServiceRole \
  --database-name mydatalake \
  --targets S3Targets=[{Path=s3://myapp-data-lake-raw-data/}]

# 3. Start Crawler
aws glue start-crawler --name mydatalake-crawler
```

#### **Phase 3: Analytics với Athena (20 minutes)**
```sql
-- Create external table
CREATE EXTERNAL TABLE sales_data (
  order_id string,
  customer_id string,
  product_id string,
  quantity int,
  price decimal(10,2),
  order_date date
)
PARTITIONED BY (year int, month int)
STORED AS PARQUET
LOCATION 's3://myapp-data-lake-processed/sales/'

-- Sample analytics query
SELECT 
  product_id,
  COUNT(*) as order_count,
  SUM(quantity * price) as total_revenue
FROM sales_data 
WHERE year = 2024 AND month = 9
GROUP BY product_id
ORDER BY total_revenue DESC
LIMIT 10;
```

### **Testing & Validation**
- [ ] **Data Upload**: Upload CSV files to S3
- [ ] **Crawler Execution**: Verify table creation trong Glue Catalog
- [ ] **Query Performance**: Run Athena queries, check performance
- [ ] **Cost Optimization**: Verify lifecycle transitions
- [ ] **Partitioning**: Test partition pruning trong queries

### **Lab Learning Objectives**
- ✅ S3 storage classes và lifecycle management
- ✅ AWS Glue data cataloging và ETL
- ✅ Amazon Athena serverless querying
- ✅ Partitioning strategies cho performance
- ✅ Cost optimization với storage classes

---

## 🔐 **Lab 3: Security & Compliance Setup**

### **Architecture Overview**
```
IAM Users/Roles → KMS → Encrypted Resources → CloudTrail → Security Hub
```

### **Step-by-Step Implementation**

#### **Phase 1: IAM Security (25 minutes)**
```bash
# 1. Create IAM Policy for S3 Access
aws iam create-policy \
  --policy-name S3ReadOnlyAccess \
  --policy-document file://s3-readonly-policy.json

# 2. Create IAM Role for EC2
aws iam create-role \
  --role-name EC2-S3-Access-Role \
  --assume-role-policy-document file://trust-policy.json

# 3. Attach Policy to Role
aws iam attach-role-policy \
  --role-name EC2-S3-Access-Role \
  --policy-arn arn:aws:iam::account:policy/S3ReadOnlyAccess
```

#### **Phase 2: Encryption với KMS (20 minutes)**
```bash
# 1. Create Customer Managed Key
aws kms create-key \
  --policy file://kms-policy.json \
  --description "MyApp encryption key"

# 2. Create Alias
aws kms create-alias \
  --alias-name alias/myapp-key \
  --target-key-id key-id

# 3. Encrypt S3 Bucket
aws s3api put-bucket-encryption \
  --bucket myapp-encrypted-bucket \
  --server-side-encryption-configuration '{
    "Rules": [{
      "ApplyServerSideEncryptionByDefault": {
        "SSEAlgorithm": "aws:kms",
        "KMSMasterKeyID": "arn:aws:kms:region:account:key/key-id"
      }
    }]
  }'
```

#### **Phase 3: Monitoring & Auditing (15 minutes)**
```bash
# 1. Enable CloudTrail
aws cloudtrail create-trail \
  --name myapp-audit-trail \
  --s3-bucket-name myapp-cloudtrail-logs \
  --include-global-service-events \
  --is-multi-region-trail

# 2. Start Logging
aws cloudtrail start-logging --name myapp-audit-trail

# 3. Enable GuardDuty
aws guardduty create-detector --enable
```

### **Lab Learning Objectives**
- ✅ IAM roles và policies cho least privilege
- ✅ KMS key management và encryption
- ✅ CloudTrail logging cho audit compliance
- ✅ GuardDuty threat detection setup
- ✅ Security best practices implementation

---

## 🔄 **Lab 4: Serverless Application**

### **Architecture Overview**
```
API Gateway → Lambda → DynamoDB
     ↓
CloudWatch Logs ← EventBridge ← S3 Events
```

### **Step-by-Step Implementation**

#### **Phase 1: DynamoDB Setup (15 minutes)**
```bash
# Create DynamoDB Table
aws dynamodb create-table \
  --table-name UserProfiles \
  --attribute-definitions \
    AttributeName=UserId,AttributeType=S \
  --key-schema \
    AttributeName=UserId,KeyType=HASH \
  --billing-mode PAY_PER_REQUEST \
  --stream-specification StreamEnabled=true,StreamViewType=NEW_AND_OLD_IMAGES
```

#### **Phase 2: Lambda Functions (30 minutes)**

**lambda-function.py**:
```python
import json
import boto3
from decimal import Decimal

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('UserProfiles')

def lambda_handler(event, context):
    http_method = event['httpMethod']
    
    if http_method == 'GET':
        user_id = event['pathParameters']['userId']
        response = table.get_item(Key={'UserId': user_id})
        return {
            'statusCode': 200,
            'body': json.dumps(response.get('Item', {}))
        }
    
    elif http_method == 'POST':
        user_data = json.loads(event['body'])
        table.put_item(Item=user_data)
        return {
            'statusCode': 201,
            'body': json.dumps({'message': 'User created successfully'})
        }
```

```bash
# Deploy Lambda Function
zip function.zip lambda-function.py
aws lambda create-function \
  --function-name user-profile-api \
  --runtime python3.9 \
  --role arn:aws:iam::account:role/lambda-execution-role \
  --handler lambda-function.lambda_handler \
  --zip-file fileb://function.zip
```

#### **Phase 3: API Gateway (20 minutes)**
```bash
# Create REST API
aws apigateway create-rest-api --name user-profile-api

# Create Resource
aws apigateway create-resource \
  --rest-api-id api-id \
  --parent-id root-resource-id \
  --path-part users

# Create Method
aws apigateway put-method \
  --rest-api-id api-id \
  --resource-id resource-id \
  --http-method GET \
  --authorization-type NONE
```

### **Testing & Validation**
- [ ] **API Endpoints**: Test GET/POST methods via API Gateway
- [ ] **Lambda Logs**: Verify CloudWatch log groups
- [ ] **DynamoDB**: Confirm data persistence  
- [ ] **Performance**: Test với concurrent requests
- [ ] **Error Handling**: Verify error responses

### **Lab Learning Objectives**
- ✅ Serverless architecture với Lambda + API Gateway
- ✅ DynamoDB integration và best practices
- ✅ CloudWatch monitoring cho serverless apps
- ✅ API Gateway configuration và testing
- ✅ Event-driven architecture patterns

---

## 📊 **Lab 5: Monitoring & Observability**

### **Architecture Overview**
```
Applications → CloudWatch Metrics → Alarms → SNS → Email/SMS
     ↓              ↓                 ↓
CloudWatch Logs → Log Insights → Dashboards
```

### **Step-by-Step Implementation**

#### **Phase 1: Custom Metrics (20 minutes)**
```python
# Custom metric example
import boto3
import time

cloudwatch = boto3.client('cloudwatch')

def publish_custom_metric():
    cloudwatch.put_metric_data(
        Namespace='MyApp/Performance',
        MetricData=[
            {
                'MetricName': 'ProcessingTime',
                'Value': 123.45,
                'Unit': 'Milliseconds',
                'Dimensions': [
                    {
                        'Name': 'Environment',
                        'Value': 'Production'
                    }
                ]
            }
        ]
    )
```

#### **Phase 2: Alarms & Notifications (15 minutes)**
```bash
# Create SNS Topic
aws sns create-topic --name app-alerts

# Subscribe to Topic  
aws sns subscribe \
  --topic-arn arn:aws:sns:region:account:app-alerts \
  --protocol email \
  --notification-endpoint your-email@domain.com

# Create CloudWatch Alarm
aws cloudwatch put-metric-alarm \
  --alarm-name "High-CPU-Usage" \
  --alarm-description "Alert when EC2 CPU exceeds 80%" \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2 \
  --alarm-actions arn:aws:sns:region:account:app-alerts
```

#### **Phase 3: Log Analysis (25 minutes)**
```bash
# Create Log Group
aws logs create-log-group --log-group-name /myapp/application

# Example Log Insights Query
aws logs start-query \
  --log-group-name /myapp/application \
  --start-time 1609459200 \
  --end-time 1609545600 \
  --query-string 'fields @timestamp, @message | filter @message like /ERROR/ | sort @timestamp desc | limit 100'
```

### **Lab Learning Objectives**
- ✅ Custom CloudWatch metrics creation
- ✅ Alarm configuration với SNS integration  
- ✅ Log Insights querying techniques
- ✅ Dashboard creation cho operational visibility
- ✅ Proactive monitoring strategies

---

## 🎯 **Lab Completion Checklist**

### **After Each Lab**
- [ ] **Clean up resources**: Delete resources để avoid charges
- [ ] **Document learnings**: Note key takeaways và challenges
- [ ] **Practice variations**: Try different configurations
- [ ] **Cost analysis**: Review AWS billing cho spend understanding
- [ ] **Architecture review**: Compare với AWS Well-Architected principles

### **Overall Learning Outcomes**
- [ ] **Hands-on experience** với 20+ AWS services
- [ ] **Architecture patterns** implementation experience  
- [ ] **Security best practices** applied knowledge
- [ ] **Cost optimization** strategies practiced
- [ ] **Monitoring & troubleshooting** skills developed
- [ ] **CLI/API usage** comfort gained
- [ ] **Real-world scenarios** preparation complete

---

## 🔧 **Troubleshooting Common Issues**

### **IAM Permission Errors**
```bash
# Check policy simulation
aws iam simulate-principal-policy \
  --policy-source-arn arn:aws:iam::account:role/MyRole \
  --action-names s3:GetObject \
  --resource-arns arn:aws:s3:::mybucket/mykey
```

### **VPC Connectivity Issues**
```bash
# Check route tables
aws ec2 describe-route-tables --filters "Name=vpc-id,Values=vpc-xxx"

# Check security groups
aws ec2 describe-security-groups --filters "Name=vpc-id,Values=vpc-xxx"
```

### **Resource Cleanup Script**
```bash
#!/bin/bash
# Cleanup script to avoid charges

# Delete EC2 instances
aws ec2 terminate-instances --instance-ids $(aws ec2 describe-instances --query 'Reservations[].Instances[].InstanceId' --output text)

# Delete RDS instances  
aws rds delete-db-instance --db-instance-identifier myapp-db --skip-final-snapshot

# Delete S3 buckets (empty first)
aws s3 rm s3://mybucket --recursive
aws s3 rb s3://mybucket
```

---

**🧪 These hands-on labs provide practical experience with AWS services essential for SAA-C03 success. Practice regularly and experiment with different configurations! 🚀**