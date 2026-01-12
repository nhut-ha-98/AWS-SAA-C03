# AWS Security Services Guide 🔒

*Comprehensive guide to AWS security services, threat detection, and compliance frameworks*

## 🎯 Overview

AWS provides a comprehensive suite of security services to protect your applications, data, and infrastructure. This guide covers threat detection, network security, identity management, and compliance tools to help you build secure, resilient architectures.

---

## 🚀 Quick Security Service Selection Table

| Category | Service | Detection Type | Response Capability | Best For |
|----------|---------|----------------|-------------------|----------|
| **Threat Detection** | GuardDuty | ML-based behavioral analysis | Alerting only | Automated threat intelligence |
| **Network Security** | Traffic Mirroring | Deep packet inspection | Manual analysis | Custom security tools/IDS |
| **Network Firewall** | AWS Network Firewall | Rule-based inspection + IPS | Block/Allow/Alert | Managed network protection |
| **Firewall Management** | Firewall Manager | Centralized policy management | Policy enforcement | Multi-account firewall governance |
| **Application Security** | WAF (Web Application Firewall) | Layer 7 filtering | Block/Rate limit | Web application protection |
| **DDoS Protection** | Shield Standard/Advanced | Traffic analysis | Automatic mitigation | DDoS attack protection |
| **Identity Security** | IAM Access Analyzer | Resource access analysis | Policy recommendations | Least privilege validation |
| **Data Security** | Macie | ML-based data classification | Data discovery/alerting | Sensitive data protection |
| **Infrastructure Security** | Config | Configuration compliance | Remediation workflows | Compliance monitoring |
| **Secret Management** | Secrets Manager | Credential lifecycle | Automatic rotation | API keys, database credentials |

---

## 🌳 Security Service Decision Tree

```
What type of security challenge do you need to address?
│
├── Threat Detection & Response
│   │
│   ├── Do you need automated threat intelligence?
│   │   │
│   │   ├── Yes → ✅ GuardDuty (ML-based detection)
│   │   └── No → Continue to manual analysis ↓
│   │
│   ├── Do you need custom threat analysis?
│   │   │
│   │   ├── Yes → ✅ Traffic Mirroring + Custom IDS/IPS
│   │   └── No → ✅ GuardDuty + Security Hub
│   │
│   └── Do you need incident response automation?
│       │
│       ├── Yes → GuardDuty → EventBridge → Lambda/Step Functions
│       └── No → GuardDuty → SNS notifications
│
├── Network Security
│   │
│   ├── What layer do you need to protect?
│   │   │
│   │   ├── Application Layer (L7) → ✅ WAF
│   │   ├── Network Layer (L3/L4) → ✅ Network Firewall
│   │   └── Both → WAF + Network Firewall
│   │
│   ├── Do you need centralized management?
│   │   │
│   │   ├── Yes (multi-account) → ✅ Firewall Manager
│   │   └── No (single account) → Individual service management
│   │
│   └── Do you need deep packet inspection?
│       │
│       ├── Yes → ✅ Network Firewall (managed) OR Traffic Mirroring (custom)
│       └── No → Security Groups + NACLs
│
├── Identity & Access Management
│   │
│   ├── What aspect of IAM needs securing?
│   │   │
│   │   ├── Policy analysis → ✅ IAM Access Analyzer
│   │   ├── Credential management → ✅ Secrets Manager
│   │   ├── User authentication → ✅ Cognito or IAM Identity Center
│   │   └── Cross-account access → ✅ Organizations + IAM roles
│   │
│   └── Do you need policy recommendations?
│       │
│       ├── Yes → ✅ Access Analyzer + CloudTrail insights
│       └── No → Manual policy review
│
├── Data Protection
│   │
│   ├── What type of data needs protection?
│   │   │
│   │   ├── Sensitive/PII data → ✅ Macie (ML-based classification)
│   │   ├── Application secrets → ✅ Secrets Manager
│   │   ├── Database data → ✅ RDS encryption + KMS
│   │   └── File storage → ✅ S3 encryption + KMS
│   │
│   └── Do you need automated data discovery?
│       │
│       ├── Yes → ✅ Macie for S3 data classification
│       └── No → Manual classification with tags
│
└── Compliance & Governance
    │
    ├── What compliance framework?
    │   │
    │   ├── PCI DSS → Config + Security Hub + GuardDuty
    │   ├── SOC 2 → Config + CloudTrail + KMS
    │   ├── HIPAA → Macie + Config + KMS + VPC
    │   └── Custom → Config rules + Security Hub
    │
    └── Do you need continuous monitoring?
        │
        ├── Yes → ✅ Config + Security Hub + EventBridge
        └── No → Periodic compliance reports
```

---

## 📋 Service Deep Dive

### 🛡️ Amazon GuardDuty
*Intelligent threat detection service*

**Key Features:**
- ✅ ML-based behavioral analysis
- ✅ Multiple data sources (DNS, VPC Flow Logs, CloudTrail)
- ✅ Threat intelligence feeds
- ✅ Anomaly detection
- ✅ Integration with Security Hub

**Threat Detection Categories:**

| Category | Detection Type | Example Threats |
|----------|---------------|-----------------|
| **Reconnaissance** | Unusual API calls, port scanning | Port probes, unusual DNS requests |
| **Instance Compromise** | Malware, cryptocurrency mining | Backdoor communication, data exfiltration |
| **Account Compromise** | Credential misuse, privilege escalation | Unusual console logins, API usage patterns |
| **Bucket Compromise** | Suspicious S3 activity | Data exfiltration, unauthorized access |
| **Malware** | Domain reputation, known bad IPs | C&C communication, malware downloads |

