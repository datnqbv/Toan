# Module 4: Tổng hợp và luyện tập — Chọn đúng phương pháp
### Bài 27 — Thực hành tính xác suất theo định nghĩa cổ điển | Toán 10, Chương IX | Chủ đề 55

---

**Mục tiêu:** Học sinh phân biệt được khi nào nên dùng phương pháp tổ hợp, khi nào nên dùng sơ đồ hình cây, và khi nào nên kết hợp thêm chiến thuật biến cố đối — trước khi bắt tay tính toán.

**Sai lầm cần giải quyết:** Chọn sai phương pháp đếm ngay từ đầu (dùng cây cho bài toán chọn nhóm đơn giản khiến rối, hoặc dùng tổ hợp cho bài có nhiều công đoạn khiến thiếu sót); không nhận ra có thể kết hợp thêm biến cố đối để đơn giản hoá.

**Loại simulation:** Sơ đồ quyết định 2 lớp (chọn phương pháp đếm → xét có cần biến cố đối không) — tái dùng đúng mô hình "bộ lọc phân loại" đã dùng ở Bài 24 Module 4.

**Thời gian hoàn thành dự kiến:** ~14 phút.

**Dạy từ đầu hay tổng kết:** Tổng hợp — không hình thành khái niệm mới, dùng lại toàn bộ kỹ thuật của Module 1-3 — cần Sổ tay kiến thức nền tảng.

---

## Sổ tay kiến thức nền tảng — Bảng phân biệt 3 phương pháp

| | Phương pháp tổ hợp | Sơ đồ hình cây | Biến cố đối (chiến thuật bổ trợ) |
|---|---|---|---|
| **Dùng khi** | Phép thử là "chọn ra 1 nhóm k phần tử" cùng lúc từ 1 hoặc vài tập hợp có sẵn | Phép thử gồm NHIỀU công đoạn/bước liên tiếp, mỗi bước có các lựa chọn riêng | Áp dụng THÊM vào 1 trong 2 cách trên, khi tính trực tiếp phức tạp |
| **Từ khoá tín hiệu** | "chọn ra", "lấy ra đồng thời k viên/k người" | "rút từ mỗi hộp", "tung/gieo liên tiếp", "quay lần lượt" | "ít nhất", "có ít nhất 1" |
| **Công thức** | n(Ω), n(E) tính bằng Cⁿₖ (kết hợp quy tắc nhân nếu có nhiều điều kiện) | n(Ω) = tổng số lá cây; n(E) = số lá thoả biến cố | P(E) = 1 − P(Ē) |
| **Câu tự kiểm tra** | Các phần tử được chọn có phân biệt "bước 1, bước 2..." không, hay chỉ là 1 nhóm duy nhất? | Có thể tách phép thử thành các bước rõ ràng, mỗi bước 1 tầng của cây không? | Nếu tính "không có... nào cả" thì có ít trường hợp hơn tính trực tiếp không? |

⚠️ **Lưu ý quan trọng:** Tổ hợp và sơ đồ hình cây là 2 cách THAY THẾ nhau (chọn 1 trong 2 tuỳ cấu trúc bài toán), còn biến cố đối là 1 chiến thuật có thể DÙNG THÊM vào bất kỳ cách nào ở trên — không phải phương pháp thứ 3 độc lập.

---

## 🖼️ Phác thảo canvas — "Bộ lọc chọn phương pháp" (tái dùng mô hình Bài 24 Module 4)

Mỗi câu luyện tập dùng lại đúng 1 khối UI:

1. **Câu hỏi 1:** *"Phép thử này là chọn ra 1 nhóm cùng lúc, hay có nhiều công đoạn liên tiếp?"* → 2 nút `[ Chọn nhóm — dùng Tổ hợp ]` / `[ Nhiều công đoạn — dùng Sơ đồ cây ]`.
2. **Câu hỏi 2** (luôn hỏi, không phụ thuộc câu 1): *"Đề bài có từ 'ít nhất' không? Nếu có, tính biến cố đối có dễ hơn không?"* → 2 nút `[ Có, dùng biến cố đối ]` / `[ Không cần ]`.
3. Sau khi chọn đủ 2 câu, hiện đúng khung tính toán tương ứng (bảng tổ hợp hoặc canvas cây) + ô nhập kết quả.

3-strike áp dụng ở cả 2 câu hỏi phân loại VÀ ở kết quả số cuối — vì việc chọn đúng chiến lược chính là kỹ năng trọng tâm của module này.

---

## 5 câu luyện tập

