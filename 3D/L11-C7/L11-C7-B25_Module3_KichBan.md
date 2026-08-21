# 📚 KỊCH BẢN — Bài 25, Module 3: "Hình lăng trụ đứng, hình chóp đều, hình hộp chữ nhật"

```
📖 PPCT: Tiết 72 — Chủ đề 9: Hai mặt phẳng vuông góc
🔗 Điều kiện tiên quyết: Module 1, 2 (góc giữa mặt phẳng, điều kiện/tính
   chất vuông góc).
🎯 Sai lầm nhắm tới (PPCT):
   (I) nhầm lăng trụ đứng với lăng trụ đều (đứng chỉ cần cạnh bên ⊥ đáy,
       KHÔNG cần đáy là đa giác đều)
   (J) nghĩ mọi hình chóp đều có mặt bên vuông góc đáy (chỉ đúng vài
       trường hợp đặc biệt)
   (K) nhầm lăng trụ XIÊN thành lăng trụ đứng (dễ nhầm khi đáy đẹp/đều)
   (L) không phân biệt chóp đều (chân đường cao TRÙNG tâm đáy) với chóp
       có đáy đều nhưng đường cao ở vị trí khác
   (M) tính sai diện tích đa giác cơ bản
📁 File: Bai25_Toan3D_Module3_LangTruChopDeuHopChuNhat.html
```

> ⚠️ **Bối cảnh:** Container vận chuyển + khối rubik/hộp quà trong nhà
> kho (warehouse) — đã duyệt, tránh dùng lại kim tự tháp (đã dùng nhiều ở
> Bài 22). Câu chuyện xuyên suốt: học sinh đóng vai **robot quản lý kho
> hàng**, cần phân loại và di chuyển các khối hàng đúng vị trí để xếp
> chồng an toàn.

## Sổ tay kiến thức (hiện dần theo bước)

```
- Lăng trụ đứng: cạnh bên VUÔNG GÓC với 2 đáy. ⚠️ KHÔNG yêu cầu đáy là đa
  giác đều — đáy có thể là tam giác/tứ giác bất kỳ.
- Lăng trụ đều: lăng trụ đứng CÓ THÊM điều kiện đáy là đa giác đều.
- Hình chóp đều: đáy là đa giác đều VÀ chân đường cao (hình chiếu của
  đỉnh) trùng TÂM của đáy.
- Hình hộp chữ nhật: lăng trụ đứng có đáy là hình chữ nhật. Các đường
  chéo bằng nhau và cắt nhau tại trung điểm mỗi đường.
- Hình lập phương: hình hộp chữ nhật có tất cả các cạnh bằng nhau.
```

---

## BƯỚC 1 — Lăng trụ đứng vs lăng trụ đều (phân loại container)

**Cấu hình 3D — mở đầu câu chuyện:**
- **Athena:** "Bạn là robot quản lý kho. Nhiệm vụ: kiểm tra các container
  có XẾP CHỒNG AN TOÀN được không — chỉ container có cạnh bên VUÔNG GÓC
  2 đáy mới xếp chồng ổn định, bất kể đáy hình gì."

**3 container để phân loại (verify Python):**
- Container A: lăng trụ đứng, đáy tam giác THƯỜNG (không đều) — cạnh bên
  vuông góc đáy (dot với pháp tuyến đáy = 1, đúng) → AN TOÀN, dù đáy
  "xấu"/không đều.
- Container B: lăng trụ đứng, đáy lục giác ĐỀU — vừa đứng vừa đều → AN
  TOÀN.
