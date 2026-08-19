# Module 4: Kết hợp quy tắc cộng và quy tắc nhân
### Bài 23 — Quy tắc đếm | Toán 10, Chương VIII | Chủ đề 47

---

**Mục tiêu:** Học sinh vận dụng đúng quy trình 3 bước để giải bài toán đếm phức hợp: (1) chia thành các trường hợp rời nhau, (2) tính số cách trong mỗi trường hợp bằng quy tắc nhân, (3) cộng kết quả các trường hợp.

**Sai lầm cần giải quyết:**
1. Tính trùng/tính thiếu do chia trường hợp không triệt để.
2. Sau khi tính đúng số cách trong từng trường hợp (bằng nhân), lại **nhân tiếp** 2 kết quả đó với nhau thay vì cộng — nhầm lẫn vì vừa dùng nhân ở bước trước.

**Loại simulation:** Quy trình có hướng dẫn (step-by-step) — mỗi trường hợp là 1 trạm tính toán riêng, trạm cuối kiểm tra việc kết hợp.

**Thời gian hoàn thành dự kiến:** ~8 phút.

**Dạy từ đầu hay tổng kết:** Dạy từ đầu, dựa trên 2 quy tắc đã học ở Module 1 (cộng) và Module 3 (nhân) — cần Sổ tay kiến thức nền tảng.

---

## 🎬 Hook mở đầu

Hook SVG: bàn đăng ký giải cờ vua học đường, có bàn cờ nhỏ, 2 xấp thẻ mã dự thi màu xanh (Nhi đồng) và cam (Thiếu niên), 1 bảng danh sách đăng ký.

**Lời thoại Athena tại hook:**
> "Giải cờ vua học đường in mã dự thi cho vận động viên. Hạng Nhi đồng dùng mã gồm 1 chữ cái đội (trong 4 đội A-D) ghép với 1 số báo danh (1 đến 8). Hạng Thiếu niên dùng mã gồm 1 chữ cái đội (trong 5 đội A-E) ghép với 1 số báo danh (1 đến 6). Bạn nghĩ toàn giải có thể in được bao nhiêu mã khác nhau?"

---

## Số liệu cụ thể (đã kiểm chứng)

- Hạng Nhi đồng: 4 đội × 8 số báo danh = **32** mã.
- Hạng Thiếu niên: 5 đội × 6 số báo danh = **30** mã.
- Mỗi vận động viên chỉ thuộc 1 trong 2 hạng tuổi → 2 trường hợp rời nhau.
- Tổng số mã toàn giải: 32 + 30 = **62**.

---

## 🖼️ Phác thảo canvas

**Bố cục:** 2 "quầy đăng ký" đặt cạnh nhau (Nhi đồng bên trái, Thiếu niên bên phải), mỗi quầy là 1 khối độc lập gồm: ô nhập/xác nhận số đội, ô nhập/xác nhận số báo danh, 1 câu hỏi trắc nghiệm "Quy tắc nào?" (Cộng / Nhân), và kết quả hiện ra sau khi chọn đúng.

Phía dưới 2 quầy: 1 khối "Kết hợp kết quả" — hiện 2 số đã tính được (32 và 30), kèm câu hỏi trắc nghiệm "Quy tắc nào để ra tổng cuối?" (Cộng / Nhân) và ô nhập đáp án cuối.

---

## Học sinh tương tác bằng cách

1. Dự đoán tổng số mã toàn giải (nhập số), chưa biết cách tính.
2. Tại quầy Nhi đồng: xác nhận số đội (4) và số báo danh (8), chọn quy tắc đúng (Nhân), xem kết quả 32.
3. Tại quầy Thiếu niên: xác nhận số đội (5) và số báo danh (6), chọn quy tắc đúng (Nhân), xem kết quả 30.
4. Tại khối "Kết hợp kết quả": chọn quy tắc đúng để cộng dồn 2 hạng (đây là bẫy chính), nhập đáp án cuối.
5. Đọc Athena khái quát hoá quy trình 3 bước.
6. *(Mở rộng, không bắt buộc)* Áp dụng nhanh với 1 tình huống mới.

### Trước mỗi bước tương tác

