# 📚 KỊCH BẢN — Bài 26, Module 3: "Dự án thiết kế cầu thang xoắn" (Kiến trúc sư kết cấu)

```
📖 PPCT: Tiết 76 — Chủ đề 10: Khoảng cách (Luyện tập tổng hợp)
🔗 Điều kiện tiên quyết: Module 1, 2.
🎯 Vai trò: học sinh nhập vai KIẾN TRÚC SƯ KẾT CẤU, nhận dự án thiết kế
   cầu thang xoắn nối 2 tầng — cần tính nhiều loại khoảng cách khác nhau
   để hoàn thiện và kiểm định bản vẽ trước khi trình duyệt.
🎯 Sai lầm nhắm tới (PPCT):
   (J) nhầm lẫn giữa các loại khoảng cách khi bài toán có nhiều đối
       tượng đan xen
   (K) sai sót trong bước dựng hình phụ khiến tính toán bị sai theo
   (L) áp dụng sai Pytago/hệ thức lượng ở bước tính trung gian
   (M) quên kiểm tra tam giác có thực sự vuông tại đỉnh mình nghĩ hay
       không
   (N) phân bổ thời gian kém, sa đà vào câu quá khó
📁 File: Bai26_Toan3D_Module3_CauThangXoan.html
```

> ⚠️ **Số liệu dự án** (đã verify bằng Node/THREE.js thật): bán kính cầu
> thang R=1,0m; chiều cao mỗi bậc (rise) = 0,17m (trong chuẩn 15-18cm);
> góc xoay mỗi bậc = 30° (12 bậc/vòng — số chia phổ biến cho cầu thang
> xoắn thực tế). Chuẩn đối chiếu: **QCXDVN 05:2008/BXD — chiều cao thông
> thuỷ cầu thang tối thiểu 2m.**

## Khung nhập vai (mở đầu module)

**Athena (vào vai ngay, không dẫn nhập dài dòng):**

> "Chào kiến trúc sư! Dự án cầu thang xoắn nối tầng 1 và tầng 2 đã có
> bản phác thảo — bán kính 1m, mỗi bậc cao 17cm, xoay 30° mỗi bậc. Trước
> khi trình duyệt, cần kiểm định 4 loại khoảng cách khác nhau để đảm bảo
> an toàn và đúng chuẩn xây dựng. Bắt đầu với kiểm định đầu tiên."

---

## Đặc tả hình ảnh & màu sắc (bổ sung sau rà soát — áp dụng token có sẵn)

**Hook mở đầu module (SVG viewBox 0 0 400 400, isometric nhẹ):**
```
- Cầu thang xoắn cách điệu nhìn từ trên: các bậc là những đoạn ngắn toả
  ra từ tâm theo hình xoắn ốc (mỗi bậc --il-terracotta, xen 1 bậc
  --il-sand để dễ phân biệt bậc liên tiếp), trục giữa --il-slate đậm.
- 1 icon mũ bảo hộ/thước đo nhỏ góc dưới (--jade) gợi ý vai "kiến trúc
  sư kết cấu".
```

**Bảng màu áp dụng xuyên suốt 4 phase:**

| Đối tượng | Token màu | Vai trò |
|---|---|---|
| Trục thang (cố định) | `--il-slate` | Mốc tham chiếu chính |
| Bậc thang đang xét (bậc i) | `--il-terracotta` | Đối tượng 1 |
| Bậc thang liền kề (bậc i+1) | `--il-ochre` | Đối tượng 2 — LUÔN khác màu bậc i để không nhầm |
| Đoạn vuông góc chung ĐÚNG | `--jade` | Đáp án chốt mỗi phase |
| Đoạn xiên/bẫy (Phase 2 mục 4) | `--accent` nét đứt | Minh hoạ sai, phân biệt ngay bằng nét đứt |
| Lan can (Phase 3) | `--il-dusty-blue` | Đối tượng khác hẳn "bậc", tránh nhầm loại |

**Quy ước nhãn:** giữ nguyên hệ thống R1/R3/R4. Riêng Phase 4 (bảng tổng
kết), dùng đúng 3 màu ✅ (`--jade-text` trên nền `--jade-pale`) cho các
mục đạt chuẩn, không tự bịa thêm màu cảnh báo mới ngoài hệ thống đã có.

