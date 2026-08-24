# 📚 KỊCH BẢN — Bài 27, Module 3: "Luyện tập mở rộng" (ngoài PPCT)

```
📌 KHÔNG thuộc PPCT gốc — module BỔ SUNG theo yêu cầu, bao quát các dạng
   bài SGK còn lại (7.28-7.31) mà Module 1-2 chưa luyện tới. Định dạng:
   4 bài ĐỘC LẬP, không nhập vai (khác Module 2 có vai kỹ sư/nhà thiết
   kế) — đúng tinh thần "ôn luyện nhanh, đa dạng dạng bài".
📁 File: Bai27_Toan3D_Module3_LuyenTapMoRong.html
```

> ⚠️ **Bối cảnh:** cả 4 bài lấy ý tưởng kỹ thuật từ SGK Bài tập
> 7.28-7.31, đã đổi số liệu cụ thể (không dùng nguyên số SGK).

## Đặc tả hình ảnh & màu sắc

**Hook mở đầu module (SVG viewBox 0 0 600 160):**
```
- 4 khối nhỏ xếp ngang, mỗi khối gắn 1 số La Mã (I, II, III, IV): tứ
  diện (--il-terracotta), lăng trụ đứng đáy tam giác (--il-slate), 2
  chóp đều nhỏ cạnh nhau (--il-ochre, cho Bài 3 — gợi ý "2 trường hợp"),
  lăng trụ xiên (--il-dusty-blue).
- Không cần nhân vật/bối cảnh nghề nghiệp — giữ tinh thần "sổ tay ôn
  luyện" gọn, khác hẳn Module 2.
```

**Bảng màu (dùng lại đúng token đã có, nhất quán toàn hệ thống):**

| Đối tượng | Token | Vai trò |
|---|---|---|
| Khối chính đang tính | `--il-slate` | Đối tượng chung |
| Đoạn/mặt kết quả ĐÚNG | `--jade` | Đáp án chốt |
| Đoạn dễ nhầm (Bài 3: OA vs OM) | 2 màu đối lập `--accent` / `--il-dusty-blue` | Phân biệt 2 lựa chọn dễ nhầm |

**Quy ước nhãn:** giữ đúng hệ thống R1 (số đo)/R3 (cung góc)/R4 (dấu
vuông) như mọi module trước.

---

## BÀI 1 — Từ chóp đều đến tứ diện đều

**Đề bài:** "Cho hình chóp tam giác đều S.ABC, cạnh đáy a=6, cạnh bên
b=5. Tính V."

**Cấu hình 3D:** chóp tam giác đều, đáy tô mờ `--il-sand`, đoạn OA (bán
kính đáy) và SO (chiều cao — kết quả cần tính) tô `--jade`.

**Thao tác — lời Athena + hành động:**

1. Học sinh tính OA (bán kính đường tròn ngoại tiếp tam giác đều đáy),
   rồi SO (Pythagore trong tam giác SOA), rồi V — hệ thống chặn từng
   bước.
   - Verify Python: OA=3,4641, SO=3,6056, V=18,735.

2. **Câu hỏi mở rộng (không chấm gắt):** "Nếu bây giờ đổi b=6 (bằng a) —
   nghĩa là chóp trở thành TỨ DIỆN ĐỀU — bấm nút 'Đổi b=a' để xem V thay
   đổi thế nào, rồi so với công thức V=a³√2/12 đã học/nghe qua ở đâu đó."
   - *Hành động HS:* kéo slider b từ 5 lên 6, quan sát khối chóp "cao
     lên" thành tứ diện đều thật (4 mặt đều là tam giác đều bằng nhau).
   - Verify Python: tại b=a=6, V=25,4558 = đúng a³√2/12.
   - **Chốt:** "Công thức 'quen thuộc' của tứ diện đều KHÔNG PHẢI 1 công
     thức riêng cần nhớ thêm — chỉ là 1 trường hợp ĐẶC BIỆT của công
     thức chóp đều tổng quát khi cạnh bên = cạnh đáy."

---

## BÀI 2 — Lăng trụ đứng, đáy tam giác có góc cho trước

