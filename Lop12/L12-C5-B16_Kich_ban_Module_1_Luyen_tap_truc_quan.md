# KỊCH BẢN MODULE 1 — LUYỆN TẬP TRỰC QUAN
## Góc giữa 2 đường thẳng & góc giữa đường thẳng-mặt phẳng
### (Bài 16, Toán 12 HK2, Tiết 28 — bổ sung bên dưới video manim)

**Mục tiêu:** Bổ sung phần thực hành trên canvas 3D sau video manim lý
thuyết — học sinh làm từng bước (loại F), gắn với 1 bài toán thực tế.

**Sai lầm cần giải quyết (từ PPCT):**
- Quên lấy trị tuyệt đối ở tử số → ra cos âm → góc tù (vô lý, vì góc giữa
  đường thẳng/mặt phẳng luôn trong [0°;90°]).
- Nhầm dùng sin hay côsin (đường-đường dùng côsin; đường-mặt dùng sin).
- Bấm máy tính sai chế độ Radian/Degree.

**Loại simulation:** F (dựng dần từng bước)
**Thời gian hoàn thành dự kiến:** ~7-8 phút
**Design:** Cream & Green, Be Vietnam Pro (đồng bộ hệ thống hiện tại).

---

### Bối cảnh: Nhà kính trồng cây có khung thép chéo

Trên nóc nhà kính có 2 cặp thanh thép chéo giằng nhau; có 1 thanh chống
nghiêng đâm từ trong ra xuyên qua mái kính.

### Cấu hình 3D (số liệu đã verify bằng script)

**Khung nhà kính (nền cố định):** 1 khối hộp mờ (opacity 0.12), kích
thước 4×4×5, làm tham chiếu không gian — không phải đối tượng tính toán.

**Bước 1 — Góc giữa 2 đường thẳng (dùng côsin), gồm 2 bài luyện tập
liên tiếp trên cùng 1 canvas:**

**Bài luyện tập 1 (làm quen cách tính):**
```
Thanh thép 1: qua E1(0;0;3), VTCP v1=(2;1;0)
Thanh thép 2: qua E2(4;0;5), VTCP v2=(1;−1;2)

cos(góc) = |v1·v2| / (|v1|·|v2|) = |2−1+0| / (√5·√6) = 1/√30 ≈ 0.183
→ góc ≈ 79,5°
```

**Bài luyện tập 2 (sau khi đã quen — ép đúng tình huống cos âm trước khi
lấy trị tuyệt đối):**
```
Thanh thép 3: qua G1(0;4;3), VTCP v3=(2;1;0)
Thanh thép 4: qua G2(4;4;5), VTCP v4=(−1;−1;2)

v3·v4 = 2·(−1) + 1·(−1) + 0·2 = −3   (ÂM)
cos(góc) = |v3·v4| / (|v3|·|v4|) = |−3| / (√5·√6) = 3/√30 ≈ 0.548
→ góc ≈ 56,8°
```

**Bước 2 — Góc giữa thanh chống nghiêng và mái kính (dùng sin):**
```
Mái kính (Q): 2x + y + 2z − 12 = 0     (VTPT n=(2;1;2))
Thanh chống: qua F(2;2;4), VTCP w=(1;−2;3)

sin(góc) = |w·n| / (|w|·|n|) = |2−2+6| / (√14·3) = 6/(3√14) = 2/√14 ≈ 0.535
→ góc ≈ 32,3°
```

---

### Học sinh tương tác bằng cách (loại F — dựng dần)

**Bước 1 (2 bài luyện tập liên tiếp):**

*Bài luyện tập 1:*
1. Canvas hiện sẵn khung nhà kính mờ + thanh thép 1, 2 (cho trước toạ độ
   2 đầu mút mỗi thanh — KHÔNG cho sẵn VTCP, học sinh phải tự suy ra).
2. Ô nhập: "Xác định VTCP của thanh thép 1" — học sinh nhập (2;1;0) từ
   toạ độ 2 đầu mút cho trước.
3. Tương tự cho thanh thép 2.
4. Ô nhập: "Tính cos(góc) giữa 2 thanh" — chấp nhận cả dạng phân số/số
   thập phân gần đúng.
