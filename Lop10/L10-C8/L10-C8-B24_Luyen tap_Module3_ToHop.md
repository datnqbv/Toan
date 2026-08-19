# Module 3: Tổ hợp (Tổng kết nhanh)
### Bài 24 — Hoán vị, chỉnh hợp và tổ hợp | Toán 10, Chương VIII | Chủ đề 50

---

**Mục tiêu:** Học sinh nhớ và áp dụng thành thạo công thức tổ hợp Cⁿₖ = n!/[(n-k)!k!], phân biệt được với chỉnh hợp (Module 2) qua nhiều ví dụ quen thuộc.

**Dạy từ đầu hay tổng kết:** **Tổng kết nhanh — đã dạy qua video Manim.**

**Loại simulation:** Luyện tập song song (4 câu hiện cùng lúc) + drill bấm máy tính cầm tay.

**Thời gian hoàn thành dự kiến:** ~3 phút.

---

## Nội dung hiển thị

**1. Thẻ công thức (cố định phía trên):**
```
Tổ hợp chập k của n: Cⁿₖ = n! / [(n-k)! · k!] = Aⁿₖ / k!   (0 ≤ k ≤ n)
Phân biệt với chỉnh hợp: tổ hợp CHỌN k trong n phần tử, KHÔNG xếp thứ tự
```

**2. Drill nhớ trình tự bấm máy tính cầm tay** (tái dùng đúng cơ chế Symbol pad — xem `02_design_toan_final.md` PHẦN 1.3c, không phải bàn phím đầy đủ):
- Đề bài mẫu: "Tính C₁₀₄". 1 ô nhập text + hàng nút nhỏ cạnh ô input: `SHIFT`, `nCr`, `=` — bấm nút để chèn token vào ô, hoặc học sinh tự gõ tay.
- Học sinh cần gõ/chèn đủ đúng trình tự: `10 SHIFT nCr 4 =`.
- Cơ chế phản hồi giống Module 1, 2 (không chặn, gợi ý ngắn nếu sai/thiếu token).

**3. Bốn câu luyện tập (hiện cùng lúc, mỗi câu 1 ô nhập + nút Kiểm tra riêng):**

| # | Câu | Đáp án |
|---|---|---|
| 1 | Một nhóm có 8 bạn, chọn 3 bạn để lập nhóm dự án (không phân vai trò) | C⁸₃ = 56 |
| 2 | Hộp có 10 viên kẹo khác vị, lấy 4 viên chia cho 1 bạn (không quan tâm thứ tự) | C¹⁰₄ = 210 |
| 3 | Thư viện có 12 đầu sách mới, chọn 5 đầu để giới thiệu trong tuần | C¹²₅ = 792 |
| 4 | Từ 9 bông hoa khác màu, chọn 4 bông để cắm vào 1 bình | C⁹₄ = 126 |

**Phản hồi mỗi câu:**
- Sai: gợi ý — *"Nhớ lại: Cⁿₖ = n!/[(n-k)!k!]. Đề bài có phân biệt thứ tự/vai trò giữa các đối tượng được chọn không?"*
- Đúng: giải thích ngắn — VD Câu 1: *"Đúng! C⁸₃ = 8!/(5!·3!) = 56, vì 3 bạn trong nhóm dự án không có vai trò phân biệt — chỉ cần chọn ra, không xếp thứ tự."*

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Thẻ công thức trên cùng → drill nhớ trình tự căn giữa (ô nhập + hàng nút nhỏ) → 4 câu luyện dạng lưới 2×2.

**Mobile (≤767px):** Xếp dọc: thẻ công thức → drill nhớ trình tự (ô nhập + hàng nút nhỏ, vùng chạm ≥32px như symbol pad) → 4 câu luyện 1 cột. Không cần lướt ngang.

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm3_may_tinh',  type: 'explored', required: true },
  { id: 'm3_cau1',      type: 'answered', required: true },
  { id: 'm3_cau2',      type: 'answered', required: true },
  { id: 'm3_cau3',      type: 'answered', required: true },
  { id: 'm3_cau4',      type: 'answered', required: true }
]
```
`progress total = 5`.

### `athenaGuidance`
```
1. m3_may_tinh: chỉ nhắc đúng trình tự phím, không bấm hộ.
2-5. m3_cau1..4: gợi ý CHỈ nhắc lại công thức và hỏi ngược "các đối
   tượng được chọn có phân biệt vai trò/thứ tự không?" — không tính hộ.
```

---

## Tổng kết kiến thức

> **Tổ hợp chập k của n** là một cách **chọn** k phần tử từ n phần tử, **không** quan tâm thứ tự. Số các tổ hợp: **Cⁿₖ = n!/[(n-k)!k!]** (0 ≤ k ≤ n).
>
> Dấu hiệu nhận biết: đề bài chỉ yêu cầu **chọn ra** một nhóm, các phần tử được chọn **không có vai trò/vị trí khác nhau**.
>
> **Bảng phân biệt nhanh 3 công thức (Module 1-3):**
> | | Chọn tất cả hay 1 phần? | Có xếp thứ tự? | Công thức |
> |---|---|---|---|
> | Hoán vị | Tất cả (k = n) | Có | Pₙ = n! |
> | Chỉnh hợp | 1 phần (k < n) | Có | Aⁿₖ = n!/(n-k)! |
> | Tổ hợp | 1 phần (k < n) | Không | Cⁿₖ = n!/[(n-k)!k!] |