**Đề bài:** "Lăng trụ đứng ABC.A'B'C', AA'=4, AB=5, BC=3, góc ABC=140°.
Tính V."

**Cấu hình 3D:** lăng trụ đứng đáy tam giác thường (KHÔNG đều, KHÔNG
vuông — nhấn mạnh "không có đường cao có sẵn"), đáy tô mờ, góc ABC=140°
hiện rõ cung góc R3 tại B.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Tam giác đáy này không vuông, không đều, không có sẵn
   đường cao để tính diện tích trực tiếp. Có cách nào tính diện tích chỉ
   từ 2 cạnh AB, BC và góc xen giữa ABC không?"
   - `dap_an_dung`: "S = (1/2)·AB·BC·sin(ABC) — công thức diện tích tam
     giác biết 2 cạnh và góc xen giữa (đã học ở lượng giác)."
   - `goi_y_khi_sai`: "Thử nhớ lại công thức diện tích tam giác dùng
     sin của góc xen giữa 2 cạnh, không cần đường cao."

2. Tính S_đáy=4,8209, rồi V=S·AA'=19,2836.

3. **Chốt (nhắm thói quen hay quên):** "Khi tập trung vào phần '3D'
   (chiều cao, thể tích), dễ quên rằng phần '2D' (diện tích đáy) cũng có
   thể cần kỹ thuật lượng giác, không phải luôn có sẵn đường cao."

---

## BÀI 3 — Phân biệt "góc cạnh bên-đáy" vs "góc mặt bên-đáy" (bài quan trọng nhất)

**Đề bài:** "Chóp tứ giác đều đáy cạnh 5. TH1: CẠNH BÊN tạo với đáy góc
50°. TH2: MẶT BÊN tạo với đáy góc 40°. Tính V mỗi trường hợp."

**Cấu hình 3D:** 2 chóp đặt CẠNH NHAU (không phải 1 mô hình đổi qua đổi
lại) để so sánh trực tiếp bằng mắt:
- Chóp TH1: đoạn OA (tâm đáy tới ĐỈNH đáy) tô `--accent`, góc SAO (giữa
  cạnh bên SA và đáy) hiện cung R3 tại A.
- Chóp TH2: đoạn OM (tâm đáy tới TRUNG ĐIỂM cạnh đáy) tô `--il-dusty-blue`
  (màu khác hẳn TH1, tránh nhầm), góc SMO (giữa mặt bên và đáy) hiện
  cung R3 tại M.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "2 hình chóp này có ĐÁY GIỐNG NHAU (cạnh bằng 5) nhưng góc cho khác
   loại, 1 bên là góc của CẠNH BÊN với đáy, 1 bên là góc của MẶT BÊN với đáy.
   Đoạn nào dùng để tính chiều cao trong mỗi trường hợp?"
   - *Hành động HS:* click chọn đúng đoạn (OA cho TH1, OM cho TH2) trên
     từng mô hình — hệ thống CHẶN nếu chọn nhầm (VD chọn OM cho TH1).

2. **3-strike (nhắm trực diện sai lầm quan trọng nhất của bài):** "Nếu
   dùng NHẦM đoạn OM (thay vì OA) để tính chiều cao ở TH1, kết quả V sẽ
   sai theo hướng nào?"
   - `dap_an_dung`: "Sai — vì OM < OA (khoảng cách tâm tới trung điểm
     cạnh luôn ngắn hơn tâm tới đỉnh), dùng nhầm OM sẽ cho chiều cao SAI
     (không khớp với góc 50° đã cho tại đỉnh A), làm V sai hoàn toàn,
     không phải chỉ lệch nhẹ."
   - `goi_y_khi_sai`: "Góc 50° trong TH1 đo tại ĐỈNH nào của tam giác
     vuông chứa nó — đỉnh A (góc cạnh bên) hay đỉnh M (góc mặt bên)?"
   - Hết lượt: hiện rõ 2 kết quả cạnh nhau — V(TH1)=35,1124,
     V(TH2)=17,4812 — **gấp hơn 2 lần**, để thấy hậu quả THẬT của nhầm
     lẫn này, không chỉ là lý thuyết trừu tượng.

