# Bài 22. Ba đường conic
## Module 2: Hypebol — "Tháp giải nhiệt nhà máy điện" (Từ thực tế → Phương trình)

> **Ghi chú build:** Module chạy SAU video Manim (đã dạy định nghĩa hình học
> |MF1−MF2|=2a và PT chính tắc x²/a²−y²/b²=1). Simulation đi chiều ngược:
> xuất phát từ số đo thực tế của tháp giải nhiệt, học sinh tự đặt hệ trục,
> tự suy ra a rồi GIẢI NGƯỢC để tìm b từ 1 điểm đo thêm (khó hơn Module 1 vì
> không đọc trực tiếp được cả 2 tham số). Độc lập với Module 1, không dùng
> lại state. **Không có bước khám phá quang học tương tác** (đã thống nhất
> với giáo viên — tháp giải nhiệt là ứng dụng kết cấu/khí động học, không có
> hiện tượng phản xạ quang học tương tự để mô phỏng).

**Mục tiêu:** Học sinh tự mô hình hoá hình dạng mặt cắt tháp giải nhiệt
(dạng hypebol) thành PT chính tắc — đặt hệ trục tại vị trí hợp lý, xác định
a trực tiếp từ điểm hẹp nhất, rồi giải ngược tìm b từ 1 điểm đo thêm.

**Sai lầm cần giải quyết:**
1. Nhầm công thức c²=a²+b² (hypebol) với c²=a²−b² (elip) — đổi dấu sai.
2. Quên hypebol có 2 nhánh (không chỉ áp dụng công thức cho 1 phía).

**Loại simulation:** B — Step-by-step (tự mô hình hoá tuần tự, có bước giải
ngược khó hơn Module 1).

**Sổ tay kiến thức: Có** (module luyện tập, khái niệm đã dạy qua video):
```
- PT chính tắc: x²/a²−y²/b²=1 (a,b>0)
- a = khoảng cách từ tâm đến đỉnh gần nhất (nửa trục thực)
- Quan hệ: c² = a² + b²  (Hypebol: CỘNG — ngược với Elip)
- Tiêu điểm F1(−c;0), F2(c;0)
- Hypebol có 2 NHÁNH — mỗi điểm trên hypebol chỉ thuộc 1 trong 2 nhánh
```

**Thời gian hoàn thành dự kiến:** ~12 phút

---

### Rà soát SGK trước khi thiết kế:
- 📖 SGK: Ví dụ 3 (đường ranh giới biển giữa 2 đảo — hiệu khoảng cách =
  hiệu bán kính), Ví dụ 4 (hypebol chính tắc x²/9−y²/16=1, tìm tiêu điểm/
  tiêu cự), Luyện tập 3, 4, Bài tập 7.20, 7.24 (LORAN). SGK Mục 4 CÓ nhắc
  "tháp giải nhiệt hình hypebol" (Hình 7.17c) nhưng chỉ dạng liệt kê 1 câu,
  KHÔNG có bài toán số liệu cụ thể nào — module này xây trọn vẹn thành bài
  toán hoàn chỉnh, không phải chép lại.
- Số liệu (a=20, b=40, điểm đo (30;25)) khác hoàn toàn mọi PT xuất hiện
  trong SGK.
- Kỹ thuật "giải ngược tìm b từ 1 điểm đo thêm" (Bước 3) là kỹ thuật SGK
  KHÔNG có — mọi ví dụ SGK đều cho sẵn cả a², b², không yêu cầu tự tìm b từ
  dữ kiện gián tiếp.

---

### Màn hình chính hiển thị:
- Canvas SVG: hình minh hoạ mặt cắt dọc tháp giải nhiệt (phong cách
  flat-icon, viền cong đặc trưng hypebol — không phải ảnh chụp).
- Panel nhập liệu bên cạnh.
- Sổ tay kiến thức thu gọn phía trên canvas.

