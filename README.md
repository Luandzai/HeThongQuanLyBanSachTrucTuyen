# Hệ Thống Bán Sách Trực Tuyến (Online Book Store)

## Giới thiệu (Overview)
Dự án "Hệ Thống Bán Sách Trực Tuyến" là một ứng dụng thương mại điện tử hoàn chỉnh, được thiết kế để cung cấp trải nghiệm mua sắm sách tiện lợi cho người dùng và cung cấp các công cụ quản lý mạnh mẽ cho quản trị viên. Hệ thống được xây dựng theo mô hình kiến trúc Client-Server với API mạnh mẽ, đảm bảo hiệu suất cao, dễ bảo trì và khả năng mở rộng tốt.

## Tính năng nổi bật (Features)

### Dành cho người dùng (Customer)
- Xác thực & Bảo mật: Đăng ký, đăng nhập an toàn với tính năng mã hóa mật khẩu (BCrypt) và giao tiếp qua JWT (JSON Web Token).
- Quản lý tài khoản: Cập nhật thông tin cá nhân, đổi mật khẩu, chức năng quên mật khẩu (xử lý gửi qua Email tự động).
- Tìm kiếm & Chọn lọc sách: Tìm kiếm sách trực quan theo tiêu đề, danh mục, tác giả, và nhà xuất bản.
- Giỏ hàng & Thanh toán: Thêm/xoá/sửa sản phẩm trong giỏ hàng, tính phí vận chuyển theo khu vực, áp dụng mã giảm giá linh hoạt (Coupon/Discount).
- Quản lý đơn hàng: Trải nghiệm thanh toán mượt mà, theo dõi lịch sử mua hàng, trạng thái và chi tiết từng đơn đặt hàng.
- Đánh giá & Phản hồi: Để lại đánh giá (Reviews) và bình luận về những cuốn sách đã mua.

### Dành cho Quản trị viên (Admin)
- Dashboard Thống kê: Theo dõi biểu đồ doanh thu, số lượng đơn hàng, và phân tích hiệu suất kinh doanh (Revenue reporting).
- Quản lý Sản phẩm (Sách): CRUD (Thêm mới, chỉnh sửa, ẩn/hiện thao tác xoá mềm, cập nhật thông tin sách) cùng hệ thống ảnh và file upload.
- Quản lý Đơn hàng: Kiểm soát trạng thái đơn trong quá trình luân chuyển (chờ duyệt, đang đóng gói, đang giao, đã hoàn thành, đã hủy).
- Quản lý Người dùng: Chặn/mở khóa tài khoản khách hàng, quản trị danh sách người dùng trên hệ thống.
- Quản lý Khuyến mãi: Tạo mã giảm giá (Discount Codes), quản lý thời hạn và số lượng sử dụng cho từng người dùng đặc thù.
- Quản trị cấu hình: Quản trị phí vận chuyển và các danh mục/thể loại (Categories).

## Công nghệ sử dụng (Technology Stack)

### Back-end (RESTful API)
- Framework: ASP.NET Core 9.0 (Web API)
- Ngôn ngữ lập trình: C#
- ORM: Entity Framework Core 9.0
- Database: Microsoft SQL Server
- Authentication & Authorization: JWT (JSON Web Token), Role-based Authorization Policy.
- Security: BCrypt.Net-Next (Băm và đối chiếu mật khẩu)
- Dịch vụ tích hợp bên thứ ba: MailKit (Gửi email OTP và thông báo), Swagger/OpenAPI (Tự động biên dịch tài liệu API Endpoint).
- Architecture: Mô hình Controller-Service phân tầng, tiêm phụ thuộc (Dependency Injection), cấu hình CORS đầy đủ.

### Front-end (Client UI)
- Công nghệ: HTML5, CSS3, JavaScript (Vanilla JS ES6+)
- Kiến trúc: Thiết kế hoàn toàn tĩnh, sử dụng Fetch API kết nối với API backend, đảm bảo Decoupled Architecture.
- Giao diện: Thiết kế giao diện tuỳ chỉnh tương thích trên đa nền tảng thiết bị (Responsive Design/Mobile-Friendly).

