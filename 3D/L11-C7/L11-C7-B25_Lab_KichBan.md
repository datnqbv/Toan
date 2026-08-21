# 📚 KỊCH BẢN — Lab trải nghiệm Bài 25: "Phòng Lab Hình Học Không Gian"

```
📌 KHÔNG thuộc PPCT — Lab mở rộng (đã duyệt ở Bước 0), MỞ RỘNG trực tiếp
   trên file `solid_library.html` đã có (không dựng lại từ đầu — kho
   khối, mode-bar, catalog overlay đã đầy đủ).
🎯 Bổ sung 3 phần: (1) Mode "Đo góc nhị diện" mới, (2) Tính năng "Tính
   cạnh" cho các khối có công thức tham số (chóp cụt đều...), (3) Cảnh
   riêng "Trái Đất & Kinh tuyến" (hình cầu, không thuộc SOLID_LIBRARY
   dạng đa diện, cần scene riêng).
📁 File: mở rộng trực tiếp `solid_library.html` (không tạo file mới)
```

---

## PHẦN 1 — Mode mới: "Đo góc nhị diện"

**Vị trí trong mode-bar hiện có:** thêm 1 nút vào `#mode-bar`, cạnh các
nút Xem/Thêm điểm/Nối/Xoá/Hạ đường cao/Thiết diện đã có:

```html
<button class="mode-btn" id="mbtn-dihedral" onclick="setMode('dihedral')">
  <span class="mode-icon">◹</span> Đo góc nhị diện
</button>
```

**Thuật toán (đã verify bằng Node/THREE.js thật — khớp 100% với tứ diện
đều 70,53° và Hình 7.54 SGK 120°):**

```javascript
// Tái dùng đúng cấu trúc faces[]/edges[] đã có sẵn trong mỗi
// SOLID_LIBRARY[key] — KHÔNG cần thêm dữ liệu mới cho khối đã có.
function dihedralAngleFromFaces(faceA_verts, faceB_verts, sharedEdge) {
  const [A, B] = sharedEdge;
  const edgeDir = B.clone().sub(A).normalize();
  const O = A.clone().add(B).multiplyScalar(0.5); // điểm O — trung điểm
                                                     // cạnh chung, dùng
                                                     // để đặt nhãn góc
  const P = faceA_verts.find(v => !v.equals(A) && !v.equals(B));
  const Q = faceB_verts.find(v => !v.equals(A) && !v.equals(B));
  function perpComponent(v, base) {
    const AV = v.clone().sub(base);
    const proj = edgeDir.clone().multiplyScalar(AV.dot(edgeDir));
    return AV.clone().sub(proj); // thành phần vuông góc cạnh chung —
                                   // chính là hướng "tia dựng góc phẳng
                                   // nhị diện" tự động, không cần học
                                   // sinh tự kẻ
  }
  const v1 = perpComponent(P, A);
  const v2 = perpComponent(Q, A);
  const cosAngle = v1.dot(v2) / (v1.length() * v2.length());
  return Math.acos(Math.max(-1, Math.min(1, cosAngle))) * 180 / Math.PI;
}
```

**Thao tác trong mode này:**
1. Học sinh click vào 2 mặt kề nhau (chung 1 cạnh) của khối đang xem.
2. Hệ thống tự tìm cạnh chung, tự dựng 2 tia vuông góc cạnh chung tại
   điểm O (trung điểm cạnh), hiện rõ trên khối (2 đoạn mảnh + cung góc +
   label số đo).
3. Nếu 2 mặt được chọn KHÔNG chung cạnh (không kề nhau) → hệ thống báo
   "2 mặt này không có cạnh chung — không tạo thành góc nhị diện", không
   cho tính (chặn đúng thao tác vô nghĩa, nhắc lại điều kiện đã học ở
   Bài 25 Module 1).
4. Nút "Hiện/ẩn cách dựng" — toggle hiện rõ 2 tia + giải thích ngắn
   "đây là 2 tia vuông góc với cạnh chung, cùng xuất phát từ điểm O" (ôn
   lại đúng điều kiện Module 1 Bước 3).

