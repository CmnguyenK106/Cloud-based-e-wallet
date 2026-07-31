---
title: "Week 2 Worklog"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 2 Objectives
  - Tasks to be carried out this week
  - Week 2 Achievements
reportType: worklog
---
### Week 2 Objectives:

* Complete all business logic for the E-Wallet backend (deposit, transfer, payment).
* Finalize the frontend with all required pages and Zod validation.
* Research and decide on the target AWS cloud architecture.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Implement safe financial transactions with `@Transactional` (deposit, transfer with recipient name lookup, virtual service payment) | 15/06 | 16/06 |
| 2   | Organize backend routes: `/api/auth/**`, `/api/user/**`, `/api/admin/**` | 16/06 | 18/06 |
| 3   | Integrate Zod validation on all frontend forms | 18/06 | 19/06 |
| 4   | Build Dashboard, Deposit/Transfer pages, Transaction History, and Admin Dashboard | 18/06 | 20/06 |
| 5   | Run local integration tests and testing | 20/06 | 20/06 |
| 6   | Analyze deployment options and finalize Hybrid Cloud architecture | 17/06 | 20/06 |
| 7   | Design architecture diagram: S3 + CloudFront for frontend, EC2 for backend, RDS for database, SES for email | 19/06 | 20/06 |

### Week 2 Achievements:

* E-Wallet application fully operational in local environment (Frontend `:5173`, Backend `:8080`, MySQL `:3307`).
* All backend unit tests passed successfully.
* Determined target Cloud architecture and list of AWS services needed.