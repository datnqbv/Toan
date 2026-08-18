# Module 2: Sơ đồ hình cây
### Bài 23 — Quy tắc đếm | Toán 10, Chương VIII | Chủ đề 47

---

**Mục tiêu:** Học sinh hiểu vì sao cần một công cụ liệt kê có hệ thống (sơ đồ hình cây), tự dựng được cây phân cấp đúng cấu trúc, và đếm số lá cây để ra số cách thực hiện công việc nhiều công đoạn.

**Sai lầm cần giải quyết:**
1. Vẽ thiếu nhánh — quên 1 vị hoặc 1 loại topping ở một nhánh nào đó.
2. Lặp nhánh — vẽ trùng 1 nhánh giống hệt 2 lần dưới cùng 1 nhánh cha.
3. Sai thứ tự phân cấp — đặt Topping ngang hàng Size (bỏ qua tầng Vị) thay vì lồng đúng bên trong từng nhánh Vị.

**Loại simulation:** Dự đoán trước khi thấy → khám phá bằng công cụ xây cây kéo-thả → tự đối chất qua đếm lá cây.

**Thời gian hoàn thành dự kiến:** ~9 phút.

**Dạy từ đầu hay tổng kết:** Dạy từ đầu, theo mạch Problem → khám phá → khái quát hoá.

---

## 🎬 Hook mở đầu

Dùng lại ảnh SVG minh hoạ quầy trà sữa đã thống nhất ở buổi trước (3 ly trà sữa vị khác nhau + hũ topping). Không cần ảnh thật cho module này.

**Lời thoại Athena tại hook:**
> "Quán trà sữa gần trường có 2 size (M, L), 3 vị trà (Trà đen, Matcha, Sữa tươi), và 2 loại topping (Trân châu đen, Trân châu trắng). Bạn nghĩ có thể pha ra bao nhiêu ly trà sữa khác nhau?"

---

## Số liệu cụ thể (đã kiểm chứng, khác SGK)

- Size: 2 lựa chọn (M, L)
- Vị trà: 3 lựa chọn (Trà đen, Matcha, Sữa tươi)
- Topping: 2 lựa chọn (Trân châu đen, Trân châu trắng)
- Cấu trúc cây: mỗi Size → 3 nhánh Vị → mỗi Vị → 2 nhánh Topping
- Tổng số lá cây (đáp án đúng): 2 × 3 × 2 = **12**

---

## 🖼️ Phác thảo canvas — Công cụ "Xây cây"

**Bố cục canvas:**
- 1 node **Gốc** ở trên cùng, chính giữa: hình chữ nhật bo góc, nhãn "Pha 1 ly trà sữa".
- Bên dưới Gốc: 2 **ô trống nét đứt** (dashed placeholder), mỗi ô có dấu "+" ở giữa — đây là nơi học sinh kéo chip Size vào.
- Sau khi 1 ô Size được điền (VD "M"), dưới node đó tự sinh thêm 3 ô trống nét đứt mới (chờ điền Vị).
- Sau khi 1 ô Vị được điền (VD "Trà đen"), dưới node đó tự sinh thêm 2 ô trống nét đứt mới (chờ điền Topping).
- Node ở tầng cuối (đã điền Topping) không sinh thêm ô trống — đây chính là **lá cây**.

**Khay chip (chip tray) cố định phía dưới canvas:**
- 7 chip có thể kéo nhiều lần không giới hạn (vì cùng 1 lựa chọn được dùng lặp lại ở nhiều nhánh cha khác nhau): `M` `L` `Trà đen` `Matcha` `Sữa tươi` `Trân châu đen` `Trân châu trắng`.
- **Không tô màu phân loại theo nhóm Size/Vị/Topping** — cố ý để chip trung tính (chỉ có chữ), buộc học sinh tự suy luận đúng vị trí dựa trên đề bài, không dựa vào màu sắc gợi ý.
- Trên mobile: khay chip cuộn ngang bên dưới canvas (canvas cuộn dọc/pinch-zoom phía trên).

**Cơ chế kéo-thả (không chặn, không tự sửa lỗi hộ):**
- Học sinh kéo bất kỳ chip nào vào bất kỳ ô trống nào — hệ thống **luôn chấp nhận**, không chặn dù đặt sai vị trí (VD kéo "Trân châu đen" vào ô Size). Đây là chủ đích: để lỗi tự lộ ra khi đếm lá cây ở Bước 4, không chặn ngay từ đầu.
- Nếu học sinh kéo trùng 1 chip vào 2 ô cùng cấp dưới cùng 1 cha (VD 2 ô Vị dưới cùng 1 Size đều là "Trà đen"): hệ thống vẫn chấp nhận, không cảnh báo.
- Học sinh có thể xoá 1 nhánh đã điền (nút "×" nhỏ góc node) để làm lại.
- Node đã điền hiện đường nối (line, không mũi tên) tới node cha.

---

## Học sinh tương tác bằng cách

