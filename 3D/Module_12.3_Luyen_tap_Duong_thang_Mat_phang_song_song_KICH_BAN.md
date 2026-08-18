# 📋 KỊCH BẢN SIMULATION — MODULE 12.3
## Luyện tập đường thẳng và mặt phẳng song song

**Bài SGK:** Bài 12 — Đường thẳng và mặt phẳng song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 12.3 — nối tiếp Module 12.1 (Định
nghĩa và điều kiện đủ), Module 12.2 (Phương pháp chứng minh). Tương ứng Tiết 32.
**Trạng thái kiến thức nền:** Đã dạy qua Module 12.1–12.2 trong cùng hệ thống —
12.3 KHÔNG dạy lại lý thuyết, chỉ luyện tập áp dụng.
**Nhân vật dẫn dắt:** Athena — avatar góc sidebar, đưa gợi ý mở đầu mỗi tab và
gợi ý khi học sinh trả lời sai ở Tab 4. Không dùng từ "robot"/"AI" ở bất kỳ đâu.

---

## 🎯 MỤC TIÊU TOÀN BÀI

- HIỂU: phân biệt được 3 dạng bài luyện tập (chứng minh song song / xác định
  giao tuyến / tìm thiết diện) tuy khác nhau về yêu cầu nhưng cùng dùng chung
  1 công cụ nền — quan hệ song song đường thẳng–mặt phẳng.
- LÀM ĐƯỢC:
  - Dạng 1: trình bày đúng trình tự 3 bước chứng minh a // (α)
  - Dạng 2: dựng đúng đường phụ (song song với đường đã biết) để tìm giao
    tuyến của 2 mặt phẳng
  - Dạng 3: xác định đủ tất cả các cạnh của thiết diện, không bỏ sót mặt nào
    của khối

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT (áp dụng xuyên suốt 4 tab)

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Viện dẫn sai tính chất — nhầm "có điểm chung" với "cắt nhau" | Không phân biệt rõ định nghĩa song song (không điểm chung) và các mệnh đề gây nhiễu | Kết luận sai dù lập luận có vẻ "nghe hợp lý" |
| Dựng nhầm đường phụ khi tìm giao tuyến | Dựng đường tuỳ ý thay vì bắt buộc phải đi qua 1 điểm đã có và song song với đường cho trước | Giao tuyến vẽ ra không thực sự nằm chung trên cả 2 mặt phẳng |
| Xác định thiết diện thiếu mặt | Dừng lại sau khi tìm được 2-3 giao tuyến, quên kiểm tra hết các mặt còn lại của khối | Thiết diện "hở", không khép kín thành đa giác |
| Hình dung không gian sai | Nhìn hình biểu diễn (phối cảnh 2D) rồi suy luận sai vì "trông giống" 1 quan hệ khác trong 3D | Nhận định ban đầu sai, chỉ lộ ra khi xoay camera |

## 🎨 THIẾT KẾ & KỸ THUẬT (áp dụng chung cả 4 tab)

**Màu đối tượng** (theo bảng chuẩn `04_design_toan_3d.md` §1.3 — không dùng
tên biến tự phát):
```javascript
const COLOR_PLANE_1    = 0x3b82f6;  // Xanh dương — mặt phẳng thứ nhất
const COLOR_PLANE_2    = 0xa78bfa;  // Tím nhạt   — mặt phẳng thứ hai
const COLOR_PLANE_3    = 0x34d399;  // Xanh ngọc  — mặt bên phụ (case hình hộp)
const COLOR_PLANE_BASE = 0x64748b;  // Xám trung tính — mặt đáy khối
const COLOR_RESULT     = 0xFAC775;  // Vàng cam sáng  — giao tuyến/thiết diện/điểm mới dựng
const COLOR_CONNECTOR  = 0x94a3b8;  // Xám nhạt, opacity 0.4 — đường phụ dựng thêm
const COLOR_EDGE_SOLID = 0xe6edf3;  // Cạnh khối nhìn thấy
const COLOR_EDGE_HIDDEN= 0x444d56;  // Cạnh khối bị khuất (nét đứt, opacity 0.5)
// Opacity mặt phẳng chính: 0.18–0.25, không vượt 0.35 trên nền tối
```

**Font:** Be Vietnam Pro (Google Fonts).

**Bố cục Desktop (≥1024px):** Header 1 dòng cố định "🧊 Hình học không gian"
(không hiện tên module cụ thể trong header) + Canvas trái `flex:1`, tối thiểu
500px + Sidebar phải 310px chứa step-tabs.

