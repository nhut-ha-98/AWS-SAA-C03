# AWS Messaging & Eventing Services Guide 📨

*Comprehensive guide to AWS messaging, queuing, and event-driven architecture services*

## 🎯 Overview

AWS provides a comprehensive suite of messaging and eventing services to enable decoupled, scalable architectures. This guide helps you choose the right service for your communication patterns, from simple queuing to complex event-driven systems.

---

## 🚀 Quick Service Selection Table

| Service                               | Communication Type        | Delivery Model        | Retention       | Ideal For                                  | Example Use Case                         |
| ------------------------------------- | ------------------------- | --------------------- | --------------- | ------------------------------------------ | ---------------------------------------- |
| **SQS (Simple Queue Service)**        | Point-to-point            | Pull (poll)           | Up to 14 days   | Decoupling producers and workers           | Job queue for EC2/Lambda workers         |
| **SNS (Simple Notification Service)** | One-to-many               | Push                  | No persistence  | Fan-out notifications                      | Send alerts to email, SMS, Lambda        |
| **EventBridge**                       | Many-to-many (Event Bus)  | Push                  | Short retention | Event-driven integrations, filtering, SaaS | Trigger workflows when S3 object created |
| **Kinesis Data Streams**              | Many-to-many (Stream)     | Pull (shard consumer) | 24h–7d          | Real-time analytics, log ingestion         | Streaming sensor or click data           |
| **Step Functions**                    | Orchestration             | State machine         | Managed state   | Workflow coordination                      | Chain Lambdas for data processing        |
| **Lambda Event Source Mapping**       | Depends (SQS/Kinesis/SNS) | Pull/Push             | —               | Auto-scale serverless consumers            | Trigger Lambda per queue or stream event |

---

## 🌳 Messaging Service Decision Tree

```
Do you need to send data between system components?
│
├──> No → ❌ No messaging needed
│
└──> Yes
     │
     ├── What communication pattern do you need?
     │   │
     │   ├── Real-time event routing (publish-subscribe) → Continue to Event Routing ↓
     │   ├── Asynchronous job/work queue (producer-consumer) → Continue to Queue Type ↓
     │   ├── Workflow orchestration → ✅ Step Functions
     │   └── Request-response (synchronous) → Use API Gateway + Lambda
     │
     ├── EVENT ROUTING BRANCH:
     │   │
     │   ├── Do you need one-to-many fanout?
     │   │   │
     │   │   ├── Yes (simple broadcast) → ✅ SNS
     │   │   └── No → Continue to advanced routing ↓
     │   │
     │   ├── Do you need event filtering, transformation, or SaaS integration?
     │   │   │
     │   │   ├── Yes → ✅ EventBridge
     │   │   └── No → Continue to streaming ↓
     │   │
     │   └── Do you need high-throughput streaming analytics?
     │       │
     │       ├── Yes → ✅ Kinesis Data Streams
     │       └── No → ✅ SNS (simple fanout)
     │
     └── QUEUE TYPE BRANCH:
         │
         ├── What's your throughput requirement?
         │   │
         │   ├── High (>300,000 messages/sec) → ✅ Kinesis Data Streams
         │   └── Standard (<300,000 messages/sec) → Continue ↓
         │
         ├── Do you need message ordering?
         │   │
         │   ├── Yes (strict ordering) → ✅ SQS FIFO Queue
         │   └── No (eventual consistency OK) → ✅ SQS Standard Queue
         │
         └── Do you need workflow coordination?
             │
             ├── Yes → ✅ Step Functions + SQS/SNS
             └── No → ✅ SQS Standard Queue
```

---

## 🔧 Service Deep Dive

### 📬 Amazon SQS (Simple Queue Service)
*Fully managed message queuing service*

**Queue Types:**

**Standard Queue:**
- ✅ Unlimited throughput
- ✅ At-least-once delivery
- ⚠️ Best-effort ordering
- ⚠️ Possible duplicate messages

**FIFO Queue:**
- ✅ Exactly-once processing
- ✅ Strict message ordering
- ✅ No duplicate messages
- ⚠️ Limited to 300 messages/sec (3,000 with batching)

**Key Features & Configuration:**

**Message Attributes:**
```json
{
    "DelaySeconds": 0,              // Delay delivery (0-900 seconds)
    "MaxReceiveCount": 3,           // Max retries before DLQ
    "MessageRetentionPeriod": 1209600, // 14 days max retention
    "VisibilityTimeoutSeconds": 30,  // Hide message during processing
    "ReceiveMessageWaitTimeSeconds": 20 // Long polling (saves costs)
}
```

