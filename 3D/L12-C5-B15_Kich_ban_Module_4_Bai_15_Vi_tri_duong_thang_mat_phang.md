# KỊCH BẢN MODULE 4 — VỊ TRÍ TƯƠNG ĐỐI GIỮA ĐƯỜNG THẲNG VÀ MẶT PHẲNG
## (Bài 15, Toán 12 HK2, Tiết 26)

> PPCT ghi rõ hình thức nội dung module này là **"simulation"** (khác Module
> 1-3 chỉ là video manim) — bắt buộc phải là simulation tương tác đầy đủ.

**Mục tiêu:** Học sinh xét được vị trí tương đối giữa 1 đường thẳng và 1 mặt
phẳng (cắt nhau / song song / nằm trong) bằng phương pháp toạ độ, tìm được
giao điểm khi cắt nhau.

**Sai lầm cần giải quyết (từ PPCT):**
- Thấy u·n=0 rồi vội kết luận song song, **quên kiểm tra 1 điểm trên đường
  thẳng có thuộc mặt phẳng không** — nếu thuộc thì đường thẳng NẰM TRONG mặt
  phẳng, không phải song song.
- Sai sót khi thế phương trình tham số vào phương trình mặt phẳng để giải
  tìm t (giao điểm).

**Loại simulation:** G (slider tham số, kéo tay cần liên tục) + H (nút
chuyển 3 trạng thái rời rạc) + I (2 câu kiểm tra nhanh cuối bài)
**Thời gian hoàn thành dự kiến:** ~6-7 phút

---

### Bối cảnh: Cần cẩu tháp xây dựng

*Lý do đổi bối cảnh:* PPCT tự gợi ý "đường bay máy bay cắt vùng cấm" — gần
giống Vận dụng 1 SGK (đường thẳng MN, mặt phẳng Oxy, tấm bìa chắn hình
tròn). Đổi sang cần cẩu tháp giữ đúng tinh thần (1 đường thẳng động, xét
quan hệ với 1 mặt phẳng cố định) nhưng khác hẳn kỹ thuật khai thác của SGK.

### Cấu hình 3D

**Mặt phẳng (P) — mái nhà đang xây, cố định:**
```
(P): x + y + 2z − 12 = 0     (VTPT n = (1;1;2))
```
Hiển thị dưới dạng 1 mảng hình chữ nhật nghiêng (footprint x∈[0,4], y∈[0,4]),
kết cấu như 1 mái nhà đang thi công (khung, chưa lợp kín — để trong suốt
opacity 0.2 vẫn nhìn xuyên qua được, đúng quy tắc mặt phẳng chính).

**Tháp cần cẩu:** 1 cột đứng (trụ mảnh) từ gốc (0,0,0) lên đỉnh (0,0,8).

**Tay cần (đường thẳng d) — 3 trạng thái chuyển bằng nút:**

| Trạng thái | Điểm neo | VTCP u | Kiểm tra |
|---|---|---|---|
| Cắt mặt mái | A(0;0;8) *(đỉnh tháp)* | u=(3;2;−4) | u·n=−3≠0 → cắt. Giao điểm M(4; 2.67; 2.67) |
| Song song | A(0;0;8) *(đỉnh tháp)* | u=(1;1;−1) | u·n=0, A không thuộc (P) (thay vào ra 4≠0) → song song |
| Nằm trong mặt mái | A'(2;2;4) *(1 xà gồ đặt áp mái, không phải tay cần chính)* | u=(1;1;−1) | u·n=0, A' thuộc (P) (thay vào ra 0) → nằm trong |

