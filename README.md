# Rider Database

Trang tra cứu các dạng biến hình Kamen Rider theo nhiều bộ.

## Cấu trúc thư mục

```
index.html
data/
  manifest.json              <- danh sách các bộ đang có
  series/
    kamen-rider-w.json       <- dữ liệu bộ W
    _template.json           <- khuôn mẫu để tạo bộ mới (không tự load)
```

## Cách thêm 1 bộ Kamen Rider mới

1. Copy file `data/series/_template.json`, đổi tên thành ví dụ `kamen-rider-kabuto.json`, để trong cùng thư mục `data/series/`.
2. Điền dữ liệu theo đúng khuôn mẫu có sẵn trong file (giữ nguyên tên các trường: `ten_form`, `gaia_memory`, `vu_khi`, `ky_nang`, `mo_ta_chung`, `image_url`, `gif_url`...).
3. Mở file `data/manifest.json`, thêm 1 dòng vào mảng `series_list`:

```json
{
  "series_list": [
    { "id": "kamen-rider-w", "file": "data/series/kamen-rider-w.json" },
    { "id": "kamen-rider-kabuto", "file": "data/series/kamen-rider-kabuto.json" }
  ]
}
```

4. Upload cả file JSON mới và file `manifest.json` đã sửa lên GitHub (Add file → Upload files → Commit).
5. Xong — không cần sửa `index.html`. Tab bộ mới sẽ tự xuất hiện trên trang.

## Lưu ý quan trọng

- Trang này dùng `fetch()` để đọc file JSON, nên **phải mở qua địa chỉ http/https** (GitHub Pages, Netlify...). Nếu bấm đúp mở file `index.html` trực tiếp từ máy (địa chỉ bắt đầu bằng `file://`), trình duyệt sẽ chặn và trang báo lỗi tải dữ liệu — đây là giới hạn bảo mật của trình duyệt, không phải lỗi code.
- Nếu muốn xem thử trên máy trước khi upload, có thể chạy lệnh sau trong thư mục này rồi mở `http://localhost:8000`:
  ```
  python3 -m http.server 8000
  ```
- Trường `image_url` / `gif_url` để trống theo mặc định. Nên dùng link nhúng từ YouTube/Giphy thay vì tự tải file gif về host, để tránh vấn đề bản quyền.