**Dead Letter Queue Setup:**
```python
import boto3
import json

sqs = boto3.client('sqs')

# Create main queue
main_queue = sqs.create_queue(
    QueueName='order-processing-queue',
    Attributes={
        'DelaySeconds': '0',
        'MaxReceiveCount': '3',
        'MessageRetentionPeriod': '1209600',
        'VisibilityTimeoutSeconds': '300'
    }
)

# Create dead letter queue
dlq = sqs.create_queue(
    QueueName='order-processing-dlq'
)

# Configure DLQ policy
dlq_policy = {
    "deadLetterTargetArn": dlq['QueueUrl'],
    "maxReceiveCount": 3
}

sqs.set_queue_attributes(
    QueueUrl=main_queue['QueueUrl'],
    Attributes={
        'RedrivePolicy': json.dumps(dlq_policy)
    }
)
```

**Polling Strategies:**

**Short Polling (Default):**
```python
# Returns immediately, may return empty even if messages exist
response = sqs.receive_message(
    QueueUrl=queue_url,
    MaxNumberOfMessages=10
)
```

**Long Polling (Recommended):**
```python
# Waits for messages, reduces API calls and costs
response = sqs.receive_message(
    QueueUrl=queue_url,
    MaxNumberOfMessages=10,
    WaitTimeSeconds=20  # Long polling
)
```

**Use Case Examples:**

**E-commerce Order Processing:**
```
Flow:
1. User places order → SQS Standard Queue
2. Lambda function processes payment
3. Success → Send to fulfillment queue
4. Failure → DLQ for manual review
```

**Batch Job Processing:**
```python
# Producer: Add jobs to queue
import boto3
import json

sqs = boto3.client('sqs')

def submit_batch_job(job_data):
    sqs.send_message(
        QueueUrl='batch-processing-queue',
        MessageBody=json.dumps(job_data),
        MessageAttributes={
            'JobType': {
                'StringValue': 'data-processing',
                'DataType': 'String'
            },
            'Priority': {
                'StringValue': 'high',
                'DataType': 'String'
            }
        }
    )

# Consumer: Process jobs
def process_jobs():
    while True:
        messages = sqs.receive_message(
            QueueUrl='batch-processing-queue',
            MaxNumberOfMessages=10,
            WaitTimeSeconds=20,
            MessageAttributeNames=['All']
        )
        
        for message in messages.get('Messages', []):
            try:
                job_data = json.loads(message['Body'])
                process_job(job_data)
                
                # Delete message after successful processing
                sqs.delete_message(
                    QueueUrl='batch-processing-queue',
                    ReceiptHandle=message['ReceiptHandle']
                )
            except Exception as e:
                print(f"Job processing failed: {e}")
                # Message will become visible again after visibility timeout
```

### 📢 Amazon SNS (Simple Notification Service)
*Fully managed pub/sub messaging service*

**Key Features:**
- ✅ Push-based delivery
- ✅ Multiple subscription types
- ✅ Message filtering
- ✅ Mobile push notifications
- ✅ Fan-out to multiple services

**Subscription Types:**

| Type | Use Case | Example |
|------|----------|---------|
| **HTTP/HTTPS** | Webhook endpoints | Slack notifications, external APIs |
| **Email/Email-JSON** | Human notifications | Alert emails, reports |
| **SMS** | Mobile notifications | OTP codes, urgent alerts |
| **SQS** | Reliable processing | Fan-out to multiple queues |
| **Lambda** | Serverless processing | Trigger functions |
| **Mobile Push** | App notifications | iOS/Android push notifications |

**Topic Configuration:**
```python
import boto3
import json

sns = boto3.client('sns')

# Create topic
topic = sns.create_topic(Name='order-notifications')
topic_arn = topic['TopicArn']

# Add email subscription
sns.subscribe(
    TopicArn=topic_arn,
    Protocol='email',
    Endpoint='admin@company.com'
)

# Add SQS subscription with filter
sqs_subscription = sns.subscribe(
    TopicArn=topic_arn,
    Protocol='sqs',
    Endpoint='arn:aws:sqs:us-east-1:123456789012:high-priority-queue'
)

# Set message filtering
filter_policy = {
    "order_status": ["shipped", "delivered"],
    "order_value": [{"numeric": [">=", 100]}]
}

sns.set_subscription_attributes(
    SubscriptionArn=sqs_subscription['SubscriptionArn'],
    AttributeName='FilterPolicy',
    AttributeValue=json.dumps(filter_policy)
)
```

