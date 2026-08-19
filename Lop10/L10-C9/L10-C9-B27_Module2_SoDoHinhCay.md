# Module 2: Tính xác suất bằng sơ đồ hình cây
### Bài 27 — Thực hành tính xác suất theo định nghĩa cổ điển | Toán 10, Chương IX | Chủ đề 55

---

**Mục tiêu:** Học sinh tự hình thành kỹ thuật dùng sơ đồ hình cây (đã học ở Bài 23) để mô tả không gian mẫu của phép thử nhiều công đoạn, đếm số lá thoả biến cố, rồi tính xác suất.

**Sai lầm cần giải quyết:** Vẽ thiếu/lặp nhánh khi dựng cây; đếm sai số lá thoả biến cố.

**Loại simulation:** Đặt vấn đề trước (phép thử phức tạp, khó liệt kê trực tiếp) → tự nhớ lại công cụ sơ đồ cây → xây dựng có hướng dẫn → luyện tập nhiều bài.

**Thời gian hoàn thành dự kiến:** ~14 phút.

**Dạy từ đầu hay tổng kết:** **Dạy từ đầu** — không có video giới thiệu trước. Sơ đồ cây đã học ở Bài 23 để ĐẾM, nhưng dùng sơ đồ cây để TÍNH XÁC SUẤT là kỹ thuật mới, cần hình thành qua ví dụ.

---

## Bối cảnh mở đầu — Hộp thăm hội chợ

**Athena:** *"Một gian hàng hội chợ có 3 hộp thăm. Hộp I có 4 màu thăm: đỏ, xanh, vàng, tím. Hộp II có 3 màu: đỏ, vàng, tím. Hộp III có 2 màu: xanh, tím. Người chơi rút ngẫu nhiên 1 thăm từ mỗi hộp. Tính xác suất để trong 3 thăm rút ra có ĐÚNG 1 thăm màu tím."*

## 🖼️ Phác thảo canvas — Hook mở đầu + công cụ xây cây

**Hook (trước khi vào bước tương tác):** hiện hình 3 hộp gỗ kiểu hội chợ, mỗi hộp có các thăm màu (thanh nhỏ dạng vé số) nhô lên đúng số màu của hộp đó (Hộp I: 4 thăm màu đỏ/xanh/vàng/tím; Hộp II: 3 thăm đỏ/vàng/tím; Hộp III: 2 thăm xanh/tím) — giúp học sinh hình dung ngay bối cảnh trước khi chuyển sang canvas xây cây tương tác.

**Canvas xây cây (từ Bước 2):** tái dùng đúng công cụ "xây cây" ở Bài 23 Module 2 — root "Rút 3 thăm" ở trên, 3 tầng ô trống nét đứt tương ứng Hộp I → II → III, khay nhãn màu cố định phía dưới (7 nhãn: đỏ, xanh, vàng, tím ×2 lần dùng lại được vì mỗi màu xuất hiện ở nhiều hộp). Node lá (đã điền đủ 3 tầng) hiện dạng "đỏ-vàng-xanh" ngắn gọn, không hiện lại toàn bộ đường đi để tránh rối mắt ở tầng cuối (24 lá).

## Bước 1 — Nhận diện vấn đề

**Athena hỏi:** *"Phép thử này có mấy công đoạn? Bạn đã học công cụ nào ở Bài 23 để liệt kê đầy đủ, có hệ thống các kết quả của phép thử nhiều công đoạn?"*

→ Học sinh tự nhớ lại **sơ đồ hình cây**.

## Bước 2 — Dựng cây mô tả không gian mẫu

**Canvas:** công cụ "xây cây" (tái dùng đúng cơ chế kéo-thả ở Bài 23 Module 2) — 3 tầng: tầng 1 là 4 nhánh (màu Hộp I), tầng 2 là 3 nhánh dưới MỖI nhánh tầng 1 (màu Hộp II), tầng 3 là 2 nhánh dưới MỖI nhánh tầng 2 (màu Hộp III).

- Học sinh tự kéo các nhãn màu vào đúng vị trí từng tầng.
- Bấm "Đếm lá cây" → n(Ω) = 4 × 3 × 2 = 24.

### Kịch bản sai lầm (không chặn, tự đối chất qua đếm lá — giống cơ chế Bài 23):
Nếu học sinh dựng thiếu nhánh hoặc lặp nhánh, số lá đếm được sẽ khác 24 — hệ thống chẩn đoán loại lỗi (thiếu/lặp) như đã làm ở Bài 23, đưa gợi ý tương ứng ở lần sai thứ 2.

## Bước 3 — Đếm lá thoả biến cố

**Athena:** *"Biến cố K: 'Đúng 1 thăm màu tím'. Bạn hãy click đánh dấu các lá cây thoả biến cố K."*

