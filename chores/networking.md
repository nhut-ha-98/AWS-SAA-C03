# AWS Networking & Content Delivery Guide 🌐

*Comprehensive guide to AWS networking services, VPC design patterns, and content delivery solutions*

## 🎯 Overview

AWS networking forms the foundation of cloud architecture, enabling secure, scalable, and high-performance applications. This guide covers core networking services, design patterns, and best practices for building robust network infrastructures.

---

## 🚀 Quick Service Selection Table

| Category | Service | Layer | Best For | Use Case Example |
|----------|---------|-------|----------|------------------|
| **Content Delivery** | CloudFront | Application (L7) | Caching static/dynamic content | Website acceleration, video streaming |
| **Global Performance** | Global Accelerator | Network (L4) | Low-latency access to apps | Gaming, real-time APIs, global apps |
| **Load Balancing** | Application Load Balancer | Application (L7) | HTTP/HTTPS traffic distribution | Web applications, microservices |
| **Load Balancing** | Network Load Balancer | Network (L4) | TCP/UDP traffic, ultra-high performance | Gaming, IoT, financial trading |
| **Load Balancing** | Gateway Load Balancer | Network (L3) | Third-party security appliances | Firewalls, IDS/IPS, DPI |
| **DNS & Routing** | Route 53 | Application (L7) | DNS resolution, health checks | Domain management, traffic routing |
| **Network Foundation** | VPC | Network (L3) | Isolated virtual networks | Secure application hosting |
| **Hybrid Connectivity** | VPN Gateway | Network (L3) | Site-to-site VPN connections | Hybrid cloud connectivity |
| **Hybrid Connectivity** | Direct Connect | Physical (L1) | Dedicated network connection | High-bandwidth, consistent latency |
| **Multi-VPC Networking** | Transit Gateway | Network (L3) | Hub-and-spoke network topology | Multi-VPC, multi-region connectivity |

---

## 🌳 Networking Service Decision Tree

```
Do you need to improve application performance or availability?
│
├──> No → Basic VPC setup may be sufficient
│
└──> Yes
     │
     ├── What type of performance improvement?
     │   │
     │   ├── Content delivery (static/cached content) → ✅ CloudFront
     │   ├── Application performance (dynamic content) → Continue to Global Performance ↓
     │   ├── Load distribution → Continue to Load Balancer Selection ↓
     │   └── DNS resolution speed → ✅ Route 53 with health checks
     │
     ├── GLOBAL PERFORMANCE BRANCH:
     │   │
     │   ├── What type of traffic?
     │   │   │
     │   │   ├── HTTP/HTTPS (web content) → ✅ CloudFront (L7 caching)
     │   │   ├── TCP/UDP (non-HTTP) → ✅ Global Accelerator (L4 optimization)
     │   │   └── Mixed traffic → Use both (CloudFront + Global Accelerator)
     │   │
     │   ├── Do you need caching?
     │   │   │
     │   │   ├── Yes → ✅ CloudFront
     │   │   └── No → ✅ Global Accelerator
     │   │
     │   └── Do you need static IP addresses?
     │       │
     │       ├── Yes → ✅ Global Accelerator
     │       └── No → ✅ CloudFront
     │
     ├── LOAD BALANCER SELECTION:
     │   │
     │   ├── What protocol layer?
     │   │   │
     │   │   ├── HTTP/HTTPS (Layer 7) → ✅ Application Load Balancer
     │   │   ├── TCP/UDP (Layer 4) → ✅ Network Load Balancer  
     │   │   └── Network Layer 3 (GENEVE) → ✅ Gateway Load Balancer
     │   │
     │   ├── Do you need advanced routing?
     │   │   │
     │   │   ├── Yes (path-based, header-based) → ✅ ALB
     │   │   └── No (simple distribution) → ✅ NLB
     │   │
     │   └── Do you need third-party appliances?
     │       │
     │       ├── Yes (firewalls, IDS/IPS) → ✅ Gateway Load Balancer
     │       └── No → ALB or NLB based on protocol
     │
     └── CONNECTIVITY REQUIREMENTS:
         │
         ├── Internet connectivity needed?
         │   │
         │   ├── Yes → Internet Gateway + NAT Gateway/Instance
         │   └── No → Private subnets only
         │
         ├── On-premises connectivity needed?
         │   │
         │   ├── Yes → Continue to hybrid options ↓
         │   └── No → VPC-only architecture
         │
         ├── What type of hybrid connectivity?
         │   │
         │   ├── Backup/occasional access → ✅ VPN Gateway
         │   ├── High bandwidth/consistent performance → ✅ Direct Connect
         │   └── Multiple VPC connections → ✅ Transit Gateway
         │
         └── Multiple VPC/account connectivity?
             │
             ├── Yes → ✅ Transit Gateway (hub-and-spoke)
             └── No → VPC Peering (point-to-point)
```