**Message Publishing with Attributes:**
```python
def publish_order_notification(order_id, status, value):
    message = {
        "order_id": order_id,
        "status": status,
        "timestamp": datetime.now().isoformat(),
        "details": "Order processing update"
    }
    
    sns.publish(
        TopicArn=topic_arn,
        Message=json.dumps(message),
        Subject=f"Order {order_id} - Status: {status}",
        MessageAttributes={
            'order_status': {
                'DataType': 'String',
                'StringValue': status
            },
            'order_value': {
                'DataType': 'Number',
                'StringValue': str(value)
            }
        }
    )
```

**Fan-out Architecture Pattern:**
```
           ┌─────────────────┐
           │   Order Event   │
           │   (SNS Topic)   │
           └────────┬────────┘
                    │
        ┌───────────┼───────────┐
        │           │           │
   ┌────▼────┐ ┌───▼───┐ ┌────▼────┐
   │Email    │ │ SMS   │ │ SQS     │
   │Alert    │ │Alert  │ │Queue    │
   └─────────┘ └───────┘ └────┬────┘
                              │
                         ┌────▼────┐
                         │ Lambda  │
                         │Function │
                         └─────────┘
```

### 🌉 Amazon EventBridge
*Serverless event bus service*

**Key Concepts:**
- **Event Bus:** Container for events
- **Rules:** Filter and route events
- **Targets:** Services that process events
- **Patterns:** JSON patterns for event matching

**Event Bus Types:**
1. **Default Bus:** Receives AWS service events
2. **Custom Bus:** For application events
3. **Partner Bus:** SaaS integrations (Shopify, Zendesk, etc.)

**Event Pattern Examples:**
```json
{
  "source": ["aws.s3"],
  "detail-type": ["Object Created"],
  "detail": {
    "bucket": {
      "name": ["my-important-bucket"]
    },
    "object": {
      "key": [{"prefix": "uploads/"}]
    }
  }
}
```

**Rule Configuration:**
```python
import boto3

eventbridge = boto3.client('events')

# Create custom event bus
eventbridge.create_event_bus(Name='order-processing-bus')

# Create rule for order events
rule_response = eventbridge.put_rule(
    Name='ProcessHighValueOrders',
    EventBusName='order-processing-bus',
    EventPattern=json.dumps({
        "source": ["ecommerce.orders"],
        "detail-type": ["Order Placed"],
        "detail": {
            "order_value": [{"numeric": [">=", 1000]}],
            "status": ["confirmed"]
        }
    }),
    State='ENABLED',
    Description='Process high-value orders'
)

# Add Lambda target
eventbridge.put_targets(
    Rule='ProcessHighValueOrders',
    EventBusName='order-processing-bus',
    Targets=[
        {
            'Id': '1',
            'Arn': 'arn:aws:lambda:us-east-1:123456789012:function:ProcessHighValueOrder',
            'InputTransformer': {
                'InputPathsMap': {
                    'order_id': '$.detail.order_id',
                    'customer_id': '$.detail.customer_id',
                    'amount': '$.detail.order_value'
                },
                'InputTemplate': '{"order": "<order_id>", "customer": "<customer_id>", "amount": <amount>}'
            }
        }
    ]
)
```

**Publishing Custom Events:**
```python
def publish_order_event(order_data):
    eventbridge.put_events(
        Entries=[
            {
                'Source': 'ecommerce.orders',
                'DetailType': 'Order Placed',
                'Detail': json.dumps({
                    'order_id': order_data['id'],
                    'customer_id': order_data['customer_id'],
                    'order_value': order_data['total'],
                    'status': 'confirmed',
                    'items': order_data['items'],
                    'timestamp': datetime.now().isoformat()
                }),
                'EventBusName': 'order-processing-bus'
            }
        ]
    )
```

**SaaS Integration Example (Shopify):**
```python
# EventBridge automatically receives Shopify events
# Rule to handle new orders from Shopify
shopify_rule = {
    "source": ["aws.partner/shopify.com/123456/mystore"],
    "detail-type": ["Order Created"],
    "detail": {
        "financial_status": ["paid"],
        "total_price": [{"numeric": [">", 0]}]
    }
}
```

### 🌊 Amazon Kinesis Data Streams
*Real-time data streaming service*

**Key Concepts:**
- **Shards:** Parallel processing units
- **Records:** Individual data items
- **Partition Key:** Determines shard assignment
- **Sequence Number:** Unique record identifier