- Container C: lăng trụ XIÊN, đáy lục giác ĐỀU (đẹp, đối xứng) — cạnh
  bên KHÔNG vuông góc đáy (dot lệch khỏi 1, chỉ ≈0,958) → KHÔNG an toàn,
  dù đáy rất đều/đẹp (nhắm trực diện sai lầm K).

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Click vào từng container, đo góc giữa cạnh bên và đáy —
   container nào xếp chồng AN TOÀN?"
   - *Hành động HS:* click từng container, hệ thống hiện góc đo được
     (A: 90°, B: 90°, C: ~73,5° — không vuông).
   - **3-strike:** nếu học sinh chọn sai (VD chọn thiếu A vì đáy "không
     đẹp", hoặc chọn nhầm C vì đáy đẹp):
     - `goi_y_khi_sai`: "Điều kiện AN TOÀN chỉ phụ thuộc góc giữa CẠNH
       BÊN và ĐÁY — không phụ thuộc đáy có đều/đẹp hay không. Đo lại góc
       xem."
     - Hết lượt: hiện đáp án đúng (A, B an toàn; C không) + giải thích:
       "Container A đáy xấu nhưng cạnh bên vuông góc đáy → VẪN là lăng
       trụ ĐỨNG, an toàn. Container C đáy đẹp/đều nhưng cạnh bên xiên →
       KHÔNG là lăng trụ đứng, dễ đổ. 'Đứng' và 'đều' là 2 điều kiện
       ĐỘC LẬP, không suy ra nhau."

2. **Chốt sổ tay:** "Lăng trụ ĐỨNG chỉ cần cạnh bên ⊥ đáy. Lăng trụ ĐỀU
   là đứng + đáy đều — 2 điều kiện tách biệt, container A minh chứng
   'đứng mà không đều', container C minh chứng 'đều mà không đứng'."

---

## BƯỚC 2 — Hình chóp đều: chân đường cao phải trùng tâm đáy

**Cấu hình 3D:** đổi bối cảnh nhỏ trong cùng câu chuyện kho hàng — 1 giá
đỡ hình chóp (dùng đỡ biển chỉ dẫn treo trần kho), đáy hình vuông.

**2 giá đỡ để so sánh (verify Python):**
- Giá đỡ 1: đỉnh đúng tâm đáy — SA=SB=SC=SD (đều bằng 4,123, verify
  khớp) → ỔN ĐỊNH, đúng là chóp đều.
- Giá đỡ 2: đỉnh LỆCH tâm (dù đáy vẫn hình vuông đều) — SA=4,805,
  SB=4,085, SC=3,562, SD=4,369 (khác nhau hoàn toàn) → MẤT CÂN BẰNG, dù
  đáy vẫn là hình vuông đều (nhắm trực diện sai lầm L).

**Thao tác — lời Athena + hành động:**

1. **Athena:** "2 giá đỡ này đều có đáy hình vuông đều. Giá nào ỔN ĐỊNH
   để treo biển chỉ dẫn — nghĩa là đỉnh giá cách đều 4 góc đáy?"
   - *Hành động HS:* click từng giá, hệ thống đo 4 khoảng cách từ đỉnh
     tới 4 góc đáy, hiện số liệu.
   - **Giải thích đúng (giá đỡ 1 đúng):** "Đây là hình chóp ĐỀU thật —
     đáy đều VÀ đỉnh chiếu đúng tâm đáy. Giá đỡ 2 tuy đáy cũng vuông đều,
     nhưng đỉnh bị lệch tâm — 4 khoảng cách khác nhau, KHÔNG phải hình
     chóp đều, dù nhìn thoáng qua đáy vẫn 'đẹp'."

2. **3-strike (nhắm sai lầm J):** "Với 1 hình chóp ĐỀU (đáy đều, đỉnh
   đúng tâm), các MẶT BÊN có luôn vuông góc với đáy không?"
   - `dap_an_dung`: "Không — chỉ đúng trong 1 số trường hợp đặc biệt
     (VD khi chóp rất 'gầy', cao vót), không phải tính chất chung của
     mọi chóp đều."
   - `goi_y_khi_sai`: "Thử tưởng tượng 1 chóp đều rất THẤP (gần như dẹt)
     — mặt bên của nó có gần vuông góc đáy không, hay gần NẰM NGANG (gần
     song song đáy)?"

---

## BƯỚC 3 — Hình hộp chữ nhật: tính chất đường chéo

**Cấu hình 3D:** 1 container dạng hộp chữ nhật chuẩn (kích thước
4×3×2m, kích thước container thật ISO đơn giản hoá).

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đo 2 đường chéo của container này (nối 2 đỉnh đối diện
   qua tâm khối) — chúng có bằng nhau không? Có cắt nhau tại 1 điểm
   không?"
   - *Hành động HS:* click chọn 2 đường chéo, hệ thống đo độ dài + kiểm
     tra giao điểm.
   - Verify Python: cả 2 đường chéo dài đúng 5,3852m, cắt nhau tại đúng
     1 điểm (2, 1.5, 1) — trung điểm của cả 2.
   - **Giải thích đúng:** "Đúng — hình hộp chữ nhật có các đường chéo
     BẰNG NHAU và CẮT NHAU tại trung điểm mỗi đường. Đây là tính chất chỉ
     riêng hình hộp chữ nhật (không đúng cho hình hộp xiên bất kỳ)."

