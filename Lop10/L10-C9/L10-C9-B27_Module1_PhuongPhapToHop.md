# Module 1: Tính xác suất bằng phương pháp tổ hợp
### Bài 27 — Thực hành tính xác suất theo định nghĩa cổ điển | Toán 10, Chương IX | Chủ đề 55

---

**Mục tiêu:** Học sinh tự hình thành kỹ thuật dùng tổ hợp để tính n(Ω), n(E) khi phép thử là "chọn ra 1 tập con", và biết phối hợp quy tắc nhân khi biến cố có nhiều điều kiện thành phần.

**Sai lầm cần giải quyết:**
1. Tính sai n(Ω) do không phân biệt có/không thứ tự — nhầm dùng chỉnh hợp thay vì tổ hợp.
2. Quên nhân các công đoạn khi biến cố có nhiều điều kiện thành phần.

**Loại simulation:** Khám phá — thử liệt kê tay trước (thấy bế tắc) → hình thành kỹ thuật → step-by-step áp dụng → luyện tập nhiều bài.

**Thời gian hoàn thành dự kiến:** ~14 phút.

**Dạy từ đầu hay tổng kết:** **Dạy từ đầu** — không có video giới thiệu trước. Tuy kỹ năng tổ hợp (Bài 24) và định nghĩa xác suất (Bài 26) đã học, nhưng CÁCH KẾT HỢP 2 kiến thức đó để giải bài toán xác suất là kỹ thuật hoàn toàn mới, cần hình thành qua ví dụ cụ thể trước khi tổng kết.

---

## Bối cảnh mở đầu — CLB Nghiên cứu khoa học

**Athena:** *"CLB Nghiên cứu khoa học của trường có 9 thành viên: 5 bạn giỏi Tin học, 4 bạn giỏi Vật lý. Nhà trường chọn ngẫu nhiên 5 bạn đại diện dự thi khoa học kỹ thuật cấp tỉnh. Hỏi có bao nhiêu cách chọn? Trong số đó, xác suất để cả 5 bạn được chọn đều giỏi Tin học là bao nhiêu?"*

## 🖼️ Phác thảo canvas — Lưới 9 thẻ tên

- **Bố cục:** lưới 3×3 thẻ, mỗi thẻ ghi "Bạn [số]" + môn mạnh. 5 thẻ tô màu xanh (Tin học), 4 thẻ tô màu cam (Vật lý) — màu sắc là tín hiệu duy nhất phân biệt 2 nhóm, không dùng icon để giữ giao diện gọn.
- **Panel bên phải (hoặc dưới, trên mobile):** khung "Đã chọn: 0/5" cập nhật real-time, nút "Tạo cách chọn mới" để xoá lựa chọn và thử lại.
- **Trạng thái 1 thẻ:** mặc định (viền mờ) → hover (viền đậm, đổi con trỏ) → đã chọn (viền dày + dấu ✓ góc trên-phải). Khi đã chọn đủ 5, các thẻ chưa chọn tạm mờ đi (opacity 0.5) để nhấn mạnh giới hạn 5, học sinh vẫn bấm được để đổi lựa chọn (bỏ 1 thẻ đã chọn trước khi chọn thẻ mới).
- **Không giới hạn số lần "Tạo cách chọn mới"** ở Bước 1 (khám phá tự do) — chỉ ghi nhận số lần học sinh đã thử để Athena tham chiếu khi hỏi "Bạn thấy có thể liệt kê hết bằng tay không?".

## Bước 1 — Thử liệt kê tay (tự thấy bế tắc)

**Canvas:** hiện 9 thẻ tên (5 thẻ xanh = Tin học, 4 thẻ cam = Vật lý). Học sinh tự click chọn 5 thẻ để tạo 1 cách chọn, hệ thống ghi lại — học sinh thử tạo vài cách khác nhau.

**Athena hỏi sau vài lần thử:** *"Bạn thấy có thể liệt kê hết tất cả các cách chọn bằng tay không? Bạn đã học công cụ nào ở Bài 24 để đếm nhanh số cách 'chọn ra 1 nhóm' mà không cần liệt kê hết?"*

→ Học sinh tự nhớ lại **tổ hợp** (Bài 24).

## Bước 2 — Hình thành kỹ thuật: xác định n(Ω)

**Athena hỏi:** *"5 bạn được chọn có phân vai trò khác nhau không (VD ai làm trưởng nhóm), hay chỉ đơn giản là 1 nhóm 5 bạn?"*

- Học sinh chọn "Không phân vai trò" → *"Vậy đây là bài toán tổ hợp: n(Ω) = C⁹₅."* Học sinh tự tính (dùng máy tính cầm tay đã học ở Bài 24): C⁹₅ = 126.
- Nếu học sinh chọn "Có phân vai trò" (sai): gợi ý — *"Đề bài có yêu cầu phân biệt vị trí/vai trò giữa 5 bạn được chọn không?"*

## Bước 3 — Biến cố F: "5 bạn được chọn đều giỏi Tin học"

- Học sinh tự nhận ra: chỉ có đúng 5 bạn giỏi Tin học trong CLB, nên chỉ có **1 cách duy nhất** chọn đủ 5 bạn đó.
- n(F) = 1, P(F) = 1/126.

## Bước 4 — Biến cố D: "Trong 5 bạn có 3 Tin học và 2 Vật lý" (nhiều điều kiện thành phần)

**Athena:** *"Biến cố này có 2 điều kiện — bạn hãy tính riêng từng phần rồi ghép lại bằng quy tắc nào đã học ở Bài 23?"*

