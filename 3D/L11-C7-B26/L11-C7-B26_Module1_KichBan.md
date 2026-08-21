# 📚 KỊCH BẢN — Bài 26, Module 1: "Khoảng cách từ một điểm đến đường thẳng, mặt phẳng"

```
📖 PPCT: Tiết 74 — Chủ đề 10: Khoảng cách
📌 Đã dạy qua kênh khác: video Manim. Không rút gọn — mô phỏng 3D đầy đủ
   theo yêu cầu, cùng tinh thần Bài 22-25.
🎯 Sai lầm nhắm tới (PPCT):
   (A) dùng đoạn thẳng BẤT KỲ nối điểm với đường/mặt mà không kiểm tra
       tính vuông góc
   (B) xác định sai chân đường vuông góc khi đáy không quen thuộc
   (C) kẻ đường vuông góc nhưng không CHỨNG MINH được nó vuông góc thật
   (D) quên kỹ thuật "kẻ hai lần" (từ chân đường cao kẻ vuông góc vào
       giao tuyến, rồi nối lên đỉnh)
   (E) kỹ thuật "dời điểm" (tỉ số khoảng cách) — lập sai tỉ lệ hệ số
📁 File: Bai26_Toan3D_Module1_KhoangCachDiemDenDuongMatPhang.html
```

> ⚠️ **Bối cảnh xuyên suốt cả module:** "Trạm phát sóng" (đúng PPCT gợi
> ý) — dùng 1 câu chuyện liền mạch cho cả 4 bước để tạo cảm giác thống
> nhất: Bước 1 (khoảng cách trạm đến con đường), Bước 2 (giá đỡ 3 chân
> của trạm — hình chóp tam giác đều), Bước 3 (khung đỡ thiết bị hình hộp
> đứng đáy thoi), Bước 4 (dây giằng từ đỉnh cột — kỹ thuật dời điểm).

## Sổ tay kiến thức (hiện dần theo bước)

```
- Khoảng cách từ điểm M đến đường thẳng a, kí hiệu d(M,a), là khoảng
  cách giữa M và HÌNH CHIẾU H của M trên a (H là chân đường vuông góc).
- Khoảng cách từ điểm M đến mặt phẳng (P), kí hiệu d(M,(P)), là khoảng
  cách giữa M và HÌNH CHIẾU H của M trên (P).
- Nhận xét: d(M,a)/d(M,(P)) là khoảng cách NHỎ NHẤT giữa M và 1 điểm bất
  kỳ thuộc a/(P) — với MỌI K khác H, MK ≥ MH.
- Kỹ thuật "kẻ hai lần": khi chưa thấy ngay đường vuông góc từ điểm đến
  mặt phẳng đích, có thể: (1) kẻ vuông góc từ điểm xuống 1 mặt phẳng liên
  quan trước (tìm chân H), (2) từ H kẻ tiếp vuông góc vào giao tuyến của
  2 mặt phẳng, (3) nối lại thành đoạn vuông góc thật cần tìm.
- Kỹ thuật "dời điểm": nếu M nằm trên đoạn AB với tỉ lệ AM:MB = m:n, và
  đã biết d(A,(P)), d(B,(P)), có thể suy d(M,(P)) theo TỈ LỆ VỊ TRÍ, KHÔNG
  cần dựng lại đường vuông góc từ đầu.
```

## Đặc tả hình ảnh & màu sắc (bổ sung sau rà soát — áp dụng token có sẵn)

> ⚠️ **Phát hiện khi rà soát:** bản kịch bản gốc mô tả đủ logic tương
> tác nhưng CHƯA gắn màu/nhãn cụ thể cho từng đối tượng — bổ sung ở đây,
> dùng đúng token đã có trong `02_design_toan_final.md` PHẦN 1, không
> tạo màu mới.

**Hook mở đầu module (hiện trước Bước 1, SVG viewBox 0 0 500 300):**
```
- 1 cột trạm phát sóng đơn giản (đường thẳng đứng --il-slate, đậm) với
  3-4 vòng cung sóng lan toả ở đỉnh (nét mảnh --jade, opacity giảm dần
  ra ngoài — gợi ý "phát sóng").
- 1 con đường ngang phía dưới (dải --il-sand).
- 1 nét đứt mảnh --accent nối từ chân cột xuống đường, kèm dấu "?" nhỏ —
  gợi mở câu hỏi "khoảng cách bao nhiêu?" trước khi vào Bước 1.
```

