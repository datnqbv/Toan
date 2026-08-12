# 📋 KỊCH BẢN SIMULATION — MODULE 13.6
## Hình hộp và tính chất

**Bài SGK:** Bài 13 — Hai mặt phẳng song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 13.6 — nối tiếp Module
13.1-13.5. Tương ứng phần định nghĩa hình hộp, Ví dụ 6, Luyện tập 6, Nhận
xét, Vận dụng 2 (trang 92-93 SGK).
**Trạng thái kiến thức nền:** Dạy khái niệm MỚI (định nghĩa hình hộp) —
tiếp nối trực tiếp khái niệm lăng trụ đã dạy ở Module 13.5. Sổ tay kiến thức
ẩn ở Tab 1, xuất hiện dần từ Tab 2.
**Nguồn SGK tham chiếu:** Định nghĩa hình hộp, Ví dụ 6, Luyện tập 6, Nhận
xét, Vận dụng 2 (trang 92-93) — số liệu/vị trí trong simulation đã đổi khác SGK.
**Tài nguyên tái dùng:** `SOLID_LIBRARY.hop_chu_nhat` từ hệ thống Kho Khối
Hình Không Gian (Nhánh B) — dựng sẵn bằng slider tham số.
**Cấu trúc:** Mirror đúng khung 4 tab của Module 13.5, đổi nội dung theo
hình hộp.

---

## 🎯 MỤC TIÊU

- HIỂU: hình hộp là lăng trụ tứ giác ĐẶC BIỆT có đáy là hình bình hành
  (không phải mọi lăng trụ tứ giác đều là hình hộp); nhận biết đỉnh đối
  diện, mặt đối diện, đường chéo của hình hộp.
- LÀM ĐƯỢC: chứng minh 4 đường chéo của hình hộp cùng đi qua trung điểm của
  mỗi đường (dạng Ví dụ 6); chứng minh 2 mặt đối diện song song (dạng Luyện
  tập 6).

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Nhầm mọi lăng trụ tứ giác là hình hộp | Quên điều kiện riêng: đáy phải là hình bình hành | Gọi 1 lăng trụ tứ giác đáy hình thang/thường là "hình hộp" |
| Nhầm "đường chéo hình hộp" với "đường chéo mặt" | Không phân biệt đường xuyên qua khối (nối 2 đỉnh đối diện) với đường nằm trên 1 mặt | Chọn nhầm 1 đường chéo mặt (VD AC) khi được hỏi về đường chéo khối |
| Bỏ qua bước lập luận trung gian khi chứng minh đường chéo cắt tại trung điểm | Kết luận trực tiếp mà không chứng minh tứ giác trung gian (VD ADC'B') là hình bình hành trước | Nhảy thẳng tới "2 đường chéo cắt tại trung điểm" mà không giải thích vì sao |

## 🧊 ĐẶC THÙ 3D

- **Khối nền:** `hop_chu_nhat` (Tab 1, 2, 4) — đổi tên đỉnh theo
  ABCD.A'B'C'D'; Tab 3 thêm 1 khối lăng trụ tứ giác đáy hình thang (không
  phải hình bình hành) để đối chiếu.
- **Quan hệ không gian trọng tâm:** cấu trúc hình hộp (đỉnh đối diện, mặt
  đối diện, đường chéo) và điều kiện riêng "đáy là hình bình hành".
- **Góc camera mặc định:** nhìn chéo để thấy rõ đường chéo xuyên khối.
- **Mức độ tương tác:** Tab 1, 3 — click chọn (H). Tab 2 — quan sát + click
  xác nhận (F). Tab 4 — kéo điểm ràng buộc (D3).
- **Lưu ý kỹ thuật:** field `explore` trong `SOLID_LIBRARY` vẫn là dead code
  — không dùng cho Tab 4. Kỹ thuật kéo điểm ràng buộc trên mặt phẳng (đã
  verify ở Bài 10) + snap lưới (đã áp dụng ở Module 13.5) tiếp tục dùng ở đây.
- **Nguyên tắc bắt buộc xuyên suốt:** sau MỌI bước tương tác đều có giải
  thích kiến thức đi kèm, không để trống hay chỉ báo "Đúng/Sai" trơn.
