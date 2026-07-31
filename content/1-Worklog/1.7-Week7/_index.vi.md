---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 1.7. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 7:

* Cấu hình Amazon SES để gửi email (xác thực domain và email identity).
* Tích hợp SMTP credentials vào Backend cho email xác thực.
* Kiểm thử tất cả luồng email: xác thực đăng ký, gửi lại mã, quên/đặt lại mật khẩu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Xác thực domain `cloud-ewallet.com` và email `noreply@cloud-ewallet.com` trên Amazon SES | 17/07 | 17/07 |
| 2   | Tạo SMTP Credentials (cổng 587, STARTTLS) | 18/07 | 18/07 |
| 3   | Cập nhật cấu hình SES SMTP vào `/home/ec2-user/ewallet-backend.env` trên EC2 | 18/07 | 18/07 |
| 4   | Kiểm thử luồng email xác thực đăng ký | 19/07 | 19/07 |
| 5   | Kiểm thử luồng gửi lại mã xác nhận | 20/07 | 20/07 |
| 6   | Kiểm thử luồng quên/đặt lại mật khẩu (token hash lưu trong `account_tokens`) | 21/07 | 21/07 |

### Kết quả đạt được:

* Hoàn thiện luồng xác thực và khôi phục tài khoản tự động qua email trên Production.
* Hiểu rõ cơ chế quản lý token, mã hóa SHA-256 và tích hợp dịch vụ Email SMTP Cloud.