⚠️ **Chưa verify bằng UI thật trong solid_library.html** (đã verify
thuật toán toán học bằng Node độc lập) — cần tích hợp thử với vài khối
trong catalog trước khi coi là hoàn thiện, đặc biệt các khối có mặt
không phải tam giác (tứ giác, lục giác — `perpComponent` vẫn đúng vì chỉ
cần 1 điểm không thuộc cạnh chung, nhưng cần chọn đúng điểm KHÔNG SUY
BIẾN, VD không cùng nằm trên đường kéo dài cạnh chung).

---

## PHẦN 2 — Tính năng "Tính cạnh" (cho khối có công thức tham số)

> Dành cho các khối mà 1 cạnh không đo trực tiếp được mà phải TÍNH từ
> các tham số khác — đặc biệt **hình chóp cụt đều** (Ví dụ 8 SGK, Hình
> 7.71): công thức cạnh bên = √(h² + (a−a')²/3).

**Thêm vào catalog:** 1 khối mới `frustum_regular` (chóp cụt đều) vào
`SOLID_LIBRARY`, tham số hoá đúng theo Ví dụ 8 SGK: chiều cao h, cạnh
đáy lớn a, cạnh đáy nhỏ a' (a > a').

**Bảng "Tính cạnh" xuất hiện cạnh khối (không phải mode riêng — chỉ hiện
khi khối đang xem có công thức tham số hoá):**

```
┌─ Tính cạnh bên chóp cụt đều ─────────────┐
│ Chiều cao h = [slider/nhập số]            │
│ Cạnh đáy lớn a = [nhập số]                │
│ Cạnh đáy nhỏ a' = [nhập số]                │
│                                            │
│ [Nút "Tính cạnh bên"] → hiện từng bước:   │
│   Bước 1: (a−a')² = ...                   │
│   Bước 2: (a−a')²/3 = ...                 │
│   Bước 3: h² + (a−a')²/3 = ...            │
│   Bước 4: √(...) = [kết quả]              │
│ → Khối 3D TỰ CẬP NHẬT đúng cạnh bên vừa   │
│   tính, học sinh xoay xem hình khớp không │
└────────────────────────────────────────────┘
```

- Verify Python: h=6, a=5, a'=3 → cạnh bên = 6,1101 — đã khớp đúng công
  thức SGK.
- **Không cho nhập thẳng đáp án cuối** — bắt buộc đi qua 4 bước hiện dần
  (giống nguyên tắc "chống dò mù" đã áp dụng toàn hệ thống), tránh học
  sinh chỉ bấm xem kết quả mà không hiểu công thức từ đâu ra.

**Áp dụng tương tự cho khối khác nếu cần tính cạnh** (tuỳ chọn mở rộng
sau): hình lập phương (đường chéo mặt = a√2, đường chéo khối = a√3),
hình hộp chữ nhật (đường chéo = √(a²+b²+c²)) — các công thức này ĐÃ có
sẵn dữ liệu cạnh trong catalog hiện tại, chỉ cần thêm panel "Tính cạnh"
tương tự nếu giáo viên muốn.

---

## PHẦN 3 — Cảnh riêng: "Trái Đất & Kinh tuyến" (làm rõ hơn Hình 7.57 SGK)

> ⚠️ **Vì sao cần scene riêng, không nhét vào SOLID_LIBRARY:** Trái Đất
> là hình CẦU (không phải đa diện — không có `faces`/`edges` dạng đỉnh
> rời rạc), và ý nghĩa sư phạm khác hẳn (minh hoạ 1 ỨNG DỤNG thực tế của
> góc nhị diện, không phải 1 khối để "phân loại/đo cạnh" như phần đa
> diện). SGK Hình 7.57 là ảnh TĨNH, phối cảnh cố định — Lab làm được hơn
> hẳn: xoay tự do 360°, kéo kinh tuyến qua P tuỳ ý, thấy rõ góc nhị diện
> động theo thời gian thực.

**Thêm 1 tab riêng trong Lab (ngoài catalog đa diện):** "🌍 Trái Đất &
Kinh tuyến"

**Cấu hình 3D (dùng đúng PHẦN 2.12 mới trong `05_threejs_engine.md` —
`createMeridianLine`, `createLatitudeCircle`, đã verify bằng Node):**
- 1 hình cầu bán kính R=5 (đơn vị mô phỏng), lưới kinh tuyến/vĩ tuyến mờ
  (`--paper-line`, giống lưới địa cầu thật) để định hướng khi xoay.
- Trục Bắc-Nam Δ vẽ rõ (đường đậm xuyên tâm, 2 đầu ghi "Bắc"/"Nam").
- Xích đạo vẽ rõ (đường tròn lớn quanh "bụng" hình cầu).
- **Kinh tuyến gốc:** 1 nửa đường tròn lớn từ cực Bắc xuống cực Nam, cố
  định tại kinh độ 0°, tô đậm (VD `--jade`).
- **Kinh tuyến qua P:** 1 nửa đường tròn lớn khác, kéo được bằng slider
  kinh độ (0°-180°, cả Đông/Tây), tô màu khác (VD `--accent`).
- Tại tâm O (tâm Trái Đất), 2 tia vuông góc trục Δ tự động dựng — nằm
  trên mặt xích đạo, mỗi tia hướng theo kinh tuyến tương ứng (verify
  Python: kinh độ 45° → góc đo giữa 2 tia = đúng 45°, khớp tuyệt đối).
- Cung góc + label số đo kinh độ hiện ngay tại O.

**Thao tác:**
1. Học sinh kéo slider kinh độ — kinh tuyến qua P (màu accent) quét
   quanh trục Δ, góc nhị diện tại O cập nhật theo thời gian thực.
2. Xoay camera tự do 360° — quan sát rõ từ mọi góc (khác hẳn ảnh SGK chỉ
   có 1 góc nhìn cố định), đặc biệt xoay để nhìn "từ trên xuống" (nhìn
   dọc theo trục Δ) sẽ thấy góc nhị diện hiện y như 1 góc phẳng thông
   thường trên "mặt đồng hồ" xích đạo — giúp học sinh nối lại trực giác
   2D quen thuộc với khái niệm 3D mới học.
3. Nút "Đặt về Đảo Trường Sa Lớn" (111,92°) — nhảy nhanh về đúng số liệu
   đã dùng ở Module 1, để học sinh đối chiếu lại.
4. Toggle "hiện/ẩn lưới kinh vĩ tuyến phụ" — mặc định ẩn (đỡ rối mắt),
   bật khi cần cảm giác "địa cầu thật" hơn.

⚠️ **Đã có pattern chính thức (PHẦN 2.12, chưa verify HTML thật)** — công
thức đã verify bằng Node (three thật qua npm): kinh tuyến gốc/45° tại
xích đạo cho đúng 45,0000°, vĩ tuyến 30° khớp đúng bán kính/độ cao lý
thuyết. Cần prototype nhỏ để test hiển thị/hiệu ứng ánh sáng lên các
đường Line mảnh và tương tác slider thật trên trình duyệt, trước khi
build chính thức vào Lab.

---

## PHẦN 4 — Bổ sung 2 preset khối theo đúng SGK (để "trải nghiệm tất cả các hình")

> Theo yêu cầu "những hình vẽ trong SGK cần làm trực quan và xoay được
> rõ hơn" — thêm 2 preset MỚI vào catalog (khác các preset trừu tượng đã
> có), khớp đúng cấu hình Hình 7.54 và Hình 7.71 SGK để học sinh có thể
> tự tay xoay xem đúng hình đã học trên giấy, kiểm chứng lại bằng mode
> "Đo góc nhị diện" và "Tính cạnh" vừa thêm.

