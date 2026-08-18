# Bài 22. Ba đường conic
## Module 5 (Mở rộng): Khám phá định vị bằng Hypebol — "Vì sao cần ít nhất 3 trạm?"

> **Ghi chú build:** Đây là module MỞ RỘNG/khám phá độc lập, tách khỏi 4
> module cốt lõi đã có (Elip, Hypebol, Parabol, Ứng dụng tổng hợp) — không
> tính vào tiến trình bắt buộc của Bài 22, có `LMS().complete()` riêng cho
> chính module này. Lấy cảm hứng từ mục "Em có biết — LORAN" của SGK, nhưng
> chuyển hẳn từ "đọc chữ + xem 1 hình tĩnh" sang trải nghiệm khám phá bằng
> kéo-thả, không yêu cầu học sinh giải toán đại số (khác hẳn Module 4 Nhiệm
> vụ 2 — module đó tính PT hypebol bằng số liệu cụ thể; module này thuần
> trực quan hình học, không có phép tính nào học sinh phải tự làm).

**Mục tiêu:** Học sinh tự khám phá bằng kéo-thả để THẤY quỹ tích hypebol
hình thành từ chính các điểm mình tìm được (không phải học lại định nghĩa
bằng lời), rồi hiểu trực quan vì sao cần giao 2 đường cong mới xác định
được chính xác 1 vị trí — nguyên lý cốt lõi của hệ thống định vị LORAN.

**Sai lầm/quan niệm cần điều chỉnh:**
1. Nghĩ rằng chỉ cần 2 trạm là đủ định vị chính xác (không nhận ra 2 trạm
   chỉ cho 1 đường, không phải 1 điểm).
2. Không hình dung được hypebol là tập hợp NHIỀU điểm rời rạc cùng thoả 1
   điều kiện, chỉ nhớ công thức mà không có trực giác hình học.

**Loại simulation:** E — Dự đoán/khám phá tự do (Pha 1: kéo-thả tìm quỹ
tích) kết hợp F — Xây dựng ngược (Pha 2: suy luận từ 2 nhánh giao nhau).

**Sổ tay kiến thức: Không cần đầy đủ** — chỉ 1 dòng nhắc ngắn (module thuần
khám phá, không phải luyện kỹ thuật):
```
- Hypebol: tập hợp các điểm M sao cho |MA − MB| = hằng số không đổi
```

**Thời gian hoàn thành dự kiến:** ~10 phút (thiên về trải nghiệm, không có
bước tính toán nặng)

---

### Rà soát trùng lặp:
- 📖 SGK "Em có biết" (trang 56) chỉ có 3 đoạn văn + 1 hình tĩnh (Hình 7.35a)
  mô tả nguyên lý bằng chữ, không có tương tác nào — module này biến thành
  trải nghiệm kéo-thả, hoàn toàn khác hình thức.
- Module 4 Nhiệm vụ 2 (đã làm trước) yêu cầu học sinh TÍNH ra PT hypebol từ
  số liệu cụ thể (200km, 0,0004 giây...) — kỹ thuật ĐẠI SỐ. Module 5 này
  KHÔNG có phép tính nào cho học sinh, thuần khám phá TRỰC QUAN HÌNH HỌC —
  khác hẳn loại kỹ năng, không trùng lặp dù cùng chủ đề LORAN.
- Số liệu dùng đơn vị lưới trừu tượng (không phải km/giây thực tế như Module
  4) — chủ đích tách biệt hoàn toàn 2 module để không gây cảm giác lặp lại.

---

### Màn hình chính hiển thị:
- Canvas SVG dạng **bản đồ minh hoạ** (nền biển xanh nhạt, có đảo nhỏ trang
  trí — phong cách illustrative, KHÁC hẳn lưới toạ độ Oxy khô khan đã dùng ở
  4 module cốt lõi, để module này cảm giác "khám phá" rõ rệt hơn).
  - Icon trạm phát sóng: cột ăng-ten (que + vòng tròn) tại 2-3 vị trí cố
    định.
  - Icon tàu thuyền: hình tam giác nhỏ cách điệu, kéo được tự do trên biển.
- Panel số liệu real-time (góc màn hình): khoảng cách MA, MB, hiệu |MA−MB|
  — cập nhật liên tục khi kéo tàu.
- Panel "Nhật ký khám phá": liệt kê các điểm đã "chốt" (đánh dấu hợp lệ).

