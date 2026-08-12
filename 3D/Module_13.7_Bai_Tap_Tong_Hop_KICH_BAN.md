# 📋 KỊCH BẢN SIMULATION — MODULE 13.7
## Bài tập tổng hợp hai mặt phẳng song song

**Bài SGK:** Bài 13 — Hai mặt phẳng song song (SGK Kết nối tri thức)
**Vị trí trong phân phối chương trình:** Module 13.7 — module cuối cùng của
Bài 13, nối tiếp 13.1-13.6. Tương ứng phần BÀI TẬP (4.21-4.28, trang 93-94).
**Trạng thái kiến thức nền:** Tổng kết — đã dạy đủ 13.1-13.6 (định
nghĩa/tính chất 2 mp song song, Thalès không gian, lăng trụ, hình hộp). Sổ
tay kiến thức tổng hợp hiện xuyên suốt cả 6 tab, không dạy khái niệm mới.
**Nguồn SGK tham chiếu:** bài 4.21, 4.22, 4.23, 4.25, 4.26, 4.27, 4.28
(trang 93-94) + nội dung lăng trụ xiên hoãn từ Module 13.5 — **toàn bộ số
liệu, cấu hình đối tượng, và dạng câu hỏi đã đổi khác SGK gốc** (xem ghi chú
bản quyền ở mỗi tab và ở Critical Review).
**Tài nguyên tái dùng:** `SOLID_LIBRARY.lang_tru_tu_dung`,
`lang_tru_luc_giac_deu`, `lang_tru_tam_vuong`, `hop_chu_nhat`,
`lang_tru_tam_xien`, `lang_tru_tu_xien` từ Kho Khối Hình Không Gian.

---

## 🎯 MỤC TIÊU

- HIỂU: tổng hợp lại toàn bộ kiến thức Bài 13 trong các tình huống bài tập
  đa dạng — không giới hạn 1 dạng bài như các module trước.
- LÀM ĐƯỢC:
  - Nhận định đúng/sai các mệnh đề tổng quát về quan hệ giữa các mặt phẳng
  - Chứng minh 1 mặt phẳng song song với mặt phẳng khác dựa trên tỉ lệ/đường
    trung gian trong bối cảnh lăng trụ
  - Chứng minh 1 hình tạo bởi mặt cắt là lăng trụ/hình hộp, tính thêm tỉ lệ
    số liệu liên quan
  - Liên hệ thực tế + nhận biết lăng trụ xiên vẫn là lăng trụ hợp lệ

## ⚠️ SAI LẦM CẦN GIẢI QUYẾT

| Sai lầm | Nguyên nhân | Dấu hiệu nhận ra |
|---|---|---|
| Áp dụng "song song" bắc cầu sai | Không kiểm tra kỹ điều kiện đề cho trước khi suy diễn (VD 2 mặt phẳng cùng song song 1 đường thẳng chưa chắc song song nhau) | Kết luận song song chỉ dựa vào "cùng song song với 1 thứ 3" mà không xét khả năng cắt nhau |
| Nhầm giữa "trọng tâm" và "trung điểm" | Áp nhầm tính chất của điểm này cho điểm kia khi dựng điểm liên quan đến lăng trụ | Lập luận sai khi tính vị trí/tính chất của đoạn nối 2 trọng tâm |
| Cho rằng mọi lăng trụ đều phải "đứng" | Quên rằng lăng trụ xiên vẫn hợp lệ nếu thoả đúng 2 điều kiện đã học | Loại bỏ 1 hình lăng trụ hợp lệ chỉ vì "trông nghiêng, lạ mắt" |

## 🧊 ĐẶC THÙ 3D

- **Khối nền:** đa dạng theo từng tab (khác các module trước chỉ dùng 1-2
  khối) — chi tiết theo từng tab bên dưới.
- **Góc camera mặc định:** `setCameraStandardSGK()` làm mặc định chung, đổi
  theo từng bài khi cần.
- **Mức độ tương tác:** đa dạng — I (MCQ), F (dựng dần), D3 (click chọn).
- **Dạy từ đầu hay tổng kết:** tổng kết — Sổ tay kiến thức tổng hợp (gồm cả
  4 mảng: song song mp / Thalès / lăng trụ / hình hộp) hiện xuyên suốt.
