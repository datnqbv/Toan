# 📚 KỊCH BẢN — Bài 27, Module 1: "Thể tích khối chóp và khối lăng trụ"

```
📖 PPCT: Tiết 77 — Chủ đề 11: Thể tích
📌 Đã dạy qua kênh khác: video Manim. Không rút gọn — mô phỏng 3D đầy đủ
   theo yêu cầu, cùng tinh thần Bài 22-26.
🎯 Sai lầm nhắm tới (PPCT):
   (A) nhầm chiều cao khối chóp với ĐỘ DÀI CẠNH BÊN (chỉ trùng khi cạnh
       bên vuông góc đáy)
   (B) tính sai diện tích đáy khi đáy không quen thuộc (ngũ giác, lục
       giác)
   (C) QUÊN NHÂN HỆ SỐ 1/3 trong công thức thể tích khối chóp
   (D) nhầm chiều cao MẶT BÊN (trung đoạn) với chiều cao TOÀN KHỐI
   (E) tính sai số học với giá trị chứa căn
📁 File: Bai27_Toan3D_Module1_TheTichChopLangTru.html
```

## Sổ tay kiến thức (hiện dần theo bước)

```
- Thể tích khối lăng trụ: V = S · h (S = diện tích đáy, h = chiều cao —
  khoảng cách giữa 2 mặt đáy).
- Thể tích khối chóp: V = (1/3) · S · h (S = diện tích đáy, h = chiều
  cao — khoảng cách từ đỉnh đến mặt đáy, KHÔNG phải cạnh bên).
- ⚠️ h CHỈ bằng độ dài cạnh bên khi cạnh bên đó vuông góc với đáy — đây
  KHÔNG phải trường hợp chung.
- ⚠️ h KHÁC trung đoạn (chiều cao của 1 mặt bên — dùng để tính diện
  tích xung quanh, KHÔNG dùng để tính thể tích).
```

---

## BƯỚC 1 — Liên hệ thể tích khối hộp chữ nhật đã biết (khởi động)

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Từ THCS, bạn đã biết thể tích khối hộp chữ nhật = dài ×
   rộng × cao = (diện tích đáy) × (chiều cao). Với LĂNG TRỤ có đáy bất
   kỳ (không chỉ hình chữ nhật), công thức này còn đúng không?"
   - *Hành động HS:* quan sát 1 lăng trụ đáy tam giác nghiêng dần thành
     lăng trụ đứng (slider), thấy công thức V=S·h vẫn áp dụng được, chỉ
     cần S là diện tích đáy TAM GIÁC thay vì hình chữ nhật.
   - **Chốt:** "V = S·h đúng cho MỌI lăng trụ đứng, không chỉ hình hộp
     chữ nhật — đây là bước mở rộng tự nhiên từ kiến thức đã biết."

---

## BƯỚC 2 — Thí nghiệm đong nước: khám phá tỉ lệ 1:3

**Cấu hình 3D:**
- 1 khối chóp và 1 khối lăng trụ CÙNG đáy (diện tích S=10), CÙNG chiều
  cao (h=6) đặt cạnh nhau. Verify Python: V_lăng trụ=60, V_chóp=20, tỉ lệ
  đúng = 3,0.
- **Animation đong nước (đặc tả đầy đủ, PHẦN 2.14 `05_threejs_engine.md`):**
  chóp đã đổ đầy sẵn (fillRatio=1). Khi bấm "Đổ nước", chạy đúng 1 hàm
  điều phối `runOnePour` — đồng bộ 3 lớp trong 1200ms: (1) mực nước chóp
  giảm dần 1→0, tiết diện co theo đúng hình chóp; (2) 1 dòng hạt nước
  nhỏ (hình cầu, màu nước `#7fb5d9`) bay theo cung Bezier từ miệng chóp
  sang miệng lăng trụ, spawn liên tục mỗi 120ms; (3) mực nước lăng trụ
  tăng dần đúng thêm 1/3 chiều cao. Bấm lại nút 2 lần nữa cho 2 lần đổ
  tiếp theo.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đây là 1 khối chóp và 1 khối lăng trụ CÙNG đáy, CÙNG
   chiều cao. Bấm 'Đổ nước' để đong đầy khối chóp, rồi trút vào lăng
   trụ — quan sát mực nước trong lăng trụ dâng đến đâu."
   - *Hành động HS:* bấm đổ nước lần 1 — xem animation trút nước chạy
     đầy đủ (1,2s), mực nước lăng trụ dâng đúng lên 1/3 chiều cao. Bấm
     lần 2 — lên 2/3. Bấm lần 3 — ĐẦY TRÀN đúng miệng lăng trụ.
   - 🎯 **Mục tiêu quan sát:** cần ĐÚNG 3 lần đổ đầy chóp mới lấp đầy
     lăng trụ — không phải 2 lần, không phải 4 lần.

