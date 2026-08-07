# 🎨 DESIGN SYSTEM — Môn Toán (v2 — Aiducation Cream · Jade · Sage · Accent)

> **Mục đích:** Từ kịch bản đã duyệt → thiết kế → build HTML simulation Toán hoàn chỉnh  
> **Dùng kèm với:** `01_scenario_builder.md`  
> **Đặc thù môn:** Đồ thị 2D, tô miền, hàm số, hình học phẳng — không cần KaTeX
>
> **v2 — thay đổi so với bản trước:** không còn chọn giữa 5 preset màu, dùng **1 bộ nhận diện
> duy nhất** (Cream · Jade · Sage · Accent — PHẦN 1.1); font đổi sang **Be Vietnam Pro**; layout
> mặc định **không dùng sidebar trái cố định** (PHẦN 3.6), header banner nếu có phải **ẩn được**
> không xoá cứng; toàn bộ component chuẩn **mobile-first**, vùng chạm ≥44px.

---

## 🤖 HƯỚNG DẪN CHO AI — ĐỌC TRƯỚC KHI LÀM BẤT CỨ ĐIỀU GÌ

Khi người dùng nói bất kỳ điều nào sau:
- "Thiết kế" / "Design" / "Làm giao diện" / "Bắt đầu thiết kế"
- "Sang giai đoạn 2" / "Chuyển sang thiết kế"
- Hoặc bất kỳ ý định nào muốn thiết kế giao diện simulation Toán

**→ Lập tức chạy BƯỚC 0 bên dưới. Không tự build HTML khi chưa có xác nhận ở Bước 5.**

Trong suốt quá trình:
- Tuân thủ đúng thứ tự — **không bỏ bước, không gộp bước**
- Mỗi bước kết thúc bằng câu hỏi rõ ràng — **chờ giáo viên trả lời rồi mới đi tiếp**

---

## PHẦN 0 — CONVERSATION FLOW

---

### BƯỚC 0 — THU THẬP KỊCH BẢN

AI nói đúng đoạn này:

---
**Chào mừng đến Giai đoạn 2 — Thiết kế giao diện Toán! Để bắt đầu, mình cần:**

**📋 Kịch bản simulation đã duyệt**
Paste kịch bản vào đây hoặc upload file lên nhé.
*(Nếu vừa làm xong Giai đoạn 1 trong cùng conversation, gõ "Dùng kịch bản vừa xong" là được)*

---

> ⏳ **Chờ nhận kịch bản rồi mới đi tiếp.**

---

### BƯỚC 1 — XÁC NHẬN LAYOUT

> Từ v2, bảng màu đã cố định 1 bộ duy nhất (Cream · Jade · Sage · Accent — xem PHẦN 1.1),
> **không còn bước chọn preset màu**. AI chuyển thẳng sang xác nhận cấu trúc layout.

AI đưa ra đúng format này:

---
**Bước đầu tiên: xác nhận layout. Dựa trên kịch bản, mình đề xuất:**

| Layout | Dùng khi |
|---|---|
| **Đơn cuộn dọc** | 1 bài, không cần chuyển module/skin |
| **Tab ngang** (đầu trang, cuộn được) | Nhiều module/skin trong cùng 1 file — thay cho sidebar cố định cũ |
| **Sidebar điều khiển** (cột slider/checkbox) | Simulation cần nhiều tham số chỉnh cùng lúc — không phải menu điều hướng |

Layout đề xuất cho bài này: **[AI điền dựa trên kịch bản]**

**→ Bạn muốn:**
- ✅ **Dùng đề xuất** — tiếp tục
- ✏️ **Đổi layout khác** — nói layout bạn muốn
- 💬 **Thảo luận thêm**

---

> ⏳ **Chờ giáo viên xác nhận rồi mới đi tiếp.**
> Nếu có ảnh minh hoạ đặc trưng cho bài (vd nhân vật, bối cảnh câu chuyện) → hỏi thêm:
> *"Bạn có muốn thêm 1 header ảnh nền không? (tuỳ chọn, không bắt buộc — xem PHẦN 3.6)"*

---

### BƯỚC 2 — CHỐT TYPOGRAPHY & CỠ CHỮ

---
**Tiếp theo: typography. Đề xuất mặc định — bạn chỉnh nếu cần:**

**Font chữ:**
- Mặc định: **Be Vietnam Pro** (Google Fonts, tiếng Việt tốt, đồng bộ toàn hệ thống Aiducation)
- Thay thế: Inter / DM Sans / System UI (chỉ dùng khi có lý do đặc biệt)

**Thang cỡ chữ:**

| Vị trí | Cỡ | Weight | Ghi chú |
|---|---|---|---|
| Tiêu đề module H1 | 24px | 700 | Màu primary |
| Tiêu đề section | 17px | 700 | Uppercase + letter-spacing |
| Section label nhỏ | 12px | 700 | Uppercase, màu text-3 |
| Body text (nền tảng) | 18px | 400 | Màu text — dễ đọc trên mọi thiết bị |
| Mô tả / phụ | 15px | 400 | Màu text-3 |
| Nút | 14px | 600 | |
| Badge / chip | 12px | 700 | |
| Caption simulation | 15px | 400 | Italic khi là gợi ý |
| Số liệu & label trên canvas | 13px | 700 | **JetBrains Mono** — tabular-nums, không giật khi số đổi, hỗ trợ ký hiệu toán/mũ/subscript |
| Tooltip | 13px | 400 | Nền tối, chữ trắng |

**→ Bạn muốn:**
- ✅ **Dùng mặc định** — tiếp tục
- ✏️ **Chỉnh** — nói mục nào muốn to/nhỏ hơn
- 💬 **Thảo luận** — điều chỉnh hệ thống font

---

> ⏳ **Chờ xác nhận rồi mới đi tiếp.**

---

### BƯỚC 3 — CHỐT TƯƠNG TÁC & HÀNH VI

AI chỉ hiện các tương tác **phù hợp với kịch bản nhận ở Bước 0**:

---
**Chốt tương tác. Tick những cái cần, hoặc 💬 Thảo luận để mô tả kỹ hơn:**

**🖱️ Input & chuột:**
- [ ] A1 — Nhập phương trình / bất phương trình vào ô text, đồ thị cập nhật ngay
- [ ] A2 — Kéo slider thay đổi tham số (hệ số a, b, c; bán kính; góc...)
- [ ] A3 — Click chọn điểm trên đồ thị
- [ ] A4 — Hover hiện tooltip tọa độ (x, y) + trạng thái thuộc miền/đường nào
- [ ] A5 — Scroll chuột để zoom in/out đồ thị
- [ ] A6 — Shift + kéo để pan đồ thị

**▶️ Animation & bước:**
- [ ] B1 — Play/Pause animation (vẽ đường, tô miền từng bước)
- [ ] B2 — Step từng bước một (dùng cho sim quy trình)
- [ ] B3 — Slider tốc độ animation
- [ ] B4 — Reset về trạng thái ban đầu

**👁️ Hiển thị / ẩn:**
- [ ] C1 — Bật/tắt từng đối tượng (đường thẳng, miền, điểm, nhãn...)
- [ ] C2 — Toggle chế độ xem (ví dụ: riêng lẻ / giao thoa hệ BPT)
- [ ] C3 — Tab chuyển giữa các chế độ trong 1 simulation

**✅ Kiểm tra & phản hồi:**
- [ ] D1 — Panel nhập điểm (x, y) để kiểm tra thuộc miền / thỏa BPT không
- [ ] D2 — Highlight tự động điểm đúng/sai trên canvas
- [ ] D3 — Caption thay đổi theo từng trạng thái tương tác

**📐 Đặc thù Toán (chỉ hiện nếu phù hợp kịch bản):**
- [ ] E1 — Vẽ đường biên nét liền (≤ ≥) hoặc nét đứt (< >) tự động theo dấu
- [ ] E2 — Tô miền nghiệm với màu phân biệt từng BPT
- [ ] E3 — Hiển thị nhãn phương trình trực tiếp trên đường trong đồ thị
- [ ] E4 — Chấm và label điểm đặc biệt (giao điểm, đỉnh parabol, điểm test...)
- [ ] E5 — Panel so sánh 2 trường hợp cạnh nhau (đúng vs sai)

**→ Tick các mục, hoặc 💬 Thảo luận để mô tả tương tác cụ thể hơn.**

---

> ⏳ **Chờ giáo viên chọn rồi mới đi tiếp.**
> Nếu 💬 Thảo luận: thảo luận xong hỏi: *"Mình tóm tắt lại các tương tác đã chốt — bạn xác nhận tiếp tục nhé?"*

---

### BƯỚC 4 — CHỐT LAYOUT & CẤU TRÚC HTML

AI đề xuất layout dựa trên kịch bản + tương tác đã chốt:

---
**Dựa trên kịch bản và tương tác đã chốt, mình đề xuất cấu trúc:**

```
Layout: [Đơn cuộn dọc / Tab ngang (nhiều module) / + Sidebar điều khiển nếu cần nhiều tham số]
Lý do: [...]

┌─ Header (tuỳ chọn, PHẢI ẩn được bằng display:none, không bắt buộc có) ─┐
│ Icon + Tiêu đề bài + Mô tả ngắn                                        │
└─────────────────────────────────────────────────────────────────────┘

[Nếu nhiều module — Tab ngang thay cho sidebar cố định cũ]:
┌─ Topbar sticky: logo + tab cuộn ngang (Module 1 ● / Module 2 / Module 3) ─┐
└────────────────────────────────────────────────────────────────────────┘
┌─ Main (max 860px, margin auto) ───────────┐
│ mod-header                                 │
│ [sdiv] Tên section                         │
│ sim-wrap                                   │
│   sim-toolbar                              │
│   canvas-wrap + tooltip                    │
│   disp-row (số liệu)                       │
│   sim-caption                              │
│   sim-controls                             │
│ info-box (nếu có)                          │
└─────────────────────────────────────────────┘

[Nếu Đơn]:
Max-width 860px, margin auto, padding 2rem desktop → 1rem mobile
mod-header → sim-wrap → info-box

[Nếu cần Sidebar điều khiển — cột slider/checkbox thông số]:
.workspace { grid-template-columns: 3.5fr 6.5fr }
→ Dưới 1024px: xếp dọc, canvas/kết quả hiện TRƯỚC, slider xuống SAU (dùng CSS order,
  xem PHẦN 3.6) — đây KHÔNG phải sidebar điều hướng, không xoá khi nhúng platform khác.
```

