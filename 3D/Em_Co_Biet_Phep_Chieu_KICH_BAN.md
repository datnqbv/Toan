# 📋 KỊCH BẢN SIMULATION — "EM CÓ BIẾT?"
## Phép chiếu song song, phép chiếu xuyên tâm và ảo giác thị giác

**Bài SGK:** Bài 14 — Phép chiếu song song (SGK Kết nối tri thức, trang 101)
**Vị trí:** Nội dung MỞ RỘNG, không thuộc module bắt buộc trong phân phối
chương trình — gắn như 1 tab tuỳ chọn cuối Module 14.4, hoặc file độc lập
học sinh có thể bỏ qua.
**Tính chất:** Thuần khám phá/quan sát, KHÔNG chấm điểm, không có sai lầm
cần "sửa" — mục tiêu là tạo trải nghiệm trực quan, gợi hứng thú.
**Thời lượng dự kiến:** ~5-6 phút (3 trạm khám phá).
**Nguồn SGK tham chiếu:** mục "Em có biết?" (trang 101) — phép chiếu xuyên
tâm, "Thác nước Escher"/"Cầu thang Penrose" (chỉ nhắc tên bằng lời, KHÔNG
dựng lại 2 tác phẩm cụ thể vì lý do bản quyền), đường ray "cắt nhau ở vô
tận".

---

## CẤU TRÚC TỔNG THỂ: 3 trạm khám phá

```
Trạm A — Đường ray "hội tụ ở vô tận" (an toàn, làm trước)
Trạm B — So sánh phép chiếu song song vs xuyên tâm (an toàn, làm trước)
Trạm C — Hình bất khả thi (thử phương án chính; nếu không ổn, dùng phương 
         án dự phòng "Chữ cái nổi 3D" — CŨNG bám sát phép chiếu song song, 
         không phải khối gỗ chung chung)
```

---

## TRẠM A — Đường ray "hội tụ ở vô tận"

**Loại simulation:** F (quan sát, camera animate bay dọc đường ray).
**Thời gian dự kiến:** ~1.5-2 phút.

### Màn hình chính hiển thị:
- 2 đường ray song song thật (khoảng cách cố định, `COLOR_RESULT`), trải
  dài xa dần trên mặt đất (`COLOR_PLANE_BASE`).
- Camera ban đầu đặt ở đầu đường ray, nhìn dọc theo hướng ray.

### Hướng dẫn mở đầu:
> "2 đường ray này SONG SONG THẬT trong không gian — không hề hội tụ. Bấm
> 'Bay dọc đường ray' để xem chúng trông như thế nào khi nhìn từ xa."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Giải thích kiến thức |
|---|---|---|
| 1 | Bấm "Bay dọc đường ray" — camera animate tiến dần về phía trước, nhìn dọc theo 2 đường ray | Quan sát: càng xa, khoảng cách hình ảnh giữa 2 đường ray càng thu hẹp trên màn hình — dù trong không gian thật chúng vẫn cách nhau đúng 1 khoảng không đổi. |
| 2 | Bấm "Đo khoảng cách thật" — hệ thống hiện số đo khoảng cách 2 ray tại vài vị trí dọc đường | Số đo xác nhận: khoảng cách thật KHÔNG đổi ở mọi vị trí — hiện tượng "hội tụ" chỉ là hiệu ứng thị giác của mắt người (và của phép chiếu phối cảnh dùng trong nhiếp ảnh/hội hoạ), không phải bản chất hình học của 2 đường ray. |
| 3 | Xoay tự do quan sát từ nhiều góc | Củng cố: nhìn từ trên xuống (góc vuông với mặt đất), 2 đường ray hiện rõ song song tuyệt đối, không hề hội tụ — chứng minh hiệu ứng "hội tụ" chỉ xuất hiện khi nhìn GẦN NHƯ DỌC THEO hướng 2 đường ray. |

### Cấu hình 3D: Animate camera di chuyển dọc trục ray (không phải animate
đối tượng). Cleanup: `clearScene()` khi sang Trạm B.

---

## TRẠM B — So sánh phép chiếu song song vs xuyên tâm

**Loại simulation:** D3 (kéo tâm chiếu C).
**Thời gian dự kiến:** ~2 phút.

### Màn hình chính hiển thị:
- 1 khối lập phương thật ở giữa.
- 2 mặt phẳng chiếu đặt 2 bên (trái: chiếu song song theo phương Δ cố
  định; phải: chiếu xuyên tâm từ điểm C kéo được).
- Hình chiếu tương ứng hiện trên mỗi mặt phẳng, cập nhật real-time.

