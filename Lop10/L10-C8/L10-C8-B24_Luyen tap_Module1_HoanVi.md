# Module 1: Hoán vị (Tổng kết nhanh)
### Bài 24 — Hoán vị, chỉnh hợp và tổ hợp | Toán 10, Chương VIII | Chủ đề 50

---

**Mục tiêu:** Học sinh nhớ và áp dụng thành thạo công thức hoán vị Pₙ = n! qua nhiều ví dụ quen thuộc, kèm luyện bấm máy tính cầm tay.

**Dạy từ đầu hay tổng kết:** **Tổng kết nhanh — đã dạy qua video Manim.** Module này KHÔNG dạy lại khái niệm từ đầu, chỉ ôn công thức + luyện áp dụng.

**Loại simulation:** Luyện tập song song (4 câu hiện cùng lúc, không khoá dần) + drill bấm máy tính cầm tay.

**Thời gian hoàn thành dự kiến:** ~3 phút.

---

## Nội dung hiển thị

**1. Thẻ công thức (cố định phía trên, luôn hiện):**
```
Hoán vị của n phần tử: Pₙ = n · (n-1) · (n-2) ··· 2 · 1 = n!
Quy ước: 0! = 1
```

**2. Drill nhớ trình tự bấm máy tính cầm tay** (tái dùng đúng cơ chế Symbol pad — xem `02_design_toan_final.md` PHẦN 1.3c, không phải bàn phím đầy đủ):
- Đề bài mẫu: "Tính 6!". 1 ô nhập text + hàng nút nhỏ cạnh ô input: `SHIFT`, `x!`, `=` — bấm nút để chèn token vào ô, hoặc học sinh có thể tự gõ tay.
- Học sinh cần gõ/chèn đủ đúng trình tự: `6 SHIFT x! =`.
- Gõ thiếu/sai thứ tự: không chặn, chỉ hiện gợi ý ngắn dưới ô — *"Bạn thử nhớ lại: cần bấm SHIFT trước khi bấm x! không?"*
- Gõ đúng trình tự (chấm bằng so sánh chuỗi đã chuẩn hoá, không phân biệt hoa/thường): hiện kết quả 720 + dòng xác nhận ngắn.

**3. Bốn câu luyện tập (hiện cùng lúc, không khoá dần — mỗi câu có ô nhập riêng + nút Kiểm tra riêng):**

| # | Câu | Đáp án |
|---|---|---|
| 1 | Có bao nhiêu cách xếp 5 cuốn sách khác nhau lên 1 giá sách? | P₅ = 120 |
| 2 | Có bao nhiêu cách xếp 4 chiếc cúp thành 1 hàng trên tủ trưng bày của lớp? | P₄ = 24 |
| 3 | Có bao nhiêu cách xếp 6 chậu hoa khác loại thành 1 hàng trước cổng trường? | P₆ = 720 |
| 4 | Có bao nhiêu cách xếp 3 lá thư vào 3 hộp thư đánh số khác nhau? | P₃ = 6 |

**Phản hồi mỗi câu (đơn giản, không cần 3-strike đầy đủ):**
- Sai: hiện gợi ý ngắn nhắc lại công thức — *"Nhớ lại: Pₙ = n!. Ở đây n bằng bao nhiêu?"*
- Đúng: giải thích ngắn — VD Câu 1: *"Đúng! P₅ = 5! = 5×4×3×2×1 = 120, vì xếp 5 vật khác nhau vào 5 vị trí là 1 hoán vị của 5 phần tử."*

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Thẻ công thức trên cùng (full-width, nhỏ gọn). Ngay dưới: drill nhớ trình tự (căn giữa, ô nhập + hàng nút nhỏ). Dưới cùng: 4 câu luyện xếp dạng lưới 2×2.

**Mobile (≤767px):** Giữ đúng thứ tự dọc: thẻ công thức → drill nhớ trình tự (ô nhập + hàng nút nhỏ, vùng chạm ≥32px như symbol pad) → 4 câu luyện xếp dọc 1 cột. Không cần pattern lướt ngang vì không có canvas cố định bị cuộn mất (mỗi câu độc lập).

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm1_may_tinh',  type: 'explored', required: true },
  { id: 'm1_cau1',      type: 'answered', required: true },
  { id: 'm1_cau2',      type: 'answered', required: true },
  { id: 'm1_cau3',      type: 'answered', required: true },
  { id: 'm1_cau4',      type: 'answered', required: true }
]
```
`progress total = 5`.

### `athenaGuidance`
```
1. m1_may_tinh: chỉ nhắc đúng trình tự phím (số → SHIFT → x! → =),
   không bấm hộ học sinh.
2-5. m1_cau1..4: gợi ý CHỈ nhắc lại công thức Pₙ = n! và hỏi ngược
   "n ở đây là bao nhiêu?" — không tính hộ đáp án.
```

---

## Tổng kết kiến thức

> **Hoán vị của n phần tử** là một cách sắp xếp có thứ tự n phần tử đó. Số các hoán vị của n phần tử: **Pₙ = n! = n·(n-1)·(n-2)···2·1** (quy ước 0! = 1).
>
> Dấu hiệu nhận biết: đề bài yêu cầu sắp xếp **TẤT CẢ** các phần tử của một tập hợp theo thứ tự (không chọn ra một phần).
