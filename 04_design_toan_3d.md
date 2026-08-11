# 🎨 DESIGN SYSTEM — Môn Toán Hình Học Không Gian (3D)

> **Mục đích:** Từ kịch bản đã duyệt → thiết kế → build HTML hình học không gian hoàn chỉnh.
> File này phục vụ **2 loại sản phẩm khác nhau** — xác định đúng loại NGAY từ đầu:
>
> - **Nhánh A — Bài học SGK cụ thể:** 1 bài, có tiến trình sư phạm theo bước
>   (step-tabs, kết luận), dùng 1 lần cho 1 nội dung. Xem PHẦN 0-A.
> - **Nhánh B — Kho công cụ / Thư viện hình:** không có "bài học" hay tiến
>   trình — là 1 canvas tự do học sinh gọi hình ra dùng nhiều lần cho nhiều
>   bài khác nhau (ví dụ `solid_library.html` — Kho Khối Hình Không Gian).
>   Xem PHẦN 0-B.
>
> **Dùng kèm với:** `01_scenario_builder.md` (Nhánh A) + `05_threejs_engine.md` (cả 2 nhánh) + `06_geometry_math.md` (cả 2 nhánh)
> **Đặc thù môn:** Three.js 3D, OrbitControls, kéo điểm/đường, màu hình học chuẩn

> ⚠️ **Khác với `02_design_toan_2.md` (Canvas 2D):**
> File này dùng Three.js (không phải Canvas 2D) — layout, màu đối tượng, và một số component khác nhau.
> Đọc PHẦN 3 trước khi build để không lấy nhầm pattern 2D vào file 3D.

---

## 🤖 HƯỚNG DẪN CHO AI — ĐỌC TRƯỚC KHI LÀM BẤT CỨ ĐIỀU GÌ

Khi người dùng nói bất kỳ điều nào sau:
- "Thiết kế" / "Design" / "Làm giao diện" / "Bắt đầu thiết kế"
- "Sang giai đoạn 2" / "Chuyển sang thiết kế"
- Bài liên quan đến **hình học không gian / 3D**: đường thẳng, mặt phẳng, góc nhị diện, khoảng cách, hình chóp, hình trụ, hình cầu, song song, chéo nhau, đồng phẳng

**→ Lập tức hỏi câu phân nhánh ở PHẦN 0 (BƯỚC -1) trước bất kỳ việc gì khác.**
**Không tự chọn nhánh A hay B — luôn hỏi, vì 2 nhánh có conversation flow và
component library khác nhau hoàn toàn.**

Trong suốt quá trình:
- Tuân thủ đúng thứ tự — **không bỏ bước, không gộp bước**
- Mỗi bước kết thúc bằng câu hỏi rõ ràng — **chờ giáo viên trả lời rồi mới đi tiếp**

---

## PHẦN 0 — CONVERSATION FLOW

---

### BƯỚC -1 — PHÂN NHÁNH: BÀI HỌC HAY KHO CÔNG CỤ?

AI nói đúng đoạn này TRƯỚC MỌI THỨ KHÁC:

---
**Chào mừng đến Giai đoạn 2 — Thiết kế Hình học Không gian! Trước tiên, mình cần biết bạn muốn xây loại sản phẩm nào:**

**🅰 Bài học SGK cụ thể** — 1 bài, có tiến trình sư phạm theo bước (ví dụ "Bài 10: Đường thẳng và mặt phẳng"), học sinh đi qua từng bước rồi đến kết luận.

**🅱 Kho công cụ / Thư viện hình** — không phải 1 bài cụ thể, mà là 1 canvas tự do: học sinh gọi hình 3D ra (chọn từ danh mục), tự dựng lại hình đề bài, thêm điểm/đoạn/đo đường cao... Dùng lại được cho nhiều bài khác nhau.

**→ Chọn 🅰 hoặc 🅱.**

---

> ⏳ **Chờ trả lời rồi mới đi tiếp.**
> Nếu 🅰 → tiếp tục BƯỚC 0 (Nhánh A) bên dưới.
> Nếu 🅱 → nhảy sang PHẦN 0-B, bỏ qua toàn bộ BƯỚC 0-6 của Nhánh A.

---

## PHẦN 0-A — NHÁNH A: BÀI HỌC SGK CỤ THỂ

---

### BƯỚC 0 — THU THẬP KỊCH BẢN

AI nói đúng đoạn này:

---
**Chào mừng đến Giai đoạn 2 — Thiết kế giao diện Hình học Không gian! Để bắt đầu, mình cần:**

**📋 Kịch bản simulation đã duyệt**
Paste kịch bản vào đây hoặc upload file lên nhé.
*(Nếu vừa làm xong Giai đoạn 1 trong cùng conversation, gõ "Dùng kịch bản vừa xong" là được)*

---

> ⏳ **Chờ nhận kịch bản rồi mới đi tiếp.**

---

### BƯỚC 1 — CHỌN CONCEPT THIẾT KẾ

AI đưa ra đúng format này:

---
**Bước đầu tiên: chọn phong cách thiết kế. Bạn có 2 cách:**

**🅐 Chọn preset có sẵn:**

| # | Tên | Nền canvas | Nền trang | Cảm giác | Phù hợp |
|---|---|---|---|---|---|
| 1 | **Navy & Teal** | Đêm `#0a1628` | Sáng `#f0f4f8` | Học thuật, chính xác | Mặt phẳng, giao tuyến, góc — bài lý thuyết |
| 2 | **Deep Space** | Rất tối `#060d1a` | Tối `#0d1117` | Công nghệ, immersive | Bài khám phá tự do, hình chóp, hình tròn xoay |
| 3 | **Sky & White** | Đêm `#0a1628` | Trắng sáng `#ffffff` | Sạch, nhẹ nhàng | Bài cho học sinh nhỏ tuổi hơn, bài ôn tập |

**🅑 Upload hình concept:**
Có hình ảnh, app hay slide nào bạn thích phong cách không? Upload lên, mình phân tích màu và đề xuất theo đó.

**→ Chọn 1 / 2 / 3, hoặc upload hình, hoặc 💬 Thảo luận thêm.**

---

> ⏳ **Chờ giáo viên chọn rồi mới đi tiếp.**
> Nếu upload hình: phân tích màu → đề xuất bộ màu cụ thể → hỏi xác nhận.
> Nếu 💬 Thảo luận: thảo luận xong hỏi: *"Bạn muốn tiếp tục với concept [X] không?"*

---

### BƯỚC 2 — CHỐT TYPOGRAPHY & CỠ CHỮ

---
**Tiếp theo: typography. Đề xuất mặc định — bạn chỉnh nếu cần:**

**Font chữ:**
- Mặc định: **Plus Jakarta Sans** (Google Fonts, tiếng Việt tốt, đồng nhất với hệ thống Toán 2D / Lý / Hoá)
- ⚠️ KHÔNG dùng Be Vietnam Pro dù file mẫu `song_song_khong_gian` đang dùng — cần đồng nhất xuyên môn

**Thang cỡ chữ:**

| Vị trí | Cỡ | Weight | Ghi chú |
|---|---|---|---|
| Tiêu đề bài (header h1) | 17px | 700 | Màu trắng, trên nền navy gradient |
| Header badge | 11px | 600 | Uppercase, pill style, rgba trắng mờ |
| Tab bước | 11px | 600 | Uppercase, letter-spacing .04em |
| Tiêu đề bước (step-title) | 13px | 700 | Màu navy `#0d2b4e` |
| Body text sidebar | 12.5px | 400 | Màu `#334155`, line-height 1.65 |
| Info box text | 12px | 400 | |
| Legend label | 12px | 600 | |
| Nút toggle | 12.5px | 400 | |
| Nút reset | 13px | 600 | |
| Label 3D trên canvas | 16px | 700 | HTML overlay qua project() — xem 05_threejs_engine PHẦN 3 |
| Label số đo (khoảng cách, góc) | 13px | 700 | Màu accent vàng #FAC775 |
| Canvas hint (góc dưới canvas) | 11.5px | 400 | Màu rgba(255,255,255,0.75), pill |

---

> ⏳ **Chờ xác nhận rồi mới đi tiếp.**

---

### BƯỚC 3 — CHỐT TƯƠNG TÁC & HÀNH VI 3D

AI chỉ hiện các tương tác **phù hợp với kịch bản nhận ở Bước 0**:

---
**Chốt tương tác. Tick những cái cần, hoặc 💬 Thảo luận để mô tả kỹ hơn:**

**🖱️ Camera & navigation:**
- [ ] N1 — OrbitControls: kéo xoay camera (bắt buộc với mọi bài 3D)
- [ ] N2 — Zoom cuộn chuột
- [ ] N3 — Nút "Đặt lại góc nhìn" (reset camera về vị trí mặc định)
- [ ] N4 — Canvas hint "Kéo để xoay · Cuộn để zoom" (bắt buộc lần đầu)

**🎯 Kéo điểm/đường:**
- [ ] D1 — Kéo điểm tự do trong không gian (DraggablePoint)
- [ ] D2 — Kéo điểm ràng buộc trên cạnh/mặt (ConstrainedPoint)
- [ ] D3 — Kéo đầu mút đường thẳng để xoay/dài đường

**👆 Click chọn:**
- [ ] S1 — Click chọn đường thẳng để đo góc / khoảng cách
- [ ] S2 — Click chọn mặt phẳng để highlight

**📐 Nhập toạ độ số:**
- [ ] I1 — Panel nhập A(x,y,z), B(x,y,z)... (đồng bộ 2 chiều với kéo chuột)
- [ ] I2 — Nhấn Enter để áp dụng toạ độ

**👁️ Hiện/ẩn:**
- [ ] V1 — Toggle từng đường thẳng (bật/tắt)
- [ ] V2 — Toggle mặt phẳng
- [ ] V3 — Toggle vector chỉ phương
- [ ] V4 — Toggle label tên điểm/đường
- [ ] V5 — Toggle lưới tham chiếu (grid)
- [ ] V6 — Toggle dấu góc vuông

