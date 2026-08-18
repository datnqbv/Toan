# Bài 22. Ba đường conic
## Module 4: Ứng dụng tổng hợp — "Chọn đúng đường conic" (Role-play)

> **Ghi chú build:** Module KHÔNG có video Manim — đây là module duy nhất
> yêu cầu simulation gánh trọn vai trò dạy + luyện + ứng dụng ở tầng cao
> nhất (PPCT: "vận dụng và vận dụng cao"). Học sinh đóng vai kỹ sư/nhà khoa
> học, được giao nguyên đề bài thực tế — độ tự chủ TĂNG DẦN qua 3 nhiệm vụ
> (không ngắt bước nhỏ như M1-M3), chỉ nộp đáp án cuối mỗi nhiệm vụ, nút
> "Xin gợi ý" ẩn sẵn (không tự động hiện). Độc lập với M1-M3, không dùng lại
> state.

**Mục tiêu:** Học sinh tự nhận diện đúng loại đường conic phù hợp với 1 tình
huống thực tế cho trước (không được gợi ý sẵn "đây là bài elip/hypebol/
parabol"), tự thiết lập và giải bài toán hoàn chỉnh với độ tự chủ tăng dần,
rồi tự tổng kết bảng phân loại 3 đường conic.

**Sai lầm cần giải quyết:**
1. Nhận dạng sai loại conic khi dữ kiện/phương trình chưa ở dạng chính tắc
   chuẩn.
2. Quên rằng dấu hiệu định nghĩa (tổng/hiệu khoảng cách không đổi, hay cách
   đều 1 điểm và 1 đường) chính là chìa khoá để chọn đúng loại conic — không
   thể chỉ đoán theo "cảm giác" bối cảnh.

**Loại simulation:** D — Kiểm tra nghiệm (Vòng khởi động) kết hợp
F — Xây dựng ngược, độ tự chủ tăng dần (3 Nhiệm vụ chính).

**Sổ tay kiến thức: Có** (module tổng hợp, kế thừa công thức từ cả 3 module
trước — hiển thị ĐẦY ĐỦ, không giấu bớt vì đây là bài tổng hợp cần tra cứu
qua lại giữa 3 loại):
```
- ELIP: x²/a²+y²/b²=1 (a>b>0). MF1+MF2=2a. c²=a²−b².
- HYPEBOL: x²/a²−y²/b²=1. |MF1−MF2|=2a. c²=a²+b².
- PARABOL: y²=2px (p>0). MF=d(M,Δ). F(p/2;0), Δ: x=−p/2.
```

**Thời gian hoàn thành dự kiến:** ~15 phút (module dài nhất, tổng hợp cả bài)

---

### Rà soát SGK trước khi thiết kế:
- 📖 SGK Mục 4 liệt kê Kepler (elip), gợi ý LORAN (hypebol, đã có ở Bài tập
  7.24 với số liệu khác), ăng-ten vệ tinh (parabol) — chỉ dạng liệt kê ý
  tưởng, không có bài toán số liệu hoàn chỉnh dạng role-play nào.
- Số liệu 3 nhiệm vụ (2-8 AU; 200km/0,0004s; khẩu độ 3m/sâu 0,5m) đều khác
  hoàn toàn mọi PT/số liệu trong SGK — đặc biệt Nhiệm vụ 2 đã đổi khác Bài
  tập 7.24 SGK (300km, 292.000km/s, 0,0005s).
- Vòng khởi động "nhận dạng nhanh" hiện thực hoá đúng gợi ý PPCT ("Trò chơi
  Nhận dạng conic: PT hoặc hình ảnh, HS phân loại") — SGK không có hoạt động
  này, phần mở rộng độc lập.

---

### Cấu trúc tổng thể:
```
Vòng khởi động (Nhận dạng nhanh, có chấm điểm nhẹ)
  → Nhiệm vụ 1: Nhà thiên văn (Elip) — scaffold NHIỀU
  → Nhiệm vụ 2: Kỹ sư LORAN (Hypebol) — scaffold ÍT HƠN
  → Nhiệm vụ 3: Kỹ sư ăng-ten (Parabol) — scaffold GẦN NHƯ KHÔNG
  → Bảng tổng kết (học sinh tự điền, đối chiếu 3 loại)
```

### Màn hình chính hiển thị:
- Canvas SVG toạ độ Oxy dùng chung cho cả 3 nhiệm vụ (mỗi nhiệm vụ tự vẽ lại
  khi bắt đầu).
- Panel đề bài: hiển thị NGUYÊN VĂN đề bài thực tế (không tách nhỏ từng
  bước), 1 khung nhập đáp án cuối cùng (PT chính tắc hoặc giá trị yêu cầu),
  nút "Nộp đáp án" và nút "Xin gợi ý" (ẩn/hiện tuỳ mức độ nhiệm vụ).
- Sổ tay kiến thức luôn có sẵn (đủ 3 công thức, vì đây là bài tổng hợp).

---

### Bảng checkpoint

**Vòng khởi động — Nhận dạng nhanh (4 câu, D-type, có giải thích ngay):**

| Câu | PT cho | Đáp án đúng | Bẫy |
|---|---|---|---|
| KĐ.1 | 4x²+9y²=36 | Elip (chia 36: x²/9+y²/4=1) | PT chưa chuẩn hoá — phải chia để đưa về dạng =1 mới nhận dạng được |
| KĐ.2 | 9x²−4y²=36 | Hypebol (x²/4−y²/9=1) | Tương tự — dấu trừ giữ nguyên nhưng vẫn cần chia chuẩn hoá |
| KĐ.3 | y²=8x | Parabol (đã chuẩn, p=4) | Câu dễ, xác nhận đọc đúng dạng đã chuẩn |
| KĐ.4 | 2x²+2y²−8=0 | KHÔNG thuộc 3 loại đã học (đây là đường tròn, x²+y²=4) | Bẫy nhận dạng nhầm — kiểm tra học sinh có máy móc ép vào 1 trong 3 loại không |

**Nhiệm vụ 1 — Nhà thiên văn (Elip), scaffold NHIỀU:**
- **Đề bài:** "Một hành tinh quay quanh 1 ngôi sao theo quỹ đạo elip, ngôi
  sao nằm tại 1 tiêu điểm. Khoảng cách gần nhất (điểm cận tinh) là 2 AU, xa
  nhất (điểm viễn tinh) là 8 AU. Lập phương trình chính tắc mô tả quỹ đạo."
- **Gợi ý LUÔN hiển thị sẵn (không cần bấm xin):** "Gợi ý: khoảng cách gần
  nhất = a−c, khoảng cách xa nhất = a+c."
- **Đáp án:** a=5, c=3, b=4 → x²/25+y²/16=1.
- **Nút "Xin thêm gợi ý" (cấp 2, ẩn):** "Từ 2 phương trình a−c=2 và a+c=8,
  cộng lại để tìm a, trừ đi để tìm c."

**Nhiệm vụ 2 — Kỹ sư định vị LORAN (Hypebol), scaffold ÍT HƠN:**
- **Đề bài:** "2 trạm phát sóng A, B cách nhau 200km. 1 tàu thu tín hiệu từ
  A sớm hơn từ B đúng 0,0004 giây (vận tốc sóng vô tuyến 300.000 km/s). Xác
  định phương trình chính tắc của nhánh hypebol chứa vị trí tàu."
- **Gợi ý:** KHÔNG hiển thị sẵn. Chỉ có nút "Xin gợi ý" ẩn (cấp 1): "Hiệu
  khoảng cách từ tàu tới 2 trạm liên hệ thế nào với 2a? Vận tốc × thời gian
  lệch cho ra đại lượng gì?"
- **Đáp án:** 2c=200 (c=100), 2a=vận tốc×thời gian lệch=300000×0,0004=120
  (a=60), b²=c²−a²=10000−3600=6400 (b=80) → x²/3600−y²/6400=1.

**Nhiệm vụ 3 — Kỹ sư ăng-ten (Parabol), GẦN NHƯ KHÔNG gợi ý:**
- **Đề bài:** "Ăng-ten vệ tinh dạng chảo parabol, đường kính miệng chảo 3m,
  độ sâu đáy chảo 0,5m. Xác định khoảng cách từ đỉnh chảo đến vị trí cần đặt
  đầu thu tín hiệu."
- **Gợi ý:** Nút "Xin gợi ý" ẩn, CHỈ hiện gợi ý cấp thấp nhất khi bấm: "Đây
  là loại đường conic nào? Đặt hệ trục ở đâu để bài toán đơn giản nhất?"
  (không đưa công thức, chỉ định hướng loại bài).
- **Đáp án:** điểm trên viền chảo (0,5; 1,5) [bán kính=1,5m tại độ sâu 0,5m]
  → 1,5²=2p×0,5 → 2,25=p → F cách đỉnh p/2=1,125m.

**Bảng tổng kết (học sinh tự điền, không có sẵn đáp án gợi ý):**

| Loại | Tính chất định nghĩa | PT chính tắc | Nhiệm vụ vừa gặp |
|---|---|---|---|
| Elip | ? | ? | ? |
| Hypebol | ? | ? | ? |
| Parabol | ? | ? | ? |

---

### Cấu trúc hình vẽ / Canvas

| Phần | Cần vẽ | Thời điểm |
|---|---|---|
| Vòng khởi động | Không cần hình — thuần nhận dạng PT bằng chữ số, giữ tốc độ nhanh cho vòng khởi động | — |
| Nhiệm vụ 1 | Canvas Oxy: vẽ ngôi sao (chấm vàng, icon tia sáng nhỏ) tại 1 tiêu điểm. Sau khi nộp đúng → vẽ quỹ đạo elip đầy đủ, đánh dấu 2 điểm cận tinh/viễn tinh trên trục | Quỹ đạo hiện sau khi đúng |
| Nhiệm vụ 2 | Canvas Oxy: 2 icon trạm phát sóng (ăng-ten nhỏ) tại A, B đối xứng qua O. Sau khi nộp đúng → vẽ 1 nhánh hypebol (nhánh gần A hơn, đúng nghĩa "tín hiệu từ A đến sớm hơn"), đánh dấu icon tàu thuyền tại 1 điểm mẫu trên nhánh | Nhánh hypebol hiện sau khi đúng |
| Nhiệm vụ 3 | Canvas Oxy: vẽ mặt cắt chảo ăng-ten (đường cong parabol cách điệu, viền kim loại). Sau khi nộp đúng → đánh dấu tiêu điểm F + icon đầu thu tín hiệu tại đúng vị trí | Đầu thu hiện sau khi đúng |
| Bảng tổng kết | Không cần hình — bảng text thuần | — |

**Tài sản minh hoạ:** icon ngôi sao, icon ăng-ten trạm phát, icon tàu thuyền
nhỏ, icon đầu thu tín hiệu — đều vẽ bằng SVG code đơn giản (2-3 hình khối
mỗi icon), đồng bộ phong cách M1-M3, không cần ảnh chụp/AI.

---

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa

**Sai lầm — nhận dạng sai khi PT chưa chuẩn hoá (Vòng khởi động):**
- Tình huống: học sinh thấy "4x²+9y²=36" có cả x² và y² dương, vội đoán elip
  mà không chia chuẩn hoá — may mắn đúng loại nhưng chưa chắc hiểu TẠI SAO;
  rủi ro hơn ở câu 9x²−4y²=36 nếu học sinh không chia mà đọc nhầm hệ số.
- Hệ thống phản hồi: dù chọn đúng loại, VẪN hỏi thêm "Bạn có chia 2 vế để
  đưa PT về đúng dạng x²/a²+y²/b²=1 trước khi kết luận không?" — xác nhận
  quy trình, không chỉ chấm đúng/sai kết quả cuối.
- Kết quả rút ra: học sinh hình thành thói quen LUÔN chuẩn hoá PT trước khi
  nhận dạng, không đoán theo cảm giác hình thức.

**Sai lầm — áp đặt máy móc phải thuộc 1 trong 3 loại (Câu KĐ.4):**
- Tình huống: học sinh cố ép 2x²+2y²−8=0 vào 1 trong 3 loại (thường chọn
  nhầm elip vì "có cả x² y² dương").
- Hệ thống phản hồi: "Kiểm tra lại: hệ số của x² và y² có BẰNG NHAU không?
  Đó là dấu hiệu của 1 loại đường khác (đường tròn) mà bài này chưa học tới."
- Kết quả rút ra: học sinh không áp đặt máy móc, biết giới hạn phạm vi kiến
  thức đã học.

---

### Giải thích kiến thức (bắt buộc mọi trạng thái)

| Phần | Khi ĐÚNG | Khi SAI |
|---|---|---|
| KĐ.1, KĐ.2 | "Chính xác! Sau khi chia chuẩn hoá, đây đúng là dạng [Elip/Hypebol]." | "Hãy chia cả 2 vế cho hằng số bên phải để đưa về dạng chuẩn =1 trước khi nhận dạng." |
| KĐ.3 | "Đúng! y²=8x đã ở đúng dạng chính tắc parabol, p=4." | "So sánh với dạng y²=2px — hệ số trước x chính là 2p." |
| KĐ.4 | "Chính xác! Hệ số x², y² bằng nhau → đây là đường tròn, không thuộc 3 loại vừa học." | "Kiểm tra lại: hệ số của x² và y² trong PT elip/hypebol/parabol có đặc điểm gì khác với PT này?" |
| Nhiệm vụ 1 | "Chính xác! a=5 (nửa tổng 2 khoảng cách), c=3 (nửa hiệu), b=4 → x²/25+y²/16=1." | "Thử cộng và trừ 2 khoảng cách cận tinh/viễn tinh để tìm a và c riêng biệt." |
| Nhiệm vụ 2 | "Đúng! 2c=200 từ khoảng cách 2 trạm; 2a=120 từ vận tốc×thời gian lệch; b²=c²−a²=6400 → x²/3600−y²/6400=1." | "Bấm 'Xin gợi ý' nếu cần định hướng — chú ý phân biệt đại lượng nào cho ra 2c, đại lượng nào cho ra 2a." |
| Nhiệm vụ 3 | "Chính xác! Điểm (0,5;1,5) trên viền chảo cho p=2,25, tiêu điểm cách đỉnh 1,125m." | "Xác định đúng loại conic trước (gợi ý cấp thấp có thể bấm nếu cần), sau đó áp dụng đúng công thức tương ứng." |
| Bảng tổng kết | "Chính xác! Bạn đã tự tổng hợp đúng đặc điểm phân biệt 3 loại conic." | "So sánh lại 3 nhiệm vụ vừa làm — mỗi nhiệm vụ dựa trên dấu hiệu định nghĩa nào (tổng khoảng cách, hiệu khoảng cách, hay cách đều 1 điểm-1 đường)?" |

---

### Trường dữ liệu bắt buộc

**Vòng khởi động (4 câu, MCQ):**
```
KĐ.1: dap_an_dung=Elip; giai_thich_dung="Chia 36: x²/9+y²/4=1"; goi_y_khi_sai="Chia 2 vế cho hằng số bên phải trước."
KĐ.2: dap_an_dung=Hypebol; giai_thich_dung="Chia 36: x²/4-y²/9=1"; goi_y_khi_sai="Chia 2 vế, chú ý dấu trừ."
KĐ.3: dap_an_dung=Parabol; giai_thich_dung="Đã chuẩn, p=4"; goi_y_khi_sai="So sánh với y²=2px."
KĐ.4: dap_an_dung="Không thuộc 3 loại (đường tròn)"; giai_thich_dung="Hệ số x², y² bằng nhau."; goi_y_khi_sai="So sánh hệ số x² và y²."
```

**Nhiệm vụ 1:**
```
dap_an_dung: x²/25+y²/16=1
giai_thich_dung: "a=5, c=3, b=4 từ a-c=2 và a+c=8."
goi_y_khi_sai: "Cộng và trừ 2 khoảng cách cận tinh/viễn tinh để tách riêng a và c."
```

**Nhiệm vụ 2:**
```
dap_an_dung: x²/3600-y²/6400=1
giai_thich_dung: "2c=200 (khoảng cách 2 trạm), 2a=120 (vận tốc×thời gian lệch), b²=c²-a²=6400."
goi_y_khi_sai: "Phân biệt: khoảng cách 2 trạm cho 2c; vận tốc×thời gian lệch cho 2a."
```

**Nhiệm vụ 3:**
```
dap_an_dung: 1.125 (mét)
giai_thich_dung: "Điểm (0,5;1,5) cho p=2,25; tiêu điểm cách đỉnh p/2=1,125m."
goi_y_khi_sai: "Xác định loại conic, đặt hệ trục, tìm 1 điểm trên viền chảo từ khẩu độ và độ sâu."
```

---

### Bố cục Mobile
Module có 5 phần lớn (khởi động, NV1, NV2, NV3, tổng kết) — đúng ngưỡng Mục
3.6b của `02_design_toan_final.md` (bắt buộc lướt ngang, có `.mobile-hint`).
Áp dụng bản hoà giải: vuốt ngang chỉ để XEM LẠI phần đã mở khoá; việc HOÀN
THÀNH/MỞ KHOÁ phần tiếp theo luôn qua 1 nút cố định đáy màn hình, phần chưa
mở khoá không render trong DOM. Nút "Xin gợi ý" (khi có) đặt CẠNH nút "Nộp
đáp án" trong cùng thanh đáy, không lẫn với việc mở khoá — để học sinh phân
biệt rõ 2 chức năng khác nhau (xin trợ giúp vs nộp bài).

### Nút và điều khiển:
- **Nộp đáp án:** xác nhận đáp án cuối, kích hoạt hình vẽ/feedback.
- **Xin gợi ý:** hiện gợi ý theo đúng cấp độ đã định nghĩa cho từng nhiệm vụ
  (không chấm điểm trừ, chỉ ghi nhận đã dùng gợi ý cho mục đích theo dõi).
- **Tiếp tục ▶ / nhãn động (mobile):** sang phần kế, chỉ hiện sau khi đúng.
- **Sổ tay:** luôn hiển thị sẵn (không cần mở/đóng vì đây là bài tổng hợp
  cần tra cứu thường xuyên).

---

## Critical Review — Tự phản biện

⚠️ Rủi ro 1: độ tự chủ giảm dần qua 3 nhiệm vụ có thể khiến học sinh yếu bị
"bỏ rơi" ở Nhiệm vụ 3 (gần như không gợi ý) — đã có nút "Xin gợi ý" cấp thấp
nhất (chỉ định hướng loại bài, không đưa công thức) để tránh bế tắc hoàn
toàn, nhưng đội build cần theo dõi tỉ lệ hoàn thành Nhiệm vụ 3 sau khi ra
mắt để điều chỉnh nếu quá khó.

⚠️ Rủi ro 2: câu KĐ.4 (đường tròn, không thuộc 3 loại) vượt nhẹ khỏi phạm
vi "3 đường conic" của bài — cần đảm bảo giải thích rõ đây là câu hỏi rèn tư
duy KHÔNG áp đặt máy móc, không phải dạy thêm kiến thức đường tròn mới.

📖 Kiểm tra caption: đã rà lại — không có dòng trống thiếu giải thích.

---

## Rà soát trùng lặp SGK

- Nhiệm vụ 1 (Kepler, 2-8 AU) khác hoàn toàn mọi số liệu SGK.
- Nhiệm vụ 2 (LORAN, 200km/0,0004s) đã đổi khác Bài tập 7.24 SGK (300km,
  292.000km/s, 0,0005s) dù cùng chủ đề LORAN — đúng gợi ý PPCT nhưng không
  trùng số liệu.
- Nhiệm vụ 3 (ăng-ten, khẩu độ 3m/sâu 0,5m) không trùng Ví dụ 5 SGK.
- Vòng khởi động hiện thực hoá đúng gợi ý "Trò chơi Nhận dạng conic" của
  PPCT — SGK không có hoạt động tương tự.
- Bảng tổng kết là hoạt động tự tổng hợp, không sao chép bảng nào có sẵn
  trong SGK (SGK không có bảng so sánh 3 conic ở phần cốt lõi — bảng này chỉ
  xuất hiện đầy đủ ở Chuyên đề mở rộng, ngoài phạm vi lần này).

---
**Trạng thái: ĐÃ DUYỆT — chuyển sang Giai đoạn 2 (Thiết kế giao diện) khi build.**

---

# Tổng kết Bài 22 — Ba đường conic
Cả 4 module đã hoàn thành:
- Module 1: Elip — "Phòng thì thầm" (`Bai22_Module1_Elip.md`)
- Module 2: Hypebol — "Tháp giải nhiệt" (`Bai22_Module2_Hypebol.md`)
- Module 3: Parabol — "Gương đèn pha ô tô" (`Bai22_Module3_Parabol.md`)
- Module 4: Ứng dụng tổng hợp — "Chọn đúng đường conic" (file này)

Điểm xuyên suốt cả bài: luồng "thực tế → phương trình" (M1-M3) thay vì
"phương trình → thực tế" như SGK, độ tự chủ tăng dần qua các module, và mọi
bối cảnh/số liệu đều đã rà soát không trùng SGK ở cả 3 lớp (tên gọi, bối
cảnh, kỹ thuật).

---

## 🔗 Athena Context & Tích hợp LMS (bắt buộc theo `02_design_toan_final.md` PHẦN 7)

> Nhân vật hướng dẫn/gợi ý trong module LUÔN gọi là **"Athena"** — không dùng
> "robot"/"AI"/tên khác, theo đúng PHẦN 7.9. Module role-play này có nút
> "Xin gợi ý" độ tự chủ giảm dần — Athena vẫn là nhân vật đứng sau nút đó,
> không phải 1 nhân vật khác.

### `structure[]` — id khớp với id dùng trong code
```
[
  { "id": "b22m4-kd", "title": "Vòng khởi động — Nhận dạng nhanh (4 câu)" },
  { "id": "b22m4-nv1", "title": "Nhiệm vụ 1 — Nhà thiên văn (Elip)" },
  { "id": "b22m4-nv2", "title": "Nhiệm vụ 2 — Kỹ sư LORAN (Hypebol)" },
  { "id": "b22m4-nv3", "title": "Nhiệm vụ 3 — Kỹ sư ăng-ten (Parabol)" },
  { "id": "b22m4-tk", "title": "Bảng tổng kết (tự điền, không có đáp án cố định)" }
]
```
**Vòng khởi động + 3 Nhiệm vụ đều BẮT BUỘC** (`progress total = 7`: 4 câu
khởi động + 3 nhiệm vụ, mỗi nhiệm vụ tính là 1 đơn vị dù chỉ có 1 đáp án
cuối cùng). **Bảng tổng kết** không có đáp án đúng/sai cố định (học sinh tự
tổng hợp) — không tính vào `total` nhưng vẫn hiển thị trước khi hoàn thành.

### `athenaGuidance` (bản nháp)
```
Module tổng hợp cuối Bài 22 — học sinh đóng vai kỹ sư/nhà khoa học, tự nhận
diện loại conic phù hợp và giải bài toán thực tế với độ tự chủ tăng dần qua
3 nhiệm vụ (không có gợi ý ngắt từng bước nhỏ như các module trước).

VÒNG KHỞI ĐỘNG (4 câu nhận dạng nhanh):
KĐ.1) Cho PT: 4x²+9y²=36. Đây là loại đường conic nào?
      Lựa chọn: A) Elip  B) Hypebol  C) Parabol
KĐ.2) Cho PT: 9x²−4y²=36. Đây là loại đường conic nào?
      Lựa chọn: A) Elip  B) Hypebol  C) Parabol
KĐ.3) Cho PT: y²=8x. Đây là loại đường conic nào?
      Lựa chọn: A) Elip  B) Hypebol  C) Parabol
KĐ.4) Cho PT: 2x²+2y²−8=0. Đây là loại đường conic nào trong 3 loại đã học?
      Lựa chọn: A) Elip  B) Hypebol  C) Parabol
                D) Không thuộc 3 loại đã học

NHIỆM VỤ 1 (Elip, có gợi ý hiện sẵn: "khoảng cách gần nhất = a−c, khoảng
cách xa nhất = a+c"): Một hành tinh quay quanh 1 ngôi sao theo quỹ đạo
elip, ngôi sao nằm tại 1 tiêu điểm. Khoảng cách gần nhất (điểm cận tinh) là
2 AU, xa nhất (điểm viễn tinh) là 8 AU. Lập phương trình chính tắc mô tả
quỹ đạo. (câu điền tự do, có nút "Xin thêm gợi ý" cấp 2)

NHIỆM VỤ 2 (Hypebol, không có gợi ý hiện sẵn, chỉ có nút "Xin gợi ý" ẩn):
2 trạm phát sóng A, B cách nhau 200km. 1 tàu thu tín hiệu từ A sớm hơn từ B
đúng 0,0004 giây (vận tốc sóng vô tuyến 300.000 km/s). Xác định phương
trình chính tắc của nhánh hypebol chứa vị trí tàu. (câu điền tự do)

NHIỆM VỤ 3 (Parabol, gần như không gợi ý — nút "Xin gợi ý" chỉ định hướng
loại bài, không đưa công thức): Ăng-ten vệ tinh dạng chảo parabol, đường
kính miệng chảo 3m, độ sâu đáy chảo 0,5m. Xác định khoảng cách từ đỉnh chảo
đến vị trí cần đặt đầu thu tín hiệu. (câu điền tự do, đáp án số)

Quy tắc đứng đặc biệt cho module này: Athena chỉ được đưa gợi ý ĐÚNG CẤP ĐỘ
đã định nghĩa cho từng nhiệm vụ khi học sinh chủ động bấm "Xin gợi ý" — với
Nhiệm vụ 3, Athena TUYỆT ĐỐI không được đưa công thức, chỉ được hỏi ngược
"Đây là loại đường conic nào? Đặt hệ trục ở đâu để bài toán đơn giản nhất?"
Không bao giờ nói thẳng đáp án đúng của bất kỳ câu/nhiệm vụ nào.
```

### Instrumentation cần gắn (đội build, theo Mục 7.4–7.6)
- `LMS().progress({done, total:7})` — 4 câu khởi động + 3 nhiệm vụ.
- `LMS().event('answered', {...})` — bắn ở mỗi câu khởi động và mỗi lần
  "Nộp đáp án" ở 3 nhiệm vụ.
- `LMS().event('hint_requested', {id, level})` — bắn riêng mỗi khi học sinh
  bấm "Xin gợi ý" (không phải `answered`), ghi rõ cấp độ gợi ý đã xem — dữ
  liệu này quan trọng để Athena biết học sinh có đang gặp khó ở Nhiệm vụ
  nào khi được hỏi giữa chừng, và để đội build theo dõi tỉ lệ dùng gợi ý ở
  Nhiệm vụ 3 (đã ghi trong Critical Review là rủi ro cần theo dõi).
- `LMS().state({...})` — cập nhật mỗi khi chuyển giữa khởi động/3 nhiệm
  vụ/bảng tổng kết.
- `LMS().complete({...})` — bắn đúng 1 lần sau khi hoàn thành Nhiệm vụ 3
  (bảng tổng kết không chặn hoàn thành vì không có đáp án cố định); `items`
  liệt kê đủ 7 mục bắt buộc (4 khởi động + 3 nhiệm vụ).