---

## BƯỚC 4 — Hoạt động "Phân loại khối hình" (PPCT gợi ý, có hình gây nhiễu)

**Cấu hình 3D:** 1 "băng chuyền" kho hàng với 6 khối lần lượt xuất hiện,
robot (học sinh) cần kéo mỗi khối vào đúng 1 trong 4 "kệ" phân loại:
**[Lăng trụ đứng]**, **[Lăng trụ đều]**, **[Lăng trụ xiên]**,
**[Không phải lăng trụ]**.

**6 khối (trộn lẫn, có gây nhiễu):**
1. Rubik (lập phương) → Lăng trụ đứng VÀ đều (cả 2 kệ đều đúng, chấp
   nhận thả vào 1 trong 2)
2. Container chữ nhật chuẩn → Lăng trụ đứng
3. Container xiên (đáy lục giác đều nhưng nghiêng, giống Bước 1 Container
   C) → Lăng trụ xiên (KHÔNG phải đứng — bẫy lại sai lầm K lần 2, khác
   bối cảnh)
4. Hộp quà lăng trụ đứng đáy ngũ giác đều → Lăng trụ đứng VÀ đều
5. Giá đỡ chóp (từ Bước 2) → Không phải lăng trụ (là hình chóp)
6. 1 khối đa diện bất kỳ KHÔNG có 2 đáy song song bằng nhau (VD 1 khối
   đá trang trí không đều) → Không phải lăng trụ

**Thao tác:** không có lời giải thích trước — học sinh tự kéo thả, hệ
thống chấm từng khối ngay khi thả (đúng kệ → hiệu ứng xác nhận nhẹ; sai
kệ → khối bật trở lại băng chuyền, không rung mạnh, cho thử lại không
giới hạn số lần vì đây là hoạt động phân loại tự do, không phải 3-strike
chấm điểm).

**Tổng kết hoạt động:** sau khi phân loại hết 6 khối, hiện bảng tổng
hợp lý do đúng/sai cho từng khối, nhấn lại 2 điểm hay nhầm: khối 3
(container xiên đáy đều — dễ tưởng lăng trụ đứng vì đáy đẹp) và khối 5
(giá đỡ chóp — không phải lăng trụ vì chỉ có 1 đáy, không có 2 đáy song
song).

---

## TỔNG HỢP KIẾN THỨC (đóng Module 3)

| Khối kiến thức | Nội dung | Xem lại tại |
|---|---|---|
| 1. Đứng ≠ Đều | Lăng trụ đứng: cạnh bên ⊥ đáy (đáy bất kỳ). Lăng trụ đều: đứng + đáy đều | Bước 1 — container A, B, C |
| 2. Chóp đều | Đáy đều VÀ đỉnh chiếu đúng tâm đáy — thiếu 1 trong 2 thì không phải chóp đều | Bước 2 — giá đỡ |
| 3. Hình hộp chữ nhật | Đường chéo bằng nhau, cắt tại trung điểm | Bước 3 |
| 4. Phân loại tổng hợp | 6 khối, có 2 khối gây nhiễu điển hình | Bước 4 |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: Bước 1-3 (click chọn/đo, hiển thị số liệu tĩnh) — dùng
   `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3) đã verify.
⚠️ Cần chú ý khi build Bước 4: kéo-thả 6 khối vào 4 kệ — về kỹ thuật là
   drag-and-drop cơ bản (không cần pattern 3D phức tạp mới), nhưng cần
   thiết kế UI rõ ràng 4 vùng thả (kệ) đủ lớn trên mobile (≥44px, theo
   đúng checklist responsive `02_design_toan_final.md`).
```

---

> **Trạng thái:** Module 3 (Bài 25) đã có kịch bản đầy đủ 4 bước + Tổng
> hợp kiến thức, số liệu đã verify bằng Python (container đứng/xiên, giá
> đỡ chóp đều/lệch tâm, đường chéo hình hộp chữ nhật). Module 4 (nhập
> vai sửa lỗi — độ dốc mái nhà) và Lab (mở rộng solid_library.html) sẽ ra
> kịch bản ở các phiên tiếp theo.
