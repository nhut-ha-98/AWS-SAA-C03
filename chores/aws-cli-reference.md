# 🖥️ AWS CLI Reference Guide for SAA-C03

> **Essential AWS CLI commands** để thành thạo cho exam và thực tế

---

## ⚙️ **CLI Setup & Configuration**

### **Installation & Initial Setup**
```bash
# Install AWS CLI v2 (macOS)
curl "https://awscli.amazonaws.com/AWSCLIV2.pkg" -o "AWSCLIV2.pkg"
sudo installer -pkg AWSCLIV2.pkg -target /

# Configure credentials
aws configure
# AWS Access Key ID: YOUR_ACCESS_KEY
# AWS Secret Access Key: YOUR_SECRET_KEY  
# Default region name: us-east-1
# Default output format: json

# Configure multiple profiles
aws configure --profile production
aws configure --profile development

# Use specific profile
aws s3 ls --profile production
export AWS_PROFILE=production
```

### **Essential Configuration Commands**
```bash
# List all configured profiles
aws configure list-profiles

# Show current configuration
aws configure list

# Set default region
aws configure set region us-west-2

# Set output format
aws configure set output table

# Test configuration
aws sts get-caller-identity
```

---

## 🔐 **IAM Commands**

### **Users & Groups Management**
```bash
# List all IAM users
aws iam list-users

# Create IAM user
aws iam create-user --user-name john-doe

# Create IAM group
aws iam create-group --group-name developers

# Add user to group
aws iam add-user-to-group --user-name john-doe --group-name developers

# Create access key for user
aws iam create-access-key --user-name john-doe

# Delete access key
aws iam delete-access-key --user-name john-doe --access-key-id AKIA...

# Change user password
aws iam update-login-profile --user-name john-doe --password NewPassword123
```

### **Policies & Roles**
```bash
# List all policies
aws iam list-policies --scope Local

# Create policy from JSON file
aws iam create-policy \
  --policy-name S3ReadOnlyAccess \
  --policy-document file://policy.json

# Attach policy to user
aws iam attach-user-policy \
  --user-name john-doe \
  --policy-arn arn:aws:iam::123456789012:policy/S3ReadOnlyAccess

# Create IAM role
aws iam create-role \
  --role-name EC2-S3-Role \
  --assume-role-policy-document file://trust-policy.json

# Attach policy to role
aws iam attach-role-policy \
  --role-name EC2-S3-Role \
  --policy-arn arn:aws:iam::aws:policy/AmazonS3ReadOnlyAccess

# List role policies
aws iam list-attached-role-policies --role-name EC2-S3-Role
```

---

## 🖥️ **EC2 Commands**

### **Instance Management**
```bash
# List all instances
aws ec2 describe-instances

# List instances in table format
aws ec2 describe-instances --query 'Reservations[].Instances[].[InstanceId,State.Name,InstanceType,PublicIpAddress]' --output table

# Launch new instance
aws ec2 run-instances \
  --image-id ami-0abcdef1234567890 \
  --count 1 \
  --instance-type t3.micro \
  --key-name my-keypair \
  --security-group-ids sg-12345678 \
  --subnet-id subnet-12345678

# Start instance
aws ec2 start-instances --instance-ids i-1234567890abcdef0

# Stop instance
aws ec2 stop-instances --instance-ids i-1234567890abcdef0

# Terminate instance
aws ec2 terminate-instances --instance-ids i-1234567890abcdef0

# Reboot instance
aws ec2 reboot-instances --instance-ids i-1234567890abcdef0
```

### **AMI Management**
```bash
# List AMIs
aws ec2 describe-images --owners self

# Create AMI from instance
aws ec2 create-image \
  --instance-id i-1234567890abcdef0 \
  --name "MyServerAMI" \
  --description "My server configuration"

# Copy AMI to another region
aws ec2 copy-image \
  --source-region us-east-1 \
  --source-image-id ami-12345678 \
  --name "CopiedAMI" \
  --region us-west-2

# Deregister AMI
aws ec2 deregister-image --image-id ami-12345678
```

### **Security Groups & Key Pairs**
```bash
# List security groups
aws ec2 describe-security-groups

# Create security group
aws ec2 create-security-group \
  --group-name web-servers \
  --description "Security group for web servers" \
  --vpc-id vpc-12345678

# Add rule to security group
aws ec2 authorize-security-group-ingress \
  --group-id sg-12345678 \
  --protocol tcp \
  --port 80 \
  --cidr 0.0.0.0/0

# Create key pair
aws ec2 create-key-pair --key-name MyKeyPair --query 'KeyMaterial' --output text > MyKeyPair.pem
chmod 400 MyKeyPair.pem

# Import existing key pair
aws ec2 import-key-pair --key-name MyExistingKey --public-key-material fileb://~/.ssh/id_rsa.pub
```