**Ghi chú bắt buộc (v2):** mọi layout build ra đều phải mobile-first — vùng chạm ≥44px, không
tràn ngang ở 375px, xem checklist responsive ở PHẦN 3.6 cuối.

**Sim-wrap chi tiết theo kịch bản:**
```
[AI điền cụ thể theo kịch bản đã nhận]
```

**→ Bạn muốn:**
- ✅ **Duyệt** — tiếp tục sang Bước 5
- ✏️ **Chỉnh** — nói phần nào cần thay đổi
- 💬 **Thảo luận** — giải thích thêm

---

> ⏳ **Chờ phản hồi rồi mới đi tiếp.**

---

### BƯỚC 5 — XÁC NHẬN TOÀN BỘ TRƯỚC KHI BUILD

---
**Tóm tắt toàn bộ trước khi build:**

```
📋 Kịch bản:      [tên bài, số module]
🎨 Bộ nhận diện:  Aiducation Cream · Jade · Sage · Accent (cố định — PHẦN 1.1, không chọn preset)
🔤 Font:          Be Vietnam Pro
📐 Layout:        [Đơn cuộn dọc / Tab ngang / + Sidebar điều khiển]
🖱️ Tương tác:    [A1, C1, D1, E1, E2...]
📐 Đặc thù Toán: [liệt kê E nào đã chọn]
📱 Mobile:        vùng chạm ≥44px, canvas aspect-ratio, test ở 375/768/1280px
🔌 LMS:           instrumentation + Athena manifest theo PHẦN 7 (bắt buộc)
✨ Ghi chú:       [nếu có]
```

**→ Xác nhận build HTML không?**
- ✅ **Có, build ngay**
- ✏️ **Khoan, mình muốn chỉnh [phần X]**

---

> ⏳ **Chỉ build khi có xác nhận "Có". Tuyệt đối không tự build.**

---

### BƯỚC 6 — BUILD HTML

Chỉ chạy sau khi có xác nhận ở Bước 5. Build theo chuẩn kỹ thuật ở PHẦN 2 bên dưới,
**và bắt buộc tích hợp LMS/Athena manifest theo PHẦN 7** ngay trong lần build đầu tiên
(không phải bước riêng sau này) — file giao cho giáo viên phải sẵn sàng nhúng vào LMS.

Sau khi build xong:

---
**File đã sẵn sàng! Bạn muốn:**
- ✅ **Duyệt** — hoàn thành Giai đoạn 2
- 🐛 **Báo lỗi** — mô tả lỗi hoặc upload ảnh chụp màn hình
- ✏️ **Chỉnh giao diện** — nói rõ phần nào muốn thay đổi
- 📖 **Viết hướng dẫn** — sinh guide text cho simulation này

---

---

### BƯỚC 7 — SINH GUIDE TEXT (chỉ chạy khi giáo viên chọn "Viết hướng dẫn")

AI sinh guide text theo template sau, **output dạng text thuần — không cài vào HTML**:

---
**Dưới đây là hướng dẫn sử dụng simulation "[Tên bài]":**

```
🎯 MỤC TIÊU
[1-2 câu — học sinh sẽ hiểu/làm được gì sau khi dùng simulation này]

📋 CÁC BƯỚC THỰC HIỆN

Bước 1 — [Tên bước]
[Mô tả ngắn hành động: học sinh cần làm gì, bấm/nhập/kéo gì]
→ Quan sát: [thấy gì xảy ra trên màn hình]

Bước 2 — [Tên bước]
[Mô tả ngắn]
→ Quan sát: [...]

Bước 3 — [Tên bước]
[Mô tả ngắn]
→ Quan sát: [...]

[Thêm bước nếu cần — thường 3-5 bước là đủ]

💡 LƯU Ý
• [Sai lầm phổ biến 1 — nhắc học sinh chú ý điều gì]
• [Sai lầm phổ biến 2]
• [Tip nhỏ nếu có]

✅ KẾT LUẬN
[1 câu tóm tắt điều học sinh rút ra được]
```

---

Sau khi xuất guide text:

---
**Guide text đã sẵn sàng! Bạn muốn:**
- ✅ **Duyệt nguyên** — lưu lại để dùng sau
- ✏️ **Chỉnh nội dung** — nói rõ bước nào cần sửa
- 🔧 **Cài vào HTML** — mình chèn vào ngay dưới tiêu đề simulation (dạng `.info-panel` 2 cột — xem PHẦN 3.6, hoặc `info-box ib-blue` nếu đơn giản hơn)

---

> ⏳ **Chờ giáo viên phản hồi. Chỉ cài vào HTML khi được yêu cầu rõ ràng.**

## PHẦN 1 — DESIGN TOKENS

### 1.1 Bộ màu chuẩn (v2 — thay thế toàn bộ hệ thống 5 preset cũ)

> Không còn chọn preset theo bài. **Mọi file dùng chung 1 bộ token này.** Dán nguyên khối vào `:root`:

```css
:root {
  /* Neutrals · giấy & mực */
  --cream:#FAF7F0; --cream-2:#F0EADD; --cream-3:#E7DECC;
  --paper-line:#E5DECF; --paper-line-2:#D6CCB6;
  --ink:#1A1A1A; --ink-2:#514C44; --ink-3:#7C756A; --ink-faint:#ABA396;

  /* Jade · hành động chính */
  --jade:#3CA57A; --jade-deep:#2D8B6F; --jade-dark:#14432F;
  --jade-text:#1B5E48; --jade-soft:#A9D0BE; --jade-pale:#DCEAE1;

  /* Sage · phụ trợ */
  --sage:#A8C9B8; --sage-deep:#7CA792; --sage-text:#46685A; --sage-pale:#E1ECE4;

  /* Accent · điểm nhấn ấm */
  --accent:#E8A24A; --accent-deep:#CE8A33; --accent-text:#8A551A; --accent-pale:#F7E7CD;

  /* Semantic · phản hồi đúng/sai/cảnh báo/info */
  --correct:#2D8B6F; --correct-bg:#DCEAE1;
  --wrong:#C15F3C;   --wrong-bg:#F3E2D6;
  --warning:#C58A2E; --warning-bg:#F5E7CB;
  --info:#4E7F92;    --info-bg:#DCE7EB;

  /* Illustration only · fill phẳng cho minh hoạ (KHÔNG dùng cho UI/text) */
  --il-terracotta:#C1704B; --il-brick:#9E4A2E; --il-ochre:#C99A3C; --il-olive:#8A9A5B;
  --il-forest:#2E6B52; --il-dusty-blue:#6E93A6; --il-slate:#4E6E7E; --il-mauve:#8A6A7E; --il-sand:#D8C4A0;

  --white:#FFFFFF;
  --radius:        10px;
  --radius-lg:     14px;
  --radius-sm:     6px;
  --shadow: 0 4px 12px rgba(45, 139, 111, 0.10);
  --shadow-sm: 0 2px 6px rgba(26, 26, 26, 0.05);
}
```

> **Không dùng alias/tên biến kiểu cũ** (`--primary`, `--bg`, `--surface`, `--text`, `--green`...) —
> luôn viết thẳng tên token ở trên (`--jade-deep`, `--cream`, `--white`, `--ink`, `--correct`...).
> Kỹ thuật alias (trỏ tên cũ sang token mới) chỉ dùng khi **redesign file cũ đã có sẵn hàng trăm
> chỗ `var(--jade-deep)`** — xem `AIDUCATION_UI_REDESIGN_PLAYBOOK.md` — không áp dụng khi xây file mới.

**Bảng hex tra nhanh cho canvas** (dùng khi phải viết thẳng chuỗi hex trong `ctx.fillStyle`,
vì canvas không đọc được CSS variable):

| Vai trò | Token | Hex |
|---|---|---|
| primary / primary-mid | `--jade-deep` / `--jade` | `#2D8B6F` / `#3CA57A` |
| primary-light (nền nhạt) | `--jade-pale` | `#DCEAE1` |
| accent | `--accent` | `#E8A24A` |
| accent đậm | `--accent-deep` | `#CE8A33` |
| bg / cream | `--cream` | `#FAF7F0` |
| border | `--paper-line` | `#E5DECF` |
| text chính | `--ink` | `#1A1A1A` |
| green (đúng) | `--correct` | `#2D8B6F` |
| red (sai) | `--wrong` | `#C15F3C` |
| amber (cảnh báo) | `--warning` | `#C58A2E` |
| blue (info) | `--info` | `#4E7F92` |

**Vector màu cho canvas Vật lý (cộng lực, cộng vận tốc...):**
```css
--color-v1: var(--jade);            /* vector thành phần 1 */
--color-v2: var(--info);            /* vector thành phần 2 */
--color-resultant: var(--accent);   /* vector tổng/hợp lực */
--color-force-red: var(--wrong);    /* lực cản, ma sát, cảnh báo */
--color-gravity: var(--ink-3);      /* trọng lực trung tính */
```

**Palette đồ thị Toán — màu cho từng đường/miền:**
```css
/* Dùng theo thứ tự này khi có nhiều đối tượng */
--plot-1: var(--wrong);       /* Cam đất — đường/miền 1 */
--plot-2: var(--info);        /* Xanh xám ấm — đường/miền 2 */
--plot-3: var(--jade-deep);   /* Xanh lá — đường/miền 3 */
--plot-4: var(--sage-text);   /* Xanh rêu đậm — đường/miền 4 */
--plot-5: var(--il-mauve);    /* Mận nhạt — đường/miền 5 */
--plot-inter: var(--accent-deep); /* Cam đậm — vùng giao thoa hệ BPT */

/* Fill (tô miền) = màu đường với alpha thấp */
/* plot-1 fill: rgba(193,95,60, 0.15) */
/* plot-2 fill: rgba(78,127,146, 0.15) */
/* Giao thoa fill: rgba(206,138,51, 0.55) */
```

### 1.2 Typography

```css
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@500;700&family=Be+Vietnam+Pro:ital,wght@0,400;0,500;0,600;0,700;0,800;1,400&display=swap');

body {
  font-family: 'Be Vietnam Pro', system-ui, sans-serif;
  font-size: 18px;   /* tăng từ 15px — dễ đọc hơn trên mọi thiết bị, đặc biệt mobile */
  line-height: 1.7;
  color: var(--ink);
  background: var(--cream);
}

/* Thang cỡ chữ chuẩn */
/* H1 module:        24px / 700 / --ink */
/* Section label:    12px / 700 / uppercase / letter-spacing .06em / --ink-3 */
/* Body:             18px / 400 / --ink (nền tảng — xem body ở trên) */
/* Body phụ:         15px / 400 / --ink-3 */
/* Nút:              14px / 600 */
/* Badge:            12px / 700 */
/* Caption sim:      15px / 400, italic khi gợi ý */
/* Số liệu/label canvas: 13px / 700 / JetBrains Mono — LUÔN dùng cho số liệu động + công thức */
/* Tooltip:          13px / 400 / màu trắng trên nền tối */
```

