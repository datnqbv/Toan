# 📋 KỊCH BẢN SIMULATION — MODULE 14.4
## Bài tập vẽ hình biểu diễn và ôn tập Chương IV

**Bài SGK:** Bài 14 — Phép chiếu song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 14.4 — nối tiếp Module
14.1-14.3, cùng Tiết 38. Tương ứng phần BÀI TẬP (4.29-4.34, trang 100).
**Trạng thái kiến thức nền:** Tổng kết — đã dạy đủ 14.1-14.3 (khái niệm,
tính chất, quy tắc vẽ hình biểu diễn). Sổ tay kiến thức tổng hợp hiện xuyên
suốt, không dạy khái niệm mới.
**Nguồn SGK tham chiếu:** bài 4.29, 4.30, 4.31, 4.32, 4.33, 4.34 (trang
100) — **toàn bộ số liệu, cấu hình đối tượng, và cách đặt câu hỏi đã đổi
khác SGK gốc** (xem ghi chú bản quyền ở mỗi tab).

---

## 🎯 MỤC TIÊU

- LÀM ĐƯỢC: nhận định đúng/sai các tính chất phép chiếu song song; giải
  thích được tính "đối xứng" của phép chiếu; chứng minh phép chiếu biến
  trọng tâm thành trọng tâm; kiểm tra được 1 hình phẳng có thể là hình biểu
  diễn hợp lệ hay không dựa vào tỉ lệ (không phải nhìn bằng mắt); vẽ hình
  biểu diễn khối chóp đáy hình thang; giải thích hiện tượng thực tế liên
  quan tới ánh sáng song song.

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Trả lời đúng nhưng không lập luận được vì sao (tính đối xứng của phép chiếu) | Đoán theo cảm tính thay vì quay lại đúng định nghĩa phép chiếu theo phương ngược lại | Chọn đúng đáp án Có/Không nhưng không giải thích được cơ chế |
| Kiểm tra tính hợp lệ của hình biểu diễn chỉ bằng mắt | Không dùng tỉ lệ cụ thể trên các cặp đoạn song song để kiểm chứng | Nhận định "trông giống nên chắc đúng" mà không đo đạc |
| Áp nhầm tính chất trung điểm cho trọng tâm | Nhầm lẫn 2 khái niệm khi chứng minh phép chiếu bảo toàn trọng tâm | Lập luận sai khi tính tỉ lệ liên quan tới trọng tâm (liên hệ sai lầm đã gặp ở Module 13.7 Tab 4) |

## 🧊 ĐẶC THÙ 3D

- **Khối/đối tượng nền:** tứ giác/hình bình hành phẳng (Tab 1), lục giác
  phẳng (Tab 2), hình chóp đáy hình thang (Tab 3), mô hình hàng rào gỗ +
  ánh sáng song song (Tab 4).
- **Góc camera mặc định:** `setCameraStandardSGK()`, riêng Tab 4 dùng góc
  nhìn kiểu ngoài trời (thấp, nhìn chéo lên).
- **Mức độ tương tác:** Tab 1 — MCQ + dựng dần (I + F). Tab 2 — đo tỉ lệ
  (D3). Tab 3 — dựng dần đối chiếu (F, tái dùng kỹ thuật Module 14.3 Tab 3).
  Tab 4 — MCQ/quan sát (I).
- **Nguyên tắc bắt buộc xuyên suốt:** sau MỌI bước tương tác đều có giải
  thích kiến thức đầy đủ, không để trống hay chỉ báo Đúng/Sai trơn.

---

## TAB 1 — Lý luận & chứng minh tính chất

**Loại simulation:** I (MCQ) + F (dựng dần).
**Thời gian dự kiến:** ~5-6 phút.

### Sổ tay kiến thức (Có — tổng hợp, hiện xuyên suốt module):
- Tính chất phép chiếu song song: biến 3 điểm thẳng hàng thành 3 điểm
  thẳng hàng cùng thứ tự; biến đoạn thẳng thành đoạn thẳng; biến 2 đường
  song song thành 2 đường song song hoặc trùng nhau; giữ nguyên tỉ số độ
  dài trên 1 đường thẳng hoặc 2 đường thẳng song song.