- **Thời lượng tổng dự kiến:** ~18-22 phút (dài hơn các module trước vì đủ
  6 tab, không giới hạn chặt theo yêu cầu của bạn).
- **Nguyên tắc bắt buộc xuyên suốt:** sau MỌI bước tương tác đều có giải
  thích kiến thức đi kèm, không để trống hay chỉ báo "Đúng/Sai" trơn.
- **Quan hệ giữa 6 tab:** độc lập nhưng khuyến khích thứ tự 1→6; Tab 4 nên
  học sau Tab 2 để đối chiếu trọng tâm/trung điểm hiệu quả nhất.

---

## TAB 1 — Nhận định đúng/sai

**Loại simulation:** I (MCQ có minh hoạ 3D, 3 mặt phẳng (P), (Q), (R)).
**Thời gian dự kiến:** ~3-4 phút.
**Giải quyết sai lầm:** áp dụng song song bắc cầu sai.

> 📝 **Ghi chú bản quyền:** 4 mệnh đề dưới đây viết HOÀN TOÀN MỚI, không
> dùng lại nội dung a/b/c/d của bài 4.21 — chỉ giữ chung dạng thức "nhận
> định đúng/sai về quan hệ mặt phẳng" và cùng nhắm đúng bẫy suy diễn song
> song bắc cầu.

### Sổ tay kiến thức (Có, tổng hợp — hiện xuyên suốt module):
- Điều kiện đủ để (P)//(Q): (P) chứa 2 đường thẳng cắt nhau, cả 2 đều song
  song (Q).
- Nếu (R) cắt (P) và (P)//(Q) thì (R) cũng cắt (Q).
- 2 mặt phẳng cùng song song với 1 đường thẳng KHÔNG chắc chắn song song
  nhau (có thể cắt nhau theo giao tuyến song song đường đó).

### Hướng dẫn mở đầu:
> "Bạn sẽ xem lần lượt 4 mệnh đề, mỗi mệnh đề có 1 hình minh hoạ 3D riêng.
> Đọc kỹ, xoay hình để kiểm chứng trước khi trả lời Đúng/Sai."

### 4 mệnh đề (đáp án Đúng/Sai không theo thứ tự cố định, minh hoạ đổi theo từng câu):

**Mệnh đề 1:** "Nếu mặt phẳng (P) chứa 2 đường thẳng cắt nhau, cả hai đều
song song với mặt phẳng (Q), thì (P) // (Q)."
- Đáp án: **Đúng**. `giai_thich_dung`: Đây chính là điều kiện đủ đã học ở
  Module 13.1 — 2 đường cắt nhau cùng song song (Q) là đủ để kết luận (P)//(Q).
- `goi_y_khi_sai`: Nhớ lại điều kiện đủ để 2 mặt phẳng song song — cần bao
  nhiêu đường thẳng, và chúng cần quan hệ gì với nhau?

**Mệnh đề 2:** "Nếu (P) // (Q) thì 2 đường thẳng bất kỳ, lần lượt nằm trong
(P) và (Q), luôn song song với nhau."
- Đáp án: **Sai**. `giai_thich_dung`: 2 đường thẳng nằm trong 2 mặt phẳng
  song song có thể song song HOẶC chéo nhau (không đồng phẳng) — chúng
  không bao giờ CẮT NHAU (vì (P), (Q) không có điểm chung), nhưng "không cắt
  nhau" không có nghĩa là "song song".
- `goi_y_khi_sai`: Thử xoay hình và chọn 2 đường bất kỳ trên 2 mặt phẳng
  song song — chúng có luôn cùng hướng không, hay có thể lệch hướng nhau?

**Mệnh đề 3:** "Nếu 2 mặt phẳng phân biệt cùng song song với 1 đường thẳng
d thì 2 mặt phẳng đó song song với nhau."
- Đáp án: **Sai**. `giai_thich_dung`: 2 mặt phẳng cùng song song với d vẫn
  có thể CẮT NHAU — khi đó giao tuyến của chúng sẽ song song với d. Đây
  chính là bẫy suy diễn bắc cầu sai lầm phổ biến nhất.