2. **Giải thích đúng + chốt công thức (nhắm trực diện sai lầm C):**
   "Thể tích khối chóp LUÔN bằng 1/3 thể tích lăng trụ cùng đáy, cùng
   chiều cao — đây chính là lý do công thức khối chóp có hệ số 1/3.
   Nhiều học sinh QUÊN mất hệ số này vì chỉ nhớ mang máng V=S·h — hãy
   nhớ lại chính thí nghiệm đong nước này mỗi khi quên."

---

## BƯỚC 3 — Xác định đúng chiều cao h (nhắm trực diện sai lầm A, D)

**Cấu hình 3D:**
- Chóp tứ giác ĐỀU S.ABCD, đáy cạnh a=4, cạnh bên b=5 (chóp KHÔNG có
  cạnh bên vuông góc đáy — cần dựng riêng chiều cao).
- Verify Python: cạnh bên SA=5; chiều cao khối SO=4,1231; trung đoạn
  (chiều cao mặt bên) SM=4,5826 — **3 giá trị khác nhau rõ ràng**.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Chóp này có cạnh bên SA=5. Đây có phải là chiều cao h
   dùng để tính thể tích không?"
   - *Hành động HS:* xoay hình quan sát — SA đi từ đỉnh XIÊN xuống 1
     GÓC đáy, không phải xuống TÂM đáy theo phương vuông góc.
   - `dap_an_dung`: "Không — h phải là khoảng cách từ đỉnh S đến MẶT
     ĐÁY theo phương VUÔNG GÓC, tức đoạn SO (O là tâm đáy), không phải
     SA."

2. **3-strike (nhắm sai lầm A):** "Chiều cao h của chóp CHỈ bằng cạnh
   bên khi nào?"
   - A. Luôn luôn bằng nhau
   - B. Chỉ khi cạnh bên đó vuông góc với đáy (đáp án đúng)
   - C. Chỉ khi đáy là hình vuông
   - Hết lượt: hiện đáp án B + nhắc lại: "Ở chóp ĐỀU như hình này, KHÔNG
     cạnh bên nào vuông góc đáy — phải luôn dựng riêng SO."

3. **Phân biệt tiếp (nhắm sai lầm D):** "Còn 1 đoạn nữa dễ nhầm: SM —
   nối từ đỉnh S đến TRUNG ĐIỂM M của 1 cạnh đáy. SM có dùng để tính thể
   tích không?"
   - *Hành động HS:* quan sát SM = 4,5826 (khác cả SA=5 và SO=4,1231).
   - `dap_an_dung`: "Không — SM là TRUNG ĐOẠN (chiều cao của 1 MẶT BÊN
     hình tam giác), dùng để tính DIỆN TÍCH XUNG QUANH, không dùng cho
     THỂ TÍCH. Thể tích chỉ dùng đúng 1 giá trị: SO."

4. **Tính hoàn chỉnh:** V = (1/3)×16×4,1231 ≈ 21,99 — verify khớp Python.

---

## BƯỚC 4 — Áp dụng trên đáy lạ (nhắm trực diện sai lầm B)

**Cấu hình 3D:**
- Chóp đều đáy LỤC GIÁC ĐỀU, cạnh a=3, chiều cao khối h=6.
- Verify Python: diện tích lục giác đều = 23,3827; V=46,7654.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Đáy lục giác đều không quen thuộc như tam giác/tứ giác
   — công thức diện tích của nó là gì?"
   - Hướng dẫn: chia lục giác đều thành 6 tam giác đều (từ tâm), diện
     tích = 6 × (√3/4)a² = (3√3/2)a².
   - Hệ thống CHẶN nếu học sinh áp nhầm công thức tam giác đều/hình
     vuông cho lục giác (không cho tính V tiếp nếu diện tích đáy sai).

