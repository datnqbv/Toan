# 📋 KỊCH BẢN SIMULATION — MODULE 14.3
## Quy tắc vẽ hình biểu diễn

**Bài SGK:** Bài 14 — Phép chiếu song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 14.3 — nối tiếp Module 14.1
(Khái niệm và định nghĩa phép chiếu song song), 14.2 (Tính chất của phép
chiếu song song). Tương ứng Tiết 38, mục "3. HÌNH BIỂU DIỄN CỦA MỘT HÌNH
KHÔNG GIAN" (trang 98-99 SGK).
**Trạng thái kiến thức nền:** Đã dạy qua Module 14.1-14.2 — 14.3 KHÔNG dạy
lại định nghĩa/tính chất phép chiếu, chỉ vận dụng vào quy tắc vẽ.
**Nguồn SGK tham chiếu:** HĐ3, định nghĩa hình biểu diễn, quy tắc vẽ hình
biểu diễn, Ví dụ 4, Luyện tập 4, Vận dụng 2 (trang 98-99) — số liệu đã đổi
khác SGK ở các tỉ lệ hình thang (xem ghi chú bản quyền).

---

## 🎯 MỤC TIÊU

- HIỂU: hình biểu diễn là hình chiếu song song (hoặc đồng dạng với hình
  chiếu đó) — phép chiếu song song KHÔNG bảo toàn góc và độ dài tuyệt đối,
  chỉ bảo toàn: 3 điểm thẳng hàng → 3 điểm thẳng hàng cùng thứ tự; 2 đường
  song song → 2 đường song song; tỉ số độ dài trên đường thẳng song song.
- LÀM ĐƯỢC: vẽ đúng hình biểu diễn cho từng loại hình đặc biệt (tam giác bất
  kỳ → tam giác; hình vuông/chữ nhật/thoi/bình hành → hình bình hành; hình
  thang → hình thang giữ đúng tỉ lệ 2 đáy; hình tròn → elip) và áp dụng vẽ
  hình biểu diễn của khối lăng trụ/hình chóp có đáy đặc biệt.

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Vẽ hình biểu diễn của hình vuông/chữ nhật vẫn giữ nguyên góc vuông | Nghĩ "vuông thì phải vẽ vuông", quên rằng phép chiếu song song không bảo toàn góc | Hình vẽ ra vẫn có 1 góc 90° thay vì hình bình hành nghiêng tự nhiên |
| Vẽ hình tròn thành hình tròn hoặc hình bầu dục tuỳ ý | Không phân biệt "hình tròn" và "elip đúng theo phép chiếu" | Vẽ tuỳ hứng thay vì dựa trên quy tắc chiếu các đường kính vuông góc |
| Vẽ tuỳ ý tỉ lệ 2 đáy hình thang | Bỏ qua điều kiện tỉ lệ AB/CD phải giữ nguyên trong hình biểu diễn | Vẽ 2 đáy hình thang biểu diễn có độ dài không đúng tỉ lệ đề cho |

## 🧊 ĐẶC THÙ 3D

- **Khối/đối tượng nền:** hình vuông và hình tròn thật trong 3D (Tab 1);
  tam giác, tứ giác đặc biệt, hình thang dạng phẳng (Tab 2); lăng trụ đáy
  hình thang (Tab 3); hình chóp đáy hình bình hành (Tab 4).
- **Quan hệ không gian trọng tâm:** phép chiếu song song và quy tắc suy ra
  hình biểu diễn.
- **Góc camera mặc định:** Tab 1 khoá góc nhìn trong lúc animate, mở tự do
  sau khi chiếu xong; các tab còn lại dùng `setCameraStandardSGK()`.
- **Mức độ tương tác:** Tab 1 — quan sát + xoay tự do (F). Tab 2 — chọn/kéo
  chỉnh (I + D3). Tab 3 — dựng dần đối chiếu (F). Tab 4 — MCQ (I).
