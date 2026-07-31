---
title: "Worklog Tuần 8"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 1.8. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 8:

* Thực hiện kiểm thử E2E toàn diện trên tên miền production.
* Tiến hành audit bảo mật và rà soát kiểm soát truy cập.
* Hoàn thiện tài liệu dự án.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Thực hiện E2E test trên domain thật: Đăng ký -> Xác thực Mail -> Nạp tiền -> Chuyển tiền -> Thanh toán -> Lịch sử -> Admin | 26/07 | 28/07 |
| 2   | Kiểm tra cơ chế khoá tài khoản: xác nhận frontend xoá session khi nhận `401` hoặc `ACCOUNT_BLOCKED` | 27/07 | 27/07 |
| 3   | Rà soát an ninh: xác nhận SSH port 22 giới hạn IP admin `/32`, các cổng không cần thiết đã đóng | 28/07 | 28/07 |
| 4   | Cập nhật `README.md`, `description.md`, `PROJECT_STATUS.md` với trạng thái triển khai và kết quả test | 28/07 | 28/07 |
| 5   | Ghi nhận lộ trình nâng cấp (ASG, ECR, CI/CD, Lambda cleanup) | 29/07 | 29/07 |

### Kết quả đạt được:

* Bàn giao thành công sản phẩm E-Wallet vận hành ổn định, an toàn trên AWS.
* Nắm vững quy trình đánh giá an ninh, kiểm thử E2E và lập tài liệu kỹ thuật chuyên nghiệp.