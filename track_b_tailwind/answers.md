# PHẦN A - ĐỌC HIỂU TAILWINDCSS (20 điểm)

## Câu A1 - Utility Classes (10đ)

### Giải thích mỗi class:

```
- flex → display: flex
- items-center → align-items: center
- justify-between → justify-content: space-between
- p-4 → padding: 1rem (16px) (tất cả 4 cạnh)
- bg-white → background-color: white
- shadow-md → box-shadow: 0 4px 6px rgba(0,0,0,0.1)
- rounded-lg → border-radius: 0.5rem (8px)
- hover:shadow-xl → box-shadow: 0 20px 25px... (khi hover)
- transition-shadow → transition: box-shadow 150ms cubic-bezier(...)
- duration-300 → transition-duration: 300ms
- w-16 → width: 4rem (64px)
- h-16 → height: 4rem (64px)
- rounded-full → border-radius: 9999px (hình tròn)
- object-cover → object-fit: cover (cắt ảnh phù hợp)
- ml-4 → margin-left: 1rem (16px)
- flex-1 → flex: 1 1 0% (chiếm hết không gian còn lại)
- text-lg → font-size: 1.125rem (18px)
- font-semibold → font-weight: 600
- text-gray-800 → color: #1f2937
- truncate → white-space: nowrap, overflow: hidden, text-overflow: ellipsis
- text-sm → font-size: 0.875rem (14px)
- text-gray-500 → color: #6b7280
- px-4 → padding-left: 1rem, padding-right: 1rem
- py-2 → padding-top: 0.5rem, padding-bottom: 0.5rem
- bg-blue-500 → background-color: #3b82f6
- text-white → color: white
- rounded-md → border-radius: 0.375rem (6px)
- hover:bg-blue-600 → background-color: #2563eb (khi hover)
- focus:ring-2 → box-shadow: 0 0 0 2px ... (khi focus)
- focus:ring-blue-300 → box-shadow color: #93c5fd
```

---

## Câu A2 - Responsive & States (10đ)

### 1. Prefix responsive:

- **`md:`** - Từ breakpoint medium (768px) trở lên
- **`lg:`** - Từ breakpoint large (1024px) trở lên
- **`xl:`** - Từ breakpoint extra large (1280px) trở lên

**Ví dụ:** `md:grid-cols-2 lg:grid-cols-4`

- Mobile: 1 cột (mặc định)
- Tablet (768px+): 2 cột
- Desktop (1024px+): 4 cột

### 2. State modifiers:

- **`hover:`** - Khi rê chuột qua (hover)
- **`focus:`** - Khi input được focus
- **`active:`** - Khi element được nhấn
- **`group-hover:`** - Khi element cha được hover (cần class `group`)

### 3. Ẩn trên mobile, hiện flex trên tablet trở lên:

```html
<div class="hidden md:flex">...</div>
```

- `hidden` = display: none (ẩn trên mobile)
- `md:flex` = display: flex (từ tablet trở lên)
- Tương đương Bootstrap: `d-none d-md-flex`

---

# PHẦN C - PHÂN TÍCH (20 điểm)

## Câu C1 - Tailwind vs CSS thuần (10đ)

### So sánh với component viết CSS thuần:

**HTML file size:**

- CSS thuần: ~100 dòng HTML + CSS riêng → file CSS: ~3KB
- Tailwind: ~150 dòng HTML (nhiều classes) → file Tailwind CSS từ CDN: ~80KB (nhưng cached)

→ **Tổng cộng:** CSS thuần thắng về file size

**Maintainability (Dễ bảo trì):**

- CSS thuần: Phải tìm CSS, dễ gây xung đột tên class, khó theo dõi
- Tailwind: CSS nằm ngay trong HTML, dễ đọc, ít xung đột

→ **Tailwind thắng** về khả năng bảo trì

**Reusability (Tái sử dụng):**

- CSS thuần: Tạo class `.card` rồi dùng lại nhiều chỗ
- Tailwind: Dùng `@apply` để tạo component hoặc copy classes
  ```css
  @layer components {
    @apply p-4 bg-white rounded-lg shadow-md;
  }
  ```

→ **Tương đương**, nhưng Tailwind phức tạp hơn

---

## Câu C2 - Performance (10đ)

### 1. Tại sao Tailwind CSS nhỏ hơn Bootstrap?

- **Bootstrap:** File CSS chứa tất cả utility + components, dù bạn có dùng không
  - Ví dụ: Bạn chỉ dùng 10% Bootstrap → file CSS vẫn đầy đủ 100%
  - File size: ~150KB (minified)

- **Tailwind:** Chỉ tạo CSS cho classes bạn thực sự dùng
  - Ví dụ: Bạn dùng `p-4`, `bg-white`, `rounded-lg` → chỉ add những classes đó vào CSS
  - File size: ~10KB (minified, sau purge)

→ **Tailwind thắng** ở file size cuối cùng

### 2. PurgeCSS / Tailwind JIT:

**JIT (Just-In-Time):**

- Scan HTML files → tìm tất cả Tailwind classes đang dùng
- Loại bỏ các classes KHÔNG dùng
- Ví dụ: Nếu HTML không có `bg-red-500`, nó sẽ bị xóa khỏi CSS
- Giảm file size từ 80KB xuống ~10KB

**Build time:** Chỉ tạo CSS khi bạn dùng (JIT)

### 3. Khi KHÔNG NÊN dùng TailwindCSS:

**Tình huống 1:**

- Dự án nhỏ (landing page 1-2 trang)
- Không cần component tái sử dụng
- Chỉ cần CSS cơ bản
  → **Viết CSS thuần nhanh hơn**

**Tình huống 2:**

- Client không có npm/build process
- Cần một file HTML đơn thuần, không cần cài đặt gì
- Dùng CDN Tailwind thì file HTML dài lên 50%, CSS từ CDN khi offline không có
  → **Bootstrap hoặc CSS thuần tốt hơn**