### Học sinh tương tác bằng cách:
1. Chọn vị trí đặt hệ trục (gốc tại "cổ" tháp — điểm hẹp nhất).
2. Đọc dữ kiện → xác định a trực tiếp.
3. Giải ngược tìm b từ 1 điểm đo thêm trên tháp.
4. Viết PT chính tắc.
5. Quay lại thực tế: tính bán kính đáy móng tháp.
6. (Không bắt buộc) Mở rộng: tính tiêu cự.

---

### Bảng checkpoint

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 — Đặt hệ trục | "Xem mặt cắt tháp. Chọn vị trí đặt gốc O hợp lý: (A) tại 'cổ' tháp — điểm hẹp nhất; (B) tại đáy tháp; (C) tại đỉnh tháp." | "Đặt gốc tại điểm hẹp nhất (đỉnh của 1 nhánh hypebol) cho PT chính tắc đơn giản, trục ngang = bán kính r, trục đứng = độ cao h." |
| 2 — Xác định a | "Tại cổ tháp (h=0), bán kính đo được là 20m. Nhập giá trị a." | "Tại đỉnh nhánh hypebol (h=0), bán kính chính là a → a=20." |
| 3 — Giải ngược tìm b | "Tại độ cao 30m tính từ cổ tháp, bán kính đo được là 25m. Nhập b." | "Thay điểm (h=30; r=25) vào r²/a²−h²/b²=1: 625/400−900/b²=1 → giải ra b²=1600 → b=40." |
| 4 — Viết PT | "Nhập PT chính tắc mô tả mặt cắt tháp (dạng r²/…−h²/…=1)." | "Thay a²=400, b²=1600 vào dạng chính tắc." |
| 5 — Quay lại thực tế | "Tính bán kính đáy móng tháp tại vị trí 50m PHÍA DƯỚI cổ tháp (h=−50)." | "Thay h=−50 vào PT: r²/400−2500/1600=1 → r≈32,02m — hypebol đối xứng nên nhánh dưới dùng cùng công thức với h âm." |
| 6 — Mở rộng (không bắt buộc) | "Tính tiêu cự 2c của mặt cắt tháp." | "c²=a²+b²=400+1600=2000 → c=20√5≈44,72 → 2c≈89,44m." |

---

### Cấu trúc hình vẽ / Canvas

| Bước | Cần vẽ | Thời điểm |
|---|---|---|
| 1 | Vẽ mặt cắt tháp (đường cong hypebol cách điệu, 2 nhánh đối xứng qua trục đứng, viền nâu/xám bê tông). Vẽ mờ 3 vị trí ứng viên gốc O (A: cổ tháp; B: đáy; C: đỉnh) dạng chấm mờ nhãn A/B/C. Sau khi chọn đúng (A) → hệ trục hiện rõ, trục ngang r, trục đứng h | Ngay khi vào bước; hệ trục rõ sau khi đúng |
| 2 | Giữ hệ trục. Sau khi đúng → đánh dấu đoạn từ O ra viền tháp tại h=0, nhãn "a=20m" | Sau khi đúng |
| 3 | Sau khi đúng → đánh dấu điểm (h=30;r=25) trên viền tháp (chấm xanh, có đường dóng ngang/dọc tới 2 trục), nhãn toạ độ | Sau khi đúng |
| 4 | Không cần vẽ thêm | — |
| 5 | Vẽ thêm phần MÓNG tháp phía dưới cổ (mở rộng nhánh hypebol xuống h=−50), đánh dấu bán kính tại đó (r≈32,02m) | Sau khi đúng |
| 6 | Đánh dấu 2 tiêu điểm F1, F2 trên trục ngang (nếu mở rộng đủ khung hình) hoặc chỉ hiện số liệu dạng text nếu tiêu điểm nằm ngoài khung nhìn hợp lý của tháp | Sau khi đúng |

**Tài sản minh hoạ:** đường cong hypebol cách điệu dạng "cổ chai" đặc trưng
tháp giải nhiệt — vẽ bằng path SVG (2 nhánh cong), không cần ảnh chụp/AI.

---

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa

