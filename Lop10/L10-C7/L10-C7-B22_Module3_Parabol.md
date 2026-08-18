# Bài 22. Ba đường conic
## Module 3: Parabol — "Gương đèn pha ô tô" (Từ thực tế → Phương trình)

> **Ghi chú build:** Module chạy SAU video Manim (đã dạy định nghĩa hình học
> cách đều tiêu điểm F và đường chuẩn Δ, PT chính tắc y²=2px). Simulation đi
> chiều ngược: xuất phát từ số đo kỹ thuật thực tế của gương đèn pha, học
> sinh tự đặt hệ trục, tự suy PT, rồi khám phá tương tác tính chất quang học
> (tia phản xạ song song) — analogous với Module 1 (Elip). Độc lập với M1, M2.

**Mục tiêu:** Học sinh tự mô hình hoá gương đèn pha (mặt cắt parabol) thành
PT chính tắc từ số đo kỹ thuật (khẩu độ, độ sâu), rồi khám phá bằng tương
tác tính chất "tia phản xạ song song" lý giải vì sao đèn pha chiếu xa được.

**Sai lầm cần giải quyết:**
1. Nhầm toạ độ tiêu điểm F(p/2;0) với F(p;0).
2. Lúng túng xác định trục đối xứng & chiều mở của parabol khi đặt hệ trục.

**Loại simulation:** B — Step-by-step (tự mô hình hoá tuần tự, Bước 1-5) kết
hợp E — Dự đoán trước khi thấy (Bước 6, khám phá quang học — analogous M1).

**Sổ tay kiến thức: Có** (module luyện tập, khái niệm đã dạy qua video):
```
- PT chính tắc: y² = 2px (p>0, trục đối xứng Ox, mở về bên phải)
- Tiêu điểm F(p/2; 0), đường chuẩn Δ: x = −p/2
- Lưu ý: F ở p/2, KHÔNG phải p
```

**Thời gian hoàn thành dự kiến:** ~13 phút

---

### Rà soát SGK trước khi thiết kế:
- 📖 SGK: Ví dụ 5 (parabol y²=x, tìm tiêu điểm/đường chuẩn/điểm cách F 1
  khoảng cho trước). Mục 4 liệt kê "đèn pha đáy parabol" (Hình 7.32c) và nêu
  đúng nguyên lý phản xạ (Hình 7.31: tia từ tiêu điểm phản xạ vuông góc với
  đường chuẩn = song song trục) nhưng KHÔNG có bài toán số liệu cụ thể nào
  cho đèn pha — module này xây trọn vẹn thành bài toán hoàn chỉnh.
- Số liệu (khẩu độ 24cm, độ sâu 4cm → p=18) khác hoàn toàn Ví dụ 5 SGK
  (y²=x, p=1/2) và mọi PT khác trong SGK.
- Bước 6 (khám phá tia song song) là mô phỏng hoá đúng Hình 7.31 SGK — SGK
  chỉ có 1 hình tĩnh minh hoạ, không có tương tác nào.

---

### Màn hình chính hiển thị:
- **Bối cảnh mở đầu (Bước 0, không chấm điểm):** 1 ảnh minh hoạ tĩnh (SVG
  illustrative, phong cách "cảnh đêm") — mặt cắt đèn pha ô tô ban đêm, gương
  parabol, bóng đèn tại tiêu điểm, chùm tia song song chiếu sáng đường — dùng
  để giới thiệu bối cảnh trước khi vào phần tính toán. **Đây là ảnh minh hoạ
  atmosphere, KHÔNG phải sơ đồ toạ độ chính xác** — không dùng để đọc số liệu.
- **Từ Bước 1 trở đi:** chuyển sang canvas SVG toạ độ Oxy chuẩn (lưới mờ,
  đồng bộ phong cách M1, M2) — đây mới là sơ đồ dùng để tính toán.
- Panel nhập liệu bên cạnh; Sổ tay kiến thức thu gọn phía trên canvas.