**Stream Configuration:**
```python
import boto3

kinesis = boto3.client('kinesis')

# Create stream with 4 shards
kinesis.create_stream(
    StreamName='user-activity-stream',
    ShardCount=4
)

# Put record with partition key
kinesis.put_record(
    StreamName='user-activity-stream',
    Data=json.dumps({
        'user_id': '12345',
        'action': 'page_view',
        'page': '/products/123',
        'timestamp': datetime.now().isoformat(),
        'session_id': 'sess_abc123'
    }),
    PartitionKey='user_12345'  # Routes to same shard for user
)

# Batch put for efficiency
records = []
for i in range(100):
    records.append({
        'Data': json.dumps({'event': f'event_{i}'}),
        'PartitionKey': f'partition_{i % 4}'
    })

kinesis.put_records(
    StreamName='user-activity-stream',
    Records=records
)
```

**Consumer Patterns:**

**Lambda Consumer (Event Source Mapping):**
```python
# Lambda function automatically triggered by Kinesis
def lambda_handler(event, context):
    for record in event['Records']:
        # Kinesis data is base64 encoded
        payload = json.loads(base64.b64decode(record['kinesis']['data']))
        
        # Process the record
        process_user_activity(payload)
        
    return {'statusCode': 200}
```

**Kinesis Client Library (KCL) Consumer:**
```python
from amazon_kclpy import kcl

class RecordProcessor(kcl.RecordProcessorBase):
    def process_records(self, process_records_input):
        try:
            for record in process_records_input.records:
                data = json.loads(record.data)
                # Process record
                self.process_record(data)
                
            # Checkpoint after successful processing
            process_records_input.checkpointer.checkpoint()
        except Exception as e:
            print(f"Error processing records: {e}")

    def process_record(self, data):
        # Your business logic here
        pass
```

**Scaling Considerations:**

**Shard Calculation:**
```
Incoming Data Rate: 1000 records/sec × 1KB average = 1MB/sec
Shard Capacity: 1MB/sec or 1000 records/sec per shard
Required Shards: max(1MB/1MB, 1000/1000) = 1 shard minimum

With growth buffer: 2-3 shards recommended
```

**Auto Scaling with Lambda:**
```python
import boto3

def lambda_handler(event, context):
    cloudwatch = boto3.client('cloudwatch')
    kinesis = boto3.client('kinesis')
    
    # Get stream metrics
    metrics = cloudwatch.get_metric_statistics(
        Namespace='AWS/Kinesis',
        MetricName='IncomingRecords',
        Dimensions=[{'Name': 'StreamName', 'Value': 'user-activity-stream'}],
        StartTime=datetime.now() - timedelta(minutes=5),
        EndTime=datetime.now(),
        Period=300,
        Statistics=['Sum']
    )
    
    # Scale if needed (simplified logic)
    current_shards = get_shard_count('user-activity-stream')
    if metrics['Datapoints'] and metrics['Datapoints'][0]['Sum'] > 4000:
        # Scale up
        kinesis.update_shard_count(
            StreamName='user-activity-stream',
            TargetShardCount=current_shards + 1,
            ScalingType='UNIFORM_SCALING'
        )
```

### 🔄 AWS Step Functions
*Visual workflow service*

**State Types:**
- **Task:** Execute work (Lambda, ECS, etc.)
- **Choice:** Conditional branching
- **Wait:** Delay execution
- **Parallel:** Execute branches concurrently
- **Map:** Process array of items
- **Pass:** Pass input to output
- **Fail/Succeed:** End states

**State Machine Definition:**
```json
{
  "Comment": "Order Processing Workflow",
  "StartAt": "ValidateOrder",
  "States": {
    "ValidateOrder": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:ValidateOrder",
      "Next": "ProcessPayment",
      "Catch": [
        {
          "ErrorEquals": ["ValidationError"],
          "Next": "ValidationFailed"
        }
      ]
    },
    "ProcessPayment": {
      "Type": "Task",
      "Resource": "arn:aws:lambda:us-east-1:123456789012:function:ProcessPayment",
      "Next": "PaymentChoice",
      "Retry": [
        {
          "ErrorEquals": ["PaymentServiceTimeout"],
          "IntervalSeconds": 2,
          "MaxAttempts": 3,
          "BackoffRate": 2.0
        }
      ]
    },
    "PaymentChoice": {
      "Type": "Choice",
      "Choices": [
        {
          "Variable": "$.payment.status",
          "StringEquals": "SUCCESS",
          "Next": "ProcessOrder"
        },
        {
          "Variable": "$.payment.status",
          "StringEquals": "FAILED",
          "Next": "PaymentFailed"
        }
      ],
      "Default": "PaymentFailed"
    },
    "ProcessOrder": {
      "Type": "Parallel",
      "Branches": [
        {
          "StartAt": "UpdateInventory",
          "States": {
            "UpdateInventory": {
              "Type": "Task",
              "Resource": "arn:aws:lambda:us-east-1:123456789012:function:UpdateInventory",
              "End": true
            }
          }
        },
        {
          "StartAt": "SendConfirmation",
          "States": {
            "SendConfirmation": {
              "Type": "Task",
              "Resource": "arn:aws:lambda:us-east-1:123456789012:function:SendConfirmation",
              "End": true
            }
          }
        }
      ],
      "Next": "OrderSuccess"
    },
    "OrderSuccess": {
      "Type": "Succeed"
    },
    "ValidationFailed": {
      "Type": "Fail",
      "Cause": "Order validation failed"
    },
    "PaymentFailed": {
      "Type": "Fail",
      "Cause": "Payment processing failed"
    }
  }
}
```

