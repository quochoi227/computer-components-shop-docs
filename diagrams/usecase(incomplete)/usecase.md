# Sơ đồ Use Case — Computer Components Shop with AI Integration

## Tổng quan các Actor

| Actor | Mô tả |
|-------|-------|
| **Guest** | Người dùng chưa đăng nhập |
| **User** | Người dùng đã đăng nhập |
| **Admin** | Quản trị viên hệ thống |
| **Gemini AI** | Google Gemini API (hệ thống ngoài) |

---

## Mô tả Use Case — Bảng tóm tắt

### Guest

| Use Case | Mô tả | Endpoint |
|----------|-------|----------|
| Xem danh sách sản phẩm | Duyệt sản phẩm có lọc, tìm kiếm, phân trang | `GET /api/products` |
| Xem chi tiết sản phẩm | Xem thông số kỹ thuật, hình ảnh, giá | `GET /api/products/{id}` |
| Tìm kiếm / Lọc sản phẩm | Lọc theo category, giá; tìm theo tên | `GET /api/products?...` |
| Đăng ký tài khoản | Tạo tài khoản mới | `POST /api/auth/register` |
| Đăng nhập | Xác thực, nhận JWT + Refresh Token | `POST /api/auth/login` |
| Sử dụng chatbot AI | Hỏi chính sách hoặc xin gợi ý cấu hình PC | `POST /api/chat` |

### User (thêm vào quyền Guest)

| Use Case | Mô tả | Endpoint |
|----------|-------|----------|
| Đăng xuất | Thu hồi Refresh Token | `POST /api/auth/logout` |
| Làm mới Access Token | Dùng Refresh Token để lấy AT mới | `POST /api/auth/refresh` |
| Xem giỏ hàng | Danh sách sản phẩm trong giỏ | `GET /api/cart` |
| Thêm vào giỏ hàng | Thêm sản phẩm vào giỏ | `POST /api/cart/items` |
| Cập nhật số lượng | Thay đổi số lượng sản phẩm trong giỏ | `PUT /api/cart/items/{id}` |
| Xóa khỏi giỏ hàng | Xóa sản phẩm khỏi giỏ | `DELETE /api/cart/items/{id}` |
| Đặt hàng (COD) | Tạo đơn hàng từ giỏ hàng | `POST /api/orders` |
| Xem lịch sử đơn hàng | Danh sách đơn hàng của chính mình | `GET /api/orders` |
| Xem chi tiết đơn hàng | Thông tin chi tiết 1 đơn | `GET /api/orders/{id}` |
| Hủy đơn hàng | Hủy đơn ở trạng thái PENDING | `PUT /api/orders/{id}/cancel` |

### Admin (thêm vào quyền User)

| Use Case | Mô tả | Endpoint |
|----------|-------|----------|
| Thêm sản phẩm mới | Tạo sản phẩm kèm upload ảnh Cloudinary/S3 | `POST /api/products` |
| Cập nhật sản phẩm | Sửa thông tin, ảnh sản phẩm | `PUT /api/products/{id}` |
| Xóa sản phẩm | Soft delete sản phẩm | `DELETE /api/products/{id}` |
| Xem tất cả đơn hàng | Quản lý toàn bộ đơn hàng | `GET /api/admin/orders` |
| Cập nhật trạng thái đơn hàng | Chuyển PENDING→CONFIRMED→SHIPPING→DELIVERED | `PUT /api/admin/orders/{id}/status` |
| Tạo PC Case mới | Chọn linh kiện + tự động kiểm tra tương thích | `POST /api/admin/pc-cases` |
| Cập nhật PC Case | Chỉnh sửa linh kiện trong PC Case | `PUT /api/admin/pc-cases/{id}` |
| Xóa PC Case | Xóa PC Case | `DELETE /api/admin/pc-cases/{id}` |
| Upload tài liệu RAG | Upload PDF/DOCX/TXT cho chatbot chính sách | `POST /api/admin/rag/documents` |
| Xem danh sách tài liệu RAG | Liệt kê tài liệu đã upload | `GET /api/admin/rag/documents` |
| Xóa tài liệu RAG | Xóa tài liệu khỏi hệ thống RAG | `DELETE /api/admin/rag/documents/{id}` |