### Học sinh tương tác bằng cách:
0. Xem ảnh bối cảnh (không chấm điểm) — chuyển cảnh sang sơ đồ toạ độ.
1. Chọn vị trí đặt hệ trục & trục đối xứng đúng.
2. Chuyển số đo kỹ thuật (khẩu độ, độ sâu) thành 1 điểm toạ độ trên parabol.
3. Giải tìm p, viết PT chính tắc.
4. Quay lại thực tế: xác định vị trí đặt bóng đèn (tiêu điểm).
5. Mở rộng: tính bán kính gương tại 1 độ sâu khác.
6. Khám phá tương tác tính chất quang học (không chấm điểm phần khám phá,
   chỉ chấm câu hỏi kết luận).
7. Đọc Nhận xét liên hệ thực tế + Tổng kết.

---

### Bảng checkpoint

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 — Đặt hệ trục | "Xem mặt cắt gương đèn pha. Chọn cách đặt hệ trục: (A) đỉnh gương tại O, trục đối xứng NGANG theo hướng chiếu sáng (Ox); (B) đỉnh gương tại O, trục đối xứng DỌC (Oy); (C) gốc tại miệng gương." | "Đúng bẫy PPCT: chọn (A) — trục đối xứng phải trùng hướng chiếu sáng (Ox) để PT có dạng chính tắc y²=2px." |
| 2 — Xác định điểm trên parabol | "Gương có khẩu độ (đường kính miệng) 24cm, độ sâu 4cm. Nhập toạ độ 1 điểm trên viền gương (x=độ sâu, y=bán kính)." | "Bán kính = nửa khẩu độ = 12cm. Điểm trên viền gương tại độ sâu 4cm là (4;12)." |
| 3 — Tìm p, viết PT | "Thay điểm (4;12) vào y²=2px, nhập p và PT chính tắc." | "144=2p·4=8p → p=18 → PT: y²=36x." |
| 4 — Quay lại thực tế | "Nên đặt bóng đèn cách đỉnh gương bao xa để ánh sáng phản xạ song song?" | "Tiêu điểm F(p/2;0)=(9;0) — cách đỉnh gương 9cm. LƯU Ý: không phải p=18cm." |
| 5 — Mở rộng | "Tại độ sâu x=2cm (gần đỉnh hơn), bán kính gương là bao nhiêu?" | "y²=36×2=72 → y=6√2≈8,49cm." |
| 6 — Khám phá quang học (tương tác) | "Bấm thử 3 điểm phản xạ khác nhau trên gương, quan sát tia ra. Sau đó trả lời: các tia phản xạ có đặc điểm chung gì?" | "Mọi tia phát từ tiêu điểm, sau phản xạ trên parabol, đều trở thành các tia SONG SONG với trục đối xứng." |
| 7 — Tổng kết | Đọc Nhận xét liên hệ đèn pha thực tế (xem nội dung chi tiết bên dưới). | — |

---

### Cấu trúc hình vẽ / Canvas (2 lớp: ảnh bối cảnh vs sơ đồ toạ độ)

> **Nguyên tắc:** tách rõ 2 vai trò hình ảnh — (1) ảnh minh hoạ bối cảnh
> (illustrative, đẹp, KHÔNG cần chính xác toạ độ) chỉ dùng ở Bước 0 mở đầu
> và có thể dùng lại phong cách tương tự (thu gọn) ở Bước 6 khám phá; (2) sơ
> đồ Oxy chính xác (lưới toạ độ, phong cách flat-icon tối giản đồng bộ M1/M2)
> dùng cho MỌI bước tính toán Bước 1-5 — không trộn lẫn 2 loại trong cùng 1
> bước để tránh học sinh nhầm ảnh minh hoạ là dữ liệu cần đọc số.