**Bảng màu áp dụng xuyên suốt cả 4 bước (nhất quán 1 màu = 1 vai trò):**

| Đối tượng | Token màu | Vai trò |
|---|---|---|
| Cột/thân chính (cột trạm, giá đỡ, cột chính) | `--il-slate` | Kết cấu chính, cố định |
| Đường/mặt phẳng "đích" cần tính khoảng cách tới | `--il-sand` | Mặt đất/mặt phẳng tham chiếu |
| Đoạn/đường vuông góc ĐÚNG (kết quả cần tìm) | `--jade` | Đáp án, luôn nổi bật nhất |
| Đoạn/đường minh hoạ SAI hoặc đang thử (bẫy) | `--accent` | Cảnh báo nhẹ, chưa xác nhận đúng |
| Dây giằng/chi tiết phụ (Bước 4) | `--il-ochre` | Chi tiết phụ, không phải trọng tâm chính |

**Quy ước nhãn/dấu hiệu (dùng lại đúng hệ thống R1-R4 đã có):**
- R1 (label số đo) — luôn hiện tại trung điểm đoạn đang đo, font theo
  đúng `--ink`, nền `--cream` mờ để nổi trên khối 3D.
- R3 (cung góc nhỏ) — tại mọi góc vuông/góc cần minh hoạ.
- R4 (dấu góc vuông hình vuông nhỏ) — bắt buộc hiện ngay khi xác nhận 1
  đoạn là đường vuông góc đúng (đổi màu viền từ `--accent` sang `--jade`
  ĐÚNG lúc xác nhận — tạo hiệu ứng "chốt đáp án" rõ ràng).

**Bổ sung theo từng bước:**
- **Bước 1:** M (trạm) = chấm tròn `--il-slate` đậm, đường a = `--il-sand`,
  đoạn MK khi K≠H = nét `--accent`, đoạn MH khi xác nhận đúng = đổi sang
  `--jade` kèm hiệu ứng "khoá lại" (nhấp nháy nhẹ 1 lần).
- **Bước 2:** giá đỡ 3 chân dùng `--il-slate` cho khung, đáy tam giác đều
  tô mờ `--il-sand` opacity 0.3, đoạn SO (chiều cao cần tính) tô `--jade`
  đậm dần theo từng bước hiện công thức.
- **Bước 3:** khung hộp đứng đáy thoi — 2 đáy tô mờ `--il-sand`, cạnh bên
  `--il-slate`, đoạn AO (kết quả kẻ 2 lần) tô `--jade`, đường chéo BD
  dùng `--il-ochre` để phân biệt với AO.
- **Bước 4:** cột chính `--il-slate`, dây giằng `--il-ochre`, điểm M kéo
  được tô `--accent` khi đang kéo, đổi `--jade` khi thả đúng vị trí kiểm
  tra.

**Nâng cấp hình khối trừu tượng → khối thực (phát hiện khi rà soát lần
2 — áp dụng cho cả Module 1, 2, 3):**

> ⚠️ Nhiều đối tượng hiện mô tả là "đoạn thẳng"/"đường thẳng" — ĐÚNG cho
> tính toán, nhưng nhìn trừu tượng, giảm cảm giác thực. Quy tắc chung: **1
> đối tượng thực tế = 1 mesh khối THẬT (trụ/hộp mỏng) mang tính minh hoạ,
> ĐI KÈM 1 đường tâm/trục mảnh (không tô đặc, chỉ nét) dùng riêng cho
> phép đo và nhãn R1/R3/R4** — tách rõ vai trò "nhìn cho thực" và "tính
> cho đúng", tránh 2 việc chồng lên nhau gây rối.