**Starting Executions:**
```python
import boto3
import json

stepfunctions = boto3.client('stepfunctions')

def start_order_workflow(order_data):
    response = stepfunctions.start_execution(
        stateMachineArn='arn:aws:states:us-east-1:123456789012:stateMachine:OrderProcessing',
        name=f"order-{order_data['order_id']}-{int(time.time())}",
        input=json.dumps(order_data)
    )
    return response['executionArn']

# Monitor execution
def get_execution_status(execution_arn):
    response = stepfunctions.describe_execution(executionArn=execution_arn)
    return {
        'status': response['status'],
        'output': response.get('output'),
        'error': response.get('error')
    }
```

---

## 🏗️ Integration Patterns

### Pattern 1: Event-Driven Microservices
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Order API     │ -> │   EventBridge   │ -> │  Microservices  │
│   (API Gateway) │    │   (Event Bus)   │    │   (Lambdas)     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │                         │
                              │                         │
                       ┌──────▼──────┐           ┌─────▼─────┐
                       │   SNS Topic │           │    SQS    │
                       │ (Broadcast) │           │  Queues   │
                       └─────────────┘           └───────────┘
```

### Pattern 2: Reliable Message Processing
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Producer      │ -> │   SQS Queue     │ -> │   Consumer      │
│   Application   │    │   (Standard)    │    │   (Lambda)      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │                         │
                              │                    ┌────▼────┐
                       ┌──────▼──────┐           │  Success │
                       │   Dead       │           └─────────┘
                       │   Letter     │           ┌─────────┐
                       │   Queue      │           │ Failure │
                       └─────────────┘           │ (Retry) │
                                                 └─────────┘
```

### Pattern 3: Real-time Analytics Pipeline
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   Web/Mobile    │ -> │   Kinesis       │ -> │   Kinesis       │
│   Applications  │    │   Data Streams  │    │   Analytics     │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │                         │
                              │                         │
                       ┌──────▼──────┐           ┌─────▼─────┐
                       │   Lambda     │           │ Real-time │
                       │  (Real-time) │           │Dashboard  │
                       └─────────────┘           └───────────┘
```

### Pattern 4: Workflow Orchestration
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│   API Request   │ -> │ Step Functions  │ -> │   Multiple      │
│                 │    │  (Workflow)     │    │   Services      │
└─────────────────┘    └─────────────────┘    └─────────────────┘
                              │                         │
                              │                         │
                       ┌──────▼──────┐           ┌─────▼─────┐
                       │   Error      │           │   SNS     │
                       │   Handling   │           │Notification│
                       └─────────────┘           └───────────┘
```

---

## 🧠 Service Selection Quick Guide

### When to Use SQS
✅ **Perfect For:**
- Decoupling application components
- Reliable message delivery required
- Variable processing times
- Dead letter queue functionality needed
- Cost-effective solution for standard throughput

❌ **Avoid When:**
- Need real-time/streaming data processing
- Require fan-out to multiple subscribers
- Need event filtering and routing
- Messages need immediate processing

### When to Use SNS
✅ **Perfect For:**
- Broadcasting messages to multiple subscribers
- Push notifications (email, SMS, mobile)
- Fan-out pattern implementation
- Integration with AWS services
- Real-time alerts and notifications

❌ **Avoid When:**
- Need message persistence and reliability
- Require exactly-once delivery
- Need complex message routing
- Processing large message volumes

### When to Use EventBridge
✅ **Perfect For:**
- Event-driven microservices architecture
- SaaS application integration
- Complex event filtering and routing
- Cross-account event sharing
- Serverless workflows