| Bước | Cần vẽ | Loại | Thời điểm |
|---|---|---|---|
| 0 | Cảnh đêm: bầu trời tối (gradient đơn, tối→hơi sáng ở chân trời), mặt đường có vạch kẻ đứt, silhouette ô tô đơn giản (thân xe + 2 bánh), cụm đèn pha gắn gương parabol cách điệu, bóng đèn phát sáng tại tiêu điểm, các tia phản xạ song song tạo dải sáng mờ chiếu trên đường. Nhãn chú thích: "Bóng đèn tại tiêu điểm F", "Gương parabol", "Tia phản xạ song song" | Illustrative (SVG nghệ thuật, màu thực: navy, vàng ấm, xám kim loại) | Hiện tĩnh, học sinh bấm "Bắt đầu tính toán" để chuyển sang sơ đồ Oxy |
| 1 | Sơ đồ Oxy: vẽ đường cong gương (parabol cách điệu, viền xám bạc) đặt SẴN trên canvas (chưa gắn trục). Vẽ mờ 3 vị trí ứng viên trục (A/B/C) dạng mũi tên mờ có nhãn. Sau khi chọn đúng (A) → trục Ox/Oy hiện rõ, đúng tại đỉnh gương, Ox theo hướng mở | Sơ đồ toạ độ (lưới mờ) | Trục rõ sau khi chọn đúng |
| 2 | Giữ hệ trục. Sau khi đúng → đánh dấu điểm (4;12) trên viền gương (chấm xanh), có đường dóng từ điểm tới 2 trục, nhãn toạ độ | Sơ đồ toạ độ | Sau khi đúng |
| 3 | Không cần vẽ thêm | — | — |
| 4 | Sau khi đúng → đánh dấu tiêu điểm F(9;0) trên trục Ox (chấm đỏ, icon bóng đèn nhỏ) | Sơ đồ toạ độ | Sau khi đúng |
| 5 | Sau khi đúng → đánh dấu thêm điểm tại x=2 trên viền gương (chấm tím), nhãn y≈8,49 | Sơ đồ toạ độ | Sau khi đúng |
| 6 | Quay lại phong cách illustrative thu gọn (chỉ gương + bóng đèn, KHÔNG cần cả xe/đường): gương parabol cách điệu, bóng đèn tại F. Học sinh bấm "Thử điểm 1/2/3" — mỗi lần chọn 1 điểm khác trên gương, animate 1 tia từ F tới điểm đó rồi phản xạ ra thành tia NGANG (song song trục). Sau 3 lần thử → chạy animation ~12-15 tia toả mọi hướng từ F, tất cả phản xạ thành chùm tia song song đồng thời (hiệu ứng "chùm sáng" rõ rệt, có dải sáng mờ overlay phía sau chùm tia) | Illustrative (thu gọn) | Tia đơn lẻ theo thao tác bấm; animation chùm sau khi bấm đủ 3 lần |

**Tài sản minh hoạ:** icon bóng đèn nhỏ (2 hình tròn lồng, vàng ấm), icon
ô tô đơn giản (2-3 hình khối) — vẽ bằng SVG code (đã có mockup xác nhận khả
thi), không cần ảnh chụp/AI thực.

---

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa

**Sai lầm 1 — nhầm trục/chiều mở (Bước 1):**
- Tình huống: học sinh chọn (B) hoặc (C) vì chưa quen tự đặt hệ trục.
- Hệ thống phản hồi: nếu chọn (B) → "Nếu đặt trục đối xứng DỌC, PT sẽ có
  dạng x²=2py — vẫn đúng toán học nhưng không khớp hướng chiếu sáng thực tế
  (ngang). Hãy chọn trục NGANG theo đúng hướng ánh sáng đi ra." Nếu chọn (C)
  → "Gốc tại miệng gương khiến đỉnh gương không còn ở O — PT sẽ phức tạp hơn
  nhiều, không còn dạng chính tắc đơn giản."
- Kết quả rút ra: học sinh hiểu việc đặt trục không chỉ là quy ước toán học
  mà cần khớp với ý nghĩa vật lý của hướng chiếu sáng.

**Sai lầm 2 — nhầm F(p/2;0) với F(p;0) (Bước 4):**
- Tình huống: học sinh nhập ngay 18 (giá trị p vừa tính) làm khoảng cách đặt
  bóng đèn, thay vì 9.
- Hệ thống phản hồi: sai lần 1 → shake. Sai lần 2 → gợi ý: "Tiêu điểm của
  y²=2px là F(p/2;0), KHÔNG phải F(p;0) — bạn vừa tính p=18, hãy chia đôi
  trước khi lấy làm khoảng cách."
- Kết quả rút ra: học sinh khắc sâu công thức F(p/2;0) ngay tại thời điểm dễ
  nhầm nhất (vừa tính xong p, còn nhớ rõ số 18 trong đầu).

---

### Giải thích kiến thức (bắt buộc mọi trạng thái)