---

## 📋 Service Deep Dive

### 🌍 Amazon CloudFront vs AWS Global Accelerator

| Feature | **CloudFront** | **Global Accelerator** |
| :------ | :------------- | :--------------------- |
| **Primary Function** | Content Delivery Network (CDN) | Global network performance optimization |
| **Layer** | **Application (L7)** | **Network (L4)** |
| **Protocol Support** | HTTP / HTTPS | TCP / UDP (any protocol) |
| **Caching** | ✅ Yes - Edge caching for content | ❌ No caching |
| **Static IP Addresses** | ❌ No (dynamic CloudFront IPs) | ✅ Yes (2 static Anycast IPs) |
| **Use Case** | Static/dynamic content delivery | Low-latency access to applications |
| **Best For** | Websites, APIs, video streaming | Gaming, IoT, real-time apps |
| **Pricing Model** | Pay per data transfer + requests | Pay per accelerator + data transfer |
| **Failover** | ⚠️ Possible, but slower | ✅ Fast automatic failover |
| **Health Checks** | Limited | ✅ Built-in endpoint health monitoring |
| **Geographic Routing** | Edge location based | Intelligent routing based on performance |

**When to Choose CloudFront:**
```
✅ Website acceleration and static content delivery
✅ API acceleration with caching benefits
✅ Video streaming and large file downloads
✅ Protection against DDoS attacks
✅ Custom SSL certificates and domain names
✅ Real-time logs and detailed analytics
```

**When to Choose Global Accelerator:**
```
✅ Gaming applications requiring consistent low latency
✅ IoT applications with UDP traffic
✅ Voice over IP (VoIP) and video conferencing
✅ Financial trading platforms requiring speed
✅ Applications needing static IP addresses
✅ Multi-region failover with health checks
```

**Configuration Examples:**

**CloudFront Setup:**
```javascript
// CloudFormation template for CloudFront distribution
{
    "Type": "AWS::CloudFront::Distribution",
    "Properties": {
        "DistributionConfig": {
            "Origins": [{
                "Id": "S3Origin",
                "DomainName": "mybucket.s3.amazonaws.com",
                "S3OriginConfig": {
                    "OriginAccessIdentity": "origin-access-identity/cloudfront/E1234567890"
                }
            }],
            "DefaultCacheBehavior": {
                "TargetOriginId": "S3Origin",
                "ViewerProtocolPolicy": "redirect-to-https",
                "CachePolicyId": "managed-caching-optimized",
                "Compress": true
            },
            "Enabled": true,
            "HttpVersion": "http2",
            "PriceClass": "PriceClass_100"
        }
    }
}
```

**Global Accelerator Setup:**
```python
import boto3

globalaccelerator = boto3.client('globalaccelerator')

# Create accelerator
accelerator = globalaccelerator.create_accelerator(
    Name='MyAppAccelerator',
    IpAddressType='IPV4',
    Enabled=True,
    Attributes={
        'FlowLogsEnabled': True,
        'FlowLogsS3Bucket': 'my-flow-logs-bucket',
        'FlowLogsS3Prefix': 'accelerator-logs/'
    }
)

# Create listener
listener = globalaccelerator.create_listener(
    AcceleratorArn=accelerator['Accelerator']['AcceleratorArn'],
    Protocol='TCP',
    PortRanges=[{
        'FromPort': 80,
        'ToPort': 80
    }]
)

# Create endpoint group
endpoint_group = globalaccelerator.create_endpoint_group(
    ListenerArn=listener['Listener']['ListenerArn'],
    EndpointGroupRegion='us-east-1',
    EndpointConfigurations=[{
        'EndpointId': 'arn:aws:elasticloadbalancing:us-east-1:123456789012:loadbalancer/app/my-load-balancer/1234567890123456',
        'Weight': 100,
        'ClientIPPreservationEnabled': True
    }],
    TrafficDialPercentage=100,
    HealthCheckIntervalSeconds=30,
    HealthCheckProtocol='HTTP',
    HealthCheckPath='/health'
)
```

### ⚖️ Load Balancer Selection Guide

#### 🌐 Application Load Balancer (ALB)
*Layer 7 HTTP/HTTPS load balancer*

**Key Features:**
- ✅ Content-based routing (path, header, query string)
- ✅ WebSocket and HTTP/2 support
- ✅ Integration with AWS WAF
- ✅ Authentication integration (Cognito, OIDC)
- ✅ Lambda targets
- ✅ Containerized application support