### Hướng dẫn mở đầu:
> "Bên trái là phép chiếu SONG SONG đã học — phương Δ cố định. Bên phải là
> phép chiếu XUYÊN TÂM — thay vì 1 phương cố định, mọi tia chiếu đều đi qua
> 1 điểm C duy nhất. Kéo điểm C ra xa dần và quan sát."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Giải thích kiến thức |
|---|---|---|
| 1 | Quan sát hình chiếu xuyên tâm ban đầu (C ở gần) — các cạnh của khối lập phương trông "toè ra" rõ rệt | Trong phép chiếu xuyên tâm, mỗi điểm M được chiếu thành M' = giao điểm của đường thẳng CM với mặt phẳng chiếu — khi C gần, các tia CM có hướng khác nhau rõ rệt, gây hiệu ứng phối cảnh mạnh (giống ảnh chụp cận cảnh). |
| 2 | Kéo điểm C ra xa dần (slider hoặc kéo trực tiếp trong 3D) | Quan sát: hình chiếu xuyên tâm bên phải dần "duỗi thẳng", các cạnh song song trong khối gốc trông ngày càng song song hơn trên hình chiếu. |
| 3 | Kéo C ra thật xa (gần giới hạn slider) — so sánh trực tiếp 2 hình chiếu trái/phải | Khi C tiến ra xa vô tận, mọi tia CM gần như trở thành các đường thẳng SONG SONG nhau (vì đều xuất phát từ 1 điểm rất xa cùng 1 hướng) — đây chính là lý do TOÁN HỌC vì sao phép chiếu song song được xem là TRƯỜNG HỢP GIỚI HẠN của phép chiếu xuyên tâm khi tâm chiếu ra xa vô cùng. Đây là 1 kết nối đẹp giữa 2 khái niệm mà SGK chỉ nói bằng lời ở mục "Em có biết". |

### Cấu hình 3D: Tái dùng hàm tính giao điểm đường thẳng-mặt phẳng đã có
sẵn (`intersectionOfTwoPlanes`-style, chỉ đổi từ "đường qua M song song Δ"
sang "đường CM"). Cleanup: `clearScene()` khi sang Trạm C.

---

## TRẠM C — Hình bất khả thi (PHƯƠNG ÁN CHÍNH)

**Loại simulation:** F (quan sát góc bí mật + xoay tự do để lộ sự thật).
**Thời gian dự kiến:** ~2 phút.
**Thứ tự thực hiện:** Build và thử nghiệm phương án này TRƯỚC. Chỉ chuyển
sang phương án dự phòng (bên dưới) nếu sau khi thử nghiệm, hiệu ứng góc bí
mật không đủ thuyết phục hoặc không ổn định qua các thiết bị/độ phân giải
màn hình khác nhau.

### Màn hình chính hiển thị:
- 3 thanh (dạng chữ L, mỗi thanh 1 màu riêng: `COLOR_PLANE_1`,
  `COLOR_PLANE_2`, `COLOR_PLANE_3`) đặt trong không gian 3D — **thực sự
  KHÔNG chạm nhau**, mỗi thanh ở 1 độ sâu (trục nhìn của camera bí mật)
  khác nhau.
- Camera BAN ĐẦU khoá cứng ở đúng góc bí mật, FOV hẹp (gần như phép chiếu
  song song, khác hẳn FOV=45° chuẩn dùng ở các sim khác).

### Hướng dẫn mở đầu:
> "Nhìn kỹ hình dưới đây — 3 thanh gỗ này trông như nối liền thành 1 tam
> giác khép kín. Nhưng đây là ẢO GIÁC. Bấm 'Xoay ra xem sự thật' để kiểm
> chứng."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Giải thích kiến thức |
|---|---|---|
| 1 | Quan sát hình ở góc camera ban đầu (khoá cứng) — nhận xét ban đầu | Ở đúng góc nhìn này, 3 thanh trông như khép kín thành 1 tam giác liên tục — đây là hiệu ứng nổi tiếng từng được nghệ sĩ Oscar Reutersvärd và nhà toán học Roger Penrose khai thác (khác với Escher — Escher vẽ tranh 2D mô tả cấu trúc tương tự, còn đây là mô hình 3D thật dựng theo cùng nguyên lý). |
| 2 | Bấm "Xoay ra xem sự thật" — camera mở khoá, animate xoay dần sang góc khác | Quan sát trực tiếp: 3 thanh KHÔNG hề chạm nhau — mỗi thanh nằm ở 1 độ sâu hoàn toàn khác trong không gian. |
| 3 | Xoay tự do, thử tìm lại đúng góc ban đầu | Học sinh tự trải nghiệm: ảo giác CHỈ xảy ra ở đúng 1 góc nhìn duy nhất (hoặc rất gần đó) — đây chính là ứng dụng "ngược" của phép chiếu: thay vì hỏi "chiếu ra hình gì", ta hỏi "cần đặt vật thể thế nào để chiếu ra ĐÚNG hình mong muốn ở 1 góc cụ thể" — cùng bản chất toán học (đường thẳng, mặt phẳng chiếu, phương chiếu) nhưng dùng theo chiều ngược lại. |