| Bước | Hướng dẫn thao tác | Kiến thức áp dụng |
|---|---|---|
| 1 | "Bạn hãy đoán xem toàn giải có thể in được bao nhiêu mã dự thi khác nhau, rồi nhấn Kiểm tra." | (không cần — chỉ là dự đoán trực giác) |
| 2 | "Bạn hãy xác nhận số đội và số báo danh ở quầy Nhi đồng, rồi chọn quy tắc phù hợp để tính số mã." | Chữ cái đội và số báo danh là 2 công đoạn nối tiếp, độc lập nhau — dùng quy tắc nhân (Module 3). |
| 3 | "Bạn làm tương tự ở quầy Thiếu niên." | Giống Bước 2, áp dụng quy tắc nhân với số liệu của hạng Thiếu niên. |
| 4 | "Bạn đã có 32 mã Nhi đồng và 30 mã Thiếu niên. Hãy chọn đúng quy tắc để ra tổng số mã toàn giải, rồi nhập kết quả." | Một vận động viên chỉ thuộc 1 trong 2 hạng — đây là 2 phương án rời nhau, dùng quy tắc cộng (Module 1). |

---

## Kịch bản dẫn dắt học sinh gặp sai lầm

**Bước 1 — dự đoán:**
> Athena: "Bạn dự đoán là [số học sinh nhập]. Mình cùng tính từng hạng một trước nhé."

**Bước 2, 3 — tính từng hạng (câu hỏi trắc nghiệm Cộng/Nhân):**
Nếu học sinh chọn "Cộng" ở đây (VD 4+8=12 thay vì 4×8=32): hệ thống không nói sai ngay, mà hỏi ngược:
> Athena: "Bạn thử nghĩ xem: chữ cái đội và số báo danh có phải làm nối tiếp nhau, mỗi đội đều ghép được với tất cả số báo danh không? Đây giống bài toán nào bạn đã gặp ở phần trước?"

Nếu vẫn chọn sai lần 2, hệ thống hiện: "Đây là 2 công đoạn nối tiếp và độc lập — giống mật mã điều tra viên đã học, phải dùng quy tắc nhân."

**Bước 4 — bẫy chính (kết hợp 2 kết quả):**
Nhiều học sinh sẽ chọn "Nhân" ở bước này (32 × 30 = 960) vì vừa quen dùng nhân ở 2 bước trước.
- Lần sai 1: rung nhẹ, không gợi ý.
- Lần sai 2: gợi ý — *"Một vận động viên có thể vừa thi Nhi đồng vừa thi Thiếu niên không? Nếu 2 hạng này hoàn toàn tách biệt, bạn nên cộng hay nhân?"*
- Lần sai 3: đáp án đúng — *"Đáp án đúng là 62. Vì Nhi đồng và Thiếu niên là 2 trường hợp rời nhau (không ai thuộc cả 2 hạng), nên phải cộng 2 kết quả: 32 + 30 = 62, không nhân."*
- Trả lời đúng: *"Chính xác! Bạn vừa áp dụng đúng cả 2 quy tắc: nhân trong từng hạng (vì 2 công đoạn nối tiếp), cộng giữa 2 hạng (vì 2 trường hợp rời nhau)."*

---

## Bước 5 — Athena khái quát hoá quy trình 3 bước

> Athena: "Để giải bài toán đếm phức hợp như thế này, bạn làm theo 3 bước: Bước 1 — chia bài toán thành các trường hợp hoàn toàn rời nhau (ở đây là 2 hạng tuổi). Bước 2 — trong mỗi trường hợp, nếu có nhiều công đoạn nối tiếp, dùng quy tắc nhân. Bước 3 — cộng kết quả của tất cả các trường hợp lại."

## Sổ tay kiến thức nền tảng (hiện xuyên suốt module)

```
- Quy tắc cộng (Module 1): 2 phương án KHÔNG trùng nhau → cộng số cách.
- Quy tắc nhân (Module 3): các công đoạn liên tiếp, ĐỘC LẬP nhau → nhân số cách.
- Quy trình kết hợp (Module 4 - mới):
  Bước 1: Chia bài toán thành các trường hợp RỜI NHAU.
  Bước 2: Trong mỗi trường hợp, tính số cách bằng quy tắc nhân (nếu có nhiều công đoạn).
  Bước 3: Cộng kết quả của tất cả các trường hợp.
```

