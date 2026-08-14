# KỊCH BẢN MODULE 5b — LUYỆN TẬP TỔNG HỢP PHƯƠNG TRÌNH ĐƯỜNG THẲNG
## (Bài 15, Toán 12 HK2 — Stage 2 của Module 5, tách riêng thành 1 file)

**Mục tiêu:** Vận dụng tổng hợp 4 kỹ năng đã học (PT tham số, PT chính tắc,
vị trí 2 đường thẳng, vị trí đường thẳng-mặt phẳng) + kỹ năng đặc trưng của
Module 5 (phân biệt "cắt quỹ đạo" và "va chạm").

**Loại simulation:** I (trắc nghiệm minh hoạ 3D) cho vòng 1–4, F (dựng dần
từng bước) cho thử thách cuối.
**Thời gian hoàn thành dự kiến:** ~13-15 phút
**Design:** Cream & Green, Be Vietnam Pro, 1 canvas dùng lại + `clearScene()`
giữa các vòng (đúng kiến trúc đã dùng ở Module 6b).

**Mở khoá thử thách cuối:** Sau khi hoàn thành ≥ 4/5 phần (4 vòng, không
tính capstone).

---

## Vòng 1 — Viết phương trình tham số (kỹ năng Module 1)

**Bối cảnh:** Dây cáp treo của 1 cầu treo, neo tại trụ tháp A(1;2;0), chạy
theo hướng VTCP u=(2;−1;3).

**Câu hỏi:** "Phương trình tham số nào đúng cho dây cáp?"

| # | Đáp án | Ghi chú |
|---|---|---|
| A | x=1+2t, y=2+t, z=3t | Nhiễu — sai dấu thành phần y (đổi −1 thành +1) |
| B | x=2+t, y=−1+2t, z=3t | Nhiễu — tráo vai trò điểm A và VTCP u |
| **C** | **x=1+2t, y=2−t, z=3t** | **`dap_an_dung`** |
| D | x=1+2t, y=2−t, z=t | Nhiễu — quên hệ số 3 ở thành phần z |

- `giai_thich_dung`: "A(1;2;0), u=(2;−1;3) → x=1+2t, y=2+(−1)t=2−t,
  z=0+3t=3t."
- `giai_thich_sai`:
  - **A:** "Sai dấu ở y — VTCP có thành phần thứ 2 là −1, nên phải là
    2−t, không phải 2+t. Lỗi đổi dấu khi thành phần VTCP âm."
  - **B:** "Nhầm vai trò: dùng toạ độ VTCP (2;−1;3) làm điểm xuất phát và
    toạ độ điểm A(1;2;0) làm hệ số t — ngược hoàn toàn vai trò 2 đối
    tượng."
  - **D:** "Thiếu hệ số 3 ở thành phần z — chỉ viết z=t thay vì z=3t, bỏ
    quên nhân với thành phần thứ 3 của VTCP."
- `goi_y_khi_sai`: "Công thức chung: x=x₀+at, y=y₀+bt, z=z₀+ct với
  (x₀;y₀;z₀) là điểm đi qua, (a;b;c) là VTCP. Đối chiếu lại từng thành
  phần."

---

## Vòng 2 — Phương trình chính tắc + điều kiện tồn tại (kỹ năng Module 2)

**Bối cảnh:** Đường ống dẫn dầu ngầm đi qua 2 điểm khảo sát M1(0;1;3) và
M2(4;1;7).

**Tính toán nền:** VTCP = M2−M1 = (4;0;4) — **thành phần thứ 2 bằng 0**.

**Câu hỏi 1:** "Đường ống này có viết được phương trình chính tắc không?"

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Có, dạng (x)/4 = (y−1)/0 = (z−3)/4 | Nhiễu — đây là sai lầm PPCT cảnh báo: viết chính tắc dù có mẫu bằng 0 (vi phạm điều kiện chia cho 0) |
| **B** | **Không — chỉ viết được phương trình tham số** | **`dap_an_dung`** |
| C | Có, bỏ qua thành phần y | Nhiễu — không đúng quy tắc, không thể tự ý bỏ 1 phương trình |
| D | Không, vì 2 điểm cho trước trùng nhau | Nhiễu — M1≠M2, đề bài không sai |

- `giai_thich_dung`: "VTCP=(4;0;4) có thành phần thứ 2 bằng 0 → không thể
  viết phương trình chính tắc (mẫu số không được bằng 0). Chỉ viết được
  phương trình tham số: x=4t, y=1, z=3+4t."
- `giai_thich_sai` cho A: "Đây chính là lỗi PPCT cảnh báo — 'cố chấp áp
  dụng phương trình chính tắc ngay cả khi VTCP có thành phần bằng 0'. Biểu
  thức (y−1)/0 không có nghĩa trong toán học, không được viết ra dù chỉ
  để 'điền đủ 3 phân số'."
