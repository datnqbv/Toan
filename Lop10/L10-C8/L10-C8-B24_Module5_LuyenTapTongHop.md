# Module 5: Luyện tập tổng hợp
### Bài 24 — Hoán vị, chỉnh hợp và tổ hợp | Toán 10, Chương VIII | Chủ đề 50

---

**Mục tiêu:** Học sinh vận dụng linh hoạt Hoán vị/Chỉnh hợp/Tổ hợp trong bài toán phối hợp nhiều bước (kết hợp với quy tắc cộng/nhân đã học ở Bài 23), qua 5 bối cảnh đa dạng.

**Sai lầm cần giải quyết:** Không phân tích bài toán phức hợp thành từng phần nhỏ trước khi chọn công thức; lẫn lộn Hoán vị/Chỉnh hợp/Tổ hợp trong bài toán thực tế nhiều lớp.

**Loại simulation:** Luyện tập tổng hợp — câu đơn dùng bộ lọc phân loại (như Module 4), câu phối hợp dùng "2 quầy tính riêng rồi kết hợp" (như Module 4, Bài 23).

**Thời gian hoàn thành dự kiến:** ~12 phút (5 câu).

**Dạy từ đầu hay tổng kết:** Luyện tập — không hình thành khái niệm mới, trừ kỹ thuật "buộc khối" ở Câu 4 (giới thiệu ngắn trước khi vào câu).

---

## Sổ tay kiến thức nền tảng (rút gọn, không lặp lại toàn bảng của Module 4)

```
- Hoán vị: Pₙ = n!            — xếp tất cả, có thứ tự
- Chỉnh hợp: Aⁿₖ = n!/(n-k)!  — chọn 1 phần, gắn vai trò/vị trí khác nhau
- Tổ hợp: Cⁿₖ = n!/[(n-k)!k!] — chọn 1 phần, không phân vai trò
- Quy tắc cộng (Bài 23): phương án rời nhau → cộng
- Quy tắc nhân (Bài 23): công đoạn nối tiếp, độc lập → nhân
- Kỹ thuật phần bù (Module 4): ràng buộc CẤM → Tổng không ràng buộc − Vi phạm
- Kỹ thuật buộc khối (mới ở Câu 4): ràng buộc PHẢI cạnh nhau → coi là 1 khối,
  hoán vị khối + các phần tử còn lại, rồi nhân với hoán vị nội khối
```

---

## 5 câu luyện tập

| # | Bối cảnh | Kỹ năng phối hợp | Đáp án |
|---|---|---|---|
| 1 | Từ 7 chữ số {1,3,5,6,7,8,9}, lập số có 4 chữ số khác nhau | Chỉnh hợp thuần | A⁷₄ = 840 |
| 2 | Cửa hàng chọn 3 nhân viên trực cuối tuần từ 8 người: 1 ca trưởng + 2 phụ (không phân biệt 2 phụ) | Chọn có vai trò × chọn không vai trò (quy tắc nhân) | 8 × C⁷₂ = 168 |
| 3 | Ban nhạc chọn 4 bạn: 2 chơi nhạc cụ dây (từ 6 bạn) + 2 chơi nhạc cụ hơi (từ 5 bạn) | Tổ hợp × Tổ hợp (quy tắc nhân) | C⁶₂ × C⁵₂ = 150 |
| 4 | Xếp 6 cuốn sách lên giá thành 1 hàng, 2 cuốn từ điển phải đứng cạnh nhau | Hoán vị + kỹ thuật buộc khối | 2! × 5! = 240 |
| 5 | Từ 20 học sinh, chọn ban cán sự 3 vai trò khác nhau, sau đó chọn thêm 2 thành viên ban thi đua (không vai trò) từ 17 bạn còn lại | Chỉnh hợp × Tổ hợp (quy tắc nhân) | A²⁰₃ × C¹⁷₂ = 930 240 |

### Trước mỗi câu — hướng dẫn thao tác

