# Bài 22. Ba đường conic
## Module 1: Elip — "Phòng thì thầm" (Từ thực tế → Phương trình)

> **Ghi chú build:** Module chạy SAU video Manim (đã dạy định nghĩa hình học
> MF1+MF2=2a và cách suy PT chính tắc x²/a²+y²/b²=1). Simulation đi CHIỀU
> NGƯỢC LẠI so với Manim: xuất phát từ 1 bối cảnh thực tế, học sinh TỰ đặt hệ
> trục, tự đọc dữ kiện, tự suy ra phương trình — không phải cho sẵn PT rồi
> hỏi tiêu điểm như cách làm truyền thống. Độc lập với các bài trước.

**Mục tiêu:** Học sinh tự mô hình hoá 1 bài toán thực tế (phòng hình elip)
thành PT chính tắc — tự chọn hệ trục hợp lý, tự đọc dữ kiện suy ra a, b, rồi
khám phá bằng tương tác tính chất quang học giải thích đúng tên gọi "phòng
thì thầm".

**Sai lầm cần giải quyết:**
1. Nhầm vai trò a, b — nhầm a là nửa chiều RỘNG thay vì nửa chiều DÀI (a
   luôn ứng với trục LỚN).
2. Nhầm quan hệ c²=a²−b² (elip) với c²=a²+b² (hypebol).

**Loại simulation:** B — Step-by-step (tự mô hình hoá tuần tự, Bước 1-4) kết
hợp E — Dự đoán trước khi thấy (Bước 5, khám phá quang học).

**Sổ tay kiến thức: Có** (module luyện tập, khái niệm đã dạy qua video):
```
- PT chính tắc: x²/a²+y²/b²=1 (a>b>0)
- a = nửa trục LỚN, b = nửa trục NHỎ (luôn có a>b)
- Quan hệ: c² = a² − b²  (Elip: TRỪ)
- Tiêu điểm F1(−c;0), F2(c;0); tiêu cự 2c
```

**Thời gian hoàn thành dự kiến:** ~13 phút

---

### Rà soát SGK trước khi thiết kế:
- 📖 SGK Vận dụng 1 dùng bối cảnh vòm cửa sổ nửa elip, cho sẵn PT, hỏi chiều
  cao tại 1 điểm — kỹ thuật "PT → tính giá trị". Module này đi chiều ngược
  (thực tế → PT), và đổi hẳn bối cảnh sang "phòng thì thầm" khai thác đúng
  tính chất 2 tiêu điểm mà SGK Mục 4 chỉ nhắc 1 câu, chưa có bài toán số liệu.
- Số liệu (phòng 20m×12m, a=10, b=6, c=8) khác hoàn toàn Ví dụ 2 SGK
  (a²=25,b²=16), Luyện tập 2 (a²=100,b²=64), Vận dụng 1 (16 và 4).

---

### Màn hình chính hiển thị:
- Canvas SVG: ảnh minh hoạ mặt bằng phòng hình elip (nhìn từ trên xuống,
  phong cách flat-icon, không phải ảnh chụp).
- Panel nhập liệu bên cạnh.
- Sổ tay kiến thức thu gọn phía trên canvas.

### Học sinh tương tác bằng cách:
1. Chọn vị trí đặt gốc toạ độ hợp lý trong 3 phương án.
2. Đọc dữ kiện thực tế (20m × 12m) → tự suy a, b.
3. Tự viết PT chính tắc.
4. Tính khoảng cách 2 "điểm thì thầm" (tiêu cự).
5. Khám phá tương tác tính chất quang học (không chấm điểm phần thao tác
   khám phá, chỉ chấm câu hỏi kết luận).
6. Đọc Nhận xét liên hệ hiện tượng thực tế + Tổng kết.

---

