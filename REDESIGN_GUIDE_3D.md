# 🛠️ REDESIGN GUIDE — Cập nhật `04_design_toan_3d.md`

> **Mục đích file này:** tổng hợp toàn bộ thay đổi cần đưa vào `04_design_toan_3d.md`
> (và ghi chú các file liên quan `05_threejs_engine.md`, `06_geometry_math.md`,
> `01_scenario_builder_3d_addendum.md`) sau quá trình rà soát + làm preview thực tế
> trên 2 file `C5-Bai10_Toan3D_KhaiNiemMoDau.html` và `C5-Bai10_Toan3D_Simulation2_GiaoTuyen.html`.
>
> File này **không phải bản thay thế** `04_design_toan_3d.md` — là bản tổng hợp
> "cần sửa gì, ở đâu, vì sao" để áp trực tiếp vào file đó trong lượt tiếp theo.
> Đã áp dụng 1 phần (mục 3) vào bản `04_design_toan_3d.md` gửi trước — các mục
> còn lại (1, 2, 4, 5) **chưa áp dụng vào doc**, chỉ mới xác nhận hướng đi.

---

## 1. ĐỔI TOÀN BỘ BẢNG MÀU — Jade/Cream thay preset Navy&Teal/Deep Space/Sky&White

### Quyết định đã chốt
Bộ màu chính thức toàn hệ thống (Neutrals/Jade/Sage/Accent/Semantic/Illustration —
đúng token trong `02_design_toan_final.md` PHẦN 1) áp dụng **cho cả 3D**, thay thế
hoàn toàn 3 preset cũ (Navy&Teal / Deep Space / Sky&White) ở §Bước 1 và §1.2.

**Ngoại lệ duy nhất — giữ nguyên, không đổi:** nền canvas 3D tối (`--canvas-bg`,
hiện là `#0a1628` hoặc tương đương theo preset cũ từng bài) và toàn bộ màu đối
tượng hình học (`06_geometry_math.md`, PHẦN 1.3 của `04_design_toan_3d.md`) —
lý do: nền sáng phá vỡ khả năng nhìn chiều sâu/khối 3D, đã thống nhất với giáo viên.

### Cần sửa trong `04_design_toan_3d.md`
- **§Bước 1 (Chọn concept thiết kế):** bỏ hẳn bảng 3 preset Navy&Teal/Deep
  Space/Sky&White. Thay bằng: xác nhận màu nền canvas tối (duy nhất còn được
  chọn, vd giữ 3 tuỳ chọn nền canvas cũ làm 3 "chế độ tối" nếu vẫn cần đa dạng
  cảm giác bài học) — nhưng **toàn bộ UI xung quanh dùng cố định 1 bộ Jade/Cream**,
  không còn là 1 phần của "concept" phải chọn nữa.
- **§1.2 (Preset màu UI — nền trang, header, sidebar):** thay nội dung bằng
  đúng khối `:root` Jade/Cream (dán từ `02_design_toan_final.md` §1.1), **cộng
  thêm dòng**: `--canvas-bg` tách riêng khỏi preset UI, khai báo cạnh khối màu
  đối tượng hình học ở §1.3, không nằm trong nhóm "màu UI" nữa.

### Cách áp dụng vào file ĐÃ BUILD trước đó (pattern alias — đã verify thực tế)
Không sửa từng chỗ gọi `var(--navy)`, `var(--teal)`... rải rác trong code — chỉ
đổi **định nghĩa** biến trong `:root` để trỏ sang Jade/Cream, giữ tên biến cũ
làm alias. Đã áp dụng thành công trên `C5-Bai10_Toan3D_KhaiNiemMoDau.html`:

```css
:root {
  /* ...dán nguyên token Jade/Cream chuẩn... */

  /* ALIAS cho code cũ — không đổi bất kỳ chỗ dùng var(--ten-cu) nào trong file,
     chỉ đổi định nghĩa để trỏ sang Jade/Cream */
  --green: var(--correct);   --green-light: var(--correct-bg);
  --red: var(--wrong);       --red-light: var(--wrong-bg);
  --amber: var(--warning);   --amber-light: var(--warning-bg);
  --blue: var(--info);       --blue-light: var(--info-bg);
  --surface: #ffffff;
  --border: var(--paper-line);
  --text: var(--ink);
  --text-2: var(--ink-2);
  --sub: var(--ink-3);

  --navy: var(--jade-dark);   /* header bg, chữ đậm */
  --teal: var(--jade-deep);   /* primary action, tab active, toggle-on */
  --bg: var(--cream);         /* nền trang ngoài canvas */

  /* NGOẠI LỆ — giữ nguyên */
  --canvas-bg: #0a1628;
}
```