**▶️ Dựng hình theo bước (có animation):**
- [ ] A1 — Animation vẽ dần đường thẳng song song (ease-out, 900ms)
- [ ] A2 — Animation hiện mặt phẳng phụ trợ
- [ ] A3 — Nút "Dựng..." kích hoạt thủ công, không tự chạy

**📊 Hiển thị kết quả:**
- [ ] R1 — Label góc nổi giữa 2 đường (HTML overlay)
- [ ] R2 — Label khoảng cách MH nổi giữa đoạn
- [ ] R3 — Cung góc nhỏ tại điểm giao
- [ ] R4 — Dấu góc vuông tại chân đường vuông góc

**→ Tick các mục, hoặc 💬 Thảo luận.**

---

> ⏳ **Chờ giáo viên chọn rồi mới đi tiếp.**

---

### BƯỚC 4 — CHỐT LAYOUT & CẤU TRÚC HTML

Layout chuẩn cho hình học không gian là **Header + Canvas trái + Sidebar phải** (khác Toán 2D thường dùng layout cuộn dọc):

---
**Dựa trên kịch bản và tương tác đã chốt, đây là cấu trúc đề xuất:**

```
┌─ Header (navy gradient) ────────────────────────────────────┐
│  [Badge 🧊 Hình học không gian]  Tiêu đề bài               │
└─────────────────────────────────────────────────────────────┘

┌─ Canvas (flex:1, min 500px) ──┐ ┌─ Sidebar (310px) ────────┐
│  Three.js WebGL               │ │  Step tabs               │
│  (nền tối #0a1628)            │ │  [Bước 1][Bước 2][Bước N]│
│                               │ │                          │
│  [label-layer HTML overlay]   │ │  Step body:              │
│                               │ │   step-title             │
│  [Canvas hint góc dưới]       │ │   step-desc              │
└───────────────────────────────┘ │   info-box (ib-*)        │
                                  │   legend                  │
                                  │                          │
                                  │  Controls:               │
                                  │   toggle-row × N         │
                                  │   [btn-reset]            │
                                  └──────────────────────────┘
```

**Responsive (max-width 680px):** flex-direction column, sidebar xuống dưới canvas, canvas min-height 320px.

**→ Bạn muốn:**
- ✅ **Duyệt** — tiếp tục sang Bước 5
- ✏️ **Chỉnh** — nói phần nào cần thay đổi
- 💬 **Thảo luận**

---

> ⏳ **Chờ phản hồi rồi mới đi tiếp.**

---

### BƯỚC 5 — XÁC NHẬN TOÀN BỘ TRƯỚC KHI BUILD

---
**Tóm tắt toàn bộ trước khi build:**

```
📋 Kịch bản:        [tên bài, chủ đề hình học]
🎨 Concept:         [preset 1/2/3 hoặc custom]
🎨 Màu canvas:      [hex nền canvas tối]
🎨 Màu UI:          navy #0d2b4e + teal #0e7a6e (hoặc custom)
🎨 Màu đối tượng:   [xem PHẦN 1.2 — bộ màu hình học]
🔤 Font:            Plus Jakarta Sans
📐 Layout:          Header + Canvas + Sidebar 310px
🖱️ Tương tác:      [N1, D1, S1, I1, V1, A1, R1...]
📊 Số bước tab:     [N bước + Kết luận]
✨ Ghi chú:         [nếu có — ví dụ: bài có nhập toạ độ, bài có animation]
```

**→ Xác nhận build HTML không?**
- ✅ **Có, build ngay**
- ✏️ **Khoan, mình muốn chỉnh [phần X]**

---

> ⏳ **Chỉ build khi có xác nhận "Có". Tuyệt đối không tự build.**
> **Trước khi build: đọc PHẦN 2 (Design Tokens 3D) và PHẦN 3 (Kỹ thuật Three.js).**

---

### BƯỚC 6 — BUILD HTML

Chỉ chạy sau khi có xác nhận ở Bước 5.

**Checklist trước khi gửi file:**
- [ ] Kiểm tra cú pháp JS bằng `new Function(scriptContent)` qua Node
- [ ] Liệt kê `const`/`let` top-level theo số dòng, xác nhận thứ tự khai báo đúng
- [ ] Mọi đối tượng Three.js bị remove phải gọi `.geometry.dispose()` + `.material.dispose()`
- [ ] `LineDashedMaterial` phải gọi `.computeLineDistances()` sau khi tạo
- [ ] `orbitControls.enabled = false` khi drag điểm, `= true` ở cả pointerup và pointerleave

Sau khi build xong:

---
**File đã sẵn sàng! Bạn muốn:**
- ✅ **Duyệt** — hoàn thành Giai đoạn 2
- 🐛 **Báo lỗi** — mô tả lỗi hoặc upload ảnh chụp màn hình
- ✏️ **Chỉnh giao diện** — nói rõ phần nào muốn thay đổi

---

---

## PHẦN 0-B — NHÁNH B: KHO CÔNG CỤ / THƯ VIỆN HÌNH

> Nhánh này **không có tiến trình sư phạm theo bước** (không step-tabs,
> không "kết luận") — sản phẩm là 1 canvas tự do, học sinh chọn hình từ
> danh mục rồi tự tương tác. Vì vậy flow ngắn hơn Nhánh A rất nhiều: không
> cần duyệt từng bước UI, vì layout đã cố định theo pattern đã verify
> (`solid_library.html`) — chỉ cần chốt PHẠM VI (những khối nào, mode nào).

---

### BƯỚC B0 — CHỐT PHẠM VI KHO

---
**Kho công cụ dùng layout cố định: Catalog sidebar trái + Canvas giữa + Config sidebar phải.**
**Mình cần biết phạm vi trước khi build:**

**1. Nhóm khối cần có** (có thể chọn nhiều, hoặc yêu cầu khối mới):
- [ ] Tứ diện (đều / vuông / thường)
- [ ] Hình chóp (tam giác đều / SA⊥đáy / tứ giác đều / SA⊥đáy)
- [ ] Lăng trụ & Hình hộp (đứng / xiên / chữ nhật / lập phương)
- [ ] Đa diện đặc biệt (chóp cụt / bát diện đều)
- [ ] Khối tròn xoay (cầu / trụ / nón)
- [ ] Khối mới — mô tả cụ thể tên + tham số (VD: "chỏm cầu, cắt bởi 1 mặt phẳng")

**2. Mode tương tác cần có** (mặc định BẬT hết nếu không nói gì khác):
- [ ] 🔒 Xem (luôn có, không tắt được)
- [ ] ✥ Kéo đỉnh (EXPLORE) — chỉ áp dụng đa diện
- [ ] ✦ Thêm điểm (trên cạnh/mặt/mặt cong)
- [ ] ⟶ Nối 2 điểm
- [ ] 🗑 Xoá điểm/đoạn
- [ ] ⊥ Hạ đường cao — chỉ áp dụng đa diện có `baseVertices`

**→ Trả lời phạm vi, hoặc 💬 Thảo luận (VD: "muốn thêm chỏm cầu, mình chưa biết dựng").**

---

> ⏳ **Chờ trả lời rồi mới đi tiếp.**

---

### BƯỚC B1 — XÁC NHẬN & BUILD

---
**Tóm tắt trước khi build:**

```
📦 Loại sản phẩm:   Kho công cụ / Thư viện hình
🗂️ Nhóm khối:       [danh sách đã chọn ở B0]
🎛️ Mode tương tác:  [danh sách đã chọn ở B0]
🎨 Theme UI:        Navy & Teal (mặc định — xem PHẦN 1-B)
📐 Layout:          Catalog (240px) + Canvas (flex:1) + Config sidebar (310px)
```

**→ Xác nhận build không?**
- ✅ **Có, build ngay**
- ✏️ **Khoan, muốn chỉnh [phần X]**

---

> ⏳ **Chỉ build khi có xác nhận "Có".**
> **Trước khi build:** đọc PHẦN 1-B + PHẦN 2-B (component riêng Nhánh B) +
> `05_threejs_engine.md` PHẦN 7-9 (SolidRenderer/RoundSolidRenderer) +
> `06_geometry_math.md` (mọi hàm toán cần).

**Checklist trước khi gửi file (giống Nhánh A + thêm 2 mục riêng Nhánh B):**
- [ ] Kiểm tra cú pháp bằng **`node --check`** (KHÔNG dùng `new Function()` —
      không bắt được lỗi trong class methods, đã từng báo "OK" sai)
- [ ] Nếu thêm khối mới vào `SOLID_LIBRARY`/`ROUND_LIBRARY`: verify
      `edges`/`faces` tam giác hoá đúng, `explore` khai báo đủ mọi đỉnh
- [ ] Nếu chuyển đổi giữa đa diện ↔ tròn xoay: xác nhận cờ `isRoundActive`
      được set TRƯỚC khi gọi `setMode()` (xem `05_threejs_engine.md` PHẦN 9.4)
- [ ] Mọi đối tượng Three.js bị remove phải `.geometry.dispose()` + `.material.dispose()`

Sau khi build xong, dùng đúng câu hỏi post-build như Nhánh A (Duyệt / Báo lỗi / Chỉnh).

---

## PHẦN 1 — DESIGN TOKENS 3D

> **Áp dụng cho CẢ 2 nhánh.** Bảng màu đối tượng hình học (1.3) giống nhau
> tuyệt đối giữa bài học và kho công cụ — `solid_library.html` dùng đúng
> `COLOR_PLANE_1`, `COLOR_EDGE_SOLID`, `COLOR_RESULT`... như file bài học.
> Token riêng cho UI kho công cụ (catalog, mode toolbar) xem 1.6.

### 1.1 CSS Variables hệ thống (dùng chung mọi preset)

```css
/* Kế thừa nguyên từ 02_design_toan_2.md — không đổi để đồng nhất xuyên môn */
:root {
  --green:        #1B8C5A;
  --green-light:  #E6F4EE;
  --red:          #C62828;
  --red-light:    #FFEBEE;
  --amber:        #EF9F27;
  --amber-light:  #FEF3E0;
  --blue:         #1565C0;
  --blue-light:   #EBF3FF;
  --surface:      #ffffff;
  --border:       #d1dce8;
  --text:         #1a2e44;
  --text-2:       #334155;
  --sub:          #64748b;
  --radius:       12px;
}
```

