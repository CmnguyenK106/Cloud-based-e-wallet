---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
includeInReport: false
---

Tại đây sẽ là phần liệt kê, giới thiệu các blogs mà các bạn đã đăng trên [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Dưới đây là ba blogs đã đăng:

###  [Blog 1 - RIOT GAMES: XỬ LÝ 20 TB DỮ LIỆU PHÂN TÍCH MỖI NGÀY VỚI AMAZON MSK TRÊN AWS](3.1-Blog1/)
Blog này giới thiệu hành trình của Riot Games trong việc xử lý 20 TB dữ liệu phân tích mỗi ngày bằng cách thay thế pipeline MapReduce batch cũ bằng Amazon MSK (Managed Streaming for Apache Kafka). Kiến trúc hướng sự kiện mới mang lại khả năng phân tích luồng gần thời gian thực cho League of Legends, VALORANT và TFT, giảm độ trễ truy vấn từ 6 giờ xuống còn 5 phút, hỗ trợ phát hiện gian lận (anti-cheat) theo thời gian thực và tiết kiệm 10 triệu USD chi phí hạ tầng hàng năm.

###  [Blog 2 - FORMULA 1 (F1 INSIGHTS): XỬ LÝ TELEMETRY THỜI GIAN THỰC & DỰ ĐOÁN ML TRÊN AWS](3.2-Blog2/)
Blog này khám phá cách Formula 1 xây dựng hệ thống F1 Insights xử lý telemetry thời gian thực và dự đoán ML trên AWS. Với hơn 300 cảm biến IoT trên mỗi chiếc xe tạo ra 1,1 triệu điểm dữ liệu mỗi giây, kiến trúc kết hợp Amazon Kinesis Data Streams, AWS Lambda, Apache Flink và Amazon SageMaker để cung cấp đồ họa phát sóng có độ trễ cực thấp (dưới 200ms) — bao gồm dự đoán xác suất vượt xe, hiệu suất lốp và chiến lược pit stop — cho hơn 1,5 tỷ khán giả truyền hình trên toàn thế giới.

###  [Blog 3 - BLUESIGHT: KIẾN TRÚC ĐA TÁC TỬ CHO TUÂN THỦ GPO PROHIBITION TRÊN AWS](3.3-Blog3/)
Blog này giới thiệu kiến trúc đa tác tử (multi-agent) của Bluesight để đảm bảo tuân thủ GPO Prohibition trên AWS. Sử dụng Amazon Bedrock (Claude) làm GPO Orchestrator phân công nhiệm vụ cho các worker agent chuyên biệt (340BCheck, ShortageCheck, CostCheck) cùng với deterministic scoring pipeline chạy 13 tín hiệu, giải pháp đạt độ chính xác xác định 100% đồng thời loại bỏ rủi ro ảo giác (hallucination) của LLM trong các cuộc kiểm toán tuân thủ định giá thuốc 340B có rủi ro cao.