- `goi_y_khi_sai`: Hãy hình dung 2 trang sách đang mở — cả 2 đều song song
  với gáy sách (đường thẳng d), nhưng 2 trang có song song nhau không?

**Mệnh đề 4:** "Nếu mặt phẳng (R) cắt mặt phẳng (P), và (P) // (Q), thì (R)
cũng phải cắt (Q)."
- Đáp án: **Đúng**. `giai_thich_dung`: Đây là tính chất đã học ở Module
  13.2 — nếu 1 mặt phẳng cắt 1 trong 2 mặt phẳng song song thì nó cũng cắt
  mặt phẳng còn lại (không thể song song với cả 2 mà chỉ cắt 1).
- `goi_y_khi_sai`: Nếu (R) song song với (Q) mà (P) cũng song song (Q), thì
  (R) và (P) có quan hệ gì? Điều đó có mâu thuẫn với việc (R) cắt (P) không?

### Quy tắc áp dụng: vị trí Đúng/Sai của 4 mệnh đề được xáo trộn thực sự khi
build (không phải luôn 2 đúng đứng trước 2 sai theo đúng thứ tự liệt kê ở
trên).

### Cấu hình 3D: mỗi mệnh đề có 1 minh hoạ riêng (3 mặt phẳng phối cảnh
khác nhau), `clearScene()` giữa các câu. Cleanup cuối: khi sang Tab 2.

---

## TAB 2 — Chứng minh song song qua tỉ lệ/đường trung gian

**Loại simulation:** F (dựng dần) — 2 case.
**Thời gian dự kiến:** ~4-5 phút.

> 📝 **Ghi chú bản quyền:** Case A đổi từ lăng trụ TAM GIÁC + trung điểm
> (4.22 gốc) sang lăng trụ TỨ GIÁC + tỉ lệ ⅓ (không phải trung điểm). Case B
> đổi từ hình THANG + cặp điểm A,D (4.23 gốc) sang hình BÌNH HÀNH + cặp
> điểm B,C — khác cả loại tứ giác và cặp điểm được chọn.

### Case A — Lăng trụ tứ giác, mặt phẳng qua 4 điểm tỉ lệ ⅓ trên cạnh bên
**Đề bài:** Cho lăng trụ tứ giác ABCD.A'B'C'D'. Gọi M, N, P, Q lần lượt là
các điểm trên AA', BB', CC', DD' sao cho AM = ⅓AA' (M, N, P, Q đều chia
theo đúng tỉ lệ ⅓ tính từ đáy dưới). Chứng minh mặt phẳng (MNPQ) song song
với mặt đáy (ABCD).

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát 4 điểm M, N, P, Q đã đặt sẵn theo đúng tỉ lệ ⅓ trên 4 cạnh bên | Cả 4 điểm cùng chia cạnh bên theo đúng 1 tỉ lệ — đây là dấu hiệu để nghĩ tới quan hệ song song với đáy. |
| 2 | Trả lời: "MN có song song với AB không?" (Có/Không) | Đúng (Có) — vì AA'//BB' (cạnh bên lăng trụ) và AM/AA' = BN/BB' = ⅓ (cùng tỉ lệ), nên theo định lí Talet trong mặt phẳng (ABB'A'), MN // AB. |
| 3 | Trả lời: "NP có song song với BC không?" (Có/Không) | Tương tự bước 2, áp dụng trên mặt phẳng (BCC'B'): NP // BC. |
| 4 | Xem kết luận | Vì MN//AB và NP//BC là 2 đường cắt nhau tại N, cả 2 đều song song mặt phẳng (ABCD) (do song song 1 đường nằm trong đó), nên theo điều kiện đủ (Module 13.1), mặt phẳng (MNPQ) song song (ABCD). |

