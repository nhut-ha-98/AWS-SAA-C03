# AWS Data Transfer Services Guide 🚚

*Comprehensive guide to AWS data transfer solutions, from edge computing to massive migrations*

## 🎯 Overview

AWS provides multiple data transfer services to handle different scenarios - from small edge deployments to exabyte-scale migrations. This guide helps you choose the right service based on data volume, location, connectivity, and timing requirements.

---

## 🚀 Quick Service Selection Table

| Service                 | Data Capacity           | Best For                                                          | Connectivity Required |
| ----------------------- | ----------------------- | ----------------------------------------------------------------- | -------------------- |
| **AWS Snowcone**        | 8 TB (HDD) / 14 TB (SSD)| Edge computing in tight/mobile spaces (drones, vehicles, IoT)     | Optional (offline)   |
| **AWS Snowball Edge**   | 80 TB / 210 TB         | Medium migrations, edge computing with local processing           | Optional (offline)   |
| **AWS Snowmobile**      | Up to 100 PB per truck | Massive data center migrations (exabyte scale)                   | No (physical truck)  |
| **AWS DataSync**        | No limit                | Continuous/scheduled online transfers between locations           | Required (network)   |
| **AWS Transfer Family** | No limit                | Application-level FTP/SFTP transfers to S3/EFS                   | Required (network)   |
| **AWS Storage Gateway** | No limit                | Hybrid cloud storage extending on-premises to AWS                 | Required (network)   |

---

## 🌳 Data Transfer Decision Tree

```
Do you need to transfer data to AWS?
│
├──> No → ❌ No transfer needed
│
└──> Yes
     │
     ├── What's your data volume?
     │   │
     │   ├── < 10 TB → Continue to connectivity check ↓
     │   ├── 10 TB - 100 TB → Consider Snowball Edge or DataSync ↓
     │   ├── 100 TB - 10 PB → Definitely Snowball Edge (multiple) ↓
     │   └── > 10 PB → ✅ Use Snowmobile
     │
     ├── Do you have reliable high-speed internet?
     │   │
     │   ├── Yes (>1 Gbps stable) → Continue to transfer type ↓
     │   └── No/Limited → Use physical devices (Snowball family) ↓
     │
     ├── What type of transfer do you need?
     │   │
     │   ├── One-time migration → Physical devices or DataSync ↓
     │   ├── Ongoing sync → ✅ DataSync (scheduled)
     │   ├── Application integration → ✅ Transfer Family (FTP/SFTP)
     │   └── Hybrid storage → ✅ Storage Gateway
     │
     ├── Do you need edge computing capabilities?
     │   │
     │   ├── Yes → Choose Snowball Edge or Snowcone ↓
     │   └── No → Continue to location analysis ↓
     │
     ├── Where is your deployment location?
     │   │
     │   ├── Space-constrained (vehicles, ships, remote) → ✅ Snowcone
     │   ├── Standard data center/office → ✅ Snowball Edge
     │   └── Massive data center → ✅ Snowmobile
     │
     └── Do you need specific protocols?
         │
         ├── NFS file access → Snowball Edge with NFS
         ├── FTP/SFTP endpoints → ✅ Transfer Family
         ├── iSCSI/NFS gateway → ✅ Storage Gateway
         └── Standard S3 API → Any Snowball device or DataSync
```

---

## 📋 Service Deep Dive

### ❄️ AWS Snowcone
*Ultra-portable edge computing device*

**Physical Specifications:**
- **Weight:** 4.5 lbs (2.1 kg)
- **Size:** 9" x 6" x 3" (227mm x 148.6mm x 82.65mm)
- **Power:** 45W (can run on battery)
- **Environment:** Rugged, military-grade design

**Key Features:**
- ✅ 8 TB HDD or 14 TB SSD storage
- ✅ 4 GB memory, 2 vCPUs
- ✅ Runs EC2 instances and Lambda functions
- ✅ Wireless capability (WiFi)
- ✅ Multiple connectivity options

**Ideal Use Cases:**
```
🚁 Drone Operations:
- Collect sensor data during flights
- Process imagery at the edge
- Sync to AWS when connected

🚢 Maritime Operations:
- Ship-to-shore data collection
- Offline processing of maritime data
- Sync during port visits

🏥 Healthcare (Mobile Units):
- Medical imaging in remote locations
- Patient data collection
- HIPAA-compliant edge processing

🎬 Content Creation:
- On-location video processing
- Real-time editing workflows
- Upload to S3 when connected
```