**Routing Rules Examples:**
```json
{
    "Rules": [
        {
            "Conditions": [{
                "Field": "path-pattern",
                "Values": ["/api/*"]
            }],
            "Actions": [{
                "Type": "forward",
                "TargetGroupArn": "arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/api-servers/1234567890123456"
            }],
            "Priority": 100
        },
        {
            "Conditions": [{
                "Field": "host-header",
                "Values": ["admin.example.com"]
            }],
            "Actions": [{
                "Type": "authenticate-oidc",
                "AuthenticateOidcConfig": {
                    "Issuer": "https://auth.example.com",
                    "AuthorizationEndpoint": "https://auth.example.com/auth",
                    "TokenEndpoint": "https://auth.example.com/token",
                    "UserInfoEndpoint": "https://auth.example.com/userinfo",
                    "ClientId": "my-client-id"
                }
            }],
            "Priority": 200
        }
    ]
}
```

**Use Cases:**
```
✅ Microservices architectures with path-based routing
✅ Blue/green deployments with weighted routing
✅ Multi-tenant applications with host-based routing
✅ Applications requiring authentication integration
✅ Serverless architectures with Lambda targets
```

#### ⚡ Network Load Balancer (NLB)
*Layer 4 TCP/UDP load balancer*

**Key Features:**
- ✅ Ultra-high performance (millions of requests/sec)
- ✅ Static IP addresses
- ✅ Source IP preservation
- ✅ Cross-zone load balancing
- ✅ TLS termination
- ✅ UDP load balancing

**Configuration Example:**
```python
import boto3

elbv2 = boto3.client('elbv2')

# Create NLB
nlb = elbv2.create_load_balancer(
    Name='high-performance-nlb',
    Subnets=['subnet-12345', 'subnet-67890'],
    Type='network',
    Scheme='internet-facing',
    IpAddressType='ipv4'
)

# Create target group for TCP traffic
target_group = elbv2.create_target_group(
    Name='tcp-targets',
    Protocol='TCP',
    Port=80,
    VpcId='vpc-12345678',
    HealthCheckProtocol='TCP',
    HealthCheckIntervalSeconds=10,
    HealthyThresholdCount=2,
    UnhealthyThresholdCount=2
)

# Register targets
elbv2.register_targets(
    TargetGroupArn=target_group['TargetGroups'][0]['TargetGroupArn'],
    Targets=[
        {'Id': 'i-1234567890abcdef0', 'Port': 80},
        {'Id': 'i-0fedcba0987654321', 'Port': 80}
    ]
)

# Create listener
listener = elbv2.create_listener(
    LoadBalancerArn=nlb['LoadBalancers'][0]['LoadBalancerArn'],
    Protocol='TCP',
    Port=80,
    DefaultActions=[{
        'Type': 'forward',
        'TargetGroupArn': target_group['TargetGroups'][0]['TargetGroupArn']
    }]
)
```

**Use Cases:**
```
✅ Gaming applications requiring ultra-low latency
✅ IoT applications with high connection counts
✅ Financial trading systems needing consistent performance
✅ Legacy applications not supporting HTTP load balancers
✅ Applications requiring static IP addresses
```

#### 🛡️ Gateway Load Balancer (GLB)
*Layer 3 transparent network gateway*

**Key Features:**
- ✅ GENEVE protocol support
- ✅ Transparent bump-in-the-wire deployment
- ✅ Source and destination IP preservation
- ✅ Integration with third-party security appliances
- ✅ Cross-AZ load balancing

**Architecture Pattern:**
```
Internet → IGW → GLB → Security Appliances → ALB/NLB → Application Instances
                │
                └─── Firewall/IDS/IPS Instances
```

**Configuration:**
```yaml
# CloudFormation for Gateway Load Balancer
GatewayLoadBalancer:
  Type: AWS::ElasticLoadBalancingV2::LoadBalancer
  Properties:
    Type: gateway
    Subnets:
      - !Ref SecuritySubnet1
      - !Ref SecuritySubnet2
    Tags:
      - Key: Name
        Value: SecurityApplianceGLB

SecurityTargetGroup:
  Type: AWS::ElasticLoadBalancingV2::TargetGroup
  Properties:
    Protocol: GENEVE
    Port: 6081
    VpcId: !Ref VPC
    TargetType: instance
    HealthCheckProtocol: HTTP
    HealthCheckPath: /health
    HealthCheckPort: 80

VPCEndpointService:
  Type: AWS::EC2::VPCEndpointService
  Properties:
    GatewayLoadBalancerArns:
      - !Ref GatewayLoadBalancer
    AcceptanceRequired: false
```

**Use Cases:**
```
✅ Network security inspection (firewall, IDS/IPS)
✅ Deep packet inspection (DPI)
✅ Network monitoring and analytics
✅ Compliance requirements for traffic inspection
✅ Third-party network virtual appliances
```

### 🏗️ VPC Design Patterns

