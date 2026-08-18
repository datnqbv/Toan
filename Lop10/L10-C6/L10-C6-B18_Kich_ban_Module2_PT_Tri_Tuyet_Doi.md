# Bài 18: Phương trình quy về phương trình bậc hai — Module 2: PT dạng |ax+b| = cx+d

**Tên Bài:** Bài 18 – Phương trình quy về phương trình bậc hai
**Tên Module:** Module 2 – Phương trình dạng |ax+b| = cx+d
**Mục tiêu:** Học sinh giải được PT chứa trị tuyệt đối bằng 2 CÁCH khác nhau (bình phương 2
vế → quy về PT bậc hai; và xét 2 trường hợp dấu) — thấy được mối liên hệ và sự khác biệt
giữa 2 cách, đặc biệt hiểu vì sao cách xét trường hợp tự động loại được nghiệm ngoại lai mà
không cần thử lại bằng số.

---

## Bối cảnh sư phạm

- Theo PPCT (I10), phương pháp CHÍNH được dạy là "xét 2 TH ax+b≥0 và ax+b<0". Nhưng vì tên
  bài là "quy về phương trình bậc hai", module này dạy THÊM cách bình phương (tạo ra đúng 1
  PT bậc hai) — rồi cho học sinh so sánh 2 cách trên CÙNG 1 ví dụ để thấy chúng cho cùng 1
  kết quả, nhưng cơ chế loại nghiệm sai khác nhau.
- Số liệu mới, không trùng SGK.

## Sai lầm cần giải quyết (theo cột M10/N10 PPCT)

| # | Sai lầm | Cơ chế đối chất |
|---|---|---|
| 1 | Chỉ xét 1 trường hợp trị tuyệt đối | Bắt buộc hoàn thành CẢ 2 trường hợp mới được qua bước sau |
| 2 | Áp dụng sai điều kiện tương đương khi bình phương PT trị tuyệt đối | So sánh trực tiếp 2 cách giải, đối chiếu chỗ khác nhau |

**Loại simulation:** Quy trình từng bước, dạy song song 2 phương pháp trên cùng 1 ví dụ.
**Thời gian dự kiến:** 10–12 phút.
**Sổ tay kiến thức:** Không có trong quá trình làm — tổng hợp chung ở Module 3.

---

## Ví dụ dẫn dắt: Giải phương trình |x+1| = 2x−5

### Cách 1 — Bình phương 2 vế (quy về PT bậc hai)

**🗣️ Hướng dẫn thao tác:**
> "Bình phương CẢ 2 VẾ của |x+1| = 2x−5 (nhớ: bình phương của trị tuyệt đối |A|² = A²). Khai
> triển, thu gọn về dạng ax²+bx+c=0, nhập kết quả."

**✅ Giải thích khi đúng (3x²−22x+24=0):**
> "Chính xác! (x+1)² = (2x−5)² ⟺ x²+2x+1 = 4x²−20x+25 ⟺ 0 = 3x²−22x+24. Đây là PT bậc hai —
> đúng tinh thần 'quy về phương trình bậc hai' của cả bài học."

**❌ Khi sai — khung 3 lần:** lần 2 gợi ý *"Khai triển riêng từng vế trước: (x+1)² = ? và
(2x−5)² = ? — sau đó mới chuyển vế và rút gọn."*; lần 3 hiện đáp án.

**🗣️ Hướng dẫn thao tác (tiếp — giải và thử lại):**
> "Giải PT bậc hai vừa tìm được (dùng công thức nghiệm, Δ=196=14²), nhập 2 nghiệm. Sau đó
> thử lại TỪNG nghiệm vào phương trình GỐC |x+1|=2x−5 để xác định nghiệm nào hợp lệ."

**✅ Giải thích khi đúng (x=6 hợp lệ, x=4/3 ngoại lai):**
> "Chính xác! Nghiệm: x=6 hoặc x=4/3. Thử lại: tại x=6, VT=|7|=7, VP=12−5=7 → thoả mãn. Tại
> x=4/3, VT=|4/3+1|=7/3, VP=2×4/3−5=−7/3 → 7/3 ≠ −7/3, KHÔNG thoả mãn (vì VT là trị tuyệt đối
> luôn ≥0, mà VP=−7/3 âm) → x=4/3 là nghiệm ngoại lai. Vậy nghiệm duy nhất là x=6."

**❌ Khi sai — khung 3 lần:** giống cơ chế Module 1 (gợi ý tính riêng VT, VP từng nghiệm; lần
3 hiện đáp án đầy đủ).

### Cách 2 — Xét 2 trường hợp dấu