**Configuration Example:**
```bash
# Configure Snowcone for edge processing
aws configure set region us-west-2
aws snowball create-job \
    --job-type EXPORT \
    --address-id ADID1234 \
    --shipping-option NEXT_DAY \
    --snowball-capacity-preference T8
```

### 🏔️ AWS Snowball Edge
*Robust edge computing and data transfer device*

**Device Options:**

**Snowball Edge Storage Optimized:**
- **Storage:** 210 TB (NVMe SSD)
- **Compute:** 52 vCPUs, 208 GB memory
- **Network:** 100 Gbps
- **Best for:** Large data migrations with some processing

**Snowball Edge Compute Optimized:**
- **Storage:** 80 TB (NVMe SSD) + optional GPU
- **Compute:** 104 vCPUs, 416 GB memory  
- **Network:** 100 Gbps + optional 10 Gbps
- **Best for:** ML inference, video analysis, industrial IoT

**Key Features:**
- ✅ NFS v3 file interface
- ✅ S3-compatible API
- ✅ Lambda functions at the edge
- ✅ EC2 instances (AMI support)
- ✅ AES-256 encryption with AWS KMS

**NFS Configuration Deep Dive:**

**What is NFS on Snowball Edge?**
- **NFS (Network File System)** allows you to mount the Snowball Edge as a network drive
- **Protocol:** NFSv3 with AES-256 encryption
- **Integration:** Works with existing backup and file management tools
- **Security:** All data encrypted, integrated with AWS KMS for key management

**NFS Setup Steps:**
```bash
# 1. Configure the Snowball Edge
snowballEdge configure-service --service-id nfs --service-configuration file://nfs-config.json

# 2. Start NFS service
snowballEdge start-service --service-id nfs

# 3. Mount on client (Linux)
sudo mkdir /mnt/snowball-nfs
sudo mount -t nfs 192.168.1.100:/buckets/my-bucket /mnt/snowball-nfs

# 4. Copy files directly
cp -r /data/* /mnt/snowball-nfs/
```

**Enterprise Migration Scenario:**
```
Company: Media Production House
Data: 500 TB of video files (on-premises NAS)
Challenge: Limited internet bandwidth (10 Mbps upload)

Solution with Snowball Edge:
1. Deploy Snowball Edge Storage Optimized (210 TB)
2. Enable NFS service
3. Mount existing NAS backup scripts to Snowball
4. Copy 210 TB → Ship device → Repeat for remaining data
5. Total time: 2 weeks vs 4+ months over internet
```

### 🚛 AWS Snowmobile
*Exabyte-scale data transfer truck*

**Specifications:**
- **Capacity:** 100 PB per truck
- **Security:** 24/7 security personnel, GPS tracking
- **Environment:** Climate-controlled, shock-resistant
- **Timeline:** Weeks to months depending on data volume

**When to Use Snowmobile:**
```
✅ Data volume > 10 PB
✅ Entire data center migrations
✅ Legacy system consolidation
✅ Media archive migrations
✅ Scientific data migrations

❌ Don't use for:
- Small datasets (< 1 PB)
- Distributed locations
- Time-sensitive migrations (< 1 month)
- Locations without truck access
```

**Process Flow:**
```
1. Assessment & Planning (2-4 weeks)
   ├─ Site survey and planning
   ├─ Security clearance
   └─ Network preparation

2. Snowmobile Deployment (1 week)
   ├─ Truck arrives at your location
   ├─ Network connection setup
   └─ Security measures activation

3. Data Transfer (Weeks to months)
   ├─ Parallel data streams
   ├─ Continuous monitoring
   └─ Progress reporting

4. Transport to AWS (1 week)
   ├─ Secure transport
   ├─ GPS tracking
   └─ 24/7 monitoring

5. Data Ingestion (Weeks)
   ├─ Import to S3
   ├─ Data validation
   └─ Customer notification
```

### 🔄 AWS DataSync
*Online data transfer service*

**Key Features:**
- ✅ Up to 10 Gbps transfer speeds
- ✅ Built-in data validation
- ✅ Incremental transfers
- ✅ Bandwidth throttling
- ✅ Detailed transfer logs

**Supported Endpoints:**
```
Sources:
├─ On-premises NFS/SMB shares
├─ Amazon S3 buckets  
├─ Amazon EFS file systems
├─ Amazon FSx file systems
└─ Google Cloud Storage

Destinations:
├─ Amazon S3 (all storage classes)
├─ Amazon EFS
├─ Amazon FSx for Windows File Server
├─ Amazon FSx for Lustre
└─ Amazon FSx for NetApp ONTAP
```