### Bảng checkpoint

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 — Đặt hệ trục | "Xem mặt bằng phòng. Chọn 1 trong 3 vị trí đặt gốc toạ độ O sao cho phương trình mô tả phòng là ĐƠN GIẢN NHẤT: (A) tâm phòng, trục Ox dọc chiều dài; (B) 1 đầu phòng; (C) 1 góc hình chữ nhật bao ngoài phòng." | "Đặt gốc tại tâm đối xứng của elip cho phương trình dạng chính tắc đơn giản nhất — các cách khác vẫn mô tả được nhưng PT phức tạp hơn nhiều." |
| 2 — Đọc dữ kiện → a, b | "Phòng dài 20m, rộng 12m. Nhập a (nửa trục lớn) và b (nửa trục nhỏ)." | "Chiều DÀI ứng với trục LỚN → a=10 (nửa của 20); chiều RỘNG ứng với trục NHỎ → b=6 (nửa của 12)." |
| 3 — Viết PT chính tắc | "Nhập PT chính tắc của elip mô tả phòng (dạng x²/…+y²/…=1)." | "Thay a²=100, b²=36 vào dạng x²/a²+y²/b²=1." |
| 4 — Quay lại thực tế | "2 'điểm thì thầm' đặt tại 2 tiêu điểm. Chúng cách nhau bao xa?" | "c²=a²−b²=100−36=64 → c=8 → 2c=16m." |
| 5 — Khám phá quang học (tương tác) | "Bấm thử 3 hướng phát âm thanh khác nhau từ F1, quan sát tia phản xạ. Sau đó trả lời: tia phản xạ luôn đi qua điểm nào?" | "Mọi tia phát từ 1 tiêu điểm, sau khi phản xạ trên elip, đều đi qua tiêu điểm còn lại." |
| 6 — Tổng kết | Đọc Nhận xét liên hệ hiện tượng "phòng thì thầm" thực tế (xem nội dung chi tiết bên dưới). | — |

---

### Cấu trúc hình vẽ / Canvas

| Bước | Cần vẽ | Thời điểm |
|---|---|---|
| 1 | Vẽ hình elip mặt bằng phòng (viền nâu/be, fill nhạt). Vẽ mờ 3 vị trí ứng viên gốc O (A: tâm; B: 1 đầu; C: góc hình chữ nhật bao ngoài) dạng chấm mờ có nhãn A/B/C. Sau khi chọn đúng (A) → hệ trục Oxy hiện rõ nét, đúng tâm | Ngay khi vào bước; hệ trục rõ nét sau khi chọn đúng |
| 2 | Giữ hệ trục đã đặt. Sau khi đúng → đánh dấu 2 đoạn: nửa chiều dài (10m, dọc Ox) và nửa chiều rộng (6m, dọc Oy), có nhãn số đo | Sau khi đúng |
| 3 | Không cần vẽ thêm — giữ nguyên hình, chỉ cần khung nhập PT | — |
| 4 | Sau khi đúng → đánh dấu 2 điểm F1(−8;0), F2(8;0) (chấm đỏ, icon loa nhỏ), vẽ đoạn nối F1F2 có nhãn "16m" | Sau khi đúng |
| 5 | Giữ nguyên elip + F1, F2. Icon nguồn âm thanh (loa nhỏ) tại F1. Học sinh bấm "Thử tia 1/2/3" → mỗi lần animate 1 tia từ F1 tới 1 điểm khác nhau trên viền elip, tự động phản xạ (tính đúng góc phản xạ hình học) đi tiếp — LUÔN đi qua F2 dù chọn hướng nào. Sau 3 lần thử riêng lẻ → chạy animation ~12-15 tia toả đều mọi hướng từ F1 cùng lúc, tất cả phản xạ hội tụ về F2 (mật độ tia dày rõ rệt tại F2). Thêm icon người (tai lắng nghe) tại F2 và 1 icon người khác ở vị trí bất kỳ KHÔNG phải tiêu điểm (giữa phòng) — tương phản: tia dồn về F2, người giữa phòng chỉ có 1-2 tia đi ngang qua | Tia đơn lẻ theo thao tác bấm; animation toả tia sau khi bấm đủ 3 lần |

**Tài sản minh hoạ:** icon loa nhỏ, icon người (tai lắng nghe, dạng đơn giản
đầu người + vòng cung tai) — vẽ bằng SVG code, không cần ảnh chụp/AI.

---

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa

