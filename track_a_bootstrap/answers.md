# PHẦN A - ĐỌC HIỂU BOOTSTRAP (20 điểm)

## Câu A1 - Grid System (10đ)

### Vẽ layout 3 kích thước:

| Kích thước | < 768px                              | 768px - 991px | ≥ 992px       |
| ---------- | ------------------------------------ | ------------- | ------------- |
| Số cột     | 1                                    | 2             | 4             |
| Box layout | 4 hàng, 1 cột (4 box chồng lên nhau) | 2 hàng, 2 cột | 1 hàng, 4 cột |

Hình vẽ:

- **< 768px**: Box1, Box2, Box3, Box4 xếp dọc
- **768px - 991px**:
  - Hàng 1: Box1, Box2
  - Hàng 2: Box3, Box4
- **≥ 992px**: Box1 | Box2 | Box3 | Box4 (ngang hết)

### Giải thích `col-md-6`:

- `col-md-6` = ở kích thước `md` (768px trở lên), element chiếm 6/12 = 50% width
- Không cần `col-sm-12` vì khi không viết, Bootstrap tự động chia full width (12 cột) ở các kích thước nhỏ hơn md

---

## Câu A2 - Utilities & Components (10đ)

### 1. Class `d-none d-md-block`:

- **`d-none`**: Ẩn element ở mọi kích thước (display: none)
- **`d-md-block`**: Từ `md` (768px) trở lên, hiển thị (display: block)
- **Kết luận**: Ẩn trên mobile (< 768px), hiện trên tablet/desktop (≥ 768px)

### 2. Năm spacing utilities:

- **`mt-3`**: margin-top = 1rem (16px) - lề trên
- **`px-4`**: padding-x = 1.5rem (24px) - lề trái phải
- **`mb-auto`**: margin-bottom = auto - đẩy element lên
- **`p-2`**: padding all = 0.5rem (8px) - lề đều
- **`ms-5`**: margin-start = 3rem (48px) - lề trái (RTL aware)

### 3. Sự khác nhau:

- **`.container`**: Max-width thay đổi theo breakpoint (sm/md/lg/xl/xxl), có margin-left/right auto
- **`.container-fluid`**: Luôn 100% width, không có max-width
- **`.container-md`**: Từ breakpoint `md` trở lên mới apply max-width, dưới đó là 100%

---

# PHẦN C - PHÂN TÍCH (20 điểm)

## Câu C1 - Tùy biến Bootstrap (10đ)

### 1. Đổi màu `$primary` sang `#E63946`:

**Quy trình:**

1. Cài Node.js + npm
2. Cài Bootstrap qua npm: `npm install bootstrap`
3. Tạo file `custom.scss`:
   ```scss
   $primary: #e63946;
   @import "../../node_modules/bootstrap/scss/bootstrap";
   ```
4. Dùng Node Sass để compile: `sass custom.scss custom.css`
5. Link file CSS mới trong HTML thay vì CDN

**Công cụ cần:** Node.js, npm, Sass compiler

### 2. Tại sao không override trực tiếp:

- Override `.btn-primary { background: red; }` chỉ thay đổi 1 element, còn các component khác vẫn dùng màu cũ
- Dùng SASS variables: thay đổi `$primary` thì tất cả components dùng biến này đều đổi (buttons, alerts, badges...)
- Dễ maintain: khi đổi lại màu, chỉ cần sửa 1 chỗ

---

## Câu C2 - So sánh CSS thuần vs Bootstrap (10đ)

### Ví dụ: Navbar responsive + Product card

**CSS thuần:**

```css
/* Navbar - khoảng 50 dòng */
.navbar { ... }
.navbar-menu { display: none; }
@media (min-width: 768px) { .navbar-menu { display: flex; } }

/* Product card - khoảng 40 dòng */
.card { ... }
.card-img { ... }
.card-title { ... }
```

**Tổng: ~90 dòng CSS**

**Bootstrap:**

```html
<nav class="navbar navbar-expand-lg">
  <div class="container">
    <a class="navbar-brand">Logo</a>
    <div class="navbar-collapse">
      <ul class="navbar-nav">
        ...
      </ul>
    </div>
  </div>
</nav>

<div class="card">
  <img class="card-img-top" ... />
  <div class="card-body">...</div>
</div>
```

**Không cần CSS, mọi thứ đã có**

### So sánh:

| Tiêu chí             | CSS thuần             | Bootstrap                  |
| -------------------- | --------------------- | -------------------------- |
| Số dòng CSS          | ~90 dòng              | 0 (hoặc rất ít)            |
| Thời gian phát triển | 2-3 giờ               | 30 phút                    |
| Số dòng HTML         | Ít                    | Nhiều classes              |
| Khả năng tùy biến    | Cao (viết lại CSS)    | Trung bình (phải override) |
| Responsive           | Phải viết media query | Tích hợp sẵn               |
| Bảo trì              | Khó (CSS phức tạp)    | Dễ (dùng lại components)   |

### Khi NÊN dùng Bootstrap:

- Dự án deadline gặt (cần nhanh)
- Team nhiều người (cần consistency)
- Dự án lớn (nhiều pages, nhiều components)
- Không cần design quá custom

### Khi KHÔNG NÊN dùng Bootstrap:

- Design quá riêng, Bootstrap không fit
- Cần file CSS rất nhẹ (Bootstrap file lớn)
- Team chỉ 1-2 người, có thể viết CSS tốt
- Dự án nhỏ (1-2 pages)
