# 📋 KỊCH BẢN SIMULATION — MODULE 13.4
## Vận dụng định lí Thalès và bài tập

**Bài SGK:** Bài 13 — Hai mặt phẳng song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 13.4 — nối tiếp Module 13.1
(Định nghĩa và điều kiện đủ), 13.2 (Tính chất và hệ quả), 13.3 (Định lí
Thalès trong không gian). Tương ứng Tiết 34.
**Trạng thái kiến thức nền:** Đã dạy qua Module 13.1–13.3 trong cùng hệ
thống — 13.4 KHÔNG dạy lại lý thuyết Thalès, chỉ vận dụng + luyện tập.
**Nguồn SGK tham chiếu:** HĐ5, Ví dụ 4, Luyện tập 4 (trang 90) + bài tập 4.24
(trang 94) — số liệu trong simulation đã đổi khác hoàn toàn so với SGK.

---

## 🎯 MỤC TIÊU

- HIỂU: nắm bản chất "3 mặt phẳng đôi một song song chắn trên 2 cát tuyến
  phân biệt những đoạn thẳng tương ứng tỉ lệ" — điều kiện tiên quyết là 3
  mặt phẳng phải **đôi một song song**.
- LÀM ĐƯỢC:
  - Tính độ dài đoạn thẳng còn thiếu khi biết tỉ lệ Thalès không gian (dạng
    Luyện tập 4)
  - Chứng minh 2 đoạn thẳng bằng nhau/tỉ lệ dựa trên tỉ lệ đã cho trên 1 cát
    tuyến, suy ra tỉ lệ tương ứng trên cát tuyến còn lại (dạng Ví dụ 4 và bài
    4.24)

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Ghép sai cặp tỉ số tương ứng | Nhầm đoạn trên cát tuyến này với đoạn trên cát tuyến kia (VD lấy AB/BC nhưng so với A'C'/C'B' thay vì đúng A'B'/B'C') | Kết quả tính ra không khớp với hình vẽ khi kiểm tra bằng mắt |
| Không kiểm tra điều kiện "3 mặt phẳng đôi một song song" trước khi áp dụng | Áp dụng Thalès không gian cho trường hợp mặt phẳng không thực sự song song | Áp dụng công thức cho 2 mặt phẳng cắt nhau, ra kết quả vô lý |
| Nhầm tỉ lệ đoạn thẳng trên CÙNG 1 cạnh với tỉ lệ GIỮA 2 cạnh khác nhau | VD nhầm SF/SA (1 cạnh) với tỉ lệ cần suy ra trên cạnh khác | Nhầm SF:FA (cạnh SA) với SG:GB (cạnh SB) khi thay số |

## 🧊 ĐẶC THÙ 3D

- **Khối/đối tượng nền:** dựng riêng theo cấu trúc Ví dụ 4/Luyện tập 4 SGK (3
  mặt phẳng đôi một song song cắt 2 cát tuyến), số liệu đổi khác SGK. Tab B
  Case 2 dùng hình chóp S.ABCD đáy hình bình hành (đổi hẳn loại khối so với
  tứ diện của bài 4.24 gốc, không chỉ đổi tỉ lệ điểm chia).
- **Quan hệ không gian trọng tâm:** định lí Thalès trong không gian (3 mặt
  phẳng đôi một song song).
- **Góc camera mặc định:** nhìn ngang để thấy rõ 3 mặt phẳng xếp chồng song
  song và 2 đường cát tuyến xuyên qua; Tab B dùng `setCameraStandardSGK()`.
- **Mức độ tương tác:** Tab A — chỉ quan sát (kéo slider, không chấm điểm).
  Tab B — đo/kiểm tra (nhập số, hệ thống chấm).
- **Dạy từ đầu hay tổng kết:** tổng kết/vận dụng — Thalès đã dạy ở 13.3,
  13.4 chỉ luyện áp dụng, có Sổ tay kiến thức.

## 🎮 CƠ CHẾ TƯƠNG TÁC — LÝ DO TÁCH 2 GIAI ĐOẠN

Ban đầu cân nhắc dùng slider real-time xuyên suốt, nhưng đây là kiểu tương
tác "1 bậc tự do + phản hồi liên tục" — rủi ro học sinh dò ra quy luật bằng
mắt (thấy số tăng/giảm theo slider) mà không cần thực sự tính theo công
thức. Mục tiêu module là kỹ năng TÍNH, không phải kỹ năng quan sát xu hướng.
→ Quyết định: tách 2 giai đoạn rõ ràng, không chấm điểm ở giai đoạn khám phá.

---

## TAB A — Khám phá bằng slider (không chấm điểm)

**Mục tiêu:** Xây trực giác rằng tỉ lệ Thalès không gian luôn đúng bất kể vị
trí cụ thể của mặt phẳng ở giữa, miễn vẫn giữ điều kiện song song.
**Loại simulation:** G (slider tham số hình học).
**Thời gian hoàn thành dự kiến:** ~2 phút.