### 1.2 Preset màu UI (nền trang, header, sidebar)

**Preset 1 — Navy & Teal (chuẩn, dùng mặc định)**
```css
:root {
  --navy:   #0d2b4e;   /* Header gradient từ, step-num, btn-reset nền */
  --teal:   #0e7a6e;   /* Active tab underline, toggle on, step-num bg, toggle on */
  --bg:     #f0f4f8;   /* Nền trang */
}
/* Header: linear-gradient(135deg, #0d2b4e 0%, #1a4a7a 100%) */
/* Canvas bg: #0a1628 */
```

**Preset 2 — Deep Space**
```css
:root {
  --navy:   #090e1a;
  --teal:   #00b4d8;
  --bg:     #0d1117;
}
/* Header: linear-gradient(135deg, #090e1a 0%, #0d1b33 100%) */
/* Canvas bg: #060d1a */
/* Sidebar bg: #0d1117, border: #21262d, text: #e6edf3 */
```

**Preset 3 — Sky & White**
```css
:root {
  --navy:   #1565C0;
  --teal:   #0e7a6e;
  --bg:     #ffffff;
}
/* Header: linear-gradient(135deg, #1565C0 0%, #1976D2 100%) */
/* Canvas bg: #0a1628 */
```

### 1.3 Bảng màu đối tượng hình học 3D

> Đây là phần MỚI, không có trong `02_design_toan_2.md`.
> Màu đối tượng trong canvas 3D (Three.js hex `0xRRGGBB`) — hoàn toàn
> tách biệt với màu UI sidebar. Lấy từ file `song_song_khong_gian__1_.html`
> (đã verify hiển thị tốt trên nền canvas tối `#0a1628`).

**Bộ cơ bản — 2 mặt phẳng, 2 đường (đủ cho hầu hết bài):**
```javascript
// MẶT PHẲNG
const COLOR_PLANE_1  = 0x3b82f6;  // Xanh dương  — mặt phẳng (α) / mặt phẳng thứ nhất
const COLOR_PLANE_2  = 0xa78bfa;  // Tím nhạt    — mặt phẳng (β) / mặt phẳng thứ hai

// ĐƯỜNG THẲNG — mỗi đường có 2 sắc độ: chính (đường) + sáng (vector chỉ phương)
const COLOR_LINE_A        = 0xf59e0b;  // Vàng cam  — đường thẳng a / đường thứ nhất
const COLOR_LINE_A_VECTOR = 0xfbbf24;  // Vàng sáng — vector chỉ phương của a
const COLOR_LINE_B        = 0xef4444;  // Đỏ        — đường thẳng b / đường thứ hai
const COLOR_LINE_B_VECTOR = 0xf87171;  // Đỏ nhạt   — vector chỉ phương của b

// ĐIỂM
const COLOR_POINT_FREE    = 0x378ADD;  // Xanh dương đậm  — điểm tự do (A, B, C)
const COLOR_POINT_ON_LINE = 0xFAC775;  // Vàng cam sáng   — điểm ràng buộc (M, H, O)

// KẾT QUẢ / PHỤ TRỢ
const COLOR_RESULT        = 0xFAC775;  // Vàng cam sáng — MH, cung góc, dấu góc vuông, d2'
const COLOR_CONNECTOR     = 0x94a3b8;  // Xám nhạt      — đường nối phụ, opacity 0.4
```

**Bộ mở rộng — cho bài có nhiều đối tượng (hình chóp, lăng trụ, ≥3 mặt/đường):**
```javascript
// MẶT PHẲNG MỞ RỘNG — theo thứ tự ưu tiên hiển thị
const COLOR_PLANE_3  = 0x34d399;  // Xanh ngọc nhạt — mặt phẳng thứ ba (mặt bên 1)
const COLOR_PLANE_4  = 0xfb923c;  // Cam nhạt       — mặt phẳng thứ tư (mặt bên 2)
const COLOR_PLANE_5  = 0xe879f9;  // Hồng tím       — mặt phẳng thứ năm (mặt bên 3)
const COLOR_PLANE_BASE = 0x64748b;// Xám trung tính — mặt đáy của hình chóp/lăng trụ

// ĐƯỜNG THẲNG MỞ RỘNG
const COLOR_LINE_C   = 0x34d399;  // Xanh ngọc — đường thứ ba
const COLOR_LINE_D   = 0xfb923c;  // Cam       — đường thứ tư

// CẠNH HÌNH KHỐI — dùng cho lăng trụ, hình chóp
const COLOR_EDGE_SOLID  = 0xe6edf3;  // Trắng sáng — cạnh nhìn thấy (nét liền)
const COLOR_EDGE_HIDDEN = 0x444d56;  // Xám tối    — cạnh bị khuất (nét đứt, opacity 0.5)

// TRỤC TOẠ ĐỘ (chuẩn Three.js AxesHelper)
const COLOR_AXIS_X  = 0xff5555;   // Đỏ
const COLOR_AXIS_Y  = 0x55ff55;   // Xanh lá
const COLOR_AXIS_Z  = 0x5599ff;   // Xanh dương
```

**Opacity mặt phẳng:**
```javascript
// Mặt phẳng chính (α, β): opacity 0.18–0.25 — nhìn xuyên thấy được, không che đường
// Mặt phẳng phụ trợ (chứa góc, kết quả): opacity 0.12–0.18 — nhẹ hơn mặt phẳng chính
// Mặt phẳng bị ẩn (học sinh tắt đi): opacity 0
// Không bao giờ dùng opacity > 0.35 trên nền tối — sẽ che khuất đường thẳng và điểm
```

**Quy tắc 2 sắc độ cho đường thẳng + vector:**
```
Mỗi đường thẳng có 2 màu liên quan:
  - Màu CHÍNH (đậm hơn):  cho đường thẳng thật
  - Màu SÁNG HƠN (~15%): cho vector chỉ phương của chính đường đó

Không đổi hue — chỉ tăng lightness một chút. Ví dụ:
  a: #f59e0b (vàng cam) → vector: #fbbf24 (vàng sáng hơn)
  b: #ef4444 (đỏ)       → vector: #f87171 (đỏ nhạt hơn)
```

### 1.4 Typography — đồng nhất với hệ thống

```css
/* Dùng đúng font này — không dùng Be Vietnam Pro dù file mẫu đang dùng */
@import url('https://fonts.googleapis.com/css2?family=Plus+Jakarta+Sans:ital,wght@0,400;0,500;0,600;0,700;0,800;1,400&display=swap');

body {
  font-family: 'Plus Jakarta Sans', system-ui, sans-serif;
  font-size: 14px;
  line-height: 1.6;
  color: var(--text);
  background: var(--bg);
}
```

### 1.5 Icon Library

```html
<!-- Dùng Tabler Icons — đồng nhất với Toán 2D / Lý / Hoá -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css">

<!-- Hay dùng trong Hình học không gian: -->
<!-- ti-cube          → Hình học 3D, hình chóp -->
<!-- ti-vector        → Vector chỉ phương -->
<!-- ti-eye / ti-eye-off → Hiện/ẩn đối tượng -->
<!-- ti-refresh       → Reset camera / Reset bài -->
<!-- ti-ruler         → Khoảng cách, đo lường -->
<!-- ti-angle         → Góc -->
<!-- ti-plane         → Mặt phẳng -->
<!-- ti-info-circle   → Info box -->
<!-- ti-check         → Kết luận đúng -->
```

### 1.6 Tokens riêng cho Nhánh B — Catalog Sidebar + Mode Toolbar

> Mọi token ở 1.1–1.5 dùng CHUNG cho cả 2 nhánh (bảng màu đối tượng hình học
> giống nhau — `solid_library.html` dùng đúng `COLOR_PLANE_*`, `COLOR_EDGE_*`,
> `COLOR_RESULT` ở 1.3). Phần dưới đây là token MỚI, chỉ Nhánh B cần, đã verify
> trong `solid_library.html`.
>
> **⚠️ Cập nhật 07/2026 — layout catalog đã đổi hẳn.** Bản trước dùng catalog
> cố định 240px chiếm chỗ vĩnh viễn (`#catalog`). Sau khi nhận phản hồi rằng
> canvas — nơi học sinh thao tác chính — bị co hẹp thường xuyên, đã đổi sang
> **icon-rail 48px cố định + overlay nổi đè lên canvas khi cần** (không chiếm
> chỗ, tự đóng sau khi chọn khối). Token `#catalog` bên dưới KHÔNG còn tồn tại
> trong code, giữ token mới thay thế.