**Số liệu động & nhãn trên canvas — luôn dùng JetBrains Mono, KHÔNG dùng Be Vietnam Pro:**

Số liệu đổi mỗi frame (kết quả tính toán, toạ độ...) và nhãn vẽ bằng `ctx.fillText` dùng font phụ
**JetBrains Mono** (monospace, hỗ trợ tiếng Việt, tải qua Google Fonts nên hiển thị đồng nhất trên mọi
thiết bị — khác với `Courier New` là font hệ điều hành, có thể thiếu trên 1 số máy/trình duyệt và bị
thay thế âm thầm bằng font khác). So với Inconsolata, JetBrains Mono có bộ ký hiệu toán/khoa học
rộng hơn (số mũ/subscript sẵn có, ký tự Hy Lạp, toán tử ≈ ≤ ≥) — phù hợp hơn cho công thức Toán/
Lý/Hoá trên canvas — đổi lại chữ hơi rộng hơn nên cần theo dõi độ dài label không bị tràn khung.
`font-variant-numeric: tabular-nums` giữ độ rộng số cố định, không giật layout khi giá trị thay đổi
liên tục:

```css
.disp-val, .canvas-label {
  font-family: 'JetBrains Mono', 'Courier New', monospace;
  font-variant-numeric: tabular-nums;
}
```

Trong canvas: `ctx.font = "bold 13px 'JetBrains Mono', monospace"` cho mọi label số liệu/công thức.


### 1.3 Ký hiệu Toán — Quy tắc render

```
Toán THPT không cần KaTeX. Dùng Unicode + HTML thuần là đủ.

Ký hiệu hay dùng:
  ≤ ≥ < > ≠ ≈         → Unicode trực tiếp
  ∈ ∉ ∩ ∪ ⊂ ⊃         → Unicode trực tiếp
  ∞ → ← ⇒ ⇔           → Unicode trực tiếp
  x² x³ xⁿ            → <sup>2</sup> trong HTML
                         hoặc "x²" Unicode trong canvas
  x₀ x₁ y₀            → <sub>0</sub> trong HTML
                         hoặc "x₀" Unicode trong canvas
  √ ∫ Δ Σ π            → Unicode trực tiếp
  · × ÷ ± ½           → Unicode trực tiếp

Quy tắc bắt buộc:
  1. Trong canvas (ctx.fillText): LUÔN dùng Unicode — không dùng HTML/KaTeX
  2. Trong sidebar/caption/HTML: dùng <sup><sub> hoặc Unicode đều được
  3. KHÔNG load MathJax hay KaTeX cho simulation Toán THPT — không cần thiết
  4. Công thức dài trong canvas: xuống dòng hoặc rút gọn, không để tràn
```

### 1.4 Icon Library

```html
<!-- Luôn dùng Tabler Icons — không dùng emoji thay thế cho icon chức năng -->
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@tabler/icons-webfont@3.19.0/dist/tabler-icons.min.css">

<!-- Hay dùng trong Toán: -->
<!-- ti-refresh      → Reset -->
<!-- ti-play         → Play -->
<!-- ti-player-pause → Pause -->
<!-- ti-chevron-left/right → Bước trước/sau -->
<!-- ti-eye / ti-eye-off   → Hiện/ẩn đối tượng -->
<!-- ti-info-circle  → Caption info -->
<!-- ti-check        → Đúng -->
<!-- ti-x            → Sai -->
<!-- ti-zoom-in/out  → Zoom -->
```

---

## PHẦN 2 — CHUẨN KỸ THUẬT TOÁN

### 2.1 Canvas — Tách CSS pixel và Physical pixel (BẮT BUỘC)

```javascript
// ĐÂY LÀ LỖI PHỔ BIẾN NHẤT — tách rõ 2 hệ tọa độ
let CW = 0, CH = 0;   // CSS pixels  — dùng cho mouse, math mapping
let PW = 0, PH = 0;   // Physical px — dùng cho canvas.width và ImageData

function resizeCanvas() {
  const rect = wrapper.getBoundingClientRect();
  CW = rect.width;
  CH = rect.height;
  const dpr = window.devicePixelRatio || 1;
  PW = Math.round(CW * dpr);
  PH = Math.round(CH * dpr);
  canvas.width  = PW;
  canvas.height = PH;
  fullDraw();
}

// Debounce ResizeObserver — tránh lỗi "ResizeObserver loop"
let roTimer = null;
const ro = new ResizeObserver(() => {
  clearTimeout(roTimer);
  roTimer = setTimeout(resizeCanvas, 30);
});
ro.observe(wrapper);

// Khi vẽ VECTOR (đường, chữ, shapes):
//   ctx.setTransform(dpr, 0, 0, dpr, 0, 0)  ← scale 1 lần
//   rồi dùng CW, CH cho tọa độ

// Khi dùng ImageData (tô miền pixel-by-pixel):
//   Tạo ImageData theo PW × PH (physical)
//   putImageData(imgData, 0, 0)  ← TRƯỚC khi setTransform
//   ctx.setTransform(dpr, 0, 0, dpr, 0, 0)  ← SAU putImageData
//   Rồi vẽ vector lên trên
```

### 2.2 Hệ tọa độ Math ↔ Canvas

```javascript
// Viewport toán học — có thể thay đổi khi zoom/pan
let vXMin = -10, vXMax = 10;
let vYMin = -10, vYMax = 10;

// Math → CSS pixel
function m2c(mx, my) {
  return {
    px: (mx - vXMin) / (vXMax - vXMin) * CW,
    py: (1 - (my - vYMin) / (vYMax - vYMin)) * CH
  };
}

// CSS pixel → Math (dùng cho mouse events)
function c2m(px, py) {
  return {
    x: vXMin + px / CW * (vXMax - vXMin),
    y: vYMin + (1 - py / CH) * (vYMax - vYMin)
  };
}

// Zoom về tâm điểm chuột
function zoomAt(cx, cy, factor) {
  const { x: mx, y: my } = c2m(cx, cy);
  vXMin = mx + (vXMin - mx) * factor;
  vXMax = mx + (vXMax - mx) * factor;
  vYMin = my + (vYMin - my) * factor;
  vYMax = my + (vYMax - my) * factor;
  fullDraw();
}
```

### 2.3 Vẽ lưới và trục tọa độ chuẩn

```javascript
function drawGrid() {
  const dpr = window.devicePixelRatio || 1;
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

  const xRange = vXMax - vXMin;
  // Chọn bước lưới tự động
  let step = 1;
  if (xRange > 40) step = 5;
  if (xRange > 100) step = 10;
  if (xRange < 4) step = 0.5;

  // Lưới mờ
  ctx.strokeStyle = 'rgba(0,0,0,0.07)';
  ctx.lineWidth = 1;
  for (let x = Math.ceil(vXMin/step)*step; x <= vXMax; x += step) {
    const { px } = m2c(x, 0);
    ctx.beginPath(); ctx.moveTo(px, 0); ctx.lineTo(px, CH); ctx.stroke();
  }
  for (let y = Math.ceil(vYMin/step)*step; y <= vYMax; y += step) {
    const { py } = m2c(0, y);
    ctx.beginPath(); ctx.moveTo(0, py); ctx.lineTo(CW, py); ctx.stroke();
  }

  // Trục chính
  ctx.strokeStyle = 'rgba(0,0,0,0.5)';
  ctx.lineWidth = 1.5;
  const { px: x0, py: y0 } = m2c(0, 0);
  if (x0 >= 0 && x0 <= CW) {
    ctx.beginPath(); ctx.moveTo(x0, 0); ctx.lineTo(x0, CH); ctx.stroke();
  }
  if (y0 >= 0 && y0 <= CH) {
    ctx.beginPath(); ctx.moveTo(0, y0); ctx.lineTo(CW, y0); ctx.stroke();
  }

  // Nhãn ticks + O + mũi tên trục (xem component drawAxis bên dưới)
}
```

### 2.4 Vẽ đường biên BPT — Nét liền vs Nét đứt

```javascript
// Nét đứt cho < và >, nét liền cho ≤ và ≥
function drawBoundary(parsedBPT, color) {
  const isDashed = parsedBPT.op === '<' || parsedBPT.op === '>';
  ctx.strokeStyle = color;
  ctx.lineWidth = 2.2;
  ctx.setLineDash(isDashed ? [7, 5] : []);

  // Vẽ đường...

  ctx.setLineDash([]); // Reset sau khi vẽ xong
}
```

### 2.5 Tô miền nghiệm — Pixel Shading

```javascript
// Dùng cho BPT và hệ BPT — tô từng pixel theo điều kiện toán học
function shadeRegions(activeBPTs, mode) {
  // Tạo ImageData theo PHYSICAL pixels
  const imgData = ctx.createImageData(PW, PH);
  const data = imgData.data;
  const xRange = vXMax - vXMin;
  const yRange = vYMax - vYMin;

  for (let py = 0; py < PH; py++) {
    // Physical pixel → Math y
    const my = vYMin + (1 - py / PH) * yRange;
    for (let px = 0; px < PW; px++) {
      // Physical pixel → Math x
      const mx = vXMin + (px / PW) * xRange;
      const idx = (py * PW + px) * 4;

      // Tính màu theo mode
      let r = 250, g = 247, b = 240, a = 0; // nền mặc định = --cream (v2)

      if (mode === 'intersection') {
        const allTrue = activeBPTs.every(bpt => bpt.fn(mx, my));
        if (allTrue) { r=206; g=138; b=51; a=210; } // --plot-inter (accent-deep)
      } else {
        // Individual: blend màu của các BPT thỏa mãn
        let tr=0, tg=0, tb=0, cnt=0;
        activeBPTs.forEach(bpt => {
          if (bpt.fn(mx, my)) {
            tr += bpt.fillRGB[0]; tg += bpt.fillRGB[1]; tb += bpt.fillRGB[2];
            cnt++;
          }
        });
        if (cnt > 0) { r=tr/cnt; g=tg/cnt; b=tb/cnt; a = cnt===1?90:160; }
      }

      if (a > 0) {
        const an = a / 255;
        data[idx]   = Math.round(r*an + 250*(1-an));
        data[idx+1] = Math.round(g*an + 247*(1-an));
        data[idx+2] = Math.round(b*an + 240*(1-an));
        data[idx+3] = 255;
      } else {
        data[idx]=250; data[idx+1]=247; data[idx+2]=240; data[idx+3]=255;
      }
    }
  }

  // putImageData TRƯỚC setTransform
  ctx.setTransform(1, 0, 0, 1, 0, 0);
  ctx.putImageData(imgData, 0, 0);
  // Sau đó vẽ vector
  const dpr = window.devicePixelRatio || 1;
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);
}
```

