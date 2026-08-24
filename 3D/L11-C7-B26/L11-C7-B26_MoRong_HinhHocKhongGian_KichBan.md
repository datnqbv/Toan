# 📚 KỊCH BẢN — Module mở rộng (Bài 22-26): "Hình học không gian trong đời sống, kỹ thuật và vũ trụ"
## (Bản v2 — có spec minh hoạ SVG + responsive mobile)

```
📌 KHÔNG thuộc PPCT — module ĐỌC THÊM/KHÁM PHÁ.
🎯 Định dạng: NHẸ — mỗi nhánh: (1) minh hoạ SVG, (2) đọc ngắn, (3) mô hình
   3D xoay được, (4) 1-2 câu hỏi khám phá MỞ (không chấm điểm gắt).
📁 File: MoRong_HinhHocKhongGian_DoiSongKyThuatVuTru.html
```

> ⚠️ **Vì sao chọn mô tả vẽ SVG, không dùng prompt ảnh AI:** hệ thống dùng
> illustration phẳng theo token màu cố định (`--il-*`, xem PHẦN 1 dưới),
> không dùng ảnh chụp/AI-generated — chèn ảnh thật (đặc biệt Kim tự tháp,
> Tháp Pisa, Capital Gate) sẽ lệch phong cách + rủi ro bản quyền ảnh thật.
> Mọi minh hoạ dưới đây vẽ bằng path/shape cơ bản, đúng token màu đã có.

---

## PHẦN 1 — Design tokens dùng trong module này (trích từ hệ thống, không thêm màu mới)

```css
/* Neutrals */
--cream:#FAF7F0; --cream-2:#F0EADD; --paper-line:#E5DECF;
--ink:#1A1A1A; --ink-2:#514C44; --ink-3:#7C756A;
/* Jade — hành động chính, dùng cho label/nút/highlight tương tác */
--jade:#3CA57A; --jade-text:#1B5E48; --jade-pale:#DCEAE1;
/* Accent — điểm nhấn ấm, dùng cho tia sáng/điểm nhấn nhỏ */
--accent:#E8A24A; --accent-pale:#F7E7CD;
/* Illustration ONLY — CHỈ dùng cho hình vẽ minh hoạ, KHÔNG dùng cho UI/text */
--il-terracotta:#C1704B; --il-ochre:#C99A3C; --il-olive:#8A9A5B;
--il-forest:#2E6B52; --il-dusty-blue:#6E93A6; --il-slate:#4E6E7E; --il-sand:#D8C4A0;
```

**Quy tắc vẽ (đúng nguyên tắc PHẦN 7, `03_game_engine_toan.md`):**
- 1 màu = 1 nghĩa cố định, dùng lặp lại xuyên suốt cả 7 tab (không đổi
  nghĩa màu giữa các tab).
- Mỗi minh hoạ chỉ 1 điểm nhấn chính (focal point), phần còn lại vẽ nhạt/
  đơn giản hơn.
- KHÔNG dùng gradient, KHÔNG dùng emoji trong SVG — vẽ path/shape thuần.
- Nét viền: `stroke: var(--ink)`, `stroke-width: 1.5-2px`, các mảng màu
  đặc 1 lớp (fill phẳng).

---

## TAB 1 — Lịch sử đo đạc: từ dây dọi đến laser level

### Minh hoạ SVG (viewBox 0 0 600 280, bố cục chia 2 nửa + mũi tên nối)

```
Nửa trái (x: 0-280) — "Ngày xưa":
- Tam giác kim tự tháp: fill=--il-ochre, stroke=--ink, đỉnh (140,40),
  đáy (60,240)-(220,240).
- 1 silhouette người thợ nhỏ (hình que đơn giản: đầu tròn r=8 + thân
  1 đường + 2 chân) đứng cạnh đáy kim tự tháp, tay cầm 1 đường thẳng
  mảnh (dây dọi) buông xuống, đầu dây có 1 chấm tròn nhỏ (quả nặng,
  fill=--ink) — đường dây dọi màu --ink-2, nét đứt nhẹ để phân biệt
  với cạnh kim tự tháp.
- Label nhỏ dưới: "~2500 TCN" (font nhỏ, --ink-3).

Nửa phải (x: 320-600) — "Ngày nay":
- 1 hình hộp nhỏ (thiết bị laser level): fill=--il-slate, kích thước
  60x40, đặt trên 1 chân 3 chạc đơn giản (3 đường thẳng mảnh).
- 2 tia sáng ngang phát ra từ hộp: 2 đường thẳng màu --jade, có thêm
  hiệu ứng "tia" bằng 3-4 đoạn ngắn song song mờ dần (opacity giảm dần
  theo khoảng cách) để gợi cảm giác ánh sáng.
- 1 dấu ✓ nhỏ (vẽ path, KHÔNG dùng ký tự Unicode) màu --jade cạnh tia
  sáng, biểu thị "đã xác định đúng phương ngang/đứng".
- Label nhỏ dưới: "Hiện đại".

Giữa 2 nửa: 1 mũi tên cong nhẹ (path Bezier), màu --ink-3, nét mảnh,
đi từ nửa trái sang nửa phải, gợi ý "dòng thời gian".

Nền toàn khung: --cream, có thể thêm lưới paper-line rất mờ (opacity
0.15) theo đúng `drawSchematicBg` đã dùng ở game engine 2D.
```