**Sai lầm 1 — nhầm vai trò a, b (Bước 2):**
- Tình huống: học sinh nhập a=6, b=10 (đảo ngược, lấy chiều rộng làm a).
- Hệ thống phản hồi: sai lần 1 → shake. Sai lần 2 → gợi ý: "a luôn ứng với
  trục LỚN hơn — phòng dài hơn hay rộng hơn? Trục ứng với chiều dài đó mới
  là a."
- Kết quả rút ra: học sinh khắc sâu quy tắc a>b thay vì chỉ nhớ máy móc thứ
  tự trong đề.

**Sai lầm 2 — nhầm công thức c²=a²−b² (Bước 4):**
- Tình huống: học sinh tính c²=100+36=136 (dùng nhầm công thức hypebol).
- Hệ thống phản hồi: sai lần 1 → shake. Sai lần 2 → gợi ý: "Elip dùng TRỪ
  (c²=a²−b²), không phải CỘNG — công thức CỘNG là của hypebol, bài sau bạn
  sẽ gặp."
- Kết quả rút ra: học sinh phân biệt rõ 2 công thức ngay tại thời điểm dễ
  nhầm nhất (trước khi học hypebol ở Module 2).

---

### Giải thích kiến thức (bắt buộc mọi trạng thái)

| Bước | Khi ĐÚNG | Khi SAI |
|---|---|---|
| 1 | "Chính xác! Đặt gốc tại tâm phòng cho phương trình đối xứng, đơn giản nhất." | "Cách này vẫn mô tả được phòng, nhưng phương trình sẽ không đối xứng quanh gốc — phức tạp hơn nhiều. Hãy tìm vị trí là TÂM ĐỐI XỨNG của elip." |
| 2 | "Đúng! Chiều dài 20m → a=10 (nửa trục lớn); chiều rộng 12m → b=6 (nửa trục nhỏ)." | "Kiểm tra lại: a luôn ứng với chiều DÀI HƠN (trục lớn), không phải theo đúng thứ tự đọc trong đề." |
| 3 | "Chính xác! x²/100+y²/36=1." | "Kiểm tra lại: đã thay đúng a²=100 và b²=36 chưa?" |
| 4 | "Đúng! c²=100−36=64 → c=8 → khoảng cách 2c=16m." | "Elip dùng công thức c²=a²−b² (TRỪ), không phải cộng — công thức cộng là của hypebol." |
| 5 | "Chính xác! Mọi tia từ F1, dù hướng nào, sau khi phản xạ trên elip đều đi qua F2." | "Thử quan sát lại cả 3 lần bấm — điểm nào cả 3 tia phản xạ đều đi qua?" |
| Sau khi hoàn thành module | — | "Tổng kết: elip có a>b>0, c²=a²−b². Khi đặt hệ trục tại tâm đối xứng, phương trình về dạng chính tắc đơn giản nhất. Tính chất đặc biệt: mọi tia (ánh sáng, âm thanh) phát từ 1 tiêu điểm, sau phản xạ trên elip, đều hội tụ về tiêu điểm còn lại." |

---

### Bước 6 — Nhận xét liên hệ thực tế (đọc, sau khi hoàn thành Bước 5)

> "Chính xác — và đây là điều đặc biệt: bạn chỉ vừa thử 3 hướng, nhưng thực
> tế âm thanh thì thầm phát ra theo **VÔ SỐ hướng cùng lúc**. Theo đúng tính
> chất bạn vừa khám phá, **TẤT CẢ các hướng đó đều hội tụ về đúng 1 điểm —
> F2**. Vì vậy, dù người nói tại F1 chỉ thì thầm rất khẽ, năng lượng âm
> thanh từ mọi hướng đều dồn về đúng vị trí F2, khiến người đứng ở đó nghe
> rõ như đang nói sát tai — còn người đứng ở bất kỳ vị trí nào khác trong
> phòng (kể cả đứng giữa phòng) lại KHÔNG nghe thấy gì, vì âm thanh không
> hội tụ vào chỗ họ đứng. Đó chính là lý do căn phòng này được gọi là
> 'phòng thì thầm'."

---

### Trường dữ liệu bắt buộc

**Bước 1:**
```
dap_an_dung: A (tâm phòng)
giai_thich_dung: "Đúng! Đặt gốc tại tâm đối xứng cho PT chính tắc đơn giản nhất."
goi_y_khi_sai: "Vẫn mô tả được, nhưng PT sẽ phức tạp hơn — tìm vị trí là tâm đối xứng của elip."
```

