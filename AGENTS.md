# AGENTS.md — Computer Components Shop with AI Integration

> **Đề tài niên luận ngành:** Xây dựng ứng dụng web bán linh kiện máy tính tích hợp AI hỗ trợ gợi ý cấu hình

---

## 1. Tổng quan dự án

Đây là ứng dụng web thương mại điện tử chuyên bán linh kiện máy tính, tích hợp chatbot AI có hai khả năng chính:

1. **Hệ thống RAG (Retrieval-Augmented Generation):** Trả lời các câu hỏi liên quan đến chính sách của shop (bảo hành, đổi trả, vận chuyển, thanh toán, v.v.) dựa trên tài liệu do admin upload.
2. **Gợi ý cấu hình PC:** Dựa trên ngân sách và nhu cầu của người dùng (học tập, gaming, đồ họa,...), chatbot lựa chọn từ các PC Case đã được admin tạo sẵn.

---

## 2. Kiến trúc hệ thống

```
┌─────────────────────────────────────────────────────────────────┐
│                        CLIENT (Browser)                         │
│                   React + Vite (TypeScript)                     │
└───────────────────────────┬─────────────────────────────────────┘
                            │ HTTP / REST API
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
│  │ (JWT + RT)   │  │ (PC Case,    │  │  │ (query PC Cases) │  │ │
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
│  PostgreSQL    │   │   pgvector     │  │  Cloudinary / S3     │
│  (main data)   │   │  (RAG embeds)  │  │  (product images)    │
└────────────────┘   └────────────────┘  └──────────────────────┘
```

### Cấu trúc repo

Dự án được tổ chức thành **2 repo riêng biệt**:

| Repo | Mô tả |
|------|-------|
| `computer-components-shop-fe` | Frontend — React + Vite (TypeScript) |
| `computer-components-shop-be` | Backend — Java + Spring Boot |

---

## 3. Tech Stack

### Frontend

| Thành phần | Công nghệ |
|-----------|-----------|
| Framework | React (Vite + TypeScript) |
| UI Library | *(tự chọn: Ant Design / MUI / Tailwind CSS)* |
| State Management | *(tự chọn: Zustand / Redux Toolkit / Context API)* |
| HTTP Client | Axios |
| Routing | React Router v6 |

### Backend

| Thành phần | Công nghệ |
|-----------|-----------|
| Framework | Java + Spring Boot |
| ORM | Spring Data JPA + Hibernate |
| Security | Spring Security + JWT (Access Token + Refresh Token) |
| Database | PostgreSQL |
| Vector Search | pgvector extension |
| AI Provider | Google Gemini API |
| Image Storage | Cloudinary |
| Build Tool | Maven |

---

## 4. Phân quyền & Authentication

### Roles

| Role | Quyền hạn |
|------|-----------| 
| **Guest** | Xem danh sách sản phẩm, chi tiết sản phẩm, xem đánh giá sản phẩm, sử dụng chatbot AI |
| **User** | Tất cả quyền của Guest + đăng ký / đăng nhập, đặt hàng, xem lịch sử đơn hàng, quản lý giỏ hàng, đánh giá sản phẩm đã mua |
| **Admin** | Tất cả quyền của User + quản lý sản phẩm, đơn hàng, tạo PC Case, quản lý tài liệu RAG, xem thống kê số liệu |

### Cơ chế xác thực

- **JWT + Refresh Token** (stateless)
- Access Token: thời gian sống ngắn (15–60 phút)
- Refresh Token: thời gian sống dài (7–30 ngày), lưu HttpOnly cookie

---

## 5. Database Schema (dự kiến)

### 5.1 Bảng chính