#### Pattern 1: Single-Tier Web Application
```
┌─────────────────────────────────────────────────────┐
│                      VPC                            │
│                   10.0.0.0/16                      │
│                                                     │
│  ┌─────────────────┐    ┌─────────────────┐        │
│  │  Public Subnet  │    │  Public Subnet  │        │
│  │    AZ-1a        │    │     AZ-1b       │        │
│  │  10.0.1.0/24    │    │  10.0.2.0/24    │        │
│  │                 │    │                 │        │
│  │ ┌─────────────┐ │    │ ┌─────────────┐ │        │
│  │ │   Web       │ │    │ │   Web       │ │        │
│  │ │  Server     │ │    │ │  Server     │ │        │
│  │ └─────────────┘ │    │ └─────────────┘ │        │
│  └─────────────────┘    └─────────────────┘        │
│             │                       │               │
│  ┌──────────▼───────────────────────▼─────────────┐ │
│  │           Internet Gateway                     │ │
│  └────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────┘
```

#### Pattern 2: Three-Tier Architecture
```
┌──────────────────────────────────────────────────────────────────┐
│                           VPC (10.0.0.0/16)                     │
│                                                                  │
│  ┌─────────────────────┐      ┌─────────────────────┐            │
│  │   Public Subnet     │      │   Public Subnet     │            │
│  │      AZ-1a          │      │      AZ-1b          │            │
│  │   10.0.1.0/24       │      │   10.0.2.0/24       │            │
│  │  ┌───────────────┐  │      │  ┌───────────────┐  │            │
│  │  │ Load Balancer │  │      │  │ Load Balancer │  │            │
│  │  │      ALB      │  │      │  │      ALB      │  │            │
│  │  └───────────────┘  │      │  └───────────────┘  │            │
│  └─────────────────────┘      └─────────────────────┘            │
│             │                            │                       │
│  ┌─────────▼─────────┐        ┌─────────▼─────────┐              │
│  │  Private Subnet   │        │  Private Subnet   │              │
│  │     AZ-1a         │        │     AZ-1b         │              │
│  │  10.0.10.0/24     │        │  10.0.20.0/24     │              │
│  │ ┌───────────────┐ │        │ ┌───────────────┐ │              │
│  │ │   App Server  │ │        │ │   App Server  │ │              │
│  │ │     EC2       │ │        │ │     EC2       │ │              │
│  │ └───────────────┘ │        │ └───────────────┘ │              │
│  └─────────────────────┘      └─────────────────────┘            │
│             │                            │                       │
│  ┌─────────▼─────────┐        ┌─────────▼─────────┐              │
│  │  Private Subnet   │        │  Private Subnet   │              │
│  │     AZ-1a         │        │     AZ-1b         │              │
│  │  10.0.100.0/24    │        │  10.0.200.0/24    │              │
│  │ ┌───────────────┐ │        │ ┌───────────────┐ │              │
│  │ │   Database    │ │        │ │   Database    │ │              │
│  │ │     RDS       │ │        │ │ (Read Replica)│ │              │
│  │ └───────────────┘ │        │ └───────────────┘ │              │
│  └─────────────────────┘      └─────────────────────┘            │
└──────────────────────────────────────────────────────────────────┘
```

#### Pattern 3: Hub-and-Spoke with Transit Gateway
```
                    ┌─────────────────────┐
                    │   Transit Gateway   │
                    │    (Hub/Router)     │
                    └──────────┬──────────┘
                               │
     ┌─────────────────────────┼─────────────────────────┐
     │                         │                         │
┌────▼────┐              ┌─────▼─────┐           ┌──────▼──────┐
│Production│              │Development│           │   Shared    │
│   VPC    │              │    VPC    │           │ Services VPC│
│10.1.0.0/16│            │10.2.0.0/16│           │10.0.0.0/16 │
└─────────┘              └───────────┘           └─────────────┘
     │                         │                         │
┌────▼────┐              ┌─────▼─────┐           ┌──────▼──────┐
│On-Premises              │   Testing │           │   Security  │
│via DX/VPN│              │    VPC    │           │Services VPC │
│192.168.0.0/16│         │10.3.0.0/16│           │10.4.0.0/16 │
└─────────┘              └───────────┘           └─────────────┘
```

### 🔒 Network Security Best Practices

#### Security Group Configuration
```python
# Web tier security group (ALB targets)
web_sg_rules = [
    {
        'IpProtocol': 'tcp',
        'FromPort': 80,
        'ToPort': 80,
        'SourceSecurityGroupId': 'sg-alb-12345678'  # Only from ALB
    },
    {
        'IpProtocol': 'tcp', 
        'FromPort': 443,
        'ToPort': 443,
        'SourceSecurityGroupId': 'sg-alb-12345678'  # Only from ALB
    },
    {
        'IpProtocol': 'tcp',
        'FromPort': 22,
        'ToPort': 22,
        'CidrIp': '10.0.0.0/16'  # SSH from bastion hosts only
    }
]

# Database tier security group
db_sg_rules = [
    {
        'IpProtocol': 'tcp',
        'FromPort': 3306,
        'ToPort': 3306,
        'SourceSecurityGroupId': 'sg-web-87654321'  # Only from web tier
    },
    {
        'IpProtocol': 'tcp',
        'FromPort': 3306,
        'ToPort': 3306,
        'SourceSecurityGroupId': 'sg-app-11111111'  # Only from app tier
    }
]
```