### 2.6 Label nhãn trên đường — Không che đồ thị

```javascript
// Tự động chọn vị trí label không đè lên đường và không tràn ra ngoài canvas
function drawLineLabel(label, color, bndFn) {
  ctx.font = "bold 13px 'JetBrains Mono', monospace"; // JetBrains Mono cho công thức/số liệu
  const tw = ctx.measureText(label).width;
  const PAD = 6, H = 20;

  // Scan 25%-75% viewport, chọn điểm gần giữa màn hình nhất
  let bestX = null, bestY = null, bestDist = Infinity;
  for (let i = 0; i <= 60; i++) {
    const mx = vXMin + (0.25 + i/60 * 0.5) * (vXMax - vXMin);
    let my; try { my = bndFn(mx); } catch { continue; }
    if (!isFinite(my) || my < vYMin || my > vYMax) continue;
    const { px, py } = m2c(mx, my);
    const dist = Math.abs(py - CH/2);
    if (dist < bestDist) { bestDist=dist; bestX=px; bestY=py; }
  }
  if (bestX === null) return;

  // Đặt label bên phải, nếu tràn thì bên trái
  let lx = bestX + 16;
  if (lx + tw + PAD*2 > CW - 8) lx = bestX - tw - PAD*2 - 10;
  let ly = bestY - H - 8;
  if (ly < 8) ly = bestY + 10;

  // Box nền trắng mờ + viền màu đường
  ctx.fillStyle = 'rgba(255,255,255,0.93)';
  ctx.strokeStyle = color;
  ctx.lineWidth = 1.5;
  ctx.setLineDash([]);
  ctx.beginPath();
  ctx.roundRect(lx - PAD, ly, tw + PAD*2, H, 4);
  ctx.fill(); ctx.stroke();

  // Text
  ctx.fillStyle = color;
  ctx.textAlign = 'left';
  ctx.textBaseline = 'middle';
  ctx.fillText(label, lx, ly + H/2);
}
```

### 2.7 Cấu trúc code JS chuẩn

```javascript
// ─── 1. CONSTANTS & PALETTE ───────────────────────
// ─── 2. STATE ─────────────────────────────────────
//     viewport: vXMin, vXMax, vYMin, vYMax
//     data: bpts[], points[], etc.
//     ui: mode, activeTab, etc.
// ─── 3. CANVAS SETUP & RESIZE ─────────────────────
//     resizeCanvas() + ResizeObserver debounced
// ─── 4. COORD HELPERS ─────────────────────────────
//     m2c(mx,my) → {px,py}
//     c2m(px,py) → {x,y}
//     zoomAt(cx,cy,factor)
// ─── 5. PARSE ─────────────────────────────────────
//     parseBPT(str) → {fn, op, boundLabel, bndFn}
// ─── 6. DRAW ──────────────────────────────────────
//     fullDraw()
//       shadeRegions()      ← ImageData, chạy trước
//       drawGrid()          ← vector, chạy sau
//       drawBoundaries()
//       drawPoints()
//       drawLabels()
// ─── 7. EVENT HANDLERS ────────────────────────────
//     wheel (zoom)
//     mousedown/move/up (pan)
//     input handlers
//     button handlers
// ─── 8. INIT ──────────────────────────────────────
//     addDefaultExamples()
//     resizeCanvas()
```

### 2.8 Checklist sau khi build

**Chức năng:**
- [ ] Tất cả nút hoạt động đúng
- [ ] Reset về đúng trạng thái ban đầu
- [ ] Caption / data display cập nhật theo trạng thái
- [ ] Không có lỗi console

**Canvas & đồ thị:**
- [ ] Miền nghiệm và đường biên khớp chính xác (không lệch)
- [ ] Nét đứt đúng cho `<` và `>`, nét liền cho `≤` và `≥`
- [ ] Label đường không chồng lên đường, không tràn ra ngoài canvas
- [ ] Tooltip tọa độ hiện đúng vị trí chuột
- [ ] Zoom scroll và pan Shift+kéo hoạt động
- [ ] Canvas không vỡ khi resize cửa sổ
- [ ] Không có lỗi ResizeObserver loop

**Sư phạm:**
- [ ] Mỗi sai lầm trong kịch bản có phản hồi rõ ràng
- [ ] Học sinh biết phải làm gì tiếp theo (caption đủ rõ)
- [ ] Không có thông tin thừa làm rối

---

## PHẦN 3 — COMPONENT LIBRARY

### 3.1 Sim Wrapper — Template đầy đủ (v2.2 Cập nhật)

```html
<div class="sim-wrap">
  <!-- Toolbar: tên + nút chuyển chế độ -->
  <div class="sim-toolbar">
    <span class="sim-toolbar-label">ĐỒ THỊ</span>
    <button class="sim-btn active" onclick="setMode('individual')">Riêng lẻ</button>
    <button class="sim-btn" onclick="setMode('intersection')">Hệ BPT</button>
    <button class="sim-btn" id="guide-btn-m1" onclick="toggleGuide('m1')">
      <i class="ti ti-book"></i> Hướng dẫn
    </button>
  </div>

  <!-- Canvas Container với Zoom Controls dọc & Tọa độ nổi tích hợp -->
  <div class="sim-canvas-wrap" id="canvasWrap">
    <canvas id="simCanvas"></canvas>
    <div class="tooltip-box" id="tooltip"></div>
    
    <!-- 1. Thanh Zoom dọc chìm mờ ở góc trên bên phải canvas -->
    <div class="canvas-zoom-controls">
      <button class="btn-canvas-zoom" onclick="doZoom(0.7)" title="Phóng to"><i class="ti ti-plus"></i></button>
      <button class="btn-canvas-zoom" onclick="doZoom(1.4)" title="Thu nhỏ"><i class="ti ti-minus"></i></button>
      <button class="btn-canvas-zoom" onclick="resetView()" title="Đặt lại"><i class="ti ti-refresh"></i></button>
    </div>

    <!-- 2. Thẻ tọa độ nổi mờ chìm sát góc dưới bên phải canvas (pointer-events: none) -->
    <div class="coord-bar" id="coordBar">x: 0.00 · y: 0.00</div>
  </div>

  <!-- Nút hành động chính (nằm ngay dưới Canvas trên Mobile & PC) -->
  <button class="btn-primary btn-draw-boundary" id="btnAction">
    <i class="ti ti-pencil"></i> Vẽ đường biên
  </button>

  <!-- Caption hướng dẫn -->
  <div class="sim-caption">
    <i class="ti ti-info-circle"></i>
    <span id="caption-m1">Nhập bất phương trình để bắt đầu...</span>
  </div>
</div>
```

```css
/* CSS chuẩn cho Thanh Zoom dọc & Thẻ Tọa độ nổi tích hợp trong Canvas Wrapper */
.canvas-zoom-controls {
  position: absolute; top: 12px; right: 12px; z-index: 15;
  display: flex; flex-direction: column;
  background: rgba(250, 247, 240, 0.55); backdrop-filter: blur(6px); -webkit-backdrop-filter: blur(6px);
  border: 1px solid rgba(229, 222, 207, 0.6); border-radius: var(--radius);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.04); overflow: hidden; opacity: 0.8;
  transition: opacity 0.2s ease, background 0.2s ease;
}
.canvas-zoom-controls:hover { opacity: 1; background: rgba(255, 255, 255, 0.92); }

.btn-canvas-zoom {
  width: 36px; height: 36px; padding: 0; background: transparent; border: none;
  font-size: 16px; font-weight: 600; cursor: pointer; color: var(--ink-2);
  display: flex; align-items: center; justify-content: center; transition: background .2s, color .2s;
}
.btn-canvas-zoom:not(:last-child) { border-bottom: 1px solid rgba(229, 222, 207, 0.6); }
.btn-canvas-zoom:hover { background: var(--jade-pale); color: var(--jade-deep); }

.coord-bar {
  position: absolute; bottom: 4px; right: 4px; z-index: 12;
  font-size: 11px; font-weight: 500; color: var(--ink-3); font-family: var(--font-mono);
  font-variant-numeric: tabular-nums; background: rgba(250, 247, 240, 0.5);
  backdrop-filter: blur(4px); -webkit-backdrop-filter: blur(4px);
  padding: 2px 6px; border-radius: 4px; border: 1px solid rgba(229, 222, 207, 0.5);
  opacity: 0.8; pointer-events: none;
}
.hint-text:empty { display: none; } /* Ẩn khoảng trắng rỗng khi chưa có thông báo */
```