**Configuration & Setup:**
```python
import boto3
import json

guardduty = boto3.client('guardduty')

# Enable GuardDuty
detector = guardduty.create_detector(
    Enable=True,
    FindingPublishingFrequency='FIFTEEN_MINUTES',  # FIFTEEN_MINUTES, ONE_HOUR, SIX_HOURS
    DataSources={
        'S3Logs': {
            'Enable': True
        },
        'KubernetesConfiguration': {
            'AuditLogs': {
                'Enable': True
            }
        },
        'MalwareProtection': {
            'ScanEc2InstanceWithFindings': {
                'EbsVolumes': True
            }
        }
    }
)

detector_id = detector['DetectorId']

# Create custom threat intelligence set
threat_intel = guardduty.create_threat_intel_set(
    DetectorId=detector_id,
    Name='CustomThreatIntel',
    Format='TXT',  # TXT, STIX, OTX_CSV, ALIEN_VAULT, PROOF_POINT, FIRE_EYE
    Location='s3://my-security-bucket/threat-intel/bad-ips.txt',
    Activate=True
)

# Create IP whitelist
ip_set = guardduty.create_ip_set(
    DetectorId=detector_id,
    Name='TrustedIPs',
    Format='TXT',
    Location='s3://my-security-bucket/whitelist/trusted-ips.txt',
    Activate=True
)
```

**Automated Response Setup:**
```yaml
# CloudFormation template for automated GuardDuty response
GuardDutyEventRule:
  Type: AWS::Events::Rule
  Properties:
    Description: "Trigger on high severity GuardDuty findings"
    EventPattern:
      source: ["aws.guardduty"]
      detail-type: ["GuardDuty Finding"]
      detail:
        severity: [7, 8, 9]  # High severity findings only
    State: ENABLED
    Targets:
      - Arn: !GetAtt SecurityResponseFunction.Arn
        Id: SecurityResponseTarget

SecurityResponseFunction:
  Type: AWS::Lambda::Function
  Properties:
    FunctionName: GuardDutyAutoResponse
    Runtime: python3.9
    Handler: index.lambda_handler
    Code:
      ZipFile: |
        import boto3
        import json
        
        def lambda_handler(event, context):
            # Parse GuardDuty finding
            finding = event['detail']
            finding_type = finding['type']
            severity = finding['severity']
            
            # Automated responses based on finding type
            if 'CryptoCurrency' in finding_type:
                # Block instance and isolate
                isolate_instance(finding)
                
            elif 'Backdoor' in finding_type:
                # Create security group to isolate
                quarantine_instance(finding)
                
            elif 'UnauthorizedAPICall' in finding_type:
                # Disable user/role temporarily
                disable_compromised_credentials(finding)
            
            # Always send to Security Hub and SNS
            send_to_security_hub(finding)
            send_alert_notification(finding)
            
            return {'statusCode': 200}
```

**Finding Analysis Example:**
```python
def analyze_guardduty_findings():
    guardduty = boto3.client('guardduty')
    
    # Get all findings from last 7 days
    findings = guardduty.list_findings(
        DetectorId='detector-id',
        FindingCriteria={
            'Criterion': {
                'updatedAt': {
                    'Gte': int((datetime.now() - timedelta(days=7)).timestamp() * 1000)
                },
                'severity': {
                    'Gte': 4.0  # Medium severity and above
                }
            }
        }
    )
    
    # Get detailed finding information
    finding_details = guardduty.get_findings(
        DetectorId='detector-id',
        FindingIds=findings['FindingIds']
    )
    
    # Analyze patterns
    finding_stats = {}
    for finding in finding_details['Findings']:
        finding_type = finding['Type']
        severity = finding['Severity']
        
        if finding_type not in finding_stats:
            finding_stats[finding_type] = {
                'count': 0,
                'max_severity': 0,
                'instances': []
            }
        
        finding_stats[finding_type]['count'] += 1
        finding_stats[finding_type]['max_severity'] = max(
            finding_stats[finding_type]['max_severity'], 
            severity
        )
        
        if finding.get('Service', {}).get('ResourceRole') == 'TARGET':
            instance_id = finding.get('Resource', {}).get('InstanceDetails', {}).get('InstanceId')
            if instance_id:
                finding_stats[finding_type]['instances'].append(instance_id)
    
    return finding_stats
```

### 🔍 VPC Traffic Mirroring
*Deep packet inspection for custom analysis*

**Key Concepts:**
- **Mirror Source:** ENI, Network Load Balancer, or Gateway Load Balancer endpoint
- **Mirror Target:** ENI or Network Load Balancer for analysis tools
- **Mirror Filter:** Rules to specify which traffic to capture
- **Mirror Session:** Active configuration linking source, target, and filter

**Use Cases:**
```
✅ Custom IDS/IPS deployment (Suricata, Snort)
✅ Network forensics and troubleshooting
✅ Compliance monitoring and audit trails
✅ Performance monitoring and optimization
✅ Security research and threat hunting
```

