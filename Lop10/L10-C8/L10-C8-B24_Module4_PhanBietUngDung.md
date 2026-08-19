# Module 4: Phân biệt và ứng dụng Hoán vị - Chỉnh hợp - Tổ hợp
### Bài 24 — Hoán vị, chỉnh hợp và tổ hợp | Toán 10, Chương VIII | Chủ đề 50

---

**Mục tiêu:** Học sinh phân biệt đúng khi nào dùng Hoán vị / Chỉnh hợp / Tổ hợp bằng sơ đồ quyết định 2 câu hỏi, và biết thêm kỹ thuật đếm phần bù cho bài toán có ràng buộc cấm.

**Sai lầm cần giải quyết:**
1. Không phân tích kỹ đề bài trước khi chọn công thức — đặc biệt nhầm khi đề dùng chữ "chọn" nhưng thực chất vẫn có phân vai trò (đúng là Chỉnh hợp, không phải Tổ hợp).
2. Bỏ sót điều kiện ràng buộc chéo (VD "2 bạn không đứng cạnh nhau") dẫn đến đếm thừa.

**Loại simulation:** Sơ đồ quyết định (chọn nhánh trước khi tính) cho 6 câu cơ bản + step-by-step có hướng dẫn cho 1 câu nâng cao (kỹ thuật phần bù).

**Thời gian hoàn thành dự kiến:** ~10 phút.

**Dạy từ đầu hay tổng kết:** Dạy từ đầu (kỹ năng phân biệt là hoàn toàn mới, dù công thức đã ôn ở M1-3) — cần Sổ tay kiến thức nền tảng.

---

## Sổ tay kiến thức nền tảng (hiện xuyên suốt module)

```
- Hoán vị: Pₙ = n!               (chọn TẤT CẢ, có thứ tự)
- Chỉnh hợp: Aⁿₖ = n!/(n-k)!     (chọn 1 phần, CÓ thứ tự)
- Tổ hợp: Cⁿₖ = n!/[(n-k)!k!]    (chọn 1 phần, KHÔNG thứ tự)

Sơ đồ quyết định:
  Câu hỏi 1: Chọn TẤT CẢ hay MỘT PHẦN?  → Tất cả → HOÁN VỊ
  Câu hỏi 2 (nếu 1 phần): Có phân biệt thứ tự/vai trò không?
    → Có → CHỈNH HỢP        → Không → TỔ HỢP
```

---

## 🖼️ Phác thảo canvas — "Bộ lọc phân loại"

Mỗi câu (1-6) dùng lại đúng 1 khối UI:

1. **Hộp Câu hỏi 1:** 2 nút lựa chọn `[ Tất cả ]` / `[ Một phần ]`.
   - Chọn "Tất cả" → ẩn hộp Câu hỏi 2, hiện ngay badge phân loại "Hoán vị".
   - Chọn "Một phần" → hiện tiếp hộp Câu hỏi 2.
2. **Hộp Câu hỏi 2** (chỉ hiện nếu Câu hỏi 1 = "Một phần"): 2 nút `[ Có thứ tự ]` / `[ Không thứ tự ]` → hiện badge "Chỉnh hợp" hoặc "Tổ hợp".
3. **Badge phân loại:** hiện tên loại + công thức tương ứng (kéo từ Sổ tay).
4. **Ô nhập kết quả số** + nút Kiểm tra, chỉ hiện sau khi có badge.

Áp dụng 3-strike ở CẢ 2 lớp: chọn sai nhánh (Câu hỏi 1/2) VÀ tính sai số — vì phân loại đúng chính là mục tiêu học của module này, không chỉ là bước phụ.

---

## 6 câu cơ bản (dùng bộ lọc phân loại)

| # | Bối cảnh | Đáp án nhánh | Đáp án số |
|---|---|---|---|
| 1 | Xếp 4 tiết mục văn nghệ vào thứ tự chương trình biểu diễn | Tất cả → Hoán vị | P₄ = 24 |
| 2 | Lớp 30 học sinh, chọn 3 bạn làm Trưởng ban, Thư ký, Thành viên (3 vai trò) | 1 phần, có thứ tự → Chỉnh hợp | A³⁰₃ = 24 360 |
| 3 | Từ 12 món trong menu, chọn 4 món cho set ăn thử (không phân biệt) | 1 phần, không thứ tự → Tổ hợp | C¹²₄ = 495 |
| 4 | Nhóm nhảy 6 thành viên xếp thành 1 hàng ngang để chụp ảnh | Tất cả → Hoán vị | P₆ = 720 |
| 5 | Cuộc thi vẽ 15 tác phẩm, chọn giải Nhất, Nhì, Ba (3 vị trí khác nhau) | 1 phần, có thứ tự → Chỉnh hợp | A¹⁵₃ = 2 730 |
| 6 | CLB 10 bạn, chọn 5 bạn đi hội trại (không phân vai trò) | 1 phần, không thứ tự → Tổ hợp | C¹⁰₅ = 252 |