- **Ngưỡng chống bí Tab 4:** giữ nguyên 90 giây không tiến triển / 5 lần thử
  sai liên tiếp (như đã áp dụng ở Module 13.5).

---

## TAB 1 — Cấu trúc hình hộp

**Loại simulation:** H (click chọn trên khối có sẵn).
**Thời gian dự kiến:** ~2-3 phút.
**Khối nền:** `hop_chu_nhat` (ABCD.A'B'C'D').
**Sổ tay kiến thức:** Ẩn — hình thành khái niệm mới, kiến thức hiện dần qua
từng bước click.

### Hướng dẫn mở đầu:
> "Đây là hình hộp ABCD.A'B'C'D'. Bạn hãy lần lượt click vào từng phần được
> đánh dấu bên dưới — mỗi lần click, mình sẽ giải thích đó là gì."

### Học sinh tương tác bằng cách — 5 bước tuần tự, có checklist:

| Bước | Hướng dẫn thao tác | Sau khi click — giải thích kiến thức |
|---|---|---|
| 1 | Click vào 1 cặp đỉnh đối diện (VD A và C') | A và C' là 2 đỉnh đối diện của hình hộp — 2 đỉnh đối diện là 2 đỉnh không cùng thuộc bất kỳ mặt nào của hình hộp. |
| 2 | Click vào 1 cặp mặt đối diện (VD ABCD và A'B'C'D') | Đây là 2 mặt đối diện — 2 mặt không có điểm chung, có thể coi là 2 đáy của hình hộp. |
| 3 | Click vào 1 đường chéo khối (VD AC') | Đây là 1 đường chéo của hình hộp — nối 2 đỉnh đối diện, xuyên qua bên trong khối. Hình hộp có đúng 4 đường chéo: AC', BD', CA', DB'. |
| 4 | Click vào 1 đường chéo MẶT (VD AC, nằm trên mặt đáy ABCD) — để phân biệt với đường chéo khối | Đây là đường chéo của MẶT ABCD, không phải đường chéo của hình hộp — đường chéo mặt nằm hoàn toàn trên 1 mặt, còn đường chéo khối xuyên qua bên trong. 2 khái niệm khác nhau, dễ nhầm nếu chỉ nhìn hình chiếu 2D. |
| 5 | Trả lời: "Hình hộp có tất cả bao nhiêu đường chéo?" (nhập số hoặc chọn 2/4/6/8) | Đáp án: 4 — ứng với 4 cặp đỉnh đối diện: (A,C'), (B,D'), (C,A'), (D,B'). |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Ở bước 4, học sinh có thể click nhầm 1 đường chéo khối khác
  (VD BD' thay vì AC) vì cả 2 loại đường đều là "đường chéo" theo trực giác
  ban đầu.
- Hệ thống phản hồi: "Đường bạn vừa chọn xuyên qua bên trong khối — đó là
  đường chéo của HÌNH HỘP. Đường chéo MẶT phải nằm hoàn toàn trên 1 mặt
  phẳng của khối (VD mặt đáy ABCD) — thử click lại đúng trên mặt đáy."
- Học sinh điều chỉnh: xoay camera nhìn thẳng vào 1 mặt để thấy rõ đường
  chéo mặt nằm gọn trong đó, không xuyên ra ngoài.
- Kết quả rút ra: Phân biệt bằng vị trí không gian thực (xuyên khối hay nằm
  trên mặt), không chỉ bằng cảm giác "đường chéo là đường nối 2 đỉnh không
  kề nhau".

### Sau khi hoàn thành checklist 5/5 — Chốt khái niệm:
> "Bạn vừa nhận diện đủ các thành phần chính của hình hộp: đỉnh đối diện —
> mặt đối diện — đường chéo khối (4 đường) — và phân biệt được với đường
> chéo mặt. Đây là nền tảng để sang Tab 2, nơi ta sẽ chứng minh 1 tính chất
> đặc biệt của 4 đường chéo này."

### Cấu hình 3D:
- Cơ chế click-to-select đã verify (`currentMode='point'`, hitMesh theo
  `kind:'face'`/`'edge'`/điểm đỉnh).
- Cleanup: `clearScene()` khi sang Tab 2.

---

## TAB 2 — Kiểm chứng tính chất 4 đường chéo cùng qua trung điểm

**Loại simulation:** F (dựng dần có animation, học sinh quan sát + click xác nhận).
**Thời gian dự kiến:** ~4-5 phút (tăng nhẹ do thêm bước tính toán).
**Khối nền:** `hop_chu_nhat`, đổi ký hiệu đỉnh thành **PQRS.P'Q'R'S'**
(khác hẳn ABCD.A'B'C'D' của Ví dụ 6 SGK, tránh trùng ký hiệu).

### Sổ tay kiến thức (Có — hiện ngay đầu tab):
- Nhắc lại: đáy của hình hộp là hình bình hành (từ định nghĩa Tab 1) → tính
  chất đường chéo hình bình hành cắt nhau tại trung điểm mỗi đường (đã học
  ở lớp dưới) sẽ được dùng làm lập luận trung gian.

### Hướng dẫn mở đầu:
> "Ta sẽ chứng minh 4 đường chéo PR', QS', RP', SQ' của hình hộp PQRS.P'Q'R'S'
> cùng đi qua 1 điểm — và điểm đó là trung điểm của MỖI đường. Đây không
> phải điều hiển nhiên nhìn bằng mắt — ta cần lập luận qua từng bước, không
> được kết luận vội. Sau khi chứng minh xong, ta sẽ TÍNH luôn 1 khoảng cách
> cụ thể để thấy tính chất này áp dụng được vào số liệu thật."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Bấm "Dựng đường chéo PR'" — hệ thống animate vẽ đoạn PR' | PR' nối đỉnh P và đỉnh đối diện R'. |
| 2 | Bấm "Dựng đường chéo SQ'" — hệ thống animate vẽ đoạn SQ' | SQ' nối đỉnh S và đỉnh đối diện Q'. |
| 3 | **Bước lập luận trung gian (bắt buộc, không cho nhảy cóc):** Trả lời: "Tứ giác PSR'Q' có phải là hình bình hành không?" (Có/Không) | Nếu ĐÚNG (Có): Vì đáy PQRS là hình bình hành nên PS // QR và PS = QR; mặt bên QRR'Q' cũng là hình bình hành nên QR // Q'R' và QR = Q'R'. Suy ra PS // Q'R' và PS = Q'R', vậy PSR'Q' là hình bình hành. Đây CHÍNH LÀ bước lập luận bắt buộc trước khi kết luận về giao điểm — không được bỏ qua. |
| 4 | Trả lời: "Vậy PR' và SQ' — là 2 đường chéo của tứ giác PSR'Q' vừa chứng minh — cắt nhau ở đâu?" (chọn: Tại trung điểm mỗi đường / Tại 1 điểm bất kỳ / Không cắt nhau) | Đáp án: Tại trung điểm mỗi đường — vì PSR'Q' là hình bình hành (đã chứng minh ở bước 3), mà 2 đường chéo của hình bình hành luôn cắt nhau tại trung điểm mỗi đường (tính chất đã học). |
| 5 | Lặp lại tương tự (rút gọn hơn, không lặp lại toàn bộ lập luận) cho cặp RP' và QS' | Tương tự bước 3-4 với tứ giác trung gian khác (VD PQR'S'), suy ra RP' và QS' cũng cắt nhau tại trung điểm. |
| 6 | Xem kết luận | Cả 4 đường chéo PR', QS', RP', SQ' đôi một cắt nhau tại trung điểm mỗi đường — mà 1 điểm chỉ có thể là trung điểm của 1 đoạn theo 1 cách duy nhất, nên cả 4 đường chéo cùng đi qua ĐÚNG 1 điểm chung O, và O là trung điểm của mỗi đường. |
| 7 **(mới thêm — phần tính toán)** | Biết đường chéo PR' = 10cm. Nhập giá trị khoảng cách từ O (giao điểm 4 đường chéo) đến đỉnh P, bấm Kiểm tra | Đáp án: OP = 5cm — vì O là trung điểm của PR' (đã chứng minh ở bước 4-6), nên OP = ½PR' = 5cm. Đây là ứng dụng số liệu thật của tính chất vừa chứng minh, không dừng lại ở mức lý luận suông. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể muốn bỏ qua bước 3 (lập luận trung gian) và
  trả lời thẳng bước 4 "nhìn hình thấy cắt tại trung điểm rồi" — đúng sai
  lầm số 3 đã xác định.
- Hệ thống phản hồi: Nút ở bước 4 chỉ sáng lên (đủ điều kiện bấm) sau khi
  bước 3 đã trả lời đúng — nếu học sinh cố tình click sớm, hiện: "Cần xác
  nhận PSR'Q' là hình bình hành trước — đây là lý do THỰC SỰ khiến 2 đường
  chéo cắt tại trung điểm, không phải vì 'nhìn thấy vậy'."
- Học sinh điều chỉnh: quay lại bước 3, tự lập luận qua các bước trung gian
  trước khi được phép kết luận.
- Kết quả rút ra: Kết quả hình học "trông đúng" luôn cần 1 chuỗi lập luận
  đứng sau, không được kết luận trực tiếp từ quan sát trực quan.
- Tình huống thêm (bước 7): Học sinh có thể nhập nhầm OP = 10cm (nhầm PR'
  với OP, quên chia đôi).
- Hệ thống phản hồi: "Bạn vừa nhập đúng bằng độ dài CẢ đường chéo PR', không
  phải khoảng cách từ trung điểm O đến P — thử chia đôi lại."
- Kết quả rút ra: Củng cố "trung điểm" là 1 khái niệm ĐỊNH LƯỢNG (chia đôi
  độ dài), không chỉ là vị trí định tính trên hình.

### Cấu hình 3D:
- Animation dựng dần từng đường chéo + tứ giác trung gian (tô màu
  `COLOR_PLANE_2` khi đang xét tứ giác PSR'Q').
- Camera: nhìn chéo để thấy rõ cả 4 đường chéo và giao điểm chung ở giữa.
- Cleanup: `clearScene()` khi sang Tab 3.

---

## TAB 3 — Đối chiếu: không phải lăng trụ tứ giác nào cũng là hình hộp

**Loại simulation:** H (click chọn) + trắc nghiệm Đúng/Sai + kéo thử (D3).
**Thời gian dự kiến:** ~3-4 phút (tăng từ 2-3 phút do thêm bước kéo thử).
**Khối nền:** 2 khối đặt song song để đối chiếu — (a) `hop_chu_nhat` (đáy
hình bình hành) và (b) lăng trụ tứ giác đáy hình thang (không phải hình
bình hành, dựng riêng vì `SOLID_LIBRARY` chưa có sẵn dạng lăng trụ đáy
thang).

### Sổ tay kiến thức (Có): "Hình hộp = lăng trụ tứ giác có đáy là hình bình
hành. Đáy không phải hình bình hành → không phải hình hộp, dù vẫn có thể là
1 lăng trụ tứ giác hợp lệ."

### Hướng dẫn mở đầu:
> "Bạn đang thấy 2 khối — cả 2 đều là lăng trụ tứ giác hợp lệ (đã thoả 2
> điều kiện lăng trụ học ở Module 13.5). Nhưng chỉ 1 trong 2 là hình hộp.
> Hãy click vào đáy mỗi khối để kiểm tra, rồi trả lời."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Click vào đáy khối (a) | Đáy khối (a) là hình bình hành (các cạnh đối song song và bằng nhau). |
| 2 | Trả lời: "Khối (a) có phải hình hộp không?" (Có/Không) | Đáp án: Có — vì đáy là hình bình hành, thoả đúng điều kiện riêng của hình hộp. |
| 3 | Click vào đáy khối (b) | Đáy khối (b) là hình thang (chỉ 1 cặp cạnh đối song song, không phải cả 2 cặp) — KHÔNG phải hình bình hành. |
| 4 | Trả lời: "Khối (b) có phải hình hộp không?" (Có/Không) | Đáp án: Không — dù khối (b) vẫn là 1 lăng trụ tứ giác hợp lệ (đủ 2 điều kiện lăng trụ), nhưng đáy không phải hình bình hành nên KHÔNG được gọi là hình hộp. |
| 5 **(mới thêm)** | "Bây giờ thử kéo đỉnh D của đáy khối (b) sao cho đáy trở thành hình bình hành — quan sát cả khối thay đổi theo real-time" | Trong lúc kéo, hiện thông tin sống: "Cạnh AD hiện dài [X], cạnh BC dài [Y]" và "AD có song song BC không: Có/Không" — học sinh tự canh cho tới khi cả 2 điều kiện (song song + bằng nhau) đều đạt. |
| 6 **(mới thêm)** | Khi đáy đã thành hình bình hành hợp lệ | "Bây giờ khối (b) đã trở thành 1 hình hộp thật sự — toàn bộ các mặt bên và cạnh bên tự động cập nhật theo vì chúng vẫn giữ nguyên hướng lăng trụ ban đầu, chỉ có đáy là thay đổi. Đây là minh chứng trực quan: chỉ cần sửa ĐÚNG 1 điều kiện (đáy) là đủ biến 1 lăng trụ tứ giác thành hình hộp." |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể trả lời "Có" cho cả khối (b) vì thấy nó
  "trông giống" khối (a) — đều có 2 đáy song song, các mặt bên là hình bình
  hành.
- Hệ thống phản hồi: "Khối (b) đúng là 1 lăng trụ tứ giác (thoả đủ điều
  kiện lăng trụ đã học), nhưng hình hộp có thêm 1 điều kiện RIÊNG: đáy phải
  là hình bình hành. Thử click lại vào đáy khối (b) và đếm xem có mấy cặp
  cạnh song song."
- Kết quả rút ra: "Lăng trụ tứ giác" và "hình hộp" không đồng nhất — hình
  hộp là tập con đặc biệt, cần kiểm tra thêm điều kiện đáy trước khi gọi tên.
- Tình huống thêm (bước 5-6, kéo thử): Học sinh có thể chỉ kéo D theo 1
  hướng (VD chỉ chỉnh cho AD//BC mà quên chỉnh độ dài bằng nhau), khiến đáy
  thành hình thang cân nhưng vẫn chưa phải hình bình hành.
- Hệ thống phản hồi: Chỉ báo "AD // BC: ✓" nhưng thiếu chỉ báo độ dài bằng
  nhau vẫn đỏ → hiện: "AD đã song song BC, nhưng độ dài 2 cạnh chưa bằng
  nhau — hình bình hành cần CẢ 2 điều kiện cùng lúc."
- Kết quả rút ra: Củng cố lại đúng định nghĩa hình bình hành (song song VÀ
  bằng nhau), không chỉ 1 trong 2, ngay trong bối cảnh trực quan của đáy hộp.

### Cấu hình 3D:
- Đối tượng kéo được (bước 5-6): đỉnh D của đáy khối (b), ràng buộc trong
  mặt phẳng đáy (2D, không đổi độ cao) — kỹ thuật kéo điểm ràng buộc trên
  mặt phẳng đã verify.
- Cleanup: `clearScene()` khi sang Tab 4.

---

## TAB 4 — Thử thách: Tự dựng 1 hình hộp

**Loại simulation:** D3 (kéo điểm ràng buộc trên mặt phẳng ngang, snap
lưới — kỹ thuật đã áp dụng ở Module 13.5).
**Thời gian dự kiến:** ~4-5 phút.

### Sổ tay kiến thức (Có, dạng checklist tự kiểm tra — 3 điều kiện, nhiều
hơn Module 13.5 vì hình hộp có thêm điều kiện riêng):
- ✓ Đáy phải là hình bình hành (điều kiện RIÊNG của hình hộp)
- ✓ Các mặt bên phải là hình bình hành (điều kiện lăng trụ)
- ✓ Các cạnh bên phải song song VÀ bằng nhau (điều kiện lăng trụ)

### Thiết kế chống "dò mù" (áp dụng lại cơ chế đã verify ở Module 13.5):
- Chia 2 giai đoạn: GĐ1 (bắt buộc) — chỉ đỉnh D' tự do, A', B', C' đặt sẵn
  đúng vị trí. GĐ2 (mở rộng, không bắt buộc) — cả 4 đỉnh trên tự do.
- Snap lưới 0.25 đơn vị — loại bỏ vấn đề dung sai/sai số dấu phẩy động.
- Số liệu trực quan sống — hiện độ dài cạnh bên và chỉ số lệch hướng.
- Chống bí: sau 90 giây không tiến triển hoặc 5 lần thử sai liên tiếp, hiện
  gợi ý cụ thể theo đúng chỉ báo còn thiếu.
- **Khác biệt so với Module 13.5:** đáy ABCD ở đây KHÔNG cố định là hình
  bình hành ngay từ đầu — đáy được đặt sẵn ĐÚNG là hình bình hành (vì việc
  kéo đáy tự do sẽ vượt phạm vi module này, đáy chuẩn được giữ cố định để
  tập trung đúng vào 3 điều kiện phía trên). Điểm mới so với 13.5 là chỉ báo
  thứ 3 ("Đáy là hình bình hành: ✓" — luôn xanh sẵn vì đáy cố định đúng,
  nhưng vẫn hiển thị để nhắc lại điều kiện, không lược bỏ).

### Hướng dẫn mở đầu:
> "Đáy ABCD đã cố định — bạn kiểm tra thấy đây là hình bình hành (chỉ báo
> đầu tiên đã xanh sẵn). Bên trên có điểm D' — hiện đang đặt SAI vị trí
> (A', B', C' đã đúng sẵn). Nhiệm vụ: kéo D' sao cho ABCD.A'B'C'D' trở
> thành 1 hình hộp thật sự — dựa đúng 3 điều kiện ở Sổ tay bên trên."

### Học sinh tương tác bằng cách:

| Giai đoạn | Hướng dẫn thao tác cụ thể | Phản hồi real-time (luôn kèm giải thích) |
|---|---|---|
| GĐ1 — Làm quen | Thử kéo D' bất kỳ hướng, điểm tự snap vào ô lưới gần nhất khi thả tay | "Bạn đang di chuyển D' trong mặt phẳng ngang — quan sát độ dài DD' và chỉ báo bên dưới thay đổi theo" |
| GĐ1 — Điều chỉnh | Kéo D' cho tới khi CẢ 3 chỉ báo đều xanh | Nếu "Mặt bên: ✓" nhưng "Cạnh bên: ✗": "Mặt bên đã đúng hình bình hành, nhưng độ dài DD' = [X] chưa bằng AA' = [Y] — thử kéo D' lên/xuống để khớp độ cao" |
| GĐ1 — Hoàn thành | Tự động khoá khi cả 3 chỉ báo đều ✓ | "Chúc mừng — bạn đã dựng được 1 hình hộp hợp lệ! Ba điều kiện: đáy là hình bình hành, mặt bên là hình bình hành, cạnh bên song song-bằng nhau — thiếu 1 trong 3 đều không phải hình hộp." |
| GĐ2 — Mở rộng (không bắt buộc) | Thử thách thêm: cả 4 đỉnh trên (A', B', C', D') đều tự do và bị xáo vị trí lại | Cùng cơ chế phản hồi như GĐ1, nhưng cả 4 điểm cùng lúc |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể kéo D' đạt đúng độ cao (điều kiện cạnh bên)
  nhưng lệch ngang khỏi vị trí đúng (khiến mặt bên ADD'A' hoặc DCC'D'
  không còn là hình bình hành).
- Hệ thống phản hồi: Chỉ báo "Cạnh bên: ✓" nhưng "Mặt bên: ✗" → hiện: "Cạnh
  bên đã đúng độ dài, nhưng mặt bên chưa phải hình bình hành — thử đối
  chiếu vị trí D' có giữ đúng hướng song song với AA', BB', CC' hay không."
- Kết quả rút ra: Củng cố rằng hình hộp cần đồng thời cả 3 điều kiện, không
  chỉ riêng độ dài cạnh bên.

### Cấu hình 3D:
- Đối tượng kéo được: GĐ1 — điểm D' (A', B', C' cố định); GĐ2 — cả 4 điểm
  A', B', C', D'.