**Sai lầm 1 — nhầm công thức c²=a²+b² (Bước 6, và ngầm cả Bước 3 nếu áp dụng sai công thức):**
- Tình huống: học sinh ở Bước 3 có thể viết nhầm công thức r²/a²+h²/b²=1
  (dùng dấu CỘNG như elip) khi giải ngược tìm b.
- Hệ thống phản hồi: sai lần 1 → shake. Sai lần 2 → gợi ý: "Đây là hypebol,
  không phải elip — công thức chính tắc dùng dấu TRỪ: r²/a²−h²/b²=1."
- Kết quả rút ra: học sinh phân biệt được ngay cả khi đang ở bước tính toán
  phức tạp (giải ngược), không chỉ ở câu hỏi lý thuyết đơn giản.

**Sai lầm 2 — quên hypebol có 2 nhánh (Bước 5):**
- Tình huống: học sinh có thể bối rối khi thấy h=−50 (số âm) và không biết
  có áp dụng được công thức không, hoặc nghĩ cần đổi công thức khác cho
  "nhánh dưới".
- Hệ thống phản hồi: gợi ý "Hypebol đối xứng qua tâm O — nhánh dưới (h âm)
  dùng ĐÚNG công thức r²/a²−h²/b²=1 như nhánh trên, chỉ cần thay h=−50 vào,
  vì h² luôn dương dù h âm."
- Kết quả rút ra: khắc sâu tính đối xứng của hypebol, không cần công thức
  riêng cho từng nhánh.

---

### Giải thích kiến thức (bắt buộc mọi trạng thái)

| Bước | Khi ĐÚNG | Khi SAI |
|---|---|---|
| 1 | "Chính xác! Đặt gốc tại cổ tháp (điểm hẹp nhất) cho PT chính tắc đơn giản, đúng vai trò 'đỉnh' của hypebol." | "Cách này vẫn mô tả được, nhưng phương trình sẽ không ở dạng chính tắc đơn giản — hãy đặt gốc tại điểm HẸP NHẤT của tháp." |
| 2 | "Đúng! Tại cổ tháp (h=0), bán kính chính là a=20." | "Tại đỉnh của nhánh hypebol (ứng với h=0), bán kính đo được chính là giá trị a." |
| 3 | "Chính xác! Thay điểm (30;25) vào PT, giải ra b²=1600, b=40." | "Kiểm tra lại: đã dùng đúng công thức TRỪ r²/a²−h²/b²=1 (không phải cộng) khi thay số chưa?" |
| 4 | "Đúng! r²/400−h²/1600=1." | "Kiểm tra lại a²=400 và b²=1600 đã thay đúng vị trí chưa." |
| 5 | "Chính xác! r≈32,02m — hypebol đối xứng nên h=−50 dùng đúng công thức như h dương." | "h âm không cần công thức khác — vì h² luôn dương, chỉ cần thay trực tiếp h=−50 vào PT đã có." |
| 6 | "Đúng! c²=a²+b²=2000 → c=20√5≈44,72, tiêu cự 2c≈89,44m." | "Hypebol dùng công thức CỘNG c²=a²+b², không phải trừ như elip — dễ nhầm nhất khi vừa học xong Module 1." |
| Sau khi hoàn thành module | — | "Tổng kết: hypebol có c²=a²+b² (CỘNG, ngược với elip). a là khoảng cách từ tâm tới đỉnh gần nhất. Hypebol có 2 nhánh đối xứng qua tâm, dùng chung 1 công thức r²/a²−h²/b²=1 cho cả 2 phía." |

---

### Trường dữ liệu bắt buộc

**Bước 1:**
```
dap_an_dung: A (cổ tháp)
giai_thich_dung: "Đúng! Đặt gốc tại điểm hẹp nhất cho PT chính tắc đơn giản."
goi_y_khi_sai: "Hãy đặt gốc tại điểm HẸP NHẤT của tháp — đó là đỉnh của nhánh hypebol."
```