```sql
-- Người dùng
users (
  id UUID PRIMARY KEY,
  email VARCHAR UNIQUE NOT NULL,
  password_hash VARCHAR NOT NULL,
  full_name VARCHAR,
  phone VARCHAR,
  address TEXT,
  role ENUM('GUEST', 'USER', 'ADMIN') DEFAULT 'USER',
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

-- Sản phẩm (dùng chung 1 bảng, phân biệt qua category)
products (
  id UUID PRIMARY KEY,
  name VARCHAR NOT NULL,
  price DECIMAL(15, 2) NOT NULL,
  stock_quantity INT NOT NULL DEFAULT 0,
  category ENUM('CPU', 'MAINBOARD', 'RAM', 'GPU', 'STORAGE', 'PSU', 'CASE', 'CPU_COOLER'),
  image_url VARCHAR,           -- URL từ Cloudinary / S3
  description TEXT,
  detail JSONB NOT NULL,       -- Đặc tính kỹ thuật theo từng category (xem mục 5.2)
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

-- Đơn hàng
orders (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  status ENUM('PENDING', 'CONFIRMED', 'SHIPPING', 'DELIVERED', 'CANCELLED'),
  payment_method ENUM('COD'),
  shipping_address TEXT NOT NULL,
  total_amount DECIMAL(15, 2) NOT NULL,
  note TEXT,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

-- Chi tiết đơn hàng
order_items (
  id UUID PRIMARY KEY,
  order_id UUID REFERENCES orders(id),
  product_id UUID REFERENCES products(id),
  quantity INT NOT NULL,
  unit_price DECIMAL(15, 2) NOT NULL  -- Giá tại thời điểm đặt hàng
)

-- Giỏ hàng
cart_items (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  product_id UUID REFERENCES products(id),
  quantity INT NOT NULL DEFAULT 1,
  UNIQUE(user_id, product_id)
)

-- Đánh giá sản phẩm
product_reviews (
  id UUID PRIMARY KEY,
  user_id UUID REFERENCES users(id),
  product_id UUID REFERENCES products(id),
  rating SMALLINT NOT NULL CHECK (rating BETWEEN 1 AND 5),
  comment TEXT,
  created_at TIMESTAMP,
  updated_at TIMESTAMP,
  UNIQUE(user_id, product_id)   -- Mỗi user chỉ đánh giá 1 lần / sản phẩm
)
```

### 5.2 Cấu trúc JSONB `detail` theo Category (dự kiến)

```jsonc
// CPU
{
  "socket": "LGA1700",        // Loại socket
  "cores": 8,                  // Số nhân
  "threads": 16,               // Số luồng
  "base_clock_ghz": 3.6,       // Xung nhịp cơ bản (GHz)
  "boost_clock_ghz": 5.2,      // Xung nhịp tối đa (GHz)
  "tdp_w": 65,                 // Công suất thiết kế nhiệt (W)
  "memory_type": "DDR4/DDR5",  // Loại RAM hỗ trợ
  "integrated_gpu": true        // Có GPU tích hợp không
}

// MAINBOARD
{
  "socket": "LGA1700",         // Socket CPU tương thích
  "form_factor": "ATX",        // Form factor (ATX / mATX / ITX)
  "chipset": "Z790",           // Chipset
  "memory_type": "DDR5",       // Loại RAM hỗ trợ
  "memory_slots": 4,           // Số khe RAM
  "max_memory_gb": 128,        // Dung lượng RAM tối đa
  "m2_slots": 3,               // Số khe M.2
  "pcie_version": 5.0          // Phiên bản PCIe
}

// RAM
{
  "type": "DDR5",              // Loại RAM
  "speed_mhz": 6000,           // Tốc độ (MHz)
  "capacity_gb": 16,           // Dung lượng mỗi thanh (GB)
  "sticks": 2,                 // Số thanh trong kit
  "total_gb": 32               // Tổng dung lượng (GB)
}

// GPU
{
  "vram_gb": 12,               // Dung lượng VRAM (GB)
  "vram_type": "GDDR6X",       // Loại VRAM
  "tdp_w": 200,                // Công suất tiêu thụ (W)
  "pcie_slot": "x16",          // Khe cắm PCIe
  "length_mm": 320             // Chiều dài card (mm)
}

// STORAGE (SSD / HDD)
{
  "type": "NVMe SSD",          // Loại (NVMe SSD / SATA SSD / HDD)
  "capacity_gb": 1000,         // Dung lượng (GB)
  "interface": "M.2 PCIe 4.0", // Giao tiếp
  "read_mbps": 7000,           // Tốc độ đọc (MB/s)
  "write_mbps": 6500           // Tốc độ ghi (MB/s)
}

// PSU (Nguồn)
{
  "wattage_w": 750,            // Công suất (W)
  "efficiency": "80+ Gold",    // Chứng chỉ hiệu suất
  "modular": "Full",           // Full / Semi / Non-modular
  "form_factor": "ATX"         // Form factor
}

// CASE (Vỏ máy tính)
{
  "form_factor_support": ["ATX", "mATX", "ITX"], // Form factor mainboard hỗ trợ
  "max_gpu_length_mm": 380,    // Chiều dài GPU tối đa
  "max_cooler_height_mm": 160, // Chiều cao tản nhiệt CPU tối đa
  "drive_bays_35": 2,          // Số khay HDD 3.5"
  "drive_bays_25": 4           // Số khay SSD 2.5"
}

// CPU_COOLER (Tản nhiệt CPU)
{
  "type": "Air",               // Air / AIO Liquid
  "socket_support": ["LGA1700", "AM5", "AM4"], // Các socket hỗ trợ
  "height_mm": 155,            // Chiều cao (mm) — với Air cooler
  "radiator_size_mm": 240,     // Kích thước radiator (mm) — với AIO
  "tdp_support_w": 250         // TDP CPU tối đa hỗ trợ (W)
}
```

