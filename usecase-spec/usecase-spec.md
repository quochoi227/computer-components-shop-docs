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

<!-- Xác thực -->
# Đăng ký tài khoản
| Use case | Nội dung |
|--- | --- |
| Tên use case | Đăng ký tài khoản |
| Mô tả | Cho phép khách vãng lai đăng ký tài khoản mới để trở thành thành viên (User) trong hệ thống |
| Actor | Khách vãng lai (Guest) |
| Điều kiện kích hoạt | Người dùng chọn chức năng "Đăng ký" trên thanh điều hướng |
| Tiền điều kiện | Người dùng chưa đăng nhập |
| Hậu điều kiện | Tài khoản mới được lưu vào bảng `users` với vai trò `USER`, mật khẩu được mã hóa an toàn |
| Luồng sự kiện chính | 1. Người dùng chọn nút "Đăng ký" trên thanh điều hướng <br> 2. Hệ thống hiển thị biểu mẫu đăng ký (họ tên, email, mật khẩu, số điện thoại, địa chỉ) <br> 3. Người dùng nhập đầy đủ thông tin và nhấn nút "Đăng ký" <br> 4. Hệ thống kiểm tra dữ liệu hợp lệ (email đúng định dạng, mật khẩu >= 6 ký tự) và kiểm tra email chưa tồn tại trong hệ thống <br> 5. Hệ thống mã hóa mật khẩu bằng BCrypt và lưu người dùng mới vào cơ sở dữ liệu <br> 6. Hệ thống hiển thị thông báo đăng ký thành công và chuyển hướng sang trang đăng nhập <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Email đã được sử dụng**: <br> 1. Ở bước 4, nếu email đã tồn tại, hệ thống thông báo lỗi "Email đã được sử dụng" <br> 2. Quay lại bước 3 của luồng chính <br> **A2 - Dữ liệu nhập không hợp lệ**: <br> 1. Ở bước 4, nếu thiếu thông tin bắt buộc hoặc mật khẩu quá ngắn, hệ thống thông báo yêu cầu nhập lại <br> 2. Quay lại bước 3 của luồng chính |

# Đăng nhập
| Use case | Nội dung |
|--- | --- |
| Tên use case | Đăng nhập |
| Mô tả | Cho phép người dùng đã có tài khoản đăng nhập vào hệ thống để mua sắm và sử dụng các tính năng thành viên |
| Actor | Khách hàng (User), Quản trị viên (Admin) |
| Điều kiện kích hoạt | Người dùng chọn chức năng "Đăng nhập" trên thanh điều hướng |
| Tiền điều kiện | Người dùng đã có tài khoản trong hệ thống |
| Hậu điều kiện | Người dùng được xác thực, hệ thống cấp phát token JWT và cập nhật giao diện đã đăng nhập |
| Luồng sự kiện chính | 1. Người dùng chọn nút "Đăng nhập" trên thanh điều hướng <br> 2. Hệ thống hiển thị biểu mẫu đăng nhập gồm email và mật khẩu <br> 3. Người dùng nhập email, mật khẩu và nhấn nút "Đăng nhập" <br> 4. Hệ thống kiểm tra thông tin tài khoản và so khớp mật khẩu trong cơ sở dữ liệu <br> 5. Hệ thống cấp phát cặp token JWT (Access Token lưu phía client, Refresh Token lưu trong HttpOnly Cookie) <br> 6. Hệ thống thông báo đăng nhập thành công và chuyển hướng người dùng về trang chủ (hoặc trang quản trị nếu là Admin) <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Thông tin đăng nhập không chính xác**: <br> 1. Ở bước 4, nếu email hoặc mật khẩu không đúng, hệ thống hiển thị thông báo lỗi "Email hoặc mật khẩu không chính xác" <br> 2. Quay lại bước 3 của luồng chính |

# Đăng xuất
| Use case | Nội dung |
|--- | --- |
| Tên use case | Đăng xuất |
| Mô tả | Cho phép người dùng đang đăng nhập kết thúc phiên làm việc an toàn trên hệ thống |
| Actor | Khách hàng (User), Quản trị viên (Admin) |
| Điều kiện kích hoạt | Người dùng chọn mục "Đăng xuất" tại menu tài khoản |
| Tiền điều kiện | Người dùng đang ở trạng thái đã đăng nhập |
| Hậu điều kiện | Phiên làm việc kết thúc, Refresh Token trong cookie bị xóa bỏ và tài khoản chuyển về trạng thái khách |
| Luồng sự kiện chính | 1. Người dùng chọn chức năng "Đăng xuất" từ menu cá nhân <br> 2. Hệ thống gửi yêu cầu đăng xuất lên backend (`/api/auth/logout`) <br> 3. Hệ thống xóa Refresh Token khỏi Cookie và vô hiệu hóa phiên làm việc <br> 4. Hệ thống xóa token lưu trữ phía client, chuyển giao diện về trạng thái chưa đăng nhập và điều hướng về trang chủ <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | Không có |

<!-- Thống kê số liệu -->
# Xem thống kê doanh thu
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem thống kê doanh thu |
| Mô tả | Cho phép quản trị viên xem tổng doanh thu và biểu đồ doanh thu của cửa hàng theo ngày, tháng hoặc năm |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên chọn mục "Thống kê doanh thu" trên menu quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Dữ liệu và biểu đồ doanh thu được hiển thị đầy đủ trên màn hình |
| Luồng sự kiện chính | 1. Quản trị viên truy cập mục "Thống kê doanh thu" tại trang quản trị <br> 2. Hệ thống truy vấn tổng doanh thu từ các đơn hàng thành công (`DELIVERED`) theo mốc thời gian <br> 3. Hệ thống hiển thị tổng doanh thu lũy kế và biểu đồ doanh thu theo ngày/tháng/năm <br> 4. Quản trị viên có thể chọn khoảng thời gian tùy chỉnh để xem số liệu tương ứng <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Không có dữ liệu trong mốc thời gian**: <br> 1. Ở bước 3, nếu khoảng thời gian được chọn chưa có đơn hàng nào hoàn tất, hệ thống hiển thị doanh thu 0 VNĐ và biểu đồ trống <br> 2. Kết thúc use case |

# Xem sản phẩm bán chạy
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem sản phẩm bán chạy |
| Mô tả | Cho phép quản trị viên xem danh sách các sản phẩm linh kiện có số lượng bán ra cao nhất của cửa hàng |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên chọn mục "Sản phẩm bán chạy" tại trang thống kê quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Bảng xếp hạng các sản phẩm bán chạy nhất được hiển thị trên giao diện |
| Luồng sự kiện chính | 1. Quản trị viên chọn mục "Sản phẩm bán chạy" tại trang thống kê <br> 2. Hệ thống truy vấn số lượng đã bán của các sản phẩm từ các đơn hàng đã giao thành công (`DELIVERED`) <br> 3. Hệ thống sắp xếp giảm dần và hiển thị danh sách Top sản phẩm bán chạy (hình ảnh, tên linh kiện, category, số lượng đã bán, tổng doanh thu tạo ra) <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chưa có dữ liệu bán hàng**: <br> 1. Ở bước 2, nếu cửa hàng chưa có đơn hàng hoàn tất nào, hệ thống thông báo "Chưa có dữ liệu sản phẩm bán ra" <br> 2. Kết thúc use case |

