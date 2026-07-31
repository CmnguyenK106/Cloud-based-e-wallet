---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
includeInReport: true
reportTableColumns:
  - Day
  - Task
  - Completion Date
reportHeadings:
  - Week 6 Objectives
  - Tasks to be carried out this week
  - Week 6 Achievements
reportType: worklog
---
### Week 6 Objectives:

* Deploy the React frontend to S3 and serve via CloudFront CDN.
* Configure CloudFront with dual origins (S3 for static files, ALB for API).
* Set up custom domain with Cloudflare DNS and SSL.

### Tasks to be carried out this week:
| Day | Task | Start Date | Completion Date |
| --- | ---- | ---------- | --------------- |
| 1   | Build React 19 production bundle (`npm run build`) and upload to S3 Bucket | 10/07 | 10/07 |
| 2   | Create CloudFront Distribution: Origin 1 (S3 via OAC) for static files, Origin 2 (ALB) for API | 11/07 | 11/07 |
| 3   | Configure Behaviors: Default (`*`) to S3, `/api/*` to ALB with full HTTP Methods & Headers | 12/07 | 12/07 |
| 4   | Configure CNAME record on Cloudflare DNS pointing `cloud-ewallet.com` to CloudFront Distribution | 13/07 | 13/07 |
| 5   | Test full HTTPS access to the application | 13/07 | 14/07 |

### Week 6 Achievements:

* Full application accessible via HTTPS at `https://cloud-ewallet.com`.
* Resolved CORS issues by serving frontend and API through the same CloudFront distribution.