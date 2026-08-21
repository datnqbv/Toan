# 📚 KỊCH BẢN — Bài 25, Module 1: "Góc giữa hai mặt phẳng"

```
📖 PPCT: Tiết 70 — Chủ đề 9: Hai mặt phẳng vuông góc
📌 Đã dạy qua kênh khác: video Manim. Không rút gọn — mô phỏng 3D đầy đủ
   theo yêu cầu, cùng tinh thần Bài 23-24.
🎯 Sai lầm nhắm tới (PPCT):
   (A) chọn 2 đường KHÔNG cùng vuông góc với giao tuyến khi dựng góc
       phẳng nhị diện
   (B) xác định sai giao tuyến của 2 mặt phẳng
   (C) kẻ 2 đường vuông góc giao tuyến nhưng KHÔNG tại cùng 1 điểm chung
   (D) lẫn lộn góc của 2 đường thẳng với góc của 2 mặt phẳng
📁 File: Bai25_Toan3D_Module1_GocGiuaHaiMatPhang.html
```

> ⚠️ **Bối cảnh:** Bước 1 dùng mô hình "gấp giấy 3D" (không phải giấy
> thật, dựng bằng 2 mặt phẳng ảo mở góc) — đúng theo PPCT gợi ý trực
> quan hoá bằng gấp giấy nhưng chuyển hẳn sang tương tác 3D. Bước 4 đổi
> ví dụ khỏi SGK: SGK dùng đúng Bia chủ quyền đảo Song Tử Tây
> (11°25'55"N, 114°8'00"E) — đây là ví dụ minh hoạ RIÊNG của SGK (chọn
> đúng đảo này + đúng toạ độ này + đúng kỹ thuật "kinh độ = góc nhị
> diện"), không phải 1 sự thật phổ quát nhiều nguồn độc lập cùng chọn
> (khác Kim tự tháp Kheops) — nên đổi sang **Đảo Trường Sa Lớn**
> (8°38'41"N, 111°55'12"E, có cột mốc chủ quyền thật, đã verify qua web
> search) — vẫn giữ đúng tinh thần giáo dục chủ quyền biển đảo, chỉ đổi
> điểm mốc cụ thể khỏi SGK.

## Sổ tay kiến thức (hiện dần theo bước)

```
- Góc giữa 2 mặt phẳng (P), (Q) cắt nhau theo giao tuyến Δ: dựng trong
  mỗi mặt phẳng 1 đường thẳng vuông góc với Δ TẠI CÙNG 1 ĐIỂM O trên Δ —
  góc giữa 2 đường đó là góc giữa (P) và (Q).
- Nếu (P), (Q) song song hoặc trùng nhau: góc = 0°.
- Quy ước: 0° ≤ φ ≤ 90° (góc giữa 2 mặt phẳng, khác góc nhị diện có thể
  tới 180° — sẽ phân biệt rõ ở Bước 3).
- Góc không phụ thuộc vị trí điểm O chọn trên Δ (miễn 2 đường vẫn vuông
  góc Δ tại điểm đó).
```

---

## BƯỚC 1 — Hình thành định nghĩa qua "gấp giấy 3D"

**Cấu hình 3D:**
- 2 mặt phẳng (P), (Q) dạng 2 "tấm" hình chữ nhật nối nhau tại 1 cạnh
  chung Δ (giao tuyến, đứng dọc — trục z trong hệ toạ độ mô phỏng). (P)
  cố định (nằm ngang, chứa Δ và trục x). (Q) xoay được quanh Δ, góc mở θ
  từ 0° đến 180° (dùng PHẦN 2.6 gốc — bản lề NGANG... **khoan, đây là bản
  lề DỌC theo Δ đứng, cung quét mặt phẳng NGANG** → dùng đúng PHẦN 2.7,
  không phải 2.6, giống cách dùng ở cửa tủ/cần cẩu Bài 23).
- **Đối tượng kéo được:** mặt (Q), xoay quanh trục Δ, giống hệt cơ chế
  "mở cửa tủ quần áo" đã dùng ở Bài 23 Module 1 Bước 1 — chỉ đổi vai diễn
  (tấm giấy thay cửa tủ).
- Tại 1 điểm O cố định trên Δ (gốc), hệ thống tự dựng 2 tia m (trong P)
  và n (trong Q), CẢ 2 đều vuông góc Δ tại O — verify Python: với θ=60°,
  góc đo giữa m, n = đúng 60°.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đây là 2 mặt phẳng (P), (Q) cắt nhau theo giao tuyến Δ.
   Kéo để mở/đóng góc giữa 2 mặt — quan sát 2 tia m, n (đã dựng sẵn,
   vuông góc Δ tại điểm O) thay đổi theo."
   - *Hành động HS:* kéo mặt (Q) qua nhiều góc mở.
   - 🎯 **Mục tiêu quan sát:** góc giữa m và n LUÔN bằng đúng góc mở giữa
     (P) và (Q) — ở mọi vị trí.

2. **Giải thích đúng:** "Chính xác — đây là định nghĩa: góc giữa 2 mặt
   phẳng cắt nhau = góc giữa 2 đường thẳng vuông góc với giao tuyến,
   dựng tại cùng 1 điểm, mỗi đường nằm trong 1 mặt phẳng."

---

## BƯỚC 2 — Định lí: chọn điểm O khác trên Δ, góc không đổi

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Nếu chọn điểm O' khác trên Δ (không phải O ban đầu) để
   dựng 2 tia m', n' vuông góc Δ, góc giữa chúng có đổi không?"
   - *Hành động HS:* kéo điểm O trượt dọc theo Δ (dùng
     `ConstrainedPoint.dragToward`, PHẦN 2.2 đã có — kéo dọc 1 đoạn thẳng
     cố định).
   - 🎯 **Mục tiêu quan sát:** dù O ở vị trí nào trên Δ, góc giữa m', n'
     LUÔN giữ nguyên giá trị đã thấy ở Bước 1 (verify Python: 60° tại
     O=(0,0,0) và O=(0,0,5) — khớp tuyệt đối).

2. **Giải thích đúng:** "Đúng — vì tịnh tiến dọc theo Δ không đổi HƯỚNG
   của m, n (chỉ đổi vị trí), nên góc giữa chúng không đổi. Đây là lý do
   góc giữa 2 mặt phẳng là 1 giá trị XÁC ĐỊNH DUY NHẤT, không phụ thuộc
   cách chọn điểm O."

---

## BƯỚC 3 — Khái niệm góc nhị diện, góc phẳng nhị diện (nhấn mạnh điều kiện)

**Cấu hình 3D:** giữ nguyên (P), (Q), Δ từ Bước 1-2. Giới thiệu thuật
ngữ mới: góc nhị diện [P, Δ, Q] (0°-180°, RỘNG hơn góc giữa 2 mặt phẳng
0°-90°), và góc phẳng của nhị diện (chính là góc m, n vừa dựng).

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Giờ thử 1 tình huống DỄ SAI: nếu chọn tia m'' trong (P)
   và tia n'' trong (Q), nhưng KHÔNG vuông góc với Δ (chỉ là đường xiên
   bất kỳ trong mỗi mặt), góc giữa m'' và n'' có còn đúng bằng góc nhị
   diện không?"
   - *Hành động HS:* dùng thanh trượt "độ xiên" để nghiêng m'', n'' lệch
     khỏi hướng vuông góc Δ (2 thanh trượt riêng, mỗi mặt 1 thanh, độ
     lệch 0°-30°).
   - 🎯 **Mục tiêu quan sát:** khi độ xiên = 0° (đúng vuông góc Δ), góc
     đo = đúng góc nhị diện thật (60°). Khi kéo độ xiên khác 0° (VD
     20° và 15°), góc đo được đổi thành 1 giá trị KHÁC (verify Python:
     57,16° — sai lệch rõ so với 60° thật).

2. **3-strike (nhắm trực diện sai lầm A):** "Để dựng ĐÚNG góc phẳng nhị
   diện, 2 tia m, n cần thoả mãn điều kiện gì?"
   - A. Cùng nằm trong 1 mặt phẳng
   - B. Cùng vuông góc với giao tuyến Δ, VÀ cùng xuất phát từ 1 điểm
     trên Δ (đáp án đúng — vị trí random)
   - C. Chỉ cần vuông góc Δ, điểm xuất phát không quan trọng
   - Sai lần 1: rung nhẹ. Sai lần 2: gợi ý "thử kéo lại thanh trượt độ
     xiên về 0° — góc có đúng lại không? Vậy điều kiện thiếu là gì?".
     Hết lượt: hiện đáp án B + giải thích, nhắc lại minh hoạ độ xiên vừa
     làm.

3. **Câu hỏi phân biệt (nhắm sai lầm C — điểm chung, và sai lầm D — góc
   đường thẳng vs góc mặt phẳng):** "Nếu m dựng tại điểm O, còn n dựng
   tại điểm O' KHÁC O (cả 2 vẫn vuông góc Δ), việc đo 'góc giữa m và n'
   theo cách thông thường (góc giữa 2 đường thẳng bất kỳ trong không
   gian) có còn là góc nhị diện không?"
   - `dap_an_dung`: "Không — góc giữa 2 đường thẳng chéo nhau (không
     chung điểm) được tính bằng cách dựng lại 1 đường song song qua 1
     điểm chung trước (theo Bài 22), không phải là góc nhị diện trực
     tiếp. Góc nhị diện BẮT BUỘC 2 tia chung 1 điểm trên giao tuyến."

