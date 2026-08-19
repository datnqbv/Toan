# Module 3: Quy tắc nhân
### Bài 23 — Quy tắc đếm | Toán 10, Chương VIII | Chủ đề 47

---

**Mục tiêu:** Học sinh hiểu và vận dụng đúng quy tắc nhân, phân biệt được "và" (nối tiếp, độc lập → nhân) với "hoặc" (loại trừ nhau → cộng, đã học ở Module 1).

**Sai lầm cần giải quyết:**
1. Nhầm dùng quy tắc cộng (cộng số lựa chọn của từng công đoạn) thay vì nhân, vì chưa phân biệt "và" với "hoặc".
2. Quên điều kiện đặc biệt của bối cảnh — chữ số hàng chục của mã vụ án không được là 0 (9 lựa chọn, không phải 10).

**Loại simulation:** Khởi động bằng bài toán thu nhỏ (khám phá) → xác minh từng công đoạn → công cụ "máy tạo mật mã" (3 vòng xoay nối tiếp) để trực quan hoá tính độc lập giữa các công đoạn → tính tổng bằng quy tắc nhân.

**Thời gian hoàn thành dự kiến:** ~9 phút.

**Dạy từ đầu hay tổng kết:** Dạy từ đầu, theo mạch Problem → khám phá → khái quát hoá.

---

## 🎬 Ảnh hook mở đầu — prompt tạo ảnh (dùng ảnh thật)

```
A realistic flat-lay style photo of a detective-themed puzzle desk, shot from
directly above. On a warm wooden desk surface: a vintage-style magnifying glass,
a closed manila case folder with a red string tie, a torn piece of paper with a
handwritten code combining one capital letter and a two-digit number (like a
secret cipher), a small notebook, and a fountain pen. Soft warm lighting, cozy
mystery/escape-room aesthetic rather than a real crime scene — playful and
inviting, appropriate for a teen educational context, not dark or grim. Muted
warm color palette (browns, creams) with the code paper subtly highlighted.
Aspect ratio 16:9, high detail, shallow shadows, no text other than the single
handwritten code fragment on the paper.

Avoid: any weapons, blood, police badges, real crime-scene tape, or anything
suggesting a serious crime — this should feel like a fun puzzle/escape-room prop
set, not an actual investigation.
```

**Lời thoại Athena tại hook:**
> "Đội điều tra dùng mật mã riêng để liên lạc bí mật: mỗi mật mã gồm 1 kí hiệu điều tra viên (chữ cái) ghép với 1 mã vụ án gồm 2 chữ số. Bạn nghĩ có thể tạo ra bao nhiêu mật mã khác nhau?"

**Nút chuyển màn hình:** `[ Bắt đầu giải mã → ]`

---

## Số liệu cụ thể (đã kiểm chứng, khác SGK)

- Kí hiệu điều tra viên: 5 lựa chọn (A, B, C, D, E).
- Mã vụ án gồm 2 chữ số: chữ số hàng chục **không được là 0** → 9 lựa chọn (1–9); chữ số hàng đơn vị → 10 lựa chọn (0–9).
- Tổng số mật mã: 5 × 9 × 10 = **450**.
- Bộ số khởi động (bài toán thu nhỏ ở Bước 2): 2 kí hiệu (A, B) × 3 mã đơn giản (1, 2, 3) → 2 × 3 = **6**.

---

## 🖼️ Phác thảo canvas

Canvas nằm ở vùng chính, xuyên suốt module, **nội dung bên trong đổi theo từng bước** (giữ nguyên vùng bố trí, không phải mở canvas mới mỗi bước):

**Bước 2 — Bảng ghép nối thu nhỏ:** lưới 2×3 ô (2 hàng kí hiệu A/B, 3 cột mã 1/2/3), mỗi ô là 1 cặp có thể "ghép" bằng cách click kí hiệu rồi click mã số tương ứng — ghép xong ô đó sáng lên và hiện nhãn cặp (VD "A1"). Học sinh phải tự ghép đủ 6 cặp.

**Bước 4-5 — "Máy tạo mật mã" (3 vòng xoay nối tiếp, kiểu ổ khoá số):**
- 3 khối hình trụ đứng cạnh nhau, mỗi khối là 1 "vòng xoay" hiển thị giá trị hiện tại ở giữa, có nút mũi tên ▲/▼ phía trên/dưới để đổi giá trị (hoặc vuốt dọc trên mobile).
- Khối 1 (Kí hiệu): xoay qua 5 giá trị A–E.
- Khối 2 (Chữ số hàng chục): xoay qua 9 giá trị 1–9.
- Khối 3 (Chữ số hàng đơn vị): xoay qua 10 giá trị 0–9.
- Phía dưới 3 khối: ô hiển thị mã hoàn chỉnh ghép lại theo thời gian thực (VD "C-47").
- Bên cạnh mỗi khối: 1 bộ đếm nhỏ "Số lựa chọn ở vòng này: X" — cố định, không đổi dù khối trước xoay tới giá trị nào (đây là chi tiết học sinh cần tự quan sát để nhận ra tính độc lập giữa các công đoạn).

