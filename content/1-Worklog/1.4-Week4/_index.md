---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 4 Objectives
  - Tasks to be carried out this week
  - Week 4 Achievements
reportType: worklog
---
### Week 4 Objectives:

* Containerize the Spring Boot backend with a multi-stage Dockerfile.
* Launch an EC2 instance and deploy the Dockerized backend.
* Configure production environment variables securely.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Write multi-stage `Dockerfile` for Maven Spring Boot 17 project | 26/06 | 26/06 |
| 2   | Launch EC2 instance in Public Subnet, install Docker Engine | 27/06 | 27/06 |
| 3   | Create `/home/ec2-user/ewallet-backend.env` for RDS connection, JWT_SECRET, and production config | 28/06 | 28/06 |
| 4   | Run `docker run` to start `ewallet-backend` container on port `8080:8080` | 29/06 | 29/06 |
| 5   | Verify backend container connects to RDS successfully | 29/06 | 29/06 |

### Week 4 Achievements:

* Backend container running stably on EC2, successfully querying data from RDS MySQL.
* Learned Docker packaging skills and secure environment variable management on cloud servers.