# Xem thống kê người dùng mới
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem thống kê người dùng mới |
| Mô tả | Cho phép quản trị viên theo dõi số lượng tài khoản người dùng đăng ký mới theo thời gian |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên chọn mục "Thống kê người dùng" tại trang quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Số liệu và biểu đồ tăng trưởng người dùng mới được hiển thị |
| Luồng sự kiện chính | 1. Quản trị viên chọn mục "Thống kê người dùng" tại dashboard quản trị <br> 2. Hệ thống truy vấn số lượng tài khoản đăng ký mới trong bảng `users` theo mốc thời gian (ngày, tuần, tháng) <br> 3. Hệ thống hiển thị tổng số người dùng hiện có và biểu đồ tăng trưởng người dùng mới theo thời gian <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | Không có |

# Xem thống kê đơn hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem thống kê đơn hàng |
| Mô tả | Cho phép quản trị viên theo dõi tổng số lượng đơn hàng và tỷ lệ phân bố theo các trạng thái xử lý |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên chọn mục "Thống kê đơn hàng" tại trang quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Biểu đồ và bảng số liệu đơn hàng theo trạng thái được hiển thị |
| Luồng sự kiện chính | 1. Quản trị viên chọn mục "Thống kê đơn hàng" tại trang quản trị <br> 2. Hệ thống tổng hợp số lượng đơn hàng từ bảng `orders` theo từng trạng thái (`PENDING`, `CONFIRMED`, `SHIPPING`, `DELIVERED`, `CANCELLED`) <br> 3. Hệ thống hiển thị tổng số đơn hàng cùng biểu đồ tròn thể hiện tỷ lệ phần trăm của từng trạng thái <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | Không có |

<!-- Quản lý sản phẩm -->
# Thêm sản phẩm mới
| Use case | Nội dung |
|--- | --- |
| Tên use case | Thêm sản phẩm mới |
| Mô tả | Cho phép quản trị viên thêm một sản phẩm linh kiện máy tính mới vào kho hàng kèm thông số kỹ thuật chi tiết và hình ảnh |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Thêm sản phẩm" tại trang Quản lý sản phẩm |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Sản phẩm mới được tạo trong bảng `products` với trạng thái `is_active = true` |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Thêm sản phẩm" tại trang quản lý sản phẩm <br> 2. Hệ thống hiển thị biểu mẫu thêm sản phẩm: thông tin chung (tên, giá, tồn kho, category, mô tả, ảnh) và các ô nhập thông số kỹ thuật riêng theo category (JSONB) <br> 3. Quản trị viên nhập thông tin, chọn tệp hình ảnh và nhấn nút "Lưu" <br> 4. Hệ thống tải ảnh lên dịch vụ lưu trữ (Cloudinary) lấy URL và kiểm tra tính hợp lệ của dữ liệu <br> 5. Hệ thống lưu sản phẩm mới vào cơ sở dữ liệu và hiển thị thông báo thêm thành công <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Dữ liệu nhập không hợp lệ**: <br> 1. Ở bước 4, nếu thiếu thông tin bắt buộc hoặc giá/số lượng tồn kho âm, hệ thống thông báo lỗi yêu cầu sửa lại <br> 2. Quay lại bước 3 của luồng chính <br> **A2 - Lỗi tải ảnh lên Cloudinary**: <br> 1. Ở bước 4, nếu upload ảnh thất bại, hệ thống thông báo "Tải ảnh thất bại, vui lòng thử lại" <br> 2. Quay lại bước 3 của luồng chính |

# Cập nhật sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Cập nhật sản phẩm |
| Mô tả | Cho phép quản trị viên chỉnh sửa thông tin, giá bán, số lượng tồn kho hoặc thông số kỹ thuật của sản phẩm đã có |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Sửa" tại dòng sản phẩm cần chỉnh sửa |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` và sản phẩm cần sửa đang tồn tại |
| Hậu điều kiện | Thông tin sản phẩm được cập nhật lại trong cơ sở dữ liệu |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Sửa" tại sản phẩm muốn chỉnh sửa trong danh sách <br> 2. Hệ thống hiển thị biểu mẫu chứa toàn bộ thông tin hiện tại của sản phẩm <br> 3. Quản trị viên thay đổi các trường thông tin cần cập nhật (giá, tồn kho, mô tả, thông số kỹ thuật, tải ảnh mới nếu cần) và nhấn "Cập nhật" <br> 4. Hệ thống kiểm tra dữ liệu hợp lệ (upload ảnh mới nếu có) <br> 5. Hệ thống lưu các thay đổi vào bảng `products` và hiển thị thông báo cập nhật thành công <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Dữ liệu cập nhật không hợp lệ**: <br> 1. Ở bước 4, nếu giá bán <= 0 hoặc số lượng tồn kho âm, hệ thống hiển thị cảnh báo lỗi <br> 2. Quay lại bước 3 của luồng chính |

# Xóa sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xóa sản phẩm |
| Mô tả | Cho phép quản trị viên xóa mềm sản phẩm (`is_active = false`) để ngừng kinh doanh mà không làm mất tính toàn vẹn dữ liệu đơn hàng cũ |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Xóa" tại dòng sản phẩm muốn ngừng kinh doanh |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` và sản phẩm tồn tại trong hệ thống |
| Hậu điều kiện | Trường `is_active` của sản phẩm được chuyển sang `false` |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Xóa" tại sản phẩm cần ngừng kinh doanh <br> 2. Hệ thống hiển thị hộp thoại xác nhận xóa sản phẩm <br> 3. Quản trị viên chọn xác nhận xóa <br> 4. Hệ thống cập nhật `is_active = false` cho sản phẩm trong cơ sở dữ liệu <br> 5. Hệ thống hiển thị thông báo xóa thành công và cập nhật lại danh sách hiển thị <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Quản trị viên hủy thao tác**: <br> 1. Ở bước 3, quản trị viên chọn "Hủy bỏ" trong hộp thoại xác nhận <br> 2. Hệ thống đóng hộp thoại và giữ nguyên sản phẩm <br> 3. Kết thúc use case |

<!-- Quản lý đơn hàng -->
# Xem tất cả đơn hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem tất cả đơn hàng |
| Mô tả | Cho phép quản trị viên theo dõi toàn bộ danh sách đơn hàng của khách hàng trên hệ thống kèm bộ lọc trạng thái |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên chọn mục "Quản lý đơn hàng" trên menu quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Danh sách toàn bộ đơn hàng trong hệ thống được hiển thị đầy đủ |
| Luồng sự kiện chính | 1. Quản trị viên chọn mục "Quản lý đơn hàng" <br> 2. Hệ thống truy vấn danh sách tất cả đơn hàng từ bảng `orders` (sắp xếp theo thời gian mới nhất) <br> 3. Hệ thống hiển thị danh sách đơn hàng gồm: mã đơn, tên khách hàng, ngày đặt, tổng tiền, phương thức COD, trạng thái đơn hàng và các nút hành động <br> 4. Quản trị viên có thể lọc danh sách theo từng trạng thái cụ thể (`PENDING`, `CONFIRMED`, `SHIPPING`, `DELIVERED`, `CANCELLED`) <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chưa có đơn hàng nào**: <br> 1. Ở bước 2, nếu hệ thống chưa có đơn hàng nào, hiển thị thông báo "Chưa có đơn hàng nào trong hệ thống" <br> 2. Kết thúc use case |

