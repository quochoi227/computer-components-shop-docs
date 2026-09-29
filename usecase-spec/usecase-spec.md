<!-- Format của một use case -->
# Ví dụ use case Đăng nhập
| Use case | Nội dung |
|--- | --- |
| Tên use case | Đăng nhập |
| Mô tả | Use case cho phép người dùng dùng đăng nhập vào hệ thống để thực hiện chức năng của mình |
| Actor | Người dùng |
| Điều kiện kích hoạt | Khi người dùng chọn chức năng đăng nhập từ trang chủ của hệ thống |
| Tiền điều kiện | Người dùng đã có tài khoản trong hệ thống |
| Hậu điều kiện | Người dùng được xác thực và truy cập vào hệ thống |
| Luồng sự kiện chính | 1. Hệ thống hiển thị màn hình đăng nhập <br> 2. Người dùng nhập tên đăng nhập và mật khẩu <br> 3. Hệ thống kiểm tra thông tin đăng nhập <br> 4. Nếu thành công, hệ thống hiển thị màn hình đăng nhập thành công <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Thông tin đăng nhập không hợp lệ**: người dùng nhập sai thông tin đăng nhập <br> 1. Hệ thống hiển thị lại màn hình đăng nhập để người dùng nhập lại thông tin kèm theo thông báo tên đăng nhập hoặc mật khẩu bị sai <br> 2. Quay lại bước 2 trong luồng sự kiện chính <br> **A2 - Quên mật khẩu**: người dùng chọn chức năng quên mật khẩu trên màn hình đăng nhập <br> 1. Hệ thống hiển thị màn hình để người dùng nhập email <br> 2. Người dùng nhập email và chọn nút chức năng Đặt lại mật khẩu <br> 3. Hệ thống kiểm tra email và gửi liên kết reset mật khẩu cho người dùng qua email <br> 4. Hệ thống hiển thị thông báo thành công <br> 5. Use case kết thúc |

# Chức năng 1