> Lưu ý khi build: trạng thái "Nằm trong" đổi hẳn điểm neo sang A' và đổi
> vai trò vật thể (không còn là tay cần cẩu đang vươn ra, mà là 1 xà gồ nằm
> áp sát mái) — để giữ tính hợp lý vật lý (tay cần cẩu thật không có lý do
> nằm áp mái), tránh vi phạm nguyên tắc "tính vật lý hợp lý của thao tác"
> trong `Luu_Y_Dung_Kich_Ban_3D.md` mục 2. Đổi nhãn vật thể trong UI tương
> ứng khi chuyển trạng thái này (VD "Tay cần" → "Xà gồ mái").

**Slider bổ sung (trong trạng thái "Cắt"):** cho phép kéo nhẹ hướng u (xoay
tay cần trong 1 khoảng góc nhỏ quanh hướng gốc) — giao điểm M di chuyển
real-time trên mặt (P), số liệu t và toạ độ M cập nhật liên tục. Đây là
phần cốt lõi thể hiện "thế t vào phương trình mặt phẳng để tìm giao điểm"
một cách trực quan, tái dùng đúng pattern đã verify ở Bài 10 Module 2 (kéo
slider mặt phẳng nghiêng dần).

**Góc camera mặc định:** Nhìn chéo từ dưới lên, thấy rõ tháp cẩu + mái nhà.

**Quan hệ hình học cần tính:** `classifyLineToPlane` (đã ✅ verify —
phân biệt `contained`/`parallel`/`intersects`), `lineIntersectPlane` (đã ✅
verify) để tính giao điểm khi kéo slider.

**Yếu tố hiển thị kèm:** Nhãn A, u, n, giao điểm M (khi ở trạng thái cắt),
info-box hiện công thức u·n đang tính + kết luận tương ứng.

### Màn hình chính hiển thị

- Canvas 3D + sidebar bên phải
- 3 nút trạng thái [Cắt][Song song][Nằm trong] ở đầu sidebar
- Khi ở trạng thái "Cắt": thêm 1 slider "Xoay tay cần" + hiển thị số liệu t
  và toạ độ M cập nhật real-time khi kéo
- Info-box công thức: hiện u·n = ... (thay số cụ thể), kết luận theo đúng
  giá trị hiện tại

### Học sinh tương tác bằng cách

1. Click từng nút trạng thái, quan sát tay cần đổi vị trí trên hình 3D +
   đọc info-box giải thích tại sao rơi vào trạng thái đó.
2. Ở trạng thái "Cắt": kéo slider, quan sát giao điểm M di chuyển trên mái
   nhà, đối chiếu số liệu t/M hiện trên info-box với phép tính tay.
3. Sau khi đã xem đủ 3 trạng thái → mở phần **"Kiểm tra nhanh"** (2 câu
   MCQ minh hoạ 3D, tái dùng đúng khối hình đang có, số liệu đã verify):

**Câu 1:** Đường thẳng d qua B(1;1;1), VTCP v=(1;1;1). Mặt phẳng (Q):
x+2y−3z+5=0 (n=(1;2;−3)). Vị trí tương đối?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Cắt nhau | Nhiễu — thấy VTCP có đủ 3 thành phần khác 0 rồi vội đoán "chắc cắt", không kiểm tra thật v·n |
| B | Trùng nhau | Nhiễu — nếu có nhầm B thuộc (Q) (tính sai 1+2−3+5 ra 0 thay vì 5), sẽ lầm sang trùng nhau |
| **C** | **Song song** | **`dap_an_dung`** — v·n=1+2−3=0 (song song hoặc nằm trong); thay B(1;1;1) vào (Q): 1+2−3+5=5≠0 → B không thuộc (Q) → song song |
| D | Không xác định được | Nhiễu — đề bài đủ dữ liệu để xác định |

- `giai_thich_dung`: "v·n=0 nên d song song hoặc nằm trong (Q). Thay điểm
  B vào phương trình (Q): 1+2·1−3·1+5=5≠0, B không thuộc (Q) → d song song
  với (Q), không nằm trong."
- `goi_y_khi_sai` (lần 2): "Bước đầu tiên là tính v·n. Nếu v·n=0, đừng
  dừng lại — phải thay tiếp 1 điểm của d vào phương trình mặt phẳng để
  phân biệt song song và nằm trong."

