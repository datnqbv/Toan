# Ước tính số lượng bằng phương pháp mẫu — Quần thể rùa biển & Pha loãng đồng vị
### Thay thế "Ước tính số cá thể trong một quần thể" | Toán 10, cuối năm

---

**Vị trí trong chương trình:** Giữ nguyên quy trình toán học của SGK (phương pháp đánh dấu - bắt lại, công thức N ≈ M·n/k, đánh giá sai số), gồm 2 phần: **Phần 1** đổi loài (rùa biển thay cho cá/hạt lạc trong SGK, vẫn đúng phương pháp đánh dấu-bắt lại gốc); **Phần 2** mở rộng sang ứng dụng thật trong ngành hạt nhân/hoá phóng xạ — **phương pháp pha loãng đồng vị (isotope dilution analysis)**.

**Mục tiêu:** Học sinh hiểu và áp dụng công thức ước tính N ≈ M·n/k trong nhiều bối cảnh khác nhau, đánh giá sai số tuyệt đối/tương đối, và nhận ra quy luật sai số giảm khi cỡ mẫu tăng — đây là 1 nguyên lí chung, không riêng cho sinh học hay hoá học.

**Loại simulation:** Step-by-step có hướng dẫn (thực hiện quy trình) + khám phá (lặp lại với cỡ mẫu khác nhau để tự thấy quy luật sai số).

**Thời gian hoàn thành dự kiến:** ~18 phút (cả 2 phần).

**Dạy từ đầu hay tổng kết:** Dạy từ đầu — công thức xác suất cổ điển đã học ở Bài 26, nhưng ỨNG DỤNG "đánh dấu-bắt lại" và "pha loãng đồng vị" là nội dung mới.

---

## Sổ tay kiến thức nền tảng

```
- Xác suất cổ điển (Bài 26): P(A) = n(E)/n(Ω).
- Phương pháp đánh dấu - bắt lại / pha loãng: thêm hoặc đánh dấu M (số
  lượng/khối lượng đã biết), trộn đều hoặc chờ phân bố lại vào quần thể/
  môi trường, sau đó lấy mẫu n, đếm/đo được số lượng đã đánh dấu k có
  trong mẫu đó.
  → N ≈ M · n / k
- Sai số tuyệt đối = |N thật − N ước tính|.
  Sai số tương đối = Sai số tuyệt đối / N thật (thường tính theo %).
```

---

## Phần 1 — Ước tính quần thể rùa biển

### 🎨 Style guide chung cho ảnh Phần 1

```
Flat-realistic illustration (KHÔNG phải ảnh chụp thật) — minh hoạ vector
phẳng, hình khối đơn giản, không đổ bóng/gradient phức tạp. Bảng màu:
nền Cream (#FAF7F0)/Cream 2 (#F0EADD); nước biển Dusty blue (#6E93A6);
rùa biển Olive (#8A9A5B)/Forest (#2E6B52); cát Sand (#D8C4A0); viền nét
mảnh Ink (#1A1A1A).
```

### 🎬 Ảnh hook mở đầu Phần 1 — prompt tạo ảnh

```
A flat-realistic vector illustration of a sea turtle conservation research
scene: a simplified sea turtle shape in Forest (#2E6B52)/Olive (#8A9A5B)
swimming in flat Dusty blue (#6E93A6) water near a Sand (#D8C4A0) beach
shore, with a small flat clipboard shape and a simple tag/marker shape in
Accent (#E8A24A) nearby suggesting a tagging research activity. Clean flat
shapes, thin Ink (#1A1A1A) outlines, no gradients or shadows, calm and
scientific mood. Aspect ratio 16:9, no legible text, no human faces (a
researcher can appear only as a simple flat silhouette from behind).
```

**Athena:** *"Một nhóm nghiên cứu sinh vật biển muốn ước tính số lượng rùa biển đang sinh sống trong 1 vịnh nhỏ, mà không thể đếm hết từng con. Họ dùng đúng phương pháp đánh dấu - bắt lại đã học: bắt 1 số con, đánh dấu, thả lại, rồi sau đó bắt lại 1 mẫu khác để suy ra tổng số."*

### 🖼️ Phác thảo canvas — Mô phỏng vịnh biển