# Cập nhật trạng thái đơn hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Cập nhật trạng thái đơn hàng |
| Mô tả | Cho phép quản trị viên chuyển đổi trạng thái đơn hàng theo đúng quy trình xử lý giao nhận |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên thay đổi trạng thái trong danh sách lựa chọn (dropdown) của đơn hàng |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` và đơn hàng đang tồn tại |
| Hậu điều kiện | Trạng thái mới của đơn hàng được cập nhật vào bảng `orders` |
| Luồng sự kiện chính | 1. Tại trang Quản lý đơn hàng, quản trị viên chọn đơn hàng cần cập nhật trạng thái <br> 2. Quản trị viên chọn trạng thái mới từ ô dropdown (chuyển sang `CONFIRMED`, `SHIPPING`, `DELIVERED`, hoặc `CANCELLED`) <br> 3. Quản trị viên nhấn nút "Lưu thay đổi" <br> 4. Hệ thống kiểm tra quy tắc chuyển trạng thái hợp lệ và cập nhật trạng thái mới cho đơn hàng trong cơ sở dữ liệu <br> 5. Nếu chuyển sang `CANCELLED`, hệ thống tự động hoàn lại số lượng tồn kho của các linh kiện trong đơn <br> 6. Hệ thống hiển thị thông báo cập nhật thành công và làm mới danh sách đơn hàng <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chuyển đổi trạng thái không hợp lệ**: <br> 1. Ở bước 4, nếu đơn hàng đã ở trạng thái `DELIVERED` hoặc `CANCELLED` mà quản trị viên cố tình thay đổi, hệ thống cảnh báo "Không thể thay đổi trạng thái của đơn hàng đã hoàn tất hoặc đã hủy" <br> 2. Giữ nguyên trạng thái cũ và kết thúc use case |

<!-- Quản lý PC Case -->
# Tạo PC Case mới
| Use case | Nội dung |
|--- | --- |
| Tên use case | Tạo PC Case mới |
| Mô tả | Cho phép quản trị viên tạo một bộ cấu hình PC hoàn chỉnh bằng cách chọn các linh kiện thành phần và được hệ thống tự động kiểm tra ràng buộc tương thích trước khi lưu |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Tạo PC Case mới" tại trang Quản lý PC Case |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Bộ PC Case mới được tạo trong bảng `pc_cases` và liên kết với các linh kiện trong `pc_case_items` |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Tạo PC Case mới" tại trang quản trị <br> 2. Hệ thống hiển thị biểu mẫu tạo cấu hình gồm: tên cấu hình, mục đích sử dụng (gaming, học tập, đồ họa,...), mô tả và danh sách chọn linh kiện cho các slot (CPU, Mainboard, RAM, GPU, Storage, PSU, Case, CPU_Cooler) <br> 3. Quản trị viên chọn linh kiện cho từng slot, hệ thống tự động tính tổng giá tiền <br> 4. Quản trị viên nhấn nút "Lưu cấu hình" <br> 5. Hệ thống kích hoạt thuật toán kiểm tra các ràng buộc tương thích phần cứng (socket CPU/Mainboard, chuẩn RAM, kích thước vỏ case, công suất nguồn,...) và kiểm tra linh kiện phải còn tồn kho <br> 6. Nếu tất cả ràng buộc hợp lệ, hệ thống lưu PC Case mới vào cơ sở dữ liệu và hiển thị thông báo thành công <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Vi phạm ràng buộc tương thích phần cứng**: <br> 1. Ở bước 5, nếu các linh kiện không tương thích hoặc có linh kiện hết hàng trong kho, hệ thống từ chối lưu và hiển thị chi tiết danh sách các lỗi vi phạm <br> 2. Quản trị viên chọn lại linh kiện phù hợp và quay lại bước 4 của luồng chính |

# Xem danh sách PC Case
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem danh sách PC Case |
| Mô tả | Cho phép quản trị viên xem danh sách các bộ cấu hình PC Case đã được tạo trong hệ thống |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên chọn mục "Quản lý PC Case" trên menu quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Danh sách các bộ cấu hình PC Case được hiển thị đầy đủ trên màn hình |
| Luồng sự kiện chính | 1. Quản trị viên chọn mục "Quản lý PC Case" trên thanh điều hướng <br> 2. Hệ thống truy vấn danh sách các bộ PC Case từ cơ sở dữ liệu (`pc_cases` và `pc_case_items`) <br> 3. Hệ thống hiển thị danh sách cấu hình gồm: tên bộ máy, mục đích sử dụng, tổng giá thành, danh sách các linh kiện thành phần, trạng thái kích hoạt và các nút hành động (Sửa, Xóa) <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chưa có cấu hình nào**: <br> 1. Ở bước 2, nếu chưa có PC Case nào trong hệ thống, hiển thị thông báo "Chưa có cấu hình PC Case nào được tạo" kèm nút "Tạo cấu hình mới" <br> 2. Kết thúc use case |

# Cập nhật PC Case
| Use case | Nội dung |
|--- | --- |
| Tên use case | Cập nhật PC Case |
| Mô tả | Cho phép quản trị viên thay đổi thông tin hoặc thay thế các linh kiện trong một bộ PC Case và kiểm tra lại tương thích |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Sửa" tại dòng cấu hình PC Case cần chỉnh sửa |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` và PC Case cần sửa đang tồn tại |
| Hậu điều kiện | Thông tin và danh sách linh kiện mới của PC Case được cập nhật lại vào cơ sở dữ liệu |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Sửa" tại một bộ PC Case trong danh sách quản trị <br> 2. Hệ thống hiển thị biểu mẫu chứa toàn bộ thông tin và danh sách linh kiện hiện tại của bộ máy <br> 3. Quản trị viên chỉnh sửa thông tin (tên, mục đích, mô tả) hoặc chọn linh kiện thay thế khác <br> 4. Quản trị viên nhấn nút "Lưu thay đổi" <br> 5. Hệ thống thực hiện kiểm tra tính tương thích của bộ linh kiện mới <br> 6. Nếu tương thích hợp lệ, hệ thống cập nhật thông tin và tính lại tổng giá của PC Case trong cơ sở dữ liệu, sau đó thông báo thành công <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Linh kiện thay thế không tương thích**: <br> 1. Ở bước 5, nếu linh kiện mới vi phạm ràng buộc kỹ thuật hoặc hết hàng, hệ thống hiển thị danh sách lỗi vi phạm và từ chối cập nhật <br> 2. Quay lại bước 3 của luồng chính |

# Xóa PC Case
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xóa PC Case |
| Mô tả | Cho phép quản trị viên vô hiệu hóa hoặc xóa một bộ PC Case khỏi hệ thống để ngừng gợi ý cấu hình này |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Xóa" tại dòng PC Case muốn loại bỏ |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` và PC Case tồn tại trong hệ thống |
| Hậu điều kiện | PC Case được chuyển trạng thái ngừng hoạt động (`is_active = false`) |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Xóa" tại bộ PC Case không còn muốn sử dụng <br> 2. Hệ thống hiển thị hộp thoại xác nhận xóa PC Case <br> 3. Quản trị viên chọn xác nhận xóa <br> 4. Hệ thống cập nhật `is_active = false` (xóa mềm) cho bản ghi PC Case trong cơ sở dữ liệu <br> 5. Hệ thống hiển thị thông báo xóa thành công và cập nhật lại danh sách hiển thị <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Quản trị viên hủy thao tác**: <br> 1. Ở bước 3, quản trị viên chọn "Hủy bỏ" trong hộp thoại xác nhận <br> 2. Hệ thống đóng hộp thoại và giữ nguyên trạng thái cấu hình <br> 3. Kết thúc use case |

