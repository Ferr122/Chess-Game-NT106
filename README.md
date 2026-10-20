# ♟️ Online Chess Game - NT106 (Nhóm 10)

<p align="center">
  <img src="https://img.shields.io/badge/.NET-C%23-blueviolet?style=for-the-badge&logo=dotnet" alt=".NET C#" />
  <img src="https://img.shields.io/badge/UI-Windows%20Forms-blue?style=for-the-badge" alt="WinForms" />
  <img src="https://img.shields.io/badge/Networking-TCP%20Socket-brightgreen?style=for-the-badge" alt="TCP Socket" />
  <img src="https://img.shields.io/badge/Database-SQL%20Server-red?style=for-the-badge&logo=microsoftsqlserver" alt="SQL Server" />
  <img src="https://img.shields.io/badge/Course-NT106-orange?style=for-the-badge" alt="NT106" />
</p>

> **Đồ án môn học:** Lập trình Mạng Căn bản (NT106)  
> **Đề tài:** Xây dựng ứng dụng Game Cờ Vua Trực Tuyến theo mô hình Client - Server.

---

## 📖 1. Tổng quan dự án

**Online Chess Game** là hệ thống cờ vua trực tuyến cho phép người chơi tạo tài khoản, đăng nhập, tìm kiếm đối thủ và tham gia thi đấu thời gian thực. Hệ thống được phát triển nhằm mô phỏng đầy đủ luật cờ vua tiêu chuẩn, tích hợp tính năng phòng chờ, ghép trận, chat trực tiếp trong trận đấu và lưu trữ lịch sử nước đi, kết quả vào cơ sở dữ liệu.

---

## ✨ 2. Tính năng chính

- 🔐 **Quản lý tài khoản:** Đăng ký, đăng nhập an toàn, cập nhật hồ sơ cá nhân và quản lý thông tin tài khoản.
- ⚔️ **Ghép trận trực tuyến:** Hệ thống hàng đợi tìm trận (Matchmaking) tự động kết nối 2 người chơi.
- ♟️ **Luật chơi hoàn chỉnh:** Kiểm tra nước đi hợp lệ của từng quân cờ, kiểm tra trạng thái Chiếu (Check), Chiếu hết (Checkmate), Hòa cờ (Stalemate / Draw).
- 💬 **Trò chuyện trực tuyến (In-game Chat):** Trao đổi tin nhắn thời gian thực giữa hai người chơi trong lúc thi đấu.
- 📜 **Lịch sử & Thống kê:** Lưu trữ từng nước đi của trận đấu, kết quả thắng/thua, hỗ trợ xem lại và xếp hạng người chơi.
- 🔄 **Đồng bộ thời gian thực:** Kết nối TCP Socket ổn định, phản hồi tức thì với độ trễ tối thiểu.

---

## 👥 3. Phân công công việc (Nhóm 10)

| STT | Hạng mục / Module | Mô tả chi tiết công việc | Người phụ trách |
| :---: | :--- | :--- | :---: |
| **01** | **Giao diện & Quản lý Tài khoản (Client)** | Thiết kế giao diện WinForms cho các chức năng đăng nhập, đăng ký, menu chính và hồ sơ người dùng; xây dựng chức năng quản lý tài khoản phía Client. | Thành viên 1 |
| **02** | **Kết nối TCP & Giao thức Truyền thông** | Xây dựng chức năng kết nối TCP, thiết kế giao thức giao tiếp giữa Client và Server, xử lý gửi nhận dữ liệu và đồng bộ trạng thái giữa các Client. | Thành viên 2 |
| **03** | **Cơ sở dữ liệu (Database & Storage)** | Thiết kế cơ sở dữ liệu SQL Server, xây dựng các bảng, khóa chính, khóa ngoại và chức năng truy vấn, lưu trữ dữ liệu tài khoản, trận đấu, lịch sử nước đi và tin nhắn. | Thành viên 3 |
| **04** | **Game Logic & Quản lý Trận đấu (Module 1)** | Xây dựng logic cờ vua, xử lý nước đi hợp lệ, kiểm tra chiếu, chiếu hết, hòa cờ; xây dựng chức năng ghép trận và quản lý trạng thái trận đấu phía Server. | Thành viên 4 |
| **05** | **Game Logic & Quản lý Trận đấu (Module 2)** | Phối hợp hoàn thiện logic cờ vua, kiểm soát tính hợp lệ của nước đi, trạng thái trận đấu, chức năng ghép trận và đồng bộ thời gian thực giữa 2 client. | Thành viên 5 |