- **Nguyên tắc bắt buộc xuyên suốt (đã rà soát kỹ theo yêu cầu):** sau MỌI
  bước tương tác đều có giải thích kiến thức đầy đủ, cặn kẽ — không chỉ nêu
  kết luận mà giải thích rõ VÌ SAO, bám vào đúng tính chất đã học ở
  Module 14.2. Không có bước nào chỉ báo Đúng/Sai trơn.

---

## TAB 1 — Quan sát: vì sao góc vuông "biến mất" khi chiếu

**Loại simulation:** F (dựng dần có animation + xoay tự do sau khi chiếu).
**Thời gian dự kiến:** ~3-4 phút.
**Sổ tay kiến thức:** Chưa hiện — đây là bước xây trực giác trước khi vào
quy tắc trừu tượng ở Tab 2.

### Màn hình chính hiển thị:
- 1 hình vuông thật ABCD trong không gian 3D (nằm ngang, `COLOR_PLANE_1`).
- 1 mặt phẳng chiếu (α) đặt nghiêng bên dưới (`COLOR_PLANE_BASE`, opacity 0.15).
- Phương chiếu Δ hiển thị dưới dạng các đường mũi tên song song, màu
  `COLOR_CONNECTOR`, đi theo hướng KHÔNG vuông góc với (α) và KHÔNG song
  song với bất kỳ cạnh nào của hình vuông.