⚠️ **Cảnh báo quan trọng phát hiện thực tế khi làm preview:** đổi `:root` là
CHƯA ĐỦ. File build cũ thường có **màu hardcode trực tiếp** (không đi qua
`var()`) rải rác trong CSS — ví dụ đã tìm thấy 22 chỗ trong 1 file (`#f8fafc`,
`#22c55e`, `#0d47a1`, `#fffbeb`, `#b45309`...) ở các class: info-box 4 loại
(`.ib-blue/.ib-teal/.ib-gold/.ib-red`), `.hud-card`, `.hud-item.valid/.invalid`,
`.badge-relation`, `.progress-dot`, `.prediction-box` (cognitive-conflict UI),
`.btn-primary:hover/:disabled`, `.sub-nav`. **Bắt buộc dò tay bằng regex hex
color (`#[0-9a-fA-F]{3,6}`) trước khi coi 1 file là "đã đổi màu xong"** — đổi
`:root` không tự động lan ra các chỗ này.

**Ngoại lệ được phép giữ hardcode — không đổi:** màu set qua JS ngay trên nhãn/
label 3D gắn trực tiếp lên khối hình trong canvas (vd `p.htmlLabel.style.color`)
— thuộc phần đối tượng hình học/canvas tương tác, không phải UI chrome.

### Cần thêm vào `04_design_toan_3d.md` — Mục ghi chú mới
Thêm 1 đoạn cảnh báo ngay sau bảng token mới ở §1.2, nội dung tương đương đoạn
"⚠️ Cảnh báo quan trọng" ở trên, để người build sau không lặp lại việc bỏ sót
hardcode color.

---

## 2. HEADER — Giữ nguyên, không ẩn; đổi màu; bỏ tên bài cụ thể

### Quyết định đã chốt (khác với pattern 2D)
- 2D ẩn hẳn `<header>` (dùng `.intro-text` thay thế) — **3D KHÔNG áp dụng theo
  2D**. Header 3D giữ hiển thị, vì đây là thành phần cấu trúc bắt buộc theo
  `04_design_toan_3d.md` §Bước 4 (Header + Canvas + Sidebar), không phải banner
  trang trí thuần.
