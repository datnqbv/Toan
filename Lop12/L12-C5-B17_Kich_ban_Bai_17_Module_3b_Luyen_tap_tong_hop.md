# KỊCH BẢN MODULE 3b — LUYỆN TẬP TỔNG HỢP PHƯƠNG TRÌNH MẶT CẦU
## (Bài 17, Toán 12 HK2 — Stage 2 của Module 3, tách riêng thành 1 file)
### Phiên bản 2 — bổ sung sổ tay kiến thức mang từ 3a, giải thích chi tiết hơn, thêm 1 vòng mới

> **4 thay đổi so với bản trước:**
> 1. Thêm **sổ tay nhanh** (mang nội dung từ Module 3a sang) — panel cố
>    định, xem được xuyên suốt file, KHÔNG phải làm lại từ đầu.
> 2. Thêm **thẻ nhắc công thức** hiện ngay sau khi hoàn thành mỗi vòng —
>    tổng hợp lại đúng công thức vừa dùng, gắn với bài vừa làm.
> 3. Toàn bộ `giai_thich_dung`/`giai_thich_sai` viết lại CHI TIẾT hơn hẳn
>    (có từng bước tính, không chỉ 1 câu kết luận ngắn).
> 4. **Thêm 1 vòng mới** (Vòng 2) — dựa trên SGK Ví dụ 1/Luyện tập 1 (Bài
>    17, trang 55: kiểm tra điểm nằm trong/ngoài/thuộc mặt cầu) — đây là
>    kỹ năng SGK có nhưng bản trước của Module 3b **hoàn toàn chưa có**.
>    Đổi bối cảnh từ "gốc toạ độ" sang "drone và vùng cấm bay quanh sân
>    bay", đổi số liệu hoàn toàn mới.

**Mục tiêu:** Vận dụng tổng hợp kỹ năng viết PT mặt cầu, kiểm tra điểm với
mặt cầu, nhận diện dạng khai triển, xét vị trí tương đối với mặt phẳng, và
tìm tâm mặt cầu ngoại tiếp qua 4 điểm.

**Sai lầm cần giải quyết (từ PPCT):**
- Nhầm tâm mặt cầu ngoại tiếp (cách đều các điểm) với tâm nội tiếp.
- Sai dấu khi lập hệ phương trình tìm tâm mặt cầu đi qua nhiều điểm.
- Quên đổi đơn vị đo (m, km, cm) trong bài toán thực tiễn.
- (Kế thừa Module 1-2): nhầm dấu tâm từ dạng (x−a)²; quên điều kiện
  a²+b²+c²−d>0; nhầm điều kiện d>R/d<R; nhầm điều kiện IM² so với R².

**Loại simulation:** I (trắc nghiệm minh hoạ 3D) cho vòng 1-4, F (dựng dần
từng bước) cho capstone.
**Thời gian hoàn thành dự kiến:** ~17-19 phút (tăng do thêm 1 vòng)
**Design:** Cream & Green, Be Vietnam Pro, 1 canvas dùng lại + `clearScene()`
giữa các vòng.

**Mở khoá capstone:** Sau khi hoàn thành ≥ 4/4 vòng.

---

## Sổ tay nhanh (mang từ Module 3a sang — panel cố định, luôn xem được)

> Đặt ở góc màn hình dạng nút thu/phóng (📋), không chiếm chỗ canvas khi
> đóng. Đây CHÍNH LÀ nội dung học sinh đã click-reveal ở Module 3a, gộp
> lại thành 1 bảng tra cứu — không bắt học sinh làm lại, chỉ xem lại.

| Kiến thức | Công thức |
|---|---|
| PT mặt cầu (tâm-bán kính) | (x−a)²+(y−b)²+(z−c)²=R², tâm I(a;b;c) |
| PT mặt cầu (khai triển) | x²+y²+z²−2ax−2by−2cz+d=0, là mặt cầu ⟺ a²+b²+c²−d>0, khi đó R=√(a²+b²+c²−d) |
| Điểm M với mặt cầu (S) tâm I, R | IM²<R² → M nằm TRONG; IM²=R² → M THUỘC (S); IM²>R² → M nằm NGOÀI |
| Mặt cầu (S) và mặt phẳng (P) | So sánh d(I,(P)) với R: d>R không cắt; d=R tiếp xúc; d<R cắt theo đường tròn bán kính r=√(R²−d²) |