<!-- Quản lý tài liệu RAG -->
# Upload tài liệu RAG
| Use case | Nội dung |
|--- | --- |
| Tên use case | Upload tài liệu RAG |
| Mô tả | Cho phép quản trị viên tải lên các tệp tài liệu chính sách của cửa hàng (PDF, DOCX, TXT) để hệ thống tự động chia đoạn và nhúng vector vào cơ sở dữ liệu phục vụ RAG |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Upload tài liệu" tại trang Quản lý tài liệu RAG |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Tài liệu được lưu vào bảng `rag_documents`, các đoạn văn bản (chunks) và vector embedding được lưu vào bảng `rag_chunks` (pgvector) |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Upload tài liệu" tại giao diện Quản lý RAG <br> 2. Hệ thống hiển thị hộp thoại cho phép chọn tệp tin (định dạng PDF, DOCX, TXT) và nhập tiêu đề tài liệu <br> 3. Quản trị viên chọn tệp tài liệu và nhấn nút "Tải lên" <br> 4. Hệ thống đọc nội dung tệp, chia nhỏ thành các đoạn văn bản (chunks) có độ dài phù hợp <br> 5. Hệ thống gọi Gemini Embedding API để sinh vector embedding 768 chiều cho từng chunk <br> 6. Hệ thống lưu tài liệu vào bảng `rag_documents` và các chunks kèm vector vào bảng `rag_chunks` <br> 7. Hệ thống hiển thị thông báo tải lên và xử lý tài liệu RAG thành công <br> 8. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Định dạng tệp không hợp lệ**: <br> 1. Ở bước 4, nếu tệp không phải định dạng PDF, DOCX hoặc TXT, hệ thống hiển thị thông báo lỗi và từ chối tải lên <br> 2. Kết thúc use case <br> **A2 - Lỗi gọi API Embedding**: <br> 1. Ở bước 5, nếu gặp sự cố kết nối với Gemini Embedding API, hệ thống thông báo "Không thể tạo vector nhúng, vui lòng thử lại" và hủy bỏ thao tác <br> 2. Kết thúc use case |