### Case B — Hình bình hành, mặt phẳng qua cặp điểm B, C
**Đề bài:** Cho hình bình hành ABCD. Qua B và C lần lượt vẽ 2 đường thẳng
p, q song song với nhau và không nằm trong mặt phẳng (ABCD). Chứng minh
mp(A, p) song song với mp(D, q).

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát p qua B, q qua C, đã dựng sẵn song song nhau | p // q theo đúng giả thiết đề bài. |
| 2 | Trả lời: "AB có song song với DC không?" (Có/Không) | Đúng (Có) — vì ABCD là hình bình hành, AB // DC (và AB = DC). |
| 3 | Xem mp(A,p) được dựng (chứa A và đường thẳng p) | mp(A,p) chứa 2 đường thẳng cắt nhau: AB và p (p qua B, cắt AB tại B). |
| 4 | Xem kết luận | mp(A,p) chứa AB và p; mp(D,q) chứa DC và q. Vì AB//DC và p//q — 2 cặp đường cắt nhau tương ứng đều song song — nên theo điều kiện đủ, mp(A,p) // mp(D,q). |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Ở Case A, học sinh có thể chỉ kiểm tra 1 cặp đường (VD chỉ
  MN//AB) rồi vội kết luận (MNPQ)//(ABCD) — thiếu đường cắt nhau thứ 2.
- Hệ thống phản hồi: Nút "Xem kết luận" chỉ sáng khi cả bước 2 VÀ bước 3 đã
  trả lời đúng — nếu bấm sớm, hiện: "Cần ít nhất 2 đường CẮT NHAU cùng song
  song mặt phẳng kia — chỉ 1 đường là chưa đủ điều kiện."
- Kết quả rút ra: Củng cố lại đúng điều kiện đủ đã học — không phải "1 đường
  song song là đủ" mà cần 2 đường cắt nhau.

### Cấu hình 3D: Case A dùng `lang_tru_tu_dung`; Case B dựng riêng hình bình
hành + 2 đường thẳng phụ. Cleanup: `clearScene()` giữa Case A/B và khi sang Tab 3.

---

## TAB 3 — Thiết diện lăng trụ lục giác đều

**Loại simulation:** F (dựng dần thiết diện, checklist đủ mặt).
**Thời gian dự kiến:** ~3-4 phút.
**Khối nền:** `lang_tru_luc_giac_deu`.

> 📝 **Ghi chú bản quyền:** Đổi từ lăng trụ TỨ GIÁC (4.25 gốc) sang lăng
> trụ LỤC GIÁC ĐỀU — khác hẳn số cạnh, mở rộng khái niệm sang đa giác phức
> tạp hơn, không chỉ đổi số liệu.

### Sổ tay kiến thức (Có): "Mặt phẳng cắt song song đáy của lăng trụ →
giao tuyến với mỗi mặt bên song song cạnh đáy tương ứng → thiết diện luôn
là 1 đa giác ĐỒNG DẠNG với đáy (cùng số cạnh, các cạnh tương ứng song song)."

### Hướng dẫn mở đầu:
> "Lăng trụ lục giác đều ABCDEF.A'B'C'D'E'F' bị cắt bởi 1 mặt phẳng song
> song đáy, ở vị trí giữa 2 đáy. Bạn dựng lần lượt từng cạnh thiết diện —
> nhớ kiểm tra ĐỦ cả 6 mặt bên, không dừng sớm."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1-6 | Bấm "Dựng cạnh [N]" lần lượt cho từng mặt bên (checklist 6 mục `.done`) | Mỗi giao tuyến song song đúng 1 cạnh đáy tương ứng — vì mặt cắt song song đáy nên cắt mỗi mặt bên theo 1 đường song song cạnh đáy của mặt đó. |
| 7 | Bấm "Kết luận" (chỉ sáng khi đủ 6/6) | Thiết diện là 1 lục giác đều, đồng dạng với đáy — đây là hệ quả trực tiếp của việc mặt cắt song song đáy, áp dụng y hệt nguyên tắc đã học dù đáy có bao nhiêu cạnh. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh dừng lại sau khi dựng 4-5/6 cạnh, tưởng "đã đủ hình"
  (đúng sai lầm "thiết diện thiếu mặt" đã học từ Module 12.3).
- Hệ thống phản hồi: Nút "Kết luận" không sáng cho tới khi đủ 6/6 — hiện
  "Thiết diện chưa khép kín, còn mặt bên nào chưa được kiểm tra?"