| # | Đề bài | Câu hỏi 1 | Câu hỏi 2 | Đáp án |
|---|---|---|---|---|
| 1 | Một hộp có 10 viên bi (6 đỏ, 4 xanh). Lấy đồng thời 4 viên. Tính xác suất được 2 đỏ và 2 xanh. | Chọn nhóm → Tổ hợp | Không cần | n(Ω)=C¹⁰₄=210; n(E)=C⁶₂·C⁴₂=90; P=3/7 |
| 2 | 3 hộp bi đánh số: Hộp 1 (1-5), Hộp 2 (1-4), Hộp 3 (1-3). Rút 1 viên từ mỗi hộp. Tính xác suất tổng 3 số bằng 6. | Nhiều công đoạn → Sơ đồ cây | Không cần | n(Ω)=60; n(E)=9; P=3/20 |
| 3 | Lớp có 15 học sinh (9 nam, 6 nữ). Chọn ngẫu nhiên 3 bạn. Tính xác suất có ÍT NHẤT 1 bạn nữ. | Chọn nhóm → Tổ hợp | Có → biến cố đối | n(Ω)=C¹⁵₃=455; n(đối)=C⁹₃=84; P=1−84/455=53/65 |
| 4 | Tung 1 đồng xu liên tiếp 4 lần. Tính xác suất có ÍT NHẤT 1 lần mặt Ngửa. | Nhiều công đoạn → Sơ đồ cây | Có → biến cố đối | n(Ω)=2⁴=16; n(đối, toàn Sấp)=1; P=1−1/16=15/16 |
| 5 | Một lô hàng 20 sản phẩm có 3 sản phẩm lỗi. Kiểm tra ngẫu nhiên 5 sản phẩm. Tính xác suất có đúng 1 sản phẩm lỗi trong 5 sản phẩm kiểm tra. | Chọn nhóm → Tổ hợp | Không cần (đề hỏi "đúng 1", không phải "ít nhất") | n(Ω)=C²⁰₅=15504; n(E)=C³₁·C¹⁷₄=7140; P=35/76≈0,461 |

### Kịch bản dẫn dắt sai lầm (áp dụng cho mọi câu)

**Câu hỏi 1 — chọn sai phương pháp đếm:**
- Lần sai 1: rung nhẹ, không gợi ý.
- Lần sai 2: gợi ý — *"Bạn thử đọc lại đề: có thể tách thành các bước rõ ràng (rút từ hộp này, rồi hộp khác) không, hay chỉ là chọn 1 lần duy nhất?"*
- Lần sai 3: hiện đáp án đúng kèm giải thích ngắn vì sao.

**Câu hỏi 2 — bỏ sót biến cố đối (Câu 3, 4) hoặc dùng thừa biến cố đối (Câu 1, 2, 5 — đề không có "ít nhất"):**
- Lần sai 2: gợi ý — *"Đề bài có từ 'ít nhất' không? Nếu không có, có cần dùng biến cố đối không?"*
- Lần sai 3: đáp án đúng kèm giải thích.

**Kết quả số cuối:** 3-strike tương tự các module trước, gợi ý nhắc lại đúng công thức tương ứng đã chọn ở 2 câu hỏi phân loại.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Mỗi câu 1 khối full-width, xếp dọc Câu 1 → Câu 5. Trong mỗi khối: 2 câu hỏi phân loại ở trên (2 hàng nút), khung tính toán + ô nhập kết quả hiện ra ngay dưới sau khi chọn đủ.

**Mobile (≤767px):** Giữ nguyên thứ tự dọc trong từng khối. Không cần pattern lướt ngang vì mỗi câu là 1 khối độc lập, không có canvas cố định xuyên suốt bị cuộn mất.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Chọn phương pháp (Câu hỏi 1) | Click 1 trong 2 nút | Chạm 1 trong 2 nút ≥44px |
| Chọn có/không dùng biến cố đối (Câu hỏi 2) | Click 1 trong 2 nút | Chạm 1 trong 2 nút ≥44px |
| Nhập kết quả số | Gõ bàn phím, click Kiểm tra | Chạm ô input `inputmode="numeric"`, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm4_cau1', type: 'answered', required: true },
  { id: 'm4_cau2', type: 'answered', required: true },
  { id: 'm4_cau3', type: 'answered', required: true },
  { id: 'm4_cau4', type: 'answered', required: true },
  { id: 'm4_cau5', type: 'answered', required: true }
]
```
`progress total = 5`.

### `athenaGuidance` (nguyên văn, khớp đúng 5 mục)
```
1-5. m4_cau1..5: 
   - Gợi ý sai Câu hỏi 1 CHỈ dùng đúng câu "Bạn thử đọc lại đề: có thể
     tách thành các bước rõ ràng không, hay chỉ là chọn 1 lần duy nhất?"
   - Gợi ý sai Câu hỏi 2 CHỈ dùng đúng câu "Đề bài có từ 'ít nhất'
     không? Nếu không có, có cần dùng biến cố đối không?"
   - Không nói thẳng phương pháp đúng hoặc đáp án số cuối ở bất kỳ gợi
     ý nào — chỉ hỏi ngược đúng 2 câu trên tuỳ đang sai ở đâu.
```

---

## Tổng kết kiến thức

> **Quy trình chọn phương pháp tính xác suất:**
> 1. Xác định cấu trúc phép thử: nếu là "chọn ra 1 nhóm cùng lúc" → dùng **tổ hợp**; nếu có **nhiều công đoạn liên tiếp** → dùng **sơ đồ hình cây**.
> 2. Kiểm tra từ khoá "ít nhất" — nếu có, xét xem tính **biến cố đối** (P(E) = 1 − P(Ē)) có dễ hơn tính trực tiếp không.
> 3. Biến cố đối không phải phương pháp thứ 3 độc lập — có thể kết hợp với CẢ tổ hợp và sơ đồ cây.
>
> ⚠️ Luôn tự hỏi 2 câu trên TRƯỚC khi bắt đầu tính toán — chọn sai chiến lược ngay từ đầu sẽ khiến bài toán rối hơn nhiều so với thực tế cần thiết.