### Học sinh tương tác bằng cách:
1. Kéo tự do con tàu, quan sát số liệu MA, MB, hiệu số thay đổi liên tục.
2. Tìm và "chốt" đủ 6 vị trí thoả hiệu số = hằng số cho trước (dung sai nhỏ
   được chấp nhận).
3. Trả lời câu hỏi nhận dạng hình dạng đường cong vừa hiện ra.
4. Xem thêm trạm C và nhánh hypebol thứ 2 (đã vẽ sẵn, không phải tự dò lại).
5. Trả lời 2 câu hỏi suy luận: vì sao 2 trạm chưa đủ, và giao điểm 2 nhánh
   cho biết điều gì.
6. Đọc Nhận xét liên hệ hệ thống LORAN thực tế.

---

### Bảng checkpoint

| Bước | Hướng dẫn thao tác | Mục tiêu nhận thức |
|---|---|---|
| 1 — Khám phá quỹ tích (Pha 1) | "Trạm A và trạm B phát tín hiệu. Tàu M nhận được tín hiệu với hiệu khoảng cách luôn là 4 ô lưới. Kéo tàu M tới các vị trí thoả điều kiện này, bấm 'Đánh dấu' mỗi khi tìm đúng — cần đủ 6 điểm." | Tự phát hiện: các điểm hợp lệ không nằm rải rác ngẫu nhiên mà tạo thành 1 đường cong có quy luật. |
| 2 — Nhận dạng | "Đường cong vừa hiện ra từ 6 điểm bạn đánh dấu có hình dạng gì?" | Nối lại đúng tên gọi đã học: đây chính là 1 nhánh hypebol, không phải hình vẽ ngẫu nhiên. |
| 3 — Vì sao cần thêm trạm (Pha 2) | "Thêm trạm C xuất hiện. Quan sát nhánh hypebol thứ 2 (từ cặp trạm B, C) đã hiện sẵn. Tại sao chỉ với 2 trạm A, B, ta CHƯA XÁC ĐỊNH được chính xác vị trí tàu?" | Hiểu: 2 trạm chỉ cho biết tàu nằm trên 1 ĐƯỜNG (vô số điểm thoả mãn), không phải 1 điểm cụ thể. |
| 4 — Suy luận giao điểm | "Giao điểm của 2 nhánh hypebol (từ cặp A-B và cặp B-C) cho ta điều gì?" | Hiểu: giao điểm chính là vị trí CHÍNH XÁC DUY NHẤT của tàu — cần ÍT NHẤT 2 đường (từ 3 trạm) mới định vị được. |
| 5 — Nhận xét & liên hệ | Đọc nội dung liên hệ hệ thống LORAN thực tế (xem chi tiết bên dưới). | — |

---

### Cấu trúc hình vẽ / Canvas

| Bước | Cần vẽ | Thời điểm |
|---|---|---|
| 1 | Bản đồ biển (nền xanh nhạt, 1-2 đảo nhỏ trang trí góc canvas). 2 trạm A, B (icon ăng-ten) cố định. Tàu M (icon tam giác) kéo được tự do. Khi kéo: vẽ live 2 đoạn nối M-A, M-B (nét mảnh, mờ) cập nhật theo vị trí. Mỗi lần "Đánh dấu" hợp lệ → để lại 1 chấm cam cố định tại vị trí đó (không biến mất khi tiếp tục kéo) | Live suốt Pha 1; chấm chốt tích luỹ dần |
| 1 (sau đủ 6 điểm) | Nối mượt 6 chấm cam thành 1 đường cong liền nét (spline/curve fit đơn giản, không cần chính xác toán học tuyệt đối vì đây là minh hoạ trực quan) — hiệu ứng "đường cong dần hiện ra" | Khi đủ 6 điểm |
| 3 | Giữ nguyên Nhánh 1. Thêm trạm C (icon ăng-ten, màu khác A/B để phân biệt). Vẽ sẵn Nhánh 2 (nét đứt, màu khác Nhánh 1) từ cặp B-C — không bắt học sinh tự dò lại, chỉ hiển thị luôn để tiết kiệm thời gian | Khi vào Bước 3 |
| 4 (sau khi đúng) | Đánh dấu giao điểm 2 nhánh bằng 1 chấm nổi bật (vàng, viền đậm) + icon tàu thật đặt đúng tại đó, có đường dóng nhẹ tới nhãn "Vị trí tàu" | Sau khi trả lời đúng Bước 4 |