| Câu | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | "Dùng bộ lọc phân loại để xác định loại, rồi nhập kết quả." | Đây là 1 công đoạn duy nhất — không cần phối hợp quy tắc cộng/nhân. |
| 2 | "Tính riêng số cách chọn ca trưởng, rồi số cách chọn 2 phụ, sau đó ghép lại." | Ca trưởng là 1 vị trí có vai trò (chọn trực tiếp trong 8), 2 phụ không phân vai trò (Tổ hợp trong 7 người còn lại) — 2 công đoạn nối tiếp, dùng quy tắc nhân. |
| 3 | "Tính riêng số cách chọn 2 bạn nhạc cụ dây và 2 bạn nhạc cụ hơi, rồi ghép lại." | Cả 2 nhóm đều không phân vai trò (Tổ hợp), 2 lựa chọn độc lập — dùng quy tắc nhân. |
| 4 | "Đọc phần Athena giới thiệu kỹ thuật buộc khối trước, rồi làm theo từng bước." | Coi 2 cuốn từ điển là 1 khối duy nhất, xếp khối + 4 cuốn còn lại, rồi nhân với số cách đổi chỗ trong khối. |
| 5 | "Tính riêng số cách chọn ban cán sự (có vai trò) và ban thi đua (không vai trò), rồi ghép lại." | Ban cán sự là Chỉnh hợp (3 vai trò trong 20 bạn), ban thi đua là Tổ hợp (2 người không vai trò, chọn từ 17 bạn còn lại sau khi đã chọn ban cán sự) — dùng quy tắc nhân. |

---

## Kịch bản dẫn dắt sai lầm

**Câu 2, 3, 5 (bẫy chính: quên nhân 2 kết quả, hoặc chọn nhầm loại ở 1 trong 2 phần):**
- Mỗi phần (VD "ca trưởng", "2 phụ") có bộ lọc phân loại + ô nhập riêng, giống Module 4 Bài 23.
- Sau khi có 2 kết quả riêng, hỏi tiếp: "Ghép 2 kết quả này lại bằng quy tắc gì?" (Cộng / Nhân) — 3-strike nếu chọn Cộng nhầm:
  - Lần sai 2: gợi ý — *"2 việc này có làm nối tiếp nhau và độc lập với nhau không? Đây có phải 2 phương án tách biệt (chỉ chọn 1 trong 2) không?"*
  - Lần sai 3: đáp án đúng kèm giải thích dùng quy tắc nhân vì đây là 2 công đoạn nối tiếp.

**Câu 4 — giới thiệu kỹ thuật buộc khối (step-by-step có hướng dẫn):**

> Athena: "2 cuốn từ điển phải luôn đứng cạnh nhau — ta dùng kỹ thuật buộc khối: coi 2 cuốn đó là 1 khối duy nhất, rồi xếp khối này cùng các cuốn còn lại."

1. Hỏi (input): "Nếu coi 2 cuốn từ điển là 1 khối, ta còn phải xếp mấy 'đơn vị' thành 1 hàng?" → đáp án 5 (khối + 4 cuốn còn lại).
2. Hỏi (input): "Số cách xếp 5 đơn vị đó thành 1 hàng là bao nhiêu?" → đáp án 5! = 120.
3. Hỏi (input): "Trong khối, 2 cuốn từ điển có thể đổi chỗ nhau theo mấy cách?" → đáp án 2! = 2.
4. Hỏi cuối (input, 3-strike): "Vậy tổng số cách xếp thoả điều kiện là bao nhiêu?" → 120 × 2 = 240.
   - Lần sai 2: gợi ý — *"Nhân số cách xếp 5 đơn vị với số cách đổi chỗ trong khối."*
   - Lần sai 3: đáp án đúng kèm phép tính 5! × 2! = 240.

---

## Athena tổng kết toàn Bài 24 (sau khi hoàn thành đủ 5 câu)

> Athena: "Qua Bài 24, bạn đã học 3 công cụ đếm: Hoán vị (xếp tất cả), Chỉnh hợp (chọn và xếp thứ tự một phần), Tổ hợp (chỉ chọn, không thứ tự). Chìa khoá để không nhầm là luôn tự hỏi 2 câu: chọn tất cả hay một phần, và có phân biệt thứ tự/vai trò không? Với bài toán phức tạp hơn, bạn còn có kỹ thuật phần bù (khi có ràng buộc cấm) và kỹ thuật buộc khối (khi có ràng buộc phải cạnh nhau)."

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Mỗi câu là 1 khối full-width, xếp dọc Câu 1 → Câu 5. Câu 2, 3, 5 có 2 khối con cạnh nhau (2 quầy tính riêng) + 1 khối "Kết hợp kết quả" full-width ngay dưới, giống layout Module 4 Bài 23. Câu 4 hiện tuần tự 4 bước dọc trong 1 khối.

