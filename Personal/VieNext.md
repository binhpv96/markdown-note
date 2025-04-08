# Documentation: Hệ thống mạng xã hội tích hợp đa chức năng

## 1. Giới thiệu

Hệ thống là một nền tảng mạng xã hội tích hợp, không chỉ cung cấp các tính năng cơ bản như đăng bài, tương tác, nhắn tin mà còn hỗ trợ công việc nhóm (họp trực tuyến), đánh giá uy tín, và giao dịch tài chính. Hệ thống được chia thành hai phiên bản:

- **v0.1**: Tập trung vào mạng xã hội cơ bản.
- **v0.2**: Bổ sung các tính năng nâng cao và tùy chọn premium (yêu cầu nạp phí).

**Mục tiêu**: Tạo ra một nền tảng đa năng, nơi người dùng kết nối, làm việc, kiểm tra độ tin cậy, và giao dịch an toàn.

**Tác giả**: Sinh viên công nghệ thông tin với kiến thức Spring Boot, React.js, Next.js, GitHub cơ bản, đang học thêm Docker và các công nghệ khác.

---

## 2. Yêu cầu

### 2.1. Yêu cầu chức năng

- **Phiên bản v0.1**:
  - Đăng bài, bình luận, thích, chia sẻ.
  - Nhắn tin real-time.
  - Quản lý hồ sơ người dùng.
- **Phiên bản v0.2**:
  - Phòng họp trực tuyến: Video call, chia sẻ màn hình, lên lịch họp, thông báo.
  - Bot thông minh: Tổng hợp thông tin, tự động đăng bài, trả lời cơ bản.
  - Đánh giá uy tín: Tra cứu thông tin (số điện thoại, email, link) để đánh giá dựa trên job freelancer, giao dịch, phản hồi.
  - Ví tiền và giao dịch: Lưu trữ tiền, chuyển tiền, thanh toán dịch vụ.
  - Tính năng premium: Nạp phí để truy cập họp trực tuyến, bot, đánh giá uy tín chi tiết.

### 2.2. Yêu cầu phi chức năng

- **Hiệu năng**: Hỗ trợ tối thiểu 1000 người dùng đồng thời ở v0.1, mở rộng lên 10,000 ở v0.2.
- **Bảo mật**: Xác thực bằng OAuth 2.0, mã hóa giao dịch.
- **Khả năng mở rộng**: Dùng microservices và Docker để dễ scale.

---

## 3. Thiết kế hệ thống

### 3.1. Kiến trúc tổng quan

Hệ thống sử dụng mô hình microservices, triển khai trên Google Cloud Platform (GCP) cho backend và Vercel cho frontend. Các thành phần chính:

- **Microservices**: User, Post, Chat, Meeting, Bot, Reputation, Payment.
- **Cơ sở dữ liệu**: MongoDB (NoSQL).
- **Cache**: Redis.
- **API Gateway**: Spring Cloud Gateway (tùy chọn trong tương lai).

![Sơ đồ kiến trúc microservices](erd-architecture.png)
*Hình 1: Sơ đồ kiến trúc microservices (Chụp từ ERD.drawio hoặc gắn link nếu upload lên GitHub/Figma)*

### 3.2. Thiết kế cơ sở dữ liệu

Dữ liệu được lưu trong MongoDB với các collections chính:

- `users`: Lưu thông tin người dùng (ID, username, email, premium status).
- `posts`: Lưu bài đăng (ID, content, userID, likes).
- `transactions`: Lưu giao dịch (ID, userID, amount, timestamp).

![Sơ đồ cơ sở dữ liệu MongoDB](erd-collections.png)
*Hình 2: Sơ đồ cơ sở dữ liệu MongoDB (Chụp từ ERD.drawio hoặc gắn link)*

### 3.3. Thiết kế giao diện

Giao diện được thiết kế trên Figma, bao gồm:

- Trang đăng bài và danh sách bài đăng.
- Trang nhắn tin real-time.
- Trang họp trực tuyến (v0.2).
- Trang đánh giá uy tín và ví tiền (v0.2).

![Giao diện trang chủ](figma-homepage.png)
*Hình 3: Giao diện trang chủ (Chụp từ Figma hoặc gắn link)*

![Giao diện nhắn tin](figma-chat.png)
*Hình 4: Giao diện nhắn tin (Chụp từ Figma hoặc gắn link)*

![Giao diện họp trực tuyến](figma-meeting.png)
*Hình 5: Giao diện họp trực tuyến (Chụp từ Figma hoặc gắn link)*

