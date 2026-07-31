# BÁO CÁO NHẬT KÝ CÔNG VIỆC (WORKLOG REPORT)

**Dự án:** Triển khai Hệ thống Ví điện tử Mô phỏng (Simulated E-Wallet) trên AWS[cite: 1, 2]  
**Tech Stack:** React 19, TypeScript, Vite, Spring Boot 17, Docker, MySQL 8, AWS (S3, CloudFront, ALB, EC2, RDS, SES)[cite: 1, 2]

---

## Tuần 1: Khởi động Dự án & Xây dựng Môi trường Local (Chưa hoàn thiện)

### Mô tả công việc
* **Cấu hình môi trường phát triển Local:**
  * Cài đặt JDK 17, Maven, Node.js và Docker Desktop.
  * Khai báo file `docker-compose.yml` chạy MySQL 8 (ánh xạ cổng host `3307`) và phpMyAdmin (cổng `8081`) để phục vụ phát triển local[cite: 2].
  * Thiết kế sơ bộ CSDL quan hệ với các bảng cốt lõi: `users`, `user_profiles`, `admin_profiles`, `wallets`, `services`, `transactions` và `account_tokens`[cite: 1, 2].
* **Khởi tạo cấu trúc mã nguồn (Source Code):**
  * **Backend (Spring Boot 17):** Khởi tạo dự án, thiết lập Spring Data JPA, cấu hình `SecurityConfig` cho xác thực JWT và mã hóa BCrypt[cite: 1, 2]. Xây dựng các API Đăng ký, Đăng nhập ban đầu[cite: 2].
  * **Frontend (React 19 + Vite):** Khởi tạo khung ứng dụng với TypeScript, cấu hình React Router, Axios client và Zustand store[cite: 1, 2]. Dựng giao diện cơ bản cho trang Login và Register[cite: 2].

### Kết quả/kiến thức đạt được
* Dựng thành công khung dự án Full-stack và hạ tầng CSDL chạy qua Docker Compose ở local[cite: 1, 2].
* *Trạng thái công việc:* Hoàn thành cơ bản phần Authentication và thiết kế CSDL; các chức năng nghiệp vụ ví (Nạp, Chuyển, Thanh toán) vẫn đang trong quá trình phát triển, ứng dụng chưa thể chạy hoàn chỉnh luồng nghiệp vụ end-to-end[cite: 2].
* Nắm vững cách thiết kế Schema CSDL quan hệ, cơ chế mã hóa mật khẩu và cấu hình dự án Spring Boot kết hợp React SPA[cite: 1, 2].

---

## Tuần 2: Hoàn thiện Dev Local & Nghiên cứu Lựa chọn Dịch vụ AWS

### Mô tả công việc
* **Hoàn thiện toàn bộ chức năng ở môi trường Local:**
  * **Backend:** Hoàn thiện các nghiệp vụ giao dịch tài chính an toàn với `@Transactional` (Nạp tiền mô phỏng, Chuyển tiền giữa các ví có tra cứu tên người nhận, Thanh toán dịch vụ ảo)[cite: 1, 2]. Phân chia chi tiết các route: `/api/auth/**`, `/api/user/**`, `/api/admin/**`[cite: 2].
  * **Frontend:** Tích hợp Zod validation form; hoàn thiện giao diện Dashboard, Nạp/Chuyển tiền, Lịch sử giao dịch và Dashboard Admin[cite: 1, 2].
  * Chạy kiểm thử tích hợp local và thực thi 72 bài unit test backend đạt kết quả 100% pass[cite: 2].
* **Khảo sát và xác định Kiến trúc Cloud trên AWS:**
  * Phân tích các phương án triển khai và chốt mô hình Hybrid Cloud: Phân phối static frontend qua S3 + CloudFront CDN; chạy Backend containerized trên EC2; chuyển CSDL sang Amazon RDS MySQL và dùng Amazon SES gửi mail xác thực[cite: 1, 2].
  * Thiết kế sơ đồ kiến trúc tổng quan hệ thống và lập kế hoạch phân tầng bảo mật mạng (VPC, Subnets, Security Groups)[cite: 1].

### Kết quả/kiến thức đạt được
* Ứng dụng E-Wallet vận hành hoàn chỉnh 100% ở môi trường Local (Frontend `:5173`, Backend `:8080`, MySQL `:3307`)[cite: 2].
* Xác định được bản vẽ kiến trúc Cloud mục tiêu và danh sách các dịch vụ AWS cần triển khai[cite: 1].
* Nắm vững kỹ thuật xử lý ACID Transaction trong Spring Boot và tư duy lựa chọn dịch vụ Cloud phù hợp với quy mô dự án[cite: 1, 2].