### Phần A — Nhận định đúng/sai (viết mới, không dùng lại mệnh đề 4.29)

**Mệnh đề 1:** "Phép chiếu song song luôn biến 1 tam giác thành 1 tam giác
có diện tích bằng nhau."
- Đáp án: **Sai**. `giai_thich_dung`: Phép chiếu song song không bảo toàn
  độ dài và góc, nên diện tích tam giác ảnh thường KHÁC diện tích tam giác
  gốc — chỉ có tỉ số độ dài trên đường thẳng song song là được bảo toàn,
  diện tích thì không.
- `goi_y_khi_sai`: Nhớ lại Tab 1 Module 14.3 — khi chiếu hình vuông, độ dài
  cạnh có giữ nguyên không?

**Mệnh đề 2:** "Nếu 2 đoạn thẳng bằng nhau và không song song thì hình
chiếu của chúng qua cùng 1 phép chiếu song song cũng luôn bằng nhau."
- Đáp án: **Sai**. `giai_thich_dung`: Tính chất bảo toàn tỉ lệ CHỈ áp dụng
  cho các đoạn thẳng nằm trên CÙNG 1 đường thẳng hoặc trên các đường thẳng
  SONG SONG với nhau — nếu 2 đoạn không song song, độ dài hình chiếu của
  chúng có thể khác nhau dù đoạn gốc bằng nhau.
- `goi_y_khi_sai`: Điều kiện chính xác của tính chất bảo toàn tỉ lệ đã học
  ở Module 14.2 là gì — áp dụng cho đoạn thẳng bất kỳ hay chỉ đoạn thẳng
  cùng phương/song song?

**Mệnh đề 3:** "Phép chiếu song song biến 1 hình chữ nhật thành 1 hình bình
hành."
- Đáp án: **Đúng**. `giai_thich_dung`: Hình chữ nhật có 2 cặp cạnh song
  song, cả 2 cặp đều giữ song song qua phép chiếu, nên ảnh là 1 hình bình
  hành (đã học ở Module 14.3).
- `goi_y_khi_sai`: Hình chữ nhật có bao nhiêu cặp cạnh song song? Chúng có
  giữ song song qua phép chiếu không?

### Phần B — Tính đối xứng của phép chiếu (case cụ thể, không dùng lại câu
hỏi tổng quát của bài 4.30)

**Đề bài:** Cho tứ giác EFGH là hình bình hành. Qua phép chiếu song song
theo phương Δ, EFGH có hình chiếu là tứ giác MNPQ. Hỏi: nếu ta thực hiện
phép chiếu song song theo phương Δ' = −Δ (ngược hướng hoàn toàn với Δ)
xuất phát từ MNPQ, có thu được lại đúng EFGH không?

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát animation chiếu EFGH → MNPQ theo phương Δ | Mỗi điểm M (thuộc MNPQ) là giao điểm của đường thẳng qua điểm gốc tương ứng (thuộc EFGH), song song Δ, với mặt phẳng chiếu. |
| 2 | Trả lời: "Chiếu MNPQ theo Δ' = −Δ có cho lại EFGH không?" (Có/Không) | Đáp án: Có. |
| 3 | **Bắt buộc chọn tiếp lý do đúng** (không cho tự luận tự do, nhưng buộc chọn đúng lập luận): (I) "Vì Δ' cùng phương với Δ, chỉ khác hướng — đường thẳng qua M song song Δ' vẫn là ĐÚNG đường thẳng đã dùng để tạo ra M ban đầu, nên đi ngược lại đúng điểm gốc E" / (II) "Vì mọi phép chiếu đều có thể đảo ngược" / (III) "Vì EFGH và MNPQ đều là hình bình hành nên đối xứng nhau" | Đáp án đúng: (I). Lý do (II) sai vì phát biểu quá chung chung, không giải thích được CƠ CHẾ; lý do (III) sai vì đây không liên quan tới việc cả 2 đều là hình bình hành — tính đối xứng này đúng với MỌI hình, không riêng gì hình bình hành. |