### Trước mỗi bước tương tác (áp dụng cho mọi câu 1-6)

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| Câu hỏi 1 | "Đọc đề rồi chọn: bài toán này chọn TẤT CẢ phần tử, hay chỉ MỘT PHẦN?" | Nếu chọn hết và xếp thứ tự tất cả → Hoán vị. |
| Câu hỏi 2 | "Các phần tử được chọn có phân biệt vai trò/vị trí không?" | Có vai trò khác nhau → Chỉnh hợp; không phân biệt → Tổ hợp. |
| Tính kết quả | "Áp dụng đúng công thức của loại vừa chọn, nhập kết quả." | Dùng công thức tương ứng trong Sổ tay kiến thức. |

### Kịch bản dẫn dắt sai lầm (áp dụng cho câu 2, 3, 5, 6 — nơi dễ nhầm)

**Câu 2 (nhiều học sinh sẽ chọn "không thứ tự" vì thấy chữ "chọn 3 bạn"):**
- Lần sai 1: rung nhẹ.
- Lần sai 2: gợi ý — *"3 bạn được chọn có vai trò Trưởng ban / Thư ký / Thành viên khác nhau không? Nếu đổi 2 bạn giữa 2 vai trò, có tính là cách khác không?"*
- Lần sai 3: đáp án đúng — *"Đây là Chỉnh hợp, vì dù đề dùng chữ 'chọn', 3 bạn vẫn có 3 vai trò khác nhau — đổi vai trò giữa 2 bạn là ra 1 cách khác."*

**Câu 3, 6 (kiểm tra chiều ngược — không nhầm sang Chỉnh hợp):**
- Gợi ý khi sai: *"Nếu đổi vị trí 2 món/2 bạn đã chọn, có tính là cách khác không? Nếu không, đây không phải Chỉnh hợp."*

**Trả lời đúng (mọi câu):** giải thích ngắn nêu lại vì sao phân loại đó đúng (không chỉ "Chính xác!").

---

## Câu 7 (nâng cao) — Kỹ thuật đếm phần bù

**Bối cảnh:** Xếp 5 bạn thành 1 hàng để chụp ảnh, nhưng 2 bạn A và B không muốn đứng cạnh nhau. Hỏi có bao nhiêu cách xếp?

**Đáp án đúng:** P₅ − 2·P₄ = 120 − 48 = **72**.

**Thiết kế step-by-step (có hướng dẫn, vì đây là kỹ thuật hoàn toàn mới):**

1. Học sinh tự phân loại: đây vẫn là Hoán vị (chọn tất cả 5 bạn, có thứ tự) — dùng đúng bộ lọc phân loại như 6 câu trên.
2. Athena giới thiệu vấn đề: *"Nếu chỉ tính P₅ = 120, con số này có tính cả những cách mà A và B đứng cạnh nhau không? Đề bài lại cấm điều đó — vậy ta cần một kỹ thuật mới: đếm phần bù."*
3. Athena giải thích ngắn: *"Đếm phần bù: Số cách hợp lệ = Tổng số cách không ràng buộc − Số cách vi phạm ràng buộc."*
4. Hỏi (input): "Tổng số cách xếp 5 bạn không ràng buộc gì là bao nhiêu?" → đáp án 120 (học sinh đã biết từ bước phân loại).
5. Hỏi tiếp (input, có gợi ý hình ảnh 2 bạn A,B dính thành 1 khối): "Nếu coi A và B luôn đứng cạnh nhau như 1 khối duy nhất, ta còn phải xếp mấy 'đơn vị' thành 1 hàng?" → đáp án 4 (khối AB + 3 bạn còn lại).
6. Hỏi tiếp (input): "Mỗi cách xếp 4 đơn vị đó, khối AB có thể đổi chỗ A-B bên trong theo mấy cách?" → đáp án 2.
7. Hệ thống tự tính: số cách vi phạm = 4! × 2 = 48 (hiện phép tính, không cần học sinh gõ lại).
8. Hỏi cuối (input, 3-strike): "Vậy số cách xếp hợp lệ (A, B không cạnh nhau) là bao nhiêu?" → đáp án 120 − 48 = 72.

**3-strike ở bước cuối:**
- Lần sai 2: gợi ý — *"Số cách hợp lệ = Tổng không ràng buộc TRỪ số cách vi phạm — bạn đã có cả 2 số này ở các bước trước."*
- Lần sai 3: đáp án đúng kèm phép tính đầy đủ 120 − 48 = 72.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Câu 1-6 xếp dạng lưới 2 cột × 3 dòng, mỗi câu là 1 khối độc lập chứa đủ bộ lọc phân loại + ô nhập kết quả. Câu 7 đặt riêng full-width bên dưới, dạng step-by-step 8 bước hiện tuần tự (không khoá dần bằng sidebar — chỉ hiện bước tiếp theo ngay dưới bước vừa hoàn thành, cuộn dọc thường).

