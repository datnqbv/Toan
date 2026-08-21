# 📚 KỊCH BẢN — Bài 26, Module 2: "Khoảng cách giữa các đối tượng song song và chéo nhau"

```
📖 PPCT: Tiết 75 — Chủ đề 10: Khoảng cách
🔗 Điều kiện tiên quyết: Module 1 (khoảng cách điểm-đường/mặt phẳng).
🎯 Sai lầm nhắm tới (PPCT):
   (F) nhầm đoạn vuông góc CHUNG của 2 đường chéo nhau với 1 đoạn vuông
       góc BẤT KỲ nối 2 đường đó (phải vuông góc với CẢ HAI đường)
   (G) chọn mặt phẳng phụ KHÔNG song song với đường thẳng cần thiết khi
       dựng đoạn vuông góc chung
   (H) tính nhầm khoảng cách 2 mặt phẳng song song thành khoảng cách 2
       điểm bất kỳ
   (I) cố dựng đoạn vuông góc chung "mù quáng" trong khi cấu hình quá
       phức tạp, thay vì quy về khoảng cách đường-mặt song song (dễ hơn)
📁 File: Bai26_Toan3D_Module2_KhoangCachSongSongCheoNhau.html
```

> ⚠️ **Bối cảnh:** Bước 1 dùng **cổng trạm thu phí** (đổi khỏi "khung
> khống chế chiều cao cầu vượt" SGK — đã duyệt). Bước 4 dùng **2 đường
> ống kỹ thuật (nước + điều hoà) trong trần giả** (đổi khỏi "2 dây cáp
> treo/dây điện chéo nhau" sau khi xác minh dây điện cao thế không thực
> tế chéo nhau tự do — đã duyệt).

## Sổ tay kiến thức (hiện dần theo bước)

```
- Khoảng cách giữa đường thẳng a và mặt phẳng (P) song song với a,
  d(a,(P)), là khoảng cách từ 1 điểm BẤT KỲ thuộc a đến (P) — vì mọi
  điểm trên a cách (P) như nhau (do a song song (P)).
- Khoảng cách giữa 2 mặt phẳng song song (P), (Q), d((P),(Q)), là
  khoảng cách từ 1 điểm bất kỳ thuộc (P) đến (Q).
- Đường vuông góc chung của 2 đường chéo nhau a, b: đường thẳng Δ cắt cả
  a, b và vuông góc với CẢ HAI. Khoảng cách giữa a, b = độ dài đoạn Δ
  cắt ra giữa 2 giao điểm.
- Nhận xét quan trọng: khoảng cách giữa 2 đường chéo nhau CŨNG BẰNG
  khoảng cách từ 1 trong 2 đường đến mặt phẳng chứa đường còn lại và
  song song với đường thứ nhất — đây là cách "quy về dễ hơn", tránh phải
  dựng trực tiếp đoạn vuông góc chung khi cấu hình phức tạp.
```

---

## Đặc tả hình ảnh & màu sắc (bổ sung sau rà soát — áp dụng token có sẵn)

**Hook mở đầu module (SVG viewBox 0 0 500 280):**
```
- Cổng trạm thu phí cách điệu: 2 cột đứng --il-slate, thanh ngang nối
  đỉnh --jade, mặt đường dốc bên dưới --il-sand (vẽ nghiêng nhẹ để gợi
  ý "dốc").
- 1 icon xe nhỏ (hình chữ nhật + 2 bánh tròn, --il-terracotta) đặt cạnh
  cổng, kèm mũi tên chỉ chiều cao xe, gợi câu hỏi "xe qua được không?"
```

**Bảng màu áp dụng xuyên suốt 4 bước:**

| Đối tượng | Token màu | Vai trò |
|---|---|---|
| Kết cấu chính (cột cổng, cạnh SA, ống chính) | `--il-slate` | Cố định, đã biết |
| Mặt phẳng/mặt dốc tham chiếu | `--il-sand` | Mặt đích cần tính khoảng cách tới |
| Đoạn/đường vuông góc chung ĐÚNG | `--jade` | Đáp án chốt |
| Đoạn xiên/bẫy (Bước 3) | `--accent` | Đang thử, chưa xác nhận |
| Đối tượng thứ 2 trong cặp chéo nhau (BC, ống điều hoà) | `--il-ochre` | Phân biệt rõ với đối tượng 1 |

**Quy ước nhãn:** giữ đúng hệ thống R1 (label số đo)/R3 (cung góc)/R4
(dấu vuông) như Module 1 — R4 đổi màu viền từ `--accent`→`--jade` đúng
lúc xác nhận đoạn vuông góc chung hợp lệ.

**Bổ sung theo từng bước:**
- **Bước 1:** cột cổng `--il-slate`, mặt dốc `--il-sand` tô mờ opacity
  0.4, thanh ngang khi CHƯA xác nhận song song = `--accent`, khi xác
  nhận = `--jade`.
- **Bước 2-3:** SA (cạnh đã biết ⊥ đáy) = `--il-slate` đậm, BC =
  `--il-ochre`, AH (đoạn vuông góc chung đúng) = `--jade`, SK (đoạn bẫy
  Bước 3) = `--accent` nét đứt (phân biệt trực quan ngay với AH nét
  liền).
- **Bước 4:** ống nước `--il-dusty-blue`, ống điều hoà `--il-ochre`, mặt
  phẳng phụ (Q) tô mờ `--jade-pale` opacity 0.25 khi dựng ra.

**Nâng cấp hình khối trừu tượng → khối thực (rà soát lần 2):**
- **Cột cổng thu phí (Bước 1):** trụ vuông/trụ tròn thật (`BoxGeometry`
  hoặc `CylinderGeometry`) màu `--il-slate`, có đế loe nhẹ tại chân —
  không dùng đường kẻ đơn.
- **Ống nước, ống điều hoà (Bước 4):** dựng bằng `CylinderGeometry` bán
  kính khác nhau thật (ống nước nhỏ hơn ống điều hoà, đúng tỉ lệ thực tế
  — ống nước ~0,05 đơn vị, ống điều hoà ~0,08 đơn vị) — KHÔNG dùng line.
  Đường tâm dùng cho phép đo là 1 đường tưởng tượng đi giữa lòng ống,
  không vẽ đè lên mesh ống (ẩn/hiện khi cần đo, tránh rối mắt khi chỉ
  xem mô hình).
- **⚠️ Bối cảnh còn thiếu — bổ sung "trần giả":** hiện Bước 4 chỉ có 2
  ống lửng giữa không gian trống, CHƯA có bối cảnh phòng/trần để neo
  cảm giác "đây là trong 1 toà nhà". Bổ sung: 1 mặt phẳng "trần giả"
  (lưới ô vuông mảnh, màu `--paper-line`, đặt phía trên 2 ống) + 1 mặt
  "sàn" mờ phía dưới (màu `--cream-2`, opacity 0.5) — chỉ cần 2 mặt
  phẳng đơn giản, không cần dựng nguyên phòng 3D đầy đủ, nhưng đủ để
  người xem hiểu đây là không gian TRONG NHÀ, không phải ngoài trời.

---

## BƯỚC 1 — Khoảng cách đường-mặt song song (cổng trạm thu phí)

**Cấu hình 3D:**
- Cổng trạm thu phí: 2 cột thẳng đứng cao L=2,5m, dựng trên đoạn đường
  dốc nghiêng α=10° so với mặt ngang. Thanh ngang nối 2 đỉnh cột.
- Verify Python: vì 2 cột đứng thẳng (theo phương ngang toàn cục, không
  theo phương vuông góc mặt dốc) và đặt cách nhau theo hướng NGANG qua
  mặt dốc, thanh ngang có hướng nằm TRONG mặt dốc (dọc theo đường mức) →
  thanh ngang SONG SONG với mặt dốc.
- Khoảng cách thanh ngang – mặt dốc = L·cos(α) = 2,5×cos(10°) ≈ 2,462m.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Cổng trạm thu phí có thanh ngang nối 2 đỉnh cột. Cột
   dựng thẳng đứng (theo phương trọng lực), nhưng mặt đường lại dốc 10°.
   Thanh ngang có song song với mặt đường không?"
   - *Hành động HS:* xoay camera quan sát, kiểm tra hướng thanh ngang so
     với mặt đường dốc.
   - 🎯 **Mục tiêu quan sát:** thanh ngang chạy dọc theo hướng NGANG qua
     mặt dốc (giống đường đồng mức) — nằm trong "hướng" của mặt dốc, nên
     song song với nó.

2. **Athena:** "Vì thanh ngang song song mặt đường, khoảng cách giữa
   chúng = khoảng cách từ 1 điểm BẤT KỲ trên thanh đến mặt đường — không
   cần đo tại nhiều điểm khác nhau trên thanh. Tính khoảng cách này, biết
   cột cao 2,5m và mặt đường dốc 10°."
   - *Hành động HS:* nhận ra khoảng cách KHÔNG phải bằng L=2,5m luôn
     (vì cột vuông góc mặt NGANG, không vuông góc mặt DỐC) — cần nhân
     thêm cos(α).
   - Kết quả: 2,5×cos(10°) ≈ 2,462m.

3. **Ứng dụng — câu hỏi thực tế:** "Nếu xe cao 2,4m, xe có qua được cổng
   không?"
   - `dap_an_dung`: "Có — vì 2,4m < 2,462m (khoảng cách thật từ thanh
     ngang đến mặt đường), xe vẫn có khoảng hở để qua."