- `goi_y_khi_sai`: "Kiểm tra lại VTCP — phương trình chính tắc chỉ tồn tại
  khi CẢ 3 thành phần VTCP đều khác 0."

---

## Vòng 3 — Vị trí tương đối hai đường thẳng (kỹ năng Module 3)

**Bối cảnh:** Hai đường ray tàu điện. Ray 1 cố định qua E(0;0;0), VTCP
p=(1;1;0).

**Câu hỏi 1:** Ray 2 qua F(2;2;5), VTCP q=(2;2;0). Vị trí tương đối?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Trùng nhau | Nhiễu — q=2p cùng phương đúng, nhưng quên kiểm tra F có thuộc Ray 1 |
| B | Cắt nhau | Nhiễu — VTCP cùng phương thì không thể cắt (trừ trùng) |
| **C** | **Song song** | **`dap_an_dung`** |
| D | Chéo nhau | Nhiễu — VTCP cùng phương nên không thể chéo |

- `giai_thich_dung`: "q=(2;2;0)=2p cùng phương với p. Thử t để (t,t,0)=
  F(2;2;5): cần t=2 (từ x,y) nhưng z=0≠5 → F không thuộc Ray 1 → 2 ray
  song song, không trùng."

**Câu hỏi 2:** Ray 2' qua G(1;−1;2), VTCP r=(0;1;−1). Vị trí tương đối?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Song song | Nhiễu — r không cùng phương p |
| B | Chéo nhau | Nhiễu — 2 ray này thực ra có điểm chung, chỉ "nhìn không cùng phương" rồi vội đoán chéo mà chưa giải hệ |
| **C** | **Cắt nhau** | **`dap_an_dung`** — tại điểm (1;1;0), ứng t=1 (Ray1), s=2 (Ray2') |
| D | Trùng nhau | Nhiễu |

- `giai_thich_dung`: "p và r không cùng phương → không song song/trùng.
  Giải hệ: Ray1(t)=(t,t,0), Ray2'(s)=(1,−1+s,2−s). Từ x: t=1. Từ y:
  1=−1+s→s=2. Từ z: 0=2−s→s=2 (khớp) → 2 ray cắt nhau tại (1;1;0)."
- `giai_thich_sai` cho B (Chéo nhau): "VTCP không cùng phương chỉ loại
  trừ song song/trùng — chưa đủ để kết luận chéo. Phải giải hệ 3 phương
  trình (x,y,z) để xem có nghiệm chung (t,s) không. Ở đây hệ CÓ nghiệm
  (t=1,s=2) → cắt nhau, không chéo."

---

## Vòng 4 — Vị trí đường thẳng và mặt phẳng (kỹ năng Module 4)

**Bối cảnh:** Cầu trượt nước công viên, mặt nước hồ là (H): z=0. Cầu trượt
là đường thẳng qua đỉnh S(2;3;5), hướng xuống u=(1;1;−5).

**Câu hỏi 1:** "Cầu trượt có chạm mặt nước không? Nếu có, tại đâu?"

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Không chạm, cầu trượt song song mặt nước | Nhiễu — u·n=−5≠0, không song song |
| B | Chạm tại (2;3;0) | Nhiễu — giữ nguyên x,y của S mà quên tính lại theo t |
| **C** | **Chạm tại (3;4;0)** | **`dap_an_dung`** |
| D | Chạm tại (1;1;−5) | Nhiễu — nhầm giao điểm với chính VTCP u |

- `giai_thich_dung`: "u·n=(1)(0)+(1)(0)+(−5)(1)=−5≠0 → cắt mặt nước. Giải
  5−5t=0 (từ toạ độ z=5−5t=0) → t=1. Thay vào: x=2+1=3, y=3+1=4, z=0 →
  điểm (3;4;0)."

**Câu hỏi 2:** Một thanh chắn an toàn khác qua S(2;3;5), hướng v=(1;1;0).
Vị trí so với mặt nước?

| # | Đáp án | Ghi chú |
|---|---|---|
| **A** | **Song song với mặt nước** | **`dap_an_dung`** |
| B | Cắt mặt nước | Nhiễu — v·n=0, không cắt |
| C | Nằm trong mặt nước | Nhiễu — S có z=5≠0, S không thuộc mặt nước |
| D | Không xác định được | Nhiễu |

- `giai_thich_dung`: "v·n=0 → song song hoặc nằm trong. S(2;3;5) có z=5≠0
  → S không thuộc mặt nước (H) → song song, không nằm trong."

---

## Thử thách cuối — Radar theo dõi 2 drone giao hàng (loại F, dựng dần)

**Mở khoá:** Sau khi hoàn thành ≥ 4/5 phần trên.

**Bối cảnh:** 2 drone giao hàng bay theo quỹ đạo thẳng đều, PT tham số theo
thời gian thực t (giây), xuất phát cùng lúc t=0.

*Lý do đổi bối cảnh:* PPCT tự gợi ý "Radar theo dõi va chạm" — nhưng ý
tưởng này trùng khá sát Vận dụng 3 SGK (2 vật thể xuất phát từ A, B với vận
tốc không đổi, xét va chạm) và Bài 5.18 (viên đạn bắn từ A, xét trúng mục
tiêu). Đổi hẳn sang khung cảnh "drone giao hàng hiện đại" — giữ đúng kỹ
thuật cần dạy nhưng khác bối cảnh cụ thể.

**Dữ liệu:**
```
Drone A: xuất phát A₀(0;0;10), vận tốc vA=(2;1;−2) (km/phút)
Drone B: xuất phát B₀(14;17;26), vận tốc vB=(−2;−3;−4) (km/phút)
```

- **Bước 1:** Viết phương trình quỹ đạo (tham số theo t) của mỗi drone.
  - Drone A: x=2t, y=t, z=10−2t
  - Drone B: x=14−2t, y=17−3t, z=26−4t

- **Bước 2:** Hỏi: "Quỹ đạo bay (dạng đường thẳng hình học) của 2 drone có
  cắt nhau không?" — Học sinh giải hệ với 2 tham số RIÊNG (t cho A, s cho
  B, vì đang hỏi về đường thẳng hình học, chưa phải thời điểm thực).
  - Đáp số: cắt tại điểm Q(4;2;6), ứng với t=2 (Drone A) và s=5 (Drone B).