- **Giá đỡ 3 chân (Bước 2):** mỗi chân dựng bằng `THREE.CylinderGeometry`
  bán kính nhỏ (không phải đường kẻ đơn), màu `--il-slate`, có khớp nối
  (hình cầu nhỏ) tại 3 điểm chân và đỉnh — giống giá đỡ máy quay/tripod
  thật. Đường tâm SO dùng cho phép đo vẫn là nét mảnh riêng, màu `--jade`,
  KHÔNG trùng với mesh trụ của chân.
- **Dây giằng (Bước 4):** dựng bằng ống trụ RẤT MỎNG (bán kính ~0,02
  đơn vị) màu `--il-ochre`, hơi chảy võng nhẹ (catenary đơn giản hoá bằng
  1 đường cong Bezier nhẹ) để gợi cảm giác dây thật chứ không phải thanh
  cứng — điểm M kéo được vẫn đặt trên đường tâm lý tưởng (thẳng, dùng cho
  tính tỉ lệ), không bắt buộc trùng khớp với độ võng thị giác.
- **Khung đỡ hình hộp (Bước 3):** cạnh khung dựng bằng thanh nhôm chữ
  nhật mỏng (`BoxGeometry` dẹt) màu `--il-slate`, không dùng line thuần.

---

## BƯỚC 1 — Định nghĩa: khoảng cách là NGẮN NHẤT (bối cảnh: trạm phát sóng)

**Cấu hình 3D:**
- 1 cột trạm phát sóng (điểm M, đại diện vị trí đặt trạm), 1 con đường
  thẳng a chạy gần đó. H là chân đường vuông góc từ M xuống a.
- **Đối tượng kéo được:** điểm K trượt dọc theo đường a (dùng
  `ConstrainedPoint.dragToward`, PHẦN 2.2 đã có).
- Verify Python: tại H, MH=4,00; kéo K ra xa H (K=0,1,2,3,5,8 trên
  đường), MK luôn ≥ 4,00 — nhỏ nhất chính xác tại K=H.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Kỹ sư cần chọn 1 điểm K trên con đường a để kéo cáp nối
   tới trạm phát sóng M — kéo K dọc đường, quan sát độ dài đoạn MK thay
   đổi thế nào. Độ dài NGẮN NHẤT đạt được khi K ở đâu?"
   - *Hành động HS:* kéo K dọc đường a, quan sát số đo MK cập nhật theo
     thời gian thực (hiện đồ thị nhỏ khoảng cách theo vị trí K, nếu khả
     thi — giúp thấy rõ đáy "chảo" tại H).
   - 🎯 **Mục tiêu quan sát:** MK nhỏ nhất khi K trùng H — điểm mà MH
     VUÔNG GÓC với đường a.

2. **Giải thích đúng + chốt định nghĩa:** "Đúng — khoảng cách từ M đến
   đường a được ĐỊNH NGHĨA là chính đoạn MH ngắn nhất này, không phải
   đoạn bất kỳ. Đây là lý do khi tính khoảng cách, PHẢI dựng đúng đường
   vuông góc, không được chọn 1 đoạn nối tiện tay."

3. **Mở rộng sang mặt phẳng:** "Tương tự, nếu trạm M cần nối tới 1 khu
   đất bằng phẳng (mặt phẳng (P)) thay vì con đường, khoảng cách ngắn
   nhất cũng là đoạn MH vuông góc (P)." — minh hoạ lại nhanh bằng 1 mặt
   phẳng thay đường thẳng, cùng cơ chế.

4. **3-strike (nhắm trực diện sai lầm A):** "Để tính khoảng cách từ 1
   điểm đến 1 đường/mặt phẳng, bước ĐẦU TIÊN cần làm là gì?"
   - A. Nối điểm đó với 1 điểm bất kỳ trên đường/mặt, đo độ dài
   - B. Xác định đúng chân đường vuông góc trước, rồi đo đoạn đó (đáp án
     đúng)
   - C. Ước lượng bằng mắt trên hình vẽ
   - Hết lượt: hiện đáp án B + nhắc lại minh hoạ Bước 1.

---

## BƯỚC 2 — Quy trình tính bằng hệ thức lượng (giá đỡ 3 chân của trạm)