**Câu 2:** Đường thẳng d qua C(0;1;2), VTCP w=(2;0;1). Mặt phẳng (R):
x+y−2z+3=0 (n=(1;1;−2)). Vị trí tương đối?

| # | Đáp án | Ghi chú |
|---|---|---|
| A | Cắt nhau | Nhiễu — w·n=2+0−2=0, không cắt |
| **B** | **Nằm trong mặt phẳng** | **`dap_an_dung`** — w·n=0 và C(0;1;2) thay vào (R): 0+1−4+3=0 → C thuộc (R) → d nằm trong (R) |
| C | Song song | Nhiễu — **đây chính là sai lầm điển hình của bài**: thấy w·n=0 rồi dừng lại kết luận song song ngay, không kiểm tra C có thuộc (R) hay không |
| D | Trùng với 1 đường khác | Nhiễu — không có cơ sở nào trong đề để kết luận điều này |

- `giai_thich_dung`: "w·n=2+0−2=0 → song song hoặc nằm trong. Thay
  C(0;1;2) vào (R): 0+1−2·2+3=0 → C THUỘC (R). Vì d đi qua 1 điểm thuộc
  (R) và có VTCP vuông góc với VTPT, toàn bộ d nằm trong (R)."
- `giai_thich_sai` cho phương án C (Song song): "Đây là lỗi phổ biến nhất
  của cả module: chỉ tính w·n=0 rồi dừng lại, không thay điểm C vào (R)
  để kiểm tra. w·n=0 chỉ cho biết d song song HOẶC nằm trong (R) — hai
  khả năng khác nhau hoàn toàn, phải kiểm tra thêm 1 điểm mới phân biệt
  được."
- `goi_y_khi_sai` (lần 2): "w·n=0 là đúng, nhưng đó chưa phải kết luận
  cuối — hãy thay điểm C vào phương trình (R) để xem C có thuộc (R) không."

### Cleanup

`clearScene()` khi chuyển giữa 3 trạng thái (đổi cả điểm neo + VTCP + nhãn
vật thể). Slider trong trạng thái "Cắt" không cần clearScene mỗi lần kéo —
chỉ cập nhật lại vị trí tay cần + giao điểm M (giống pattern kéo tự do đã
verify, không phải sub-step rời rạc).

---

## CRITICAL REVIEW

- 🧊 **Rủi ro kỹ thuật 3D:** `classifyLineToPlane` và `lineIntersectPlane`
  đã ✅ verify trong `06_geometry_math.md`. Slider xoay nhẹ VTCP quanh 1
  hướng gốc — cần đảm bảo giới hạn góc xoay đủ hẹp để giao điểm M luôn nằm
  trong footprint mái nhà (x∈[0,4], y∈[0,4]) trong suốt dải slider, tránh
  giao điểm "bay ra ngoài" mái nhìn vô lý — **cần verify bằng script Node
  trước khi build**, quét toàn dải slider và kiểm tra M luôn trong footprint.
- ✅ **Số liệu 2 câu "Kiểm tra nhanh" đã verify đầy đủ bằng script** (xem
  bảng trên) — cả v·n, w·n, và việc thay điểm vào phương trình mặt phẳng
  đều đã tính đúng, khớp với kết luận nêu trong `giai_thich_dung`.
- ✅ Đáp án MCQ đã xáo vị trí (câu 1 đúng ở C, câu 2 đúng ở B).
- ©️ **Rà soát bản quyền:** Bối cảnh cần cẩu tháp xây dựng khác hẳn "đường
  bay máy bay" (PPCT gợi ý, gần Vận dụng 1 SGK). Số liệu mặt phẳng
  x+y+2z−12=0 và các VTCP tự đặt mới, số liệu 2 câu quiz cũng tự đặt mới.