**Transfer Scenarios:**

**Scenario 1: Hybrid File Sync**
```python
# Create DataSync task for daily backup
import boto3

datasync = boto3.client('datasync')

# Create task
response = datasync.create_task(
    SourceLocationArn='arn:aws:datasync:us-east-1:123456789012:location/loc-source',
    DestinationLocationArn='arn:aws:datasync:us-east-1:123456789012:location/loc-dest',
    Options={
        'VerifyMode': 'POINT_IN_TIME_CONSISTENT',
        'OverwriteMode': 'ALWAYS',
        'PreserveDeletedFiles': 'REMOVE',
        'BytesPerSecond': 104857600  # 100 Mbps limit
    },
    Schedule={
        'ScheduleExpression': 'cron(0 2 * * ? *)'  # Daily at 2 AM
    }
)
```

**Scenario 2: One-time Migration**
```bash
# Install DataSync agent on-premises
wget https://s3.amazonaws.com/datasync-downloads/DataSyncAgent.ova

# Create locations
aws datasync create-location-nfs \
    --server-hostname 192.168.1.100 \
    --subdirectory /shared/data \
    --on-prem-config AgentArns=arn:aws:datasync:us-east-1:123456789012:agent/agent-id

aws datasync create-location-s3 \
    --s3-bucket-arn arn:aws:s3:::my-migration-bucket \
    --s3-config BucketAccessRoleArn=arn:aws:iam::123456789012:role/DataSyncS3Role
```

### 📡 AWS Transfer Family
*Managed FTP/SFTP/FTPS service*

**Supported Protocols:**
- **SFTP:** SSH File Transfer Protocol (most secure)
- **FTPS:** FTP over SSL/TLS
- **FTP:** File Transfer Protocol (legacy support)
- **AS2:** Applicability Statement 2 (B2B messaging)

**Key Features:**
- ✅ Fully managed (no server maintenance)
- ✅ Auto-scaling
- ✅ Integration with S3 and EFS
- ✅ Custom identity providers (LDAP, Active Directory)
- ✅ VPC endpoint support

**Authentication Methods:**

**Service-Managed Users:**
```bash
# Create SFTP server
aws transfer create-server \
    --protocols SFTP \
    --identity-provider-type SERVICE_MANAGED \
    --endpoint-type PUBLIC

# Add user
aws transfer create-user \
    --server-id s-1234567890abcdef0 \
    --user-name john.doe \
    --home-directory /my-bucket/john-folder \
    --role arn:aws:iam::123456789012:role/TransferRole \
    --ssh-public-key-body "ssh-rsa AAAAB3NzaC1yc2E..."
```

**Custom Identity Provider (LDAP):**
```python
# Lambda function for custom authentication
import json
import boto3

def lambda_handler(event, context):
    username = event['username']
    password = event['password']
    
    # Authenticate against LDAP
    if authenticate_ldap(username, password):
        return {
            'Role': 'arn:aws:iam::123456789012:role/TransferRole',
            'HomeDirectory': f'/my-bucket/users/{username}',
            'Policy': json.dumps({
                'Version': '2012-10-17',
                'Statement': [{
                    'Effect': 'Allow',
                    'Action': ['s3:GetObject', 's3:PutObject'],
                    'Resource': f'arn:aws:s3:::my-bucket/users/{username}/*'
                }]
            })
        }
    else:
        return {'Role': ''}  # Authentication failed
```

**B2B Integration Example:**
```
Trading Partner Setup:
├─ Create dedicated SFTP server
├─ Configure custom domain (ftp.company.com)
├─ Set up partner-specific users and permissions
├─ Enable CloudWatch logging for compliance
└─ Implement automated file processing workflows
```

### 🌉 AWS Storage Gateway
*Hybrid cloud storage gateway*

**Gateway Types:**

**File Gateway (NFS/SMB):**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   On-Premises   │    │  File Gateway   │    │      AWS S3     │
│   Applications  │◄──►│   (VM/HW)       │◄──►│   Storage       │
│   (NFS/SMB)     │    │                 │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

**Volume Gateway - Stored Volumes:**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Applications  │    │ Volume Gateway  │    │      AWS S3     │
│   (iSCSI)       │◄──►│ Primary: Local  │◄──►│   Async Backup  │
│                 │    │ Backup: S3      │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

**Volume Gateway - Cached Volumes:**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Applications  │    │ Volume Gateway  │    │      AWS S3     │
│   (iSCSI)       │◄──►│ Cache: Local    │◄──►│ Primary Storage │
│                 │    │ Primary: S3     │    │                 │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