**Bố cục Mobile (≤768px):** Stack dọc — canvas lên trên `min-height:320px`
cố định, sidebar xuống dưới để chiều cao tự nhiên, cuộn theo trang (không ép
`height:50%`, không cuộn nội bộ riêng). Có 4 tab vẫn dùng stack dọc thường,
KHÔNG chuyển sang lướt ngang (khác quy tắc Toán 2D — canvas 3D nằm trong khối
cố định riêng, không bị cuộn trang đẩy ra khỏi màn hình).

**Ánh xạ thao tác Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Kéo điểm dựng thiết diện/giao tuyến | Kéo chuột (Pointer Events) | Kéo ngón tay — cùng handler, bắt buộc `touch-action:none` trên canvas khi đang kéo |
| Click chọn điểm/giao điểm/cạnh | Click chuột | Tap — giữ nguyên vùng hit-mesh |
| Chọn đáp án MCQ (Tab 4) | Click nút | Tap — vùng chạm nút tối thiểu 44×44px |

**Cleanup:** `clearScene()` bắt buộc mỗi khi chuyển sub-step trong cùng 1 tab
(dispose object 3D cũ trước khi dựng đối tượng mới) — tránh lỗi canvas rối do
object cũ còn sót lại đã từng gặp ở Bài 10.

---

## TAB 1 — Chứng minh đường thẳng song song mặt phẳng

**Mục tiêu:** Áp dụng đúng quy trình 3 bước để chứng minh 1 đường thẳng song
song với 1 mặt phẳng trong hình chóp tam giác.
**Sai lầm cần giải quyết:** Viện dẫn sai tính chất; bỏ sót bước kiểm tra
d ⊄ (α) trước khi kết luận.
**Loại simulation:** F (dựng dần từng bước) + nhận định đúng/sai.
**Thời gian hoàn thành dự kiến:** ~3–4 phút.

### Màn hình chính hiển thị:
- Hình chóp tam giác **S.MNP** (đáy tam giác MNP, đỉnh S) — khối cạnh trắng
  sáng `COLOR_EDGE_SOLID`, cạnh khuất nét đứt `COLOR_EDGE_HIDDEN`.
- Điểm **I, K** lần lượt trên SM, SN sao cho **SI = ⅓SM, SK = ⅓SN** (đặt
  sẵn, màu `COLOR_RESULT`) — cố ý dùng tỉ lệ ⅓ thay vì trung điểm để buộc
  lý luận bằng tam giác đồng dạng tỉ số, tránh trùng cách giải "đường trung
  bình" của bài 4.17 SGK.
- Mặt đáy (MNP) tô nhẹ `COLOR_PLANE_BASE`, opacity 0.2.
- Nhãn tên điểm bằng HTML overlay, đúng theo đúng vị trí 3D.

### Sổ tay kiến thức (Có — tự bấm gọi ra phía trên canvas):
- Định nghĩa: d // (α) ⟺ d và (α) không có điểm chung
- Quy trình 3 bước: (1) Tìm đường b nằm trong (α) sao cho b // d; (2) Chứng
  minh d // b; (3) Kết luận d // (α) (kèm điều kiện d ⊄ (α))

### Học sinh tương tác bằng cách:
1. Quan sát hình chóp S.MNP với I, K trên SM, SN sao cho SI=⅓SM, SK=⅓SN đã
   đánh dấu sẵn.
2. Trả lời câu hỏi dự đoán: "IK có song song với mặt phẳng (MNP) không?"
   (chọn Có/Không).
3. Bấm "Dựng đường phụ" — hệ thống tự vẽ đường MN trong mặt đáy (màu
   `COLOR_CONNECTOR`) để học sinh đối chiếu IK // MN.
4. Kéo camera xoay để tự kiểm chứng IK và MN không cắt nhau, cùng nằm trên
   2 mặt phẳng song song về mặt thị giác.
5. Trả lời 1 câu nhận định đúng/sai (bẫy tính chất, xem bên dưới).
6. Xem kết luận đầy đủ 3 bước.

### Trước mỗi bước tương tác:

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | Chọn "Có" hoặc "Không" cho dự đoán ban đầu | Vì SI/SM = SK/SN = ⅓ (cùng tỉ lệ trên 2 cạnh SM, SN của tam giác SMN), theo định lí Talet đảo trong tam giác, IK // MN |
| 2 | Bấm "Dựng đường phụ" để hệ thống vẽ MN | MN nằm trong mặt phẳng đáy (MNP) |
| 3 | Xoay camera để quan sát, sau đó bấm "Tiếp tục" | Nếu IK // MN và MN ⊂ (MNP) thì theo điều kiện đủ, IK // (MNP) |
| 4 | Chọn Đúng/Sai cho nhận định | Phân biệt "có điểm chung" và "cắt nhau" — không phải cứ có 1 điểm chung là cắt nhau theo mọi nghĩa mơ hồ, mà phải xét đúng định nghĩa |