**🗣️ Hướng dẫn thao tác:**
> "Giờ giải LẠI đúng phương trình |x+1|=2x−5 bằng cách khác: xét 2 trường hợp theo dấu của
> biểu thức trong trị tuyệt đối.
> • Trường hợp 1: x+1≥0 (tức x≥−1) → PT trở thành x+1=2x−5. Giải tìm x, rồi kiểm tra x có
> thoả mãn điều kiện x≥−1 không.
> • Trường hợp 2: x+1<0 (tức x<−1) → PT trở thành −(x+1)=2x−5. Giải tìm x, rồi kiểm tra x có
> thoả mãn điều kiện x<−1 không.
> Hoàn thành CẢ 2 trường hợp mới được xem kết luận (không được bỏ qua 1 trường hợp nào)."

**✅ Giải thích khi hoàn thành đúng cả 2 TH:**
> "Chính xác!
> • TH1 (x≥−1): x+1=2x−5 ⟺ x=6. Kiểm tra: 6≥−1 ✓ đúng điều kiện → x=6 là nghiệm.
> • TH2 (x<−1): −(x+1)=2x−5 ⟺ −x−1=2x−5 ⟺ −3x=−4 ⟺ x=4/3. Kiểm tra: 4/3<−1? SAI (4/3 là số
> dương, không nhỏ hơn −1) → x=4/3 KHÔNG thoả điều kiện của chính trường hợp này, LOẠI NGAY
> tại đây, không cần thay số vào phương trình gốc.
> Vậy nghiệm duy nhất vẫn là x=6 — TRÙNG với kết quả ở Cách 1! Nhưng chú ý: ở Cách 2, nghiệm
> x=4/3 bị loại NGAY từ bước kiểm tra điều kiện của trường hợp, không cần thử lại bằng số như
> Cách 1 — đây chính là điểm khác biệt giữa 2 phương pháp."

**❌ Khi chỉ làm 1 trường hợp rồi bỏ qua trường hợp còn lại — cơ chế chặn:**
> Hệ thống KHÔNG cho xem kết luận cuối cùng nếu 1 trong 2 trường hợp còn bỏ trống. athenaGuidance:
> *"Bạn mới xét 1 trường hợp — với PT trị tuyệt đối, LUÔN phải xét ĐỦ CẢ 2 trường hợp dấu,
> dù có thể trực giác đoán được đáp số. Hoàn thành trường hợp còn lại trước khi xem kết luận."*

**❌ Khi sai trong tính toán từng trường hợp — khung 3 lần cho mỗi trường hợp riêng:** lần 2
gợi ý theo đúng TH đang làm (nhắc lại cách bỏ dấu trị tuyệt đối theo đúng dấu đã giả sử); lần
3 hiện đáp án của đúng trường hợp đó.

### So sánh 2 cách (đối chất, không phải bước tính toán)

**🗣️ athenaGuidance:**
> "Bạn vừa giải CÙNG 1 phương trình bằng 2 cách, đều ra x=6. Khác biệt: Cách 1 (bình phương)
> cho ra 2 nghiệm rồi phải THỬ LẠI BẰNG SỐ để loại nghiệm sai. Cách 2 (xét trường hợp) loại
> nghiệm sai NGAY khi kiểm tra điều kiện dấu của từng trường hợp, không cần thử số. Cả 2 cách
> đều đúng — chọn cách nào tuỳ bạn thấy thuận tiện hơn, nhưng LUÔN phải hoàn tất bước kiểm
> tra (thử lại hoặc kiểm tra điều kiện) ở bất kỳ cách nào."

---

## Bố cục giao diện Desktop & Mobile

- Desktop: Cách 1 và Cách 2 hiện thành 2 cột cạnh nhau để dễ đối chiếu trực tiếp khi tới phần
  So sánh; Mobile: Cách 1 làm xong cuộn xuống mới hiện Cách 2, phần So sánh hiện dạng bảng 2
  hàng thu gọn.

## LMS `complete()`

- `items[]`: Cách 1 (thu gọn PT bậc hai, nghiệm, thử lại), Cách 2 (TH1, TH2 riêng biệt — ghi
  nhận nếu học sinh cố bỏ qua 1 trường hợp), So sánh (câu hỏi đối chất, không chấm đúng/sai).

## Critical Review

- Số liệu (|x+1|=2x−5, nghiệm x=6 hợp lệ, x=4/3 ngoại lai) đã kiểm chứng bằng code, cho kết
  quả đẹp để dạy song song cả 2 phương pháp.
- Module dạy CẢ 2 cách (bình phương + xét trường hợp) theo đúng tinh thần PPCT (I10 nêu xét
  trường hợp, tên bài yêu cầu quy về bậc hai) — cần giáo viên xác nhận có đồng ý dạy cả 2 hay
  chỉ cần 1 cách để đỡ nặng cho học sinh.