### Phần C — Chứng minh phép chiếu biến trọng tâm thành trọng tâm (dựng dần)

**Đề bài:** Phép chiếu song song biến tam giác EFG thành tam giác E'F'G'.
Chứng minh phép chiếu này biến trọng tâm K của EFG thành trọng tâm K' của
E'F'G'.

> ⏱️ **Lưu ý nhịp độ (sau rà soát):** Phần C là phần lập luận phức tạp nhất
> trong cả module — đã chia lại thành 7 bước nhỏ (thay vì 4 bước gộp), mỗi
> bước chỉ chứa ĐÚNG 1 ý mới, không dồn nhiều lý do vào cùng 1 dòng. Không
> có bước nào yêu cầu học sinh tự suy ra 2 điều cùng lúc.

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát tam giác EFG và điểm K (trọng tâm) đã đánh dấu sẵn — bấm "Nhắc lại trọng tâm là gì?" | Trọng tâm K là giao điểm của 3 đường trung tuyến (đoạn nối 1 đỉnh với trung điểm cạnh đối diện). Đây là kiến thức đã học ở lớp dưới, chỉ nhắc lại để dùng tiếp. |
| 2 | Bấm "Dựng trung tuyến EM" — hệ thống animate vẽ M (trung điểm FG) rồi vẽ đoạn EM | EM là 1 trong 3 đường trung tuyến của tam giác EFG, đi qua đỉnh E và trung điểm M của cạnh đối diện FG. |
| 3 | Quan sát: hệ thống hiện rõ số đo "EK : KM = 2 : 1" ngay trên hình | Đây là tính chất CỐ ĐỊNH của mọi trọng tâm tam giác: trọng tâm luôn chia mỗi đường trung tuyến theo đúng tỉ lệ 2:1 tính từ đỉnh. Ghi nhớ số này — bước sau sẽ dùng lại. |
| 4 | Bấm "Chiếu cả hình" — hệ thống animate chiếu ĐỒNG THỜI tam giác EFG, điểm M, và điểm K sang E'F'G', M', K' theo cùng 1 phép chiếu | Toàn bộ hình (bao gồm cả đường trung tuyến EM và điểm K) đều được chiếu cùng lúc, theo đúng 1 phép chiếu song song duy nhất — không có phép chiếu nào khác cho từng điểm riêng lẻ. |
| 5 | Trả lời (chỉ 1 câu hỏi, không kèm gì khác): "M có phải là trung điểm của FG không?" (Có/Không) | Đáp án: Có — M được dựng chính là trung điểm FG ở bước 2. (Đây chỉ là câu hỏi xác nhận lại, chưa phải phần chiếu.) |
| 6 | Trả lời: "Vậy M' (ảnh của M qua phép chiếu) có phải là trung điểm của F'G' không?" (Có/Không) | Đáp án: Có — vì phép chiếu song song bảo toàn tỉ lệ trên 1 đoạn thẳng (đã học Module 14.2). M chia FG theo tỉ lệ 1:1 (vì là trung điểm), nên M' cũng chia F'G' theo đúng tỉ lệ 1:1 — tức M' là trung điểm F'G'. |
| 7 | Trả lời: "K chia EM theo tỉ lệ 2:1 (từ bước 3) — vậy K' có chia E'M' theo đúng tỉ lệ 2:1 không?" (Có/Không) | Đáp án: Có — cùng lý do bảo toàn tỉ lệ trên đoạn thẳng: K nằm trên EM với tỉ lệ EK:KM = 2:1, nên K' cũng nằm trên E'M' với đúng tỉ lệ E'K':K'M' = 2:1, không đổi. |
| 8 | Xem kết luận | Ghép lại 2 điều vừa xác nhận: (a) M' là trung điểm F'G' (bước 6), (b) K' chia E'M' theo tỉ lệ 2:1 từ đỉnh E' (bước 7). Mà "điểm chia đường trung tuyến theo tỉ lệ 2:1 từ đỉnh" CHÍNH LÀ định nghĩa của trọng tâm — nên K' là trọng tâm của E'F'G'. Đây là ví dụ điển hình: KHÔNG áp trực tiếp "trọng tâm chiếu thành trọng tâm" như 1 điều hiển nhiên, mà phải LẬP LUẬN qua từng bước tỉ lệ trên trung tuyến — đúng lưu ý về sai lầm nhầm trọng tâm/trung điểm đã học ở Module 13.7. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống Phần C: Học sinh có thể muốn kết luận ngay ở bước 3-4 "trọng
  tâm chiếu thành trọng tâm vì nó luôn đúng vậy" mà không qua hết các bước
  lập luận trung gian bằng trung tuyến.
