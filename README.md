# TechZone - WEB2053 ASM FINAL (JavaScript nâng cao)

Website thương mại điện tử laptop, chạy hoàn toàn phía client (HTML/CSS/JavaScript thuần) nên có thể triển khai trực tiếp trên GitHub Pages hoặc bất kỳ hosting tĩnh nào.

## Xem website

Bản công khai: xem mục **GitHub Pages** ở phần cài đặt repository (Settings → Pages).

Chạy trên máy tính, chỉ cần một web server tĩnh bất kỳ:

```bash
# Cách 1: Python (có sẵn trên macOS/Linux, hoặc tải python.org)
python -m http.server 8080

# Cách 2: Node.js
npx serve .
```

Sau đó mở http://localhost:8080

> Không mở trực tiếp file `index.html` bằng `file://` vì trình duyệt sẽ chặn `fetch('db.json')`.

Tài khoản admin demo: `admin` / `TechZone@123`

## Cấu trúc dự án

```
TechZone_JS_ASM/
├── index.html              # Trang chính (trang chủ, sản phẩm, danh mục, blog, liên hệ)
├── db.json                 # Dữ liệu khởi tạo: 20 sản phẩm, 5 danh mục, 3 bài viết, cấu hình SEO
├── assets/
│   ├── css/style.css       # Toàn bộ giao diện, responsive desktop/mobile
│   └── js/app.js           # Toàn bộ logic ứng dụng
├── package.json            # Metadata dự án
└── .nojekyll               # Bắt buộc để GitHub Pages phục vụ thư mục assets
```

## Kiến trúc dữ liệu

Ứng dụng đọc `db.json` một lần khi tải trang, sau đó lưu bản sao vào `localStorage` (khóa `techzone-db-v1`). Nhờ vậy toàn bộ chức năng quản trị (thêm/sửa/xóa) hoạt động được trên hosting tĩnh mà không cần backend.

Trong `app.js`, hàm `api(path, options)` mô phỏng đúng hợp đồng của `json-server`:

| Thao tác | Ví dụ |
| --- | --- |
| Lấy danh sách | `api('products')` |
| Lấy một bản ghi | `api('settings/1')` |
| Lọc theo trường | `api('users?username=admin&password=...')` |
| Thêm mới | `api('products', { method: 'POST', body })` |
| Cập nhật | `api('products/5', { method: 'PATCH', body })` |
| Xóa | `api('products/5', { method: 'DELETE' })` |

Muốn khôi phục dữ liệu gốc: mở DevTools → Application → Local Storage → xóa khóa `techzone-db-v1` → tải lại trang.

## Tính năng bám đề ASM

- 5 danh mục, 20 sản phẩm laptop có ảnh minh họa.
- Trang chủ, tìm kiếm, lọc theo danh mục, sắp xếp theo giá, trang chi tiết sản phẩm, giỏ hàng, đặt hàng.
- Admin: CRUD sản phẩm / danh mục / bài viết, cấu hình SEO cho từng sản phẩm, bài viết và cho toàn hệ thống.
- Cấu hình liên kết Facebook, Facebook Pixel, GA4, Google Search Console.
- 3 bài viết blog có cấu hình SEO và backlink về website/Fanpage.
- Đơn hàng demo được lưu lại và xem được trong trang quản trị.
- Responsive cho desktop và mobile.

## Lưu ý

- Dữ liệu mẫu phục vụ bài tập/demo, không dùng làm hệ thống thương mại thật.
- Ảnh sản phẩm lấy từ Unsplash và một số CDN bên ngoài, cần có mạng khi xem.
- Mã GA4, Search Console, Pixel trong phần quản trị phải thay bằng mã thật của bạn. Website chưa tự tạo tài khoản Google/Facebook, chưa tự đăng bài Fanpage/Blogger hay gửi email thật.
- Dữ liệu quản trị lưu trong `localStorage` của từng trình duyệt, không đồng bộ giữa các máy. Đây là giới hạn của hosting tĩnh, không phải lỗi.
- Không dùng tài khoản/mật khẩu demo trên website công khai; cần bổ sung xác thực an toàn nếu triển khai thật.
