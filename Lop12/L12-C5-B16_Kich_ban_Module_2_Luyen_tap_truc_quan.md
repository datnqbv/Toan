# KỊCH BẢN MODULE 2 — LUYỆN TẬP TRỰC QUAN
## Góc giữa 2 mặt phẳng & luyện tập tổng hợp 3 loại góc
### (Bài 16, Toán 12 HK2, Tiết 29 — bổ sung bên dưới video manim)

**Mục tiêu:** Bổ sung phần thực hành trên canvas 3D sau video manim lý
thuyết — tính góc giữa 2 mặt phẳng, sau đó tổng hợp cả 3 loại góc trên
cùng 1 hình (đúng yêu cầu PPCT Module 2).

**Sai lầm cần giải quyết (từ PPCT):**
- Nhầm dùng sin hay côsin giữa 3 loại góc.
- Chọn sai vectơ đại diện (dùng VTPT thay VTCP hoặc ngược lại).
- Sai dấu khi tính toán với vectơ có nhiều thành phần âm.

**Loại simulation:** F (dựng dần từng bước)
**Thời gian hoàn thành dự kiến:** ~8-9 phút
**Design:** Cream & Green, Be Vietnam Pro.

**File độc lập với Module 1** — vì vậy mở đầu bằng phần **dẫn dắt, dựng
lại nhanh** scene nhà kính đã làm ở Module 1, trước khi vào nội dung mới.

---

### Phần dẫn dắt — Quay lại nhà kính đã dựng ở Module 1

**Không lặp lại toàn bộ các bước tính toán cũ** (học sinh đã làm rồi ở
Module 1) — chỉ dựng lại NHANH toàn bộ hình đã có sẵn kết quả, kèm 1 dòng
nhắc lại ngắn, để học sinh định hướng trước khi học nội dung mới:

> 🔄 **"Ở phần trước, chúng ta đã dựng 1 nhà kính có khung thép chéo trên
> nóc và 1 mái kính (Q). Ta đã tính được: góc giữa 2 thanh thép ≈ 79,5°
> (và ≈ 56,8° ở cặp thứ 2), góc giữa thanh chống và mái kính ≈ 32,3°. Giờ
> ta sẽ thêm 1 mái kính thứ 2, tạo thành mái chữ A, để học cách tính góc
> giữa 2 mặt phẳng."**

Canvas hiện luôn TOÀN BỘ hình đã hoàn thiện (khung nhà kính + 4 thanh thép
+ mái (Q)) — không yêu cầu học sinh tính lại, chỉ là bối cảnh nền để tiếp
tục xây dựng. Có 1 nút nhỏ "🔍 Xem lại 3 góc đã tính" — bấm vào để
highlight lần lượt từng cặp đối tượng + hiện số liệu góc tương ứng (chỉ
xem, không phải làm lại).

### Cấu hình 3D bổ sung (số liệu đã verify bằng script)

**Mái kính thứ 2 (R) — tạo hình mái dốc 2 phía kiểu "nhà kính mái chữ A":**
```
(R): x − y + z − 5 = 0     (VTPT n'=(1;−1;1))
```

**Bước 1 — Góc giữa (Q) và (R), gồm 2 bài luyện tập liên tiếp (giống cấu
trúc đã quen ở Module 1 — 1 ví dụ dễ trước, 1 ví dụ ép tình huống dấu âm
sau):**

**Bài luyện tập 1 (làm quen — (Q) và (R)):**
```
cos(góc) = |n·n'| / (|n|·|n'|) = |2−1+2| / (3·√3) = 3/(3√3) = 1/√3 ≈ 0.577
→ góc ≈ 54,7°
```

**Bài luyện tập 2 (thêm 1 vách kính bên hông nhà kính (S), nghiêng nhẹ ra
ngoài để thoát nước mưa — ép tình huống tích vô hướng VTPT âm):**
```
Vách bên (S): −3x + y + 2z − 8 = 0     (VTPT n''=(−3;1;2))

n'·n'' = 1·(−3) + (−1)·1 + 1·2 = −2   (ÂM)
cos(góc giữa (R) và (S)) = |n'·n''| / (|n'|·|n''|) = |−2| / (√3·√14) = 2/√42 ≈ 0.309
→ góc ≈ 72,0°
```

**Bước 2 — Luyện tập tổng hợp (phối hợp cả 3 loại góc trên cùng 1 hình):**
```
sin(góc giữa thanh thép 1 [Module 1] và mái (R)) = |v1·n'| / (|v1|·|n'|)
= |2−1+0| / (√5·√3) = 1/√15 ≈ 0.258 → góc ≈ 15,0°
```

### Bảng tra nhanh tương tác "Ba loại góc trong không gian"

Đúng theo gợi ý PPCT — panel bên cạnh canvas, 3 thẻ có thể click:

