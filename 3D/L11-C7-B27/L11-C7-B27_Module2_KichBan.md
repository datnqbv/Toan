# 📚 KỊCH BẢN — Bài 27, Module 2: "Luyện tập tổng hợp tính thể tích"

```
📖 PPCT: Tiết 78 — Chủ đề 11: Thể tích (Luyện tập tổng hợp)
🔗 Điều kiện tiên quyết: Module 1.
🎯 Vai trò: học sinh đóng 2 vai nghề nghiệp lần lượt — KỸ SƯ XÂY DỰNG
   (Bước 1-2: tính khối lượng bê tông, kỹ thuật tỉ số thể tích) và NHÀ
   THIẾT KẾ (Bước 3-4: khuôn bánh, chậu gốm bonsai — dự án so sánh
   phương án).
🎯 Sai lầm nhắm tới (PPCT):
   (F) quên nhân hệ số 1/3 khi tính thể tích khối chóp
   (G) sai đơn vị đo khi chuyển đổi cm³/m³/lít
   (H) lẫn lộn thể tích khối lăng trụ và khối chóp
   (I) dùng tỉ số thể tích (Simpson) SAI cho chóp KHÔNG phải tam giác
       (chóp tứ giác phải chia thành 2 chóp tam giác trước)
   (J) quên đơn vị khối của thể tích (VD a³)
📁 File: Bai27_Toan3D_Module2_LuyenTapTheTich.html
```

> ⚠️ **Bối cảnh:** Bước 3 dùng **"Cô Mai làm khuôn bánh"** (đổi khỏi "bác
> Hùng cắt tôn" — nhân vật này đã dùng ở Bài 25 cho kỹ thuật cắt-gấp
> tương tự, đổi cả nhân vật và vật liệu). Bước 4 dùng **"Xưởng gốm bonsai
> nhiều hình thù"** (dự án so sánh phương án, đúng PPCT gợi ý "Thiết kế
> bao bì tối ưu" nhưng đổi sang bối cảnh gốm bonsai).

## Sổ tay kiến thức (module LUYỆN TẬP — sổ tay đầy đủ ngay từ đầu)

```
- V(khối chóp) = (1/3)·S·h — LUÔN có hệ số 1/3, dễ quên khi vội.
- V(khối lăng trụ) = S·h — KHÔNG có hệ số 1/3.
- V(khối chóp cụt đều) = (1/3)·(S+S'+√(S·S'))·h.
- Đổi đơn vị thể tích: 1 m³ = 1.000.000 cm³ (= 100³, KHÔNG phải ×100).
  1 lít = 1.000 cm³ = 1 dm³.
- Tỉ số thể tích (Simpson): CHỈ áp dụng trực tiếp cho CHÓP TAM GIÁC (tứ
  diện) — V(S.MNP)/V(S.ABC) = (SM/SA)·(SN/SB)·(SP/SC). Với chóp TỨ GIÁC
  trở lên, PHẢI chia thành các chóp tam giác trước, áp dụng riêng từng
  phần, rồi cộng lại — KHÔNG nhân trực tiếp 4 tỉ số.
```

---

## PHẦN A — Kỹ sư xây dựng

### Bước 1 — Tính khối lượng bê tông (nhắm sai lầm G, J)

**Đề bài:** "Móng cột dạng chóp cụt đều: đáy dưới vuông cạnh 2m, đáy trên
vuông cạnh 1,2m, cao 1,5m. Tính thể tích bê tông cần, và khối lượng (biết
khối lượng riêng bê tông ≈ 2.400 kg/m³)."

**Cấu hình 3D (bổ sung — bản gốc thiếu hẳn phần này):**
- Móng cột chóp cụt đặt trong 1 "hố móng" đơn giản (viền đất `--il-sand`
  tô mờ xung quanh đáy, gợi công trường thật).
- Bên trong khối bê tông, vẽ thêm 4-6 đường lưới thép mảnh (`--il-ochre`,
  nét đứt) chạy dọc theo chiều cao — chi tiết nhỏ nhưng tăng cảm giác
  "công trình xây dựng thật", không chỉ là 1 khối hình học trơn.