2. **Tính hoàn chỉnh:** V = (1/3)×23,3827×6 ≈ 46,7654.

---

## TỔNG HỢP KIẾN THỨC (đóng Module 1)

| Khối kiến thức | Nội dung | Xem lại tại |
|---|---|---|
| 1. Mở rộng công thức | V=S·h đúng cho MỌI lăng trụ đứng | Bước 1 |
| 2. Tỉ lệ 1:3 | Chóp = 1/3 lăng trụ cùng đáy, cùng cao | Bước 2 |
| 3. Đúng h | h ≠ cạnh bên (trừ khi ⊥ đáy), h ≠ trung đoạn | Bước 3 |
| 4. Đáy lạ | Chia nhỏ đa giác đều thành tam giác để tính diện tích | Bước 4 |

## Đặc tả hình ảnh & màu sắc

**Hook mở đầu (SVG viewBox 0 0 500 280):**
```
- 1 khối chóp (fill=--il-terracotta, mờ) và 1 khối lăng trụ (fill=
  --il-slate) đặt cạnh nhau, cùng đáy cùng cao (đường kẻ ngang mảnh nối
  2 đỉnh cao bằng nhau để nhấn "cùng chiều cao").
- 3 giọt nước nhỏ (--jade) rơi từ chóp xuống lăng trụ, gợi ý hoạt động
  đong nước sắp tới.
```

**Bảng màu:**

| Đối tượng | Token | Vai trò |
|---|---|---|
| Khối chóp | `--il-terracotta` | Đối tượng chính Bước 2-4 |
| Khối lăng trụ (Bước 1-2) | `--il-slate` | Đối chiếu |
| Chiều cao h ĐÚNG (SO) | `--jade` | Đáp án chốt |
| Cạnh bên (bẫy) | `--accent` | Dễ nhầm, cần phân biệt |
| Trung đoạn (bẫy khác) | `--il-ochre` | Dễ nhầm, phân biệt màu riêng với cạnh bên |
| Nước mô phỏng | `#7fb5d9` (đúng màu nước đã dùng trong `04a_nhiet_hoc.md`, tương đương `--il-dusty-blue`) | Hiệu ứng đong nước Bước 2 |

## Rủi ro kỹ thuật 3D

```
✅ An toàn: Bước 1, 3, 4 — chỉ dựng hình tĩnh + đo, dùng
   `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3) đã có.
✅ Đã đặc tả ĐẦY ĐỦ (chưa verify HTML thật): Bước 2 (animation đong nước
   + trút nước) — PHẦN 2.13 + 2.14 (05_threejs_engine.md). Mực nước
   dâng chuyển thể từ thư viện Vật Lý sẵn có (`04a_nhiet_hoc.md` —
   `animateCalorimeter`); animation trút nước dùng dòng hạt bay theo
   cung Bezier, đồng bộ đủ 3 lớp trong 1 hàm `runOnePour` duy nhất —
   KHÔNG để đội build tự quyết cách làm. Tái dùng thẳng `Ease`/`lerp` từ
   `04d_daodong_helpers.md`. Đã verify toán học đầy đủ bằng Node (quỹ
   đạo cung, tỉ lệ 3 lần đổ đúng 0→1/3→2/3→1) — còn thiếu verify hiệu
   ứng hình ảnh thật (giật khung hình khi nhiều hạt bay cùng lúc) trên
   trình duyệt, cần prototype trước khi build.
```

---

> **Trạng thái:** Module 1 (Bài 27) đã có kịch bản đầy đủ 4 bước + Tổng
> hợp kiến thức + đặc tả hình ảnh, số liệu đã verify bằng Python. Module
> 2 (luyện tập — vai kỹ sư/nhà thiết kế, dự án chậu gốm bonsai) và trang
> Tổng hợp trực quan cuối bài sẽ ra kịch bản ở các phiên tiếp theo.