| Preset mới | Khớp hình SGK | Dùng để luyện |
|---|---|---|
| "Chóp đáy hình thoi (SA⊥đáy)" | Hình 7.54, Ví dụ 4 | Đo góc nhị diện [B,SA,D] (kỳ vọng 120°, đã verify) |
| "Chóp cụt đều (tính cạnh bên)" | Hình 7.71, Ví dụ 8 | Tính cạnh bên bằng công thức tham số (Phần 2 trên) |

---

## PHẦN 5 — "Lướt qua tính chất": chuỗi 5 hình lăng trụ/hộp đặc biệt (Mục 5 SGK)

> ⚠️ **Rà lại catalog hiện có, phát hiện thiếu 1 mắt xích:** SOLID_LIBRARY
> đã có "Hình hộp chữ nhật" (`hop_chu_nhat`) và "Hình hộp xiên"
> (`hop_xien` — thực ra đáy vẫn là HÌNH CHỮ NHẬT, chỉ cạnh bên xiên,
> không phải hình bình hành tổng quát) — nhưng **THIẾU đúng "Hình hộp
> ĐỨNG"** theo định nghĩa SGK (c): lăng trụ đứng có đáy là HÌNH BÌNH HÀNH
> (không vuông, không phải chữ nhật). Cần thêm preset mới `hop_dung`.