---

## 🏗️ 4. Kiến trúc hệ thống & Cấu trúc thư mục

Hệ thống được tổ chức theo mô hình **Client - Server**:

```text
Chess-Game-NT106/
├── ChessClient/          # Giao diện Windows Forms người dùng, xử lý thao tác bàn cờ
├── ChessSever/           # Ứng dụng Server quản lý kết nối TCP, phòng đấu, logic và DB
├── Shared/               # Thư viện lớp dùng chung (Giao thức mạng, Packet, DTO, Enums)
├── DataBase/             # Chứa script khởi tạo cơ sở dữ liệu
│   └── MainDataBase.sql  # Script tạo cấu trúc bảng, khóa chính/ngoại, index
├── OnlineChess.slnx      # Solution quản lý toàn bộ dự án
└── README.md             # Tài liệu hướng dẫn dự án
```

### 📡 Giao thức truyền thông
- **Mô hình kết nối:** TCP Socket kết nối liên tục (Persistent Connection).
- **Cơ chế xử lý:** Server lắng nghe đa luồng (`Multi-threaded / Asynchronous Socket`) để xử lý đồng thời nhiều Client.
- **Dữ liệu trao đổi:** Đóng gói dạng chuỗi/packet chuẩn hóa trong `Shared`, hỗ trợ phân tích và phản hồi trạng thái nhanh chóng.

---

## 🛠️ 5. Công nghệ sử dụng

- **Ngôn ngữ lập trình:** C# (.NET Framework / .NET Core)
- **Giao diện người dùng (UI):** Windows Forms (WinForms)
- **Giao thức mạng:** TCP Socket (System.Net.Sockets)
- **Hệ quản trị CSDL:** Microsoft SQL Server
- **Công cụ phát triển:** Visual Studio 2022 / JetBrains Rider, SQL Server Management Studio (SSMS)

---

## 🚀 6. Hướng dẫn cài đặt và khởi chạy

### Bước 1: Chuẩn bị môi trường
- Đã cài đặt [Visual Studio 2022](https://visualstudio.microsoft.com/) (có workload **.NET desktop development**).
- Đã cài đặt [Microsoft SQL Server](https://www.microsoft.com/en-us/sql-server) và [SSMS](https://learn.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms).

### Bước 2: Khởi tạo Cơ sở dữ liệu
1. Mở SQL Server Management Studio (SSMS) và kết nối tới server SQL của bạn.
2. Mở file [MainDataBase.sql](file:///c:/Users/doanh.LUCK/OneDrive/Documents/ChatSkibidi%20and%20Gehihi/NT106_ChessGame_Nhom10/Chess-Game-NT106/DataBase/MainDataBase.sql).
3. Thực thi (Execute) script để tạo cơ sở dữ liệu và các bảng liên quan.
4. Kiểm tra chuỗi kết nối (`Connection String`) trong file cấu hình của `ChessSever` cho khớp với SQL Server cục bộ của bạn.

### Bước 3: Mở và chạy ứng dụng
1. Mở solution `OnlineChess.slnx` bằng Visual Studio.
2. Build toàn bộ Solution (`Ctrl + Shift + B`).
3. **Khởi chạy Server:** Chuột phải vào project `ChessSever` -> Chọn **Debug** -> **Start New Instance** (hoặc chạy file `.exe` đã build).
4. **Khởi chạy Client:** Chuột phải vào project `ChessClient` -> Chọn **Debug** -> **Start New Instance** (có thể mở 2 Client cùng lúc để test ghép trận giữa 2 tài khoản).

---

## 🎯 7. Mục tiêu đồ án

- Áp dụng kiến thức nền tảng về lập trình mạng (TCP/IP Socket, giao thức truyền tin, truyền nhận dữ liệu bất đồng bộ).
- Hiện thực hóa một trò chơi hoàn chỉnh với logic phức tạp, đòi hỏi độ chính xác cao về tính toàn vẹn dữ liệu và đồng bộ trạng thái.
- Rèn luyện kỹ năng làm việc nhóm, thiết kế CSDL, phân chia module và tích hợp hệ thống.