### Đọc & Mô hình 3D & Câu hỏi khám phá — giữ nguyên nội dung bản v1

*(Đọc, mô hình 3D kim tự tháp Khufu + dây dọi ảo xoay được, câu hỏi khám
phá về ảo giác góc nhìn — không đổi so với bản trước.)*

---

## TAB 2 — Thiên văn định hướng: hệ toạ độ chân trời

### Minh hoạ SVG (viewBox 0 0 600 300)

```
- Nền trời: --cream (KHÔNG tô đen kịt — giữ tinh thần schematic phẳng,
  không kịch tính hoá "bầu trời đêm").
- Đường chân trời: 1 đường ngang tại y=220, màu --paper-line, dày 2px.
- Dải đất/biển dưới chân trời: fill=--cream-2, từ y=220 xuống đáy.
- 3-4 chấm sao: chấm tròn nhỏ r=3-4, fill=--accent, rải ngẫu nhiên phía
  trên đường chân trời (y: 40-200).
- 1 sextant (kính lục phân) cách điệu ở góc dưới trái: hình quạt 1/6
  vòng tròn (path arc), fill=--il-dusty-blue, có 1 kim chỉ mảnh từ tâm
  ra viền, màu --ink.
- Từ tâm sextant, 1 đường ngắm (nét đứt, --jade) nối tới 1 trong các
  sao — tại điểm giao với đường chân trời (kéo dài xuống), vẽ 1 cung
  góc nhỏ (arc, stroke=--accent) biểu thị "độ cao góc", kèm label số đo.
```

### Đọc & Mô hình 3D & Câu hỏi khám phá — giữ nguyên nội dung bản v1

---

## TAB 3 — Con quay hồi chuyển: giữ hướng trong không gian

### Minh hoạ SVG (viewBox 0 0 400 400, đối xứng tâm)

```
- 3 vòng elip lồng nhau (phối cảnh nhẹ, giống gimbal thật), tâm chung
  (200,200):
  - Vòng ngoài: rx=160, ry=60, stroke=--il-slate, stroke-width=4,
    fill=none.
  - Vòng giữa: rx=110, ry=90 (xoay 90° so với vòng ngoài — vẽ bằng
    transform rotate), stroke=--il-dusty-blue, stroke-width=4, fill=none.
  - Vòng trong: rx=70, ry=70 (gần tròn), stroke=--sage-deep,
    stroke-width=4, fill=none.
- 1 mũi tên/trục xuyên tâm theo 1 hướng cố định (VD chếch 20° so với
  trục đứng), màu --accent, đậm, có đầu mũi tên rõ ràng (path tam giác
  nhỏ ở 1 đầu).
- 2 mũi tên cong nhỏ (path arc + đầu mũi tên) quanh vòng NGOÀI và
  vòng GIỮA, màu --ink-3, biểu thị "2 lớp khung này xoay được tự do".
- KHÔNG vẽ mũi tên cong quanh trục accent ở giữa — nhấn mạnh trực quan
  "trục này KHÔNG xoay theo khung ngoài".
```

### Đọc & Mô hình 3D & Câu hỏi khám phá — giữ nguyên nội dung bản v1

---

## TAB 4 — Kiến trúc & bản vẽ kỹ thuật

### Minh hoạ SVG (viewBox 0 0 600 400)