**Cấu hình 3D:**
- Giá đỡ trạm phát sóng dạng chóp tam giác ĐỀU: 3 chân cách đều nhau
  90cm (tại đáy), mỗi chân dài 150cm, đỉnh giá là nơi đặt thiết bị.
- Verify Python: OA (bán kính đáy) = 51,96cm, chiều cao giá đỡ SO =
  140,71cm.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Kỹ sư cần biết thiết bị đặt cao bao nhiêu so với mặt đất
   — chính là khoảng cách từ đỉnh giá đỡ (S) đến mặt đất (đáy chóp). Quy
   trình: (1) xác định chân đường vuông góc, (2) tính bằng hệ thức
   lượng."
   - *Hành động HS:* click xác định chân đường vuông góc — vì giá đỡ là
     chóp ĐỀU, chân đường cao trùng TÂM đáy (ôn lại Bài 25 Module 3).
   - Học sinh tính OA (bán kính đường tròn ngoại tiếp tam giác đều đáy)
     rồi áp Pythagore trong tam giác vuông SOA để ra SO.
   - Hệ thống chặn từng bước (không cho nhảy thẳng tới đáp án): phải
     tính đúng OA trước, mới cho tính SO.

2. **Giải thích đúng:** "Chiều cao giá đỡ = SO = √(SA² − OA²) =
   140,71cm — đây chính là khoảng cách từ đỉnh S đến mặt đất."

---

## BƯỚC 3 — Kỹ thuật "kẻ hai lần" (khung đỡ thiết bị hình hộp đứng)

**Cấu hình 3D:**
- Khung đỡ thiết bị hình hộp ĐỨNG ABCD.A'B'C'D', đáy là HÌNH THOI cạnh
  a=4, góc BAD=100°, chiều cao AA'=h=5.
