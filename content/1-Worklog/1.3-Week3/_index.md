---
title: "Week 3 Worklog"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 1.3. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 3 Objectives
  - Tasks to be carried out this week
  - Week 3 Achievements
reportType: worklog
---
### Week 3 Objectives:

* Create a custom VPC with multi-AZ architecture.
* Configure Security Groups with least-privilege rules.
* Deploy Amazon RDS for MySQL in a private subnet.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Create custom VPC `ewallet-vpc` (CIDR `10.0.0.0/16`) in `ap-southeast-1` | 22/06 | 22/06 |
| 2   | Create 2 Public Subnets (for ALB) and 2 Private Subnets (for EC2 & RDS) across 2 AZs | 22/06 | 22/06 |
| 3   | Create Internet Gateway (IGW) and configure Route Table for Public Subnets | 23/06 | 23/06 |
| 4   | Configure Security Groups: `alb-sg` (HTTP 80), `ec2-backend-sg` (port 8080 from ALB, SSH 22 from admin IP), `rds-sg` (port 3306 from backend only) | 24/06 | 24/06 |
| 5   | Launch Amazon RDS for MySQL 8 in Private Subnet Group (Publicly Accessible = No) | 25/06 | 25/06 |
| 6   | Execute SQL scripts: `001_schema.sql`, `002_admin_template.sql`, `003_services_seed.sql` on RDS | 25/06 | 25/06 |

### Week 3 Achievements:

* VPC network infrastructure and managed RDS database operational in private subnet.
* Practical understanding of AWS Networking (Subnets, Route Tables, IGW) and least-privilege Security Groups.