### Hướng dẫn mở đầu:
> "Đây là hình vuông ABCD thật trong không gian. Bạn bấm 'Chiếu xiên' để
> xem nó bị chiếu xuống mặt phẳng (α) theo phương Δ như thế nào. Quan sát
> kỹ: hình chiếu có còn là hình vuông không?"

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Bấm "Chiếu xiên" — animate từng đỉnh A, B, C, D "rơi" dọc theo phương Δ xuống mặt phẳng (α), tạo thành A', B', C', D' | Mỗi đỉnh M được chiếu thành M' là giao điểm của đường thẳng qua M song song Δ với mặt phẳng (α) — đúng định nghĩa phép chiếu song song đã học ở Module 14.1. |
| 2 | Sau khi chiếu xong, OrbitControls tự động mở khoá — xoay tự do để quan sát hình A'B'C'D' từ nhiều góc | Xoay để thấy rõ: A'B'C'D' vẫn có 2 cặp cạnh song song (AB//CD chiếu thành A'B'//C'D', tính chất "biến 2 đường song song thành 2 đường song song" đã học ở Module 14.2), nhưng KHÔNG còn góc vuông. |
| 3 | Bấm "Đo góc tại A'" — hệ thống hiện số đo góc thực tế tại đỉnh A' | Góc tại A' KHÁC 90° — chứng minh trực tiếp bằng số liệu: phép chiếu song song không bảo toàn độ lớn góc, dù vẫn bảo toàn tính chất song song. |
| 4 | Bấm "Thử lại với hình tròn" — lặp lại animate tương tự với 1 hình tròn thật | Hình tròn bị chiếu thành 1 hình elip — vì các đường kính vuông góc của hình tròn, sau khi chiếu, không còn vuông góc nhưng vẫn giữ đúng trung điểm (do tính chất bảo toàn tỉ lệ trên đường thẳng), tạo thành 2 trục của elip. |
| 5 | Xoay tự do quan sát hình elip từ nhiều góc, bấm "Kết luận" | Cả 2 thí nghiệm đều cho thấy: hình biểu diễn giữ được TÍNH SONG SONG và TỈ LỆ, nhưng KHÔNG giữ được GÓC và HÌNH DẠNG chính xác (vuông thành không vuông, tròn thành elip) — đây là điều quan trọng nhất cần nhớ trước khi học quy tắc vẽ cụ thể ở Tab 2. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Sau khi xem animation, học sinh có thể vẫn nghĩ đây chỉ là
  "hiệu ứng hình ảnh do góc camera", không phải bản chất toán học.
- Hệ thống phản hồi: Bước 3 (đo góc bằng số liệu cụ thể) chính là để phản
  bác nhận định này — số đo góc hiện ra rõ ràng khác 90°, không phụ thuộc
  góc camera đang xoay.
- Kết quả rút ra: Phân biệt "trông có vẻ khác do góc nhìn" với "thực sự
  khác về bản chất toán học" — số đo cụ thể là bằng chứng khách quan, không
  phụ thuộc góc quan sát.

### Cấu hình 3D:
- Animation chiếu từng đỉnh dọc theo phương Δ (interpolate theo tham số t
  từ vị trí gốc tới giao điểm với mặt phẳng α).
- Đối tượng kéo được: không có — chỉ bấm nút và xoay camera.
- Yếu tố hiển thị kèm: nhãn góc động (bước 3), phương chiếu Δ luôn hiển thị
  làm mốc tham chiếu.
- Cleanup: `clearScene()` khi sang Tab 2.

### Nút và điều khiển:
- **Chiếu xiên:** chạy animation chiếu hình vuông.
- **Đo góc tại A':** hiện số đo góc thực tế.
- **Thử lại với hình tròn:** chạy animation chiếu hình tròn.
- **Đặt lại góc nhìn:** reset camera.

---

## TAB 2 — Luyện quy tắc cho hình phẳng

**Loại simulation:** I (chọn đáp án) + D3 (kéo chỉnh tỉ lệ).
**Thời gian dự kiến:** ~4-5 phút.

### Sổ tay kiến thức (Có — hiện từ đây trở đi):
- Quy tắc: tam giác (cân, đều, vuông) → tam giác bất kỳ; hình vuông/chữ
  nhật/thoi/bình hành → hình bình hành; hình thang → hình thang giữ đúng tỉ
  lệ 2 đáy; hình tròn → elip.

### Hướng dẫn mở đầu:
> "Bạn sẽ luyện 3 quy tắc vẽ hình biểu diễn qua 3 case. Ở mỗi case, đọc kỹ
> yêu cầu trước khi chọn hoặc kéo chỉnh."

### Case (a) — Tam giác
**Đề bài:** Tam giác ABC (tam giác VUÔNG tại A, có 1 góc vuông rõ ràng)
trong không gian. Chọn đúng hình biểu diễn của nó trong 3 phương án.

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát 3 phương án: (I) tam giác vuông giữ nguyên góc vuông; (II) tam giác thường bất kỳ, không giữ góc vuông, không giữ tỉ lệ cạnh gốc; (III) tam giác đều | Mỗi phương án minh hoạ 1 cách hiểu (đúng hoặc sai) về quy tắc. |
| 2 | Chọn phương án đúng (vị trí đáp án đúng random khi build) | Đáp án: (II) — vì hình biểu diễn của MỘT tam giác bất kỳ (dù là tam giác đặc biệt như cân, đều, vuông) chỉ cần LÀ một tam giác, không cần giữ nguyên góc vuông hay bất kỳ đặc điểm đặc biệt nào của tam giác gốc. Đây là quy tắc "lỏng" nhất trong 4 quy tắc — khác hẳn hình vuông/chữ nhật (phải chiếu thành hình bình hành, không phải tam giác bất kỳ). |

### Case (b) — Hình vuông/chữ nhật/thoi
**Đề bài:** Hình vuông ABCD. Chọn đúng hình biểu diễn trong 3 phương án.

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát 3 phương án: (I) hình bình hành nghiêng, không góc vuông; (II) vẫn giữ 1 góc vuông (bẫy — đúng sai lầm số 1); (III) hình thang (chỉ 1 cặp cạnh song song) | Mỗi phương án minh hoạ 1 hiểu lầm khả dĩ. |
| 2 | Chọn phương án đúng (vị trí random) | Đáp án: (I) — vì hình vuông có 2 cặp cạnh song song (AB//DC và AD//BC), qua phép chiếu, CẢ 2 cặp đều giữ song song (tính chất Module 14.2), nên hình biểu diễn PHẢI là hình bình hành — không được có góc vuông "còn sót lại" (phương án II sai), và không được chỉ có 1 cặp song song (phương án III sai vì đó là đặc điểm hình thang, không phải hình bình hành). |

### Case (c) — Hình thang (kéo chỉnh tỉ lệ)
**Đề bài:** Hình thang ABCD, AB // CD, với **AB = 1.5×CD** (tỉ lệ số thập
phân, khác cả Ví dụ 4 SGK dùng AB=2CD và bài 4.33 dùng CD=3AB).

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát hình thang biểu diễn A'B'C'D' đã dựng sẵn NHƯNG SAI tỉ lệ (VD đang để A'B' = C'D', tỉ lệ 1:1) | Đây là hình thang nhưng CHƯA đúng — thiếu điều kiện tỉ lệ 2 đáy. |
| 2 | Kéo thanh trượt "Độ dài đáy trên A'B'" cho tới khi tỉ lệ A'B'/C'D' = 1.5 (hiển thị số real-time) | Quy tắc bắt buộc: hình biểu diễn của hình thang phải giữ ĐÚNG tỉ số 2 đáy như hình gốc — AB/CD = A'B'/C'D' (tính chất "giữ nguyên tỉ số độ dài trên 2 đường thẳng song song" đã học ở Module 14.2). Đây KHÔNG phải là 1 lựa chọn tự do, mà là điều kiện bắt buộc. |
| 3 | Khi tỉ lệ đạt đúng 1.5 (dung sai nhỏ), hệ thống tự khoá và xác nhận | "Chính xác — A'B'/C'D' = 1.5, đúng bằng AB/CD của hình gốc. Đây chính là lý do vì sao khi vẽ hình biểu diễn hình thang, ta LUÔN phải tính trước tỉ lệ 2 đáy, không được vẽ tuỳ hứng như với tam giác thường (Case a)." |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống Case (b): Học sinh có thể chọn phương án (II) vì trực giác
  "hình vuông thì đặc biệt, nên hình biểu diễn cũng nên giữ lại chút gì đặc
  biệt (góc vuông)".
- Hệ thống phản hồi (khi chọn sai): "Bạn vừa chọn 1 hình vẫn còn góc vuông
  — nhưng nhớ lại Tab 1: khi ta chiếu hình vuông thật, góc tại A' đo được
  KHÁC 90°. Không có lý do gì để hình biểu diễn 'đặc cách' giữ lại góc vuông
  — quay lại xem Tab 1 nếu cần."
- Kết quả rút ra: Tab 1 (trực quan) và Tab 2 (quy tắc) liên kết chặt — quy
  tắc không phải "phải nhớ máy móc" mà là hệ quả trực tiếp của tính chất đã
  quan sát.

### Cấu hình 3D: Case (a), (b) hiển thị hình phẳng 2D overlay (không cần
xoay 3D); Case (c) có thanh trượt (slider) điều khiển độ dài A'B' theo thời
gian thực. Cleanup: `clearScene()` giữa các case và khi sang Tab 3.