**Tape Gateway (VTL):**
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│ Backup Software │    │  Tape Gateway   │    │ S3 / Glacier /  │
│ (Veeam, NetBackup)◄──►│     (VTL)       │◄──►│ Glacier Deep    │
│                 │    │                 │    │   Archive       │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

---

## 🏗️ Migration Architecture Patterns

### Pattern 1: Phased Data Center Migration
```
Phase 1: Assessment & Planning
├─ Data discovery and classification
├─ Network bandwidth analysis
├─ Application dependency mapping
└─ Migration timeline creation

Phase 2: Pilot Migration (Snowball Edge)
├─ Select low-risk datasets (10-50 TB)
├─ Test data validation processes
├─ Verify application connectivity
└─ Refine migration procedures

Phase 3: Bulk Migration (Multiple Snowballs/Snowmobile)
├─ Large datasets (>100 TB)
├─ Parallel data streams
├─ Continuous monitoring
└─ Regular progress reporting

Phase 4: Incremental Sync (DataSync)
├─ Final delta sync
├─ Application cutover
├─ Post-migration validation
└─ Decommission on-premises storage
```

### Pattern 2: Hybrid Cloud Storage Integration
```
┌─────────────────────────────────────────────────────────┐
│                    On-Premises                          │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │    Apps     │  │   Storage   │  │   Backup    │     │
│  │             │  │   Gateway   │  │   Software  │     │
│  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────┬───────────┬───────────────┬───────────────┘
              │           │               │
    ┌─────────▼──────┐   │    ┌─────────▼──────┐
    │ File Gateway    │   │    │ Tape Gateway    │
    │ (NFS/SMB)       │   │    │ (VTL)          │
    └─────────┬──────┘   │    └─────────┬──────┘
              │          │              │
┌─────────────▼──────────▼──────────────▼───────────────┐
│                      AWS Cloud                        │
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐   │
│  │     S3      │  │   Glacier   │  │ Glacier DA  │   │
│  │   Standard  │  │   Flexible  │  │             │   │
│  └─────────────┘  └─────────────┘  └─────────────┘   │
└───────────────────────────────────────────────────────┘
```

---

## 💰 Cost Analysis & Optimization

### Transfer Cost Comparison

**10 TB Dataset Transfer:**

| Method | Time | Direct Cost | Opportunity Cost | Total |
|--------|------|-------------|------------------|-------|
| **Internet (100 Mbps)** | 9 days | $0 | High (9 days downtime) | High |
| **Internet (1 Gbps)** | 22 hours | $0 | Medium (1 day) | Medium |
| **Snowball Edge** | 7-10 days | $300 + shipping | Low (parallel work) | Low |
| **DataSync** | 22 hours | $0.0125/GB = $125 | Medium | Medium |

**100 TB Dataset Transfer:**

| Method | Time | Direct Cost | Opportunity Cost | Total |
|--------|------|-------------|------------------|-------|
| **Internet (1 Gbps)** | 9 days | $0 | Very High | Very High |
| **Multiple Snowballs** | 2 weeks | $1,500 + shipping | Low | Low |
| **Snowmobile** | 4-6 weeks | $5,000/month | Very Low | Very Low |

### Snowball Edge Pricing Breakdown
```
Device Fees (per job):
├─ Snowball Edge Storage Optimized: $300
├─ Snowball Edge Compute Optimized: $400  
├─ Additional days (after 10 free): $15/day
└─ Shipping: $50-200 (depending on location)

Data Transfer:
├─ Import to S3: Free
├─ Export from S3: Standard rates apply
└─ Cross-region transfer: Standard rates
```

### DataSync Pricing Optimization
```bash
# Configure bandwidth throttling to avoid ISP overages
aws datasync update-task \
    --task-arn arn:aws:datasync:region:account:task/task-id \
    --options BytesPerSecond=52428800  # 50 MB/s (400 Mbps)

# Schedule transfers during off-peak hours
aws datasync put-task-schedule \
    --task-arn arn:aws:datasync:region:account:task/task-id \
    --schedule-expression "cron(0 2 * * ? *)"  # 2 AM daily
```

---

## 🔒 Security Best Practices

### Data Encryption Standards

**Snowball Family:**
- ✅ AES-256 encryption (FIPS 140-2 Level 2)
- ✅ Encrypted key management with AWS KMS
- ✅ Secure key erasure after import
- ✅ Tamper-evident enclosures

**DataSync:**
- ✅ TLS 1.2 encryption in transit
- ✅ VPC endpoint support (private connectivity)
- ✅ IAM integration for access control
- ✅ CloudTrail logging for audit

