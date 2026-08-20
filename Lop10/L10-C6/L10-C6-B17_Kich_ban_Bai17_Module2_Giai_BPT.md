# Bài 17: Dấu của tam thức bậc hai — Module 2: Giải bất phương trình bậc hai

**Tên Bài:** Bài 17 – Dấu của tam thức bậc hai
**Tên Module:** Module 2 – Giải bất phương trình bậc hai
**Mục tiêu:** Học sinh nắm vững quy trình 3 bước giải BPT bậc hai (tính Δ+nghiệm → lập bảng
dấu → đọc kết quả) qua 1 bài toán thực tiễn cụ thể (xe qua hầm parabol, đúng PPCT), sau đó tự
luyện lại quy trình này bằng công cụ luyện tập không giới hạn số lần.

---

## Bối cảnh sư phạm (theo đúng PPCT — Module 2, dòng 7)

- PPCT chỉ định rõ: mục tiêu D7 "Vận dụng được bất phương trình bậc hai một ẩn vào giải quyết
  bài toán thực tiễn, chẳng hạn xác định chiều cao tối đa để xe có thể qua được hầm có hình
  dạng parabol"; hoạt động gợi ý O7 "Bài toán Xe tải qua hầm: HS tính chiều rộng tối đa từ PT
  mặt cắt hầm parabol." — bài toán hầm chui PHẢI nằm trong Module này, không tách riêng.
- Sau ví dụ dẫn dắt bằng bài toán hầm, module có thêm 1 công cụ luyện tập TỔNG QUÁT (hệ số
  a,b,c tự nhập/mặc định, nút "Làm bài khác") để củng cố quy trình — mô phỏng đúng tinh thần
  công cụ luyện tập BPT bậc nhất 2 ẩn mà giáo viên đã cung cấp làm mẫu tham khảo.

## Sai lầm cần giải quyết (theo cột M7/N7 PPCT)

| # | Sai lầm | Cơ chế đối chất |
|---|---|---|
| 1 | Lấy nhầm tập nghiệm khi f(x)>0, a>0, Δ>0 (phải lấy NGOÀI [x₁;x₂], hay lấy nhầm TRONG) | Bước 3 — đối chiếu đúng dấu, không chọn theo cảm tính vị trí |
| 2 | Quên điều kiện thực tiễn của biến | Xử lý ngay trong bài toán hầm — đối chiếu nghiệm với domain thực tế (khoảng cách không âm, không vượt bề rộng hầm) |

**Loại simulation:** Ví dụ dẫn dắt có bối cảnh thực tế (Phần A) + công cụ luyện tập quy trình
tổng quát (Phần B).
**Thời gian dự kiến:** 12–14 phút (Phần A ~6–7 phút; Phần B ~6–7 phút/lượt, có thể làm lại).
**Sổ tay kiến thức:** Có — hiện xuyên suốt, học sinh tự bấm gọi ra khi cần.

