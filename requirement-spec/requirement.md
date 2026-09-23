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

Tài liệu Đặc tả Yêu cầu Phần mềm (Software Requirements Specification - SRS) này định nghĩa chi tiết và toàn diện các yêu cầu chức năng, yêu cầu phi chức năng, kiến trúc logic, giao diện và các ràng buộc kỹ thuật của hệ thống **"Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình"** (*Computer Components Shop with AI Integration*). Tài liệu đóng vai trò là cơ sở kỹ thuật chính thức giữa các bên tham gia dự án, làm nền tảng cho việc thiết kế kiến trúc, hiện thực hóa mã nguồn, kiểm thử phần mềm và nghiệm thu kết quả đề tài niên luận ngành Công nghệ thông tin.

Các nhóm đối tượng sử dụng tài liệu này bao gồm:

- **Đội ngũ phát triển (Developers - Frontend & Backend)**: Nắm vững các yêu cầu nghiệp vụ, cấu trúc dữ liệu linh hoạt (JSONB), các giao tiếp RESTful API, thuật toán kiểm tra ràng buộc tương thích phần cứng và quy trình tích hợp mô hình trí tuệ nhân tạo (Google Gemini API & pgvector).
- **Đội ngũ kiểm thử (Testers / QA)**: Sử dụng tài liệu làm căn cứ để thiết kế kế hoạch kiểm thử (Test Plan), xây dựng các kịch bản kiểm thử (Test Cases), kiểm tra tính tương thích giữa các linh kiện trong PC Case, kiểm tra tính đúng đắn của luồng mua sắm và đánh giá độ chính xác, an toàn của chatbot AI.
- **Giảng viên hướng dẫn & Hội đồng đánh giá**: Theo dõi tiến độ triển khai dự án, đánh giá mức độ hoàn thành và chất lượng kỹ thuật của sản phẩm so với các mục tiêu đề tài đã đề ra.
- **Quản trị viên hệ thống (Admin)**: Hiểu rõ phạm vi hoạt động của hệ thống, quy trình quản lý kho hàng linh kiện, cơ chế tạo cấu hình PC mẫu, cách thức cập nhật tài liệu chính sách cho AI RAG và khai thác báo cáo thống kê.

## Phạm vi sản phẩm

- **Tên sản phẩm**: Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình (*Computer Components Shop with AI Integration*).
- **Mục đích của sản phẩm**:
  Hệ thống được xây dựng nhằm cung cấp một nền tảng thương mại điện tử chuyên sâu trong lĩnh vực bán lẻ linh kiện máy tính (PC parts), kết hợp sức mạnh của Trí tuệ nhân tạo (Generative AI) để tự động hóa quy trình tư vấn kỹ thuật và hỗ trợ khách hàng 24/7. Sản phẩm bao gồm ba phân hệ trọng tâm:
  1. **Phân hệ Thương mại điện tử (E-commerce Core)**:
     - Cho phép khách hàng tìm kiếm, duyệt danh mục và lọc linh kiện chuyên sâu theo các đặc tính kỹ thuật riêng biệt của từng loại phần cứng (CPU, Mainboard, RAM, GPU, SSD/HDD, Nguồn, Vỏ Case, Tản nhiệt).
     - Hỗ trợ đầy đủ chu trình mua sắm: quản lý giỏ hàng, đặt hàng với phương thức thanh toán khi nhận hàng (COD), theo dõi trạng thái và lịch sử đơn hàng.
     - Cho phép người mua đánh giá sản phẩm (xếp hạng 1–5 sao kèm nhận xét) đối với các mặt hàng đã mua thành công.
  2. **Phân hệ Trợ lý ảo AI (AI Chatbot Service)**:
     - *Hỏi đáp chính sách cửa hàng (RAG - Retrieval-Augmented Generation)*: Tự động tra cứu và giải đáp chính xác các thắc mắc liên quan đến chính sách bảo hành, đổi trả, vận chuyển và phương thức thanh toán dựa trên cơ sở tri thức do quản trị viên cung cấp (thông qua kỹ thuật tìm kiếm vector tương đồng cosine với `pgvector` và Gemini Embedding API), loại bỏ hiện tượng ảo giác thông tin.
     - *Tư vấn gợi ý cấu hình PC (PC Configuration Suggestion)*: Tiếp nhận yêu cầu bằng ngôn ngữ tự nhiên từ người dùng về ngân sách và nhu cầu sử dụng (học tập, làm việc văn phòng, gaming, đồ họa - dựng video...). Chatbot sẽ phân tích và gợi ý 1–3 bộ PC Case hoàn chỉnh phù hợp nhất. Điểm mấu chốt là AI **chỉ được phép lựa chọn** từ danh mục các cấu hình PC Case đã được Admin tạo và kiểm định tương thích từ trước, đồng thời đảm bảo toàn bộ linh kiện thành phần đều còn hàng trong kho (`stock_quantity > 0`), tuyệt đối không tự ý ghép nối linh kiện tùy tiện.
  3. **Phân hệ Quản trị (Admin Panel)**:
     - Quản lý danh mục và thông số sản phẩm linh hoạt thông qua thuộc tính kỹ thuật dạng JSONB.
     - Quản lý và xử lý đơn hàng theo quy trình trạng thái rõ ràng.
     - Tạo và quản lý các bộ cấu hình PC mẫu (PC Case) tích hợp thuật toán tự động kiểm định ràng buộc tương thích phần cứng trước khi lưu.
     - Quản lý tài liệu RAG (upload tài liệu văn bản, tự động chia đoạn và nhúng vector).
     - Theo dõi dashboard thống kê kinh doanh trực quan (doanh thu, đơn hàng, sản phẩm bán chạy, người dùng mới).
- **Lợi ích và mục tiêu kinh doanh**:
  - *Đối với người dùng*: Tháo gỡ hoàn toàn rào cản kỹ thuật phức tạp về sự tương thích linh kiện phần cứng; giúp người dùng dễ dàng lựa chọn cấu hình máy tính tối ưu cho ngân sách mà không lo sai sót kỹ thuật; hỗ trợ giải đáp chính sách minh bạch, nhanh chóng mọi lúc mọi nơi.
  - *Đối với doanh nghiệp/cửa hàng*: Tự động hóa khâu tư vấn khách hàng 24/7, giảm thiểu chi phí nhân sự trực chat; nâng cao tỷ lệ chuyển đổi từ khách tham khảo thành đơn hàng thực tế; quản lý kho hàng và cấu hình máy tính tập trung, khoa học và tin cậy.

## Bảng chú giải thuật ngữ

Bảng dưới đây định nghĩa các thuật ngữ kỹ thuật, từ viết tắt và khái niệm chuyên ngành được sử dụng trong toàn bộ tài liệu đặc tả:

| STT | Thuật ngữ / Từ viết tắt | Định nghĩa / Giải thích |
| :---: | :--- | :--- |
| 1 | **SRS** (Software Requirements Specification) | Tài liệu đặc tả yêu cầu phần mềm, mô tả toàn diện hành vi, chức năng và ràng buộc kỹ thuật của hệ thống. |
| 2 | **AI** (Artificial Intelligence) | Trí tuệ nhân tạo, công nghệ mô phỏng các quá trình suy nghĩ và học hỏi của con người bằng máy tính. |
| 3 | **LLM** (Large Language Model) | Mô hình ngôn ngữ lớn, mô hình học sâu được huấn luyện trên lượng dữ liệu văn bản khổng lồ để hiểu và sinh ngôn ngữ tự nhiên. |
| 4 | **RAG** (Retrieval-Augmented Generation) | Kỹ thuật tăng cường sinh văn bản bằng cách truy xuất thông tin từ một cơ sở tri thức ngoại vi trước khi đưa vào mô hình ngôn ngữ lớn để trả lời. |
| 5 | **pgvector** | Tiện ích mở rộng (extension) mã nguồn mở của PostgreSQL cho phép lưu trữ, đánh chỉ mục và tìm kiếm vector tương đồng (vector similarity search). |
| 6 | **Embedding** | Quá trình biểu diễn ngữ nghĩa của văn bản (từ, đoạn văn) dưới dạng một vector số thực nhiều chiều (ví dụ: vector 768 chiều). |
| 7 | **Cosine Similarity / Cosine Distance** | Độ đo hình học tính toán góc cosin giữa hai vector trong không gian đa chiều, dùng để xác định mức độ tương đồng ngữ nghĩa giữa câu hỏi và đoạn tài liệu. |
| 8 | **Anti-hallucination** | Kỹ thuật / nguyên tắc thiết kế prompt và ràng buộc hệ thống nhằm ngăn ngừa hiện tượng mô hình AI bịa đặt hoặc cung cấp thông tin sai lệch ngoài thực tế. |
| 9 | **PC Case** | Trong tài liệu này, ngoài nghĩa vỏ thùng máy tính, "PC Case" còn được dùng để chỉ **một bộ cấu hình máy tính hoàn chỉnh** (gồm 8 linh kiện thành phần đã được kiểm tra tương thích). |
| 10 | **JSONB** (Binary JSON) | Kiểu dữ liệu trong PostgreSQL lưu trữ tài liệu JSON dưới định dạng nhị phân đã phân tích cú pháp, hỗ trợ đánh chỉ mục và truy vấn dữ liệu phi cấu trúc với hiệu năng cao. |
| 11 | **CPU** (Central Processing Unit) | Bộ vi xử lý trung tâm, đóng vai trò là não bộ tính toán và điều khiển của máy tính. |
| 12 | **GPU / VGA** (Graphics Processing Unit) | Bộ xử lý đồ họa / Card màn hình chuyên dụng xử lý các tác vụ đồ họa, hình ảnh, dựng video và chơi game. |
| 13 | **RAM** (Random Access Memory) | Bộ nhớ truy xuất ngẫu nhiên, lưu trữ tạm thời dữ liệu cho các ứng dụng đang thực thi. |
| 14 | **Mainboard / Motherboard** | Bo mạch chủ kết nối toàn bộ các linh kiện phần cứng máy tính với nhau. |
| 15 | **PSU** (Power Supply Unit) | Bộ nguồn máy tính chuyển đổi dòng điện xoay chiều thành dòng điện một chiều cấp cho các linh kiện trong máy. |
| 16 | **TDP** (Thermal Design Power) | Công suất thiết kế nhiệt (đơn vị: Watt), chỉ mức tiêu thụ điện năng tối đa và lượng nhiệt phát sinh mà hệ thống tản nhiệt cần giải tỏa. |
| 17 | **Socket** | Đế cắm cơ học và kết nối điện tử trên bo mạch chủ dùng để lắp đặt bộ vi xử lý CPU (ví dụ: LGA1700, AM5). |
| 18 | **Form Factor** | Tiêu chuẩn quy định kích thước vật lý và hình dạng của linh kiện phần cứng (ví dụ: chuẩn bo mạch chủ ATX, Micro-ATX, Mini-ITX). |
| 19 | **JWT** (JSON Web Token) | Chuẩn mở (RFC 7519) định nghĩa phương thức truyền tải thông tin an toàn giữa các bên dưới dạng đối tượng JSON có chữ ký số. |
| 20 | **HttpOnly Cookie** | Thuộc tính của Cookie ngăn chặn mã kịch bản JavaScript phía Client truy xuất, giúp bảo vệ phiên làm việc và phòng chống tấn công XSS. |
| 21 | **RBAC** (Role-Based Access Control) | Cơ chế kiểm soát truy cập dựa trên vai trò của người dùng (Guest, User, Admin). |
| 22 | **COD** (Cash On Delivery) | Phương thức thanh toán bằng tiền mặt khi nhận hàng. |
| 23 | **SPA** (Single Page Application) | Ứng dụng web đơn trang, chỉ tải một trang HTML duy nhất và cập nhật nội dung động bằng JavaScript mà không cần tải lại toàn bộ trang. |
| 24 | **RESTful API** | Kiểu kiến trúc giao tiếp phần mềm qua giao thức HTTP dựa trên các phương thức chuẩn (GET, POST, PUT, DELETE). |
| 25 | **IDOR** (Insecure Direct Object References) | Lỗ hổng kiểm soát truy cập cho phép kẻ tấn công thay đổi tham số định danh để truy cập trái phép dữ liệu của người khác. |

## Tài liệu tham khảo

Dưới đây là danh mục các tài liệu tiêu chuẩn, tài liệu kỹ thuật và hướng dẫn được tham chiếu trong quá trình xây dựng tài liệu đặc tả này (các tài liệu tham khảo mẫu học thuật phục vụ đề tài niên luận):

1. **IEEE Computer Society**, *IEEE Std 830-1998: IEEE Recommended Practice for Software Requirements Specifications*, IEEE, New York, NY, USA, 1998.
2. **Khoa Công nghệ Thông tin**, *Đề cương và Hướng dẫn thực hiện đề tài Niên luận ngành Công nghệ thông tin / Kỹ thuật phần mềm*, Trường Đại học, 2026.
3. **Nhóm phát triển đề tài**, *problem-description.md & AGENTS.md — Tài liệu mô tả bài toán và kiến trúc kỹ thuật hệ thống Computer Components Shop with AI Integration*, Kho lưu trữ dự án, 2026.
4. **PostgreSQL Global Development Group**, *PostgreSQL 15.0 Documentation*, 2022. [Trực tuyến]. Địa chỉ: https://www.postgresql.org/docs/15/
5. **Andrew Kane**, *pgvector: Open-source vector similarity search for Postgres*, GitHub Repository, 2023. [Trực tuyến]. Địa chỉ: https://github.com/pgvector/pgvector
6. **Google AI for Developers**, *Google Gemini API Documentation & Text Embeddings Guide*, Google, 2024. [Trực tuyến]. Địa chỉ: https://ai.google.dev/docs
7. **VMware Tanzu / Spring Team**, *Spring Boot Reference Documentation (Version 3.x) & Spring Security Architecture*, 2024. [Trực tuyến]. Địa chỉ: https://docs.spring.io/spring-boot/docs/current/reference/html/
8. **Cloudinary Ltd.**, *Cloudinary Java SDK & Image Management API Guide*, 2024. [Trực tuyến]. Địa chỉ: https://cloudinary.com/documentation
9. **Meta Open Source & Vercel**, *React Documentation & Vite Build Tool Reference*, 2024. [Trực tuyến]. Địa chỉ: https://react.dev/ và https://vitejs.dev/
10. **The Open Web Application Security Project (OWASP)**, *OWASP Top 10 Web Application Security Risks*, 2021. [Trực tuyến]. Địa chỉ: https://owasp.org/www-project-top-ten/

## Bố cục tài liệu

Tài liệu Đặc tả Yêu cầu Phần mềm này được cấu trúc thành 6 phần chính và các phụ lục theo chuẩn IEEE Std 830:

- **Phần 1: Giới thiệu (Introduction)**: Xác định mục tiêu của tài liệu, đối tượng sử dụng, phạm vi sản phẩm phần mềm, bảng chú giải các thuật ngữ kỹ thuật, tài liệu tham khảo và bố cục tổng quan.
- **Phần 2: Mô tả tổng quan (Overall Description)**: Trình bày bối cảnh của sản phẩm trong hệ thống tổng thể kèm sơ đồ kiến trúc, tóm tắt các chức năng chính, đặc điểm các nhóm người dùng, môi trường vận hành, các ràng buộc thiết kế & thực thi, cùng các giả định và phụ thuộc.
- **Phần 3: Các yêu cầu giao tiếp bên ngoài (External Interface Requirements)**: Mô tả chi tiết giao diện người sử dụng (hệ thống màn hình Client và Admin), giao tiếp phần cứng, giao tiếp phần mềm (PostgreSQL, Gemini API, Cloudinary) và giao tiếp truyền thông tin an toàn (HTTPS, CORS, Cookie).
- **Phần 4: Các tính năng của hệ thống (System Features)**: Đặc tả chi tiết 8 nhóm tính năng chức năng nghiệp vụ của hệ thống (Xác thực, Tra cứu sản phẩm, Giỏ hàng & Đặt hàng COD, Đánh giá sản phẩm, Chatbot AI RAG & PC Config, Quản lý PC Case & Thuật toán tương thích, Quản trị kho hàng & Đơn hàng, Quản lý RAG & Thống kê), mỗi tính năng đều kèm theo mô tả, mức ưu tiên, chuỗi đáp ứng và mã định danh yêu cầu `REQ-xxx-n`.
- **Phần 5: Các yêu cầu phi chức năng (Non-functional Requirements)**: Định nghĩa các yêu cầu về hiệu năng thực thi (thời gian đáp ứng, thông lượng), an toàn dữ liệu (giao dịch ACID, chống bán quá tồn kho, sao lưu), an ninh bảo mật (JWT, RBAC, BCrypt, phòng chống OWASP), các đặc điểm chất lượng phần mềm và bảng 8 quy tắc nghiệp vụ cốt lõi (`BR-01` đến `BR-08`).
- **Phần 6: Các yêu cầu khác & Phụ lục (Other Requirements & Appendices)**: Đề cập đến các yêu cầu mở rộng trong tương lai, sơ đồ phân tích mô hình hóa và các nội dung cần xác định tiếp theo.