**Transfer Family:**
- ✅ SFTP with SSH key authentication
- ✅ FTPS with SSL/TLS certificates
- ✅ VPC endpoint for internal connectivity
- ✅ Custom identity providers (LDAP/AD)

### Network Security Configuration

**VPC Endpoint Setup for DataSync:**
```bash
# Create VPC endpoint for private DataSync access
aws ec2 create-vpc-endpoint \
    --vpc-id vpc-12345678 \
    --service-name com.amazonaws.region.datasync \
    --vpc-endpoint-type Interface \
    --subnet-ids subnet-12345678 subnet-87654321 \
    --security-group-ids sg-12345678 \
    --policy-document file://datasync-endpoint-policy.json
```

**Security Group Rules for Transfer Family:**
```json
{
    "SecurityGroupRules": [
        {
            "IpPermissions": [
                {
                    "IpProtocol": "tcp",
                    "FromPort": 22,
                    "ToPort": 22,
                    "IpRanges": [
                        {"CidrIp": "10.0.0.0/8", "Description": "Internal network SFTP"}
                    ]
                }
            ]
        }
    ]
}
```

---

## 📊 Monitoring & Troubleshooting

### CloudWatch Metrics

**DataSync Metrics:**
```bash
# Monitor transfer progress
aws cloudwatch get-metric-statistics \
    --namespace AWS/DataSync \
    --metric-name BytesTransferred \
    --dimensions Name=TaskId,Value=task-0123456789abcdef0 \
    --start-time 2023-10-01T00:00:00Z \
    --end-time 2023-10-07T23:59:59Z \
    --period 3600 \
    --statistics Sum
```

**Transfer Family Metrics:**
```python
import boto3
cloudwatch = boto3.client('cloudwatch')

# Create custom dashboard
cloudwatch.put_dashboard(
    DashboardName='TransferFamily-Monitoring',
    DashboardBody=json.dumps({
        "widgets": [
            {
                "type": "metric",
                "properties": {
                    "metrics": [
                        ["AWS/Transfer", "FilesIn", "ServerId", "s-1234567890abcdef0"],
                        [".", "FilesOut", ".", "."],
                        [".", "BytesIn", ".", "."],
                        [".", "BytesOut", ".", "."]
                    ],
                    "period": 300,
                    "stat": "Sum",
                    "region": "us-east-1",
                    "title": "Transfer Activity"
                }
            }
        ]
    })
)
```

### Common Troubleshooting Issues

**Snowball Edge Connectivity:**
```bash
# Check network configuration
snowballEdge describe-device
snowballEdge list-access-keys
snowballEdge associate-s3-access-key --access-key-id AKIAIOSFODNN7EXAMPLE

# Test NFS connectivity
showmount -e 192.168.1.100
mount -v -t nfs 192.168.1.100:/buckets/my-bucket /mnt/test
```

**DataSync Performance Issues:**
```
Common causes:
├─ Network bandwidth limitations
├─ Source storage performance bottlenecks  
├─ Large number of small files
├─ Network latency issues
└─ Insufficient DataSync agent resources

Solutions:
├─ Increase agent instance size
├─ Use multiple parallel tasks
├─ Optimize source storage performance
├─ Implement bandwidth throttling
└─ Archive small files before transfer
```

---

## 🎯 Best Practices Summary

### Pre-Migration Planning
- [ ] Conduct thorough data assessment and classification
- [ ] Test network bandwidth and performance
- [ ] Plan for application dependencies and downtime
- [ ] Establish data validation procedures
- [ ] Create rollback plans for critical systems

### Security & Compliance
- [ ] Implement proper encryption for data at rest and in transit
- [ ] Use IAM roles with least privilege access
- [ ] Enable audit logging (CloudTrail, VPC Flow Logs)
- [ ] Validate compliance requirements (HIPAA, PCI, etc.)
- [ ] Test security controls before full migration

### Performance Optimization
- [ ] Choose appropriate transfer methods based on data volume
- [ ] Use parallel transfers when possible
- [ ] Optimize file formats and compression
- [ ] Monitor and tune network performance
- [ ] Implement proper error handling and retry logic

### Cost Management
- [ ] Compare total cost of ownership (TCO) for different methods
- [ ] Factor in opportunity costs and business impact
- [ ] Use Reserved Instances for predictable workloads
- [ ] Implement lifecycle policies for long-term storage
- [ ] Regular review and optimization of transfer patterns

---

*Last Updated: October 2025 | AWS SAA-C03 Study Guide*