---

## 🗄️ **S3 Commands**

### **Bucket Operations**
```bash
# List all buckets
aws s3 ls

# Create bucket
aws s3 mb s3://my-unique-bucket-name

# Delete empty bucket
aws s3 rb s3://my-bucket-name

# Delete bucket with contents
aws s3 rb s3://my-bucket-name --force

# List bucket contents
aws s3 ls s3://my-bucket-name
aws s3 ls s3://my-bucket-name/folder/ --recursive

# Sync directory with bucket
aws s3 sync ./local-folder s3://my-bucket-name/remote-folder
aws s3 sync s3://my-bucket-name/remote-folder ./local-folder
```

### **Object Operations**
```bash
# Upload file
aws s3 cp file.txt s3://my-bucket-name/
aws s3 cp file.txt s3://my-bucket-name/folder/newname.txt

# Download file
aws s3 cp s3://my-bucket-name/file.txt ./
aws s3 cp s3://my-bucket-name/file.txt ./downloaded-file.txt

# Move file
aws s3 mv s3://my-bucket-name/old-location.txt s3://my-bucket-name/new-location.txt

# Remove file
aws s3 rm s3://my-bucket-name/file.txt

# Remove all objects in folder
aws s3 rm s3://my-bucket-name/folder/ --recursive
```

### **S3 Configuration**
```bash
# Set bucket versioning
aws s3api put-bucket-versioning \
  --bucket my-bucket-name \
  --versioning-configuration Status=Enabled

# Configure bucket encryption
aws s3api put-bucket-encryption \
  --bucket my-bucket-name \
  --server-side-encryption-configuration '{
    "Rules": [{
      "ApplyServerSideEncryptionByDefault": {
        "SSEAlgorithm": "AES256"
      }
    }]
  }'

# Set lifecycle policy
aws s3api put-bucket-lifecycle-configuration \
  --bucket my-bucket-name \
  --lifecycle-configuration file://lifecycle.json

# Enable static website hosting
aws s3api put-bucket-website \
  --bucket my-bucket-name \
  --website-configuration '{
    "IndexDocument": {"Suffix": "index.html"},
    "ErrorDocument": {"Key": "error.html"}
  }'
```

---

## 🌐 **VPC & Networking**

### **VPC Management**
```bash
# List VPCs
aws ec2 describe-vpcs

# Create VPC
aws ec2 create-vpc --cidr-block 10.0.0.0/16

# Create subnet
aws ec2 create-subnet \
  --vpc-id vpc-12345678 \
  --cidr-block 10.0.1.0/24 \
  --availability-zone us-east-1a

# Create internet gateway
aws ec2 create-internet-gateway

# Attach internet gateway to VPC
aws ec2 attach-internet-gateway \
  --internet-gateway-id igw-12345678 \
  --vpc-id vpc-12345678

# Create route table
aws ec2 create-route-table --vpc-id vpc-12345678

# Create route to internet gateway
aws ec2 create-route \
  --route-table-id rtb-12345678 \
  --destination-cidr-block 0.0.0.0/0 \
  --gateway-id igw-12345678

# Associate route table with subnet
aws ec2 associate-route-table \
  --route-table-id rtb-12345678 \
  --subnet-id subnet-12345678
```

### **Load Balancers**
```bash
# Create Application Load Balancer
aws elbv2 create-load-balancer \
  --name my-alb \
  --subnets subnet-12345678 subnet-87654321 \
  --security-groups sg-12345678

# Create target group
aws elbv2 create-target-group \
  --name my-targets \
  --protocol HTTP \
  --port 80 \
  --vpc-id vpc-12345678

# Register targets
aws elbv2 register-targets \
  --target-group-arn arn:aws:elasticloadbalancing:region:account:targetgroup/my-targets/1234567890123456 \
  --targets Id=i-1234567890abcdef0,Port=80

# Create listener
aws elbv2 create-listener \
  --load-balancer-arn arn:aws:elasticloadbalancing:region:account:loadbalancer/app/my-alb/1234567890123456 \
  --protocol HTTP \
  --port 80 \
  --default-actions Type=forward,TargetGroupArn=arn:aws:elasticloadbalancing:region:account:targetgroup/my-targets/1234567890123456
```

