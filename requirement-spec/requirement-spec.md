<!-- trang 1 -->
# Đặc Tả Yêu Cầu Phần Mềm

cho

Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình

Phiên bản 1.0 được phê chuẩn

Được chuẩn bị bởi

Thành viên 1 - MSSV  
Thành viên 2 - MSSV  
Thành viên 3 - MSSV

21/09/2026

<!-- trang 2 -->

Theo dõi phiên bản tài liệu

| **Tên** | **Ngày** | **Lý do thay đổi** | **Phiên bản** |
| ------- | -------- | ------------------ | ------------- |
|         |          |                    |               |
|         |          |                    |               |

<!-- trang 3 -->

# Giới thiệu

## Mục tiêu

Tài liệu Đặc tả Yêu cầu Phần mềm (SRS) này xác định các yêu cầu chức năng, yêu cầu phi chức năng và giao diện của hệ thống **"Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình"** (*Computer Components Shop with AI Integration*). Tài liệu đóng vai trò là cơ sở kỹ thuật chính thức định hướng thiết kế kiến trúc, hiện thực hóa mã nguồn, kiểm thử và nghiệm thu cho đề tài niên luận ngành Công nghệ thông tin / Kỹ thuật phần mềm.

Đối tượng sử dụng tài liệu bao gồm:
- **Nhóm phát triển & kiểm thử**: Làm căn cứ xây dựng mã nguồn, thiết kế cơ sở dữ liệu và kịch bản kiểm thử (Test Cases).
- **Giảng viên hướng dẫn & Hội đồng đánh giá**: Theo dõi tiến độ, đánh giá mức độ hoàn thành và chất lượng kỹ thuật của đề tài.

## Phạm vi sản phẩm

- **Tên sản phẩm**: Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình (*Computer Components Shop with AI Integration*).
- **Mục tiêu hệ thống**: Cung cấp nền tảng thương mại điện tử chuyên biệt cho lĩnh vực linh kiện máy tính (PC parts), đồng thời tích hợp trợ lý AI (Generative AI) để tự động hóa khâu giải đáp chính sách cửa hàng và tư vấn cấu hình PC tối ưu theo nhu cầu và ngân sách của khách hàng.
- **Các phân hệ cốt lõi**:
  1. **Phân hệ Thương mại điện tử (E-commerce)**: Duyệt, tìm kiếm và lọc linh kiện theo thông số kỹ thuật đặc thù; quản lý giỏ hàng; đặt hàng với hình thức thanh toán khi nhận hàng (COD); quản lý lịch sử đơn hàng và đánh giá sản phẩm đã mua.
  2. **Phân hệ Trợ lý ảo AI (AI Chatbot)**:
     - *Hỏi đáp chính sách (RAG)*: Tra cứu và giải đáp các thắc mắc về chính sách bảo hành, đổi trả, vận chuyển dựa trên tài liệu cửa hàng bằng kỹ thuật RAG (Google Gemini Embedding + PostgreSQL pgvector).
     - *Tư vấn cấu hình PC*: Tiếp nhận yêu cầu bằng ngôn ngữ tự nhiên (ngân sách, mục đích sử dụng) và gợi ý 1–3 bộ PC Case hoàn chỉnh tối ưu. AI chỉ lựa chọn từ các PC Case đã được Admin tạo sẵn và kiểm tra tính tương thích phần cứng, đảm bảo toàn bộ linh kiện thành phần còn tồn kho.
  3. **Phân hệ Quản trị (Admin Panel)**: Quản lý danh mục linh kiện (thông số kỹ thuật lưu dạng JSONB linh hoạt); quản lý đơn hàng; tạo và tự động kiểm tra ràng buộc tương thích phần cứng cho cấu hình PC Case; quản lý tài liệu RAG; theo dõi thống kê kinh doanh (doanh thu, đơn hàng, sản phẩm bán chạy, người dùng mới).

## Bảng chú giải thuật ngữ

| Thuật ngữ / Từ viết tắt | Định nghĩa / Giải thích |
| :--- | :--- |
| **SRS** (Software Requirements Specification) | Tài liệu đặc tả yêu cầu phần mềm theo chuẩn IEEE 830. |
| **RAG** (Retrieval-Augmented Generation) | Kỹ thuật tăng cường sinh văn bản bằng cách truy xuất thông tin từ cơ sở tri thức trước khi đưa vào mô hình ngôn ngữ lớn để trả lời. |
| **pgvector** | Tiện ích mở rộng của PostgreSQL hỗ trợ lưu trữ và tìm kiếm vector tương đồng (vector similarity search). |
| **Vector Embedding** | Biểu diễn ngữ nghĩa của văn bản dưới dạng vector số thực nhiều chiều phục vụ tìm kiếm tương đồng. |
| **PC Case** | Trong hệ thống, thuật ngữ này chỉ **một bộ cấu hình PC hoàn chỉnh** (gồm tập hợp các linh kiện tương thích: CPU, Mainboard, RAM, GPU, Storage, PSU, Case, CPU Cooler). |
| **JSONB** | Kiểu dữ liệu JSON nhị phân trong PostgreSQL, dùng để lưu linh hoạt các thuộc tính kỹ thuật riêng của từng loại linh kiện. |
| **JWT** (JSON Web Token) | Chuẩn token không trạng thái (stateless) dùng để xác thực và phân quyền người dùng giữa Client và Server. |
| **COD** (Cash On Delivery) | Phương thức thanh toán bằng tiền mặt khi nhận hàng. |

## Tài liệu tham khảo