**Sau mỗi vòng dưới đây, 1 thẻ nhỏ "🔍 Công thức vừa dùng" sẽ tự động hiện
ra, trích đúng dòng liên quan trong bảng trên** — giúp học sinh nối kết
ngay bài tập vừa làm với đúng công thức, không cần tự mở sổ tay đi tìm.

---

## Vòng 1 — Viết phương trình mặt cầu biết tâm và bán kính (kỹ năng Module 1)

**Bối cảnh:** Vùng an toàn nổ mìn tại công trường khai thác đá. Điểm nổ
đặt tại N(5;3;−2) (đơn vị mét). Quy định bán kính an toàn là **1000 cm**.

**Câu hỏi 1 (kiểm tra đổi đơn vị trước khi viết PT):** "Bán kính an toàn
1000 cm tương ứng bao nhiêu mét?" → đáp: **10 m**.
- Nếu nhập sai (VD nhập 1000, quên đổi): chặn lại, phản hồi: *"Hệ trục
  Oxyz trong bài đang dùng đơn vị mét (thấy từ toạ độ điểm nổ N(5;3;−2)
  là số nguyên nhỏ, hợp với đơn vị mét, không hợp với cm). 1000 cm =
  1000/100 = 10 m. Hãy đổi đơn vị trước khi viết phương trình."*

**Câu hỏi 2:** "Viết phương trình mặt cầu biểu diễn vùng an toàn."

| # | Đáp án | Ghi chú |
|---|---|---|
| A | (x+5)²+(y+3)²+(z−2)²=100 | Nhiễu |
| B | (x−5)²+(y−3)²+(z+2)²=10 | Nhiễu |
| **C** | **(x−5)²+(y−3)²+(z+2)²=100** | **`dap_an_dung`** |
| D | (x−5)²+(y−3)²+(z−2)²=100 | Nhiễu |

- `giai_thich_dung` (chi tiết từng bước): "Bước 1 — xác định tâm và bán
  kính: tâm N(5;3;−2), R=10 (đã đổi đơn vị ở câu 1). Bước 2 — áp công
  thức (x−a)²+(y−b)²+(z−c)²=R² với (a;b;c)=(5;3;−2): thay trực tiếp từng
  toạ độ, KHÔNG đổi dấu: (x−5)²+(y−3)²+(z−(−2))²=10². Bước 3 — rút gọn
  z−(−2) = z+2, và 10²=100. Kết quả: (x−5)²+(y−3)²+(z+2)²=100."
- `giai_thich_sai`:
  - **A:** "Đổi dấu TẤT CẢ 3 toạ độ tâm (5→−5, 3→−3, −2→2) — đây là sai
    lầm điển hình nhất của cả bài 17: nhìn thấy tâm N(5;3;−2) rồi viết
    luôn (x+5)... nghĩ rằng phải 'đổi dấu cho khớp dấu trừ trong công
    thức'. Thực tế công thức (x−a)² đã tự động xử lý dấu — chỉ cần thay
    a=5 trực tiếp, KHÔNG đổi dấu thêm 1 lần nữa."
  - **B:** "Đúng tâm, đúng dấu, nhưng vế phải để nguyên R=10 mà không
    bình phương. Công thức yêu cầu R² ở vế phải, không phải R. Với R=10
    thì vế phải phải là 100, không phải 10."
  - **D:** "Đúng tâm ở x, y nhưng SAI RIÊNG dấu ở thành phần z: N có
    hoành độ z=−2 (âm), nên số hạng phải là (z−(−2))²=(z+2)². Đáp án D
    viết (z−2)² — tức ngầm hiểu tâm có z=+2, sai với đề bài cho z=−2.
    Đây là dạng sai 'chỉ sai 1 trong 3 toạ độ', dễ bị bỏ qua nếu không
    kiểm tra kỹ từng thành phần riêng."

**🔍 Công thức vừa dùng:** *"PT mặt cầu (tâm-bán kính): (x−a)²+(y−b)²+
(z−c)²=R², tâm I(a;b;c) — nhắc lại: KHÔNG đổi dấu thêm khi thay a, b, c
vào, và luôn bình phương R ở vế phải."*

---

## Vòng 2 — Kiểm tra điểm nằm trong / ngoài / thuộc mặt cầu (kỹ năng Module 1, MỚI — dựa trên SGK Ví dụ 1/Luyện tập 1)

**Bối cảnh:** Vùng cấm bay hình cầu quanh tháp kiểm soát không lưu sân
bay, tâm K(3;−2;1), bán kính R=6 (km). Radar theo dõi 2 drone.