## Cơ sở dữ liệu (Database Schema)
Hệ thống sử dụng cơ sở dữ liệu quan hệ SQL Server được thiết kế tối ưu, đạt chuẩn hoá, bao gồm các cụm bảng chính:
- Tài khoản: `Users`, `Roles` (Quản lý cấp quyền).
- Sản phẩm: `Books`, `Categories`, `Authors`, `Publishers` (Thiết lập kho tàng khoa học).
- Thương mại: `Carts`, `Discounts`, `UserDiscounts`, `Reviews`.
- Giao dịch: `Orders`, `OrderDetails`, `Payments`, `ShippingFees`, `Transactions`, `Revenues`.

> *Toàn bộ cấu trúc thực thể đã được thiết lập qua Code-First Entity Framework tích hợp script CSDL có sẵn (`SQLQuery20.sql`).*

## Hướng dẫn cài đặt và chạy dự án (Getting Started)

### 1. Yêu cầu hệ thống (Prerequisites)
- [.NET 9.0 SDK](https://dotnet.microsoft.com/download/dotnet/9.0)
- [SQL Server](https://www.microsoft.com/en-us/sql-server/sql-server-downloads) & SQL Server Management Studio (SSMS)
- [Visual Studio 2022](https://visualstudio.microsoft.com/) hoặc VS Code
- Trình duyệt web hiện đại (Chrome, Edge, Firefox, Safari)

### 2. Cài đặt Cơ sở dữ liệu (Database Setup)
1. Mở SSMS, kết nối tới Server SQL Server trên thiết bị cục bộ của bạn.
2. Mở file `SQLQuery20.sql` (nằm ở ngoài cùng thư mục gốc của dự án).
3. Chạy lệnh truy vấn (Execute) kịch bản SQL này để tự động tạo cơ sở dữ liệu `OnlineBookStore` với đầy đủ các bảng dữ liệu liên quan.

### 3. Cài đặt và Chạy Back-end
1. Điều hướng tới thư mục chứa Backend: `OnlineBookStore/Back-end/BookStoreApi`.
2. Mở file `appsettings.json` và cấu hình lại chuỗi kết nối (ConnectionString) thiết lập phù hợp với tên hệ thống máy của bạn:
   ```json
   "ConnectionStrings": {
     "DefaultConnection": "Server=YOUR_SERVER_NAME;Database=OnlineBookStore;Trusted_Connection=True;MultipleActiveResultSets=true;TrustServerCertificate=True"
   }
   ```
3. *(Tùy chọn)* Cấu hình tham số gửi Email từ hệ thống vào phần `EmailSettings` cũng ở trong file cấu hình json.
4. Mở cửa sổ terminal từ thư mục đó, và khôi phục các Packages:
   ```bash
   dotnet restore
   ```
5. Khởi chạy Server:
   ```bash
   dotnet run
   ```
6. Truy cập địa chỉ URL được sinh ra, (VD: `https://localhost:<port>/swagger`) để mở Swagger UI xem và thử nghiệm toàn bộ API của dự án.

### 4. Khởi chạy Front-end
Do Front-end sử dụng mã HTML/JS thuần (dạng tĩnh):
1. Điều hướng vào thư mục phân vùng người dùng: `OnlineBookStore/Front-end/html`.
2. Mở thẳng file `index.html` trong trình duyệt web để kích hoạt màn hình Trang chủ của trang web. Hoặc tốt nhất, cài đặt và mở bằng **Live Server** extension trong VS Code để tạo host ảo trên máy.

## Hình ảnh minh họa (Screenshots)

---
*Dự án được xây dựng và thiết kế nhằm mục đích hoàn thiện quá trình nghiên cứu & phát triển học thuật. Phù hợp cho việc trình diễn kỹ năng xây dựng Web API và Full-stack Web Development.*