**Bổ sung theo từng phase:**
- **Phase 1:** 2 mặt phẳng ngang (bậc 0 và bậc 12) tô mờ `--il-sand`
  opacity 0.3 mỗi mặt nhưng viền khác nhau (`--il-terracotta` vs
  `--il-ochre`) để phân biệt "dưới/trên", khoảng cách 2,04m hiện bằng
  R1 màu `--jade`.
- **Phase 2:** đúng theo bảng trên (bậc i `--il-terracotta`, bậc i+1
  `--il-ochre`), đoạn nối trên trục = `--jade`. Đoạn bẫy (nối 2 đầu
  ngoài bậc) = `--accent` nét đứt, hiện SONG SONG với đoạn đúng để so
  sánh trực quan độ dài ngay trên hình (không cần đọc số mới thấy khác).
- **Phase 3:** lan can `--il-dusty-blue` (đổi hẳn màu, không dùng lại
  terracotta/ochre của "bậc" để nhấn mạnh "đây là loại đối tượng khác").

**Nâng cấp hình khối trừu tượng → khối thực (rà soát lần 2 — QUAN TRỌNG
cho module này, vì hiện tại mô tả "mỗi bậc là 1 đoạn thẳng" khá trừu
tượng, dễ không nhận ra đây là cầu thang thật):**

- **Mỗi bậc thang:** dựng bằng `BoxGeometry` DẸT (dạng bậc thang thật —
  rộng theo bán kính R, sâu ~0,25m theo phương ngang vuông góc bán kính,
  dày ~0,03m) — KHÔNG dùng đoạn thẳng đơn. Màu xen kẽ theo đúng bảng
  (bậc chẵn `--il-terracotta`, bậc lẻ `--il-ochre`) để mắt tự nhận ra
  nhịp xoắn khi xoay camera.
- **Trục trung tâm:** 1 trụ tròn thật (`CylinderGeometry`, bán kính nhỏ
  ~0,08m) màu `--il-slate`, chạy suốt chiều cao — không phải đường kẻ.
- **Đường tâm/mép dùng cho phép đo (Phase 1, 2):** vẫn là 1 đường MẢNH
  riêng, chạy dọc theo mép trong của mỗi bậc (nơi bậc gắn vào trục) —
  KHÔNG trùng với mesh bậc dày, để nhãn R1/R3/R4 không bị che bởi khối
  bậc khi hiện số đo.
- **Lan can (Phase 3):** ống trụ mỏng (~0,03m bán kính) chạy theo đường
  xoắn nối các đầu ngoài bậc — có thể cong nhẹ mềm mại (dùng `CatmullRomCurve3`
  qua các điểm đầu bậc) thay vì đoạn thẳng cứng nối 2 điểm, để giống tay
  vịn cầu thang xoắn thật hơn — NHƯNG phép tính khoảng cách ở Phase 3 chỉ
  dùng đúng đoạn THẲNG nối bậc 0 và bậc 3 (đơn giản hoá cho tính toán),
  không dùng đường cong đầy đủ — ghi rõ điều này trong lời Athena để
  học sinh không nhầm "lan can cong thật" với "đoạn thẳng dùng để tính".

---

## PHASE 1 — Kiểm tra chiều cao thông thuỷ (đối chiếu chuẩn QCXDVN)

**Cấu hình 3D:** mô hình cầu thang xoắn đầy đủ 12 bậc (1 vòng), mỗi bậc
là 1 đoạn từ trục trung tâm ra ngoài bán kính R=1m, tại độ cao và góc
xoay tăng dần.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Chiều cao thông thuỷ là khoảng cách thẳng đứng từ 1 bậc
   đến bậc cùng góc xoay ở vòng phía trên (ở đây là sau đúng 1 vòng, 12
   bậc). Tính khoảng cách này."
   - *Hành động HS:* nhận ra đây là khoảng cách giữa 2 mặt phẳng NGANG
     song song (mặt phẳng chứa bậc 0 và mặt phẳng chứa bậc 12, cùng góc
     xoay) — chỉ cần lấy hiệu độ cao: 12×0,17 = 2,04m.
   - Verify Node: đúng 2,040m.

2. **Đối chiếu chuẩn:** "QCXDVN 05:2008/BXD quy định chiều cao thông
   thuỷ cầu thang KHÔNG NHỎ HƠN 2m. Thiết kế này có đạt chuẩn không?"
   - `dap_an_dung`: "Đạt — 2,04m > 2m, vượt chuẩn 4cm, an toàn."

