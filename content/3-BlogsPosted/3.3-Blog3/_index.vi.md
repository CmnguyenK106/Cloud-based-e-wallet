---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# [Tổng quan Case Study] Bluesight: Kiến trúc Đa tác tử cho Tuân thủ GPO Prohibition trên AWS

## Thông tin tài liệu
* **Lĩnh vực:** Healthcare FinTech, Tuân thủ Dược phẩm, Hệ thống GenAI, Kiến trúc AWS.
* **Hệ thống mục tiêu:** Bluesight (Nền tảng Thông minh về Thuốc).
* **Mẫu kiến trúc chính:** Multi-Agent Orchestration + Deterministic Scoring Pipeline + Model Context Protocol (MCP).
* **AWS Core Stack:** Amazon Bedrock (Claude 3.5 Sonnet / Haiku), Amazon Cognito, AWS Lambda, AgentCore Gateway, Amazon CloudWatch, AWS VPC Private Subnets.

---

## 1. Bối cảnh Kinh doanh & Vấn đề

### 1.1 Khái niệm Nghiệp vụ
* **Chương trình Giá thuốc 340B:** Một chương trình liên bang Hoa Kỳ cho phép các nhà cung cấp dịch vụ y tế an toàn mua thuốc ngoại trú với chiết khấu đáng kể (20%–50%).
* **GPO Prohibition:** Các bệnh viện tham gia 340B bị nghiêm cấm mua thuốc ngoại trú thông qua hợp đồng Tổ chức Mua sắm Nhóm (GPO).
* **Tác động tuân thủ:** Vi phạm GPO Prohibition dẫn đến phạt tài chính nghiêm trọng (hàng triệu USD), hoàn trả truy thu cho nhà sản xuất thuốc, hoặc bị loại khỏi chương trình 340B.

### 1.2 Độ phức tạp Kiểm toán & Nút thắt Kỹ thuật
Để đánh giá tuân thủ GPO Prohibition, nhân viên tuân thủ phải đối chiếu dữ liệu qua ba sản phẩm/nguồn dữ liệu riêng biệt:
1. **340BCheck:** Trạng thái đủ điều kiện bệnh nhân và phân bổ đơn thuốc 340B.
2. **ShortageCheck:** Dữ liệu thiếu hụt thuốc từ FDA và nội bộ (tình trạng thiếu có thể tạo ngoại lệ hợp pháp).
3. **CostCheck:** Chênh lệch giá qua các kênh mua sắm (WAC, GPO, 340B).

### 1.3 Tại sao AI Truyền thống / Đơn tác tử Thất bại
* **Quá tải Context Window:** Đưa hướng dẫn liên bang 340B, cơ sở dữ liệu giá thời gian thực và nhật ký giao dịch vào một prompt duy nhất làm giảm chất lượng suy luận.
* **Rủi ro Hallucination trong Kiểm toán Pháp lý:** Độ chính xác xác định là bắt buộc; LLM đưa ra phán đoán chủ quan về tuân thủ pháp lý tạo ra rủi ro trách nhiệm pháp lý lớn.

---

## 2. Phân tích Kiến trúc Kỹ thuật

![Bluesight multi-agent architecture](/images/3-BlogsPosted/3.3-Blog3/architecture.png)

<p style="text-align: center;"><em>Figure 3.3. Bluesight Multi-Agent Orchestration Architecture.</em></p>

### Phân tích Chi tiết Thành phần

#### A. Lớp Ingress & Bảo mật
* **Amazon Cognito:** Xử lý xác thực OAuth2 + JWT cho `Người dùng Tuân thủ Bệnh viện`.
* **VPC Private Subnets:** Cách ly mạng cho `AgentCore Runtime` để tuân thủ các tiêu chuẩn bảo mật dữ liệu y tế.

#### B. Lớp Điều phối (Bộ não)
* **GPO Orchestrator Agent:** Được hỗ trợ bởi **Amazon Bedrock (Claude 3.5 Sonnet / Haiku)**. Đóng vai trò là công cụ suy luận trung tâm, phân tích ý định người dùng, phân rã tác vụ, ủy quyền tác vụ con cho các tác tử chuyên biệt, và theo dõi dấu vết suy luận qua **Amazon CloudWatch**.