- Ràng buộc: trong 1 mặt phẳng ngang, độ cao chỉnh qua slider riêng, snap
  lưới 0.25 đơn vị.
- Vị trí khởi tạo: D' lệch khỏi vị trí đúng.
- Tính toán real-time: kiểm tra (1) đáy là hình bình hành (cố định đúng
  sẵn), (2) mặt bên có phải hình bình hành, (3) cạnh bên cùng vector chỉ
  phương và độ dài — so sánh bằng số nguyên lưới, không cần dung sai dấu
  phẩy động.
- Cleanup: `clearScene()` khi rời Tab 4 (kết thúc module).

---

## 🎯 TỔNG KẾT CUỐI MODULE 13.6

**Tổng kết kiến thức:**
- Hình hộp là lăng trụ tứ giác có đáy là hình bình hành — đây là điều kiện
  RIÊNG, thêm vào 2 điều kiện chung của lăng trụ (mặt bên là hình bình hành,
  cạnh bên song song-bằng nhau).
- Hình hộp có 4 đường chéo, cùng đi qua 1 điểm chung, và điểm đó là trung
  điểm của mỗi đường chéo — chứng minh dựa trên tính chất đường chéo hình
  bình hành cắt nhau tại trung điểm, áp dụng qua các tứ giác trung gian.
