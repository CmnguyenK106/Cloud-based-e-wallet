---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 1.6. </b> "
reportTableColumns:
  - Thứ
  - Công việc
  - Ngày hoàn thành
reportType: worklog
---
### Mục tiêu tuần 6:

* Triển khai React frontend lên S3 và phục vụ qua CloudFront CDN.
* Cấu hình CloudFront với hai Origins (S3 cho tĩnh, ALB cho API).
* Thiết lập tên miền tùy chỉnh với Cloudflare DNS và SSL.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành |
| --- | --------- | ------------ | --------------- |
| 1   | Build React 19 production (`npm run build`) và upload lên S3 Bucket | 10/07 | 10/07 |
| 2   | Tạo CloudFront Distribution: Origin 1 (S3 qua OAC) cho file tĩnh, Origin 2 (ALB) cho API | 11/07 | 11/07 |
| 3   | Cấu hình Behavior: Default (`*`) đến S3, `/api/*` đến ALB với đầy đủ HTTP Methods & Headers | 12/07 | 12/07 |
| 4   | Cấu hình bản ghi CNAME trên Cloudflare DNS trỏ `cloud-ewallet.com` đến CloudFront Distribution | 13/07 | 13/07 |
| 5   | Kiểm thử truy cập HTTPS toàn bộ ứng dụng | 13/07 | 14/07 |

### Kết quả đạt được:

* Toàn bộ ứng dụng truy cập thành công qua HTTPS tại `https://cloud-ewallet.com`.
* Xử lý triệt để sự cố CORS bằng giải pháp hợp nhất Frontend và API trên cùng CloudFront Distribution.