#### Network ACL Configuration
```python
# Restrictive NACL for database subnet
db_nacl_rules = [
    # Inbound rules
    {
        'RuleNumber': 100,
        'Protocol': '6',  # TCP
        'RuleAction': 'allow',
        'CidrBlock': '10.0.10.0/24',  # App subnet
        'PortRange': {'From': 3306, 'To': 3306}
    },
    {
        'RuleNumber': 110,
        'Protocol': '6',  # TCP
        'RuleAction': 'allow',
        'CidrBlock': '10.0.20.0/24',  # App subnet AZ-b
        'PortRange': {'From': 3306, 'To': 3306}
    },
    {
        'RuleNumber': 32767,  # Default rule
        'Protocol': '-1',
        'RuleAction': 'deny',
        'CidrBlock': '0.0.0.0/0'
    }
]
```

#### VPC Flow Logs Configuration
```python
import boto3

ec2 = boto3.client('ec2')

# Enable VPC Flow Logs
flow_logs = ec2.create_flow_logs(
    ResourceIds=['vpc-12345678'],
    ResourceType='VPC',
    TrafficType='ALL',  # ACCEPT, REJECT, or ALL
    LogDestinationType='s3',
    LogDestination='arn:aws:s3:::my-flow-logs-bucket/vpc-flow-logs/',
    LogFormat='${account-id} ${interface-id} ${srcaddr} ${dstaddr} ${srcport} ${dstport} ${protocol} ${packets} ${bytes} ${windowstart} ${windowend} ${action} ${flowlogstatus}',
    MaxAggregationInterval=60,  # 1 or 10 minutes
    Tags=[
        {
            'Key': 'Name',
            'Value': 'VPC-FlowLogs-Production'
        }
    ]
)
```

### 🌐 Hybrid Connectivity Solutions

#### VPN Gateway Configuration
```yaml
# CloudFormation template for VPN connection
VPNGateway:
  Type: AWS::EC2::VpnGateway
  Properties:
    Type: ipsec.1
    Tags:
      - Key: Name
        Value: Main-VPN-Gateway

AttachVPNGateway:
  Type: AWS::EC2::VPCGatewayAttachment
  Properties:
    VpcId: !Ref VPC
    VpnGatewayId: !Ref VPNGateway

CustomerGateway:
  Type: AWS::EC2::CustomerGateway
  Properties:
    Type: ipsec.1
    BgpAsn: 65000
    IpAddress: 203.0.113.12  # Your public IP
    Tags:
      - Key: Name
        Value: Main-Customer-Gateway

VPNConnection:
  Type: AWS::EC2::VpnConnection
  Properties:
    Type: ipsec.1
    StaticRoutesOnly: false  # Use BGP
    CustomerGatewayId: !Ref CustomerGateway
    VpnGatewayId: !Ref VPNGateway
    Tags:
      - Key: Name
        Value: Main-VPN-Connection
```

#### Direct Connect Setup Process
```
1. Order Direct Connect Port:
   ├─ Choose location (DX location near your data center)
   ├─ Select port speed (1Gbps, 10Gbps, 100Gbps)
   ├─ Complete LOA-CFA (Letter of Authorization)
   └─ Coordinate with colocation provider

2. Create Virtual Interfaces (VIFs):
   ├─ Private VIF (access to VPC)
   ├─ Transit VIF (access via Transit Gateway)
   └─ Public VIF (access to AWS public services)

3. Configure BGP:
   ├─ Exchange BGP information
   ├─ Configure route advertisements
   └─ Test connectivity and failover

4. Implement Redundancy:
   ├─ Multiple DX connections
   ├─ DX + VPN backup
   └─ Cross-region redundancy
```

**Direct Connect Gateway Configuration:**
```python
import boto3

directconnect = boto3.client('directconnect')

# Create Direct Connect Gateway
dx_gateway = directconnect.create_direct_connect_gateway(
    name='main-dx-gateway'
)

# Create Virtual Interface
vif = directconnect.create_private_virtual_interface(
    connectionId='dxcon-fg5678gh',
    newPrivateVirtualInterface={
        'virtualInterfaceName': 'production-vif',
        'vlan': 100,
        'asn': 65000,
        'mtu': 1500,
        'authKey': 'BGP-auth-key',
        'amazonAddress': '169.254.1.1/30',
        'customerAddress': '169.254.1.2/30',
        'addressFamily': 'ipv4',
        'directConnectGatewayId': dx_gateway['directConnectGateway']['directConnectGatewayId']
    }
)

# Associate with Transit Gateway
ec2 = boto3.client('ec2')
association = ec2.create_direct_connect_gateway_attachment(
    DirectConnectGatewayId=dx_gateway['directConnectGateway']['directConnectGatewayId'],
    TransitGatewayId='tgw-1234567890abcdef0',
    Tags=[
        {
            'Key': 'Name',
            'Value': 'DX-TGW-Association'
        }
    ]
)
```