---

## 6. Tính năng AI

### 6.1 RAG — Hỗ trợ chính sách shop

**Luồng xử lý:**
1. Admin upload tài liệu (PDF, DOCX, text) qua trang quản trị.
2. Backend chia nhỏ nội dung thành chunks → tạo embedding bằng Gemini Embedding API.
3. Lưu vector embedding vào PostgreSQL (pgvector extension).

```sql
-- Bảng lưu tài liệu RAG
rag_documents (
  id UUID PRIMARY KEY,
  title VARCHAR,
  source_file VARCHAR,
  created_at TIMESTAMP
)

-- Bảng lưu chunks và vector embedding
rag_chunks (
  id UUID PRIMARY KEY,
  document_id UUID REFERENCES rag_documents(id),
  content TEXT NOT NULL,
  embedding VECTOR(768),   -- Chiều vector phụ thuộc model Gemini
  created_at TIMESTAMP
)

CREATE INDEX ON rag_chunks USING ivfflat (embedding vector_cosine_ops);
```

4. Khi user hỏi → Backend tạo embedding cho câu hỏi → Tìm top-K chunks gần nhất bằng cosine similarity.
5. Nhồi chunks vào prompt → gửi Gemini API → trả lời.

### 6.2 Gợi ý cấu hình PC

#### Quy trình Admin tạo PC Case

Admin tạo cấu hình PC (PC Case) thông qua giao diện Admin Panel bằng cách chọn linh kiện cho từng slot. Backend sẽ kiểm tra ràng buộc tương thích bằng thuật toán trước khi lưu.

**Ràng buộc tương thích cần kiểm tra:**

| STT | Ràng buộc |
|-----|-----------|
| 1 | `CPU.socket == MAINBOARD.socket` |
| 2 | `CPU.memory_type` chứa `MAINBOARD.memory_type` (hoặc ngược lại) |
| 3 | `RAM.type == MAINBOARD.memory_type` |
| 4 | `MAINBOARD.form_factor` nằm trong `CASE.form_factor_support` |
| 5 | `GPU.length_mm <= CASE.max_gpu_length_mm` |
| 6 | `CPU_COOLER.height_mm <= CASE.max_cooler_height_mm` |
| 7 | `CPU_COOLER.socket_support` chứa `CPU.socket` |
| 8 | Tổng TDP (CPU + GPU) `<= PSU.wattage_w * 0.8` (hệ số an toàn) |
| 9 | Tất cả linh kiện phải có `stock_quantity > 0` |

```java
// Ví dụ interface kiểm tra ràng buộc (Backend - Java)
public interface CompatibilityChecker {
    CompatibilityResult check(PcCaseRequest request);
}

public class CompatibilityResult {
    private boolean compatible;
    private List<String> violations; // Danh sách vi phạm nếu có
}
```

**Bảng lưu PC Case:**

```sql
-- PC Case do admin tạo
pc_cases (
  id UUID PRIMARY KEY,
  name VARCHAR NOT NULL,           -- Tên gợi ý: "Gaming Entry 2025", v.v.
  use_case VARCHAR,                -- "gaming", "study", "office", "rendering"
  total_price DECIMAL(15, 2),      -- Tổng giá (tính tự động)
  description TEXT,
  is_active BOOLEAN DEFAULT TRUE,
  created_at TIMESTAMP,
  updated_at TIMESTAMP
)

-- Liên kết PC Case với các linh kiện
pc_case_items (
  id UUID PRIMARY KEY,
  pc_case_id UUID REFERENCES pc_cases(id),
  product_id UUID REFERENCES products(id),
  category ENUM('CPU', 'MAINBOARD', 'RAM', 'GPU', 'STORAGE', 'PSU', 'CASE', 'CPU_COOLER'),
  UNIQUE(pc_case_id, category)     -- Mỗi slot chỉ có 1 linh kiện (trừ RAM, Storage nếu cần)
)
```