- Hệ thống phản hồi: Nút "Xem kết luận" (bước 8) chỉ sáng sau khi bước 5,
  6, 7 đã trả lời đúng theo ĐÚNG thứ tự — nếu bấm sớm, hiện: "Cần xác nhận
  từng bước qua trung tuyến EM trước — đây là cách LẬP LUẬN đúng, không
  phải điều hiển nhiên."
- Kết quả rút ra: Củng cố thói quen lập luận qua các bước trung gian
  (trung điểm → tỉ lệ trên trung tuyến → trọng tâm), không kết luận trực
  tiếp.

### Cấu hình 3D: Phần A/B minh hoạ tĩnh xoay được; Phần C animate dựng dần
trung tuyến. Cleanup: `clearScene()` giữa các phần và khi sang Tab 2.

---

## TAB 2 — Kiểm tra tính hợp lệ của hình biểu diễn

**Loại simulation:** D3 (đo tỉ lệ) + nhận định.
**Thời gian dự kiến:** ~3-4 phút.

> 📝 **Ghi chú bản quyền:** Đổi hình lục giác (số liệu/hình dạng khác Hình
> 4.65 SGK — SGK cho lục giác có các cạnh đánh dấu bằng nhau theo kiểu
> riêng, ở đây đổi cách đánh dấu và tỉ lệ khác).

### Đề bài: Hình MNPQRS dưới đây được cho là hình biểu diễn của 1 lục giác
đều. Dùng công cụ đo tỉ lệ để tự kiểm tra xem điều này có hợp lý không.

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát hình MNPQRS — KHÔNG kết luận vội bằng mắt | Nhắc lại: lục giác đều có 3 cặp cạnh đối song song và bằng nhau — hình biểu diễn phải giữ đúng tính chất song song VÀ tỉ lệ (không nhất thiết trông "đều" bằng mắt). |
| 2 | Bấm "Đo tỉ lệ cặp cạnh 1" (MN và QP, đối diện nhau) — hệ thống hiện tỉ số độ dài | Kết quả đo: MN/QP = [giá trị cụ thể]. |
| 3 | Lặp lại "Đo tỉ lệ cặp cạnh 2" và "cặp cạnh 3" cho 2 cặp cạnh đối diện còn lại | So sánh: nếu cả 3 tỉ lệ đều bằng 1 (các cặp cạnh đối bằng nhau) VÀ các cặp đều song song (đã quan sát ở bước 1), thì hình này CÓ THỂ là hình biểu diễn hợp lệ của lục giác đều. |
| 4 | Trả lời kết luận: "Hình MNPQRS có thể là hình biểu diễn hợp lệ của 1 lục giác đều không?" (Có/Không) | Đáp án tuỳ theo số liệu cụ thể được build (thiết kế sao cho ĐÚNG là hợp lệ, để học sinh thấy quy trình đo tỉ lệ dẫn tới kết luận khẳng định, củng cố tích cực việc dùng công cụ đo thay vì chỉ nhìn). |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể nhìn hình MNPQRS thấy "không đều, méo mó" và
  vội kết luận "Không" mà chưa đo.
- Hệ thống phản hồi: Nút "Trả lời kết luận" chỉ sáng sau khi đã đo đủ 3 cặp
  cạnh (bước 2-3) — nếu cố trả lời sớm, hiện: "Hình biểu diễn của lục giác
  đều KHÔNG cần trông đều bằng mắt — bạn cần đo tỉ lệ cụ thể trước khi kết
  luận."
