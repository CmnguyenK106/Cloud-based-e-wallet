---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 1.2. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 2:

* Hoàn thiện toàn bộ nghiệp vụ Backend Ví điện tử (nạp, chuyển, thanh toán).
* Hoàn thiện Frontend với đầy đủ trang và Zod validation.
* Nghiên cứu và chọn kiến trúc Cloud mục tiêu trên AWS.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Implement giao dịch tài chính an toàn với `@Transactional` (Nạp, Chuyển tiền có tra cứu tên, Thanh toán dịch vụ ảo) | 15/06 | 16/06 |
| 2   | Phân chia route Backend: `/api/auth/**`, `/api/user/**`, `/api/admin/**` | 16/06 | 18/06 |
| 3   | Tích hợp Zod validation cho các form Frontend | 18/06 | 19/06 |
| 4   | Xây dựng Dashboard, trang Nạp/Chuyển tiền, Lịch sử GD, Dashboard Admin | 18/06 | 20/06 |
| 5   | Chạy kiểm thử tích hợp local và kiểm thử | 20/06 | 20/06 |
| 6   | Phân tích phương án triển khai và chốt kiến trúc Hybrid Cloud | 17/06 | 20/06 |
| 7   | Thiết kế sơ đồ kiến trúc: S3 + CloudFront cho frontend, EC2 cho backend, RDS cho database, SES cho email | 19/06 | 20/06 |

### Kết quả đạt được:

* Ứng dụng E-Wallet vận hành hoàn chỉnh ở môi trường Local.
* Tất cả unit test backend đạt 100% pass.
* Xác định được kiến trúc Cloud mục tiêu và danh sách dịch vụ AWS.