- Đường chéo hình hộp (xuyên qua khối) khác đường chéo mặt (nằm trên 1 mặt)
  — 2 khái niệm không được nhầm lẫn.

**Tổng kết sai lầm:**
1. Nhầm mọi lăng trụ tứ giác là hình hộp — dấu hiệu: gọi tên "hình hộp" mà
   chưa kiểm tra đáy có phải hình bình hành.
2. Nhầm đường chéo khối với đường chéo mặt — dấu hiệu: chọn nhầm 1 đường
   nằm trên mặt khi được hỏi về đường chéo của khối.
3. Bỏ qua bước lập luận trung gian — dấu hiệu: kết luận "cắt tại trung
   điểm" ngay mà không chứng minh tứ giác trung gian là hình bình hành trước.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

📝 **Cập nhật rà soát bản quyền (sau khi review toàn bộ Bài 12-13):** Tab 2
ban đầu dùng nguyên ký hiệu ABCD.A'B'C'D' + đúng 4 đường chéo AC', BD', CA',
DB' + đúng yêu cầu "chứng minh cùng qua trung điểm" — gần như bản sao Ví dụ
6 SGK dù đã thêm bước tương tác. Đã đổi ký hiệu đỉnh thành PQRS.P'Q'R'S' và
thêm hẳn 1 bước TÍNH TOÁN số liệu cụ thể (khoảng cách OP = ½PR' khi biết
PR'=10cm) — không chỉ dừng ở mức chứng minh tồn tại như bản gốc, biến nội
dung buộc phải dạy (tính chất 4 đường chéo) thành 1 sản phẩm khác về hình
thức thể hiện.

⚠️ **Rủi ro 1 (đã xác nhận, cần thực hiện khi build):** Tab 3 cần dựng riêng
1 khối lăng trụ tứ giác đáy hình thang (không có sẵn trong `SOLID_LIBRARY`)
— bắt buộc verify bằng script Node độc lập trước khi build để đảm bảo khối
này vẫn thoả đúng 2 điều kiện lăng trụ (mặt bên hình bình hành, cạnh bên
song song-bằng nhau) trong khi đáy KHÔNG phải hình bình hành.

⚠️ **Rủi ro 2 (đã xác nhận giữ nguyên):** Tab 4 — đáy ABCD cố định đúng sẵn
khiến GĐ1 dễ hơn tương đối so với Tab 4 của Module 13.5. Đã xác nhận giữ
nguyên như vậy vì đây là bài thực hành giúp học sinh nắm khái niệm, không
cần tăng độ khó — GĐ2 (mở rộng) vẫn đủ cho học sinh muốn thử thách thêm.

📖 **Kiểm tra caption:** Đã rà toàn bộ 4 tab — mọi bước tương tác đều có
giải thích kiến thức đi kèm, không có bước nào chỉ báo Đúng/Sai trơn, bao
gồm cả 2 bước mới thêm ở Tab 3 (kéo thử).

---

**Kịch bản đã sẵn sàng! Các bước tiếp theo:**
- ✅ Duyệt — chuyển sang Giai đoạn 2 (Thiết kế giao diện chi tiết), sau đó
  tiếp tục Bước 0 cho Module 13.7 (bài tập tổng hợp — nhớ thêm nội dung
  lăng trụ xiên đã ghi chú từ Module 13.5)
- ✏️ Chỉnh — nêu rõ phần nào cần thay đổi

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 11/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`,
> `01_scenario_builder_3d_addendum.md`, `04_design_toan_3d.md`,
> `05_threejs_engine.md`, `06_geometry_math.md`, đối chiếu với
> `solid_library.html` (Kho Khối Hình Không Gian — Nhánh B) và
> Module 13.5 (mirror cấu trúc 4 tab)
