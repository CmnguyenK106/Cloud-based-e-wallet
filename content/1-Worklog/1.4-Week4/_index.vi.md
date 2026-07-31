---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 4
chapter: false
pre: " <b> 1.4. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 4:

* Container hóa ứng dụng Spring Boot backend với Dockerfile đa tầng.
* Khởi tạo EC2 instance và triển khai backend đã đóng gói.
* Cấu hình biến môi trường production an toàn.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Viết `Dockerfile` đa tầng cho dự án Maven Spring Boot 17 | 26/06 | 26/06 |
| 2   | Khởi tạo EC2 instance trong Public Subnet, cài đặt Docker Engine | 27/06 | 27/06 |
| 3   | Tạo file `/home/ec2-user/ewallet-backend.env` chứa thông tin RDS, JWT_SECRET, cấu hình production | 28/06 | 28/06 |
| 4   | Chạy `docker run` để khởi động container `ewallet-backend` trên cổng `8080:8080` | 29/06 | 29/06 |
| 5   | Xác nhận backend container kết nối RDS thành công | 29/06 | 29/06 |

### Kết quả đạt được:

* Container backend vận hành ổn định trên EC2, truy vấn dữ liệu từ RDS MySQL thành công.
* Nắm vững kỹ năng Docker và quản lý biến môi trường bảo mật trên máy chủ Cloud.