#### Quy trình gợi ý cho User

```
User nhập: "Mình muốn build PC chơi game với ngân sách 20 triệu"
     │
     ▼
Backend: Query pc_cases
  WHERE is_active = TRUE
    AND tất cả linh kiện có stock_quantity > 0
  JOIN pc_case_items + products (giá, tên, thông số)
     │
     ▼
Tạo Prompt gửi Gemini:
  System: "Bạn là chuyên gia tư vấn PC. Dựa vào danh sách cấu hình có sẵn sau đây,
           hãy gợi ý cho user cấu hình phù hợp nhất với nhu cầu và ngân sách.
           CHỈ được chọn từ các cấu hình trong danh sách, KHÔNG tự lắp ghép linh kiện mới."
  User: [yêu cầu của user]
  Context: [danh sách PC Cases đã query từ DB]
     │
     ▼
Gemini trả về: Giải thích + gợi ý 1–3 PC Case phù hợp nhất
```

---

## 7. API Endpoints (Tổng quan)

### Authentication
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| POST | `/api/auth/register` | Đăng ký tài khoản | Public |
| POST | `/api/auth/login` | Đăng nhập | Public |
| POST | `/api/auth/refresh` | Làm mới Access Token | Refresh Token |
| POST | `/api/auth/logout` | Đăng xuất | User |

### Products
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| GET | `/api/products` | Danh sách sản phẩm (lọc, tìm kiếm, phân trang) | Public |
| GET | `/api/products/{id}` | Chi tiết sản phẩm | Public |
| POST | `/api/products` | Tạo sản phẩm mới | Admin |
| PUT | `/api/products/{id}` | Cập nhật sản phẩm | Admin |
| DELETE | `/api/products/{id}` | Xoá sản phẩm (soft delete) | Admin |

### Orders
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| GET | `/api/orders` | Lịch sử đơn hàng của user hiện tại | User |
| GET | `/api/orders/{id}` | Chi tiết đơn hàng | User |
| POST | `/api/orders` | Tạo đơn hàng mới | User |
| PUT | `/api/orders/{id}/cancel` | Huỷ đơn hàng | User |
| GET | `/api/admin/orders` | Tất cả đơn hàng | Admin |
| PUT | `/api/admin/orders/{id}/status` | Cập nhật trạng thái đơn hàng | Admin |

### Cart
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| GET | `/api/cart` | Xem giỏ hàng | User |
| POST | `/api/cart/items` | Thêm sản phẩm vào giỏ | User |
| PUT | `/api/cart/items/{id}` | Cập nhật số lượng | User |
| DELETE | `/api/cart/items/{id}` | Xoá sản phẩm khỏi giỏ | User |

### PC Cases (Admin)
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| GET | `/api/admin/pc-cases` | Danh sách PC Case | Admin |
| POST | `/api/admin/pc-cases` | Tạo PC Case mới + kiểm tra ràng buộc | Admin |
| PUT | `/api/admin/pc-cases/{id}` | Cập nhật PC Case | Admin |
| DELETE | `/api/admin/pc-cases/{id}` | Xoá PC Case | Admin |
| POST | `/api/admin/pc-cases/validate` | Kiểm tra ràng buộc tương thích | Admin |

### AI / Chatbot
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| POST | `/api/chat` | Gửi tin nhắn chatbot (RAG + PC Config) | Public |
| POST | `/api/admin/rag/documents` | Upload tài liệu RAG | Admin |
| GET | `/api/admin/rag/documents` | Danh sách tài liệu RAG | Admin |
| DELETE | `/api/admin/rag/documents/{id}` | Xoá tài liệu RAG | Admin |

### Reviews (Đánh giá sản phẩm)
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| GET | `/api/products/{id}/reviews` | Xem tất cả đánh giá của sản phẩm | Public |
| POST | `/api/products/{id}/reviews` | Viết đánh giá cho sản phẩm (đã mua) | User |
| PUT | `/api/products/{id}/reviews/{reviewId}` | Cập nhật đánh giá của mình | User |
| DELETE | `/api/products/{id}/reviews/{reviewId}` | Xoá đánh giá của mình | User |