---

## 🗃️ **RDS Commands**

### **Database Management**
```bash
# List DB instances
aws rds describe-db-instances

# Create DB instance
aws rds create-db-instance \
  --db-instance-identifier mydb \
  --db-instance-class db.t3.micro \
  --engine mysql \
  --master-username admin \
  --master-user-password mypassword \
  --allocated-storage 20

# Create DB snapshot
aws rds create-db-snapshot \
  --db-instance-identifier mydb \
  --db-snapshot-identifier mydb-snapshot-$(date +%Y%m%d)

# Restore from snapshot
aws rds restore-db-instance-from-db-snapshot \
  --db-instance-identifier mydb-restored \
  --db-snapshot-identifier mydb-snapshot-20240925

# Modify DB instance
aws rds modify-db-instance \
  --db-instance-identifier mydb \
  --allocated-storage 40 \
  --apply-immediately

# Delete DB instance
aws rds delete-db-instance \
  --db-instance-identifier mydb \
  --skip-final-snapshot
```

### **Aurora Clusters**
```bash
# Create Aurora cluster
aws rds create-db-cluster \
  --db-cluster-identifier myaurora \
  --engine aurora-mysql \
  --master-username admin \
  --master-user-password mypassword

# Create cluster instance
aws rds create-db-instance \
  --db-instance-identifier myaurora-instance-1 \
  --db-instance-class db.r5.large \
  --engine aurora-mysql \
  --db-cluster-identifier myaurora

# Create cluster snapshot
aws rds create-db-cluster-snapshot \
  --db-cluster-identifier myaurora \
  --db-cluster-snapshot-identifier myaurora-snapshot
```

---

## ⚡ **Lambda Commands**

### **Function Management**
```bash
# List functions
aws lambda list-functions

# Create function
aws lambda create-function \
  --function-name my-function \
  --runtime python3.9 \
  --role arn:aws:iam::123456789012:role/lambda-execution-role \
  --handler index.handler \
  --zip-file fileb://function.zip

# Update function code
aws lambda update-function-code \
  --function-name my-function \
  --zip-file fileb://updated-function.zip

# Update function configuration
aws lambda update-function-configuration \
  --function-name my-function \
  --timeout 30 \
  --memory-size 256

# Invoke function
aws lambda invoke \
  --function-name my-function \
  --payload '{"key": "value"}' \
  response.json

# Get function logs
aws logs filter-log-events \
  --log-group-name /aws/lambda/my-function \
  --start-time $(date -d '1 hour ago' +%s)000
```

### **Event Sources**
```bash
# Create event source mapping (SQS)
aws lambda create-event-source-mapping \
  --function-name my-function \
  --event-source-arn arn:aws:sqs:region:account:queue-name \
  --batch-size 10

# Add S3 trigger permission
aws lambda add-permission \
  --function-name my-function \
  --statement-id s3-trigger \
  --action lambda:InvokeFunction \
  --principal s3.amazonaws.com \
  --source-arn arn:aws:s3:::my-bucket
```

---

## 📊 **CloudWatch Commands**

### **Metrics & Alarms**
```bash
# List metrics
aws cloudwatch list-metrics

# Get metric statistics
aws cloudwatch get-metric-statistics \
  --namespace AWS/EC2 \
  --metric-name CPUUtilization \
  --dimensions Name=InstanceId,Value=i-1234567890abcdef0 \
  --start-time 2024-09-25T00:00:00Z \
  --end-time 2024-09-25T23:59:59Z \
  --period 3600 \
  --statistics Average

# Put custom metric
aws cloudwatch put-metric-data \
  --namespace MyApp/Performance \
  --metric-data MetricName=ResponseTime,Value=150,Unit=Milliseconds

# Create alarm
aws cloudwatch put-metric-alarm \
  --alarm-name cpu-alarm \
  --alarm-description "CPU usage alarm" \
  --metric-name CPUUtilization \
  --namespace AWS/EC2 \
  --statistic Average \
  --period 300 \
  --threshold 80 \
  --comparison-operator GreaterThanThreshold \
  --evaluation-periods 2

# List alarms
aws cloudwatch describe-alarms
```

### **Logs Management**
```bash
# List log groups
aws logs describe-log-groups

# Create log group
aws logs create-log-group --log-group-name /myapp/application

# Put log events
aws logs put-log-events \
  --log-group-name /myapp/application \
  --log-stream-name stream1 \
  --log-events timestamp=$(date +%s)000,message="Test log message"

# Start query
aws logs start-query \
  --log-group-name /myapp/application \
  --start-time $(date -d '1 hour ago' +%s) \
  --end-time $(date +%s) \
  --query-string 'fields @timestamp, @message | filter @message like /ERROR/'
```