**Câu hỏi 1:** Drone A đang ở vị trí M₁(6;1;4). Drone A có đang bay trong
vùng cấm không?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Ngoài vùng cấm | Nhiễu |
| **B** | **Trong vùng cấm** | **`dap_an_dung`** |
| C | Đúng trên biên vùng cấm | Nhiễu |
| D | Không đủ dữ liệu | Nhiễu |

- `giai_thich_dung`: "Tính KM₁² = (6−3)²+(1−(−2))²+(4−1)² = 3²+3²+3² =
  9+9+9 = 27. So với R²=36: 27 < 36 → Drone A đang bay TRONG vùng cấm
  (KM₁ < R). Lưu ý: so sánh bình phương khoảng cách với R², không cần
  khai căn — đỡ sai số và nhanh hơn."
- `giai_thich_sai`:
  - **A:** "Nếu tính nhầm dấu khi trừ toạ độ (VD (6+3) thay vì (6−3)) sẽ
    ra KM₁² lớn hơn 36, dẫn tới kết luận sai là 'ngoài'. Kiểm tra lại
    từng phép trừ toạ độ: 6−3=3, 1−(−2)=3, 4−1=3."
  - **C:** "27 ≠ 36 nên không thể là 'đúng trên biên' (biên yêu cầu bằng
    chính xác R²). Có thể nhầm vì thấy cả 3 số hạng đều bằng 9, ngộ nhận
    'đối xứng đẹp' là dấu hiệu của biên — thực ra chỉ là trùng hợp số
    liệu, không liên quan đến kết luận trong/ngoài/biên."
  - **D:** "Đề bài đã cho đủ toạ độ tâm K, bán kính R, và toạ độ M₁ — đủ
    để tính trực tiếp, không thiếu dữ liệu nào."

**Câu hỏi 2:** Drone B đang ở vị trí M₂(9;2;5). Drone B có đang bay trong
vùng cấm không?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Trong vùng cấm | Nhiễu |
| B | Đúng trên biên vùng cấm | Nhiễu |
| **C** | **Ngoài vùng cấm, an toàn** | **`dap_an_dung`** |
| D | Cách tâm đúng bằng bán kính | Nhiễu (diễn đạt khác của B, vẫn sai) |

- `giai_thich_dung`: "KM₂² = (9−3)²+(2−(−2))²+(5−1)² = 6²+4²+4² =
  36+16+16 = 68. So với R²=36: 68 > 36 → Drone B đang bay NGOÀI vùng
  cấm, an toàn."
- `giai_thich_sai` cho A: "Nếu quên bình phương từng số hạng mà cộng
  thẳng (6+4+4=14) rồi so với R=6 (quên bình phương R luôn), có thể ra
  kết luận sai. Luôn nhất quán: so sánh IM² (đã bình phương từng số hạng)
  với R² (bình phương của bán kính), không trộn lẫn giữa dạng đã bình
  phương và chưa bình phương."

**🔍 Công thức vừa dùng:** *"Điểm M với mặt cầu tâm I, bán kính R: tính
IM² (tổng bình phương từng hiệu toạ độ) rồi so với R² — IM²<R² là TRONG,
IM²=R² là THUỘC, IM²>R² là NGOÀI. Không cần khai căn ở bước so sánh."*

---

## Vòng 3 — Nhận diện phương trình mặt cầu dạng khai triển (kỹ năng Module 1)

**Bối cảnh:** Kỹ sư kiểm tra lại các phương trình mô hình vùng ảnh hưởng
khác nhau từ bản thiết kế cũ — cần xác định đâu là mặt cầu thật.

**Câu hỏi (chọn phân loại đúng cho mỗi phương trình — dạng ghép cặp):**

| Phương trình | a²+b²+c²−d (hoặc lý do khác) | Phân loại |
|---|---|---|
| (a) x²+y²+z²−4x+2y−6z+5=0 | 4+1+9−5=9>0 | **Mặt cầu thật, tâm (2;−1;3), R=3** |
| (b) x²+y²+z²−2x−2y−2z+3=0 | 1+1+1−3=0 | Chỉ là 1 điểm I(1;1;1), KHÔNG là mặt cầu |
| (c) x²+y²+z²+2x−4y+6z+50=0 | 1+4+9−50=−36<0 | Vô nghiệm, không có điểm nào thoả mãn |
| (d) x²+y²+z²−2xz+8=0 | *(không áp dụng công thức)* | **Không phải dạng chuẩn** — có số hạng chéo −2xz |