**Mobile (≤767px):** Giữ đúng thứ tự dọc; ở Câu 2, 3, 5 thì 2 khối con xếp chồng dọc thay vì cạnh nhau. Không cần pattern lướt ngang — không có canvas cố định bị cuộn mất, mỗi câu/mỗi khối con độc lập về nội dung.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Chọn nhánh phân loại | Click 1 trong 2 nút | Chạm 1 trong 2 nút ≥44px |
| Chọn quy tắc kết hợp (Cộng/Nhân) | Click 1 trong 2 nút | Chạm 1 trong 2 nút ≥44px |
| Nhập kết quả số (mọi bước) | Gõ bàn phím, click Kiểm tra | Chạm ô input `inputmode="numeric"`, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm5_cau1',        type: 'answered', required: true },
  { id: 'm5_cau2_p1',     type: 'answered', required: true },
  { id: 'm5_cau2_p2',     type: 'answered', required: true },
  { id: 'm5_cau2_kethop', type: 'answered', required: true },
  { id: 'm5_cau3_p1',     type: 'answered', required: true },
  { id: 'm5_cau3_p2',     type: 'answered', required: true },
  { id: 'm5_cau3_kethop', type: 'answered', required: true },
  { id: 'm5_cau4',        type: 'answered', required: true },
  { id: 'm5_cau5_p1',     type: 'answered', required: true },
  { id: 'm5_cau5_p2',     type: 'answered', required: true },
  { id: 'm5_cau5_kethop', type: 'answered', required: true }
]
```
`progress total = 11`.

### `athenaGuidance` (nguyên văn, khớp đúng 11 mục)
```
1. m5_cau1: gợi ý dùng đúng sơ đồ quyết định 2 câu hỏi đã học ở Module 4
   — không nói thẳng đáp án 840.
2-3. m5_cau2_p1/p2, m5_cau3_p1/p2, m5_cau5_p1/p2: mỗi phần chỉ xác nhận
   đúng/sai đơn giản theo công thức tương ứng, không gợi ý phức tạp.
4. m5_cau2_kethop, m5_cau3_kethop, m5_cau5_kethop: gợi ý lần sai thứ 2
   CHỈ dùng đúng câu: "2 việc này có làm nối tiếp nhau và độc lập với
   nhau không? Đây có phải 2 phương án tách biệt (chỉ chọn 1 trong 2)
   không?" — không nói thẳng đáp án cuối.
5. m5_cau4: mỗi bước con (4 bước) chỉ xác nhận đúng/sai đơn giản, trừ
   bước cuối dùng gợi ý "Nhân số cách xếp 5 đơn vị với số cách đổi chỗ
   trong khối" — không tính hộ con số cuối.
```

---

## Tổng kết kiến thức (tổng kết toàn Bài 24)

> **Ba công cụ đếm đã học:**
> - **Hoán vị** dùng khi ta sắp xếp TẤT CẢ các phần tử của một tập hợp theo một thứ tự nào đó. Số cách sắp xếp là Pₙ = n!.
> - **Chỉnh hợp** dùng khi ta chọn ra MỘT PHẦN các phần tử, và các phần tử được chọn có vai trò hoặc vị trí khác nhau (có thứ tự). Số cách chọn là Aⁿₖ = n!/(n-k)!.
> - **Tổ hợp** dùng khi ta chọn ra MỘT PHẦN các phần tử, nhưng không phân biệt vai trò hay vị trí giữa chúng (không có thứ tự). Số cách chọn là Cⁿₖ = n!/[(n-k)!k!].
>
> **Với bài toán phức hợp** (gồm nhiều yêu cầu nhỏ trong cùng 1 đề bài): trước tiên hãy chia bài toán thành từng phần nhỏ, xác định đúng công cụ cần dùng cho mỗi phần (Hoán vị, Chỉnh hợp, hay Tổ hợp), tính riêng từng phần, sau đó ghép các kết quả lại bằng quy tắc cộng hoặc quy tắc nhân đã học ở Bài 23.
>
> **Khi đề bài có điều kiện "không được đứng cạnh nhau"** (một ràng buộc CẤM), ta dùng **kỹ thuật đếm phần bù**: tính tổng số cách sắp xếp khi không có ràng buộc gì, sau đó trừ đi số cách sắp xếp mà điều bị cấm đó vẫn xảy ra. Ví dụ: số cách xếp sao cho A và B không đứng cạnh nhau = tổng số cách xếp không ràng buộc − số cách xếp mà A và B đứng cạnh nhau.
>
> **Khi đề bài có điều kiện "phải luôn đứng cạnh nhau"** (một ràng buộc BẮT BUỘC), ta dùng **kỹ thuật buộc khối**: coi hai phần tử luôn phải đứng cạnh nhau đó như một "khối" duy nhất (dính chặt với nhau), rồi sắp xếp khối này cùng với các phần tử còn lại như bình thường. Vì bên trong khối, hai phần tử vẫn có thể đổi chỗ cho nhau (A đứng trước B, hoặc B đứng trước A), nên cuối cùng phải nhân thêm với số cách đổi chỗ đó (thường là 2! = 2 nếu khối chỉ gồm 2 phần tử).
