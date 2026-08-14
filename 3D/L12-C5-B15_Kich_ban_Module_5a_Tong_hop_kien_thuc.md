# KỊCH BẢN MODULE 5a — TỔNG HỢP KIẾN THỨC PHƯƠNG TRÌNH ĐƯỜNG THẲNG
## (Bài 15, Toán 12 HK2 — Stage 1 của Module 5, tách riêng thành 1 file)

**Mục tiêu:** Học sinh nhìn lại toàn bộ kiến thức Bài 15 (VTCP, PT tham số,
PT chính tắc, vị trí tương đối 2 đường thẳng, vị trí đường thẳng–mặt phẳng)
trên cùng 1 hình 3D, trước khi luyện tập ở Module 5b (file riêng).

**Loại simulation:** E (xoay đối chiếu) + H (click chọn + nút chuyển trạng
thái)
**Thời gian hoàn thành dự kiến:** ~4 phút
**Design:** Cream & Green (đồng bộ Module 6a) — nền `#FAF7F0`, bảng màu
xanh lá đa cấp độ, font Be Vietnam Pro.

---

### Cấu hình 3D (số liệu đã verify bằng script)

**Đường thẳng d1 (cố định, trục tham chiếu):**
```
d1 qua A(0;1;−2), VTCP u1=(1;2;−1)
PT tham số:   x=t, y=1+2t, z=−2−t
```

**Đường thẳng d2 — 4 trạng thái chuyển bằng nút:**

| Trạng thái | Điểm neo | VTCP | Kiểm tra (đã verify) |
|---|---|---|---|
| Song song | B(3;0;4) | u2=(2;4;−2) *(=2·u1)* | Cùng phương u1; B không thuộc d1 (thử t: không có t nào cho (3,0,4)) |
| Trùng | B'(2;5;−4) | u2=(2;4;−2) | Cùng phương u1; B'=A+2·u1 (t=2) → B' thuộc d1 |
| Cắt | C(−1;5;−5) | u3=(1;−1;1) | Không cùng phương u1; cắt d1 tại P0(1;3;−3), ứng t=1 (d1) và s=2 (d2) |
| Chéo | D(4;4;4) | u4=(1;0;1) | Không cùng phương u1; hệ phương trình vô nghiệm (đã verify bằng thế số) |

**Mặt phẳng (P) — dùng để ôn lại quan hệ đường thẳng–mặt phẳng (Module 4):**
```
(P): x + y + z − 6 = 0     (n=(1;1;1))
d1 cắt (P) tại t=3.5, giao điểm (3.5; 8; −5.5)
```

**Góc camera mặc định:** Nhìn chéo từ trên, thấy rõ cả d1 và vùng không
gian đủ rộng để hiện đủ 4 vị trí của d2 khi chuyển trạng thái.

**Quan hệ hình học cần tính:** hàm kiểm tra cùng phương (dot/cross đơn
giản), `classifyLineToPlane`, `lineIntersectPlane` — đều đã ✅ verify.

**Yếu tố hiển thị kèm:** Nhãn A, u1, d1 cố định luôn hiện; d2 đổi màu theo
từng trạng thái (dùng đúng `COLOR_QUADRIC` gamma xanh lá đã có, không cần
màu mới); điểm giao P0 (trạng thái cắt) và giao điểm với (P) đều đánh dấu
rõ.

### Màn hình chính hiển thị

- Canvas 3D chiếm ~65% màn hình, d1 luôn hiện, d2 đổi theo nút chọn
- 6 nhãn có thể click: **u1 · PT tham số (d1) · PT chính tắc (d1) · d2
  (4 trạng thái) · (P) · Giao điểm d1∩(P)**
- Panel bên phải hiện thẻ giải thích khi click từng nhãn

### Sổ tay kiến thức nền tảng

Không có ô riêng — module này đóng vai trò sổ tay kiến thức bằng
click-and-reveal, giống Module 6a.

### Học sinh tương tác bằng cách

1. Xoay camera quan sát tổng thể trước.
2. Click từng nhãn:
   - **u1:** Highlight vectơ u1. Thẻ: *"u1=(1;2;−1) là VTCP của d1 — giá
     của u1 song song hoặc trùng với d1."*
   - **PT tham số (d1):** Thẻ: *"x=t, y=1+2t, z=−2−t — mỗi giá trị t cho
     1 điểm thuộc d1."*
   - **PT chính tắc (d1):** Thẻ: *"(x−0)/1 = (y−1)/2 = (z+2)/(−1) — viết
     được vì cả 3 thành phần của u1 đều khác 0."*
   - **d2:** Hiện 4 nút [Song song][Trùng][Cắt][Chéo] trong thẻ — bấm từng
     nút, d2 đổi vị trí, thẻ cập nhật đúng điều kiện đại số + số liệu.
     - *Song song:* "u2 cùng phương u1, nhưng B(3;0;4) không thuộc d1 →
       song song, không trùng."
     - *Trùng:* "u2 cùng phương u1, và B'(2;5;−4) thuộc d1 (ứng t=2) →
       trùng nhau — cùng 1 đường thẳng."
     - *Cắt:* "u3 không cùng phương u1. Giải hệ tìm được d1 và d2 cắt
       nhau tại P0(1;3;−3)."
     - *Chéo:* "u4 không cùng phương u1, nhưng hệ phương trình vô nghiệm
       → 2 đường thẳng không có điểm chung, không đồng phẳng → chéo nhau."
   - **(P):** Thẻ hiện phương trình (P) và VTPT n=(1;1;1).
   - **Giao điểm d1∩(P):** Thẻ: *"u1·n=2≠0 → d1 cắt (P) tại t=3.5, toạ độ
     (3.5; 8; −5.5) — đây chính là kỹ năng của Module 4."*
3. Sau khi click đủ 6 nhãn → nút "Xem tổng kết" mở bảng gộp toàn bộ, xếp
   theo đúng thứ tự logic (VTCP → tham số → chính tắc → vị trí 2 đường
   thẳng → vị trí đường thẳng-mặt phẳng).

### Cleanup

Không cần `clearScene()` giữa lần click các nhãn tĩnh (u1, PT, (P)...).
**Chỉ khi đổi trạng thái d2** cần dispose mesh d2 cũ trước khi dựng mesh
mới, theo đúng pattern PHẦN 3.4-BIS.

### Hoàn thành

`LMS().complete()` bắn khi học sinh đã click đủ 6/6 nhãn.

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** Giống cấu trúc Module 6a đã build — an toàn,
  chỉ cần dispose đúng d2 khi đổi trạng thái.
- ✅ Toàn bộ 4 trạng thái d2 + quan hệ d1-(P) đã verify bằng script Python
  (dot product, thế điểm, giải hệ) — xem bảng trên, không có số liệu suy
  đoán.
- ©️ Số liệu tự đặt mới, không trùng SGK.