```javascript
/* JS chuẩn cho tính năng Lăn chuột Zoom (Mouse Wheel Zoom) trên Canvas */
function setupWheel(canvas, getCW, getCH) {
  canvas.addEventListener('wheel', e => {
    e.preventDefault();
    const rect = canvas.getBoundingClientRect();
    const factor = e.deltaY > 0 ? 1.15 : 0.87;
    const cx = e.clientX - rect.left, cy = e.clientY - rect.top;
    const CW = getCW(), CH = getCH();
    if (CW === 0 || CH === 0) return;
    const { x: mx, y: my } = c2m(cx, cy, CW, CH);
    const xRange = vXMax - vXMin, yRange = vYMax - vYMin;
    const newXR = xRange * factor, newYR = yRange * factor;
    if (newXR < 2 || newXR > 50000) return;
    const pctX = cx / CW, pctY = 1 - cy / CH;
    vXMin = mx - pctX * newXR; vXMax = vXMin + newXR;
    vYMin = my - pctY * newYR; vYMax = vYMin + newYR;
    fullRedraw();
  }, { passive: false });
}

/* JS chuẩn cho tính năng Kéo di chuyển (Pan Dragging) bằng chuột & cảm ứng */
let isPanning = false, startPX = 0, startPY = 0;
let startXMin = 0, startXMax = 0, startYMin = 0, startYMax = 0;

function setupPan(canvas, getCW, getCH) {
  canvas.addEventListener('mousedown', e => {
    isPanning = true;
    startPX = e.clientX; startPY = e.clientY;
    startXMin = vXMin; startXMax = vXMax; startYMin = vYMin; startYMax = vYMax;
    canvas.style.cursor = 'grabbing';
  });

  canvas.addEventListener('mousemove', e => {
    if (!isPanning) return;
    const CW = getCW(), CH = getCH(); if (!CW || !CH) return;
    const dx = e.clientX - startPX, dy = e.clientY - startPY;
    const xRange = startXMax - startXMin, yRange = startYMax - startYMin;
    const mxDiff = (dx / CW) * xRange, myDiff = (dy / CH) * yRange;
    vXMin = startXMin - mxDiff; vXMax = startXMax - mxDiff;
    vYMin = startYMin + myDiff; vYMax = startYMax + myDiff;
    fullRedraw();
  });

  canvas.addEventListener('mouseleave', () => { if (isPanning) { isPanning = false; canvas.style.cursor = 'crosshair'; } });
  window.addEventListener('mouseup', () => { if (isPanning) { isPanning = false; canvas.style.cursor = 'crosshair'; } });

  canvas.addEventListener('touchstart', e => {
    if (e.touches.length === 1) {
      const t = e.touches[0];
      isPanning = true;
      startPX = t.clientX; startPY = t.clientY;
      startXMin = vXMin; startXMax = vXMax; startYMin = vYMin; startYMax = vYMax;
    }
  }, { passive: true });

  canvas.addEventListener('touchmove', e => {
    if (!isPanning || e.touches.length !== 1) return;
    const t = e.touches[0], CW = getCW(), CH = getCH(); if (!CW || !CH) return;
    const dx = t.clientX - startPX, dy = t.clientY - startPY;
    const xRange = startXMax - startXMin, yRange = startYMax - startYMin;
    const mxDiff = (dx / CW) * xRange, myDiff = (dy / CH) * yRange;
    vXMin = startXMin - mxDiff; vXMax = startXMax - mxDiff;
    vYMin = startYMin + myDiff; vYMax = startYMax + myDiff;
    fullRedraw();
  }, { passive: true });

  canvas.addEventListener('touchend', () => { isPanning = false; });
}

/* JS chuẩn cho các Nút bấm Zoom (.canvas-zoom-controls) */
function applyZoom(factor) {
  if (CW === 0 || CH === 0) return;
  zoomAt(CW / 2, CH / 2, factor);
}

function zoomAt(cx, cy, factor) {
  const { x: mx, y: my } = c2m(cx, cy);
  const xRange = vXMax - vXMin, yRange = vYMax - vYMin;
  const newXR = xRange * factor, newYR = yRange * factor;
  if (newXR < 2 || newXR > 500) return;
  const pctX = cx / CW, pctY = 1 - cy / CH;
  vXMin = mx - pctX * newXR; vXMax = vXMin + newXR;
  vYMin = my - pctY * newYR; vYMax = vYMin + newYR;
  fullRedraw();
}

function resetView() {
  vXMin = -10; vXMax = 10; vYMin = -10; vYMax = 10;
  fullRedraw();
}
```

### 3.2 Trạng thái nút

```css
/* Toolbar (nền tối) */
.sim-btn          { opacity:.6; border:1px solid rgba(255,255,255,.25); }
.sim-btn.active   { background:var(--accent); color:var(--jade-deep); opacity:1; }
.sim-btn:hover    { border-color:var(--accent); color:var(--accent); opacity:1; }

/* Nút tròn điều khiển */
.ctrl-btn         { width:34px; height:34px; border-radius:50%; border:1.5px solid var(--paper-line); }
.ctrl-btn.playing { background:var(--jade-deep); color:var(--accent); }
.ctrl-btn:hover   { border-color:var(--jade-deep); color:var(--jade-deep); }

/* Nút bước */
.step-btn         { border:1.5px solid var(--paper-line); background:var(--white); }
.step-btn:disabled{ opacity:.4; cursor:default; }
.step-btn:hover:not(:disabled) { border-color:var(--jade-deep); color:var(--jade-deep); }
```

### 3.3 Info Box — 3 loại

```html
<!-- Định nghĩa, khái niệm -->
<div class="info-box ib-blue">
  <div class="ib-icon">📘</div>
  <div class="ib-body">
    <div class="ib-title">Định nghĩa</div>
    <div class="ib-text">Nội dung...</div>
  </div>
</div>

<!-- Lưu ý, cảnh báo nhầm lẫn -->
<div class="info-box ib-gold">
  <div class="ib-icon">⚠️</div>
  <div class="ib-body">
    <div class="ib-title">Lưu ý</div>
    <div class="ib-text">Nội dung...</div>
  </div>
</div>

<!-- Kết luận, ghi nhớ -->
<div class="info-box ib-green">
  <div class="ib-icon">✅</div>
  <div class="ib-body">
    <div class="ib-title">Kết luận</div>
    <div class="ib-text">Nội dung...</div>
  </div>
</div>
```

### 3.4 Section Divider

```html
<div class="sdiv"><span>TÊN SECTION</span></div>
```

### 3.5 Data Display Row

```html
<!-- Hiển thị số liệu real-time bên dưới canvas -->
<div class="disp-row">
  <div class="disp-card">
    <div class="disp-label">SỐ BPT</div>
    <div class="disp-val" id="cntBPT">0</div>
    <div class="disp-unit">bpt</div>
  </div>
  <div class="disp-card">
    <div class="disp-label">ĐIỂM TEST</div>
    <div class="disp-val" id="testResult">—</div>
    <div class="disp-unit"></div>
  </div>
  <div class="disp-insight" id="insight">
    Nhập BPT để bắt đầu khám phá miền nghiệm.
  </div>
</div>
```

### 3.6 Header / Topbar-Tabs / Sidebar điều khiển — chuẩn v2 (thay thế "Preset 5" cũ)

> Không còn ràng buộc theo preset. 3 component dưới đây dùng chung cho mọi bài, chọn theo layout
> đã xác nhận ở BƯỚC 1 (Đơn / Tab ngang / + Sidebar điều khiển).

**Header ảnh nền — tuỳ chọn, phải ẩn được:**
```html
<header>
  <div class="header-badge label-small"><i class="ti ti-flask"></i> Thí nghiệm hóa học</div>
  <h1>TIÊU ĐỀ BÀI HỌC VIẾT HOA</h1>
  <div class="desc">Mô tả ngắn. Bộ sách: Kết nối tri thức với cuộc sống.</div>
</header>
```
```css
header {
  width: 100%; max-width: 760px;
  background: url('ĐỔI_URL_ẢNH_TẠI_ĐÂY');
  background-position: center 30%; background-size: cover; background-repeat: no-repeat;
  border-radius: 16px; padding: 1.5rem 2rem; overflow: hidden; position: relative;
  box-shadow: var(--shadow);
}
header::before, header::after {
  content: ''; position: absolute; border-radius: 50%;
  background: rgba(255,255,255,0.10); pointer-events: none;
}
header::before { width: 200px; height: 200px; top: -60px; right: -40px; }
header::after  { width: 140px; height: 140px; bottom: -50px; left: 20%; }
.header-badge {
  background: transparent; border: none; color: rgba(255,255,255,0.9);
  font-size: 1.05rem; font-weight: 600; margin-bottom: 6px;
  display: flex; align-items: center; gap: 8px;
}
header h1 { color: #fff; font-size: 1.6rem; font-weight: 700; margin-bottom: 4px;
  text-shadow: 0 2px 4px rgba(0,0,0,0.2); }
header .desc { color: rgba(255,255,255,0.8); font-size: 0.95rem; max-width: 90%;
  text-shadow: 0 1px 2px rgba(0,0,0,0.15); }

/* BẮT BUỘC nếu header chứa id JS cập nhật động (điểm số, kết quả...):
   tách phần tử đó ra ngoài header (vd .stat-bar riêng) để có thể ẩn header
   mà không mất dữ liệu. Khi cần nhúng vào platform khác:
   header { display: none; }  ← ẩn, không xoá node */
```

**Tab ngang — thay cho sidebar cố định khi có nhiều module:**
```html
<header class="topbar">
  <div class="topbar-brand">
    <div class="logo"><i class="ti ti-compass"></i><span>Aiducation</span></div>
    <span class="topbar-desc">Mô tả ngắn bộ bài học</span>
  </div>
  <ul class="menu-list" role="tablist">
    <li class="menu-item active" onclick="switchModule(1)" id="menu-mod-1" role="tab">
      <i class="ti ti-icon-tuy-chon"></i><span>1. Tên module</span>
    </li>
    <!-- lặp lại cho module 2, 3, 4... -->
  </ul>
</header>
```
```css
.topbar { background: var(--white); border-bottom: 1px solid var(--paper-line);
  position: sticky; top: 0; z-index: 30; padding: 1rem 1.25rem 0; }
.topbar-brand { display: flex; align-items: baseline; gap: 10px; flex-wrap: wrap; margin-bottom: .75rem; }
.logo { font-weight: 800; font-size: 1.15rem; color: var(--jade-deep);
  display: flex; align-items: center; gap: 6px; }
.topbar-desc { font-size: .78rem; color: var(--ink-3); }
.menu-list { list-style:none; display:flex; gap:6px; overflow-x:auto;
  -webkit-overflow-scrolling:touch; scrollbar-width:none; }
.menu-list::-webkit-scrollbar { display:none; }
.menu-item { flex:0 0 auto; padding:10px 16px; min-height:44px;
  border-radius: var(--radius) var(--radius) 0 0; border-bottom:3px solid transparent;
  display:flex; align-items:center; gap:8px; font-weight:600; font-size:.85rem;
  color: var(--ink-2); white-space:nowrap; cursor:pointer; transition: all .2s ease; }
.menu-item:hover { background: var(--cream); color: var(--jade-deep); }
.menu-item.active { color: var(--jade-deep); border-bottom-color: var(--jade-deep);
  background: var(--jade-pale); }
```
Giữ nguyên `id="menu-mod-n"` + `onclick="switchModule(n)"` — JS chuyển module không đổi logic
dù đổi từ `<aside>` sang tab ngang.