### Statistics (Admin)
| Method | Endpoint | Mô tả | Auth |
|--------|----------|-------|------|
| GET | `/api/admin/statistics/revenue` | Thống kê doanh thu theo ngày/tháng/năm | Admin |
| GET | `/api/admin/statistics/orders` | Thống kê số lượng đơn hàng theo trạng thái | Admin |
| GET | `/api/admin/statistics/top-products` | Top sản phẩm bán chạy nhất | Admin |
| GET | `/api/admin/statistics/users` | Thống kê người dùng mới theo thời gian | Admin |

---

## 8. Cấu trúc thư mục đề xuất

### Frontend (`computer-components-shop-fe`)

```
src/
├── api/              # Axios instances, API calls
├── assets/           # Hình ảnh, icon tĩnh
├── components/       # UI components tái sử dụng
│   ├── common/       # Button, Input, Modal, ...
│   ├── product/      # ProductCard, ProductDetail, ...
│   ├── cart/         # CartItem, CartSummary, ...
│   ├── chat/         # ChatBox, ChatMessage, ...
│   ├── review/       # ReviewForm, ReviewList, StarRating, ...
│   └── admin/        # AdminTable, PcCaseForm, StatisticsChart, ...
├── contexts/         # React Context (Auth, Cart)
├── hooks/            # Custom hooks
├── pages/            # Route-level components
│   ├── HomePage.tsx
│   ├── ProductListPage.tsx
│   ├── ProductDetailPage.tsx
│   ├── CartPage.tsx
│   ├── CheckoutPage.tsx
│   ├── OrderHistoryPage.tsx
│   ├── ChatPage.tsx
│   └── admin/
│       ├── AdminDashboard.tsx
│       ├── StatisticsDashboard.tsx
│       ├── ProductManagement.tsx
│       ├── OrderManagement.tsx
│       ├── PcCaseManagement.tsx
│       └── RagDocumentManagement.tsx
├── routes/           # React Router config, route guards
├── store/            # Global state (Zustand / Redux)
├── types/            # TypeScript interfaces & types
└── utils/            # Helper functions
```

### Backend (`computer-components-shop-be`)

```
src/main/java/com/example/pcshop/
├── config/           # Spring Security, JWT, CORS, Cloudinary config
├── controller/       # REST Controllers
│   ├── AuthController.java
│   ├── ProductController.java
│   ├── OrderController.java
│   ├── CartController.java
│   ├── ChatController.java
│   ├── ReviewController.java
│   └── admin/
│       ├── AdminProductController.java
│       ├── AdminOrderController.java
│       ├── AdminPcCaseController.java
│       ├── AdminRagController.java
│       └── AdminStatisticsController.java
├── dto/              # Request/Response DTOs
├── entity/           # JPA Entities (User, Product, Order, ProductReview, ...)
├── exception/        # Custom exceptions, GlobalExceptionHandler
├── repository/       # Spring Data JPA Repositories
├── security/         # JWT utils, UserDetailsService, filters
├── service/          # Business logic
│   ├── AuthService.java
│   ├── ProductService.java
│   ├── OrderService.java
│   ├── CartService.java
│   ├── ReviewService.java                     # Đánh giá sản phẩm
│   ├── StatisticsService.java                 # Thống kê số liệu cho Admin
│   ├── PcCaseService.java
│   ├── CompatibilityCheckerService.java       # Kiểm tra ràng buộc linh kiện
│   ├── ChatService.java                       # Điều phối RAG vs PC Config
│   ├── RagService.java                        # RAG pipeline
│   └── PcConfigSuggestionService.java         # Gợi ý cấu hình PC
└── util/             # Các tiện ích dùng chung
```

---

## 9. Các tính năng chính (Feature List)

### Người dùng (Guest / User)
- Xem danh sách sản phẩm với bộ lọc (category, giá, hãng)
- Tìm kiếm sản phẩm theo tên
- Xem chi tiết sản phẩm (thông số kỹ thuật, hình ảnh)
- Xem đánh giá và điểm sao trung bình của sản phẩm
- Thêm sản phẩm vào giỏ hàng (yêu cầu đăng nhập)
- Đặt hàng với thanh toán COD
- Xem lịch sử và trạng thái đơn hàng
- Đánh giá sản phẩm (1–5 sao + nhận xét) sau khi đã mua hàng thành công
- Sử dụng chatbot AI (không cần đăng nhập)