```css
/* Icon-rail (trái, 48px cố định) — thay cho catalog 240px cũ */
#icon-rail { width: 48px; flex-shrink: 0; background: #fff;
             border-right: 1px solid #d1dce8; display: flex; flex-direction: column;
             align-items: center; justify-content: center; gap: 8px; padding: 10px 0; z-index: 15; }
.rail-btn { width: 36px; height: 36px; border-radius: 10px; border: none;
            background: transparent; color: #64748b; cursor: pointer;
            display: flex; align-items: center; justify-content: center; font-size: 17px; }
.rail-btn:hover { background: #eaf1f8; color: #0d2b4e; }
.rail-btn.active { background: #0d2b4e; color: #fff; }
/* Icon SVG nét mảnh (stroke=currentColor, không dùng ký tự Unicode) — 1 icon/nhóm khối:
   Tứ diện (khung dây), Chóp (đáy thoi phối cảnh + đỉnh), Lăng trụ & Hộp (lập phương),
   Đa diện đặc biệt (bát diện), Khối tròn xoay (quả cầu có kinh/vĩ tuyến) */

/* Overlay catalog — trượt ra đè lên canvas, KHÔNG đẩy layout, tự đóng khi chọn xong khối */
#catalog-overlay { position: absolute; top: 0; left: 48px; bottom: 0; width: 260px;
           background: #fff; border-right: 1px solid #d1dce8; display: flex;
           flex-direction: column; overflow: hidden; z-index: 20;
           box-shadow: 8px 0 28px rgba(10,22,40,.16);
           transform: translateX(-12px); opacity: 0; pointer-events: none;
           transition: transform .16s ease, opacity .16s ease; }
#catalog-overlay.open { transform: translateX(0); opacity: 1; pointer-events: auto; }
.cat-header { padding: 10px 14px; background: #f4f8fb; border-bottom: 1px solid #d1dce8;
              font-size: 11px; font-weight: 700; text-transform: uppercase;
              letter-spacing: .06em; color: #0d2b4e;
              display: flex; align-items: center; justify-content: space-between; }
.cat-overlay-close { cursor: pointer; color: #94a3b8; font-size: 13px; font-weight: 700; }
.cat-search-wrap { padding: 8px 10px; border-bottom: 1px solid #edf2f7; position: relative; }
#cat-search { width: 100%; padding: 7px 10px 7px 30px; font-size: 12px; border-radius: 8px;
              border: 1px solid #d1dce8; background: #f8fafc; color: #0d2b4e; }
.cat-list { flex: 1; overflow-y: auto; }

/* Accordion nhóm khối — bên trong overlay, hành vi đổi: click 1 icon rail →
   CHỈ mở đúng 1 nhóm tương ứng (các nhóm khác tự thu gọn), auto-scroll tới nhóm đó */
.cg-header { display: flex; align-items: center; justify-content: space-between;
             padding: 9px 12px; cursor: pointer; font-size: 12px; font-weight: 700;
             color: #0d2b4e; background: #f8fafc; }
.cg-header .cg-count { font-size: 10px; font-weight: 600; color: #94a3b8;
                        background: #e2e8f0; border-radius: 10px; padding: 1px 7px; }
.cg-header .cg-arrow { transition: transform .2s; }
.cg-header.open .cg-arrow { transform: rotate(180deg); }
.cg-body { display: none; padding: 5px 7px; }
.cg-body.open { display: flex; flex-direction: column; gap: 2px; }
.shape-btn { width: 100%; text-align: left; padding: 7px 10px; font-size: 12px;
             border-radius: 7px; border: none; background: transparent; color: #4a5568; }
.shape-btn.active { background: #0d2b4e; color: #fff; font-weight: 600; }
.shape-btn .shape-tag { display: block; font-size: 10px; color: #94a3b8; }

/* Mode toolbar (nổi trên canvas, góc trên trái) — 6 nút hiện tại:
   Xem / Thêm điểm / Nối / Xoá / Hạ đường cao / Thiết diện.
   (Đã bỏ "Kéo đỉnh" khỏi Nhánh B — xem 05_threejs_engine.md PHẦN 7.4 ghi chú phạm vi) */
#mode-bar { position: absolute; top: 14px; left: 14px; z-index: 10;
            display: flex; gap: 6px; background: rgba(10,22,40,0.88);
            padding: 6px 8px; border-radius: 10px; backdrop-filter: blur(8px); }
.mode-btn { display: flex; align-items: center; gap: 5px; padding: 6px 11px;
            border: none; border-radius: 7px; font-size: 12px; font-weight: 700;
            color: rgba(255,255,255,0.65); background: transparent; }
.mode-btn.active { background: #0e7a6e; color: white; }
.mode-hint { font-size: 11px; padding: 6px 10px; border-radius: 6px;
             background: #fef3c7; color: #92400e; font-weight: 600; }
.mode-hint.green { background: #d1fae5; color: #065f46; }

/* Nút toggle hiện toạ độ X,Y,Z nổi trên canvas (góc trên PHẢI, đối xứng mode-bar) */
#coord-toggle-btn { position: absolute; top: 14px; right: 14px; z-index: 10;
          padding: 6px 11px; border-radius: 7px; font-size: 12px; font-weight: 700;
          color: rgba(255,255,255,0.65); background: rgba(10,22,40,0.88);
          border: 1px solid rgba(255,255,255,0.1); backdrop-filter: blur(8px); }
#coord-toggle-btn.active { background: #0e7a6e; color: white; }
/* Nhãn (x,y,z) nổi cạnh từng điểm trong canvas khi bật toggle trên */
.coord-label { position: absolute; font-size: 10px; font-weight: 600; color: #cbd5e1;
          background: rgba(10,22,40,.72); padding: 1px 5px; border-radius: 4px;
          pointer-events: none; display: none; }

/* Section header thu gọn/mở rộng (▾) — dùng cho "Khối hình" và
   "Điểm & Đoạn thẳng" trong config sidebar phải */
.s-section-head { display: flex; align-items: center; justify-content: space-between;
          cursor: pointer; user-select: none; }
.s-chevron { font-size: 12px; color: #94a3b8; transition: transform .18s; }
.s-chevron.collapsed { transform: rotate(-90deg); }

/* Danh sách điểm/đoạn thẳng trong config sidebar — ĐỔI: giờ có ô đổi tên
   inline + ô sửa x/y/z (áp dụng cho CẢ đỉnh gốc lẫn điểm tự do) thay vì chỉ
   hiện tên tĩnh + toạ độ chỉ đọc như bản trước */
.pt-row { display: flex; flex-direction: column; gap: 3px; padding: 6px 8px;
          border-radius: 6px; font-size: 12px; border: 2px solid transparent;
          background: #f8fafc; }
.pt-row.sel { border-color: #0e7a6e; background: #d1fae5; } /* đang chọn để nối/thiết diện */
.pt-name-input { font-weight: 700; color: #0d2b4e; width: 42px; border: 1px solid transparent;
          border-radius: 4px; background: transparent; }
.pt-name-input:hover, .pt-name-input:focus { border-color: #d1dce8; background: #fff; }
.pt-xyz { color: #64748b; font-size: 10px; } /* chỉ đọc — tâm/đỉnh khối tròn xoay */
.pt-xyz-edit input { width: 42px; border: 1px solid #d1dce8; border-radius: 4px;
          padding: 2px 3px; font-size: 10px; text-align: center; } /* sửa được */
.pt-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
.pt-del, .seg-del { margin-left: auto; color: #ef4444; cursor: pointer; }
.seg-item { display: flex; align-items: center; gap: 8px; padding: 4px 8px;
            border-radius: 6px; background: #f8fafc; font-size: 12px; }

/* Khối công thức thể tích/diện tích — CHỈ hiện công thức chữ, KHÔNG tính ra
   số (chủ đích sư phạm: không lộ đáp số bài tập) */
.formula-box { margin-top: 8px; padding: 8px 10px; background: #f0f9ff;
          border: 1px solid #bae6fd; border-radius: 8px; font-size: 12.5px; color: #0c4a6e; }

/* Ô đổi màu thiết diện (input type="color") trong danh sách "Thiết diện đã tạo" */
input.section-color { width: 22px; height: 22px; padding: 0; border: 1px solid #d1dce8;
          border-radius: 5px; cursor: pointer; background: none; }

/* Slider kích thước khối trong config sidebar */
.slider-row label { display: flex; justify-content: space-between; font-size: 12px; }
.slider-row input[type=range] { width: 100%; accent-color: #0e7a6e; }
```

> **Không tạo màu mới cho mode-bar/catalog/coord-toggle-btn** — dùng đúng
> `--navy`/`--teal` đã có ở 1.2. Nền `rgba(10,22,40,0.88)` là navy pha alpha,
> không phải màu mới.

---

## PHẦN 2 — COMPONENT LIBRARY 3D

> **Áp dụng cho:** 2.1–2.9 dùng cho Nhánh A (bài học, có step-tabs). 2.10–2.13
> (cuối phần) dùng cho Nhánh B (kho công cụ, có catalog + mode toolbar).
> Header (2.1), canvas wrap (2.2), responsive (2.9) áp dụng cho CẢ 2 nhánh.

### 2.1 Header chuẩn

```html
<header>
  <div class="header-badge">🧊 Hình học không gian</div>
  <h1>Tên bài học</h1>
</header>
```

```css
header {
  background: linear-gradient(135deg, var(--navy) 0%, #1a4a7a 100%);
  color: #fff;
  padding: 18px 28px 16px;
  display: flex;
  align-items: center;
  gap: 14px;
}
.header-badge {
  background: rgba(255,255,255,0.15);
  border: 1px solid rgba(255,255,255,0.25);
  border-radius: 20px;
  padding: 4px 12px;
  font-size: 11px; font-weight: 600;
  letter-spacing: .06em;
  text-transform: uppercase;
  white-space: nowrap;
}
header h1 {
  font-size: 17px; font-weight: 700;
  letter-spacing: .01em;
  flex: 1;
}
```

### 2.2 Canvas wrap + canvas hint

```html
<div class="canvas-wrap" id="canvas-wrap">
  <!-- Three.js renderer append vào đây -->
  <div id="label-layer"></div>  <!-- HTML overlay cho label điểm/đường -->
  <div class="canvas-hint">🖱 Kéo để xoay · Cuộn để zoom · Nhấn giữa để dịch chuyển</div>
</div>
```

```css
.canvas-wrap {
  flex: 1;
  position: relative;
  background: #0a1628;  /* hoặc màu canvas của preset đã chọn */
  min-height: 500px;
}
.canvas-hint {
  position: absolute; bottom: 14px; left: 50%;
  transform: translateX(-50%);
  background: rgba(255,255,255,0.10);
  color: rgba(255,255,255,0.75);
  border: 1px solid rgba(255,255,255,0.15);
  border-radius: 20px;
  padding: 5px 14px;
  font-size: 11.5px;
  pointer-events: none; white-space: nowrap;
}
/* Label layer — đè lên canvas, pointer-events: none để không chặn click Three.js */
#label-layer {
  position: absolute; top: 0; left: 0;
  width: 100%; height: 100%;
  pointer-events: none; overflow: hidden;
}
```

### 2.3 Sidebar step-tabs