---

## BƯỚC 2 — Dựng đoạn vuông góc chung của 2 đường chéo nhau

**Cấu hình 3D:**
- Hình chóp S.ABC, SA⊥(ABC), AB=6, góc ABC=70°. Cần tính khoảng cách
  giữa SA và BC (2 đường chéo nhau — SA không cắt BC, không song song).
- Verify Python: gọi H là hình chiếu của A trên BC — AH ⊥ BC (đã kiểm
  tra: tích vô hướng = 0) VÀ AH ⊥ SA (vì SA⊥(ABC), AH nằm trong (ABC)) —
  AH = 5,6382 = đúng khoảng cách cần tìm.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Để dựng đoạn vuông góc chung của SA và BC, ta cần 1 đoạn
   vuông góc với CẢ HAI đường. Vì SA đã vuông góc CẢ MẶT PHẲNG (ABC),
   SA tự động vuông góc với BẤT KỲ đường nào trong (ABC) — kể cả đường
   ta sắp dựng. Vậy chỉ cần tìm 1 đường trong (ABC) vuông góc BC."
   - *Hành động HS:* dựng AH vuông góc BC (H là chân đường vuông góc từ
     A xuống BC) — dùng hệ thức lượng tam giác vuông ABH để tính
     BH=2,0521, rồi AH=5,6382 (= AB·sin(ABC)).
   - Hệ thống xác nhận: AH vuông góc BC (✓) VÀ AH vuông góc SA (✓, vì
     SA⊥(ABC)) → AH chính là đoạn vuông góc chung.

