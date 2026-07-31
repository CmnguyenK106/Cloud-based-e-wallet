---
title: "Worklog Tuần 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.1. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 1:

* Thiết lập môi trường phát triển local cho dự án Full-stack.
* Khởi tạo khung ứng dụng Spring Boot backend và React frontend.
* Thiết kế sơ đồ cơ sở dữ liệu quan hệ cho hệ thống Ví điện tử.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Cài đặt JDK 17, Maven, Node.js và Docker Desktop | 08/06 | 08/06 |
| 2   | Tạo `docker-compose.yml` cho MySQL 8 (cổng 3307) và phpMyAdmin (cổng 8081) | 08/06 | 08/06 |
| 3   | Thiết kế schema CSDL: `users`, `user_profiles`, `admin_profiles`, `wallets`, `services`, `transactions`, `account_tokens` | 09/06 | 13/06 |
| 4   | Khởi tạo dự án Spring Boot 17 với Spring Data JPA, SecurityConfig (JWT + BCrypt) | 09/06 | 10/06 |
| 5   | Xây dựng API Đăng ký/Đăng nhập cơ bản | 09/06 | 12/06 |
| 6   | Khởi tạo dự án React 19 + Vite + TypeScript với React Router, Axios, Zustand | 10/06 | 12/06 |
| 7   | Dựng giao diện cơ bản cho trang Login và Register | 10/06 | 13/06 |

### Kết quả đạt được:

* Thiết lập thành công môi trường local với Docker Compose.
* Hoàn thành luồng xác thực cơ bản (Đăng ký/Đăng nhập) với JWT.
* Thiết kế và tạo schema cơ sở dữ liệu quan hệ.
* Khung frontend với routing và state management sẵn sàng.