**Bước 2:**
```
dap_an_dung: a=20
giai_thich_dung: "Đúng! Tại cổ tháp (h=0), bán kính chính là a."
goi_y_khi_sai: "Bán kính tại điểm hẹp nhất (h=0) chính là giá trị a."
```

**Bước 3:**
```
dap_an_dung: b=40
giai_thich_dung: "Đúng! Thay (30;25) vào r²/400-h²/b²=1, giải ra b²=1600, b=40."
goi_y_khi_sai: "Dùng đúng công thức TRỪ (không phải cộng) khi thay điểm đo vào."
```

**Bước 4:**
```
dap_an_dung: r²/400-h²/1600=1
giai_thich_dung: "Đúng! Thay a²=400, b²=1600 vào dạng chính tắc."
goi_y_khi_sai: "Kiểm tra lại a², b² đã thay đúng vị trí trong công thức."
```

**Bước 5:**
```
dap_an_dung: ≈32.02 (mét)
giai_thich_dung: "Đúng! Thay h=-50 vào PT, r²=400(1+2500/1600)≈1025, r≈32,02m."
goi_y_khi_sai: "Thay trực tiếp h=-50 vào PT đã lập ở Bước 4, không cần đổi công thức."
```

**Bước 6 (không bắt buộc):**
```
dap_an_dung: ≈89.44 (mét)
giai_thich_dung: "Đúng! c²=a²+b²=2000, c=20√5, tiêu cự 2c≈89,44m."
goi_y_khi_sai: "Hypebol dùng c²=a²+b² (CỘNG), khác elip dùng trừ."
```

---

### Bố cục Mobile
Module có 6 bước — đúng ngưỡng Mục 3.6b của `02_design_toan_final.md` (bắt
buộc lướt ngang, có `.mobile-hint`). Áp dụng bản hoà giải: vuốt ngang chỉ để
XEM LẠI thẻ đã mở khoá; việc HOÀN THÀNH/MỞ KHOÁ bước tiếp theo luôn qua 1 nút
cố định đáy màn hình với nhãn động, thẻ chưa mở khoá không render trong DOM.
Bước 6 (mở rộng) có nút "Hoàn thành" riêng, không chặn tiến trình chính nếu
học sinh bỏ qua.

### Nút và điều khiển:
- **Kiểm tra:** xác nhận đáp án, kích hoạt hình vẽ/feedback.
- **Tiếp tục ▶ / nhãn động (mobile):** sang bước kế, chỉ hiện sau khi đúng.
- **Sổ tay:** mở/đóng panel công thức.

---

## Critical Review — Tự phản biện

⚠️ Rủi ro: Bước 3 (giải ngược tìm b) là bước khó nhất module — cần đảm bảo
gợi ý sai lần 2 đủ cụ thể (chỉ ra đúng công thức cần dùng), tránh học sinh bị
kẹt hoàn toàn nếu chưa quen thao tác giải phương trình từ 1 điểm dữ liệu.

📖 Kiểm tra caption: đã rà lại — không có dòng trống thiếu giải thích.

💡 Ghi nhận: Module này CHỦ Ý không có bước khám phá tương tác kiểu Module 1
— đã thống nhất với giáo viên rằng tháp giải nhiệt là ứng dụng kết cấu, không
có nguyên lý quang học tương tự để mô phỏng có ý nghĩa.

---

## Rà soát trùng lặp SGK

- Bối cảnh "tháp giải nhiệt" được SGK Mục 4 nhắc tên (Hình 7.17c) nhưng
  không có bài toán số liệu — module này xây mới hoàn toàn, không sao chép.
- Số liệu (a=20, b=40, điểm đo (30;25), h=−50) không trùng bất kỳ PT nào
  trong SGK (Ví dụ 3, 4, Luyện tập 3, 4, Bài tập 7.20, 7.24).
- Kỹ thuật "giải ngược tìm b từ 1 điểm đo" không xuất hiện trong bất kỳ ví
  dụ/bài tập nào của SGK — phần mở rộng độc lập, khó hơn hẳn các bài SGK chỉ
  yêu cầu đọc trực tiếp a², b² cho sẵn.