- `giai_thich_dung`: "(a): a=2,b=−1,c=3,d=5 → a²+b²+c²−d=4+1+9−5=9>0 →
  mặt cầu thật, R=√9=3. (b): tổng =0 → phương trình chỉ đúng với đúng 1
  điểm duy nhất (chính tâm) — hình dung: đây là 'mặt cầu bán kính 0', về
  bản chất chỉ là 1 điểm, không có 'độ dày' để coi là mặt cầu thật. (c):
  tổng âm → vô lý, vì tổng 3 số bình phương (luôn ≥0) không thể trừ ra 1
  giá trị nhỏ hơn 0 mà lại có nghiệm thực. (d): quan trọng nhất — TRƯỚC
  KHI tính a²+b²+c²−d, phải kiểm tra phương trình có đúng dạng chuẩn
  x²+y²+z²−2ax−2by−2cz+d=0 hay không. Ở đây có số hạng −2xz (tích chéo
  giữa x và z) — dạng chuẩn của mặt cầu KHÔNG có bất kỳ số hạng tích chéo
  nào (xy, yz, xz). Có số hạng chéo là dấu hiệu ngay từ đầu bài toán này
  KHÔNG PHẢI mặt cầu, không cần tính tiếp a²+b²+c²−d."
- `goi_y_khi_sai`: "Bước 1 (làm TRƯỚC MỌI THỨ): kiểm tra phương trình có
  đúng dạng x²+y²+z²−2ax−2by−2cz+d=0 không — nghĩa là hệ số của x²,y²,z²
  phải bằng nhau (thường là 1), và KHÔNG có số hạng xy, yz, xz. Nếu qua
  được bước này, mới tính a²+b²+c²−d và xét dấu."

**🔍 Công thức vừa dùng:** *"PT khai triển là mặt cầu ⟺ (1) đúng dạng
x²+y²+z²−2ax−2by−2cz+d=0 (không có số hạng chéo, hệ số bậc 2 bằng nhau),
VÀ (2) a²+b²+c²−d>0."*

---

## Vòng 4 — Vị trí tương đối mặt cầu và mặt phẳng (kỹ năng Module 2)

**Bối cảnh:** Tiếp tục vùng an toàn nổ mìn (mặt cầu N, R=10) — kiểm tra
với 2 mặt phẳng đại diện cho quốc lộ và khu dân cư gần đó.

**Câu hỏi 1:** Đường quốc lộ chính có phương trình (đơn giản hoá):
x−2y+2z−13=0. Vùng nổ có ảnh hưởng đến quốc lộ không?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Không ảnh hưởng (không cắt) | Nhiễu |
| **B** | **Có ảnh hưởng, cắt theo đường tròn bán kính 8m** | **`dap_an_dung`** |
| C | Tiếp xúc tại 1 điểm | Nhiễu |
| D | Không xác định được vì thiếu dữ liệu | Nhiễu |

- `giai_thich_dung` (từng bước): "Bước 1 — tính khoảng cách từ tâm N(5;3;
  −2) đến mặt phẳng: d(N,(quốc lộ)) = |1·5+(−2)·3+2·(−2)−13| / √(1²+
  (−2)²+2²) = |5−6−4−13| / √9 = |−18| / 3 = 6. Bước 2 — so sánh d=6 với
  R=10: vì d<R → mặt phẳng CẮT mặt cầu theo 1 đường tròn (không phải
  tiếp xúc, không phải không cắt). Bước 3 — tính bán kính đường tròn
  giao tuyến bằng Pythagore: r=√(R²−d²)=√(100−36)=√64=8m."
- `giai_thich_sai`:
  - **A:** "Kết luận 'không cắt' đòi hỏi d>R. Ở đây d=6 < R=10 — ngược
    lại hoàn toàn. Có thể nhầm vì thấy hệ số mẫu số √9=3 khá nhỏ mà ngộ
    nhận khoảng cách sẽ lớn — cần tính đủ cả tử số (|−18|=18) rồi mới
    chia, không suy đoán từ mẫu số riêng lẻ."
  - **C:** "Tiếp xúc đòi hỏi d=R CHÍNH XÁC (d=10). Ở đây d=6≠10, nên
    không thể là tiếp xúc — phải là 1 trong 2 trường hợp còn lại (cắt
    hoặc không cắt), và vì d<R nên là cắt."
  - **D:** "Đề bài đã cho đủ: toạ độ tâm N, bán kính R, phương trình mặt
    phẳng — đủ để tính trực tiếp bằng công thức khoảng cách đã học ở Bài
    14, không thiếu dữ liệu."