```html
<div class="sidebar">
  <div class="step-tabs">
    <div class="step-tab active" data-step="1">Bước 1</div>
    <div class="step-tab" data-step="2">Bước 2</div>
    <div class="step-tab" data-step="3">Kết luận</div>
  </div>
  <div class="step-body">
    <!-- step panels -->
  </div>
  <div class="controls">
    <!-- toggles, btn-reset -->
  </div>
</div>
```

```css
.sidebar {
  width: 310px;
  background: var(--surface);
  border-left: 1px solid var(--border);
  display: flex; flex-direction: column;
  overflow-y: auto;
}
.step-tabs { display: flex; border-bottom: 1px solid var(--border); }
.step-tab {
  flex: 1; padding: 11px 4px;
  font-size: 11px; font-weight: 600;
  text-align: center; cursor: pointer;
  color: var(--sub);
  border-bottom: 2.5px solid transparent;
  transition: all .2s;
  letter-spacing: .04em; text-transform: uppercase;
}
.step-tab.active {
  color: var(--navy);
  border-bottom-color: var(--teal);
  background: #f7fafc;
}
.step-body { padding: 18px 18px 12px; flex: 1; }
.step-panel { display: none; }
.step-panel.active { display: block; }
```

### 2.4 Step title + step-num

```html
<div class="step-title">
  <div class="step-num">1</div>
  Tên bước
</div>
<!-- Bước kết luận: -->
<div class="step-title">
  <div class="step-num">✓</div>
  Kết luận
</div>
```

```css
.step-title {
  font-size: 13px; font-weight: 700;
  color: var(--navy);
  margin-bottom: 10px;
  display: flex; align-items: center; gap: 8px;
}
.step-num {
  width: 22px; height: 22px;
  border-radius: 50%;
  background: var(--teal);
  color: #fff;
  font-size: 11px; font-weight: 700;
  display: flex; align-items: center; justify-content: center;
  flex-shrink: 0;
}
.step-desc {
  font-size: 12.5px; line-height: 1.65;
  color: #334155; margin-bottom: 14px;
}
```

### 2.5 Info boxes — 4 loại ngữ nghĩa

```html
<!-- Định nghĩa / điều kiện -->
<div class="info-box ib-blue">
  <div class="ib-icon">📐</div>
  <div>
    <div class="ib-title">Tiêu đề</div>
    Nội dung...
  </div>
</div>

<!-- Gợi ý / hướng dẫn -->
<div class="info-box ib-teal">
  <div class="ib-icon">💡</div>
  <div>Nội dung...</div>
</div>

<!-- Điều kiện cần và đủ / lưu ý quan trọng -->
<div class="info-box ib-gold">
  <div class="ib-icon">⚠️</div>
  <div>
    <div class="ib-title">Điều kiện cần và đủ</div>
    Nội dung...
  </div>
</div>

<!-- Phản ví dụ / không thỏa mãn -->
<div class="info-box ib-red">
  <div class="ib-icon">❌</div>
  <div>Nội dung...</div>
</div>
```

```css
.info-box {
  border-radius: var(--radius); padding: 12px 13px;
  display: flex; gap: 10px;
  margin-bottom: 10px;
  font-size: 12px; line-height: 1.6;
}
.info-box .ib-icon { font-size: 16px; flex-shrink: 0; margin-top: 1px; }
.info-box .ib-title { font-weight: 700; font-size: 11.5px; margin-bottom: 3px; }
.ib-blue  { background: #eff6ff; border: 1px solid #bfdbfe; color: #1e3a5f; }
.ib-teal  { background: #f0fdf9; border: 1px solid #99f6e4; color: #134e4a; }
.ib-gold  { background: #fffbeb; border: 1px solid #fde68a; color: #78350f; }
.ib-red   { background: #fef2f2; border: 1px solid #fecaca; color: #7f1d1d; }
```

### 2.6 Legend (chú thích màu đối tượng)

```html
<div class="legend">
  <div class="legend-row">
    <div class="legend-dot" style="background:#3b82f6; opacity:.55"></div>
    <span class="legend-label">Mặt (α)</span>
    <span style="color:var(--sub)">mặt phẳng phía dưới</span>
  </div>
  <div class="legend-row">
    <div class="legend-dot" style="background:#f59e0b; height:4px"></div>
    <span class="legend-label">a</span>
    <span style="color:var(--sub)">nằm trong mặt phẳng (α)</span>
  </div>
</div>
```

```css
.legend { margin-top: 6px; }
.legend-row {
  display: flex; align-items: center; gap: 9px;
  padding: 6px 0;
  border-bottom: 1px solid #f1f5f9;
  font-size: 12px; color: #334155;
}
.legend-row:last-child { border-bottom: none; }
.legend-dot { width: 14px; height: 6px; border-radius: 3px; flex-shrink: 0; }
.legend-label { font-weight: 600; min-width: 26px; }
```

### 2.7 Conclusion box

```html
<div class="conclusion">
  Nội dung kết luận... <strong>a ∥ b</strong>.
  <br><br>
  Câu bổ sung thêm nếu cần.
</div>
```

```css
.conclusion {
  background: linear-gradient(135deg, #0d2b4e, #0e7a6e);
  color: #fff; border-radius: var(--radius);
  padding: 14px 15px;
  font-size: 12.5px; line-height: 1.65;
  margin-top: 2px;
}
.conclusion strong { color: #6ee7b7; }
/* Để highlight kết quả quan trọng (ví dụ số đo góc): */
.conclusion strong.result { color: #fde68a; }
```

### 2.8 Controls — toggle switches và btn-reset

```html
<div class="controls">
  <div class="ctrl-title">Hiển thị</div>
  <div class="toggle-row">
    <span>Mặt phẳng (α) và (β)</span>
    <button class="toggle on" id="tog-planes" onclick="togglePlanes()"></button>
  </div>
  <div class="toggle-row">
    <span>Đường thẳng a</span>
    <button class="toggle" id="tog-a" onclick="toggleLineA()"></button>
  </div>
  <button class="btn-reset" onclick="resetCamera()">↺ Đặt lại góc nhìn</button>
</div>
```

```css
.controls { padding: 14px 18px; border-top: 1px solid var(--border); }
.ctrl-title {
  font-size: 11px; font-weight: 700; text-transform: uppercase;
  letter-spacing: .07em; color: var(--sub); margin-bottom: 10px;
}
.toggle-row {
  display: flex; justify-content: space-between; align-items: center;
  margin-bottom: 8px; font-size: 12.5px; color: #334155;
}
.toggle {
  width: 36px; height: 20px; border-radius: 10px;
  background: #cbd5e1; position: relative; cursor: pointer;
  transition: background .2s; border: none;
}
.toggle.on { background: var(--teal); }
.toggle::after {
  content: ''; position: absolute; left: 3px; top: 3px;
  width: 14px; height: 14px; border-radius: 50%;
  background: #fff; transition: transform .2s;
}
.toggle.on::after { transform: translateX(16px); }
.btn-reset {
  width: 100%; padding: 9px;
  background: var(--navy); color: #fff;
  border: none; border-radius: 8px;
  font-size: 13px; font-weight: 600;
  cursor: pointer; margin-top: 10px;
  font-family: inherit; transition: background .2s;
}
.btn-reset:hover { background: #1a4a7a; }
```

### 2.9 Responsive

```css
@media (max-width: 680px) {
  .main { flex-direction: column; }
  .sidebar { width: 100%; border-left: none; border-top: 1px solid var(--border); }
  .canvas-wrap { min-height: 320px; }
}
```

> ⚠️ Không tự thêm `height: 50%` cho `.sidebar` ở breakpoint này — sidebar để
> chiều cao tự nhiên, cuộn theo trang. Ép `height: 50%` (đã gặp ở file build
> trước 08/2026) làm sidebar bị chật trên mobile khi nội dung bước dài hơn
> nửa màn hình, không đúng tinh thần spec ở trên.

---

### 2.9b Resize — báo chiều cao thật cho LMS (khắc phục khoảng trắng thừa cuối trang)

> **Đồng bộ với `02_design_toan_final.md` §7.2 + §7.7 + §7.8 — 3D trước giờ
> chưa có mục này, đây là phần bổ sung mới.** Áp dụng cho CẢ 2 nhánh.
>
> **Vì sao 3D cần diễn giải lại, không copy y nguyên:** cơ chế resize của
> 2D dựa vào `document.documentElement.scrollHeight` để báo chiều cao THẬT
> của trang cho LMS (LMS nhúng file bằng iframe — không báo đúng chiều cao
> thì LMS phải đoán, để lại khoảng trắng lớn trước file/video kế tiếp).
> Cơ chế này chỉ đúng khi `body` được để co giãn tự nhiên theo nội dung.
> 3D trước giờ luôn khoá `body { height:100vh; overflow:hidden }` (kiến
> trúc "app-shell" — xem Header/Canvas/Sidebar ở §Bước 4) → `scrollHeight`
> lúc đó luôn bằng đúng viewport, không phản ánh nội dung thật, khiến
> `resize()` báo sai ngay từ đầu. **Đây chính là nguyên nhân khoảng trắng
> thừa khi nhúng file 3D lên LMS.**

**Bắt buộc — bỏ khoá viewport ở cấp `body`:**
```css
/* SAI — không dùng cho file build mới */
body { height: 100vh; overflow: hidden; }

/* ĐÚNG — body co theo nội dung thật, không ép bằng viewport */
body { /* không set height/overflow ở đây */ }
```
> Vùng cần giữ chiều cao cố định (canvas cần kích thước pixel xác định để
> Three.js render đúng) đặt ở cấp `.app-body`/`.main` — KHÔNG đặt ở `body`.
> Ví dụ: `.app-body { height: 640px; }` (giống quy ước `.sim-card` 640px
> của 2D) hoặc theo đúng số đã chốt ở §Bước 4 (`Canvas flex:1 min-500px`).
> Bên trong khối đó vẫn có thể `overflow:hidden` + sidebar `overflow-y:auto`
> như cũ — chỉ bỏ việc ép **toàn trang** bằng `100vh`, không đổi cách canvas
> lấy kích thước (`wrap.clientWidth/clientHeight` ở `05_threejs_engine.md`
> không phụ thuộc `body` có `100vh` hay không).

