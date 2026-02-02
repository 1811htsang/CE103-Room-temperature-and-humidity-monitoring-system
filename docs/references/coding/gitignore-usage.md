# Giới thiệu
gitignore là một tệp cấu hình đặc biệt trong Git, dùng để chỉ định các tệp và thư mục mà bạn muốn Git bỏ qua, không theo dõi sự thay đổi của chúng. Điều này rất hữu ích để tránh việc commit các tệp tạm thời, tệp cấu hình cá nhân, hoặc các tệp sinh ra trong quá trình biên dịch mà không cần thiết phải đưa vào kho mã nguồn.

# Cách sử dụng .gitignore
1. **Tạo tệp .gitignore**: Tạo một tệp có tên `.gitignore` ở thư mục gốc của dự án Git của bạn.
2. **Thêm quy tắc vào .gitignore**: Mỗi dòng trong tệp `.gitignore` đại diện cho một mẫu tệp hoặc thư mục mà bạn muốn Git bỏ qua. Ví dụ:
   - `*.log` sẽ bỏ qua tất cả các tệp có phần mở rộng `.log`.
   - `temp/` sẽ bỏ qua toàn bộ thư mục `temp` và tất cả các tệp bên trong nó.
   - `config/*.json` sẽ bỏ qua tất cả các tệp `.json` trong thư mục `config`.

# Các quy tắc phổ biến
- Sử dụng `#` để thêm chú thích trong tệp `.gitignore`.
- Dùng dấu `/` để chỉ định thư mục cụ thể.
- Dùng dấu `*` làm ký tự đại diện cho bất kỳ chuỗi ký tự nào.
- Dùng dấu `!` để phủ định một quy tắc, tức là theo dõi tệp hoặc thư mục đó ngay cả khi nó bị bỏ qua bởi quy tắc trước đó.