**Configuration Setup:**
```python
import boto3

ec2 = boto3.client('ec2')

# Create traffic mirror filter
mirror_filter = ec2.create_traffic_mirror_filter(
    Description='Security monitoring filter',
    TagSpecifications=[
        {
            'ResourceType': 'traffic-mirror-filter',
            'Tags': [
                {
                    'Key': 'Name',
                    'Value': 'SecurityMonitoringFilter'
                }
            ]
        }
    ]
)

filter_id = mirror_filter['TrafficMirrorFilter']['TrafficMirrorFilterId']

# Add ingress rules to capture specific traffic
ingress_rules = [
    {
        'TrafficDirection': 'ingress',
        'RuleNumber': 100,
        'RuleAction': 'accept',
        'Protocol': 6,  # TCP
        'DestinationCidrBlock': '10.0.0.0/16',
        'SourceCidrBlock': '0.0.0.0/0',
        'DestinationPortRange': {'FromPort': 80, 'ToPort': 80}
    },
    {
        'TrafficDirection': 'ingress', 
        'RuleNumber': 110,
        'RuleAction': 'accept',
        'Protocol': 6,  # TCP
        'DestinationCidrBlock': '10.0.0.0/16',
        'SourceCidrBlock': '0.0.0.0/0',
        'DestinationPortRange': {'FromPort': 443, 'ToPort': 443}
    }
]

for rule in ingress_rules:
    ec2.create_traffic_mirror_filter_rule(
        TrafficMirrorFilterId=filter_id,
        **rule
    )

# Create traffic mirror target (analysis instance)
mirror_target = ec2.create_traffic_mirror_target(
    NetworkInterfaceId='eni-security-analysis-instance',
    Description='Security analysis target'
)

target_id = mirror_target['TrafficMirrorTarget']['TrafficMirrorTargetId']

# Create mirror session for production web servers
mirror_session = ec2.create_traffic_mirror_session(
    NetworkInterfaceId='eni-web-server-1',  # Source ENI
    TrafficMirrorTargetId=target_id,
    TrafficMirrorFilterId=filter_id,
    SessionNumber=1,
    PacketLength=1500,  # Full packet capture
    Description='Web server security monitoring'
)
```

**Analysis Tools Integration:**
```bash
# Example: Setting up Suricata for traffic analysis
sudo yum update -y
sudo yum install -y epel-release
sudo yum install -y suricata

# Configure Suricata for mirrored traffic
sudo tee /etc/suricata/suricata.yaml > /dev/null <<EOF
vars:
  address-groups:
    HOME_NET: "[10.0.0.0/16]"
    EXTERNAL_NET: "!$HOME_NET"

af-packet:
  - interface: eth1  # Interface receiving mirrored traffic
    cluster-id: 99
    cluster-type: cluster_flow
    defrag: yes

detect-engine:
  - rule-files:
      - suricata.rules
      - /etc/suricata/rules/*.rules

outputs:
  - fast:
      enabled: yes
      filename: fast.log
  - eve-log:
      enabled: yes
      filetype: regular
      filename: eve.json
      types:
        - alert
        - http
        - dns
        - tls
EOF

# Start Suricata
sudo systemctl enable suricata
sudo systemctl start suricata

# Monitor alerts in real-time
sudo tail -f /var/log/suricata/fast.log
```

### 🔥 AWS Network Firewall
*Managed network security service*

**Key Features:**
- ✅ Stateful and stateless filtering
- ✅ Intrusion Prevention System (IPS)
- ✅ Domain-based filtering
- ✅ TLS inspection
- ✅ Managed rule groups from AWS and partners

**Rule Types:**

| Rule Type | Purpose | Example Use Case |
|-----------|---------|------------------|
| **Stateless Rules** | Fast packet filtering | Block known bad IPs, allow specific ports |
| **Stateful Rules** | Connection-aware filtering | Allow outbound HTTPS, block return traffic |
| **Domain Rules** | DNS-based filtering | Block malware domains, allow business domains |
| **IPS Rules** | Signature-based detection | Detect/block known attack patterns |

**Network Firewall Setup:**
```yaml
# CloudFormation template for Network Firewall
NetworkFirewall:
  Type: AWS::NetworkFirewall::Firewall
  Properties:
    FirewallName: ProductionNetworkFirewall
    FirewallPolicyArn: !Ref NetworkFirewallPolicy
    VpcId: !Ref VPC
    SubnetMappings:
      - SubnetId: !Ref FirewallSubnet1
      - SubnetId: !Ref FirewallSubnet2
    Tags:
      - Key: Environment
        Value: Production

NetworkFirewallPolicy:
  Type: AWS::NetworkFirewall::FirewallPolicy
  Properties:
    FirewallPolicyName: ProductionFirewallPolicy
    FirewallPolicy:
      StatelessDefaultActions:
        - aws:forward_to_sfe  # Send to stateful engine
      StatelessFragmentDefaultActions:
        - aws:forward_to_sfe
      StatefulRuleGroupReferences:
        - ResourceArn: !Ref MalwareDetectionRuleGroup
        - ResourceArn: !Ref WebSecurityRuleGroup
      StatelessRuleGroupReferences:
        - ResourceArn: !Ref BasicFilteringRuleGroup
          Priority: 1

# Stateful rule group for web security
WebSecurityRuleGroup:
  Type: AWS::NetworkFirewall::RuleGroup
  Properties:
    RuleGroupName: WebSecurityRules
    Type: STATEFUL
    Capacity: 100
    RuleGroup:
      RulesSource:
        RulesString: |
          alert http any any -> any any (msg:"Potential SQL Injection"; content:"union select"; nocase; sid:1001; rev:1;)
          alert http any any -> any any (msg:"Potential XSS Attack"; content:"<script"; nocase; sid:1002; rev:1;)
          pass http any any -> any 80 (msg:"Allow HTTP"; sid:1003; rev:1;)
          pass http any any -> any 443 (msg:"Allow HTTPS"; sid:1004; rev:1;)
      StatefulRuleOptions:
        RuleOrder: STRICT_ORDER

# Domain-based filtering
DomainFilteringRuleGroup:
  Type: AWS::NetworkFirewall::RuleGroup
  Properties:
    RuleGroupName: DomainFiltering
    Type: STATEFUL
    Capacity: 50
    RuleGroup:
      RuleVariables:
        IPSets:
          HOME_NET:
            Definition:
              - 10.0.0.0/16
      RulesSource:
        RulesSourceList:
          TargetTypes:
            - HTTP_HOST
            - TLS_SNI
          Targets:
            - ".malware-domain.com"
            - ".suspicious-site.org"
          GeneratedRulesType: DENYLIST
```