- Kết quả rút ra: Củng cố nguyên tắc "đo tỉ lệ, không đoán bằng mắt" — đúng
  sai lầm trọng tâm cần giải quyết của tab này.

### Cấu hình 3D: Công cụ đo hiện số tỉ lệ real-time khi bấm từng cặp cạnh.
Cleanup: `clearScene()` khi sang Tab 3.

---

## TAB 3 — Vẽ hình biểu diễn khối chóp đáy hình thang

**Loại simulation:** F (dựng dần, đối chiếu khối 3D thật — tái dùng kỹ
thuật đã luyện ở Module 14.3 Tab 3).
**Thời gian dự kiến:** ~3-4 phút.

> 📝 **Ghi chú bản quyền:** Đổi từ AB=2cm, CD=6cm (bài 4.33 gốc, tỉ lệ
> CD=3AB) sang **AB = 4cm, CD = 3cm** (tỉ lệ AB=4/3×CD) — số nguyên mới,
> chưa trùng với bất kỳ tỉ lệ nào đã dùng ở Ví dụ 4 SGK (2), bài 4.33 gốc
> (3), hay Module 14.3 Tab 2c (1.5) và Tab 3 (2.5). Đổi từ lăng trụ (14.3)
> sang HÌNH CHÓP để đa dạng hoá loại khối.

### Đề bài: Cho hình chóp S.ABCD, đáy ABCD là hình thang, AB // CD,
AB = 4cm, CD = 3cm. Vẽ hình biểu diễn của hình chóp này.

### Sổ tay kiến thức (Có — nhắc lại): quy tắc hình thang (giữ tỉ lệ 2 đáy)
+ đỉnh chóp S không nằm trên mặt đáy nên hình biểu diễn của S là 1 điểm bất
kỳ không thẳng hàng với các cạnh đáy đã vẽ (khác lăng trụ, không cần tịnh
tiến toàn bộ đáy).

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Kéo chỉnh tỉ lệ đáy hình thang biểu diễn A'B'C'D' sao cho A'B'/C'D' = 4/3 | Áp dụng đúng quy tắc: hình thang biểu diễn phải giữ tỉ lệ AB/CD = 4/3 như đề cho. |
| 2 | Đặt điểm S' (đỉnh chóp biểu diễn) ở vị trí bất kỳ phía trên, không thẳng hàng với các cạnh đáy | Vì S không nằm trong mặt phẳng đáy ABCD, hình biểu diễn S' của nó chỉ cần là 1 điểm không thuộc mặt phẳng chứa đáy biểu diễn — không có ràng buộc tỉ lệ đặc biệt như với đáy (khác hẳn lăng trụ, nơi đáy trên phải tịnh tiến theo đúng 1 vector). |
| 3 | Bấm "Nối các cạnh bên" — hệ thống tự nối S'A', S'B', S'C', S'D' | Đây chính là hình biểu diễn hoàn chỉnh của hình chóp — 4 cạnh bên nối từ đỉnh biểu diễn tới 4 đỉnh đáy biểu diễn, không cần giữ tỉ lệ hay song song đặc biệt giữa các cạnh bên (khác lăng trụ). |
| 4 | Đối chiếu với khối 3D thật xoay được bên cạnh | So sánh trực quan: dù S' được đặt khá tự do, hình biểu diễn vẫn truyền tải đúng cấu trúc "1 đỉnh, đáy hình thang" nhờ giữ đúng tỉ lệ đáy — đây là điểm khác biệt quan trọng giữa vẽ hình chóp (đỉnh tự do) và lăng trụ (đáy trên bị ràng buộc bởi phép tịnh tiến, đã luyện ở Module 14.3 Tab 3). |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể nhầm lẫn với quy tắc lăng trụ đã học, cố
  gắng "tịnh tiến" đáy để tìm vị trí đỉnh S' thay vì đặt tự do.