### Sổ tay kiến thức
- Δ = b² − 4ac (hoặc Δ' = b'² − ac với b=2b').
- Δ<0: f(x) cùng dấu a, mọi x. Δ=0: cùng dấu a, trừ x=−b/2a. Δ>0: 2 nghiệm x₁<x₂; cùng dấu a
  NGOÀI [x₁;x₂], trái dấu a TRONG (x₁;x₂).

---

## Phần A — Ví dụ dẫn dắt: Xe siêu trường qua hầm chui

*(Bối cảnh lấy cảm hứng từ hầm chui Kim Liên, Hà Nội — số liệu trong bài là MÔ PHỎNG MINH
HOẠ cho mục đích học tập, không phải số đo chính xác của hầm thật, vì số liệu thật có thể
khác.)*

Mặt cắt vòm hầm được mô hình hoá bởi parabol **y = 5,5 − 0,05x²** (x = khoảng cách tính từ
tim hầm, y = độ cao vòm, đơn vị mét, miền xác định thực tế −10,49 ≤ x ≤ 10,49 — nơi vòm chạm
mặt đất). Xe siêu trường cao **4,2m** (đúng ngưỡng xe quá khổ theo quy định VN) muốn đi qua
hầm.

### Bước 1 — Thiết lập bất phương trình

**🗣️ Hướng dẫn thao tác:**
> "Điều kiện để xe không vướng vòm là ĐỘ CAO VÒM tại vị trí xe đi qua phải LỚN HƠN HOẶC BẰNG
> chiều cao xe. Viết bất phương trình thể hiện điều kiện này, dùng công thức y = 5,5−0,05x²
> và chiều cao xe 4,2m."

**✅ Giải thích khi đúng (5,5−0,05x² ≥ 4,2):**
> "Chính xác! Điều kiện an toàn là 5,5 − 0,05x² ≥ 4,2 — đây chính là 1 bất phương trình bậc
> hai, và giải nó sẽ cho ta biết PHẠM VI x (khoảng cách tới tim hầm) mà xe được phép đi qua."

**❌ Khi sai — khung 3 lần:** lần 2 gợi ý *"Độ cao vòm là y = 5,5−0,05x², chiều cao xe là
4,2 — 'không vướng' nghĩa là độ cao vòm phải ≥ chiều cao xe."*; lần 3 hiện đáp án.

### Bước 2 — Tính Δ, tìm nghiệm

**🗣️ Hướng dẫn thao tác:**
> "Chuyển bất phương trình về dạng ax²+bx+c ≥ 0 (hoặc ≤0), tính Δ và tìm nghiệm của tam thức
> tương ứng."

**✅ Giải thích khi đúng:**
> "Chính xác! 5,5−0,05x²≥4,2 ⟺ −0,05x²+1,3≥0 ⟺ (nhân −20, ĐỔI CHIỀU) x²−26≤0. Tam thức
> x²−26 có Δ'=26>0 (dùng b=0 nên Δ'=−ac=26), 2 nghiệm x=±√26 (√26≈5,1)."

**❌ Khi sai — khung 3 lần:** lần 2 gợi ý *"Khi nhân/chia cả 2 vế với số ÂM, nhớ đổi chiều bất
phương trình trước khi tính Δ."*; lần 3 hiện đáp án.

### Bước 3 — Lập bảng dấu và đọc kết quả (đối chiếu điều kiện thực tế)

**🗣️ Hướng dẫn thao tác:**
> "Lập bảng xét dấu cho tam thức x²−26, đọc ra tập nghiệm của x²−26≤0. Sau đó, đối chiếu kết
> quả với Ý NGHĨA THỰC TẾ của bài toán: x đại diện cho khoảng cách tới tim hầm — có giá trị
> nào trong tập nghiệm KHÔNG có ý nghĩa thực tế không?"

**✅ Giải thích khi đúng (x∈[−√26;√26], không có giá trị nào cần loại thêm):**
> "Chính xác! x²−26≤0 ⟺ −√26≤x≤√26 (√26≈5,1). Đối chiếu thực tế: x là khoảng cách tới tim
> hầm, có thể âm (bên trái tim hầm) hoặc dương (bên phải) — vì hầm đối xứng 2 bên, nên toàn bộ
> khoảng [−5,1; 5,1] đều có ý nghĩa (miễn không vượt quá bề rộng hầm thực tế). Vậy xe phải đi
> trong phạm vi cách tim hầm KHÔNG QUÁ 5,1m mỗi bên mới không vướng vòm."

**❌ Khi sai (đặc biệt nếu lấy nhầm miền ngoài [−√26;√26] thay vì trong) — khung 3 lần:** lần
2 gợi ý *"Xem lại bảng dấu — bạn đang cần x²−26 ≤ 0 hay ≥ 0? Chọn đúng khoảng có dấu khớp,
không chọn theo cảm tính trong/ngoài."*; lần 3 hiện đáp án đầy đủ kèm giải thích.

---

## Phần B — Công cụ luyện tập quy trình giải BPT bậc hai

*(Mô phỏng đúng cấu trúc công cụ mẫu: hệ số a,b,c và dấu BPT có thể tự nhập hoặc dùng mặc
định, các bước khoá tuần tự, có nút "Làm bài khác" sinh đề mới ngẫu nhiên — vì KHÔNG có 1 đáp
số cố định, Athena chỉ hướng dẫn theo QUY TẮC chung, không tính hộ hay đọc thẳng kết quả.)*

**Mặc định ban đầu:** f(x) = x² − 5x + 6, dấu BPT ≥ 0. Học sinh có thể đổi a, b, c và dấu BPT
bất kỳ lúc nào, hoặc bấm "Làm bài khác" để hệ thống tự sinh bộ số mới (xoay vòng đủ cả 3
trường hợp Δ qua nhiều lượt bấm).

