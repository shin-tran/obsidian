### 1. Tổng quan công nghệ (Tech Stack)
- **Backend:** PHP thuần (Native PHP) xây dựng theo mô hình **MVC tự triển khai (Custom MVC)**, không sử dụng framework lớn (như Laravel hay Symfony).
- **Frontend:** TypeScript (được biên dịch sang JS), TailwindCSS (sử dụng plugin DaisyUI).
- **Database:** MySQL (sử dụng thư viện PDO trong `App\Core\Database`).
- **Công cụ Build & Quản lý gói:** Bun (hoặc NPM), Composer (cho PHP dependencies như `phpmailer`, `php-jwt`).
### 2. Cấu trúc hệ thống (Backend)
- **Core:**
    - `Router.php`: Xử lý định tuyến dựa trên Regex, hỗ trợ Middleware (Auth, Guest, Permission, Sanitize).
    - `Database.php`: Wrapper cho PDO, xử lý kết nối và các phương thức CRUD cơ bản, có ghi log lỗi.
    - `View.php`: Render giao diện từ thư mục `app/Views`.
- **Authentication (Xác thực):**
    - Sử dụng cơ chế **JWT (JSON Web Token)** cho Access Token và **Cookie** cho Refresh Token.
    - Có đầy đủ quy trình: Đăng ký (gửi mail kích hoạt), Đăng nhập, Quên mật khẩu, Đăng xuất, Refresh Token.
- **Controllers:** Chia thành 2 nhóm chính:
    - `Controllers`: Xử lý render giao diện HTML (PageController, DashboardController...).
    - `Controllers/Api`: Xử lý logic nghiệp vụ và trả về JSON (ApiController, ProductController, OrderController...).
### 3. Frontend & Logic Client-side
- **TypeScript:** Code được tổ chức trong `resources/ts`.
    - Logic giỏ hàng, thanh toán, địa chỉ được tách thành các class quản lý riêng: `CartManager`, `CheckoutManager`, `AddressManager`.
    - Sử dụng `authService` để gọi API (fetchWithAuth) và tự động xử lý Refresh Token khi Access Token hết hạn (401 Unauthorized).
- **Giao diện:** Layout chia thành `main` (cho khách) và `dashboard` (cho admin), sử dụng các components của DaisyUI.
### 4. Cơ sở dữ liệu (Database Schema)
Dự án bao gồm các bảng chính:
- `users` & `user_addresses`: Quản lý thông tin người dùng và nhiều địa chỉ giao hàng.
- `roles` & `role_user`: Phân quyền (Admin/Customer).
- `products` & `categories`: Sản phẩm và danh mục.
- `orders` & `order_details`: Quản lý đơn hàng và chi tiết sản phẩm trong đơn.
- `reviews`: Đánh giá sản phẩm.
- `shipping_config`: Cấu hình phí vận chuyển động.
### 5. Các tính năng nghiệp vụ chính
- **Đặt hàng:** Lưu giỏ hàng ở LocalStorage -> API kiểm tra tồn kho -> Tạo đơn hàng -> Trừ tồn kho.
- **Quản lý đơn hàng:** Luồng trạng thái: `pending` -> `packing` -> `shipping` -> `completed` (hoặc `cancelled`). Nếu hủy đơn sẽ hoàn lại số lượng tồn kho.
- **Dashboard Admin:** Thống kê doanh thu, quản lý người dùng, sản phẩm, danh mục và xử lý đơn hàng