- Hệ thống phản hồi: "Khác với lăng trụ (có 2 đáy), hình chóp chỉ có 1 đáy
  và 1 đỉnh duy nhất — không cần quy tắc tịnh tiến. Bạn có thể đặt S' ở bất
  kỳ đâu phía trên, miễn không thẳng hàng với các cạnh đáy."
- Kết quả rút ra: Phân biệt rõ 2 quy trình vẽ khác nhau cho 2 loại khối
  (lăng trụ ràng buộc chặt, hình chóp tự do hơn ở vị trí đỉnh).

### Cấu hình 3D: Khung trái khối 3D thật xoay tự do; khung phải canvas 2D
dựng hình biểu diễn. Cleanup: `clearScene()` khi sang Tab 4.

---

## TAB 4 — Liên hệ thực tế: hàng rào gỗ dưới nắng

**Loại simulation:** I (MCQ) + quan sát.
**Thời gian dự kiến:** ~2-3 phút.

> 📝 **Ghi chú bản quyền:** Đổi bối cảnh từ "cái thang có 2 thanh chắn"
> (bài 4.34 gốc) sang **hàng rào gỗ có 2 thanh ngang** — giữ nguyên bản
> chất vật lý (ánh nắng song song = phép chiếu song song tự nhiên) nhưng
> đổi hẳn vật thể minh hoạ.