```
- Khối nhà ở giữa (phối cảnh isometric nhẹ, giống style Object Library
  đã dùng ở game engine): thân hộp fill=--il-sand, mái tam giác
  fill=--il-terracotta, viền --ink.
- 3 mũi tên nét đứt (màu --jade-text) từ khối nhà chiếu ra 3 hướng:
  lên (tới màn "mặt bằng"), sang phải (tới màn "mặt đứng"), sang trái-
  xuống (tới màn "mặt cắt").
- 3 "màn chiếu" là 3 hình chữ nhật viền --ink, fill=--cream-2, đặt ở 3
  vị trí tương ứng đầu mũi tên — mỗi màn có 1 hình 2D đơn giản bên
  trong (nét mảnh --ink-2): mặt bằng = hình chữ nhật; mặt đứng = hình
  chữ nhật + tam giác nhỏ trên đỉnh (mái); mặt cắt = hình chữ nhật khác
  tỉ lệ.
```

### Đọc & Mô hình 3D & Câu hỏi khám phá — giữ nguyên nội dung bản v1

---

## TAB 5 — Công trình nghiêng: lỗi ngoài ý muốn vs chủ đích thiết kế

### Minh hoạ SVG (viewBox 0 0 500 350, 2 tháp cạnh nhau)

```
- Nền đất chung: 1 dải ngang fill=--cream-2 ở đáy.
- Tháp trái ("Pisa"): 1 hình trụ nghiêng nhẹ (~8° — vẽ bằng transform
  skew hoặc rotate toàn khối), fill=--il-terracotta, có 3-4 đường ngang
  mảnh (--ink-2) chia "tầng" cho giống tháp chuông thật, KHÔNG vẽ lõi
  bên trong (đặc, 1 khối duy nhất).
- Tháp phải ("Capital Gate"): 1 hình khối nghiêng NHIỀU hơn (~18°, rõ
  rệt hơn tháp trái), fill=--il-dusty-blue với opacity 0.55 (để thấy
  xuyên qua), BÊN TRONG vẽ 1 lõi thẳng đứng riêng (hình chữ nhật hẹp,
  fill=--il-forest, KHÔNG nghiêng theo khối ngoài) chạy từ đế lên gần
  đỉnh — đây là điểm nhấn chính của minh hoạ (đúng nguyên tắc "1 điểm
  nhấn/cảnh").
- Label số đo góc nghiêng dưới mỗi tháp (--ink-3, nhỏ): "~4°" / "18°".
```

### Đọc & Mô hình 3D & Câu hỏi khám phá — giữ nguyên nội dung bản v1

---

## TAB 6 — Tự nhiên & vuông góc: cây mọc theo trọng lực

### Minh hoạ SVG (viewBox 0 0 500 350)

```
- Sườn núi: 1 tam giác lớn nghiêng, fill=--il-olive, đáy tại y=320,
  đỉnh chếch sang 1 bên (dốc ~30°).
- 3 cây trên sườn núi (mỗi cây: 1 hình tam giác nhỏ màu --il-forest +
  1 thân chữ nhật hẹp màu --il-terracotta), đặt tại 3 vị trí khác nhau
  trên sườn dốc, TẤT CẢ ĐỀU THẲNG ĐỨNG (song song nhau, không xoay theo
  độ dốc của tam giác núi).
- 1 cây "đối chiếu" mờ (opacity 0.3, nét đứt viền --ink-3, không tô
  màu đặc) vẽ THÊM cạnh 1 cây thật, nghiêng theo ĐÚNG độ dốc mặt núi
  (vuông góc mặt dốc, sai với thực tế) — để học sinh so ngay trên hình
  tĩnh sự khác biệt giữa "vuông góc mặt dốc" (sai, mờ) và "thẳng đứng
  thật" (đúng, đậm).
- 1 đường chấm ngắn ở đáy tam giác núi biểu thị "mặt phẳng nằm ngang"
  làm mốc so sánh.
```

### Đọc & Mô hình 3D & Câu hỏi khám phá — giữ nguyên nội dung bản v1

---

## TAB 7 — Vì sao "đứng bóng" chỉ xảy ra trong vùng nội chí tuyến? (mới — Bài 26)

> **Mở rộng phạm vi module:** ban đầu module này gói Bài 22-24, nay bổ
> sung Tab 7 dựa trên "Em có biết" cuối Bài 26 — nối trực tiếp với Tab 2
> (thiên văn định hướng) và mô hình Trái Đất đã dựng ở Lab Bài 25, đồng
> thời dùng lại chính kỹ thuật "khoảng cách/góc so sánh" vừa học ở Bài
> 26. Phạm vi module giờ là **Bài 22-26**.

### Minh hoạ SVG (viewBox 0 0 600 320)