# Xem danh sách tài liệu RAG
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem danh sách tài liệu RAG |
| Mô tả | Cho phép quản trị viên xem danh mục các tài liệu chính sách đã được nạp vào cơ sở tri thức của hệ thống RAG |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên truy cập mục "Quản lý tài liệu RAG" trên menu quản trị |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` |
| Hậu điều kiện | Danh sách tài liệu RAG được hiển thị đầy đủ trên màn hình |
| Luồng sự kiện chính | 1. Quản trị viên chọn mục "Quản lý tài liệu RAG" từ menu quản trị <br> 2. Hệ thống truy vấn danh sách tài liệu từ bảng `rag_documents` <br> 3. Hệ thống hiển thị bảng danh sách tài liệu gồm: tiêu đề tài liệu, tên tệp nguồn, ngày tải lên và nút thao tác xóa <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chưa có tài liệu nào**: <br> 1. Ở bước 2, nếu chưa có tài liệu nào trong hệ thống, hiển thị thông báo "Chưa có tài liệu chính sách nào trong hệ thống" kèm nút "Upload tài liệu" <br> 2. Kết thúc use case |

# Xóa tài liệu RAG
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xóa tài liệu RAG |
| Mô tả | Cho phép quản trị viên xóa một tài liệu chính sách cũ cùng toàn bộ các vector embedding liên quan khỏi hệ thống tri thức RAG |
| Actor | Quản trị viên (Admin) |
| Điều kiện kích hoạt | Quản trị viên nhấn nút "Xóa" tại dòng tài liệu muốn xóa trong danh sách tài liệu RAG |
| Tiền điều kiện | Quản trị viên đã đăng nhập với vai trò `ADMIN` và tài liệu cần xóa đang tồn tại |
| Hậu điều kiện | Bản ghi tài liệu và toàn bộ các chunks kèm vector embedding bị xóa hoàn toàn khỏi cơ sở dữ liệu |
| Luồng sự kiện chính | 1. Quản trị viên nhấn nút "Xóa" tại dòng tài liệu chính sách muốn loại bỏ <br> 2. Hệ thống hiển thị hộp thoại cảnh báo xác nhận xóa tài liệu và toàn bộ vector tri thức liên quan <br> 3. Quản trị viên chọn xác nhận xóa <br> 4. Hệ thống xóa các bản ghi chunks tương ứng trong bảng `rag_chunks` và xóa tài liệu trong bảng `rag_documents` <br> 5. Hệ thống hiển thị thông báo xóa thành công và cập nhật lại danh sách trên giao diện <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Quản trị viên hủy thao tác**: <br> 1. Ở bước 3, quản trị viên chọn "Hủy bỏ" trong hộp thoại xác nhận <br> 2. Hệ thống giữ nguyên tài liệu và đóng hộp thoại <br> 3. Kết thúc use case |

<!-- Giỏ hàng & Đặt hàng -->
# Thêm vào giỏ hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Thêm vào giỏ hàng |
| Mô tả | Cho phép người dùng thêm sản phẩm với số lượng mong muốn vào giỏ hàng cá nhân |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn nút "Thêm vào giỏ hàng" tại trang sản phẩm |
| Tiền điều kiện | Người dùng đã đăng nhập vào hệ thống; sản phẩm còn hàng trong kho (`stock_quantity > 0`) |
| Hậu điều kiện | Sản phẩm được thêm mới hoặc tăng số lượng trong giỏ hàng |
| Luồng sự kiện chính | 1. Người dùng chọn số lượng và nhấn nút "Thêm vào giỏ hàng" <br> 2. Hệ thống kiểm tra số lượng tồn kho của sản phẩm <br> 3. Hệ thống kiểm tra giỏ hàng: nếu sản phẩm đã có thì cộng dồn số lượng, nếu chưa thì thêm mới vào giỏ <br> 4. Hệ thống lưu giỏ hàng và hiển thị thông báo thêm thành công <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Số lượng vượt quá tồn kho**: <br> 1. Ở bước 2, nếu số lượng yêu cầu vượt quá số lượng còn trong kho, hệ thống thông báo lỗi "Số lượng vượt quá tồn kho" <br> 2. Kết thúc use case <br> **A2 - Người dùng chưa đăng nhập**: <br> 1. Nếu phát hiện chưa đăng nhập, hệ thống chuyển hướng sang trang Đăng nhập <br> 2. Kết thúc use case |

# Xem giỏ hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem giỏ hàng |
| Mô tả | Cho phép người dùng xem danh sách sản phẩm, số lượng, đơn giá và tổng số tiền tạm tính trong giỏ hàng |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn vào biểu tượng "Giỏ hàng" trên thanh điều hướng |
| Tiền điều kiện | Người dùng đã đăng nhập vào hệ thống |
| Hậu điều kiện | Màn hình giỏ hàng hiển thị đầy đủ thông tin các mặt hàng đã chọn |
| Luồng sự kiện chính | 1. Người dùng chọn biểu tượng Giỏ hàng <br> 2. Hệ thống truy vấn danh sách các mặt hàng trong giỏ của người dùng <br> 3. Hệ thống tính toán thành tiền từng món và tổng tiền tạm tính của giỏ hàng <br> 4. Hệ thống hiển thị giao diện giỏ hàng với thông tin sản phẩm, đơn giá, số lượng và tổng tiền <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Giỏ hàng trống**: <br> 1. Ở bước 2, nếu giỏ hàng chưa có sản phẩm nào, hệ thống hiển thị thông báo "Giỏ hàng của bạn đang trống" kèm nút điều hướng "Tiếp tục mua sắm" <br> 2. Kết thúc use case |

# Cập nhật số lượng trong giỏ
| Use case | Nội dung |
|--- | --- |
| Tên use case | Cập nhật số lượng trong giỏ |
| Mô tả | Cho phép người dùng thay đổi số lượng (tăng, giảm hoặc nhập số lượng mới) của sản phẩm trong giỏ hàng |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn nút tăng/giảm hoặc nhập số lượng mới của sản phẩm tại trang giỏ hàng |
| Tiền điều kiện | Người dùng đã đăng nhập và đang ở trang Giỏ hàng |
| Hậu điều kiện | Số lượng sản phẩm được cập nhật, tổng tiền giỏ hàng được tính toán lại |
| Luồng sự kiện chính | 1. Người dùng thay đổi số lượng của một sản phẩm trong giỏ hàng <br> 2. Hệ thống kiểm tra số lượng mới hợp lệ (> 0) và không vượt quá tồn kho <br> 3. Hệ thống cập nhật lại số lượng sản phẩm trong giỏ hàng <br> 4. Hệ thống tính toán lại thành tiền và tổng giá trị đơn hàng, cập nhật lại giao diện <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Số lượng vượt quá tồn kho**: <br> 1. Ở bước 2, nếu số lượng vượt quá tồn kho thực tế, hệ thống cảnh báo và đặt lại số lượng tối đa khả dụng <br> 2. Kết thúc use case <br> **A2 - Người dùng giảm số lượng về 0**: <br> 1. Hệ thống hỏi xác nhận xóa sản phẩm khỏi giỏ hàng <br> 2. Nếu đồng ý, thực hiện use case "Xóa khỏi giỏ hàng" <br> 3. Kết thúc use case |

# Xóa khỏi giỏ hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xóa khỏi giỏ hàng |
| Mô tả | Cho phép người dùng xóa một sản phẩm không còn nhu cầu mua ra khỏi giỏ hàng |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn nút "Xóa" cạnh sản phẩm tại trang giỏ hàng |
| Tiền điều kiện | Người dùng đã đăng nhập và giỏ hàng có sản phẩm |
| Hậu điều kiện | Sản phẩm được xóa khỏi giỏ hàng, tổng tiền giỏ hàng được cập nhật lại |
| Luồng sự kiện chính | 1. Người dùng nhấn nút "Xóa" tại sản phẩm muốn xóa trong giỏ hàng <br> 2. Hệ thống hiển thị hộp thoại yêu cầu xác nhận xóa <br> 3. Người dùng chọn xác nhận <br> 4. Hệ thống xóa sản phẩm khỏi giỏ hàng trong cơ sở dữ liệu <br> 5. Hệ thống tính lại tổng tiền, cập nhật giao diện giỏ hàng và hiển thị thông báo thành công <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Người dùng hủy thao tác**: <br> 1. Ở bước 3, người dùng chọn "Hủy bỏ" trong hộp thoại xác nhận <br> 2. Hệ thống đóng hộp thoại và giữ nguyên sản phẩm trong giỏ hàng <br> 3. Kết thúc use case |

# Đặt hàng (COD)
| Use case | Nội dung |
|--- | --- |
| Tên use case | Đặt hàng (COD) |
| Mô tả | Cho phép người dùng tiến hành đặt mua các sản phẩm trong giỏ hàng theo phương thức thanh toán khi nhận hàng (COD) |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn nút "Tiến hành đặt hàng" hoặc "Thanh toán" tại trang giỏ hàng |
| Tiền điều kiện | Người dùng đã đăng nhập và giỏ hàng có ít nhất một sản phẩm còn hàng |
| Hậu điều kiện | Đơn hàng mới được tạo với trạng thái `PENDING`, tồn kho sản phẩm bị trừ, giỏ hàng được xóa các mặt hàng đã đặt |
| Luồng sự kiện chính | 1. Người dùng nhấn nút "Tiến hành đặt hàng" từ trang giỏ hàng <br> 2. Hệ thống hiển thị màn hình Đặt hàng (Checkout) gồm danh sách sản phẩm, tổng tiền và biểu mẫu thông tin giao hàng <br> 3. Người dùng nhập/kiểm tra thông tin người nhận (họ tên, số điện thoại, địa chỉ, ghi chú) và chọn phương thức thanh toán COD <br> 4. Người dùng nhấn nút "Xác nhận đặt hàng" <br> 5. Hệ thống kiểm tra tính hợp lệ của thông tin và kiểm tra lại tồn kho của tất cả sản phẩm <br> 6. Hệ thống tạo đơn hàng mới với trạng thái `PENDING`, lưu chi tiết các sản phẩm trong đơn (`order_items`) kèm giá bán tại thời điểm đặt, trừ số lượng tồn kho tương ứng và làm sạch giỏ hàng <br> 7. Hệ thống hiển thị thông báo đặt hàng thành công kèm mã đơn hàng <br> 8. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Thông tin giao hàng không hợp lệ**: <br> 1. Ở bước 5, nếu thiếu thông tin bắt buộc (họ tên, SĐT, địa chỉ), hệ thống hiển thị thông báo yêu cầu nhập đầy đủ <br> 2. Quay lại bước 3 của luồng chính <br> **A2 - Sản phẩm hết hàng hoặc không đủ tồn kho**: <br> 1. Ở bước 5, nếu có sản phẩm không còn đủ số lượng tồn kho, hệ thống thông báo lỗi chi tiết sản phẩm thiếu hàng <br> 2. Hệ thống chuyển hướng người dùng về trang giỏ hàng để cập nhật lại <br> 3. Kết thúc use case |

# Xem lịch sử đơn hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem lịch sử đơn hàng |
| Mô tả | Cho phép người dùng xem danh sách toàn bộ các đơn hàng mà mình đã từng đặt trên hệ thống |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng chọn mục "Lịch sử đơn hàng" từ menu tài khoản hoặc thanh điều hướng |
| Tiền điều kiện | Người dùng đã đăng nhập vào hệ thống |
| Hậu điều kiện | Danh sách các đơn hàng đã đặt của người dùng được hiển thị |
| Luồng sự kiện chính | 1. Người dùng chọn mục "Lịch sử đơn hàng" <br> 2. Hệ thống truy vấn danh sách các đơn hàng của tài khoản từ cơ sở dữ liệu <br> 3. Hệ thống hiển thị danh sách đơn hàng (mã đơn hàng, ngày đặt, tổng tiền, phương thức COD, trạng thái: PENDING, CONFIRMED, SHIPPING, DELIVERED, CANCELLED) theo thứ tự thời gian mới nhất <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chưa có đơn hàng nào**: <br> 1. Ở bước 2, nếu người dùng chưa có đơn hàng nào, hệ thống hiển thị thông báo "Bạn chưa có đơn hàng nào" kèm nút "Mua sắm ngay" <br> 2. Kết thúc use case |

# Xem chi tiết đơn hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem chi tiết đơn hàng |
| Mô tả | Cho phép người dùng xem thông tin chi tiết một đơn hàng cụ thể: thông tin người nhận, danh sách linh kiện đã mua và trạng thái đơn hàng |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn chọn một đơn hàng hoặc bấm nút "Xem chi tiết" tại trang lịch sử đơn hàng |
| Tiền điều kiện | Người dùng đã đăng nhập và đơn hàng thuộc về chính tài khoản đó |
| Hậu điều kiện | Thông tin chi tiết của đơn hàng được hiển thị trên màn hình |
| Luồng sự kiện chính | 1. Tại trang lịch sử đơn hàng, người dùng chọn đơn hàng muốn xem chi tiết <br> 2. Hệ thống kiểm tra quyền sở hữu và truy xuất dữ liệu đơn hàng cùng danh sách sản phẩm trong đơn <br> 3. Hệ thống hiển thị chi tiết: mã đơn hàng, ngày đặt, trạng thái đơn hàng, thông tin giao hàng (họ tên, SĐT, địa chỉ, ghi chú), danh sách sản phẩm (tên, hình ảnh, đơn giá mua, số lượng, thành tiền) và tổng tiền đơn hàng <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Đơn hàng không tồn tại hoặc không hợp lệ**: <br> 1. Ở bước 2, nếu không tìm thấy đơn hàng hoặc đơn hàng không thuộc về người dùng, hệ thống thông báo lỗi "Không tìm thấy thông tin đơn hàng" <br> 2. Chuyển hướng người dùng về trang Lịch sử đơn hàng <br> 3. Kết thúc use case |

# Hủy đơn hàng
| Use case | Nội dung |
|--- | --- |
| Tên use case | Hủy đơn hàng |
| Mô tả | Cho phép người dùng chủ động hủy đơn hàng đã đặt khi đơn hàng vẫn đang ở trạng thái chờ xác nhận (`PENDING`) |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn nút "Hủy đơn hàng" tại trang lịch sử đơn hàng hoặc trang chi tiết đơn hàng |
| Tiền điều kiện | Người dùng đã đăng nhập và đơn hàng cần hủy đang ở trạng thái `PENDING` |
| Hậu điều kiện | Đơn hàng chuyển sang trạng thái `CANCELLED`, số lượng tồn kho của các linh kiện được hoàn trả |
| Luồng sự kiện chính | 1. Người dùng nhấn nút "Hủy đơn hàng" tại đơn hàng có trạng thái `PENDING` <br> 2. Hệ thống hiển thị hộp thoại xác nhận hủy đơn hàng <br> 3. Người dùng chọn xác nhận hủy <br> 4. Hệ thống kiểm tra lại trạng thái đơn hàng trong cơ sở dữ liệu: nếu vẫn là `PENDING`, hệ thống cập nhật trạng thái sang `CANCELLED` <br> 5. Hệ thống hoàn lại số lượng các linh kiện trong đơn vào lại kho hàng (`stock_quantity`) <br> 6. Hệ thống hiển thị thông báo hủy đơn hàng thành công và cập nhật lại giao diện <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Đơn hàng không còn ở trạng thái PENDING**: <br> 1. Ở bước 4, nếu đơn hàng đã được admin xác nhận (`CONFIRMED`) hoặc đang giao (`SHIPPING`), hệ thống hiển thị thông báo lỗi "Đơn hàng đã được xác nhận hoặc đang xử lý, không thể hủy" <br> 2. Hệ thống tải lại trạng thái mới nhất của đơn hàng <br> 3. Kết thúc use case <br> **A2 - Người dùng hủy thao tác**: <br> 1. Ở bước 3, người dùng chọn đóng hộp thoại xác nhận <br> 2. Hệ thống giữ nguyên trạng thái đơn hàng <br> 3. Kết thúc use case |

<!-- Đánh giá sản phẩm -->
# Đánh giá sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Đánh giá sản phẩm |
| Mô tả | Cho phép người dùng đã mua và nhận hàng thành công đánh giá chất lượng sản phẩm bằng số sao (1–5) kèm nhận xét |
| Actor | Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn nút "Viết đánh giá" tại trang chi tiết sản phẩm hoặc trang chi tiết đơn hàng đã giao |
| Tiền điều kiện | Người dùng đã đăng nhập, đã mua sản phẩm trong đơn hàng có trạng thái `DELIVERED`, và chưa từng đánh giá sản phẩm này |
| Hậu điều kiện | Đánh giá mới được lưu vào cơ sở dữ liệu (`product_reviews`), điểm sao trung bình của sản phẩm được cập nhật lại |
| Luồng sự kiện chính | 1. Người dùng chọn chức năng "Viết đánh giá" cho sản phẩm <br> 2. Hệ thống hiển thị biểu mẫu đánh giá gồm: chọn số sao (1–5 sao) và ô nhập nhận xét <br> 3. Người dùng chọn số sao, nhập nội dung nhận xét và nhấn nút "Gửi đánh giá" <br> 4. Hệ thống kiểm tra điều kiện hợp lệ: người dùng đã mua sản phẩm trong đơn hàng `DELIVERED` và chưa từng đánh giá sản phẩm này trước đó <br> 5. Hệ thống lưu đánh giá vào cơ sở dữ liệu và tính toán lại điểm đánh giá trung bình của sản phẩm <br> 6. Hệ thống hiển thị thông báo gửi đánh giá thành công và cập nhật lại giao diện <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Chưa đủ điều kiện đánh giá**: <br> 1. Ở bước 4, nếu người dùng chưa từng mua sản phẩm hoặc đơn hàng chưa hoàn tất giao, hệ thống hiển thị thông báo "Bạn chỉ có thể đánh giá sản phẩm sau khi đã mua và nhận hàng thành công" <br> 2. Kết thúc use case <br> **A2 - Đã từng đánh giá sản phẩm này**: <br> 1. Ở bước 4, nếu người dùng đã từng đánh giá sản phẩm này trước đó, hệ thống thông báo "Mỗi sản phẩm bạn chỉ được đánh giá một lần" <br> 2. Kết thúc use case <br> **A3 - Thiếu điểm sao hoặc nội dung không hợp lệ**: <br> 1. Ở bước 4, nếu người dùng chưa chọn số sao hoặc nội dung quá dài (> 1000 ký tự), hệ thống cảnh báo yêu cầu bổ sung/chỉnh sửa <br> 2. Quay lại bước 3 của luồng chính |

# Xem đánh giá sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem đánh giá sản phẩm |
| Mô tả | Cho phép người dùng xem điểm sao trung bình và danh sách các nhận xét, đánh giá từ khách hàng khác về sản phẩm |
| Actor | Khách vãng lai (Guest), Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng cuộn xuống phần "Đánh giá sản phẩm" tại trang chi tiết sản phẩm |
| Tiền điều kiện | Người dùng đang xem trang chi tiết của một sản phẩm cụ thể |
| Hậu điều kiện | Danh sách các đánh giá và điểm số trung bình được hiển thị đầy đủ |
| Luồng sự kiện chính | 1. Người dùng truy cập trang chi tiết của sản phẩm và cuộn đến khu vực đánh giá <br> 2. Hệ thống truy vấn danh sách các đánh giá của sản phẩm đó từ cơ sở dữ liệu (`product_reviews`) <br> 3. Hệ thống tính toán điểm sao trung bình và tổng số lượt đánh giá <br> 4. Hệ thống hiển thị: điểm sao trung bình, tổng số đánh giá, và danh sách từng đánh giá gồm tên người mua, số sao, nhận xét và ngày đánh giá <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Sản phẩm chưa có đánh giá**: <br> 1. Ở bước 2, nếu sản phẩm chưa có lượt đánh giá nào, hệ thống hiển thị thông báo "Chưa có đánh giá nào cho sản phẩm này" <br> 2. Kết thúc use case |

<!-- Xem sản phẩm -->
# Xem danh sách sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem danh sách sản phẩm |
| Mô tả | Cho phép người dùng duyệt xem danh sách các linh kiện máy tính đang kinh doanh kèm theo phân trang và sắp xếp |
| Actor | Khách vãng lai (Guest), Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng truy cập trang chủ hoặc chọn mục "Sản phẩm" trên thanh điều hướng |
| Tiền điều kiện | Không có |
| Hậu điều kiện | Danh sách các sản phẩm đang kinh doanh (`is_active = true`) được hiển thị trên giao diện |
| Luồng sự kiện chính | 1. Người dùng chọn mục Sản phẩm trên thanh điều hướng <br> 2. Hệ thống truy vấn danh sách sản phẩm đang hoạt động (`is_active = true`) từ cơ sở dữ liệu có áp dụng phân trang (mặc định 12 sản phẩm/trang) <br> 3. Hệ thống hiển thị danh sách sản phẩm dạng lưới: hình ảnh, tên sản phẩm, giá bán, tình trạng còn hàng và điểm sao đánh giá <br> 4. Người dùng có thể chuyển trang phân trang hoặc chọn sắp xếp theo giá (tăng/giảm dần) hoặc sản phẩm mới nhất <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Không có sản phẩm nào**: <br> 1. Ở bước 2, nếu hệ thống chưa có sản phẩm nào đang kích hoạt, hiển thị thông báo "Hiện chưa có sản phẩm nào" <br> 2. Kết thúc use case |

# Tìm kiếm sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Tìm kiếm sản phẩm |
| Mô tả | Cho phép người dùng tìm kiếm nhanh linh kiện máy tính theo từ khóa tên sản phẩm |
| Actor | Khách vãng lai (Guest), Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhập từ khóa vào ô tìm kiếm trên thanh điều hướng và nhấn phím Enter hoặc nút Tìm kiếm |
| Tiền điều kiện | Không có |
| Hậu điều kiện | Danh sách sản phẩm có tên khớp với từ khóa tìm kiếm được hiển thị |
| Luồng sự kiện chính | 1. Người dùng nhập từ khóa tìm kiếm (tên linh kiện, model) vào ô tìm kiếm và bấm Enter/biểu tượng Tìm kiếm <br> 2. Hệ thống gửi yêu cầu lên backend để tra cứu các sản phẩm có tên chứa từ khóa (không phân biệt chữ hoa, chữ thường) <br> 3. Hệ thống hiển thị danh sách sản phẩm khớp với từ khóa tìm kiếm kèm theo tổng số kết quả tìm thấy <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Không tìm thấy kết quả**: <br> 1. Ở bước 2, nếu không có sản phẩm nào khớp với từ khóa, hệ thống hiển thị thông báo "Không tìm thấy sản phẩm nào phù hợp với từ khóa" và gợi ý người dùng thử lại từ khóa khác <br> 2. Kết thúc use case <br> **A2 - Từ khóa tìm kiếm để trống**: <br> 1. Nếu người dùng nhấn tìm kiếm khi ô nhập rỗng, hệ thống giữ nguyên trang hoặc hiển thị danh sách toàn bộ sản phẩm <br> 2. Kết thúc use case |

# Lọc sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Lọc sản phẩm |
| Mô tả | Cho phép người dùng thu hẹp danh sách sản phẩm theo danh mục linh kiện (CPU, RAM, GPU,...) và khoảng giá |
| Actor | Khách vãng lai (Guest), Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng chọn các tiêu chí lọc (danh mục, khoảng giá) tại thanh lọc của trang sản phẩm |
| Tiền điều kiện | Người dùng đang ở trang Danh sách sản phẩm |
| Hậu điều kiện | Danh sách sản phẩm thỏa mãn đồng thời các điều kiện lọc được hiển thị |
| Luồng sự kiện chính | 1. Tại trang sản phẩm, người dùng chọn tiêu chí lọc: danh mục linh kiện (CPU, Mainboard, RAM, GPU, PSU, Case, CPU_COOLER, STORAGE) và/hoặc chọn khoảng giá <br> 2. Người dùng nhấn nút "Áp dụng" (hoặc hệ thống tự động lọc theo thao tác) <br> 3. Hệ thống truy vấn danh sách sản phẩm thỏa mãn đồng thời các điều kiện lọc <br> 4. Hệ thống cập nhật hiển thị danh sách sản phẩm tương ứng kèm số lượng kết quả tìm được <br> 5. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Không có sản phẩm phù hợp**: <br> 1. Ở bước 3, nếu không tìm thấy sản phẩm nào thỏa mãn tất cả tiêu chí, hệ thống hiển thị thông báo "Không có sản phẩm nào phù hợp với bộ lọc đã chọn" kèm nút "Đặt lại bộ lọc" <br> 2. Kết thúc use case <br> **A2 - Khoảng giá không hợp lệ**: <br> 1. Nếu người dùng nhập giá tối thiểu lớn hơn giá tối đa hoặc nhập số âm, hệ thống hiển thị cảnh báo và yêu cầu nhập lại <br> 2. Quay lại bước 1 của luồng chính |

# Xem chi tiết sản phẩm
| Use case | Nội dung |
|--- | --- |
| Tên use case | Xem chi tiết sản phẩm |
| Mô tả | Cho phép người dùng xem thông tin toàn diện về một sản phẩm, bao gồm giá, tồn kho, mô tả, thông số kỹ thuật chi tiết (JSONB) và đánh giá |
| Actor | Khách vãng lai (Guest), Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng nhấn vào thẻ, tên hoặc hình ảnh của một sản phẩm trong danh sách |
| Tiền điều kiện | Sản phẩm được chọn tồn tại trong hệ thống |
| Hậu điều kiện | Trang chi tiết sản phẩm được hiển thị đầy đủ thông tin |
| Luồng sự kiện chính | 1. Người dùng nhấn chọn một sản phẩm từ danh sách hoặc kết quả tìm kiếm <br> 2. Hệ thống truy xuất dữ liệu sản phẩm từ cơ sở dữ liệu (`products`), gồm: tên, giá, số lượng tồn kho (`stock_quantity`), mô tả, hình ảnh và thông số kỹ thuật chi tiết trong trường `detail` (JSONB) <br> 3. Hệ thống hiển thị trang chi tiết: hình ảnh lớn, tên sản phẩm, giá bán, tình trạng còn/hết hàng, bảng thông số kỹ thuật theo từng category (socket, xung nhịp, công suất, kích thước,...), nút "Thêm vào giỏ hàng" và khu vực đánh giá <br> 4. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Sản phẩm không tồn tại hoặc đã ngừng bán**: <br> 1. Ở bước 2, nếu sản phẩm không tìm thấy hoặc đã bị xóa mềm (`is_active = false`), hệ thống hiển thị thông báo "Sản phẩm không tồn tại hoặc đã ngừng kinh doanh" và điều hướng về trang danh sách sản phẩm <br> 2. Kết thúc use case |

<!-- Chatbot AI -->
# Gửi tin nhắn cho chatbot
| Use case | Nội dung |
|--- | --- |
| Tên use case | Gửi tin nhắn cho chatbot |
| Mô tả | Cho phép người dùng nhập câu hỏi hoặc yêu cầu tư vấn vào khung chat để trò chuyện với Chatbot AI của cửa hàng |
| Actor | Khách vãng lai (Guest), Khách hàng (User) |
| Điều kiện kích hoạt | Người dùng mở khung chat ở góc màn hình và gửi tin nhắn văn bản |
| Tiền điều kiện | Không yêu cầu đăng nhập |
| Hậu điều kiện | Tin nhắn được tiếp nhận, hệ thống xử lý và hiển thị phản hồi từ Chatbot AI cho người dùng |
| Luồng sự kiện chính | 1. Người dùng nhấn biểu tượng Chatbot AI để mở cửa sổ trò chuyện <br> 2. Người dùng nhập câu hỏi (về chính sách shop hoặc nhu cầu tư vấn cấu hình PC) và nhấn nút "Gửi" <br> 3. Hệ thống hiển thị tin nhắn của người dùng trong khung chat và hiển thị trạng thái đang xử lý ("Bot đang trả lời...") <br> 4. Hệ thống phân tích ý định của tin nhắn: nếu là câu hỏi chính sách shop thì thực hiện use case "Trả lời chính sách shop (RAG)", nếu là yêu cầu tư vấn PC thì thực hiện use case "Gợi ý cấu hình PC" <br> 5. Hệ thống nhận câu trả lời từ phân hệ AI tương ứng và hiển thị tin nhắn phản hồi lên khung chat cho người dùng <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Nội dung tin nhắn trống**: <br> 1. Nếu người dùng gửi tin nhắn rỗng, hệ thống không gửi yêu cầu và nhắc người dùng nhập nội dung <br> 2. Kết thúc use case <br> **A2 - Lỗi kết nối dịch vụ AI**: <br> 1. Ở bước 5, nếu gọi Gemini API gặp sự cố hoặc mất kết nối mạng, hệ thống hiển thị tin nhắn "Xin lỗi, chatbot đang bận hoặc gặp sự cố kết nối. Vui lòng thử lại sau giây lát!" <br> 2. Kết thúc use case |

# Trả lời chính sách shop (RAG)
| Use case | Nội dung |
|--- | --- |
| Tên use case | Trả lời chính sách shop (RAG) |
| Mô tả | Hệ thống tự động tra cứu tài liệu chính sách (bảo hành, đổi trả, vận chuyển, thanh toán) bằng vector embedding và sử dụng Gemini AI để trả lời chính xác, tránh ảo giác thông tin |
| Actor | Gemini AI |
| Điều kiện kích hoạt | Use case "Gửi tin nhắn cho chatbot" phân loại tin nhắn của người dùng là câu hỏi liên quan đến chính sách cửa hàng |
| Tiền điều kiện | Tài liệu chính sách đã được Admin upload và lưu trữ vector embedding trong bảng `rag_chunks` (pgvector) |
| Hậu điều kiện | Phản hồi chính xác dựa trên tài liệu chính sách của cửa hàng được sinh ra và gửi cho người dùng |
| Luồng sự kiện chính | 1. Hệ thống tiếp nhận câu hỏi chính sách từ use case "Gửi tin nhắn cho chatbot" <br> 2. Hệ thống gọi Gemini Embedding API để tạo vector biểu diễn ngữ nghĩa cho câu hỏi <br> 3. Hệ thống thực hiện tìm kiếm vector tương đồng (khoảng cách cosine) trên bảng `rag_chunks` trong PostgreSQL để lấy top các đoạn tài liệu chính sách liên quan nhất <br> 4. Hệ thống đưa các đoạn trích tài liệu này vào ngữ cảnh (Context) kèm câu lệnh ràng buộc (System Instruction: chỉ trả lời dựa trên tài liệu được cung cấp) gửi tới Gemini Chat API <br> 5. Gemini AI tổng hợp nội dung và trả về câu trả lời tự nhiên, chính xác theo tài liệu của shop <br> 6. Hệ thống chuyển tiếp câu trả lời về cho khung chat hiển thị cho người dùng <br> 7. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Không tìm thấy thông tin chính sách liên quan**: <br> 1. Ở bước 3 và 4, nếu cơ sở tri thức không có tài liệu nào liên quan đến câu hỏi, chatbot phản hồi lịch sự rằng cửa hàng chưa có thông tin về vấn đề này và hướng dẫn người dùng liên hệ trực tiếp với nhân viên hỗ trợ <br> 2. Kết thúc use case |

# Gợi ý cấu hình PC
| Use case | Nội dung |
|--- | --- |
| Tên use case | Gợi ý cấu hình PC |
| Mô tả | Hệ thống tư vấn và đề xuất 1–3 bộ PC Case hoàn chỉnh phù hợp nhất với ngân sách và nhu cầu của người dùng từ danh sách cấu hình có sẵn và còn hàng trong kho |
| Actor | Gemini AI |
| Điều kiện kích hoạt | Use case "Gửi tin nhắn cho chatbot" phân loại tin nhắn của người dùng là yêu cầu tư vấn hoặc gợi ý cấu hình PC |
| Tiền điều kiện | Hệ thống có sẵn các bộ PC Case do Admin tạo (`is_active = true`) và toàn bộ linh kiện thành phần phải còn tồn kho (`stock_quantity > 0`) |
| Hậu điều kiện | Danh sách 1–3 bộ PC Case phù hợp kèm giải thích được hiển thị trên khung chat |
| Luồng sự kiện chính | 1. Hệ thống tiếp nhận yêu cầu về ngân sách và mục đích sử dụng từ use case "Gửi tin nhắn cho chatbot" <br> 2. Hệ thống truy vấn từ bảng `pc_cases` danh sách các bộ PC Case đang kinh doanh (`is_active = true`) và kiểm tra toàn bộ linh kiện thành phần phải có `stock_quantity > 0` <br> 3. Hệ thống cấu trúc hóa danh sách PC Case hợp lệ (tên, mục đích sử dụng, tổng giá, danh sách linh kiện) thành dữ liệu ngữ cảnh đưa vào Prompt gửi tới Gemini AI kèm nguyên tắc: "Chỉ được chọn từ các bộ cấu hình trong danh sách, tuyệt đối không tự ý ghép nối linh kiện mới" <br> 4. Gemini AI phân tích nhu cầu và ngân sách của người dùng, lựa chọn ra từ 1 đến 3 bộ PC Case phù hợp nhất kèm lời giải thích lý do <br> 5. Hệ thống nhận kết quả từ Gemini API, định dạng câu trả lời kèm thẻ thông tin chi tiết từng bộ PC Case và gửi về khung chat hiển thị cho người dùng <br> 6. Kết thúc use case |
| Luồng sự kiện phụ | **A1 - Không có cấu hình nào phù hợp ngân sách hoặc nhu cầu**: <br> 1. Ở bước 4, nếu ngân sách của người dùng không đủ hoặc không có bộ máy nào phù hợp, chatbot thông báo lịch sự mức giá tối thiểu của các cấu hình hiện có và đưa ra lời khuyên phù hợp <br> 2. Kết thúc use case <br> **A2 - Các cấu hình trong tầm giá tạm hết hàng**: <br> 1. Ở bước 2, nếu các bộ PC Case phù hợp có linh kiện bị hết hàng, hệ thống thông báo tạm hết hàng và gợi ý các cấu hình gần nhất còn hàng trong kho <br> 2. Kết thúc use case |
