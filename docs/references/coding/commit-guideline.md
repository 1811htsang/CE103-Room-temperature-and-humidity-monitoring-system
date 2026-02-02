# Giới thiệu
Đối với dự án này, tập trung vào tuân thủ tiêu chuẩn *Conventional commits* để đảm bảo lịch sử cam kết rõ ràng và nhất quán.

# Công thức chuẩn
Cấu trúc một commit tuân theo định dạng sau:
```
Type(Scope): Subject
```

Trong đó:
- **Type** để chỉ định loại thay đổi được thực hiện.
- **Scope** là tùy chọn và chỉ định phần cụ thể của mã bị ảnh hưởng. (Có thể chỉ rõ các file bị ảnh hưởng)
- **Subject** là mô tả ngắn gọn về thay đổi. (Sử dụng *imperative mood*)

## Đối với nhóm tính năng mới
Sử dụng loại commit `feat` để biểu thị việc thêm một tính năng mới vào dự án. 
Các thao tác ở nhóm commit này là
- **Implement**: Triển khai một chức năng hoàn chỉnh (dùng nhiều nhất).
  - Ví dụ: *feat(uart): implement XMODEM protocol for file transfer*
- **Integrate**: Tích hợp thư viện hoặc module bên ngoài.
  - Ví dụ: *feat(rtos): integrate FreeRTOS kernel v10.4*
- **Introduce**: Giới thiệu một cấu hình hoặc kiến trúc mới.
  - Ví dụ: *feat(bsp): introduce linker script for dual-bank flash*
- **Expose**: Mở API cho layer khác sử dụng.
  - Ví dụ: *feat(i2s): expose DMA interrupt callback functions*

## Đối với nhóm sửa lỗi
Sử dụng loại commit `fix` để biểu thị việc sửa lỗi trong mã nguồn.
Các thao tác ở nhóm commit này là
- **Resolve**: Giải quyết triệt để một vấn đề logic.
  - Ví dụ: *fix(dma): resolve circular buffer overflow on high load*
- **Handle**: Xử lý các trường hợp ngoại lệ (Edge cases).
  - Ví dụ: *fix(adc): handle jitter when wifi is transmitting*
- **Prevent**: Ngăn chặn lỗi tiềm ẩn.
  - Ví dụ: *fix(bootloader): prevent jump to app if checksum fails*
- **Patch**: Vá lỗi nhanh hoặc sửa lỗi nhỏ.
  - Ví dụ: *fix(gpio): patch wrong pin definition for LED_BUILTIN*

## Đối với nhóm tối ưu , tái cấu trúc
Sử dụng loại commit `refactor` để biểu thị việc tái cấu trúc mã nguồn mà không thêm tính năng mới hoặc sửa lỗi.
Các thao tác ở nhóm commit này là
- **Optimize**: Tối ưu hóa hiệu năng/bộ nhớ.
  - Ví dụ: *perf(isr): optimize interrupt latency by moving code to IRAM*
  - Ví dụ: *perf(flash): reduce code size by bypassing HAL libraries*
- **Refactor**: Viết lại code cho sạch hơn mà không đổi tính năng.
  - Ví dụ: *refactor(uart): decouple hardware dependency from logic layer*
- **Simplify**: Đơn giản hóa logic phức tạp.
  - Ví dụ: *refactor(fsm): simplify state transition logic*

## Đối với nhóm tài liệu
Sử dụng loại commit `docs` để biểu thị việc cập nhật tài liệu.
Các thao tác ở nhóm commit này là
- **Document**: Viết tài liệu code.
  - Ví dụ: *docs(readme): document wiring diagram for ESP32 and Mic*
- **Configure**: Thay đổi cài đặt hệ thống.
  - Ví dụ: *chore(cmake): configure build output directory*
- **Update**: Cập nhật thông thường (hạn chế dùng cho code logic, dùng cho docs/tool).
  - Ví dụ: *docs(contributing): update commit guidelines*
- **Add**: Thêm tài liệu mới.
  - Ví dụ: *docs(api): add API reference for UART driver*

## Đối với nhóm cấu trúc quản lý phiên bản
Sử dụng loại commit `struct` để biểu thị việc thay đổi cấu trúc quản lý phiên bản mà không ảnh hưởng đến mã nguồn.
Các thao tác ở nhóm commit này là
- **Bump**: Tăng phiên bản phần mềm.
- **Merge**: Hợp nhất các nhánh quản lý phiên bản.
- **Release**: Đánh dấu phát hành phiên bản mới.
- **Tag**: Gắn thẻ phiên bản trong hệ thống quản lý mã nguồn.

# Lưu ý bổ sung

## 1. Nguyên tắc "Nhánh nào việc nấy" (Separation of Concerns)
Mặc dù đã đồng bộ (merge) hai nhánh, nhưng mục đích ban đầu của chúng vẫn khác nhau:
*   **Nhánh `feat`**: Tập trung phát triển tính năng (Code là chính).
*   **Nhánh `docs`**: Tập trung viết tài liệu (Markdown, hướng dẫn là chính).

**Nếu bạn đang ở nhánh `feat` mà lại sửa tài liệu:**
Sau này khi bạn tạo Pull Request (PR) để đưa code vào nhánh chính (`main` hoặc `develop`), cái PR đó sẽ bị lẫn lộn giữa "Code tính năng" và "Cập nhật tài liệu". Người review sẽ khó theo dõi.

