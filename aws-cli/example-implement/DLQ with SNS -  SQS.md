## 1️⃣ How SNS Dead Letter Queue (DLQ) works — step by step

### 🧩 Architecture (your case)

```
Producer → SNS Topic → HTTPS endpoint (on-prem)
                          ↓
                    (delivery fails)
                          ↓
                    SQS Dead Letter Queue
```

---

### 🔄 Step-by-step flow

#### **Step 1: Application publishes a message**

Your ecommerce app publishes an order message to an **SNS topic**.

```text
Order created → SNS Publish
```

---

#### **Step 2: SNS attempts delivery**

SNS tries to deliver the message to the **HTTPS subscription** (on-prem warehouse).

* SNS retries automatically using **exponential backoff**
* Default retry period: **several hours**
* Reasons for failure:

  * Endpoint timeout
  * 5xx response
  * Network/VPN issue
  * TLS / certificate problem

---

#### **Step 3: Delivery fails after retries**

If SNS **cannot deliver** the message after all retries:

```text
SNS marks the message as undeliverable
```

---

#### **Step 4: SNS sends message to DLQ**

SNS **automatically sends the failed message** to the configured **SQS DLQ**.

What’s stored in the DLQ:

* Original message body
* Message attributes
* Failure metadata (why delivery failed)

---

#### **Step 5: Retain & analyze**

* SQS retains messages for **up to 14 days**
* Engineers can:

  * Inspect messages
  * Replay them
  * Analyze failure patterns

✅ **No message loss**
✅ **No custom retry code**
✅ **Minimal operational effort**

---

## 2️⃣ Implement SNS DLQ with AWS CLI (minimal & exam-correct)

### ✅ Prerequisites

* AWS CLI configured
* SNS topic already exists (or create one)

---

### **Step 1: Create the SQS DLQ (14-day retention)**

```bash
aws sqs create-queue \
  --queue-name sns-order-dlq \
  --attributes MessageRetentionPeriod=1209600
```

👉 `1209600 seconds = 14 days`

---

### **Step 2: Get the DLQ ARN**

```bash
aws sqs get-queue-attributes \
  --queue-url https://sqs.<region>.amazonaws.com/<account-id>/sns-order-dlq \
  --attribute-names QueueArn
```

Save the `QueueArn`.

---

### **Step 3: Allow SNS to send messages to the DLQ**

Create a policy file `sqs-dlq-policy.json`:

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "Allow-SNS-SendMessage",
      "Effect": "Allow",
      "Principal": {
        "Service": "sns.amazonaws.com"
      },
      "Action": "sqs:SendMessage",
      "Resource": "<DLQ_ARN>",
      "Condition": {
        "ArnEquals": {
          "aws:SourceArn": "<SNS_TOPIC_ARN>"
        }
      }
    }
  ]
}
```

Apply it:

```bash
aws sqs set-queue-attributes \
  --queue-url https://sqs.<region>.amazonaws.com/<account-id>/sns-order-dlq \
  --attributes Policy="$(cat sqs-dlq-policy.json)"
```

---

### **Step 4: Configure DLQ on the SNS subscription**

First, get the **subscription ARN**:

```bash
aws sns list-subscriptions-by-topic \
  --topic-arn <SNS_TOPIC_ARN>
```

Then attach the DLQ:

```bash
aws sns set-subscription-attributes \
  --subscription-arn <SUBSCRIPTION_ARN> \
  --attribute-name RedrivePolicy \
  --attribute-value '{
    "deadLetterTargetArn": "<DLQ_ARN>"
  }'
```

✅ Done — SNS DLQ is now active.

---

## 3️⃣ How to analyze failed messages

### 📥 Receive messages from DLQ

```bash
aws sqs receive-message \
  --queue-url https://sqs.<region>.amazonaws.com/<account-id>/sns-order-dlq \
  --max-number-of-messages 10
```

### 🔁 Replay messages (optional)

* Extract message body
* Re-publish to SNS:

```bash
aws sns publish \
  --topic-arn <SNS_TOPIC_ARN> \
  --message "<message-body>"
```

---

## 4️⃣ High-yield exam facts (memorize)

* SNS **supports DLQ only via SQS**
* Max SQS retention = **14 days**
* DLQ captures **undeliverable messages only**
* DLQ works for:

  * HTTPS
  * Lambda
  * SQS subscriptions
* **Least development effort** → configure, don’t code