### Admin
- Quản lý sản phẩm (CRUD + upload ảnh lên Cloudinary/S3)
- Quản lý đơn hàng (xem, cập nhật trạng thái)
- Tạo và quản lý PC Case (chọn linh kiện + kiểm tra ràng buộc)
- Quản lý tài liệu RAG (upload, xem, xoá)
- Xem thống kê số liệu: doanh thu theo thời gian, đơn hàng theo trạng thái, sản phẩm bán chạy, người dùng mới

### Chatbot AI
- Trả lời câu hỏi về chính sách shop (RAG)
- Gợi ý cấu hình PC phù hợp với ngân sách và nhu cầu
- Chỉ gợi ý linh kiện còn hàng trong kho
- Không tự tổng hợp linh kiện mới — chỉ chọn từ PC Case có sẵn

---

## 10. Quy ước code

### General
- Ngôn ngữ commit message: **Tiếng Anh**
- Convention: `feat:`, `fix:`, `refactor:`, `docs:`, `chore:`
- Branch naming: `feature/<tên-tính-năng>`, `fix/<mô-tả-lỗi>`

### Backend (Java / Spring Boot)
- Đặt tên class: `PascalCase`
- Đặt tên method, biến: `camelCase`
- Mọi response API bọc trong wrapper `ApiResponse<T>`:
  ```json
  {
    "success": true,
    "message": "OK",
    "data": { ... }
  }
  ```
- Dùng `@Valid` + DTO validation cho tất cả request body
- Không để business logic trong Controller

### Frontend (React / TypeScript)
- Đặt tên component: `PascalCase`
- Đặt tên file component: `PascalCase.tsx`
- Đặt tên hook custom: bắt đầu bằng `use` (e.g., `useCart`, `useAuth`)
- Đặt tên biến, function: `camelCase`
- Không gọi API trực tiếp trong component — dùng custom hook hoặc service layer

---

## 11. Môi trường & Biến môi trường

### Backend (`application.yml` / `.env`)
```yaml
# Database
spring.datasource.url: jdbc:postgresql://localhost:5432/pc_shop
spring.datasource.username: postgres
spring.datasource.password: <password>

# JWT
jwt.secret: <secret-key>
jwt.access-token-expiry-ms: 900000       # 15 phút
jwt.refresh-token-expiry-days: 30

# Google Gemini
gemini.api-key: <api-key>
gemini.embedding-model: text-embedding-004
gemini.chat-model: gemini-1.5-flash

# Cloudinary (hoặc AWS S3)
cloudinary.cloud-name: <cloud-name>
cloudinary.api-key: <api-key>
cloudinary.api-secret: <api-secret>

# pgvector
pgvector.embedding-dimension: 768
pgvector.top-k: 5
```

### Frontend (`.env`)
```env
VITE_API_BASE_URL=http://localhost:8080/api
```

---

## 12. Checklist phát triển

- [ ] Khởi tạo project Spring Boot (Backend)
- [ ] Khởi tạo project React + Vite (Frontend)
- [ ] Cấu hình PostgreSQL + pgvector
- [ ] Implement Auth (JWT + Refresh Token)
- [ ] Implement CRUD Products (API + UI)
- [ ] Implement Cart & Order (API + UI)
- [ ] Implement PC Case management + Compatibility Checker
- [ ] Implement RAG pipeline (embedding + vector search)
- [ ] Implement Chatbot UI + API
- [ ] Implement PC Config Suggestion (query DB + prompt Gemini)
- [ ] Implement Image Upload (Cloudinary / S3)
- [ ] Implement Product Reviews (API + UI — đánh giá, chấm sao)
- [ ] Implement Admin Statistics Dashboard (API + UI — doanh thu, đơn hàng, top sản phẩm, người dùng mới)
- [ ] Viết tài liệu API (Swagger / OpenAPI)
- [ ] Kiểm thử & sửa lỗi

---

*Tài liệu này mô tả kiến trúc tổng thể và các quyết định thiết kế cho dự án. Chi tiết triển khai cụ thể có thể thay đổi trong quá trình phát triển.*