**Info Panel 2 cột (quan sát + hướng dẫn) — token hoá, không hardcode hex:**
```html
<div class="info-panel">
  <div class="info-col info-col-observe">
    <div class="info-col-label"><i class="ti ti-target"></i> Mục đích thí nghiệm</div>
    <p>Nội dung mô tả...</p>
  </div>
  <div class="info-col info-col-guide">
    <div class="info-col-label"><i class="ti ti-hand-click"></i> Hướng dẫn thao tác</div>
    <ul>
      <li><i class="ti ti-circle-number-1"></i><span>Bước 1...</span></li>
      <li><i class="ti ti-circle-number-2"></i><span>Bước 2...</span></li>
    </ul>
  </div>
</div>
```
```css
.info-panel { width: 100%; max-width: 760px; border-radius: var(--radius-lg);
  display: flex; overflow: hidden; }
.info-col { flex: 1; padding: 1.1rem 1.25rem; }
.info-col-observe { background: var(--sage-pale); border: 1px solid var(--sage);
  border-radius: var(--radius-lg) 0 0 var(--radius-lg); }
.info-col-guide { background: var(--jade-pale); border: 1px solid var(--jade-soft);
  border-radius: 0 var(--radius-lg) var(--radius-lg) 0; }
.info-col-label { display:flex; align-items:center; gap:5px; font-size:11px; font-weight:600;
  text-transform:uppercase; letter-spacing:.6px; color: var(--jade-deep); margin-bottom:8px; }
.info-col p, .info-col ul li { font-size:.83rem; color: var(--ink-2); line-height:1.55; }
.info-col ul { list-style:none; padding:0; margin:0; }
.info-col ul li { display:flex; align-items:flex-start; gap:6px; margin-bottom:4px; }
.info-col ul li i { color: var(--jade-deep); font-size:13px; flex-shrink:0; }

@media (max-width: 640px) {
  .info-panel { flex-direction: column; }
  .info-col-observe { border-radius: var(--radius-lg) var(--radius-lg) 0 0; border-bottom: none; }
  .info-col-guide { border-radius: 0 0 var(--radius-lg) var(--radius-lg); }
}
```

**Status Bar (đặt giữa info-panel và canvas):**
```html
<div class="status-bar"><i class="ti ti-info-circle"></i><span id="statusText">Chọn hóa chất để bắt đầu.</span></div>
```
```css
.status-bar { width:100%; max-width:760px; background: var(--white);
  border:1px solid var(--paper-line); border-radius: var(--radius-lg);
  padding:.65rem 1.1rem; display:flex; align-items:center; gap:8px; font-size:.82rem; }
.status-bar i { color: var(--jade-deep); font-size:15px; }
#statusText { font-weight:500; color: var(--ink); }
```

**Sidebar điều khiển (slider/checkbox thông số) — mobile-first ngay từ đầu:**
```html
<div class="workspace">
  <div class="sidebar">
    <div class="card" id="controls-card">
      <div class="card-title"><i class="ti ti-adjustments-horizontal"></i><span>Thiết lập thông số</span></div>
      <!-- sliders / checkbox ở đây -->
    </div>
  </div>
  <div class="canvas-container">
    <!-- canvas + kết quả -->
  </div>
</div>
```
```css
.workspace { display: grid; grid-template-columns: 3.5fr 6.5fr; gap: 1.25rem; }

@media (max-width: 1024px) {
  .workspace { display: flex; flex-direction: column; }
  .canvas-container { order: -1; } /* canvas/kết quả hiện trước, control xuống dưới */
}
@media (max-width: 640px) {
  input[type="range"]::-webkit-slider-thumb { width: 26px; height: 26px; }
  .checkbox-item, .btn, .btn-action { min-height: 44px; }
}
```
> Sidebar này là **tính năng thật** (chứa slider/checkbox), khác hoàn toàn `.sidebar` điều hướng
> cũ đã bỏ ở Mục 3.2 — không bao giờ xoá nội dung bên trong, chỉ đổi thứ tự hiển thị trên mobile.

**Buttons — dùng token, không hardcode navy/teal:**
```css
.btn-group { display: flex; gap: 7px; flex-wrap: wrap; }
.btn {
  padding: 6px 14px; min-height: 40px; border-radius: 20px;
  font-family: inherit; font-size: 0.8rem; font-weight: 600; cursor: pointer;
  transition: all .2s ease; border: 1.5px solid var(--paper-line);
  background: var(--white); color: var(--ink);
  display: inline-flex; align-items: center; gap: 5px;
}
.btn:hover:not(:disabled):not(.btn-active) { border-color: var(--jade-deep); color: var(--jade-deep); }
.btn.btn-active { background: var(--jade-deep); color: #fff; border-color: var(--jade-deep);
  box-shadow: var(--shadow); }
.btn:disabled { opacity: 0.6; cursor: not-allowed; }
.btn-action { padding: 8px 22px; font-size: 0.85rem; min-height: 44px; }
.btn-reset { border: 1.5px dashed var(--paper-line); background: var(--white); color: var(--ink-3); }
.btn-reset:hover { border-color: var(--jade); color: var(--jade); background: var(--jade-pale); }
```

**Explanation Box — dùng token thay vì hex viết cứng:**
```html
<div class="explanation-box" id="explanationBox">
  <div class="eb-title" id="ebTitle"><i class="ti ti-info-circle"></i> Chuẩn bị thí nghiệm</div>
  <div class="eb-body" id="ebBody">Nội dung giải thích...</div>
</div>
```
```css
.explanation-box {
  width: 100%; max-width: 760px; background: var(--jade-pale);
  border: 1px solid var(--jade-soft); border-left: 4px solid var(--jade);
  border-radius: var(--radius-lg); padding: 1.1rem 1.3rem;
  transition: border-color .4s, background .4s, opacity .2s, transform .2s;
}
.explanation-box.reacted { border-left-color: var(--jade-text); background: var(--sage-pale); }
.explanation-box.fade { opacity: 0; transform: translateY(6px); }
.eb-title { display:flex; align-items:center; gap:7px; font-size:.875rem; font-weight:700;
  color: var(--jade-deep); margin-bottom:8px; }
.explanation-box.reacted .eb-title { color: var(--jade-text); }
.eb-body { font-size:.83rem; color: var(--ink-2); line-height:1.65; }
.eb-body strong { color: var(--ink); }
.eb-highlight { display:inline-flex; align-items:center; gap:4px; background: var(--warning-bg);
  border-radius:6px; padding:2px 8px; font-weight:600; color: var(--accent-text); font-size:.78rem; margin-top:6px; }
.eb-eq { margin-top:9px; background: var(--cream-2); border-radius:8px; padding:8px 12px;
  font-size:.8rem; color: var(--ink); font-weight:500; border-left:3px solid var(--jade-deep);
  font-family: 'JetBrains Mono', 'Courier New', monospace; }
.explanation-box.reacted .eb-eq { border-left-color: var(--jade-text); background: var(--correct-bg); }
```

**JS pattern — fade khi cập nhật nội dung (không đổi):**
```javascript
function setExplanationContent(icon, title, body, equation) {
  const box = document.getElementById('explanationBox');
  box.classList.add('fade');
  setTimeout(() => {
    document.getElementById('ebTitle').innerHTML = `<i class="ti ${icon}"></i> ${title}`;
    document.getElementById('ebBody').innerHTML =
      body + (equation ? `<div class="eb-eq">${equation}</div>` : '');
    box.classList.remove('fade');
  }, 200);
}
// Khi reacted: box.classList.add('reacted') trước khi gọi setExplanationContent
```

**Checklist mobile/responsive bắt buộc — áp dụng cho mọi component ở trên:**
- [ ] Mọi nút/tab/input/checkbox ≥ 44×44px trên mobile
- [ ] Canvas không có `height` cố định theo px — dùng `aspect-ratio`
- [ ] Không tràn ngang ở 375px
- [ ] Tab/menu ngang cuộn được, ẩn scrollbar
- [ ] Sidebar điều khiển: canvas/kết quả hiện trước, control xuống sau (`order`)


---

### 3.7 Collapsible Panel — "nút gom" cho nội dung dài phía trên canvas (bắt buộc cân nhắc)

> **Vấn đề cần tránh:** info-panel / explanation-box / hướng dẫn dài đặt phía trên canvas sẽ đẩy
> canvas xuống dưới màn hình đầu tiên — trên mobile, học sinh phải cuộn qua hết chữ mới thấy được
> phần tương tác. Dùng component này bất cứ khi nào nội dung tĩnh phía trên canvas dài quá ~4 dòng.

**Quy tắc vị trí:** Canvas/phần tương tác chính luôn phải lọt trong màn hình đầu tiên trên mobile
(375px, không cuộn). Nếu hướng dẫn dài, mặc định **thu gọn trên mobile**, **mở sẵn trên desktop**
(đủ chỗ). `status-bar` (Mục 3.6) vẫn luôn hiện — đó là dòng tóm tắt 1 dòng thay thế cho việc phải
mở panel dài ra mới biết đang làm gì.

```html
<div class="collapsible-panel" id="guidePanel">
  <button class="cp-toggle" onclick="toggleCollapsible('guidePanel')"
          aria-expanded="true" aria-controls="guidePanel-body">
    <span><i class="ti ti-info-circle"></i> Hướng dẫn & mục tiêu</span>
    <i class="ti ti-chevron-up cp-chevron"></i>
  </button>
  <div class="cp-body" id="guidePanel-body">
    <!-- info-panel / explanation-box / nội dung dài đặt ở đây -->
  </div>
</div>
```
```css
.collapsible-panel { width: 100%; max-width: 860px; }
.cp-toggle {
  width: 100%; display: flex; justify-content: space-between; align-items: center;
  min-height: 44px; padding: 0.65rem 1rem; background: var(--white);
  border: 1px solid var(--paper-line); border-radius: var(--radius-lg);
  cursor: pointer; font-weight: 600; font-size: 0.85rem; color: var(--ink);
}
.cp-toggle span { display: flex; align-items: center; gap: 6px; }
.cp-chevron { transition: transform 0.25s ease; color: var(--ink-3); }
.cp-body {
  overflow: hidden; max-height: 1200px; margin-top: 0.5rem;
  transition: max-height 0.3s ease, opacity 0.2s ease, margin-top 0.3s ease;
}
.collapsible-panel.collapsed .cp-body { max-height: 0; opacity: 0; margin-top: 0; }
.collapsible-panel.collapsed .cp-chevron { transform: rotate(180deg); }
```
```javascript
function toggleCollapsible(id) {
  document.getElementById(id).classList.toggle('collapsed');
}
// Mặc định thu gọn trên mobile khi trang load — canvas hiện ngay không cần cuộn
document.querySelectorAll('.collapsible-panel').forEach(p => {
  if (window.matchMedia('(max-width: 768px)').matches) p.classList.add('collapsed');
});
```