- Tiêu đề trong header **chỉ còn 1 dòng cố định: "🧊 Hình học không gian"**
  (badge sẵn có) — **bỏ hẳn `<h1>Tên bài học</h1>`** (tên bài cụ thể, VD "Bài
  10: Đường thẳng và Mặt phẳng..."). Lý do: nhìn "ghê", quá cụ thể/nặng so với
  phần còn lại của giao diện sau khi đổi sang Jade/Cream.
- Gradient header đổi từ `navy→#1a4a7a` sang `var(--jade-dark)→var(--teal)`
  (alias, tức `#14432F → #2D8B6F`).

### Cần sửa trong `04_design_toan_3d.md`
**§2.1 Header chuẩn** — template HTML hiện tại vẫn còn:
```html
<header>
  <div class="header-badge">🧊 Hình học không gian</div>
  <h1>Tên bài học</h1>   <!-- ← XOÁ dòng này -->
</header>
```
→ Sửa thành:
```html
<header>
  <div class="header-badge">🧊 Hình học không gian</div>
</header>
```
Đồng thời xoá luôn định nghĩa CSS `header h1 { ... }` nếu không còn dùng ở đâu
khác, hoặc giữ lại (không hại gì) nhưng ghi rõ "không dùng trong template chuẩn
mới — chỉ còn cho file cũ chưa patch".

**Cũng cần sửa gradient trong §2.1:**
```css
/* Cũ */
background: linear-gradient(135deg, var(--navy) 0%, #1a4a7a 100%);
/* Mới — sau khi alias --navy/--teal đã trỏ Jade/Cream */
background: linear-gradient(135deg, var(--navy) 0%, var(--teal) 100%);
```

> ⚠️ **Cần bạn xác nhận thêm:** quyết định "bỏ tên bài, chỉ còn Hình học không
> gian" áp dụng cho **mọi bài 3D** hay chỉ 2 file `C5-Bai10` đang test? Nếu áp
> dụng toàn hệ thống, cần nghĩ lại cách học sinh biết mình đang học bài nào khi
> mở file độc lập (ngoài LMS, không có breadcrumb) — có thể cần thêm 1 dòng
> subtitle nhỏ khác vị trí (không phải h1 chính) hoặc chấp nhận việc này chỉ
> hiển thị đúng trong ngữ cảnh LMS (đã có breadcrumb/tên bài ở khung ngoài).

---

## 3. LMS RESIZE (khoảng trắng cuối trang) — ĐÃ ÁP DỤNG VÀO DOC

> Mục này đã được thêm thành **§2.9b** trong bản `04_design_toan_3d.md` gửi
> trước — nhắc lại tóm tắt ở đây để guide này đầy đủ, không cần đọc lại file cũ.

- **Nguyên nhân:** `body { height:100vh; overflow:hidden }` khiến
  `document.documentElement.scrollHeight` luôn bằng đúng viewport, không phản
  ánh nội dung thật → `LMS().resize()` (nếu có gọi) báo sai ngay từ đầu →
  LMS phải tự đoán chiều cao iframe → để lại khoảng trắng thừa.
- **Sửa:** bỏ `height:100vh`/`overflow:hidden` ở cấp `body`. Chiều cao cố định
  cần cho canvas (Three.js cần kích thước pixel xác định) dời xuống cấp
  `.app-body`/`.main` — không đặt ở `body`.
- **Thêm:** safe accessor `function LMS(){...}` (dùng chung 2D/3D, không đổi) +
  `reportHeight()` gọi lúc `load` và qua `ResizeObserver` (có fallback
  `setInterval` cho WebView cũ không hỗ trợ `ResizeObserver`).
- Đã thêm checklist "sẵn sàng LMS" riêng cho 3D (4 mục) vào cuối §2.9b.
- Tiện thể sửa luôn §2.9: xoá việc ép `.sidebar { height: 50% }` trên mobile
  (không có trong spec gốc, tự phát sinh ở file build trước, gây sidebar chật).

---

## 4. RESPONSIVE / MOBILE — Quy chuẩn Mobile Responsive toàn hệ thống

- **Breakpoint chính thức:** Thống nhất dùng `@media (max-width: 992px)` cho toàn bộ ứng dụng Toán (cả 2D và 3D).
- **Cấu trúc Canvas Sticky (`viewport-container`):** Trên Mobile, `.viewport-container` được ghim ở đỉnh màn hình (`position: sticky; top: 0; z-index: 50`) với chiều cao `calc((100vh - 48px) * 0.45)` (45vh) kèm bóng đổ `box-shadow: 0 4px 16px rgba(0, 0, 0, 0.12)`. Giúp học sinh luôn quan sát được hình 3D/2D trực quan khi cuộn bên dưới.
- **Sidebar & Card co giãn tự nhiên:** `.sidebar` để chiều cao tự nhiên (`height: auto; overflow: visible`), cuộn theo trang. Các phần tử `.card`, `.info-box`, `.text-input` áp dụng `box-sizing: border-box; width: 100%` để đảm bảo không bao giờ bị vỡ khung hay tràn ô nhập trên màn hình nhỏ.

---

## 5. LMS/ATHENA — PHẦN CHƯA LÀM, CẦN LƯỢT SAU

> Xác nhận rõ: đây là phần **lớn nhất còn thiếu**, chưa đưa vào `04_design_toan_3d.md`.
> Nguyên nhân gốc: dòng "Kế thừa" cuối file 3D trỏ vào `02_design_toan_2.md`
> (tên file cũ) — tức 3D được viết dựa trên bản 2D **trước khi** các mục dưới
> đây được thêm vào (theo changelog v2.2/v2.3.1 của `02_design_toan_final.md`).

Cần bổ sung vào `04_design_toan_3d.md` (có thể làm chung 1 mục "PHẦN 7 —
Athena Manifest cho 3D", diễn giải riêng phần liên quan đến `structure[].id`):

1. **§7.1 Sandbox constraints** — không fetch/XHR mạng ngoài, không
   localStorage/cookie, không `eval`/`new Function`. Copy nguyên từ 2D, không
   cần diễn giải lại (không phụ thuộc kiến trúc layout).
2. **§7.3 Athena Manifest (`athena-context`)** — cần quy ước riêng cho 3D:
   `structure[].id` phải khớp với id của từng `step-tab`/`data-step` trong
   sidebar 3D (hiện đang dùng số thô `data-step="0..4"` — cần chốt format,
   ví dụ giữ số hoặc đổi `step0`, `step1`...).
3. **§7.4-7.6 Progress/Event/Complete/State** — copy nguyên logic, chỉ đổi
   ví dụ minh hoạ sang ngữ cảnh 3D (đổi step, kéo điểm, chọn mặt phẳng...).
4. **§7.9 Quy tắc đặt tên "Athena"** — bỏ hẳn "robot"/"AI" trong mọi lời
   thoại/nhãn/nhân vật, **áp dụng chung toàn hệ thống Toán 2D+3D** (2D đã có,
   3D chưa có dòng nào) — chỉ cần thêm 1 dòng trỏ chéo sang §7.9 của doc 2D,
   không cần viết lại.
5. **Quy tắc MCQ không trùng vị trí đáp án đúng giữa các câu** — đã có sẵn,
   đầy đủ, đúng vị trí ở `01_scenario_builder_3d_addendum.md` (dòng 31-63,
   mục "QUY TẮC TRẮC NGHIỆM MCQ BẮT BUỘC"). **Không cần chuyển vào
   `04_design_toan_3d.md`** — đây là quy tắc nội dung/kịch bản (Giai đoạn 1),
   không phải quy tắc thiết kế/layout (Giai đoạn 2). Chỉ cần thêm 1 dòng
   trỏ chéo trong `04_design_toan_3d.md` để người đọc biết quy tắc này tồn
   tại, tránh tưởng 3D không có ràng buộc gì về MCQ.
6. **Sửa dòng "Kế thừa" cuối file** — đổi tên file tham chiếu từ
   `02_design_toan_2.md` → `02_design_toan_final.md`, và ghi rõ **kế thừa đến
   phiên bản nào** (vd "kế thừa đến v2.3.1") để lần cập nhật sau biết ngay
   cần đối chiếu changelog từ mốc nào, không phải đọc lại toàn bộ doc 2D.

---

## 6. TÓM TẮT — Việc cần làm khi patch `04_design_toan_3d.md` lần tới

| # | Việc | Trạng thái |
|---|---|---|
| 1 | Xoá 3 preset Navy&Teal/Deep Space/Sky&White ở §Bước 1, thay bằng Jade/Cream cố định ở §1.2 | ⬜ Chưa làm |
| 2 | Thêm cảnh báo "dò hardcode color" sau §1.2 | ⬜ Chưa làm |
| 3 | Sửa §2.1: xoá `<h1>Tên bài học</h1>`, sửa gradient sang jade | ⬜ Chưa làm — cần xác nhận phạm vi áp dụng (mục 2) |
| 4 | §2.9b Resize LMS | ✅ Đã làm (bản gửi trước) |
| 5 | §2.9: bỏ ép `sidebar height:50%` mobile | ✅ Đã làm (bản gửi trước) |
| 6 | Thống nhất breakpoint 680px vs 768px | ⬜ Chưa quyết |
| 7 | Bàn riêng vùng chạm toggle switch | ⬜ Chưa quyết |
| 8 | Thêm PHẦN 7 Athena Manifest riêng cho 3D (7.1, 7.3-7.6, 7.9) | ⬜ Chưa làm |
| 9 | Thêm dòng trỏ chéo sang quy tắc MCQ ở scenario builder | ⬜ Chưa làm |
| 10 | Sửa dòng "Kế thừa" cuối file — tên file + version mốc | ⬜ Chưa làm |

---

## 7. Áp dụng vào 2 file HTML thật (`C5-Bai10`) — checklist riêng

- [ ] `KhaiNiemMoDau.html`: đã có bản preview Jade (`_JADE_v2.html`) — cần áp
      thêm §2.9b (bỏ `100vh`, thêm `resize()`) — **chưa làm trên file preview
      hiện tại**, mới làm màu + header.
- [ ] `GiaoTuyen.html`: **chưa bắt đầu** — cần làm lại toàn bộ pattern đã làm
      trên `KhaiNiemMoDau` (đổi `:root` + alias, dò hardcode color riêng của
      file này — chưa audit, có thể khác 22 chỗ đã tìm ở file kia, giữ header
      hiện, bỏ `<h1>`, thêm `min-height:320px` đang thiếu, thêm §2.9b).