---

## TAB 3 — Áp dụng: vẽ hình biểu diễn khối lăng trụ

**Loại simulation:** F (dựng dần, đối chiếu khối 3D thật).
**Thời gian dự kiến:** ~4-5 phút.

> 📝 **Ghi chú bản quyền:** Đổi từ tỉ lệ AB=2CD (Ví dụ 4 SGK) sang **CD =
> 2.5AB** (đáy dưới dài hơn đáy trên — hướng ngược lại Ví dụ 4, và là số
> thập phân khác hẳn tỉ lệ nguyên CD=3AB của bài 4.33). Góc nhìn ban đầu
> của khối 3D cũng đặt khác Hình 4.64 SGK.

### Đề bài: Cho hình lăng trụ ABCD.A'B'C'D' có đáy ABCD là hình thang, AB //
CD, CD = 2.5AB. Vẽ hình biểu diễn của lăng trụ này.

### Sổ tay kiến thức (Có — nhắc lại từ Tab 2): quy tắc hình thang (giữ tỉ
lệ 2 đáy) + quy tắc lăng trụ (mặt bên là hình bình hành nên hình biểu diễn
của lăng trụ cũng có các mặt bên là hình bình hành, đã học ở Module 13.5).

### Hướng dẫn mở đầu:
> "Bên trái là khối lăng trụ thật, xoay được tự do để bạn đối chiếu. Bên
> phải là khung vẽ 2D — bạn dựng hình biểu diễn từng bước theo hướng dẫn."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Vẽ đáy dưới ABCD dạng hình thang biểu diễn (kéo chỉnh tỉ lệ CD/AB = 2.5, tương tự kỹ thuật đã luyện ở Tab 2 case c) | Áp dụng đúng quy tắc: hình thang biểu diễn phải giữ tỉ lệ CD/AB = 2.5 như đề cho. |
| 2 | Bấm "Tịnh tiến đáy trên" — hệ thống animate tạo đáy A'B'C'D' bằng cách tịnh tiến đáy dưới theo 1 vector xiên (không vuông góc đáy dưới trên hình 2D) | Vì các mặt bên của lăng trụ là hình bình hành (đã học Module 13.5), hình biểu diễn của mặt bên cũng phải là hình bình hành — cách đơn giản nhất để đảm bảo điều này là tịnh tiến toàn bộ đáy dưới theo 1 vector cố định. |
| 3 | Bấm "Nối cạnh bên" — hệ thống tự nối AA', BB', CC', DD' | Các đoạn AA', BB', CC', DD' này chính là hình biểu diễn của các cạnh bên — chúng song song và bằng nhau trên hình vẽ (vì đều là cùng 1 vector tịnh tiến), đúng phản ánh tính chất cạnh bên lăng trụ. |
| 4 | Đối chiếu: xoay khối 3D thật ở khung bên trái về đúng góc nhìn ban đầu, so sánh hình dạng tổng thể với hình biểu diễn 2D vừa dựng | So sánh trực quan: hình biểu diễn 2D tuy "méo" so với khối 3D thật (góc không giữ nguyên, hình thang trông khác), nhưng NGƯỜI ĐỌC vẫn nhận ra đúng cấu trúc lăng trụ đáy thang nhờ giữ đúng 2 yếu tố cốt lõi: song song và tỉ lệ. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Ở bước 2, học sinh có thể cố tình tịnh tiến đáy trên thẳng
  đứng lên trên (giống nhìn từ góc vuông góc thật), khiến hình biểu diễn bị
  "phẳng dẹt", khó nhận ra là hình khối khi vẽ trên giấy.