- Nhãn S (đáy dưới) và S' (đáy trên) hiện rõ dạng tô mờ 2 màu khác nhau
  (`--jade-pale` cho S, `--accent-pale` cho S') khi học sinh tính từng
  bước — giúp phân biệt ngay 2 đại lượng dễ nhầm.

- Verify Python: V = 3,92m³ → khối lượng = 9.408kg ≈ 9,408 tấn.

**Thao tác — lời Athena + hành động:**

1. Học sinh tính S, S', √(S·S'), rồi V theo công thức chóp cụt — hệ
   thống chặn từng bước (không cho nhảy tới đáp án).
2. Đổi V sang khối lượng — nhân khối lượng riêng.

3. **3-strike (nhắm trực diện sai lầm G):** "1 bạn học sinh khác tính
   được V = 3.920.000 cm³, rồi đổi sang m³ bằng cách CHIA CHO 100, ra
   39.200 m³. Kết quả này đúng hay sai?"
   - `dap_an_dung`: "Sai — 1 m³ = 1.000.000 cm³ (100×100×100), không
     phải 100. Phải chia cho 1.000.000, ra đúng 3,92 m³ (khớp kết quả
     tính trực tiếp bằng mét)."
   - `goi_y_khi_sai`: "1 mét = 100cm. Vậy 1 m³ = 100×100×100 cm³ = ?"

### Bước 2 — Kỹ thuật tỉ số thể tích Simpson (nhắm trực diện sai lầm I)

**Đề bài:** "Cho chóp tứ giác đều S.ABCD, đáy vuông cạnh 4, cao 6. Các
điểm M, N, P, Q trên SA, SB, SC, SD với tỉ lệ SM/SA=0,5; SN/SB=0,7;
SP/SC=0,5; SQ/SD=0,3. Tính thể tích khối S.MNPQ."

**Cấu hình 3D (bổ sung — QUAN TRỌNG NHẤT của cả module, bản gốc chỉ định
"hiện 2 số cạnh nhau" mà bỏ lỡ hình ảnh mạnh nhất):**
- Chóp S.ABCD dựng đầy đủ, đáy tô mờ `--il-sand`.
- **Đường chéo AC** vẽ rõ (nét đậm `--jade`) — đây là "lát cắt" chia đáy
  thành 2 tam giác. Kèm mặt phẳng phụ trợ (SAC) tô mờ rất nhẹ để thấy rõ
  đây là mặt chia đôi khối chóp.
- **2 tứ diện sau khi chia** tô 2 màu ĐỐI LẬP rõ ràng: S.ABC = `--il-dusty-blue`
  (opacity 0,35), S.ACD = `--il-olive` (opacity 0,35) — học sinh nhìn
  ngay "khối tứ giác gồm đúng 2 khối tam giác ghép lại", không cần suy
  diễn trừu tượng.
- Điểm M, N, P, Q đánh dấu rõ trên 4 cạnh bên (chấm `--accent`, kèm nhãn
  R1 hiện tỉ lệ SM/SA... ngay cạnh điểm).
- **Đường chéo MP** (tương ứng AC nhưng ở "tầng" các điểm M,N,P,Q) vẽ
  bằng nét đứt `--jade` — cho thấy khối S.MNPQ CŨNG được chia đúng theo
  cùng quy tắc (S.MNP thuộc phần dusty-blue, S.MPQ thuộc phần olive).
- Nút "Bật/tắt chia tứ diện" — cho học sinh tự bật/tắt để so sánh hình
  TRƯỚC và SAU khi hiểu ra cách chia, tăng tính khám phá.

- Verify Python: V(S.ABCD)=32. V(S.MNPQ) ĐÚNG (chia 2 tứ diện S.MNP +
  S.MPQ theo đường chéo MP) = **4,0**. Nếu SAI áp trực tiếp tích 4 tỉ số
  (0,5×0,7×0,5×0,3×32) = **1,68** — lệch tới **58%**.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Với chóp TAM GIÁC, công thức Simpson cho tỉ số thể tích
   trực tiếp bằng tích 3 tỉ số cạnh. Với chóp TỨ GIÁC S.ABCD này, có thể
   áp dụng trực tiếp tích 4 tỉ số (SM/SA)(SN/SB)(SP/SC)(SQ/SD) không?"
   - *Hành động HS:* thử tính cả 2 cách, hệ thống hiện song song 2 kết
     quả (4,0 vs 1,68) để thấy rõ sự khác biệt LỚN.

