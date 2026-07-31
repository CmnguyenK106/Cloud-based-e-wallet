---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 7 Objectives
  - Tasks to be carried out this week
  - Week 7 Achievements
reportType: worklog
---
### Week 7 Objectives:

* Configure Amazon SES for email sending (verify domain and email identity).
* Integrate SMTP credentials into the backend for authentication emails.
* Test all email flows: registration verification, resend code, forgot/reset password.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Verify domain `cloud-ewallet.com` and email `noreply@cloud-ewallet.com` on Amazon SES | 17/07 | 17/07 |
| 2   | Generate SMTP Credentials (port 587, STARTTLS) | 18/07 | 18/07 |
| 3   | Update SES SMTP config in `/home/ec2-user/ewallet-backend.env` on EC2 | 18/07 | 18/07 |
| 4   | Test registration verification email flow | 19/07 | 19/07 |
| 5   | Test resend confirmation code flow | 20/07 | 20/07 |
| 6   | Test forgot/reset password flow (token hash stored in `account_tokens`) | 21/07 | 21/07 |

### Week 7 Achievements:

* Completed automatic email authentication and account recovery flow on the production environment.
* Understood token lifecycle management, SHA-256 token hash encryption, and SMTP cloud service integration.