- **Canvas chính:** hình 1 vịnh biển nhìn từ trên xuống (top-down), rải rác các hình rùa biển nhỏ (icon phẳng) di chuyển chậm (animation nhẹ, không cần vật lý phức tạp).
- **Bước đánh dấu:** học sinh bấm "Bắt & đánh dấu 40 con" — 40 hình rùa trong vịnh đổi màu (thêm chấm cam nhỏ trên mai), rồi "Thả lại" — rùa đã đánh dấu trộn lẫn ngẫu nhiên vào vịnh.
- **Bước bắt lại:** bấm "Bắt mẫu 60 con" — hệ thống chọn ngẫu nhiên 60 hình rùa trong vịnh, đếm số có chấm cam (k), hiện kết quả.
- **Kết quả:** ô nhập N̂, sau khi đúng thì hiện công thức đầy đủ N̂ = M·n/k.

### Hoạt động 1 — Thực hiện quy trình ước tính

**Athena:** *"Nhóm nghiên cứu bắt và đánh dấu 40 con rùa, thả lại vào vịnh. Sau đó bắt lại 1 mẫu 60 con, thấy trong đó có 8 con đã có dấu. Hãy ước tính tổng số rùa biển trong vịnh."*

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | "Bấm 'Bắt & đánh dấu 40 con' rồi 'Thả lại' trên canvas." | Rùa đã đánh dấu cần thời gian trộn lẫn tự nhiên vào quần thể trước khi bắt lại — nếu bắt lại ngay, tỉ lệ sẽ không đại diện. |
| 2 | "Bấm 'Bắt mẫu 60 con', đọc số liệu k = 8 con có dấu." | Mẫu bắt lại nên đủ lớn để tỉ lệ trong mẫu phản ánh đúng tỉ lệ toàn vịnh. |
| 3 | "Nhập công thức và tính N̂." | N ≈ M · n / k = 40 × 60 / 8. |

- Đáp án: N̂ = 40×60/8 = 300 (con).
- 3-strike: lần sai 2 gợi ý — *"Công thức là N ≈ M·n/k — bạn đã thay đúng M=40, n=60, k=8 chưa?"*

### Hoạt động 2 — Đánh giá sai số khi cỡ mẫu thay đổi

**Athena:** *"Giả sử số rùa thật trong vịnh (đã được kiểm định bằng phương pháp khác, VD gắn thiết bị định vị theo dõi lâu dài) là 300 con. Nhóm nghiên cứu lặp lại quy trình 3 lần với cỡ mẫu bắt lại khác nhau. Hãy hoàn thành bảng sau."*

| Lần | n (con bắt lại) | k (con có dấu) | N̂ | Sai số tuyệt đối | Sai số tương đối |
|---|---|---|---|---|---|
| 1 | 30 | 5 | ? | ? | ? |
| 2 | 90 | 11 | ? | ? | ? |
| 3 | 150 | 19 | ? | ? | ? |

**Đáp án (đã kiểm chứng bằng code):**

| Lần | N̂ (con) | Sai số tuyệt đối | Sai số tương đối |
|---|---|---|---|
| 1 | 240,0 | 60,0 | 20,00% |
| 2 | 327,3 | 27,3 | 9,09% |
| 3 | 315,8 | 15,8 | 5,26% |

**Câu hỏi nhận xét:** *"Bạn nhận xét gì về sai số khi cỡ mẫu bắt lại tăng dần?"* → Athena xác nhận: *"Cỡ mẫu càng lớn, ước tính càng ổn định, sai số càng có xu hướng giảm — đây là quy luật chung của mọi phương pháp ước tính bằng mẫu."*

---

## Phần 2 — Ước tính khối lượng chất phóng xạ (pha loãng đồng vị)

### 🎬 Ảnh hook mở đầu Phần 2 — prompt tạo ảnh (flat-realistic illustration, không phải ảnh chụp)

```
Style guide: flat-realistic illustration (KHÔNG phải ảnh chụp thật) —
minh hoạ vector phẳng, hình khối đơn giản, không đổ bóng/gradient phức
tạp, phong cách sách giáo khoa hiện đại. Bảng màu bắt buộc: nền Cream
(#FAF7F0)/Cream 2 (#F0EADD); màu chủ đạo Jade (#3CA57A), Dusty blue
(#6E93A6), Slate (#4E6E7E); vật thể minh hoạ Sage (#A8C9B8), Ochre
(#C99A3C); viền nét mảnh Ink (#1A1A1A).
```