### Màn hình chính hiển thị:
- 3 mặt phẳng song song `(P)`, `(Q)`, `(R)` — màu `COLOR_PLANE_1`,
  `COLOR_PLANE_2`, `COLOR_PLANE_3`, opacity 0.2.
- 2 đường thẳng (cát tuyến) `d`, `d'` xuyên qua cả 3 mặt phẳng, cắt tại các
  điểm `A, B, C` (trên `d`) và `A', B', C'` (trên `d'`) — điểm màu
  `COLOR_RESULT`.
- Nhãn tỉ số hiển thị dạng phân số ở góc canvas, cập nhật real-time.

### Sổ tay kiến thức (Có):
- Định lí Thalès không gian: 3 mặt phẳng đôi một song song chắn trên 2 cát
  tuyến phân biệt những đoạn thẳng tương ứng tỉ lệ: AB/BC = A'B'/B'C'
- Điều kiện bắt buộc: 3 mặt phẳng phải đôi một song song (không chỉ 2 trong 3)

### Học sinh tương tác bằng cách:
1. Quan sát 3 mặt phẳng và 2 cát tuyến đã dựng sẵn.
2. Kéo slider "Vị trí mặt phẳng (Q)" — (Q) trượt dọc theo khoảng giữa (P)
   và (R).
3. Quan sát 2 tỉ số AB/BC và A'B'/B'C' hiện song song, cập nhật real-time.
4. Trả lời câu hỏi phản tư: "Khi kéo (Q), 2 tỉ số có luôn bằng nhau không?"
   (Có/Không).

### Trước mỗi bước tương tác:

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | Kéo slider để dịch chuyển (Q) | (P), (Q), (R) luôn giữ song song trong lúc kéo |
| 2 | Quan sát 2 tỉ số hiển thị | Theo Thalès không gian, 2 tỉ số này luôn bằng nhau |
| 3 | Trả lời Có/Không | Củng cố lại bằng lời trước khi sang Tab B |

### Giải thích kiến thức:

| Trạng thái | Caption | Giải thích kiến thức |
|---|---|---|
| Trả lời "Có" | Chính xác! | Đây chính là nội dung định lí Thalès không gian — tỉ lệ không phụ thuộc vị trí cụ thể của (Q), miễn vẫn giữ điều kiện song song |
| Trả lời "Không" | Thử kéo chậm lại và quan sát kỹ 2 con số | Có thể học sinh nhìn nhầm 2 tỉ số ở 2 thời điểm khác nhau — gợi ý dừng slider lại rồi đọc kỹ |

### Cấu hình 3D:
- **Đối tượng kéo được:** chỉ (Q) theo 1 trục (slider ánh xạ vị trí), không
  kéo tự do 6 bậc.
- **Góc camera mặc định:** nhìn ngang để thấy rõ 3 mặt phẳng xếp chồng.
- **Quan hệ hình học cần tính:** tính tỉ số AB/BC, A'B'/B'C' theo vị trí (Q)
  hiện tại, cập nhật mỗi frame khi slider thay đổi.
- **Yếu tố hiển thị kèm:** 2 tỉ số dạng phân số góc canvas, đồng bộ màu với
  điểm tương ứng.
- **Cleanup:** `clearScene()` khi chuyển sang Tab B.

### Nút và điều khiển:
- **Slider "Vị trí mặt phẳng (Q)":** kéo dịch chuyển (Q) giữa (P) và (R).
- **Đặt lại góc nhìn:** reset camera.

---

## TAB B — Luyện tập nhập số (có chấm điểm)

**Mục tiêu:** Áp dụng đúng công thức tỉ lệ Thalès không gian để tính số liệu
cụ thể, không còn gì để dò bằng mắt.
**Loại simulation:** I2 (nhập số + xác nhận).
**Thời gian hoàn thành dự kiến:** ~4-5 phút.

### Case 1 — dạng Luyện tập 4 SGK (đổi số)
**Đề bài:** Cho AB = 3cm, BC = 5cm, A'B' = 4.5cm. Tính B'C'.
- Học sinh nhập số vào ô, bấm "Kiểm tra".
- Đáp án đúng: B'C' = 7.5cm (sai số cho phép ±0.1).