**Bước 2:**
```
dap_an_dung: a=10, b=6
giai_thich_dung: "Đúng! Chiều dài (20m) cho a=10, chiều rộng (12m) cho b=6."
goi_y_khi_sai: "a luôn ứng với trục LỚN hơn — phòng dài hơn hay rộng hơn?"
```

**Bước 3:**
```
dap_an_dung: x²/100+y²/36=1
giai_thich_dung: "Đúng! Thay a²=100, b²=36 vào dạng chính tắc."
goi_y_khi_sai: "Kiểm tra lại a², b² đã thay đúng vào đúng vị trí chưa."
```

**Bước 4:**
```
dap_an_dung: 16 (mét)
giai_thich_dung: "Đúng! c²=100-36=64, c=8, 2c=16m."
goi_y_khi_sai: "Dùng đúng công thức c²=a²-b² của elip (không phải cộng)."
```

**Bước 5 (câu hỏi kết luận sau khám phá):**
```
dap_an_dung: F2 (tiêu điểm còn lại)
giai_thich_dung: "Đúng! Mọi tia từ 1 tiêu điểm, sau phản xạ trên elip, đều đi qua tiêu điểm còn lại."
goi_y_khi_sai: "Quan sát lại cả 3 lần bấm thử — điểm nào cả 3 tia phản xạ đều đi qua chung?"
```

---

### Bố cục Mobile
Module có 6 bước — đúng ngưỡng Mục 3.6b của `02_design_toan_final.md` (bắt
buộc lướt ngang, có `.mobile-hint`). Áp dụng bản hoà giải: vuốt ngang chỉ để
XEM LẠI thẻ đã mở khoá; việc HOÀN THÀNH/MỞ KHOÁ bước tiếp theo luôn qua 1 nút
cố định đáy màn hình, thẻ chưa mở khoá không render trong DOM. Riêng Bước 5
(khám phá): 3 nút "Thử tia 1/2/3" đặt ngay trong canvas (không phải thanh nút
đáy, vì đây là thao tác khám phá không chấm điểm) — thanh nút đáy chỉ xuất
hiện SAU khi đã bấm đủ 3 lần, hiện nút "Xem toàn cảnh" rồi mới tới câu hỏi
kết luận.

### Nút và điều khiển:
- **Kiểm tra:** xác nhận đáp án, kích hoạt hình vẽ/feedback.
- **Tiếp tục ▶ / nhãn động (mobile):** sang bước kế, chỉ hiện sau khi đúng.
- **Thử tia 1/2/3 (Bước 5):** không chấm điểm, thuần khám phá.
- **Sổ tay:** mở/đóng panel công thức.

---

## Critical Review — Tự phản biện

⚠️ Rủi ro: Bước 1 (chọn vị trí đặt hệ trục) là dạng câu hỏi mới, chưa từng
dùng ở các bài trước — cần đảm bảo cả 2 phương án sai (B, C) đều dẫn tới
phản hồi giải thích rõ TẠI SAO phức tạp hơn (không chỉ báo "sai"), để không
biến thành đoán mò 1/3.

📖 Kiểm tra caption: đã rà lại — không có dòng trống thiếu giải thích.

💡 Điểm mạnh: Bước 5 chuyển từ "đọc giải thích thụ động" sang khám phá tương
tác có kiểm chứng lặp lại (3 lần) trước khi kết luận — đúng tinh thần "quan
sát → tự đặt giả thuyết → kiểm chứng bằng câu trả lời".

---

## Rà soát trùng lặp SGK

- Bối cảnh "phòng thì thầm" hoàn toàn khác Vận dụng 1 SGK (vòm cửa sổ).
- Chiều bài toán đảo ngược (thực tế→PT) so với mọi ví dụ SGK (PT→thực tế).
- Số liệu (20m×12m, a=10,b=6,c=8) không trùng bất kỳ PT nào trong SGK.
- Bước 5 (khám phá quang học tương tác) là nội dung SGK chỉ liệt kê 1 câu ở
  Mục 4, chưa có bài toán/mô phỏng cụ thể nào — phần mở rộng độc lập.