---

## 🔄 **Auto Scaling**

### **Auto Scaling Groups**
```bash
# Create launch template
aws ec2 create-launch-template \
  --launch-template-name my-template \
  --launch-template-data '{
    "ImageId":"ami-12345678",
    "InstanceType":"t3.micro",
    "SecurityGroupIds":["sg-12345678"],
    "IamInstanceProfile":{"Name":"MyInstanceProfile"}
  }'

# Create Auto Scaling group
aws autoscaling create-auto-scaling-group \
  --auto-scaling-group-name my-asg \
  --launch-template LaunchTemplateName=my-template,Version=1 \
  --min-size 1 \
  --max-size 3 \
  --desired-capacity 2 \
  --vpc-zone-identifier "subnet-12345678,subnet-87654321"

# Update Auto Scaling group
aws autoscaling update-auto-scaling-group \
  --auto-scaling-group-name my-asg \
  --min-size 2 \
  --max-size 5 \
  --desired-capacity 3

# Create scaling policy
aws autoscaling put-scaling-policy \
  --auto-scaling-group-name my-asg \
  --policy-name scale-up-policy \
  --scaling-adjustment 1 \
  --adjustment-type ChangeInCapacity
```

---

## 🎯 **Quick Reference Cheat Sheet**

### **Most Used Commands**
```bash
# Check AWS CLI version
aws --version

# Get account identity
aws sts get-caller-identity

# List all regions
aws ec2 describe-regions --query 'Regions[].RegionName' --output text

# List all availability zones
aws ec2 describe-availability-zones --query 'AvailabilityZones[].ZoneName' --output text

# Get AWS service endpoints
aws ec2 describe-regions --query 'Regions[].[RegionName,Endpoint]' --output table

# Format output options
--output json    # Default JSON format
--output table   # Human readable table
--output text    # Tab-delimited text
--output yaml    # YAML format
```

### **Useful Filters & Queries**
```bash
# Filter EC2 instances by state
aws ec2 describe-instances --filters "Name=instance-state-name,Values=running"

# Query specific fields
aws ec2 describe-instances --query 'Reservations[].Instances[].[InstanceId,State.Name]'

# Filter S3 objects by size
aws s3api list-objects-v2 --bucket my-bucket --query 'Contents[?Size > `1048576`]'

# Get latest AMI
aws ec2 describe-images \
  --owners amazon \
  --filters "Name=name,Values=amzn2-ami-hvm-*" \
  --query 'Images | sort_by(@, &CreationDate) | [-1]'
```

### **Common Troubleshooting**
```bash
# Check AWS credentials
aws configure list

# Test permissions
aws sts get-caller-identity

# Debug API calls
aws s3 ls --debug

# Validate JSON syntax
aws iam create-policy --policy-name test --policy-document file://policy.json --dry-run

# Get help for any command
aws ec2 help
aws s3 cp help
```

---

## 💡 **Pro Tips for SAA-C03**

### **Exam-Focused Commands**
1. **Multi-AZ RDS**: `aws rds create-db-instance --multi-az`
2. **Cross-Region S3 Replication**: `aws s3api put-bucket-replication`
3. **EBS Snapshot**: `aws ec2 create-snapshot --volume-id vol-xxx`
4. **CloudFront Distribution**: `aws cloudfront create-distribution`
5. **Route53 Health Check**: `aws route53 create-health-check`

### **Performance Optimization**
```bash
# Use pagination for large result sets
aws s3api list-objects-v2 --bucket large-bucket --page-size 100

# Parallel uploads for large files
aws s3 cp large-file.zip s3://my-bucket/ --cli-write-timeout 0

# Use filters to reduce data transfer
aws ec2 describe-instances --filters "Name=tag:Environment,Values=Production"
```

### **Security Best Practices**
```bash
# Use IAM roles instead of access keys
aws sts assume-role --role-arn arn:aws:iam::account:role/MyRole --role-session-name session1

# Enable MFA for sensitive operations
aws sts get-session-token --serial-number arn:aws:iam::account:mfa/user --token-code 123456

# Rotate access keys regularly
aws iam create-access-key --user-name myuser
aws iam update-access-key --user-name myuser --access-key-id AKIA... --status Inactive
```

---

**🖥️ Master these CLI commands để confident trong SAA-C03 exam và real-world AWS operations! 🚀**