3. **Liên hệ:** "Đây chính là 2 khái niệm đã học riêng ở Bài 24 — góc
   giữa ĐƯỜNG THẲNG và mặt phẳng (cạnh bên-đáy) khác góc giữa 2 MẶT
   PHẲNG (mặt bên-đáy, thực chất là góc nhị diện liên quan Bài 25)."

---

## BÀI 4 — Lăng trụ xiên có 3 cạnh bên từ 1 đỉnh bằng nhau

**Đề bài:** "Lăng trụ ABC.A'B'C', đáy là tam giác đều cạnh 4, và
A'A=A'B=A'C=6. Tính V."

**Cấu hình 3D:** lăng trụ XIÊN (cạnh bên không vuông góc đáy — nhấn mạnh
qua góc nghiêng rõ trên hình), đáy tam giác đều tô mờ, đoạn OA' (chiều
cao thật, kết quả cần tìm) tô `--jade`, phân biệt rõ với cạnh bên A'A
(tô `--il-slate`, khác hẳn OA').

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Lăng trụ này là Lăng trụ XIÊN — cạnh bên A'A không vuông góc đáy.
   Nhưng biết A'A=A'B=A'C (cách đều 3 đỉnh đáy). Điều này cho ta biết gì về
   vị trí hình chiếu của A' trên đáy?"
   - `dap_an_dung`: "Hình chiếu của A' trùng TÂM đường tròn ngoại tiếp
     tam giác đáy — vì A' cách đều A, B, C (đúng kỹ thuật đã học ở Bài
     25/26 cho hình chóp, áp dụng tương tự ở đây cho lăng trụ)."
   - `goi_y_khi_sai`: "Điểm nào trong mặt đáy cách đều cả 3 đỉnh A, B,
     C?"

2. Tính OA (bán kính đáy)=2,3094, chiều cao thật h=5,5377 (Pythagore từ
   A'A=6), V=S_đáy·h=38,3667.

3. **Chốt:** "Kỹ thuật 'cách đều 3 điểm → hình chiếu là tâm' không chỉ
   dùng cho HÌNH CHÓP — áp dụng được cho MỌI trường hợp có 1 điểm cách
   đều 3 điểm khác trong 1 mặt phẳng, kể cả lăng trụ xiên như bài này."

---

## TỔNG HỢP KIẾN THỨC (đóng Module 3 — đóng toàn bộ Bài 27)

| Bài | Kỹ thuật ôn lại | Liên hệ |
|---|---|---|
| 1 | Tứ diện đều = trường hợp đặc biệt của chóp đều | Module 1 |
| 2 | Diện tích tam giác biết 2 cạnh + góc xen giữa | Lượng giác đã học |
| 3 | Phân biệt góc cạnh bên-đáy ≠ góc mặt bên-đáy | Bài 24, 25 |
| 4 | "Cách đều 3 điểm → hình chiếu là tâm" áp dụng cho cả lăng trụ | Bài 25, 26 |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: cả 4 bài — dựng hình tĩnh + đo/tính, dùng
   `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3) đã có, không cần
   pattern 3D mới.
✅ An toàn: Bài 1 (slider b đổi chóp đều thành tứ diện đều) — chỉ là đổi
   1 tham số hình học đơn giản, không cần pattern mới.
✅ An toàn: Bài 3 (2 mô hình đặt cạnh nhau, click chọn đoạn) — pattern
   click-chọn-chặn đã dùng nhiều lần ở các module trước.
```

---

> **Trạng thái:** Module 3 (Bài 27, module bổ sung ngoài PPCT) đã có
> kịch bản đầy đủ 4 bài, có tương tác 3-strike cho Bài 3 (bẫy quan trọng
> nhất), đặc tả hình ảnh đầy đủ theo đúng quy chuẩn các module trước. Số
> liệu đã verify bằng Python. **Bài 27 giờ có đầy đủ 3 module + trang
> Tổng hợp trực quan.**