❌ **Avoid When:**
- Need high-throughput streaming (>10,000 events/sec)
- Simple point-to-point messaging
- Real-time analytics processing
- Cost is primary concern (can be expensive)

### When to Use Kinesis
✅ **Perfect For:**
- Real-time data streaming and analytics
- High-throughput data ingestion (>100k records/sec)
- Ordered data processing
- Multiple consumers of same data stream
- Real-time dashboards and monitoring

❌ **Avoid When:**
- Simple request-response patterns
- Low throughput requirements (<1000 records/sec)
- Don't need real-time processing
- Message delivery guarantees more important than speed

### When to Use Step Functions
✅ **Perfect For:**
- Complex multi-step workflows
- Coordinating multiple AWS services
- Long-running processes with state management
- Business process automation
- Error handling and retry logic

❌ **Avoid When:**
- Simple linear processing
- High-frequency micro-workflows
- Real-time processing requirements
- Cost-sensitive applications (can be expensive)

---

## 💡 Real-World Scenarios

### Scenario 1: E-commerce Platform
**Requirements:** Handle orders, inventory, notifications, and fulfillment

**Architecture:**
```
Order Placed (API Gateway)
    ↓
EventBridge (Order Event Bus)
    ↓
├── Inventory Service (Lambda + SQS)
├── Payment Service (Step Functions)
├── Notification Service (SNS → Email/SMS)
└── Analytics Service (Kinesis Data Streams)
```

**Implementation:**
1. **Order Event:** EventBridge captures order placement
2. **Inventory Check:** SQS queue for reliable inventory processing
3. **Payment Workflow:** Step Functions for complex payment logic
4. **Notifications:** SNS for customer and admin alerts
5. **Analytics:** Kinesis for real-time order tracking

### Scenario 2: IoT Data Processing
**Requirements:** Process millions of sensor readings with real-time alerts

**Architecture:**
```
IoT Devices
    ↓
Kinesis Data Streams (High throughput)
    ↓
├── Real-time Analytics (Kinesis Analytics)
├── Anomaly Detection (Lambda)
├── Data Lake Storage (Kinesis Firehose → S3)
└── Alert System (SNS → PagerDuty/Slack)
```

### Scenario 3: Content Management System
**Requirements:** Process uploads, generate thumbnails, update search index

**Architecture:**
```
File Upload (S3)
    ↓
S3 Event → EventBridge
    ↓
├── Image Processing (SQS → Lambda)
├── Search Index Update (SQS FIFO → Lambda)
├── CDN Invalidation (SNS → CloudFront)
└── User Notification (SNS → WebSocket API)
```

### Scenario 4: Financial Trading Platform
**Requirements:** Process trades with strict ordering and audit trails

**Architecture:**
```
Trade Orders
    ↓
SQS FIFO Queue (Strict ordering)
    ↓
Step Functions (Trade Workflow)
    ↓
├── Risk Assessment (Lambda)
├── Order Matching (Lambda)
├── Settlement (Lambda)
└── Audit Trail (Kinesis → S3 → Athena)
```

---

## 📊 Performance & Scaling

### SQS Scaling Characteristics
```
Standard Queue:
├─ Throughput: Unlimited
├─ Batch Size: Up to 10 messages
├─ Message Size: Up to 256 KB
├─ Scaling: Automatic
└─ Latency: Low (< 10ms)

FIFO Queue:
├─ Throughput: 300 TPS (3,000 with batching)
├─ Batch Size: Up to 10 messages
├─ Message Size: Up to 256 KB
├─ Scaling: Limited by design
└─ Latency: Low (< 10ms)
```

### SNS Scaling Characteristics
```
Throughput: 300,000 messages/second (standard)
Fan-out: Unlimited subscribers
Message Size: Up to 256 KB
Delivery: Push (immediate)
Retry: Automatic with exponential backoff
```

### EventBridge Scaling Characteristics
```
Throughput: 10,000 events/second per region (soft limit)
Rules: 300 per event bus (soft limit)
Targets: 5 per rule
Event Size: Up to 256 KB
Latency: Near real-time (< 500ms)
```

### Kinesis Scaling Characteristics
```
Per Shard:
├─ Ingestion: 1,000 records/sec or 1 MB/sec
├─ Consumption: 2 MB/sec or 5 reads/sec per consumer
├─ Record Size: Up to 1 MB
└─ Retention: 24 hours to 7 days

Stream Level:
├─ Shards: 1 to 100,000+ (no hard limit)
├─ Scaling: Manual or auto-scaling
└─ Total Throughput: Shards × Per-shard limits
```

---

## 💰 Cost Optimization