| Bước | Khi ĐÚNG | Khi SAI |
|---|---|---|
| 1 | "Chính xác! Trục đối xứng ngang theo đúng hướng ánh sáng, đỉnh gương tại O cho PT chính tắc y²=2px đơn giản nhất." | "Cách này vẫn có PT mô tả được, nhưng không đúng dạng chính tắc đơn giản khớp hướng chiếu sáng — hãy chọn trục NGANG tại đỉnh gương." |
| 2 | "Đúng! Bán kính = nửa khẩu độ = 12cm, tại độ sâu 4cm → điểm (4;12)." | "Kiểm tra lại: khẩu độ là ĐƯỜNG KÍNH miệng gương — bán kính phải chia đôi trước khi lấy làm toạ độ y." |
| 3 | "Chính xác! 144=8p → p=18 → y²=36x." | "Kiểm tra lại: đã thay đúng x=4, y=12 vào y²=2px chưa?" |
| 4 | "Đúng! F(9;0) — cách đỉnh gương 9cm, đúng bằng p/2." | "Tiêu điểm là F(p/2;0), không phải F(p;0) — bạn vừa tính p=18, hãy chia đôi." |
| 5 | "Chính xác! y=6√2≈8,49cm." | "Kiểm tra lại: đã thay đúng x=2 vào PT y²=36x chưa?" |
| 6 | "Chính xác! Mọi tia từ tiêu điểm, sau phản xạ trên parabol, đều song song với trục đối xứng." | "Quan sát lại cả 3 lần bấm — các tia ra ngoài có cùng hướng không, dù xuất phát điểm phản xạ khác nhau?" |
| Sau khi hoàn thành module | — | "Tổng kết: parabol y²=2px có tiêu điểm F(p/2;0) — luôn nhớ chia đôi p, không lấy trực tiếp. Trục đối xứng phải đặt đúng theo hướng vật lý của bài toán (ở đây là hướng chiếu sáng). Tính chất đặc biệt: mọi tia phát từ tiêu điểm, sau phản xạ trên parabol, đều trở thành các tia song song — đây là lý do gương đèn pha có dạng parabol." |

---

### Bước 7 — Nhận xét liên hệ thực tế (đọc, sau khi hoàn thành Bước 6)

> "Chính xác — và đây là lý do gương đèn pha luôn có dạng parabol chứ không
> phải hình cầu hay hình phẳng: đặt bóng đèn đúng tại tiêu điểm F, ánh sáng
> phát ra theo **VÔ SỐ hướng cùng lúc** đều được gương biến thành **các tia
> SONG SONG** hướng thẳng về phía trước. Nếu dùng gương cầu (hình tròn) thay
> vì parabol, các tia phản xạ sẽ không song song mà toả rộng dần — ánh sáng
> yếu đi nhanh theo khoảng cách, xe chỉ nhìn rõ đường ở cự ly gần. Nhờ chùm
> tia song song của gương parabol, đèn pha ô tô giữ được cường độ sáng mạnh
> ngay cả ở khoảng cách xa phía trước xe."

---

### Trường dữ liệu bắt buộc

**Bước 1:**
```
dap_an_dung: A (trục ngang tại đỉnh gương)
giai_thich_dung: "Đúng! Trục ngang theo đúng hướng chiếu sáng cho PT chính tắc đơn giản."
goi_y_khi_sai: "Hãy chọn trục NGANG theo đúng hướng ánh sáng đi ra, gốc tại đỉnh gương."
```

**Bước 2:**
```
dap_an_dung: (4;12)
giai_thich_dung: "Đúng! Bán kính = nửa khẩu độ = 12cm, tại độ sâu 4cm."
goi_y_khi_sai: "Khẩu độ là đường kính — bán kính (toạ độ y) phải chia đôi trước."
```

**Bước 3:**
```
dap_an_dung: p=18; y²=36x
giai_thich_dung: "Đúng! 144=8p → p=18 → PT y²=36x."
goi_y_khi_sai: "Thay x=4, y=12 vào y²=2px rồi giải p."
```

**Bước 4:**
```
dap_an_dung: 9 (cm)
giai_thich_dung: "Đúng! F(p/2;0)=(9;0), cách đỉnh gương 9cm."
goi_y_khi_sai: "Tiêu điểm là F(p/2;0) — chia đôi p=18 trước khi lấy làm khoảng cách."
```