- **Bước 3:** Hỏi: "2 drone có va chạm không?" — Học sinh nhận ra: Drone A
  đi qua Q lúc t=2, còn Drone B đi qua Q lúc t=5 (khác thời điểm, dùng
  CHUNG 1 đồng hồ thời gian thực) → **KHÔNG va chạm**, dù quỹ đạo bay có
  cắt nhau. Đây đúng là sai lầm trọng tâm PPCT nêu.

- **Bước 4 (biến thể ngay sau đó, không đổi bối cảnh):** "Nếu Drone B xuất
  phát muộn hơn từ điểm B₀'(8;8;14) với cùng vận tốc vB, 2 drone có va
  chạm không?" — Học sinh tính lại: Drone B' đi qua Q(4;2;6) lúc t=2 —
  **CÙNG thời điểm t=2 với Drone A** → **CÓ va chạm** tại (4;2;6).

Mỗi bước có ô nhập kết quả riêng, không giới hạn số lần thử. Sau bước 4,
hiện lại toàn bộ 2 tình huống song song để học sinh đối chiếu trực quan sự
khác biệt "cắt quỹ đạo" vs "va chạm" trên hình 3D (2 đường bay vẽ cùng lúc,
1 case có điểm va chạm đánh dấu nổi bật, 1 case chỉ giao nhau về hình học).

---

## Bảng sai lầm giải quyết theo từng vòng

| Vòng | Sai lầm chính |
|---|---|
| 1 | Sai dấu khi VTCP có thành phần âm; tráo vai trò điểm/VTCP |
| 2 | Cố áp dụng PT chính tắc khi VTCP có thành phần bằng 0 |
| 3 | Cùng phương VTCP mà quên kiểm tra điểm chung (song song vs trùng); không cùng phương mà vội kết luận chéo (quên giải hệ) |
| 4 | Quên tính lại toạ độ theo t (giữ nguyên điểm gốc); nhầm giao điểm với VTCP |
| Capstone | Nhầm "cắt quỹ đạo hình học" với "va chạm cùng thời điểm" |

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** Dùng 1 canvas dùng lại cho 5 phần (4 vòng +
  capstone) — `clearScene()` bắt buộc ở đầu mỗi hàm chuyển vòng.
- ✅ **Toàn bộ số liệu đã verify bằng script Python** — mỗi vòng và capstone
  đều đã tính tay/thế số kiểm tra trước khi đưa vào kịch bản (xem các dòng
  tính toán nền), không có số liệu suy đoán.
- ✅ MCQ đáp án đúng đã xáo vị trí khác nhau giữa các câu; mỗi phương án
  nhiễu đều có giải thích lý do sai cụ thể.
- ©️ **Rà soát bản quyền:** Capstone đổi bối cảnh từ "radar theo dõi va
  chạm"/"2 vật thể" (PPCT gợi ý, gần Vận dụng 3 và BT 5.18 SGK) sang "2
  drone giao hàng" — giữ đúng kỹ thuật cần dạy (phân biệt cắt quỹ đạo và
  va chạm) nhưng khung cảnh và cách đặt câu hỏi (2 bước biến thể liên tiếp
  cùng 1 bộ số liệu) khác cách SGK trình bày.