### SQS Cost Optimization
```
Pricing Factors:
├─ Requests: $0.40 per million requests (first 1M free)
├─ Data Transfer: Standard rates
└─ Additional Features: Free

Optimization Tips:
├─ Use batching (up to 10 messages per request)
├─ Implement long polling (reduces empty receives)
├─ Right-size visibility timeouts
└─ Use SQS for appropriate use cases only
```

### SNS Cost Optimization
```
Pricing:
├─ Publish: $0.50 per million requests (first 1M free)
├─ Email: $2.00 per 100,000 notifications
├─ SMS: $0.75 per 100 notifications (US)
├─ Mobile Push: $0.50 per million notifications
└─ HTTP/SQS: $0.50 per million notifications

Optimization:
├─ Use message filtering to reduce unnecessary deliveries
├─ Batch notifications when possible
├─ Choose appropriate notification channels
└─ Monitor and optimize subscription patterns
```

### EventBridge Cost Optimization
```
Pricing:
├─ Custom Events: $1.00 per million events
├─ Third-party Events: $1.00 per million events
├─ Cross-region Replication: $0.01 per GB
└─ Archive/Replay: Additional charges

Optimization:
├─ Use efficient event filtering
├─ Minimize cross-region event replication
├─ Archive only necessary events
└─ Consider SNS for simple fan-out scenarios
```

### Kinesis Cost Optimization
```
Pricing:
├─ Shard Hour: $0.015 per shard per hour
├─ PUT Payload Units: $0.014 per million units
├─ Extended Retention: $0.023 per shard per hour
└─ Enhanced Fan-out: $0.013 per consumer per hour

Optimization:
├─ Right-size shard count based on actual throughput
├─ Use batch puts to reduce payload unit costs
├─ Implement appropriate data retention policies
├─ Monitor shard utilization and merge underutilized shards
└─ Use standard consumers unless enhanced fan-out is required
```

---

## 🔒 Security Best Practices

### IAM Policies and Permissions

**SQS Least Privilege Policy:**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "sqs:SendMessage",
                "sqs:ReceiveMessage",
                "sqs:DeleteMessage",
                "sqs:GetQueueAttributes"
            ],
            "Resource": "arn:aws:sqs:us-east-1:123456789012:order-processing-queue",
            "Condition": {
                "StringEquals": {
                    "aws:SourceAccount": "123456789012"
                }
            }
        }
    ]
}
```

**EventBridge Cross-Account Policy:**
```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Principal": {
                "AWS": "arn:aws:iam::TRUSTED-ACCOUNT:root"
            },
            "Action": "events:PutEvents",
            "Resource": "arn:aws:events:us-east-1:123456789012:event-bus/shared-event-bus",
            "Condition": {
                "StringEquals": {
                    "events:source": "trusted.application"
                }
            }
        }
    ]
}
```

### Encryption and Data Protection

**SQS Encryption Configuration:**
```python
# Enable KMS encryption for SQS queue
sqs.create_queue(
    QueueName='secure-queue',
    Attributes={
        'KmsMasterKeyId': 'alias/aws/sqs',  # Use AWS managed key
        'KmsDataKeyReusePeriodSeconds': '300'
    }
)

# Custom KMS key
sqs.create_queue(
    QueueName='highly-secure-queue',
    Attributes={
        'KmsMasterKeyId': 'arn:aws:kms:us-east-1:123456789012:key/12345678-1234-1234-1234-123456789012',
        'KmsDataKeyReusePeriodSeconds': '300'
    }
)
```

**Kinesis Encryption:**
```python
# Enable server-side encryption
kinesis.enable_stream_encryption(
    StreamName='secure-stream',
    EncryptionType='KMS',
    KeyId='alias/aws/kinesis'
)
```

### Network Security

**VPC Endpoints for Private Access:**
```bash
# Create VPC endpoint for SQS
aws ec2 create-vpc-endpoint \
    --vpc-id vpc-12345678 \
    --service-name com.amazonaws.us-east-1.sqs \
    --vpc-endpoint-type Interface \
    --subnet-ids subnet-12345678 \
    --security-group-ids sg-12345678 \
    --private-dns-enabled
```

---

## 🔧 Monitoring & Troubleshooting

### CloudWatch Metrics and Alarms

**SQS Monitoring:**
```python
import boto3

cloudwatch = boto3.client('cloudwatch')

