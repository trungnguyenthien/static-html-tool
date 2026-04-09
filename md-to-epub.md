# Tóm tắt chức năng: Markdown → EPUB Converter (`md-to-epub.html`)

Đây là một ứng dụng web chạy hoàn toàn trên trình duyệt, không cần máy chủ (client-side only), giúp chuyển đổi các file định dạng Markdown (`.md`, `.txt`) thành sách điện tử định dạng EPUB. 

## Các tính năng chính

1. **Chuyển đổi hàng loạt (Batch Processing)**
   - Cho phép tải lên (kéo thả hoặc chọn file) nhiều file Markdown cùng một lúc.
   - Hiển thị danh sách các file đang chờ xử lý và trạng thái của từng file (sẵn sàng, đang xử lý, lỗi, xong).

2. **Xử lý hình ảnh từ Internet**
   - Tự động quét và nhúng ảnh được gắn dưới dạng URL (`http`/`https`) trong nội dung file Markdown.
   - Hỗ trợ vượt qua ngăn chặn CORS (nhờ sử dụng public proxy api.allorigins.win) để đảm bảo trình duyệt có thể nhúng thành công và đưa thẳng vào tệp EPUB. (Những ảnh local trỏ tới đường dẫn máy tính sẽ bị bỏ qua).

3. **Xử lý văn bản & Tạo EPUB**
   - Sử dụng thư viện `marked.js` để parse Markdown sang định dạng HTML (hỗ trợ Github Flavored Markdown).
   - Tự thay thế linh hoạt đường dẫn ảnh trong Markdown bằng đường dẫn nội bộ (internal path) của ảnh được nhúng vào EPUB.
   - Sử dụng thư viện `jszip` để nén các tệp nội dung, cấu trúc tệp bắt buộc của chuẩn EPUB (mimetype, META-INF/container.xml, nội dung xhtml, file ảnh opf & toc/nav).
   - Có sẵn bộ CSS cơ bản (typography) giúp EPUB sau khi chuyển đổi có khả năng hiển thị đẹp mắt và dễ tiếp cận người đọc.
   - Tự động tải xuống file `.epub` sau khi sinh ra hoàn tất.

4. **Giao diện & Trải nghiệm**
   - Thiết kế trực quan, dễ thao tác với tông màu tối.
   - Cung cấp log hệ thống trực tiếp (real-time log) về số lượng ảnh tải được, file nào thành công/bị lỗi chi tiết để người dùng dễ dàng theo dõi tiến độ.

## Thư viện và tài nguyên bên ngoài sử dụng
- **JSZip (v3.10.1)**: Tạo và lưu cấu trúc thư mục dạng tập tin nén `.epub` (ZIP archive).
- **Marked.js (v9.1.6)**: Parser cho Markdown hiển thị đầu ra HTML.
- **Google Fonts**: Sử dụng `Playfair Display`, `JetBrains Mono`, `Crimson Pro` cho giao diện người dùng.
