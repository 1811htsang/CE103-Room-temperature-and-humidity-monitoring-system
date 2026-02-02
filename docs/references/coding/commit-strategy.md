Đối với một dự án Embedded (nhất là khi làm một mình hoặc nhóm nhỏ để xây dựng Portfolio), chiến lược **Git Flow tối giản kết hợp "Squash Merge"** là lựa chọn vàng.

Mục tiêu của chiến lược này là: **"Nháp thì cứ nháp thoải mái, nhưng khi nộp bài (merge vào main) thì phải sạch đẹp như sách giáo khoa"**.

Dưới đây là thiết kế chi tiết chiến lược phân nhánh (Branching Strategy).

---

### 1. CẤU TRÚC NHÁNH (BRANCH STRUCTURE)

Bạn chỉ cần duy trì **2 loại nhánh** chính:

1.  **`main` (hoặc `master`):**
    *   **Vai trò:** Đây là nhánh "Production". Code trên nhánh này **BẮT BUỘC** phải biên dịch được (compilable) và chạy ổn định.
    *   **Ý nghĩa:** Đây là bộ mặt của bạn. Khi nhà tuyển dụng vào xem, họ sẽ xem nhánh này đầu tiên.
    *   **Quy tắc:** Không bao giờ commit trực tiếp lên `main`.

2.  **`feat/...`, `fix/...`, `docs/...` (Short-lived Branches):**
    *   **Vai trò:** Nhánh tạm thời để phát triển tính năng hoặc sửa lỗi.
    *   **Ý nghĩa:** Đây là công trường xây dựng. Bạn có thể commit 10 lần, code sai, sửa lại... không sao cả.
    *   **Quy tắc:** Tạo ra từ `main`, làm xong thì merge lại vào `main` rồi xóa đi.

---

### 2. QUY TẮC ĐẶT TÊN NHÁNH (NAMING CONVENTION)

Áp dụng format: `category/scope-description`

*   **`feat/`**: Tính năng mới (Feature).
    *   Ví dụ: `feat/uart-driver`, `feat/bootloader-logic`, `feat/esp32-i2s`.
*   **`fix/`**: Sửa lỗi (Bug fix).
    *   Ví dụ: `fix/uart-baudrate`, `fix/dma-buffer-overflow`.
*   **`docs/`**: Tài liệu.
    *   Ví dụ: `docs/wiring-diagram`, `docs/update-readme`.
*   **`refactor/`**: Tối ưu code cũ.
    *   Ví dụ: `refactor/gpio-registers`.

---

### 3. CHIẾN LƯỢC "SQUASH MERGE" (VŨ KHÍ BÍ MẬT)

Đây là chìa khóa để lịch sử commit của bạn **SẠCH**.

**Vấn đề:**
Khi làm tính năng `feat/uart-driver`, có thể commit 5 lần:
1. "Start coding uart" (Code chưa chạy)
2. "Fix typo" (Sửa lỗi chính tả)
3. "Uart working but buggy" (Chạy được nhưng lỗi)
4. "Fix bug"
5. "Finalize uart driver"

Nếu merge cả 5 commit này vào `main`, lịch sử sẽ rất rác.

**Giải pháp (Squash Merge):**
Gộp 5 commit "nháp" kia thành **1 commit duy nhất** và đưa vào `main`.
Message của commit gộp đó sẽ là chuẩn chỉnh: `feat(uart): implement polling uart driver with baudrate configuration`.

---

### 4. QUY TRÌNH LÀM VIỆC (WORKFLOW)

Giả sử bắt đầu viết Driver cho GPIO.

#### Bước 1: Tạo nhánh mới từ Main
```bash
git checkout main
git pull origin main          # Đảm bảo code mới nhất
git checkout -b feat/gpio-driver
```

#### Bước 2: Code và Commit (Thoải mái)
Code, test, sửa lỗi. Commit bao nhiêu lần tùy thích.
```bash
git add .
git commit -m "wip: setup gpio struct"
... code tiếp ...
git add .
git commit -m "gpio toggle working"
```

#### Bước 3: Merge vào Main (Dùng giao diện GitHub/GitLab)
1.  Push nhánh lên GitHub: `git push origin feat/gpio-driver`
2.  Tạo **Pull Request (PR)** từ `feat/gpio-driver` vào `main`.
3.  **QUAN TRỌNG:** Khi nhấn nút Merge trên GitHub, chọn mũi tên xổ xuống và chọn **"Squash and merge"**.
4.  Viết lại tiêu đề commit theo chuẩn: `feat(gpio): implement bare-metal gpio driver`.

#### Bước 4: Dọn dẹp
Sau khi merge xong, xóa nhánh `feat/gpio-driver` đi.

---

### 5. QUẢN LÝ PHIÊN BẢN (VERSION TAGGING)

Với dự án nhúng, "Release" gắn liền với phần cứng, nên dùng **Tags** để đánh dấu các cột mốc quan trọng.

*   **v0.1.0:** Hoàn thành Drivers cơ bản (GPIO, UART).
*   **v0.2.0:** Hoàn thành Bootloader logic (chưa có OTA).
*   **v1.0.0:** Hoàn thành Project (Bootloader + App + Python Tool).

**Cách làm:**
Sau khi một tính năng lớn hoàn thành và merge vào `main`:
```bash
git tag -a v0.1.0 -m "Release v0.1.0: Basic Drivers Completed"
git push origin v0.1.0
```
*Trên GitHub, nó sẽ hiện ra mục "Releases" rất chuyên nghiệp bên cạnh source code.*

---

### 6. MÔ HÌNH TRỰC QUAN (VISUALIZATION)

Nếu làm đúng chiến lược **Squash Merge**, cây lịch sử (Git Graph) sẽ trông như một đường thẳng tắp, rất đẹp (Linear History):

```text
(Main Branch)
  O  <-- feat(release): v1.0.0 complete project
  |
  O  <-- fix(boot): resolve vector table offset issue
  |
  O  <-- feat(boot): implement xmodem protocol logic
  |
  O  <-- feat(drivers): implement uart and timer drivers
  |
  O  <-- feat(bsp): initial board support package
  |
  O  <-- chore: initial project structure
```

**Ngược lại (Nếu không Squash):** Nó sẽ rối như mạng nhện với các nhánh rẽ ra rẽ vào và các commit vô nghĩa như "fix typo", "update".

### TỔNG KẾT CHIẾN LƯỢC:

1.  **Branching:** Tạo nhánh `feat/...` cho mỗi chức năng (GPIO, UART, I2S...).
2.  **Working:** Commit thoải mái trên nhánh con.
3.  **Merging:** Luôn dùng **Squash Merge** để gộp thành 1 commit "xịn" khi đưa vào `main`.
4.  **Release:** Đánh **Tag** (`v1.0`) khi hoàn thành một giai đoạn lớn.