### Case 2 — dạng bài 4.24 SGK (đổi khác hẳn loại khối, không chỉ đổi số)
**Đề bài:** Cho hình chóp **S.ABCD, đáy ABCD là hình bình hành** (khác hẳn
tứ diện S.ABC của bản trước — vốn vẫn còn quá gần cấu hình 4.24 gốc). Trên
cạnh SC lấy điểm E sao cho **SE = 2EC** (tỉ lệ 2:1, khác tỉ lệ chia 3 đều
của bản trước). Mặt phẳng (P) qua E, song song với mặt đáy (ABCD), cắt SA
tại F và SB tại G. Biết SA = 6cm, SB = 12cm. Tính SF, FA (trên cạnh SA), sau
đó tự suy ra SG, GB (trên cạnh SB) — 2 phần nhập số riêng biệt, phần sau
không hiện gợi ý số liệu để buộc học sinh áp dụng lại đúng tỉ lệ 2:1 một
cách độc lập, không chỉ copy kết quả phần trước.
- Học sinh nhập 4 số tổng cộng (SF, FA trước — khoá lại sau khi đúng; rồi
  mới mở SG, GB), hệ thống chấm từng ô.
- Đáp án: SF = 4cm, FA = 2cm (vì SF/SA = SE/SC = 2/3); SG = 8cm, GB = 4cm
  (cùng tỉ lệ 2/3, nhưng học sinh phải tự lập lại trên cạnh SB, không được
  nhắc lại số liệu của SA).

### Trước mỗi bước tương tác:

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| Case 1 | Nhập giá trị B'C' rồi bấm Kiểm tra | AB/BC = A'B'/B'C' — thay số đã biết vào để giải B'C' |
| Case 2a | Nhập SF rồi FA, bấm Kiểm tra từng ô | (P) // (ABCD) nên theo Thalès không gian, SF/SA = SE/SC = 2/3 — 3 mặt phẳng (ABCD đáy), (P), và mặt phẳng qua S song song đáy đôi một song song |
| Case 2b | Sau khi Case 2a đúng, ô nhập SG, GB mở ra — nhập rồi bấm Kiểm tra | Cùng nguyên tắc như 2a nhưng áp dụng ĐỘC LẬP trên cạnh SB — củng cố rằng tỉ lệ 2/3 đúng với MỌI cạnh bên đi qua S, không chỉ riêng SA |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Ở Case 1, học sinh có thể tính B'C' = AB × A'B'/BC (ghép sai
  cặp, đảo tử/mẫu).
- Hệ thống phản hồi: Sai lần 1 → chỉ báo sai, không giải thích. Sai lần 2 →
  hiện gợi ý "Viết lại đúng thứ tự: đoạn nào trên cát tuyến 1 tương ứng đoạn
  nào trên cát tuyến 2? So khớp theo đúng thứ tự A-B-C và A'-B'-C'." Sai lần
  3 → hiện đáp án + giải thích đầy đủ.
- Kết quả rút ra: Học sinh tự nhận ra cần khớp đúng thứ tự điểm trước khi
  lập tỉ số, không ghép ngẫu nhiên.
- Tình huống thêm (Case 2b): sau khi làm đúng Case 2a (SF, FA), học sinh
  có thể chủ quan gõ nguyên số 4cm, 2cm cho SG, GB vì "thấy quen tay",
  trong khi SB = 12cm khác SA = 6cm nên kết quả thực tế khác (8cm, không phải
  3cm).
- Hệ thống phản hồi: Nếu nhập đúng 4/2 (sai vì áp số cũ của SA), phản hồi
  riêng — không xếp chung nhóm "sai lần 1" bình thường mà chỉ rõ ngay: "Số
  này giống hệt kết quả của SA — nhưng SB có độ dài khác SA, thử tính lại
  theo đúng tỉ lệ 2/3 trên SB." — cảnh báo đúng loại lỗi "copy kết quả" chứ
  không lẫn
  vào lỗi ghép sai cặp tỉ số thông thường.
- Kết quả rút ra: Củng cố rằng tỉ lệ Thalès áp dụng ĐỘC LẬP trên từng cát
  tuyến theo đúng độ dài riêng của nó, không suy ra bằng cách copy số từ cát
  tuyến khác dù tỉ lệ chia là như nhau.

### Giải thích kiến thức:

| Trạng thái | Caption | Giải thích kiến thức |
|---|---|---|
| Đúng | Chính xác! | Nêu lại phép tính cụ thể đã áp dụng đúng công thức |
| Sai lần 1 | Chưa đúng, thử lại | (không giải thích) |
| Sai lần 2 | Gợi ý khớp thứ tự điểm | Đã nêu ở kịch bản trên |
| Sai lần 3 | Hiện đáp án | Giải đầy đủ theo từng bước thay số |
| Case 2b — nhập đúng số của SA (copy nhầm) | Số này giống hệt kết quả của SA, thử tính lại | SB = 12cm khác SA = 6cm nên dù cùng tỉ lệ 2/3, độ dài từng đoạn khác nhau — không suy ra bằng cách copy |
| Case 2b — đúng | Chính xác, cả 2 cạnh đều thoả tỉ lệ 2/3! | Củng cố: định lí Thalès không gian áp dụng đúng trên MỌI cạnh bên đi qua S, không riêng gì 1 cạnh |