5. Xác nhận đáp số góc ≈ 79,5° (làm tròn 1 chữ số thập phân theo đúng quy
   ước SGK "Trong bài học này, nếu không nói gì thêm, ta quy ước tính góc
   theo đơn vị độ và làm tròn đến chữ số thập phân thứ nhất").

*Bài luyện tập 2 (mở ra ngay sau khi hoàn thành bài 1 — thêm thanh thép
3, 4 vào canvas, KHÔNG xoá thanh thép 1, 2):*
1. Học sinh lặp lại đúng quy trình: xác định VTCP thanh thép 3, 4, rồi
   tính tích vô hướng v3·v4.
2. Khi học sinh nhập kết quả tích vô hướng (−3, đúng), hệ thống xác nhận
   đúng nhưng nhắc thêm: *"Đúng, tích vô hướng ra −3. Bước tiếp theo tính
   cos — nhớ quan sát dấu của kết quả trước khi kết luận."*
3. Nếu học sinh nhập cos = −3/√30 (quên trị tuyệt đối) → hệ thống phản
   hồi riêng: *"cos âm nghĩa là góc tù — nhưng góc giữa 2 đường thẳng
   trong không gian luôn ≤ 90°. Kiểm tra lại: có lấy trị tuyệt đối ở tử
   số chưa?"*
4. Xác nhận đáp số đúng: cos ≈ 0,548 → góc ≈ 56,8°.
5. **Ngay dưới bài luyện tập 2**, hiện ghi chú cố định (luôn hiển thị sau
   khi hoàn thành bài, không phải phản hồi khi sai): *"💡 Tích vô hướng
   v3·v4 ra số ÂM (−3) — nếu không lấy trị tuyệt đối ở tử số, cos sẽ âm,
   dẫn đến góc tù (>90°). Nhưng góc giữa 2 đường thẳng trong không gian
   LUÔN nằm trong [0°;90°] — đây là lý do công thức bắt buộc phải có dấu
   trị tuyệt đối, không phải quy ước tuỳ ý."*

**Bước 2:**
1. Mái kính (Q) xuất hiện thêm trên canvas (mờ, opacity 0.2).
2. Ô nhập: "Đây là góc giữa đường thẳng và mặt phẳng — công thức dùng sin
   hay côsin?" (câu hỏi nhỏ trước khi tính, buộc học sinh chọn đúng công
   thức, đánh đúng vào sai lầm PPCT nêu) → chọn **sin**.
3. Học sinh tính w·n, |w|, |n|, rồi sin(góc), nhập từng bước.
4. Xác nhận đáp số góc ≈ 32,3°.

### Cleanup

Không `clearScene()` giữa các bài luyện tập/bước trong file này — mỗi đối
tượng mới (thanh thép 3&4, mái (Q)) chỉ THÊM vào scene đang có, giữ nguyên
đối tượng cũ (đúng tinh thần "case study nối tiếp" trong 1 file).

### Hoàn thành

`LMS().complete()` bắn sau khi hoàn thành Bước 2.

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** File độc lập, 1 canvas dùng xuyên suốt toàn
  bài, không cần `clearScene()` (chỉ cộng thêm đối tượng). An toàn.
- ✅ Toàn bộ 3 góc (79,5° / 56,8° / 32,3°) đã verify bằng script Python.
- ©️ **Rà soát bản quyền:** Bối cảnh "nhà kính khung thép chéo" hoàn toàn
  mới, không trùng SGK (SGK Bài 16 không có ví dụ thực tế cụ thể ở phần
  lý thuyết). PPCT gợi ý "đo góc dây cáp treo" — không dùng lại vì bối
  cảnh "dây cáp treo" đã dùng ở Module 5b Vòng 1 (Bài 15), tránh lặp bối
  cảnh nội bộ hệ thống.
- 📌 **Lưu ý cho Module 2 (file riêng):** Module 2 sẽ cần DỰNG LẠI scene
  này (khung nhà kính + thanh thép 1-4 + mái (Q)) ở phần dẫn dắt đầu bài,
  vì đây là 2 file độc lập — xem kịch bản Module 2 để biết cách dẫn dắt.