### Nhận định đúng/sai (viết mới, không trùng cấu trúc 4.16 SGK):

> "Nếu đường thẳng d không nằm trong mặt phẳng (α) và d không cắt (α) tại
> điểm nào, thì chắc chắn tồn tại một đường thẳng b nằm trong (α) sao cho
> d // b."

- **Đáp án: Đúng.**
- `giai_thich_dung`: Đúng, đây chính là chiều ngược của tính chất d // (α):
  nếu d // (α) thì mọi mặt phẳng chứa d cắt (α) theo giao tuyến song song d,
  nên luôn tìm được ít nhất 1 đường thẳng b ⊂ (α) mà d // b.
- `goi_y_khi_sai`: Thử nghĩ lại: nếu d không có điểm chung nào với (α), quan
  hệ giữa d và (α) là gì theo đúng định nghĩa đã học ở Module 12.1?

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể dự đoán sai "Không" ở bước 1 vì chỉ nhìn hình
  vẽ phẳng, không tính ra được tỉ lệ SI/SM = SK/SN dẫn tới IK // MN.
- Hệ thống phản hồi: Không phán xét ngay, cho xem đường phụ MN trước, để học
  sinh tự đối chiếu bằng mắt trước khi kết luận lại.
- Học sinh điều chỉnh: Xoay camera quan sát, nhận ra IK // MN, tự sửa lại dự
  đoán.
- Kết quả rút ra: Hiểu được vai trò của "đường phụ trong mặt phẳng" như là
  công cụ trung gian để chứng minh song song, không chứng minh trực tiếp
  "không điểm chung" bằng mắt.

### Giải thích kiến thức:

| Trạng thái | Caption (procedural) | Giải thích kiến thức (conceptual) |
|---|---|---|
| Dự đoán đúng ("Có") | Chính xác, cùng kiểm chứng bằng đường phụ nhé | SI/SM = SK/SN = ⅓ nên theo định lí Talet đảo, IK // MN — đây là cách suy luận bằng tỉ số, khác với đường trung bình (chỉ áp dụng khi là trung điểm) |
| Dự đoán sai ("Không") | Chưa đúng, hãy quan sát đường phụ MN mình vừa dựng | I, K chia SM, SN theo đúng cùng 1 tỉ lệ ⅓ nên IK song song cạnh đáy MN — đây là dấu hiệu nhận biết đường phụ theo tỉ số Talet |
| Nhận định sai (chọn "Sai") | Chưa đúng, thử lại | Đã nêu ở `goi_y_khi_sai` phía trên |
| Sau khi hoàn thành Tab 1 | — | Chốt lại: muốn chứng minh d // (α), luôn cần 1 đường phụ b ⊂ (α) với b // d — không chứng minh trực tiếp "không điểm chung" bằng cách nhìn hình |

### Cấu hình 3D:
- **Khối nền:** Hình chóp tam giác S.MNP (không dùng SOLID_LIBRARY sẵn có,
  dựng riêng theo tỉ lệ đơn giản để I, K dễ quan sát).
- **Đối tượng kéo được:** Không có (chỉ OrbitControls xoay/zoom).
- **Góc camera mặc định:** Nhìn chéo từ trên, thấy rõ cả đáy MNP và đỉnh S.
- **Quan hệ hình học cần tính:** tính điểm I, K theo đúng tỉ lệ SI=⅓SM,
  SK=⅓SN (lerp theo tỉ số, không phải trung điểm — chú ý code build không
  dùng hàm midpoint mặc định).
- **Yếu tố hiển thị kèm:** Nhãn tên điểm; đường MN tô màu `COLOR_CONNECTOR`
  khi bấm "Dựng đường phụ"; đường IK tô `COLOR_RESULT` khi kết luận.
- **Cleanup:** `clearScene()` khi chuyển sang Tab 2.

### Nút và điều khiển:
- **Dựng đường phụ:** vẽ MN trong mặt đáy.
- **Tiếp tục:** chuyển sang câu nhận định đúng/sai.
- **Đặt lại góc nhìn:** reset camera về góc chuẩn.

---

## TAB 2 — Xác định giao tuyến khi biết đường thẳng song song mặt phẳng

**Mục tiêu:** Dựng đúng đường phụ qua 1 điểm cho trước, song song với đường
đã biết, để xác định giao tuyến của 2 mặt phẳng.
**Sai lầm cần giải quyết:** Dựng đường phụ tuỳ ý thay vì bắt buộc đi qua điểm
đã có và song song đúng đường cho trước.
**Loại simulation:** D3 (click chọn điểm dựng đường phụ), tái dùng pattern
Tab 1/2 của file Bài 10 Simulation 2 (`t1StartPointSelection`/raycaster).
**Thời gian hoàn thành dự kiến:** ~4–5 phút.