```
A flat-realistic vector illustration of a nuclear safety laboratory
interior: a simple flat figure shape (visible only from behind/side, no
face) wearing a Cream (#FAF7F0) lab coat, standing at a workbench shape in
Slate (#4E6E7E) with simplified scientific equipment shapes — a small
sample vial shape in Jade (#3CA57A), a radiation detector device shape in
Dusty blue (#6E93A6) with a flat abstract display (no legible
numbers/text). Clean flat Cream/Sage (#A8C9B8) color palette, thin Ink
(#1A1A1A) outlines, no gradients or shadows. Professional and calm mood
(not alarming or dramatic), no warning symbols or hazard signage in
close-up focus. Aspect ratio 16:9.

Avoid: any legible text/numbers on displays, any visible faces, any
dramatic or frightening mood — this should feel calm and professional,
like routine lab work; no 3D shading or photorealistic textures.
```

**Athena:** *"Vừa rồi bạn ước tính số lượng cá thể sống bằng cách đánh dấu-bắt lại. Cùng công thức đó còn dùng được cho vật chất không sống: 1 bể chứa chất thải phóng xạ tại nhà máy điện hạt nhân cần được ước tính khối lượng chất còn lại, để tính khối lượng an toàn xử lý. Kỹ thuật viên dùng phương pháp pha loãng đồng vị — thêm vào 1 lượng nhỏ chất đánh dấu đã biết chính xác khối lượng, rồi suy ra tổng khối lượng."*

### 🖼️ Phác thảo canvas — Mô phỏng bể chứa

- **Canvas chính:** hình 1 bể chứa hình trụ (nhìn từ trên xuống hoặc mặt cắt bên), có hiệu ứng "khuấy đều" (animation xoáy nhẹ) khi học sinh bấm "Thêm chất đánh dấu".
- **Bước thêm chất đánh dấu:** hiện icon nhỏ (giọt màu Jade) rơi vào bể, số "M = 50g" hiện rõ cạnh bể.
- **Bước lấy mẫu:** 1 ống nghiệm nhỏ animation "hút" 1 phần từ bể ra, hiện số "n = ...g" (khối lượng mẫu).
- **Bước đo:** hiện máy đo với số "k = ...g" (khối lượng chất đánh dấu đo được trong mẫu) — đây là số liệu đề cho, không phải học sinh tự đo.
- **Kết quả:** ô nhập N̂, sau khi đúng thì hiện công thức đầy đủ N̂ = M·n/k.

### Hoạt động 1 — Thực hiện quy trình ước tính

**Athena:** *"Kỹ thuật viên thêm 50g chất đánh dấu vào bể, khuấy đều. Sau đó lấy ra 1 mẫu 200g, đo được trong mẫu đó có 3,9g chất đánh dấu. Hãy ước tính tổng khối lượng chất trong bể."*

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | "Bấm 'Thêm chất đánh dấu' rồi 'Khuấy đều' trên canvas." | Chất đánh dấu phải phân bố đồng đều trong toàn bể trước khi lấy mẫu — nếu không, tỉ lệ trong mẫu sẽ không đại diện cho tỉ lệ toàn bể. |
| 2 | "Bấm 'Lấy mẫu 200g', đọc số liệu k = 3,9g hiện ra." | Mẫu phải đủ nhỏ so với bể (không làm thay đổi đáng kể tổng khối lượng còn lại). |
| 3 | "Nhập công thức và tính N̂." | N ≈ M · n / k = 50 × 200 / 3,9. |

- Đáp án: N̂ = 50×200/3,9 ≈ 2564,1 (g).
- 3-strike: lần sai 2 gợi ý — *"Công thức là N ≈ M·n/k — bạn đã thay đúng M=50, n=200, k=3,9 chưa?"*

### Hoạt động 2 — Đánh giá sai số khi cỡ mẫu thay đổi

**Athena:** *"Giả sử khối lượng thật của bể (đã được kiểm định bằng phương pháp khác) là 2600g. Kỹ thuật viên lặp lại quy trình 3 lần với cỡ mẫu khác nhau. Hãy hoàn thành bảng sau."*

| Lần | n (g) | k (g) | N̂ (g) | Sai số tuyệt đối | Sai số tương đối |
|---|---|---|---|---|---|
| 1 | 80 | 1,6 | ? | ? | ? |
| 2 | 200 | 3,9 | ? | ? | ? |
| 3 | 400 | 7,7 | ? | ? | ? |

**Đáp án (đã kiểm chứng bằng code):**

