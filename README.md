# Online Chess

> Đồ án game cờ vua trực tuyến được xây dựng theo mô hình Client - Server.

## Tổng quan

Online Chess cho phép người chơi đăng ký tài khoản, đăng nhập và ghép trận để thi đấu cờ vua trực tuyến. Dự án cũng tích hợp các tính năng hỗ trợ nhằm nâng cao trải nghiệm người dùng trong quá trình chơi.

## Tính năng chính

- Đăng ký và đăng nhập tài khoản
- Ghép trận thi đấu trực tuyến
- Chơi cờ vua giữa hai người chơi
- Trò chuyện trong quá trình thi đấu
- Xem lịch sử các trận đấu
- Bảng xếp hạng người chơi

## Kiến trúc dự án

Dự án được tổ chức theo mô hình Client - Server, gồm các thành phần chính:

- **ChessClient**: Ứng dụng phía người chơi, cung cấp giao diện và các chức năng tương tác.
- **ChessSever**: Ứng dụng máy chủ, xử lý kết nối và logic của trò chơi.
- **Shared**: Chứa các thành phần được sử dụng chung giữa Client và Server.
- **DataBase**: Chứa tập lệnh khởi tạo cơ sở dữ liệu.

## Công nghệ sử dụng

- C# / .NET
- Mô hình Client - Server
- Cơ sở dữ liệu quan hệ

## Cài đặt và chạy dự án

1. Clone repository.
2. Chạy file `OnlineChess.slnx` bằng Visual Studio.
3. Khởi tạo cơ sở dữ liệu bằng script trong thư mục `DataBase`.
4. Chạy `ChessSever` trước rồi sau đó chạy `ChessClient`.

## Mục tiêu

Xây dựng một nền tảng cờ vua trực tuyến có khả năng hỗ trợ thi đấu, giao tiếp và quản lý thông tin trận đấu giữa những người chơi phù hợp với các tiêu chí của môn học cũng như hướng đến cân bằng ở sự đóng góp của các thành viên.