- Kết quả rút ra: Củng cố lại nguyên tắc rà đủ TẤT CẢ các mặt, áp dụng được
  cho bất kỳ đa giác đáy nào, không riêng tứ giác.

### Cấu hình 3D: Cleanup: `clearScene()` khi sang Tab 4.

---

## TAB 4 — Trọng tâm và lăng trụ

**Loại simulation:** D3 (click chọn) + câu hỏi mở.
**Thời gian dự kiến:** ~3-4 phút.
**Khối nền:** `lang_tru_tam_vuong` (lăng trụ đứng, đáy tam giác vuông).
**Giải quyết sai lầm:** nhầm trọng tâm với trung điểm.

> 📝 **Ghi chú bản quyền:** Đổi từ lăng trụ tam giác ĐỀU (4.26 gốc dùng
> hình chữ, không nêu rõ nhưng theo hình minh hoạ SGK là tam giác thường)
> sang lăng trụ đáy tam giác VUÔNG; đổi từ 2 yêu cầu chứng minh ĐÓNG (a, b)
> sang 1 câu hỏi MỞ, không rập khuôn cấu trúc chứng minh 2 bước của SGK.

### Sổ tay kiến thức (Có): "Lăng trụ là kết quả của phép tịnh tiến đáy dưới
theo đúng vector cạnh bên — MỌI điểm trên đáy dưới (kể cả trọng tâm) đều
tịnh tiến thành điểm tương ứng ở đáy trên theo đúng vector đó, không chỉ
riêng các đỉnh."