![Giao diện đánh giá uy tín](figma-reputation.png)
*Hình 6: Giao diện đánh giá uy tín (Chụp từ Figma hoặc gắn link)*

![Giao diện ví tiền](figma-wallet.png)
*Hình 7: Giao diện ví tiền (Chụp từ Figma hoặc gắn link)*

---

## 4. Công nghệ áp dụng

- **Backend**: Spring Boot (microservices), MongoDB, OAuth 2.0, Spring WebSocket, Redis.
- **Frontend**: React.js/Next.js (deploy trên Vercel), WebRTC.
- **Bot và AI**: Python (FastAPI).
- **Thanh toán**: Stripe/PayPal API.
- **DevOps**: GitHub, Docker, GCP (GKE, Cloud Storage), Vercel, Swagger.

---

## 5. Danh sách Microservices

1. **User Service**: Đăng ký, đăng nhập (OAuth 2.0), quản lý hồ sơ, phân quyền free/premium.
2. **Post Service**: Đăng bài, bình luận, thích, chia sẻ.
3. **Chat Service**: Nhắn tin real-time.
4. **Meeting Service**: Video call (WebRTC), lên lịch họp.
5. **Bot Service**: Tổng hợp thông tin, tự động đăng bài.
6. **Reputation Service**: Đánh giá uy tín.
7. **Payment Service**: Ví tiền, giao dịch, nạp phí premium.

---

## 6. API Documentation

API được tài liệu hóa bằng Swagger. Một số endpoint chính:

- **User Service**:
  - `POST /api/users/register`: Đăng ký người dùng.
  - `POST /api/users/login`: Đăng nhập (trả về token OAuth 2.0).
- **Post Service**:
  - `POST /api/posts`: Tạo bài đăng.
  - `GET /api/posts`: Lấy danh sách bài đăng.
- **Payment Service**:
  - `POST /api/payments/deposit`: Nạp tiền vào ví.

![Swagger UI](swagger-ui.png)
*Hình 8: Giao diện Swagger UI (Chụp sau khi triển khai Swagger hoặc gắn link)*

---

## 7. Hướng dẫn cài đặt

### 7.1. Yêu cầu môi trường

- Java 17 (cho Spring Boot).
- Node.js 18+ (cho React/Next.js).
- Docker Desktop.
- MongoDB local hoặc MongoDB Atlas.
- Tài khoản GCP và Vercel.

### 7.2. Cài đặt local

1. Clone repository từ GitHub:
   ```bash
   git clone [URL]
2. Cài đặt backend:
- Vào thư mục từng microservice (ví dụ: `user-service`).
- Chạy
   ```bash
   mvn clean install
- Tạo Dockerfile:
   ```bash
   FROM openjdk:17
   COPY target/user-service.jar app.jar
   ENTRYPOINT ["java", "-jar", "app.jar"] 
- Chạy
   ```bash
   docker build -t user-service . && docker run -p 8080:8080 user-service
3. Cài đặt frontend:
- Vào thư mục frontend.
- Chạy
   ```bash
   npm install && npm run dev
4. Cấu hình docker-compose.yml:
   ```bash
    version: '3'
    services:
        user-service:
            image: user-service
            ports: ["8080:8080"]
        mongo:
            image: mongo:latest
            ports: ["27017:27017"]

---

## 8. Hướng dẫn sử dụng
- Người dùng free:
    - Đăng ký, đăng nhập, đăng bài, nhắn tin.
- Người dùng premium:
    - Nạp tiền qua ví (Payment Service).
    - Truy cập họp trực tuyến, bot, đánh giá uy tín.

![Flow đăng kí](flow-dang-ki.png)
*Hình 9: Flow đăng ký người dùng (Chụp từ Figma nếu có hoặc gắn link)*

![Flow nạp tiền](flow-nap-tien.png)
*Hình 10: Flow nạp tiền (Chụp từ Figma nếu có hoặc gắn link)*

---

## 9. Lộ trình phát triển
- Chuẩn bị ban đầu (2-3 tuần): Tài liệu, học công nghệ.
- v0.1 (6-8 tuần): User, Post, Chat, frontend cơ bản.
- v0.2 (12-16 tuần): Meeting, Bot, Reputation, Payment, frontend nâng cao.
- Kiểm thử và triển khai (5-7 tuần): Test, deploy lên Vercel/GCP.

---

## 10. Branch trên GitHub
- `main`: Code ổn định.
- `develop`: Tích hợp code.
- `feature/v0.1-user-service`, `feature/v0.1-post-service`, v.v.
- `feature/v0.2-meeting-service`, `feature/v0.2-payment-service`, v.v.
- `release/v0.1`, `release/v0.2`.