**Safe accessor (dán đầu `<script>` đầu tiên — dùng chung 2D/3D, không đổi):**
```javascript
function LMS(){return window.AiducationLMS||{ready:function(){},progress:function(){},event:function(){},state:function(){},complete:function(){},resize:function(){}};}
```

**Gọi resize khi tải xong và mỗi khi chiều cao đổi:**
```javascript
function reportHeight() {
  const h = document.documentElement.scrollHeight;
  LMS().resize({ height: h });
}
window.addEventListener('load', reportHeight);
if (typeof ResizeObserver !== 'undefined') {
  const ro = new ResizeObserver(() => { clearTimeout(window._rz); window._rz = setTimeout(reportHeight, 100); });
  ro.observe(document.body);
} else {
  setInterval(reportHeight, 800); // fallback — WebView cũ không có ResizeObserver
}
```

**Checklist trước khi coi 1 file 3D là "sẵn sàng LMS" (bổ sung riêng cho 3D):**
- [ ] `body` KHÔNG có `height: 100vh` / `min-height: 100vh` / `overflow: hidden` ở cấp body
- [ ] Chiều cao cố định (nếu cần cho canvas) đặt ở `.app-body`/`.main`, không đặt ở `body`
- [ ] Đã gọi `LMS().resize()` lúc load + qua `ResizeObserver` mỗi khi nội dung đổi chiều cao
      (đổi step-tab, mở/đóng panel, hiện kết luận...)
- [ ] Test thử: thu nhỏ cửa sổ trình duyệt xuống mobile — trang cuộn được bình thường,
      không bị cắt/khoá ở đúng 1 màn hình

---

### 2.10 (Nhánh B) Icon-rail + Catalog Overlay — thay accordion sidebar cố định

> **⚠️ Cập nhật 07/2026 — đổi hẳn cấu trúc so với bản trước** (accordion
> trong `#catalog` 240px cố định). Lý do đổi: canvas — nơi học sinh thao
> tác chính — bị co hẹp thường xuyên dù không cần dùng catalog. Giờ tách
> làm 2: dải icon 48px cố định (không đóng được) + overlay accordion nổi
> đè lên canvas, ẩn/hiện theo yêu cầu.

```html
<div id="icon-rail"></div> <!-- render bằng JS, 1 icon SVG / nhóm khối trong CATALOG -->

<div id="catalog-overlay">
  <div class="cat-header">
    <span>📚 Danh sách khối</span>
    <span class="cat-overlay-close" onclick="closeCatalogOverlay()">✕</span>
  </div>
  <div class="cat-search-wrap">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
      <circle cx="11" cy="11" r="8"/><path d="m21 21-4.35-4.35"/>
    </svg>
    <input id="cat-search" type="text" placeholder="Tìm khối…" oninput="buildCatalog(this.value)">
  </div>
  <div class="cat-list" id="cat-list"></div>
  <!-- accordion group render bằng JS — xem buildCatalog() trong 05_threejs_engine.md PHẦN 9.5 -->
</div>
```

```javascript
// Cấu trúc CATALOG không đổi — vẫn nhóm khối theo chương SGK, cờ round
// quyết định tra thư viện nào. Khác biệt: giờ CATALOG còn được dùng để
// suy ra icon rail (1 icon/nhóm, theo đúng thứ tự mảng) VÀ để tra công
// thức thể tích theo nhóm (xem 2.12 bên dưới).
const CATALOG = [
  { label: 'Tứ diện', keys: ['tet_deu', 'tet_vuong', 'tet_thuong'] },        // → SOLID_LIBRARY
  { label: 'Khối tròn xoay', keys: ['khoi_cau','khoi_tru','khoi_non'], round: true }, // → ROUND_LIBRARY
];
```

> **Hành vi overlay:** click 1 icon trong `#icon-rail` → mở overlay, tự
> thu gọn accordion về ĐÚNG 1 nhóm tương ứng (không mở tràn lan như bản
> accordion cũ), tự cuộn tới đầu nhóm đó. Chọn xong 1 khối → overlay tự
> đóng ngay. Bấm lại đúng icon đang mở, bấm nút ✕, hoặc click ra ngoài
> overlay/rail → cũng đóng. Search vẫn lọc theo `info.name`/`info.notation`,
> không phân biệt hoa/thường, không đổi so với bản trước.

### 2.11 (Nhánh B) Mode Toolbar — float trên canvas, khoá 1 hành động/lúc

> **⚠️ Cập nhật 07/2026:** đã bỏ nút "Kéo đỉnh" (`mbtn-explore`) khỏi
> toolbar này — không phải xoá tính năng khỏi tài liệu chung (pattern vẫn
> giữ nguyên ở `05_threejs_engine.md` PHẦN 7.4 cho công cụ khác dùng), chỉ
> là `solid_library.html` không dùng nữa. Thêm mới nút "Thiết diện".

```html
<div id="mode-bar">
  <button class="mode-btn active" id="mbtn-view" onclick="setMode('view')">
    <span class="mode-icon">🔒</span> Xem
  </button>
  <button class="mode-btn" id="mbtn-point" onclick="setMode('point')">
    <span class="mode-icon">✦</span> Thêm điểm
  </button>
  <button class="mode-btn" id="mbtn-connect" onclick="setMode('connect')">
    <span class="mode-icon">⟶</span> Nối
  </button>
  <button class="mode-btn" id="mbtn-delete" onclick="setMode('delete')">
    <span class="mode-icon">🗑</span> Xoá
  </button>
  <button class="mode-btn" id="mbtn-height" onclick="setMode('height')">
    <span class="mode-icon">⊥</span> Hạ đường cao
  </button>
  <button class="mode-btn" id="mbtn-section" onclick="setMode('section')">
    <span class="mode-icon">✂</span> Thiết diện
  </button>
</div>
<div id="mode-hint">🔒 Xoay / zoom tự do</div>
<button id="coord-toggle-btn" onclick="toggleCoords()">📐 Toạ độ X,Y,Z</button>
```

> **Quy tắc bắt buộc:** `#mode-bar` đặt góc trên TRÁI canvas, `#coord-toggle-btn`
> đối xứng ở góc trên PHẢI (không tranh chỗ nhau). Luôn có `#mode-hint` ngay
> dưới toolbar hiện hướng dẫn theo mode đang chọn. Với khối tròn xoay, ẩn
> `mbtn-height` (chưa hỗ trợ — cần vertices/faces đặt tên); `mbtn-section`
> (Thiết diện) dùng được cho CẢ 2 loại khối nhưng với khối tròn xoay chỉ nối
> thẳng 3 điểm (chưa tính được giao tuyến conic thật — xem
> `06_geometry_math.md` G.4). Xem `updateModeBarVisibility()` trong
> `05_threejs_engine.md` PHẦN 9.4.

### 2.12 (Nhánh B) Config Sidebar phải — slider kích thước + danh sách điểm/đoạn

> **⚠️ Cập nhật 07/2026 — nhiều thay đổi so với bản trước:**
> 1. "Khối hình" và "Điểm & Đoạn thẳng" giờ **thu gọn/mở rộng được** (chevron
>    ▾, trạng thái giữ nguyên suốt phiên làm việc, không tự mở lại khi đổi
>    khối/sửa điểm).
> 2. "Khối hình" có thêm khối công thức thể tích/diện tích — **CHỈ công thức
>    chữ, không tính ra số** (chủ đích sư phạm, xem `getSolidVolumeFormulaHTML()`
>    trong code — suy công thức theo NHÓM catalog, không hardcode từng khối).
> 3. Mỗi dòng điểm giờ có **ô tên sửa được inline** (áp dụng cho cả đỉnh gốc
>    A,B,C,S... lẫn điểm tự do) và **ô x/y/z sửa được** (đỉnh gốc đa diện sửa
>    được — xem `05_threejs_engine.md` PHẦN 7.10; tâm/đỉnh khối tròn xoay vẫn
>    chỉ đọc vì không ảnh hưởng hình dạng thật).
> 4. Có thêm danh sách "Thiết diện đã tạo" với ô đổi màu (`input type="color"`).

```html
<div id="sidebar">
  <div class="s-section">
    <div class="s-section-head" onclick="toggleKhoiHinhCollapse()">
      <h3>Khối hình</h3>
      <span class="s-chevron" id="khoi-hinh-chevron">▾</span>
    </div>
    <div id="khoi-hinh-body">
      <div style="font-size:13px;font-weight:600;color:#0d2b4e">Hình chóp tứ giác đều</div>
      <p class="note">Đáy hình vuông, đỉnh S nằm trên tâm đáy.</p>
      <div class="formula-box">V = (1/3) · S<sub>đáy</sub> · h</div>
    </div>
  </div>
  <div class="s-section">
    <h3>Kích thước</h3>
    <div class="slider-row">
      <label>Chiều cao (h) <span id="lbl-h">3.0</span></label>
      <input type="range" min=".5" max="5" step=".1" value="3" oninput="onSlider('h',this.value)">
    </div>
  </div>
  <div class="s-section" id="pts-section"></div> <!-- render bằng updatePtsSidebar() -->
</div>
```

```html
<!-- 1 dòng điểm (áp dụng chung cho đỉnh gốc lẫn điểm tự do) trong pts-section -->
<div class="pt-row">
  <div class="pt-row-top">
    <div class="pt-dot" style="background:#FAC775"></div>
    <input class="pt-name-input" value="M" onchange="renamePoint(3, this.value)">
    <span class="pt-loc">cạnh SA</span>
    <span class="pt-del" onclick="removePoint(3)">✕</span>
  </div>
  <!-- điểm tự do: 3 ô sửa được -->
  <div class="pt-xyz-edit">
    <label>x<input value="1.20" onchange="applyPointXYZ(3,'x',this.value)"></label>
    <label>y<input value="0.00" onchange="applyPointXYZ(3,'y',this.value)"></label>
    <label>z<input value="2.40" onchange="applyPointXYZ(3,'z',this.value)"></label>
  </div>
</div>
<!-- 1 dòng đoạn nối -->
<div class="seg-item">
  <span style="font-weight:700">MN</span>
  <span class="seg-del" onclick="removeSegment(1)">✕</span>
</div>
<!-- 1 dòng thiết diện -->
<div class="seg-item">
  <input type="color" class="section-color" value="#f59e0b" onchange="setSectionColor(0,this.value)">
  <span style="font-weight:700;flex:1">qua M, N, P</span>
  <span class="seg-del" onclick="removeSection(0)">✕</span>
</div>
```


