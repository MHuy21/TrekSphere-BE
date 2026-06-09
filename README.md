# TrekSphere Backend

TrekSphere là nền tảng chuyên cung cấp các tour du lịch trekking và trải nghiệm khám phá thiên nhiên tại Việt Nam. Dự án Backend được xây dựng bằng ngôn ngữ Java với Framework Spring Boot, áp dụng các tiêu chuẩn thiết kế hiện đại và kiến trúc phân lớp rõ ràng để đảm bảo tính mở rộng, hiệu năng cao và dễ bảo trì.

---

## 🛠️ Công nghệ & Thư viện Sử dụng

Hiện tại, dự án đang sử dụng các công nghệ và thư viện cốt lõi sau:

| Công nghệ / Thư viện | Phiên bản   | Mô tả                                                                                     |
| :------------------- | :---------- | :---------------------------------------------------------------------------------------- |
| **Java**             | 21          | Sử dụng các tính năng mới của Java LTS (Record, Pattern Matching, Virtual Threads ready). |
| **Spring Boot**      | 3.5.x       | Framework phát triển ứng dụng Java Web nhanh chóng và mạnh mẽ.                            |
| **PostgreSQL**       | 15 (Alpine) | Cơ sở dữ liệu quan hệ chính, tối ưu hiệu năng và độ ổn định cao.                          |

---

## 📂 Cấu trúc Thư mục Dự án

Mã nguồn được cấu trúc theo mô hình phân lớp (Layered Architecture) chuẩn hóa giúp tách biệt mối quan tâm giữa các tầng xử lý dữ liệu, logic nghiệp vụ và giao tiếp ngoại vi:

```text
treksphere-be/
├── .env                         # File lưu trữ biến môi trường (Database credentials, pgAdmin, ports...)
├── docker-compose.yml           # Định nghĩa các dịch vụ Docker (PostgreSQL, pgAdmin)
├── pom.xml                      # Cấu hình dự án Maven và quản lý dependencies
├── src/main/
│   ├── java/com/sep/treksphere/
│   │   ├── TreksphereBeApplication.java  # Class khởi chạy ứng dụng
│   │   ├── config/              # Chứa các lớp cấu hình hệ thống (CORS, Swagger/OpenAPI...)
│   │   ├── controller/          # Tầng tiếp nhận request RESTful API và gửi trả response
│   │   ├── dto/                 # Chứa các đối tượng chuyển đổi dữ liệu (Request DTO, Response DTO)
│   │   │   ├── request/
│   │   │   └── response/
│   │   ├── entity/              # Các Entity tương ứng với các bảng trong Database (JPA)
│   │   ├── enums/               # Các định nghĩa hằng số dạng Enum (Ví dụ: ErrorCode)
│   │   ├── exception/           # Xử lý ngoại lệ tập trung (Global Exception Handler & Custom Exceptions)
│   │   ├── mapper/              # Các interface định nghĩa ánh xạ đối tượng bằng MapStruct
│   │   ├── repository/          # Tầng giao tiếp trực tiếp với cơ sở dữ liệu (Spring Data JPA)
│   │   ├── service/             # Tầng chứa logic nghiệp vụ cốt lõi (Business Logic)
│   │   └── utils/               # Các lớp tiện ích dùng chung cho hệ thống
│   └── resources/
│       ├── application.yml      # File cấu hình cấu trúc ứng dụng Spring Boot
│       ├── static/              # Lưu trữ tài nguyên tĩnh (nếu có)
│       └── templates/           # Thư mục template HTML (nếu có)
```

---

## 🚀 Hướng dẫn Cài đặt & Khởi chạy Nhanh

### 1. Yêu cầu Hệ thống

Trước khi khởi chạy dự án, hãy đảm bảo máy tính của bạn đã cài đặt các công cụ sau:

- **Java Development Kit (JDK) 21** trở lên.
- **Docker** và **Docker Compose**.
- **Maven**

### 2. Thiết lập Biến Môi trường (`.env`)

Tạo một file đặt tên là `.env` tại thư mục gốc của dự án `treksphere-be` (nếu chưa có) và cấu hình các thông số phù hợp:

```env
POSTGRES_DB=treksphere_db
POSTGRES_USER=admin
POSTGRES_PASSWORD=your_secure_password

PGADMIN_DEFAULT_EMAIL=admin@treksphere.com
PGADMIN_DEFAULT_PASSWORD=admin_password

DB_HOST=localhost
DB_PORT=5432
```

### 3. Khởi chạy Cơ sở Dữ liệu (Docker)

Tại thư mục gốc của dự án `treksphere-be` (nơi chứa file `docker-compose.yml`), khởi chạy các container cơ sở dữ liệu ở chế độ chạy ngầm (detached mode):

```bash
docker-compose up -d
```

Để kiểm tra trạng thái hoạt động của các container:

```bash
docker-compose ps
```

### 4. Chạy Ứng dụng Backend Spring Boot

Bạn có thể import dự án vào các IDE phổ biến như IntelliJ IDEA, Eclipse hoặc chạy trực tiếp bằng dòng lệnh:

- **Sử dụng Maven Wrapper trên Windows (PowerShell / CMD):**
  ```powershell
  .\mvnw spring-boot:run
  ```
- **Sử dụng Maven Wrapper trên Linux/macOS:**
  ```bash
  ./mvnw spring-boot:run
  ```

Ứng dụng mặc định sẽ khởi chạy trên cổng **`8080`**.

---