2. **Giải thích đúng:** "Công thức Simpson CHỈ đúng cho tứ diện (chóp
   tam giác) — vì đó là trường hợp CHỨNG MINH được bằng tỉ số 3 cạnh độc
   lập. Với chóp tứ giác, PHẢI chia thành 2 chóp tam giác (S.ABC và
   S.ACD qua đường chéo AC), tính riêng tỉ số cho mỗi phần theo đúng các
   điểm M,N,P (thuộc phần 1) và M,P,Q (thuộc phần 2), rồi CỘNG LẠI — cho
   ra đúng 4,0, khác hẳn cách nhân tắt 4 tỉ số (1,68)."

3. **3-strike:** "Vì sao KHÔNG thể áp dụng trực tiếp tích 4 tỉ số cho
   chóp tứ giác?"
   - `dap_an_dung`: "Vì công thức Simpson dựa trên tính chất hình học
     riêng của TỨ DIỆN (3 cạnh từ 1 đỉnh xác định duy nhất hình dạng) —
     chóp tứ giác có THÊM 1 đỉnh, không còn tính chất đó, phải quy về
     tứ diện bằng cách chia nhỏ trước."

---

## PHẦN B — Nhà thiết kế

### Bước 3 — Cô Mai làm khuôn bánh (chóp cụt, nhắm sai lầm H)

**Đề bài:** "Cô Mai làm khuôn bánh kim loại dạng chóp cụt đều: đáy lớn
(miệng khuôn) cạnh 18cm, đáy nhỏ (đáy khuôn) cạnh 10cm, cao 8cm. Tính
dung tích khuôn (đổi ra lít) và độ dài cạnh bên cần khi gấp kim loại."

**Cấu hình 3D (bổ sung):**
- Khuôn bánh dựng bằng vật liệu "kim loại" sáng (`#c7ccd1`, ánh kim nhẹ
  qua `metalness` nếu build hỗ trợ — nếu không, dùng màu sáng + viền đậm
  để gợi cảm giác kim loại).
- **Animation "trải phẳng"** (tuỳ chọn, tăng trực quan): 1 nút "Xem tấm
  kim loại gốc" — khối khuôn "mở bung" thành hình khai triển phẳng (4
  mặt bên trải ra như hoa), giúp học sinh thấy rõ vì sao cạnh bên cần
  tính đúng độ dài trước khi cắt-gấp thật. Bấm lại để "gấp về" hình chóp
  cụt.
- Sau khi tính dung tích, đổ 1 lớp "bột bánh" màu vàng nhạt (`--accent-pale`)
  lấp đầy khuôn tới đúng miệng — minh hoạ trực quan con số "1,61 lít" vừa
  tính ra, không chỉ là số trừu tượng.