**Tài sản minh hoạ:** icon ăng-ten (que + vòng tròn), icon tàu (tam giác cách
điệu), 1-2 hình đảo đơn giản (path bo tròn, fill xanh lá) — vẽ bằng SVG code,
không cần ảnh chụp/AI.

> **Lưu ý build:** đường cong Nhánh 1, 2 không cần tính bằng công thức
> chính tắc hypebol tường minh — có thể vẽ bằng thuật toán số (sample nhiều
> điểm thoả `|MA-MB|=const` trong vùng canvas rồi nối spline) vì đây là
> module minh hoạ trực quan, không đòi hỏi độ chính xác đại số như module
> luyện tập.

---

### Giải thích kiến thức (mọi trạng thái)

| Bước | Khi ĐÚNG/đủ điều kiện | Khi SAI/chưa đủ |
|---|---|---|
| 1 | "Đủ 6 điểm! Nhìn lại: dù bạn kéo tàu ở nhiều vị trí rất khác nhau, tất cả các điểm hợp lệ đều nằm trên cùng 1 đường cong." | (Khi hiệu số chưa đúng) "Hiệu khoảng cách hiện tại chưa đạt 4 — thử kéo tàu xa trạm A hơn hoặc gần trạm B hơn." |
| 2 | "Chính xác! Đây là 1 nhánh hypebol — đúng tập hợp các điểm có hiệu khoảng cách tới 2 điểm cố định không đổi." | "Nhìn lại hình dạng đường cong — nó có giống đồ thị hypebol đã học không?" |
| 3 | "Đúng! Vì vô số điểm trên Nhánh 1 đều thoả mãn tín hiệu từ A, B — tàu có thể ở BẤT KỲ đâu trên đường đó, chưa xác định được vị trí cụ thể." | "Thử đếm: có bao nhiêu điểm thoả mãn điều kiện hiệu khoảng cách không đổi từ A, B? Chỉ 1 điểm hay cả 1 đường?" |
| 4 | "Chính xác! Giao điểm của 2 nhánh là điểm DUY NHẤT vừa thoả điều kiện với A, B, VỪA thoả điều kiện với B, C — đó chính là vị trí tàu." | "So sánh: Nhánh 1 cho vô số điểm khả dĩ, Nhánh 2 cũng vậy — điểm nào vừa nằm trên CẢ HAI nhánh?" |
| Sau khi hoàn thành | — | "Tổng kết: hypebol là quỹ tích các điểm có hiệu khoảng cách tới 2 điểm cố định không đổi. Với đúng 2 trạm phát sóng, ta chỉ xác định được 1 ĐƯỜNG chứa vị trí — cần ít nhất 3 trạm (tạo ra 2 đường) để tìm giao điểm, xác định CHÍNH XÁC 1 vị trí duy nhất." |

---

### Nhận xét & liên hệ thực tế (Bước 5, đọc)

> "Đây chính xác là nguyên lý của hệ thống **LORAN (Long Range Navigation)**
> — từng được dùng rộng rãi cho tàu thuyền và máy bay trước khi có GPS vệ
> tinh. Các trạm phát sóng cố định trên mặt đất liên tục phát tín hiệu vô
> tuyến; thiết bị trên tàu đo được hiệu thời gian nhận tín hiệu giữa từng
> CẶP trạm — hiệu thời gian này tỉ lệ trực tiếp với hiệu khoảng cách, nên
> mỗi cặp trạm cho biết tàu nằm trên 1 nhánh hypebol xác định. Với ÍT NHẤT
> 3 trạm (2 cặp trạm độc lập), giao điểm của 2 nhánh hypebol chính là vị trí
> chính xác của tàu — đúng như bạn vừa tự khám phá ra bằng cách kéo-thả.
>
> 💡 Hệ thống GPS hiện đại dùng nguyên lý tương tự nhưng với vệ tinh và mặt
> cầu trong không gian 3 chiều thay vì hypebol phẳng — đó là lý do GPS cần
> tín hiệu từ ÍT NHẤT 4 vệ tinh để định vị chính xác vị trí (bao gồm cả độ
> cao), nhiều hơn 3 trạm LORAN vì bài toán chuyển từ 2D sang 3D."

---

### Trường dữ liệu bắt buộc