- Hệ thống phản hồi: "Vector tịnh tiến thẳng đứng sẽ khiến hình biểu diễn
  trông như 2D phẳng, không gợi được cảm giác không gian. Trong hình biểu
  diễn, ta thường chọn vector tịnh tiến XIÊN (có cả thành phần ngang) để
  người xem dễ hình dung đây là vật thể 3D — thử kéo lại theo hướng xiên."
- Kết quả rút ra: Hình biểu diễn không chỉ cần ĐÚNG về mặt toán học (song
  song, tỉ lệ) mà còn cần chọn phương chiếu hợp lý để dễ hình dung — đây là
  khía cạnh thực hành, không chỉ lý thuyết thuần tuý.

### Cấu hình 3D:
- Khung trái: khối lăng trụ 3D thật, xoay tự do (OrbitControls).
- Khung phải: canvas 2D (hoặc mặt phẳng ảo trong 3D scene nhìn trực diện)
  để dựng hình biểu diễn.
- Cleanup: `clearScene()` khi sang Tab 4.

### Nút và điều khiển:
- **Kéo chỉnh tỉ lệ đáy:** slider CD/AB.
- **Tịnh tiến đáy trên:** animate tạo đáy trên.
- **Nối cạnh bên:** tự động nối 4 cạnh bên.
- **Đặt lại góc nhìn (khối 3D thật):** reset camera khung trái.

