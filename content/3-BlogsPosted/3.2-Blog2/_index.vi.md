---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---
# [Tổng quan Case Study] Formula 1 (F1 Insights): Xử lý Telemetry Thời gian Thực & Dự đoán ML trên AWS

## Thông tin tài liệu
* **Lĩnh vực:** Thể thao Chuyên nghiệp, Truyền thông & Giải trí, IoT, Phân tích Thời gian Thực, ML Dự đoán.
* **Hệ thống mục tiêu:** Formula 1 (Hệ thống Phát sóng Trực tiếp F1 Insights).
* **Mẫu kiến trúc chính:** Xử lý Luồng Sự kiện + Suy luận ML Độ trễ Thấp + Feature Store + Ingestion Phân tách.
* **AWS Core Stack:** Amazon Kinesis Data Streams, Amazon SageMaker, Amazon DynamoDB, AWS Lambda, Amazon Managed Service for Apache Flink, Amazon S3.

---

## 1. Bối cảnh Kinh doanh & Vấn đề

### 1.1 Quy mô Hệ thống
* **Cảm biến mỗi xe:** Hơn 300 cảm biến IoT trên mỗi xe F1 đo nhiệt độ lốp, lực phanh, áp suất ERS, G-force, ga và khí động học.
* **Khối lượng Dữ liệu:** 1,1 triệu điểm dữ liệu telemetry mỗi giây được tạo ra từ 20 xe.
* **Bối cảnh Lịch sử:** 3 GB dữ liệu telemetry mỗi xe mỗi cuối tuần đua, kết hợp với hơn 70 năm dữ liệu lịch sử từ năm 1950.
* **Khán giả Toàn cầu:** Hơn 1,5 tỷ người xem truyền hình trên toàn thế giới mong đợi số liệu thống kê tương tác trực tiếp.

### 1.2 Thách thức Kỹ thuật
1. **Ràng buộc Độ trễ Cực thấp (< 100ms):** Dữ liệu telemetry phải đi từ cảm biến xe đến máy chủ trackside, qua đám mây để suy luận ML, và quay lại công cụ đồ họa phát sóng trong vòng 100–200ms để đồng bộ với hình ảnh TV trực tiếp.
2. **Môi trường Mạng Mất gói:** Xe di chuyển ở tốc độ 350 km/h gây mất tín hiệu RF gián đoạn, yêu cầu đệm luồng dữ liệu mạnh mẽ và xử lý dữ liệu không theo thứ tự.
3. **Kỹ thuật Đặc trưng Thời gian Thực:** Kết hợp luồng telemetry trực tiếp với dữ liệu lịch sử hàng thập kỷ trên S3 để đánh giá phong cách lái, điều kiện đường đua và cửa sổ chiến lược ngay lập tức.

---

## 2. Phân tích Kiến trúc Kỹ thuật

![F1_insight](/images/3-BlogsPosted/3.2-Blog2/F1_architecture.png)

<p style="text-align: center;"><em>Figure 3.3. F1 Insights Architecture.</em></p>

### Phân tích Chi tiết Thành phần

#### A. Lớp Ingestion
* **Xử lý Edge Trackside:** Bộ thu RF trackside nhận telemetry thô từ xe và áp dụng lọc ban đầu.
* **Amazon Kinesis Data Streams:** Đóng vai trò bộ đệm sự kiện thông lượng cao, tự động mở rộng để xử lý hàng triệu sự kiện streaming mỗi giây với không mất dữ liệu.

#### B. Lớp Xử lý Luồng & Feature Store
* **AWS Lambda & Apache Flink:** Thực hiện biến đổi luồng, lọc nhiễu và tổng hợp thời gian thực (ví dụ: tốc độ trung bình sector).
* **Amazon DynamoDB:** Đóng vai trò là kho lưu trữ trạng thái/feature store có độ trễ cực thấp (<10ms) để duy trì trạng thái xe thời gian thực (mòn lốp, vị trí, khoảng cách với xe trước/sau).

#### C. Lớp Suy luận Machine Learning
* **Amazon S3 Data Lake:** Lưu trữ hơn 70 năm dữ liệu lịch sử đua xe được sử dụng để huấn luyện mô hình ML dự đoán.
* **Amazon SageMaker:** Huấn luyện mô hình dự đoán phức tạp ngoại tuyến và lưu trữ trên **SageMaker Real-Time Inference Endpoints**, thực thi suy luận ML dưới 20ms mỗi yêu cầu.

---

## 3. Các Trường hợp Sử dụng ML Dự đoán (F1 Insights)

| Đồ họa F1 Insight | Mô hình / Kỹ thuật ML | Giá trị Mang lại |
| :--- | :--- | :--- |
| **Xác suất Vượt mặt** | Phân tích khoảng cách xe, chênh lệch tốc độ, độ mòn lốp, lực cản khí động học và vùng DRS sắp tới. | Dự đoán % chính xác khả năng vượt tại góc cua tiếp theo. |
| **Hiệu suất & Tuổi thọ Lốp** | Dự đoán độ mòn dựa trên G-forces, nhiệt độ mặt đường, áp suất phanh và phong cách lái lịch sử. | Hiển thị % mòn lốp thời gian thực mà không cần chờ pit stop. |
| **Chiến thuật Pit Battle** | So sánh phân tích tốc độ undercut/overcut và cửa sổ khoảng cách trong giao thông. | Dự báo thời điểm pit stop tối ưu và vị trí trên đường đua sau pit. |
| **Phân tích Góc cua** | So sánh telemetry giữa các tay đua tại apex cụ thể (điểm phanh, tốc độ apex, thời điểm ga). | Giải thích chênh lệch thời gian giữa các tay đua mỗi sector một cách trực quan. |

---

## 4. Bài học Kỹ thuật Chính

1. **Kiến trúc Luồng Phân tách:** Tách ingestion (Kinesis) khỏi inference (SageMaker) ngăn tắc nghẽn kết xuất phát sóng ảnh hưởng đến xử lý dữ liệu thượng nguồn.
2. **Feature Store Trong Bộ nhớ & Độ trễ Thấp:** Truy cập kho lưu trữ trạng thái dưới 10ms (DynamoDB) là thiết yếu cho engine suy luận ML thời gian thực để đưa ra quyết định tức thời.
3. **Mẫu Edge-Cloud Hybrid:** Lọc nhiễu tại edge trackside trước khi truyền đến AWS Cloud tối ưu hóa băng thông đắt đỏ.

## 5. Post và URL 

![F1_insight](/images/3-BlogsPosted/3.2-Blog2/blog_2.png)

<p style="text-align: center;"><em>Figure 3.3. Blog Post.</em></p>

Thông tin chi tiết tại đây [AWS Blog](https://aws.amazon.com/vi/blogs/machine-learning/accelerating-innovation-how-serverless-machine-learning-on-aws-powers-f1-insights/).