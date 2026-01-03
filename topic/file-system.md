
# 🧭 AWS FILE SYSTEM — DECISION WORKFLOW

Think in this exact order 👇
(90% of exam questions collapse once you follow this path)

---

## ① Is this **BLOCK** or **FILE** storage?

### 🟦 Block storage

* Single instance (or limited sharing)
* OS-level disks
* Databases

👉 **EBS** (gp3 / io1 / io2)

⛔ STOP — not a file system question

---

### 🟩 File storage (shared files)

* Multiple instances
* POSIX / NFS-style access

👉 Continue ↓

---

## ② Is this **HPC / high-performance computing**?

Keywords:

* HPC
* Sub-millisecond latency
* Massive parallel access
* Thousands of nodes
* Scientific workloads (weather, genomics, ML)

### ✅ YES → **FSx for Lustre**

Now choose type:

#### 🔹 Temporary / re-creatable data?

👉 **FSx for Lustre – Scratch**

#### 🔹 Durable / highly available?

👉 **FSx for Lustre – Persistent**

⛔ STOP — answer found

---

### ❌ NO → Continue ↓

---

## ③ Is this **Windows** or **Linux / Unix**?

### 🪟 Windows-based workloads?

Keywords:

* Windows Server
* SMB
* Active Directory
* .NET apps
* Lift-and-shift Windows apps

👉 **Amazon FSx for Windows File Server**

⛔ STOP

---

### 🐧 Linux / Unix workloads?

👉 Continue ↓

---

## ④ Do you need **extreme performance**?

Keywords:

* Very high IOPS
* Low latency
* Heavy parallel access
* Enterprise NAS workloads

👉 **Amazon FSx for NetApp ONTAP**

Use when:

* You need snapshots, cloning
* Advanced data management
* High performance but **not HPC**

⛔ STOP

---

### ❌ Normal performance → Continue ↓

---

## ⑤ Do you need **simple, scalable, serverless** file storage?

Keywords:

* NFS
* Containers
* Kubernetes (EKS)
* Lambda (via EFS)
* Web apps
* Shared config / uploads

👉 **Amazon EFS**

Now choose throughput mode:

---

## ⑥ EFS Throughput mode decision

### 🔹 Spiky / unpredictable traffic?

👉 **EFS Bursting Throughput**

* Default
* Cheaper
* Depends on stored data size

---

### 🔹 Sustained / predictable throughput?

👉 **EFS Provisioned Throughput**

* Pay for guaranteed throughput
* Independent of size

⛔ STOP

---

# 🧠 ONE-PAGE MEMORY MAP (EXAM GOLD)

```
BLOCK?
 └─ EBS

FILE?
 ├─ HPC? ── FSx for Lustre
 │          ├─ Scratch (temp)
 │          └─ Persistent (HA)
 │
 ├─ Windows? ── FSx Windows
 │
 ├─ Extreme NAS? ── FSx NetApp ONTAP
 │
 └─ General purpose? ── EFS
              ├─ Bursting
              └─ Provisioned
```

---

# 🧪 Keyword → Service Mapping (INSTANT PICK)

| Keyword in question      | Auto-pick        |
| ------------------------ | ---------------- |
| Sub-millisecond latency  | FSx for Lustre   |
| Thousands of nodes       | FSx for Lustre   |
| Windows + SMB            | FSx Windows      |
| Kubernetes / EKS         | EFS              |
| Simple shared storage    | EFS              |
| HPC / Weather / Genomics | FSx Lustre       |
| Durable enterprise NAS   | FSx NetApp ONTAP |

---

## ⚠️ Common exam traps

❌ EFS ≠ HPC
❌ Bursting ≠ sustained throughput
❌ Scratch ≠ highly available
❌ gp2 ≠ independent IOPS


Yesss 😄 let’s do it.
Here’s a **10-question AWS Storage mini-mock**, **SAA style**, focused on **decision-making** (not trivia).

📌 **Rules**

* Choose **ONE best answer**
* Don’t overthink — AWS loves the *simplest service that fits*
* When you’re done, send me your answers like:
  `1A 2C 3B ...`

---

# 🟦 AWS STORAGE MINI-MOCK (10 QUESTIONS)

---

### **Q1**

A Linux-based application needs a **shared file system** that can be mounted by **hundreds of EC2 instances**. The workload has **spiky throughput** and the company wants to **minimize cost**.

Which solution should a solutions architect choose?

A. Amazon EBS gp3
B. Amazon FSx for Lustre persistent
C. Amazon EFS with Bursting Throughput
D. Amazon S3 with Transfer Acceleration

---

### **Q2**

A genomics research team runs **HPC workloads** that require **sub-millisecond latency** and **massive parallel throughput**. The data can be **re-created** if lost.

Which storage solution meets these requirements?

A. Amazon EFS with Provisioned Throughput
B. Amazon FSx for Lustre scratch
C. Amazon FSx for Windows File Server
D. Amazon EBS io2

---

### **Q3**

A financial application runs on Amazon RDS for MySQL and requires **15,000 IOPS**, provisioned **independently of storage size**, at the **lowest cost**.

Which storage configuration should be used?

A. EBS gp2
B. EBS io1
C. EBS gp3
D. EBS magnetic

---

### **Q4**

A company needs **shared storage for containers** running on Amazon EKS. The storage must be **highly available**, **POSIX-compliant**, and require **no server management**.

What should the company use?

A. Amazon EBS
B. Amazon FSx for Lustre
C. Amazon EFS
D. Amazon S3

---

### **Q5**

A Windows-based application requires a **shared file system** using the **SMB protocol** and integration with **Active Directory**.

Which solution should be used?

A. Amazon EFS
B. Amazon FSx for Windows File Server
C. Amazon FSx for Lustre
D. Amazon S3

---

### **Q6**

A company needs **block storage** for a single EC2 instance running a production database. The workload requires **very high IOPS and low latency**.

Which solution should be used?

A. Amazon EBS gp3
B. Amazon EBS io2
C. Amazon EFS Provisioned Throughput
D. Amazon FSx for Lustre

---

### **Q7**

A media company stores **petabytes of video files** that are rarely accessed but must be **durable** and **low cost**.

Which storage solution is MOST appropriate?

A. Amazon EFS
B. Amazon S3 Standard
C. Amazon S3 Glacier Flexible Retrieval
D. Amazon EBS gp3

---

### **Q8**

A company needs a **high-performance shared file system** with **advanced data management features** such as **snapshots and cloning**, but **not HPC workloads**.

Which solution should be used?

A. Amazon EFS
B. Amazon FSx for NetApp ONTAP
C. Amazon FSx for Lustre scratch
D. Amazon S3

---

### **Q9**

A workload requires **shared storage across multiple Availability Zones** with **automatic scaling** and **no capacity planning**.

Which solution meets these requirements?

A. Amazon EBS
B. Amazon FSx for Lustre
C. Amazon EFS
D. Amazon EC2 Instance Store

---

### **Q10**

A startup runs a web application that uploads user images. The images must be **highly durable**, **globally accessible**, and **cost-efficient**.

Which storage solution should be used?

A. Amazon EBS
B. Amazon EFS
C. Amazon S3
D. Amazon FSx for Windows

---

## 🧠 Tip before answering

If you feel torn between two options, ask:

> **Which service was AWS literally designed for this use case?**

---

Send me your answers when ready 😏
After that, I’ll:

* Grade it
* Explain **why wrong answers are wrong** (exam gold)
* Give you a **score → SAA readiness level** 💯