```
- Hình cầu Trái Đất cách điệu (fill=--il-dusty-blue nhạt), trục Bắc-Nam
  vẽ đậm (--ink) xuyên tâm.
- 2 đường chí tuyến (Bắc, Nam) — 2 vòng nhỏ ngang trên hình cầu, cách
  đều 2 bên xích đạo, tô màu --accent, có label "23,5°".
- Vùng NGOÀI 2 chí tuyến (2 chỏm cực) tô nhạt màu --il-slate, opacity
  0.35 — biểu thị "vùng KHÔNG BAO GIỜ đứng bóng thực sự".
- 1 tia sáng Mặt Trời (đường thẳng màu --il-ochre, có mũi tên) chiếu tới
  đúng 1 điểm P₀ trên đoạn nối tâm Trái Đất – tâm Mặt Trời (điểm duy
  nhất tại đó tia sáng vuông góc mặt đất tại 1 thời điểm).
- 1 điểm P khác (chấm --il-terracotta) đặt trong vùng chỏm cực (ngoài
  chí tuyến) — tia sáng tới P vẽ XIÊN (không vuông góc mặt đất tại P),
  đối lập trực quan với tia tới P₀.
```

### Đọc

"Vùng phía bắc chí tuyến Bắc và phía nam chí tuyến Nam KHÔNG BAO GIỜ có
hiện tượng 'đứng bóng thực sự' (tia nắng vuông góc mặt đất) — vì trục
Trái Đất luôn nghiêng với mặt phẳng quỹ đạo 1 góc ~66,5°, nên góc từ tâm
Trái Đất tới bất kỳ điểm nào ngoài chí tuyến (vĩ độ > 23,5°) luôn NHỎ HƠN
66,5° — mâu thuẫn với điều kiện cần để đứng bóng xảy ra tại đó."

### Mô hình 3D

Tái dùng chính mô hình "Trái Đất & Kinh tuyến" đã dựng ở Lab Bài 25
(PHẦN 2.12, `05_threejs_engine.md`) — bổ sung: 2 vòng chí tuyến (vẽ bằng
`createLatitudeCircle(R, 23.5, màu accent)` và `createLatitudeCircle(R,
-23.5, màu accent)` — TÁI DÙNG NGUYÊN hàm đã verify, không cần viết
thêm), và 1 điểm P kéo được dọc theo 1 kinh tuyến để học sinh tự thử các
vĩ độ khác nhau, quan sát góc tia sáng đổi từ "gần vuông góc" (trong nội
chí tuyến) sang "xiên hẳn" (ngoài chí tuyến).

### Câu hỏi khám phá

"Kéo điểm P dọc kinh tuyến từ xích đạo lên gần cực Bắc — tại vĩ độ nào
thì tia sáng KHÔNG BAO GIỜ vuông góc mặt đất được nữa, dù chọn bất kỳ
ngày nào trong năm?"
- *Gợi ý:* đúng tại vĩ độ 23,5° (chí tuyến Bắc) — qua khỏi đó là không
  còn khả năng đứng bóng thực sự nữa.

**Liên hệ:** Bài 24 Module 2 Phần 4 (Trái Đất nghiêng trục); Lab Bài 25
(mô hình kinh tuyến); Bài 26 (kỹ thuật so sánh góc/khoảng cách dùng
trong chứng minh).

---

## PHẦN 2 — Responsive: Desktop & Mobile (bắt buộc chốt ở đây)

### Desktop (≥1024px)

```
- Màn hình chọn: lưới thẻ (card grid) — 6 tab đầu xếp 3 cột × 2 dòng, Tab
  7 (mới) xếp riêng 1 dòng cuối full-width hoặc thêm vào ô còn trống nếu
  lưới đổi thành 4 cột × 2 dòng (tuỳ giáo viên chọn bố cục), mỗi thẻ = 1 tab,
  hiện thumbnail SVG rút gọn (chỉ phần minh hoạ, thu nhỏ) + tên nhánh.
- Click 1 thẻ → mở nội dung chi tiết trong khu vực chính bên phải HOẶC
  modal lớn (đề xuất: modal, vì nội dung mỗi tab độc lập, không cần giữ
  layout trang chọn phía sau).
- Trong modal: minh hoạ SVG full-size ở trên (căn giữa, max-width 600px)
  → đọc ngắn ngay dưới → mô hình 3D (nếu tab có, cao ~360px) → câu hỏi
  khám phá + nút "Xem gợi ý" ở cuối.
- Nút đóng modal góc trên phải, không có nút "Tiếp theo" ép tuyến tính
  (đúng tinh thần "xem tuỳ ý, không bắt buộc thứ tự").
```

