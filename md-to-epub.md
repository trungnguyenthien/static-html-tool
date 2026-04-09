# Tóm tắt chức năng: Markdown → EPUB Converter (`md-to-epub.html`)

Đây là một ứng dụng web chạy trực tiếp trên trình duyệt, không cần tải phần mềm hay máy chủ (client-side only), giúp bạn chuyển đổi các file định dạng Markdown (`.md`, `.txt`) thành sách điện tử định dạng EPUB. 

## Cấu trúc và Tính năng cốt lõi

1. **Quản lý & Chuyển đổi linh hoạt (Individual Conversion)**
   - Cho phép tải lên (kéo thả hoặc tuỳ chọn) nhiều file Markdown cùng một lúc vào "Select Markdown files".
   - Mỗi tệp có trạng thái độc lập và được xử lý riêng rẽ qua nút **"convert to EPUB"**.

2. **Cơ chế thu thập ảnh tiên tiến**
   - Tự động nhận diện và tải các đường link ảnh (`http`/`https`) trong cấu trúc Markdown để nhúng vào dạng base64 bên trong thư mục EPUB.
   - Giải quyết triệt để lỗi Network (CORS) bằng **cơ chế Fallback thông qua 3 lớp Proxy Bypass** hoạt động tuần tự thay thế (gồm ngẫu nhiên `corsproxy` và `allorigins`, `codetabs`), chống lỗi nghẽn tải.

3. **Chuẩn hoá hiển thị văn bản (NFC Normalization)**
   - Các tên file tiếng Việt có dấu khi gõ ở một số hệ điều hành (như thư mục macOS dùng chuỗi NFD bị tách rời dấu) sẽ được **tự động gộp chuẩn hoá**, tránh triệt để lỗi vỡ chữ trên giao diện hệ thống log và danh sách tệp đính kèm.

4. **Xử lý tài liệu và Đóng gói EPUB**
   - Sử dụng `marked.js` để parse Markdown sang định dạng HTML một cách chính xác nhất, có hỗ trợ cú pháp Github Flavored Markdown.
   - Sử dụng thư viện `jszip` tự động thiết lập và nén cấu trúc cây cho định dạng mở EPUB (như `META-INF`, `mimetype`, `nav/toc`,...).
   - Nhúng sẵn bộ CSS thiết kế kiểu chữ (typography) thân thiện để eBook sinh ra hiển thị đẹp và dễ tiếp cận cho mắt người đọc trên các ứng dụng sách.
   - Việc bắt đầu tải tệp về là tự động hoàn toàn khi xử lý xong tệp.

5. **Giao diện & Theo dõi (Log Tracking)**
   - UI với thiết kế Tối (Dark mode) rõ ràng, lược bỏ mọi phiền nhiễu và những cài đặt thủ công thừa thãi (Ngôn ngữ được ẩn định mặc định ở dạng `vi`).
   - Tích hợp khung lưới hệ thống Log ghi chép trực tiếp trạng thái theo thời gian thực: File nào, ảnh gì thành công/thất bại, do lỗi gì để tiện theo dõi.

## Thư viện và tài nguyên áp dụng
- **JSZip (v3.10.1)**: Core API tạo và nén cấu trúc EPUB.
- **Marked.js (v9.1.6)**: Core Parser cho Markdown -> HTML.
- **Google Fonts**: Sử dụng `Playfair Display`, `JetBrains Mono`, `Crimson Pro` để đồng bộ UI ứng dụng.
