# 📋 KỊCH BẢN SIMULATION — MODULE 13.5
## Hình lăng trụ: định nghĩa và tính chất

**Bài SGK:** Bài 13 — Hai mặt phẳng song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 13.5 — nối tiếp Module 13.1-13.4.
Tương ứng phần "4. HÌNH LĂNG TRỤ VÀ HÌNH HỘP" (trang 91-92 SGK).
**Trạng thái kiến thức nền:** Dạy khái niệm MỚI (định nghĩa hình lăng trụ) —
khác 13.4 (luyện tập). Sổ tay kiến thức chỉ xuất hiện từ Tab 2 trở đi.
**Nguồn SGK tham chiếu:** HĐ6, định nghĩa hình lăng trụ, Ví dụ 5, Luyện tập 5,
HĐ7 (trang 91-92) — số liệu/vị trí trong simulation đã đổi khác SGK.
**Tài nguyên tái dùng:** `SOLID_LIBRARY.lang_tru_tam_dung`,
`SOLID_LIBRARY.lang_tru_tu_dung` từ hệ thống Kho Khối Hình Không Gian (Nhánh
B) — dựng sẵn bằng slider tham số, không cần code lại khối từ đầu.

---

## 🎯 MỤC TIÊU

- HIỂU: nhận biết cấu trúc hình lăng trụ (2 mặt đáy là đa giác bằng nhau nằm
  trên 2 mặt phẳng song song, các mặt bên là hình bình hành, các cạnh bên
  song song và bằng nhau).
- LÀM ĐƯỢC: chứng minh 1 hình là hình lăng trụ khi biết mặt phẳng song song
  đáy cắt các cạnh bên (dạng Ví dụ 5/Luyện tập 5).

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Nhầm lẫn "lăng trụ" với "hình hộp" ngay từ đầu | Nghĩ lăng trụ phải có đáy tứ giác | Gọi sai tên khi đáy không phải hình bình hành hoặc quên rằng hình hộp chỉ là 1 dạng đặc biệt của lăng trụ tứ giác |
| Không kiểm tra đủ 2 điều kiện | Chỉ kiểm tra 1 trong 2 (mặt bên là hình bình hành HOẶC cạnh bên song song-bằng nhau) | Kết luận "là lăng trụ" vội vàng chỉ sau khi thấy 1 điều kiện thoả |
| Nhầm tên gọi lăng trụ theo đáy | Không đếm đúng số cạnh của đa giác đáy | Đếm sai số cạnh hoặc gọi theo hình dạng tổng thể thay vì đúng số cạnh đáy |

## 🧊 ĐẶC THÙ 3D

- **Khối nền:** tái dùng `lang_tru_tam_dung` (Tab 1, 4), `lang_tru_tu_dung`
  (Tab 2, 3) từ `SOLID_LIBRARY` — không dựng riêng.
- **Quan hệ không gian trọng tâm:** cấu trúc hình lăng trụ (đáy, mặt bên,
  cạnh bên) và 2 điều kiện định nghĩa.
- **Góc camera mặc định:** nhìn chéo để thấy rõ cả 2 đáy và các mặt bên.
- **Mức độ tương tác:** Tab 1, 3 — click chọn (H). Tab 2 — quan sát + click
  xác nhận (F). Tab 4 — kéo điểm ràng buộc (D3).
- **Lưu ý kỹ thuật quan trọng:** field `explore` trong `SOLID_LIBRARY` là
  metadata CHƯA được code sử dụng (dead code) — không dựa vào đây cho bất kỳ
  tương tác kéo-thả nào. Tab 4 dùng kỹ thuật kéo điểm ràng buộc trên mặt
  phẳng đã verify riêng ở hệ thống Bài 10.
- **Nguyên tắc bắt buộc xuyên suốt cả module:** sau MỌI bước tương tác — dù
  đúng hay sai — đều có giải thích kiến thức đi kèm, không để trống hay chỉ
  báo "Đúng/Sai" trơn. Mỗi bước đều có hướng dẫn thao tác cụ thể trước khi
  học sinh làm.

---

## TAB 1 — Cấu trúc lăng trụ tam giác

