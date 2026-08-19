# Module 3: Xác suất của biến cố đối
### Bài 27 — Thực hành tính xác suất theo định nghĩa cổ điển | Toán 10, Chương IX | Chủ đề 55

---

**Mục tiêu:** Học sinh tự nhận ra khi nào nên dùng chiến thuật biến cố đối (đặc biệt với các bài có từ "ít nhất"), và hình thành công thức P(E) = 1 − P(Ē) qua trải nghiệm "cách khó → cách dễ".

**Sai lầm cần giải quyết:**
1. Không nhận ra chiến thuật biến cố đối khi bài toán có từ "ít nhất" — cố tính trực tiếp dù rất phức tạp.
2. Tính sai dẫn đến P(E) + P(Ē) ≠ 1.

**Loại simulation:** Đối chất trực tiếp (thử cách khó trước, tự thấy bế tắc, rồi mới hình thành cách dễ hơn) + mô hình trực quan "thanh chia ô" nối lại từ Bài 26.

**Thời gian hoàn thành dự kiến:** ~14 phút.

**Dạy từ đầu hay tổng kết:** **Dạy từ đầu** — không có video giới thiệu trước. Biến cố đối (khái niệm) đã học ở Bài 26, nhưng nhận diện KHI NÀO nên dùng chiến thuật này để tính xác suất là kỹ năng mới.

---

## 🖼️ Phác thảo canvas — Thanh chia ô (nối lại Bài 26)

- 1 thanh ngang chia 2 vùng liền nhau, không có khoảng hở giữa 2 vùng (để nhấn mạnh "cộng lại vừa đúng cả thanh"): vùng trái tô xanh ngọc (nhãn "E — P(E)"), vùng phải tô cam (nhãn "Ē — P(Ē) = 1 − P(E)"). Độ rộng mỗi vùng CẬP NHẬT đúng theo tỉ lệ P(E) thực tế của ví dụ đang xét (không cố định 50/50), để học sinh thấy rõ "phần nào lớn hơn" ứng với xác suất nào cao hơn.
- Khi chuyển sang ví dụ mới (Bước 2 trở đi), thanh này thu nhỏ lại thành 1 biểu tượng nhỏ ở góc màn hình (bấm vào để phóng to lại) — tránh chiếm chỗ khi học sinh đang tập trung vào ví dụ chính.

## Bước 1 — Nhắc lại bằng mô hình thanh chia ô (nối lại Bài 26)

Hiện lại đúng mô hình thanh chia ô từ Bài 26: 1 thanh tô 2 màu, phần xanh là biến cố E, phần cam là Ē. Độ dài phần xanh + độ dài phần cam = cả thanh (=1).

**Athena:** *"Nhớ lại: nếu biết P(E), ta suy ra ngay P(Ē) = 1 − P(E), vì 2 phần này cộng lại vừa đúng cả thanh."*

## Bước 2 — Đặt vấn đề: thử cách khó trước (đối chất)

**Athena:** *"Chọn ngẫu nhiên 2 số từ tập {1, 2, ..., 11}. Biến cố H: 'Trong 2 số được chọn có ÍT NHẤT 1 số chia hết cho 3'. Bạn hãy thử tính trực tiếp n(H)."*

- Học sinh được gợi ý chia thành các trường hợp: "đúng 1 số chia hết cho 3" + "cả 2 số chia hết cho 3", rồi cộng lại — hệ thống để học sinh tự thử vài phép tính, KHÔNG chặn nhưng cũng không xác nhận đúng/sai ngay.
- Sau khoảng 1-2 lần thử, Athena hỏi: *"Bạn thấy cách này có nhiều trường hợp phải xét không? Có cách nào khác dễ hơn để tính n(H) không?"*

## Bước 3 — Hình thành kỹ thuật: chuyển sang biến cố đối

**Athena:** *"Thử tính biến cố đối H̄: 'CẢ 2 số được chọn đều KHÔNG chia hết cho 3' — có dễ hơn không?"*

- Trong tập {1,...,11}, các số chia hết cho 3 là {3, 6, 9} (3 số), còn lại 8 số không chia hết cho 3.
- n(Ω) = C¹¹₂ = 55. n(H̄) = C⁸₂ = 28.
- P(H̄) = 28/55. Từ đó P(H) = 1 − 28/55 = 27/55.

**Athena chốt:** *"Chỉ cần đúng 1 phép tính tổ hợp cho H̄, thay vì phải chia nhiều trường hợp cho H trực tiếp — đây chính là lý do nên nhận ra dấu hiệu 'ít nhất' để chuyển sang biến cố đối."*

### 3-strike khi tính n(H̄) hoặc P(H):
- Lần sai 2: gợi ý — *"Các số KHÔNG chia hết cho 3 trong tập {1,...,11} gồm những số nào? Có bao nhiêu số?"*
- Lần sai 3: đáp án đúng kèm phép tính đầy đủ.