0. Xem hook + đọc câu hỏi Athena.
1. Dự đoán số cách pha 1 ly trà sữa (nhập số), CHƯA thấy công cụ cây.
2. Thử liệt kê thủ công bằng cách gõ ra vài cách (ô text tự do), tự nhận ra dễ sót/dễ trùng.
3. Dùng công cụ xây cây kéo-thả để dựng đầy đủ cấu trúc 3 tầng.
4. Bấm "Đếm lá cây" — hệ thống highlight toàn bộ node tầng cuối (lá) và đếm tổng.
5. So sánh với dự đoán ở Bước 1, nhập lại đáp án đúng.
6. Đọc Athena khái quát hoá vai trò sơ đồ hình cây.
7. *(Mở rộng, không bắt buộc)* Dựng cây cho 1 tình huống mới.

### Trước mỗi bước tương tác

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | "Bạn hãy đoán xem quán có thể pha ra bao nhiêu ly trà sữa khác nhau, rồi nhấn Kiểm tra." | (không cần — chỉ là dự đoán trực giác) |
| 2 | "Bạn hãy thử liệt kê ra một vài cách pha cụ thể, gõ mỗi cách trên 1 dòng." | (không cần — mục đích để tự thấy khó liệt kê hết) |
| 3 | "Bạn hãy kéo các chip bên dưới vào đúng vị trí trên cây: bắt đầu từ Size, tiếp đến Vị, cuối cùng là Topping." | Mỗi nhánh cha cần đủ số nhánh con theo đúng số lựa chọn ở công đoạn đó. |
| 4 | "Khi dựng cây xong, nhấn nút Đếm lá cây để hệ thống highlight và đếm giúp bạn." | Số lá cây chính là số cách thực hiện toàn bộ công việc. |
| 5 | "So sánh số lá cây vừa đếm được với dự đoán ban đầu của bạn, rồi nhập lại đáp án đúng." | Nếu 2 số không khớp, cây bạn dựng có thể thiếu nhánh, lặp nhánh, hoặc sai tầng. |

---

## Kịch bản dẫn dắt học sinh gặp sai lầm

**Bước 1 — dự đoán:**
> Athena: "Bạn dự đoán là [số học sinh nhập]. Mình chưa nói đúng hay sai vội — thử liệt kê ra vài cách cụ thể xem sao."

**Bước 2 — liệt kê thủ công:**
> Athena (sau khi học sinh gõ vài dòng): "Bạn đã liệt kê được [n] cách. Nếu liệt kê hết bằng tay như vậy, bạn có chắc không bị sót hay viết trùng cách nào không? Mình có 1 công cụ giúp liệt kê không sót, không trùng — gọi là sơ đồ hình cây."

**Bước 3 — xây cây (không chặn lỗi):** học sinh tự do kéo chip, có thể mắc 1 trong 3 lỗi. Hệ thống không phản hồi gì trong lúc dựng, chỉ chờ đến Bước 4.

**Bước 4 — đếm lá cây, hệ thống tự chẩn đoán loại lỗi (ẩn, dùng để chọn đúng gợi ý ở Bước 5):**
- Nếu tổng lá < 12 và có nhánh cha thiếu con so với các nhánh cha cùng cấp khác → nghi vấn *thiếu nhánh*.
- Nếu tổng lá > 12 và có 2 node con trùng nhãn dưới cùng 1 cha → nghi vấn *lặp nhánh*.
- Nếu có nhánh có độ sâu khác các nhánh còn lại (VD chỉ 2 tầng thay vì 3) → nghi vấn *sai thứ tự phân cấp*.

**Bước 5 — nhập lại đáp án, 3-strike với gợi ý theo đúng loại lỗi phát hiện được:**
- **Lần sai 1:** ô input rung nhẹ, không gợi ý.
- **Lần sai 2:** Athena đưa đúng 1 trong 3 gợi ý sau tuỳ loại lỗi hệ thống chẩn đoán:
  - Thiếu nhánh: *"Bạn thử kiểm tra: mỗi nhánh Size đã có đủ 3 vị trà chưa?"*
  - Lặp nhánh: *"Bạn thử xem: có nhánh nào bị lặp lại y hệt dưới cùng 1 nhánh cha không?"*
  - Sai thứ tự phân cấp: *"Bạn thử xem: Topping có đang được đặt ngay dưới Size, bỏ qua bước chọn Vị không?"*
- **Lần sai 3:** hiện đáp án đúng kèm giải thích: *"Đáp án đúng là 12. Với 2 size, mỗi size có 3 vị, mỗi vị lại có 2 topping, cây đúng phải có 2 × 3 × 2 = 12 lá — nghĩa là 12 cách pha khác nhau."*
- **Trả lời đúng:** *"Chính xác! Sơ đồ hình cây giúp bạn liệt kê đủ, không sót, không trùng — chỉ cần đếm số lá là ra đáp án."*

---

## Bước 6 — Athena khái quát hoá