**Loại simulation:** H (click chọn trên khối có sẵn).
**Thời gian dự kiến:** ~2-3 phút.
**Khối nền:** `lang_tru_tam_dung` (ABC.A'B'C').
**Sổ tay kiến thức:** Ẩn — đây là hình thành khái niệm mới, kiến thức hiện
dần qua từng bước click.

### Hướng dẫn mở đầu (hiện ngay khi vào tab):
> "Đây là hình lăng trụ tam giác ABC.A'B'C'. Bạn hãy lần lượt click vào từng
> phần được đánh dấu bên dưới — mỗi lần click, mình sẽ giải thích đó là gì
> và vì sao nó được gọi như vậy."

### Học sinh tương tác bằng cách — 5 bước tuần tự, có checklist:

| Bước | Hướng dẫn thao tác | Sau khi click — giải thích kiến thức |
|---|---|---|
| 1 | Click vào mặt đáy dưới (tam giác ABC, viền vàng nhấp nháy gợi ý) | Đây là 1 trong 2 mặt đáy của lăng trụ. Mặt đáy là đa giác nằm trên 1 trong 2 mặt phẳng song song tạo nên lăng trụ. |
| 2 | Click vào mặt đáy trên (tam giác A'B'C') | Đây là mặt đáy còn lại — luôn bằng mặt đáy dưới (cùng hình dạng, cùng kích thước), nằm trên mặt phẳng song song với mặt đáy dưới. |
| 3 | Click vào 1 mặt bên bất kỳ (VD ABB'A') | Đây là mặt bên — luôn có dạng hình bình hành. Lăng trụ tam giác có đúng 3 mặt bên (bằng số cạnh của đáy). |
| 4 | Click vào 1 cạnh bên (VD AA') | Đây là cạnh bên — nối 1 đỉnh đáy dưới với đỉnh tương ứng ở đáy trên. Tất cả cạnh bên của 1 lăng trụ luôn song song và bằng nhau. |
| 5 | Click vào 1 cạnh đáy (VD AB) | Đây là cạnh đáy — thuộc 1 trong 2 mặt đáy, không phải cạnh bên. Phân biệt: cạnh đáy nằm ngang trong mặt đáy, cạnh bên nối 2 đáy. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể click nhầm cạnh bên (AA') tưởng là cạnh đáy vì
  trong hình chiếu 2D nhìn cũng là 1 đoạn thẳng.
- Hệ thống phản hồi: Khi click sai loại đối tượng ở đúng bước đang yêu cầu
  (VD bước 5 yêu cầu cạnh đáy nhưng click cạnh bên), hiện: "Đây là cạnh bên
  (nối 2 mặt đáy), không phải cạnh đáy — cạnh đáy nằm NGANG trong 1 mặt đáy.
  Thử click lại."
- Học sinh điều chỉnh: xoay camera nhìn từ trên xuống để phân biệt rõ cạnh
  nằm trong mặt đáy và cạnh nối 2 đáy.
- Kết quả rút ra: Phân biệt rõ 2 loại cạnh bằng vị trí không gian, không chỉ
  bằng hình chiếu 2D.

### Sau khi hoàn thành checklist 5/5 — Chốt khái niệm:
> "Bạn vừa nhận diện đủ 4 thành phần của hình lăng trụ: 2 mặt đáy (song
> song, bằng nhau) — mặt bên (hình bình hành) — cạnh bên (song song, bằng
> nhau) — cạnh đáy. Đây chính là cấu trúc chung của MỌI hình lăng trụ, không
> riêng gì lăng trụ tam giác."

### Cấu hình 3D:
- Dùng cơ chế click-to-select đã verify của Kho Khối Hình Không Gian
  (`currentMode='point'`, hitMesh theo `kind:'face'`/`'edge'`) để bắt sự
  kiện click đúng loại đối tượng theo từng bước.
- **Không dùng** field `explore` (dead code).
- Cleanup: `clearScene()` khi sang Tab 2.

---

## TAB 2 — Kiểm chứng qua câu hỏi ngược (mặt phẳng cắt tạo lăng trụ mới)

**Loại simulation:** F (dựng dần có animation, học sinh quan sát + click xác nhận).
**Thời gian dự kiến:** ~3-4 phút.
**Khối nền:** `lang_tru_tu_dung` (ABCD.A'B'C'D' — đổi từ lăng trụ **tam
giác** sang **tứ giác** so với bản trước, tránh trùng đối tượng của Ví dụ 5
SGK).

### Sổ tay kiến thức (Có — hiện ngay đầu tab):
- Nhắc lại 2 điều kiện lăng trụ (từ Tab 1): (1) các mặt bên là hình bình
  hành; (2) các cạnh bên đôi một song song và bằng nhau.

### Hướng dẫn mở đầu (đổi hướng câu hỏi — THUẬN sang NGƯỢC so với Ví dụ 5
SGK, tránh trùng cấu trúc "cho sẵn mặt cắt rồi yêu cầu chứng minh"):
> "Lăng trụ ABCD.A'B'C'D' có 1 mặt phẳng cắt các cạnh bên tại A'', B'', C'',
> D''. Hệ thống cho bạn xem lần lượt 3 phương án vị trí mặt cắt khác nhau —
> nhiệm vụ của bạn KHÔNG phải là chứng minh 1 phương án có sẵn, mà là TỰ XÁC
> ĐỊNH xem phương án nào (nếu có) khiến ABCD.A''B''C''D'' trở thành 1 hình
> lăng trụ hợp lệ."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Bấm "Xem phương án 1" — mặt cắt SONG SONG đáy nhưng đặt LỆCH (không cùng khoảng cách đến đáy dưới tại mỗi cạnh bên — mặt cắt bị "nghiêng" giả) | Quan sát: các điểm A'', B'', C'', D'' KHÔNG cùng nằm trên 1 mặt phẳng thật sự song song đáy. |
| 2 | Trả lời: "Phương án 1 có tạo thành lăng trụ hợp lệ không?" (Có/Không) | Đáp án: Không — vì mặt cắt không phải mặt phẳng thật (các điểm không đồng phẳng đúng cách), nên cạnh bên AA'', BB'', CC'', DD'' không cùng độ dài, mặt bên không còn là hình bình hành. |
| 3 | Bấm "Xem phương án 2" — mặt cắt là 1 mặt phẳng thật, song song đáy, nhưng cắt LỆCH TÂM (gần đáy dưới hơn hẳn ở 1 phía) | Quan sát: đây LÀ 1 mặt phẳng thật (các điểm đồng phẳng), song song đáy. |
| 4 | Trả lời: "Phương án 2 có tạo thành lăng trụ hợp lệ không?" (Có/Không) | Đáp án: Có — dù cắt lệch tâm thị giác, vì mặt cắt là 1 mặt phẳng thật SỰ song song đáy, nên giao tuyến với mỗi mặt bên đều song song cạnh đáy tương ứng (tính chất đã học Module 13.1-13.2), khiến AA''=BB''=CC''=DD'' và các mặt bên đều là hình bình hành. Vị trí "lệch tâm thị giác" không ảnh hưởng — chỉ cần LÀ mặt phẳng song song đáy là đủ. |
| 5 | Xem kết luận tổng hợp | Điều kiện duy nhất quyết định là mặt cắt có phải 1 mặt phẳng THẬT SỰ song song đáy hay không — không liên quan đến việc nó "trông cân đối" hay "lệch tâm" trên hình vẽ. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể trả lời "Có" cho phương án 1 vì nhìn thoáng
  qua các điểm A'', B'', C'', D'' vẫn "trông như" nằm ngang tương đối đều
  nhau trên các cạnh bên.
- Hệ thống phản hồi: Không phán xét ngay — cho phép bấm "Kiểm tra đồng
  phẳng" để hệ thống tô màu 4 điểm và thử vẽ 1 mặt phẳng đi qua chúng; nếu
  không đồng phẳng, mặt phẳng thử sẽ hiện "méo"/không khớp hoàn toàn 4 điểm.
- Học sinh điều chỉnh: quan sát trực quan mặt phẳng thử bị lệch, tự nhận ra
  4 điểm không đồng phẳng.
- Kết quả rút ra: "Trông đều nhau trên từng cạnh riêng lẻ" không đồng nghĩa
  "cùng nằm trên 1 mặt phẳng" — đây là góc nhìn mới, khác hẳn sai lầm số 2 đã
  học ở bản trước (chỉ kiểm tra 1/2 điều kiện) — ở đây là kiểm tra điều kiện
  TIỀN ĐỀ (có phải mặt phẳng thật hay không) trước khi xét đến 2 điều kiện
  lăng trụ.

### Cấu hình 3D:
- Animation chuyển đổi giữa 2 phương án mặt cắt (dựng lại điểm A'', B'', C'',
  D'' theo từng phương án, không animate dựng dần từng điểm như Ví dụ 5 gốc).
- Camera: nhìn chéo thấy rõ cả đáy dưới, mặt cắt, và đáy trên.
- Cleanup: `clearScene()` khi sang Tab 3.

---

## TAB 3 — Đối chiếu tên gọi lăng trụ theo đáy

**Loại simulation:** H (click chọn) + trắc nghiệm ngắn.
**Thời gian dự kiến:** ~2 phút.
**Khối nền:** `lang_tru_tu_dung` (đáy hình bình hành).

### Sổ tay kiến thức (Có): "Tên lăng trụ gọi theo tên đa giác đáy".

### Hướng dẫn mở đầu:
> "Ở đây là hình lăng trụ tứ giác ABCD.A'B'C'D'. Bạn đếm số cạnh của mặt
> đáy, rồi chọn đúng tên gọi trong 4 lựa chọn."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Click vào mặt đáy ABCD, đếm số cạnh | Mặt đáy ABCD có 4 cạnh. |
| 2 | Chọn tên gọi đúng: "Lăng trụ tam giác" / "Lăng trụ tứ giác" / "Lăng trụ ngũ giác" / "Hình hộp" (đáp án đúng: Lăng trụ tứ giác, vị trí random) | Nếu đúng: Tên lăng trụ luôn gọi theo tên đa giác đáy — đáy có 4 cạnh nên gọi là lăng trụ tứ giác (đúng Chú ý trong SGK). Nếu sai — VD chọn "Hình hộp": Hình hộp là 1 trường hợp riêng của lăng trụ tứ giác (khi 2 đáy là hình bình hành) — ở đây ABCD là hình bình hành nên đúng là 1 dạng đặc biệt, nhưng tên gọi tổng quát theo số cạnh đáy vẫn là "lăng trụ tứ giác" trước, "hình hộp" là tên gọi thêm khi đáy thoả điều kiện hình bình hành (học kỹ ở Module 13.6). |

### Cấu hình 3D: Cleanup: `clearScene()` khi sang Tab 4.

> **📝 Ghi chú (đã lược bỏ khỏi Tab 3, chuyển sang Module 13.7):** Nội dung
> "lăng trụ xiên vẫn là lăng trụ hợp lệ dù cạnh bên không vuông góc đáy"
> (dùng `lang_tru_tam_xien`/`lang_tru_tu_xien` có sẵn trong `SOLID_LIBRARY`)
> vốn dự kiến làm bước 3 của tab này, nhưng bị đánh giá là nội dung MỞ RỘNG
> ngoài đúng phạm vi Ví dụ 5/Luyện tập 5 SGK, dễ lệch thời lượng dự kiến của
> module dạy khái niệm mới. Sẽ đưa vào phần luyện tập/MCQ của **Module
> 13.7 — Bài tập tổng hợp** thay vì ở đây.

---

## TAB 4 — Thử thách: Tự dựng 1 hình lăng trụ

**Loại simulation:** D3 (kéo điểm ràng buộc trên mặt phẳng ngang — kỹ thuật
đã verify từ Bài 10, KHÔNG dùng field `explore` chưa được build của
`SOLID_LIBRARY`).
**Thời gian dự kiến:** ~4-5 phút.

### Sổ tay kiến thức (Có, dạng checklist tự kiểm tra):
- ✓ Các mặt bên phải là hình bình hành
- ✓ Các cạnh bên phải song song VÀ bằng nhau (thiếu 1 trong 2 đều không đạt)

### Thiết kế chống "dò mù" (đã điều chỉnh sau phản biện):
Ban đầu định để cả 3 điểm A', B', C' tự do cùng lúc — rủi ro biến thành thử
thách vận động tay (fine motor) hơn là thử thách hiểu khái niệm, dễ khiến
học sinh "kéo mãi không trúng" dù đã hiểu đúng lý thuyết. Đã sửa theo 3
hướng:
1. **Chia 2 giai đoạn** — GĐ1 (bắt buộc): chỉ 1 điểm tự do (C'), A' và B' đã
   đặt SẴN ĐÚNG vị trí. GĐ2 (mở rộng, không bắt buộc để hoàn thành module):
   cả 3 điểm tự do.
2. **Snap theo lưới** (grid step 0.25 đơn vị) thay vì kéo tự do pixel-perfect
   — học sinh chỉ cần đưa điểm vào đúng ô lưới là khớp tuyệt đối, loại bỏ
   hoàn toàn vấn đề dung sai/sai số dấu phẩy động.
3. **Số liệu trực quan sống** — hiện độ dài từng cạnh bên (AA', BB', CC') và
   1 chỉ số lệch hướng cạnh mỗi điểm, để học sinh đọc số mà canh, không dò
   bằng mắt thuần túy.
4. **Chống bí:** sau 90 giây không tiến triển hoặc 5 lần thử sai liên tiếp,
   hiện gợi ý cụ thể theo đúng chỉ báo còn thiếu.

### Hướng dẫn mở đầu:
> "Đáy ABC đã cố định. Bên trên có 1 mặt phẳng ngang chứa điểm C' — hiện
> đang đặt SAI vị trí (A', B' đã đúng sẵn). Nhiệm vụ: kéo C' trong mặt phẳng
> đó (và có thể chỉnh độ cao bằng slider riêng) sao cho ABC.A'B'C' trở thành
> 1 hình lăng trụ thật sự — dựa đúng 2 điều kiện đã ôn ở Sổ tay bên trên.
> Điểm sẽ tự khớp vào ô lưới gần nhất khi bạn thả tay, không cần kéo chính
> xác tuyệt đối."

### Học sinh tương tác bằng cách:

| Giai đoạn | Hướng dẫn thao tác cụ thể | Phản hồi real-time (luôn kèm giải thích) |
|---|---|---|
| GĐ1 — Làm quen | "Thử kéo điểm C' bất kỳ hướng để làm quen thao tác — điểm sẽ tự snap vào ô lưới gần nhất khi thả tay" | Khi vừa kéo lần đầu: "Bạn đang di chuyển C' trong mặt phẳng ngang — quan sát độ dài CC' và chỉ báo bên dưới thay đổi theo" |
| GĐ1 — Điều chỉnh | "Kéo C' cho tới khi CẢ 2 chỉ báo đều xanh" | Nếu "Mặt bên: ✓" nhưng "Cạnh bên: ✗" (độ dài CC' ≠ AA', BB'): "Mặt bên đã đúng hình bình hành, nhưng độ dài CC' = [X] chưa bằng AA' = BB' = [Y] — thử kéo C' lên/xuống để khớp độ cao" |
| GĐ1 — Hoàn thành | Tự động khoá khi cả 2 chỉ báo đều ✓ | "Chúc mừng — bạn đã dựng được 1 hình lăng trụ hợp lệ! Đây chính là 2 điều kiện cốt lõi: mặt bên hình bình hành VÀ cạnh bên song song-bằng nhau." + tên gọi tự động: "Lăng trụ tam giác ABC.A'B'C'" |
| GĐ2 — Mở rộng (không bắt buộc) | "Thử thách thêm: bây giờ cả A', B', C' đều tự do và bị xáo vị trí lại — dựng lại từ đầu" | Cùng cơ chế phản hồi như GĐ1, nhưng cả 3 điểm cùng lúc — dành cho học sinh muốn thử thêm |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể kéo C' đạt đúng độ cao (điều kiện cạnh bên)
  nhưng lệch ngang khỏi vị trí đúng (khiến mặt bên không còn là hình bình
  hành).
- Hệ thống phản hồi: Chỉ báo "Cạnh bên: ✓" nhưng "Mặt bên: ✗" → hiện: "Cạnh
  bên đã đúng độ dài, nhưng mặt bên chưa phải hình bình hành — thử đối
  chiếu vị trí C' có giữ đúng hướng song song với AA', BB' hay không (chỉ
  tịnh tiến theo đúng hướng, không lệch ngang tự do)."
- Kết quả rút ra: Cảm giác "nhìn có vẻ đúng" không đủ — cần đối chiếu đúng 2
  điều kiện định lượng được (song song + bằng nhau), củng cố đúng bài học
  cốt lõi của cả module.

### Cấu hình 3D:
- Đối tượng kéo được: GĐ1 — điểm C' (A', B' cố định); GĐ2 — cả 3 điểm A',
  B', C'. Ràng buộc: trong 1 mặt phẳng ngang (kỹ thuật kéo điểm ràng buộc
  trên mặt phẳng, đã verify ở Bài 10), độ cao mặt phẳng chỉnh qua slider
  riêng, snap lưới 0.25 đơn vị.
- Vị trí khởi tạo: lệch khỏi vị trí đúng (không tạo lăng trụ hợp lệ ngay từ
  đầu) để bài toán có ý nghĩa.
- Tính toán real-time: kiểm tra (1) mặt bên có phải hình bình hành (vector
  cạnh đối song song, bằng nhau) và (2) AA', BB', CC' có cùng vector chỉ
  phương và độ dài không — nhờ snap lưới nên so sánh bằng số nguyên lưới,
  không cần dung sai dấu phẩy động.
- Cleanup: `clearScene()` khi rời Tab 4 (kết thúc module).

---

## 🎯 TỔNG KẾT CUỐI MODULE 13.5

**Tổng kết kiến thức:**
- Hình lăng trụ gồm 2 mặt đáy là đa giác bằng nhau, nằm trên 2 mặt phẳng
  song song; các mặt bên là hình bình hành; các cạnh bên đôi một song song
  và bằng nhau.
- Tên lăng trụ gọi theo tên đa giác đáy (lăng trụ tam giác, tứ giác...);
  lăng trụ KHÔNG bắt buộc cạnh bên vuông góc đáy (lăng trụ đứng chỉ là 1
  trường hợp riêng — nội dung này sẽ mở rộng ở Module 13.7).

**Tổng kết sai lầm:**
1. Nhầm lăng trụ với hình hộp — dấu hiệu: gọi sai tên khi đáy không phải
   hình bình hành hoặc quên rằng hình hộp chỉ là 1 dạng đặc biệt của lăng
   trụ tứ giác.
2. Chỉ kiểm tra 1/2 điều kiện — dấu hiệu: kết luận "là lăng trụ" chỉ sau khi
   thấy 1 điều kiện thoả mà chưa xác nhận điều kiện còn lại.
3. Nhầm tên gọi theo đáy — dấu hiệu: đếm sai số cạnh đáy hoặc gọi theo hình
   dạng tổng thể thay vì đúng số cạnh đa giác đáy.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

📝 **Cập nhật rà soát bản quyền (sau khi review toàn bộ Bài 12-13):** Tab 2
ban đầu dùng nguyên lăng trụ TAM GIÁC + đúng ký hiệu A'', B'', C'' + đúng
yêu cầu "cho mặt cắt sẵn rồi chứng minh" — gần như bản sao Ví dụ 5 SGK. Đã
đổi sang lăng trụ TỨ GIÁC và đảo hướng câu hỏi thành câu hỏi NGƯỢC (so sánh
2 phương án mặt cắt, tự xác định phương án nào hợp lệ, dựa trên điều kiện
"có đồng phẳng thật hay không" thay vì chỉ lặp lại 2 điều kiện lăng trụ đã
học ở Tab 1) — khác cả đối tượng, cả cấu trúc câu hỏi so với SGK gốc.

⚠️ **Rủi ro đã xử lý:** Tab 4 ban đầu có nguy cơ "dò mù" do kéo tự do 3
điểm + dung sai dấu phẩy động quá chặt — đã sửa bằng snap-lưới + chia 2 giai
đoạn (1 điểm tự do trước, 3 điểm tự do sau, không bắt buộc) + số liệu trực
quan sống + cơ chế chống bí sau 90s/5 lần sai.

⚠️ **Rủi ro đã xử lý:** Tab 3 bước "lăng trụ xiên" bị đánh giá lệch phạm vi
SGK — đã lược bỏ, chuyển ghi chú sang Module 13.7.

📖 **Kiểm tra caption:** Đã rà toàn bộ 4 tab — mọi bước tương tác đều có
giải thích kiến thức đi kèm, không có bước nào chỉ báo Đúng/Sai trơn (đúng
yêu cầu bắt buộc đã đặt ra).

❓ **Cần làm rõ trước khi build:** Ngưỡng "90 giây không tiến triển" — cần
xác nhận đây có phải mốc thời gian phù hợp với tốc độ thao tác trung bình
của học sinh, hay cần điều chỉnh khi có dữ liệu test người dùng thật.

---

**Kịch bản đã sẵn sàng! Các bước tiếp theo:**
- ✅ Duyệt — chuyển sang Giai đoạn 2 (Thiết kế giao diện chi tiết), sau đó
  tiếp tục Bước 0 cho Module 13.6
- ✏️ Chỉnh — nêu rõ phần nào cần thay đổi

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 11/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`,
> `01_scenario_builder_3d_addendum.md`, `04_design_toan_3d.md`,
> `05_threejs_engine.md`, `06_geometry_math.md`, đối chiếu với
> `solid_library.html` (Kho Khối Hình Không Gian — Nhánh B)