- Verify Python: AO (nửa đường chéo AC) = 2,5712.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Cần tính khoảng cách từ cạnh AA' đến mặt (BDD'B') — mặt
   này KHÔNG chứa đỉnh A hay A', và không có sẵn đường vuông góc rõ
   ràng. Đây là lúc dùng kỹ thuật 'kẻ hai lần'."
   - **Hướng dẫn từng bước (không cho nhảy cóc):**
     - *Kẻ lần 1:* trong mặt đáy (ABCD), kẻ AO vuông góc với BD (đường
       chéo hình thoi vuông góc nhau — tính chất đã học) — O là giao 2
       đường chéo.
     - *Kẻ lần 2:* vì AA'⊥(ABCD) và AO⊥BD, suy ra AO⊥(BDD'B') (áp dụng
       định lí — AO vuông góc với 2 đường cắt nhau BD và AA' trong mặt
       phẳng chứa nó... — thực chất là AO là đoạn vuông góc THẬT cần
       tìm, không cần kẻ thêm).
   - *Hành động HS:* tự dựng lần lượt AO trong đáy, sau đó xác nhận AO
     cũng vuông góc mặt (BDD'B') bằng cách kiểm tra 2 điều kiện (vuông
     góc BD và vuông góc AA').
   - Kết quả: d(AA',(BDD'B')) = AO = 2,5712.

2. **3-strike (nhắm sai lầm D):** "Nếu chỉ kẻ 1 đường vuông góc trong
   đáy mà KHÔNG kiểm tra thêm điều kiện với cạnh bên (AA'), có thể kết
   luận ngay đó là khoảng cách cần tìm không?"
   - `dap_an_dung`: "Không — phải kiểm tra đủ CẢ 2 điều kiện (vuông góc
     với đường trong đáy VÀ vuông góc với cạnh bên/mặt liên quan), đây
     chính là ý nghĩa 'kẻ hai lần' — không dừng ở bước đầu."

---

## BƯỚC 4 — Kỹ thuật "dời điểm" (dây giằng từ đỉnh cột — bước quan trọng nhất)

**Cấu hình 3D:**
- Cột chính của trạm phát sóng, đỉnh S, chân A, SA⊥mặt đất (ABC), SA=8m.
  Dây giằng chạy từ S xuống 3 điểm neo B, C trên mặt đất. Điểm M là 1
  khoen nối ở giữa dây SA (trung điểm).

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đã biết khoảng cách từ đỉnh cột S đến mặt đất là 8m
   (chính là SA). Nếu M là khoen nối chính giữa dây SA (trung điểm),
   khoảng cách từ M đến mặt đất là bao nhiêu? Đừng tính lại từ đầu — hãy
   dùng TỈ LỆ VỊ TRÍ của M trên đoạn SA."
   - *Hành động HS:* kéo con trượt đặt M tại các tỉ lệ khác nhau trên SA
     (không chỉ trung điểm) — quan sát khoảng cách d(M, mặt đất) BIẾN
     ĐỔI THEO ĐÚNG TỈ LỆ, không cần tính toạ độ lại.
   - Verify Python: M tại trung điểm (tỉ lệ 1/2) → d(M,đáy) = 4,0m =
     đúng 1/2 của 8m — khớp hoàn toàn với toạ độ thực tính trực tiếp.

2. **Giải thích đúng + tổng quát hoá:** "Đây là kỹ thuật DỜI ĐIỂM: khi
   1 điểm M nằm trên đoạn SA với SA đã biết khoảng cách đến mặt phẳng,
   khoảng cách từ M cũng tỉ lệ THEO ĐÚNG VỊ TRÍ của M trên đoạn — không
   cần dựng lại đường vuông góc từ đầu. Đây là kỹ thuật CỐT LÕI cho các
   bài toán khoảng cách phức tạp sau này."

3. **3-strike (nhắm trực diện sai lầm E — lập sai tỉ lệ):** "Nếu M nằm
   trên SA sao cho SM:MA = 1:3 (không phải trung điểm), khoảng cách từ M
   đến mặt đất là bao nhiêu, biết d(S, đáy)=8m và d(A, đáy)=0 (A đã
   thuộc mặt đất)?"
   - `dap_an_dung`: "6m — vì SM:MA=1:3 nghĩa là M chia SA theo tỉ lệ, M
     gần S hơn (SM = 1/4 SA), nên d(M, đáy) = d(A,đáy) + (MA/SA)×(d(S,đáy)
     − d(A,đáy)) = 0 + (3/4)×8 = 6m."
   - `goi_y_khi_sai`: "M gần A hay gần S hơn theo tỉ lệ 1:3? Khoảng cách
     từ M phải gần giá trị của điểm nào hơn (S hay A)?" — bẫy thường gặp:
     nhầm lấy 1/4 × 8 = 2m (lấy nhầm tỉ lệ phần gần S thay vì phần xa S).

---

## TỔNG HỢP KIẾN THỨC (đóng Module 1)

| Khối kiến thức | Nội dung | Xem lại tại |
|---|---|---|
| 1. Định nghĩa | d(M,a)/d(M,(P)) = khoảng cách đến hình chiếu, là khoảng cách NHỎ NHẤT | Bước 1 |
| 2. Quy trình cơ bản | Chân đường vuông góc + hệ thức lượng | Bước 2 |
| 3. Kẻ hai lần | Kiểm tra đủ 2 điều kiện vuông góc, không dừng ở bước đầu | Bước 3 |
| 4. Dời điểm | Tỉ lệ vị trí trên đoạn thẳng → suy khoảng cách, không tính lại từ đầu | Bước 4 |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: toàn bộ 4 bước — dùng `ConstrainedPoint.dragToward` (PHẦN
   2.2), `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3) đã có, không
   cần pattern 3D mới.
✅ An toàn: Bước 1 (đồ thị nhỏ khoảng cách theo vị trí K) — nếu build,
   chỉ là 1 biểu đồ 2D phụ (HTML/canvas overlay), không phải pattern 3D.
```

---

> **Trạng thái:** Module 1 (Bài 26) đã có kịch bản đầy đủ 4 bước + Tổng
> hợp kiến thức, xuyên suốt bởi câu chuyện "trạm phát sóng", số liệu đã
> verify bằng Python. Module 2 (khoảng cách song song/chéo nhau — cổng
> trạm thu phí, ống kỹ thuật) và Module 3 (luyện tập — vai kỹ sư/kiến
> trúc sư, dự án cầu thang xoắn) sẽ ra kịch bản ở các phiên tiếp theo.