2. **Giải thích đúng:** "Khoảng cách giữa SA và BC = AH = 5,6382. Đây là
   kỹ thuật thường gặp: khi ĐÃ CÓ 1 đường vuông góc cả mặt phẳng (như SA
   ở đây), chỉ cần tìm thêm 1 đường vuông góc với đường chéo còn lại
   TRONG mặt phẳng đó — không cần dựng mặt phẳng phụ phức tạp."

---

## BƯỚC 3 — Bẫy: đoạn vuông góc BẤT KỲ ≠ đoạn vuông góc CHUNG (nhắm trực diện sai lầm F)

**Cấu hình 3D:** dùng lại hình chóp Bước 2, thêm điểm K trên BC (khác H,
lệch 2 đơn vị).

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Nếu nối S với điểm K (khác H) trên BC, đoạn SK có phải
   là 1 cách khác để tính khoảng cách SA-BC không?"
   - *Hành động HS:* kéo K dọc BC (khác vị trí H), đo độ dài SK, so sánh
     với SH (đoạn nối S với H — đường xiên qua AH và SA).
   - Verify Python: SK = 7,7967 (khi K lệch H 2 đơn vị) so với SH =
     7,5358 (đường nối đúng qua H) — SK LUÔN DÀI HƠN, và SK KHÔNG vuông
     góc BC (tích vô hướng = −2 ≠ 0).

2. **3-strike (nhắm trực diện sai lầm F):** "SK có phải là đoạn vuông
   góc chung của SA và BC không?"
   - `dap_an_dung`: "Không — SK không vuông góc với BC (chỉ là 1 đoạn
     xiên bất kỳ). Đoạn vuông góc CHUNG phải vuông góc với CẢ HAI đường,
     và chỉ có 1 đoạn duy nhất thoả điều kiện đó — đoạn qua đúng điểm H."
   - `goi_y_khi_sai`: "Kéo K về đúng vị trí H và so sánh độ dài SK khi
     đó với SK khi K ở vị trí khác — đoạn nào NGẮN NHẤT?"