**Áp dụng vào đâu:** bọc `.collapsible-panel` quanh `.info-panel` (Mục 3.6) và/hoặc
`.explanation-box` (Mục 3.6) khi nội dung dài — không cần bọc `status-bar` (luôn hiện) hay
`sim-wrap`/canvas (không bao giờ thu gọn phần tương tác chính).

> Đây KHÔNG cần lưu trạng thái qua `LMS().state()` (PHẦN 7) — chỉ là tiện ích UI, mỗi lần tải
> trang lại mặc định theo breakpoint là đủ, không cần nhớ học sinh đã đóng/mở lần trước.

---

### 3.8 Tương tác chạm trên canvas — Tap-to-toggle (bắt buộc, thay hover-only)

> **Vấn đề:** `mouseenter`/`mouseleave` một mình KHÔNG chạy trên thiết bị cảm ứng (không có
> trạng thái hover) — mọi tooltip/thông tin gắn theo hover sẽ hoàn toàn không hiện được trên
> mobile/tablet dù giao diện đã responsive đúng.

**Quy tắc bắt buộc:** mọi điểm tương tác trên canvas hiện tooltip/thông tin phải dùng `click`
(chạy được cho cả chuột và tap chạm), theo mô hình tap-to-toggle:

```javascript
function svgPointToScreen(svgEl, svgX, svgY) {
  const pt = svgEl.createSVGPoint();
  pt.x = svgX; pt.y = svgY;
  const p = pt.matrixTransform(svgEl.getScreenCTM());
  return { x: p.x, y: p.y };
}

function showTooltip(x, y, text) {
  const tt = document.getElementById('canvasTooltip');
  const screenPos = svgPointToScreen(document.getElementById('svgLayer'), x, y);
  tt.style.opacity = 1; tt.textContent = text;
  const r = tt.getBoundingClientRect(), vw = innerWidth, vh = innerHeight;
  let left = screenPos.x + 15, top = screenPos.y - 15;
  if (left + r.width > vw - 12) left = screenPos.x - r.width - 15;
  if (top < 12) top = screenPos.y + 20;
  tt.style.left = Math.max(8, Math.min(left, vw - r.width - 8)) + 'px';
  tt.style.top = Math.max(8, Math.min(top, vh - r.height - 8)) + 'px';
}

let activeTooltipId = null;
function bindTapTooltip(el, id, x, y, text) {
  el.style.cursor = 'pointer';
  el.addEventListener('click', (e) => {
    e.stopPropagation();
    if (activeTooltipId === id) { hideTooltip(); activeTooltipId = null; }
    else { showTooltip(x, y, text); activeTooltipId = id; }
  });
}
document.addEventListener('click', () => {
  if (activeTooltipId !== null) { hideTooltip(); activeTooltipId = null; }
});
```

Lý do dùng `getScreenCTM()`: nếu quy đổi thẳng toạ độ SVG làm toạ độ pixel màn hình, tooltip sẽ
lệch vị trí khi SVG bị scale nhỏ lại trên mobile — bắt buộc quy đổi qua CTM.

**Ghim thanh nút điều hướng vào đáy màn hình mobile** — dùng khi nội dung/canvas phía trên vẫn
còn cao dù đã áp dụng Mục 3.7, khiến nút "Tiếp theo" bị đẩy xa:

```css
@media (max-width: 767px) {
  .ctrl-actions /* hoặc đúng class chứa nút điều hướng của file */ {
    position: fixed !important; left: 0; right: 0; bottom: 0; z-index: 50;
    background: var(--white); border-top: 1px solid var(--paper-line);
    box-shadow: 0 -4px 16px rgba(0,0,0,0.10);
    padding: 10px 16px calc(10px + env(safe-area-inset-bottom, 0px));
    margin: 0 !important;
  }
  body { padding-bottom: 76px; } /* chừa chỗ để nội dung cuối không bị thanh nút che */
}
```

**Checklist bổ sung cho Mục 2.8 (Checklist sau khi build):**
- [ ] Không có `mouseenter`/`mouseleave` đứng một mình cho tooltip — luôn có `click`/tap song song
- [ ] Tooltip tự kẹp trong khung nhìn, không tràn mép màn hình ở 375px
- [ ] Nếu canvas/nội dung cao, nút điều hướng chính đã ghim đáy màn hình trên mobile hoặc luôn
      nằm trong màn hình đầu tiên



## PHẦN 4 — NAMING CONVENTION

```
File HTML:
  Chuong[X]_Bai[Y]_Toan_Module_[Z].html
  Chuong[X]_Bai[Y]_Toan_Module_[1_va_2].html

Element ID (prefix theo module):
  Canvas:        simCanvas, simCanvas-m2
  Play:          btnPlay-m1
  Play icon:     playIcon-m1
  Caption:       caption-m1
  Coord bar:     coordBar-m1
  Guide:         guide-btn-m1, guide-panel-m1
  Audio:         audio-btn-m1, audio-icon-m1
  Check result:  checkResult-m1

CSS class prefix:
  sim-*    → simulation wrapper & toolbar
  mod-*    → module / sidebar item
  ctrl-*   → controls (play, step, speed)
  disp-*   → data display row & card
  ib-*     → info box
  ql-*     → quiz level badge (basic/good/hard)
  btn-*    → buttons ngoài sim (zoom, add, check)

CSS variables: LUÔN dùng đúng tên token ở PHẦN 1 (--jade, --ink, --cream...).
KHÔNG dùng tên biến kiểu cũ (--primary, --bg, --surface, --text...) trong file mới.
```

> **Liên kết với PHẦN 7:** id module (`m1`, `m2`...) dùng ở trên PHẢI là đúng id dùng trong
> `structure[].id` của Athena manifest và trong `LMS().progress()/state()` — dùng chung 1 bộ id
> xuyên suốt file, không đặt tên khác nhau ở từng chỗ.

---

## PHẦN 5 — GIỚI HẠN VÒNG LẶP

```
- Nếu sau 2 lần fix lỗi vẫn không đúng:
  AI dừng và hỏi lại 3 câu:
  1. "Bạn thấy gì trên màn hình?" (yêu cầu upload ảnh)
  2. "Bạn mong muốn nó trông như thế nào?"
  3. "Lỗi xảy ra khi làm thao tác gì?"

- Lỗi canvas hay gặp ở Toán:
  → Miền và đường lệch nhau: kiểm tra putImageData trước setTransform
  → ResizeObserver loop: kiểm tra debounce 30ms
  → Label tràn ra ngoài: kiểm tra hàm drawLineLabel()
  → Nét đứt không reset: kiểm tra ctx.setLineDash([]) sau mỗi đường

- Mỗi phiên chỉ build 1 file HTML.
  Muốn làm bài khác → bắt đầu conversation mới.
```

---

## PHẦN 7 — TÍCH HỢP LMS & ATHENA MANIFEST (bắt buộc, mọi file mới đều phải có)

> **Vì sao:** Module HTML được nhúng vào LMS Aiducation, nơi gia sư AI "Athena" theo dõi tiến độ
> và trả lời câu hỏi của học sinh **mà không đọc được DOM** — mọi thứ Athena biết về bài học đến
> từ đúng 1 nguồn: manifest + state được instrumentation bên dưới phát ra. Thiếu 1 phần =
> Athena "mù" một phần bài học đó.
> **Khi build:** viết instrumentation này **cùng lúc** với logic thật của module (gọi từ trong
> chính handler chọn đáp án / chuyển section...), không phải lớp quan sát tách rời gắn thêm sau.

### 7.1 Ràng buộc môi trường chạy (sandbox — không được phá vỡ)

```
- Không được gọi mạng: fetch / XHR / WebSocket bị chặn.
- Tài nguyên ngoài chỉ được phép từ: cdn.jsdelivr.net, fonts.googleapis.com, fonts.gstatic.com.
  Ảnh: inline SVG, data: URI, hoặc https:.
- KHÔNG dùng localStorage / cookie để lưu trạng thái — lưu qua LMS().state().
- 1 file HTML tự chứa (self-contained). Không build step, không import, không eval (CSP nghiêm).
```

### 7.2 Safe accessor — dán đầu `<script>` đầu tiên

Để file vẫn chạy được khi mở độc lập (ngoài LMS), không lỗi `window.AiducationLMS is undefined`:

```javascript
function LMS(){return window.AiducationLMS||{ready:function(){},progress:function(){},event:function(){},state:function(){},complete:function(){},resize:function(){}};}
```

### 7.3 Athena Manifest — dán trong `<head>`

```html
<script type="application/json" id="athena-context">
{
  "title": "...",          // lấy từ <title> hoặc heading chính
  "subject": "Toán", "grade": "10", "track": "...",   // suy luận nếu rõ, bỏ qua nếu không chắc
  "objectives": ["...", "..."],   // 2-5 mục tiêu học tập, tiếng Việt, cụ thể
  "structure": [ { "id": "m1", "title": "Module 1 — ..." } ],  // id PHẢI trùng id dùng ở 7.4/7.5
  "athenaGuidance": "..."  // xem quy tắc viết ở dưới
}
</script>
```

**Quy tắc viết `athenaGuidance` (đây là toàn bộ những gì Athena biết về bài — phải tự đủ nghĩa):**
```
(a) 1-2 câu: bài này dạy gì, học sinh thao tác gì.
(b) Danh sách đánh số TỪNG câu hỏi/tương tác, kèm NGUYÊN VĂN các lựa chọn đáp án, ví dụ:
      "1) <câu hỏi> — Lựa chọn: A) … B) … C) … D)"
    Lấy đúng từ nội dung file — KHÔNG tóm tắt, KHÔNG ghi đáp án đúng ở đây.
(c) Quy tắc đứng: Athena chỉ gợi ý/hướng dẫn, KHÔNG BAO GIỜ nói thẳng đáp án đúng.
Viết đủ, không cắt ngắn cho gọn — thiếu thông tin ở đây Athena sẽ trả lời sai/thiếu với học sinh.
```

### 7.4 Progress + Events — gọi từ trong logic thật