#### C. Lớp Xử lý Dữ liệu (Các tác tử chuyên biệt)
Thay vì thực thi truy vấn trực tiếp, Orchestrator ủy quyền tác vụ cho 3 tác tử theo lĩnh vực:
* **`340BCheck Worker`:** Truy vấn phân bổ đơn thuốc 340B và quy tắc đủ điều kiện bệnh nhân.
* **`ShortageCheck Worker`:** Truy vấn tình trạng thiếu thuốc từ FDA và thị trường.
* **`CostCheck Worker`:** Truy vấn giá lịch sử, chênh lệch chi phí WAC so với GPO so với 340B.

#### D. Lớp Tích hợp & Công cụ
* **AgentCore Gateway:** Điều phối giao tiếp API giữa các Worker Agent và nguồn dữ liệu cơ bản.
* **Lambda-backed MCP Tools:** Chuẩn hóa thực thi công cụ bằng **Model Context Protocol (MCP)** triển khai dưới dạng hàm AWS Lambda để truy vấn cơ sở dữ liệu sản phẩm (`CostCheck`, `ShortageCheck`, `340BCheck`).

#### E. Pipeline Tính điểm Xác định (Lớp bảo vệ Zero-Hallucination)
* **Chức năng:** Một pipeline phi-LLM, thuần toán học/logic chạy **13 tín hiệu xác định (quy tắc)**.
* **Thực thi:** Worker Agents lấy dữ liệu thô và đóng gói thành **Bằng chứng (Evidence)** có cấu trúc. Bằng chứng được xử lý bởi Scoring Pipeline để tính điểm rủi ro tuân thủ được xác minh toán học ($100\\%$ độ chính xác xác định).

---

## 3. Chuỗi Thực thi End-to-End

1. **Tiếp nhận Yêu cầu:** Người dùng xác thực qua Cognito và gửi truy vấn tuân thủ về danh sách thuốc ngoại trú đã mua.
2. **Phân tích Ý định & Ủy quyền:** `GPO Orchestrator` nhận yêu cầu, lập kế hoạch luồng thực thi qua Bedrock, và ủy quyền tác vụ bất đồng bộ cho `340BCheck Worker`, `ShortageCheck Worker`, và `CostCheck Worker`.
3. **Truy xuất Dữ liệu qua MCP:** Mỗi Worker Agent thực thi `Lambda-backed MCP Tools` qua `AgentCore Gateway` để lấy bản ghi liên quan từ cơ sở dữ liệu sản phẩm.
4. **Xác thực Xác định:** Bằng chứng thô từ tất cả worker được chuyển vào `Deterministic Scoring Pipeline (13 Signals)` để tính toán tuân thủ.
5. **Tạo Báo cáo:** `GPO Orchestrator` nhận điểm tuân thủ đã xác thực, định dạng kết quả thành báo cáo kiểm toán ngôn ngữ tự nhiên với trích dẫn, và trả về cho người dùng.

---

## 4. Bài học Kỹ thuật Chính

1. **Mẫu Multi-Agent Phân tách:** Phân chia kiến thức miền qua các Worker Agent chuyên biệt ngăn chặn phình to context window, giảm độ trễ qua thực thi song song, và cải thiện độ chính xác chọn công cụ.
2. **Trí tuệ Lai (LLM + Engine Xác định):** LLM tối ưu cho suy luận, lập kế hoạch tác vụ và sinh ngôn ngữ; thuật toán xác định là bắt buộc cho tính toán pháp lý/tài chính. Kết hợp cả hai loại bỏ ảo giác AI trong các lĩnh vực rủi ro cao.
3. **Công cụ Chuẩn hóa với MCP:** Áp dụng Model Context Protocol (MCP) tách logic điều phối tác tử khỏi tích hợp nguồn dữ liệu, cho phép onboarding liền mạch các sản phẩm hoặc cơ sở dữ liệu mới.

## 5. Post và URL 

![Bluesight multi-agent architecture](/images/3-BlogsPosted/3.3-Blog3/blog_3.png)

<p style="text-align: center;"><em>Figure 3.3. Blog Post.</em></p>

Thông tin chi tiết tại đây [AWS Blog](https://aws.amazon.com/vi/blogs/machine-learning/building-an-agentic-ai-solution-at-bluesight-with-amazon-bedrock/).

Link bài viết [AWS Study Group - Facebook](https://www.facebook.com/groups/660548818043427?multi_permalinks=2227994621298831).