4. **Sổ tay bổ sung:** "Góc nhị diện [P,Δ,Q] nhận giá trị 0°-180°. Góc
   GIỮA 2 MẶT PHẲNG (P), (Q) luôn 0°-90° — nếu góc phẳng nhị diện đo được
   > 90°, góc giữa 2 mặt phẳng là phần bù (180° − góc đó)."

---

## BƯỚC 4 — Áp dụng: kinh độ Trái Đất (giữ bối cảnh, đã duyệt)

**Cấu hình 3D:**
- Mô hình Trái Đất (hình cầu), trục Bắc-Nam là giao tuyến Δ. 2 "múi"
  kinh tuyến: kinh tuyến gốc (qua Greenwich, kinh độ 0°) và kinh tuyến
  qua **cột mốc chủ quyền trên Đảo Trường Sa Lớn** (8°38'41"N,
  111°55'12"E — đảo lớn nhất quần đảo Trường Sa, có cột mốc chủ quyền
  ghi rõ kinh độ/vĩ độ).
- Verify Python: kinh độ = 111 + 55/60 + 12/3600 = 111,92° — dựng 2 tia
  m, n vuông góc trục Δ tại tâm O (tâm Trái Đất), nằm trong mỗi mặt
  kinh tuyến, góc đo được = đúng 111,92°.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đây là mặt phẳng chứa kinh tuyến gốc (qua Greenwich) và
   mặt phẳng chứa kinh tuyến qua cột mốc chủ quyền trên Đảo Trường Sa
   Lớn — đảo lớn nhất của quần đảo Trường Sa, Việt Nam. Giao tuyến của 2
   mặt phẳng này là gì?"
   - `dap_an_dung`: "Trục Bắc-Nam của Trái Đất — vì mọi mặt phẳng kinh
     tuyến đều chứa trục quay này."
   - `goi_y_khi_sai`: "Mọi kinh tuyến trên Trái Đất đều đi qua 2 điểm cố
     định nào?"