**Bước 5:**
```
dap_an_dung: 6√2 (≈8.49 cm)
giai_thich_dung: "Đúng! y²=36×2=72 → y=6√2≈8,49cm."
goi_y_khi_sai: "Thay x=2 vào PT y²=36x vừa lập ở Bước 3."
```

**Bước 6 (câu hỏi kết luận sau khám phá):**
```
dap_an_dung: Song song (với trục đối xứng)
giai_thich_dung: "Đúng! Mọi tia từ tiêu điểm, sau phản xạ trên parabol, đều song song với trục."
goi_y_khi_sai: "Quan sát lại 3 lần bấm — các tia ra ngoài có cùng hướng không?"
```

---

### Bố cục Mobile
Module có 7 bước (0-6) — đúng ngưỡng Mục 3.6b của `02_design_toan_final.md`
(bắt buộc lướt ngang, có `.mobile-hint`). Áp dụng bản hoà giải: vuốt ngang
chỉ để XEM LẠI thẻ đã mở khoá; việc HOÀN THÀNH/MỞ KHOÁ bước tiếp theo luôn
qua 1 nút cố định đáy màn hình, thẻ chưa mở khoá không render trong DOM.
Bước 0 (ảnh bối cảnh) và Bước 6 (khám phá) không có nút "Kiểm tra" trong
thanh nút đáy — thay bằng nút "Bắt đầu tính toán" / "Thử điểm 1/2/3" đặt
ngay trong canvas, giống thiết kế đã dùng ở Module 1 Bước 5.

### Nút và điều khiển:
- **Bắt đầu tính toán (Bước 0):** chuyển từ ảnh bối cảnh sang sơ đồ Oxy.
- **Kiểm tra:** xác nhận đáp án, kích hoạt hình vẽ/feedback.
- **Tiếp tục ▶ / nhãn động (mobile):** sang bước kế, chỉ hiện sau khi đúng.
- **Thử điểm 1/2/3 (Bước 6):** không chấm điểm, thuần khám phá.
- **Sổ tay:** mở/đóng panel công thức.

---

## Critical Review — Tự phản biện

⚠️ Rủi ro: Bước 0 (ảnh bối cảnh illustrative) và Bước 1 (sơ đồ toạ độ) dùng
2 phong cách vẽ khác hẳn nhau (nghệ thuật có màu thực vs sơ đồ lưới tối
giản) — cần chuyển cảnh mượt (fade/transition) để không gây cảm giác "nhảy"
đột ngột giữa 2 phong cách, ảnh hưởng trải nghiệm.

📖 Kiểm tra caption: đã rà lại — không có dòng trống thiếu giải thích.

💡 Điểm mạnh: đã kiểm chứng khả năng vẽ thực tế bằng mockup SVG hoàn chỉnh
(cảnh đêm, ô tô, gương, chùm tia song song) trước khi đưa vào kịch bản —
xác nhận khả thi về mặt kỹ thuật lẫn thẩm mỹ trước khi giao cho đội build.

---

## Rà soát trùng lặp SGK

- Bối cảnh "gương đèn pha" được SGK Mục 4 nhắc tên + có 1 câu nguyên lý
  (Hình 7.31, 7.32c) nhưng không có bài toán số liệu — module này xây mới
  hoàn toàn.
- Số liệu (khẩu độ 24cm, độ sâu 4cm, p=18) không trùng Ví dụ 5 SGK (y²=x).
- Bước 6 (khám phá tia song song tương tác) mô phỏng hoá Hình 7.31 SGK
  (vốn chỉ là 1 hình tĩnh) thành trải nghiệm tương tác — phần mở rộng độc
  lập, không sao chép.

---
**Trạng thái: ĐÃ DUYỆT — chuyển sang Giai đoạn 2 (Thiết kế giao diện) khi build.**

---

## 🔗 Athena Context & Tích hợp LMS (bắt buộc theo `02_design_toan_final.md` PHẦN 7)

> Nhân vật hướng dẫn/gợi ý trong module LUÔN gọi là **"Athena"** — không dùng
> "robot"/"AI"/tên khác, theo đúng PHẦN 7.9.