---

## Tuần 3: Thiết lập AWS VPC Architecture & Triển khai Amazon RDS

### Mô tả công việc
* **Khởi tạo hạ tầng mạng VPC (Multi-AZ):**
  * Tạo Custom VPC `ewallet-vpc` (CIDR `10.0.0.0/16`) trên region `ap-southeast-1`[cite: 2].
  * Chia tách 2 Public Subnets (cho ALB) và 2 Private Subnets (cho EC2 Backend và RDS) trên 2 Availability Zones[cite: 1].
  * Tạo Internet Gateway (IGW) và cấu hình Route Table trỏ `0.0.0.0/0` ra IGW cho Public Subnets[cite: 1].
* **Cấu hình Security Groups (SG) & Amazon RDS MySQL:**
  * Thiết lập `alb-sg` (cho phép HTTP port 80), `ec2-backend-sg` (chỉ cho phép port 8080 từ `alb-sg` và SSH port 22 từ IP admin `/32`) và `rds-sg` (chỉ cho phép port 3306 từ `ec2-backend-sg`)[cite: 1].
  * Khởi tạo Amazon RDS for MySQL 8 trong Private Subnet Group (`Publicly Accessible = No`)[cite: 1, 2].
  * Thực thi các file SQL (`001_schema.sql`, `002_admin_template.sql`, `003_services_seed.sql`) khởi tạo schema và seed dữ liệu lên RDS[cite: 1, 2].

### Kết quả/kiến thức đạt được
* Hạ tầng mạng VPC và Cơ sở dữ liệu Managed Service trên AWS RDS đi vào hoạt động an toàn trong Private Subnet[cite: 1, 2].
* Hiểu sâu về AWS Networking (Subnets, Route Tables, IGW) và quy tắc phân quyền tối thiểu (*Least Privilege*) qua Security Groups[cite: 1].

---

## Tuần 4: Dockerize Backend & Triển khai lên Amazon EC2

### Mô tả công việc
* **Container hóa ứng dụng (Dockerization):**
  * Soạn thảo `Dockerfile` đa tầng (Multi-stage build) cho dự án Maven Spring Boot 17 để tối ưu dung lượng Image[cite: 1].
* **Cấu hình máy chủ EC2 & Deploy Backend:**
  * Khởi tạo EC2 Instance trong Public Subnet, cài đặt môi trường Docker Engine[cite: 1].
  * Tạo file biến môi trường độc lập ngoài Git `/home/ec2-user/ewallet-backend.env` trên EC2 lưu thông tin kết nối RDS, `JWT_SECRET` và cấu hình production[cite: 1, 2].
  * Thực thi lệnh `docker run` chạy container `ewallet-backend` lắng nghe cổng `8080:8080` kết nối tới RDS[cite: 1, 2].

### Kết quả/kiến thức đạt được
* Container backend vận hành ổn định trên EC2, truy vấn dữ liệu thành công từ RDS MySQL[cite: 1, 2].
* Nắm vững kỹ năng đóng gói ứng dụng bằng Docker và quản lý biến môi trường bảo mật trên máy chủ đám mây[cite: 1, 2].

---

## Tuần 5: Thiết lập Application Load Balancer (ALB) & Health Check

### Mô tả công việc
* **Thiết lập Target Group & ALB:**
  * Tạo Target Group `ewallet-backend-tg` (Port 8080, Protocol HTTP) và đăng ký EC2 Instance[cite: 1].
  * Cấu hình đường dẫn Health Check trỏ về `/actuator/health` của Spring Boot Actuator[cite: 1].
  * Khởi tạo Internet-facing ALB, gắn `alb-sg` và định tuyến traffic HTTP cổng 80 vào Target Group[cite: 1].
* **Rà soát An toàn Mạng:**
  * Đóng các cổng 80 và 443 trên EC2; xác nhận cổng 8080 bị chặn hoàn toàn khi truy cập trực tiếp từ IP công cộng của EC2[cite: 1].

### Kết quả/kiến thức đạt được
* ALB kiểm tra sức khỏe Target đạt trạng thái *Healthy*, đóng vai trò cổng tiếp nhận duy nhất cho API[cite: 1].
* Nắm vững cơ chế cân bằng tải, giám sát điểm sống ứng dụng qua Spring Actuator và ẩn máy chủ Compute đằng sau Load Balancer[cite: 1].