---
**Trạng thái: ĐÃ DUYỆT — chuyển sang Giai đoạn 2 (Thiết kế giao diện) khi build.**

---

## 🔗 Athena Context & Tích hợp LMS (bắt buộc theo `02_design_toan_final.md` PHẦN 7)

> Nhân vật hướng dẫn/gợi ý trong module LUÔN gọi là **"Athena"** — không dùng
> "robot"/"AI"/tên khác, theo đúng PHẦN 7.9.

### `structure[]` — id khớp với id dùng trong code
```
[
  { "id": "b22m2-b1", "title": "Bước 1 — Đặt hệ trục (tháp giải nhiệt)" },
  { "id": "b22m2-b2", "title": "Bước 2 — Xác định a" },
  { "id": "b22m2-b3", "title": "Bước 3 — Giải ngược tìm b" },
  { "id": "b22m2-b4", "title": "Bước 4 — Viết PT chính tắc" },
  { "id": "b22m2-b5", "title": "Bước 5 — Tính bán kính đáy móng" },
  { "id": "b22m2-b6", "title": "Bước 6 — Mở rộng: tính tiêu cự (không bắt buộc)" }
]
```
**Bước 1–5 BẮT BUỘC** (`progress total = 5`). **Bước 6 KHÔNG BẮT BUỘC** —
không tính vào `total`.

### `athenaGuidance` (bản nháp)
```
Module dạy học sinh tự mô hình hoá mặt cắt tháp giải nhiệt (dạng hypebol)
thành PT chính tắc — đặt hệ trục, xác định a trực tiếp, rồi giải ngược tìm
b từ 1 điểm đo thêm (kỹ thuật khó hơn Module 1, SGK không có dạng bài này).

1) Xem mặt cắt tháp. Chọn vị trí đặt gốc O hợp lý.
   Lựa chọn: A) Tại "cổ" tháp — điểm hẹp nhất  B) Tại đáy tháp
             C) Tại đỉnh tháp
2) Tại cổ tháp (h=0), bán kính đo được là 20m. Nhập giá trị a. (câu điền tự
   do)
3) Tại độ cao 30m tính từ cổ tháp, bán kính đo được là 25m. Nhập b. (câu
   điền tự do — giải ngược từ phương trình, không đọc trực tiếp)
4) Nhập PT chính tắc mô tả mặt cắt tháp (dạng r²/…−h²/…=1). (câu điền tự do)
5) Tính bán kính đáy móng tháp tại vị trí 50m PHÍA DƯỚI cổ tháp (h=−50).
   (câu điền tự do, đáp án số)
6) (không bắt buộc) Tính tiêu cự 2c của mặt cắt tháp. (câu điền tự do, đáp
   án số)

Quy tắc đứng: Athena chỉ gợi ý theo đúng cột "Kiến thức áp dụng"/"Giải
thích" của từng bước (VD "hypebol dùng công thức TRỪ, không phải cộng như
elip" hay "hypebol đối xứng nên h âm dùng đúng công thức như h dương"),
KHÔNG BAO GIỜ nói thẳng đáp án số khi học sinh hỏi giữa chừng.
```

### Instrumentation cần gắn (đội build, theo Mục 7.4–7.6)
- `LMS().progress({done, total:5})` — Bước 6 không cộng vào `total`.
- `LMS().event('answered', {...})` — bắn ở Bước 1–5; Bước 6 nếu học sinh có
  làm thì đánh dấu `required:false`.
- `LMS().state({...})` — cập nhật mỗi khi chuyển bước, đặc biệt quan trọng
  ở Bước 3 (giải ngược, bước khó nhất module) để Athena hỗ trợ đúng lúc nếu
  học sinh hỏi giữa chừng.
- `LMS().complete({...})` — bắn đúng 1 lần khi Bước 5 hoàn thành (không chờ
  Bước 6); `items` liệt kê đủ 5 mục bắt buộc.