---

## TAB 4 — Củng cố tổng hợp (MCQ)

**Loại simulation:** I (MCQ có minh hoạ).
**Thời gian dự kiến:** ~3-4 phút.

### Danh sách câu hỏi:

**Câu 1 (quy tắc chung):** "Hình biểu diễn của 1 hình bình hành là gì?"
(chọn: Hình bình hành / Hình vuông / Hình thang / Hình chữ nhật)
- Đáp án: Hình bình hành (vị trí random). `giai_thich_dung`: Hình bình hành
  có 2 cặp cạnh song song, qua phép chiếu cả 2 cặp đều giữ song song, nên
  hình biểu diễn vẫn là 1 hình bình hành (dù góc và độ dài cụ thể có thể
  khác).
- `goi_y_khi_sai`: Nhớ lại Tab 2 case (b) — hình vuông, chữ nhật, thoi,
  hình bình hành đều chung 1 quy tắc biểu diễn là gì?

**Câu 2 (hình tròn):** "Hình biểu diễn của 1 hình tròn là gì?" (chọn: Hình
tròn / Elip / Hình bầu dục tuỳ ý / Đường thẳng)
- Đáp án: Elip. `giai_thich_dung`: Đã quan sát trực tiếp ở Tab 1 — hình
  tròn khi chiếu song song (không theo phương vuông góc) luôn cho ra 1
  elip xác định, không phải hình bầu dục vẽ tuỳ hứng.
- `goi_y_khi_sai`: Nhớ lại animation "Thử lại với hình tròn" ở Tab 1 — hình
  chiếu ra có hình dạng cụ thể nào?

**Câu 3 (áp dụng — hình chóp đáy hình bình hành, phương chiếu cụ thể):**
Cho hình chóp S.ABCD, đáy ABCD là hình bình hành. Phép chiếu song song theo
phương Δ (không song song với bất kỳ cạnh nào của khối, đã cho hình minh
hoạ cụ thể trong câu hỏi — khác Luyện tập 4 SGK vốn không quy định phương
chiếu cụ thể). Hỏi hình biểu diễn S'A'B'C'D' có đáy A'B'C'D' là hình gì?
- Đáp án: Hình bình hành. `giai_thich_dung`: Đáy ABCD là hình bình hành nên
  áp dụng đúng quy tắc đã học — đáy của hình biểu diễn cũng là 1 hình bình
  hành, bất kể phương chiếu Δ cụ thể là gì (miễn không suy biến — xem Chú ý
  ở SGK: nếu 1 đường thẳng cùng phương với phương chiếu thì hình chiếu của
  nó là 1 điểm).
- `goi_y_khi_sai`: Đáy của hình chóp là loại tứ giác gì? Quy tắc biểu diễn
  cho loại tứ giác đó là gì (đã luyện ở Tab 2)?

**Câu 4 (liên hệ Tab 3 — tỉ lệ hình thang):** Cho hình lăng trụ đáy hình
thang, EF // GH với EF = 4cm, GH = 10cm. Trong hình biểu diễn, nếu vẽ đáy
trên E'F' = 2cm, thì đáy dưới G'H' đúng theo quy tắc phải bằng bao nhiêu?
- Đáp án: 5cm (nhập số). `giai_thich_dung`: Tỉ lệ EF/GH = 4/10 = 0.4 phải
  giữ nguyên trong hình biểu diễn: E'F'/G'H' = 0.4, với E'F'=2cm thì
  G'H' = 2/0.4 = 5cm.
- `goi_y_khi_sai`: Tính tỉ lệ EF/GH trước, rồi áp dụng đúng tỉ lệ đó cho
  E'F' đã cho để suy ra G'H'.