**Vùng sidebar bước (bên cạnh canvas):** danh sách các bước 1→7 dạng thẻ khoá dần, thẻ đang làm mở, thẻ chưa tới bị mờ/khoá.

---

## Học sinh tương tác bằng cách

0. Xem hook + đọc câu hỏi Athena.
1. Dự đoán tổng số mật mã có thể tạo ra (nhập số), CHƯA biết cách tính.
2. Khởi động bằng bài toán thu nhỏ: ghép đủ 6 cặp (kí hiệu × mã đơn giản) trên bảng ghép nối.
3. Quay lại bài toán thật, xác nhận số lựa chọn ở từng công đoạn (kí hiệu, chữ số hàng chục, chữ số hàng đơn vị).
4. Dùng "máy tạo mật mã" để tự quan sát: đổi khối 1, kiểm tra số lựa chọn ở khối 2/3 có đổi không.
5. Tính tổng bằng quy tắc nhân, nhập đáp án đúng.
6. Đọc Athena khái quát hoá quy tắc nhân, đối chiếu với quy tắc cộng (Module 1).
7. *(Mở rộng, không bắt buộc)* Áp dụng nhanh với 1 mật mã khác cấu trúc.

### Trước mỗi bước tương tác

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | "Bạn hãy đoán xem có thể tạo ra bao nhiêu mật mã khác nhau, rồi nhấn Kiểm tra." | (không cần — chỉ là dự đoán trực giác) |
| 2 | "Bạn hãy click 1 kí hiệu rồi click 1 mã số để ghép thành 1 cặp. Ghép đủ tất cả các cặp có thể." | Mỗi kí hiệu có thể ghép với TẤT CẢ các mã số — đây là quan hệ "và", không phải "hoặc". |
| 3 | "Bạn hãy nhập số lựa chọn ở từng công đoạn: kí hiệu, chữ số hàng chục, chữ số hàng đơn vị." | Chú ý điều kiện của mã vụ án: chữ số hàng chục không được là 0. |
| 4 | "Bạn hãy thử xoay khối Kí hiệu sang vài giá trị khác nhau, rồi quan sát số lựa chọn ở 2 khối còn lại có thay đổi không." | Quy tắc nhân chỉ áp dụng khi các công đoạn độc lập với nhau. |
| 5 | "Nhân 3 số lựa chọn ở từng công đoạn lại với nhau, nhập kết quả." | Công đoạn 1 có m₁ cách, công đoạn 2 có m₂ cách, làm liên tiếp thì có m₁ × m₂ cách. |

---

## Kịch bản dẫn dắt học sinh gặp sai lầm

**Bước 1 — dự đoán:**
> Athena: "Bạn dự đoán là [số học sinh nhập]. Mình chưa nói đúng hay sai vội — thử với 1 bài toán nhỏ hơn trước nhé."

**Bước 2 — khởi động bằng bài toán thu nhỏ (phát hiện "và" = nhân):**
Sau khi học sinh ghép đủ 6 cặp:
> Athena: "Bạn vừa ghép được 6 cặp từ 2 kí hiệu và 3 mã số. Nếu cộng 2 + 3 = 5, có khớp với 6 cặp bạn vừa ghép không? Vậy khi 2 công đoạn nối tiếp nhau và độc lập với nhau, ta không cộng — ta nhân: 2 × 3 = 6."

**Bước 3 — xác nhận từng công đoạn (bẫy điều kiện đặc biệt):**
- Ô 1 "Kí hiệu điều tra viên": học sinh nhập → đúng là 5, xác nhận ngay.
- Ô 2 "Chữ số hàng chục": nhiều học sinh sẽ nhập 10 (quên loại trừ số 0) — hệ thống áp dụng 3-strike riêng cho ô này:
  - Lần sai 1: rung nhẹ.
  - Lần sai 2: gợi ý — *"Bạn thử đọc lại đề: mã vụ án có yêu cầu gì đặc biệt về chữ số hàng chục không?"*
  - Lần sai 3: đáp án đúng — *"Chữ số hàng chục không được là 0 (vì 0 ở đầu không hợp lệ), nên chỉ có 9 lựa chọn: 1 đến 9."*
- Ô 3 "Chữ số hàng đơn vị": đúng là 10, không có điều kiện đặc biệt, xác nhận ngay.