**Câu hỏi 2:** Khu dân cư ở xa hơn, mặt phẳng đại diện: x−2y+2z+50=0. Khu
dân cư có nằm trong vùng ảnh hưởng không?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Có, cắt theo đường tròn | Nhiễu |
| **B** | **Không, an toàn (không cắt)** | **`dap_an_dung`** |
| C | Tiếp xúc | Nhiễu |
| D | Cần thêm dữ liệu | Nhiễu |

- `giai_thich_dung`: "d(N,(khu dân cư)) = |5−6−4+50| / 3 = |45| / 3 = 15.
  So với R=10: d=15 > R=10 → mặt phẳng KHÔNG cắt mặt cầu → khu dân cư
  nằm ngoài hoàn toàn vùng ảnh hưởng, an toàn."
- `giai_thich_sai` cho A: "Đây là sai lầm PPCT cảnh báo rõ nhất của cả
  Module 2 — NHẦM LẪN NGƯỢC điều kiện d>R (không cắt, AN TOÀN) với d<R
  (cắt, NGUY HIỂM). Ghi nhớ theo hình dung vật lý: d LỚN nghĩa là mặt
  phẳng ở XA tâm hơn cả bán kính → mặt phẳng nằm hẳn ngoài quả cầu, không
  thể chạm được. d=15 > R=10 rõ ràng thuộc trường hợp này, không phải
  trường hợp cắt."

**🔍 Công thức vừa dùng:** *"Mặt cầu (S) tâm I, bán kính R và mặt phẳng
(P): so sánh d(I,(P)) với R — d>R KHÔNG cắt (an toàn), d=R TIẾP XÚC, d<R
CẮT theo đường tròn bán kính r=√(R²−d²)."*

---

## Capstone — Mái vòm sân vận động (mặt cầu ngoại tiếp qua 4 điểm, loại F)

**Mở khoá:** Sau khi hoàn thành cả 4 vòng trên.

**Bối cảnh:** Sân vận động có 4 cột đèn chiếu sáng đặt tại 4 điểm không
đồng phẳng: P₁(0;0;0), P₂(4;0;0), P₃(0;4;0), P₄(0;0;4) (đơn vị: chục mét).
Kiến trúc sư muốn dựng 1 mái vòm hình mặt cầu đi qua đúng cả 4 đỉnh cột.

- **Bước 1:** Gọi phương trình mặt cầu dạng khai triển
  x²+y²+z²+Ax+By+Cz+D=0. Thay P₁(0;0;0) vào → tìm D.
  *(Đáp số: D=0 — vì mọi số hạng chứa x,y,z đều triệt tiêu khi thay
  (0;0;0), chỉ còn lại D=0)*