**Integration with Route Tables:**
```python
import boto3

ec2 = boto3.client('ec2')

# Update route tables to direct traffic through Network Firewall
def update_routes_for_firewall(vpc_id, firewall_endpoint_id):
    # Get all route tables in VPC
    route_tables = ec2.describe_route_tables(
        Filters=[
            {'Name': 'vpc-id', 'Values': [vpc_id]}
        ]
    )
    
    for rt in route_tables['RouteTables']:
        rt_id = rt['RouteTableId']
        
        # Add route to send internet traffic through firewall
        try:
            ec2.create_route(
                RouteTableId=rt_id,
                DestinationCidrBlock='0.0.0.0/0',
                VpcEndpointId=firewall_endpoint_id
            )
            print(f"Updated route table {rt_id}")
        except Exception as e:
            print(f"Failed to update route table {rt_id}: {e}")

# Monitor firewall metrics
def monitor_firewall_metrics(firewall_name):
    cloudwatch = boto3.client('cloudwatch')
    
    metrics = [
        'DroppedPackets',
        'PassedPackets',
        'InvalidDroppedPackets',
        'OtherDroppedPackets'
    ]
    
    for metric in metrics:
        response = cloudwatch.get_metric_statistics(
            Namespace='AWS/NetworkFirewall',
            MetricName=metric,
            Dimensions=[
                {
                    'Name': 'Firewall',
                    'Value': firewall_name
                }
            ],
            StartTime=datetime.utcnow() - timedelta(hours=1),
            EndTime=datetime.utcnow(),
            Period=300,
            Statistics=['Sum']
        )
        
        print(f"{metric}: {response['Datapoints']}")
```

### 🛠️ AWS Firewall Manager
*Centralized firewall policy management*

**Key Features:**
- ✅ Centralized policy management across accounts
- ✅ Automatic policy enforcement
- ✅ Compliance monitoring and reporting
- ✅ Support for WAF, Shield Advanced, Security Groups, Network Firewall
- ✅ Resource-based policy application

**Policy Types:**
```
1. AWS WAF Policies:
   ├─ Classic WAF rules
   ├─ WAF v2 web ACLs
   └─ Rate-based rules

2. Shield Advanced Policies:
   ├─ DDoS response team engagement
   ├─ Cost protection
   └─ Advanced metrics

3. Security Group Policies:
   ├─ Common security groups
   ├─ Content audit policies
   └─ Usage audit policies

4. Network Firewall Policies:
   ├─ Firewall deployment
   ├─ Rule group management
   └─ Logging configuration

5. DNS Firewall Policies:
   ├─ Domain filtering
   ├─ Query logging
   └─ Response policies
```

**Firewall Manager Setup:**
```python
import boto3

fms = boto3.client('fms')

# Create WAF policy for all accounts
waf_policy = {
    'PolicyName': 'OrganizationWAFPolicy',
    'SecurityServiceType': 'WAFV2',
    'ResourceType': 'AWS::CloudFront::Distribution',
    'ResourceTags': [
        {
            'Key': 'Environment',
            'Value': 'Production'
        }
    ],
    'ExcludeResourceTags': False,
    'RemediationEnabled': True,
    'IncludeMap': {
        'ACCOUNT': ['123456789012', '123456789013']  # Specific accounts
    },
    'SecurityServicePolicyData': {
        'Type': 'WAFV2',
        'ManagedServiceData': json.dumps({
            'type': 'WAFV2',
            'preProcessRuleGroups': [
                {
                    'ruleGroupArn': 'arn:aws:wafv2:us-east-1:aws:managed/aws-managed-rule-set/AWSManagedRulesCommonRuleSet',
                    'overrideAction': {'type': 'NONE'},
                    'managedRuleGroupIdentifier': {
                        'version': None,
                        'vendorName': 'AWS',
                        'managedRuleGroupName': 'AWSManagedRulesCommonRuleSet'
                    }
                }
            ],
            'defaultAction': {'type': 'ALLOW'}
        })
    }
}

# Create the policy
policy_response = fms.put_policy(Policy=waf_policy)
print(f"Created policy: {policy_response['Policy']['PolicyArn']}")

# Create Security Group audit policy
sg_audit_policy = {
    'PolicyName': 'SecurityGroupAuditPolicy',
    'SecurityServiceType': 'SECURITY_GROUPS_CONTENT_AUDIT',
    'ResourceType': 'AWS::EC2::SecurityGroup',
    'RemediationEnabled': False,  # Audit only, no automatic remediation
    'SecurityServicePolicyData': {
        'Type': 'SECURITY_GROUPS_CONTENT_AUDIT',
        'ManagedServiceData': json.dumps({
            'type': 'SECURITY_GROUPS_CONTENT_AUDIT',
            'securityGroupAction': 'ALLOW',
            'securityGroups': [
                {
                    'id': 'sg-baseline-web',
                    'rules': [
                        {
                            'ipPermissions': [
                                {
                                    'ipProtocol': 'tcp',
                                    'fromPort': 80,
                                    'toPort': 80,
                                    'ipRanges': [{'cidrIp': '0.0.0.0/0'}]
                                },
                                {
                                    'ipProtocol': 'tcp',
                                    'fromPort': 443,
                                    'toPort': 443,
                                    'ipRanges': [{'cidrIp': '0.0.0.0/0'}]
                                }
                            ]
                        }
                    ]
                }
            ]
        })
    }
}

# Monitor compliance across accounts
def check_compliance_status():
    # Get all policies
    policies = fms.list_policies()
    
    for policy in policies['PolicyList']:
        policy_id = policy['PolicyId']
        
        # Get compliance status
        compliance = fms.get_compliance_detail(
            PolicyId=policy_id,
            MemberAccount='123456789012'  # Check specific account
        )
        
        print(f"Policy: {policy['PolicyName']}")
        print(f"Compliance Status: {compliance['PolicyComplianceDetail']['EvaluationLimitExceeded']}")
        
        # Check violations
        if compliance['PolicyComplianceDetail']['Violators']:
            print("Violations found:")
            for violator in compliance['PolicyComplianceDetail']['Violators']:
                print(f"  Resource: {violator['ResourceId']}")
                print(f"  Type: {violator['ResourceType']}")
                print(f"  Violation: {violator['ViolationReason']}")
```

