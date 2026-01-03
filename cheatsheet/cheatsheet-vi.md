# Hướng dẫn tham khảo AWS Certified Solutions Architect Associate (SAA-C03/SAA-C04) [2025]

![Hướng dẫn tham khảo AWS Certified Solutions Architect Associate (SAA-C03/SAA-C04)](/extras/AWS_Certified_Solutions_Architect_Associate_SAA_C03_Cheatsheet_logo.png)

Kho lưu trữ này chứa hướng dẫn tham khảo với thông tin chính để giúp bạn chuẩn bị cho kỳ thi AWS Certified Solutions Architect Associate (SAA-C03/SAA-C04), **được cập nhật cho năm 2025**.

![Bản đồ dịch vụ AWS](/extras/aws_services_map.jpg)

Hướng dẫn tham khảo này tóm tắt các dịch vụ, khái niệm và phương pháp tốt nhất quan trọng được kiểm tra trong kỳ thi. Nó có thể được sử dụng như một hướng dẫn tham khảo nhanh để học tập.

Thông tin được tổ chức thành các phần sau:

## Mục lục

- [Hướng dẫn tham khảo AWS Certified Solutions Architect Associate (SAA-C03/SAA-C04) \[2025\]](#hướng-dẫn-tham-khảo-aws-certified-solutions-architect-associate-saa-c03saa-c04-2025)
  - [Mục lục](#mục-lục)
  - [Amazon Elastic Compute Cloud (EC2)](#amazon-elastic-compute-cloud-ec2)
  - [Amazon Elastic Container Service (ECS)](#amazon-elastic-container-service-ecs)
  - [Amazon Elastic Container Registry (ECR)](#amazon-elastic-container-registry-ecr)
  - [Amazon Elastic Kubernetes Service (EKS)](#amazon-elastic-kubernetes-service-eks)
  - [AWS Lambda](#aws-lambda)
  - [Amazon Virtual Private Cloud (VPC)](#amazon-virtual-private-cloud-vpc)
  - [Amazon Route 53](#amazon-route-53)
  - [Amazon Elastic Load Balancing (ELB)](#amazon-elastic-load-balancing-elb)
  - [AWS Transfer for SFTP](#aws-transfer-for-sftp)
  - [AWS Direct Connect](#aws-direct-connect)
  - [Amazon Simple Storage Service (S3)](#amazon-simple-storage-service-s3)
  - [Amazon Elastic Block Store (EBS)](#amazon-elastic-block-store-ebs)
  - [Amazon Elastic File System (EFS)](#amazon-elastic-file-system-efs)
  - [Amazon Relational Database Service (RDS)](#amazon-relational-database-service-rds)
  - [Amazon Aurora](#amazon-aurora)
  - [Amazon DynamoDB](#amazon-dynamodb)
  - [Amazon Redshift](#amazon-redshift)
  - [Amazon Simple Queue Service (SQS)](#amazon-simple-queue-service-sqs)
  - [Amazon Simple Notification Service (SNS)](#amazon-simple-notification-service-sns)
  - [Amazon API Gateway](#amazon-api-gateway)
  - [Amazon Cognito](#amazon-cognito)
  - [Amazon CloudWatch](#amazon-cloudwatch)
  - [AWS CloudTrail](#aws-cloudtrail)
  - [AWS Identity and Access Management (IAM)](#aws-identity-and-access-management-iam)
  - [AWS Key Management Service (KMS)](#aws-key-management-service-kms)
  - [AWS Security Hub](#aws-security-hub)
  - [AWS CloudFormation](#aws-cloudformation)
  - [AWS Systems Manager](#aws-systems-manager)
  - [AWS Well-Architected Framework](#aws-well-architected-framework)
  - [AWS Core Services](#aws-core-services)
  - [AWS Networking and Security Services](#aws-networking-and-security-services)
  - [AWS Deployment and Management Services](#aws-deployment-and-management-services)
  - [AWS Cost Optimization Strategies](#aws-cost-optimization-strategies)
  - [Amazon EventBridge](#amazon-eventbridge)
  - [AWS Step Functions](#aws-step-functions)
  - [Amazon Kinesis](#amazon-kinesis)
  - [Amazon GuardDuty](#amazon-guardduty)
  - [Amazon Inspector](#amazon-inspector)
  - [Amazon Macie](#amazon-macie)
  - [AWS IAM Access Analyzer](#aws-iam-access-analyzer)
  - [AWS CodePipeline](#aws-codepipeline)
  - [AWS CodeBuild](#aws-codebuild)
  - [AWS CodeDeploy](#aws-codedeploy)
  - [AWS CodeCommit](#aws-codecommit)
  - [Đóng góp](#đóng-góp)
  - [Giấy phép](#giấy-phép)

## Amazon Elastic Compute Cloud (EC2)

Amazon EC2 cung cấp khả năng tính toán an toàn, có thể thay đổi quy mô trong đám mây. Các khái niệm kỳ thi chính:

- **Loại phiên bản**:
  - General Purpose (M7g, T4g, M7i, T3, M7a, M7gd)
  - Compute Optimized (C7g, C7i, C7a, C7gd)
  - Memory Optimized (R7iz, X2idn, X2iedn, R7a, R7g, U7i family, I7i, I7ie)
  - Accelerated Computing (P4d, G5, VT1, P5en, Trn2)
  - Storage Optimized (Im4gn, Is4gen, I4i)

- **Mô hình định giá**:
  - On-Demand (cần thiết ngắn hạn)
  - Savings Plans (cam kết 1-3 năm, hạn chế sử dụng cho một khách hàng cuối cùng từ ngày 1 tháng 6, 2025)
  - Spot Instances (giảm giá lên đến 90%)
  - Reserved Instances (đặt trước dung lượng, hạn chế sử dụng cho một khách hàng cuối cùng từ ngày 1 tháng 6, 2025)
  - Dedicated Hosts (máy chủ vật lý dành cho bạn sử dụng)
  - Dedicated Instances (phiên bản EC2 trên phần cứng đơn lẻ)
  - Capacity Reservations (đặt trước dung lượng EC2 cho bất kỳ thời lượng nào)

- **Tính năng nâng cao**:
  - Nitro System (bảo mật và hiệu suất nâng cao)
  - Elastic Fabric Adapter (EFA) cho HPC và ML networking
  - Capacity Blocks for ML (dung lượng GPU đặt trước cho thời lượng cụ thể, tận dụng các phiên bản AI/ML mới như P5en, Trn2)
  - EC2 Instance Connect để SSH dựa trên trình duyệt
  - EC2 Fleet và Spot Fleet (kết hợp On-Demand, Reserved và Spot Instances)

- **Phương pháp tốt nhất**:
  - Sử dụng Instance Metadata Service (IMDSv2) để bảo mật nâng cao
  - Bật Detailed Monitoring cho <1 phút metrics (CloudWatch)
  - Tận dụng Placement Groups (Cluster, Spread, Partition) cho nhu cầu khối lượng công việc cụ thể
  - Triển khai EC2 Auto Scaling để linh hoạt và độ sẵn sàng cao
  - Triển khai AWS Systems Manager để tự động hóa vận hành
  - Liên tục giám sát và tối ưu hóa chi phí bằng AWS Cost Explorer và Compute Optimizer

EC2 là dịch vụ cốt lõi trong AWS, và nó được hàng triệu khách hàng trên toàn thế giới sử dụng. Nó là một công cụ mạnh mẽ và linh hoạt có thể được sử dụng để xây dựng và chạy nhiều loại ứng dụng khác nhau.

## Amazon Elastic Container Service (ECS)

Amazon ECS là dịch vụ điều phối container có thể mở rộng cao, hiệu suất cao hỗ trợ container Docker. ECS cho phép bạn dễ dàng triển khai, quản lý và mở rộng các ứng dụng được chứa trong container. ECS cung cấp nhiều tính năng để giúp bạn quản lý các ứng dụng được chứa trong container, bao gồm:

- **Khám phá dịch vụ:** ECS tự động khám phá và đăng ký các container của bạn, để bạn có thể dễ dàng truy cập chúng từ ứng dụng của mình.
- **Cân bằng tải:** ECS tự động phân phối lưu lượng truy cập trên các container của bạn, để đảm bảo ứng dụng của bạn có độ sẵn sàng cao.  
- **Giám sát sức khỏe:** ECS giám sát sức khỏe của các container và tự động khởi động lại bất kỳ container không khỏe nào.
- **Tự động mở rộng:** ECS có thể tự động mở rộng các container của bạn lên hoặc xuống dựa trên nhu cầu, để đảm bảo ứng dụng của bạn có tài nguyên cần thiết.

Dưới đây là một số thông tin ngắn về Amazon ECS mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- ECS là dịch vụ điều phối container có thể mở rộng cao, hiệu suất cao.  
- ECS hỗ trợ container Docker và hình ảnh OCI tương thích.
- ECS cung cấp nhiều loại khởi chạy, bao gồm EC2 và serverless AWS Fargate.
- ECS cung cấp nhiều tính năng để giúp bạn quản lý các ứng dụng được chứa trong container, bao gồm khám phá dịch vụ, cân bằng tải, giám sát sức khỏe, tự động mở rộng và tích hợp sâu với lưu trữ liên tục.
- ECS Anywhere mở rộng ECS để chạy container trên cơ sở hạ tầng của riêng bạn (on-premises, đám mây khác).

Dưới đây là một số chi tiết bổ sung về Amazon ECS mà bạn có thể muốn biết:

- ECS có thể được sử dụng để triển khai và quản lý các ứng dụng được chứa trong container ở bất kỳ Khu vực AWS nào.
- ECS có thể được sử dụng để triển khai và quản lý các ứng dụng được chứa trong container có bất kỳ kích thước nào, từ một trang web nhỏ đến một ứng dụng doanh nghiệp lớn.  
- ECS có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon S3, Amazon Route 53, Amazon EBS và Amazon EFS.
- Hỗ trợ Windows Containers cho các khối lượng công việc cụ thể.
- AWS Copilot CLI đơn giản hóa việc triển khai và quản lý các ứng dụng được chứa trong container trên ECS.
- Nhấn mạnh bảo mật và cô lập theo thiết kế cho các khối lượng công việc được chứa trong container.

ECS là một công cụ mạnh mẽ để quản lý các ứng dụng được chứa trong container. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn triển khai, quản lý và mở rộng các ứng dụng được chứa trong container một cách an toàn và hiệu quả.

## Amazon Elastic Container Registry (ECR)

Amazon ECR là registry container được quản lý hoàn toàn giúp dễ dàng lưu trữ, quản lý và triển khai hình ảnh container Docker và các artifact tương thích Open Container Initiative (OCI). ECR được tích hợp với Amazon Elastic Container Service (ECS) và Amazon Kubernetes Service (EKS), để bạn có thể dễ dàng triển khai các ứng dụng được chứa trong container của mình vào sản xuất.

Dưới đây là một số thông tin ngắn về Amazon ECR mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- ECR là registry container được quản lý hoàn toàn.
- ECR được tích hợp với ECS và EKS.  
- ECR lưu trữ hình ảnh container Docker và artifact OCI tương thích.
- ECR cung cấp nhiều tính năng để giúp bạn quản lý hình ảnh container của mình, bao gồm:
- Gắn thẻ và phiên bản hình ảnh
- Sao chép hình ảnh
- Quét hình ảnh
- Quản lý vòng đời hình ảnh

Dưới đây là một số chi tiết bổ sung về Amazon ECR mà bạn có thể muốn biết:

- ECR có thể được sử dụng để lưu trữ hình ảnh container có bất kỳ kích thước nào.  
- ECR hình ảnh có thể được triển khai đến cụm ECS hoặc EKS ở bất kỳ Khu vực AWS nào.
- ECR hình ảnh có thể được truy cập bằng AWS Management Console, AWS CLI hoặc AWS SDKs.
- ECR hỗ trợ IPv6 để nâng cao khả năng mạng.
- ECR cung cấp Pull Through Cache rules để tự động lưu trữ hình ảnh từ registry công khai upstream.

ECR là một công cụ mạnh mẽ để quản lý hình ảnh container. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn quản lý hình ảnh của mình một cách an toàn và hiệu quả.

## Amazon Elastic Kubernetes Service (EKS)

Amazon EKS là dịch vụ Kubernetes được quản lý hoàn toàn giúp dễ dàng triển khai, quản lý và mở rộng các ứng dụng Kubernetes trên AWS. EKS cung cấp các nút worker Kubernetes, trong khi control plane được quản lý bởi AWS. EKS cũng cung cấp nhiều tính năng để giúp bạn quản lý các ứng dụng Kubernetes của mình, bao gồm:

- **Điều phối Kubernetes:** EKS tự động cung cấp và quản lý cụm Kubernetes, để bạn có thể tập trung vào việc xây dựng và chạy ứng dụng của mình.
- **Bảo mật:** EKS cung cấp nhiều tính năng bảo mật để giúp bảo vệ các ứng dụng Kubernetes của bạn, bao gồm mã hóa, xác thực và ủy quyền.  
- **Cân bằng tải:** EKS cung cấp cân bằng tải cho các ứng dụng Kubernetes của bạn, để đảm bảo các ứng dụng của bạn có độ sẵn sàng cao.
- **Giám sát:** EKS cung cấp giám sát cho các ứng dụng Kubernetes của bạn, để bạn có thể theo dõi sức khỏe và hiệu suất của các ứng dụng của mình.

Dưới đây là một số thông tin ngắn về Amazon EKS mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- EKS là dịch vụ Kubernetes được quản lý hoàn toàn.
- EKS cung cấp máy chủ API Kubernetes, control plane Kubernetes và nút worker Kubernetes. Kể từ ngày 29 tháng 5, 2025, Amazon EKS hỗ trợ phiên bản Kubernetes 1.33.
- EKS cung cấp nhiều tính năng để giúp bạn quản lý các ứng dụng Kubernetes của mình, bao gồm điều phối Kubernetes, bảo mật nâng cao, tùy chọn cân bằng tải linh hoạt (ALB, NLB, CLB) và giám sát toàn diện (CloudWatch Container Insights).

Dưới đây là một số chi tiết bổ sung về Amazon EKS mà bạn có thể muốn biết:

- EKS có thể được sử dụng để triển khai và quản lý các ứng dụng Kubernetes ở bất kỳ Khu vực AWS nào.
- EKS có thể được sử dụng để triển khai và quản lý các ứng dụng Kubernetes có bất kỳ kích thước nào, từ một trang web nhỏ đến một ứng dụng doanh nghiệp lớn.
- EKS có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon S3 và Amazon Route 53.
- EKS Dashboard cung cấp khả năng hiển thị và quản lý tập trung của các cụm Kubernetes.
- EKS Pod Identity đơn giản hóa thông tin xác thực IAM cho pods.
- Hỗ trợ mở rộng cho Edge và Hybrid use cases (ví dụ: EKS Anywhere).

EKS là một công cụ mạnh mẽ để quản lý các ứng dụng Kubernetes. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn triển khai, quản lý và mở rộng các ứng dụng Kubernetes một cách an toàn và hiệu quả.

## AWS Lambda

AWS Lambda là dịch vụ tính toán serverless cho phép bạn chạy mã mà không cần cung cấp hoặc quản lý máy chủ. Lambda thực thi mã của bạn chỉ khi cần thiết và tự động mở rộng quy mô, để bạn có thể tập trung vào mã của mình chứ không phải quản lý cơ sở hạ tầng. Lambda hỗ trợ nhiều ngôn ngữ lập trình và runtime (ví dụ: Node.js 22, Python 3.13, Java 21, .NET 9, Ruby 3.4 và runtime tùy chỉnh cho Go).

Dưới đây là một số thông tin ngắn về AWS Lambda mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Lambda là dịch vụ tính toán serverless.
- Lambda thực thi mã của bạn chỉ khi cần thiết và tự động mở rộng quy mô.  
- Lambda hỗ trợ nhiều ngôn ngữ lập trình và runtime, với cập nhật liên tục và chu kỳ ngừng sử dụng.

Dưới đây là một số chi tiết bổ sung về AWS Lambda mà bạn có thể muốn biết:

- Các hàm Lambda có thể được kích hoạt bởi nhiều loại sự kiện khác nhau, chẳng hạn như yêu cầu HTTP, thay đổi đối tượng S3 và thông điệp từ luồng Kinesis.
- Các hàm Lambda có thể được sử dụng để xây dựng nhiều loại ứng dụng khác nhau, bao gồm ứng dụng web, backend di động và pipeline xử lý dữ liệu.
- Các hàm Lambda có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như API Gateway, S3 và DynamoDB.
- Hỗ trợ kiến trúc `arm64` (AWS Graviton) để cải thiện hiệu suất và hiệu quả chi phí.
- Sử dụng Amazon Linux 2023 cho các runtime mới hơn.
- Cho phép triển khai các hàm Lambda dưới dạng hình ảnh container để có nhiều phụ thuộc và công cụ quen thuộc hơn.

Lambda là một công cụ mạnh mẽ để xây dựng các ứng dụng serverless. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn phát triển, triển khai và quản lý các ứng dụng serverless hiệu quả.

## Amazon Virtual Private Cloud (VPC)

Amazon Virtual Private Cloud (VPC) cho phép bạn khởi chạy tài nguyên AWS vào một mạng ảo riêng biệt mà bạn định nghĩa. Mạng ảo này tương tự như mạng truyền thống mà bạn có thể vận hành trong trung tâm dữ liệu của riêng mình, với lợi ích của việc sử dụng cơ sở hạ tầng có thể mở rộng của AWS.

Dưới đây là một số thông tin ngắn về Amazon VPC mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- VPC là mạng ảo riêng biệt mà bạn định nghĩa.
- VPC cung cấp cho bạn quyền kiểm soát hoàn toàn đối với môi trường mạng ảo của mình, bao gồm lựa chọn phạm vi IP của riêng bạn, tạo subnet và cấu hình bảng định tuyến, gateway mạng (Internet Gateway, Virtual Private Gateway), và VPC Endpoints.
- Bạn có thể sử dụng cả IPv4 và IPv6 cho hầu hết tài nguyên trong VPC của mình, hỗ trợ cấu hình dual-stack.

Dưới đây là một số chi tiết bổ sung về Amazon VPC mà bạn có thể muốn biết:

- VPC có thể được chia thành subnet, là các mạng nhỏ hơn, riêng biệt trong VPC của bạn.
- Bạn có thể cấu hình bảng định tuyến để kiểm soát cách lưu lượng truy cập chảy giữa subnet và giữa VPC của bạn với internet hoặc VPC khác.
- Bạn có thể sử dụng gateway mạng để kết nối VPC của bạn với internet hoặc VPC khác.
- Bạn có thể sử dụng nhóm bảo mật để kiểm soát lưu lượng truy cập vào và ra khỏi tài nguyên VPC của bạn ở cấp độ phiên bản, và Network Access Control Lists (NACLs) ở cấp độ subnet.
- VPC Flow Logs ghi lại thông tin về lưu lượng IP đi vào và ra khỏi giao diện mạng trong VPC của bạn, cho phép giám sát và khắc phục sự cố.

VPC là một công cụ mạnh mẽ để xây dựng và quản lý mạng an toàn và riêng biệt trong đám mây. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn đáp ứng nhu cầu mạng của mình.

## Amazon Route 53  

Amazon Route 53 là dịch vụ DNS đám mây có thể mở rộng cao và sẵn sàng. Nó cung cấp cách đáng tin cậy và an toàn để định tuyến người dùng cuối đến ứng dụng internet bằng cách dịch tên miền, chẳng hạn như example.com, thành địa chỉ IP số của cơ sở hạ tầng cơ bản nơi ứng dụng được lưu trữ.

Dưới đây là một số thông tin ngắn về Amazon Route 53 mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Route 53 là dịch vụ DNS đám mây có thể mở rộng cao và sẵn sàng.
- Route 53 cung cấp cách đáng tin cậy và an toàn để định tuyến người dùng cuối đến ứng dụng internet.
- Route 53 hỗ trợ nhiều loại bản ghi DNS, bao gồm A, AAAA, CNAME, MX, NS, SOA, TXT, SRV và CAA.
- Route 53 cung cấp nhiều tính năng để giúp bạn quản lý bản ghi DNS của mình, bao gồm:
- Kiểm tra sức khỏe DNS
- Định tuyến luồng lưu lượng (bao gồm Geolocation, Latency, Weighted, Failover và Multi-value answer routing)
- Định tuyến geolocation
- Bản ghi alias
- Route 53 Resolver (để phân giải DNS trong VPC của bạn)
- Hỗ trợ DNSSEC để bảo mật nâng cao

Dưới đây là một số chi tiết bổ sung về Amazon Route 53 mà bạn có thể muốn biết:

- Route 53 có thể được sử dụng để định tuyến lưu lượng truy cập đến bất kỳ loại ứng dụng internet nào, bao gồm trang web, ứng dụng web, ứng dụng di động và API.
- Route 53 có thể được sử dụng để định tuyến lưu lượng truy cập đến ứng dụng được lưu trữ trên AWS, on-premises hoặc với nhà cung cấp đám mây khác.
- Route 53 có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon S3 và Amazon CloudFront.

Route 53 là một công cụ mạnh mẽ để quản lý bản ghi DNS và định tuyến lưu lượng truy cập đến ứng dụng internet. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn đáp ứng nhu cầu DNS và định tuyến của mình.

## Amazon Elastic Load Balancing (ELB)

Elastic Load Balancing (ELB) là dịch vụ cân bằng tải tự động phân phối lưu lượng truy cập đến đến nhiều mục tiêu, chẳng hạn như phiên bản EC2, container và địa chỉ IP, trong một hoặc nhiều Availability Zone. Nó giám sát sức khỏe của các mục tiêu đã đăng ký của mình và đảm bảo rằng lưu lượng truy cập chỉ được định tuyến đến các mục tiêu khỏe mạnh. ELB tự động mở rộng dung lượng load balancer của bạn để đáp ứng các thay đổi trong lưu lượng truy cập đến.

Dưới đây là một số thông tin ngắn về Amazon ELB mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- ELB là dịch vụ cân bằng tải phân phối lưu lượng truy cập đến đến nhiều mục tiêu.
- ELB giám sát sức khỏe của các mục tiêu đã đăng ký của mình và định tuyến lưu lượng truy cập chỉ đến các mục tiêu khỏe mạnh.
- ELB tự động mở rộng dung lượng load balancer của bạn để đáp ứng các thay đổi trong lưu lượng truy cập đến.
- ELB hỗ trợ bốn loại load balancer khác nhau:
- Application Load Balancer: Định tuyến lưu lượng truy cập đến ứng dụng web (Lớp 7).
- Network Load Balancer: Định tuyến lưu lượng truy cập đến ứng dụng TCP và UDP (Lớp 4).
- Gateway Load Balancer: Cho phép bạn triển khai, mở rộng quy mô và quản lý thiết bị ảo của bên thứ ba.
- Classic Load Balancer: Load balancer kế thừa vẫn được hỗ trợ, nhưng không được khuyến nghị cho các ứng dụng mới.

Dưới đây là một số chi tiết bổ sung về Amazon ELB mà bạn có thể muốn biết:

- ELB có thể được sử dụng để cân bằng tải lưu lượng truy cập đến ứng dụng được lưu trữ trên AWS, on-premises hoặc với nhà cung cấp đám mây khác.
- ELB có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon S3 và Amazon CloudFront.
- ELB cung cấp nhiều tính năng để giúp bạn quản lý load balancer của mình, bao gồm:
- Kiểm tra sức khỏe: Giám sát sức khỏe của các mục tiêu đã đăng ký của bạn và định tuyến lưu lượng truy cập chỉ đến các mục tiêu khỏe mạnh.
- Quy tắc listener: Định tuyến lưu lượng truy cập đến các mục tiêu khác nhau dựa trên yêu cầu.
- Nhóm mục tiêu: Nhóm các mục tiêu mà bạn có thể đăng ký với load balancer của mình.
- Nhóm bảo mật: Kiểm soát lưu lượng truy cập vào và ra khỏi load balancer của bạn.

Elastic Load Balancing là một công cụ mạnh mẽ để phân phối lưu lượng truy cập đến đến nhiều mục tiêu và đảm bảo rằng các ứng dụng của bạn có độ sẵn sàng cao và có thể mở rộng quy mô. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn đáp ứng nhu cầu cân bằng tải của mình.

## AWS Transfer for SFTP

AWS Transfer for SFTP là dịch vụ được quản lý giúp dễ dàng chuyển tệp qua Secure File Transfer Protocol (SFTP). Nó cung cấp cách an toàn và đáng tin cậy để chuyển tệp giữa hệ thống on-premises của bạn và dịch vụ lưu trữ AWS, chẳng hạn như Amazon S3 và Amazon Elastic File System (EFS).

Dưới đây là một số thông tin ngắn về AWS Transfer for SFTP mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- AWS Transfer for SFTP là dịch vụ được quản lý giúp dễ dàng chuyển tệp qua SFTP, FTPS và FTP.
- AWS Transfer for SFTP cung cấp cách an toàn và đáng tin cậy để chuyển tệp giữa hệ thống on-premises của bạn và dịch vụ lưu trữ AWS.
- AWS Transfer for SFTP hỗ trợ nhiều client SFTP khác nhau, bao gồm WinSCP, Cyberduck và FileZilla.
- AWS Transfer for SFTP cung cấp nhiều tính năng để giúp bạn quản lý việc chuyển tệp của mình, bao gồm:
- Quản lý người dùng và nhóm (bao gồm tích hợp với AWS IAM và Active Directory)
- Kiểm soát truy cập (sử dụng vai trò IAM và chính sách)
- Ghi nhật ký hoạt động (qua CloudTrail)
- Thông báo chuyển tệp (sử dụng Amazon SNS)
- Hỗ trợ nhiều phương thức xác thực khác nhau, bao gồm mật khẩu, khóa SSH và tích hợp dịch vụ thư mục.

Dưới đây là một số chi tiết bổ sung về AWS Transfer for SFTP mà bạn có thể muốn biết:

- AWS Transfer for SFTP có thể được sử dụng để chuyển tệp có bất kỳ kích thước nào, từ tệp văn bản nhỏ đến tệp video lớn.
- AWS Transfer for SFTP có thể được sử dụng để chuyển tệp giữa hệ thống on-premises của bạn và dịch vụ lưu trữ AWS ở bất kỳ Khu vực AWS nào.  
- AWS Transfer for SFTP có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon CloudTrail và Amazon CloudWatch.

AWS Transfer for SFTP là một công cụ mạnh mẽ để chuyển tệp qua SFTP một cách an toàn và đáng tin cậy. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn quản lý việc chuyển tệp của mình hiệu quả.

## AWS Direct Connect

AWS Direct Connect là kết nối mạng chuyên dụng giữa mạng on-premises của bạn và một trong các vị trí AWS Direct Connect. Nó cung cấp kết nối an toàn, đáng tin cậy và hiệu suất cao đến AWS. AWS Direct Connect có thể được sử dụng để kết nối với bất kỳ dịch vụ AWS nào, bao gồm Amazon EC2, Amazon S3 và Amazon RDS.

Dưới đây là một số thông tin ngắn về AWS Direct Connect mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- AWS Direct Connect là kết nối mạng chuyên dụng giữa mạng on-premises của bạn và AWS.
- AWS Direct Connect cung cấp kết nối an toàn, đáng tin cậy và hiệu suất cao đến AWS.
- AWS Direct Connect có thể được sử dụng để kết nối với bất kỳ dịch vụ AWS nào.
- AWS Direct Connect cung cấp hai loại kết nối chính:
- Dedicated Connections: Kết nối vật lý chuyên dụng giữa mạng on-premises của bạn và AWS, cung cấp nhiều tùy chọn băng thông.
- Hosted Connections: Kết nối được cung cấp bởi đối tác AWS Direct Connect, với tùy chọn băng thông được định sẵn.

Dưới đây là một số chi tiết bổ sung về AWS Direct Connect mà bạn có thể muốn biết:

- AWS Direct Connect là dịch vụ toàn cầu với vị trí ở hơn 90 thành phố trên toàn thế giới.  
- AWS Direct Connect cung cấp nhiều tùy chọn băng thông, từ 1 Gbps đến 100 Gbps.
- AWS Direct Connect có thể được sử dụng để tạo nhiều cấu hình mạng khác nhau, bao gồm VPN site-to-site, kết nối point-to-point, mạng hub-and-spoke và tích hợp với AWS Transit Gateway để quản lý mạng đơn giản hóa.
- AWS Direct Connect có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như AWS Virtual Private Cloud (VPC) và AWS Transit Gateway.

AWS Direct Connect là một công cụ mạnh mẽ để kết nối mạng on-premises của bạn với AWS một cách an toàn, đáng tin cậy và với hiệu suất cao. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn đáp ứng nhu cầu mạng của mình.

## Amazon Simple Storage Service (S3)

Amazon S3 là dịch vụ lưu trữ đối tượng có thể mở rộng cao, bền bỉ và sẵn sàng được thiết kế để lưu trữ và truy xuất bất kỳ lượng dữ liệu nào, từ bất kỳ đâu trên web. S3 cung cấp cơ sở hạ tầng lưu trữ an toàn, bền bỉ và chi phí thấp để lưu trữ trang web tĩnh của bạn, lưu trữ dữ liệu được sử dụng bởi dịch vụ web, ứng dụng di động, sao lưu và khôi phục, lưu trữ, ứng dụng phân tích dữ liệu lớn và khối lượng công việc học máy.

Dưới đây là một số thông tin ngắn về Amazon S3 mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- S3 là dịch vụ lưu trữ đối tượng có thể mở rộng cao, bền bỉ và sẵn sàng.  
- S3 có thể được sử dụng để lưu trữ bất kỳ loại dữ liệu nào, bao gồm trang web, hình ảnh, video và cơ sở dữ liệu.
- S3 an toàn, bền bỉ và chi phí thấp.
- S3 dễ sử dụng và cung cấp nhiều tính năng để giúp bạn quản lý dữ liệu của mình, bao gồm:
- Phiên bản đối tượng
- Kiểm soát truy cập (IAM, Bucket Policies, Access Points, Access Grants)
- Chính sách bucket
- Mã hóa phía máy chủ (SSE-S3, SSE-KMS, SSE-C)
- Lưu trữ trang web tĩnh
- S3 Storage Lens (cho khả năng hiển thị toàn tổ chức)
- S3 Object Lambda (xử lý dữ liệu khi truy xuất)

Dưới đây là một số chi tiết bổ sung về Amazon S3 mà bạn có thể muốn biết:

- S3 lưu trữ dữ liệu trong bucket, là container logic cho dữ liệu của bạn.
- Đối tượng S3 được xác định duy nhất bởi khóa (tên) và ID phiên bản (nếu bật phiên bản).  
- Đối tượng S3 có thể lên đến 5 TB kích thước.
- S3 cung cấp nhiều lớp lưu trữ để đáp ứng nhu cầu của bạn, bao gồm S3 Standard, S3 Intelligent-Tiering, S3 Standard-IA, S3 One Zone-IA, S3 Glacier Instant Retrieval, S3 Glacier Flexible Retrieval, S3 Glacier Deep Archive và S3 Express One Zone.
- S3 có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon CloudFront, Amazon Lambda, AWS Storage Gateway và AWS Lake Formation.
- S3 Access Grants để quản lý truy cập dữ liệu đơn giản hóa.
- S3 Express One Zone cho truy cập hiệu suất cao.

Amazon S3 là một công cụ mạnh mẽ để lưu trữ và truy xuất bất kỳ lượng dữ liệu nào. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn quản lý dữ liệu của mình một cách an toàn, đáng tin cậy và hiệu quả.

## Amazon Elastic Block Store (EBS)

Elastic Block Store (EBS) là dịch vụ lưu trữ khối được thiết kế để sử dụng với phiên bản Amazon Elastic Compute Cloud (EC2). Các volume EBS cung cấp lưu trữ liên tục cho ứng dụng chạy trên phiên bản EC2. Các volume EBS được nhân bản trong Availability Zone mà chúng được tạo để bảo vệ khỏi mất dữ liệu.  

Các volume EBS có sẵn ở năm loại volume:

- **General Purpose SSD (gp3):** Khuyến nghị cho hầu hết khối lượng công việc. Cơ sở 3.000 IOPS và 125 MB/s thông lượng, có thể mở rộng quy mô lên 16.000 IOPS và 1.000 MB/s.
- **Provisioned IOPS SSD (io2 Block Express):** SSD hiệu suất cao nhất cho ứng dụng quan trọng. Hỗ trợ lên đến 256.000 IOPS và 4.000 MB/s thông lượng cho mỗi volume. Hỗ trợ Multi-Attach.
- **Throughput Optimized HDD (st1):** Chi phí hiệu quả cho khối lượng công việc được truy cập thường xuyên, đòi hỏi thông lượng cao như dữ liệu lớn.
- **Cold HDD (sc1):** Chi phí thấp nhất cho khối lượng công việc được truy cập ít thường xuyên hơn.
- **io1 (Legacy):** Thế hệ trước của Provisioned IOPS SSD.
- **gp2 (Legacy):** Thế hệ trước của General Purpose SSD.
- **EBS Snapshots Archive:** Lưu trữ chi phí hiệu quả lâu dài cho snapshot EBS.

Các volume EBS có thể được gắn vào phiên bản EC2 bất kỳ lúc nào, và chúng có thể được thay đổi kích thước lên hoặc xuống mà không có thời gian ngừng hoạt động. Các volume EBS cũng có thể được sử dụng để tạo snapshot, là bản sao point-in-time của volume EBS. Snapshot có thể được sử dụng để tạo volume EBS mới hoặc khôi phục volume EBS về trạng thái trước đó.

EBS là một phần quan trọng của AWS Well-Architected Framework. Well-Architected Framework là một tập hợp các phương pháp tốt nhất để thiết kế và vận hành kiến trúc đám mây đáng tin cậy, an toàn, hiệu quả và tiết kiệm chi phí. Well-Architected Framework khuyến nghị sử dụng EBS cho lưu trữ liên tục cho tất cả ứng dụng chạy trên EC2.

Dưới đây là một số thông tin bổ sung về EBS mà bạn sẽ cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Các volume EBS được gắn vào phiên bản EC2 bằng cách sử dụng ánh xạ thiết bị khối.
- Các volume EBS có thể được mã hóa tại nghỉ ngơi bằng AWS Key Management Service (KMS).  
- Các volume EBS có thể được mã hóa khi truyền bằng Transport Layer Security (TLS).
- Các volume EBS có thể được sử dụng để tạo mảng RAID.
- Các volume EBS có thể được sử dụng để tạo volume boot cho phiên bản EC2.
- Các volume EBS có thể được sử dụng để tạo volume root cho phiên bản EC2.
- Các volume EBS có thể được sử dụng để tạo volume dữ liệu cho phiên bản EC2.

## Amazon Elastic File System (EFS)

Amazon Elastic File System (EFS) là hệ thống tệp đám mây, linh hoạt cung cấp cách đơn giản, có thể mở rộng và bền bỉ để chia sẻ tệp trên nhiều phiên bản Amazon Elastic Compute Cloud (EC2) và máy chủ on-premises. EFS là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô lưu trữ của mình.

Hệ thống tệp EFS có độ sẵn sàng cao và bền bỉ, và chúng có thể mở rộng quy mô đến petabyte dữ liệu. EFS cũng cung cấp tính nhất quán mạnh và khóa tệp, làm cho nó trở thành lựa chọn tốt cho nhiều loại khối lượng công việc, bao gồm ứng dụng web, hệ thống quản lý nội dung và cơ sở dữ liệu.

Dưới đây là một số thông tin ngắn về EFS mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- EFS là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô lưu trữ của mình.
- Hệ thống tệp EFS có độ sẵn sàng cao và bền bỉ, và chúng có thể mở rộng quy mô đến petabyte dữ liệu.  
- EFS cung cấp tính nhất quán mạnh và khóa tệp.
- EFS có thể được sử dụng với phiên bản EC2, Amazon Elastic Container Service (ECS), Amazon Elastic Kubernetes Service (EKS), hàm AWS Lambda, và AWS Fargate.
- EFS có thể được sử dụng để lưu trữ dữ liệu cho nhiều loại khối lượng công việc, bao gồm ứng dụng web, hệ thống quản lý nội dung, cơ sở dữ liệu và học máy.
- Lớp lưu trữ EFS One Zone để lưu trữ chi phí tối ưu.
- EFS Replication để bảo vệ dữ liệu cross-region.

Dưới đây là một số chi tiết bổ sung về EFS mà bạn có thể muốn biết:

- EFS sử dụng giao thức Network File System (NFS) để cung cấp truy cập đến hệ thống tệp.
- Hệ thống tệp EFS có thể được gắn trên phiên bản EC2 trong virtual private cloud (VPC) của bạn.  
- Hệ thống tệp EFS có thể được truy cập từ máy chủ on-premises bằng AWS Direct Connect hoặc AWS VPN.
- Hệ thống tệp EFS có thể được mã hóa bằng AWS Key Management Service (KMS).
- Hệ thống tệp EFS có thể được sử dụng để tạo mảng RAID.
- Hệ thống tệp EFS có thể được sử dụng để tạo volume boot cho phiên bản EC2.

## Amazon Relational Database Service (RDS)  

Amazon Relational Database Service (RDS) là dịch vụ cơ sở dữ liệu được quản lý cung cấp cơ sở hạ tầng cơ sở dữ liệu quan hệ để triển khai, mở rộng quy mô và quản lý cơ sở dữ liệu quan hệ trong đám mây. RDS hỗ trợ nhiều engine cơ sở dữ liệu, bao gồm MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server và Amazon Aurora.

Dưới đây là một số thông tin ngắn về RDS mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- RDS là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô cơ sở dữ liệu của mình.
- RDS hỗ trợ nhiều engine cơ sở dữ liệu, bao gồm MySQL, PostgreSQL, Oracle Database, Microsoft SQL Server, Amazon Aurora, MariaDB và SAP HANA.
- RDS cung cấp độ sẵn sàng cao và bền bỉ cho cơ sở dữ liệu của bạn.
- RDS cung cấp nhiều tính năng để giúp bạn bảo mật cơ sở dữ liệu của mình, bao gồm mã hóa, kiểm soát truy cập, kiểm tra và tích hợp với AWS Secrets Manager.
- RDS có thể được sử dụng để triển khai nhiều loại khối lượng công việc cơ sở dữ liệu, bao gồm ứng dụng web, hệ thống quản lý nội dung và ứng dụng doanh nghiệp.

Dưới đây là một số chi tiết bổ sung về RDS mà bạn có thể muốn biết:

- Phiên bản RDS có thể được triển khai ở nhiều tùy chọn triển khai khác nhau, bao gồm single-AZ, Multi-AZ (với standby hoặc Multi-AZ DB cluster deployments), và read replicas.
- Phiên bản RDS có thể được sao lưu tự động đến Amazon Simple Storage Service (S3).
- Phiên bản RDS có thể được khôi phục từ bản sao lưu để tạo phiên bản RDS mới.  
- Phiên bản RDS có thể được mở rộng quy mô lên hoặc xuống mà không có thời gian ngừng hoạt động.
- Phiên bản RDS có thể được di chuyển từ engine cơ sở dữ liệu này sang engine khác.

## Amazon Aurora  

Amazon Aurora là dịch vụ cơ sở dữ liệu quan hệ kết hợp hiệu suất và độ sẵn sàng của cơ sở dữ liệu thương mại cấp cao với tính đơn giản và hiệu quả chi phí của cơ sở dữ liệu nguồn mở. Aurora tương thích với MySQL và PostgreSQL, vì vậy các nhà phát triển có thể sử dụng mã, kỹ năng và công cụ hiện có để xây dựng ứng dụng mới hoặc di chuyển ứng dụng hiện có sang đám mây.

Dưới đây là một số thông tin ngắn về Aurora mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Aurora là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô cơ sở dữ liệu của mình.
- Aurora tương thích với MySQL và PostgreSQL, vì vậy các nhà phát triển có thể sử dụng mã, kỹ năng và công cụ hiện có để xây dựng ứng dụng mới hoặc di chuyển ứng dụng hiện có sang đám mây.
- Aurora nhanh hơn gấp năm lần so với cơ sở dữ liệu MySQL và PostgreSQL tiêu chuẩn, và nó cung cấp 99.99% độ sẵn sàng.
- Aurora hiệu quả chi phí, và nó cung cấp nhiều tính năng để giúp bạn tiết kiệm tiền, chẳng hạn như tự động mở rộng quy mô, reserved instances và tùy chọn serverless.
- Aurora có thể được sử dụng để triển khai nhiều loại khối lượng công việc cơ sở dữ liệu, bao gồm ứng dụng web, hệ thống quản lý nội dung, ứng dụng doanh nghiệp và học máy.

Dưới đây là một số chi tiết bổ sung về Aurora mà bạn có thể muốn biết:

- Aurora sử dụng hệ thống lưu trữ phân tán để đạt được hiệu suất và độ sẵn sàng cao.  
- Aurora hỗ trợ nhiều Availability Zone để độ sẵn sàng cao và khôi phục thảm họa.
- Aurora cung cấp sao lưu liên tục và khôi phục point-in-time.
- Aurora có thể được mở rộng quy mô lên hoặc xuống mà không có thời gian ngừng hoạt động.
- Aurora tương thích với Amazon RDS tools và APIs.

## Amazon DynamoDB

Amazon DynamoDB là cơ sở dữ liệu NoSQL được quản lý hoàn toàn, đa vùng, đa master, bền bỉ với bảo mật tích hợp, sao lưu và khôi phục, và bộ nhớ đệm trong bộ nhớ cho ứng dụng internet-scale. DynamoDB cung cấp hiệu suất mili giây đơn vị ở bất kỳ quy mô nào. Nó là cơ sở dữ liệu linh hoạt và có thể mở rộng quy mô có thể được sử dụng cho nhiều loại khối lượng công việc, bao gồm di động, web, chơi game, quảng cáo, IoT và hơn thế nữa.

Dưới đây là một số thông tin ngắn về DynamoDB mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- DynamoDB là cơ sở dữ liệu NoSQL, có nghĩa là nó không sử dụng schema cơ sở dữ liệu quan hệ truyền thống.  
- DynamoDB là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô cơ sở dữ liệu của mình.
- DynamoDB có độ sẵn sàng cao và bền bỉ, và nó có thể mở rộng quy mô đến petabyte dữ liệu.
- DynamoDB cung cấp hiệu suất mili giây đơn vị ở bất kỳ quy mô nào.
- DynamoDB hiệu quả chi phí, và nó cung cấp nhiều tính năng để giúp bạn tiết kiệm tiền, chẳng hạn như reserved capacity, provisioned throughput và chế độ on-demand capacity.
- DynamoDB có thể được sử dụng để triển khai nhiều loại khối lượng công việc cơ sở dữ liệu, bao gồm di động, web, chơi game, quảng cáo, IoT và học máy.
- DynamoDB Accelerator (DAX) cho bộ nhớ đệm trong bộ nhớ.

Dưới đây là một số chi tiết bổ sung về DynamoDB mà bạn có thể muốn biết:

- DynamoDB sử dụng mô hình dữ liệu key-value và document, hỗ trợ cả đọc eventually consistent và strongly consistent.
- Bảng DynamoDB bao gồm các mục, là tập hợp các cặp attribute-value.
- Bảng DynamoDB có thể có một hoặc nhiều primary key, được sử dụng để xác định và truy xuất mục.
- Bảng DynamoDB cũng có thể có secondary indexes (Global Secondary Indexes và Local Secondary Indexes), được sử dụng để truy vấn mục dựa trên giá trị attribute.
- DynamoDB cung cấp nhiều APIs để truy cập và quản lý dữ liệu, bao gồm AWS SDKs, AWS CLI và AWS Management Console.

## Amazon Redshift  

Amazon Redshift là dịch vụ data warehouse được quản lý hoàn toàn, petabyte-scale trong đám mây. Redshift giúp đơn giản và tiết kiệm chi phí để phân tích tất cả dữ liệu của bạn bằng SQL tiêu chuẩn và công cụ BI hiện có. Redshift nhanh hơn gấp 100 lần so với data warehouse truyền thống, và nó cung cấp nhiều tính năng để giúp bạn phân tích dữ liệu của mình, bao gồm:

- **Xử lý song song hàng loạt (MPP):** Redshift sử dụng MPP để phân tán dữ liệu trên nhiều nút tính toán, cho phép nó xử lý tập dữ liệu lớn nhanh chóng và hiệu quả.
- **Lưu trữ cột:** Redshift lưu trữ dữ liệu theo cột, cải thiện đáng kể hiệu suất cho truy vấn phân tích.
- **Trình tối ưu hóa truy vấn nâng cao:** Tối ưu hóa kế hoạch thực thi truy vấn để có kết quả nhanh hơn.
- **Materialized Views:** Tiền tính toán và lưu trữ kết quả của truy vấn phức tạp để truy cập nhanh hơn.
- **Concurrency Scaling:** Tự động thêm dung lượng để xử lý truy vấn đồng thời.
- **Redshift ML:** Tạo, đào tạo và triển khai mô hình học máy trực tiếp từ Redshift.
- **Tương thích SQL:** Redshift tương thích với SQL tiêu chuẩn, vì vậy bạn có thể sử dụng công cụ BI hiện có để phân tích dữ liệu của mình.
- **Redshift Serverless:** Chạy và mở rộng quy mô khối lượng công việc data warehouse mà không quản lý cơ sở hạ tầng.

Dưới đây là một số thông tin ngắn về Redshift mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Redshift là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô data warehouse của mình.  
- Redshift nhanh hơn gấp 100 lần so với data warehouse truyền thống.
- Redshift tương thích với SQL tiêu chuẩn.
- Redshift hiệu quả chi phí, và nó cung cấp nhiều tính năng để giúp bạn tiết kiệm tiền, chẳng hạn như reserved instances và spot instances.
- Redshift có thể được sử dụng để triển khai nhiều loại khối lượng công việc data warehouse, bao gồm phân tích, business intelligence và học máy.

Dưới đây là một số chi tiết bổ sung về Redshift mà bạn có thể muốn biết:

- Cụm Redshift có thể được triển khai ở nhiều kích thước khác nhau, từ cụm nhỏ cho phát triển và thử nghiệm đến cụm lớn cho sản xuất.
- Cụm Redshift có thể được mở rộng quy mô lên (resize) hoặc mở rộng quy mô ra (Concurrency Scaling) mà không có thời gian ngừng hoạt động.
- Cụm Redshift có thể được sao lưu tự động đến Amazon Simple Storage Service (S3).
- Cụm Redshift có thể được khôi phục từ bản sao lưu để tạo cụm Redshift mới.
- Redshift có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon Athena, Amazon EMR và Amazon QuickSight.

## Amazon Simple Queue Service (SQS)

Amazon Simple Queue Service (SQS) là dịch vụ hàng đợi thông điệp được quản lý hoàn toàn cho phép bạn tách rời và mở rộng quy mô microservices, hệ thống phân tán và ứng dụng serverless. SQS cung cấp cách đơn giản, đáng tin cậy và có thể mở rộng quy mô để tách rời và mở rộng quy mô hệ thống phân tán và microservices. Nó là hàng đợi lưu trữ được quản lý, bền bỉ và có thể mở rộng quy mô để lưu trữ thông điệp khi chúng di chuyển giữa ứng dụng hoặc microservices. SQS di chuyển dữ liệu giữa các thành phần ứng dụng phân tán và giúp bạn tách rời các thành phần này.

Dưới đây là một số thông tin ngắn về SQS mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- SQS là dịch vụ hàng đợi thông điệp, có nghĩa là nó lưu trữ thông điệp khi chúng di chuyển giữa ứng dụng hoặc microservices.
- SQS là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô hàng đợi của mình.
- SQS có độ sẵn sàng cao và bền bỉ, và nó có thể mở rộng quy mô đến hàng triệu thông điệp mỗi giây.
- SQS hiệu quả chi phí, và nó cung cấp nhiều tính năng để giúp bạn tiết kiệm tiền, chẳng hạn như giá pay-as-you-go và dead-letter queues.
- SQS có thể được sử dụng để tách rời và mở rộng quy mô nhiều loại ứng dụng và microservices, bao gồm ứng dụng web, ứng dụng di động và IoT.
- SQS có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon Lambda, Amazon SNS, AWS EventBridge và AWS S3.

Dưới đây là một số chi tiết bổ sung về SQS mà bạn có thể muốn biết:

- SQS cung cấp hai loại hàng đợi: Standard Queues (giao nhận at-least-once, best-effort ordering) và FIFO Queues (xử lý exactly-once, ordering nghiêm ngặt).
- Hàng đợi SQS có thể được cấu hình với các timeout visibility khác nhau, xác định thời gian thông điệp hiển thị cho người tiêu dùng trước khi được ẩn tự động.
- Hàng đợi SQS có thể được cấu hình với dead-letter queues, là hàng đợi nơi thông điệp được gửi nếu chúng không thể được xử lý thành công.
- SQS có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon Lambda, Amazon SNS, AWS EventBridge và AWS S3.

## Amazon Simple Notification Service (SNS)

Amazon Simple Notification Service (SNS) là dịch vụ thông điệp pub/sub được quản lý hoàn toàn cho phép bạn tách rời microservices, hệ thống phân tán và ứng dụng serverless. SNS cung cấp cách đơn giản, đáng tin cậy và có thể mở rộng quy mô để thông báo cho nhiều người đăng ký về tính sẵn sàng của dữ liệu mới, chẳng hạn như thông điệp trong hàng đợi hoặc sự kiện trong cơ sở dữ liệu.

Dưới đây là một số thông tin ngắn về Amazon SNS mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- SNS là dịch vụ thông điệp pub/sub, có nghĩa là nhà xuất bản gửi thông điệp đến topics, và người đăng ký nhận thông điệp từ topics.
- SNS là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô cơ sở hạ tầng thông điệp của mình.
- SNS có độ sẵn sàng cao và bền bỉ, và nó có thể mở rộng quy mô đến hàng triệu thông điệp mỗi giây.
- SNS hiệu quả chi phí, và nó cung cấp nhiều tính năng để giúp bạn tiết kiệm tiền, chẳng hạn như giá pay-as-you-go và dead-letter queues.
- SNS có thể được sử dụng để tách rời và mở rộng quy mô nhiều loại ứng dụng và microservices, bao gồm ứng dụng web, ứng dụng di động và IoT.

Dưới đây là một số chi tiết bổ sung về Amazon SNS mà bạn có thể muốn biết:

- Topics SNS có thể có nhiều người đăng ký, và người đăng ký có thể đăng ký nhiều topics.
- Thông điệp SNS có thể được gửi ở nhiều định dạng khác nhau, bao gồm JSON, XML và văn bản thô.
- Thông điệp SNS có thể được mã hóa tại nghỉ ngơi (SSE) và khi truyền (HTTPS).
- Thông điệp SNS có thể được giao đến nhiều điểm cuối khác nhau, bao gồm email, SMS, HTTP/S, hàng đợi Amazon SQS, hàm AWS Lambda, thông báo đẩy di động và thông báo đẩy di động.
- SNS có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EC2, Amazon Lambda, Amazon CloudWatch, AWS EventBridge và Amazon Kinesis Data Firehose.
- SNS hỗ trợ FIFO topics để ordering thông điệp nghiêm ngặt, deduplication và grouping thông điệp.

## Amazon API Gateway

Amazon API Gateway là dịch vụ được quản lý hoàn toàn giúp dễ dàng tạo, xuất bản, duy trì, giám sát và bảo mật API ở bất kỳ quy mô nào. Với API Gateway, bạn có thể tạo REST APIs truy cập dữ liệu, ứng dụng và dịch vụ được lưu trữ trên AWS hoặc on-premises. API Gateway cũng cung cấp nhiều tính năng để giúp bạn quản lý API của mình, bao gồm:

- **Ủy quyền và xác thực API:** Bạn có thể sử dụng API Gateway để ủy quyền và xác thực người dùng của API của mình bằng nhiều phương thức khác nhau, bao gồm vai trò AWS Identity and Access Management (IAM), nhóm người dùng Amazon Cognito và OAuth 2.0.
- **Giám sát API:** API Gateway cung cấp số liệu chi tiết (CloudWatch) và logs (CloudWatch Logs, X-Ray) cho API của bạn, để bạn có thể giám sát hiệu suất và xác định bất kỳ vấn đề nào.
- **Lưu trữ API:** API Gateway có thể lưu trữ phản hồi cho API của bạn, có thể cải thiện hiệu suất và giảm tải trên hệ thống backend của bạn.
- **Phiên bản API:** API Gateway hỗ trợ phiên bản API và stages, để bạn có thể tạo phiên bản mới của API mà không phá vỡ khách hàng hiện có.
- **Usage Plans:** Kiểm soát truy cập đến API của bạn và throttling requests.
- **Tích hợp AWS WAF:** Bảo vệ API của bạn khỏi các exploit web phổ biến.

Dưới đây là một số thông tin ngắn về API Gateway mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- API Gateway là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô cơ sở hạ tầng API của mình.
- API Gateway hỗ trợ REST APIs, WebSocket APIs, HTTP APIs (tối ưu hóa cho khối lượng công việc serverless), và gRPC APIs.
- API Gateway cung cấp nhiều tính năng để giúp bạn quản lý API của mình, bao gồm ủy quyền và xác thực, giám sát, lưu trữ và phiên bản.
- API Gateway có thể được sử dụng để tạo API truy cập dữ liệu, ứng dụng và dịch vụ được lưu trữ trên AWS hoặc on-premises.

Dưới đây là một số chi tiết bổ sung về API Gateway mà bạn có thể muốn biết:

- API Gateway APIs được định nghĩa bằng thông số OpenAPI.
- API Gateway APIs có thể được triển khai đến production, staging và test environments bằng stages.
- API Gateway APIs có thể được gọi bằng nhiều công cụ khác nhau, bao gồm AWS Console, AWS CLI, AWS SDKs và khách hàng tùy chỉnh.
- API Gateway có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như AWS Lambda, Amazon DynamoDB, Amazon S3, AWS Step Functions và AWS AppSync.
- API Gateway hỗ trợ private APIs để truy cập an toàn trong VPC.

## Amazon Cognito  

Amazon Cognito là dịch vụ quản lý danh tính và truy cập người dùng được quản lý hoàn toàn cho phép bạn dễ dàng thêm xác thực người dùng, ủy quyền và quản lý vào ứng dụng web và di động của mình. Cognito cung cấp các tính năng như đăng ký người dùng, đăng nhập, đăng xuất, khôi phục mật khẩu và kiểm soát truy cập, để bạn có thể tập trung vào việc xây dựng trải nghiệm người dùng tuyệt vời.

Cognito có thể được sử dụng để xác thực người dùng bằng nhiều phương thức khác nhau, bao gồm:

- **Tên người dùng và mật khẩu**
- **Đăng nhập xã hội** (ví dụ: Facebook, Google, Amazon, Apple)
- **Xác thực đa yếu tố (MFA)** với SMS hoặc TOTP
- **Lược đồ xác thực tùy chỉnh** (ví dụ: sử dụng AWS Lambda)
- **Federation SAML và OIDC** cho danh tính doanh nghiệp

Cognito cũng có thể được sử dụng để ủy quyền người dùng truy cập tài nguyên của bạn. Ví dụ, bạn có thể sử dụng Cognito để tạo nhóm người dùng và vai trò, và sau đó gán quyền cho các nhóm và vai trò đó. Điều này cho phép bạn kiểm soát ai có quyền truy cập gì trong ứng dụng của mình. Cognito tích hợp với AWS IAM để kiểm soát truy cập chi tiết.

Cognito là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần lo lắng về việc cung cấp, quản lý hoặc mở rộng quy mô cơ sở hạ tầng IAM của mình. Cognito cũng có độ sẵn sàng cao và bền bỉ, vì vậy bạn có thể tự tin rằng người dùng của mình sẽ có thể truy cập ứng dụng của mình khi họ cần.

Dưới đây là một số thông tin ngắn về Amazon Cognito mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Cognito là dịch vụ quản lý danh tính và truy cập người dùng được quản lý hoàn toàn.
- Cognito có thể được sử dụng để xác thực người dùng bằng nhiều phương thức khác nhau, bao gồm tên người dùng và mật khẩu, đăng nhập xã hội, MFA và lược đồ xác thực tùy chỉnh.
- Cognito cũng có thể được sử dụng để ủy quyền người dùng truy cập tài nguyên của bạn.  
- Cognito là dịch vụ có độ sẵn sàng cao và bền bỉ.

Dưới đây là một số chi tiết bổ sung về Amazon Cognito mà bạn có thể muốn biết:

- Cognito User Pools cung cấp thư mục người dùng an toàn cho đăng ký và đăng nhập, quản lý hồ sơ người dùng và phát hành JWT tokens.
- Cognito Identity Pools (Federated Identities) cho phép bạn cấp cho người dùng của mình thông tin xác thực AWS tạm thời để truy cập dịch vụ AWS trực tiếp.
- Cognito hỗ trợ nhiều nhà cung cấp danh tính khác nhau, bao gồm xã hội (Facebook, Google, Apple, Amazon), SAML và OIDC.
- Ủy quyền Cognito có thể được sử dụng để kiểm soát ai có quyền truy cập gì trong ứng dụng của mình thông qua chính sách IAM.
- Cognito hỗ trợ di chuyển người dùng để chuyển đổi liền mạch từ thư mục người dùng hiện có.
- Cognito có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon API Gateway, AWS Lambda và Amazon S3.

## Amazon CloudWatch  

Amazon CloudWatch là dịch vụ giám sát và quan sát cung cấp dữ liệu và hiểu biết trong logs, metrics và events. Nó thu thập metrics và logs từ tất cả dịch vụ AWS của bạn, và bạn có thể giám sát chúng, trực quan hóa dữ liệu và hành động tự động để thay đổi trong các dịch vụ này.

Dưới đây là một số thông tin ngắn về CloudWatch mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- CloudWatch thu thập và giám sát metrics, logs và events từ tất cả dịch vụ và tài nguyên AWS.
- Metrics CloudWatch là các giá trị số đo lường hiệu suất của tài nguyên AWS của bạn.
- Logs CloudWatch là tệp văn bản chứa thông tin về các sự kiện xảy ra trong tài nguyên AWS của bạn.
- Events CloudWatch là thông báo được tạo bởi dịch vụ và tài nguyên AWS khi các sự kiện nhất định xảy ra.
- Dashboards CloudWatch cho phép bạn trực quan hóa metrics, logs và events của mình theo thời gian thực.
- Alarms CloudWatch cho phép bạn được thông báo khi các điều kiện nhất định được đáp ứng.

Dưới đây là một số chi tiết bổ sung về CloudWatch mà bạn có thể muốn biết:

- Metrics CloudWatch có thể được sử dụng để giám sát nhiều đặc điểm hiệu suất khác nhau, chẳng hạn như CPU utilization, memory usage và disk I/O.
- CloudWatch Logs có thể được sử dụng để khắc phục sự cố, phân tích xu hướng và kiểm tra hệ thống của bạn. Log Insights cho phép phân tích tương tác của dữ liệu log.
- CloudWatch Events (bây giờ là Amazon EventBridge) có thể được sử dụng để kích hoạt dịch vụ AWS khác, chẳng hạn như Auto Scaling và Lambda, dựa trên events.
- Dashboards CloudWatch có thể được sử dụng để tạo chế độ xem tùy chỉnh của metrics, logs và events của bạn để giám sát thời gian thực.
- Alarms CloudWatch có thể được sử dụng để thông báo cho bạn qua email, SMS hoặc SNS, hoặc kích hoạt hành động tự động (ví dụ: Auto Scaling, hành động EC2) khi các điều kiện nhất định được đáp ứng.
- CloudWatch Contributor Insights giúp bạn tìm top talkers và xác định nguyên nhân gốc của các vấn đề hiệu suất.
- CloudWatch Synthetics cho phép bạn tạo canaries để giám sát endpoints và APIs của bạn.
- CloudWatch Internet Monitor để giám sát hiệu suất internet.
- CloudWatch Application Signals để giám sát hiệu suất ứng dụng.

## AWS CloudTrail  

AWS CloudTrail là dịch vụ cho phép quản trị, tuân thủ, kiểm tra vận hành và giảm thiểu rủi ro bằng cách ghi lại, logging, lưu trữ và phân phối tệp log sự kiện ghi lại các cuộc gọi API được thực hiện đến tài khoản AWS của bạn và tài nguyên của bạn. Với CloudTrail, bạn có thể theo dõi hoạt động người dùng và sử dụng API trên dịch vụ AWS của mình và tài nguyên.

Dưới đây là một số thông tin ngắn mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- CloudTrail là dịch vụ được quản lý hoàn toàn liên tục logging tất cả cuộc gọi API được thực hiện đến tài khoản AWS của bạn và tài nguyên của bạn.
- Logs CloudTrail có thể được phân phối đến Amazon S3 và Amazon CloudWatch Logs.
- Logs CloudTrail có thể được sử dụng để theo dõi hoạt động người dùng, khắc phục sự cố và kiểm tra môi trường AWS của bạn.
- Logs CloudTrail có thể được giữ lại lên đến hai năm.

Dưới đây là một số chi tiết bổ sung mà bạn có thể muốn biết:

- Logs CloudTrail có thể được lọc để chỉ bao gồm events quan trọng đối với bạn.
- Logs CloudTrail có thể được sử dụng để tạo alerts và thông báo qua CloudWatch Alarms.
- Logs CloudTrail có thể được tích hợp với dịch vụ AWS khác, chẳng hạn như Amazon IAM, Amazon GuardDuty và AWS Security Hub.
- CloudTrail Lake cho phép lưu trữ bất biến và truy vấn SQL của events.
- CloudTrail Insights để phát hiện bất thường.

Ví dụ về trường hợp sử dụng của CloudTrail:

- **Kiểm tra:** Logs CloudTrail có thể được sử dụng để kiểm tra tất cả cuộc gọi API được thực hiện đến tài khoản AWS của bạn và tài nguyên của bạn. Điều này có thể giúp bạn xác định bất kỳ hoạt động đáng ngờ hoặc truy cập trái phép nào vào tài nguyên của bạn.
- **Khắc phục sự cố:** Logs CloudTrail có thể được sử dụng để khắc phục sự cố với tài nguyên AWS của bạn. Ví dụ, nếu bạn đang gặp vấn đề hiệu suất, bạn có thể xem xét logs CloudTrail của mình để xem cuộc gọi API nào dẫn đến vấn đề.
- **Tuân thủ:** Logs CloudTrail có thể được sử dụng để giúp bạn tuân thủ các quy định ngành khác nhau. Ví dụ, nếu bạn phải tuân thủ HIPAA, bạn có thể sử dụng logs CloudTrail để theo dõi tất cả truy cập đến thông tin sức khỏe được bảo vệ (PHI) của bạn.

## AWS Identity and Access Management (IAM)

AWS Identity and Access Management (IAM) là dịch vụ web cho phép bạn kiểm soát an toàn truy cập đến dịch vụ và tài nguyên AWS. Sử dụng IAM, bạn có thể tạo và quản lý người dùng và nhóm AWS, và sử dụng quyền để cho phép và từ chối truy cập của họ đến tài nguyên AWS.

Dưới đây là một số thông tin ngắn mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- IAM là dịch vụ được quản lý hoàn toàn cho phép bạn kiểm soát an toàn truy cập đến dịch vụ và tài nguyên AWS.  
- IAM sử dụng người dùng, nhóm và vai trò để quản lý truy cập đến tài nguyên AWS.
- IAM sử dụng chính sách dựa trên danh tính (đính kèm với người dùng, nhóm, vai trò), chính sách dựa trên tài nguyên (đính kèm với tài nguyên như bucket S3, hàng đợi SQS), và danh sách kiểm soát truy cập (ACLs) để quản lý truy cập đến tài nguyên AWS.
- Người dùng IAM là những người riêng lẻ được ủy quyền sử dụng dịch vụ và tài nguyên AWS.
- Nhóm IAM là tập hợp người dùng IAM được gán cùng quyền.
- Vai trò IAM là tập hợp quyền có thể được gán cho người dùng hoặc nhóm IAM.
- Quyền IAM là hành động mà người dùng hoặc nhóm IAM được phép thực hiện trên tài nguyên AWS.

Dưới đây là một số chi tiết bổ sung mà bạn có thể muốn biết:

- IAM có thể được sử dụng để triển khai truy cập least privilege, có nghĩa là người dùng và nhóm chỉ được cấp quyền họ cần để thực hiện công việc của mình.
- IAM có thể được sử dụng để triển khai xác thực đa yếu tố (MFA) để bảo mật nâng cao.
- IAM có thể được sử dụng để kiểm tra tất cả truy cập đến tài nguyên AWS của bạn bằng AWS CloudTrail và IAM Access Analyzer.
- IAM Access Analyzer giúp xác định truy cập không mong muốn đến tài nguyên của bạn.
- IAM Roles Anywhere cho phép khối lượng công việc bên ngoài AWS sử dụng vai trò IAM.
- IAM hỗ trợ kiểm soát truy cập dựa trên thuộc tính (ABAC) để quyền chi tiết.

Ví dụ về trường hợp sử dụng của IAM:

- **Tạo và quản lý người dùng và nhóm AWS:** IAM có thể được sử dụng để tạo và quản lý người dùng và nhóm AWS. Điều này cho phép bạn kiểm soát ai có truy cập đến tài nguyên AWS của bạn và họ có thể làm gì với chúng.
- **Triển khai truy cập least privilege:** IAM có thể được sử dụng để triển khai truy cập least privilege, có nghĩa là người dùng và nhóm chỉ được cấp quyền họ cần để thực hiện công việc của mình. Điều này giúp cải thiện bảo mật của môi trường AWS của bạn.
- **Triển khai xác thực đa yếu tố:** IAM có thể được sử dụng để triển khai xác thực đa yếu tố (MFA), thêm lớp bảo mật bổ sung cho tài khoản AWS của bạn. MFA yêu cầu người dùng nhập mã từ điện thoại di động của họ ngoài mật khẩu khi đăng nhập.  
- **Kiểm tra tất cả truy cập đến tài nguyên AWS của bạn:** IAM có thể được sử dụng để kiểm tra tất cả truy cập đến tài nguyên AWS của bạn, để bạn có thể theo dõi ai đang truy cập cái gì và khi nào. Thông tin này có thể được sử dụng để khắc phục sự cố và xác định hoạt động đáng ngờ.

## AWS Key Management Service (KMS)

AWS Key Management Service (KMS) là dịch vụ được quản lý giúp bạn dễ dàng tạo và kiểm soát các khóa mật mã được sử dụng để bảo vệ dữ liệu của bạn. KMS cung cấp nhiều tính năng giúp dễ dàng quản lý khóa của bạn một cách an toàn, bao gồm:

- **Tạo khóa:** KMS có thể tạo khóa mật mã chất lượng cao cho bạn.
- **Lưu trữ khóa:** KMS lưu trữ khóa của bạn trong môi trường an toàn cao.
- **Xoay khóa:** KMS có thể xoay khóa của bạn theo định kỳ để giúp bảo vệ chúng khỏi bị xâm phạm.
- **Kiểm tra khóa:** KMS cung cấp kiểm tra chi tiết về tất cả hoạt động khóa.

Dưới đây là một số thông tin ngắn mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- KMS là dịch vụ được quản lý giúp bạn dễ dàng tạo và kiểm soát các khóa mật mã được sử dụng để bảo vệ dữ liệu của bạn.
- KMS cung cấp nhiều tính năng giúp dễ dàng quản lý khóa của bạn một cách an toàn, bao gồm tạo khóa, lưu trữ khóa, xoay khóa và kiểm tra khóa.
- KMS có thể được sử dụng để mã hóa dữ liệu tại nghỉ ngơi và khi truyền.
- KMS mã hóa dữ liệu lên đến 4KB mỗi cuộc gọi. Đối với dữ liệu lớn hơn, sử dụng envelope encryption với AWS Encryption Encryption SDK.
- KMS hỗ trợ custom key stores được sao lưu bởi CloudHSM hoặc nhà quản lý khóa bên ngoài.
- KMS có thể được sử dụng để quản lý khóa cho nhiều dịch vụ AWS, bao gồm Amazon S3, Amazon RDS, Amazon EBS, Amazon DynamoDB và AWS Lambda.
- KMS hỗ trợ khóa mã hóa symmetric và asymmetric, và khóa HMAC.

Dưới đây là một số chi tiết bổ sung mà bạn có thể muốn biết:

- KMS sử dụng nhiều biện pháp bảo mật để bảo vệ khóa của bạn, bao gồm module bảo mật phần cứng (HSMs) và mã hóa.
- KMS có độ sẵn sàng cao và bền bỉ.
- KMS được tích hợp với nhiều dịch vụ AWS khác.

Ví dụ về trường hợp sử dụng của KMS:

- **Mã hóa dữ liệu tại nghỉ ngơi:** KMS có thể được sử dụng để mã hóa dữ liệu tại nghỉ ngơi trong Amazon S3, Amazon RDS và Amazon EBS. Điều này giúp bảo vệ dữ liệu của bạn khỏi truy cập trái phép, ngay cả khi phương tiện lưu trữ cơ bản bị xâm phạm.
- **Mã hóa dữ liệu khi truyền:** KMS có thể được sử dụng để mã hóa dữ liệu khi truyền giữa dịch vụ AWS. Điều này giúp bảo vệ dữ liệu của bạn khỏi bị nghe lén và man-in-the-middle attacks.
- **Quản lý khóa cho nhiều dịch vụ AWS:** KMS có thể được sử dụng để quản lý khóa cho nhiều dịch vụ AWS, ngoài Amazon S3, Amazon RDS và Amazon EBS. Điều này bao gồm dịch vụ như Amazon CloudFront, Amazon Elasticsearch Service và Amazon Redshift.

## AWS Security Hub  

AWS Security Hub cung cấp quản trị bảo mật tập trung trên tài khoản AWS với các tính năng liên quan đến kỳ thi chính sau:

- **Tiêu chuẩn tuân thủ**:
  - PCI DSS v4.0 (cập nhật mới nhất)
  - AWS Foundational Security Best Practices (FSBP)
  - CIS AWS Foundations Benchmark
  - NIST SP 800-53
  - ISO 27001
- **Tương quan findings tự động**: Nhóm các findings liên quan từ GuardDuty, Inspector, Macie, IAM Access Analyzer và các dịch vụ tích hợp khác.
- **Điểm bảo mật**: Đo lường định lượng về trạng thái tuân thủ và tư thế bảo mật tổng thể.
- **Tích hợp đa vùng/tài khoản**: Chế độ xem tập trung về tư thế bảo mật trên nhiều tài khoản và vùng AWS.
- **Tích hợp với AWS Organizations**: Quản lý bảo mật ở quy mô trên tổ chức của bạn.
- **Insights tùy chỉnh**: Tạo truy vấn tùy chỉnh để xác định các vấn đề bảo mật cụ thể.
- **Khắc phục tự động**: Tích hợp với AWS Systems Manager Automation và AWS Lambda để phản hồi tự động.

Dưới đây là một số thông tin ngắn mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Security Hub là dịch vụ quản lý tư thế bảo mật đám mây cung cấp chế độ xem toàn diện về trạng thái bảo mật của bạn trên tài khoản, dịch vụ và sản phẩm bên thứ ba được hỗ trợ.
- Security Hub thu thập findings từ nhiều nguồn khác nhau, bao gồm Amazon GuardDuty, Amazon Inspector, Amazon Macie và AWS IAM Access Analyzer, và ưu tiên chúng dựa trên mức độ nghiêm trọng và rủi ro.
- Security Hub cũng cung cấp khuyến nghị cho khắc phục, để bạn có thể nhanh chóng và dễ dàng giải quyết bất kỳ vấn đề bảo mật nào.  
- Security Hub có thể được tích hợp với dịch vụ AWS khác, chẳng hạn như Amazon EventBridge và Amazon CloudWatch, để tự động hóa hành động khắc phục.
- Security Hub hỗ trợ kiểm soát bảo mật cho dịch vụ AWS và sản phẩm đối tác.

Dưới đây là một số chi tiết bổ sung mà bạn có thể muốn biết:

- Security Hub là dịch vụ khu vực. Bạn phải bật Security Hub ở mỗi vùng mà bạn muốn sử dụng nó.
- Security Hub có thể được sử dụng để tạo tiêu chuẩn bảo mật tùy chỉnh và chính sách.
- Security Hub có thể được sử dụng để tạo báo cáo về tư thế bảo mật của bạn.

Ví dụ về trường hợp sử dụng của Security Hub:

- **Xác định và khắc phục vấn đề bảo mật:** Security Hub tổng hợp findings trên nhiều dịch vụ bảo mật AWS (ví dụ: GuardDuty, Inspector, Macie, IAM Access Analyzer) và giải pháp đối tác.
- **Đáp ứng yêu cầu tuân thủ:** Kiểm tra tuân thủ tự động cho nhiều tiêu chuẩn ngành (ví dụ: PCI DSS, HIPAA, ISO 27001, NIST).
- **Tự động hóa bảo mật:** Tích hợp với AWS Systems Manager Automation và AWS Lambda cho quy trình khắc phục tự động.
- **Vận hành bảo mật tập trung:** Cung cấp một pane of glass duy nhất cho quản lý tư thế bảo mật trên môi trường AWS của bạn.

## AWS CloudFormation

AWS CloudFormation là dịch vụ giúp bạn mô hình hóa và thiết lập tài nguyên cơ sở hạ tầng AWS của mình. CloudFormation cho phép bạn sử dụng templates để định nghĩa tập hợp tài nguyên AWS và các phụ thuộc giữa chúng. Sau đó, bạn có thể triển khai, cập nhật hoặc xóa cơ sở hạ tầng của mình bằng một template CloudFormation duy nhất.

Dưới đây là một số thông tin ngắn mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- CloudFormation là dịch vụ giúp bạn mô hình hóa và thiết lập tài nguyên cơ sở hạ tầng AWS của mình.
- CloudFormation sử dụng templates để định nghĩa tập hợp tài nguyên AWS và các phụ thuộc giữa chúng.
- Templates CloudFormation có thể được viết bằng JSON hoặc YAML.
- Templates CloudFormation có thể được sử dụng để triển khai, cập nhật hoặc xóa cơ sở hạ tầng của bạn theo cách có kiểm soát và lặp lại.
- CloudFormation có thể được sử dụng để triển khai best practices, chẳng hạn như infrastructure as code và idempotency, và kiểm soát phiên bản.
- CloudFormation Drift Detection giúp xác định khi cấu hình stack đã triển khai của bạn khác với template của nó.
- CloudFormation Hooks cho phép bạn gọi logic tùy chỉnh trước hoặc sau hoạt động tài nguyên.

Dưới đây là một số chi tiết bổ sung mà bạn có thể muốn biết:

- Templates CloudFormation có thể được tham số hóa, cho phép bạn tạo templates có thể tái sử dụng.
- Templates CloudFormation có thể được lồng nhau, cho phép bạn tạo triển khai cơ sở hạ tầng phức tạp.
- Templates CloudFormation có thể được phiên bản hóa, cho phép bạn theo dõi thay đổi đối với cơ sở hạ tầng của bạn theo thời gian.
- CloudFormation có thể được tích hợp với dịch vụ AWS khác, chẳng hạn như AWS CodePipeline, AWS Systems Manager và AWS Service Catalog.
- CloudFormation hỗ trợ import tài nguyên để đưa tài nguyên hiện có dưới quản lý CloudFormation.
- CloudFormation hỗ trợ CloudFormation Guard cho policy as code.
- CloudFormation StackSets cho phép bạn triển khai stacks CloudFormation trên nhiều tài khoản và vùng.

Ví dụ về trường hợp sử dụng của CloudFormation:

- **Triển khai ứng dụng web:** CloudFormation có thể được sử dụng để triển khai ứng dụng web, bao gồm phiên bản Amazon EC2, cơ sở dữ liệu Amazon RDS và bucket Amazon S3 cần thiết.
- **Tạo môi trường phát triển:** CloudFormation có thể được sử dụng để tạo môi trường phát triển, bao gồm phiên bản Amazon EC2, cơ sở dữ liệu Amazon RDS và bucket Amazon S3 cần thiết.
- **Triển khai kế hoạch khôi phục thảm họa:** CloudFormation có thể được sử dụng để triển khai kế hoạch khôi phục thảm họa, bao gồm phiên bản Amazon EC2, cơ sở dữ liệu Amazon RDS và bucket Amazon S3 cần thiết.

## AWS Systems Manager

AWS Systems Manager là dịch vụ giúp bạn quản lý và tự động hóa tài nguyên AWS của mình. Systems Manager cung cấp tập hợp công cụ và khả năng có thể được sử dụng để:

- Triển khai, quản lý và cấu hình ứng dụng
- Tự động hóa nhiệm vụ vận hành
- Thu thập và phân tích dữ liệu từ cơ sở hạ tầng của bạn
- Phản hồi sự kiện và alerts

Dưới đây là một số thông tin ngắn mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- Systems Manager là dịch vụ được quản lý hoàn toàn giúp bạn quản lý và tự động hóa tài nguyên AWS của mình.
- Systems Manager cung cấp tập hợp công cụ và khả năng có thể được sử dụng để triển khai, quản lý và cấu hình ứng dụng; tự động hóa nhiệm vụ vận hành; thu thập và phân tích dữ liệu từ cơ sở hạ tầng của bạn; và phản hồi sự kiện và alerts.
- Systems Manager có thể được sử dụng để triển khai best practices, chẳng hạn như infrastructure as code, configuration management và continuous integration and continuous delivery (CI/CD).

Dưới đây là một số chi tiết bổ sung mà bạn có thể muốn biết:

- Systems Manager bao gồm nhiều tính năng khác nhau, chẳng hạn như:
- Patch Manager: Giúp bạn quản lý và triển khai patches phần mềm cho tài nguyên AWS của mình.
- State Manager: Giúp bạn tự động hóa cấu hình và quản lý tài nguyên AWS của mình.
- Automation: Giúp bạn tạo và chạy scripts để tự động hóa nhiệm vụ vận hành trên tài nguyên AWS của mình.
- Inventory: Cung cấp inventory chi tiết của tài nguyên AWS của bạn, bao gồm phần mềm đã cài đặt và chi tiết cấu hình.
- Parameter Store: Cung cấp lưu trữ phân cấp an toàn cho dữ liệu cấu hình và quản lý secrets.
- Session Manager: Cung cấp quản lý phiên bản an toàn và có thể kiểm tra mà không mở cổng inbound.
- Patch Manager: Tự động hóa patching của hệ điều hành và ứng dụng.
- State Manager: Tự động hóa quá trình giữ cho phiên bản EC2 và tài nguyên AWS khác của bạn ở trạng thái được định nghĩa.
- Systems Manager có thể được tích hợp với dịch vụ AWS khác, chẳng hạn như AWS Systems Manager Incident Manager, AWS CloudFormation, AWS CodePipeline và AWS Config.
- Systems Manager hỗ trợ Run Command cho thực thi từ xa của commands trên instances.

Ví dụ về trường hợp sử dụng của Systems Manager:

- **Triển khai ứng dụng:** Systems Manager có thể được sử dụng để triển khai ứng dụng đến fleet phiên bản Amazon EC2.

- **Tự động hóa patching:** Systems Manager có thể được sử dụng để tự động hóa patching của tài nguyên AWS của bạn.

- **Quản lý cấu hình:** Systems Manager có thể được sử dụng để quản lý cấu hình của tài nguyên AWS của bạn.

- **Phản hồi incidents:** Systems Manager có thể được sử dụng để phản hồi incidents bằng cách tự động chạy scripts để khắc phục sự cố và giải quyết vấn đề.

## AWS Well-Architected Framework

AWS Well-Architected Framework là tập hợp các nguyên tắc hướng dẫn để thiết kế và vận hành kiến trúc đám mây đáng tin cậy, an toàn, hiệu quả và tiết kiệm chi phí. Nó bao gồm sáu trụ cột:

- **Operational Excellence:** Tập trung vào việc chạy và giám sát hệ thống để cung cấp giá trị kinh doanh và liên tục cải thiện các quy trình và thủ tục hỗ trợ.
- **Security:** Tập trung vào việc bảo vệ thông tin, hệ thống và tài sản trong khi cung cấp giá trị kinh doanh thông qua đánh giá rủi ro và biện pháp giảm thiểu.
- **Reliability:** Tập trung vào khả năng của hệ thống để khôi phục từ cơ sở hạ tầng hoặc dịch vụ disruptions, động học thu thập tài nguyên tính toán để đáp ứng nhu cầu và giảm thiểu disruptions như misconfigurations hoặc transient network issues.
- **Performance Efficiency:** Tập trung vào việc sử dụng tài nguyên tính toán hiệu quả để đáp ứng yêu cầu hệ thống và duy trì hiệu quả đó khi nhu cầu thay đổi và công nghệ phát triển.
- **Cost Optimization:** Tập trung vào việc tránh chi phí không cần thiết. Điều này bao gồm hiểu và kiểm soát nơi tiền đang được chi tiêu, chọn dịch vụ và tài nguyên phù hợp nhất và đúng kích thước, phân tích chi tiêu theo thời gian và mở rộng quy mô để đáp ứng nhu cầu kinh doanh mà không chi tiêu quá mức.
- **Sustainability:** Tập trung vào việc giảm thiểu tác động môi trường của việc chạy khối lượng công việc đám mây. Điều này bao gồm mô hình trách nhiệm chia sẻ cho tính bền vững giữa AWS và khách hàng.

## AWS Core Services

Dịch vụ cốt lõi AWS là nền tảng của nền tảng đám mây AWS. Chúng cung cấp các khối xây dựng cơ bản để xây dựng, triển khai và quản lý ứng dụng đám mây. Một số dịch vụ cốt lõi quan trọng nhất bao gồm:

- **Amazon Elastic Compute Cloud (EC2):** Dịch vụ web cung cấp khả năng tính toán an toàn, có thể thay đổi quy mô trong đám mây.

- **Amazon Simple Storage Service (S3):** Dịch vụ lưu trữ đối tượng cung cấp khả năng mở rộng, tính sẵn sàng, bảo mật và hiệu suất hàng đầu trong ngành.

- **Amazon Relational Database Service (RDS):** Dịch vụ web giúp dễ dàng thiết lập, vận hành và mở rộng cơ sở dữ liệu quan hệ trong đám mây.

- **Amazon Elastic Block Store (EBS):** Dịch vụ web cung cấp volumes lưu trữ khối cho sử dụng với phiên bản EC2.

## AWS Networking and Security Services

Dịch vụ mạng và bảo mật AWS cung cấp các công cụ bạn cần để xây dựng và quản lý mạng an toàn trong đám mây. Một số dịch vụ mạng và bảo mật quan trọng nhất bao gồm:

- **Amazon Virtual Private Cloud (VPC):** Phân đoạn riêng biệt về mặt logic của đám mây AWS nơi bạn có thể khởi chạy tài nguyên AWS trong mạng riêng.

- **Amazon Simple Notification Service (SNS):** Dịch vụ web cho phép bạn tách rời microservices, hệ thống phân tán và ứng dụng serverless.

- **Amazon Simple Queue Service (SQS):** Dịch vụ hàng đợi thông điệp được quản lý hoàn toàn cho phép bạn tách rời và mở rộng quy mô microservices, hệ thống phân tán và ứng dụng serverless.

- **Amazon Route 53:** Dịch vụ DNS đám mây có độ sẵn sàng và khả năng mở rộng cao.

- **AWS Identity and Access Management (IAM):** Dịch vụ web cho phép bạn kiểm soát an toàn truy cập đến tài nguyên AWS.

## AWS Deployment and Management Services

Dịch vụ triển khai và quản lý AWS cung cấp các công cụ bạn cần để triển khai, quản lý và giám sát ứng dụng đám mây của mình. Một số dịch vụ triển khai và quản lý quan trọng nhất bao gồm:

- **AWS CloudFormation:** Dịch vụ giúp bạn định nghĩa và triển khai tài nguyên trong AWS.

- **AWS Systems Manager:** Bộ sưu tập công cụ và dịch vụ giúp bạn quản lý cơ sở hạ tầng và ứng dụng AWS của mình.

- **AWS CodePipeline:** Dịch vụ CI/CD giúp bạn tự động hóa quy trình phát hành phần mềm của mình.

- **AWS CodeDeploy:** Dịch vụ giúp bạn triển khai, quản lý và mở rộng ứng dụng web và di động của mình.

- **AWS CloudWatch:** Dịch vụ giám sát và quan sát cung cấp dữ liệu và hiểu biết để giúp bạn quản lý tài nguyên và ứng dụng AWS của mình.

## AWS Cost Optimization Strategies  

Chiến lược tối ưu hóa chi phí AWS giúp bạn giảm chi phí AWS mà không hy sinh hiệu suất hoặc độ tin cậy. Một số chiến lược tối ưu hóa chi phí quan trọng nhất bao gồm:

- **Chọn dịch vụ phù hợp cho công việc:** Chọn dịch vụ AWS phù hợp nhất cho khối lượng công việc của bạn, xem xét các tính năng, hiệu suất và mô hình định giá của nó.
- **Right-size tài nguyên của bạn:** Liên tục phân tích và điều chỉnh kích thước tài nguyên AWS của bạn (ví dụ: phiên bản EC2, cơ sở dữ liệu RDS) để phù hợp với nhu cầu thực tế của khối lượng công việc của bạn, tránh over-provisioning.
- **Sử dụng hiệu quả mô hình định giá:**
  - **Savings Plans:** Mô hình định giá linh hoạt cung cấp tiết kiệm đáng kể (lên đến 72%) cho việc sử dụng EC2, Fargate và Lambda trong cam kết 1 năm hoặc 3 năm về lượng sử dụng tính toán nhất quán.
  - **Reserved Instances (RIs):** Cung cấp giảm giá đáng kể (lên đến 75%) so với giá On-Demand cho cam kết về loại phiên bản cụ thể trong vùng cho 1 năm hoặc 3 năm.
  - **Spot Instances:** Tận dụng dung lượng EC2 không sử dụng với giảm giá sâu (lên đến 90%) cho khối lượng công việc chịu lỗi.
- **Triển khai Cost Allocation Tags:** Gắn thẻ tài nguyên của bạn để phân loại và theo dõi chi phí trên các dự án, bộ phận hoặc môi trường khác nhau.
- **Giám sát và Phân tích Chi phí:** Sử dụng AWS Cost Explorer, AWS Budgets và AWS Organizations để trực quan hóa, quản lý và dự báo chi tiêu của bạn, và xác định cơ hội tối ưu hóa chi phí.
- **Tự động hóa Kiểm soát Chi phí:** Triển khai tự động hóa để dừng tài nguyên idle, giảm quy mô trong giờ thấp điểm và xóa tài nguyên không cần thiết.
- **Tận dụng Kiến trúc Serverless:** Chỉ trả cho thời gian tính toán tiêu thụ, loại bỏ chi phí dung lượng idle.
- **Tối ưu hóa Chi phí Chuyển dữ liệu:** Thiết kế kiến trúc để giảm thiểu chuyển dữ liệu trên các vùng, Availability Zones và đến internet.
- **Sử dụng AWS Compute Optimizer:** Nhận khuyến nghị cho right-sizing tài nguyên tính toán của bạn.
- **Sử dụng AWS Trusted Advisor:** Nhận khuyến nghị cho tối ưu hóa chi phí, bảo mật, hiệu suất, độ tin cậy và giới hạn dịch vụ.
- **Xem xét sử dụng lớp lưu trữ chi phí hiệu quả cho S3, chẳng hạn như S3 Glacier Flexible Retrieval và S3 Glacier Deep Archive.**

## Amazon EventBridge

Amazon EventBridge là bus sự kiện serverless giúp dễ dàng kết nối ứng dụng với nhau bằng sự kiện. Nó cho phép bạn tách rời và mở rộng quy mô microservices, ứng dụng serverless và ứng dụng kế thừa. EventBridge có thể phát hiện sự kiện từ nhiều nguồn khác nhau, bao gồm dịch vụ AWS, ứng dụng và thiết bị kết nối. Sau đó, nó có thể định tuyến các sự kiện đó đến mục tiêu như hàm AWS Lambda, máy trạng thái Step Functions, luồng Kinesis và chủ đề Amazon SNS.

Dưới đây là một số thông tin ngắn về Amazon EventBridge mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- EventBridge là bus sự kiện serverless giúp dễ dàng kết nối ứng dụng với nhau bằng sự kiện.
- Nó cho phép bạn tách rời và mở rộng quy mô microservices, ứng dụng serverless và ứng dụng kế thừa.
- EventBridge có thể phát hiện sự kiện từ nhiều nguồn khác nhau, bao gồm dịch vụ AWS, ứng dụng tùy chỉnh của bạn và ứng dụng SaaS (qua tích hợp EventBridge SaaS).
- Nó có thể định tuyến các sự kiện đó đến mục tiêu như hàm AWS Lambda, máy trạng thái Step Functions, luồng Kinesis Amazon và chủ đề Amazon SNS.
- EventBridge là dịch vụ có khả năng mở rộng cao và đáng tin cậy có thể xử lý hàng triệu sự kiện mỗi giây với độ trễ thấp.
- Nó cũng là dịch vụ hiệu quả chi phí, vì bạn chỉ trả cho sự kiện bạn xử lý và phân phối.
- EventBridge Schema Registry cho phép bạn khám phá, quản lý và chia sẻ schemas cho sự kiện.

Dưới đây là một số chi tiết bổ sung về Amazon EventBridge mà bạn có thể muốn biết:

- EventBridge có thể được sử dụng để xây dựng nhiều loại ứng dụng serverless, chẳng hạn như pipelines xử lý dữ liệu thời gian thực, kiến trúc event-driven và hệ thống thông báo.
- Nó cũng có thể được sử dụng để tích hợp dịch vụ AWS với nhau, với ứng dụng tùy chỉnh của bạn và với ứng dụng SaaS bên thứ ba.
- EventBridge là công cụ mạnh mẽ có thể được sử dụng để đơn giản hóa và tự động hóa kiến trúc ứng dụng của bạn, thúc đẩy loose coupling và khả năng mở rộng.
- EventBridge Pipes cho phép bạn xây dựng tích hợp point-to-point giữa nguồn sự kiện và mục tiêu với lọc và làm giàu tùy chọn.
- EventBridge hỗ trợ API Destinations để gọi APIs HTTP.
- EventBridge hỗ trợ EventBridge Archive cho lưu trữ sự kiện lâu dài.

Dưới đây là ví dụ về cách Amazon EventBridge có thể được sử dụng để xây dựng ứng dụng serverless:

- Bạn có ứng dụng tạo sự kiện mới mỗi khi đơn hàng khách hàng mới được đặt.
- Bạn có thể sử dụng EventBridge để tạo quy tắc định tuyến sự kiện này đến hàm AWS Lambda.
- Hàm Lambda sau đó có thể xử lý đơn hàng và gửi email xác nhận đến khách hàng.
- Bạn cũng có thể sử dụng EventBridge để tạo quy tắc định tuyến sự kiện đến chủ đề Amazon SNS.
- Chủ đề này sau đó có thể được sử dụng để thông báo cho các hệ thống khác về đơn hàng mới, chẳng hạn như hệ thống inventory hoặc CRM của bạn.

Đây chỉ là một ví dụ về cách Amazon EventBridge có thể được sử dụng để xây dựng ứng dụng serverless. EventBridge là công cụ linh hoạt và mạnh mẽ có thể được sử dụng để giải quyết nhiều vấn đề khác nhau.

## AWS Step Functions

AWS Step Functions là dịch vụ workflow serverless giúp dễ dàng điều phối việc thực thi các ứng dụng phân tán và microservices. Nó cho phép bạn định nghĩa workflows dưới dạng chuỗi các bước, và sau đó Step Functions sẽ xử lý việc thực thi các bước đó theo thứ tự đúng, xử lý retries và lỗi tự động.

Dưới đây là một số thông tin ngắn về AWS Step Functions mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- AWS Step Functions là dịch vụ workflow serverless giúp dễ dàng điều phối việc thực thi các ứng dụng phân tán và microservices.
- Nó cho phép bạn định nghĩa workflows dưới dạng chuỗi các bước, và sau đó Step Functions sẽ xử lý việc thực thi các bước đó theo thứ tự đúng, xử lý retries và lỗi tự động.
- Step Functions có thể tích hợp với nhiều dịch vụ AWS khác nhau, bao gồm AWS Lambda, Amazon S3, Amazon DynamoDB, Amazon SNS, Amazon SQS, AWS EventBridge và hơn 200 dịch vụ AWS trực tiếp.
- Step Functions là dịch vụ có khả năng mở rộng cao và đáng tin cậy có thể xử lý hàng triệu workflows mỗi giây, với xử lý lỗi tích hợp, retries và thực thi song song.
- Nó cũng là dịch vụ hiệu quả chi phí, vì bạn chỉ trả cho trạng thái transitions và executions.
- Step Functions hỗ trợ hai loại workflows: Standard Workflows (long-running, durable, auditable) và Express Workflows (high-volume, short-duration, event-driven).

Dưới đây là một số chi tiết bổ sung về AWS Step Functions mà bạn có thể muốn biết:

- Workflows Step Functions được định nghĩa bằng Amazon States Language, ngôn ngữ có cấu trúc JSON.
- Workflows Step Functions có thể được thực thi đồng bộ hoặc không đồng bộ, tùy thuộc vào loại workflow (Standard hoặc Express).
- Workflows Step Functions có thể được kích hoạt bởi nhiều loại sự kiện khác nhau, chẳng hạn như sự kiện Amazon EventBridge, tải lên đối tượng S3, chèn luồng DynamoDB hoặc gọi hàm AWS Lambda.
- Workflows Step Functions có thể được giám sát và quản lý bằng AWS Management Console, AWS CLI, AWS SDKs và tích hợp với CloudWatch và X-Ray để quan sát.
- Step Functions Distributed Map cho phép xử lý tập dữ liệu lớn với iterations song song.
- Step Functions hỗ trợ Workflow Studio cho thiết kế workflow trực quan và orchestration.
- Step Functions hỗ trợ tích hợp với hơn 200 dịch vụ AWS, bao gồm tích hợp dịch vụ mới trong 2024-2025.

Dưới đây là ví dụ về cách AWS Step Functions có thể được sử dụng để xây dựng ứng dụng serverless:

- Bạn có ứng dụng xử lý hình ảnh được tải lên S3.
- Bạn có thể sử dụng Step Functions để tạo workflow đầu tiên resize hình ảnh, sau đó chuyển đổi sang định dạng khác và cuối cùng lưu trữ trong bucket S3 khác.
- Workflow có thể được kích hoạt mỗi khi hình ảnh mới được tải lên bucket nguồn S3.
- Step Functions sẽ xử lý việc thực thi các bước của workflow theo thứ tự đúng, xử lý retries và lỗi tự động.

Đây chỉ là một ví dụ về cách AWS Step Functions có thể được sử dụng để xây dựng ứng dụng serverless. Step Functions là công cụ linh hoạt và mạnh mẽ có thể được sử dụng để giải quyết nhiều vấn đề khác nhau.

Dưới đây là một số mẹo để sử dụng AWS Step Functions trong ứng dụng AWS của bạn:

- Sử dụng Step Functions để điều phối việc thực thi các ứng dụng phân tán và microservices.
- Sử dụng Step Functions để tự động hóa workflows phức tạp, chẳng hạn như xử lý đơn hàng, xử lý hình ảnh và xử lý dữ liệu.
- Sử dụng Step Functions để xử lý retries và lỗi tự động.
- Sử dụng Step Functions để tích hợp với nhiều dịch vụ AWS.
- Sử dụng Step Functions để giám sát và quản lý workflows của bạn.

AWS Step Functions là công cụ mạnh mẽ có thể được sử dụng để đơn giản hóa và tự động hóa kiến trúc ứng dụng của bạn.

## Amazon Kinesis

Amazon Kinesis là dịch vụ streaming dữ liệu được quản lý hoàn toàn, có khả năng mở rộng, thời gian thực, giúp dễ dàng thu thập và xử lý hàng triệu bản ghi mỗi giây, làm cho nó lý tưởng cho nhiều trường hợp sử dụng, chẳng hạn như:

- Xử lý dữ liệu IoT
- Phân tích thời gian thực
- Giám sát ứng dụng
- Tổng hợp log

Kinesis bao gồm ba thành phần cốt lõi:

- **Kinesis Data Streams:** Dịch vụ này thu thập và xử lý streaming dữ liệu thời gian thực. Dữ liệu có thể được ingest vào Kinesis Data Streams từ nhiều nguồn khác nhau, chẳng hạn như thiết bị IoT, ứng dụng web và logs máy chủ.
- **Kinesis Data Firehose:** Dịch vụ này phân phối streaming dữ liệu đến data lakes và ứng dụng phân tích. Kinesis Data Firehose có thể biến đổi và buffer dữ liệu trước khi phân phối đến đích của nó, giúp dễ dàng tích hợp với nhiều hệ thống xử lý dữ liệu khác nhau.
- **Kinesis Data Analytics:** Dịch vụ này giúp dễ dàng xử lý streaming dữ liệu bằng Apache Flink và Apache Spark. Kinesis Data Analytics cung cấp nhiều thư viện và connectors tích hợp, giúp dễ dàng bắt đầu với xử lý dữ liệu thời gian thực.

Dưới đây là một số thông tin ngắn về Amazon Kinesis mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:

- **Kinesis Data Streams:** Dịch vụ streaming dữ liệu thời gian thực có khả năng mở rộng cao và bền bỉ có thể thu thập và lưu trữ liên tục gigabytes dữ liệu mỗi giây từ hàng trăm nghìn nguồn.
- **Kinesis Data Firehose:** Dịch vụ được quản lý hoàn toàn để phân phối streaming dữ liệu thời gian thực đến đích như Amazon S3, Amazon Redshift, Amazon OpenSearch Service và Splunk. Nó có thể biến đổi, buffer và nén dữ liệu trước khi phân phối.
- **Kinesis Data Analytics:** Dịch vụ được quản lý hoàn toàn giúp dễ dàng xử lý và phân tích streaming dữ liệu thời gian thực bằng Apache Flink hoặc SQL.
- **Kinesis Video Streams:** Dịch vụ được quản lý hoàn toàn giúp dễ dàng stream video an toàn từ thiết bị kết nối đến AWS để phân tích, machine learning (ML) và xử lý khác.

Dưới đây là một số chi tiết bổ sung về Amazon Kinesis mà bạn có thể muốn biết:

- Kinesis Data Streams là dịch vụ bền bỉ lưu trữ dữ liệu lên đến 365 ngày và có thể chịu được mất dữ liệu và hỏng.
- Kinesis Data Streams có khả năng mở rộng, cho phép bạn dễ dàng điều chỉnh dung lượng shard để xử lý tỷ lệ ingest dữ liệu thay đổi.
- Kinesis Data Streams an toàn, với dữ liệu được mã hóa tại nghỉ ngơi (KMS) và khi truyền (HTTPS).
- Kinesis Data Firehose là dịch vụ hiệu quả chi phí và serverless để phân phối streaming dữ liệu đến nhiều đích khác nhau.
- Kinesis Data Analytics là dịch vụ serverless đơn giản hóa xử lý dữ liệu thời gian thực với connectors và templates tích hợp.
- Kinesis Video Streams cung cấp lưu trữ an toàn, bền bỉ và chi phí hiệu quả cho streams video.

Amazon Kinesis là công cụ mạnh mẽ và linh hoạt có thể được sử dụng để xây dựng và chạy nhiều loại ứng dụng xử lý dữ liệu thời gian thực.

## Amazon GuardDuty

Amazon GuardDuty là dịch vụ phát hiện mối đe dọa sử dụng machine learning để phân tích và xác định hoạt động độc hại trong tài khoản và khối lượng công việc AWS của bạn. GuardDuty giám sát nhiều nguồn dữ liệu khác nhau, bao gồm logs AWS CloudTrail, sự kiện Amazon S3 và luồng VPC flow logs, để tìm dấu hiệu hoạt động đáng ngờ. Khi GuardDuty phát hiện mối đe dọa tiềm ẩn, nó tạo finding mà bạn có thể xem xét và điều tra.

GuardDuty có thể giúp bạn xác định nhiều loại mối đe dọa, bao gồm:

- **Truy cập trái phép:** GuardDuty có thể phát hiện truy cập trái phép vào tài nguyên AWS của bạn, chẳng hạn như logins trái phép, cuộc gọi API trái phép và truy cập dữ liệu trái phép.
- **Malware:** GuardDuty có thể phát hiện nhiễm malware trên instances và containers AWS của bạn.
- **Exfiltration dữ liệu:** GuardDuty có thể phát hiện exfiltration dữ liệu trái phép từ tài khoản AWS của bạn.
- **Cryptojacking:** GuardDuty có thể phát hiện mining cryptocurrency trái phép trên instances và containers AWS của bạn.

GuardDuty là công cụ có giá trị để cải thiện bảo mật của tài khoản và khối lượng công việc AWS của bạn. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn xác định, điều tra và phản hồi mối đe dọa.
## Amazon Inspector

Amazon Inspector là dịch vụ đánh giá bảo mật tự động giúp bạn xác định và khắc phục các lỗ hổng bảo mật tiềm ẩn trong phiên bản Amazon Elastic Compute Cloud (Amazon EC2) và container Amazon Elastic Container Service (Amazon ECS) của bạn.

Inspector sử dụng nhiều kỹ thuật đánh giá khác nhau, bao gồm phân tích mã tĩnh, phân tích động và phân tích mạng, để xác định lỗ hổng bảo mật. Inspector cũng cung cấp khuyến nghị về cách khắc phục các lỗ hổng mà nó tìm thấy.

Inspector là công cụ có giá trị để cải thiện bảo mật của khối lượng công việc AWS của bạn. Nó dễ sử dụng và có thể giúp bạn xác định và khắc phục các lỗ hổng bảo mật mà bạn có thể không biết.

**Dưới đây là một số thông tin ngắn về Amazon Inspector mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- Inspector là dịch vụ đánh giá bảo mật tự động giúp bạn xác định và khắc phục các lỗ hổng bảo mật tiềm ẩn trong phiên bản Amazon EC2 và container Amazon ECS của bạn.
- Inspector sử dụng nhiều kỹ thuật đánh giá để xác định lỗ hổng bảo mật, bao gồm quét dựa trên agent tự động cho phiên bản EC2 và quét không agent cho hình ảnh container trong ECR.
- Inspector cũng cung cấp khuyến nghị về cách khắc phục các lỗ hổng mà nó tìm thấy, ưu tiên theo mức độ nghiêm trọng.
- Inspector hỗ trợ quét liên tục môi trường của bạn.

**Dưới đây là một số chi tiết bổ sung về Amazon Inspector mà bạn có thể muốn biết:**

- Inspector là dịch vụ được quản lý, vì vậy bạn không cần quản lý bất kỳ cơ sở hạ tầng nào.
- Inspector có thể được tích hợp với AWS Systems Manager để triển khai và quản lý agent, và với Amazon EventBridge và AWS Lambda để tự động hóa phản hồi của bạn đối với các phát hiện bảo mật.
- Inspector có sẵn ở tất cả Khu vực AWS và hỗ trợ quản lý đa tài khoản thông qua AWS Organizations.
- Inspector quét các lỗ hổng phần mềm, tiếp xúc mạng không mong muốn và sai lệch khỏi các phương pháp tốt nhất về bảo mật.

Inspector là công cụ mạnh mẽ để cải thiện bảo mật của khối lượng công việc AWS của bạn. Nó dễ sử dụng và có thể giúp bạn xác định và khắc phục các lỗ hổng bảo mật mà bạn có thể không biết.

## Amazon Macie

Amazon Macie là dịch vụ bảo mật dữ liệu sử dụng machine learning để tự động khám phá, phân loại và bảo vệ dữ liệu nhạy cảm trong Amazon S3. Macie có thể giúp bạn xác định và bảo vệ nhiều loại dữ liệu nhạy cảm khác nhau, bao gồm thông tin cá nhân có thể xác định (PII), dữ liệu tài chính, tài sản trí tuệ và dữ liệu chăm sóc sức khỏe.

Macie sử dụng nhiều kỹ thuật để khám phá và phân loại dữ liệu nhạy cảm, bao gồm:

- **Machine learning:** Macie sử dụng machine learning để xác định các mẫu trong dữ liệu của bạn cho thấy dữ liệu nhạy cảm.
- **Xử lý ngôn ngữ tự nhiên:** Macie sử dụng xử lý ngôn ngữ tự nhiên để xác định dữ liệu nhạy cảm trong các trường văn bản, chẳng hạn như thông điệp email và tệp tài liệu.
- **Biểu thức chính quy:** Macie sử dụng biểu thức chính quy để xác định dữ liệu nhạy cảm ở các định dạng cụ thể, chẳng hạn như số thẻ tín dụng và số an sinh xã hội.

Sau khi Macie đã xác định và phân loại dữ liệu nhạy cảm, nó cung cấp cho bạn nhiều tính năng để giúp bạn bảo vệ nó, bao gồm:

- **Cảnh báo:** Macie có thể tạo cảnh báo khi nó phát hiện dữ liệu nhạy cảm đang được truy cập hoặc chia sẻ theo cách vi phạm chính sách bảo mật của bạn.
- **Mã hóa:** Macie có thể giúp bạn mã hóa dữ liệu nhạy cảm tại nghỉ ngơi và khi truyền.
- **Kiểm tra:** Macie có thể cung cấp cho bạn báo cáo kiểm tra về cách dữ liệu nhạy cảm của bạn đang được truy cập và chia sẻ.

Macie là công cụ có giá trị cho bất kỳ tổ chức nào đang sử dụng AWS S3 để lưu trữ dữ liệu nhạy cảm. Nó có thể giúp bạn xác định và bảo vệ dữ liệu nhạy cảm của bạn khỏi truy cập trái phép, trộm cắp và mất mát.

**Dưới đây là một số thông tin ngắn về Amazon Macie mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- Macie là dịch vụ bảo mật dữ liệu sử dụng machine learning để tự động khám phá, phân loại và bảo vệ dữ liệu nhạy cảm trong Amazon S3.
- Macie có thể giúp bạn xác định và bảo vệ nhiều loại dữ liệu nhạy cảm khác nhau, bao gồm thông tin cá nhân có thể xác định (PII), dữ liệu tài chính, tài sản trí tuệ và dữ liệu chăm sóc sức khỏe, trên các bucket S3 của bạn.
- Macie cung cấp nhiều tính năng để giúp bạn bảo vệ dữ liệu nhạy cảm của mình, bao gồm khám phá dữ liệu nhạy cảm tự động, cảnh báo và phát hiện chi tiết.
- Macie cung cấp điểm nhạy cảm dữ liệu cho các bucket S3 của bạn.

**Dưới đây là một số chi tiết bổ sung về Amazon Macie mà bạn có thể muốn biết:**

- Macie có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EventBridge và Amazon Simple Notification Service (SNS), để tự động hóa phản hồi của bạn đối với các phát hiện dữ liệu nhạy cảm.
- Macie có sẵn ở tất cả Khu vực AWS và hỗ trợ quản lý đa tài khoản thông qua AWS Organizations.
- Macie cung cấp bảng điều khiển để có chế độ xem tập trung về tư thế bảo mật dữ liệu S3 của bạn.

Macie là công cụ mạnh mẽ để cải thiện bảo mật của dữ liệu nhạy cảm của bạn trong AWS S3. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn xác định, bảo vệ và kiểm tra dữ liệu nhạy cảm của mình.

## AWS IAM Access Analyzer

AWS IAM Access Analyzer là dịch vụ giúp bạn xác định, hiểu và khắc phục các rủi ro bảo mật tiềm ẩn trong chính sách AWS Identity and Access Management (IAM) của bạn. Access Analyzer sử dụng phân tích đồ thị để phân tích chính sách IAM của bạn và xác định các rủi ro bảo mật tiềm ẩn, chẳng hạn như:

- **Quyền quá mức:** Access Analyzer có thể xác định chính sách IAM cấp cho người dùng hoặc vai trò nhiều quyền hơn họ cần.
- **Truy cập không mong muốn:** Access Analyzer có thể xác định chính sách IAM cấp cho người dùng hoặc vai trò truy cập vào tài nguyên mà họ không nên có quyền truy cập.
- **Truy cập công khai:** Access Analyzer có thể xác định chính sách IAM cấp truy cập công khai vào tài nguyên.

Access Analyzer cũng cung cấp cho bạn khuyến nghị về cách khắc phục các rủi ro bảo mật mà nó xác định.

**Dưới đây là một số thông tin ngắn về AWS IAM Access Analyzer mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- AWS IAM Access Analyzer là dịch vụ giúp bạn xác định, hiểu và khắc phục các rủi ro bảo mật tiềm ẩn trong chính sách AWS IAM của bạn.
- Access Analyzer sử dụng phân tích đồ thị để phân tích chính sách IAM của bạn và xác định các rủi ro bảo mật tiềm ẩn, chẳng hạn như quyền quá mức, truy cập không mong muốn và truy cập công khai.
- Access Analyzer cũng cung cấp cho bạn khuyến nghị về cách khắc phục các rủi ro bảo mật mà nó xác định.

**Dưới đây là một số chi tiết bổ sung về AWS IAM Access Analyzer mà bạn có thể muốn biết:**

- Access Analyzer là dịch vụ được quản lý, vì vậy bạn không cần quản lý bất kỳ cơ sở hạ tầng nào.
- Access Analyzer có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như Amazon EventBridge và Amazon Simple Notification Service (SNS), để tự động hóa phản hồi của bạn đối với các phát hiện bảo mật.
- Access Analyzer có sẵn ở tất cả Khu vực AWS và hỗ trợ phân tích đa tài khoản thông qua AWS Organizations.

**Dưới đây là một số lợi ích của việc sử dụng AWS IAM Access Analyzer:**

- **Cải thiện tư thế bảo mật:** Access Analyzer có thể giúp bạn xác định và khắc phục các rủi ro bảo mật tiềm ẩn trong chính sách IAM của bạn, điều này có thể giúp cải thiện tư thế bảo mật của môi trường AWS của bạn.
- **Giảm rủi ro tuân thủ:** Access Analyzer có thể giúp bạn tuân thủ các quy định bảo mật dữ liệu bằng cách xác định chính sách cấp truy cập không mong muốn.
- **Giảm chi phí vận hành:** Access Analyzer là dịch vụ được quản lý, vì vậy bạn không cần quản lý bất kỳ cơ sở hạ tầng hoặc phát triển bất kỳ mã tùy chỉnh nào để sử dụng nó.

Tổng thể, AWS IAM Access Analyzer là công cụ có giá trị cho bất kỳ tổ chức nào đang sử dụng AWS. Nó có thể giúp bạn cải thiện bảo mật của môi trường AWS, giảm rủi ro tuân thủ và giảm chi phí vận hành của bạn.

**Ngoài những điều trên, dưới đây là một số điều khác cần lưu ý về AWS IAM Access Analyzer:**

- Access Analyzer có thể được sử dụng để phân tích chính sách IAM cho tất cả loại thực thể IAM, bao gồm người dùng, vai trò, nhóm và dịch vụ.
- Access Analyzer có thể được sử dụng để phân tích chính sách IAM cho tất cả loại tài nguyên AWS, bao gồm bucket Amazon S3, phiên bản Amazon EC2, cơ sở dữ liệu Amazon RDS và khóa KMS.
- Access Analyzer có thể được sử dụng để phân tích chính sách IAM cho cả thực thể và tài nguyên IAM mới và hiện có.
- Access Analyzer cung cấp phát hiện làm nổi bật tài nguyên có thể truy cập từ bên ngoài tài khoản AWS của bạn.

AWS IAM Access Analyzer là công cụ mạnh mẽ để cải thiện bảo mật của môi trường AWS của bạn. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn xác định, hiểu và khắc phục các rủi ro bảo mật tiềm ẩn trong chính sách IAM của bạn.

## AWS CodePipeline

AWS CodePipeline là dịch vụ phân phối liên tục giúp bạn tự động hóa quy trình phát hành và triển khai cho ứng dụng của bạn. CodePipeline xây dựng, kiểm tra và triển khai mã của bạn mỗi khi có thay đổi, để bạn có thể phát hành các tính năng mới thường xuyên và đáng tin cậy hơn.

CodePipeline hoạt động bằng cách mô hình hóa và tự động hóa các bước cần thiết để phát hành phần mềm của bạn. Bạn có thể tạo pipeline bao gồm các giai đoạn sau:

- **Giai đoạn nguồn:** Giai đoạn nguồn truy xuất mã từ kho mã nguồn của bạn, chẳng hạn như AWS CodeCommit, GitHub, Bitbucket hoặc Amazon S3.
- **Giai đoạn xây dựng:** Giai đoạn xây dựng biên dịch, đóng gói và kiểm tra mã của bạn bằng các dịch vụ như AWS CodeBuild.
- **Giai đoạn kiểm tra:** (Tùy chọn) Giai đoạn kiểm tra chạy các kiểm tra bổ sung trên mã của bạn.
- **Giai đoạn triển khai:** Giai đoạn triển khai triển khai mã của bạn đến môi trường sản xuất bằng các dịch vụ như AWS CodeDeploy, AWS Elastic Beanstalk hoặc AWS CloudFormation.

CodePipeline có thể được tích hợp với nhiều dịch vụ AWS khác nhau, chẳng hạn như Amazon S3, Amazon Elastic Container Registry (ECR), AWS Lambda và AWS CloudFormation. Điều này cho phép bạn sử dụng CodePipeline để tự động hóa quy trình phát hành và triển khai cho nhiều loại ứng dụng khác nhau.

**Dưới đây là một số thông tin ngắn về AWS CodePipeline mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- AWS CodePipeline là dịch vụ phân phối liên tục giúp bạn tự động hóa quy trình phát hành và triển khai cho ứng dụng của bạn.
- CodePipeline hoạt động bằng cách mô hình hóa và tự động hóa các bước cần thiết để phát hành phần mềm của bạn, chẳng hạn như truy xuất mã từ kho mã nguồn của bạn, biên dịch, đóng gói và kiểm tra mã của bạn, và triển khai mã của bạn đến môi trường sản xuất của bạn.
- CodePipeline có thể được tích hợp với nhiều dịch vụ AWS khác nhau, chẳng hạn như Amazon S3, Amazon ECR, AWS Lambda, AWS CloudFormation và AWS CodeStar.

**Dưới đây là một số chi tiết bổ sung về AWS CodePipeline mà bạn có thể muốn biết:**

- CodePipeline là dịch vụ được quản lý, vì vậy bạn không cần quản lý bất kỳ cơ sở hạ tầng cơ bản nào.
- CodePipeline hỗ trợ nhiều mục tiêu triển khai khác nhau, bao gồm phiên bản Amazon EC2, cụm Amazon ECS, hàm AWS Lambda và máy chủ on-premises.
- CodePipeline cung cấp nhiều tính năng để giúp bạn giám sát và quản lý pipeline của mình, chẳng hạn như cập nhật trạng thái thời gian thực, cảnh báo (qua SNS) và nhật ký kiểm tra (qua CloudTrail).
- CodePipeline hỗ trợ phê duyệt thủ công ở bất kỳ giai đoạn nào của pipeline.

**Dưới đây là một số lợi ích của việc sử dụng AWS CodePipeline:**

- **Tăng tần suất phát hành:** CodePipeline có thể giúp bạn phát hành các tính năng mới thường xuyên hơn bằng cách tự động hóa quy trình phát hành và triển khai.
- **Cải thiện độ tin cậy:** CodePipeline có thể giúp bạn cải thiện độ tin cậy của các bản phát hành bằng cách tự động hóa quy trình xây dựng, kiểm tra và triển khai, giảm lỗi của con người.
- **Giảm rủi ro:** CodePipeline có thể giúp bạn giảm rủi ro phát hành mã lỗi bằng cách tự động hóa quy trình kiểm tra và cho phép rollback nhanh.
- **Cải thiện khả năng hiển thị:** CodePipeline cung cấp nhiều tính năng để giúp bạn giám sát và quản lý pipeline của mình, điều này có thể giúp bạn xác định và giải quyết vấn đề nhanh chóng.

Tổng thể, AWS CodePipeline là công cụ có giá trị cho bất kỳ tổ chức nào đang phát triển và triển khai phần mềm. Nó có thể giúp bạn tăng tần suất phát hành, cải thiện độ tin cậy của các bản phát hành, giảm rủi ro phát hành mã lỗi và cải thiện khả năng hiển thị của quy trình phát hành của bạn.

**Ngoài những điều trên, dưới đây là một số điều khác cần lưu ý về AWS CodePipeline:**

- CodePipeline có thể được sử dụng để tự động hóa quy trình phát hành và triển khai cho ứng dụng có tất cả kích thước, từ trang web nhỏ đến ứng dụng doanh nghiệp lớn.
- CodePipeline có thể được sử dụng để tự động hóa quy trình phát hành và triển khai cho ứng dụng được phát triển bằng nhiều ngôn ngữ lập trình và framework khác nhau.
- CodePipeline có thể được sử dụng để tự động hóa quy trình phát hành và triển khai cho ứng dụng được triển khai đến nhiều môi trường khác nhau, bao gồm môi trường on-premises, đám mây và hybrid.
- CodePipeline hỗ trợ mẫu pipeline để thiết lập nhanh.

AWS CodePipeline là công cụ mạnh mẽ để tự động hóa quy trình phát hành và triển khai cho ứng dụng của bạn. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn cải thiện tần suất, độ tin cậy và rủi ro của các bản phát hành của bạn.

## AWS CodeBuild

AWS CodeBuild là dịch vụ tích hợp liên tục được quản lý hoàn toàn tự động hóa việc xây dựng, kiểm tra và đóng gói phần mềm của bạn. Nó mở rộng quy mô theo nhu cầu của bạn và giúp bạn phát hành phần mềm chất lượng cao nhanh hơn và đáng tin cậy hơn.

CodeBuild hoạt động bằng cách xây dựng mã của bạn trong môi trường container Docker, thực thi các lệnh xây dựng mà bạn chỉ định trong tệp buildspec của mình. Tệp buildspec là tệp YAML định nghĩa các bước mà CodeBuild nên thực hiện để xây dựng và kiểm tra mã của bạn.

CodeBuild có thể được tích hợp với nhiều dịch vụ AWS khác nhau, chẳng hạn như Amazon S3, Amazon Elastic Container Registry (ECR) và AWS CodePipeline. Điều này cho phép bạn tự động hóa quy trình xây dựng, kiểm tra và triển khai cho ứng dụng của bạn.

**Dưới đây là một số thông tin ngắn về AWS CodeBuild mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- AWS CodeBuild là dịch vụ tích hợp liên tục được quản lý hoàn toàn tự động hóa việc xây dựng, kiểm tra và đóng gói phần mềm của bạn.
- CodeBuild mở rộng quy mô theo nhu cầu của bạn và giúp bạn phát hành phần mềm chất lượng cao nhanh hơn và đáng tin cậy hơn.
- CodeBuild hoạt động bằng cách xây dựng mã của bạn trong môi trường container Docker và thực thi các lệnh xây dựng được chỉ định trong tệp buildspec của bạn.
- CodeBuild có thể được tích hợp với nhiều dịch vụ AWS khác nhau, chẳng hạn như Amazon S3, Amazon ECR và AWS CodePipeline.

**Dưới đây là một số chi tiết bổ sung về AWS CodeBuild mà bạn có thể muốn biết:**

- CodeBuild hỗ trợ nhiều môi trường xây dựng khác nhau, bao gồm hình ảnh Docker cho các ngôn ngữ lập trình phổ biến (ví dụ: Java, Python, Node.js, .NET, Go, Ruby) và hình ảnh Docker tùy chỉnh.
- CodeBuild cung cấp nhiều tính năng để giúp bạn giám sát và quản lý các bản xây dựng của mình, chẳng hạn như cập nhật trạng thái thời gian thực, nhật ký xây dựng chi tiết (CloudWatch Logs) và thông báo xây dựng (SNS).
- CodeBuild có thể được sử dụng để xây dựng và kiểm tra mã cho ứng dụng có tất cả kích thước, từ trang web nhỏ đến ứng dụng doanh nghiệp lớn.
- CodeBuild hỗ trợ lưu trữ cache artifact xây dựng trong S3 để tăng tốc các bản xây dựng tiếp theo.
- CodeBuild hỗ trợ tùy chỉnh môi trường xây dựng với hình ảnh Docker, bao gồm việc sử dụng hình ảnh được quản lý và tùy chỉnh.

**Dưới đây là một số lợi ích của việc sử dụng AWS CodeBuild:**

- **Tăng tần suất xây dựng:** CodeBuild có thể giúp bạn phát hành các tính năng mới thường xuyên hơn bằng cách tự động hóa quy trình xây dựng và kiểm tra.
- **Cải thiện độ tin cậy:** CodeBuild có thể giúp bạn cải thiện độ tin cậy của các bản phát hành bằng cách cung cấp môi trường xây dựng nhất quán và tự động hóa quy trình kiểm tra.
- **Giảm rủi ro:** CodeBuild có thể giúp bạn giảm rủi ro phát hành mã lỗi bằng cách tự động hóa quy trình kiểm tra và cung cấp báo cáo xây dựng chi tiết.
- **Cải thiện khả năng hiển thị:** CodeBuild cung cấp nhiều tính năng để giúp bạn giám sát và quản lý các bản xây dựng của mình, điều này có thể giúp bạn xác định và giải quyết vấn đề nhanh chóng.

Tổng thể, AWS CodeBuild là công cụ có giá trị cho bất kỳ tổ chức nào đang phát triển và triển khai phần mềm. Nó có thể giúp bạn tăng tần suất xây dựng, cải thiện độ tin cậy của các bản xây dựng, giảm rủi ro phát hành mã lỗi và cải thiện khả năng hiển thị của quy trình xây dựng của bạn.

**Ngoài những điều trên, dưới đây là một số điều khác cần lưu ý về AWS CodeBuild:**

- CodeBuild có thể được sử dụng để xây dựng và kiểm tra mã cho ứng dụng được phát triển bằng nhiều ngôn ngữ lập trình và framework khác nhau.
- CodeBuild có thể được sử dụng để xây dựng và kiểm tra mã cho ứng dụng được triển khai đến nhiều môi trường khác nhau, bao gồm môi trường on-premises, đám mây và hybrid.
- CodeBuild có thể được tích hợp với nhiều công cụ CI/CD khác nhau, chẳng hạn như AWS CodePipeline, Jenkins và CircleCI.
- CodeBuild hỗ trợ chạy bản xây dựng trong VPC để truy cập mạng riêng.

AWS CodeBuild là công cụ mạnh mẽ và linh hoạt để tự động hóa quy trình xây dựng và kiểm tra cho ứng dụng của bạn. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn cải thiện tần suất, độ tin cậy và rủi ro của các bản xây dựng của bạn.

## AWS CodeDeploy

AWS CodeDeploy là dịch vụ triển khai giúp bạn tự động hóa việc triển khai ứng dụng đến phiên bản Amazon Elastic Compute Cloud (Amazon EC2), phiên bản on-premises, ứng dụng serverless (AWS Lambda) và dịch vụ container Amazon ECS/EKS. CodeDeploy giúp dễ dàng triển khai mã và thay đổi cơ sở hạ tầng đến ứng dụng của bạn một cách đáng tin cậy.

CodeDeploy hoạt động bằng cách triển khai mã ứng dụng của bạn đến một tập hợp các phiên bản hoặc hàm serverless. CodeDeploy sau đó định tuyến lưu lượng truy cập đến các triển khai mới và giám sát việc triển khai để đảm bảo nó thành công, với tùy chọn rollback tự động.

CodeDeploy có thể được tích hợp với nhiều dịch vụ AWS khác nhau, chẳng hạn như Amazon S3, AWS CloudFormation và AWS CodePipeline. Điều này cho phép bạn tự động hóa quy trình triển khai cho ứng dụng của bạn.

**Dưới đây là một số thông tin ngắn về AWS CodeDeploy mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- AWS CodeDeploy là dịch vụ triển khai giúp bạn tự động hóa việc triển khai ứng dụng đến phiên bản Amazon EC2, phiên bản on-premises, ứng dụng serverless (AWS Lambda) và Amazon ECS/EKS.
- CodeDeploy giúp dễ dàng triển khai mã và thay đổi cơ sở hạ tầng đến ứng dụng của bạn một cách đáng tin cậy.
- CodeDeploy hoạt động bằng cách triển khai mã ứng dụng của bạn đến một tập hợp các phiên bản hoặc hàm, định tuyến lưu lượng truy cập và giám sát việc triển khai để thành công.
- CodeDeploy có thể được tích hợp với nhiều dịch vụ AWS khác nhau, chẳng hạn như Amazon S3, AWS CloudFormation và AWS CodePipeline.

**Dưới đây là một số chi tiết bổ sung về AWS CodeDeploy mà bạn có thể muốn biết:**

- CodeDeploy hỗ trợ nhiều chiến lược triển khai khác nhau, chẳng hạn như triển khai tại chỗ, triển khai xanh/xanh dương (cho EC2/On-Premises và ECS), và triển khai tuyến tính/canary (cho Lambda).
- CodeDeploy cung cấp nhiều tính năng để giúp bạn giám sát và quản lý các triển khai của mình, chẳng hạn như cập nhật trạng thái thời gian thực, sự kiện triển khai (CloudWatch Events) và nhật ký kiểm tra (CloudTrail).
- CodeDeploy có thể được sử dụng để triển khai ứng dụng có tất cả kích thước, từ trang web nhỏ đến ứng dụng doanh nghiệp lớn.
- CodeDeploy hỗ trợ rollback tự động khi triển khai thất bại.
- CodeDeploy hỗ trợ nhiều chiến lược triển khai, bao gồm tại chỗ, xanh/xanh dương và canary.

**Dưới đây là một số lợi ích của việc sử dụng AWS CodeDeploy:**

- **Giảm rủi ro:** CodeDeploy có thể giúp bạn giảm rủi ro của các triển khai bằng cách tự động hóa quy trình triển khai, cung cấp nhiều chiến lược triển khai và cho phép rollback tự động.
- **Cải thiện độ tin cậy:** CodeDeploy có thể giúp bạn cải thiện độ tin cậy của các triển khai bằng cách đảm bảo triển khai nhất quán và giảm thiểu thời gian ngừng hoạt động.
- **Tăng hiệu quả:** CodeDeploy có thể giúp bạn tăng hiệu quả của các triển khai bằng cách tự động hóa quy trình triển khai và cung cấp giám sát chi tiết.

Tổng thể, AWS CodeDeploy là công cụ có giá trị cho bất kỳ tổ chức nào đang phát triển và triển khai phần mềm. Nó có thể giúp bạn giảm rủi ro, cải thiện độ tin cậy và tăng hiệu quả của các triển khai của bạn.

**Ngoài những điều trên, dưới đây là một số điều khác cần lưu ý về AWS CodeDeploy:**

- CodeDeploy có thể được sử dụng để triển khai ứng dụng được phát triển bằng nhiều ngôn ngữ lập trình và framework khác nhau.
- CodeDeploy có thể được sử dụng để triển khai ứng dụng được triển khai đến nhiều môi trường khác nhau, bao gồm môi trường on-premises, đám mây và hybrid.
- CodeDeploy có thể được tích hợp với nhiều công cụ DevOps khác nhau, chẳng hạn như AWS CodePipeline, Jenkins và CircleCI.
- CodeDeploy sử dụng tệp AppSpec để quản lý cấu hình triển khai.

AWS CodeDeploy là công cụ mạnh mẽ và linh hoạt để tự động hóa quy trình triển khai cho ứng dụng của bạn. Nó dễ sử dụng và cung cấp nhiều tính năng để giúp bạn giảm rủi ro, cải thiện độ tin cậy và tăng hiệu quả của các triển khai của bạn.

## AWS CodeCommit

AWS CodeCommit là dịch vụ kiểm soát nguồn được quản lý hoàn toàn, có khả năng mở rộng cao, an toàn lưu trữ kho Git riêng. CodeCommit giúp dễ dàng cho các nhóm hợp tác phát triển mã và theo dõi thay đổi theo thời gian.

CodeCommit là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần cung cấp hoặc quản lý bất kỳ máy chủ nào. CodeCommit cũng cung cấp nhiều tính năng bảo mật để giúp bạn bảo vệ mã của mình, chẳng hạn như mã hóa tại nghỉ ngơi và khi truyền, và tích hợp với AWS IAM để kiểm soát truy cập.

CodeCommit có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như AWS CodePipeline, AWS CodeDeploy và AWS CodeBuild. Điều này cho phép bạn tự động hóa quy trình phát triển và triển khai phần mềm của mình.

**Dưới đây là một số thông tin ngắn về AWS CodeCommit mà bạn cần biết để vượt qua kỳ thi AWS Certified Solutions Architect Associate:**

- AWS CodeCommit là dịch vụ kiểm soát nguồn được quản lý hoàn toàn, có khả năng mở rộng cao, an toàn lưu trữ kho Git riêng.
- CodeCommit giúp dễ dàng cho các nhóm hợp tác phát triển mã và theo dõi thay đổi theo thời gian.
- CodeCommit là dịch vụ được quản lý hoàn toàn, vì vậy bạn không cần cung cấp hoặc quản lý bất kỳ máy chủ nào.
- CodeCommit cung cấp nhiều tính năng bảo mật để giúp bạn bảo vệ mã của mình, bao gồm mã hóa tại nghỉ ngơi và khi truyền.
- CodeCommit có thể được tích hợp với nhiều dịch vụ AWS khác, chẳng hạn như AWS CodePipeline, AWS CodeDeploy và AWS CodeBuild.

**Dưới đây là một số chi tiết bổ sung về AWS CodeCommit mà bạn có thể muốn biết:**

- CodeCommit hỗ trợ tất cả các tính năng Git tiêu chuẩn, chẳng hạn như nhánh, commit, pull request và merge.
- CodeCommit cung cấp nhiều tính năng để giúp bạn quản lý kho của mình, chẳng hạn như chính sách nhánh, quy trình xem xét mã và thông báo.
- CodeCommit có thể được truy cập bằng nhiều công cụ khác nhau, chẳng hạn như bảng điều khiển AWS CodeCommit, Git CLI và bất kỳ client Git nào.
- CodeCommit tích hợp với AWS IAM để kiểm soát truy cập chi tiết đến kho và nhánh.
- CodeCommit hỗ trợ pull request và quy trình xem xét mã.

**Dưới đây là một số lợi ích của việc sử dụng AWS CodeCommit:**

- **Bảo mật:** CodeCommit cung cấp nhiều tính năng bảo mật để giúp bạn bảo vệ mã của mình, chẳng hạn như mã hóa tại nghỉ ngơi và khi truyền, và kiểm soát truy cập chi tiết thông qua IAM.
- **Khả năng mở rộng:** CodeCommit là dịch vụ có khả năng mở rộng cao có thể xử lý kho có bất kỳ kích thước nào, từ dự án nhỏ đến ứng dụng doanh nghiệp lớn.
- **Độ tin cậy:** CodeCommit là dịch vụ đáng tin cậy có sẵn 24/7, với dữ liệu được nhân bản trên nhiều Availability Zone.
- **Dễ sử dụng:** CodeCommit là dịch vụ dễ sử dụng cung cấp trải nghiệm Git quen thuộc và tích hợp liền mạch với các dịch vụ AWS khác.

Tổng thể, AWS CodeCommit là công cụ có giá trị cho bất kỳ tổ chức nào đang phát triển và triển khai phần mềm. Nó cung cấp cách an toàn, có khả năng mở rộng và đáng tin cậy để lưu trữ kho Git riêng của bạn.

**Ngoài những điều trên, dưới đây là một số điều khác cần lưu ý về AWS CodeCommit:**

- CodeCommit có thể được sử dụng để lưu trữ kho cho ứng dụng có tất cả kích thước, từ trang web nhỏ đến ứng dụng doanh nghiệp lớn.
- CodeCommit có thể được sử dụng để lưu trữ kho cho ứng dụng được phát triển bằng nhiều ngôn ngữ lập trình và framework khác nhau.
- CodeCommit có thể được sử dụng để lưu trữ kho cho ứng dụng được triển khai đến nhiều môi trường khác nhau, bao gồm môi trường on-premises, đám mây và hybrid.
- CodeCommit hỗ trợ trigger kho để hành động tự động trên thay đổi mã.

## Đóng góp

Chúng tôi hoan nghênh đóng góp từ cộng đồng. Nếu bạn có ý tưởng, báo cáo lỗi hoặc yêu cầu tính năng, vui lòng mở vấn đề hoặc gửi pull request.

## Giấy phép

Dự án này được cấp phép theo Giấy phép MIT.