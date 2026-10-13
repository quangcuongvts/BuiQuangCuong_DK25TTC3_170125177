# Mini Football Booking

Hệ thống đặt sân bóng mini trực tuyến. Website quản lý sân, lịch, giá theo khung giờ, đặt sân, thanh toán, check-in/check-out, voucher, đánh giá và báo cáo doanh thu.

## Công nghệ

- ASP.NET Core MVC 8
- Entity Framework Core 8 + SQL Server
- ASP.NET Core Identity (mật khẩu được băm, không lưu plain text)
- Razor, Bootstrap 5, Chart.js, SweetAlert2, Bootstrap Icons

## Chức năng chính

- Khách chưa đăng nhập xem sân, lịch trống, giá, khuyến mãi, bài viết và liên hệ. Bấm đặt sân sẽ chuyển tới đăng nhập.
- Khách hàng tìm sân, đặt sân, áp voucher, thanh toán (tiền mặt, chuyển khoản, QR, VNPay mô phỏng), xem lịch sử, hủy, đổi giờ và đánh giá sau khi hoàn thành trận.
- Nhân viên xem ca trong ngày, tạo booking tại quầy, check-in, bắt đầu trận, check-out, thu tiền và thêm dịch vụ.
- Quản lý quản lý sân, loại sân, bảng giá, lịch, booking, dịch vụ, voucher, bảo trì, đánh giá và báo cáo.
- Quản trị viên quản lý người dùng, vai trò, bài viết, banner, liên hệ, cấu hình, audit log và dashboard.

Không đặt trùng khung giờ. Giá lấy từ bảng `PriceRule` (giờ thường, cao điểm, cuối tuần). Hủy trước 24 giờ hoàn 100%, từ 6 đến 24 giờ hoàn 50%, dưới 6 giờ không hoàn tiền.

## Phân quyền

| Vai trò | Email | Mật khẩu |
|---|---|---|
| Admin | admin@football.com | Admin@123 |
| Manager | manager@football.com | Manager@123 |
| Staff | staff@football.com | Staff@123 |
| Staff | staff2@football.com | Staff@123 |
| Staff | staff3@football.com | Staff@123 |
| Customer | customer@football.com | Customer@123 |

Các tài khoản `customer02@football.com` đến `customer18@football.com` dùng mật khẩu `Customer@123`.

Khách vãng lai tạo tại quầy có mật khẩu tạm `Walkin@123`.

Voucher mẫu: `NEWUSER50` (giảm 50.000đ, đơn từ 300.000đ), `FOOTBALL10` (giảm 10%, tối đa 100.000đ), `WEEKEND100` (giảm 100.000đ, đơn từ 500.000đ), `VIP20` (giảm 20%, tối đa 200.000đ). Mỗi khách dùng một mã một lần.

## Cài đặt

Cài [.NET SDK 8](https://dotnet.microsoft.com/download/dotnet/8.0) và SQL Server (bản đầy đủ hoặc LocalDB). Mở terminal tại thư mục này:

```bash
cd MiniFootballBooking
dotnet restore
dotnet ef database update
dotnet run
```

Ứng dụng lắng nghe `http://localhost:5196`. Lần chạy đầu cũng tự áp dụng migration và nạp dữ liệu mẫu, nên có thể demo ngay sau `dotnet run`.

Chuỗi kết nối nằm trong `MiniFootballBooking/appsettings.json`:

```json
"DefaultConnection": "Server=localhost;Database=MiniFootballBookingDB;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=True;"
```

Nếu dùng LocalDB, đổi thành:

```text
Server=(localdb)\MSSQLLocalDB;Database=MiniFootballBookingDB;Trusted_Connection=True;TrustServerCertificate=True;MultipleActiveResultSets=True;
```

Quên mật khẩu trong đồ án không gửi email. Sau khi nhập email, trang sẽ hiện liên kết đặt lại mật khẩu.

## VS Code

Mở thư mục dự án bằng VS Code, cài extension C# Dev Kit hoặc C#, rồi bấm F5 với cấu hình **Mini Football Booking**. Không cần Visual Studio.