> Athena: "Sơ đồ hình cây là cách vẽ ra tất cả các lựa chọn theo từng công đoạn, để không bỏ sót và không đếm trùng. Số lá cây chính là số cách thực hiện toàn bộ công việc. Ở bài lớp học lúc trước, bạn đã học quy tắc cộng khi có phần chung giữa 2 nhóm — còn ở đây, mỗi nhánh trong cây là một lựa chọn hoàn toàn tách biệt, nên chỉ cần đếm lá là đủ, không cần trừ phần chung nào cả."

Sổ tay kiến thức nền tảng: Không có — module này đang giới thiệu công cụ mới (sơ đồ hình cây), chưa cần công thức nào từ trước.

## Bước 7 — Mở rộng (không bắt buộc)

Tình huống mới: 1 tiệm bánh có 2 loại đế bánh (đế giòn, đế mềm), mỗi đế có 2 loại nhân (socola, dâu) — dựng cây và đếm lá (đáp án 4). Không chặn hoàn thành module nếu bỏ qua.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Canvas cây chiếm phần trên (~70% chiều cao), khay chip cố định ngay bên dưới canvas, khung thoại Athena + ô nhập đáp án đặt bên phải dạng panel cố định.

**Mobile (≤767px):** Canvas cây hiện trước (cho phép cuộn ngang/pinch-zoom nếu cây rộng hơn màn hình), khay chip cuộn ngang ngay bên dưới canvas, khung thoại Athena + ô nhập đáp án xuống cuối cùng.

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`

```javascript
structure: [
  { id: 'm2_du_doan',       type: 'answered', required: true },
  { id: 'm2_liet_ke_tay',   type: 'explored', required: true },
  { id: 'm2_xay_cay',       type: 'explored', required: true },
  { id: 'm2_dem_la_cay',    type: 'explored', required: true },
  { id: 'm2_dap_an_dung',   type: 'answered', required: true },
  { id: 'm2_mo_rong',       type: 'answered', required: false }
]
```

`progress total = 5` (không tính `m2_mo_rong`).

### Sự kiện LMS theo từng bước

| Bước | Sự kiện | Ghi chú |
|---|---|---|
| 1 | `LMS().event('answered', {id: 'm2_du_doan', value})` | Dự đoán ban đầu, vẫn ghi nhận dù sai |
| 2 | `LMS().event('explored', {id: 'm2_liet_ke_tay', trial})` | Liệt kê tự do, không chấm điểm |
| 3 | `LMS().event('explored', {id: 'm2_xay_cay', trial})` | Kéo-thả xây cây, không chấm điểm từng thao tác |
| 4 | `LMS().event('explored', {id: 'm2_dem_la_cay', trial})` | Bấm đếm lá cây — vẫn là khám phá vì có thể bấm lại sau khi sửa cây |
| 5 | `LMS().event('answered', {id: 'm2_dap_an_dung', tries})` | Đáp án cuối cùng, tối đa 3 lần thử |
| 7 | `LMS().event('answered', {id: 'm2_mo_rong', required:false})` | Không chặn `LMS().complete()` |

`LMS().complete()` gọi ngay sau khi Bước 5 đạt đúng.

### `athenaGuidance` (nguyên văn, khớp đúng 5 mục bắt buộc)

```
1. m2_du_doan: nếu học sinh hỏi gợi ý, Athena chỉ hỏi ngược: "Bạn thử
   nghĩ xem, có bao nhiêu lựa chọn ở mỗi công đoạn?" — KHÔNG nói trước
   đáp án 12.
2. m2_liet_ke_tay: Athena chỉ hỏi: "Bạn có chắc đã liệt kê hết và không
   trùng cách nào chưa?" — không liệt kê hộ học sinh.
3. m2_xay_cay: Athena chỉ nhắc quy trình: "Bắt đầu từ Size, tiếp đến
   Vị, cuối cùng là Topping." — không chỉ ra vị trí kéo cụ thể.
4. m2_dem_la_cay: Athena chỉ xác nhận đã đếm xong, không nói cây đúng
   hay sai ở bước này.
5. m2_dap_an_dung: gợi ý lần sai thứ 2 CHỈ dùng đúng 1 trong 3 câu đã
   định nghĩa ở mục "Kịch bản dẫn dắt sai lầm" (tuỳ loại lỗi hệ thống
   chẩn đoán) — không được gộp cả 3 gợi ý cùng lúc, không nói thẳng
   đáp án 12 ở gợi ý này.
```

---

## Tổng kết kiến thức

> **Sơ đồ hình cây** là công cụ liệt kê có hệ thống các khả năng của một công việc gồm nhiều công đoạn liên tiếp: mỗi công đoạn là 1 tầng của cây, mỗi lựa chọn ở công đoạn đó là 1 nhánh. **Số lá cây (nhánh tận cùng) chính là tổng số cách thực hiện toàn bộ công việc.**
>
> ⚠️ Khi dựng cây, mỗi nhánh cha cùng cấp phải có đủ và không lặp số nhánh con giống các nhánh cha khác — thiếu, lặp, hoặc đặt sai tầng đều dẫn đến đếm sai số lá.