- Học sinh click từng lá (mỗi lá là 1 tổ hợp 3 màu) có đúng 1 màu tím trong 3.
- Đáp án: 11 lá thoả mãn trong tổng 24 lá.
- 3-strike: lần sai 2 gợi ý — *"Bạn thử kiểm tra từng lá: có đúng 1 chữ 'tím' xuất hiện không (không phải 0, không phải 2)?"*

## Bước 4 — Tính xác suất & khái quát hoá

P(K) = 11/24.

> Athena: *"Số lá cây chính là n(Ω); số lá đánh dấu chính là n(E). Với mọi phép thử nhiều công đoạn, bạn có thể dùng đúng cách này: dựng cây → đếm tổng lá → đánh dấu lá thoả biến cố → tính P(E) = n(E)/n(Ω)."*

---

## Tổng kết kiến thức

> Với phép thử gồm nhiều công đoạn liên tiếp, **sơ đồ hình cây** giúp liệt kê đầy đủ, không sót, không trùng các kết quả của không gian mẫu Ω (số lá cây = n(Ω)). Để tính xác suất của 1 biến cố, đánh dấu các lá cây thoả điều kiện của biến cố đó (n(E) = số lá được đánh dấu), rồi áp dụng P(E) = n(E)/n(Ω).

---

## Bài tập luyện tập (3 câu, bối cảnh mới)

| # | Đề bài | Đáp án (đã kiểm chứng) |
|---|---|---|
| 1 | Máy bán nước tự động có 2 cần gạt: cần chọn cỡ ly (nhỏ, vừa, lớn) và cần chọn vị (cam, chanh, dâu, việt quất). Tính xác suất nhận được ly cỡ LỚN và vị CAM hoặc CHANH. | Cây 2 tầng: n(Ω)=3×4=12; n(E)=2; P=1/6 |
| 2 | Tung liên tiếp 1 đồng xu 3 lần. Tính xác suất có ĐÚNG 2 lần mặt Sấp. | Cây 3 tầng: n(Ω)=2³=8; n(E)=3 (SSN,SNS,NSS); P=3/8 |
| 3 | Gieo 1 xúc xắc 2 lần liên tiếp. Tính xác suất tổng số chấm 2 lần gieo bằng 8. | Cây 2 tầng (6×6): n(Ω)=36; n(E)=5 — các cặp (2,6),(3,5),(4,4),(5,3),(6,2); P=5/36 |

Mỗi câu dựng cây riêng (tái dùng công cụ "xây cây"), có ô nhập kết quả + 3-strike riêng.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Mỗi bước/câu 1 khối full-width. Canvas cây đặt bên trái ~65%, khay nhãn + khung thoại bên phải ~35%.

**Mobile (≤767px):** Canvas cây hiện trước (cho phép cuộn ngang/pinch-zoom nếu cây rộng), khay nhãn cuộn ngang ngay dưới, khung thoại xuống cuối. Không cần pattern lướt ngang toàn trang.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:** (tái dùng nguyên bảng đã có ở Bài 23 Module 2)

| Thao tác | Desktop | Mobile |
|---|---|---|
| Kéo nhãn màu vào cây | Kéo-thả bằng chuột | Kéo-thả bằng ngón tay (Pointer Events, `touch-action:none`) |
| Đếm lá / đánh dấu lá thoả biến cố | Click từng lá | Chạm từng lá ≥44px |
| Nhập kết quả xác suất | Gõ bàn phím, click Kiểm tra | Chạm ô input, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm2_nhan_dien',    type: 'explored', required: true },
  { id: 'm2_xay_cay',      type: 'explored', required: true },
  { id: 'm2_dem_la_k',     type: 'answered', required: true },
  { id: 'm2_tinh_xs_k',    type: 'answered', required: true },
  { id: 'm2_bt1',          type: 'answered', required: true },
  { id: 'm2_bt2',          type: 'answered', required: true },
  { id: 'm2_bt3',          type: 'answered', required: true }
]
```
`progress total = 7`.

### `athenaGuidance`
```
1. m2_nhan_dien: chỉ hỏi ngược "Phép thử này có mấy công đoạn? Bạn đã
   học công cụ nào ở Bài 23?" — không nói thẳng đây là sơ đồ cây.
2. m2_xay_cay: chỉ nhắc quy trình dựng cây theo đúng thứ tự Hộp I → II
   → III, không chỉ vị trí kéo cụ thể.
3. m2_dem_la_k: gợi ý lần sai thứ 2 CHỈ dùng đúng câu "Bạn thử kiểm tra
   từng lá: có đúng 1 chữ 'tím' xuất hiện không?" — không nói số lá
   đúng là 11.
4. m2_tinh_xs_k: chỉ xác nhận đúng/sai đơn giản.
5-7. m2_bt1..3: gợi ý tương tự mục 3, đổi theo đúng điều kiện biến cố
   của từng bài.
```