### Preset mới cần thêm: `hop_dung` (Hình hộp đứng)

```javascript
hop_dung: {
  info: {
    name: 'Hình hộp đứng',
    notation: "ABCD.A'B'C'D'",
    desc: 'Lăng trụ đứng có đáy là HÌNH BÌNH HÀNH (không vuông) — cạnh bên vuông góc 2 đáy, nhưng đáy KHÔNG phải hình chữ nhật.'
  },
  params: [
    { id:'h',    label:'Chiều cao (h)',  min:.5, max:5, step:.1, val:3   },
    { id:'ab',   label:'Cạnh AB',        min:.5, max:5, step:.1, val:3   },
    { id:'ad',   label:'Cạnh AD',        min:.5, max:4, step:.1, val:2.2 },
    { id:'skewBase', label:'Độ nghiêng đáy (làm ABCD thành bình hành không vuông)', min:0, max:2, step:.1, val:1 }
  ],
  vertices(p) {
    const { h, ab, ad, skewBase } = p;
    const A = [0,0,0], B = [ab,0,0], D = [skewBase, 0, ad], C = [ab+skewBase, 0, ad];
    return { A, B, C, D,
      A1:[A[0],h,A[2]], B1:[B[0],h,B[2]], C1:[C[0],h,C[2]], D1:[D[0],h,D[2]] };
  },
  // edges/faces/explore/baseVertices: giống hop_chu_nhat (cấu trúc đỉnh
  // ABCD.A'B'C'D' đồng dạng), chỉ khác công thức vertices() ở trên
},
```

> **Verify đã thực hiện (Python):** với `skewBase=1`, ABCD đúng là hình
> bình hành thật (AB ∥ DC, AD ∥ BC) và KHÔNG vuông (AB·AD ≠ 0) — khác
> hẳn `hop_chu_nhat`/`hop_xien` đều có đáy hình chữ nhật.

### Tour "Lướt qua tính chất" — 5 bước cố định, đi từ tổng quát → đặc biệt

> Đúng mạch HĐ6→HĐ10 của SGK Mục 5 — mỗi bước chỉ tăng thêm 1 điều kiện
> so với bước trước, học sinh thấy rõ "đặc biệt hơn" nghĩa là gì.

| Bước | Khối hiện | Điều kiện MỚI so với bước trước | Câu hỏi lướt nhanh (không chấm gắt) |
|---|---|---|---|
| 1 | Lăng trụ tam giác đứng (đáy thường) | Cạnh bên ⊥ đáy | "Mặt bên là hình gì? Có vuông góc đáy không?" → hình chữ nhật, có |
| 2 | Lăng trụ tam giác ĐỀU | + đáy là đa giác đều | "Các mặt bên có cùng kích thước không?" → có, đều là hình chữ nhật bằng nhau |
| 3 | **Hình hộp đứng** (preset mới) | Đổi đáy sang hình bình hành (4 cạnh, không cần đều) | "Trong 6 mặt, ÍT NHẤT bao nhiêu mặt là hình chữ nhật?" → ít nhất 4 (các mặt bên), 2 đáy có thể KHÔNG phải chữ nhật |
| 4 | Hình hộp CHỮ NHẬT | + đáy là hình chữ nhật (không chỉ bình hành) | "Giờ cả 6 mặt là hình gì? Đường chéo có tính chất gì?" → cả 6 mặt là hình chữ nhật; 4 đường chéo bằng nhau, cắt tại 1 điểm (dùng lại kết quả đã verify ở Module 3 Bước 3) |
| 5 | Hình LẬP PHƯƠNG | + tất cả cạnh bằng nhau | "Tất cả 6 mặt giờ là hình gì?" → hình vuông |