---

## 🏗️ Security Architecture Patterns

### Pattern 1: Defense in Depth
```
Internet
    ↓
┌─────────────────────┐
│    CloudFront       │ ← WAF rules, DDoS protection
│   + AWS Shield     │
└─────────┬───────────┘
          ↓
┌─────────────────────┐
│  Application        │ ← Layer 7 filtering
│  Load Balancer      │
│      + WAF          │
└─────────┬───────────┘
          ↓
┌─────────────────────┐
│  Network Firewall   │ ← IPS, domain filtering
│  (Inspection VPC)   │
└─────────┬───────────┘
          ↓
┌─────────────────────┐
│   Application       │ ← Security Groups, NACLs
│      VPC            │
│  ┌─────────────────┐│
│  │ EC2 Instances   ││ ← Host-based security
│  │ + GuardDuty     ││
│  └─────────────────┘│
└─────────────────────┘
```

### Pattern 2: Zero Trust Network
```
┌─────────────────────────────────────────────────────────────┐
│                    Zero Trust Architecture                   │
│                                                             │
│  ┌─────────────┐    ┌─────────────┐    ┌─────────────┐     │
│  │   Identity  │    │   Device    │    │   Network   │     │
│  │ Verification│    │Verification │    │Segmentation │     │
│  │             │    │             │    │             │     │
│  │ • IAM       │    │ • Device    │    │ • Micro-    │     │
│  │ • Cognito   │    │   Trust     │    │   segments  │     │
│  │ • MFA       │    │ • Endpoint  │    │ • Security  │     │
│  │             │    │   Security  │    │   Groups    │     │
│  └─────────────┘    └─────────────┘    └─────────────┘     │
│         │                   │                   │          │
│  ┌──────▼───────────────────▼───────────────────▼──────┐   │
│  │              Policy Engine                          │   │
│  │         (Decision Point)                            │   │
│  └─────────────────────┬───────────────────────────────┘   │
│                        │                                   │
│  ┌─────────────────────▼───────────────────────────────┐   │
│  │           Application Access                        │   │
│  │    (Always Verify, Never Trust)                     │   │
│  └─────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────┘
```

### Pattern 3: Incident Response Automation
```
┌─────────────────────────────────────────────────────────────┐
│                 Security Event Sources                      │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌────────┐ │
│  │ GuardDuty   │ │    WAF      │ │   Config    │ │CloudTrail│ │
│  │  Findings   │ │   Logs      │ │   Rules     │ │  Events │ │
│  └─────────────┘ └─────────────┘ └─────────────┘ └────────┘ │
└──────────┬────────────┬─────────────┬─────────────┬─────────┘
           │            │             │             │
    ┌──────▼────────────▼─────────────▼─────────────▼──────┐
    │                Security Hub                          │
    │            (Centralized Dashboard)                   │
    └──────────────────────┬───────────────────────────────┘
                           │
    ┌──────────────────────▼───────────────────────────────┐
    │                 EventBridge                          │
    │             (Event Routing)                          │
    └─┬──────────┬──────────┬──────────┬──────────┬────────┘
      │          │          │          │          │
┌─────▼────┐ ┌───▼───┐ ┌───▼────┐ ┌───▼───┐ ┌───▼────┐
│ Lambda   │ │ SNS   │ │ Step   │ │Ticket │ │ Lambda │
│(Isolate  │ │(Alert)│ │Functions│ │System │ │(Block  │
│Instance) │ │       │ │        │ │       │ │  IP)   │
└──────────┘ └───────┘ └────────┘ └───────┘ └────────┘
```

---

## 🔧 Compliance & Governance

### Compliance Frameworks Mapping