### Bảng hướng dẫn đọc tài liệu theo vai trò:

| Nhóm đối tượng người đọc | Mục đích tiếp cận tài liệu | Các phần khuyến nghị nên đọc kỹ |
| :--- | :--- | :--- |
| **Đội ngũ phát triển (Developers)** | Hiểu rõ kiến trúc, luồng dữ liệu, cấu trúc JSONB, quy cách API, thuật toán kiểm tra tương thích phần cứng và pipeline RAG/AI để hiện thực mã nguồn. | **Phần 2**, **Phần 3**, **Phần 4** (toàn bộ các yêu cầu chức năng `REQ`), và **Phần 5** (ràng buộc kỹ thuật, bảo mật). |
| **Đội ngũ kiểm thử (Testers / QA)** | Xây dựng kịch bản kiểm thử, kiểm tra tính đúng đắn của quy trình mua hàng, kiểm thử thuật toán tương thích và độ chính xác của phản hồi AI. | **Mục 1.2**, **Phần 4** (chuỗi đáp ứng và yêu cầu `REQ`), **Mục 5.1** (hiệu năng), và **Mục 5.5** (quy tắc nghiệp vụ). |
| **Giảng viên hướng dẫn & Hội đồng** | Đánh giá tổng quan quy mô đề tài, tính khả thi, mức độ đáp ứng mục tiêu đề ra và chất lượng học thuật của tài liệu đặc tả. | **Phần 1**, **Phần 2**, **Mục 4.x.1** (mức ưu tiên và lợi ích), và **Mục 5.5** (quy tắc nghiệp vụ). |
| **Quản trị viên hệ thống (Admin)** | Hiểu rõ quy trình vận hành cửa hàng, quản lý cấu hình PC Case, nạp tài liệu chính sách RAG và xem báo cáo thống kê. | **Mục 1.2**, **Mục 2.2**, **Mục 2.3**, **Mục 4.6**, **Mục 4.7**, **Mục 4.8**, và **Mục 5.5**. |

# Mô tả tổng quan

## Bối cảnh của sản phẩm

Hệ thống **"Ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình"** là một sản phẩm phần mềm hoàn chỉnh, độc lập, được nghiên cứu và xây dựng mới nhằm phục vụ đề tài niên luận ngành Kỹ thuật phần mềm. Hệ thống kết hợp giữa mô hình thương mại điện tử chuyên ngành linh kiện phần cứng máy tính và công nghệ Trí tuệ nhân tạo tạo sinh (Generative AI).

Sản phẩm được xây dựng dựa trên kiến trúc phân tầng hiện đại, tách biệt hoàn toàn giữa Client (Frontend) và Server (Backend), giao tiếp hai chiều thông qua các giao thức mạng tiêu chuẩn (HTTPS / RESTful API). Hệ thống bao gồm 2 kho mã nguồn (repository) độc lập:
- **Client (Frontend)**: Xây dựng dưới dạng Single Page Application (SPA) bằng React, Vite, TypeScript, giao diện người dùng sử dụng Shadcn UI và Tailwind CSS, quản lý trạng thái tập trung với Zustand.
- **Server (Backend)**: Xây dựng bằng Java và Spring Boot framework, quản lý truy xuất dữ liệu thông qua Spring Data JPA và Hibernate, kiểm soát bảo mật và phân quyền với Spring Security và JWT.
- **Cơ sở dữ liệu tập trung**: PostgreSQL 15+ tích hợp phần mở rộng `pgvector` cho phép lưu trữ song song cả dữ liệu nghiệp vụ quan hệ (người dùng, sản phẩm, đơn hàng, cấu hình máy tính) và dữ liệu vector embedding (phục vụ cơ chế tìm kiếm tương đồng vector của RAG).
- **Các dịch vụ tích hợp bên ngoài (External Services)**:
  - **Google Gemini API**: Đóng vai trò là bộ não xử lý ngôn ngữ tự nhiên, bao gồm *Gemini Embedding API* (tạo vector ngữ nghĩa 768 chiều cho văn bản tài liệu và câu hỏi của người dùng) và *Gemini Chat / Generative Model* (tổng hợp câu trả lời chính sách dựa trên ngữ cảnh được cung cấp và đóng vai trò chuyên gia phân tích gợi ý cấu hình PC).
  - **Cloudinary API**: Dịch vụ lưu trữ đám mây và phân phối hình ảnh sản phẩm chất lượng cao qua mạng phân phối nội dung (CDN).