**Thao tác:** mỗi bước chỉ cần xoay khối hiện tại, trả lời nhanh câu hỏi
(không chấm điểm gắt, chỉ hiện gợi ý ngay), bấm "Bước tiếp" để khối tự
đổi sang preset kế tiếp (giữ nguyên góc camera đang xoay, không reset về
góc mặc định — để học sinh thấy rõ sự "thu hẹp dần" liền mạch, không bị
ngắt cảm giác giữa các bước).

**Chốt tour:** "Đây là chuỗi 5 hình đặc biệt hoá dần: Lăng trụ đứng ⊃
Lăng trụ đều, và Lăng trụ đứng ⊃ Hình hộp đứng ⊃ Hình hộp chữ nhật ⊃
Hình lập phương. Mỗi mũi tên thêm ĐÚNG 1 điều kiện — không hình nào tự
động suy ra hình sau nó."

---

- **"Tìm góc nhị diện lớn nhất trong khối này"** — với MỖI khối trong
  catalog, có 1 nút "Thử thách" (tuỳ chọn, không bắt buộc): hệ thống yêu
  cầu học sinh dùng mode "Đo góc nhị diện" đo hết các cặp mặt kề nhau,
  tìm ra cặp có góc LỚN NHẤT. Không có "đáp án" cố định hiện sẵn — hệ
  thống tự so sánh các lần đo học sinh đã thực hiện, xác nhận khi đã đo
  đủ và đúng cặp lớn nhất.

## Rủi ro kỹ thuật 3D (tổng hợp cả Lab)

```
✅ An toàn: tái dùng toàn bộ mode-bar, catalog overlay, SOLID_LIBRARY đã
   có trong solid_library.html — không đổi kiến trúc gốc.
✅ An toàn (đã verify thuật toán): Mode "Đo góc nhị diện" — công thức
   projection đã verify khớp 100% qua Node/THREE.js thật (tứ diện đều
   70,53°, Hình 7.54 120°).
✅ An toàn (đã verify công thức): "Tính cạnh" chóp cụt đều — verify bằng
   Python, khớp đúng Ví dụ 8 SGK.
✅ An toàn (đã verify công thức): preset mới `hop_dung` (Hình hộp đứng,
   đáy hình bình hành) — verify bằng Python, đáy đúng là bình hành không
   vuông, cạnh bên đúng vuông góc đáy. Cấu trúc `vertices()` đồng dạng
   `hop_chu_nhat` đã có, rủi ro tích hợp thấp.
✅ Đã có pattern chính thức (chưa verify HTML thật): dựng lưới kinh/vĩ
   tuyến cho cảnh "Trái Đất" — PHẦN 2.12 (05_threejs_engine.md), dùng
   `THREE.EllipseCurve` (core, không cần thư viện thêm). Đã verify bằng
   Node — góc kinh tuyến 45° khớp đúng 45,0000°, vĩ tuyến 30° khớp đúng
   bán kính/độ cao lý thuyết.
⚠️ Cần kiểm tra khi build Mode "Đo góc nhị diện": với các khối có mặt
   TỨ GIÁC/LỤC GIÁC (không chỉ tam giác), hàm `perpComponent` cần chọn
   đúng 1 điểm không suy biến (không nằm trên đường kéo dài cạnh chung)
   — với đa giác lồi đều, chọn đỉnh XA cạnh chung nhất là an toàn nhất.
✅ An toàn: tour "Lướt qua tính chất" — chỉ chuyển đổi preset đã có sẵn
   (+ 1 preset mới `hop_dung`), không cần animation phức tạp, giữ
   nguyên góc camera giữa các bước (chỉ đổi `SOLID_LIBRARY[key]` đang
   active, dựng lại mesh, không reset `camera.position`).
```

---

> **Trạng thái:** Lab đã có kịch bản đầy đủ 5 phần bổ sung (mode đo góc
> nhị diện, tính năng tính cạnh, cảnh Trái Đất riêng, 2 preset khớp SGK,
> tour "Lướt qua tính chất" 5 hình lăng trụ/hộp đặc biệt kèm 1 preset mới
> `hop_dung` bù đúng mắt xích còn thiếu) + 1 nhiệm vụ nhỏ, mở rộng trực
> tiếp trên `solid_library.html` có sẵn. Toàn bộ công thức đã verify
> bằng Python/Node. **Bài 25 đã hoàn tất cả 4 module + Lab.**