**PCI DSS Compliance:**
```yaml
# PCI DSS Requirements mapping to AWS services
PCI_DSS_Controls:
  Requirement_1: # Install and maintain firewall configuration
    Services:
      - AWS WAF
      - Network Firewall  
      - Security Groups
      - NACLs
    
  Requirement_2: # Do not use vendor-supplied defaults
    Services:
      - Config Rules (default password detection)
      - Systems Manager (patch compliance)
      
  Requirement_3: # Protect stored cardholder data
    Services:
      - KMS (encryption)
      - S3 (encryption at rest)
      - RDS (encryption)
      - Macie (sensitive data discovery)
      
  Requirement_4: # Encrypt transmission of cardholder data
    Services:
      - Certificate Manager
      - Application Load Balancer (SSL termination)
      - CloudFront (SSL/TLS)
      
  Requirement_10: # Track and monitor all access
    Services:
      - CloudTrail
      - VPC Flow Logs
      - GuardDuty
      - Security Hub
```

**SOC 2 Type II Controls:**
```python
# SOC 2 control implementation
soc2_controls = {
    'CC6.1': {  # Logical Access Security
        'description': 'System logical access controls',
        'aws_services': [
            'IAM (least privilege)',
            'Cognito (authentication)', 
            'MFA enforcement',
            'Access Analyzer'
        ],
        'evidence_sources': [
            'CloudTrail logs',
            'IAM credential reports',
            'Access Analyzer findings'
        ]
    },
    'CC7.1': {  # System Operation
        'description': 'System availability monitoring',
        'aws_services': [
            'CloudWatch (monitoring)',
            'Config (compliance)',
            'Systems Manager (patch management)',
            'GuardDuty (threat detection)'
        ],
        'evidence_sources': [
            'CloudWatch metrics',
            'Config compliance reports',
            'Patch compliance reports'
        ]
    },
    'CC8.1': {  # Change Management
        'description': 'Configuration change controls',
        'aws_services': [
            'CloudFormation (IaC)',
            'Config (change tracking)',
            'CodeCommit (version control)',
            'CodePipeline (automated deployment)'
        ],
        'evidence_sources': [
            'CloudFormation templates',
            'Git commit logs',
            'Config change history'
        ]
    }
}

def generate_soc2_evidence_report():
    """Generate automated SOC 2 evidence collection"""
    evidence_report = {}
    
    for control_id, control_info in soc2_controls.items():
        evidence_report[control_id] = {
            'control_description': control_info['description'],
            'implementation_date': datetime.now(),
            'evidence_collected': [],
            'compliance_status': 'COMPLIANT'  # Determined by automated checks
        }
        
        # Collect evidence from each source
        for evidence_source in control_info['evidence_sources']:
            if 'CloudTrail' in evidence_source:
                evidence = collect_cloudtrail_evidence()
            elif 'Config' in evidence_source:
                evidence = collect_config_evidence()
            elif 'CloudWatch' in evidence_source:
                evidence = collect_cloudwatch_evidence()
                
            evidence_report[control_id]['evidence_collected'].append({
                'source': evidence_source,
                'collection_date': datetime.now(),
                'evidence_count': len(evidence) if evidence else 0
            })
    
    return evidence_report
```

### Automated Compliance Monitoring
```python
import boto3
from datetime import datetime, timedelta

def setup_compliance_monitoring():
    config = boto3.client('config')
    
    # Define compliance rules
    compliance_rules = [
        {
            'ConfigRuleName': 'encrypted-volumes',
            'Description': 'Checks whether EBS volumes are encrypted',
            'Source': {
                'Owner': 'AWS',
                'SourceIdentifier': 'ENCRYPTED_VOLUMES'
            },
            'Scope': {
                'ComplianceResourceTypes': ['AWS::EC2::Volume']
            }
        },
        {
            'ConfigRuleName': 'root-mfa-enabled',
            'Description': 'Checks whether root account has MFA enabled',
            'Source': {
                'Owner': 'AWS',
                'SourceIdentifier': 'ROOT_MFA_ENABLED'
            }
        },
        {
            'ConfigRuleName': 'restricted-ssh',
            'Description': 'Checks whether security groups allow SSH from 0.0.0.0/0',
            'Source': {
                'Owner': 'AWS',
                'SourceIdentifier': 'INCOMING_SSH_DISABLED'
            },
            'Scope': {
                'ComplianceResourceTypes': ['AWS::EC2::SecurityGroup']
            }
        },
        {
            'ConfigRuleName': 's3-bucket-ssl-requests-only',
            'Description': 'Checks whether S3 buckets have policies requiring SSL',
            'Source': {
                'Owner': 'AWS',
                'SourceIdentifier': 'S3_BUCKET_SSL_REQUESTS_ONLY'
            },
            'Scope': {
                'ComplianceResourceTypes': ['AWS::S3::Bucket']
            }
        }
    ]
    
    # Create compliance rules
    for rule in compliance_rules:
        try:
            config.put_config_rule(ConfigRule=rule)
            print(f"Created rule: {rule['ConfigRuleName']}")
        except Exception as e:
            print(f"Failed to create rule {rule['ConfigRuleName']}: {e}")

def generate_compliance_report():
    config = boto3.client('config')
    
    # Get compliance status for all rules
    compliance_summary = config.get_compliance_summary_by_config_rule()
    
    report = {
        'report_date': datetime.now().isoformat(),
        'total_rules': 0,
        'compliant_rules': 0,
        'non_compliant_rules': 0,
        'rule_details': []
    }
    
    # Get detailed compliance for each rule
    rules = config.describe_config_rules()
    
    for rule in rules['ConfigRules']:
        rule_name = rule['ConfigRuleName']
        
        try:
            compliance_details = config.get_compliance_details_by_config_rule(
                ConfigRuleName=rule_name
            )
            
            compliant_count = len([
                result for result in compliance_details['EvaluationResults']
                if result['ComplianceType'] == 'COMPLIANT'
            ])
            
            non_compliant_count = len([
                result for result in compliance_details['EvaluationResults']  
                if result['ComplianceType'] == 'NON_COMPLIANT'
            ])
            
            report['rule_details'].append({
                'rule_name': rule_name,
                'compliant_resources': compliant_count,
                'non_compliant_resources': non_compliant_count,
                'compliance_percentage': (
                    compliant_count / (compliant_count + non_compliant_count) * 100
                    if (compliant_count + non_compliant_count) > 0 else 0
                )
            })
            
            report['total_rules'] += 1
            if non_compliant_count == 0:
                report['compliant_rules'] += 1
            else:
                report['non_compliant_rules'] += 1
                
        except Exception as e:
            print(f"Error getting compliance for rule {rule_name}: {e}")
    
    # Calculate overall compliance percentage
    report['overall_compliance_percentage'] = (
        report['compliant_rules'] / report['total_rules'] * 100
        if report['total_rules'] > 0 else 0
    )
    
    return report
```