**Bước 1 (không chấm điểm từng lần kéo — chỉ kiểm tra ĐỦ 6 điểm hợp lệ):**
```
Điều kiện hoàn thành: đủ 6 điểm có |MA-MB| = 4 (± dung sai 0.15 đơn vị lưới)
giai_thich_dung: "Đủ 6 điểm hợp lệ — đường cong đã hiện rõ."
goi_y_khi_chua_du: "Tiếp tục kéo tàu và thử ở các vị trí khác — chỉ cần hiệu khoảng cách đúng bằng 4."
```

**Bước 2:**
```
dap_an_dung: 1 nhánh hypebol
giai_thich_dung: "Đúng! Đây là tập hợp điểm có hiệu khoảng cách tới A, B không đổi — định nghĩa hypebol."
goi_y_khi_sai: "So sánh hình dạng đường cong với đồ thị hypebol đã học ở Module 2."
```

**Bước 3:**
```
dap_an_dung: Vì tàu có thể ở bất kỳ đâu trên cả đường cong (vô số vị trí thoả mãn)
giai_thich_dung: "Đúng! 2 trạm chỉ xác định được 1 đường (vô số điểm), không phải 1 điểm."
goi_y_khi_sai: "Đếm số điểm thoả điều kiện hiệu khoảng cách không đổi từ A, B — có phải chỉ 1 điểm không?"
```

**Bước 4:**
```
dap_an_dung: Vị trí chính xác duy nhất của tàu
giai_thich_dung: "Đúng! Giao điểm là điểm duy nhất thoả mãn CẢ HAI điều kiện cùng lúc."
goi_y_khi_sai: "Điểm nào vừa nằm trên Nhánh 1 (từ A, B), vừa nằm trên Nhánh 2 (từ B, C)?"
```

---

### Bố cục Mobile
Module có 5 bước, thuộc ngưỡng Mục 3.6b của `02_design_toan_final.md` (bắt
buộc lướt ngang, có `.mobile-hint`) — áp dụng đúng bản hoà giải đã thống
nhất: vuốt ngang chỉ để xem lại bước đã mở khoá, việc hoàn thành/mở khoá
luôn qua 1 nút cố định đáy màn hình. Riêng Bước 1 (khám phá kéo-thả): nút
"Đánh dấu" đặt ngay trong canvas (không phải thanh nút đáy, vì lặp lại nhiều
lần và cần ở gần vị trí tàu đang kéo để thao tác nhanh) — thanh nút đáy chỉ
hiện nút "Tiếp tục ▶" sau khi đã đủ 6 điểm. Canvas bản đồ cần tối thiểu
300px chiều cao trên mobile để đủ không gian kéo-thả chính xác bằng ngón
tay — `touch-action: none` trên icon tàu để tránh cuộn trang khi đang kéo.

### Nút và điều khiển:
- **Đánh dấu (Bước 1):** ghi nhận 1 điểm hợp lệ, không chấm điểm sai/đúng
  theo nghĩa MCQ — chỉ kiểm tra điều kiện hiệu khoảng cách.
- **Kiểm tra (Bước 2, 3, 4):** xác nhận đáp án MCQ.
- **Tiếp tục ▶ / nhãn động (mobile):** sang bước kế, chỉ hiện khi đủ điều
  kiện (đủ 6 điểm ở Bước 1, hoặc trả lời đúng ở Bước 2-4).

---

## Critical Review — Tự phản biện

⚠️ Rủi ro 1: dung sai `±0.15` ở Bước 1 cần đội build tinh chỉnh thực tế khi
test bằng ngón tay trên mobile — quá chặt sẽ khiến học sinh khó chốt đủ 6
điểm, quá lỏng sẽ làm đường cong hiện ra không rõ hình dạng hypebol.

⚠️ Rủi ro 2: thuật toán vẽ đường cong bằng sample số + spline (không phải
công thức chính tắc tường minh) cần đội build kiểm tra kỹ để đường cong
không bị méo/gãy khúc, ảnh hưởng tới việc học sinh nhận ra đúng hình dạng
hypebol ở Bước 2.

📖 Kiểm tra caption: đã rà lại — không có dòng trống thiếu giải thích.

💡 Điểm mạnh: module hoàn toàn không có phép tính đại số nào bắt học sinh
làm — đúng vai trò "mở rộng trực quan" tương đương "Em có biết" SGK nhưng
nâng cấp thành trải nghiệm chủ động thay vì đọc thụ động.

---

## 🔗 Athena Context & Tích hợp LMS (bắt buộc theo `02_design_toan_final.md` PHẦN 7)