- Verify Python: cạnh bên = 9,2376cm (dùng công thức Bài 25 Ví dụ 8:
  √(h²+(a−a')²/3)). V = 1.610,67cm³ ≈ **1,61 lít**.

**Thao tác — lời Athena + hành động:**

1. Học sinh tính cạnh bên trước (cần cho việc GẤP kim loại thật), rồi
   tính thể tích (cần cho việc BIẾT DUNG TÍCH bánh nướng ra).

2. **3-strike (nhắm sai lầm H):** "Nếu cô Mai lỡ dùng công thức V=S·h
   (công thức LĂNG TRỤ) cho khuôn bánh hình chóp cụt này, kết quả sẽ
   sai theo hướng nào?"
   - `dap_an_dung`: "Sai — TĂNG quá mức, vì S·h (dùng đáy lớn 18×18=324
     nhân cả chiều cao) sẽ luôn LỚN HƠN công thức chóp cụt đúng (khối
     chóp cụt THU NHỎ dần lên trên, luôn ít thể tích hơn 1 lăng trụ cùng
     đáy lớn và cùng cao)."

### Bước 4 — Xưởng gốm bonsai: so sánh 3 phương án thiết kế (dự án tổng kết)

**Đề bài:** "Xưởng gốm cần chọn 1 trong 3 phương án chậu bonsai (cùng
chiều cao 15cm) để sản xuất — cần thể tích đất trồng NHIỀU nhất, tốn ít
đất nung nhất (ước lượng qua diện tích đáy lớn)."

**Cấu hình 3D (bổ sung):**
- 3 chậu (A, B, C) đặt CẠNH NHAU trên 1 mặt bàn xưởng gốm (`--il-sand`
  tô mờ), đúng 3 màu đã định trong bảng (`--il-terracotta`,
  `--il-dusty-blue`, `--il-ochre` — điều chỉnh: dùng đúng 3 màu đối lập
  rõ để không nhầm khi nhìn cạnh nhau).
- Mỗi chậu có 1 chấm xanh nhỏ (`--il-olive`) ở giữa miệng chậu, tượng
  trưng 1 cây bonsai tí hon — chi tiết nhỏ giúp bối cảnh "chậu cây" thật
  hơn hẳn 3 khối hình học trơn.
- Nhãn nổi (R1) trên mỗi chậu hiện luôn 2 số: thể tích và diện tích đáy
  lớn — để so sánh trực tiếp bằng mắt, không cần lật bảng riêng.
- Khi học sinh trả lời đúng "phương án tối ưu" (Phương án A), chậu đó có
  hiệu ứng viền sáng nhẹ (đổi màu viền sang `--jade`) để xác nhận, 2 chậu
  còn lại giữ nguyên.

| Phương án | Hình dạng | Đáy lớn (cm) | Đáy nhỏ (cm) | Thể tích | Diện tích đáy lớn |
|---|---|---|---|---|---|
| A | Chóp cụt đều | 20 | 14 | **4.380 cm³** | 400 |
| B | Lăng trụ đứng | 16 | (không thu nhỏ) | 3.840 cm³ | 256 |
| C | Chóp cụt đều (dốc hơn) | 22 | 10 | 4.020 cm³ | 484 |

- Verify Python: đã tính đúng cả 3.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Nhìn bảng trên — phương án nào có đáy lớn NHẤT? Phương
   án đó có thể tích LỚN NHẤT không?"
   - *Hành động HS:* quan sát: Phương án C có đáy lớn nhất (484) nhưng
     thể tích lại KHÔNG lớn nhất (4.020 < 4.380 của phương án A).
   - 🎯 **Mục tiêu quan sát (phát hiện phản trực giác):** đáy lớn KHÔNG
     đồng nghĩa thể tích lớn — vì phương án C "dốc" nhiều (thu nhỏ nhanh
     từ 22 xuống 10), làm giảm thể tích tổng dù đáy khởi điểm lớn hơn.

2. **Athena hỏi tiếp:** "Xưởng muốn thể tích đất trồng nhiều NHƯNG tốn ít
   đất nung (đáy lớn nhỏ) — phương án nào tối ưu nhất theo 2 tiêu chí
   này?"
   - `dap_an_dung`: "Phương án A — thể tích LỚN NHẤT (4.380) trong khi
     diện tích đáy lớn (400) còn nhỏ hơn hẳn phương án C (484) — vừa lợi
     về thể tích, vừa tiết kiệm vật liệu hơn C."
   - Ghi chú: phương án B (lăng trụ) tốn ít vật liệu nhất (đáy chỉ 256)
     nhưng thể tích lại thấp nhất — mỗi phương án có ưu/nhược riêng, đây
     là bài toán ĐA TIÊU CHÍ, không có "đáp án tuyệt đối" mà cần cân
     nhắc theo mục tiêu ưu tiên của xưởng.

3. **Chốt dự án:** Athena tổng hợp bảng so sánh cuối, để học sinh tự
   chọn phương án theo tiêu chí ưu tiên riêng (không có 3-strike ép chọn
   1 đáp án duy nhất — đây là bài toán mở, rèn năng lực mô hình hoá và ra
   quyết định đa tiêu chí, đúng PPCT).

---

## TỔNG HỢP KIẾN THỨC (đóng Module 2 — đóng cả Bài 27)

| Phần | Nội dung | Nhắm sai lầm |
|---|---|---|
| A.1 — Kỹ sư xây dựng | Đổi đơn vị thể tích đúng (1m³=1.000.000cm³) | G, J |
| A.2 — Kỹ sư xây dựng | Tỉ số Simpson chỉ đúng cho tứ diện, chóp tứ giác phải chia nhỏ | I |
| B.3 — Nhà thiết kế | Không nhầm chóp cụt với lăng trụ (S·h luôn lớn hơn công thức đúng) | H |
| B.4 — Nhà thiết kế | Bài toán đa tiêu chí — đáy lớn ≠ thể tích lớn | Tổng hợp |

## Đặc tả hình ảnh & màu sắc (bổ sung sau rà soát — module gốc thiếu hẳn phần "Cấu hình 3D" ở cả 4 bước, chỉ có bảng số/text)

**Hook mở đầu module (SVG viewBox 0 0 500 280, chia 2 nửa theo 2 vai):**
```
- Nửa trái "Kỹ sư xây dựng": 1 mũ bảo hộ (--il-slate) + 1 bay trát vữa
  nhỏ chéo góc, cạnh 1 khối chóp cụt bê tông thu nhỏ (--il-slate đậm).
- Nửa phải "Nhà thiết kế": 1 khuôn bánh chóp cụt nhỏ (--il-ochre nhạt,
  như kim loại) + 1 chậu cây bonsai tí hon (--il-terracotta) kèm 1 chấm
  xanh nhỏ (--il-olive) làm cây con.
- Giữa 2 nửa: 1 mũi tên cong nhẹ (--jade) nối 2 bên, gợi "cùng 1 công cụ
  — công thức thể tích — dùng cho 2 nghề khác nhau".
```

**Bảng màu (giữ nguyên, bổ sung 2 dòng):**

| Đối tượng | Token | Vai trò |
|---|---|---|
| Khối bê tông/khuôn bánh (đối tượng chính) | `--il-slate` hoặc màu vật liệu thật (xám bê tông `#8a9199`, kim loại khuôn `#c7ccd1`) | Đối tượng đang tính |
| Đường/mặt phụ trợ (S,S' tô mờ, đường chéo chia tứ diện) | `--jade` | Kết quả/đường dựng thêm |
| Khối SAI trong bẫy (naive Simpson, lăng trụ nhầm) | `--accent` nét đứt | Minh hoạ sai để so sánh |
| 3 phương án chậu gốm (Bước 4) | 3 màu khác nhau (`--il-terracotta`, `--il-ochre`, `--il-dusty-blue`) | Phân biệt rõ 3 phương án khi đặt cạnh nhau |
| Tứ diện S.ABC (Bước 2, phần chia 1) | `--il-dusty-blue`, tô mờ opacity 0.35 | Phân biệt 2 phần chia của chóp tứ giác |
| Tứ diện S.ACD (Bước 2, phần chia 2) | `--il-olive`, tô mờ opacity 0.35 | Phân biệt rõ với phần chia 1 (màu đối lập) |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: Bước 1, 4 — dựng hình tĩnh + tô màu/nhãn, không cần pattern
   3D mới.
⚠️ Cần chú ý khi build Bước 2 (chia 2 tứ diện trực quan): cần dựng đúng
   mặt phẳng phụ trợ (SAC) và đường chéo MP tương ứng — về kỹ thuật chỉ
   là vẽ thêm 2-3 mặt/đường tô màu, KHÔNG cần pattern 3D mới, nhưng cần
   đội build đối chiếu kỹ đúng 4 điểm M,N,P,Q theo toạ độ đã verify
   (Python) để 2 tứ diện tô màu khớp chính xác hình dạng thật, không chỉ
   là "trang trí gần đúng".
✅ Đã có pattern + đã verify qua prototype thật: Bước 3 (animation trải
   phẳng khuôn bánh) — PHẦN 2.15 (05_threejs_engine.md), tái dùng kỹ
   thuật bản lề đã có, KHÔNG cần viết từ đầu. Đã bắt và sửa 1 lỗi dấu
   xoay thật trong quá trình verify (2 mặt gập lộn xuống dưới sàn nếu
   dùng sai công thức dấu) — đã sửa và verify lại đủ cả 4 mặt. Vẫn giữ
   nguyên là phần TUỲ CHỌN (không bắt buộc build) theo đúng đánh giá ban
   đầu, nhưng nếu build thì đã có code tham khảo đầy đủ, giảm rủi ro hơn
   hẳn so với để đội build tự mò từ đầu.
```

---

> **Trạng thái:** Module 2 (Bài 27) đã có kịch bản đầy đủ 4 bước (2 vai
> nghề nghiệp), số liệu đã verify bằng Python — đặc biệt bẫy Simpson cho
> chênh lệch 58% (rất thuyết phục), và phát hiện phản trực giác ở Bước 4
> (đáy lớn không đồng nghĩa thể tích lớn). Đã rà soát và bổ sung đầy đủ
> "Cấu hình 3D" cho cả 4 bước (bản gốc thiếu hoàn toàn phần này) + hook
> mở đầu module — đặc biệt Bước 2 giờ có hình ảnh trực quan chia 2 tứ
> diện (trước đó chỉ là bảng số). **Bài 27 đã hoàn tất cả 2 module.**
> Trang "Tổng hợp trực quan" cuối bài (theo yêu cầu ban đầu) sẽ ra kịch
> bản ở phiên tiếp theo.