3. **Chốt nguyên tắc:** "Đoạn vuông góc chung LUÔN là đoạn NGẮN NHẤT
   nối 2 đường chéo nhau — giống định nghĩa khoảng cách điểm-đường ở
   Module 1 (MK≥MH), ở đây là phiên bản mở rộng cho 2 đường chéo nhau."

---

## BƯỚC 4 — Ứng dụng: 2 đường ống kỹ thuật chéo nhau (2 cách tiếp cận)

**Cấu hình 3D:**
- Trong trần giả toà nhà: ống nước chạy ngang tại độ cao 1,0m (theo 1
  hướng), ống điều hoà chạy chéo tại độ cao 1,8m (hướng khác, chéo 45°
  so với ống nước) — 2 ống KHÔNG cắt nhau, KHÔNG song song → chéo nhau.
- Verify Python: mặt phẳng (Q) chứa ống điều hoà và song song ống nước
  có pháp tuyến CHỈ có thành phần thẳng đứng — khoảng cách giữa 2 ống =
  |1,8−1,0| = 0,8m.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đội thi công cơ điện cần đảm bảo 2 ống này không va vào
   nhau khi lắp đặt. Có 2 cách tính khoảng cách giữa chúng — thử CÁCH 1
   trước: dựng trực tiếp đoạn vuông góc chung."
   - *Hành động HS:* thử dựng đoạn vuông góc chung trực tiếp (như Bước
     2) — nhận thấy phức tạp hơn vì 2 ống đều chéo, không có sẵn 1 ống
     nào vuông góc hẳn với 1 mặt phẳng chứa ống kia.

2. **Athena:** "Giờ thử CÁCH 2: dựng 1 mặt phẳng (Q) chứa ống điều hoà,
   SONG SONG với ống nước — rồi tính khoảng cách từ ống nước đến (Q)."
   - *Hành động HS:* dựng (Q), quan sát (Q) hoá ra chính là MẶT PHẲNG
     NẰM NGANG đi qua ống điều hoà (vì cả 2 ống đều là đường "ngang",
     chỉ khác độ cao) → khoảng cách = hiệu độ cao = 0,8m — đơn giản hơn
     hẳn cách 1.

3. **3-strike (nhắm sai lầm I):** "Trong tình huống này, cách nào NÊN
   dùng khi cấu hình phức tạp (không có sẵn đường nào vuông góc hẳn 1
   mặt phẳng)?"
   - `dap_an_dung`: "Cách 2 — quy về khoảng cách đường-mặt phẳng song
     song, dễ áp dụng hơn dựng trực tiếp đoạn vuông góc chung."

4. **Lưu ý mở rộng (nhắm sai lầm G):** "Khi dựng mặt phẳng (Q) ở cách 2,
   điều kiện BẮT BUỘC nào (Q) phải thoả?"
   - `dap_an_dung`: "(Q) phải chứa 1 đường (ống điều hoà) VÀ song song
     với đường còn lại (ống nước) — nếu chọn (Q) không song song ống
     nước, toàn bộ cách tính sai từ đầu."

---

## TỔNG HỢP KIẾN THỨC (đóng Module 2)

| Khối kiến thức | Nội dung | Xem lại tại |
|---|---|---|
| 1. Đường-mặt song song | Khoảng cách = từ 1 điểm bất kỳ trên đường đến mặt | Bước 1 — cổng trạm thu phí |
| 2. Dựng đoạn vuông góc chung | Tận dụng đường đã ⊥ mặt phẳng nếu có sẵn | Bước 2 |
| 3. Không phải đoạn bất kỳ | Đoạn vuông góc chung PHẢI ⊥ cả 2 đường, và luôn ngắn nhất | Bước 3 |
| 4. Quy về dễ hơn | Đường-mặt song song thường dễ hơn dựng trực tiếp | Bước 4 — ống kỹ thuật |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: toàn bộ 4 bước — dùng `isPerpendicular`/`angleBetweenLines`
   (06 PHẦN C.3), `ConstrainedPoint.dragToward` (PHẦN 2.2) đã có, không
   cần pattern 3D mới.
```

---

> **Trạng thái:** Module 2 (Bài 26) đã có kịch bản đầy đủ 4 bước + Tổng
> hợp kiến thức, số liệu đã verify bằng Python (cổng trạm thu phí, đoạn
> vuông góc chung SA-BC, bẫy đoạn xiên SK, 2 ống kỹ thuật). Module 3
> (luyện tập tổng hợp — vai kỹ sư/kiến trúc sư, dự án cầu thang xoắn) sẽ
> ra kịch bản ở phiên tiếp theo.