### 2.13 (Nhánh B) Không dùng — step-tabs, kết luận, canvas-hint cố định

> Nhánh B **không có** các component sau (dù chúng thuộc PHẦN 2 dùng cho
> Nhánh A) — đừng vô tình build nhầm:
> - `.step-tabs` / `.step-panel` (2.3) — kho công cụ không có tiến trình bước
> - `.conclusion` (2.7) — không có "kết luận", vì không phải 1 bài cụ thể
> - `.canvas-hint` cố định (2.2) — thay bằng `#mode-hint` động theo mode (2.11)

---

## PHẦN 3 — KỸ THUẬT THREE.JS (BRIDGE SANG `05_threejs_engine.md`)

> File này chỉ ghi **quy tắc build áp dụng trực tiếp** — không lặp lại code đã có trong
> `05_threejs_engine.md`. Khi build, đọc song song cả 2 file.

### 3.1 Setup bắt buộc

```
- Dùng đúng Three.js r128 + OrbitControls r128
- ResizeObserver thay vì window.resize để canvas co giãn đúng với canvas-wrap
- renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2)) — tránh quá nặng trên màn retina
- scene.background = new THREE.Color(0x0a1628) — dùng đúng màu canvas của preset đã chọn
```

### 3.2 Ánh sáng chuẩn cho hình học

```javascript
// Mọi bài hình học không gian dùng bộ ánh sáng này:
scene.add(new THREE.AmbientLight(0xffffff, 0.8));
// Không cần DirectionalLight cho đường/mặt phẳng thuần (không có mesh đặc cần đổ bóng)
// Chỉ thêm DirectionalLight khi có hình chóp/trụ đặc cần bóng để nhìn rõ khối
```

### 3.3 Label điểm/đường — luôn dùng HTML overlay

```
- LUÔN dùng HTML overlay (div trong #label-layer, đồng bộ qua project()) cho label tên điểm và số đo
- KHÔNG dùng Sprite cho tên điểm — chữ Việt dễ bị mờ, khó style đồng nhất với sidebar
- Xem PHẦN 3.2 trong 05_threejs_engine.md để lấy code syncHtmlLabel() đã verify
- Nhớ kiểm tra screenPos.z > 1 để ẩn label khi điểm ở sau camera
```

### 3.4 (Nhánh A) Step tabs đồng bộ với Three.js scene

> Chỉ áp dụng Nhánh A. Nhánh B không có step-tabs — xem 3.7 cho pattern tương ứng.

```javascript
// Pattern chuẩn: mỗi lần click tab, tự động set visible đúng đối tượng
document.querySelectorAll('.step-tab').forEach(tab => {
  tab.addEventListener('click', () => {
    const step = tab.dataset.step;
    // 1. Cập nhật active class
    document.querySelectorAll('.step-tab').forEach(t => t.classList.remove('active'));
    document.querySelectorAll('.step-panel').forEach(p => p.classList.remove('active'));
    tab.classList.add('active');
    document.getElementById('panel-' + step).classList.add('active');
    // 2. Đồng bộ THREE.js scene theo step
    if (step === '1') {
      // Chỉ hiện mặt phẳng, ẩn đường...
    } else if (step === '2') {
      // Hiện mặt phẳng + đường a...
    }
    // 3. Đồng bộ lại toggle buttons sidebar
    setToggle('tog-planes', planesOn);
  });
});
```

### 3.4-BIS Sub-step/sub-tab bên trong 1 step — BẮT BUỘC clearScene()

> **Đây là nguồn lỗi thực tế phổ biến nhất khi build module kiểu "N tính chất"
> hoặc "N cách xác định X" (VD Bài 10 SGK: Mục 2 có 4-5 tính chất, Mục 3 có
> 3 cách xác định mặt phẳng) — nơi 1 step lớn (`case 2:`, `case 3:` trong
> 3.4) lại chia tiếp thành nhiều sub-step/sub-tab dùng chung 1 canvas.

**Vấn đề:** Pattern 3.4 ở trên chỉ đồng bộ scene khi đổi **step lớn**
(`step-tab`). Nó KHÔNG tự động áp dụng cho các hàm con kiểu `setupStep2()`,
`setupStep3()` xử lý việc đổi **sub-step/sub-tab** (`sub-tab-pill`,
`progress-dot`) bên trong 1 step. Nếu hàm con này chỉ đổi
`display: none/block` của `.sub-panel` mà không dispose object 3D cũ,
điểm/đường/mặt phẳng của tính chất trước vẫn nằm trong scene và bị vẽ
chồng lên tính chất mới — canvas rối, không phân biệt được hình nào thuộc
sub-step nào.

**Quy tắc bắt buộc:** Bất kỳ hàm nào đổi sub-step/sub-tab con bên trong 1
step lớn đều phải gọi `clearScene()` (PHẦN 3.6 dưới đây, bản mở rộng — xoá
toàn bộ `activePoints`/`activeLines`/`activePlanes` và các mảng đối tượng
đặc thù module) ở dòng ĐẦU TIÊN của hàm, trước khi rẽ nhánh dựng sub-step
mới. Đây là mặc định — CHỈ bỏ qua nếu kịch bản đã ghi rõ lý do sư phạm cần
giữ lại object cũ (VD module Tổng kết dùng lại scene để học sinh ôn nhanh
mà không rebuild, xem `01_scenario_builder_3d_addendum.md` BƯỚC 5).

```javascript
// ❌ SAI — chỉ đổi UI, không dọn object 3D → hình cũ chèn lên hình mới
function setupStep2() {
  document.querySelectorAll('.sub-panel').forEach((sub, idx) => {
    sub.style.display = (idx + 1 === step2SubStep) ? 'block' : 'none';
  });
  if (step2SubStep === 1) setupTC1();
  else if (step2SubStep === 2) setupTC2();
  // ... TC1's points/lines/planes vẫn còn trong scene khi setupTC2() chạy
}

// ✅ ĐÚNG — dọn sạch canvas trước khi dựng sub-step mới
function setupStep2() {
  clearScene();   // BẮT BUỘC — dòng đầu tiên, trước mọi thứ khác
  document.querySelectorAll('.sub-panel').forEach((sub, idx) => {
    sub.style.display = (idx + 1 === step2SubStep) ? 'block' : 'none';
  });
  if (step2SubStep === 1) setupTC1();
  else if (step2SubStep === 2) setupTC2();
}
```

Áp dụng đúng cách này cho MỌI hàm điều phối sub-step/sub-tab trong file —
không chỉ hàm của step 2, mà cả step 3, hoặc bất kỳ module nào khác có cấu
trúc tương tự. Khi review code trước khi bàn giao, kiểm tra: mỗi hàm dạng
`setupStepN()` có rẽ nhánh theo 1 biến sub-step nội bộ (`stepNSubStep`,
`stepNTab`...) đều phải có `clearScene()` ở đầu, trừ khi có comment giải
thích rõ lý do cố ý giữ lại object cũ.

### 3.5 Màu đối tượng → ánh xạ sang CSS cho legend

```javascript
// Mỗi đối tượng Three.js có hex (0xRRGGBB) → cần CSS string (#RRGGBB) cho legend
// Không viết 2 bộ màu riêng — dùng hàm chuyển đổi:
function hexToCSS(hex) { return '#' + hex.toString(16).padStart(6, '0'); }

// Ví dụ:
// legend-dot style="background: " + hexToCSS(COLOR_PLANE_1) // → #3b82f6
```

### 3.6 Dọn dẹp bộ nhớ khi rebuild object

> Có 2 cấp độ dọn dẹp, đừng nhầm lẫn:
> - **Cấp object đơn lẻ** (bên dưới): dispose 1 mesh khi giá trị của nó đổi
>   trong lúc học sinh đang tương tác (VD kéo điểm làm mặt phẳng đổi hình).
> - **Cấp toàn bộ scene** (`clearScene()`, xem 3.4-BIS): dọn SẠCH mọi object
>   đang có khi chuyển sang 1 step/sub-step khác hoàn toàn. `clearScene()`
>   gọi dispose theo đúng pattern dưới đây, nhưng lặp qua toàn bộ mảng
>   `activePoints`/`activeLines`/`activePlanes` (và mọi mảng đối tượng đặc
>   thù module khác) chứ không chỉ 1 biến mesh đơn lẻ.

```javascript
// BẮT BUỘC gọi trước khi tạo object thay thế — nếu không memory leak sau vài phút kéo
if (mesh) {
  scene.remove(mesh);
  mesh.geometry.dispose();
  mesh.material.dispose();
  mesh = null;
}
```

```javascript
// clearScene() — bản đầy đủ dùng ở cấp step/sub-step (3.4, 3.4-BIS)
// Lặp qua MỌI mảng đối tượng đang active, không chỉ 1 mesh
function clearScene() {
  stopDragging();
  activePoints.forEach(p => p.dispose());
  activePoints = [];
  activeLines.forEach(l => l.dispose());
  activeLines = [];
  activePlanes.forEach(pl => pl.dispose());
  activePlanes = [];
  // + mọi mảng đối tượng đặc thù module khác (VD m1PlacedPoints...)
  // + reset các mảng phụ trợ như allDraggableHitMeshes = []
}
```

### 3.7 (Nhánh B) Bridge sang `05_threejs_engine.md` PHẦN 7-9

