# CareBike Project

CareBike là hệ thống quản lý bảo trì và cứu hộ xe máy, phục vụ ba nhóm người dùng: quản trị viên, chi nhánh và khách hàng.

## Thành phần hệ thống

- **Backend:** Java Spring Boot, Spring Data JPA, WebSocket và SQL Server.
- **Web App:** React, TypeScript và Vite dành cho quản trị viên và chi nhánh.
- **Mobile App:** Flutter dành cho khách hàng và nhân viên chi nhánh.
- **AI Vision API:** Python dùng để phân tích hình ảnh và hỗ trợ kiểm tra tình trạng xe/lốp.
- **Database:** Microsoft SQL Server.

## Yêu cầu môi trường

- Java 17 trở lên.
- Node.js và npm.
- Flutter SDK và Android SDK.
- Python 3 và các thư viện trong `python-vision-api/requirements.txt`.
- Microsoft SQL Server và SQL Server Management Studio (SSMS).

## Khởi tạo database

1. Mở SQL Server Management Studio.
2. Tạo database có tên `care_bike`.
3. Mở file `database/care_bike_db.sql`.
4. Chọn đúng database `care_bike` và chạy toàn bộ script.
5. Kiểm tra thông tin kết nối trong `backend-java/src/main/resources/application.properties` hoặc cấu hình qua biến môi trường.

Không commit mật khẩu database, khóa Gemini hoặc Firebase service-account lên GitHub.

## Tài khoản demo

> Các tài khoản dưới đây chỉ dùng cho demo và môi trường học tập. Hãy đổi mật khẩu nếu triển khai hệ thống công khai.

| Vai trò | Email | Mật khẩu |
|---|---|---|
| Admin | `admin@carebike.com` | `admin123` |
| Branch | `carebike_q1@carebike.com` | `123456` |
| Customer | `customer1@example.com` | `123456` |

## Cách chạy dự án

Mở PowerShell tại thư mục gốc `CareBike_Project`. Mỗi dịch vụ nên được chạy trong một terminal riêng.

### 1. Chạy Backend

```powershell
cd backend-java
.\mvnw.cmd clean spring-boot:run
```

Backend mặc định chạy tại `http://localhost:8080`.

Nếu sử dụng Gemini, hãy khai báo khóa trong terminal trước khi chạy backend:

```powershell
$env:GEMINI_API_KEY="YOUR_GEMINI_API_KEY"
```

### 2. Chạy Web App

Lần đầu tiên, cài thư viện bằng `npm install`, sau đó chạy web:

```powershell
cd web-app
npm install
npm run dev
```

Web App thường chạy tại `http://localhost:5173`.

### 3. Chạy AI Vision API

```powershell
cd python-vision-api
.\start-ai-server.ps1
```

AI Vision API mặc định chạy tại `http://localhost:8000`.

### 4. Kết nối máy thật và máy ảo với Backend/AI

Kết nối thiết bị Android hoặc mở máy ảo. Trong một terminal tại thư mục gốc dự án, chạy:

```powershell
.\adb-reverse-all.ps1
```

Script này chuyển tiếp các cổng cần thiết cho tất cả thiết bị ADB đang kết nối. Nếu thiết bị hoặc máy ảo được khởi động lại, hãy chạy lại script.

### 5. Chạy Mobile App

```powershell
cd mobile_app
flutter pub get
flutter run
```

Bạn cũng có thể mở `mobile_app` bằng Android Studio và chạy đồng thời trên máy thật cùng máy ảo.

## Thứ tự khởi động đề xuất

1. SQL Server.
2. Backend Java.
3. AI Vision API.
4. Web App.
5. Máy thật/máy ảo Android và `adb-reverse-all.ps1`.
6. Mobile App Flutter.

## Cấu trúc thư mục chính

```text
CareBike_Project/
├── backend-java/       # Spring Boot REST API và WebSocket
├── web-app/            # React/TypeScript Web App
├── mobile_app/         # Flutter Mobile App
├── python-vision-api/  # Dịch vụ AI phân tích hình ảnh
├── database/           # Script SQL Server
├── docs/               # Tài liệu và sơ đồ hệ thống
└── adb-reverse-all.ps1 # Chuyển tiếp cổng cho thiết bị Android
```

## Lưu ý

- Không đưa `.env`, khóa API, service-account hoặc mật khẩu thật lên Git.
- Sau khi thay đổi Java, hãy khởi động lại backend.
- Sau khi thay đổi dịch vụ khởi tạo hoặc WebSocket trong Flutter, nên dùng **Hot Restart**.
- Khi thiết bị Android mất kết nối, chạy lại `adb-reverse-all.ps1`.