### Đề bài: Một hàng rào gỗ có 2 thanh ngang AB và CD (AB, CD song song
nhau trong không gian thực, gắn cố định trên hàng rào). Dưới ánh nắng mặt
trời, bóng của chúng đổ xuống mặt đất tại 2 đoạn A'B' và C'D'.

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát mô hình 3D — hàng rào với 2 thanh ngang, các tia nắng minh hoạ song song đi tới mặt đất | Ánh nắng mặt trời (do khoảng cách rất xa) được coi là các tia sáng song song — đây chính là 1 phép chiếu song song tự nhiên, với mặt đất là mặt phẳng chiếu và hướng tia nắng là phương chiếu. |
| 2 | Trả lời: "Vì sao bóng A'B' và C'D' trên mặt đất luôn song song nhau?" (chọn: Vì AB//CD trong thực tế và phép chiếu song song bảo toàn tính song song / Vì ánh nắng luôn thẳng đứng / Vì tình cờ hàng rào được lắp song song) | Đáp án: Vì AB//CD trong thực tế và phép chiếu song song bảo toàn tính song song — đúng tính chất đã học ở Module 14.2 (2 đường song song chiếu thành 2 đường song song hoặc trùng nhau), áp dụng cho hiện tượng tự nhiên chứ không phải trùng hợp. |
| 3 | Bấm "Đổi thời điểm trong ngày" — animate góc nắng thay đổi (sáng/trưa/chiều), quan sát bóng A'B', C'D' thay đổi độ dài nhưng vẫn giữ song song | Dù góc nắng thay đổi liên tục trong ngày (phương chiếu Δ thay đổi), tính song song của bóng KHÔNG bao giờ mất — vì AB//CD là bất biến, chỉ có ĐỘ DÀI và HƯỚNG cụ thể của bóng thay đổi theo phương chiếu, còn tính CHẤT song song luôn được bảo toàn với bất kỳ phương chiếu nào. |

### Cấu hình 3D: Animate thay đổi góc nắng (thời gian trong ngày) làm nổi
bật tính bất biến của "song song" dù phương chiếu thay đổi. Cleanup:
`clearScene()` khi kết thúc module.

---

## 🎯 TỔNG KẾT CUỐI MODULE 14.4

**Tổng kết kiến thức:**
- Phép chiếu song song bảo toàn: thẳng hàng, đoạn thẳng, song song, tỉ lệ
  trên đường thẳng/2 đường thẳng song song — KHÔNG bảo toàn: góc, độ dài
  tuyệt đối, diện tích.
- Phép chiếu song song có tính đối xứng: nếu chiếu theo phương Δ cho ảnh
  A'B'C', thì chiếu ngược lại theo phương −Δ từ A'B'C' sẽ cho lại đúng ABC.
- Kiểm tra tính hợp lệ của 1 hình biểu diễn cần ĐO TỈ LỆ cụ thể trên các
  cặp cạnh song song, không dựa vào cảm giác thị giác.
- Vẽ hình chóp và lăng trụ có quy trình khác nhau: lăng trụ ràng buộc chặt
  (đáy trên phải tịnh tiến theo đúng 1 vector), hình chóp tự do hơn (đỉnh
  có thể đặt bất kỳ vị trí không thẳng hàng với đáy).
- Hiện tượng ánh nắng tạo bóng song song là 1 ứng dụng thực tế trực tiếp
  của phép chiếu song song.

**Tổng kết sai lầm:**
1. Trả lời đúng mà không lập luận được vì sao — dấu hiệu: chọn đúng đáp án
   Có/Không nhưng không giải thích được cơ chế đứng sau.
2. Kiểm tra tính hợp lệ hình biểu diễn chỉ bằng mắt — dấu hiệu: kết luận
   "trông giống nên chắc đúng" mà không đo tỉ lệ.
3. Áp nhầm tính chất trung điểm cho trọng tâm — dấu hiệu: lập luận sai khi
   tính tỉ lệ liên quan tới trọng tâm.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

📝 **Rà soát bản quyền:** Tab 1 Phần B đổi từ câu hỏi tổng quát (4.30 gốc)
sang case cụ thể với tứ giác EFGH/MNPQ và phương Δ/−Δ, có thêm bước bắt
buộc chọn đúng LẬP LUẬN (không có trong SGK gốc). Tab 2 đổi số liệu/cách
đánh dấu lục giác khác Hình 4.65. Tab 3 đổi tỉ lệ AB=4cm, CD=3cm (số nguyên
mới, chưa trùng bất kỳ tỉ lệ nào dùng trước đó) + đổi từ lăng trụ (14.3)
sang hình chóp. Tab 4 đổi bối cảnh "cái thang" sang "hàng rào gỗ", thêm
phần animate đổi góc nắng trong ngày (không có trong SGK gốc).

📖 **Kiểm tra caption:** Đã rà toàn bộ 4 tab — mọi bước tương tác đều có
giải thích kiến thức đầy đủ, không có bước nào chỉ báo Đúng/Sai trơn.

⚠️ **Rủi ro 1 (đã xử lý):** Tab 1 Phần C ban đầu gộp 4 bước, mỗi bước chứa
nhiều lý do cùng lúc — đã chia lại thành 8 bước nhỏ, mỗi bước chỉ 1 ý mới,
tách riêng phần "xác nhận M là trung điểm FG" (kiến thức đã biết) khỏi phần
"suy ra M' là trung điểm F'G'" (kiến thức mới, cần lập luận). Đảm bảo không
bước nào yêu cầu học sinh tự suy 2 điều cùng lúc.

⚠️ **Rủi ro 2 (đã xác nhận, cần thực hiện khi build):** Tab 2 (đo tỉ lệ lục
giác) — bắt buộc verify bằng script Node độc lập số liệu dựng sẵn trước khi
build, đảm bảo kết quả đo ra đúng "Có" (hợp lệ) với sai số dựng hình đủ nhỏ
để không gây hoài nghi.

---

**Kịch bản đã sẵn sàng! Đây là module cuối cùng của Bài 14 (14.1→14.4) mà
bạn yêu cầu — 14.5/14.6 (Ôn tập chương IV) là bài học riêng, chưa nằm trong
phạm vi lần này.**

- ✅ Duyệt — mình chuyển sang draft ý tưởng phần "Em có biết" như đã hẹn
- ✏️ Chỉnh — nêu rõ phần nào cần thay đổi

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 12/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`,
> `01_scenario_builder_3d_addendum.md`, `04_design_toan_3d.md`,
> `05_threejs_engine.md`, `06_geometry_math.md`, đối chiếu với
> Module 14.3 (kỹ thuật dựng hình biểu diễn tái dùng ở Tab 3)
