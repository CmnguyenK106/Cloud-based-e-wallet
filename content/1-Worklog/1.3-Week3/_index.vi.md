---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 3:

* Tạo VPC tùy chỉnh với kiến trúc đa Availability Zone.
* Cấu hình Security Groups theo nguyên tắc phân quyền tối thiểu.
* Triển khai Amazon RDS for MySQL trong Private Subnet.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Tạo VPC `ewallet-vpc` (CIDR `10.0.0.0/16`) tại `ap-southeast-1` | 22/06 | 22/06 |
| 2   | Tạo 2 Public Subnets (cho ALB) và 2 Private Subnets (cho EC2 & RDS) trên 2 AZs | 22/06 | 22/06 |
| 3   | Tạo Internet Gateway (IGW) và cấu hình Route Table cho Public Subnets | 23/06 | 23/06 |
| 4   | Cấu hình Security Groups: `alb-sg` (HTTP 80), `ec2-backend-sg` (cổng 8080 từ ALB, SSH 22 từ admin IP), `rds-sg` (cổng 3306 chỉ từ backend) | 24/06 | 24/06 |
| 5   | Khởi tạo Amazon RDS for MySQL 8 trong Private Subnet Group (Publicly Accessible = No) | 25/06 | 25/06 |
| 6   | Thực thi SQL scripts: `001_schema.sql`, `002_admin_template.sql`, `003_services_seed.sql` trên RDS | 25/06 | 25/06 |

### Kết quả đạt được:

* Hạ tầng VPC và RDS hoạt động an toàn trong Private Subnet.
* Hiểu sâu về AWS Networking và quy tắc phân quyền tối thiểu qua Security Groups.