### Cấu hình 3D:
- **Khối nền:** Case 1 dùng 3 mặt phẳng + 2 cát tuyến (tĩnh, không slider);
  Case 2 dùng hình chóp S.ABCD đáy hình bình hành.
- **Đối tượng kéo được:** không có — chỉ OrbitControls xoay/zoom.
- **Góc camera mặc định:** `setCameraStandardSGK()`.
- **Quan hệ hình học cần tính:** kiểm tra giá trị nhập vào so với đáp án
  đúng, sai số cho phép nhỏ (±0.1) để buộc tính đúng công thức, không đoán.
- **Yếu tố hiển thị kèm:** số liệu đã biết hiển thị nhãn cố định trên hình;
  ô nhập số ở sidebar.
- **Cleanup:** `clearScene()` giữa Case 1 và Case 2.

### Nút và điều khiển:
- **Ô nhập số + nút Kiểm tra:** xác nhận đáp án từng case.
- **Đặt lại góc nhìn:** reset camera.

---

## 🎯 TỔNG KẾT CUỐI MODULE

**Tổng kết kiến thức:** 3 mặt phẳng đôi một song song luôn chắn trên 2 cát
tuyến phân biệt những đoạn thẳng tương ứng tỉ lệ — điều kiện "đôi một song
song" là bắt buộc, thiếu điều kiện này thì không được áp dụng tỉ lệ.

**Tổng kết sai lầm:**
1. Ghép sai cặp tỉ số — dấu hiệu: kết quả tính ra không khớp với hình vẽ khi
   kiểm tra bằng mắt.
2. Quên kiểm tra điều kiện đôi một song song — dấu hiệu: áp dụng công thức
   cho 2 mặt phẳng cắt nhau, ra kết quả vô lý.
3. Nhầm tỉ lệ trong-cùng-cát-tuyến với tỉ lệ giữa-2-cát-tuyến — dấu hiệu:
   nhầm SF:FA (cùng 1 cạnh) với SG:GB (cạnh khác) khi thay số.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

⚠️ **Rủi ro 1:** Tab A dùng slider dịch chuyển (Q) giữa (P) và (R) — cần
verify bằng script Node độc lập công thức tính tỉ số real-time khi (Q) ở các
vị trí biên (gần trùng (P) hoặc (R)), tránh chia cho 0 hoặc số quá lớn gây
lỗi hiển thị.

⚠️ **Rủi ro 2:** Case 2 Tab B (hình chóp S.ABCD đáy hình bình hành, mặt
phẳng song song đáy) có độ phức tạp hình học cao hơn Case 1, nay còn mở
rộng thêm phần 2b (SG, GB) — cần đảm bảo caption đủ rõ để học sinh không bị
rối giữa 2 cạnh SA và SB, đặc biệt là khoá UI đúng thứ tự (2b chỉ mở sau
khi 2a đúng, không hiện đồng thời 4 ô nhập cùng lúc).

⚠️ **Rủi ro 3 (mới):** Cố ý đặt SA = 6cm, SB = 12cm (khác nhau) để bẫy lỗi
"copy kết quả" ở 2b — cần verify kỹ số liệu này không vô tình tạo thêm 1
phép tính lẻ (kiểm tra SA×2/3=4, SB×2/3=8 đều là số nguyên, không sai số
thập phân gây khó chấm điểm).

📝 **Cập nhật rà soát bản quyền (sau khi review toàn bộ Bài 12-13):** Case 2
ban đầu dùng tứ diện S.ABC với A₁, A₂ chia 3 phần bằng nhau trên SA — bị
đánh giá gần như bản sao bài 4.24 SGK (chỉ đảo chiều đếm điểm từ A thay vì
từ S). Đã đổi hẳn sang hình chóp S.ABCD đáy hình bình hành, điểm E trên SC
với tỉ lệ SE=2EC (không chia 3 đều), mặt phẳng song song đáy cắt SA, SB —
khác cả loại khối, tỉ lệ chia, và số cạnh liên quan so với 4.24 gốc.

📖 **Kiểm tra caption:** Đã rà toàn bộ bảng "Giải thích kiến thức" — không
có dòng nào chỉ nói "Đúng rồi!"/"Sai rồi" mà thiếu giải thích bản chất, kể
cả dòng mới thêm cho Case 2b.

---

**Kịch bản đã sẵn sàng! Các bước tiếp theo:**
- ✅ Duyệt — chuyển sang Giai đoạn 2 (Thiết kế giao diện chi tiết)
- ✏️ Chỉnh — nêu rõ Tab/phần nào cần thay đổi

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 11/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`,
> `01_scenario_builder_3d_addendum.md`, `04_design_toan_3d.md`,
> `05_threejs_engine.md`, `06_geometry_math.md`