### `structure[]` — id khớp với id dùng trong code
```
[
  { "id": "b22m3-b0", "title": "Bước 0 — Ảnh bối cảnh (không chấm điểm)" },
  { "id": "b22m3-b1", "title": "Bước 1 — Đặt hệ trục (gương đèn pha)" },
  { "id": "b22m3-b2", "title": "Bước 2 — Xác định điểm trên parabol" },
  { "id": "b22m3-b3", "title": "Bước 3 — Tìm p, viết PT" },
  { "id": "b22m3-b4", "title": "Bước 4 — Xác định vị trí đặt bóng đèn" },
  { "id": "b22m3-b5", "title": "Bước 5 — Mở rộng: bán kính tại độ sâu khác" },
  { "id": "b22m3-b6", "title": "Bước 6 — Khám phá quang học (kết luận sau khám phá)" },
  { "id": "b22m3-b7", "title": "Bước 7 — Nhận xét & Tổng kết" }
]
```
**Bước 1–4, 6 BẮT BUỘC** (`progress total = 5`). **Bước 0** (ảnh bối cảnh,
không chấm điểm) và **Bước 5** (mở rộng) KHÔNG BẮT BUỘC — không tính vào
`total`. **Bước 7** là đọc nhận xét/tổng kết, không chấm điểm.

### `athenaGuidance` (bản nháp)
```
Module dạy học sinh tự mô hình hoá gương đèn pha ô tô (mặt cắt parabol)
thành PT chính tắc từ số đo kỹ thuật, sau đó khám phá tương tác tính chất
quang học (tia phản xạ song song) giải thích vì sao đèn pha chiếu xa được.

1) Xem mặt cắt gương đèn pha. Chọn cách đặt hệ trục.
   Lựa chọn: A) Đỉnh gương tại O, trục đối xứng NGANG theo hướng chiếu sáng
             B) Đỉnh gương tại O, trục đối xứng DỌC
             C) Gốc tại miệng gương
2) Gương có khẩu độ (đường kính miệng) 24cm, độ sâu 4cm. Nhập toạ độ 1 điểm
   trên viền gương (x=độ sâu, y=bán kính). (câu điền tự do)
3) Thay điểm vừa tìm vào y²=2px, nhập p và PT chính tắc. (câu điền tự do)
4) Nên đặt bóng đèn cách đỉnh gương bao xa để ánh sáng phản xạ song song?
   (câu điền tự do, đáp án số — bẫy nhầm F(p/2;0) với F(p;0))
5) (không bắt buộc) Tại độ sâu x=2cm (gần đỉnh hơn), bán kính gương là bao
   nhiêu? (câu điền tự do, đáp án số)
6) Bấm thử 3 điểm phản xạ khác nhau trên gương, quan sát tia ra. Sau đó trả
   lời: các tia phản xạ có đặc điểm chung gì? (câu điền tự do/chọn, đáp án
   "song song")

Quy tắc đứng: Athena chỉ gợi ý theo đúng cột "Kiến thức áp dụng"/"Giải
thích" của từng bước (VD "tiêu điểm là F(p/2;0), không phải F(p;0)"),
KHÔNG BAO GIỜ nói thẳng đáp án đúng khi học sinh hỏi giữa chừng — kể cả ở
Bước 6, Athena không được tiết lộ trước "song song" mà chỉ gợi ý "hãy quan
sát lại cả 3 lần bấm thử".
```

### Instrumentation cần gắn (đội build, theo Mục 7.4–7.6)
- `LMS().progress({done, total:5})` — Bước 0 và Bước 5 không cộng vào
  `total`.
- `LMS().event('answered', {...})` — bắn ở Bước 1–4 và câu hỏi kết luận
  Bước 6; thao tác "Thử điểm 1/2/3" ở Bước 6 bắn
  `LMS().event('explored', {id:'b22m3-b6', trial:1|2|3})` (không phải
  `answered`).
- `LMS().state({...})` — cập nhật mỗi khi chuyển bước, bao gồm việc đã
  chuyển từ Bước 0 (ảnh bối cảnh) sang Bước 1 (sơ đồ Oxy) hay chưa.
- `LMS().complete({...})` — bắn đúng 1 lần sau khi Bước 7 (tổng kết) hiển
  thị; `items` liệt kê đủ 5 mục bắt buộc (Bước 1–4, 6).
