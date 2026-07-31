---
title: "Blog 1"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.1. </b> "
includeInReport: false
---
# [Tổng quan Case Study] Riot Games: Xử lý 20 TB Dữ liệu Phân tích Mỗi Ngày với Amazon MSK trên AWS

## Thông tin tài liệu
* **Lĩnh vực:** Game Trực tuyến, Thể thao điện tử, Phân tích Luồng Thời gian Thực, Kỹ thuật Dữ liệu Lớn.
* **Hệ thống mục tiêu:** Riot Games Data & Game Infrastructure (League of Legends, VALORANT, TFT).
* **Mẫu kiến trúc chính:** Ingestion Luồng Hướng Sự kiện + Xử lý Luồng Thời gian Thực + Data Lake Phân tách.
* **AWS Core Stack:** Amazon MSK (Managed Streaming for Apache Kafka), Amazon EMR (Apache Spark), Amazon S3, Amazon EKS, Amazon Athena / OpenSearch.

---

## 1. Bối cảnh Kinh doanh & Vấn đề

### 1.1 Quy mô Hệ thống
* **Người dùng:** Hơn 180 triệu Người dùng Hoạt động Hàng tháng (MAU) trên toàn cầu.
* **Khối lượng Dữ liệu:** Khoảng 20 TB dữ liệu telemetry và phân tích được tạo ra mỗi ngày.
* **Hệ thống Hạ nguồn Chính:** Engine ghép trận, cá nhân hóa trong game, phát hiện gian lận & bảo mật, hệ thống hành vi người chơi, và đồ họa phát sóng thể thao điện tử thời gian thực.

### 1.2 Thách thức Kỹ thuật
1. **Độ trễ Cao (3–6 Giờ):** Pipeline MapReduce cũ gây ra độ trễ 3-6 giờ giữa sự kiện trong game và dữ liệu sẵn sàng để truy vấn.
2. **Chi phí Vận hành Cao:** Quản lý hạ tầng batch cũ tốn nhiều tài nguyên và đắt đỏ.
3. **Không hỗ trợ Trường hợp Sử dụng Thời gian Thực:** Xử lý batch không thể đáp ứng các yêu cầu thời gian thực như phát hiện gian lận tức thời hoặc điều chỉnh ghép trận động.

---

## 2. Phân tích Kiến trúc Kỹ thuật

### Phân tích Chi tiết Thành phần

#### A. Lớp Ingestion Luồng
* **Amazon MSK (Managed Streaming for Apache Kafka):** Đóng vai trò xương sống nhắn tin trung tâm. Tiếp nhận tất cả luồng sự kiện game toàn cầu, thay thế pipeline MapReduce cũ đồng thời loại bỏ vận hành bảo trì cụm Kafka.

#### B. Lớp Xử lý Luồng & Data Lake
* **Apache Spark trên Amazon EMR:** Xử lý, lọc và biến đổi dữ liệu streaming gần thời gian thực khi các sự kiện chảy qua MSK.
* **Amazon S3 Data Lake:** Lưu trữ bền vững các sự kiện game đã xử lý và có cấu trúc, cho phép truy vấn trực tiếp qua Amazon Athena và OpenSearch.

#### C. Lớp Compute & Điều phối Container
* **Amazon EKS (Elastic Kubernetes Service):** Hạ tầng container hóa lưu trữ workloads máy chủ game và microservices, tự động mở rộng dựa trên lưu lượng người chơi.

---

## 3. Kết quả Kỹ thuật & Kinh doanh Chính

* **Giảm Độ trễ:** Độ trễ truy vấn giảm từ **6 giờ xuống còn 5 phút**.
* **Bảo mật & Chống Gian lận Thời gian Thực:** Cho phép phát hiện độc hại và bất thường gian lận gần thời gian thực.
* **Tiết kiệm Chi phí Hạ tầng:** Di chuyển sang Amazon EKS tiết kiệm **10 triệu USD chi phí hạ tầng hàng năm**.
* **Tốc độ Triển khai Toàn cầu:** Tăng tốc triển khai vùng game mới lên **12 lần**.
* **Phân tích Thể thao Điện tử:** Trích xuất dữ liệu trận đấu thời gian thực cung cấp số liệu thống kê phát sóng trực tiếp cho các giải đấu eSports toàn cầu (ví dụ: Worlds, VCT).

---

## 4. Bài học Kỹ thuật Chính

1. **Tận dụng Kafka Được Quản lý (MSK):** Chuyển vận hành cụm Kafka cho dịch vụ được quản lý giải phóng nhóm kỹ thuật tập trung vào xử lý dữ liệu cốt lõi và logic nghiệp vụ.
2. **Chuyển đổi Batch sang Thời gian Thực:** Chuyển đổi pipeline MapReduce cũ thành luồng Kafka thời gian thực mở khóa phân tích dưới phút quan trọng cho phát hiện gian lận và tối ưu hóa trải nghiệm người dùng.

## 5. Post và URL

![Riot](/images/3-BlogsPosted/3.1-Blog1/blog_1.png)

<p style="text-align: center;"><em>Figure 3.3. Blog Post.</em></p>

How Riot Games processes 20 TB of analytics data daily on AWS [Here](https://youtu.be/5L1K_moG-dY?si=UbMtqlufY4SgawjE).

Riot Games Cuts $10M Annual Infrastructure Costs by Migrating to Amazon EKS [Here](https://aws.amazon.com/vi/solutions/case-studies/riot-games-case-study/).

Scaling global game infrastructure using AWS Local Zones with Riot Games [Here](https://aws.amazon.com/vi/solutions/case-studies/riot-games-local-zones-case-study/).

Link bài viết [AWS Study Group - Facebook](https://www.facebook.com/groups/660548818043427?multi_permalinks=2226935201404773).