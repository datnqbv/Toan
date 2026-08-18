# Bài 17: Dấu của tam thức bậc hai — Module 3: Luyện tập tổng hợp

**Tên Bài:** Bài 17 – Dấu của tam thức bậc hai
**Tên Module:** Module 3 – Luyện tập tổng hợp (gộp cả phần quy trình giải BPT bậc hai đã có
video Manim, không tách Module 2 riêng)
**Mục tiêu:** Phần 3A giúp học sinh tự luyện lại đúng quy trình 3 bước giải BPT bậc hai
(đã học qua video Manim) bằng công cụ luyện tập lặp lại không giới hạn. Phần 3B vận dụng
vào bài toán tham số, trò chơi tìm lỗi sai, và 1 ứng dụng thực tế.

---

## Bối cảnh sư phạm

- Module 2 (Giải BPT bậc hai) đã có video Manim dạy quy trình — theo yêu cầu giáo viên,
  KHÔNG tách thành module riêng mà gộp vào đây làm Phần 3A: 1 công cụ luyện tập TỔNG QUÁT
  (hệ số a,b,c có thể đổi, có nút "Làm bài khác" sinh đề mới), mô phỏng đúng tinh thần công
  cụ luyện tập BPT bậc nhất 2 ẩn mà giáo viên đã cung cấp làm mẫu tham khảo.
- Phần 3B dùng bối cảnh thực tế **lấy cảm hứng từ hầm chui Kim Liên (Hà Nội)** — số liệu
  trong bài là MÔ PHỎNG MINH HOẠ (không khẳng định là số đo chính xác của hầm thật, vì số
  liệu thật có thể khác), chỉ dùng địa danh có thật để bài toán gần gũi, dễ hình dung hơn.

## Sai lầm cần giải quyết (theo cột M7/M8 PPCT)

| # | Sai lầm | Phần xử lý |
|---|---|---|
| 1 | Lấy nhầm miền trong/ngoài nghiệm khi đọc kết quả BPT | Phần 3A, Bước 3 |
| 2 | Quên điều kiện thực tế của biến khi có bối cảnh | Phần 3B, B3a/B3b/B3c |
| 3 | Sai dấu khi nhân/chia BPT với số âm | Phần 3B, trò chơi "Chữa bệnh" + B3b |
| 4 | Lẫn Δ>0 với Δ≥0 khi biện luận tham số | Phần 3B, bài tham số + trò chơi "Chữa bệnh" |

**Loại simulation:** Phần 3A — công cụ luyện tập quy trình tổng quát, lặp lại không giới
hạn. Phần 3B — luyện tập tổng hợp có bối cảnh + trò chơi tìm lỗi sai.
**Thời gian dự kiến:** 18–22 phút (3A ~7-8 phút mỗi lượt, có thể làm lại nhiều lượt; 3B ~11–14
phút với 3 ứng dụng thực tế đa dạng lĩnh vực).
**Sổ tay kiến thức:** Có — hiện xuyên suốt cả Phần 3A và 3B, học sinh tự bấm gọi ra khi cần.