---

## 📊 Security Monitoring & Analytics

### Security Metrics Dashboard
```python
import boto3
import json
from datetime import datetime, timedelta

def create_security_dashboard():
    cloudwatch = boto3.client('cloudwatch')
    
    dashboard_body = {
        "widgets": [
            {
                "type": "metric",
                "properties": {
                    "metrics": [
                        ["AWS/GuardDuty", "FindingCount", "FindingType", "Recon:EC2/PortProbeUnprotectedPort"],
                        [".", ".", ".", "UnauthorizedAPICall:IAMUser/InstanceCredentialsExfiltration"],
                        [".", ".", ".", "CryptoCurrency:EC2/BitcoinTool.B!DNS"]
                    ],
                    "period": 300,
                    "stat": "Sum",
                    "region": "us-east-1",
                    "title": "GuardDuty Findings by Type"
                }
            },
            {
                "type": "metric", 
                "properties": {
                    "metrics": [
                        ["AWS/WAFV2", "BlockedRequests", "WebACL", "ProductionWebACL", "Region", "us-east-1", "Rule", "RateLimitRule"],
                        [".", "AllowedRequests", ".", ".", ".", ".", ".", "."]
                    ],
                    "period": 300,
                    "stat": "Sum",
                    "region": "us-east-1", 
                    "title": "WAF Request Metrics"
                }
            },
            {
                "type": "log",
                "properties": {
                    "query": "SOURCE '/aws/lambda/security-response'\n| fields @timestamp, @message\n| filter @message like /SECURITY_INCIDENT/\n| sort @timestamp desc\n| limit 20",
                    "region": "us-east-1",
                    "title": "Recent Security Incidents",
                    "view": "table"
                }
            }
        ]
    }
    
    response = cloudwatch.put_dashboard(
        DashboardName='SecurityMonitoring',
        DashboardBody=json.dumps(dashboard_body)
    )
    
    return response

def setup_security_alarms():
    cloudwatch = boto3.client('cloudwatch')
    sns = boto3.client('sns')
    
    # Create SNS topic for security alerts
    topic = sns.create_topic(Name='SecurityAlerts')
    topic_arn = topic['TopicArn']
    
    # Subscribe email to topic
    sns.subscribe(
        TopicArn=topic_arn,
        Protocol='email',
        Endpoint='security-team@company.com'
    )
    
    # High severity GuardDuty findings alarm
    cloudwatch.put_metric_alarm(
        AlarmName='HighSeverityGuardDutyFindings',
        ComparisonOperator='GreaterThanThreshold',
        EvaluationPeriods=1,
        MetricName='FindingCount',
        Namespace='AWS/GuardDuty',
        Period=300,
        Statistic='Sum',
        Threshold=0,
        ActionsEnabled=True,
        AlarmActions=[topic_arn],
        AlarmDescription='Alert on high severity GuardDuty findings',
        Dimensions=[
            {
                'Name': 'FindingSeverity',
                'Value': 'High'
            }
        ]
    )
    
    # Unusual API call patterns
    cloudwatch.put_metric_alarm(
        AlarmName='UnusualAPICallPattern',
        ComparisonOperator='GreaterThanThreshold',
        EvaluationPeriods=2,
        MetricName='ErrorCount',
        Namespace='AWS/ApiGateway',
        Period=300,
        Statistic='Sum',
        Threshold=100,
        ActionsEnabled=True,
        AlarmActions=[topic_arn],
        AlarmDescription='Unusual API error patterns detected',
        TreatMissingData='notBreaching'
    )
```