---

## 🚀 Performance Optimization

### CloudFront Performance Tuning
```javascript
// Advanced CloudFront caching configuration
{
    "CacheBehaviors": [
        {
            "PathPattern": "/api/*",
            "TargetOriginId": "APIOrigin", 
            "ViewerProtocolPolicy": "https-only",
            "CachePolicyId": "managed-caching-disabled",  // Don't cache API responses
            "OriginRequestPolicyId": "managed-cors-s3-origin",
            "ResponseHeadersPolicyId": "managed-cors-preflight-response"
        },
        {
            "PathPattern": "/static/*",
            "TargetOriginId": "StaticOrigin",
            "ViewerProtocolPolicy": "https-only", 
            "CachePolicyId": "managed-caching-optimized",  // Aggressive caching
            "Compress": true
        },
        {
            "PathPattern": "/images/*",
            "TargetOriginId": "ImageOrigin",
            "ViewerProtocolPolicy": "https-only",
            "CachePolicyId": "custom-image-caching",
            "ResponseHeadersPolicyId": "custom-security-headers"
        }
    ]
}

// Custom cache policy for images
{
    "CachePolicyConfig": {
        "Name": "ImageCachingPolicy",
        "DefaultTTL": 86400,      // 1 day
        "MaxTTL": 31536000,       // 1 year
        "MinTTL": 86400,          // 1 day minimum
        "ParametersInCacheKeyAndForwardedToOrigin": {
            "EnableAcceptEncodingGzip": true,
            "EnableAcceptEncodingBrotli": true,
            "QueryStringsConfig": {
                "QueryStringBehavior": "whitelist",
                "QueryStrings": ["version", "format", "quality"]
            },
            "HeadersConfig": {
                "HeaderBehavior": "whitelist",
                "Headers": ["Accept", "CloudFront-Viewer-Country"]
            }
        }
    }
}
```

### Route 53 Health Check Optimization
```python
import boto3

route53 = boto3.client('route53')

# Create calculated health check
calculated_health_check = route53.create_health_check(
    Type='CALCULATED',
    CallerReference='calculated-hc-' + str(int(time.time())),
    HealthCheckConfig={
        'Type': 'CALCULATED',
        'ChildHealthChecks': [
            'health-check-primary-endpoint',
            'health-check-secondary-endpoint'
        ],
        'HealthThreshold': 1,  # At least 1 must be healthy
        'CloudWatchAlarmRegion': 'us-east-1',
        'InsufficientDataHealthStatus': 'Failure'
    }
)

# Weighted routing with health checks
primary_record = route53.change_resource_record_sets(
    HostedZoneId='Z3M3LMPEXAMPLE',
    ChangeBatch={
        'Changes': [{
            'Action': 'CREATE',
            'ResourceRecordSet': {
                'Name': 'api.example.com',
                'Type': 'A',
                'SetIdentifier': 'primary-us-east-1',
                'Weight': 100,
                'TTL': 60,
                'ResourceRecords': [{'Value': '203.0.113.1'}],
                'HealthCheckId': 'primary-health-check-id'
            }
        }]
    }
)

# Failover routing
failover_record = route53.change_resource_record_sets(
    HostedZoneId='Z3M3LMPEXAMPLE',
    ChangeBatch={
        'Changes': [{
            'Action': 'CREATE',
            'ResourceRecordSet': {
                'Name': 'api.example.com',
                'Type': 'A',
                'SetIdentifier': 'failover-us-west-2',
                'Failover': 'SECONDARY',
                'TTL': 60,
                'ResourceRecords': [{'Value': '203.0.113.2'}],
                'HealthCheckId': 'secondary-health-check-id'
            }
        }]
    }
)
```

---

## 📊 Monitoring & Troubleshooting

### CloudWatch Metrics for Networking Services