> Nhánh B KHÔNG có state machine theo bước (3.4) — thay vào đó là **mode
> system** (setMode) và **catalog dispatch** (chọn khối → load đúng renderer).
> Toàn bộ code đã verify nằm ở `05_threejs_engine.md`, không lặp lại ở đây:

```
- Đa diện (SOLID_LIBRARY + SolidRenderer)     → 05_threejs_engine.md PHẦN 7
- Hạ đường cao (baseVertices + planeFromVertexNames) → PHẦN 8
- Tròn xoay (ROUND_LIBRARY + RoundSolidRenderer)      → PHẦN 9
- Mọi hàm toán thuần (definePlaneFromPoints, barycentricCoords,
  pointOnSphere/Cylinder/ConeSide...)                  → 06_geometry_math.md
```

> **Quy tắc bắt buộc khi build Nhánh B:** đọc CẢ 3 file (05 PHẦN 7-9 + 06 +
> file này PHẦN 2.10-2.13) trước khi viết dòng code đầu tiên — thiếu 1 trong
> 3 rất dễ dẫn đến việc viết lại 1 hàm đã có (và có thể viết SAI so với bản
> đã verify, như trường hợp `buildRightAngleMark` từng có 2 signature khác
> nhau giữa các file test).

---

## PHẦN 4 — NAMING CONVENTION

### 4.1 (Nhánh A) Bài học SGK cụ thể

```
File HTML:
  Chuong[X]_Bai[Y]_Toan3D_[TenBai].html
  Ví dụ: Chuong4_Bai10_Toan3D_SongSong.html

Three.js objects — tên biến nhất quán:
  Mặt phẳng:   planeAlphaMesh, planeBetaMesh, planeMesh (bài chỉ 1 mặt)
  Đường thẳng: lineA, lineB, lineC
  Vector:       vecA, vecB
  Điểm:         pointA, pointB, pointC, pointM, pointH (chân đường vuông góc)
  Đoạn phụ:    mhLine (đoạn MH), perpMarkMesh (dấu góc vuông), footPointH

HTML element IDs:
  Canvas:       three-canvas
  Canvas wrap:  canvas-wrap (dùng ResizeObserver trên element này)
  Label layer:  label-layer
  Panel:        panel-1, panel-2, panel-N
  Toggles:      tog-planes, tog-a, tog-b, tog-vec, tog-label

CSS class prefix:
  step-*    → tabs và panels bước học
  ib-*      → info box (ib-blue, ib-teal, ib-gold, ib-red)
  legend-*  → chú thích màu
  toggle-*  → toggle row
  ctrl-*    → controls section
  canvas-*  → canvas wrap và canvas-hint
  pt-label  → label tên điểm HTML overlay
  dist-label → label số đo khoảng cách/góc HTML overlay
```

### 4.2 (Nhánh B) Kho công cụ / Thư viện hình

```
File HTML:
  Kho_[TenNoiDung]_Toan3D.html
  Ví dụ: Kho_HinhHoc_KhongGian_Toan3D.html (= solid_library.html hiện tại)

JS object toàn cục (đặt tên CỐ ĐỊNH — mọi kho công cụ dùng đúng tên này để
05_threejs_engine.md áp dụng được nguyên vẹn, không cần đổi tên biến):
  SOLID_LIBRARY     → config đa diện (vertices/edges/faces/explore/baseVertices)
  ROUND_LIBRARY     → config khối tròn xoay (type/params)
  CATALOG           → nhóm khối theo chương SGK, cờ round: true
  solidRenderer     → instance SolidRenderer (đa diện)
  roundRenderer     → instance RoundSolidRenderer (tròn xoay)
  pointPool         → mảng điểm chung (đỉnh gốc + điểm cạnh/mặt/mặt cong)
  segments, heights, sections → mảng đoạn nối / đường cao / thiết diện đã tạo
  isRoundActive     → cờ boolean quyết định renderer nào đang active

Tên mode (string, dùng trong currentMode/setMode()) — cập nhật 07/2026,
đã bỏ 'explore' khỏi công cụ này (pattern vẫn còn ở 05_threejs_engine.md
PHẦN 7.4 cho công cụ khác), thêm 'section':
  'view' | 'point' | 'connect' | 'delete' | 'height' | 'section'

HTML element IDs — cập nhật 07/2026 (catalog đổi cấu trúc, xem 2.10):
  Catalog:      icon-rail, catalog-overlay, cat-search, cat-list
  Mode toolbar: mode-bar, mbtn-view, mbtn-point, mbtn-connect,
                mbtn-delete, mbtn-height, mbtn-section, mode-hint
  Toạ độ:       coord-toggle-btn
  Config:       sidebar, pts-section, khoi-hinh-body, khoi-hinh-chevron

CSS class prefix:
  rail-btn  → icon trong icon-rail (trái)
  cg-*      → catalog group (accordion nhóm khối, trong overlay)
  shape-btn → nút chọn khối trong catalog
  mode-btn  → nút trong mode toolbar
  s-section-head / s-chevron → header thu gọn/mở rộng (Khối hình, Điểm & Đoạn thẳng)
  pt-row / seg-item → dòng điểm/đoạn trong config sidebar (pt-row thay pt-item cũ)
  pt-name-input → ô đổi tên điểm inline
  pt-xyz / pt-xyz-edit → toạ độ chỉ đọc / sửa được
  formula-box → khối công thức thể tích-diện tích (chỉ chữ, không tính số)
  section-color → ô đổi màu thiết diện
  slider-row → dòng slider kích thước khối
```

---

## PHẦN 5 — GIỚI HẠN VÒNG LẶP

```
- Nếu sau 2 lần fix lỗi vẫn không đúng:
  AI dừng và hỏi lại 3 câu:
  1. "Bạn thấy gì trên màn hình?" (yêu cầu upload ảnh)
  2. "Bạn mong muốn nó trông như thế nào?"
  3. "Lỗi xảy ra khi làm thao tác gì?"

- Lỗi hay gặp trong Three.js (xem thêm PHỤ LỤC trong 05_threejs_engine.md):
  → Điểm kéo bị trôi xa: kiểm tra billboard drag-plane dùng camera.getWorldDirection()
  → Kéo điểm vô tình xoay camera: kiểm tra orbitControls.enabled = false/true
  → Label dính ngược: kiểm tra screenPos.z > 1 để ẩn
  → Nét đứt thành nét liền: kiểm tra computeLineDistances() sau khi tạo Line
  → Memory leak: kiểm tra dispose() trước khi rebuild mesh
  → Biến undefined: kiểm tra thứ tự khai báo bằng grep "^const \|^let "

- **Nhánh A:** mỗi phiên chỉ build 1 file HTML (1 bài học).
  Muốn làm bài khác → bắt đầu conversation mới.
- **Nhánh B:** kho công cụ là 1 file DUY NHẤT được MỞ RỘNG DẦN qua nhiều
  phiên (thêm khối mới, thêm mode mới) — không tạo file mới mỗi lần thêm
  tính năng. Luôn `node --check` sau mỗi lần chỉnh sửa lớn trước khi coi là
  xong, vì file càng lớn càng dễ vô tình xoá mất 1 dòng khai báo khi
  `str_replace` (đã xảy ra thật — xem `05_threejs_engine.md` Phụ lục).
```

---

> **Phiên bản:** 2.0
> **Tạo:** 06/2026 · **Cập nhật:** 07/2026 — tách 2 nhánh rõ ràng: Nhánh A
> (bài học SGK cụ thể, giữ nguyên toàn bộ flow Bước 0-6 gốc) và Nhánh B mới
> (kho công cụ/thư viện hình — BƯỚC -1 phân nhánh, PHẦN 0-B flow riêng gọn
> hơn, PHẦN 1.6 token catalog/mode-toolbar, PHẦN 2.10-2.13 component Nhánh B,
> PHẦN 3.7 bridge sang engine PHẦN 7-9, PHẦN 4.2 naming convention riêng).
> Lý do tách: `solid_library.html` (Kho Khối Hình Không Gian) đã chứng minh
> đây là loại sản phẩm hoàn toàn khác về UX (catalog + mode toolbar, không
> step-tabs/kết luận) — dùng chung 1 flow với Nhánh A sẽ ép sai khuôn.
> **Nguồn màu UI:** `song_song_khong_gian__1_.html` (đã verify)
> **Nguồn màu hình học:** rút ra từ các file test Three.js (test_drag_3d,
> test_parallel_construction, test_point_plane_distance, test_b_parallel,
> test_c_angles, test_d_distances) — bộ màu KHÔNG đổi giữa 2 nhánh.
> **Nguồn component Nhánh B:** `solid_library.html` (đã verify chạy, tương
> tác đầy đủ 6 mode, 11 khối đa diện + 3 khối tròn xoay)
> **Kế thừa:** skeleton Bước 0–7, typography, tokens từ `02_design_toan_2.md`
> **Dùng cùng:** `05_threejs_engine.md` (kỹ thuật Three.js, PHẦN 7-9 cho
> Nhánh B) + `06_geometry_math.md` (hàm toán thuần, cả 2 nhánh)

> **Phiên bản 2.1 — 08/2026:** thêm §2.9b (Resize LMS — khắc phục khoảng
> trắng thừa cuối trang khi nhúng file 3D lên LMS), đồng bộ với
> `02_design_toan_final.md` §7.2/§7.7/§7.8. Ghi chú thêm ở §2.9: không tự
> ép `.sidebar { height: 50% }` trên mobile — nguyên nhân sidebar bị chật
> gặp ở file build trước đó.
>
> ⚠️ **Chưa đồng bộ trong bản này (còn nợ, cần làm lượt sau):** §7.1
> (sandbox), §7.3-7.6 (Athena manifest đầy đủ — objectives/structure/
> athenaGuidance/progress/event/complete/state), và §7.9 (quy tắc đặt tên
> nhân vật "Athena", bỏ "robot") của `02_design_toan_final.md` — dòng "Kế
> thừa" ở trên trỏ vào `02_design_toan_2.md` (tên file cũ, trước khi 3 mục
> này được thêm vào doc 2D ở bản v2.2/v2.3.1) nên chưa có trong file 3D.