---

## Tuần 6: Deploy Frontend (S3 + CloudFront) & Phân giải Tên miền Cloudflare

### Mô tả công việc
* **Deploy Static Website lên S3 & CloudFront CDN:**
  * Build bản sản xuất ứng dụng React 19 (`npm run build`) và upload tĩnh lên S3 Bucket[cite: 1, 2].
  * Khởi tạo CloudFront Distribution: Cấu hình Origin 1 (S3 qua OAC) phục vụ file tĩnh; Origin 2 (ALB) phục vụ đường dẫn API[cite: 1].
  * Thiết lập Behavior: Default (`*`) trỏ về S3; Behavior `/api/*` chuyển tiếp về ALB với đầy đủ HTTP Methods và Headers[cite: 1].
* **Cấu hình Tên miền & SSL:**
  * Cấu hình bản ghi CNAME trên Cloudflare DNS trỏ tên miền `cloud-ewallet.com` về CloudFront Distribution[cite: 1].

### Kết quả/kiến thức đạt được
* Toàn bộ ứng dụng giao diện đã truy cập thành công qua HTTPS tại miền `https://cloud-ewallet.com`[cite: 1].
* Xử lý triệt để sự cố CORS bằng giải pháp hợp nhất Frontend và API trên cùng một phân phối CDN[cite: 1, 2].

---

## Tuần 7: Tích hợp Dịch vụ Email Xác thực qua Amazon SES SMTP

### Mô tả công việc
* **Thực thi cấu hình Amazon SES:**
  * Xác thực domain `cloud-ewallet.com` và email gửi `noreply@cloud-ewallet.com` trên Amazon SES[cite: 1].
  * Khởi tạo SMTP Credentials (cổng 587 STARTTLS)[cite: 1].
* **Tích hợp luồng gửi Mail trên Backend:**
  * Cập nhật cấu hình SES SMTP vào file `/home/ec2-user/ewallet-backend.env` trên EC2, giữ cấu hình `Resend` làm phương án dự phòng rollback[cite: 1, 2].
  * Kiểm thử các luồng: Gửi email xác thực khi đăng ký, gửi lại mã xác nhận và quên/đặt lại mật khẩu (lưu token hash vào `account_tokens`)[cite: 1, 2].

### Kết quả/kiến thức đạt được
* Hoàn thiện luồng xác thực và khôi phục tài khoản tự động qua email trên môi trường Production[cite: 1, 2].
* Hiểu rõ cơ chế quản lý vòng đời token, mã hóa SHA-256 token hash và tích hợp dịch vụ Email SMTP Cloud[cite: 1, 2].

---

## Tuần 8: Audit Bảo mật, Kiểm thử E2E & Hoàn thiện Tài liệu

### Mô tả công việc
* **Kiểm thử toàn diện (E2E) & Audit Bảo mật:**
  * Thực hiện kiểm thử E2E trên tên miền chính thức toàn bộ luồng nghiệp vụ: Đăng ký $\rightarrow$ Xác thực Mail $\rightarrow$ Nạp tiền $\rightarrow$ Chuyển tiền $\rightarrow$ Thanh toán dịch vụ $\rightarrow$ Xem lịch sử $\rightarrow$ Quản trị Admin[cite: 1, 2].
  * Kiểm tra cơ chế khoá tài khoản: Xác nhận frontend xóa session ngay lập tức khi nhận phản hồi `401` hoặc `ACCOUNT_BLOCKED` từ backend[cite: 1, 2].
  * Rà soát an ninh: Đảm bảo SSH port 22 giới hạn duy nhất IP admin `/32`; các cổng không cần thiết đều đã được đóng[cite: 1].
* **Đóng gói Tài liệu Dự án:**
  * Cập nhật file `README.md`, `description.md` và `PROJECT_STATUS.md` ghi nhận trạng thái triển khai thực tế, kết quả kiểm thử và danh sách định hướng nâng cấp (ASG, ECR, CI/CD, Lambda cleanup)[cite: 1, 2].

### Kết quả/kiến thức đạt được
* Bàn giao thành công sản phẩm Simulated E-Wallet vận hành ổn định, an toàn và chuẩn hóa trên hạ tầng AWS[cite: 1, 2].
* Nắm vững quy trình đánh giá an ninh hệ thống, kiểm thử E2E và phương pháp lập tài liệu kỹ thuật chuyên nghiệp[cite: 1, 2].