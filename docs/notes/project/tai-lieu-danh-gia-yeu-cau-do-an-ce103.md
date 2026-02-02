# BỘ CHECKLIST ĐÁNH GIÁ YÊU CẦU ĐỒ ÁN
**(Dựa trên tiêu chuẩn BEA - 4C & System Context)**

## Phần 1: Khám phá Yêu cầu (Requirements Elicitation)
*Mục tiêu: Đảm bảo không bỏ sót mong muốn của giáo viên (Stakeholder).*

| STT | Nội dung kiểm tra                                                                                                | Trạng thái (V) |                                                       Trả lời                                                       | Ghi chú                                                    | Mức độ cần thiết | Giai đoạn đánh giá |
| :-: | :--------------------------------------------------------------------------------------------------------------- | :------------: | :-----------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------- | ---------------- | ------------------ |
|  1  | Đã xác định rõ **Mục tiêu hệ thống** (Business/Usage Level) mà giáo viên mong muốn chưa?                         |       x        |                                     - Thu thập được nhiệt độ, độ ẩm trong phòng                                     | Giải quyết bài toán gì thực tế?                            | Cao              | 1                  |
|  2  | Đã hỏi giáo viên về các **Yêu cầu ngầm định (Implicit)** chưa?                                                   |       x        |                  - Có thiết kế mạch<br>- Có khả năng chạy được<br>- Thu thập được nhiệt độ, độ ẩm                   | Các tính năng giáo viên coi là "hiển nhiên phải có".       |                  | 2                  |
|  3  | Đã xác định **Bối cảnh hệ thống (System Context)**: Hệ thống giao tiếp với những cảm biến, cơ cấu chấp hành nào? |       x        | - Mạch ESP32<br>- Cảm biến SHT30 (I2C)<br>- Màn 16x2 LCD (I2C) (**OPTIONAL**)<br>- Web (MQTT, HTTPS) (**OPTIONAL**) | Kiểm tra trong [[bea-requirement-engineering.pdf#page=20]] |                  | 2                  |
|  4  | Đã xác định rõ **Ràng buộc công nghệ**: Giáo viên yêu cầu dùng dòng vi điều khiển nào (STM32, ESP32, PIC...)?    |       x        |                                          Tự chọn tùy ý -> ESP32 (ESP-IDF)                                           | Ràng buộc (Constraints).                                   | Cao              | 1                  |

## Phần 2: Phân loại Yêu cầu (Classification)
*Mục tiêu: Tách biệt tính năng và các tiêu chuẩn kỹ thuật.*

| STT | Nội dung kiểm tra                                                                                                            | Trạng thái (V) |                                                                                                                     Trả lời                                                                                                                      | Ghi chú                                                    | Mức độ cần thiết | Giai đoạn đánh giá |
| :-: | :--------------------------------------------------------------------------------------------------------------------------- | :------------: | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :--------------------------------------------------------- | ---------------- | ------------------ |
|  5  | **Yêu cầu chức năng (Functional):** Đã liệt kê đủ các chế độ hoạt động (Auto, Manual, Error state...)?                       |       x        |                                                                                                     Tùy thuộc vào thiết kế bổ sung của nhóm                                                                                                      | Hệ thống làm được gì?                                      |                  | 2                  |
|  6  | **Yêu cầu chất lượng (Non-functional):** Đã có thông số về thời gian đáp ứng (Real-time), độ chính xác, tiêu thụ năng lượng? |       x        |                                                                                                                Không cần xét đến                                                                                                                 | Kiểm tra trong [[bea-requirement-engineering.pdf#page=17]] |                  | 2                  |
|  7  | **Giao diện (Interface):** Đã chốt cách thức giao tiếp (I2C, SPI, UART hay App/Web)?                                         |       x        |                                                                                                 I2C, WDT (Watchdog), RCC (Reset & Clock control)                                                                                                 |                                                            |                  | 2                  |
|  8  | **Độ ưu tiên:** Đã phân loại yêu cầu nào là Bắt buộc (Essential) và yêu cầu nào là Điểm cộng (Desirable)?                    |       x        | - Có thiết kế mạch (**BẮT BUỘC**)<br>- Có thu thập nhiệt độ, độ ẩm (**BẮT BUỘC**)<br>- Lịch sử dữ liệu (**TÙY CHỌN** - 2nd)<br>- Chế độ tiết kiệm pin (**TÙY CHỌN** 1st)<br>- Tính toán (**TÙY CHỌN** 2nd)<br>- Giao diện Web (**TÙY CHỌN** 3nd) | Kiểm tra trong [[bea-requirement-engineering.pdf#page=17]] | Cao              | 1                  |


<div style="page-break-after: always;"></div> 

## Phần 3: Đánh giá chất lượng 4C (Quality Criteria)
*Mục tiêu: Đảm bảo yêu cầu viết ra đủ tiêu chuẩn để thực hiện thiết kế (Design).*

| STT | Nội dung kiểm tra                                                                                                               | Trạng thái (V) |                       Trả lời                        | Ghi chú                           | Mức độ cần thiết | Giai đoạn đánh giá |
| :-: | :------------------------------------------------------------------------------------------------------------------------------ | :------------: | :--------------------------------------------------: | :-------------------------------- | ---------------- | ------------------ |
|  9  | **Clear (Rõ ràng):** Các yêu cầu có chứa từ mơ hồ không (ví dụ: "chạy nhanh", "tiết kiệm pin")?                                 |       x        |                  Không cần xét đến                   | Phải dùng con số cụ thể (ms, mA). |                  | 2                  |
| 10  | **Complete (Đầy đủ):** Đã tính đến trường hợp hệ thống gặp lỗi hoặc mất nguồn đột ngột chưa?                                    |       x        |                   Có thể cân nhắc                    | Xem xét toàn bộ vòng đời.         |                  | 2                  |
| 11  | **Consistent (Nhất quán):** Có yêu cầu nào mâu thuẫn với nhau không (ví dụ: vừa muốn màn hình sáng rõ vừa muốn pin dùng 1 năm)? |       x        | Không cần xét đến vì các yêu cầu bổ sung đã thỏa mãn | Cân bằng các thỏa hiệp.           |                  | 2                  |
| 12  | **Correct (Chính xác):** Giáo viên đã xác nhận tập yêu cầu này đúng ý thầy/cô chưa?                                             |       x        |                     Thầy accept                      |                                   |                  | 2                  |

## Phần 4: Tài liệu hóa (Documentation)
*Mục tiêu: Trình bày yêu cầu một cách chuyên nghiệp.*

| STT | Nội dung kiểm tra                                                                     | Trạng thái (V) |   Trả lời    | Ghi chú                                                    | Mức độ cần thiết | Giai đoạn đánh giá |
| :-: | :------------------------------------------------------------------------------------ | :------------: | :----------: | :--------------------------------------------------------- | ---------------- | ------------------ |
| 13  | Đã sử dụng cấu trúc **User Story** cho các yêu cầu hướng người dùng chưa?             |                | Chưa xét đến | "I as a... want... because..."                             |                  | 2                  |
| 14  | Mỗi yêu cầu đã có một **ID duy nhất** (ví dụ: REQ_001, REQ_002) để dễ truy xuất chưa? |                | Chưa xét đến | Kiểm tra trong [[bea-requirement-engineering.pdf#page=34]] |                  | 2                  |
| 15  | Đã có mô tả về **Tiêu chí nghiệm thu (Acceptance Criteria)** cho từng yêu cầu chưa?   |                | Chưa xét đến | Làm sao giáo viên biết bạn đã hoàn thành?                  |                  | 2                  |

## Phần 5: Quản lý thay đổi (Change Management)
*Mục tiêu: Kiểm soát khi giáo viên thay đổi ý định giữa kỳ.*

| STT | Nội dung kiểm tra                                                                                                   | Trạng thái (V) |            Trả lời             | Ghi chú                                                    | Giai đoạn đánh giá |
| :-: | :------------------------------------------------------------------------------------------------------------------ | :------------: | :----------------------------: | :--------------------------------------------------------- | ------------------ |
| 16  | Nếu giáo viên yêu cầu thêm tính năng mới, bạn đã phân tích tác động (Impact Analysis) đến phần cứng/thời gian chưa? |       x        |       Không cần xét đến        | Kiểm tra trong [[bea-requirement-engineering.pdf#page=36]] | 3                  |
| 17  | Đã cập nhật **Baseline** (Bản chốt yêu cầu) mới nhất sau khi thảo luận với nhóm và giáo viên chưa?                  |                | Đang trong quá trình thảo luận | Kiểm tra trong [[bea-requirement-engineering.pdf#page=34]] | 3                  |