- Ô 1: "Chọn 3 bạn từ 5 bạn Tin học" → C⁵₃ = 10.
- Ô 2: "Chọn 2 bạn từ 4 bạn Vật lý" → C⁴₂ = 6.
- Ô 3: "Ghép lại bằng quy tắc nào?" → Nhân: 10 × 6 = 60. P(D) = 60/126 = 10/21.

### 3-strike ở Ô 3 (bẫy quên nhân, cộng nhầm):
- Lần sai 2: gợi ý — *"2 công đoạn này có làm nối tiếp nhau, độc lập với nhau không? Nhớ lại quy tắc nhân ở Bài 23."*
- Lần sai 3: đáp án đúng kèm giải thích 10 × 6 = 60.

## Bước 5 — Athena khái quát hoá kỹ thuật

> Athena: *"Khi phép thử là 'chọn ra 1 nhóm' (không phân biệt thứ tự), ta dùng tổ hợp để tính n(Ω) và n(E). Nếu biến cố có nhiều điều kiện thành phần độc lập, tính riêng số cách mỗi điều kiện rồi nhân lại trước khi áp dụng P(E) = n(E)/n(Ω)."*

---

## Tổng kết kiến thức

> Khi phép thử là "chọn ra 1 nhóm/tập con" (không phân biệt thứ tự, vai trò), dùng **tổ hợp** để tính n(Ω) và n(E). Nếu biến cố gồm nhiều điều kiện thành phần độc lập, tính riêng số cách mỗi điều kiện rồi **nhân** lại (quy tắc nhân — Bài 23) trước khi áp dụng P(E) = n(E)/n(Ω).
>
> ⚠️ Luôn tự hỏi trước khi tính: phép thử này có phân biệt thứ tự/vai trò giữa các phần tử được chọn không? Nếu KHÔNG → dùng tổ hợp, không dùng chỉnh hợp.

---

## Bài tập luyện tập (3 câu, bối cảnh mới)

| # | Đề bài | Đáp án (đã kiểm chứng) |
|---|---|---|
| 1 | CLB Văn nghệ có 14 thành viên: 8 bạn giỏi vẽ, 6 bạn giỏi nhạc. Chọn ngẫu nhiên 6 bạn vào ban tổ chức hội diễn. Tính xác suất để số bạn giỏi vẽ bằng số bạn giỏi nhạc. | n(Ω)=C¹⁴₆=3003; n(E)=C⁸₃·C⁶₃=1120; P=160/429≈0,373 |
| 2 | Đội tuyển Toán của trường có 12 học sinh: 7 em lớp 10, 5 em lớp 11. Chọn ngẫu nhiên 4 em thi giao lưu. Tính xác suất cả 4 em đều học lớp 10. | n(Ω)=C¹²₄=495; n(E)=C⁷₄=35; P=7/99 |
| 3 | Vẫn đội tuyển ở Câu 2, tính xác suất trong 4 em có đúng 2 em lớp 10 và 2 em lớp 11. | n(E)=C⁷₂·C⁵₂=210; P=210/495=14/33 |

Mỗi câu hiện độc lập (không khoá dần), có ô nhập riêng + 3-strike riêng theo đúng cơ chế đã dùng ở phần hình thành kiến thức.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Bước 1-4 mỗi bước 1 khối full-width xếp dọc. Canvas 9 thẻ tên đặt bên trái ~60% ở Bước 1, khung thoại bên phải ~40%. Bài tập luyện tập xếp dọc 3 khối full-width bên dưới.

**Mobile (≤767px):** Giữ nguyên thứ tự dọc, 9 thẻ tên xếp lưới 3×3, vùng chạm mỗi thẻ ≥44px. Không cần pattern lướt ngang.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Click chọn thẻ tên (Bước 1) | Click từng thẻ | Chạm từng thẻ ≥44px |
| Chọn "Có/Không phân vai trò" | Click 1 trong 2 nút | Chạm 1 trong 2 nút ≥44px |
| Nhập kết quả số | Gõ bàn phím, click Kiểm tra | Chạm ô input `inputmode="numeric"`, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm1_thu_liet_ke',    type: 'explored', required: true },
  { id: 'm1_xac_dinh_omega', type: 'answered', required: true },
  { id: 'm1_bien_co_f',      type: 'answered', required: true },
  { id: 'm1_bien_co_d',      type: 'answered', required: true },
  { id: 'm1_bt1',            type: 'answered', required: true },
  { id: 'm1_bt2',            type: 'answered', required: true },
  { id: 'm1_bt3',            type: 'answered', required: true }
]
```
`progress total = 7`.

### `athenaGuidance`
```
1. m1_thu_liet_ke: chỉ hỏi ngược "Bạn thấy có thể liệt kê hết bằng tay
   không? Bạn đã học công cụ nào ở Bài 24?" — không nói thẳng đáp án
   là tổ hợp.
2. m1_xac_dinh_omega: gợi ý lần sai thứ 2 CHỈ dùng đúng câu "Đề bài có
   yêu cầu phân biệt vị trí/vai trò giữa các bạn được chọn không?"
3. m1_bien_co_f: chỉ xác nhận đúng/sai đơn giản.
4. m1_bien_co_d: gợi ý lần sai thứ 2 CHỈ dùng đúng câu "2 công đoạn này
   có làm nối tiếp nhau, độc lập với nhau không?" — không tính hộ 60.
5-7. m1_bt1..3: gợi ý tương tự mục 4, áp dụng đúng số liệu từng câu —
   không tính hộ đáp án cuối.
```
