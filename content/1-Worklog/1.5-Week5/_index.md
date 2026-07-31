---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 5 Objectives
  - Tasks to be carried out this week
  - Week 5 Achievements
reportType: worklog
---
### Week 5 Objectives:

* Create a Target Group and configure health checks with Spring Boot Actuator.
* Set up an Internet-facing Application Load Balancer (ALB).
* Harden network security by restricting direct EC2 access.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Create Target Group `ewallet-backend-tg` (Port 8080, HTTP) and register EC2 instance | 03/07 | 03/07 |
| 2   | Configure Health Check path to `/actuator/health` | 03/07 | 03/07 |
| 3   | Create Internet-facing ALB, attach `alb-sg`, route HTTP port 80 to Target Group | 04/07 | 04/07 |
| 4   | Close ports 80 and 443 on EC2, verify port 8080 is blocked from direct public IP access | 04/07 | 04/07 |

### Week 5 Achievements:

* ALB health check shows Target as *Healthy*, serving as the single entry point for all API traffic.
* Mastered load balancing, health monitoring via Spring Actuator, and hiding compute instances behind the Load Balancer.