---
title: "Week 8 Worklog"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 8 Objectives
  - Tasks to be carried out this week
  - Week 8 Achievements
reportType: worklog
---
### Week 8 Objectives:

* Perform comprehensive E2E testing on the production domain.
* Conduct security audit and review access controls.
* Finalize project documentation.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Execute E2E test on live domain: Register -> Email Verification -> Deposit -> Transfer -> Service Payment -> History -> Admin | 26/07 | 28/07 |
| 2   | Test account lock mechanism: verify frontend clears session on `401` or `ACCOUNT_BLOCKED` response | 27/07 | 27/07 |
| 3   | Security review: confirm SSH port 22 restricted to admin IP `/32`, all unnecessary ports closed | 28/07 | 28/07 |
| 4   | Update `README.md`, `description.md`, and `PROJECT_STATUS.md` with deployment status and test results | 28/07 | 28/07 |
| 5   | Document upgrade roadmap (ASG, ECR, CI/CD, Lambda cleanup) | 29/07 | 29/07 |

### Week 8 Achievements:

* Successfully delivered a stable, secure, and standardized Simulated E-Wallet product on AWS infrastructure.
* Mastered system security assessment, E2E testing, and professional technical documentation practices.