## Bước 4 — Athena khái quát hoá kỹ thuật

> Athena: *"Bất cứ khi nào đề bài có từ 'ít nhất', hãy tự hỏi: biến cố đối (nghĩa là 'không có... nào cả') có dễ tính hơn không? Nếu có, hãy tính P(Ē) trước rồi suy ra P(E) = 1 − P(Ē)."*

---

## Tổng kết kiến thức

> **Công thức biến cố đối:** P(E) = 1 − P(Ē).
>
> ⚠️ **Dấu hiệu nên dùng biến cố đối:** khi bài toán có từ "ít nhất" — biến cố đối ("không có... nào cả") thường dễ đếm hơn nhiều so với tính trực tiếp (tránh phải chia nhiều trường hợp cộng lại). Luôn tự kiểm tra: P(E) + P(Ē) phải bằng 1.

---

## Bài tập luyện tập (3 câu, bối cảnh mới)

| # | Đề bài | Đáp án (đã kiểm chứng) |
|---|---|---|
| 1 | Hộp A có 4 thẻ: 1, 2, 3, 4. Hộp B có 3 thẻ: 2, 3, 4 (không có số 1). Hộp C có 2 thẻ: 1, 2. Rút 1 thẻ từ mỗi hộp. Tính xác suất trong 3 thẻ rút ra có ÍT NHẤT 1 thẻ số 1. | Biến cố đối: n(Ω)=4×3×2=24; n(M̄)=3×3×1=9; P(M̄)=3/8; P(M)=5/8 |
| 2 | Chọn ngẫu nhiên 3 số từ tập {1, 2, ..., 10}. Tính xác suất có ÍT NHẤT 1 số lẻ. | Biến cố đối "cả 3 số đều chẵn": n(Ω)=C¹⁰₃=120; n(đối)=C⁵₃=10; P(đối)=1/12; P(E)=11/12 |
| 3 (Vận dụng, nối lại "nguyên lí xác suất bé" — Bài 26) | Một giải xổ số chọn 6 số từ 1 đến 40. Một người chơi đã chọn bộ số {2; 9; 17; 24; 31; 38}. Tính xác suất người đó trúng giải Nhất (khớp đúng 5/6 số). | n(Ω)=C⁴⁰₆=3 838 380; n(G)=C⁶₅×C³⁴₁=6×34=204; P(G)=204/3 838 380 ≈ 0,0000531 |

**Lời thoại Athena ở Câu 3 (liên hệ ngược Bài 26):** *"Xác suất này rất bé — đúng như nguyên lí xác suất bé đã học: trong 1 lần chơi, khả năng trúng giải gần như không xảy ra. Nhưng nếu có hàng triệu người cùng chơi, vẫn sẽ có một số ít người trúng — giống câu chuyện máy ATM ở Bài 26."*

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Mỗi bước/câu 1 khối full-width. Mô hình thanh chia ô ở Bước 1 full-width, các bước sau có ô nhập/công thức bên trái, khung thoại bên phải.

**Mobile (≤767px):** Giữ nguyên thứ tự dọc, không cần pattern lướt ngang.

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Thử tính trực tiếp (Bước 2) | Gõ số vào các ô trường hợp | Chạm ô input `inputmode="numeric"` |
| Nhập kết quả tổ hợp/xác suất | Gõ bàn phím, click Kiểm tra | Chạm ô input, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`
```javascript
structure: [
  { id: 'm3_thu_cach_kho',   type: 'explored', required: true },
  { id: 'm3_bien_co_doi_h',  type: 'answered', required: true },
  { id: 'm3_bt1',            type: 'answered', required: true },
  { id: 'm3_bt2',            type: 'answered', required: true },
  { id: 'm3_bt3_van_dung',   type: 'answered', required: true }
]
```
`progress total = 5`.

### `athenaGuidance`
```
1. m3_thu_cach_kho: không xác nhận đúng/sai, chỉ hỏi ngược "Bạn thấy
   cách này có nhiều trường hợp phải xét không?" để dẫn dắt sang biến
   cố đối.
2. m3_bien_co_doi_h: gợi ý lần sai thứ 2 CHỈ dùng đúng câu "Các số
   KHÔNG chia hết cho 3 trong tập {1,...,11} gồm những số nào?" —
   không nói thẳng đáp án 27/55.
3. m3_bt1: gợi ý tương tự, đổi theo đúng 3 hộp thẻ.
4. m3_bt2: gợi ý — "Biến cố đối là gì khi 'ít nhất 1 số lẻ' không xảy
   ra?" — không nói thẳng đáp án 11/12.
5. m3_bt3_van_dung: gợi ý lần sai thứ 2 CHỈ nhắc "Cần đúng 5/6 số
   khớp — chọn 5 trong 6 số đã đăng ký, và 1 số còn lại phải khác 6 số
   đó." — không tính hộ n(G) = 204.
```