| Thẻ | Công thức | Vectơ đại diện | Hàm dùng |
|---|---|---|---|
| Đường – Đường | cos = \|u·u'\|/(\|u\|\|u'\|) | 2 VTCP | Côsin |
| Đường – Mặt | sin = \|u·n\|/(\|u\|\|n\|) | VTCP + VTPT | Sin |
| Mặt – Mặt | cos = \|n·n'\|/(\|n\|\|n'\|) | 2 VTPT | Côsin |

Click vào từng thẻ → highlight đúng đối tượng tương ứng trên hình 3D đang
có + hiện lại đúng phép tính vừa làm làm ví dụ minh hoạ, không cần ví dụ
mới. Giúp học sinh "nhìn thấy" vì sao đường-mặt khác biệt (dùng sin) so
với 2 loại còn lại (dùng côsin).

---

### Học sinh tương tác bằng cách (loại F — dựng dần)

**Bước 1 (2 bài luyện tập liên tiếp):**

*Bài luyện tập 1:*
1. Mái (R) xuất hiện thêm trên canvas (mờ, opacity 0.2), tạo hình mái chữ
   A hoàn chỉnh với (Q).
2. Câu hỏi lựa chọn công thức trước khi tính: "Đây là góc giữa 2 mặt
   phẳng — dùng sin hay côsin, vectơ đại diện là gì?" → chọn **côsin, 2
   VTPT** (đánh vào sai lầm "chọn sai vectơ đại diện" PPCT nêu).
3. Tính n·n', |n|, |n'|, cos, nhập từng bước → xác nhận ≈ 54,7°.

*Bài luyện tập 2 (thêm vách bên (S), KHÔNG xoá (Q), (R)):*
1. Học sinh lặp lại quy trình: tính n'·n'', nhận được −2 (âm).
2. Hệ thống xác nhận đúng, nhắc: *"Đúng, tích vô hướng ra −2. Nhớ quan
   sát dấu trước khi kết luận cos."*
3. Nếu nhập cos = −2/√42 (quên trị tuyệt đối) → phản hồi: *"cos âm nghĩa
   là góc tù — góc giữa 2 mặt phẳng cũng luôn ≤ 90°, giống góc giữa 2
   đường thẳng. Kiểm tra lại trị tuyệt đối."*
4. Xác nhận đáp số đúng: cos ≈ 0,309 → góc ≈ 72,0°.
5. Ghi chú cố định dưới bài 2: *"💡 Quy tắc trị tuyệt đối áp dụng CHO CẢ
   3 loại góc, không chỉ riêng góc giữa 2 đường thẳng — vì cả góc giữa 2
   mặt phẳng và góc giữa đường thẳng-mặt phẳng đều được định nghĩa trong
   [0°;90°]."*

**Bước 2 (luyện tập tổng hợp):**
1. Câu hỏi: "Tính góc giữa thanh thép 1 (đã dựng ở phần trước) và mái
   (R)."
2. Học sinh phải tự nhận ra: đây là góc đường-mặt (không phải đường-đường
   như Bước 1 Module 1, cũng không phải mặt-mặt như Bước 1 vừa làm ở
   trên) → chọn đúng công thức **sin** trước khi tính.
3. Tính ra ≈ 15,0°.
4. Sau bước này, hiện bảng tổng kết toàn bộ góc đã tính qua cả Module 1 và
   2 (79,5° / 56,8° / 32,3° / 54,7° / 72,0° / 15,0°) trên cùng 1 hình 3D,
   để học sinh thấy rõ 1 công trình thực tế có thể chứa đủ cả 3 loại góc
   cùng lúc.

### Cleanup

Không `clearScene()` xuyên suốt file này — chỉ thêm đối tượng mới (mái
(R), vách (S)) vào scene tái dựng ban đầu.

### Hoàn thành

`LMS().complete()` bắn sau khi hoàn thành Bước 2.

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** File độc lập — cần dựng lại TOÀN BỘ scene
  Module 1 (khung nhà kính, 4 thanh thép, mái (Q)) ở phần dẫn dắt đầu bài,
  dùng ĐÚNG số liệu đã verify ở kịch bản Module 1 (không tính lại, chỉ vẽ
  lại hình). Đây là phần code trùng giữa 2 file — nên tách thành 1 hàm
  dựng scene chung `buildGreenhouseBase()` dùng lại ở cả 2 file, tránh
  chép tay 2 lần dễ lệch số liệu.
- ✅ Toàn bộ góc mới trong file này (54,7° / 72,0° / 15,0°) đã verify bằng
  script Python.
- ✅ Cấu trúc "2 bài luyện tập liên tiếp" (ví dụ dễ trước, ví dụ ép dấu âm
  sau) được lặp lại nhất quán với Module 1 — giúp học sinh nhận ra đây là
  1 khuôn mẫu chung áp dụng cho cả 3 loại góc, không phải đặc thù riêng
  góc đường-đường.
- ©️ **Rà soát bản quyền:** Vách bên (S) là bối cảnh mới tự thêm, không
  trùng SGK. Bảng tra nhanh 3 loại góc đúng theo gợi ý PPCT (không phải
  lấy từ SGK).