3. **3-strike (nhắm sai lầm J):** "Đây là loại khoảng cách nào trong 4
   loại đã học?"
   - A. Điểm đến đường thẳng
   - B. Hai mặt phẳng song song (đáp án đúng)
   - C. Hai đường thẳng chéo nhau
   - Hết lượt: hiện đáp án B + nhắc "vì 2 bậc cùng góc xoay đều nằm
     trong 2 mặt phẳng NGANG khác độ cao, song song nhau."

---

## PHASE 2 — Khoảng cách giữa 2 bậc thang liên tiếp (TRỌNG TÂM — 2 đường chéo nhau)

**Cấu hình 3D:** phóng to 2 bậc liên tiếp (bậc i, bậc i+1) để quan sát
rõ — mỗi bậc là 1 đoạn thẳng từ trục ra ngoài, lệch nhau đúng 30° và
0,17m độ cao.

**Thao tác — lời Athena + hành động:**

1. **Athena (dự đoán trước khi tính — tăng tính khám phá):** "Trước khi
   tính, hãy dự đoán: khoảng cách giữa 2 bậc liên tiếp này có PHỤ THUỘC
   vào góc xoay 30° không, hay chỉ phụ thuộc chiều cao mỗi bậc?"
   - Học sinh chọn dự đoán (không chấm điểm dự đoán, chỉ ghi nhận để đối
     chiếu sau).

2. **Athena:** "Giờ tính thật — 2 bậc này CHÉO NHAU (không cắt nhau,
   không song song). Dựng đoạn vuông góc chung."
   - **Hướng dẫn dựng (chặn từng bước, nhắm sai lầm K):**
     - Nhận xét: cả 2 đoạn bậc đều NẰM NGANG (vuông góc với trục thẳng
       đứng của cầu thang).
     - Vì trục thẳng đứng vuông góc với CẢ HAI đoạn bậc (cả 2 đều nằm
       ngang), đoạn trên trục nối 2 độ cao tương ứng CHÍNH LÀ đoạn vuông
       góc chung — không cần dựng mặt phẳng phụ phức tạp.
   - *Hành động HS:* xác nhận: đoạn nối (0, h_i, 0) và (0, h_{i+1}, 0)
     trên trục vuông góc với CẢ 2 đoạn bậc (kiểm tra bằng tích vô hướng).
   - Kết quả: khoảng cách = |h_{i+1} − h_i| = 0,17m — verify Node: đúng
     0,1700m cho cả cặp bậc (0,1) và cặp (5,6) — **giống nhau tuyệt đối**.

3. **Đối chiếu dự đoán:** "Khoảng cách giữa 2 bậc liên tiếp LUÔN đúng
   bằng 0,17m — CHIỀU CAO MỖI BẬC, không phụ thuộc góc xoay 30°! Dự đoán
   của bạn có đúng không?" — thảo luận ngắn, không chấm điểm.
   - **Giải thích sâu:** "Vì cả 2 đoạn bậc đều nằm ngang (vuông góc với
     trục đứng), trục đứng luôn là phương vuông góc chung — khoảng cách
     giữa chúng chỉ phụ thuộc CHIỀU CAO, không phụ thuộc góc xoay ngang.
     Đây là 1 tính chất khá bất ngờ nhưng logic khi nhìn kỹ."

4. **3-strike (nhắm sai lầm L, M):** "Bước nào sau đây là SAI khi 1 bạn
   học sinh khác giải: 'Nối đầu ngoài của 2 bậc (2 điểm ở bán kính R),
   tam giác tạo thành vuông tại đó, áp Pytago ra khoảng cách'?"
   - `dap_an_dung`: "Sai — chưa kiểm tra tam giác đó có thực sự vuông
     tại đỉnh nào không. Nối 2 đầu ngoài bậc không tạo ra đoạn vuông góc
     chung — đó chỉ là 1 đoạn xiên bất kỳ, dài hơn đáp án đúng (giống bẫy
     đã học ở Module 2 Bước 3)."

---

## PHASE 3 — Khoảng cách lan can đến trục thang (chống nhầm loại khoảng cách)

