---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

This section presents the Cloud E-Wallet deployment architecture on AWS and the deployment process we completed as a team. The content follows the dependencies among the database, backend, frontend, routing, security, and validation so that readers can trace the complete deployment flow from infrastructure to application.

![Cloud E-Wallet deployment architecture on AWS](/images/5-Workshop/5.1-Prerequisites/architecture.png)

<p style="text-align: center;"><em>Figure 5.1. Cloud E-Wallet deployment architecture on AWS.</em></p>

In this architecture, users send HTTPS requests to a CloudFront distribution that we protected with AWS WAF. We used the default behavior to serve the React frontend from Amazon S3, while we routed `/api/*` through the internet-facing ALB and Target Group to two EC2 instances in private subnets across two Availability Zones. We managed these instances with an Auto Scaling Group configured as `Min 0 / Desired 2 / Max 2`. The backend connects to a Single-AZ RDS MySQL over the private network and uses Amazon SES for email delivery. CloudWatch provides monitoring, KMS supports encryption-key management, and we deployed one NAT Gateway in a public subnet to provide outbound Internet access for the private EC2 instances. Cloudflare manages only DNS and the AWS/SES verification records.

We built Cloud E-Wallet with simulated balances only; it does not process real money, does not connect to a payment gateway, and does not send card data to the backend.

## Procedure

| Step | Main work | Expected outcome |
| --- | --- | --- |
| [5.1. Prepare the environment](5.1-Prerequisites/) | We verified the tools and source, identified the two IAM users, and configured the frontend, backend, RDS, JWT, CORS, and Amazon SES | Deployment environment is ready in the correct Region with no exposed secrets |
| [5.2. Deploy the database](5.2-Database-deployment/) | We configured a private RDS, then initialized the schema and baseline data | The production database is ready for the backend |
| [5.3. Deploy the backend](5.3-Backend-deployment/) | We prepared EC2/Docker/SES, built the image, and released the Spring Boot container | The backend connects to RDS, sends email, and serves traffic through the ALB |
| [5.4. Deploy the frontend](5.4-Frontend-deployment/) | We configured S3/CloudFront, built the React frontend, and released the static files | The frontend is delivered over HTTPS through CloudFront or the custom domain |
| [5.5. Configure routing and security](5.5-Traffic-security/) | We configured WAF, the target group, ALB, ASG, CloudFront `/api/*`, Cloudflare DNS, and security groups | Traffic follows CloudFront/WAF → ALB → Target Group → EC2 without unnecessary direct exposure of EC2 or RDS |
| [5.6. Validate the deployment](5.6-Validation/) | We confirmed backend health, sign-in, wallet information, money transfer, and password-reset email through Amazon SES | Primary production workflows operate end to end |
| [5.7. Clean up resources](5.7-Cleanup/) | We backed up the required data, verified dependencies, and stopped or deleted unused resources | Post-demo charges are reduced |