**Load Balancer Metrics:**
```python
import boto3
from datetime import datetime, timedelta

cloudwatch = boto3.client('cloudwatch')

# ALB performance metrics
alb_metrics = [
    'TargetResponseTime',
    'RequestCount', 
    'HTTPCode_Target_2XX_Count',
    'HTTPCode_Target_4XX_Count',
    'HTTPCode_Target_5XX_Count',
    'UnHealthyHostCount',
    'ActiveConnectionCount'
]

for metric in alb_metrics:
    response = cloudwatch.get_metric_statistics(
        Namespace='AWS/ApplicationELB',
        MetricName=metric,
        Dimensions=[
            {
                'Name': 'LoadBalancer',
                'Value': 'app/my-load-balancer/50dc6c495c0c9188'
            }
        ],
        StartTime=datetime.utcnow() - timedelta(hours=1),
        EndTime=datetime.utcnow(),
        Period=300,
        Statistics=['Average', 'Maximum', 'Sum']
    )
    print(f"{metric}: {response['Datapoints']}")
```

**CloudFront Metrics:**
```python
# CloudFront real-time metrics
cloudfront_metrics = [
    'Requests',
    'BytesDownloaded', 
    'BytesUploaded',
    '4xxErrorRate',
    '5xxErrorRate',
    'OriginLatency',
    'CacheHitRate'
]

for metric in cloudfront_metrics:
    response = cloudwatch.get_metric_statistics(
        Namespace='AWS/CloudFront',
        MetricName=metric,
        Dimensions=[
            {
                'Name': 'DistributionId',
                'Value': 'E1GHQBW5A2XBHU'
            }
        ],
        StartTime=datetime.utcnow() - timedelta(hours=24),
        EndTime=datetime.utcnow(),
        Period=3600,  # 1 hour intervals
        Statistics=['Sum', 'Average']
    )
    print(f"{metric}: {response['Datapoints']}")
```

### Common Network Troubleshooting

**Connectivity Issues Checklist:**
```
1. Security Group Rules:
   ├─ Check inbound rules on target instances
   ├─ Verify outbound rules on source instances
   ├─ Ensure proper port ranges are open
   └─ Validate security group references

2. Network ACL Rules:
   ├─ Check subnet-level NACL rules
   ├─ Verify both inbound and outbound rules
   ├─ Remember NACLs are stateless
   └─ Check ephemeral port ranges (32768-65535)

3. Route Tables:
   ├─ Verify routes to target subnets
   ├─ Check Internet Gateway routes for public access
   ├─ Validate NAT Gateway/Instance routes for private subnets
   └─ Confirm VPC peering or Transit Gateway routes

4. DNS Resolution:
   ├─ Check Route 53 hosted zone records
   ├─ Verify health check status
   ├─ Test DNS resolution from client location
   └─ Check TTL values for DNS changes
```

**Load Balancer Troubleshooting:**
```bash
# Check ALB target health
aws elbv2 describe-target-health \
    --target-group-arn arn:aws:elasticloadbalancing:us-east-1:123456789012:targetgroup/my-targets/1234567890123456

# Check NLB flow logs
aws logs filter-log-events \
    --log-group-name /aws/networkloadbalancer/my-nlb \
    --start-time $(date -d '1 hour ago' +%s)000 \
    --filter-pattern '[timestamp, elb, client_ip = "192.168.1.100", *]'

# Test connectivity from load balancer
aws ec2 describe-instances \
    --filters "Name=tag:aws:autoscaling:groupName,Values=my-asg" \
    --query 'Reservations[].Instances[].{ID:InstanceId,IP:PrivateIpAddress,State:State.Name}'
```

**VPC Flow Log Analysis:**
```bash
# Query VPC Flow Logs in CloudWatch Logs Insights
fields @timestamp, srcaddr, dstaddr, srcport, dstport, protocol, action
| filter action = "REJECT"
| stats count() by srcaddr, dstaddr, dstport
| sort count desc
| limit 20

# Analyze rejected connections
fields @timestamp, srcaddr, dstaddr, dstport, protocol
| filter action = "REJECT" and dstport = 80
| stats count() by srcaddr
| sort count desc
```

---

## 💰 Cost Optimization

### CloudFront Cost Optimization
```
Pricing Factors:
├─ Data Transfer Out: $0.085 - $0.170 per GB (varies by region)
├─ HTTP/HTTPS Requests: $0.0075 per 10,000 requests
├─ Regional Edge Caches: $0.020 per 10,000 requests
└─ Additional Features: SSL certificates, real-time logs

Optimization Strategies:
├─ Use appropriate price class (PriceClass_100, _All)
├─ Optimize cache hit ratios with proper TTL settings
├─ Compress content to reduce data transfer costs
├─ Use origin request policies to minimize origin requests
└─ Implement proper cache invalidation strategies
```