## 2. Hiện tượng "File rác" khi chuyển nhánh (Working Directory)
Có một điểm quan trọng: Nếu bạn tạo một file mới nhưng **chưa commit**, khi bạn dùng `git checkout` sang nhánh khác, file đó sẽ "đi theo" bạn sang nhánh mới.
**Nguy cơ:** Bạn định thêm tài liệu vào nhánh `docs`, nhưng quên không checkout, bạn tạo file ở `feat`. Sau đó bạn nhớ ra và checkout sang `docs`, file đó vẫn nằm đó. Nếu bạn không cẩn thận `git add`, bạn sẽ commit nhầm những thứ không liên quan.

## 3. Quy trình làm việc (Workflow) khuyến nghị

Để tránh nhập nhằng, bạn nên áp dụng quy trình sau:

### Kịch bản A: Bạn muốn bổ sung Tài liệu
1.  `git checkout docs` (Chuyển hẳn sang nhánh tài liệu).
2.  Thực hiện viết tài liệu, tạo file mới.
3.  `git add` và `git commit`.
4.  Nếu muốn nhánh `feat` cũng có tài liệu mới này: `git checkout feat` -> `git merge docs`.

### Kịch bản B: Bạn muốn bổ sung Code
1.  `git checkout feat`.
2.  Viết code, tạo file code mới.
3.  `git add` và `git commit`.
4.  (Thường thì nhánh `docs` không cần chứa code đang phát triển, nên bạn không cần merge ngược lại).

## Mẹo xử lý khi "Lỡ quên" (Sử dụng Git Stash)
Nếu bạn đang code dở ở nhánh `feat` nhưng đột nhiên sếp bảo cập nhật tài liệu gấp ở nhánh `docs`:

1.  **Lưu tạm code đang dở:**
    ```bash
    git stash
    ```
2.  **Chuyển sang nhánh docs và làm việc:**
    ```bash
    git checkout docs
    # Sửa tài liệu...
    git add .
    git commit -m "Update docs"
    ```
3.  **Quay lại nhánh feat và lấy lại code đang làm dở:**
    ```bash
    git checkout feat
    git stash pop
    ```

## Tổng kết
Việc **checkout đúng nhánh trước khi tạo file/sửa file** là một thói quen cực tốt. Nó giúp:
*   Lịch sử Git rõ ràng (Nhìn vào log biết ngay commit nào sửa cái gì).
*   Tránh xung đột (Conflict) không đáng có.
*   Dễ dàng làm việc nhóm (Người khác nhìn vào nhánh `docs` chỉ thấy tài liệu, không thấy code rác).

**Lời khuyên:** Nếu tài liệu đó **phục vụ trực tiếp** cho tính năng đang làm ở nhánh `feat`, bạn có thể sửa trực tiếp ở `feat`. Nhưng sau khi xong, hãy merge `feat` vào `docs` để nhánh tài liệu luôn là "nguồn sự thật" (Source of truth) mới nhất.

# Sửa đổi commit message
Để sửa đổi commit message của commit gần nhất, bạn có thể sử dụng lệnh:
```bash
git commit --amend
```

Nếu commit đã push lên remote, bạn cần force push sau khi sửa đổi với `commit --amend`:
```bash
git push --force
```

# Thống nhất cách làm việc 
Dự án sẽ gồm các nhánh chính:
- `main`: Nhánh chính, chứa mã nguồn ổn định đã được kiểm thử kỹ lưỡng.
- `feat`: Nhánh phát triển tính năng mới.
- `docs`: Nhánh dành riêng cho tài liệu.
- `fix`: Nhánh sửa lỗi khi đang ở `feat` nhưng code bị lỗi cần sửa.
- `reft`: Nhánh tái cấu trúc khi cần tối ưu code mà không thêm tính năng mới hoặc sửa lỗi.
- `strc`: Nhánh quản lý phiên bản khi cần thay đổi cấu trúc thư mục và quản lý phiên bản.
Mỗi nhánh sẽ có mục đích riêng biệt, giúp tổ chức công việc rõ ràng và hiệu quả hơn.

Khi làm việc trên một tính năng mới, bạn sẽ làm việc trên nhánh `feat`. Nếu cần cập nhật tài liệu liên quan đến tính năng đó, bạn có thể tạo một commit trên nhánh `docs` sau khi hoàn thành công việc trên `feat`. Điều này giúp giữ cho lịch sử commit rõ ràng và dễ theo dõi.

Khi cần sửa lỗi, tối ưu mã nguồn hoặc thay đổi cấu trúc dự án, cần đảm bảo rằng đang ở đúng nhánh và ưu tiên nhánh `feat` cần được cập nhật trước khi thực hiện các thay đổi trên các nhánh khác.

Quy cách bổ sung docs/codes khi đang làm việc trên codes/docs đã có đề cập ở bên trên.

Quy cách về sửa đổi commit đã có đề cập ở bên trên.

Khi cần merge giữa 2 nhánh `a` (pwd) và `b`, commit mesage sẽ theo định dạng:
```
struct(b, a): Merge 'b' into 'a' to +<lý do cụ thể>
```