| Lần | N̂ (g) | Sai số tuyệt đối | Sai số tương đối |
|---|---|---|---|
| 1 | 2500,0 | 100,0 | 3,85% |
| 2 | 2564,1 | 35,9 | 1,38% |
| 3 | 2597,4 | 2,6 | 0,10% |

**Câu hỏi nhận xét (không chấm điểm nghiêm ngặt, chỉ 1 lần thử + giải thích ngay):** *"Bạn nhận xét gì về sai số khi cỡ mẫu n tăng dần?"* → Athena xác nhận: *"Cỡ mẫu càng lớn, ước tính càng chính xác, sai số càng nhỏ — đúng quy luật bạn đã thấy ở Phần 1 với rùa biển. Đây là nguyên lí chung của mọi phương pháp ước tính bằng mẫu, dù áp dụng cho sinh vật sống hay chất vô tri."*

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Mỗi Phần 1 khối full-width. Canvas (vịnh biển / bể chứa) đặt bên trái ~60%, khung thoại + bảng số liệu bên phải ~40%.

**Mobile (≤767px):** Canvas hiện trước, bảng số liệu Hoạt động 2 cho phép cuộn ngang nếu cần (5 cột hơi nhiều cho màn hình hẹp), vùng chạm các nút ≥44px. Không cần pattern lướt ngang toàn trang vì mỗi Phần tự chứa canvas riêng.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Bắt & đánh dấu / thả lại / bắt mẫu (Phần 1) | Click nút | Chạm nút ≥44px |
| Thêm chất đánh dấu / khuấy đều / lấy mẫu (Phần 2) | Click nút | Chạm nút ≥44px |
| Nhập kết quả tính toán | Gõ bàn phím, click Kiểm tra | Chạm ô input `inputmode="decimal"`, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'p1_hd1_quy_trinh',   type: 'answered', required: true },
  { id: 'p1_hd2_bang_saiso',  type: 'answered', required: true },
  { id: 'p1_hd2_nhan_xet',    type: 'explored',  required: true },
  { id: 'p2_hd1_quy_trinh',   type: 'answered', required: true },
  { id: 'p2_hd2_bang_saiso',  type: 'answered', required: true },
  { id: 'p2_hd2_nhan_xet',    type: 'explored',  required: true }
]
```
`progress total = 6`.

### `athenaGuidance`
```
1. p1_hd1_quy_trinh: gợi ý lần sai thứ 2 CHỈ dùng đúng câu "Công thức là
   N ≈ M·n/k — bạn đã thay đúng M=40, n=60, k=8 chưa?" — không tính hộ
   đáp án 300.
2. p1_hd2_bang_saiso: gợi ý tương tự cho từng ô còn thiếu trong bảng.
3. p1_hd2_nhan_xet: giải thích đầy đủ ngay sau khi học sinh trả lời.
4. p2_hd1_quy_trinh: gợi ý lần sai thứ 2 CHỈ dùng đúng câu "Công thức là
   N ≈ M·n/k — bạn đã thay đúng M=50, n=200, k=3,9 chưa?" — không tính
   hộ đáp án 2564,1.
5. p2_hd2_bang_saiso: gợi ý tương tự cho từng ô còn thiếu trong bảng.
6. p2_hd2_nhan_xet: giải thích đầy đủ ngay sau khi học sinh trả lời, có
   thể liên hệ ngược lại Phần 1 (rùa biển) nếu học sinh hỏi thêm.
```

---

## Tổng kết kiến thức

> **Phương pháp đánh dấu - bắt lại / pha loãng:** để ước tính tổng số lượng N (số cá thể sống, hoặc khối lượng 1 chất) khi không thể đo/đếm trực tiếp toàn bộ, thêm hoặc đánh dấu 1 lượng M đã biết, để phân bố đều vào quần thể/môi trường, sau đó lấy mẫu n, đếm/đo số lượng đã đánh dấu k có trong mẫu, rồi tính **N ≈ M · n / k**.
>
> **Sai số tuyệt đối** = |N thật − N ước tính|; **sai số tương đối** = sai số tuyệt đối / N thật. Cỡ mẫu n càng lớn, ước tính càng chính xác — sai số giảm dần. Đây là nguyên lí chung của mọi phương pháp ước tính bằng mẫu, được ứng dụng rộng rãi từ sinh học (ước tính quần thể động vật như rùa biển) đến hoá học hạt nhân (ước tính khối lượng chất phóng xạ) và y học (đo thể tích máu).