**Bước 4 — máy tạo mật mã (khám phá tính độc lập):**
Học sinh xoay khối 1 qua vài giá trị (A→B→C…), quan sát số lựa chọn hiển thị cạnh khối 2 và khối 3 luôn giữ nguyên (9 và 10) dù khối 1 đổi giá trị nào.
> Athena: "Dù bạn chọn kí hiệu nào, số lựa chọn ở 2 vòng còn lại vẫn không đổi — đây chính là điều kiện để áp dụng quy tắc nhân: các công đoạn phải độc lập với nhau."

**Bước 5 — tính tổng, 3-strike:**
- Lần sai 1: rung nhẹ ô nhập.
- Lần sai 2: gợi ý — *"Bạn thử nhân lần lượt 3 số lựa chọn ở 3 công đoạn: kí hiệu, hàng chục, hàng đơn vị."*
- Lần sai 3: đáp án đúng — *"5 × 9 × 10 = 450. Vì đây là 3 công đoạn liên tiếp và độc lập nhau, ta nhân các số lựa chọn lại."*
- Trả lời đúng: *"Chính xác! Khi các công đoạn nối tiếp nhau và không phụ thuộc lẫn nhau, số cách thực hiện toàn bộ công việc bằng tích số cách của từng công đoạn."*

---

## Bước 6 — Athena khái quát hoá và đối chiếu Module 1

> Athena: "Đây là quy tắc nhân: nếu công việc gồm nhiều công đoạn liên tiếp, mỗi công đoạn độc lập với công đoạn trước, số cách thực hiện toàn bộ công việc bằng tích số cách của từng công đoạn. Khác với Module 1, ở đó bạn dùng từ 'hoặc' để chọn 1 trong 2 phương án tách biệt — quy tắc cộng. Ở đây bạn dùng từ 'và' để làm nối tiếp nhiều công đoạn — quy tắc nhân."

Sổ tay kiến thức nền tảng: có, gọi lại đúng câu quy tắc cộng đã học ở Module 1 để đối chiếu song song:
```
- Quy tắc cộng (đã học): 2 phương án KHÔNG trùng nhau → cộng số cách.
- Quy tắc nhân (mới): các công đoạn liên tiếp, ĐỘC LẬP nhau → nhân số cách.
```

## Bước 7 — Mở rộng (không bắt buộc)

Tình huống mới: mật mã dạng 2 chữ cái (không giới hạn) + 1 chữ số bất kỳ (0–9) → đáp án 26×26×10 = 6 760. Không chặn hoàn thành module nếu bỏ qua.

---

## Bố cục giao diện — Desktop & Mobile (kiểm tra kỹ)

> ⚠️ Module này có **sidebar nhiều thẻ bước khoá dần (7 bước) đi kèm 1 vùng canvas cố định** (canvas đổi nội dung theo bước nhưng vùng hiển thị không đổi vị trí) — theo đúng điều kiện ở `02_design_toan_final.md` PHẦN 3.6b, mobile **BẮT BUỘC dùng pattern lướt ngang**, KHÔNG dùng cuộn dọc thường.

**Desktop (≥1024px):**
- Vùng canvas chính đặt bên trái (~65% chiều rộng): lần lượt hiển thị bảng ghép nối (Bước 2) rồi máy tạo mật mã 3 vòng xoay (Bước 4-5).
- Sidebar bên phải (~35%), cố định theo chiều dọc trang: danh sách 7 thẻ bước khoá dần, thẻ đang làm mở rộng hiển thị đầy đủ hướng dẫn + ô nhập, các thẻ chưa tới hiện mờ có khoá.
- Khung thoại Athena nằm trong từng thẻ bước, không phải 1 khối cố định riêng.