### Threat Intelligence Integration
```python
def integrate_threat_intelligence():
    """Integrate external threat intelligence with GuardDuty"""
    
    guardduty = boto3.client('guardduty')
    s3 = boto3.client('s3')
    
    # Download threat intelligence feeds
    threat_feeds = [
        {
            'name': 'emerging-threats',
            'url': 'https://rules.emergingthreats.net/blockrules/compromised-ips.txt',
            'format': 'TXT'
        },
        {
            'name': 'abuse-ch-malware',
            'url': 'https://feodotracker.abuse.ch/downloads/ipblocklist.txt', 
            'format': 'TXT'
        }
    ]
    
    bucket_name = 'security-threat-intelligence'
    
    for feed in threat_feeds:
        # Download and upload to S3
        response = requests.get(feed['url'])
        if response.status_code == 200:
            s3.put_object(
                Bucket=bucket_name,
                Key=f"threat-intel/{feed['name']}.txt",
                Body=response.content
            )
            
            # Create/update GuardDuty threat intel set
            try:
                guardduty.create_threat_intel_set(
                    DetectorId='detector-id',
                    Name=feed['name'],
                    Format=feed['format'],
                    Location=f's3://{bucket_name}/threat-intel/{feed["name"]}.txt',
                    Activate=True
                )
            except guardduty.exceptions.BadRequestException:
                # Update existing threat intel set
                threat_intel_sets = guardduty.list_threat_intel_sets(
                    DetectorId='detector-id'
                )
                
                for set_id in threat_intel_sets['ThreatIntelSetIds']:
                    set_details = guardduty.get_threat_intel_set(
                        DetectorId='detector-id',
                        ThreatIntelSetId=set_id
                    )
                    
                    if set_details['Name'] == feed['name']:
                        guardduty.update_threat_intel_set(
                            DetectorId='detector-id',
                            ThreatIntelSetId=set_id,
                            Location=f's3://{bucket_name}/threat-intel/{feed["name"]}.txt'
                        )
                        break

def analyze_security_logs():
    """Automated security log analysis using CloudWatch Logs Insights"""
    
    logs = boto3.client('logs')
    
    # Common security queries
    security_queries = {
        'failed_logins': {
            'query': '''
                fields @timestamp, sourceIPAddress, userIdentity.type, errorCode
                | filter eventName = "ConsoleLogin" and errorCode = "SigninFailure"
                | stats count() by sourceIPAddress
                | sort count desc
                | limit 20
            ''',
            'log_group': '/aws/cloudtrail'
        },
        'privilege_escalation': {
            'query': '''
                fields @timestamp, sourceIPAddress, userIdentity.userName, eventName
                | filter eventName like /Put|Create|Attach/ and eventName like /Policy|Role/
                | filter userIdentity.type != "AssumedRole" or userIdentity.type != "SAMLUser"
                | sort @timestamp desc
                | limit 50
            ''',
            'log_group': '/aws/cloudtrail'
        },
        'data_exfiltration': {
            'query': '''
                fields @timestamp, sourceIPAddress, eventName, requestParameters
                | filter eventName = "GetObject" or eventName = "CopyObject"
                | filter requestParameters.bucketName like /sensitive|confidential|private/
                | stats count() by sourceIPAddress, userIdentity.userName
                | sort count desc
                | limit 20
            ''',
            'log_group': '/aws/cloudtrail'
        }
    }
    
    results = {}
    
    for query_name, query_config in security_queries.items():
        start_time = int((datetime.now() - timedelta(hours=24)).timestamp())
        end_time = int(datetime.now().timestamp())
        
        response = logs.start_query(
            logGroupName=query_config['log_group'],
            startTime=start_time,
            endTime=end_time,
            queryString=query_config['query']
        )
        
        query_id = response['queryId']
        
        # Wait for query completion (simplified - should implement proper polling)
        import time
        time.sleep(10)
        
        query_results = logs.get_query_results(queryId=query_id)
        results[query_name] = query_results['results']
    
    return results
```

---

## 🎯 Best Practices Summary

### Threat Detection
- [ ] **Enable GuardDuty** in all regions and accounts
- [ ] **Configure custom threat intelligence** feeds for industry-specific threats
- [ ] **Set up automated response workflows** for high-severity findings
- [ ] **Use Traffic Mirroring** for deep packet inspection when needed
- [ ] **Implement Security Hub** for centralized security posture management

### Network Security
- [ ] **Deploy Network Firewall** for inspection VPCs
- [ ] **Use WAF** on all public-facing applications
- [ ] **Implement Firewall Manager** for multi-account environments
- [ ] **Enable VPC Flow Logs** for network monitoring
- [ ] **Use Security Groups as stateful firewalls** with minimal required access

### Identity & Access Management
- [ ] **Implement least privilege access** with IAM roles and policies
- [ ] **Use IAM Access Analyzer** to identify overly permissive policies
- [ ] **Enable MFA** for all human users
- [ ] **Use Secrets Manager** for application credentials
- [ ] **Implement cross-account access** with IAM roles, not users

### Data Protection
- [ ] **Enable encryption at rest** for all data stores
- [ ] **Use KMS** for centralized key management
- [ ] **Implement Macie** for sensitive data discovery
- [ ] **Enable encryption in transit** for all communications
- [ ] **Use S3 bucket policies** to enforce secure access patterns

### Compliance & Governance
- [ ] **Use AWS Config** for configuration compliance monitoring
- [ ] **Implement automated remediation** for common compliance violations
- [ ] **Enable comprehensive logging** (CloudTrail, VPC Flow Logs, application logs)
- [ ] **Set up compliance dashboards** and regular reporting
- [ ] **Conduct regular security assessments** and penetration testing

### Incident Response
- [ ] **Create incident response playbooks** for common scenarios
- [ ] **Implement automated containment** for high-severity threats
- [ ] **Set up proper alerting** with SNS and escalation procedures
- [ ] **Practice incident response** with regular tabletop exercises
- [ ] **Maintain forensic capabilities** with proper log retention

---

*Last Updated: October 2025 | AWS SAA-C03 Study Guide*