# Create alarm for queue depth
cloudwatch.put_metric_alarm(
    AlarmName='SQS-Queue-Depth-High',
    ComparisonOperator='GreaterThanThreshold',
    EvaluationPeriods=2,
    MetricName='ApproximateNumberOfVisibleMessages',
    Namespace='AWS/SQS',
    Period=300,
    Statistic='Average',
    Threshold=1000.0,
    ActionsEnabled=True,
    AlarmActions=[
        'arn:aws:sns:us-east-1:123456789012:sqs-alerts'
    ],
    AlarmDescription='Queue depth is too high',
    Dimensions=[
        {
            'Name': 'QueueName',
            'Value': 'order-processing-queue'
        }
    ]
)

# Create alarm for age of oldest message
cloudwatch.put_metric_alarm(
    AlarmName='SQS-Message-Age-High',
    ComparisonOperator='GreaterThanThreshold',
    EvaluationPeriods=1,
    MetricName='ApproximateAgeOfOldestMessage',
    Namespace='AWS/SQS',
    Period=300,
    Statistic='Maximum',
    Threshold=600.0,  # 10 minutes
    ActionsEnabled=True,
    AlarmActions=[
        'arn:aws:sns:us-east-1:123456789012:sqs-alerts'
    ],
    AlarmDescription='Messages are aging in queue'
)
```

**Kinesis Monitoring:**
```python
# Monitor shard utilization
def monitor_shard_utilization(stream_name):
    metrics = cloudwatch.get_metric_statistics(
        Namespace='AWS/Kinesis',
        MetricName='IncomingRecords',
        Dimensions=[
            {'Name': 'StreamName', 'Value': stream_name}
        ],
        StartTime=datetime.now() - timedelta(hours=1),
        EndTime=datetime.now(),
        Period=300,
        Statistics=['Sum', 'Average']
    )
    
    # Calculate utilization
    for datapoint in metrics['Datapoints']:
        utilization = (datapoint['Sum'] / 300) / 1000 * 100  # % of 1000 records/sec limit
        if utilization > 80:
            print(f"High shard utilization: {utilization}%")
```

### Common Issues and Solutions

**SQS Issues:**
```
Issue: Messages not being processed
Solutions:
├─ Check dead letter queue for failed messages
├─ Verify consumer is polling with correct credentials
├─ Check visibility timeout (too short/long)
├─ Monitor ReceiveCount for stuck messages
└─ Verify message retention period

Issue: Duplicate message processing
Solutions:
├─ Implement idempotency in consumer logic
├─ Use FIFO queue if order matters
├─ Check for multiple consumers racing
└─ Implement proper error handling
```

**EventBridge Issues:**
```
Issue: Events not triggering targets
Solutions:
├─ Verify event pattern matching (test with CLI)
├─ Check IAM permissions for targets
├─ Monitor failed invocations metric
├─ Validate JSON structure of events
└─ Check event bus permissions

Issue: High latency in event processing
Solutions:
├─ Optimize target function cold starts
├─ Use reserved concurrency for critical functions
├─ Consider async processing patterns
└─ Monitor target execution duration
```

**Kinesis Issues:**
```
Issue: High write throttling
Solutions:
├─ Increase shard count
├─ Optimize partition key distribution
├─ Implement exponential backoff
├─ Use batch puts instead of individual puts
└─ Monitor hot shard metrics

Issue: Consumer lag increasing
Solutions:
├─ Scale out consumers (add more instances)
├─ Optimize consumer processing logic
├─ Use parallel processing within consumer
├─ Consider Kinesis Analytics for real-time processing
└─ Monitor iterator age metrics
```

---

## 🎯 Best Practices Summary

### Design Principles
- [ ] **Loose Coupling:** Use messaging to decouple system components
- [ ] **Fault Tolerance:** Implement proper error handling and retry logic
- [ ] **Scalability:** Choose services that can scale with your needs
- [ ] **Security:** Use IAM, encryption, and network controls appropriately
- [ ] **Cost Optimization:** Right-size resources and use appropriate pricing models

### Implementation Guidelines
- [ ] **Message Design:** Keep messages small, self-contained, and versioned
- [ ] **Idempotency:** Ensure operations can be safely retried
- [ ] **Monitoring:** Implement comprehensive monitoring and alerting
- [ ] **Testing:** Test failure scenarios and scaling limits
- [ ] **Documentation:** Document message schemas and integration patterns

### Performance Optimization
- [ ] **Batching:** Use batch operations where supported
- [ ] **Parallelization:** Design for parallel processing
- [ ] **Caching:** Cache frequently accessed data
- [ ] **Right-sizing:** Match service characteristics to use case requirements
- [ ] **Monitoring:** Continuously monitor and optimize based on metrics

---

*Last Updated: October 2025 | AWS SAA-C03 Study Guide*