**Mobile (≤767px) — dùng pattern "lướt ngang" PHẦN 3.6b:**
- Canvas LUÔN cố định ở trên cùng màn hình (không bị cuộn mất khi chuyển bước).
- Ngay dưới canvas: dòng gợi ý nhỏ *"← vuốt ngang để xem các bước →"*.
- Bên dưới dòng gợi ý: các thẻ bước xếp NGANG, cuộn/vuốt để chuyển bước (mỗi thẻ chiếm ~86% chiều rộng màn hình, snap vào giữa khi vuốt xong).
- Vùng chạm (nút ▲/▼ của vòng xoay, nút Kiểm tra, ô input) đều ≥44×44px.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Ghép cặp kí hiệu — mã số (Bước 2) | Click kí hiệu, rồi click mã số | Chạm kí hiệu, rồi chạm mã số — vùng chạm ≥44px |
| Đổi giá trị vòng xoay (Bước 4-5) | Click nút ▲/▼ cạnh mỗi khối | Vuốt dọc trên khối (touch-action: pan-y) hoặc chạm nút ▲/▼ ≥44px |
| Chuyển giữa các thẻ bước | Cuộn dọc trang bình thường (sidebar cố định bên phải) | Vuốt ngang giữa các thẻ (scroll-snap-x), có dòng gợi ý chữ |
| Nhập đáp án + Kiểm tra | Click vào ô input, gõ bàn phím, click nút Kiểm tra | Chạm ô input (mở bàn phím số `inputmode="numeric"`), chạm nút Kiểm tra ≥44px |
| Xem gợi ý khi sai (lần 2) | Text hiện ngay dưới ô input, không cần thao tác thêm | Giống desktop — không dùng hover nên không có khác biệt |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`

```javascript
structure: [
  { id: 'm3_du_doan',        type: 'answered', required: true },
  { id: 'm3_ghep_cap',       type: 'explored', required: true },
  { id: 'm3_so_ki_hieu',     type: 'answered', required: true },
  { id: 'm3_so_hang_chuc',   type: 'answered', required: true },
  { id: 'm3_so_hang_donvi',  type: 'answered', required: true },
  { id: 'm3_may_mat_ma',     type: 'explored', required: true },
  { id: 'm3_dap_an_dung',    type: 'answered', required: true },
  { id: 'm3_mo_rong',        type: 'answered', required: false }
]
```

`progress total = 7` (không tính `m3_mo_rong`).

### Sự kiện LMS theo từng bước

| Bước | Sự kiện | Ghi chú |
|---|---|---|
| 1 | `LMS().event('answered', {id: 'm3_du_doan', value})` | Dự đoán ban đầu |
| 2 | `LMS().event('explored', {id: 'm3_ghep_cap', trial})` | Ghép cặp khởi động, không chấm điểm |
| 3 | `LMS().event('answered', {id: 'm3_so_ki_hieu', tries})`, tương tự cho `m3_so_hang_chuc`, `m3_so_hang_donvi` | 3 sự kiện riêng — `m3_so_hang_chuc` là nơi bẫy điều kiện đặc biệt, cần đếm `tries` riêng để theo dõi tỉ lệ mắc lỗi |
| 4 | `LMS().event('explored', {id: 'm3_may_mat_ma', trial})` | Xoay khối quan sát, không chấm điểm |
| 5 | `LMS().event('answered', {id: 'm3_dap_an_dung', tries})` | Đáp án cuối cùng |
| 7 | `LMS().event('answered', {id: 'm3_mo_rong', required:false})` | Không chặn `LMS().complete()` |

`LMS().complete()` gọi ngay sau khi Bước 5 đạt đúng.

### `athenaGuidance` (nguyên văn, khớp đúng 7 mục bắt buộc)

```
1. m3_du_doan: nếu học sinh hỏi gợi ý, Athena chỉ hỏi ngược: "Bạn thử
   nghĩ xem công việc này có mấy công đoạn?" — không nói trước đáp án 450.
2. m3_ghep_cap: Athena chỉ nhắc: "Mỗi kí hiệu có thể ghép với tất cả các
   mã số." — không nói trước đây là quy tắc nhân.
3. m3_so_ki_hieu: xác nhận đúng/sai đơn giản, không cần gợi ý phức tạp
   (câu hỏi này không có bẫy).
4. m3_so_hang_chuc: gợi ý lần sai thứ 2 CHỈ dùng đúng câu: "Bạn thử đọc
   lại đề: mã vụ án có yêu cầu gì đặc biệt về chữ số hàng chục không?"
   — không được nói thẳng đáp án 9 ở gợi ý này.
5. m3_so_hang_donvi: xác nhận đúng/sai đơn giản, không có bẫy.
6. m3_may_mat_ma: Athena chỉ xác nhận học sinh đã quan sát xong, không
   giải thích thêm cho tới khi học sinh tự nói ra nhận xét hoặc sang Bước 5.
7. m3_dap_an_dung: gợi ý lần sai thứ 2 CHỈ dùng đúng câu: "Bạn thử nhân
   lần lượt 3 số lựa chọn ở 3 công đoạn: kí hiệu, hàng chục, hàng đơn vị."
   — không được nói thẳng đáp án 450 ở gợi ý này.
```

---

## Tổng kết kiến thức

> **Quy tắc nhân:** Nếu một công việc phải hoàn thành qua nhiều công đoạn liên tiếp nhau, công đoạn một có m₁ cách thực hiện, và với mỗi cách thực hiện công đoạn một, công đoạn hai (độc lập) có m₂ cách thực hiện, thì công việc đó có m₁ × m₂ cách thực hiện.
>
> ⚠️ Phân biệt với quy tắc cộng: "hoặc" giữa 2 phương án tách biệt → cộng (Module 1); "và" giữa các công đoạn nối tiếp, độc lập → nhân (Module 3). Luôn kiểm tra điều kiện đặc biệt của từng công đoạn trước khi đếm số lựa chọn (ví dụ: chữ số hàng đầu không được là 0).