1. **IEEE Computer Society**, *IEEE Std 830-1998: IEEE Recommended Practice for Software Requirements Specifications*, IEEE, 1998.
2. **Khoa Công nghệ Thông tin**, *Đề cương môn học Niên luận ngành Công nghệ Thông tin / Kỹ thuật Phần mềm*, 2026.
3. **Spring Boot Documentation**, *Spring Boot Reference Guide & Spring Security*, VMware Tanzu, 2024. [https://spring.io/projects/spring-boot](https://spring.io/projects/spring-boot)
4. **PostgreSQL & pgvector**, *PostgreSQL Documentation & pgvector extension*, 2024. [https://github.com/pgvector/pgvector](https://github.com/pgvector/pgvector)
5. **Google AI for Developers**, *Gemini API & Text Embeddings Documentation*, Google, 2024. [https://ai.google.dev/docs](https://ai.google.dev/docs)

## Bố cục tài liệu

Tài liệu được cấu trúc thành các phần chính sau:
- **Phần 1: Giới thiệu**: Trình bày mục tiêu, phạm vi sản phẩm, thuật ngữ và tài liệu tham khảo.
- **Phần 2: Mô tả tổng quan**: Khái quát kiến trúc hệ thống, các chức năng chính, các nhóm người dùng và các ràng buộc kỹ thuật.
- **Phần 3: Yêu cầu giao tiếp bên ngoài**: Đặc tả giao diện người dùng (UI), giao diện phần mềm (API, CSDL) và giao thức truyền thông.
- **Phần 4: Yêu cầu chức năng**: Mô tả chi tiết từng nhóm tính năng hệ thống kèm mã định danh yêu cầu `REQ-xxx`.
- **Phần 5: Yêu cầu phi chức năng & Quy tắc nghiệp vụ**: Xác định các tiêu chuẩn về hiệu năng, an toàn, bảo mật và các quy tắc nghiệp vụ cốt lõi (`BR-01` đến `BR-08`).
- **Phần 6: Phụ lục**: Các sơ đồ mô hình hóa và nội dung mở rộng.

# Mô tả tổng quan

## Bối cảnh của sản phẩm

Hệ thống **"Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình"** là một ứng dụng web độc lập, được phát triển nhằm giải quyết bài toán kinh doanh trực tuyến và tự động hóa khâu tư vấn kỹ thuật linh kiện máy tính. Hệ thống áp dụng kiến trúc phân tầng hiện đại, tách biệt giữa giao diện người dùng (Client) và xử lý nghiệp vụ (Server):

- **Client (Frontend)**: Ứng dụng Single Page Application (SPA) phát triển bằng React, TypeScript, Vite, Tailwind CSS và Shadcn UI.
- **Server (Backend)**: Xây dựng bằng Java, Spring Boot 3.x, sử dụng Spring Data JPA và Spring Security kết hợp JWT.
- **Cơ sở dữ liệu**: PostgreSQL 15+ tích hợp extension `pgvector` phục vụ lưu trữ song song dữ liệu quan hệ và vector embedding cho RAG.
- **Dịch vụ tích hợp bên ngoài**:
  - **Google Gemini API**: Xử lý tạo vector nhúng (Text Embedding) và sinh phản hồi ngôn ngữ tự nhiên (Chatbot).
  - **Cloudinary**: Lưu trữ và tối ưu hóa hình ảnh sản phẩm.

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT (Browser)                         │
│               React + Vite (TypeScript) + Shadcn UI             │
└───────────────────────────┬─────────────────────────────────────┘
                            │ HTTPS / RESTful API (JSON)
┌───────────────────────────▼─────────────────────────────────────┐
│                   BACKEND (Spring Boot / Java)                  │
│                                                                 │
│  ┌──────────────┐  ┌──────────────┐  ┌────────────────────────┐ │
│  │ Product API  │  │  Order API   │  │      AI / Chat API     │ │
│  │ (CRUD, tìm   │  │ (đặt hàng,   │  │  ┌──────────────────┐  │ │
│  │  kiếm, lọc)  │  │  lịch sử)    │  │  │ RAG Service      │  │ │
│  └──────────────┘  └──────────────┘  │  │ (pgvector query) │  │ │
│                                      │  └──────────────────┘  │ │
│  ┌──────────────┐  ┌──────────────┐  │  ┌──────────────────┐  │ │
│  │  Auth API    │  │ Admin API    │  │  │ PC Config Service│  │ │
│  │    (JWT)     │  │ (PC Case,    │  │  │ (query PC Cases) │  │ │
│  └──────────────┘  │  RAG docs)   │  │  └──────────────────┘  │ │
│                    └──────────────┘  │  ┌──────────────────┐  │ │
│                                      │  │ Gemini API Call  │  │ │
│                                      │  └──────────────────┘  │ │
│                                      └────────────────────────┘ │
└──────────────────────────────┬──────────────────────────────────┘
                               │
          ┌────────────────────┼─────────────────────┐
          │                    │                     │
┌─────────▼──────┐   ┌─────────▼──────┐  ┌───────────▼──────────┐
│   PostgreSQL   │   │    pgvector    │  │    Cloudinary CDN    │
│  (Main Data)   │   │  (RAG Embeds)  │  │   (Product Images)   │
└────────────────┘   └────────────────┘  └──────────────────────┘
```

## Các chức năng chính của sản phẩm

Hệ thống cung cấp 7 nhóm chức năng trọng tâm:

1. **Xác thực và phân quyền (Authentication & Authorization)**: Đăng ký tài khoản, đăng nhập cấp phát Access Token (JWT) và Refresh Token (HttpOnly Cookie), phân quyền theo vai trò (Guest, User, Admin).
2. **Duyệt và tìm kiếm sản phẩm (Product Browsing & Search)**: Duyệt linh kiện theo danh mục (CPU, Mainboard, RAM, GPU, Storage, PSU, Case, CPU Cooler), tìm kiếm theo từ khóa, lọc theo khoảng giá và thương hiệu, xem chi tiết thông số kỹ thuật (dữ liệu JSONB).
3. **Giỏ hàng và Đặt hàng (Cart & Order Processing)**: Quản lý giỏ hàng (thêm/sửa/xóa linh kiện lẻ và PC Case); đặt hàng với hình thức thanh toán khi nhận hàng (COD); theo dõi lịch sử và trạng thái đơn hàng (PENDING, CONFIRMED, SHIPPING, DELIVERED, CANCELLED); hủy đơn khi đang ở trạng thái PENDING.
4. **Đánh giá sản phẩm (Product Reviews)**: Người dùng đã mua hàng có thể đánh giá (1–5 sao) và để lại nhận xét cho linh kiện hoặc bộ PC Case đã mua.
5. **Trợ lý thông minh Chatbot AI**:
   - *Hỏi đáp chính sách (RAG)*: Tra cứu chính sách bảo hành, đổi trả, giao hàng; tìm kiếm đoạn tài liệu tương đồng bằng cosine similarity trên `pgvector` và gửi ngữ cảnh cho Gemini để trả lời chính xác.
   - *Gợi ý cấu hình PC*: Tiếp nhận ngân sách và mục đích sử dụng; truy vấn danh sách PC Case đang kích hoạt và còn đủ hàng trong kho (`stock_quantity > 0`); gửi cho Gemini để chọn và tư vấn 1–3 bộ PC Case tối ưu nhất.
6. **Quản lý cấu hình PC Case & Kiểm tra tương thích (PC Case Management)**: Admin tạo cấu hình PC từ các linh kiện trong kho. Hệ thống tự động thực thi thuật toán kiểm định tính tương thích phần cứng (socket CPU/Mainboard, chuẩn RAM, kích thước Case/GPU/Cooler, tổng TDP và công suất nguồn) trước khi lưu vào CSDL.
7. **Quản trị hệ thống & Thống kê (Admin Operations & Statistics)**: Quản lý kho hàng linh kiện (thông số JSONB, ảnh Cloudinary); xử lý trạng thái đơn hàng; upload/xóa tài liệu RAG; theo dõi thống kê doanh thu, đơn hàng, top sản phẩm bán chạy và người dùng mới.

## Đặc điểm người sử dụng

| Nhóm người dùng | Mô tả | Quyền hạn và phạm vi sử dụng chính |
| :--- | :--- | :--- |
| **Khách vãng lai (Guest)** | Người dùng chưa đăng nhập hệ thống. | - Xem, tìm kiếm, lọc linh kiện và cấu hình PC.<br>- Xem đánh giá sản phẩm.<br>- Sử dụng Chatbot AI (hỏi đáp chính sách, tư vấn cấu hình).<br>- Đăng ký tài khoản mới. |
| **Khách hàng thành viên (User)** | Khách hàng đã đăng ký và đăng nhập tài khoản. | Thừa hưởng quyền của Guest, đồng thời:<br>- Quản lý giỏ hàng cá nhân (linh kiện lẻ & PC Case).<br>- Đặt hàng COD, xem lịch sử đơn hàng và hủy đơn PENDING.<br>- Đánh giá, nhận xét sản phẩm đã mua. |
| **Quản trị viên (Admin)** | Nhân viên quản lý vận hành cửa hàng. | Thừa hưởng quyền của User, đồng thời:<br>- Quản lý sản phẩm linh kiện (CRUD, ảnh Cloudinary, thông số JSONB).<br>- Quản lý đơn hàng và cập nhật trạng thái đơn.<br>- Thiết lập cấu hình PC Case (kiểm tra tương thích tự động).<br>- Quản lý tài liệu RAG (upload, bóc tách chunks, nhúng vector).<br>- Xem biểu đồ thống kê kinh doanh. |

## Môi trường vận hành

- **Phía Người dùng (Client-side)**:
  - Thiết bị: Máy tính cá nhân (Desktop/Laptop), máy tính bảng, điện thoại thông minh (hỗ trợ Responsive Design).
  - Trình duyệt: Các trình duyệt web hiện đại hỗ trợ HTML5, CSS3, JavaScript (Google Chrome, Mozilla Firefox, Microsoft Edge, Apple Safari).
- **Phía Máy chủ (Server-side)**:
  - Môi trường thực thi: Java Development Kit (JDK) 17 hoặc 21 (LTS).
  - Framework: Spring Boot 3.x tích hợp máy chủ nhúng Apache Tomcat.
  - Hệ điều hành máy chủ: Linux (Ubuntu/Debian) hoặc Windows Server, hỗ trợ đóng gói Docker container.
- **Phía Cơ sở dữ liệu**:
  - Hệ quản trị CSDL: PostgreSQL 15+ tích hợp tiện ích mở rộng `pgvector`.
- **Dịch vụ bên ngoài (Third-party Services)**:
  - Google Gemini API (model hội thoại và mô hình Text Embedding).
  - Cloudinary CDN (lưu trữ và phân phối hình ảnh).

## Các ràng buộc về thực thi và thiết kế

1. **Kiến trúc và giao tiếp**: Mô hình Client-Server tách biệt; giao tiếp hoàn toàn thông qua RESTful API định dạng JSON chuẩn qua giao thức HTTPS.
2. **Mô hình dữ liệu linh hoạt (JSONB)**: Thông số kỹ thuật riêng biệt của từng loại linh kiện (socket, bus, vram, tdp...) bắt buộc lưu trữ trong cột `detail` dạng `JSONB` của PostgreSQL, đảm bảo tính mềm dẻo khi mở rộng loại linh kiện mới mà không cần sửa đổi schema.
3. **Ràng buộc tương thích phần cứng**: Mọi cấu hình PC Case do Admin tạo phải vượt qua thuật toán kiểm tra ràng buộc tương thích kỹ thuật trước khi lưu vào CSDL.
4. **Ràng buộc đối với Chatbot AI**:
   - **Chống ảo giác (Anti-hallucination)**: AI không tự lắp ghép linh kiện tùy tiện, chỉ được gợi ý từ danh mục cấu hình PC Case đã được Admin tạo và kiểm tra tương thích từ trước.
   - **Tồn kho thực tế**: Chỉ gợi ý các bộ cấu hình PC Case mà toàn bộ linh kiện thành phần đều đang có số lượng tồn kho khả dụng (`stock_quantity > 0`).
5. **Bảo mật và xác thực**: Sử dụng kiến trúc Stateless Token với JWT (Access Token ngắn hạn và Refresh Token lưu trong HttpOnly Cookie có cờ bảo mật); mật khẩu người dùng mã hóa an toàn bằng thuật toán BCrypt.

## Các giả định và phụ thuộc

1. **Giả định (Assumptions)**:
   - Người dùng có thiết bị kết nối mạng Internet ổn định.
   - Quản trị viên nhập dữ liệu thông số kỹ thuật linh kiện chính xác và tuân thủ định dạng JSON theo từng danh mục.
   - Phương thức thanh toán triển khai trong phạm vi đề tài là thanh toán khi nhận hàng (COD), đơn vị tiền tệ là Việt Nam Đồng (VND).
2. **Yếu tố phụ thuộc (Dependencies)**:
   - Google Gemini API: Độ sẵn sàng và hạn ngạch (quota) của Gemini ảnh hưởng trực tiếp đến phản hồi của Chatbot. Trong trường hợp lỗi dịch vụ AI, hệ thống phải thông báo thân thiện và không làm gián đoạn các luồng mua bán thông thường.
   - Cloudinary: Khả năng lưu trữ và phân phối hình ảnh sản phẩm.
   - Tiện ích mở rộng `pgvector` trên PostgreSQL phục vụ truy vấn vector embedding.

# Các yêu cầu giao tiếp bên ngoài

## Giao diện người sử dụng

Hệ thống được xây dựng dưới dạng Single Page Application (SPA) bằng **React**, **TypeScript**, **Vite**, sử dụng bộ thư viện giao diện **Shadcn UI** và **Tailwind CSS**. Giao diện đáp ứng tốt trên cả máy tính để bàn (Desktop) và thiết bị di động (Mobile Responsive).

### 1. Phía Khách hàng (Client Portal)
- **Trang chủ (HomePage)**: Biểu ngữ quảng cáo, thanh danh mục linh kiện truy cập nhanh, danh sách sản phẩm nổi bật/bán chạy và nút cửa sổ chat nổi (Chat widget).
- **Trang danh sách & lọc sản phẩm (ProductListPage)**: Thanh tìm kiếm từ khóa, bộ lọc theo danh mục, khoảng giá, thương hiệu; lưới hiển thị thẻ sản phẩm (ảnh, tên, giá, nút thêm vào giỏ).
- **Trang chi tiết sản phẩm (ProductDetailPage)**: Thư viện ảnh sản phẩm, thông tin giá bán và tình trạng tồn kho, bảng thông số kỹ thuật chi tiết trích xuất từ `detail` (JSONB), khu vực đánh giá và nhận xét sản phẩm (1–5 sao).
- **Trang giỏ hàng (CartPage)**: Danh sách linh kiện lẻ và bộ PC Case đã chọn, công cụ điều chỉnh số lượng, tạm tính tổng tiền.
- **Trang đặt hàng (CheckoutPage)**: Biểu mẫu nhập thông tin giao nhận, mặc định áp dụng hình thức thanh toán khi nhận hàng (COD), tóm tắt đơn hàng và nút xác nhận đặt hàng.
- **Trang lịch sử đơn hàng (OrderHistoryPage)**: Bảng theo dõi các đơn hàng cá nhân kèm trạng thái (PENDING, CONFIRMED, SHIPPING, DELIVERED, CANCELLED); hỗ trợ hủy đơn hàng khi ở trạng thái PENDING.
- **Khung Chatbot AI (ChatBox / ChatPage)**: Khung hội thoại hỗ trợ định dạng Markdown giải đáp chính sách; hiển thị các thẻ cấu hình PC Case tương tác (tên bộ máy, tổng giá, danh sách linh kiện thành phần, nút xem chi tiết và thêm vào giỏ hàng).
- **Trang xác thực (AuthPages)**: Form đăng nhập, đăng ký tài khoản với tính năng kiểm tra lỗi hợp lệ trực tiếp tại client.

### 2. Phía Quản trị viên (Admin Panel)
- **Bảng điều khiển thống kê (StatisticsDashboard)**: Thẻ chỉ số tổng quan (doanh thu, đơn hàng, khách hàng, sản phẩm), biểu đồ biến động doanh thu, biểu đồ cơ cấu đơn hàng và danh sách top sản phẩm bán chạy.
- **Quản lý sản phẩm (ProductManagement)**: Danh sách sản phẩm kèm tìm kiếm/lọc, modal thêm/sửa sản phẩm (nhập thông số kỹ thuật JSONB theo danh mục, upload ảnh Cloudinary) và xóa mềm sản phẩm.
- **Quản lý đơn hàng (OrderManagement)**: Bảng danh sách đơn hàng toàn hệ thống, xem chi tiết đơn và cập nhật chuyển đổi trạng thái đơn hàng.
- **Quản lý cấu hình PC Case (PcCaseManagement)**: Danh sách PC Case, form chọn linh kiện 8 slot, nút "Kiểm tra tương thích" (tự động chạy thuật toán kiểm tra ràng buộc phần cứng và hiển thị cảnh báo vi phạm nếu có).
- **Quản lý tài liệu RAG (RagDocumentManagement)**: Upload tài liệu chính sách (PDF, DOCX, TXT), danh sách tài liệu đã bóc tách chunk/nhúng vector và nút xóa tài liệu lỗi thời.

## Giao tiếp phần cứng

Do hệ thống vận hành trên nền tảng Web nên không yêu cầu giao tiếp vật lý trực tiếp với các thiết bị ngoại vi chuyên dụng:
- **Phía Người dùng**: Máy tính cá nhân, máy tính bảng hoặc điện thoại thông minh có kết nối Internet, màn hình hiển thị tiêu chuẩn và thiết bị nhập liệu (bàn phím, chuột hoặc màn hình cảm ứng).
- **Phía Máy chủ**: Máy chủ hoặc máy phát triển có kết nối Internet để gọi API bên thứ ba (Google Gemini, Cloudinary); cấu hình tối thiểu 2 Cores CPU, 4 GB RAM và ổ cứng SSD để vận hành ổn định Spring Boot và PostgreSQL.

## Giao tiếp phần mềm

Hệ thống kết nối và giao tiếp với các phần mềm và dịch vụ sau:
1. **PostgreSQL (v15+) & pgvector**:
   - Lưu trữ dữ liệu quan hệ thông qua Spring Data JPA / Hibernate trên cổng TCP `5432`.
   - Sử dụng kiểu dữ liệu `VECTOR(768)` và toán tử khoảng cách cosine `<=>` của `pgvector` để tìm kiếm các đoạn tài liệu chính sách liên quan nhất (top-K chunks).
2. **Google Gemini API**:
   - *Gemini Embedding API*: Nhận chuỗi văn bản và sinh vector nhúng 768 chiều.
   - *Gemini Chat API*: Xử lý ngữ cảnh và yêu cầu của người dùng để sinh phản hồi tự nhiên cho chatbot.
   - Giao tiếp qua REST API bằng giao thức bảo mật HTTPS.
3. **Cloudinary API**:
   - Tiếp nhận tải lên hình ảnh sản phẩm từ Backend qua Java SDK, lưu trữ trên nền tảng đám mây và trả về URL ảnh an toàn (HTTPS CDN).
4. **Giao tiếp Client (Frontend) - Server (Backend)**:
   - Giao tiếp qua RESTful API định dạng JSON (`application/json`) hoặc `multipart/form-data` (upload file).
   - Định dạng phản hồi chuẩn:
     ```json
     {
       "success": true,
       "message": "Thông báo trạng thái",
       "data": { ... }
     }
     ```
   - Xác thực qua tiêu đề HTTP `Authorization: Bearer <JWT_TOKEN>` đối với Access Token và HttpOnly Cookie đối với Refresh Token.

## Giao tiếp truyền thông tin

1. **Giao thức mạng**: Sử dụng giao thức an toàn HTTPS (TLS 1.2/1.3) trên cổng chuẩn `443`. Toàn bộ lưu lượng HTTP cổng `80` được tự động chuyển hướng sang HTTPS.
2. **Bảng mã ký tự**: Sử dụng bảng mã `UTF-8` cho toàn bộ Request Headers, Request Body và Response Body để hỗ trợ tiếng Việt toàn vẹn.
3. **Chính sách kiểm soát và bảo mật truyền thông**:
   - **CORS (Cross-Origin Resource Sharing)**: Backend cấu hình giới hạn chỉ cho phép tên miền của Client truy cập, hỗ trợ gửi kèm thông tin xác thực (`allowCredentials = true`).
   - **Bảo mật Cookie**: Cookie lưu Refresh Token bắt buộc bật các cờ `HttpOnly` (chống XSS), `Secure` (chỉ truyền qua HTTPS) và `SameSite=Strict` (chống CSRF).
   - **Quản lý thời gian chờ (Timeout)**: Thiết lập Connection Timeout (5 giây) và Read Timeout (30 giây) khi Backend giao tiếp với các dịch vụ AI bên ngoài nhằm tránh hiện tượng nghẽn luồng xử lý.

# Các tính năng của hệ thống

Hệ thống bao gồm 8 nhóm tính năng chức năng chính, bao quát toàn bộ nghiệp vụ từ người dùng đến quản trị và trợ lý trí tuệ nhân tạo.

---

## 4.1 Quản lý xác thực và phân quyền (Authentication & Authorization)

- **Mô tả & Mức ưu tiên**: Cung cấp cơ chế xác thực không trạng thái (Stateless) bằng JWT, cấp mới phiên bằng Refresh Token và phân quyền vai trò người dùng. **Mức ưu tiên: Cao**.
- **Tác nhân**: Khách vãng lai (Guest), Khách hàng thành viên (User), Quản trị viên (Admin).
- **Luồng nghiệp vụ chính**:
  1. Người dùng gửi thông tin đăng ký (`/api/auth/register`) hoặc đăng nhập (`/api/auth/login`).
  2. Backend kiểm tra tính hợp lệ, băm/so khớp mật khẩu bằng BCrypt, cấp phát `accessToken` (15–60 phút) trong response JSON và `refreshToken` (7–30 ngày) trong HttpOnly Cookie.
  3. Khi `accessToken` hết hạn, Client tự động gọi `/api/auth/refresh` để nhận token mới mà không cần đăng nhập lại.
  4. Người dùng đăng xuất qua `/api/auth/logout`, hệ thống thu hồi Refresh Token và xóa cookie.
- **Các yêu cầu chức năng**:
  - **REQ-AUTH-1**: Cho phép đăng ký tài khoản với họ tên, email, mật khẩu (mã hóa một chiều bằng BCrypt), số điện thoại và địa chỉ nhận hàng.
  - **REQ-AUTH-2**: Xác thực đăng nhập bằng email và mật khẩu; trả về Access Token (JWT) và lưu Refresh Token trong HttpOnly, Secure Cookie.
  - **REQ-AUTH-3**: Cung cấp endpoint cấp phát lại Access Token mới dựa trên Refresh Token hợp lệ trong cookie.
  - **REQ-AUTH-4**: Cho phép đăng xuất và vô hiệu hóa phiên làm việc của người dùng.
  - **REQ-AUTH-5**: Phân quyền truy cập tài nguyên API dựa trên vai trò (RBAC) với 3 nhóm quyền: `GUEST`, `USER`, `ADMIN`.

---

## 4.2 Duyệt, tìm kiếm và xem chi tiết sản phẩm (Product Catalog & Search)

- **Mô tả & Mức ưu tiên**: Hỗ trợ tra cứu, lọc linh kiện theo đặc tính kỹ thuật và xem chi tiết thông số theo từng loại sản phẩm. **Mức ưu tiên: Cao**.
- **Tác nhân**: Guest, User, Admin.
- **Luồng nghiệp vụ chính**:
  1. Người dùng chọn danh mục linh kiện, nhập từ khóa tìm kiếm hoặc điều chỉnh khoảng giá/thương hiệu.
  2. Backend truy vấn sản phẩm đang kích hoạt (`is_active = true`), áp dụng phân trang và sắp xếp theo yêu cầu.
  3. Khi xem chi tiết một sản phẩm, Backend trích xuất toàn bộ thông tin từ cột `detail` (JSONB) và danh sách đánh giá của sản phẩm đó.
- **Các yêu cầu chức năng**:
  - **REQ-PROD-1**: Hiển thị danh sách sản phẩm có phân trang, hỗ trợ sắp xếp theo giá (tăng/giảm dần) hoặc mới nhất.
  - **REQ-PROD-2**: Tìm kiếm sản phẩm theo tên linh kiện theo cơ chế gần đúng, không phân biệt hoa thường.
  - **REQ-PROD-3**: Hỗ trợ lọc đa điều kiện kết hợp: theo danh mục (`category`), khoảng giá (`minPrice` - `maxPrice`), và thương hiệu.
  - **REQ-PROD-4**: Hiển thị chi tiết sản phẩm gồm giá bán, ảnh sản phẩm, số lượng tồn kho và bảng thông số kỹ thuật đặc thù trích xuất từ dữ liệu `detail` (JSONB).
  - **REQ-PROD-5**: Hiển thị trạng thái còn hàng/hết hàng dựa trên `stock_quantity`.

---

## 4.3 Quản lý giỏ hàng và đặt hàng COD (Cart & Order Processing)

- **Mô tả & Mức ưu tiên**: Hỗ trợ giỏ hàng cá nhân, đặt hàng với phương thức thanh toán khi nhận hàng (COD), xem lịch sử và hủy đơn hàng. **Mức ưu tiên: Cao**.
- **Tác nhân**: Khách hàng thành viên (User).
- **Luồng nghiệp vụ chính**:
  1. User thêm linh kiện hoặc bộ PC Case vào giỏ hàng; Backend kiểm tra tồn kho (`stock_quantity >= quantity`) trước khi cập nhật.
  2. Tại trang Checkout, User nhập địa chỉ, số điện thoại và xác nhận đặt hàng với phương thức COD.
  3. Backend mở giao dịch (`@Transactional`): tạo đơn hàng ở trạng thái `PENDING`, lưu chi tiết mặt hàng kèm đơn giá thời điểm đặt (`unit_price`), trừ tồn kho và làm trống giỏ hàng.
  4. User có thể xem lịch sử đơn hàng hoặc hủy đơn nếu đơn hàng vẫn đang ở trạng thái `PENDING` (hệ thống tự động hoàn lại tồn kho).
- **Các yêu cầu chức năng**:
  - **REQ-ORD-1**: Quản lý giỏ hàng cá nhân (thêm, cập nhật số lượng, xóa linh kiện lẻ hoặc bộ PC Case).
  - **REQ-ORD-2**: Kiểm tra tồn kho trước khi thêm vào giỏ và trước khi tạo đơn hàng (`stock_quantity >= quantity`).
  - **REQ-ORD-3**: Tạo đơn hàng mới với hình thức thanh toán COD, lưu địa chỉ giao hàng và cố định đơn giá thời điểm mua.
  - **REQ-ORD-4**: Xem danh sách lịch sử đơn hàng kèm trạng thái (`PENDING`, `CONFIRMED`, `SHIPPING`, `DELIVERED`, `CANCELLED`).
  - **REQ-ORD-5**: Cho phép người dùng hủy đơn hàng của mình khi đang ở trạng thái `PENDING` và tự động hoàn lại số lượng tồn kho.

---

## 4.4 Đánh giá sản phẩm (Product Reviews)

- **Mô tả & Mức ưu tiên**: Khách hàng đã nhận hàng đánh giá chất lượng sản phẩm (1–5 sao kèm nhận xét). **Mức ưu tiên: Trung bình**.
- **Tác nhân**: Khách hàng thành viên (User - đánh giá), Khách vãng lai (Guest - xem).
- **Luồng nghiệp vụ chính**:
  1. User truy cập sản phẩm đã mua trong đơn hàng đã giao thành công (`DELIVERED`), gửi số sao và nhận xét.
  2. Backend kiểm tra điều kiện mua hàng và giới hạn mỗi user chỉ đánh giá 1 lần/sản phẩm.
  3. Hệ thống lưu đánh giá, tự động tính điểm sao trung bình và hiển thị công khai.
- **Các yêu cầu chức năng**:
  - **REQ-REV-1**: Chỉ cho phép đánh giá nếu người dùng đã mua sản phẩm và đơn hàng đã ở trạng thái `DELIVERED`; tối đa 1 đánh giá/sản phẩm.
  - **REQ-REV-2**: Đánh giá bắt buộc bao gồm điểm số từ 1 đến 5 sao và nhận xét văn bản.
  - **REQ-REV-3**: Hiển thị công khai danh sách đánh giá và tự động tính điểm sao trung bình của sản phẩm/PC Case.
  - **REQ-REV-4**: Cho phép người dùng chỉnh sửa hoặc xóa đánh giá của chính mình.

---

## 4.5 Trợ lý ảo Chatbot AI — RAG và Gợi ý cấu hình PC (AI Assistant)

- **Mô tả & Mức ưu tiên**: Tự động giải đáp chính sách cửa hàng bằng RAG và tư vấn cấu hình PC phù hợp với ngân sách/nhu cầu từ danh mục có sẵn. **Mức ưu tiên: Cao**.
- **Tác nhân**: Guest, User, Google Gemini API.
- **Luồng nghiệp vụ chính**:
  1. Người dùng gửi tin nhắn qua widget chat (`POST /api/chat`); hệ thống tự động phân loại ý định (`RAG` hoặc `PC_CONFIG`).
  2. **Nhánh RAG**: Tạo vector embedding câu hỏi -> truy vấn top-5 chunk liên quan nhất trên `pgvector` bằng cosine distance -> đưa vào prompt cho Gemini sinh câu trả lời chính xác theo tài liệu.
  3. **Nhánh Gợi ý PC**: Truy vấn danh sách PC Case đang kích hoạt (`is_active = true`) và có **100% linh kiện thành phần còn hàng** (`stock_quantity > 0`) -> đưa vào prompt cho Gemini chọn và tư vấn 1–3 bộ PC Case phù hợp nhất.
- **Các yêu cầu chức năng**:
  - **REQ-AI-1**: Cung cấp API `/api/chat` tiếp nhận tin nhắn văn bản (không bắt buộc đăng nhập) và tự động nhận diện ý định hội thoại.
  - **REQ-AI-2**: Tạo vector nhúng cho câu hỏi và truy vấn top-5 đoạn tài liệu tương đồng nhất trên `pgvector` bằng toán tử `<=>`.
  - **REQ-AI-3**: Tổng hợp ngữ cảnh tài liệu và gọi Gemini Chat API để sinh câu trả lời chính sách mạch lạc, chính xác.
  - **REQ-AI-4**: Chỉ truy vấn và gửi cho AI các bộ PC Case đang kích hoạt và toàn bộ linh kiện thành phần có `stock_quantity > 0`.
  - **REQ-AI-5**: Chatbot phân tích nhu cầu/ngân sách của người dùng, lựa chọn 1–3 bộ PC Case tối ưu nhất từ danh sách có sẵn kèm phân tích ưu điểm.
  - **REQ-AI-6**: Tuân thủ nguyên tắc chống ảo giác (Anti-hallucination): AI tuyệt đối không tự ý ghép nối linh kiện ngoài danh mục PC Case đã cung cấp.

---

## 4.6 Quản lý cấu hình PC Case & Thuật toán kiểm tra tương thích (PC Case Management)

- **Mô tả & Mức ưu tiên**: Admin tạo và quản lý cấu hình PC hoàn chỉnh; hệ thống tự động kiểm tra 8 ràng buộc phần cứng trước khi lưu. **Mức ưu tiên: Cao**.
- **Tác nhân**: Quản trị viên (Admin).
- **Luồng nghiệp vụ chính**:
  1. Admin chọn linh kiện cho 8 vị trí bắt buộc trong bộ PC Case và nhấn kiểm tra/lưu.
  2. `CompatibilityCheckerService` đọc thông số từ trường `detail` (JSONB) của từng linh kiện và kiểm tra tuần tự 8 ràng buộc.
  3. Nếu có vi phạm, trả về lỗi 422 kèm danh sách lỗi chi tiết; nếu hợp lệ, tính tổng giá tự động và lưu vào CSDL.
- **Các yêu cầu chức năng**:
  - **REQ-CASE-1**: Quản lý danh sách PC Case (lọc theo mục đích sử dụng, xem chi tiết linh kiện thành phần và tổng giá).
  - **REQ-CASE-2**: Bắt buộc chọn đầy đủ linh kiện cho 8 vị trí: CPU, Mainboard, RAM, GPU, Storage, PSU, Case, CPU Cooler.
  - **REQ-CASE-3**: Thuật toán kiểm định tự động bắt buộc thỏa mãn đồng thời 8 ràng buộc phần cứng:
    1. Socket CPU trùng khớp Socket Mainboard (`CPU.socket == MAINBOARD.socket`).
    2. Chuẩn RAM được Mainboard hỗ trợ (`RAM.type == MAINBOARD.memory_type`).
    3. Chuẩn kích thước Mainboard được Vỏ Case hỗ trợ (`MAINBOARD.form_factor ∈ CASE.form_factor_support`).
    4. Chiều dài GPU không vượt quá giới hạn Case (`GPU.length_mm <= CASE.max_gpu_length_mm`).
    5. Chiều cao tản nhiệt không vượt quá giới hạn Case (`CPU_COOLER.height_mm <= CASE.max_cooler_height_mm`).
    6. Socket CPU nằm trong danh sách hỗ trợ của Tản nhiệt (`CPU.socket ∈ CPU_COOLER.socket_support`).
    7. Công suất nguồn an toàn: `(CPU.tdp_w + GPU.tdp_w) <= PSU.wattage_w * 0.8`.
    8. Toàn bộ linh kiện được chọn phải có số lượng tồn kho `stock_quantity > 0`.
  - **REQ-CASE-4**: Cung cấp API `POST /api/admin/pc-cases/validate` cho phép kiểm tra tương thích độc lập trước khi lưu.
  - **REQ-CASE-5**: Tự động tính tổng giá bán của bộ PC Case dựa trên tổng đơn giá hiện hành của các linh kiện thành phần.

---

## 4.7 Quản trị sản phẩm, kho hàng và đơn hàng (Admin Operations)

- **Mô tả & Mức ưu tiên**: Hỗ trợ vận hành quản lý danh mục sản phẩm (thông số JSONB, ảnh Cloudinary) và xử lý quy trình đơn hàng. **Mức ưu tiên: Cao**.
- **Tác nhân**: Quản trị viên (Admin).
- **Luồng nghiệp vụ chính**:
  1. Admin thêm/sửa sản phẩm: tải ảnh lên Cloudinary, nhập thông tin chung và các thông số kỹ thuật riêng biệt lưu vào cột `detail` (JSONB).
  2. Admin theo dõi danh sách đơn hàng toàn hệ thống và cập nhật trạng thái đơn hàng theo quy trình.
- **Các yêu cầu chức năng**:
  - **REQ-ADM-1**: Thêm mới sản phẩm kèm theo cấu trúc thông số kỹ thuật JSONB `detail` tương ứng với từng danh mục linh kiện.
  - **REQ-ADM-2**: Tích hợp tải ảnh sản phẩm lên Cloudinary và lưu đường dẫn URL CDN an toàn vào cơ sở dữ liệu.
  - **REQ-ADM-3**: Cập nhật thông tin, giá bán, số lượng tồn kho và hỗ trợ xóa mềm (`is_active = false`) để bảo toàn dữ liệu lịch sử đơn hàng.
  - **REQ-ADM-4**: Xem toàn bộ danh sách đơn hàng, lọc theo trạng thái và xem chi tiết người nhận, địa chỉ, linh kiện đặt mua.
  - **REQ-ADM-5**: Cập nhật trạng thái đơn hàng theo quy trình tuần tự (`PENDING` -> `CONFIRMED` -> `SHIPPING` -> `DELIVERED` hoặc hủy sang `CANCELLED`).

---

## 4.8 Quản lý tài liệu RAG và Thống kê kinh doanh (RAG & Statistics)

- **Mô tả & Mức ưu tiên**: Quản lý cơ sở tri thức cho Chatbot AI qua tài liệu văn bản và cung cấp báo cáo thống kê tình hình kinh doanh. **Mức ưu tiên: Trung bình**.
- **Tác nhân**: Quản trị viên (Admin).
- **Luồng nghiệp vụ chính**:
  1. Admin upload tài liệu chính sách (PDF, DOCX, TXT); hệ thống bóc tách văn bản, chia chunk và gọi Gemini Embedding API tạo vector lưu vào `pgvector`.
  2. Admin theo dõi dashboard thống kê kinh doanh thông qua các truy vấn tổng hợp SQL.
- **Các yêu cầu chức năng**:
  - **REQ-RAG-1**: Cho phép tải lên các tệp tài liệu chính sách cửa hàng định dạng PDF, DOCX, TXT.
  - **REQ-RAG-2**: Tự động chia nhỏ nội dung tài liệu thành các đoạn văn bản (chunks) kèm đoạn gối đầu (overlap) để giữ ngữ cảnh.
  - **REQ-RAG-3**: Gửi từng chunk tới Gemini Embedding API để tạo vector 768 chiều và lưu vào bảng `rag_chunks` trong PostgreSQL (`pgvector`).
  - **REQ-RAG-4**: Xem danh sách tài liệu RAG đã nạp và xóa tài liệu lỗi thời (tự động xóa sạch các chunk vector liên quan).
  - **REQ-STAT-1**: Thống kê tổng doanh thu theo ngày, tháng, năm.
  - **REQ-STAT-2**: Thống kê số lượng và tỷ lệ phần trăm đơn hàng theo từng trạng thái xử lý.
  - **REQ-STAT-3**: Thống kê danh sách Top sản phẩm bán chạy nhất theo số lượng và doanh thu.
  - **REQ-STAT-4**: Thống kê số lượng người dùng mới đăng ký theo chu kỳ thời gian.

# Các yêu cầu phi chức năng

## 5.1 Yêu cầu thực thi (Performance Requirements)

1. **Thời gian đáp ứng (Response Time)**:
   - Các API đọc dữ liệu (`GET /api/products`, `GET /api/cart`): Thời gian phản hồi Backend dưới **500ms** (P95 Latency). Tải trang phía Client dưới **1.5 giây**.
   - Các thao tác ghi dữ liệu (`POST /api/orders`, cập nhật giỏ hàng): Thời gian xử lý dưới **1.0 giây**.
   - Thuật toán kiểm định 8 ràng buộc phần cứng của PC Case: Thời gian thực thi dưới **200ms**.
   - Phân hệ Chatbot AI: Thời gian truy vấn embedding và tìm kiếm top-5 chunk trên `pgvector` dưới **500ms**; tổng thời gian nhận phản hồi từ Gemini API gửi về client trung bình từ **3.0 đến 5.0 giây** (Timeout tối đa 30 giây).
2. **Thông lượng và tải đồng thời**:
   - Phục vụ ổn định từ **50 đến 100 người dùng đồng thời** (Concurrent Users) trên cấu hình máy chủ tiêu chuẩn (2 Cores CPU, 4GB RAM).
   - Thông lượng máy chủ Backend đạt tối thiểu **100 RPS** đối với các truy vấn đọc.
3. **Tối ưu hóa cơ sở dữ liệu**:
   - Thiết lập chỉ mục B-Tree trên các cột tìm kiếm và lọc: `products(category, price, is_active, name)`, `orders(user_id, status, created_at)`.
   - Thiết lập chỉ mục vector `ivfflat` trên cột `rag_chunks(embedding)` với toán tử `vector_cosine_ops`.
   - Cấu hình HikariCP connection pool tối đa 20 kết nối đồng thời.

## 5.2 Yêu cầu an toàn (Safety Requirements)

1. **Toàn vẹn giao dịch (ACID) & Chống bán quá tồn kho**:
   - Các thao tác đặt hàng, trừ kho, hủy đơn hoàn kho bắt buộc bọc trong `@Transactional`. Mọi lỗi phát sinh phải được Rollback 100%.
   - Kiểm tra tồn kho tại thời điểm ghi đơn, đảm bảo `stock_quantity >= 0`, không xảy ra hiện tượng âm kho khi nhiều người cùng đặt hàng.
2. **Xử lý sự cố và suy giảm tính năng (Graceful Degradation)**:
   - Xử lý ngoại lệ tập trung qua `GlobalExceptionHandler` (`@ControllerAdvice`), trả về JSON chuẩn `ApiResponse<T>`, không làm lộ Stack Trace ra ngoài.
   - Khi dịch vụ Google Gemini API gặp sự cố hoặc cạn quota, hệ thống phản hồi lỗi thân thiện mà không gây gián đoạn các luồng mua bán thông thường.
3. **Sao lưu dữ liệu**: Thiết lập sao lưu định kỳ cơ sở dữ liệu PostgreSQL hàng ngày (Daily Backup).

## 5.3 Yêu cầu bảo mật (Security Requirements)

1. **Xác thực và Quản lý phiên**:
   - Sử dụng chuẩn JWT (HMAC-SHA256) không trạng thái: Access Token có thời hạn ngắn (15–60 phút), Refresh Token (7–30 ngày) lưu trong HttpOnly Cookie có cờ `Secure`, `SameSite=Strict`.
   - Khóa bí mật `JWT_SECRET` được cấu hình qua biến môi trường máy chủ, không lưu cứng trong mã nguồn.
2. **Kiểm soát phân quyền (RBAC) & Chống IDOR**:
   - Phân quyền nghiêm ngặt tại tầng Spring Security Filter Chain cho 3 vai trò: `GUEST`, `USER`, `ADMIN`.
   - Phòng chống lỗ hổng IDOR: Người dùng chỉ được xem/hủy đơn hàng của chính mình (kiểm tra quyền sở hữu `user_id` tại Backend).
3. **Mã hóa và Bảo vệ dữ liệu**:
   - Mật khẩu người dùng bắt buộc băm một chiều bằng thuật toán **BCrypt** (Strength >= 10) kèm Salt ngẫu nhiên trước khi lưu vào CSDL.
   - Toàn bộ lưu lượng mạng Client - Server và Server - Third Party được mã hóa qua kênh truyền **HTTPS / TLS 1.2+**.
4. **Phòng chống lỗ hổng OWASP**:
   - Sử dụng PreparedStatements qua Spring Data JPA để chống SQL Injection.
   - Kiểm tra dữ liệu đầu vào bằng Jakarta Validation (`@Valid`) kết hợp cơ chế mã hóa đầu ra của React để phòng ngừa XSS.
   - Cấu hình CORS chặt chẽ, chỉ cho phép Origin từ tên miền của Frontend.

## 5.4 Các đặc điểm chất lượng phần mềm (Software Quality Attributes)

- **Tính sẵn có (Availability)**: Duy trì thời gian hoạt động ổn định tối thiểu **99.0%**; giám sát sức khỏe dịch vụ qua endpoint `/actuator/health`.
- **Tính dễ bảo trì (Maintainability)**: Mã nguồn phân tầng rõ ràng (`controller`, `service`, `repository`, `entity`, `dto`, `exception`, `security`); tuân thủ quy ước đặt tên và commit Conventional Commits.
- **Tính dễ sử dụng (Usability)**: Giao diện trực quan với Shadcn UI & Tailwind CSS, hỗ trợ responsive trên mọi thiết bị; tối ưu hóa quy trình đặt hàng COD trong vòng 3 bước.
- **Tính khả chuyển (Portability)**: Đóng gói toàn bộ Backend, Frontend và PostgreSQL (`pgvector`) qua Docker và Docker Compose, dễ dàng triển khai trên môi trường phát triển và máy chủ sản xuất.
- **Tính tin cậy và độ chính xác (Reliability)**:
  - Thuật toán kiểm tra 8 ràng buộc tương thích phần cứng đạt độ chính xác kỹ thuật 100%.
  - Chatbot AI tuân thủ nguyên tắc chống ảo giác: 100% PC Case gợi ý phải là cấu hình có sẵn và toàn bộ linh kiện còn hàng trong kho.

## 5.5 Các quy tắc nghiệp vụ cốt lõi (Business Rules)

| Mã quy tắc | Tên quy tắc | Nội dung quy tắc |
| :--- | :--- | :--- |
| **BR-01** | **Hủy đơn hàng** | Khách hàng chỉ có thể tự hủy đơn hàng trực tuyến khi đơn hàng đang ở trạng thái `PENDING`. Khi đã chuyển sang `CONFIRMED`, `SHIPPING` hoặc `DELIVERED`, khách hàng không thể tự hủy trên website. |
| **BR-02** | **Đánh giá sản phẩm** | Chỉ người dùng đã mua sản phẩm trong đơn hàng giao thành công (`DELIVERED`) mới có quyền đánh giá và chấm điểm sao; mỗi người dùng chỉ đánh giá tối đa **1 lần / sản phẩm** (`UNIQUE(user_id, product_id)`). |
| **BR-03** | **Đóng băng đơn giá** | Tại thời điểm đặt hàng thành công, đơn giá sản phẩm phải được lưu cố định vào trường `unit_price` của chi tiết đơn hàng, không bị ảnh hưởng bởi biến động giá sản phẩm trong tương lai. |
| **BR-04** | **Kiểm định tương thích PC Case** | Bộ PC Case chỉ được lưu nếu thỏa mãn đầy đủ **8/8** ràng buộc phần cứng: Socket CPU-Mainboard, Chuẩn RAM, Form Factor Case, Chiều dài GPU, Chiều cao Tản nhiệt, Socket Tản nhiệt, Công suất PSU an toàn 80%, và Tồn kho linh kiện > 0. Vi phạm sẽ bị từ chối với lỗi 422. |
| **BR-05** | **Gợi ý PC chống ảo giác** | Chatbot AI chỉ được chọn từ danh mục các bộ PC Case do Admin tạo sẵn, đang kích hoạt (`is_active = true`) và toàn bộ linh kiện còn hàng (`stock_quantity > 0`). Tuyệt đối không tự ý ghép linh kiện ngoài danh mục. |
| **BR-06** | **Xóa mềm dữ liệu** | Khi xóa sản phẩm linh kiện hoặc cấu hình PC Case, hệ thống chỉ cập nhật cờ `is_active = false` (soft delete) nhằm bảo toàn dữ liệu lịch sử đơn hàng và đánh giá đã phát sinh. |
| **BR-07** | **Thanh toán & Tiền tệ** | Phương thức thanh toán duy nhất áp dụng là Thanh toán khi nhận hàng (**COD**); đơn vị tiền tệ thống nhất là Việt Nam Đồng (**VND**). |
| **BR-08** | **Định danh người dùng** | Mỗi tài khoản người dùng gắn liền với một địa chỉ Email duy nhất (`UNIQUE`) trong hệ thống. |

# Các yêu cầu khác

&lt;Định nghĩa các yêu cầu khác mà chúng chưa được trình bày. Có thể bao gồm các yêu cầu về cơ sở dữ liệu, các yêu cầu về phong tục – văn hóa, các yêu cầu luật pháp, các mục tiêu tái sử dụng của dự án, v.v. &gt;

Phụ lục A: Các mô hình phân tích

&lt;Tùy chọn, bao gồm các mô hình phân tích như các lưu đồ dòng dữ liệu, lưu đồ lớp, lưu đồ chuyển dịch trạng thái, hay lưu đồ thực thể - quan hệ.&gt;

Phụ lục B: TBD – Danh sách sẽ được xác định

&lt;Thu thập một danh sách được đánh số của các tham khảo TBD (To Be Determine) mà chúng vẫn còn trong tài liệu đặc tả.&gt;