**Mobile (≤767px):** Câu 1-6 xếp dọc 1 cột theo đúng thứ tự. Câu 7 giữ nguyên 8 bước hiện tuần tự dọc — không cần pattern lướt ngang vì đây không phải nhiều thẻ bước cạnh 1 canvas cố định, mà là 1 mạch câu hỏi nối tiếp đơn giản.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Chọn nhánh (Câu hỏi 1/2) | Click 1 trong 2 nút | Chạm 1 trong 2 nút ≥44px |
| Nhập kết quả số | Gõ bàn phím, click Kiểm tra | Chạm ô input `inputmode="numeric"`, chạm nút Kiểm tra ≥44px |
| Xem lại Sổ tay kiến thức | Click icon cố định góc màn hình | Chạm icon, mở dạng bottom-sheet |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm4_c1', type: 'answered', required: true },
  { id: 'm4_c2', type: 'answered', required: true },
  { id: 'm4_c3', type: 'answered', required: true },
  { id: 'm4_c4', type: 'answered', required: true },
  { id: 'm4_c5', type: 'answered', required: true },
  { id: 'm4_c6', type: 'answered', required: true },
  { id: 'm4_c7', type: 'answered', required: true }
]
```
`progress total = 7`.

### `athenaGuidance` (nguyên văn, khớp đúng 7 mục)
```
1-6. m4_c1..c6: gợi ý lần sai thứ 2 luôn dùng đúng dạng câu hỏi ngược
   "Nếu đổi chỗ/đổi vai trò 2 phần tử đã chọn, có tính là cách khác
   không?" — điều chỉnh theo đúng bối cảnh câu hỏi, không nói thẳng
   loại đúng (Hoán vị/Chỉnh hợp/Tổ hợp) ở gợi ý này.
7. m4_c7: mỗi bước con (4 bước nhập số) chỉ xác nhận đúng/sai đơn giản,
   trừ bước cuối cùng dùng gợi ý "Số cách hợp lệ = Tổng không ràng buộc
   TRỪ số cách vi phạm" — không tính hộ con số cuối.
```

---

## Tổng kết kiến thức

### Bảng dấu hiệu nhận biết

| | Hoán vị | Chỉnh hợp | Tổ hợp |
|---|---|---|---|
| **Chọn bao nhiêu?** | Tất cả (k = n) | Một phần (k < n) | Một phần (k < n) |
| **Có thứ tự/vai trò?** | Có | Có | Không |
| **Tình huống hay gặp** | Xếp tất cả thành 1 hàng/1 dãy (chụp ảnh, biểu diễn, xếp đủ chỗ) | Chọn ra rồi gắn vai trò/vị trí cụ thể khác nhau (giải Nhất-Nhì-Ba, Trưởng-Phó-Thư ký) | Chọn ra một nhóm/tập con, không phân vai trò (lập ban không chức danh, chọn nhóm làm việc chung) |
| **Từ khoá tín hiệu** | "xếp tất cả", "sắp thứ tự cả nhóm" | "chọn... rồi phân công", "vị trí 1-2-3", "giải Nhất/Nhì/Ba" | "chọn ra một nhóm", "lập một đội/ban" (không nêu chức danh riêng) |
| **Câu tự kiểm tra** | Đổi chỗ 2 phần tử — có ra cách khác không? (Có → Hoán vị) | Đổi vai trò 2 người đã chọn — có tính là cách khác không? (Có → Chỉnh hợp) | Đổi vai trò 2 người đã chọn — có tính là cách khác không? (Không → Tổ hợp) |

> ⚠️ **Lưu ý quan trọng nhất:** đề bài dùng từ "chọn" KHÔNG đồng nghĩa với Tổ hợp — luôn kiểm tra tiếp xem "chọn ra" đó có đi kèm phân vai trò/vị trí khác nhau hay không (nếu có → vẫn là Chỉnh hợp).

### Kỹ thuật đếm phần bù

> Khi bài toán có một điều kiện CẤM (ví dụ: "hai bạn A và B không được đứng cạnh nhau"), cách tính trực tiếp thường rất khó vì phải loại trừ rất nhiều trường hợp. Thay vào đó, ta tính theo hướng ngược lại — dễ hơn nhiều: **Số cách xếp hợp lệ = Tổng số cách xếp KHÔNG có điều kiện gì − Số cách xếp mà điều bị cấm đó vẫn xảy ra.**
>
> Để tính "số cách xếp mà điều bị cấm đó vẫn xảy ra" (ở đây là A và B đứng cạnh nhau), ta coi A và B như dính chặt thành một khối duy nhất, rồi xếp khối đó cùng với các phần tử còn lại — sau đó nhân thêm với số cách A và B có thể đổi chỗ nhau bên trong khối (A trước B, hoặc B trước A).