**Cấu hình 3D:** lan can (tay vịn) là 1 đoạn thẳng nối từ đầu ngoài bậc
0 (góc 0°, cao 0) đến đầu ngoài bậc 3 (góc 90°, cao 3×0,17=0,51m) — mô
phỏng 1 đoạn tay vịn nghiêng theo cầu thang.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Kỹ sư kết cấu cần đảm bảo lan can không va vào trục
   trung tâm khi xoay. Tính khoảng cách giữa đoạn lan can này và trục
   thang."
   - 💡 **Lưu ý hiển thị:** "Lan can thật cong mềm theo cả đường xoắn,
     nhưng để tính toán, ta chỉ cần xét đoạn THẲNG nối 2 điểm đầu và cuối
     của 1 đoạn lan can (ở đây là từ bậc 0 đến bậc 3) — đây là cách đơn
     giản hoá hợp lý, không phải sai sót."
   - ⚠️ **Lưu ý quan trọng (nhắm sai lầm J một lần nữa, ở dạng khác):**
     Athena cảnh báo trước: "Chú ý — lan can này KHÔNG nằm ngang như các
     bậc ở Phase 2, nên trục đứng KHÔNG TỰ ĐỘNG vuông góc với nó. Không
     thể áp lại y hệt cách làm ở Phase 2."
   - *Hành động HS:* nhận ra cần dựng lại đoạn vuông góc chung THẬT (áp
     dụng đúng kỹ thuật Module 2, không phải phép tính đơn giản như
     Phase 2).
   - Verify Node: khoảng cách = 0,7071m (khác hẳn kết quả 0,17m ở Phase
     2, vì đây là cấu hình khác, không phải 2 đoạn ngang cùng gốc trục).

2. **Giải thích đúng:** "Kết quả 0,7071m — khác Phase 2 vì lan can
   KHÔNG nằm ngang. Đây chính là lý do sai lầm phổ biến nhất ở bài luyện
   tập tổng hợp: áp DẬP một công thức/cách làm đã quen từ bài trước cho
   1 cấu hình khác mà không kiểm tra lại điều kiện."

---

## PHASE 4 — Tổng kết dự án, trình bản vẽ

**Thao tác:** Athena tổng hợp lại toàn bộ 3 phase thành "báo cáo kiểm
định" gửi lên cấp trên (hiển thị dạng bảng tổng hợp trực quan):

| Hạng mục kiểm định | Loại khoảng cách | Kết quả | Đạt chuẩn? |
|---|---|---|---|
| Chiều cao thông thuỷ | 2 mặt phẳng song song | 2,04m | ✅ (chuẩn ≥2m) |
| Khoảng cách 2 bậc liên tiếp | 2 đường thẳng chéo nhau | 0,17m | Thông tin thiết kế |
| Khoảng cách lan can – trục | 2 đường thẳng chéo nhau (cấu hình khác) | 0,7071m | Thông tin thiết kế |

**Athena (chốt vai diễn):** "Cảm ơn kiến trúc sư đã hoàn thành kiểm
định! Điều quan trọng nhất rút ra từ dự án này: dù đều là 'khoảng cách 2
đường chéo nhau', Phase 2 và Phase 3 có cách giải KHÁC NHAU hoàn toàn vì
cấu hình hình học khác nhau — không có công thức 'dùng chung cho mọi
trường hợp', luôn phải kiểm tra lại điều kiện trước khi áp dụng cách
làm cũ."

> 💡 **Lưu ý phân bổ thời gian (nhắm sai lầm N):** nếu triển khai dạng
> bài kiểm tra có giới hạn thời gian, đề xuất Phase 2 (trọng tâm, có
> "khám phá bất ngờ") được phân bổ thời gian nhiều nhất, Phase 1 và 3
> ngắn gọn hơn — tránh học sinh sa đà vào Phase 3 (khó nhất) mà bỏ lỡ
> Phase 2 (giá trị sư phạm cao nhất).

## Rủi ro kỹ thuật 3D

```
✅ An toàn: toàn bộ 4 phase — dùng `angleBetweenLines`/`isPerpendicular`
   (06 PHẦN C.3) đã có, mô hình cầu thang xoắn chỉ là các đoạn thẳng
   tĩnh tính bằng công thức tham số hoá (góc, độ cao) — không cần dựng
   khối cong/xoắn phức tạp, không cần pattern 3D mới.
```

---

> **Trạng thái:** Module 3 (Bài 26) đã có kịch bản đầy đủ 4 phase theo
> đúng dự án "Thiết kế cầu thang xoắn", vai kiến trúc sư kết cấu xuyên
> suốt, số liệu đã verify bằng Node/THREE.js thật (khoảng cách bậc liên
> tiếp luôn = 0,17m bất kể góc xoay — 1 kết quả khá bất ngờ và có giá
> trị khám phá cao). Đối chiếu đúng chuẩn thật QCXDVN 05:2008/BXD. **Bài
> 26 đã hoàn tất toàn bộ 3 module.**