### Cấu hình 3D: mỗi câu có 1 minh hoạ tĩnh riêng (xoay được), `clearScene()`
giữa các câu. Cleanup cuối: khi kết thúc module.

---

## 🎯 TỔNG KẾT CUỐI MODULE 14.3

**Tổng kết kiến thức:**
- Hình biểu diễn là hình chiếu song song của 1 hình (hoặc đồng dạng với
  hình chiếu đó) — giữ được tính song song và tỉ lệ độ dài trên đường thẳng
  song song, nhưng KHÔNG giữ được góc và độ dài tuyệt đối.
- 4 quy tắc cốt lõi: tam giác → tam giác bất kỳ; hình vuông/chữ nhật/thoi/
  bình hành → hình bình hành; hình thang → hình thang giữ đúng tỉ lệ 2 đáy;
  hình tròn → elip.

**Tổng kết sai lầm:**
1. Giữ nguyên góc vuông trong hình biểu diễn — dấu hiệu: vẽ hình vuông/chữ
   nhật biểu diễn vẫn có 1 góc 90°.
2. Vẽ hình tròn thành hình tròn hoặc bầu dục tuỳ ý — dấu hiệu: không dựa
   trên quy tắc chiếu cụ thể mà vẽ theo cảm tính.
3. Vẽ tuỳ ý tỉ lệ 2 đáy hình thang — dấu hiệu: độ dài 2 đáy trong hình biểu
   diễn không đúng tỉ lệ đề cho.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

📝 **Rà soát bản quyền:** Tab 2 case (c) đổi tỉ lệ AB=2CD (Ví dụ 4 SGK)
sang AB=1.5CD; Tab 3 đổi CD=2.5AB (khác hướng và khác số thập phân so với
cả Ví dụ 4 lẫn bài 4.33); Tab 4 câu 3 quy định phương chiếu cụ thể (Luyện
tập 4 SGK không quy định); Tab 4 câu 4 dùng tên điểm EF/GH hoàn toàn mới,
không dùng lại AB/CD.

📖 **Rà soát độ cặn kẽ của giải thích (theo yêu cầu):** Đã kiểm tra lại
toàn bộ 4 tab — mỗi bước đều giải thích VÌ SAO chứ không chỉ nêu kết luận:
Tab 1 dùng số đo góc cụ thể làm bằng chứng khách quan (không chỉ nói "góc
đã đổi"); Tab 2 mỗi case đều nối lại với tính chất đã học ở Module 14.2
(không yêu cầu học sinh chỉ ghi nhớ quy tắc suông); Tab 3 giải thích cả lý
do kỹ thuật (chọn vector xiên) lẫn lý do toán học (tỉ lệ, song song); Tab 4
mỗi câu MCQ đều có `giai_thich_dung` VÀ `goi_y_khi_sai` trỏ lại đúng phần
kiến thức liên quan ở tab trước.

⚠️ **Rủi ro 1:** Tab 1 bước 3 (đo góc tại A') cần verify công thức tính góc
3D chính xác giữa 2 cạnh sau khi chiếu — đặc biệt khi phương chiếu gần song
song với mặt phẳng chiếu (trường hợp biên gây sai số).

⚠️ **Rủi ro 2:** Tab 3 bước 4 (đối chiếu khối 3D thật với hình biểu diễn
2D) đòi hỏi đồng bộ góc nhìn giữa 2 khung — cần thiết kế UI rõ ràng để học
sinh không nhầm lẫn 2 khung đang thao tác độc lập.

---

**Kịch bản đã sẵn sàng!**
- ✅ Duyệt — mình tiếp tục Bước 0 cho Module 14.4
- ✏️ Chỉnh — nêu rõ phần nào cần thay đổi

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 12/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`,
> `01_scenario_builder_3d_addendum.md`, `04_design_toan_3d.md`,
> `05_threejs_engine.md`, `06_geometry_math.md`