> Nhân vật hướng dẫn/gợi ý trong module LUÔN gọi là **"Athena"** — không dùng
> "robot"/"AI"/tên khác, theo đúng PHẦN 7.9. Module này có `structure[]` và
> manifest RIÊNG, độc lập với 4 module cốt lõi của Bài 22 — vì đây là nội
> dung mở rộng tự chọn, không phải phần bắt buộc của chương trình chính.

### `structure[]`
```
[
  { "id": "b22m5-b1", "title": "Bước 1 — Khám phá quỹ tích (kéo-thả)" },
  { "id": "b22m5-b2", "title": "Bước 2 — Nhận dạng hình dạng đường cong" },
  { "id": "b22m5-b3", "title": "Bước 3 — Vì sao cần thêm trạm" },
  { "id": "b22m5-b4", "title": "Bước 4 — Suy luận giao điểm" },
  { "id": "b22m5-b5", "title": "Bước 5 — Nhận xét & liên hệ LORAN" }
]
```
**Bước 1–4 BẮT BUỘC để hoàn thành MODULE NÀY** (`progress total = 4`, module
này tính riêng, không cộng vào tổng tiến trình 4 module cốt lõi của Bài 22).
Bước 5 là đọc, không chấm điểm.

### `athenaGuidance` (bản nháp)
```
Module mở rộng (không bắt buộc trong chương trình chính) giúp học sinh khám
phá bằng kéo-thả tại sao hệ thống định vị LORAN cần ít nhất 3 trạm phát
sóng, dựa trên tính chất định nghĩa của hypebol.

1) Kéo tàu M tới các vị trí thoả hiệu khoảng cách |MA-MB|=4 (đơn vị lưới),
   đánh dấu đủ 6 điểm hợp lệ. (thao tác khám phá, không phải câu hỏi
   đúng/sai — chỉ kiểm tra điều kiện số học)
2) Đường cong vừa hiện ra từ 6 điểm đánh dấu có hình dạng gì?
   Lựa chọn: A) 1 nhánh hypebol  B) 1 đường elip  C) 1 đường parabol
3) Tại sao chỉ với 2 trạm A, B, ta CHƯA XÁC ĐỊNH được chính xác vị trí tàu?
   Lựa chọn: A) Vì tàu có thể ở bất kỳ đâu trên cả đường cong (vô số vị trí
                thoả mãn)
             B) Vì tín hiệu radio không đủ mạnh
             C) Vì 2 trạm không đủ khoảng cách với nhau
4) Giao điểm của 2 nhánh hypebol (từ cặp A-B và cặp B-C) cho ta điều gì?
   Lựa chọn: A) Vị trí chính xác duy nhất của tàu
             B) Vận tốc của tàu
             C) Khoảng cách giữa 2 trạm

Quy tắc đứng: Athena chỉ gợi ý theo đúng cột "Khi SAI/chưa đủ" đã định
nghĩa cho từng bước, KHÔNG BAO GIỜ nói thẳng đáp án đúng khi học sinh hỏi
giữa chừng — kể cả ở Bước 1 (khám phá), Athena chỉ được nhắc lại điều kiện
cần đạt ("hiệu khoảng cách phải bằng 4"), không được gợi ý vị trí cụ thể
nên kéo tàu tới đâu.
```

### Instrumentation cần gắn
- `LMS().progress({done, total:4})` — module tính riêng, độc lập với 4
  module cốt lõi Bài 22.
- `LMS().event('explored', {id:'b22m5-b1', pointsMarked})` — bắn mỗi khi
  học sinh đánh dấu 1 điểm hợp lệ ở Bước 1 (không phải `answered`, vì đây
  là thao tác khám phá tích luỹ, không có khái niệm đúng/sai từng lần).
- `LMS().event('answered', {...})` — bắn ở Bước 2, 3, 4 (câu hỏi MCQ thật
  sự có đáp án đúng/sai).
- `LMS().state({...})` — cập nhật `pointsMarked` liên tục trong Bước 1 để
  Athena biết học sinh đã đánh dấu bao nhiêu điểm nếu được hỏi giữa chừng.
- `LMS().complete({...})` — bắn đúng 1 lần khi Bước 4 hoàn thành (không chờ
  Bước 5); `items` liệt kê đủ 4 mục (Bước 1 ghi `pointsMarked` thay vì
  `chosen`/`correct` vì không phải câu hỏi trắc nghiệm).

---
**Trạng thái: ĐÃ DUYỆT — chuyển sang Giai đoạn 2 (Thiết kế giao diện) khi build.**