### Hướng dẫn mở đầu:
> "G là trọng tâm tam giác đáy dưới ABC, G' là trọng tâm tam giác đáy trên
> A'B'C'. Khác với Tab 2 (dùng trung điểm), ở đây ta xét TRỌNG TÂM — hãy tự
> trả lời câu hỏi mở bên dưới, không có sẵn đáp án đóng khung."

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Click chọn G (trọng tâm đáy dưới) và G' (trọng tâm đáy trên) trên hình | G, G' được xác định là giao 3 đường trung tuyến của mỗi tam giác đáy — khác hẳn cách xác định trung điểm (chỉ cần 1 cạnh). |
| 2 | Trả lời câu hỏi mở: "Đoạn GG' có song song với cạnh bên AA' không? Độ dài GG' so với AA' như thế nào?" (nhập nhận xét dạng chọn 2 ý: Có/Không song song + Bằng nhau/Khác nhau) | Đáp án: GG' // AA' VÀ GG' = AA'. Vì lăng trụ là phép tịnh tiến đáy ABC thành đáy A'B'C' theo đúng vector $\vec{AA'}$, mà phép tịnh tiến biến trọng tâm tam giác thành trọng tâm tam giác ảnh, nên G tịnh tiến thành G' theo ĐÚNG vector đó — tức $\vec{GG'} = \vec{AA'}$, suy ra song song và bằng nhau. |
| 3 | Xem kết luận mở rộng | Tính chất này ĐÚNG với BẤT KỲ điểm tương ứng nào giữa 2 đáy (trọng tâm, trực tâm, hay bất kỳ điểm nào xác định theo cùng 1 quy tắc trên cả 2 tam giác) — không phải vì "trọng tâm có gì đặc biệt", mà vì bản chất lăng trụ là phép tịnh tiến. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Học sinh có thể áp nhầm công thức "đoạn nối 2 trung điểm thì
  bằng nửa..." (tính chất trung điểm ở Tab 2) sang cho trọng tâm — nghĩ GG'
  có độ dài bằng 1 phần nào đó của AA' thay vì bằng nguyên vẹn.
- Hệ thống phản hồi: "Bạn đang áp dụng tính chất của TRUNG ĐIỂM (chia đôi)
  cho TRỌNG TÂM — đây là 2 khái niệm khác nhau. Thử nghĩ lại: lăng trụ là
  phép TỊNH TIẾN, không phải phép chia tỉ lệ — mọi điểm tương ứng đều dịch
  chuyển theo ĐÚNG 1 vector duy nhất."
- Kết quả rút ra: Phân biệt rõ 2 khái niệm và hiểu đúng bản chất "lăng trụ =
  tịnh tiến" thay vì nhớ máy móc từng công thức riêng lẻ cho từng loại điểm.

### Cấu hình 3D: Camera xoay để thấy rõ 2 tam giác đáy và vị trí trọng tâm
mỗi tam giác. Cleanup: `clearScene()` khi sang Tab 5.

---

## TAB 5 — Thiết diện hình hộp + tỉ lệ diện tích đáy

**Loại simulation:** F (dựng dần) + tính toán.
**Thời gian dự kiến:** ~4-5 phút.
**Khối nền:** `hop_chu_nhat`.

> 📝 **Ghi chú bản quyền:** Đổi mặt cắt song song mặt bên KHÁC (ADD'A' thay
> vì ABB'A' như 4.27 gốc), và đổi yêu cầu: không chỉ "chứng minh là hình
> hộp" như 4.27, mà THÊM tính tỉ lệ diện tích đáy — kết hợp lại góc nhìn
> Thalès (Module 13.4), không lặp y hệt yêu cầu chứng minh thuần tuý của
> bản gốc. (Dừng ở diện tích, không tính thể tích khối — nội dung thể tích
> chưa được dạy trong phạm vi Bài 13.)

### Đề bài: Cho hình hộp ABCD.A'B'C'D'. Lấy M trên AB sao cho AM = ⅓AB. Mặt
phẳng (α) qua M, song song với mặt bên (ADD'A'), cắt BC tại N, cắt A'B' tại
M', cắt B'C' tại N'.

### Học sinh tương tác bằng cách:

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát M trên AB (AM=⅓AB) đã đặt sẵn, bấm "Dựng mặt cắt" | Mặt phẳng (α) song song (ADD'A') sẽ cắt các cạnh còn lại theo đúng tỉ lệ tương ứng (Thalès không gian, 3 mặt phẳng (ADD'A'), (α), (BCC'B') đôi một song song). |
| 2 | Trả lời: "N trên BC được xác định thế nào — BN bằng bao nhiêu phần BC?" (chọn ⅓ / ½ / ⅔) | Đáp án: ⅓ — vì (α) song song (ADD'A') và (BCC'B'), áp dụng đúng tỉ lệ AM/AB = BN/BC = ⅓ theo Thalès không gian. |
| 3 | Xem hình AMND.A'M'N'D' được tô sáng — trả lời: "Đây có phải 1 hình hộp con hợp lệ không?" (Có/Không) | Đúng (Có) — vì đáy AMND là hình bình hành (do AM//DN, cùng tỉ lệ ⅓ trên 2 cạnh tương ứng của hình bình hành ABCD gốc) và các cạnh bên vẫn song song-bằng nhau (kế thừa từ hình hộp gốc). |
| 4 | Nhập số: "Nếu diện tích đáy ABCD là 36cm², diện tích đáy AMND là bao nhiêu?" | Đáp án: 12cm² — vì đáy AMND có 1 chiều bằng AM = ⅓AB (chiều còn lại AD giữ nguyên), nên diện tích tỉ lệ đúng theo tỉ lệ đó: 36×⅓=12cm² (không bình phương vì chỉ 1 chiều thay đổi, không đồng dạng toàn phần). |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Ở bước 4, học sinh có thể tính sai bằng cách bình phương tỉ
  lệ (nhầm với trường hợp đồng dạng toàn phần 2 chiều, nghĩ diện tích tỉ lệ
  (⅓)² như các bài toán đồng dạng hình phẳng thu nhỏ đều đã gặp).
- Hệ thống phản hồi: "Ở đây chỉ 1 CHIỀU của đáy thay đổi (từ AB thành AM),
  chiều còn lại (AD) giữ nguyên — không phải thu nhỏ đều theo cả 2 chiều,
  nên không bình phương tỉ lệ."
- Kết quả rút ra: Phân biệt trường hợp "thu nhỏ đều theo mọi chiều" (tỉ lệ
  diện tích = bình phương tỉ lệ dài) với trường hợp "chỉ 1 chiều thay đổi"
  (tỉ lệ diện tích = đúng tỉ lệ đó, không luỹ thừa).

### Cấu hình 3D: Cleanup: `clearScene()` khi sang Tab 6.

---

## TAB 6 — Thực tế + Lăng trụ xiên

**Loại simulation:** I (MCQ) — 2 phần.
**Thời gian dự kiến:** ~3-4 phút.

> 📝 **Ghi chú bản quyền:** Phần A đổi bối cảnh "cầu thang xương cá" (4.28
> gốc) sang "kệ sách bậc thang". Phần B là nội dung MỚI (lăng trụ xiên) đã
> hoãn từ Module 13.5, không có trong SGK gốc.

### Phần A — Kệ sách bậc thang
**Tình huống:** Một kệ sách có dạng bậc thang, mỗi bậc là 1 tấm ván nằm
ngang. Mép trước của mỗi bậc ván đều song song với bức tường phía sau (mặt
phẳng cố định).

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát mô hình 3D kệ sách bậc thang | Mỗi bậc ván là 1 đoạn thẳng nằm ngang, mép trước song song bức tường. |
| 2 | Trả lời: "Vì sao mép các bậc ván luôn song song nhau dù độ cao khác nhau?" (chọn: Vì cùng song song 1 mặt phẳng cố định / Vì được đo bằng thước / Vì tình cờ) | Đáp án: Vì cùng song song 1 mặt phẳng cố định — mỗi mép ván song song với mặt tường phía sau (và với mặt sàn), mà các đường thẳng cùng song song với 1 mặt phẳng và nằm trên các mặt phẳng ngang song song nhau thì đôi một song song. |

### Phần B — Lăng trụ xiên vẫn hợp lệ
**Nội dung (chuyển từ Module 13.5):**

| Bước | Hướng dẫn thao tác | Sau khi thao tác — giải thích kiến thức |
|---|---|---|
| 1 | Quan sát 2 hình: (a) lăng trụ tam giác ĐỨNG (`lang_tru_tam_dung`), (b) lăng trụ tam giác XIÊN (`lang_tru_tam_xien`, cạnh bên không vuông góc đáy) | Cả 2 đều có 2 đáy song song, bằng nhau. |
| 2 | Trả lời: "Hình (b) có phải là 1 lăng trụ hợp lệ không?" (Có/Không) | Đáp án: Có — định nghĩa lăng trụ KHÔNG yêu cầu cạnh bên vuông góc đáy, chỉ cần các cạnh bên song song và bằng nhau (đã học Module 13.5). "Lăng trụ đứng" chỉ là 1 trường hợp riêng. |
| 3 | Click vào cạnh bên của hình (b) để xem số đo — xác nhận các cạnh bên vẫn song song và bằng nhau dù nhìn "nghiêng" | Số đo xác nhận: độ dài các cạnh bên bằng nhau, góc giữa các cạnh bên = 0° (song song) — đúng đủ 2 điều kiện lăng trụ dù hình dạng tổng thể trông khác lăng trụ đứng quen thuộc. |

### Kịch bản dẫn dắt học sinh gặp sai lầm và tự sửa:
- Tình huống: Ở Phần B bước 2, học sinh dễ trả lời "Không" vì hình (b)
  "trông lạ" so với các lăng trụ đứng đã quen ở các module trước.
- Hệ thống phản hồi: Không phán xét ngay — cho phép click lại vào cạnh bên
  (bước 3) để xem số đo cụ thể trước khi trả lời lại.
- Kết quả rút ra: Hình "trông lạ" không đồng nghĩa "không hợp lệ" — luôn
  quay về đúng 2 điều kiện định nghĩa để kết luận, không dựa vào cảm giác
  thị giác (đúng nguyên tắc đã học ở Module 13.5 Tab 3).

### Cấu hình 3D: Cleanup: `clearScene()` khi kết thúc module.

---

## 🎯 TỔNG KẾT CUỐI MODULE 13.7

**Tổng kết kiến thức:**
- Điều kiện đủ để 2 mặt phẳng song song: chứa 2 đường thẳng cắt nhau, cả 2
  đều song song mặt phẳng kia — chỉ 1 đường là chưa đủ.
- 2 đối tượng cùng song song với 1 đối tượng thứ 3 KHÔNG chắc chắn song
  song với nhau (bẫy bắc cầu).
- Lăng trụ là kết quả phép tịnh tiến đáy dưới theo vector cạnh bên — mọi
  điểm tương ứng (đỉnh, trung điểm, trọng tâm...) đều tuân theo đúng 1
  vector tịnh tiến đó.
- Thiết diện của mặt cắt song song đáy luôn đồng dạng với đáy, áp dụng cho
  mọi loại đa giác đáy.
- Lăng trụ không bắt buộc "đứng" — lăng trụ xiên vẫn hợp lệ nếu đủ 2 điều
  kiện định nghĩa.

**Tổng kết sai lầm:**
1. Áp dụng song song bắc cầu sai — dấu hiệu: kết luận song song chỉ dựa vào
   "cùng song song với 1 thứ 3" mà không xét khả năng cắt nhau.
2. Nhầm trọng tâm với trung điểm — dấu hiệu: áp nhầm công thức chia tỉ lệ
   của trung điểm cho trọng tâm hoặc ngược lại.
3. Cho rằng lăng trụ phải "đứng" — dấu hiệu: loại bỏ 1 lăng trụ hợp lệ chỉ
   vì hình dạng trông nghiêng, lạ mắt.

---

## ✅ CRITICAL REVIEW — TỰ PHẢN BIỆN

📝 **Rà soát bản quyền (áp dụng theo đúng nguyên tắc đã dùng nhất quán từ
Module 12.3 tới giờ):** Đã rà toàn bộ 6 tab — mỗi tab đều đổi ít nhất 1 yếu
tố cấu trúc so với bài SGK gốc tương ứng (loại đa giác đáy, cặp điểm được
chọn, tỉ lệ chia, hướng mặt cắt, hoặc dạng câu hỏi đóng/mở), không chỉ đổi
số liệu đơn thuần. Chi tiết từng tab xem ghi chú bản quyền riêng ở đầu mỗi
tab.

⚠️ **Rủi ro 1 (đã xử lý):** Tab 5 bước 4 ban đầu hỏi tỉ lệ THỂ TÍCH — bị
đánh giá vượt phạm vi Bài 13 (chưa dạy thể tích khối ở chương này). Đã đổi
sang tỉ lệ DIỆN TÍCH ĐÁY, giữ đúng cùng bản chất "chỉ 1 chiều thay đổi,
không luỹ thừa tỉ lệ" nhưng bám sát đúng kiến thức đã dạy.

⚠️ **Rủi ro 2:** Module có 6 tab, thời lượng ~18-22 phút — dài hơn đáng kể
so với các module trước (~10-15 phút). Cần cân nhắc chia thành 2 buổi học
nếu học sinh khó tập trung liên tục, hoặc giữ nguyên vì đây đã được xác
nhận là "luyện tập tổng hợp, có thể dài hơn".

📖 **Kiểm tra caption:** Đã rà toàn bộ 6 tab — mọi bước tương tác đều có
giải thích kiến thức đi kèm, không có bước nào chỉ báo Đúng/Sai trơn.

---

**Kịch bản đã sẵn sàng! Đây là module cuối cùng của Bài 13 (13.1→13.7) —
toàn bộ chuỗi module Bài 12-13 đã hoàn thành kịch bản chi tiết.**

- ✅ Duyệt — chuyển sang Giai đoạn 2 (Thiết kế giao diện chi tiết) cho toàn
  bộ các module
- ✏️ Chỉnh — nêu rõ tab/phần nào cần thay đổi

---

> **Phiên bản:** 1.0
> **Ngày tạo:** 12/08/2026
> **Tài liệu tham chiếu:** `01_scenario_builder_v4_1.md`,
> `01_scenario_builder_3d_addendum.md`, `04_design_toan_3d.md`,
> `05_threejs_engine.md`, `06_geometry_math.md`, đối chiếu với
> `solid_library.html` (Kho Khối Hình Không Gian — Nhánh B) và
> Module 13.5 (nguồn nội dung lăng trụ xiên hoãn lại)