### Màn hình chính hiển thị:
- Hình chóp tứ giác **S.ABCD**, đáy là **hình bình hành** ABCD (AD // BC,
  AB // DC — khác hẳn cấu hình "đáy hình thang" của SGK).
- Điểm **E** trên cạnh SA, ở vị trí tỉ lệ **SE = ⅓SA** (không phải trung
  điểm như Ví dụ 4/4.19 SGK).
- Mặt phẳng (P) qua E, song song với **AD** (một cạnh bên đáy, khác cặp
  AB//CD mà SGK hay dùng).

### Sổ tay kiến thức (Có):
- Tính chất: nếu d // (α) và (β) ⊃ d, (β) cắt (α) theo giao tuyến b thì b // d
- Quy trình dựng giao tuyến: xác định 1 điểm chung của 2 mặt phẳng → dựng
  đường qua điểm đó, song song với đường đã biết song song mặt phẳng còn lại

### Học sinh tương tác bằng cách:
1. Quan sát hình chóp S.ABCD và điểm E trên SA (SE = ⅓SA) đã đặt sẵn.
2. Đọc đề: "(P) là mặt phẳng qua E, song song với AD. Tìm giao tuyến của (P)
   với mặt bên (SAD)."
3. Bấm "Chọn điểm" rồi click đúng vị trí trên cạnh SD sao cho đường nối với
   E song song AD (hệ thống raycast kiểm tra khoảng cách tới điểm đúng).
4. Nếu chọn đúng: hệ thống nối E với điểm vừa chọn thành giao tuyến, tô màu
   `COLOR_RESULT`.
5. Nếu chọn sai: hiệu ứng rung nhẹ, không lộ đáp án ngay (theo đúng số lần
   thử ở bảng dưới).
6. Lặp lại cho mặt bên còn lại (SBC) để hoàn thành thiết diện tam giác.

### Trước mỗi bước tương tác:

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | Đọc đề, quan sát điểm E trên SA | (P) qua E, song song AD |
| 2 | Bấm "Chọn điểm", click trên cạnh SD | Vì AD ⊂ (SAD) và (P) // AD, giao tuyến của (P) với (SAD) phải song song AD |
| 3 | Xác nhận điểm vừa chọn | Điểm cần tìm chia SD theo đúng tỉ lệ SE:SA (định lí Thalès trong không gian, đã học ở Bài 13 nếu học trước, hoặc suy từ tam giác đồng dạng) |
| 4 | Lặp lại cho cạnh SC | Cùng nguyên tắc — giao tuyến với (SBC) cũng phải song song AD (vì BC // AD) |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể click bừa 1 điểm bất kỳ trên SD mà không tính
  tỉ lệ, nghĩ "chỉ cần nằm trên SD là được".
- Hệ thống phản hồi: Rung nhẹ báo sai lần 1, không giải thích ngay.
- Lần sai thứ 2: hiện gợi ý "Thử kẻ 1 đường thẳng tưởng tượng từ E, giữ đúng
  hướng song song AD — nó cắt SD ở đâu?"
- Lần sai thứ 3: hiện đáp án đúng, giải thích đầy đủ bằng tỉ lệ Thalès.
- Kết quả rút ra: Giao tuyến không phải "đường nối 2 điểm tuỳ ý cùng nằm
  trong 2 mặt phẳng", mà phải thoả điều kiện song song với đường đã biết.

### Giải thích kiến thức:

| Trạng thái | Caption | Giải thích kiến thức |
|---|---|---|
| Chọn đúng điểm trên SD (lần đầu) | Chính xác! | Đường vừa dựng song song AD vì (P) // AD và cả 2 đường cùng nằm trong mặt phẳng (SAD) |
| Sai lần 1 | Chưa đúng, thử lại | (không giải thích, chỉ hiệu ứng rung) |
| Sai lần 2 | Gợi ý xem trên | Đã nêu ở kịch bản trên |
| Sai lần 3 | Hiện đáp án đúng | Điểm cần chọn chia SD theo đúng tỉ lệ SE:EA — vì tam giác SAD có E, F cùng thoả EF // AD nên SE/SA = SF/SD |
| Sau khi hoàn thành Tab 2 | — | Chốt: giao tuyến của (P) với 1 mặt phẳng chứa đường d (mà (P) // d) luôn song song d — đây là công cụ chính để dựng đúng giao tuyến, không đoán mò |

### Cấu hình 3D:
- **Khối nền:** Hình chóp tứ giác S.ABCD, đáy hình bình hành.
- **Đối tượng kéo được:** Không kéo tự do — dùng click-to-select tại các vị
  trí candidate trên cạnh SD, SC (hit-mesh ẩn dọc theo cạnh).
- **Góc camera mặc định:** `setCameraStandardSGK()` — giữ nhất quán với Bài
  10.
- **Quan hệ hình học cần tính:** hàm tính điểm chia đoạn theo tỉ lệ (tương tự
  `lerpVectors` đã dùng ở file mẫu), kiểm tra khoảng cách click tới điểm đúng.
- **Yếu tố hiển thị kèm:** Mặt phẳng (P) tô `COLOR_PLANE_1` opacity 0.2; giao
  tuyến tô `COLOR_RESULT` sau khi dựng đúng.
- **Cleanup:** `clearScene()` khi chuyển sang Tab 3.

### Nút và điều khiển:
- **Chọn điểm:** bật chế độ raycast chọn điểm trên cạnh.
- **Đặt lại góc nhìn:** reset camera.

---

## TAB 3 — Tìm thiết diện

**Mục tiêu:** Xác định đủ tất cả các cạnh của thiết diện khi mặt phẳng cắt
song song với 1 đường/mặt cho trước, không bỏ sót mặt nào của khối.
**Sai lầm cần giải quyết:** Thiết diện thiếu mặt — dừng lại sau khi tìm được
2-3 giao tuyến.
**Loại simulation:** F (dựng dần từng cạnh thiết diện, checklist `.done`) —
tái dùng pattern `t5bNextStep` của file Bài 10 Simulation 2.
**Thời gian hoàn thành dự kiến:** ~5–6 phút.

### Sub-pills: Case A (hình chóp) / Case B (hình hộp)

### CASE A — Hình chóp đáy hình bình hành, cắt song song 1 cạnh bên

**Đề bài (viết mới, khác 4.19):** Hình chóp tứ giác S.ABCD, đáy ABCD là hình
bình hành. Gọi G là điểm trên cạnh SB sao cho SG = 2GB. Mặt phẳng (Q) đi qua
G và song song với mặt phẳng (SAD) (khác hẳn việc song song với 2 cạnh đáy
như Ví dụ 4/4.19 — ở đây song song với cả 1 MẶT PHẲNG, thiết diện thu được là
tam giác, không phải hình bình hành EFGH như SGK).

### Học sinh tương tác bằng cách:
1. Quan sát khối và điểm G đã đặt sẵn trên SB.
2. Đọc đề, xác định (Q) song song mặt (SAD) — nghĩa là (Q) không cắt (SAD)
   ở bất kỳ đường nào bên trong khối.
3. Bấm "Dựng cạnh 1" — hệ thống hỏi: cạnh này phải song song với đường nào
   trong (SAD)? (chọn giữa SA / SD / AD qua choice-group).
4. Sau khi chọn đúng, hệ thống tự vẽ cạnh thiết diện qua G, song song đường
   đã chọn, cắt 1 cạnh khác của khối tại điểm mới (đặt tên tự động H).
5. Lặp lại "Dựng cạnh 2", "Dựng cạnh 3" cho đến khi thiết diện khép kín
   (checklist 3 mục `.done`).
6. Xem kết luận: thiết diện là tam giác GHK.

### CASE B — Hình hộp, cắt song song mặt chéo

**Đề bài (viết mới, khác 4.20):** Hình hộp ABCD.A'B'C'D'. Gọi M là trung
điểm cạnh AA'. Mặt phẳng (R) qua M, song song với mặt chéo (BDD'B') (khác
hẳn bài 4.20 vốn hỏi về mặt phẳng cố định của cửa xoay — ở đây là bài dựng
thiết diện cụ thể qua 1 điểm cho trước).

### Học sinh tương tác bằng cách (tương tự Case A):
1. Quan sát hình hộp và điểm M trên AA'.
2. Dựng từng cạnh thiết diện — mỗi cạnh phải song song với 1 trong 2 đường
   chéo BD hoặc B'D' của mặt (BDD'B').
3. Hoàn thành thiết diện (thường là hình bình hành hoặc lục giác tuỳ vị trí
   M — hệ thống tính đúng theo toạ độ đã dựng sẵn).

### Trước mỗi bước tương tác (áp dụng cả 2 case):

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | Đọc đề, xác định mặt phẳng (Q)/(R) song song với mặt nào | (Q) // (SAD) nghĩa là (Q) không có điểm chung nào với (SAD) |
| 2 | Bấm "Dựng cạnh", chọn đúng đường trong mặt đã cho để song song | Nếu (Q) // (SAD) thì giao tuyến của (Q) với bất kỳ mặt nào chứa 1 đường của (SAD) đều song song đường đó |
| 3 | Lặp lại đến khi checklist đủ | Phải kiểm tra HẾT các mặt của khối tiếp giáp với (Q)/(R), không dừng sớm |
| 4 | Xem kết luận thiết diện | Thiết diện là đa giác khép kín gồm các đoạn giao tuyến vừa dựng |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh dựng xong 2 cạnh thấy "có vẻ đã đủ hình" rồi bấm Kết
  luận sớm, trong khi khối còn 1-2 mặt chưa được kiểm tra.
- Hệ thống phản hồi: Nút "Kết luận" chỉ sáng lên (đủ điều kiện bấm) khi
  checklist đã đủ số mục `.done` tương ứng số mặt cần cắt qua — nếu bấm sớm
  khi chưa đủ, hiện cảnh báo "Thiết diện chưa khép kín, còn mặt nào chưa được
  kiểm tra?"
- Học sinh điều chỉnh: quay lại rà từng mặt còn thiếu.
- Kết quả rút ra: Quy trình tìm thiết diện luôn phải rà đủ TẤT CẢ các mặt
  tiếp giáp, không dừng khi "trông có vẻ đủ".

### Giải thích kiến thức:

| Trạng thái | Caption | Giải thích kiến thức |
|---|---|---|
| Chọn đúng đường song song | Chính xác! | Giải thích cụ thể theo case, dựa trên tính chất giao tuyến 2 mặt phẳng song song |
| Chọn sai đường | Chưa đúng, xem lại | (Q)/(R) chỉ song song với 1 mặt phẳng cụ thể — cần xác định đúng đường nằm trong mặt đó, không phải cạnh bất kỳ của khối |
| Bấm Kết luận khi chưa đủ | Thiết diện chưa khép kín | Rà lại đủ các mặt tiếp giáp — xem checklist còn mục nào chưa `.done` |
| Sau khi hoàn thành Tab 3 | — | Chốt: thiết diện là toàn bộ các giao tuyến của mặt cắt với TẤT CẢ các mặt của khối mà nó đi qua — bỏ sót 1 mặt là thiết diện sai |

### Cấu hình 3D:
- **Case A — Khối nền:** Hình chóp tứ giác đáy hình bình hành (dùng lại cấu
  trúc Tab 2, đổi vị trí điểm G).
- **Case B — Khối nền:** Hình hộp `ABCD.A'B'C'D'` (SOLID_LIBRARY nếu có sẵn).
- **Đối tượng kéo được:** Không kéo tự do — chọn qua choice-group xác định
  hướng song song, hệ thống tự vẽ.
- **Góc camera mặc định:** `setCameraStandardSGK()` (Case A),
  `setCameraTetraSGK()` hoặc góc tương tự phù hợp hình hộp (Case B).
- **Quan hệ hình học cần tính:** dựng đường qua 1 điểm song song 1 đường cho
  trước trong mặt phẳng (tương tự pattern `animateBuildParallelLine`).
- **Yếu tố hiển thị kèm:** Thiết diện tô `COLOR_RESULT`, opacity 0.5; checklist
  từng cạnh `.done` ở sidebar.
- **Cleanup:** `clearScene()` khi chuyển đổi giữa Case A ↔ Case B (sub-pills),
  và khi chuyển sang Tab 4.

### Nút và điều khiển:
- **Dựng cạnh [N]:** vẽ 1 cạnh thiết diện theo lựa chọn hướng song song.
- **Kết luận:** chỉ bật khi checklist đủ, hiện thiết diện hoàn chỉnh + tên gọi.
- **Đặt lại góc nhìn:** reset camera.

---

## TAB 4 — Luyện tập tổng hợp (MCQ)

**Mục tiêu:** Củng cố cả 3 dạng bài qua câu hỏi trắc nghiệm có minh hoạ 3D.
**Sai lầm cần giải quyết:** Cả 4 sai lầm đã liệt kê ở đầu tài liệu, mỗi câu
nhắm vào 1 sai lầm cụ thể.
**Loại simulation:** I (trắc nghiệm có minh hoạ 3D, hình xoay được, không cần
dựng tay).
**Thời gian hoàn thành dự kiến:** ~4–5 phút.

### Màn hình chính hiển thị:
- Hình chóp/hình hộp tĩnh (đổi theo từng câu), chỉ OrbitControls xoay/zoom.
- Panel câu hỏi + 4 lựa chọn dạng `choice-btn` bên sidebar.
- Athena xuất hiện góc sidebar, đưa gợi ý khi học sinh trả lời sai lần 2.

### Danh sách câu hỏi (nội dung mới, không copy nguyên đề 4.16–4.20):

**Câu 1 (nhắm sai lầm "viện dẫn sai tính chất"):**
> Cho đường thẳng d và mặt phẳng (α). Biết d có đúng 1 điểm chung với (α).
> Kết luận nào sau đây đúng?
> A. d ⊂ (α)  B. d // (α)  C. d cắt (α)  D. Không xác định được

- `dap_an_dung`: C (vị trí random khi build — không cố định ở C)
- `giai_thich_dung`: Đúng, có đúng 1 điểm chung nghĩa là d và (α) cắt nhau tại
  điểm đó — khác với "vô số điểm chung" (d ⊂ (α)) và "không điểm chung" (d // (α)).
- `goi_y_khi_sai`: Thử nhớ lại 3 vị trí tương đối của đường thẳng và mặt
  phẳng — mỗi vị trí ứng với bao nhiêu điểm chung?

**Câu 2 (nhắm sai lầm "dựng nhầm đường phụ"):**
> Cho hình chóp S.ABCD, đáy ABCD là hình bình hành. Gọi (P) là mặt phẳng qua
> 1 điểm trên SA và song song với BC. Giao tuyến của (P) với mặt đáy (ABCD)
> (nếu có) sẽ có tính chất gì?
> A. Vuông góc BC  B. Song song BC  C. Trùng với BC  D. Cắt BC

- `dap_an_dung`: B (vị trí random)
- `giai_thich_dung`: Đúng, vì (P) // BC và (ABCD) ⊃ BC, nên giao tuyến của
  (P) với (ABCD) phải song song BC.
- `goi_y_khi_sai`: Xoay hình 3D và thử hình dung: nếu (P) không được phép
  chạm vào BC (vì song song), giao tuyến của nó với mặt chứa BC có thể cắt
  BC được không?

**Câu 3 (nhắm sai lầm "thiết diện thiếu mặt"):**
> Khi xác định thiết diện của 1 hình chóp tứ giác bị cắt bởi 1 mặt phẳng,
> bước nào sau đây là BẮT BUỘC để đảm bảo thiết diện đúng?
> A. Chỉ cần tìm giao tuyến với 2 mặt bất kỳ rồi nối lại
> B. Chỉ cần tìm giao tuyến với mặt đáy
> C. Phải kiểm tra giao tuyến với tất cả các mặt mà mặt cắt đi qua
> D. Chỉ cần tìm 1 giao tuyến rồi suy ra các cạnh còn lại bằng đối xứng

- `dap_an_dung`: C (vị trí random)
- `giai_thich_dung`: Đúng, bỏ sót 1 mặt sẽ khiến thiết diện "hở", không khép
  kín thành đa giác đúng.
- `goi_y_khi_sai`: Nhớ lại ở Tab 3 — nút "Kết luận" chỉ sáng lên khi nào?

**Câu 4 (nhắm sai lầm "hình dung không gian sai"):**
> Trên hình vẽ phối cảnh của hình chóp S.ABCD, 2 đường thẳng SA và BD có vẻ
> như cắt nhau tại 1 điểm gần tâm hình. Nhận định nào đúng trong không gian
> thực?
> A. SA và BD luôn cắt nhau  B. SA và BD luôn song song
> C. SA và BD chéo nhau (không đồng phẳng)  D. Không thể xác định

- `dap_an_dung`: C (vị trí random)
- `giai_thich_dung`: Đúng, SA thuộc mặt bên còn BD thuộc mặt đáy — 2 đường
  này không cùng nằm trong 1 mặt phẳng nên chéo nhau; điểm "trông như cắt"
  trên hình vẽ chỉ là hiệu ứng phối cảnh 2D.
- `goi_y_khi_sai`: Hãy xoay hình 3D sang góc nhìn từ bên hông — 2 đường này
  có thực sự chạm nhau không?

**Câu 5 (tình huống thực tế, nhắm tổng hợp):**
> Một khung cửa sổ hình chữ nhật được lắp các thanh chắn song song với 1
> cạnh của khung. Khi khung cửa xoay quanh bản lề (cạnh còn lại), các thanh
> chắn có còn song song với mặt sàn không, nếu ban đầu chúng song song mặt
> sàn?
> A. Luôn còn song song  B. Không còn song song
> C. Tuỳ vào góc xoay  D. Chỉ song song khi khung đóng hoàn toàn

- `dap_an_dung`: A (vị trí random)
- `giai_thich_dung`: Đúng, các thanh chắn song song với trục bản lề (cố
  định), nên khi khung xoay quanh đúng trục đó, các thanh vẫn giữ nguyên
  hướng song song với mặt sàn.
- `goi_y_khi_sai`: Thử liên hệ với bài dây nhợ căng khi xây tường đã học ở
  Module 12.1 — điều gì giữ nguyên khi 1 vật xoay quanh 1 trục cố định?

### Quy tắc áp dụng cho toàn bộ Tab 4:
- Vị trí đáp án đúng random giữa 5 câu (không dồn về 1 vị trí cố định khi
  build thật — ví dụ trên chỉ minh hoạ nội dung, thứ tự hiển thị A/B/C/D
  phải xáo trộn thực sự).
- Trả lời đúng → hiện `giai_thich_dung` ngay, có highlight đường/mặt liên
  quan trên hình 3D.
- Trả lời sai lần 1 → chỉ hiệu ứng rung, chưa gợi ý.
- Trả lời sai lần 2 → hiện `goi_y_khi_sai` (giọng Athena), cho chọn lại.
- Trả lời sai lần 3 → hiện đáp án đúng + `giai_thich_dung` đầy đủ.

### Cấu hình 3D:
- **Khối nền:** đổi theo từng câu (câu 1-3 dùng chóp tứ giác đáy hình bình
  hành như Tab 2/3, câu 4 dùng chóp tứ giác chuẩn SGK để học sinh liên hệ
  lại hình quen thuộc, câu 5 dùng khung cửa hình chữ nhật đơn giản).
- **Đối tượng kéo được:** Không có — chỉ OrbitControls.
- **Cleanup:** `clearScene()` giữa mỗi câu hỏi.

### Nút và điều khiển:
- **4 nút lựa chọn (choice-btn):** chọn đáp án.
- **Đặt lại góc nhìn:** reset camera cho câu hiện tại.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

📝 **Cập nhật rà soát bản quyền (sau khi review toàn bộ Bài 12-13):** Tab 1
ban đầu dùng I, K là trung điểm SM, SN — bị đánh giá trùng kỹ thuật "đường
trung bình" với bài 4.17 SGK (M, N trung điểm AC, AD). Đã sửa sang tỉ lệ
SI=⅓SM, SK=⅓SN, buộc lý luận bằng định lí Talet đảo thay vì đường trung
bình, khác hẳn cách giải của 4.17.

⚠️ **Rủi ro 1:** Tab 2 và Tab 3 dùng click-to-select với điểm chia tỉ lệ
(SE = ⅓SA, SG = 2GB) — cần verify bằng script Node độc lập công thức tính
điểm trước khi build, đặc biệt sai số cho phép khi raycast (tránh học sinh
click gần đúng vẫn được tính đúng, làm mất tác dụng kiểm tra hiểu).

⚠️ **Rủi ro 2:** Tab 3 Case B (hình hộp cắt song song mặt chéo) có thể cho
thiết diện là lục giác tuỳ vị trí M — nếu build đúng vị trí AA' cho ra ngũ
giác/lục giác, độ phức tạp caption/checklist sẽ tăng hơn Case A (tam giác).
Cần cân nhắc đơn giản hoá vị trí M để thiết diện chỉ là tứ giác/ngũ giác dễ
kiểm soát, tránh Case B quá nặng so với thời lượng ~5-6 phút dự kiến.

📖 **Kiểm tra caption:** Đã rà toàn bộ bảng "Giải thích kiến thức" — không có
dòng nào chỉ nói "Đúng rồi!"/"Sai rồi" mà thiếu giải thích bản chất.

💡 **Gợi ý thêm:** Có thể thêm 1 nút "Xem lại Sổ tay" nổi cố định góc canvas
(không chỉ trong sidebar) để học sinh không phải chuyển tab khi đang dựng
hình mà quên công thức.

❓ **Cần làm rõ trước khi build:**
1. Case B Tab 3 — xác nhận lại vị trí điểm M để thiết diện không quá phức tạp?
2. Tab 4 câu 5 (khung cửa xoay) — có cần thêm animation xoay khung thật, hay
   chỉ mô tả bằng lời + hình tĩnh xoay camera?
3. Athena avatar — dùng hình ảnh có sẵn từ hệ thống hay cần thiết kế mới?

---

**Kịch bản đã sẵn sàng! Các bước tiếp theo:**
- ✅ Duyệt — chuyển sang Giai đoạn 2 (Thiết kế giao diện chi tiết)
- ✏️ Chỉnh — nêu rõ Tab/phần nào cần thay đổi
- 🔄 Cross-check với AI khác — xuất gói tóm tắt để phản biện chéo

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 11/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`, `01_scenario_builder_3d_addendum.md`,
> `04_design_toan_3d.md`, `05_threejs_engine.md`, `06_geometry_math.md`,
> đối chiếu với file mẫu `C5-Bai10_Toan3D_Simulation2_GiaoTuyen.html` và
> `C5-Bai10_Toan3D_KhaiNiemMoDau.html`
