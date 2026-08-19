# Module 2: Chỉnh hợp (Tổng kết nhanh)
### Bài 24 — Hoán vị, chỉnh hợp và tổ hợp | Toán 10, Chương VIII | Chủ đề 50

---

**Mục tiêu:** Học sinh nhớ và áp dụng thành thạo công thức chỉnh hợp Aⁿₖ = n!/(n-k)!, phân biệt được với hoán vị (Module 1) qua nhiều ví dụ quen thuộc.

**Dạy từ đầu hay tổng kết:** **Tổng kết nhanh — đã dạy qua video Manim.**

**Loại simulation:** Luyện tập song song (4 câu hiện cùng lúc) + drill bấm máy tính cầm tay.

**Thời gian hoàn thành dự kiến:** ~3 phút.

---

## Nội dung hiển thị

**1. Thẻ công thức (cố định phía trên):**
```
Chỉnh hợp chập k của n: Aⁿₖ = n·(n-1)···(n-k+1) = n! / (n-k)!   (1 ≤ k ≤ n)
Phân biệt với hoán vị: chỉnh hợp CHỌN k trong n phần tử rồi XẾP THỨ TỰ
(hoán vị là trường hợp đặc biệt khi k = n: Pₙ = Aⁿₙ)
```

**2. Drill nhớ trình tự bấm máy tính cầm tay** (tái dùng đúng cơ chế Symbol pad — xem `02_design_toan_final.md` PHẦN 1.3c, không phải bàn phím đầy đủ):
- Đề bài mẫu: "Tính A⁹₃". 1 ô nhập text + hàng nút nhỏ cạnh ô input: `SHIFT`, `nPr`, `=` — bấm nút để chèn token vào ô, hoặc học sinh tự gõ tay.
- Học sinh cần gõ/chèn đủ đúng trình tự: `9 SHIFT nPr 3 =`.
- Cơ chế phản hồi giống Module 1 (không chặn, gợi ý ngắn nếu sai/thiếu token).

**3. Bốn câu luyện tập (hiện cùng lúc, mỗi câu 1 ô nhập + nút Kiểm tra riêng):**

| # | Câu | Đáp án |
|---|---|---|
| 1 | Từ 6 bạn trong lớp, chọn 3 bạn làm lớp trưởng, lớp phó, thư ký (3 vai trò khác nhau) | A⁶₃ = 120 |
| 2 | Một cửa hàng có 8 mẫu áo, chọn 3 mẫu trưng bày ở vị trí 1, 2, 3 trên tủ kính | A⁸₃ = 336 |
| 3 | Từ 5 vận động viên, chọn 2 người nhận huy chương Vàng và Bạc | A⁵₂ = 20 |
| 4 | Một lớp có 7 bạn đăng ký thi hát, ban tổ chức chọn 4 bạn xếp thứ tự biểu diễn 1-2-3-4 | A⁷₄ = 840 |

**Phản hồi mỗi câu:**
- Sai: gợi ý — *"Nhớ lại: Aⁿₖ = n!/(n-k)!. Ở đây n và k là bao nhiêu? Đề bài có xếp thứ tự các đối tượng được chọn không?"*
- Đúng: giải thích ngắn — VD Câu 1: *"Đúng! A⁶₃ = 6!/3! = 120, vì 3 vai trò lớp trưởng/lớp phó/thư ký là có thứ tự (phân biệt vai trò), không phải chọn ngẫu nhiên 3 bạn."*

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Thẻ công thức trên cùng → drill nhớ trình tự căn giữa (ô nhập + hàng nút nhỏ) → 4 câu luyện dạng lưới 2×2.

**Mobile (≤767px):** Xếp dọc: thẻ công thức → drill nhớ trình tự (ô nhập + hàng nút nhỏ, vùng chạm ≥32px như symbol pad) → 4 câu luyện 1 cột. Không cần lướt ngang.

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm2_may_tinh',  type: 'explored', required: true },
  { id: 'm2_cau1',      type: 'answered', required: true },
  { id: 'm2_cau2',      type: 'answered', required: true },
  { id: 'm2_cau3',      type: 'answered', required: true },
  { id: 'm2_cau4',      type: 'answered', required: true }
]
```
`progress total = 5`.

### `athenaGuidance`
```
1. m2_may_tinh: chỉ nhắc đúng trình tự phím, không bấm hộ.
2-5. m2_cau1..4: gợi ý CHỈ nhắc lại công thức và hỏi ngược "đề bài có
   yêu cầu xếp thứ tự các đối tượng được chọn không?" — không tính hộ.
```

---

## Tổng kết kiến thức

> **Chỉnh hợp chập k của n** là một cách chọn k phần tử từ n phần tử và **sắp xếp chúng theo thứ tự**. Số các chỉnh hợp: **Aⁿₖ = n!/(n-k)!** (1 ≤ k ≤ n).
>
> Dấu hiệu nhận biết: đề bài chọn **một phần** trong tập hợp (k < n), và các phần tử được chọn có **vai trò/vị trí khác nhau** (có thứ tự). Nếu chọn hết tất cả (k = n), chỉnh hợp trở thành hoán vị: Pₙ = Aⁿₙ.
