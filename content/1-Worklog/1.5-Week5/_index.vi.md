---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 1.5. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 5:

* Tạo Target Group và cấu hình Health Check với Spring Boot Actuator.
* Thiết lập Application Load Balancer (ALB) hướng Internet.
* Tăng cường bảo mật mạng bằng cách hạn chế truy cập trực tiếp vào EC2.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Tạo Target Group `ewallet-backend-tg` (Port 8080, HTTP) và đăng ký EC2 instance | 03/07 | 03/07 |
| 2   | Cấu hình Health Check trỏ đến `/actuator/health` | 03/07 | 03/07 |
| 3   | Tạo ALB hướng Internet, gắn `alb-sg`, định tuyến HTTP port 80 vào Target Group | 04/07 | 04/07 |
| 4   | Đóng cổng 80 và 443 trên EC2, xác nhận cổng 8080 bị chặn khi truy cập trực tiếp IP công cộng | 04/07 | 04/07 |

### Kết quả đạt được:

* ALB kiểm tra sức khỏe Target đạt *Healthy*, là cổng tiếp nhận duy nhất cho API.
* Nắm vững cơ chế cân bằng tải, giám sát ứng dụng và ẩn máy chủ Compute đằng sau Load Balancer.