### Mobile (≤767px)

```
- KHÔNG dùng modal toàn màn hình kiểu popup che hết (dễ khó thoát trên
  màn nhỏ) — thay bằng: **thanh tab lướt ngang cố định trên đầu** (7 nhãn
  ngắn — thêm "Đứng bóng" vào cuối danh sách cũ: "Đo đạc", "Thiên văn",
  "Con quay", "Kiến trúc", "Nghiêng", "Tự nhiên", "Đứng bóng"), nội dung
  tab đang chọn hiện NGAY DƯỚI, cuộn dọc bình thường.
  > ⚠️ **Đây dùng đúng PHẦN 3.6c** (`02_design_toan_final.md`, phiên bản
  > 2.5) — thanh tab độc lập, lướt ngang, không cần canvas chung — vì
- Thứ tự xếp dọc trong mỗi tab (mobile): minh hoạ SVG (full-width, giữ
  đúng tỉ lệ viewBox) → đọc ngắn → mô hình 3D (full-width, cao tối
  thiểu 280px để vẫn thao tác xoay được bằng ngón tay) → câu hỏi khám
  phá + nút "Xem gợi ý" (full-width, ≥44px cao, dễ chạm).
- Thanh tab lướt ngang: mỗi nhãn tab padding đủ rộng (≥44px vùng chạm),
  tab đang chọn có nền --jade-pale + chữ --jade-text, các tab khác nền
  --cream-2 + chữ --ink-2 (đúng bảng SIGNAL, không tự bịa màu mới).
- Mô hình 3D trên mobile: touch-action:none trên canvas, dùng Pointer
  Events cho xoay (1 ngón = xoay, 2 ngón = zoom) — đúng chuẩn đã có ở
  05_threejs_engine.md, không cần thêm gì mới.
```

**Ánh xạ tương tác Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Chọn tab/nhánh | Click thẻ trong lưới → mở modal | Tap nhãn trên thanh lướt ngang → nội dung hiện dưới |
| Xoay mô hình 3D | Kéo chuột (OrbitControls) | Vuốt 1 ngón (Pointer Events) |
| Zoom mô hình 3D | Cuộn chuột | Chụm/mở 2 ngón (pinch) |
| Xem gợi ý câu hỏi | Click nút "Xem gợi ý" | Tap nút "Xem gợi ý" (full-width, ≥44px) |
| Đóng nội dung tab (desktop only) | Click nút X góc modal | — (không cần, mobile không dùng modal) |

---

## Rủi ro kỹ thuật 3D (giữ nguyên từ bản v1, bổ sung phần responsive)

```
✅ An toàn: mọi minh hoạ SVG (Tab 1-6) — vẽ tĩnh bằng path/shape cơ bản,
   không cần thư viện ngoài, tương thích mọi kích thước màn hình khi đặt
   viewBox đúng + width:100% trong CSS.
⚠️ Cần prototype trước khi build: Tab 3 (gimbal 3 lớp, mô hình 3D) — như
   đã ghi ở bản v1, không đổi.
⚠️ Mới: thanh tab lướt ngang mobile (7 nhãn) cần test thật trên màn hình
   ≤375px — 7 nhãn ngắn càng khó hiện đồng thời hơn (so với 6 trước đó),
   cần đảm bảo scroll ngang mượt (`overflow-x: auto`, `-webkit-overflow-scrolling:
   touch`, ẩn scrollbar nhưng vẫn scroll được).
✅ Đã có pattern chính thức: `02_design_toan_final.md` PHẦN 3.6c (phiên
   bản 2.5) — thanh tab độc lập, lướt ngang, `position:sticky`, không cần
   canvas cố định. Dùng đúng class `.tab-bar-standalone`/`.tab-pill`/
   `.tab-panel` theo đúng HTML/CSS mẫu đã định nghĩa ở đó.
```

---

> **Trạng thái:** Bản v2 đã bổ sung spec minh hoạ SVG cụ thể cho cả 7 tab
> (thêm Tab 7 "Đứng bóng và chí tuyến" từ Em có biết Bài 26, phạm vi
> module giờ là Bài 22-26)
> (dùng đúng token màu illustration có sẵn, không cần màu mới) và chốt
> đầy đủ layout responsive desktop/mobile. Nội dung đọc, mô hình 3D, câu
> hỏi khám phá giữ nguyên như bản v1 đã duyệt — chỉ bổ sung phần hình ảnh
> và responsive, không đổi nội dung kiến thức.