```javascript
LMS().progress({ done, total });   // mỗi khi 1 section bắt buộc hoàn thành
                                    // done = số đã xong, total = số bắt buộc — LMS tự tính %
LMS().event('answered', { id:'q2', chosen:'B', correct:false });  // mọi tương tác có ý nghĩa
```

### 7.5 Completion + Results — bắn ĐÚNG 1 LẦN (guard bằng biến boolean)

Khi tất cả section bắt buộc đã xong. `results` phải tự mô tả đủ, vì Athena đọc thẳng JSON này
để nói cho học sinh biết đúng/sai chỗ nào:

```javascript
LMS().complete({
  summary: "...",          // 1 câu tóm tắt tiếng Việt
  score: 0, max: 0,
  items: [
    { id: "q1", prompt: "...", options: ["A) …","B) …","C) …","D) …"],
      chosen: "...", correct: "...", isCorrect: true }
    // 1 phần tử / 1 câu hỏi-tương tác, lấy từ state trả lời THẬT của module
  ]
});
// Không lấy được giá trị nào → dùng null, ghi chú ở notes. TUYỆT ĐỐI không bịa câu hỏi/đáp án.
```

### 7.6 Live State — gọi mỗi lần UI thay đổi có ý nghĩa

Đổi tab, đổi bước/section, chọn đáp án, lật thẻ... — để Athena biết chính xác học sinh đang ở
đâu khi họ hỏi giữa chừng. Nhãn dùng tiếng Việt:

```javascript
LMS().state({
  activeTab: "Luyện tập",
  currentStep: 3, totalSteps: 5,
  answeredSoFar: { q1: "B", q2: null },
  lastAction: "mở tab Luyện tập"
});

// Bắt buộc hỗ trợ resume — áp lại đúng state đã lưu lần cuối:
if (window.AiducationLMS) window.AiducationLMS.onResume = function(state){ /* áp lại state */ };
```

### 7.7 Resize — báo chiều cao thật cho LMS (khắc phục khoảng trắng thừa giữa các file/video)

> **Nguyên nhân khoảng trắng vô lý khi nhúng file lên LMS:** LMS nhúng file bằng iframe. Nếu file
> không báo chiều cao nội dung THẬT của nó, LMS phải đoán/dùng chiều cao mặc định (thường cao hơn
> nội dung thật) → để lại khoảng trắng lớn trước khi tới file/video tiếp theo. `resize` đã có sẵn
> trong safe accessor (Mục 7.2) nhưng **phải chủ động gọi**, không tự chạy.

```javascript
function reportHeight() {
  const h = document.documentElement.scrollHeight;
  LMS().resize({ height: h });
}
// Gọi khi tải xong...
window.addEventListener('load', reportHeight);
// ...và mỗi khi nội dung đổi chiều cao (mở/đóng collapsible panel, đổi tab/module, quiz hiện thêm...)
// BẮT BUỘC kiểm tra ResizeObserver có tồn tại trước khi dùng — 1 số WebView cũ (app LMS nhúng
// trên Android cũ, hoặc trình duyệt embed hiếm) không hỗ trợ ResizeObserver. Nếu gọi thẳng
// `new ResizeObserver(...)` mà API không tồn tại, dòng này crash NGAY LẬP TỨC ở cấp module —
// toàn bộ phần script phía SAU (kể cả logic vẽ canvas, tương tác...) sẽ KHÔNG chạy nữa, khiến
// cả trang trông như trống trơn/hỏng dù code hoàn toàn đúng. Luôn bọc feature-check:
if (typeof ResizeObserver !== 'undefined') {
  const ro = new ResizeObserver(() => { clearTimeout(window._rz); window._rz = setTimeout(reportHeight, 100); });
  ro.observe(document.body);
} else {
  // Fallback: vẫn báo chiều cao định kỳ dù không có ResizeObserver, tránh im lặng bỏ qua hẳn
  setInterval(reportHeight, 800);
}
```

**2 nguyên nhân khác cũng gây khoảng trắng — kiểm tra cùng lúc:**
- `body { min-height: 100vh; }` hoặc `height: 100vh` — ép trang cao bằng nguyên viewport dù nội
  dung ngắn hơn nhiều. **Bỏ hẳn `min-height:100vh`/`height:100vh` trên `body`** khi file được build
  để nhúng LMS — để chiều cao trang co theo đúng nội dung, rồi báo lại qua `resize()` ở trên.
- Margin/padding lớn cuối trang (`<body>` hoặc phần tử cuối cùng) — kiểm tra không còn khoảng đệm
  thừa sau phần tử cuối (thường là quiz/kết luận).

**Quy tắc Khóa chiều cao bố cục theo bước dài nhất (Layout Height Locking):**
- Đối với các simulation có mở từng bước dồn dập (ví dụ Module 2 có 4 bước mở dần), nếu để chiều cao co giãn tự nhiên, iframe LMS sẽ bị nảy/re-scale hoặc đẩy thanh sidebar khi học sinh bấm tới từng bước.
- **Giải pháp bắt buộc:** Đặt `min-height` cố định trên `.sim-left` (ví dụ `min-height: 520px` desktop / `480px` mobile) tương ứng với chiều cao khi mở ĐẦY ĐỦ TẤT CẢ CÁC BƯỚC.
- Việc này giúp chiều cao toàn trang (`scrollHeight`) được tính ổn định chuẩn xác 100% ngay từ khi trang vừa load, LMS iframe nhận đúng kích thước tối đa duy nhất 1 lần và không bao giờ bị giật/scale lại khi chuyển bước.
- **Hướng dẫn cho AI:** Khi tạo bài mới hoặc refactor bài bất kỳ, AI sẽ tự động phân tích số bước trong kịch bản để thiết lập `min-height` chuẩn sẵn trong code, người dùng KHÔNG cần phải tự đo đạc hay sửa thủ công.

> **Lưu ý:** contract LMS hiện tại chỉ định nghĩa `resize` là 1 hàm rỗng trong fallback, chưa nêu
> rõ tham số mong đợi (`{height}` là suy đoán hợp lý theo convention của các iframe auto-resize
> phổ biến). Cần xác nhận lại đúng shape tham số với phía kỹ thuật LMS trước khi áp dụng hàng loạt
> — nếu sai shape, `resize()` gọi cũng vô hại (an toàn), chỉ là không có tác dụng.

### 7.8 Checklist trước khi coi 1 file là "sẵn sàng LMS"

- [ ] Có `function LMS(){...}` safe accessor ở đầu script đầu tiên
- [ ] `#athena-context` tồn tại, JSON hợp lệ, `structure[].id` khớp id dùng ở progress/complete/state
- [ ] `athenaGuidance` liệt kê ĐỦ mọi câu hỏi kèm nguyên văn lựa chọn — không tóm tắt, không lộ đáp án đúng
- [ ] `LMS().progress()` và `LMS().event()` được gọi từ trong handler thật, không phải observer rời
- [ ] `LMS().complete()` bắn đúng 1 lần, có guard, `results.items[]` khớp 1-1 với câu hỏi thật trong bài
- [ ] `LMS().state()` gọi ở mọi thay đổi UI có ý nghĩa + có `onResume` áp lại state
- [ ] Không dùng `localStorage`/cookie để lưu tiến độ — chỉ qua `LMS().state()`
- [ ] Không gọi mạng ngoài danh sách domain cho phép ở 7.1
- [ ] Vẫn là 1 file HTML tự chứa — không build step, không import, không `eval`
- [ ] Đã gọi `LMS().resize()` lúc load + mỗi khi chiều cao nội dung đổi (Mục 7.7)
- [ ] `body` KHÔNG có `min-height: 100vh` / `height: 100vh` — chiều cao co theo nội dung thật
- [ ] Nội dung dài phía trên canvas đã bọc `.collapsible-panel` nếu cần (Mục 3.7)

### 7.9 Quy tắc đặt tên nhân vật AI (áp dụng mọi nội dung mới)

> Toàn hệ thống Aiducation dùng thống nhất tên **"Athena"** cho gia sư AI. **Không** dùng "AI"
> hay "Robot"/"robot" để chỉ nhân vật/trợ lý trong nội dung mới — kể cả khi kịch bản gốc còn ghi
> tên cũ (do làm trước quy định này). Áp dụng cho mọi câu thoại, caption, tên nhân vật hiển thị
> cho học sinh — **không** áp dụng cho các bài có "robot" là **đối tượng vật lý/toán học thật
> trong đề bài** (ví dụ bài minh hoạ dãy số hội tụ bằng robot đi từng nửa quãng đường còn lại) —
> trường hợp đó là nhân vật của đề toán, không phải trợ lý AI, giữ nguyên không đổi.



---

> **Phiên bản 2.2** — sau khi đối chiếu với file design Vật Lý (bản trưởng thành hơn, tham chiếu
> `Quy_chuan_tao_HTML_Aiducation.pdf` — nay không còn dùng file PDF đó nữa):
> - Xoá hẳn PHẦN 6 (multi-file project structure) — chưa từng dùng trong thực tế (luôn build 1 file
>   HTML duy nhất để upload lên hệ thống) và mâu thuẫn trực tiếp với ràng buộc "1 file tự chứa,
>   không build step" ở PHẦN 7 (LMS).
> - Bỏ lớp alias (`--primary`, `--bg`, `--surface`, `--text`...) khỏi PHẦN 1 — dùng thẳng tên token
>   gốc (`--jade-deep`, `--cream`, `--white`, `--ink`...) trong mọi CSS mới. Alias chỉ còn giữ trong
>   `AIDUCATION_UI_REDESIGN_PLAYBOOK.md` (dùng khi vá file cũ đã có sẵn `var(--primary)` rải rác).
> - Đổi font số liệu/canvas từ Courier New → Inconsolata → **JetBrains Mono** (cả hai đều load qua
>   Google Fonts nên hiển thị đồng nhất mọi thiết bị, thay vì phụ thuộc font hệ điều hành có thể
>   thiếu trên 1 số máy). Lý do đổi từ Inconsolata sang JetBrains Mono: bộ ký hiệu toán/khoa học
>   rộng hơn (số mũ/subscript sẵn có, ký tự Hy Lạp, toán tử ≈ ≤ ≥), phù hợp hơn cho công thức
>   Toán/Lý/Hoá hiển thị trên canvas. Cả hai đều hỗ trợ tiếng Việt đầy đủ.
> - Tăng cỡ chữ nền tảng body 15px → **18px** và toàn bộ thang cỡ chữ theo tỉ lệ tương ứng, dễ đọc
>   hơn trên mọi thiết bị đặc biệt mobile.