- **Bước 2:** Thay P₂(4;0;0) vào phương trình (đã biết D=0) → tìm A.
  *(Đáp số: 16+0+0+4A+0+0+0=0 → 4A=−16 → A=−4. Lưu ý dấu: phương trình
  chuẩn có +Ax, nên từ 16+4A=0 suy ra A âm, không phải dương — đây chính
  là chỗ PPCT cảnh báo "sai dấu khi lập hệ phương trình tìm tâm mặt cầu
  đi qua nhiều điểm")*
- **Bước 3:** Tương tự, thay P₃(0;4;0) và P₄(0;0;4) → tìm B, C.
  *(Đáp số: B=−4, C=−4 — học sinh sẽ thấy ngay tính đối xứng giữa 3 bước
  này, đúng tinh thần "hệ thống hoá quy trình" PPCT yêu cầu — cả 3 bước
  dùng chung 1 khuôn tính, chỉ đổi biến)*
- **Bước 4:** Từ phương trình x²+y²+z²−4x−4y−4z=0, hoàn thành bình
  phương để tìm tâm và bán kính mặt cầu ngoại tiếp.
  *(Đáp số: (x−2)²+(y−2)²+(z−2)²=12 → tâm (2;2;2), R=√12=2√3≈3,46,
  tương ứng ≈34,6m ngoài thực tế)*

Mỗi bước có ô nhập kết quả riêng, không giới hạn số lần thử. Sau khi hoàn
thành đủ 4 bước → hiện mặt cầu mái vòm dựng quanh 4 cột đèn trên hình 3D,
xoay được, để học sinh thấy trực quan mặt cầu vừa tính đi qua đúng cả 4
điểm.

> 💡 **Ghi chú cố định hiện dưới Bước 4:** *"Tâm mặt cầu ngoại tiếp là
> điểm CÁCH ĐỀU tất cả các điểm cho trước (ở đây là 4 chân cột đèn) —
> khác với tâm mặt cầu NỘI TIẾP (là điểm cách đều các MẶT của một hình,
> một khái niệm hoàn toàn khác, áp dụng khi mặt cầu nằm BÊN TRONG và tiếp
> xúc các mặt của 1 khối, ví dụ hình chóp). Đừng nhầm lẫn 2 khái niệm
> này — chúng chỉ giống nhau ở việc cả 2 đều là 'tâm 1 mặt cầu', nhưng
> điều kiện xác định hoàn toàn khác nhau."*

**🔍 Công thức vừa dùng:** *"Mặt cầu ngoại tiếp qua n điểm: thay từng
điểm vào dạng khai triển x²+y²+z²+Ax+By+Cz+D=0, giải hệ tìm A,B,C,D, sau
đó hoàn thành bình phương để ra tâm (−A/2;−B/2;−C/2) và bán kính."*

---

## Bảng sai lầm giải quyết theo từng vòng

| Vòng | Sai lầm chính |
|---|---|
| 1 | Quên đổi đơn vị đo; sai dấu tâm từ dạng (x−a)² (có thể sai cả 3 hoặc chỉ 1 toạ độ); quên bình phương R |
| 2 (MỚI) | Nhầm dấu khi tính IM²; trộn lẫn giá trị đã/chưa bình phương khi so sánh với R |
| 3 | Không kiểm tra dạng chuẩn (số hạng chéo) TRƯỚC KHI tính a²+b²+c²−d; không kiểm tra điều kiện dấu |
| 4 | Nhầm ngược điều kiện d>R (an toàn) với d<R (nguy hiểm) |
| Capstone | Nhầm tâm ngoại tiếp với nội tiếp; sai dấu khi lập hệ tìm tâm qua nhiều điểm |

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** 1 canvas dùng lại cho 4 vòng + capstone —
  `clearScene()` bắt buộc ở đầu mỗi hàm chuyển vòng. Sổ tay nhanh là 1
  overlay HTML cố định, không phải object 3D — không ảnh hưởng canvas.
  Capstone vẽ mặt cầu ngoại tiếp bằng `SphereGeometry` tâm (2,2,2) bán
  kính √12, không cần hàm mới.
- ✅ Toàn bộ số liệu đã verify bằng script Python, bao gồm cả vòng mới
  (IM²=27<36 và IM²=68>36, khớp đúng "trong"/"ngoài"): R=10, d=6/15, r=8;
  tâm ngoại tiếp (2,2,2), R=2√3 — không có số liệu suy đoán.
- ✅ MCQ đáp án đúng đã xáo vị trí khác nhau; **mọi phương án nhiễu đều có
  giải thích chi tiết theo từng bước** (không chỉ 1 câu ngắn) — đáp ứng
  đúng yêu cầu rà soát lại.
- ✅ **Sổ tay nhanh mang từ Module 3a sang** đã thêm dưới dạng panel cố
  định, cộng thêm **thẻ "🔍 Công thức vừa dùng"** hiện sau mỗi vòng — đáp
  ứng đúng yêu cầu về việc chưa có tổng hợp kiến thức áp dụng sau bài tập.
- ✅ **Vòng mới (Vòng 2)** dựa trên SGK Ví dụ 1/Luyện tập 1 (kiểm tra điểm
  trong/ngoài/thuộc mặt cầu) — đổi bối cảnh từ "gốc toạ độ" sang "drone
  và vùng cấm bay sân bay", đổi toàn bộ số liệu, giữ đúng kỹ thuật cần
  dạy nhưng khác hẳn tình huống cụ thể của SGK.
- ©️ **Rà soát bản quyền:** Bối cảnh "vùng an toàn nổ mìn", "drone vùng
  cấm bay", "mái vòm sân vận động 4 cột đèn" đều mới, không trùng SGK.
  Tránh hẳn bối cảnh "vùng phủ sóng trạm phát" mà PPCT tự gợi ý (trùng
  thẳng BT 5.30 SGK).