### Load Balancer Cost Optimization
```bash
# ALB pricing calculation
ALB_HOURS_PER_MONTH=730
ALB_HOURLY_RATE=0.0225
LCU_PRICE_PER_HOUR=0.008
AVERAGE_LCU_USAGE=5

ALB_MONTHLY_COST=$(echo "$ALB_HOURS_PER_MONTH * $ALB_HOURLY_RATE" | bc)
LCU_MONTHLY_COST=$(echo "$ALB_HOURS_PER_MONTH * $LCU_PRICE_PER_HOUR * $AVERAGE_LCU_USAGE" | bc)
TOTAL_ALB_COST=$(echo "$ALB_MONTHLY_COST + $LCU_MONTHLY_COST" | bc)

echo "ALB Base Cost: $${ALB_MONTHLY_COST}/month"
echo "LCU Cost: $${LCU_MONTHLY_COST}/month" 
echo "Total ALB Cost: $${TOTAL_ALB_COST}/month"

# NLB pricing (often more cost-effective for high throughput)
NLB_HOURLY_RATE=0.0225
NLCU_PRICE_PER_HOUR=0.006
AVERAGE_NLCU_USAGE=3

NLB_MONTHLY_COST=$(echo "$ALB_HOURS_PER_MONTH * $NLB_HOURLY_RATE" | bc)
NLCU_MONTHLY_COST=$(echo "$ALB_HOURS_PER_MONTH * $NLCU_PRICE_PER_HOUR * $AVERAGE_NLCU_USAGE" | bc)
TOTAL_NLB_COST=$(echo "$NLB_MONTHLY_COST + $NLCU_MONTHLY_COST" | bc)

echo "NLB Total Cost: $${TOTAL_NLB_COST}/month"
```

### Direct Connect Cost Analysis
```python
def calculate_dx_cost(bandwidth_gbps, monthly_data_transfer_tb, region='us-east-1'):
    """Calculate Direct Connect costs vs Internet transfer"""
    
    # Direct Connect port costs (monthly)
    dx_port_costs = {
        '1Gbps': 30,      # $30/month for 1Gbps port
        '10Gbps': 300,    # $300/month for 10Gbps port
        '100Gbps': 2250   # $2,250/month for 100Gbps port
    }
    
    # Direct Connect data transfer rates (per GB)
    dx_transfer_rate = 0.02  # $0.02 per GB
    
    # Internet data transfer rates (per GB, after free tier)
    internet_transfer_rate = 0.09  # $0.09 per GB
    
    # Calculate costs
    dx_port_cost = dx_port_costs.get(f'{bandwidth_gbps}Gbps', 0)
    dx_data_cost = monthly_data_transfer_tb * 1024 * dx_transfer_rate
    total_dx_cost = dx_port_cost + dx_data_cost
    
    internet_cost = monthly_data_transfer_tb * 1024 * internet_transfer_rate
    
    savings = internet_cost - total_dx_cost
    break_even_tb = dx_port_cost / (internet_transfer_rate - dx_transfer_rate) / 1024
    
    return {
        'direct_connect_cost': total_dx_cost,
        'internet_cost': internet_cost,
        'monthly_savings': savings,
        'break_even_tb': break_even_tb
    }

# Example calculation
result = calculate_dx_cost(
    bandwidth_gbps=10,
    monthly_data_transfer_tb=50
)

print(f"Direct Connect Cost: ${result['direct_connect_cost']:.2f}")
print(f"Internet Transfer Cost: ${result['internet_cost']:.2f}")
print(f"Monthly Savings: ${result['monthly_savings']:.2f}")
print(f"Break-even Point: {result['break_even_tb']:.1f} TB/month")
```

---

## 🎯 Best Practices Summary

### Network Design Principles
- [ ] **Defense in Depth:** Layer security controls (SG, NACL, WAF)
- [ ] **Least Privilege:** Grant minimum required network access
- [ ] **High Availability:** Design across multiple AZs
- [ ] **Scalability:** Use auto-scaling load balancers and endpoints
- [ ] **Performance:** Choose appropriate service tiers and configurations

### Security Best Practices
- [ ] **Enable VPC Flow Logs** for network monitoring and forensics
- [ ] **Use Security Groups as firewalls** with specific, minimal rules
- [ ] **Implement NACLs for subnet-level protection** as additional layer
- [ ] **Enable AWS Config** for compliance and configuration monitoring
- [ ] **Use AWS Certificate Manager** for SSL/TLS certificate management

### Performance Optimization
- [ ] **Right-size load balancers** based on traffic patterns
- [ ] **Optimize CloudFront caching** with appropriate TTL values
- [ ] **Use Route 53 health checks** for intelligent traffic routing
- [ ] **Monitor and analyze performance metrics** regularly
- [ ] **Implement connection pooling** and keep-alive for efficient connections

### Cost Management
- [ ] **Regularly review and optimize** service configurations
- [ ] **Use appropriate CloudFront price classes** for your geographic needs
- [ ] **Implement lifecycle policies** for log retention
- [ ] **Monitor data transfer costs** and optimize routing
- [ ] **Consider Reserved Capacity** for predictable workloads

---

*Last Updated: October 2025 | AWS SAA-C03 Study Guide*