---
**Trạng thái: ĐÃ DUYỆT — chuyển sang Giai đoạn 2 (Thiết kế giao diện) khi build.**

---

## 🔗 Athena Context & Tích hợp LMS (bắt buộc theo `02_design_toan_final.md` PHẦN 7)

> Nhân vật hướng dẫn/gợi ý trong module LUÔN gọi là **"Athena"** — không dùng
> "robot"/"AI"/tên khác, theo đúng PHẦN 7.9.

### `structure[]` — id khớp với id dùng trong code
```
[
  { "id": "b22m1-b1", "title": "Bước 1 — Đặt hệ trục (phòng thì thầm)" },
  { "id": "b22m1-b2", "title": "Bước 2 — Xác định a, b" },
  { "id": "b22m1-b3", "title": "Bước 3 — Viết PT chính tắc" },
  { "id": "b22m1-b4", "title": "Bước 4 — Tính khoảng cách 2 tiêu điểm" },
  { "id": "b22m1-b5", "title": "Bước 5 — Khám phá quang học (kết luận sau khám phá)" },
  { "id": "b22m1-b6", "title": "Bước 6 — Nhận xét & Tổng kết" }
]
```
**Bước 1–5 BẮT BUỘC** (`progress total = 5`, Bước 5 tính là 1 đơn vị ứng
đúng câu hỏi kết luận sau khám phá, không tính riêng 3 lần "Thử tia"). Bước 6
là đọc nhận xét/tổng kết, không chấm điểm, không tính vào `total`.

### `athenaGuidance` (bản nháp)
```
Module dạy học sinh tự mô hình hoá bài toán thực tế (phòng hình elip "phòng
thì thầm") thành PT chính tắc, sau đó khám phá tương tác tính chất quang
học giải thích tên gọi hiện tượng.

1) Xem mặt bằng phòng elip. Chọn 1 trong 3 vị trí đặt gốc toạ độ O sao cho
   phương trình mô tả phòng là ĐƠN GIẢN NHẤT.
   Lựa chọn: A) Tâm phòng, trục Ox dọc chiều dài  B) 1 đầu phòng
             C) 1 góc hình chữ nhật bao ngoài phòng
2) Phòng dài 20m, rộng 12m. Nhập a (nửa trục lớn) và b (nửa trục nhỏ). (câu
   điền tự do)
3) Nhập PT chính tắc của elip mô tả phòng (dạng x²/…+y²/…=1). (câu điền tự
   do)
4) 2 "điểm thì thầm" đặt tại 2 tiêu điểm. Chúng cách nhau bao xa? (câu điền
   tự do, đáp án số)
5) Bấm thử 3 hướng phát âm thanh khác nhau từ F1, quan sát tia phản xạ. Sau
   đó trả lời: tia phản xạ luôn đi qua điểm nào? (câu điền tự do/chọn, đáp
   án "F2")

Quy tắc đứng: Athena chỉ gợi ý theo đúng cột "Kiến thức áp dụng"/"Giải
thích" của từng bước, KHÔNG BAO GIỜ nói thẳng đáp án đúng khi học sinh hỏi
giữa chừng — kể cả ở Bước 5, Athena không được tiết lộ trước "F2" mà chỉ
gợi ý "hãy quan sát lại cả 3 lần bấm thử".
```

### Instrumentation cần gắn (đội build, theo Mục 7.4–7.6)
- `LMS().progress({done, total:5})`.
- `LMS().event('answered', {...})` — bắn ở Bước 1–4 và câu hỏi kết luận
  Bước 5; riêng thao tác "Thử tia 1/2/3" ở Bước 5 nên bắn
  `LMS().event('explored', {id:'b22m1-b5', trial:1|2|3})` (không phải
  `answered`, vì không chấm điểm) để Athena biết học sinh đã khám phá đủ
  chưa nếu được hỏi.
- `LMS().state({...})` — cập nhật mỗi khi chuyển bước.
- `LMS().complete({...})` — bắn đúng 1 lần sau khi Bước 6 (tổng kết) hiển
  thị; `items` liệt kê đủ 5 mục bắt buộc.