### Sổ tay kiến thức
- Δ = b² − 4ac (hoặc Δ' = b'² − ac với b=2b').
- Δ<0: f(x) cùng dấu a, mọi x. Δ=0: cùng dấu a, trừ x=−b/2a (f=0 tại đó). Δ>0: 2 nghiệm
  x₁<x₂; cùng dấu a NGOÀI [x₁;x₂], trái dấu a TRONG (x₁;x₂).
- Khi nhân/chia cả 2 vế BPT với 1 số ÂM, phải ĐỔI CHIỀU bất phương trình.
- "2 nghiệm phân biệt" cần Δ>0 (nghiêm ngặt) — Δ=0 chỉ cho 1 nghiệm kép (không phải "2
  nghiệm trùng nhau" theo nghĩa 2 nghiệm phân biệt).

---

## Phần 3A — Công cụ luyện tập quy trình giải BPT bậc hai

*(Mô phỏng đúng cấu trúc công cụ mẫu: hệ số a,b,c và dấu BPT có thể tự nhập hoặc dùng mặc
định, các bước khoá tuần tự, có nút "Làm bài khác" sinh đề mới ngẫu nhiên — vì KHÔNG có 1 đáp
số cố định, Athena chỉ hướng dẫn theo QUY TẮC chung, không tính hộ hay đọc thẳng kết quả.)*

**Mặc định ban đầu:** f(x) = x² − 5x + 6, dấu BPT ≥ 0 (tức giải x²−5x+6 ≥ 0). Học sinh có
thể đổi a, b, c và dấu BPT bất kỳ lúc nào, hoặc bấm "Làm bài khác" để hệ thống tự sinh bộ số
mới (đảm bảo xoay vòng đủ cả 3 trường hợp Δ qua nhiều lượt bấm).

### Bước 1 — Tính Δ, tìm nghiệm

**🗣️ Hướng dẫn thao tác (quy tắc chung, không phụ thuộc số cụ thể):**
> "Với tam thức f(x) = ax² + bx + c hiện trên màn hình, tính Δ = b² − 4ac, nhập vào ô. Sau
> đó: nếu Δ>0, tìm 2 nghiệm x₁, x₂ bằng công thức nghiệm; nếu Δ=0, tìm nghiệm kép; nếu Δ<0,
> chọn 'Vô nghiệm'."

**✅ Giải thích (áp dụng quy tắc chung, không đọc số cụ thể hộ học sinh):**
> "Đúng! Bạn vừa tính đúng Δ và xác định đúng số nghiệm theo dấu của Δ. Đây luôn là bước đầu
> tiên bắt buộc trước khi lập bảng xét dấu — không có Δ và nghiệm thì không thể biết tam thức
> đổi dấu ở đâu."

**❌ Khi sai — khung 3 lần (áp dụng quy tắc chung):**
- Lần 1: shake, không gợi ý.
- Lần 2: gợi ý *"Kiểm tra lại công thức Δ = b² − 4ac — bạn đã thay đúng a, b, c của tam thức
  hiện tại chưa? Chú ý dấu của từng hệ số."*
- Lần 3: hệ thống tự tính và hiện đúng Δ, nghiệm (nếu có) cho bộ số HIỆN TẠI trên màn hình
  của học sinh — TUYỆT ĐỐI không dùng số của bộ đề khác.

### Bước 2 — Lập bảng xét dấu

**🗣️ Hướng dẫn thao tác:**
> "Dựa vào Δ và nghiệm vừa tìm, lập bảng xét dấu của f(x): click vào từng ô trong bảng để
> chọn dấu (+ hoặc −) của f(x) trên mỗi khoảng, dựa vào dấu của hệ số a và định lí dấu tam
> thức đã học."

**✅ Giải thích:**
> "Chính xác — bạn đã áp dụng đúng định lí: các khoảng NGOÀI nghiệm cùng dấu với a, khoảng
> TRONG 2 nghiệm (nếu có) trái dấu với a. Bảng xét dấu này chính là công cụ để đọc ra tập
> nghiệm BPT ở Bước 3."

**❌ Khi sai — khung 3 lần:** lần 2 gợi ý *"Nhớ lại: dấu a là gì? Ngoài các nghiệm, dấu f(x)
LUÔN giống dấu a — chỉ đổi dấu ở khoảng NẰM GIỮA 2 nghiệm (nếu có 2 nghiệm phân biệt)."*; lần
3 hệ thống tự điền đúng bảng dấu cho bộ số hiện tại.

### Bước 3 — Đọc kết quả theo đúng dấu BPT (bước hay sai nhất)

**🗣️ Hướng dẫn thao tác:**
> "Nhìn lại dấu của BPT đang yêu cầu (hiện ở đầu bài — VD f(x)≥0). Từ bảng xét dấu ở Bước 2,
> chọn ĐÚNG các khoảng mà dấu f(x) khớp với yêu cầu này (click chọn trên trục số hoặc trên
> chính bảng xét dấu)."

**✅ Giải thích:**
> "Chính xác! Bạn đã chọn đúng các khoảng có dấu khớp với yêu cầu BPT. Đây là bước học sinh
> hay sai nhất — dễ lấy NHẦM miền TRONG 2 nghiệm thay vì miền NGOÀI (hoặc ngược lại) khi hệ
> số a âm. Luôn quay lại đối chiếu: bảng xét dấu cho biết dấu ở TỪNG khoảng, còn BPT yêu cầu
> dấu NÀO — chỉ chọn đúng khoảng có dấu khớp, không chọn theo cảm tính vị trí trong/ngoài."*

**❌ Khi sai (đặc biệt nếu chọn nhầm miền trong ↔ ngoài) — khung 3 lần:**
- Lần 1: shake, không gợi ý.
- Lần 2: gợi ý *"Xem lại bảng xét dấu Bước 2 — khoảng nào có dấu ĐÚNG BẰNG dấu mà đề bài yêu
  cầu (BPT hiện tại đang hỏi dấu gì)? Đừng chọn theo vị trí 'trong/ngoài' một cách máy móc,
  hãy chọn theo ĐÚNG DẤU trong bảng."*
- Lần 3: hệ thống tự tô sáng đúng miền nghiệm trên bảng dấu và trục số cho bộ số hiện tại,
  học sinh chỉ cần đọc và viết lại thành tập nghiệm.

**🔁 Nút "Làm bài khác":** sau khi hoàn thành cả 3 bước, học sinh có thể bấm để hệ thống sinh
bộ (a,b,c, dấu BPT) mới — khoá lại cả 3 bước để luyện lại từ đầu với số liệu khác, không giới
hạn số lần luyện tập.

---

## Phần 3B — Luyện tập tổng hợp: tham số, tìm lỗi sai, ứng dụng thực tế

### B1. Bài toán tham số

**🗣️ Hướng dẫn thao tác:**
> "Tìm tất cả giá trị của m để f(x) = x² − 2mx + m + 6 luôn DƯƠNG với mọi x ∈ ℝ. Gợi ý: một
> tam thức có a>0 luôn dương với mọi x khi nào (liên hệ tới Δ)? Tính Δ theo m trước, sau đó
> giải bất phương trình theo m."

**✅ Giải thích khi đúng (−2<m<3):**
> "Chính xác! f(x) luôn dương với mọi x khi a>0 (ở đây a=1>0, luôn đúng) VÀ Δ<0. Ta có
> Δ = 4m² − 4(m+6) = 4(m²−m−6) = 4(m−3)(m+2). Giải Δ<0 ⟺ (m−3)(m+2)<0 ⟺ −2<m<3. Đây chính
> là bài toán 'biện luận tham số' — thay vì có số cụ thể, ta coi Δ như 1 biểu thức theo m rồi
> giải bất phương trình để tìm m."

**❌ Khi sai — khung 3 lần:**
- Lần 2: gợi ý *"Tính Δ theo m trước (đừng quên khai triển đúng (−2m)² = 4m²). Sau đó bạn
  đang cần Δ<0 hay Δ≤0 — 'luôn dương' nghĩa là KHÔNG BAO GIỜ chạm 0, vậy Δ phải NGHIÊM NGẶT
  âm."*
- Lần 3: hiện đáp án đầy đủ kèm giải thích như trên.

### B2. Trò chơi "Chữa bệnh cho bài giải"

**🗣️ Hướng dẫn thao tác:**
> "Bên dưới là 2 bài giải có SẴN LỖI SAI (do 1 bạn học sinh khác làm). Đọc kỹ từng dòng, tìm
> ra dòng bị sai, chạm/click vào đúng dòng đó, rồi chọn sửa lại cho đúng."

**Bài giải sai #1 (lỗi đổi chiều BPT khi nhân số âm):**
> Đề: Giải BPT −2x² + 3x − 1 ≥ 0.
> Bài giải sai: "Nhân cả 2 vế với −1, ta được: 2x² − 3x + 1 ≥ 0 (dòng SAI — đây là dòng cần
> tìm) ⟹ giải ra x ≤ 1/2 hoặc x ≥ 1."

**✅ Giải thích sau khi học sinh chỉ đúng dòng sai:**
> "Đúng — dòng sai nằm ở phép nhân cả 2 vế với −1. Khi nhân/chia BẤT PHƯƠNG TRÌNH với 1 số
> ÂM, phải ĐỔI CHIỀU bất phương trình: −2x²+3x−1≥0 nhân với −1 phải cho ra 2x²−3x+1 ≤ 0 (đổi
> ≥ thành ≤), không giữ nguyên chiều ≥ như bài giải sai đã làm. Sửa lại đúng: 2x²−3x+1≤0 ⟺
> (2x−1)(x−1)≤0 ⟺ 1/2 ≤ x ≤ 1."

**Bài giải sai #2 (lẫn Δ>0 với Δ≥0):**
> Đề: Tìm m để phương trình x² − 4x + m = 0 có 2 nghiệm phân biệt.
> Bài giải sai: "Cần Δ ≥ 0 (dòng SAI) ⟺ 16 − 4m ≥ 0 ⟺ m ≤ 4."

**✅ Giải thích sau khi học sinh chỉ đúng dòng sai:**
> "Đúng — dòng sai là điều kiện Δ≥0. '2 NGHIỆM PHÂN BIỆT' yêu cầu Δ PHẢI DƯƠNG NGHIÊM NGẶT
> (Δ>0), không được bằng 0 — vì Δ=0 chỉ cho ĐÚNG 1 nghiệm kép (2 nghiệm trùng nhau thành 1
> điểm), không phải '2 nghiệm phân biệt'. Sửa lại đúng: Δ>0 ⟺ 16−4m>0 ⟺ m<4."

**❌ Khi học sinh chỉ sai dòng — khung 3 lần:** lần 1 shake; lần 2 gợi ý riêng theo từng bài
(bài 1: *"Có bước nào nhân/chia BPT với số âm không? Kiểm tra xem chiều bất đẳng thức có được
đổi đúng chưa."*; bài 2: *"'Phân biệt' nghĩa là 2 nghiệm khác nhau hoàn toàn — Δ=0 có cho ra
2 nghiệm khác nhau không?"*); lần 3 tô sáng đúng dòng sai kèm giải thích.

### B3. Ứng dụng thực tế (3 bối cảnh khác nhau, đa dạng lĩnh vực)

#### B3a. Xe siêu trường qua hầm chui

*(Bối cảnh lấy cảm hứng từ hầm chui Kim Liên, Hà Nội — số liệu trong bài là MÔ PHỎNG MINH
HOẠ cho mục đích luyện tập, không phải số đo chính xác của hầm thật.)*

Mặt cắt vòm hầm được mô hình hoá bởi parabol **y = 5,5 − 0,05x²** (x = khoảng cách tính từ
tim hầm, y = độ cao vòm, đơn vị mét). Xe siêu trường cao **4,2m** (đúng ngưỡng xe quá khổ
theo quy định VN) muốn đi qua hầm.

**🗣️ Hướng dẫn thao tác:**
> "Xe cao 4,2m đi qua hầm có mặt cắt vòm y = 5,5 − 0,05x². Viết bất phương trình thể hiện
> điều kiện 'xe không vướng vòm' (so sánh độ cao vòm với chiều cao xe), sau đó giải bất
> phương trình đó để tìm x — đây chính là phạm vi xe được phép đi so với tim hầm."

**✅ Giải thích khi đúng:**
> "Chính xác! Điều kiện an toàn là 5,5−0,05x² ≥ 4,2 ⟺ 0,05x² ≤ 1,3 ⟺ x² ≤ 26 ⟺ −√26 ≤ x ≤
> √26 (√26 ≈ 5,1). Vậy xe phải đi trong phạm vi cách tim hầm KHÔNG QUÁ khoảng 5,1m mỗi bên
> mới không vướng vòm hầm. Đây đúng là bước 'đối chiếu điều kiện thực tế' mà PPCT nhắc — nếu
> xe đi lệch quá xa về 1 bên (hơn 5,1m), dù toán học vẫn giải được BPT nhưng thực tế xe sẽ bị
> vướng."

**❌ Khi sai — khung 3 lần:**
- Lần 2: gợi ý *"Điều kiện an toàn là ĐỘ CAO VÒM phải LỚN HƠN HOẶC BẰNG chiều cao xe — viết
  đúng chiều bất phương trình này trước khi giải."*
- Lần 3: hiện đáp án đầy đủ kèm giải thích như trên.

#### B3b. Doanh thu tối thiểu — CLB Robotics bán vé workshop

CLB Lập trình Robotics tổ chức workshop, bán vé **200.000đ**, dự kiến **30 bạn** tham gia.
Cứ giảm giá **20.000đ**, ước tính có thêm **10 bạn** đăng ký. CLB cần huy động **ít nhất
8.000.000đ** để đủ trả thù lao giảng viên mời ngoài và thuê thiết bị.

Gọi x = số lần giảm giá 20.000đ. Doanh thu: R(x) = (200.000−20.000x)(30+10x) =
**−200.000x² + 1.400.000x + 6.000.000**.

**🗣️ Hướng dẫn thao tác:**
> "Viết bất phương trình R(x) ≥ 8.000.000, sau đó giải để tìm khoảng x (số lần giảm giá) mà
> CLB đạt được mục tiêu doanh thu. Từ đó suy ra khoảng giá vé tương ứng."

**✅ Giải thích khi đúng:**
> "Chính xác! Giải −200.000x²+1.400.000x+6.000.000 ≥ 8.000.000 ⟺ −200.000x²+1.400.000x
> −2.000.000 ≥ 0 ⟺ (chia cho −200.000, ĐỔI CHIỀU) x²−7x+10 ≤ 0 ⟺ (x−2)(x−5) ≤ 0 ⟺ 2 ≤ x ≤ 5.
> Vậy CLB cần giảm giá từ 2 đến 5 lần — tức giá vé nằm trong khoảng từ 100.000đ (giảm 5 lần)
> đến 160.000đ (giảm 2 lần) — mới đạt doanh thu tối thiểu 8.000.000đ. Chú ý: giảm giá QUÁ
> NHIỀU (x>5) hay QUÁ ÍT (x<2) đều KHÔNG đạt được mục tiêu — đây là ví dụ BPT bậc hai cho ra
> 1 KHOẢNG nghiệm, khác với bài toán tối ưu ở Bài 16 (chỉ tìm 1 điểm duy nhất cho doanh thu
> LỚN NHẤT)."

**❌ Khi sai (đặc biệt nếu quên đổi chiều khi chia cho số âm) — khung 3 lần:** lần 2 gợi ý
*"Khi chia cả 2 vế bất phương trình cho 1 số ÂM (như −200.000), nhớ ĐỔI CHIỀU bất đẳng
thức"*; lần 3 hiện đáp án đầy đủ kèm giải thích.

#### B3c. Nồng độ oxy trong ao nuôi cá — cần bật máy sục khí lúc nào?

Sau 1 trận mưa lớn, nồng độ oxy hoà tan trong ao nuôi cá thay đổi theo thời gian t (giờ,
tính từ lúc mưa tạnh, 0≤t≤10) theo mô hình: **O(t) = 0,25t² − 2,5t + 9,25** (mg/L). Ngưỡng
an toàn cho cá là O(t) ≥ 4 mg/L — nếu thấp hơn, cần bật máy sục khí bổ sung oxy.

**🗣️ Hướng dẫn thao tác:**
> "Tìm khoảng thời gian t mà nồng độ oxy XUỐNG DƯỚI mức an toàn (O(t) < 4), để biết khi nào
> cần bật máy sục khí. Viết bất phương trình rồi giải."

**✅ Giải thích khi đúng:**
> "Chính xác! Giải 0,25t²−2,5t+9,25 < 4 ⟺ 0,25t²−2,5t+5,25 < 0 ⟺ (nhân 4) t²−10t+21 < 0 ⟺
> (t−3)(t−7) < 0 ⟺ 3 < t < 7. Vậy từ giờ thứ 3 đến giờ thứ 7 sau khi mưa tạnh, nồng độ oxy
> xuống dưới mức an toàn (thấp nhất còn 3mg/L tại giờ thứ 5) — đây chính là khung giờ CẦN bật
> máy sục khí. Trước giờ thứ 3 và sau giờ thứ 7, nồng độ oxy tự phục hồi về mức an toàn, hàm
> số này có hệ số a>0 (khác 2 bài trên có a<0) — một dạng bài BPT khác: tìm khoảng KHÔNG đạt
> yêu cầu, thay vì khoảng ĐẠT yêu cầu."

**❌ Khi sai — khung 3 lần:** lần 2 gợi ý *"Viết đúng chiều bất phương trình trước: đang tìm
lúc oxy THẤP HƠN 4, nghĩa là O(t) < 4, không phải ≥4."*; lần 3 hiện đáp án kèm giải thích.

---

## 📚 Tổng kết kiến thức (cuối Module 3)

> **1.** Quy trình giải BPT bậc hai luôn gồm đúng 3 bước: (1) tính Δ, tìm nghiệm, (2) lập
> bảng xét dấu dựa theo định lí dấu tam thức, (3) đọc kết quả — CHỌN ĐÚNG khoảng có dấu khớp
> với yêu cầu BPT (đây là bước dễ sai miền trong/ngoài nhất).
>
> **2.** Khi nhân/chia cả 2 vế bất phương trình với 1 số ÂM, luôn phải ĐỔI CHIỀU bất đẳng
> thức.
>
> **3.** "2 nghiệm phân biệt" cần Δ dương NGHIÊM NGẶT (Δ>0) — không được nhầm với Δ≥0.
>
> **4.** Với bài toán thực tế, luôn đối chiếu nghiệm toán học với điều kiện thực tế trước khi
> kết luận. BPT bậc hai có 2 dạng bài phổ biến: tìm khoảng ĐẠT ngưỡng yêu cầu (VD hầm chui,
> doanh thu tối thiểu) và tìm khoảng KHÔNG ĐẠT ngưỡng an toàn (VD nồng độ oxy) — luôn đọc kỹ
> đề để viết đúng chiều bất phương trình cần giải.

---

## Bố cục giao diện Desktop & Mobile

- Phần 3A: Desktop hiện đồ thị + bảng xét dấu cạnh nhau; Mobile xếp dọc, bảng xét dấu thu
  gọn thành các hàng cuộn ngang nếu cần.
- Phần 3B (B2 — Chữa bệnh): Desktop hiện toàn bộ lời giải sai trên 1 khung, click trực tiếp
  vào dòng; Mobile mỗi dòng là 1 thẻ riêng, tap để chọn dòng sai.
- Phần 3B (B3 — 3 ứng dụng thực tế): mỗi bối cảnh có canvas/hình minh hoạ riêng (mặt cắt
  hầm, biểu đồ doanh thu theo giá vé, biểu đồ nồng độ oxy theo giờ) kèm thanh trượt để học
  sinh thử các giá trị trước khi chốt đáp án bất phương trình.

## LMS `complete()`

- Phần 3A: `items[]` ghi `attempts` theo từng bước (1,2,3) CHO MỖI LƯỢT "Làm bài khác" —
  lưu lại số lượt đã luyện tập để giáo viên theo dõi mức độ luyện tập lặp lại.
- Phần 3B: `items[]` cho B1 (tham số), B2 (2 bài chữa bệnh riêng), B3a/B3b/B3c (3 ứng dụng
  thực tế, mỗi bối cảnh 1 item riêng).

## Critical Review

- Đã gộp Module 2 (giải BPT bậc hai) vào Module 3 làm Phần 3A theo đúng yêu cầu giáo viên,
  mô phỏng cấu trúc công cụ luyện tập tổng quát (hệ số tự nhập/mặc định, nút "Làm bài khác",
  các bước khoá tuần tự, TUYỆT ĐỐI không tính hộ số cụ thể) theo đúng file mẫu BPT bậc nhất
  2 ẩn giáo viên cung cấp.
- **Đã bổ sung 2 ứng dụng thực tế mới** (B3b doanh thu tối thiểu CLB Robotics, B3c nồng độ
  oxy ao nuôi cá) bên cạnh hầm chui, theo phản hồi giáo viên rằng BPT bậc hai ứng dụng thực
  tế rất đa dạng — không nên chỉ có 1 ví dụ. 3 bối cảnh giờ trải đều 3 lĩnh vực khác nhau
  (giao thông/kỹ thuật, kinh tế, môi trường/sinh học), và đa dạng cả về dấu hệ số a (B3a,
  B3b có a<0; B3c có a>0) lẫn dạng bài (B3a/B3c tìm khoảng ĐẠT/KHÔNG ĐẠT ngưỡng, B3b liên hệ
  trực tiếp tới bài toán tối ưu đã học ở Bài 16 để học sinh thấy sự khác biệt giữa "tìm 1
  điểm tối ưu" và "tìm 1 khoảng thoả mãn").
- Bối cảnh hầm chui (B3a) đã đổi cách trình bày: chỉ nêu là "lấy cảm hứng từ hầm chui Kim
  Liên", không khẳng định số liệu là số đo chính xác thực tế — theo đúng yêu cầu giáo viên.
- Chiều cao xe đã giữ đúng 4,2m (ngưỡng quy định xe siêu trường VN), không thổi phồng.
- Bài tham số (x²−2mx+m+6, đáp số −2<m<3), 2 bài "chữa bệnh", và cả B3b/B3c đều dùng số liệu
  mới, khác BT 6.17 SGK và khác các ví dụ SGK đã dùng (rào vườn, ném bóng, cầu vượt).