2. **Athena:** "Góc nhị diện giữa 2 mặt phẳng kinh tuyến này chính là
   ĐẠI LƯỢNG ĐỊA LÝ nào bạn đã biết?"
   - `dap_an_dung`: "Kinh độ — kinh độ của 1 điểm chính là góc nhị diện
     giữa mặt phẳng kinh tuyến qua điểm đó và mặt phẳng kinh tuyến gốc."
   - *Hành động HS:* xoay mô hình Trái Đất, quan sát 2 tia m, n dựng tại
     tâm O, đọc số đo góc hiện ra (111°55'12" ≈ 111,92°).

3. **Liên hệ mở rộng:** "Vậy vĩ độ (8°38'41"N của Đảo Trường Sa Lớn) có
   phải là góc nhị diện giống kinh độ không?" — câu hỏi mở, không chấm
   điểm, gợi mở cho bài sau/kiến thức địa lý liên môn (vĩ độ thực chất là
   góc giữa đường thẳng và mặt phẳng — liên hệ Bài 24, không phải góc
   nhị diện giữa 2 mặt phẳng).

---

## TỔNG HỢP KIẾN THỨC (đóng Module 1)

| Khối kiến thức | Nội dung | Xem lại tại |
|---|---|---|
| 1. Định nghĩa | Góc 2 mặt phẳng = góc 2 đường ⊥ giao tuyến, cùng 1 điểm | Bước 1 |
| 2. Tính bất biến | Không phụ thuộc điểm O chọn trên giao tuyến | Bước 2 |
| 3. Điều kiện dựng đúng | 2 tia PHẢI cùng vuông góc giao tuyến + cùng 1 điểm | Bước 3 |
| 4. Phân biệt góc nhị diện vs góc 2 mặt phẳng | Nhị diện 0°-180°, góc 2 mặt phẳng 0°-90° (lấy bù nếu >90°) | Bước 3 |
| 5. Ứng dụng | Kinh độ = góc nhị diện giữa 2 mặt kinh tuyến | Bước 4 |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: Bước 1 (xoay mặt (Q) quanh trục Δ đứng) — dùng đúng PHẦN 2.7
   (05_threejs_engine.md), đã verify công thức ở Bài 23, KHÔNG dùng 2.6.
✅ An toàn: Bước 2 (kéo điểm O dọc Δ) — pattern
   `ConstrainedPoint.dragToward` PHẦN 2.2 đã có sẵn.
✅ An toàn: Bước 3 (2 thanh trượt độ xiên độc lập) — chỉ là biến đổi góc
   tuyến tính đơn giản, không cần pattern mới.
✅ An toàn: Bước 4 (mô hình Trái Đất, dựng 2 mặt kinh tuyến tĩnh) — dùng
   `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3) để tính/kiểm tra
   góc, đã verify.
```

---

> **Trạng thái:** Module 1 (Bài 25) đã có kịch bản đầy đủ 4 bước + Tổng
> hợp kiến thức, số liệu đã verify bằng Python (góc gấp giấy 60°, bẫy độ
> xiên 57,16°, kinh độ Đảo Trường Sa Lớn 111,92°). Module 2 (điều kiện & tính
> chất — vách kính phòng tắm), Module 3 (container/rubik warehouse),
> Module 4 (nhập vai sửa lỗi — độ dốc mái nhà), và Lab (mở rộng
> solid_library.html) sẽ ra kịch bản ở các phiên tiếp theo.