### Bước 1 — Tính Δ, tìm nghiệm

**🗣️ Hướng dẫn thao tác (quy tắc chung):**
> "Với tam thức f(x) = ax² + bx + c hiện trên màn hình, tính Δ = b² − 4ac, nhập vào ô. Sau
> đó: nếu Δ>0, tìm 2 nghiệm x₁, x₂; nếu Δ=0, tìm nghiệm kép; nếu Δ<0, chọn 'Vô nghiệm'."

**✅ Giải thích:** "Đúng! Đây luôn là bước đầu tiên bắt buộc trước khi lập bảng xét dấu."

**❌ Khung 3 lần:** lần 2 gợi ý kiểm tra lại công thức Δ và dấu từng hệ số; lần 3 hệ thống tự
tính cho bộ số HIỆN TẠI.

### Bước 2 — Lập bảng xét dấu

**🗣️ Hướng dẫn thao tác:**
> "Dựa vào Δ và nghiệm vừa tìm, lập bảng xét dấu của f(x): click chọn dấu (+/−) trên mỗi
> khoảng, dựa vào dấu hệ số a và định lí dấu tam thức."

**✅ Giải thích:** "Chính xác — khoảng NGOÀI nghiệm cùng dấu a, khoảng TRONG 2 nghiệm trái
dấu a."

**❌ Khung 3 lần:** lần 2 gợi ý nhắc lại quy tắc dấu; lần 3 hệ thống tự điền bảng dấu.

### Bước 3 — Đọc kết quả theo đúng dấu BPT (bước hay sai nhất)

**🗣️ Hướng dẫn thao tác:**
> "Nhìn dấu BPT đang yêu cầu, chọn ĐÚNG khoảng mà dấu f(x) khớp với yêu cầu này."

**✅ Giải thích:** "Chính xác! Đây là bước hay sai nhất — luôn đối chiếu ĐÚNG DẤU đề bài yêu
cầu với bảng xét dấu, không chọn theo cảm tính trong/ngoài."

**❌ Khung 3 lần:** lần 2 gợi ý đối chiếu lại dấu yêu cầu với bảng; lần 3 hệ thống tự tô sáng
đúng miền nghiệm.

**🔁 Nút "Làm bài khác":** sinh bộ (a,b,c, dấu BPT) mới, khoá lại cả 3 bước để luyện lại,
không giới hạn số lần.

---

## 📚 Tổng kết kiến thức (cuối module)

> **1.** Quy trình giải BPT bậc hai luôn gồm đúng 3 bước: (1) tính Δ, tìm nghiệm, (2) lập
> bảng xét dấu, (3) đọc kết quả — CHỌN ĐÚNG khoảng có dấu khớp với yêu cầu BPT.
>
> **2.** Với bài toán thực tế, sau khi giải BPT xong, luôn ĐỐI CHIẾU nghiệm với điều kiện
> thực tế của biến (VD khoảng cách không âm, không vượt giới hạn vật lý) trước khi kết luận.

---

## Bố cục giao diện Desktop & Mobile

- Phần A: canvas mặt cắt vòm hầm với xe minh hoạ ở giữa, thanh trượt để xem thử các vị trí x
  khác nhau trước khi chốt đáp án bất phương trình.
- Phần B: Desktop hiện đồ thị + bảng xét dấu cạnh nhau; Mobile xếp dọc, bảng xét dấu thu gọn
  cuộn ngang nếu cần.

## LMS `complete()`

- Phần A: `items[]` cho Bước 1, 2, 3 (bài toán hầm).
- Phần B: `items[]` ghi `attempts` theo từng bước (1,2,3) CHO MỖI LƯỢT "Làm bài khác".

## Critical Review

- Cấu trúc module đã sửa lại bám đúng PPCT (dòng 7): bài toán hầm chui PHẢI nằm trong Module
  2 (không tách thành module riêng như bản trước) — đây là ví dụ dẫn dắt chính (Phần A), sau
  đó mới tới công cụ luyện tập tổng quát (Phần B) để củng cố quy trình.
- Bối cảnh hầm chui: chỉ nêu "lấy cảm hứng từ hầm chui Kim Liên", không khẳng định số liệu
  chính xác thực tế. Chiều cao xe giữ đúng 4,2m (ngưỡng quy định xe siêu trường VN).
- Số liệu đã kiểm chứng bằng code: nghiệm x=±√26≈±5,1.