## Bước 6 — Mở rộng (không bắt buộc)

Tình huống mới: 1 rạp chiếu phim có 2 khung giờ chiếu (sáng/tối, rời nhau), khung sáng có 3 phòng × 2 hạng ghế, khung tối có 4 phòng × 2 hạng ghế → đáp án (3×2)+(4×2) = 6+8 = 14. Không chặn hoàn thành module nếu bỏ qua.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** 2 quầy đăng ký đặt cạnh nhau ngang hàng (mỗi quầy ~45% chiều rộng), khối "Kết hợp kết quả" đặt full-width ngay dưới 2 quầy. Không có sidebar bước khoá dần riêng — toàn bộ hiện trên 1 màn hình cuộn dọc.

**Mobile (≤767px):** 2 quầy xếp dọc chồng lên nhau (Nhi đồng trước, Thiếu niên sau), khối "Kết hợp kết quả" xuống cuối cùng. Đây là dạng cuộn dọc thường (không phải sidebar nhiều thẻ bước khoá dần cạnh 1 canvas cố định như Module 3), nên **không cần** pattern lướt ngang PHẦN 3.6b — cuộn dọc bình thường là đủ vì không có canvas nào bị cuộn mất (mỗi quầy tự chứa đủ thông tin của nó).

**Bảng ánh xạ tương tác — Desktop ↔ Mobile:**

| Thao tác | Desktop | Mobile |
|---|---|---|
| Xác nhận số đội/số báo danh | Click ô xác nhận | Chạm ô xác nhận ≥44px |
| Chọn quy tắc (Cộng/Nhân) | Click 1 trong 2 nút lựa chọn | Chạm 1 trong 2 nút, mỗi nút ≥44px chiều cao |
| Nhập đáp án cuối | Gõ bàn phím, click Kiểm tra | Chạm ô input mở bàn phím số, chạm nút Kiểm tra ≥44px |

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`

```javascript
structure: [
  { id: 'm4_du_doan',        type: 'answered', required: true },
  { id: 'm4_nhi_dong',       type: 'answered', required: true },
  { id: 'm4_thieu_nien',     type: 'answered', required: true },
  { id: 'm4_ket_hop',        type: 'answered', required: true },
  { id: 'm4_mo_rong',        type: 'answered', required: false }
]
```

`progress total = 4`.

### `athenaGuidance` (nguyên văn, khớp đúng 4 mục bắt buộc)

```
1. m4_du_doan: chỉ hỏi ngược "Bạn thử nghĩ xem bài toán này có mấy trường
   hợp tách biệt?" — không nói trước đáp án 62.
2. m4_nhi_dong / m4_thieu_nien: nếu học sinh chọn "Cộng" sai, Athena chỉ
   hỏi ngược: "Chữ cái đội và số báo danh có làm nối tiếp nhau không?
   Giống bài toán nào bạn đã gặp ở phần trước?" — không nói thẳng đây là
   quy tắc nhân ở lần gợi ý đầu.
3. m4_ket_hop: gợi ý lần sai thứ 2 CHỈ dùng đúng câu: "Một vận động viên
   có thể vừa thi Nhi đồng vừa thi Thiếu niên không? Nếu 2 hạng hoàn
   toàn tách biệt, bạn nên cộng hay nhân?" — không nói thẳng đáp án 62.
4. m4_mo_rong: bước không bắt buộc, có thể nhắc học sinh bỏ qua nếu muốn.
```

---

## Tổng kết kiến thức

> **Quy trình giải bài toán đếm kết hợp:** Bước 1 — chia bài toán thành các trường hợp **rời nhau**. Bước 2 — trong mỗi trường hợp, nếu có nhiều công đoạn nối tiếp và độc lập, dùng **quy tắc nhân**. Bước 3 — **cộng** kết quả của tất cả các trường hợp lại.
>
> ⚠️ Sai lầm phổ biến nhất: sau khi đã nhân đúng trong từng trường hợp, lại tiếp tục nhân 2 kết quả đó với nhau. Hãy luôn tự hỏi: các trường hợp lớn có tách biệt nhau không? Nếu có, phải **cộng**, không nhân.
