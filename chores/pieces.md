✅ Correct answer:
[x] If you use production online transaction processing (OLTP) workloads.

Explanation:

You should choose Provisioned IOPS (Input/Output Operations Per Second) for Amazon RDS when your workloads require high, consistent, and low-latency I/O performance — typically in production OLTP systems such as financial, e-commerce, or ERP databases.

| Storage Type                   | Description                                                              | Best for                                                            |
| ------------------------------ | ------------------------------------------------------------------------ | ------------------------------------------------------------------- |
| **Provisioned IOPS (io1/io2)** | You specify the IOPS rate; offers consistent and predictable performance | **Production OLTP workloads**, mission-critical databases           |
| **General Purpose (gp2/gp3)**  | Balances price and performance; bursts allowed                           | Development, testing, or moderate workloads                         |
| **Magnetic (standard)**        | Legacy option; lowest cost but inconsistent performance                  | **Batch workloads** or archival data, **not performance-sensitive** |


So:

❌ Batch-oriented workloads → Use Standard or General Purpose SSD, not Provisioned IOPS.

✅ Production OLTP workloads → Use Provisioned IOPS.

❌ Workloads not sensitive to consistent performance → Don’t need Provisioned IOPS.


| Thuật ngữ                            | Dịch vụ         | Chức năng chính                             | Mục đích sử dụng                            |
| ------------------------------------ | --------------- | ------------------------------------------- | ------------------------------------------- |
| **RRS (Reduced Redundancy Storage)** | Amazon S3       | Lưu trữ giá rẻ, độ bền thấp                 | Cho dữ liệu có thể tái tạo (PDF, CSV)       |
| **EMR (Elastic MapReduce)**          | Amazon EMR      | Xử lý dữ liệu lớn (Big Data, Hadoop, Spark) | Sinh báo cáo, xử lý log hàng ngày           |
| **Reserved Instance (Redshift)**     | Amazon Redshift | Kho dữ liệu phân tích (data warehouse)      | Giảm chi phí cho workload chạy thường xuyên |


Spot Instance là loại EC2 Instance giá rẻ mà Amazon bán lại công suất dư thừa (unused capacity) trong hệ thống của họ.

Bạn có thể mua rẻ hơn tới 70–90% so với giá On-Demand.

Tuy nhiên, vì đây là tài nguyên “dư”, nên AWS có thể thu hồi (tắt instance) bất kỳ lúc nào nếu họ cần lại công suất đó cho người khác.


💡 Khi nào nên dùng Spot Instances

Spot Instances rất phù hợp cho các công việc:

Trường hợp	Giải thích
✅ Batch processing	Các job xử lý theo lô (như EMR job, video encoding, big data, CI/CD...) có thể tạm dừng và chạy lại được.
✅ Stateless workload	Ứng dụng không phụ thuộc vào trạng thái máy cụ thể, có thể phân phối lại công việc nếu một máy bị tắt.
✅ Big Data / EMR	Bạn có thể trộn Spot (cho task node) và On-Demand (cho master/core node) để tiết kiệm tiền mà vẫn ổn định.


Amazon Instance Store – temporary block storage physically attached to the host computer (data is lost when the instance stops).

Amazon Elastic Block Store (EBS) – persistent block storage that remains available even after stopping or terminating the instance.



| Option                         | Type             | POSIX      | Scalable   | Managed | Typical Use                             |
| ------------------------------ | ---------------- | ---------- | ---------- | ------- | --------------------------------------- |
| **Amazon EFS**                 | NFS              | ✅          | ✅          | ✅       | General Linux apps, web, shared storage |
| **Amazon FSx for Lustre**      | HPC File System  | ✅          | ✅          | ✅       | HPC, ML, big data                       |
| **Amazon FSx for Windows FS**  | SMB              | ❌          | ✅          | ✅       | Windows workloads                       |
| **S3 File Gateway**            | Object (via NFS) | ⚠️ Partial | ✅          | ✅       | Archival, backup, low-write workloads   |
| **Self-managed NFS/GlusterFS** | Custom           | ✅          | ✅ (manual) | ❌       | Custom control or hybrid setups         |



⭐ A. Configure an S3 Gateway Endpoint — CORRECT

An S3 Gateway VPC Endpoint lets your EC2 instances access S3 privately, through the AWS network, without using the internet, without NAT, and without a public IP.




An egress-only internet gateway (EIGW) is an AWS gateway used only for IPv6 traffic that allows outbound connections from your VPC but blocks all inbound connections from the internet.

🔥 NAT Instance vs NAT Gateway
✅ NAT Gateway — Modern, recommended (managed service)
❌ NAT Instance — Legacy, not recommended (self-managed)





DataSYNC SF


        On-Premises Data Center
        ┌──────────────────────────┐
        │                          │
        │   SFTP Server (NFS)      │
        │     200 GB of data       │
        │                          │
        │   +-------------------+   │
        │   | DataSync Agent    |   │
        │   +---------+---------+   │
        └─────────────|─────────────┘
                      |
                      | Encrypted Transfer
                      | over the Internet / VPN / DX
                      v
        ┌──────────────────────────┐
        │          AWS             │
        │                          │
        │  +--------------------+  │
        │  | AWS DataSync       |  │
        │  |  (managed service) |  │
        │  +---------+----------+  │
        │            |             │
        │            | writes data │
        │            v             │
        │   +-------------------+  │
        │   | Amazon EFS        |  │
        │   +---------+---------+  │
        │             | mount       │
        │             v             │
        │   +-------------------+   │
        │   | EC2 SFTP Server   |   │
        │   | (mounts EFS)      |   │
        │   +-------------------+   │
        └──────────────────────────┘
