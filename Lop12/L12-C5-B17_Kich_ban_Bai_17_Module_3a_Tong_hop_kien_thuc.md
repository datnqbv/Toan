# KỊCH BẢN MODULE 3a — TỔNG HỢP KIẾN THỨC PHƯƠNG TRÌNH MẶT CẦU
## (Bài 17, Toán 12 HK2 — Stage 1 của Module 3, tách riêng thành 1 file)

**Mục tiêu:** Học sinh nhìn lại toàn bộ kiến thức Bài 17 (PT mặt cầu dạng
tâm-bán kính, dạng khai triển + điều kiện tồn tại, 3 vị trí tương đối với
mặt phẳng) trên cùng 1 hình 3D, trước khi luyện tập ở Module 3b (file riêng).

**Loại simulation:** E (xoay đối chiếu) + H (click chọn + nút chuyển trạng
thái)
**Thời gian hoàn thành dự kiến:** ~4 phút
**Design:** Cream & Green, Be Vietnam Pro (đồng bộ hệ thống hiện tại).

---

### Cấu hình 3D (số liệu đã verify bằng script)

**Mặt cầu (S) — cố định:**
```
(S): tâm I(1;2;−1), bán kính R = 5
Dạng tâm-bán kính: (x−1)² + (y−2)² + (z+1)² = 25
Dạng khai triển:   x² + y² + z² − 2x − 4y + 2z − 19 = 0
Kiểm tra: a²+b²+c²−d = 1+4+1−(−19) = 25 = R² ✓
```

**Mặt phẳng (Q) — 3 trạng thái chuyển bằng nút (cùng họ mặt phẳng z=k,
chỉ đổi giá trị k để dễ so sánh trực quan):**

| Trạng thái | Mặt phẳng | d(I,(Q)) | Kết luận |
|---|---|---|---|
| Không cắt | z = −8 | d = \|−1−(−8)\| = 7 > R=5 | Không cắt nhau |
| Tiếp xúc | z = 4 | d = \|−1−4\| = 5 = R | Tiếp xúc tại H(1;2;4) |
| Cắt theo đường tròn | z = 2 | d = \|−1−2\| = 3 < R=5 | Cắt theo đường tròn tâm (1;2;2), bán kính r=√(25−9)=4 |

**Góc camera mặc định:** Nhìn chéo từ trên-phải, thấy rõ mặt cầu + mặt
phẳng cắt qua ở các độ cao khác nhau. OrbitControls tự do.

**Quan hệ hình học cần tính:** khoảng cách điểm-mặt phẳng (đã có sẵn,
Bài 14), công thức Pythagore R²=d²+r² (thuần đại số, không cần hàm riêng).

**Yếu tố hiển thị kèm:** Nhãn I, R, (Q); khi ở trạng thái tiếp xúc/cắt,
hiện thêm điểm H hoặc đường tròn giao tuyến (tô màu riêng, có nhãn bán
kính r).

### Màn hình chính hiển thị

- Canvas 3D chiếm ~65% màn hình, mặt cầu (S) opacity 0.35 (bán trong suốt
  để nhìn xuyên vào tâm), mặt phẳng (Q) opacity 0.2
- 4 nhãn có thể click: **(S) dạng tâm-bán kính · (S) dạng khai triển ·
  (Q) [3 trạng thái] · Đường tròn giao tuyến**
- Panel bên phải hiện thẻ giải thích khi click từng nhãn

### Học sinh tương tác bằng cách

1. Xoay camera quan sát tổng thể trước.
2. Click từng nhãn:
   - **(S) dạng tâm-bán kính:** Thẻ: *"(S): (x−1)²+(y−2)²+(z+1)²=25 — tâm
     I(1;2;−1), bán kính R=5. Lưu ý dấu: từ (x−1)² suy ra hoành độ tâm là
     +1, KHÔNG phải −1 — đây là sai lầm phổ biến nhất của bài."*
   - **(S) dạng khai triển:** Thẻ: *"x²+y²+z²−2x−4y+2z−19=0. Ở đây a=1,
     b=2, c=−1, d=−19. Kiểm tra a²+b²+c²−d = 1+4+1−(−19) = 25 > 0 → đúng
     là phương trình mặt cầu, với R=√25=5."*
   - **(Q):** Hiện 3 nút [Không cắt][Tiếp xúc][Cắt theo đường tròn] —
     bấm từng nút, (Q) trượt lên xuống theo trục z, thẻ cập nhật đúng d,
     so sánh với R, và kết luận tương ứng.
   - **Đường tròn giao tuyến (chỉ hiện khi (Q) ở trạng thái cắt):** Thẻ:
     *"R²=d²+r² → r=√(R²−d²)=√(25−9)=4. Tâm đường tròn giao tuyến là hình
     chiếu vuông góc của I lên (Q), tại đây là (1;2;2) — KHÔNG phải I."*
3. Sau khi click đủ 4 nhãn → nút "Xem tổng kết" mở bảng gộp toàn bộ, xếp
   theo đúng thứ tự logic (PT mặt cầu 2 dạng → 3 vị trí tương đối → công
   thức bán kính giao tuyến).

### Cleanup

Không cần `clearScene()` giữa lần click các nhãn tĩnh. **Chỉ khi đổi
trạng thái (Q)** cần dispose mesh (Q) cũ (và đường tròn giao tuyến nếu
có) trước khi dựng lại, theo đúng pattern PHẦN 3.4-BIS.

### Hoàn thành

`LMS().complete()` bắn khi học sinh đã click đủ 4/4 nhãn.

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** Cấu trúc giống Module 6a/5a đã build — an
  toàn. Điểm mới duy nhất là vẽ đường tròn giao tuyến (1 `CircleGeometry`
  đặt đúng tâm + bán kính r, xoay pháp tuyến theo (Q)) — không phức tạp
  nhưng chưa có sẵn pattern y hệt trong hệ thống, nên **cần verify nhanh
  bằng 1 file test nhỏ trước khi build đại trà** (không phải rủi ro cao,
  chỉ là chưa có tiền lệ y hệt).
- ✅ Toàn bộ số liệu (R=5, d=7/5/3, r=4) đã verify bằng script Python —
  không có số liệu suy đoán. Đã phát hiện và sửa 1 lỗi số liệu trong lúc
  verify (trạng thái "Không cắt" ban đầu chọn z=−6 cho d=5, thực ra là
  tiếp xúc — đã sửa thành z=−8 cho d=7 đúng nghĩa "không cắt").
- ©️ **Rà soát bản quyền:** Số liệu tự đặt mới, không trùng SGK.