Dưới đây là sơ đồ khối kiến trúc tổng thể của hệ thống:

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
│  PostgreSQL    │   │   pgvector     │  │  Cloudinary CDN      │
│  (Main Data)   │   │  (RAG Embeds)  │  │  (Product Images)    │
└────────────────┘   └────────────────┘  └──────────────────────┘
```

## Các chức năng của sản phẩm

Hệ thống cung cấp một tập hợp các chức năng toàn diện từ bán lẻ trực tuyến đến quản trị vận hành và trợ lý thông minh. Các chức năng được phân loại thành 7 nhóm chính sau:

1. **Quản lý xác thực và phân quyền (Authentication & Authorization)**:
   - Đăng ký tài khoản người dùng mới với thông tin cơ bản (họ tên, email, mật khẩu, số điện thoại, địa chỉ,...).
   - Đăng nhập hệ thống, cấp phát mã truy cập Access Token (JWT) và Refresh Token lưu trữ an toàn trong HttpOnly Cookie.
   - Phân quyền chặt chẽ theo 3 vai trò: Khách vãng lai (Guest), Khách hàng thành viên (User) và Quản trị viên (Admin).

2. **Duyệt, tìm kiếm và tra cứu sản phẩm (Product Browsing & Search)**:
   - Duyệt danh mục sản phẩm theo các nhóm linh kiện máy tính: CPU, Mainboard, RAM, GPU, Ổ cứng (Storage), Nguồn (PSU), Vỏ máy tính (Case), Tản nhiệt (CPU Cooler).
   - Tìm kiếm sản phẩm theo tên hoặc từ khóa liên quan.
   - Bộ lọc đa tiêu chí: Lọc theo danh mục linh kiện, khoảng giá thành và thương hiệu.
   - Xem trang thông tin chi tiết sản phẩm: Hiển thị đầy đủ hình ảnh, giá bán, số lượng tồn kho và bảng thông số kỹ thuật chi tiết đặc thù được lưu trữ linh hoạt dưới dạng JSONB.

3. **Quản lý giỏ hàng và đặt hàng (Cart & Order Processing)**:
   - Quản lý giỏ hàng cá nhân: Thêm linh kiện vào giỏ hàng, cập nhật số lượng, xóa từng linh kiện hoặc làm trống giỏ hàng.
   - Đặt hàng trực tuyến hỗ trợ phương thức thanh toán khi nhận hàng (COD), lưu trữ địa chỉ giao hàng và ghi chú đơn hàng.
   - Quản lý lịch sử đơn hàng cá nhân: Xem danh sách các đơn hàng đã đặt kèm trạng thái thực tế (PENDING, CONFIRMED, SHIPPING, DELIVERED, CANCELLED).
   - Cho phép người dùng hủy đơn hàng khi đơn hàng đang ở trạng thái chờ xác nhận (PENDING).

4. **Đánh giá và nhận xét sản phẩm (Product Reviews)**:
   - Khách hàng đã mua hàng và nhận hàng thành công có quyền viết nhận xét và chấm điểm sao (từ 1 đến 5 sao) cho sản phẩm đã mua (mỗi người dùng đánh giá tối đa 1 lần/sản phẩm).
   - Xem danh sách đánh giá của các khách hàng khác và điểm đánh giá sao trung bình của từng sản phẩm.
   - Người dùng có thể chỉnh sửa hoặc xóa đánh giá của chính mình.

5. **Trợ lý ảo thông minh Chatbot AI (AI Assistant Services)**:
   - Tự động tiếp nhận thông điệp của người dùng, phân tích và phân loại ý định (classify intent) thành 2 nhánh:
     - *Nhánh RAG (Hỏi đáp chính sách)*: Chuyển đổi câu hỏi thành vector embedding, truy vấn top-K đoạn tài liệu liên quan nhất từ cơ sở dữ liệu `pgvector`, tổng hợp ngữ cảnh và gửi tới Google Gemini API để tạo câu trả lời chính xác, đáng tin cậy về chính sách bảo hành, đổi trả, thanh toán và giao hàng.
     - *Nhánh PC Config (Tư vấn gợi ý cấu hình PC)*: Tiếp nhận yêu cầu bằng ngôn ngữ tự nhiên về ngân sách (ví dụ: "khoảng 20 triệu") và mục đích sử dụng (gaming, văn phòng, đồ họa...), truy vấn danh sách các bộ PC Case đang khả dụng (is_active = true) và tất cả linh kiện thành phần còn hàng trong kho (`stock_quantity > 0`), nhồi vào prompt để Gemini lựa chọn và tư vấn từ 1 đến 3 cấu hình tối ưu nhất kèm phân tích chi tiết.

6. **Quản lý cấu hình PC mẫu và Kiểm tra tương thích (PC Case & Compatibility Engine)**:
   - Quản trị viên khởi tạo và cấu hình các bộ máy tính hoàn chỉnh (PC Case) bằng cách lựa chọn linh kiện cụ thể cho từng vị trí slot.
   - Hệ thống tự động thực thi thuật toán kiểm định tính tương thích phần cứng (`CompatibilityCheckerService`) với các quy tắc kỹ thuật nghiêm ngặt:
     1. Socket CPU phải trùng khớp với Socket Mainboard (`CPU.socket == MAINBOARD.socket`).
     2. Chuẩn RAM phải tương thích với Mainboard (`RAM.type == MAINBOARD.memory_type`).
     3. Chuẩn kích thước Mainboard phải nằm trong danh sách hỗ trợ của Vỏ Case (`MAINBOARD.form_factor ∈ CASE.form_factor_support`).
     4. Chiều dài Card đồ họa không vượt quá giới hạn chiều dài của Vỏ Case (`GPU.length_mm <= CASE.max_gpu_length_mm`).
     5. Chiều cao Tản nhiệt CPU không vượt quá giới hạn chiều cao của Vỏ Case (`CPU_COOLER.height_mm <= CASE.max_cooler_height_mm`).
     6. Socket CPU phải nằm trong danh mục hỗ trợ của Tản nhiệt CPU (`CPU.socket ∈ CPU_COOLER.socket_support`).
     7. Tổng công suất tiêu thụ của CPU và GPU phải nằm trong ngưỡng an toàn của Nguồn máy tính (`(CPU.tdp_w + GPU.tdp_w) <= PSU.wattage_w * 0.8`).
     8. Toàn bộ các linh kiện được chọn phải có số lượng tồn kho lớn hơn 0 (`stock_quantity > 0`).
   - Cập nhật, kích hoạt/hủy kích hoạt và xóa bỏ (soft delete) các bộ PC Case.

7. **Quản trị vận hành cửa hàng và Thống kê số liệu (Admin Operations & Analytics)**:
   - Quản lý sản phẩm: Thêm mới, chỉnh sửa thông tin, giá bán, số lượng tồn kho, tải hình ảnh lên Cloudinary và xóa sản phẩm (soft delete).
   - Quản lý đơn hàng: Xem danh sách toàn bộ đơn hàng của khách hàng trên hệ thống, thực hiện cập nhật chuyển đổi trạng thái đơn hàng (PENDING -> CONFIRMED -> SHIPPING -> DELIVERED).
   - Quản lý tài liệu RAG: Upload các tệp tài liệu chính sách của cửa hàng (PDF, DOCX, TXT), hệ thống tự động bóc tách thành các chunks, tính toán vector embedding và lưu vào cơ sở dữ liệu `pgvector`; xem danh sách và xóa tài liệu lỗi thời.
   - Thống kê và báo cáo số liệu: Thống kê doanh thu theo mốc thời gian (ngày, tháng, năm), thống kê đơn hàng theo trạng thái xử lý, danh sách các sản phẩm bán chạy nhất (Top Products) và thống kê tốc độ tăng trưởng người dùng mới.

## Đặc điểm người sử dụng

Hệ thống phục vụ ba nhóm người dùng chính với các đặc điểm, quyền hạn và tần suất tương tác khác nhau:

| Tiêu chí | Khách vãng lai (Guest) | Khách hàng thành viên (User) | Quản trị viên (Admin) |
| :--- | :--- | :--- | :--- |
| **Mô tả đối tượng** | Khách truy cập ẩn danh, chưa đăng ký hoặc chưa đăng nhập tài khoản. | Khách hàng đã đăng ký tài khoản và đăng nhập thành công vào hệ thống. | Nhân viên quản lý cửa hàng, kỹ thuật viên có chuyên môn về phần cứng máy tính. |
| **Tần suất sử dụng** | Không thường xuyên, phụ thuộc vào nhu cầu tham khảo hoặc mua sắm đột xuất. | Định kỳ hoặc thường xuyên khi có nhu cầu mua sắm linh kiện, nâng cấp máy tính hoặc theo dõi đơn hàng. | Hàng ngày, liên tục trong giờ làm việc để vận hành hệ thống kinh doanh. |
| **Chức năng sử dụng chính** | - Tìm kiếm, lọc và xem thông tin sản phẩm.<br>- Xem đánh giá sản phẩm từ cộng đồng.<br>- Trò chuyện với Chatbot AI để hỏi đáp chính sách hoặc xin gợi ý cấu hình PC.<br>- Đăng ký tài khoản mới. | Thừa hưởng toàn bộ quyền của Guest, đồng thời:<br>- Quản lý giỏ hàng cá nhân.<br>- Đặt hàng (COD) và hủy đơn hàng.<br>- Xem lịch sử và tiến độ đơn hàng.<br>- Viết đánh giá sản phẩm đã mua thành công. | Thừa hưởng toàn bộ quyền của User, đồng thời:<br>- Quản lý kho sản phẩm (CRUD, upload ảnh).<br>- Duyệt và cập nhật trạng thái đơn hàng.<br>- Thiết lập PC Case và kiểm tra tương thích.<br>- Nạp và quản lý tài liệu RAG.<br>- Xem bảng điều khiển thống kê doanh thu. |
| **Trình độ tin học & Kỹ năng** | Từ cơ bản đến nâng cao; nhiều người dùng thiếu kiến thức chuyên sâu về độ tương thích phần cứng máy tính. | Phổ thông; thành thạo các thao tác mua hàng trực tuyến trên nền tảng thương mại điện tử. | Nâng cao; có kiến thức chuyên sâu về phần cứng máy tính (socket, TDP, form factor...) và quy trình nghiệp vụ bán lẻ. |
| **Mức độ ưu tiên đối với hệ thống** | Nhóm người dùng tiềm năng, tạo nguồn chuyển đổi khách hàng. | **Nhóm người dùng trọng tâm nhất**, trực tiếp tạo ra doanh thu và giá trị thương mại cho cửa hàng. | Nhóm người dùng vận hành, quyết định chất lượng dữ liệu và sự ổn định của hệ thống bán hàng. |

## Môi trường vận hành

Sản phẩm được thiết kế để vận hành ổn định trên các nền tảng sau:

1. **Môi trường phía Người dùng (Client-side)**:
   - **Thiết bị hỗ trợ**: Máy tính để bàn (PC), máy tính xách tay (Laptop), máy tính bảng (Tablet) và điện thoại thông minh (Smartphone).
   - **Giao diện hiển thị**: Hỗ trợ thiết kế thích ứng (Responsive Web Design) tự động tối ưu hóa bố cục theo độ phân giải màn hình.
   - **Trình duyệt web**: Hỗ trợ đầy đủ các phiên bản mới nhất của các trình duyệt web phổ biến: Google Chrome (phiên bản 100+), Mozilla Firefox (phiên bản 100+), Microsoft Edge (phiên bản 100+), Apple Safari (phiên bản 15+). Yêu cầu trình duyệt bật JavaScript, hỗ trợ HTML5, CSS3 và cho phép lưu trữ Cookie / Web Storage.

2. **Môi trường phía Máy chủ ứng dụng (Server-side)**:
   - **Hệ điều hành**: Windows, Linux (Ubuntu 20.04/22.04 LTS, Debian 11/12, Rocky Linux) hoặc Windows Server 2019/2022. Khuyến nghị triển khai trên môi trường Docker container để đảm bảo tính nhất quán.
   - **Nền tảng thực thi**: Java Development Kit (JDK) phiên bản 17 hoặc 21 (LTS).
   - **Framework máy chủ**: Spring Boot phiên bản 3.x với máy chủ web nhúng Apache Tomcat.
   - **Yêu cầu tài nguyên tối thiểu**: CPU 2 Cores, RAM tối thiểu 2GB (khuyến nghị 4GB trở lên), dung lượng đĩa trống tối thiểu 10GB.

3. **Môi trường Cơ sở dữ liệu (Database Server)**:
   - **Hệ quản trị cơ sở dữ liệu**: PostgreSQL phiên bản 15.0 trở lên.
   - **Phần mở rộng bắt buộc**: Extension `pgvector` phục vụ việc lưu trữ kiểu dữ liệu vector và thực thi các truy vấn tìm kiếm độ tương đồng cosine index (`ivfflat`).

4. **Dịch vụ mạng và Dịch vụ đám mây tích hợp (External Services)**:
   - **Google Gemini API**: Đòi hỏi kết nối Internet ổn định, có API Key hợp lệ và được cấp quota cho các model Gemini Chat và Text-Embedding.
   - **Cloudinary Service**: Dịch vụ lưu trữ và phân phối hình ảnh qua giao thức bảo mật HTTPS.
   - **Mạng truyền thông**: Hạ tầng mạng hỗ trợ băng thông ổn định, chứng chỉ số bảo mật SSL/TLS phục vụ giao tiếp HTTPS giữa Client, Server và các bên thứ ba.

## Các ràng buộc về thực thi và thiết kế

Quá trình thiết kế và phát triển hệ thống phải tuân thủ nghiêm ngặt các ràng buộc kỹ thuật, nghiệp vụ và an toàn sau:

1. **Ràng buộc về kiến trúc và giao tiếp hệ thống**:
   - Kiến trúc tách biệt độc lập giữa Frontend (React SPA) và Backend (Spring Boot REST API). Toàn bộ dữ liệu trao đổi giữa hai tầng này bắt buộc sử dụng định dạng JSON qua giao thức HTTPS.
   - Mọi response API gửi từ Backend phải được đóng gói thống nhất trong một cấu trúc wrapper chuẩn `ApiResponse<T>`:
     ```json
     {
       "success": true,
       "message": "Thông báo trạng thái",
       "data": { ... }
     }
     ```
   - Tất cả các yêu cầu nhận dữ liệu đầu vào (Request Body) tại các Controller phải được định nghĩa bằng các lớp DTO riêng biệt và xác thực tự động thông qua annotation `@Valid` (Jakarta Validation). Không cho phép đưa trực tiếp các lớp Entity JPA ra ngoài tầng Controller.

2. **Ràng buộc lưu trữ và mô hình dữ liệu (Database Schema Constraints)**:
   - Đặc tính kỹ thuật của các nhóm linh kiện máy tính rất khác biệt (ví dụ CPU có `socket`, `cores`, `tdp_w`; Mainboard có `chipset`, `form_factor`, `memory_slots`; RAM có `bus_speed`, `capacity_gb`; Nguồn có `wattage_w`, `efficiency`). Do đó, bảng `products` bắt buộc phải sử dụng trường `detail` kiểu dữ liệu `JSONB` của PostgreSQL để lưu trữ linh hoạt thông số kỹ thuật riêng của từng danh mục mà không làm phình to hoặc phá vỡ cấu trúc bảng cơ sở dữ liệu khi mở rộng.

3. **Ràng buộc thuật toán kiểm định tương thích phần cứng (Hardware Compatibility Rules)**:
   - Hệ thống không cho phép lưu trữ bất kỳ cấu hình PC Case nào khi chưa vượt qua đầy đủ các kiểm tra tương thích kỹ thuật trong `CompatibilityCheckerService`. Khi phát hiện vi phạm, hệ thống phải trả về mã lỗi HTTP 422 (Unprocessable Entity) kèm theo mảng liệt kê chi tiết các vi phạm tương thích để Admin khắc phục.

4. **Ràng buộc nghiệp vụ đối với Trợ lý ảo Chatbot AI**:
   - **Nguyên tắc chống ảo giác (Anti-hallucination)**: Mô hình AI KHÔNG ĐƯỢC tự ý lắp ráp hoặc đề xuất các linh kiện ngẫu nhiên nằm ngoài hệ thống. Chatbot chỉ được phép lựa chọn và giới thiệu từ danh mục các bộ PC Case đã được Admin tạo và kiểm tra tương thích từ trước.
   - **Ràng buộc tồn kho thực tế**: Tại thời điểm người dùng yêu cầu tư vấn, hệ thống chỉ truy vấn và gửi cho AI những bộ PC Case mà **toàn bộ linh kiện thành phần đều đang có số lượng tồn kho lớn hơn 0** (`stock_quantity > 0`).

5. **Ràng buộc về an ninh và bảo mật (Security Constraints)**:
   - Áp dụng cơ chế xác thực Stateless Token-based thông qua chuẩn JWT.
   - Thời gian sống của Access Token được giới hạn ngắn (từ 15 đến 60 phút) để giảm thiểu nguy cơ khi bị rò rỉ mã token.
   - Refresh Token có thời hạn dài hơn (từ 7 đến 30 ngày) và bắt buộc phải được lưu trữ trong `HttpOnly` Cookie với các cờ bảo mật (`SameSite=Strict`, `Secure`) nhằm ngăn chặn tấn công đánh cắp phiên qua Cross-Site Scripting (XSS).
   - Toàn bộ mật khẩu của người dùng phải được băm một chiều bằng thuật toán mã hóa an toàn BCrypt với Salt ngẫu nhiên trước khi ghi xuống cơ sở dữ liệu.
   - Áp dụng cơ chế phân quyền kiểm soát truy cập dựa trên vai trò (Role-Based Access Control - RBAC) tại tầng bộ lọc của Spring Security.

6. **Ràng buộc về công nghệ và tiêu chuẩn mã nguồn**:
   - Backend: Sử dụng ngôn ngữ Java (phiên bản 17 trở lên), Spring Boot 3.x, công cụ quản lý dự án Maven. Đặt tên lớp theo `PascalCase`, phương thức và biến theo `camelCase`.
   - Frontend: Sử dụng React 18+, Vite, TypeScript, cấu trúc quản lý trạng thái bằng Zustand, thư viện UI Shadcn UI kết hợp Tailwind CSS.

## Các giả định và phụ thuộc

1. **Các giả định của dự án (Assumptions)**:
   - Người sử dụng hệ thống sở hữu thiết bị có khả năng kết nối mạng Internet ổn định và được cài đặt trình duyệt web tiêu chuẩn.
   - Quản trị viên nhập liệu thông tin sản phẩm và các thông số kỹ thuật (trong trường `detail` của sản phẩm) một cách chính xác, đầy đủ và tuân thủ đúng chuẩn cấu trúc JSON quy định của từng danh mục.
   - Các tài liệu chính sách do quản trị viên tải lên cho hệ thống RAG là các tài liệu văn bản tiếng Việt hợp lệ, rõ ràng, không chứa nội dung độc hại hay sai lệch so với chính sách hoạt động thực tế của cửa hàng.
   - Phương thức thanh toán triển khai trong phạm vi đề tài niên luận là phương thức thanh toán khi nhận hàng (COD), đơn vị tiền tệ áp dụng thống nhất là Việt Nam Đồng (VND).

2. **Các yếu tố phụ thuộc bên ngoài (Dependencies)**:
   - **Google Gemini API**: Phân hệ Chatbot AI phụ thuộc hoàn toàn vào tính khả dụng, độ trễ mạng, tính ổn định và hạn mức gọi (quota / rate limit) từ dịch vụ Google Gemini (cả mô hình text-embedding và mô hình hội thoại ngôn ngữ lớn). Trong trường hợp dịch vụ AI gặp sự cố hoặc cạn kiệt quota, phân hệ Chatbot sẽ trả về thông báo lỗi tạm thời nhưng không được làm ảnh hưởng đến hoạt động mua bán bình thường của các phân hệ e-commerce khác.
   - **Dịch vụ lưu trữ hình ảnh đám mây Cloudinary**: Việc tải lên, lưu trữ và kết xuất hình ảnh của các linh kiện máy tính phụ thuộc vào dịch vụ Cloudinary. Nếu dịch vụ này gián đoạn, hình ảnh sản phẩm có thể không hiển thị được đúng cách.
   - **Phần mở rộng `pgvector` trên PostgreSQL**: Việc phân tích tương đồng ngữ nghĩa vector trong hệ thống RAG phụ thuộc vào việc extension `pgvector` được cài đặt chính xác và hoạt động ổn định trên máy chủ cơ sở dữ liệu PostgreSQL.

# Các yêu cầu giao tiếp bên ngoài

## Giao diện người sử dụng

### 1. Phong cách thiết kế tổng thể và Tiêu chuẩn GUI
Giao diện người dùng của hệ thống được xây dựng dưới dạng Single Page Application (SPA) hiện đại sử dụng thư viện **React**, **Vite** và **TypeScript**. Hệ thống giao diện áp dụng ngôn ngữ thiết kế tối giản, trực quan và hiện đại của **Shadcn UI** kết hợp với **Tailwind CSS**, mang phong cách đặc trưng của các sàn thương mại điện tử linh kiện công nghệ.
- **Bảng màu và Typography**: Sử dụng bảng màu trung tính chuyên nghiệp (đen, xám đậm, trắng) kết hợp với các màu nhấn công nghệ (xanh dương hoặc tím neon) để làm nổi bật các nút hành động (Call To Action - CTA). Font chữ không chân (sans-serif như Inter, Roboto) giúp tăng khả năng đọc trên mọi kích thước màn hình.
- **Thiết kế thích ứng (Responsive Web Design)**: Toàn bộ các trang và thành phần giao diện tuân thủ các điểm ngắt (breakpoints) tiêu chuẩn của Tailwind CSS (`sm: 640px`, `md: 768px`, `lg: 1024px`, `xl: 1280px`), tự động tối ưu hóa trải nghiệm hiển thị từ màn hình di động nhỏ, máy tính bảng đến màn hình máy tính để bàn độ phân giải cao.
- **Quy chuẩn thông báo và phản hồi trạng thái**:
  - Thông báo nổi (Toast notifications) thông qua thư viện Sonner/Toast hiển thị ở góc màn hình để báo hiệu kết quả các thao tác (Thêm vào giỏ hàng thành công, Lỗi kiểm tra dữ liệu, Đặt hàng thành công, v.v.).
  - Hiệu ứng tải dữ liệu bộ xương (Skeleton Loaders) được áp dụng khi chờ dữ liệu phản hồi từ Backend REST API nhằm hạn chế tình trạng giật cục layout (Cumulative Layout Shift).
  - Hộp thoại xác nhận (Confirmation Modals) đối với các hành động quan trọng có nguy cơ rủi ro cao (Hủy đơn hàng, Xóa sản phẩm khỏi kho, Xóa tài liệu RAG, Xóa cấu hình PC Case).

### 2. Các màn hình chính phía Khách hàng (Client Portal)
- **Trang chủ (HomePage)**:
  - Khối biểu ngữ (Banner) quảng cáo chương trình ưu đãi và cấu hình PC nổi bật.
  - Danh mục truy cập nhanh các nhóm linh kiện máy tính (CPU, Mainboard, RAM, GPU, Ổ cứng, Nguồn, Case, Tản nhiệt).
  - Khối sản phẩm bán chạy nhất (Top Sellers) và sản phẩm mới về kho.
  - Nút biểu tượng cửa sổ chat nổi (Chat widget) ở góc dưới bên phải màn hình, cho phép mở nhanh giao diện trò chuyện với Trợ lý ảo AI.
- **Trang danh mục và lọc sản phẩm (ProductListPage)**:
  - Thanh tìm kiếm sản phẩm theo từ khóa tên linh kiện.
  - Bảng điều khiển bộ lọc (Filter Sidebar) bên trái: Cho phép lọc theo nhóm danh mục linh kiện, thanh trượt lọc khoảng giá (Price range slider), lọc theo thương hiệu sản xuất.
  - Khu vực hiển thị kết quả sản phẩm: Trình bày dạng lưới các thẻ sản phẩm (`ProductCard`) gồm hình ảnh đại diện (lấy từ Cloudinary), tên linh kiện, giá niêm yết, tình trạng tồn kho và nút thêm nhanh vào giỏ hàng. Hỗ trợ sắp xếp theo giá (tăng/giảm dần) và phân trang dữ liệu.
- **Trang chi tiết sản phẩm (ProductDetailPage)**:
  - Bộ sưu tập hình ảnh sản phẩm (Image Gallery) hỗ trợ phóng to (zoom) và xem nhiều góc chụp.
  - Khu vực thông tin thương mại: Tên sản phẩm, giá bán chính thức, số lượng tồn kho còn lại (`stock_quantity`), bộ chọn số lượng cần mua và nút "Thêm vào giỏ hàng" (`Add to Cart`).
  - Bảng thông số kỹ thuật chi tiết (Technical Specifications): Tự động trích xuất và hiển thị trực quan các cặp thuộc tính - giá trị từ trường `detail` (JSONB) tùy theo danh mục (ví dụ: CPU hiển thị socket, số nhân, số luồng, xung nhịp, TDP; RAM hiển thị chuẩn DDR, bus, dung lượng; GPU hiển thị dung lượng VRAM, chiều dài card, công suất nguồn khuyến nghị...).
  - Khu vực đánh giá sản phẩm (Product Reviews): Hiển thị điểm sao trung bình (1–5 sao), tổng số lượt đánh giá, danh sách các nhận xét từ khách hàng đã mua sản phẩm; form cho phép khách hàng đã mua sản phẩm gửi đánh giá mới hoặc cập nhật đánh giá cũ.
- **Trang giỏ hàng (CartPage)**:
  - Bảng danh sách các linh kiện đang chọn: Ảnh thu nhỏ, tên sản phẩm, đơn giá, bộ tăng giảm số lượng sản phẩm, thành tiền cho từng dòng và nút xóa sản phẩm khỏi giỏ.
  - Khung tóm tắt đơn hàng: Tổng tiền thanh toán tạm tính và nút dẫn đến trang tiến hành đặt hàng ("Thanh toán ngay").
- **Trang đặt hàng / Thanh toán (CheckoutPage)**:
  - Biểu mẫu nhập thông tin người nhận: Họ và tên, số điện thoại, địa chỉ nhận hàng chi tiết và trường ghi chú giao hàng.
  - Lựa chọn phương thức thanh toán: Mặc định áp dụng phương thức Thanh toán khi nhận hàng (COD - Cash On Delivery).
  - Tóm tắt lại danh sách mặt hàng, số lượng và tổng số tiền phải thanh toán khi nhận hàng.
  - Nút "Xác nhận đặt hàng" kích hoạt gửi yêu cầu tạo đơn hàng và chuyển hướng sang trang thông báo thành công.
- **Trang lịch sử đơn hàng (OrderHistoryPage)**:
  - Bảng liệt kê các đơn hàng đã đặt của tài khoản: Mã đơn hàng, ngày đặt, tổng tiền, phương thức thanh toán và huy hiệu trạng thái đơn hàng (PENDING, CONFIRMED, SHIPPING, DELIVERED, CANCELLED).
  - Hỗ trợ xem chi tiết đơn hàng (danh sách linh kiện, đơn giá tại thời điểm mua, địa chỉ nhận hàng).
  - Nút "Hủy đơn hàng" hiển thị khả dụng khi đơn hàng đang ở trạng thái `PENDING`.
- **Giao diện Chatbot AI (ChatBox / ChatPage)**:
  - Thiết kế khung chat hiện đại, hỗ trợ mở rộng toàn màn hình hoặc thu nhỏ thành widget nổi góc màn hình.
  - Khung hiển thị lịch sử đối thoại phân định rõ ràng giữa tin nhắn của người dùng và tin nhắn phản hồi của Trợ lý AI.
  - Hỗ trợ định dạng Markdown (in đậm, danh sách gạch đầu dòng, bảng biểu) đối với các câu trả lời giải đáp chính sách cửa hàng.
  - Hiển thị các khối gợi ý cấu hình PC trực quan (Interactive PC Case Cards): Mỗi cấu hình gợi ý hiển thị tên bộ máy, mục đích sử dụng (Gaming, Văn phòng, Đồ họa...), tổng giá thành, danh sách các linh kiện thành phần cấu thành và nút xem chi tiết để người dùng có thể bấm thêm nhanh cả bộ cấu hình vào giỏ hàng.
- **Trang xác thực tài khoản (Auth Pages)**:
  - Form Đăng nhập: Ô nhập Email và Mật khẩu, liên kết dẫn đến trang Đăng ký tài khoản.
  - Form Đăng ký: Các trường nhập Họ và tên, Email, Mật khẩu, Số điện thoại và Địa chỉ.
  - Tích hợp kiểm tra lỗi trực tiếp trên giao diện (Client-side validation) cho định dạng email hợp lệ, độ dài mật khẩu và bắt buộc nhập các trường thiết yếu.

### 3. Các màn hình phía Quản trị viên (Admin Panel)
- **Bảng điều khiển thống kê (StatisticsDashboard)**:
  - Các thẻ chỉ số tổng quan (KPI Cards): Tổng doanh thu lũy kế, tổng số đơn hàng đã hoàn tất, tổng số khách hàng đăng ký và tổng số mặt hàng đang kinh doanh.
  - Biểu đồ đường/cột biểu diễn doanh thu theo chu kỳ thời gian (theo ngày trong tháng, theo tháng trong năm).
  - Biểu đồ tròn thể hiện tỷ lệ cơ cấu đơn hàng theo các trạng thái xử lý.
  - Bảng thống kê Top 5 / Top 10 sản phẩm bán chạy nhất hệ thống.
- **Quản lý danh mục & sản phẩm (ProductManagement)**:
  - Bảng danh sách sản phẩm với các bộ lọc tìm kiếm nhanh theo tên, danh mục và khoảng giá.
  - Modal tạo mới / cập nhật sản phẩm: Cho phép chọn danh mục linh kiện, tự động hiển thị các trường nhập liệu thông số kỹ thuật tương ứng với danh mục đó để lưu vào JSONB `detail`; tích hợp khu vực chọn tệp hình ảnh để tải trực tiếp lên Cloudinary.
  - Thao tác xóa mềm sản phẩm (soft delete) để ngừng kinh doanh mà không làm mất tính toàn vẹn dữ liệu lịch sử đơn hàng.
- **Quản lý đơn hàng (OrderManagement)**:
  - Bảng dữ liệu theo dõi toàn bộ đơn hàng của cửa hàng kèm bộ lọc trạng thái đơn hàng.
  - Xem chi tiết từng đơn hàng và dropdown cho phép Quản trị viên chuyển đổi trạng thái đơn hàng theo đúng quy trình nghiệp vụ (`PENDING` -> `CONFIRMED` -> `SHIPPING` -> `DELIVERED` hoặc chuyển sang `CANCELLED`).
- **Quản lý cấu hình PC Case (PcCaseManagement)**:
  - Danh sách các bộ cấu hình PC Case đã được tạo trên hệ thống kèm tổng giá bán và mục đích sử dụng.
  - Biểu mẫu thiết lập cấu hình: Cho phép Admin chọn từng linh kiện cho đủ 8 vị trí slot (CPU, Mainboard, RAM, GPU, Storage, PSU, Case, CPU Cooler).
  - Nút "Kiểm tra tương thích" (Validate): Kích hoạt gọi API kiểm tra thuật toán 8 ràng buộc phần cứng, hiển thị trực quan các vi phạm màu đỏ (nếu có lỗi) hoặc thông báo tích xanh hợp lệ kèm tổng công suất tiêu thụ và tổng chi phí ước tính.
- **Quản lý tài liệu tri thức RAG (RagDocumentManagement)**:
  - Khu vực kéo thả tải lên các tệp tài liệu chính sách của cửa hàng hỗ trợ các định dạng PDF, DOCX, TXT.
  - Bảng hiển thị danh sách tài liệu đã được nạp vào cơ sở tri thức (tên tệp, ngày nạp, số lượng chunks đã vector hóa) và nút thao tác xóa tài liệu khi chính sách có thay đổi.

## Giao tiếp phần cứng

Hệ thống được triển khai trên nền tảng ứng dụng Web theo mô hình SaaS (Software as a Service), do đó không có yêu cầu giao tiếp vật lý trực tiếp với các vi điều khiển hay trình điều khiển thiết bị (device drivers) độc quyền. Thay vào đó, hệ thống giao tiếp gián tiếp qua các giao diện phần cứng sau:

1. **Phía thiết bị đầu cuối của người dùng (Client Devices)**:
   - **Thiết bị nhập liệu**: Bàn phím chuẩn (QWERTY), chuột điều hướng hoặc màn hình cảm ứng điện dung đa điểm (Capacitive Touchscreen) trên thiết bị di động.
   - **Thiết bị hiển thị**: Màn hình có độ phân giải tối thiểu 360 x 640 pixel (đối với điện thoại thông minh) và tối ưu ở độ phân giải 1920 x 1080 pixel (Full HD) hoặc cao hơn (đối với máy tính bảng, máy tính xách tay và máy tính để bàn).
   - **Bộ nhớ thiết bị**: Thiết bị khách cần có dung lượng RAM tối thiểu 2 GB để trình duyệt web có thể phân tích và kết xuất giao diện Single Page Application mượt mà.

2. **Phía máy chủ hạ tầng (Server Infrastructure)**:
   - **Giao tiếp mạng (Network Interface Card - NIC)**: Card mạng có băng thông tối thiểu 1 Gbps (Gigabit Ethernet) để đảm bảo khả năng xử lý đồng thời hàng nghìn kết nối HTTP/HTTPS, truyền tải các tệp tài liệu RAG và gọi các API ngoại vi với độ trễ thấp.
   - **Lưu trữ dữ liệu (Storage)**: Khuyến nghị sử dụng ổ cứng thể rắn SSD chuẩn NVMe để tối ưu hóa tốc độ truy xuất I/O ngẫu nhiên (Random Read/Write) đối với cơ sở dữ liệu PostgreSQL và hoạt động quét chỉ mục không gian vector `ivfflat` của `pgvector`.
   - **Bộ xử lý trung tâm (CPU) & RAM máy chủ**: Máy chủ backend yêu cầu tối thiểu 2 Cores CPU (kiến trúc x86_64 hoặc ARM64) và 4 GB RAM để JVM thực thi tối ưu trình thu gom rác (Garbage Collection) và duy trì kết nối cơ sở dữ liệu liên tục qua HikariCP.

## Giao tiếp phần mềm

Hệ thống kết nối và tương tác chặt chẽ với các thành phần phần mềm, thư viện và dịch vụ đám mây sau:

1. **Hệ quản trị cơ sở dữ liệu PostgreSQL (v15+)**:
   - **Giao thức và Cổng**: Kết nối thông qua giao thức JDBC (Java Database Connectivity) qua cổng TCP `5432`.
   - **Phần mở rộng `pgvector`**: Sử dụng kiểu dữ liệu `VECTOR(768)` để lưu trữ vector đặc trưng của các đoạn văn bản; sử dụng toán tử `<=>` (Cosine Distance) để thực thi tìm kiếm top-K văn bản tương đồng nhất trong không gian vector.
   - **Quản lý kết nối**: Sử dụng thư viện HikariCP tích hợp sẵn trong Spring Boot để duy trì hồ bơi kết nối (Connection Pool), hạn chế việc tạo mới kết nối liên tục làm suy giảm hiệu năng.
   - **Tầng ORM**: Sử dụng Hibernate 6.x và Spring Data JPA để ánh xạ quan hệ đối tượng giữa các bảng dữ liệu (`users`, `products`, `orders`, `order_items`, `cart_items`, `product_reviews`, `pc_cases`, `pc_case_items`, `rag_documents`, `rag_chunks`) sang các Java Entities.

2. **Dịch vụ trí tuệ nhân tạo Google Gemini API**:
   - **Mô hình nhúng ngữ nghĩa (Gemini Embedding API)**:
     - Model: `text-embedding-004` (hoặc `embedding-001`).
     - Mục đích: Tiếp nhận các chuỗi văn bản (chunks tài liệu chính sách hoặc câu hỏi của người dùng) qua HTTPS POST và trả về mảng số thực 768 chiều.
   - **Mô hình ngôn ngữ lớn (Gemini Generative Chat API)**:
     - Model: `gemini-1.5-flash` hoặc `gemini-1.5-pro`.
     - Mục đích: Xử lý prompt bao gồm System Instruction, Context ngữ cảnh (từ RAG hoặc dữ liệu PC Case) và tin nhắn của người dùng; sinh câu trả lời tự nhiên hỗ trợ khách hàng.
   - **Phương thức kết nối**: Gọi REST API qua HTTPS sử dụng WebClient / RestTemplate hoặc Google GenAI Java SDK.

3. **Dịch vụ lưu trữ hình ảnh đám mây Cloudinary**:
   - **Giao thức**: HTTPS RESTful API thông qua thư viện chính thức `cloudinary-http44` (Java SDK).
   - **Mục đích**: Tiếp nhận tệp hình ảnh sản phẩm do Quản trị viên tải lên, lưu trữ trên nền tảng lưu trữ phân tán, tự động tối ưu hóa định dạng ảnh (WebP/AVIF) và kích thước; trả về đường dẫn URL an toàn (HTTPS CDN) để lưu vào trường `image_url` của bảng `products`.

4. **Giao tiếp giữa Client Frontend và Server Backend**:
   - **Giao thức**: RESTful API qua HTTPS.
   - **Quy chuẩn trao đổi dữ liệu**: Định dạng JSON (`application/json`) cho các thao tác dữ liệu nghiệp vụ và `multipart/form-data` cho các thao tác tải lên tệp tài liệu và hình ảnh.
   - **Cấu trúc gói tin chuẩn (`ApiResponse<T>`)**:
     - Khi thành công:
       ```json
       {
         "success": true,
         "message": "Thao tác thành công",
         "data": { ... }
       }
       ```
     - Khi xảy ra lỗi:
       ```json
       {
         "success": false,
         "message": "Mô tả nguyên nhân lỗi",
         "data": null
       }
       ```
   - **Cơ chế xác thực và phiên làm việc**:
     - Access Token: Chuỗi JSON Web Token (JWT) được gửi kèm trong tiêu đề HTTP `Authorization: Bearer <token>` ở mỗi yêu cầu cần xác thực.
     - Refresh Token: Chuỗi token bảo mật được lưu trữ trong Cookie với cờ `HttpOnly`, `Secure` và `SameSite=Strict`, gửi tự động đến endpoint `/api/auth/refresh` để cấp mới Access Token mà không làm gián đoạn trải nghiệm của người dùng.

5. **Môi trường hệ điều hành và công cụ nền tảng**:
   - **Hệ điều hành máy chủ**: Windows, Ubuntu Server 22.04 LTS hoặc bất kỳ bản phân phối Linux hỗ trợ Docker.
   - **Môi trường ảo hóa container**: Docker Engine 24.x và Docker Compose giúp đóng gói đồng bộ toàn bộ dịch vụ Backend, PostgreSQL và môi trường chạy.

## Giao tiếp truyền thông tin

1. **Giao thức mạng và tiêu chuẩn bảo mật truyền thông**:
   - **Giao thức truyền siêu văn bản an toàn (HTTPS)**: Toàn bộ luồng truyền thông tin giữa trình duyệt của người dùng và máy chủ Backend, cũng như giữa máy chủ Backend và các dịch vụ bên ngoài (Google Gemini API, Cloudinary) bắt buộc phải được mã hóa thông qua giao thức HTTPS sử dụng giao thức bảo mật tầng truyền vận TLS phiên bản 1.2 hoặc 1.3.
   - **Cổng giao tiếp chuẩn**:
     - Cổng `443` (TCP): Tiếp nhận mọi yêu cầu HTTPS của người dùng từ Internet vào máy chủ.
     - Cổng `80` (TCP): Tự động chuyển hướng toàn bộ lưu lượng (HTTP 301 Redirect) sang cổng 443 nhằm loại trừ rủi ro truyền thông văn bản thuần (plaintext).
     - Cổng `8080` / `5432`: Được cấu hình đóng kín trong mạng nội bộ (Internal Docker Network), chỉ mở kết nối qua Reverse Proxy (Nginx/Traefik).

2. **Quy chuẩn định dạng và mã hóa thông điệp**:
   - **Bảng mã ký tự**: Bắt buộc sử dụng chuẩn mã hóa ký tự `UTF-8` cho tất cả các thông điệp HTTP Headers, Request Body và Response Body để hỗ trợ hiển thị toàn vẹn tiếng Việt có dấu.
   - **Loại nội dung (MIME Types)**:
     - `application/json; charset=UTF-8`: Cho tất cả các cuộc gọi API trao đổi dữ liệu có cấu trúc.
     - `multipart/form-data`: Cho các luồng tải lên tài liệu RAG và ảnh linh kiện.
     - `application/pdf`, `application/vnd.openxmlformats-officedocument.wordprocessingml.document`, `text/plain`: Định dạng các tài liệu được chấp nhận cho kho tri thức RAG.

3. **Chính sách kiểm soát và bảo mật truyền thông**:
   - **Cấu hình chia sẻ tài nguyên nguồn gốc chéo (CORS - Cross-Origin Resource Sharing)**:
     - Máy chủ Backend cấu hình nghiêm ngặt danh sách các nguồn gốc (Allowed Origins) được phép truy cập, chỉ chấp nhận tên miền của Client Frontend, từ chối toàn bộ các yêu cầu từ các domain lạ nhằm chống tấn công Cross-Site Scripting và đánh cắp tài nguyên.
     - Cho phép các phương thức HTTP cần thiết: `GET`, `POST`, `PUT`, `DELETE`, `OPTIONS`.
     - Cho phép gửi kèm thông tin xác thực (`allowCredentials = true`) để hỗ trợ truyền tải HttpOnly Cookie.
   - **Quản lý thời gian chờ kết nối (Timeouts)**:
     - Thiết lập Connection Timeout (5 giây) và Read Timeout (30 giây) đối với các cuộc gọi từ Backend tới Google Gemini API nhằm ngăn ngừa việc ứng dụng bị nghẽn luồng (thread exhaustion) khi dịch vụ AI bên thứ ba phản hồi chậm.
   - **Bảo mật Cookie truyền thông**:
     - Cờ `HttpOnly`: Ngăn chặn mã kịch bản JavaScript phía trình duyệt đọc được nội dung Cookie, triệt tiêu nguy cơ đánh cắp Refresh Token thông qua lỗi XSS.
     - Cờ `Secure`: Đảm bảo Cookie chỉ được truyền tải qua các kết nối được mã hóa HTTPS.
     - Thuộc tính `SameSite=Strict` (hoặc `Lax`): Ngăn ngừa trình duyệt gửi kèm Cookie trong các truy vấn chéo trang, bảo vệ hệ thống trước tấn công giả mạo yêu cầu chéo trang (CSRF).

# Các tính năng của hệ thống

Hệ thống được tổ chức thành 8 nhóm tính năng chức năng chính, bao quát toàn bộ quy trình nghiệp vụ từ phía người dùng đến quản trị viên và các dịch vụ tích hợp trí tuệ nhân tạo.

---

## 4.1 Quản lý xác thực và tài khoản người dùng (Authentication & User Management)

### 4.1.1 Mô tả và mức ưu tiên
Tính năng này cung cấp các cơ chế định danh, xác thực và phân quyền cho người dùng hệ thống. Hệ thống áp dụng mô hình xác thực phi trạng thái (Stateless Authentication) dựa trên chuẩn JSON Web Token (JWT) kết hợp cơ chế cấp phát lại phiên làm việc (Refresh Token) an toàn.
- **Mức độ ưu tiên**: **Cao (High)** — Là tính năng nền tảng bảo mật cho toàn bộ các giao dịch mua sắm và quản trị.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 9/9 (Bảo vệ dữ liệu người dùng, quản lý giỏ hàng, lịch sử mua sắm và phân quyền quản trị).
  - *Chi phí hiện thực*: 3/9 (Sử dụng Spring Security, JJWT và chuẩn Rest Controller).
  - *Rủi ro*: 7/9 (Nguy cơ rò rỉ token hoặc lộ thông tin nếu không lưu trữ token đúng chuẩn bảo mật).

### 4.1.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Khách vãng lai (Guest), Khách hàng thành viên (User).
- **Chuỗi đáp ứng luồng chính (Đăng ký & Đăng nhập)**:
  1. Người dùng nhập thông tin đăng ký (Họ tên, Email, Mật khẩu, Số điện thoại, Địa chỉ) hoặc thông tin đăng nhập (Email, Mật khẩu) trên giao diện Client.
  2. Client gửi yêu cầu HTTP POST tới Backend (`/api/auth/register` hoặc `/api/auth/login`).
  3. Backend xác thực thông tin: Kiểm tra tính hợp lệ dữ liệu, kiểm tra email trùng lặp, so khớp mật khẩu đã mã hóa (BCrypt).
  4. Nếu hợp lệ, Backend sinh cặp mã: `accessToken` (thời hạn 15–60 phút) trả về trong phản hồi JSON, và `refreshToken` (thời hạn 7–30 ngày) được đính kèm vào HttpOnly Cookie.
  5. Client lưu trữ `accessToken` trong bộ nhớ ứng dụng và điều hướng người dùng tới trang tương ứng.
- **Chuỗi đáp ứng làm mới token (Refresh Token)**:
  1. Khi `accessToken` hết hạn, Client tự động gửi yêu cầu HTTP POST tới `/api/auth/refresh` kèm HttpOnly Cookie chứa `refreshToken`.
  2. Backend kiểm tra tính hợp lệ của Refresh Token trong cơ sở dữ liệu/chữ ký JWT. Nếu hợp lệ, cấp phát `accessToken` mới.
- **Chuỗi đáp ứng luồng ngoại lệ**:
  - Nếu email đăng ký đã tồn tại: Hệ thống trả về lỗi 409 (Conflict) kèm thông báo "Email đã được sử dụng".
  - Nếu thông tin đăng nhập sai: Hệ thống trả về lỗi 401 (Unauthorized) kèm thông báo "Email hoặc mật khẩu không chính xác".

### 4.1.3 Các yêu cầu chức năng
- **REQ-AUTH-1 (Đăng ký tài khoản)**: Hệ thống cho phép người dùng đăng ký tài khoản mới bằng Email, Mật khẩu, Họ tên, Số điện thoại và Địa chỉ. Mật khẩu phải có độ dài tối thiểu 6 ký tự và được băm bằng thuật toán BCrypt trước khi lưu trữ vào cơ sở dữ liệu.
- **REQ-AUTH-2 (Đăng nhập hệ thống)**: Hệ thống phải xác thực danh tính người dùng bằng Email và Mật khẩu. Khi đăng nhập thành công, hệ thống cấp phát Access Token (JWT) trong phần thân phản hồi và Refresh Token trong `HttpOnly`, `Secure` Cookie.
- **REQ-AUTH-3 (Làm mới Access Token)**: Hệ thống phải cung cấp API `/api/auth/refresh` nhận Refresh Token từ Cookie để cấp phát Access Token mới khi token cũ hết hạn mà không yêu cầu người dùng đăng nhập lại.
- **REQ-AUTH-4 (Đăng xuất)**: Hệ thống phải cung cấp API `/api/auth/logout` để thu hồi phiên làm việc, xóa bỏ Refresh Token khỏi Cookie và vô hiệu hóa phiên của người dùng.
- **REQ-AUTH-5 (Phân quyền truy cập RBAC)**: Hệ thống phải phân định rõ ràng 3 vai trò người dùng (`GUEST`, `USER`, `ADMIN`) và kiểm soát quyền truy cập tài nguyên API tại tầng Spring Security Filter Chain.

---

## 4.2 Duyệt, tìm kiếm và xem chi tiết sản phẩm (Product Catalog, Search & Details)

### 4.2.1 Mô tả và mức ưu tiên
Tính năng cho phép người dùng dễ dàng tra cứu, duyệt danh mục linh kiện máy tính, tìm kiếm theo tên và lọc linh kiện theo các tiêu chí kỹ thuật chuyên sâu, đồng thời xem chi tiết thông số kỹ thuật được cấu trúc hóa theo từng category.
- **Mức độ ưu tiên**: **Cao (High)** — Tính năng cốt lõi của website thương mại điện tử.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 9/9 (Giúp khách hàng nhanh chóng tìm kiếm và lựa chọn sản phẩm phù hợp).
  - *Chi phí hiện thực*: 3/9 (Truy vấn Spring Data JPA, JPA Specifications/QueryDSL).
  - *Rủi ro*: 3/9 (Hiệu năng truy vấn khi số lượng linh kiện lớn hoặc lọc đa điều kiện).

### 4.2.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Khách vãng lai (Guest), Khách hàng thành viên (User), Quản trị viên (Admin).
- **Chuỗi đáp ứng luồng chính**:
  1. Người dùng chọn danh mục linh kiện (CPU, GPU, RAM, v.v.), nhập từ khóa tìm kiếm hoặc điều chỉnh khoảng giá trên giao diện.
  2. Client gửi yêu cầu HTTP GET tới `/api/products` kèm các tham số truy vấn (`category`, `keyword`, `minPrice`, `maxPrice`, `page`, `size`, `sort`).
  3. Backend truy vấn cơ sở dữ liệu với các điều kiện lọc và chỉ lấy các sản phẩm có `is_active = true`.
  4. Backend trả về danh sách sản phẩm phân trang kèm tổng số trang và tổng số sản phẩm.
  5. Người dùng nhấn chọn một sản phẩm cụ thể: Client gửi HTTP GET tới `/api/products/{id}`.
  6. Backend truy vấn và trả về toàn bộ thông tin chi tiết của sản phẩm, bao gồm dữ liệu thuộc tính kỹ thuật dạng JSONB `detail` và danh sách đánh giá.
- **Chuỗi đáp ứng luồng ngoại lệ**:
  - Nếu mã sản phẩm không tồn tại hoặc đã bị xóa mềm (`is_active = false`): Hệ thống trả về mã lỗi 404 (Not Found).

### 4.2.3 Các yêu cầu chức năng
- **REQ-PROD-1 (Duyệt danh sách sản phẩm)**: Hệ thống phải hiển thị danh sách sản phẩm phân trang (mặc định 12 sản phẩm/trang) và hỗ trợ sắp xếp theo giá (tăng dần/giảm dần) hoặc ngày tạo mới nhất.
- **REQ-PROD-2 (Tìm kiếm sản phẩm)**: Hệ thống phải cho phép tìm kiếm sản phẩm theo tên linh kiện theo cơ chế so khớp gần đúng không phân biệt chữ hoa, chữ thường (case-insensitive).
- **REQ-PROD-3 (Lọc sản phẩm nâng cao)**: Hệ thống phải hỗ trợ kết hợp đồng thời nhiều bộ lọc: theo danh mục (`category`), theo khoảng giá (`minPrice` đến `maxPrice`), và theo thương hiệu/nhà sản xuất.
- **REQ-PROD-4 (Xem chi tiết thông số kỹ thuật)**: Hệ thống phải hiển thị đầy đủ thông tin chi tiết của sản phẩm bao gồm tên, giá, số lượng tồn kho (`stock_quantity`), mô tả, hình ảnh chất lượng cao và bảng thông số kỹ thuật riêng biệt tương ứng với từng category trích xuất từ trường `detail` (JSONB).
- **REQ-PROD-5 (Hiển thị tình trạng kho hàng)**: Hệ thống phải hiển thị rõ ràng trạng thái còn hàng hoặc hết hàng dựa trên thuộc tính `stock_quantity` của sản phẩm.

---

## 4.3 Quản lý giỏ hàng và đặt hàng COD (Shopping Cart & Order Processing)

### 4.3.1 Mô tả và mức ưu tiên
Cung cấp toàn bộ chu trình mua hàng trực tuyến cho khách hàng thành viên: quản lý giỏ hàng cá nhân, tiến hành đặt hàng với phương thức thanh toán khi nhận hàng (COD), xem lịch sử đơn hàng và hủy đơn hàng khi chưa được xác nhận.
- **Mức độ ưu tiên**: **Cao (High)** — Quy trình kinh doanh trực tiếp tạo doanh thu cho hệ thống.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 9/9 (Hoàn tất giao dịch thương mại, ghi nhận doanh thu).
  - *Chi phí hiện thực*: 5/9 (Xử lý giao dịch cơ sở dữ liệu transactional, kiểm tra tồn kho).
  - *Rủi ro*: 6/9 (Đồng thời đặt hàng làm âm kho nếu không xử lý khóa lạc quan/bi quan).

### 4.3.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Khách hàng thành viên (User).
- **Chuỗi đáp ứng luồng giỏ hàng**:
  1. User bấm "Thêm vào giỏ hàng" tại trang sản phẩm kèm số lượng mong muốn.
  2. Client gửi HTTP POST tới `/api/cart/items` kèm `productId` và `quantity`.
  3. Backend kiểm tra tồn kho (`stock_quantity >= quantity`). Nếu hợp lệ, thêm mới hoặc cộng dồn số lượng trong bảng `cart_items` của User.
  4. User có thể cập nhật số lượng (`PUT /api/cart/items/{id}`) hoặc xóa sản phẩm khỏi giỏ (`DELETE /api/cart/items/{id}`).
- **Chuỗi đáp ứng luồng đặt hàng (Checkout COD)**:
  1. User truy cập trang Checkout, kiểm tra giỏ hàng, nhập địa chỉ nhận hàng, số điện thoại người nhận và ghi chú đơn hàng.
  2. User nhấn "Xác nhận đặt hàng": Client gửi HTTP POST tới `/api/orders`.
  3. Backend mở giao dịch (`@Transactional`):
     - Kiểm tra lại tồn kho của tất cả sản phẩm trong giỏ.
     - Tạo bản ghi mới trong bảng `orders` với trạng thái `PENDING`, phương thức thanh toán `COD`.
     - Sao chép các mặt hàng từ giỏ hàng sang bảng `order_items`, lưu lại giá bán thực tế tại thời điểm mua (`unit_price`).
     - Trừ số lượng tồn kho tương ứng trong bảng `products`.
     - Xóa các mặt hàng đã đặt khỏi giỏ hàng của User.
  4. Backend trả về thông tin đơn hàng đã tạo thành công (201 Created).
- **Chuỗi đáp ứng luồng hủy đơn hàng**:
  1. User xem lịch sử đơn hàng, chọn một đơn hàng ở trạng thái `PENDING` và nhấn "Hủy đơn hàng".
  2. Client gửi HTTP PUT tới `/api/orders/{id}/cancel`.
  3. Backend chuyển trạng thái đơn hàng sang `CANCELLED` và hoàn trả số lượng linh kiện tương ứng vào lại kho `stock_quantity`.

### 4.3.3 Các yêu cầu chức năng
- **REQ-ORD-1 (Quản lý giỏ hàng)**: Hệ thống cho phép người dùng đã đăng nhập thêm sản phẩm vào giỏ, cập nhật số lượng, xóa sản phẩm khỏi giỏ và xem toàn bộ danh sách sản phẩm trong giỏ hàng kèm tổng tiền tạm tính.
- **REQ-ORD-2 (Kiểm tra tồn kho khi chọn mua)**: Hệ thống phải từ chối thêm vào giỏ hoặc đặt hàng nếu số lượng yêu cầu vượt quá số lượng tồn kho khả dụng (`stock_quantity`) của sản phẩm.
- **REQ-ORD-3 (Tạo đơn hàng thanh toán COD)**: Hệ thống phải cho phép tạo đơn hàng mới với phương thức thanh toán khi nhận hàng (COD), lưu trữ thông tin địa chỉ giao nhận, số điện thoại, tính toán tổng tiền thanh toán và đóng băng đơn giá của từng sản phẩm tại thời điểm mua (`unit_price`).
- **REQ-ORD-4 (Tra cứu lịch sử đơn hàng)**: Hệ thống cho phép người dùng xem danh sách các đơn hàng đã đặt của tài khoản kèm theo mã đơn hàng, ngày đặt, trạng thái hiện tại (`PENDING`, `CONFIRMED`, `SHIPPING`, `DELIVERED`, `CANCELLED`) và chi tiết danh sách linh kiện trong đơn hàng.
- **REQ-ORD-5 (Hủy đơn hàng)**: Người dùng có quyền hủy đơn hàng của chính mình khi đơn hàng đang ở trạng thái chờ xác nhận (`PENDING`). Khi hủy thành công, hệ thống phải tự động hoàn lại số lượng tồn kho cho các sản phẩm trong đơn.

---

## 4.4 Đánh giá và nhận xét sản phẩm (Product Reviews & Ratings)

### 4.4.1 Mô tả và mức ưu tiên
Tính năng cho phép khách hàng đã mua và nhận hàng thành công viết đánh giá (chấm điểm sao và viết nhận xét) cho sản phẩm, giúp xây dựng cộng đồng người dùng tin cậy và hỗ trợ những khách hàng khác trong quyết định mua sắm.
- **Mức độ ưu tiên**: **Trung bình (Medium)** — Nâng cao trải nghiệm người dùng và tính minh bạch của cửa hàng.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 7/9 (Tăng độ tin cậy của sản phẩm, thu thập phản hồi của khách hàng).
  - *Chi phí hiện thực*: 3/9 (Bảng `product_reviews`, tính toán điểm trung bình).
  - *Rủi ro*: 3/9 (Kiểm soát đánh giá rác hoặc đánh giá khi chưa mua hàng).

### 4.4.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Khách hàng thành viên (User), Khách vãng lai (Guest).
- **Chuỗi đáp ứng luồng đánh giá**:
  1. User truy cập trang chi tiết của sản phẩm đã mua thành công, chọn mức điểm sao (1–5 sao) và nhập nhận xét.
  2. Client gửi HTTP POST tới `/api/products/{id}/reviews`.
  3. Backend kiểm tra điều kiện nghiệp vụ: User đã có ít nhất một đơn hàng ở trạng thái `DELIVERED` chứa sản phẩm này và chưa từng đánh giá sản phẩm trước đó (ràng buộc `UNIQUE(user_id, product_id)`).
  4. Nếu hợp lệ, lưu bản ghi đánh giá vào bảng `product_reviews`.
  5. Backend trả về bản ghi đánh giá vừa tạo kèm điểm sao trung bình mới của sản phẩm.
- **Chuỗi đáp ứng luồng xem và chỉnh sửa**:
  - Mọi người dùng (kể cả Guest) đều có thể xem danh sách đánh giá của sản phẩm qua `GET /api/products/{id}/reviews`.
  - User có thể chỉnh sửa nhận xét của mình (`PUT /api/products/{id}/reviews/{reviewId}`) hoặc xóa đánh giá (`DELETE /api/products/{id}/reviews/{reviewId}`).

### 4.4.3 Các yêu cầu chức năng
- **REQ-REV-1 (Kiểm soát điều kiện đánh giá)**: Hệ thống chỉ cho phép người dùng viết đánh giá sản phẩm nếu người dùng đó đã mua sản phẩm và đơn hàng tương ứng đã hoàn tất giao hàng thành công (trạng thái `DELIVERED`). Mỗi người dùng chỉ được đánh giá tối đa một lần cho mỗi sản phẩm.
- **REQ-REV-2 (Nội dung đánh giá)**: Một đánh giá bắt buộc phải có điểm số từ 1 đến 5 sao và phần bình luận nhận xét bằng văn bản (tối đa 1000 ký tự).
- **REQ-REV-3 (Hiển thị đánh giá và điểm sao trung bình)**: Hệ thống phải hiển thị công khai danh sách tất cả các đánh giá của sản phẩm kèm họ tên người đánh giá, số sao, nhận xét, thời gian đánh giá và tự động tính toán điểm đánh giá sao trung bình.
- **REQ-REV-4 (Chỉnh sửa và xóa đánh giá)**: Người dùng có quyền cập nhật lại số sao, nội dung nhận xét hoặc xóa đánh giá của chính mình.

---

## 4.5 Trợ lý ảo Chatbot AI — RAG và Gợi ý cấu hình PC (AI Chatbot Assistant)

### 4.5.1 Mô tả và mức ưu tiên
Đây là tính năng thông minh cốt lõi của đề tài niên luận. Chatbot tích hợp trực tiếp trên website, hoạt động 24/7 và phục vụ mọi đối tượng người dùng (không bắt buộc đăng nhập). Chatbot giải quyết hai bài toán nghiệp vụ trọng tâm:
1. **Hệ thống RAG**: Giải đáp chính xác các thắc mắc về chính sách của cửa hàng (bảo hành, đổi trả, giao hàng, thanh toán) dựa trên cơ sở tri thức tài liệu do Admin nạp vào, hạn chế tối đa hiện tượng ảo giác thông tin.
2. **Gợi ý cấu hình PC**: Lắng nghe nhu cầu sử dụng và mức ngân sách của người dùng bằng ngôn ngữ tự nhiên, sau đó truy vấn và lựa chọn từ các bộ PC Case đã được Admin tạo và kiểm tra tương thích từ trước, đảm bảo 100% linh kiện thành phần còn hàng trong kho.
- **Mức độ ưu tiên**: **Cao (High)** — Tính năng điểm nhấn kỹ thuật và đề tài chính của đồ án.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 9/9 (Tự động hóa tư vấn 24/7, xóa bỏ rào cản kỹ thuật cho khách hàng, tăng tỷ lệ chốt đơn).
  - *Chi phí hiện thực*: 7/9 (Tích hợp pgvector, Gemini Embedding API, Gemini Chat API, xây dựng prompt engineering).
  - *Rủi ro*: 8/9 (Ảo giác thông tin của LLM, phụ thuộc vào quota và độ trễ của Gemini API bên thứ ba).

### 4.5.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Khách vãng lai (Guest), Khách hàng thành viên (User), Dịch vụ Google Gemini API.
- **Chuỗi đáp ứng phân loại ý định (Intent Classification)**:
  1. Người dùng nhập câu hỏi vào cửa sổ chat (ví dụ: "Chính sách đổi trả hàng như thế nào?" hoặc "Tư vấn cho mình bộ PC tầm 15 triệu để chơi game LOL và dựng video").
  2. Client gửi HTTP POST tới `/api/chat` kèm nội dung tin nhắn (`message`).
  3. `ChatService` phân tích và phân loại ý định của tin nhắn thành một trong hai nhánh: `RAG` hoặc `PC_CONFIG`.
- **Nhánh A — RAG (Hỏi đáp chính sách cửa hàng)**:
  1. `ChatService` chuyển tiếp câu hỏi sang `RagService`.
  2. `RagService` gọi Gemini Embedding API để tạo vector ngữ nghĩa 768 chiều từ câu hỏi của người dùng.
  3. `RagService` thực thi truy vấn cosine distance trên cơ sở dữ liệu `pgvector`:
     ```sql
     SELECT content FROM rag_chunks ORDER BY embedding <=> ? LIMIT 5;
     ```
  4. Lấy top-5 đoạn văn bản liên quan nhất làm ngữ cảnh (Context), nhồi vào Prompt kèm System Instruction quy định: "Chỉ trả lời dựa trên ngữ cảnh được cung cấp, nếu không có thông tin thì thông báo lịch sự từ chối trả lời".
  5. Gửi Prompt tới Gemini Generative Chat API để tổng hợp câu trả lời ngôn ngữ tự nhiên.
  6. Trả về phản hồi cho Client hiển thị.
- **Nhánh B — Gợi ý cấu hình PC (PC Configuration Suggestion)**:
  1. `ChatService` chuyển tiếp yêu cầu sang `PcConfigSuggestionService`.
  2. `PcConfigSuggestionService` truy vấn từ bảng `pc_cases` danh sách tất cả các bộ PC Case đang khả dụng (`is_active = true`), đồng thời kiểm tra điều kiện **toàn bộ linh kiện thành phần phải có số lượng tồn kho `stock_quantity > 0`**.
  3. Hệ thống cấu trúc hóa danh sách các bộ PC Case hợp lệ (tên, mục đích sử dụng, tổng giá, thông số linh kiện thành phần) thành chuỗi dữ liệu ngữ cảnh.
  4. Đưa ngữ cảnh vào Prompt kèm quy tắc nghiêm ngặt: "Bạn là chuyên gia tư vấn máy tính. Hãy phân tích nhu cầu và ngân sách của người dùng, sau đó chọn ra từ 1 đến 3 bộ cấu hình phù hợp nhất từ danh sách có sẵn. Tuyệt đối KHÔNG tự ý sáng tạo hay thay đổi linh kiện ngoài danh sách được cung cấp".
  5. Gửi Prompt tới Gemini Generative Chat API để tạo phản hồi tư vấn chi tiết kèm mã định danh của các bộ PC Case được chọn.
  6. Backend đóng gói câu trả lời và dữ liệu các bộ PC Case gợi ý gửi về Client để kết xuất thành các thẻ cấu hình trực quan.

### 4.5.3 Các yêu cầu chức năng
- **REQ-AI-1 (Tiếp nhận tin nhắn và Phân loại ý định)**: Hệ thống phải cung cấp API công khai `/api/chat` tiếp nhận tin nhắn văn bản của người dùng (không bắt buộc xác thực) và tự động nhận diện ý định hội thoại (hỏi chính sách cửa hàng hoặc xin gợi ý cấu hình PC).
- **REQ-AI-2 (Truy vấn ngữ nghĩa vector RAG)**: Phân hệ RAG phải sử dụng Gemini Embedding API để tạo vector biểu diễn câu hỏi, sau đó truy vấn top-K (mặc định K = 5) đoạn tài liệu có độ tương đồng ngữ nghĩa cao nhất bằng toán tử khoảng cách cosine (`<=>`) trên bảng `rag_chunks` trong PostgreSQL.
- **REQ-AI-3 (Tổng hợp câu trả lời chính sách)**: Hệ thống phải nhồi các đoạn tài liệu tìm được vào ngữ cảnh của prompt và gọi Gemini Chat API để sinh câu trả lời chính xác, mạch lạc và tuân thủ đúng nội dung tài liệu chính sách của cửa hàng.
- **REQ-AI-4 (Lọc cấu hình PC khả dụng và còn hàng)**: Khi nhận yêu cầu tư vấn cấu hình, hệ thống chỉ được phép lấy các bộ PC Case đang được kích hoạt (`is_active = true`) và có tất cả linh kiện thành phần đều còn tồn kho (`stock_quantity > 0`).
- **REQ-AI-5 (Gợi ý cấu hình PC tối ưu)**: Chatbot phải lựa chọn từ 1 đến 3 bộ PC Case phù hợp nhất với tầm giá và mục đích sử dụng của khách hàng, kèm theo giải thích ưu điểm và cấu hình chi tiết của từng bộ máy.
- **REQ-AI-6 (Nguyên tắc chống ảo giác của AI)**: Mô hình AI tuyệt đối không được tự ý sáng tạo ra các linh kiện phần cứng mới hoặc tự lắp ráp tùy tiện các linh kiện ngoài danh mục PC Case có sẵn trong hệ thống.

---

## 4.6 Quản lý cấu hình PC Case và Thuật toán kiểm tra tương thích (PC Case Management & Compatibility Engine)

### 4.6.1 Mô tả và mức ưu tiên
Tính năng cho phép Quản trị viên khởi tạo, biên tập và quản lý các bộ máy tính hoàn chỉnh (PC Case). Trước khi lưu bất kỳ cấu hình nào, hệ thống bắt buộc phải tự động kiểm định 8 ràng buộc tương thích phần cứng khắt khe nhằm đảm bảo tính khả thi tuyệt đối của bộ máy khi lắp ráp thực tế.
- **Mức độ ưu tiên**: **Cao (High)** — Tính năng nền tảng đảm bảo dữ liệu đầu vào chuẩn xác cho Chatbot AI gợi ý cấu hình.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 9/9 (Đảm bảo cấu hình đúng chuẩn kỹ thuật 100%, bảo vệ uy tín cửa hàng).
  - *Chi phí hiện thực*: 6/9 (Xây dựng thuật toán kiểm tra ràng buộc tương thích phần cứng đa thông số).
  - *Rủi ro*: 7/9 (Bỏ sót các quy chuẩn tương thích dẫn đến tư vấn cấu hình sai cho khách).

### 4.6.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Quản trị viên (Admin).
- **Chuỗi đáp ứng tạo cấu hình PC Case**:
  1. Admin truy cập giao diện Quản lý PC Case, chọn "Tạo cấu hình mới".
  2. Admin nhập Tên cấu hình, Phân khúc/Mục đích sử dụng (Gaming, Văn phòng, Đồ họa...), Mô tả, và chọn từng linh kiện cho đủ các vị trí slot bắt buộc (CPU, Mainboard, RAM, GPU, Storage, PSU, Case, CPU Cooler).
  3. Admin nhấn "Kiểm tra tương thích" hoặc "Lưu cấu hình": Client gửi HTTP POST tới `/api/admin/pc-cases/validate` hoặc `/api/admin/pc-cases`.
  4. Backend chuyển yêu cầu tới `CompatibilityCheckerService`:
     - Lấy thông số kỹ thuật chi tiết của tất cả linh kiện đã chọn từ trường `detail` trong bảng `products`.
     - Thực hiện kiểm tra tuần tự 8 ràng buộc tương thích kỹ thuật.
  5. Nếu phát hiện vi phạm:
     - Backend trả về mã lỗi 422 (Unprocessable Entity) kèm theo mảng danh sách chi tiết các lỗi vi phạm (ví dụ: "Socket CPU LGA1700 không khớp với Socket Mainboard AM5").
     - Giao diện Admin hiển thị cảnh báo đỏ tương ứng tại từng linh kiện vi phạm.
  6. Nếu tất cả ràng buộc đều thỏa mãn:
     - Hệ thống tự động tính toán tổng giá bán bằng tổng đơn giá của 8 linh kiện thành phần.
     - Lưu bản ghi vào bảng `pc_cases` và các liên kết trong `pc_case_items`.
     - Backend trả về thông tin PC Case đã lưu thành công (201 Created).
- **Chuỗi đáp ứng cập nhật và xóa PC Case**:
  - Admin cập nhật linh kiện trong PC Case (`PUT /api/admin/pc-cases/{id}`): Hệ thống bắt buộc chạy lại kiểm định 8 ràng buộc tương thích trước khi lưu thay đổi.
  - Admin xóa PC Case (`DELETE /api/admin/pc-cases/{id}`): Hệ thống thực hiện xóa mềm (chuyển `is_active = false`) để tránh ảnh hưởng đến các đơn hàng cũ.

### 4.6.3 Các yêu cầu chức năng
- **REQ-CASE-1 (Quản lý danh sách PC Case)**: Hệ thống cho phép Quản trị viên xem danh sách các bộ cấu hình PC Case đã tạo, lọc theo mục đích sử dụng (use case), tìm kiếm theo tên và xem chi tiết linh kiện cấu thành cùng tổng giá tiền.
- **REQ-CASE-2 (Cấu hình slot linh kiện)**: Khi tạo mới hoặc cập nhật một bộ PC Case, hệ thống bắt buộc Quản trị viên phải chọn đầy đủ linh kiện cho các nhóm danh mục: CPU, MAINBOARD, RAM, GPU, STORAGE, PSU, CASE, CPU_COOLER.
- **REQ-CASE-3 (Thuật toán kiểm định 8 ràng buộc tương thích phần cứng)**: Hệ thống bắt buộc phải kiểm tra thông qua thuật toán tự động và chỉ chấp nhận cấu hình nếu thỏa mãn đầy đủ cả 8 quy tắc sau:
  1. **Tương thích Socket**: Socket của CPU phải trùng khớp với Socket của Mainboard (`CPU.socket == MAINBOARD.socket`).
  2. **Tương thích Chuẩn RAM**: Loại RAM phải được hỗ trợ bởi Mainboard (`RAM.type == MAINBOARD.memory_type`).
  3. **Tương thích Form Factor Bo mạch chủ**: Chuẩn kích thước Mainboard phải nằm trong danh sách form factor được hỗ trợ của Vỏ Case (`MAINBOARD.form_factor ∈ CASE.form_factor_support`).
  4. **Giới hạn Chiều dài Card đồ họa**: Chiều dài của Card đồ họa không được vượt quá chiều dài GPU tối đa mà Vỏ Case cho phép (`GPU.length_mm <= CASE.max_gpu_length_mm`).
  5. **Giới hạn Chiều cao Tản nhiệt**: Chiều cao của Tản nhiệt CPU không được vượt quá chiều cao tản nhiệt tối đa mà Vỏ Case cho phép (`CPU_COOLER.height_mm <= CASE.max_cooler_height_mm`).
  6. **Tương thích Socket Tản nhiệt**: Danh sách socket hỗ trợ của Tản nhiệt CPU phải chứa socket của CPU đã chọn (`CPU.socket ∈ CPU_COOLER.socket_support`).
  7. **Hệ số An toàn Nguồn điện (PSU)**: Tổng công suất thiết kế nhiệt (TDP) của CPU và GPU không được vượt quá 80% công suất danh định của Nguồn máy tính (`(CPU.tdp_w + GPU.tdp_w) <= PSU.wattage_w * 0.8`).
  8. **Ràng buộc Tồn kho thực tế**: Tất cả các linh kiện được chọn cấu thành bộ máy phải có số lượng tồn kho khả dụng lớn hơn 0 (`stock_quantity > 0`).
- **REQ-CASE-4 (API kiểm tra tương thích độc lập)**: Hệ thống phải cung cấp API độc lập `POST /api/admin/pc-cases/validate` cho phép giao diện Client kiểm tra tương thích ngay lập tức và trả về danh sách vi phạm (nếu có) trước khi Admin nhấn lưu.
- **REQ-CASE-5 (Tự động tính tổng giá thành)**: Hệ thống phải tự động tính toán tổng giá của bộ PC Case dựa trên tổng đơn giá hiện hành của các linh kiện được chọn và cập nhật lại khi linh kiện thành phần có sự thay đổi giá.

---

## 4.7 Quản trị sản phẩm, kho hàng và đơn hàng (Admin Product & Order Operations)

### 4.7.1 Mô tả và mức ưu tiên
Tính năng hỗ trợ Quản trị viên vận hành các hoạt động kinh doanh hàng ngày của cửa hàng: thêm mới, cập nhật sản phẩm kèm thông số JSONB linh hoạt, tải ảnh lên Cloudinary, quản lý tồn kho và cập nhật trạng thái đơn hàng.
- **Mức độ ưu tiên**: **Cao (High)** — Chức năng quản trị thiết yếu duy trì hoạt động của cửa hàng.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 9/9 (Kiểm soát kho hàng, cập nhật thông tin sản phẩm và xử lý đơn hàng cho khách).
  - *Chi phí hiện thực*: 4/9 (Form quản trị, tích hợp Cloudinary API).
  - *Rủi ro*: 5/9 (Sai lệch dữ liệu tồn kho, xử lý nhầm trạng thái đơn hàng).

### 4.7.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Quản trị viên (Admin).
- **Chuỗi đáp ứng quản lý sản phẩm**:
  1. Admin mở form thêm/sửa sản phẩm, nhập thông tin chung (Tên, Giá, Tồn kho, Danh mục, Mô tả), tải tệp ảnh lên.
  2. Client gửi ảnh lên Cloudinary qua Backend (`POST /api/products` multipart).
  3. Backend nhận ảnh, upload lên Cloudinary lấy URL an toàn.
  4. Admin nhập các thông số kỹ thuật đặc thù tương ứng với danh mục đã chọn (ví dụ: chọn CPU thì nhập socket, cores, threads, tdp; chọn RAM thì nhập bus, capacity, sticks...).
  5. Backend lưu thông số kỹ thuật vào cột `detail` dạng JSONB trong bảng `products`.
  6. Admin có thể thực hiện xóa mềm sản phẩm (`DELETE /api/products/{id}`), Backend cập nhật cờ `is_active = false`.
- **Chuỗi đáp ứng xử lý đơn hàng**:
  1. Admin xem danh sách đơn hàng toàn hệ thống (`GET /api/admin/orders`).
  2. Admin chọn đơn hàng và cập nhật trạng thái (`PUT /api/admin/orders/{id}/status`) theo quy trình: `PENDING` -> `CONFIRMED` -> `SHIPPING` -> `DELIVERED`.
  3. Hệ thống ghi nhận trạng thái mới và cập nhật thời điểm `updated_at`.

### 4.7.3 Các yêu cầu chức năng
- **REQ-ADM-1 (Thêm sản phẩm mới kèm thông số JSONB)**: Hệ thống cho phép Quản trị viên thêm sản phẩm mới với tên, danh mục (CPU, MAINBOARD, RAM, GPU, STORAGE, PSU, CASE, CPU_COOLER), giá bán, số lượng tồn kho ban đầu, mô tả và cấu trúc dữ liệu JSONB `detail` tương ứng với danh mục.
- **REQ-ADM-2 (Tải ảnh linh kiện lên Cloudinary)**: Hệ thống phải tích hợp dịch vụ Cloudinary để nhận tệp ảnh từ Quản trị viên, lưu trữ trên đám mây và trả về đường dẫn URL CDN an toàn lưu vào trường `image_url` của sản phẩm.
- **REQ-ADM-3 (Cập nhật và Xóa mềm sản phẩm)**: Quản trị viên có quyền cập nhật thông tin, giá bán và số lượng tồn kho của bất kỳ sản phẩm nào. Khi xóa sản phẩm, hệ thống chỉ cập nhật cờ `is_active = false` (soft delete) nhằm bảo toàn tính toàn vẹn dữ liệu của các đơn hàng và PC Case trong quá khứ.
- **REQ-ADM-4 (Quản lý toàn bộ đơn hàng)**: Hệ thống phải cung cấp cho Quản trị viên giao diện xem toàn bộ đơn hàng của khách hàng trên hệ thống, hỗ trợ tìm kiếm theo mã đơn hàng, lọc theo trạng thái và xem chi tiết thông tin người nhận, địa chỉ giao hàng và danh sách linh kiện.
- **REQ-ADM-5 (Cập nhật trạng thái đơn hàng)**: Quản trị viên có quyền cập nhật trạng thái đơn hàng theo đúng chu trình nghiệp vụ tuần tự (`PENDING` -> `CONFIRMED` -> `SHIPPING` -> `DELIVERED` hoặc hủy đơn sang `CANCELLED`).

---

## 4.8 Quản lý tài liệu RAG và Thống kê số liệu (RAG Document Management & Statistics)

### 4.8.1 Mô tả và mức ưu tiên
Tính năng hỗ trợ Quản trị viên xây dựng và bảo trì cơ sở tri thức chính sách cho Chatbot AI thông qua việc upload tài liệu và tự động số hóa vector, đồng thời cung cấp bảng điều khiển thống kê tổng quan tình hình kinh doanh của cửa hàng.
- **Mức độ ưu tiên**: **Trung bình (Medium)** — Hỗ trợ vận hành AI và quản lý chiến lược kinh doanh.
- **Đánh giá tiêu chí**:
  - *Lợi ích*: 8/9 (Tự chủ cập nhật chính sách cho AI, nắm bắt doanh thu và hiệu quả bán hàng).
  - *Chi phí hiện thực*: 5/9 (Xử lý bóc tách file văn bản, nhúng vector pgvector, biểu đồ thống kê SQL).
  - *Rủi ro*: 4/9 (Tài liệu upload định dạng không tương thích hoặc dung lượng quá lớn).

### 4.8.2 Tác nhân / Chuỗi đáp ứng
- **Tác nhân kích hoạt**: Quản trị viên (Admin).
- **Chuỗi đáp ứng nạp tài liệu RAG**:
  1. Admin chọn tệp tài liệu chính sách của cửa hàng (hỗ trợ PDF, DOCX, TXT) và gửi lên qua API `POST /api/admin/rag/documents`.
  2. Backend lưu thông tin tài liệu vào bảng `rag_documents`.
  3. `RagService` bóc tách toàn bộ nội dung văn bản từ tệp, chia thành các đoạn nhỏ (chunks) theo kích thước phù hợp và có đoạn gối đầu (overlap) để giữ ngữ cảnh.
  4. Với mỗi chunk, gọi Gemini Embedding API để tạo vector 768 chiều và lưu vào bảng `rag_chunks` kèm khóa ngoại liên kết tới tài liệu.
  5. Trả về thông báo thành công cho Admin kèm tổng số chunks đã được lập chỉ mục vector.
  6. Khi chính sách hết hiệu lực, Admin có thể xóa tài liệu (`DELETE /api/admin/rag/documents/{id}`), hệ thống tự động xóa sạch tài liệu và toàn bộ chunks vector liên quan.
- **Chuỗi đáp ứng xem thống kê kinh doanh**:
  1. Admin truy cập trang Statistics Dashboard (`GET /api/admin/statistics/...`).
  2. Backend thực thi các câu lệnh truy vấn tổng hợp SQL và trả về số liệu doanh thu theo ngày/tháng/năm, số lượng đơn hàng theo trạng thái, Top sản phẩm bán chạy nhất và biểu đồ người dùng mới.

### 4.8.3 Các yêu cầu chức năng
- **REQ-RAG-1 (Upload tài liệu chính sách)**: Hệ thống cho phép Quản trị viên tải lên các tệp tài liệu chính sách cửa hàng với các định dạng văn bản được hỗ trợ bao gồm PDF, DOCX và TXT.
- **REQ-RAG-2 (Tự động chia đoạn văn bản - Chunking)**: Hệ thống phải tự động bóc tách nội dung từ tệp tài liệu được tải lên thành các đoạn văn bản nhỏ (chunks) có kích thước tối ưu kèm đoạn chồng lặp (overlap) để bảo toàn ngữ nghĩa ngữ cảnh.
- **REQ-RAG-3 (Tạo và lưu trữ Vector Embedding)**: Hệ thống phải tự động gửi từng chunk văn bản tới Gemini Embedding API để tạo vector nhúng 768 chiều và lưu trữ trực tiếp vào cột `embedding` kiểu `VECTOR(768)` trong bảng `rag_chunks`.
- **REQ-RAG-4 (Xem danh sách và Xóa tài liệu RAG)**: Quản trị viên có thể xem danh sách các tài liệu RAG đã nạp và có quyền xóa tài liệu; khi xóa tài liệu, hệ thống phải tự động xóa bỏ toàn bộ các chunk vector tương ứng khỏi cơ sở dữ liệu.
- **REQ-STAT-1 (Thống kê doanh thu)**: Hệ thống phải cung cấp báo cáo thống kê tổng doanh thu bán hàng theo các chu kỳ thời gian linh hoạt (theo ngày trong tháng, theo tháng trong năm hoặc khoảng ngày tùy chọn).
- **REQ-STAT-2 (Thống kê đơn hàng theo trạng thái)**: Hệ thống phải thống kê số lượng và tỷ lệ phần trăm đơn hàng phân bổ theo từng trạng thái xử lý (`PENDING`, `CONFIRMED`, `SHIPPING`, `DELIVERED`, `CANCELLED`).
- **REQ-STAT-3 (Thống kê Top sản phẩm bán chạy)**: Hệ thống phải thống kê danh sách các sản phẩm có số lượng bán ra nhiều nhất và mang lại doanh thu cao nhất.
- **REQ-STAT-4 (Thống kê người dùng mới)**: Hệ thống phải thống kê số lượng tài khoản người dùng đăng ký mới theo chu kỳ thời gian để theo dõi tốc độ phát triển khách hàng.

# Các yêu cầu phi chức năng

Hệ thống phải tuân thủ nghiêm ngặt các yêu cầu phi chức năng về hiệu năng, độ tin cậy, an toàn, bảo mật và chất lượng phần mềm nhằm đảm bảo tính khả dụng cao và trải nghiệm người dùng tối ưu.

---

## 5.1 Yêu cầu thực thi (Performance Requirements)

### 1. Thời gian đáp ứng của hệ thống (Response Time)
- **Truy vấn danh mục và sản phẩm**:
  - Thời gian phản hồi của các API đọc dữ liệu (`GET /api/products`, `GET /api/products/{id}`, `GET /api/cart`) không được vượt quá **500ms** đối với 95% số lượng yêu cầu (P95 Latency) trong điều kiện tải bình thường.
  - Tải trang danh mục sản phẩm phía Client (bao gồm render DOM và hiển thị ảnh thumbnail) phải hoàn tất trong vòng **1.5 giây**.
- **Thao tác ghi dữ liệu và giao dịch**:
  - Các thao tác thêm sản phẩm vào giỏ hàng, cập nhật số lượng, tạo đơn hàng COD (`POST /api/orders`) phải có thời gian xử lý phản hồi Backend dưới **1.0 giây**.
- **Thuật toán kiểm định tương thích phần cứng**:
  - Thời gian thực thi thuật toán kiểm định 8 ràng buộc kỹ thuật của `CompatibilityCheckerService` khi Quản trị viên bấm "Kiểm tra tương thích" hoặc "Lưu PC Case" phải hoàn tất dưới **200ms**.
- **Phân hệ Trợ lý ảo Chatbot AI**:
  - *Nhánh RAG (Hỏi đáp chính sách)*: Thời gian tạo vector embedding và truy vấn top-5 chunks tương đồng nhất trên cơ sở dữ liệu `pgvector` không được vượt quá **500ms**. Tổng thời gian hoàn tất sinh câu trả lời tự nhiên từ Google Gemini Generative API gửi về Client phải đạt từ **3.0 đến 5.0 giây** trong điều kiện mạng ổn định. Thời gian chờ tối đa (Read Timeout) được định cấu hình là **30 giây**.
  - *Nhánh PC Config (Gợi ý cấu hình PC)*: Thời gian truy vấn các PC Case đang hoạt động và còn hàng trong kho kết hợp sinh gợi ý từ Gemini API không vượt quá **5.0 giây**.

### 2. Thông lượng và khả năng mở rộng (Throughput & Scalability)
- **Người dùng đồng thời (Concurrent Users)**: Hệ thống phải có khả năng phục vụ ổn định tối thiểu **50 đến 100 người dùng truy cập đồng thời** (Concurrent Users) trên cấu hình máy chủ tiêu chuẩn (2 Cores CPU, 4GB RAM) mà không xảy ra hiện tượng nghẽn luồng hay sập dịch vụ.
- **Thông lượng xử lý API (Throughput)**: Máy chủ Backend Spring Boot phải có khả năng xử lý thông lượng tối thiểu **100 requests/giây (RPS)** đối với các truy vấn đọc dữ liệu thông thường.

### 3. Tối ưu hóa truy vấn và tài nguyên cơ sở dữ liệu
- **Thiết lập chỉ mục (Database Indexing)**:
  - Bảng `products`: Tạo chỉ mục B-Tree trên các cột thường xuyên tìm kiếm và lọc: `category`, `price`, `is_active`, `name`.
  - Bảng `orders`: Tạo chỉ mục B-Tree trên cột `user_id`, `status` và `created_at` để tối ưu hóa việc truy vấn lịch sử đơn hàng và thống kê doanh thu.
  - Bảng `rag_chunks`: Tạo chỉ mục không gian vector `ivfflat` (Inverted File Flat) với toán tử `vector_cosine_ops` trên cột `embedding` nhằm tăng tốc độ truy vấn độ tương đồng cosine khi tập dữ liệu tri thức mở rộng:
    ```sql
    CREATE INDEX idx_rag_chunks_embedding ON rag_chunks USING ivfflat (embedding vector_cosine_ops) WITH (lists = 100);
    ```
- **Quản lý kết nối (Connection Pooling)**: Cấu hình HikariCP tối đa 20 kết nối đồng thời (`maximum-pool-size: 20`), thời gian chờ kết nối tối đa 30 giây (`connection-timeout: 30000ms`) để tái sử dụng hiệu quả tài nguyên kết nối CSDL, tránh cạn kiệt bộ nhớ máy chủ.

---

## 5.2 Yêu cầu an toàn (Safety Requirements)

### 1. Tính toàn vẹn dữ liệu giao dịch (ACID & Concurrency Control)
- **Giao dịch nguyên tử (Atomic Transactions)**: Mọi thao tác đặt hàng, trừ tồn kho sản phẩm, hủy đơn hoàn tồn kho, hoặc cập nhật cấu hình PC Case bắt buộc phải được bọc trong ngữ cảnh giao dịch `@Transactional` của Spring. Nếu xảy ra bất kỳ ngoại lệ nào trong quá trình xử lý (ví dụ: một linh kiện hết hàng giữa chừng hoặc lỗi mạng), toàn bộ các thao tác trước đó phải được Rollback tự động 100%, bảo đảm không gây ra tình trạng mất mát dữ liệu hoặc sai lệch số liệu tồn kho.
- **Chống bán quá tồn kho (Anti-overselling)**: Áp dụng cơ chế kiểm soát đồng thời (Concurrency Control) khi nhiều khách hàng cùng đặt mua một sản phẩm tại cùng một thời điểm: hệ thống phải khóa hoặc kiểm tra số lượng tồn kho khả dụng tại thời điểm ghi đơn, đảm bảo thuộc tính `stock_quantity` không bao giờ bị âm (`stock_quantity >= 0`).

### 2. Sao lưu và phục hồi dữ liệu (Backup & Disaster Recovery)
- **Sao lưu tự động định kỳ**: Cơ sở dữ liệu PostgreSQL phải được thiết lập sao lưu tự động định kỳ hàng ngày (Daily Automated Dump) vào các khung giờ thấp điểm (02:00 AM) và lưu trữ trên vùng lưu trữ an toàn tách biệt.
- **Chỉ số phục hồi mục tiêu**:
  - *Thời gian phục hồi mục tiêu (Recovery Time Objective - RTO)*: Dưới **2 giờ** để khôi phục toàn bộ hệ thống hoạt động bình thường trong trường hợp máy chủ gặp sự cố vật lý hoặc hỏng hóc CSDL.
  - *Điểm phục hồi mục tiêu (Recovery Point Objective - RPO)*: Tối đa **24 giờ**, đảm bảo mức độ mất mát dữ liệu không vượt quá dữ liệu phát sinh trong một ngày.

### 3. Xử lý sự cố và suy giảm tính năng an toàn (Graceful Degradation)
- **Bộ xử lý lỗi tập trung**: Toàn bộ các ngoại lệ trong hệ thống phải được bắt và xử lý tập trung thông qua `GlobalExceptionHandler` (`@ControllerAdvice`), chuyển hóa thành định dạng JSON chuẩn `ApiResponse<T>` với mã lỗi và thông báo thân thiện cho người dùng, tuyệt đối không làm lộ Stack Trace kỹ thuật ra bên ngoài.
- **Khả năng chịu lỗi dịch vụ ngoại vi**: Trong tình huống dịch vụ Google Gemini API bị quá tải hoặc cạn kiệt quota, hệ thống phải trả về thông báo lỗi lịch sự ("Hệ thống trợ lý AI đang bận, vui lòng thử lại sau") mà không làm sập ứng dụng Backend; các tính năng thương mại điện tử cốt lõi (duyệt hàng, giỏ hàng, đặt hàng) vẫn phải duy trì hoạt động bình thường 100%.

---

## 5.3 Yêu cầu bảo mật (Security Requirements)

### 1. Xác thực và quản lý phiên làm việc (Authentication & Session Security)
- **Cơ chế xác thực không trạng thái (Stateless JWT)**:
  - Hệ thống sử dụng cặp mã Access Token và Refresh Token chuẩn JWT (JSON Web Token) có chữ ký số an toàn bằng thuật toán `HMAC-SHA256` (HS256).
  - Khóa bí mật (JWT Secret Key) phải có độ dài tối thiểu 256-bit, được lưu trong biến môi trường máy chủ (`JWT_SECRET`), nghiêm cấm lưu cứng (hardcode) trong mã nguồn dự án.
  - Access Token có thời gian sống ngắn (từ **15 đến 60 phút**).
  - Refresh Token có thời hạn dài hơn (từ **7 đến 30 ngày**) và bắt buộc phải được lưu trữ trong Cookie với đầy đủ các cờ bảo mật: `HttpOnly` (chống JavaScript phía client đọc token), `Secure` (chỉ truyền qua HTTPS), và `SameSite=Strict` (phòng chống tấn công CSRF).

### 2. Kiểm soát phân quyền dựa trên vai trò (Role-Based Access Control - RBAC)
- Hệ thống áp dụng ma trận phân quyền nghiêm ngặt tại tầng Spring Security Filter Chain:
  - Các endpoint công khai (`/api/auth/**`, `/api/products/**` (GET), `/api/chat`): Cho phép mọi đối tượng (Guest, User, Admin) truy cập.
  - Các endpoint khách hàng (`/api/cart/**`, `/api/orders/**`, `/api/products/{id}/reviews` (POST/PUT/DELETE)): Bắt buộc phải có Access Token hợp lệ mang vai trò `USER` hoặc `ADMIN`.
  - Các endpoint quản trị (`/api/admin/**`): Bắt buộc người dùng phải được xác thực với vai trò `ADMIN`. Mọi truy cập trái phép từ vai trò khác phải bị từ chối với mã lỗi HTTP 403 (Forbidden).
- **Phòng chống tấn công tham chiếu trực tiếp đối tượng không an toàn (Anti-IDOR)**: Khi người dùng xem chi tiết hoặc hủy đơn hàng (`/api/orders/{id}`), Backend bắt buộc phải kiểm tra quyền sở hữu: đơn hàng phải thuộc về chính `user_id` đang đăng nhập (hoặc người thực hiện phải có vai trò `ADMIN`), ngăn chặn người dùng này truy cập hoặc hủy đơn hàng của người dùng khác.

### 3. Bảo vệ dữ liệu nhạy cảm và mã hóa (Data Protection & Cryptography)
- **Mã hóa mật khẩu một chiều**: Mật khẩu của người dùng bắt buộc phải được băm bằng thuật toán an toàn **BCrypt** với độ phức tạp (Strength/Cost factor) tối thiểu là **10** kèm Salt ngẫu nhiên trước khi lưu trữ vào bảng `users`. Tuyệt đối không lưu mật khẩu dưới dạng văn bản thuần (plaintext) hay giải thuật băm lỗi thời (MD5, SHA-1).
- **Mã hóa đường truyền**: Toàn bộ dữ liệu truyền giữa Client và Backend, cũng như giữa Backend và các dịch vụ đám mây (Gemini API, Cloudinary) bắt buộc phải được mã hóa qua kênh truyền bảo mật **HTTPS / TLS 1.2+**.

### 4. Phòng chống các lỗ hổng bảo mật phổ biến (OWASP Top 10 Mitigation)
- **Phòng chống SQL Injection (SQLi)**: Sử dụng hoàn toàn Spring Data JPA, Hibernate ORM và các truy vấn tham số hóa (Parameterized Queries / PreparedStatements). Tuyệt đối không ghép chuỗi thủ công trong các câu lệnh truy vấn CSDL.
- **Phòng chống Cross-Site Scripting (XSS)**: Thư viện React tự động mã hóa đầu ra (output encoding) khi kết xuất dữ liệu trên giao diện. Các trường văn bản đầu vào từ người dùng (nhận xét đánh giá, ghi chú đơn hàng) phải được làm sạch và kiểm tra độ dài nghiêm ngặt thông qua Jakarta Validation (`@Valid`, `@NotBlank`, `@Size`).
- **Phòng chống Cross-Site Request Forgery (CSRF)**: Do ứng dụng sử dụng mô hình RESTful API stateless với JWT, đồng thời Refresh Token được bảo vệ bằng thuộc tính `SameSite=Strict` trên Cookie, hệ thống được bảo vệ an toàn trước các cuộc tấn công CSRF.
- **Cấu hình chia sẻ tài nguyên nguồn gốc chéo (CORS)**: Cấu hình Backend chỉ chấp nhận các yêu cầu có nguồn gốc (`Origin`) xuất phát từ danh sách domain được cấp phép của Frontend Client (ví dụ: `http://localhost:5173` trong môi trường phát triển và domain chính thức khi triển khai sản xuất).

---

## 5.4 Các đặc điểm chất lượng phần mềm (Software Quality Attributes)

### 1. Tính sẵn có (Availability)
- Hệ thống phải duy trì thời gian hoạt động ổn định (System Uptime) đạt mức tối thiểu **99.0%** trong thời gian vận hành chính thức, không tính các khoảng thời gian bảo trì hệ thống định kỳ đã được thông báo trước cho người dùng.
- Cơ chế giám sát sức khỏe ứng dụng thông qua Spring Boot Actuator (`/actuator/health`) cho phép quản trị viên theo dõi trạng thái hoạt động liên tục của ứng dụng, kết nối cơ sở dữ liệu và dung lượng đĩa.

### 2. Tính có thể bảo trì (Maintainability)
- **Kiến trúc phân tầng rõ ràng**: Mã nguồn Backend được cấu trúc chặt chẽ theo các tầng độc lập: `config`, `controller`, `service`, `repository`, `entity`, `dto`, `exception`, `security`. Không để business logic xuất hiện trong tầng Controller; không để tầng Controller truy xuất trực tiếp tầng Repository.
- **Tuân thủ quy ước mã nguồn**: Đặt tên lớp theo `PascalCase`, phương thức và biến theo `camelCase`, commit message bằng tiếng Anh theo quy ước Conventional Commits (`feat:`, `fix:`, `refactor:`, `docs:`, `chore:`).
- **Ghi nhật ký hệ thống (Logging)**: Tích hợp thư viện SLF4J với Logback, phân cấp độ ghi nhật ký rõ ràng (`INFO`, `WARN`, `ERROR`), ghi nhận chi tiết thời điểm, người dùng thực hiện và thông tin lỗi để phục vụ công tác giám sát và điều tra sự cố.

### 3. Tính dễ sử dụng (Usability)
- **Thiết kế giao diện hiện đại và trực quan**: Sử dụng thư viện thành phần Shadcn UI và Tailwind CSS giúp giao diện nhất quán, tinh gọn và dễ điều hướng.
- **Tối ưu hóa quy trình mua sắm**: Quy trình đặt hàng trực tuyến được thiết kế tối giản, cho phép người dùng hoàn tất đặt hàng trong tối đa **3 bước** từ giỏ hàng.
- **Tương tác ngôn ngữ tự nhiên thân thiện**: Chatbot AI phản hồi bằng tiếng Việt chuẩn mực, mạch lạc, dễ hiểu; kết xuất các thẻ cấu hình PC trực quan kèm nút bấm hành động tiện lợi.

### 4. Tính khả chuyển (Portability)
- Toàn bộ các dịch vụ Backend, Frontend và Cơ sở dữ liệu PostgreSQL (`pgvector`) đều được đóng gói thành các tệp Dockerfile và điều phối qua `docker-compose.yml`. Điều này cho phép hệ thống có thể triển khai nhanh chóng và đồng nhất trên mọi nền tảng hệ điều hành (Linux, Windows, macOS) hoặc các nhà cung cấp đám mây (AWS, Google Cloud, DigitalOcean) mà không đòi hỏi cài đặt môi trường cục bộ phức tạp.

### 5. Tính tin cậy và độ chính xác (Reliability & Accuracy)
- **Độ chính xác thuật toán kiểm định**: Thuật toán kiểm tra 8 ràng buộc tương thích phần cứng của `CompatibilityCheckerService` phải đạt độ chính xác kỹ thuật **100%** dựa trên dữ liệu thông số linh kiện được nạp vào, không để lọt bất kỳ cấu hình xung đột phần cứng nào vào hệ thống.
- **Độ tin cậy của Chatbot AI**: Chatbot tuân thủ nghiêm ngặt nguyên tắc **chống ảo giác (Anti-hallucination)**: 100% các cấu hình PC được gợi ý phải là các cấu hình có thật đã được Quản trị viên tạo sẵn và toàn bộ linh kiện thành phần còn hàng trong kho (`stock_quantity > 0`).

---

## 5.5 Các quy tắc nghiệp vụ (Business Rules)

Hệ thống vận hành dựa trên tập hợp 8 quy tắc nghiệp vụ cốt lõi sau:

| Mã quy tắc | Tên quy tắc nghiệp vụ | Mô tả chi tiết và Phạm vi áp dụng |
| :--- | :--- | :--- |
| **BR-01** | **Quy tắc Hủy đơn hàng** | Khách hàng chỉ có quyền tự hủy đơn hàng trực tuyến khi đơn hàng đang ở trạng thái chờ xác nhận (`PENDING`). Khi đơn hàng đã được Quản trị viên duyệt sang trạng thái `CONFIRMED`, `SHIPPING` hoặc `DELIVERED`, khách hàng không thể tự hủy trên website mà phải liên hệ trực tiếp bộ phận hỗ trợ của cửa hàng. |
| **BR-02** | **Quy tắc Đánh giá sản phẩm** | Một người dùng chỉ được phép viết đánh giá và chấm điểm sao cho một sản phẩm nếu người dùng đó đã từng mua sản phẩm trong một đơn hàng đã giao thành công (trạng thái `DELIVERED`). Mỗi người dùng chỉ được đánh giá tối đa **1 lần duy nhất** cho mỗi sản phẩm (`UNIQUE(user_id, product_id)`). |
| **BR-03** | **Quy tắc Đóng băng đơn giá (Price Freezing)** | Tại thời điểm người dùng hoàn tất đặt hàng, đơn giá hiện hành của từng linh kiện phải được lưu cố định vào trường `unit_price` của bảng `order_items`. Mọi sự thay đổi về giá bán của sản phẩm trong tương lai đều không làm thay đổi giá trị của đơn hàng đã tạo trong quá khứ. |
| **BR-04** | **Quy tắc Kiểm định tương thích PC Case** | Một cấu hình PC Case chỉ được phép lưu vào cơ sở dữ liệu nếu vượt qua đầy đủ **100% (8/8)** các kiểm tra ràng buộc tương thích phần cứng: Socket CPU - Mainboard, Chuẩn RAM - Mainboard, Form factor Mainboard - Case, Chiều dài GPU - Case, Chiều cao Tản nhiệt - Case, Socket Tản nhiệt - CPU, Hệ số an toàn công suất Nguồn `(CPU.tdp + GPU.tdp) <= PSU.wattage * 0.8`, và Tồn kho linh kiện > 0. Nếu vi phạm bất kỳ tiêu chí nào, hệ thống từ chối lưu và trả về mã lỗi 422. |
| **BR-05** | **Quy tắc Gợi ý cấu hình PC của AI (Chống ảo giác)** | Khi nhận yêu cầu tư vấn cấu hình từ người dùng, Chatbot AI **chỉ được phép chọn lọc** từ danh sách các bộ PC Case đã được Admin tạo trước đó, đang được kích hoạt (`is_active = true`) và **toàn bộ linh kiện thành phần đều phải còn hàng trong kho** (`stock_quantity > 0`). Chatbot tuyệt đối không được tự ý sáng tạo hay lắp ghép các linh kiện rời rạc nằm ngoài danh sách có sẵn. |
| **BR-06** | **Quy tắc Xóa mềm dữ liệu (Soft Delete)** | Khi Quản trị viên thực hiện xóa một sản phẩm linh kiện hoặc một bộ PC Case, hệ thống không được xóa vật lý bản ghi khỏi cơ sở dữ liệu mà chỉ cập nhật cờ trạng thái `is_active = false`. Điều này nhằm bảo toàn tính toàn vẹn dữ liệu lịch sử của các đơn hàng và đánh giá đã phát sinh trước đó. |
| **BR-07** | **Quy tắc Phương thức thanh toán và Tiền tệ** | Phương thức thanh toán duy nhất được áp dụng trong phạm vi đề tài niên luận là Thanh toán khi nhận hàng (**COD** - Cash On Delivery). Đơn vị tiền tệ áp dụng thống nhất trong toàn bộ hệ thống là Việt Nam Đồng (**VND**), không hỗ trợ quy đổi đa tiền tệ. |
| **BR-08** | **Quy tắc Định danh tài khoản duy nhất** | Mỗi tài khoản người dùng gắn liền với một địa chỉ Email duy nhất (`UNIQUE`) trong toàn bộ hệ thống. Hệ thống không cho phép đăng ký hai tài khoản khác nhau có cùng địa chỉ email. |

# Các yêu cầu khác

&lt;Định nghĩa các yêu cầu khác mà chúng chưa được trình bày. Có thể bao gồm các yêu cầu về cơ sở dữ liệu, các yêu cầu về phong tục – văn hóa, các yêu cầu luật pháp, các mục tiêu tái sử dụng của dự án, v.v. &gt;

Phụ lục A: Các mô hình phân tích

&lt;Tùy chọn, bao gồm các mô hình phân tích như các lưu đồ dòng dữ liệu, lưu đồ lớp, lưu đồ chuyển dịch trạng thái, hay lưu đồ thực thể - quan hệ.&gt;

Phụ lục B: TBD – Danh sách sẽ được xác định

&lt;Thu thập một danh sách được đánh số của các tham khảo TBD (To Be Determine) mà chúng vẫn còn trong tài liệu đặc tả.&gt;