### Kịch bản kỹ thuật (không phải sai lầm học sinh — đây là ghi chú build):
- Camera ban đầu PHẢI khoá cứng đúng góc + FOV hẹp đã tính toán trước —
  không cho học sinh xoay tự do ngay từ đầu (sẽ phá vỡ ảo giác trước khi
  kịp gây ấn tượng).
- Cần thử nghiệm trên nhiều kích thước màn hình (điện thoại/máy tính) vì
  góc bí mật khá nhạy — lệch nhỏ có thể phá vỡ hiệu ứng trên khung hình tỉ
  lệ khác nhau.

### Cấu hình 3D: 3 hình học tuỳ chỉnh (không dùng SOLID_LIBRARY — hình dạng
đặc thù). Camera: FOV hẹp (~15-20°, khác chuẩn 45° hệ thống), đặt xa, khoá
cứng ban đầu rồi mở khoá OrbitControls sau bước 2. Cleanup: `clearScene()`
khi kết thúc.

---

## TRẠM C — Chữ cái nổi 3D (PHƯƠNG ÁN DỰ PHÒNG)

> 📝 **Lý do chọn phương án này thay vì "khối gỗ lập phương chung chung":**
> Đây là nội dung TRỰC TIẾP có trong SGK — Vận dụng 2 (trang 99) dùng phép
> chiếu song song để tạo "dạng nổi 3D" của chữ cái (minh hoạ chữ E, gợi ý
> luyện tập thêm L, N, T). Dùng lại đúng tinh thần này (nhưng đổi chữ cái
> khác, xem ghi chú bản quyền) vừa AN TOÀN kỹ thuật, vừa bám sát chủ đề
> phép chiếu song song hơn hẳn 1 khối lập phương trung tính không có nội
> dung toán liên quan.

**Loại simulation:** F (quan sát + xoay tự do).
**Thời gian dự kiến:** ~2 phút.

> 📝 **Ghi chú bản quyền:** SGK đã dùng chữ "E" làm ví dụ minh hoạ và gợi ý
> L, N, T cho học sinh tự luyện. Ở đây dùng chữ **"H"** — chưa xuất hiện
> trong ví dụ hay gợi ý của SGK.

### Màn hình chính hiển thị:
- Chữ cái "H" dạng nổi 3D, dựng bằng cách chiếu song song 1 hình chữ "H"
  phẳng theo 1 phương chiếu cố định (kỹ thuật y hệt Vận dụng 2 SGK, chỉ đổi
  chữ cái).

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Giải thích kiến thức |
|---|---|---|
| 1 | Quan sát chữ "H" nổi 3D, xoay tự do | Đây được dựng bằng CHÍNH kỹ thuật phép chiếu song song vừa học — lấy hình chữ "H" phẳng, "kéo dài" nó theo 1 phương chiếu cố định để tạo độ dày, giống hệt cách vẽ hình biểu diễn 1 khối lăng trụ (đáy = hình chữ H, cạnh bên = phương chiếu). |
| 2 | Bấm "Ẩn/hiện phương chiếu" để xem trục kéo dài | Xác nhận: mọi điểm trên mặt "trước" của chữ H đều nối với điểm tương ứng ở mặt "sau" theo ĐÚNG 1 phương duy nhất — đúng bản chất phép chiếu song song, không phải "đùn" ngẫu nhiên theo nhiều hướng khác nhau. |

### Cấu hình 3D: Custom geometry (chữ H extrude theo 1 vector cố định).
Cleanup: `clearScene()` khi kết thúc.

---

## ✅ GHI CHÚ TỔNG KẾT

- Trạm A, B: an toàn kỹ thuật, dùng lại hàm giao điểm đường-mặt phẳng đã
  verify, chỉ đổi tham số (phương cố định → hướng về 1 điểm).
- Trạm C phương án chính: khả thi về mặt hình học (phương pháp đã dùng
  thật cho tác phẩm điêu khắc "hình bất khả thi" ngoài đời), nhưng cần thử
  nghiệm thực tế góc camera + FOV trước khi khẳng định ổn định trên mọi
  thiết bị — đây là rủi ro kỹ thuật DUY NHẤT của cả "Em có biết", không
  phải rủi ro về mặt "có làm được hay không".
- Trạm C phương án dự phòng: an toàn tuyệt đối, bám sát đúng nội dung
  Vận dụng 2 SGK, không cần thử nghiệm phức tạp.
- Không có phần nào chấm điểm hay có "đáp án đúng/sai" — toàn bộ là trải
  nghiệm khám phá tự do.

---

**Bạn duyệt cấu trúc này chứ? Đây là nội dung mở rộng, không bắt buộc — có
thể build sau khi các module chính (12.3, 13.4-13.7, 14.3-14.4) đã hoàn
tất, không cần ưu tiên ngay.**

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 12/08/2026
> **Tài liệu tham chiếu:** `04_design_toan_3d.md`, `05_threejs_engine.md`,
> `06_geometry_math.md`
