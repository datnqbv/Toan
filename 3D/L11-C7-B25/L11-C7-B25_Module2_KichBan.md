# 📚 KỊCH BẢN — Bài 25, Module 2: "Điều kiện và tính chất hai mặt phẳng vuông góc"

```
📖 PPCT: Tiết 71 — Chủ đề 9: Hai mặt phẳng vuông góc
🔗 Điều kiện tiên quyết: Module 1 (góc giữa 2 mặt phẳng, góc nhị diện).
🎯 Sai lầm nhắm tới (PPCT):
   (E) kết luận 2 mặt phẳng vuông góc chỉ vì "trông vuông góc" trên hình
       vẽ, chưa chỉ rõ đường thẳng cụ thể theo định lí
   (F) áp dụng nhầm tính chất giữa 2 mặt phẳng song song và 2 mặt phẳng
       vuông góc
   (G) nghĩ "2 mặt phẳng vuông góc thì MỌI đường trong mặt này vuông góc
       MỌI đường trong mặt kia" (chỉ đúng với đường ⊥ giao tuyến)
   (H) chứng minh thiếu bước chỉ ra đường thẳng "chìa khoá" nằm trong mặt
       này vuông góc với mặt kia
📁 File: Bai25_Toan3D_Module2_DieuKienTinhChat.html
```

> ⚠️ **Bối cảnh:** đổi khỏi "bức tường vuông góc sàn nhà" (PPCT gợi ý,
> khá giống tinh thần Bài 23) sang **vách kính phòng tắm vuông góc sàn**
> (đã duyệt) — vẫn giữ đúng kỹ thuật nền tảng "1 mặt chứa đường ⊥ mặt
> kia", nhưng bối cảnh mới và có khung nhôm làm "đường chìa khoá" rất tự
> nhiên để minh hoạ.

## Sổ tay kiến thức (hiện dần theo bước)

```
- Định nghĩa: (P) ⊥ (Q) khi góc giữa chúng bằng 90°.
- Định lí (điều kiện đủ): (P) chứa 1 đường thẳng vuông góc với (Q) thì
  (P) ⊥ (Q).
- Tính chất 1: nếu (P) ⊥ (Q), đường thẳng a nằm trong (P) và vuông góc
  với giao tuyến Δ của (P), (Q) thì a ⊥ (Q). ⚠️ CHỈ đúng với đường VUÔNG
  GÓC GIAO TUYẾN — không phải mọi đường trong (P).
- Tính chất 2: nếu (P), (Q) cắt nhau theo giao tuyến a và cùng vuông góc
  với (R) thì a ⊥ (R).
```

---

## BƯỚC 1 — Điều kiện đủ: tìm "đường chìa khoá"

**Cấu hình 3D:**
- Vách kính phòng tắm (Q1) lắp đúng, đứng thẳng, giao với sàn (P) theo
  giao tuyến Δ1 (chân vách kính). Khung nhôm của vách có: 1 thanh ĐỨNG
  (cạnh bên khung), 1 thanh NGANG (cạnh trên khung), và có thể hiện thêm
  đường chéo khung.
- Verify Python: thanh đứng có hướng song song pháp tuyến sàn — vuông
  góc sàn thật; thanh ngang và đường chéo thì không.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Thợ lắp đã dùng thước thuỷ đo thanh nhôm ĐỨNG của khung
   vách kính — xác nhận thanh đó vuông góc với sàn. Vậy mặt kính (Q1) có
   vuông góc với sàn (P) không? Click vào đúng thanh khung là 'đường
   chìa khoá' để xác nhận."
   - 3 lựa chọn click: thanh đứng (đúng), thanh ngang (sai), đường chéo
     khung (sai).
   - **3-strike:** sai lần 1 rung nhẹ; sai lần 2 gợi ý "đường chìa khoá
     phải vuông góc SÀN — thanh nào trong khung có hướng thẳng đứng?";
     hết lượt hiện đáp án + giải thích: "Chỉ cần khung kính CHỨA 1 đường
     vuông góc sàn (thanh đứng) — theo định lí, cả mặt kính (Q1) vuông
     góc sàn (P) ngay, không cần kiểm tra thêm."

---

## BƯỚC 2 — Bẫy "trông vuông góc" (nhắm trực diện sai lầm E)

**Cấu hình 3D:**
- Vách kính (Q1') lắp LỖI, nghiêng 5° quanh giao tuyến Δ1 (nghiêng ra
  ngoài nhẹ). Từ 1 góc camera mặc định, vách TRÔNG như vẫn thẳng đứng.
- Verify Python: pháp tuyến của (Q1') lệch khỏi vuông góc sàn (dot =
  −0,087 ≠ 0) — xác nhận KHÔNG vuông góc thật, dù nhìn gần giống.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "Nhìn vách kính này — bạn thấy nó có vuông góc sàn
   không?"
   - *Hành động HS:* quan sát từ góc camera mặc định (trông gần như
     thẳng đứng).
   - 🎯 Nếu học sinh vội trả lời "có" chỉ dựa vào quan sát → Athena
     không chấm sai ngay, mà dẫn tiếp bước 2.

2. **Athena:** "Đừng vội kết luận bằng mắt — hãy tìm 1 đường chìa khoá
   thật trong vách này: kéo thử 1 thanh dọc khung, xem nó có ĐÚNG vuông
   góc sàn không (dùng công cụ đo góc)."
   - *Hành động HS:* kéo/chọn thanh khung, hệ thống hiện số đo góc thật
     giữa thanh và sàn — ra 85° (không phải 90°).
   - **Giải thích đúng:** "Đúng — vách này nghiêng 5°, KHÔNG thực sự
     vuông góc sàn, dù nhìn thoáng qua rất giống. Đây chính là lý do
     PHẢI chỉ rõ 1 đường thẳng cụ thể và ĐO/CHỨNG MINH, không kết luận
     chỉ vì 'trông vuông góc'."

3. **3-strike:** "Để khẳng định 2 mặt phẳng vuông góc, cách làm ĐÚNG là
   gì?"
   - A. Nhìn hình vẽ, nếu thấy giống vuông góc thì kết luận vuông góc
   - B. Chỉ rõ 1 đường thẳng cụ thể nằm trong 1 mặt, chứng minh đường đó
     vuông góc mặt kia (đáp án đúng)
   - C. Đo bằng thước trên hình vẽ (không phải số liệu thật)
   - Hết lượt: hiện đáp án B, nhắc lại minh hoạ vách kính nghiêng 5° vừa
     làm.

---

## BƯỚC 3 — Tính chất: giao tuyến 2 mặt cùng ⊥ mặt thứ 3

**Cấu hình 3D:**
- 2 vách kính (Q1), (Q2) tạo thành góc phòng tắm (2 vách vuông góc
  nhau, cùng vuông góc sàn (P)). Giao tuyến của (Q1), (Q2) là đường
  thẳng đứng tại góc phòng.
- Verify Python: giao tuyến có hướng (0,−1,0) — song song pháp tuyến sàn
  → giao tuyến vuông góc sàn, xác nhận đúng tính chất.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "2 vách kính (Q1), (Q2) đều đã vuông góc sàn (P). Chúng
   cắt nhau tại 1 đường ở góc phòng — đường giao đó có vuông góc sàn
   không?"
   - *Hành động HS:* quan sát đường giao (góc phòng), đo góc với sàn.
   - 🎯 **Mục tiêu quan sát:** đường giao LUÔN vuông góc sàn — thẳng
     đứng, giống 2 vách tạo ra nó.

2. **Giải thích đúng:** "Đúng — tính chất: nếu 2 mặt phẳng cắt nhau và
   CÙNG vuông góc với 1 mặt phẳng thứ ba, giao tuyến của chúng cũng
   vuông góc với mặt phẳng thứ ba đó. Đây là lý do góc phòng tắm (nơi 2
   vách kính giao nhau) luôn là 1 đường thẳng đứng — không cần đo lại,
   suy luận được ngay."

---

## BƯỚC 4 — Bẫy: KHÔNG phải mọi đường đều vuông góc (nhắm trực diện sai lầm G)

**Cấu hình 3D:** dùng lại (Q1) đã xác nhận ⊥ (P) ở Bước 1.

**Thao tác — lời Athena + hành động:**

1. **Athena:** "(Q1) đã vuông góc sàn (P). Bây giờ chọn đường CHÉO của
   khung kính (không vuông góc với chân vách/giao tuyến) — đường chéo
   này có vuông góc sàn (P) không?"
   - *Hành động HS:* chọn đường chéo khung, đo góc với sàn.
   - Verify Python: đường chéo (hướng (1,1,0)) không vuông góc giao
     tuyến (dot=1≠0) VÀ không vuông góc sàn (dot=1≠0).

2. **3-strike (nhắm sai lầm G):** "(Q1) đã vuông góc (P). Vậy MỌI đường
   thẳng trong (Q1) có chắc vuông góc (P) không?"
   - `dap_an_dung`: "Không — CHỈ đường nào vuông góc với GIAO TUYẾN của
     (Q1), (P) mới chắc chắn vuông góc (P). Đường chéo khung (không
     vuông góc giao tuyến) thì KHÔNG vuông góc sàn, dù nằm trong (Q1) đã
     vuông góc sàn."
   - `goi_y_khi_sai`: "Thử đo lại đường chéo khung — nó có vuông góc với
     chân vách (giao tuyến) không? Nếu không, có nên tin nó vuông góc
     sàn không?"

3. **Phân biệt sai lầm F (không nhầm với 2 mặt song song):** "2 mặt
   phẳng SONG SONG thì mọi đường trong mặt này CÓ song song mặt kia
   không? Còn 2 mặt VUÔNG GÓC thì mọi đường trong mặt này có vuông góc
   mặt kia không?" — câu hỏi đối chiếu, không chấm điểm, chỉ để phân
   biệt rõ 2 tính chất dễ nhầm.

---

## TỔNG HỢP KIẾN THỨC (đóng Module 2)

| Khối kiến thức | Nội dung | Xem lại tại |
|---|---|---|
| 1. Điều kiện đủ | 1 mặt chứa đường ⊥ mặt kia → 2 mặt ⊥ nhau | Bước 1 |
| 2. Không tin bằng mắt | Phải chỉ rõ đường + đo/chứng minh, không kết luận qua hình vẽ | Bước 2 |
| 3. Tính chất giao tuyến | 2 mặt cắt nhau, cùng ⊥ mặt thứ 3 → giao tuyến ⊥ mặt thứ 3 | Bước 3 |
| 4. Không phải mọi đường | Chỉ đường ⊥ giao tuyến trong 1 mặt mới chắc ⊥ mặt kia | Bước 4 |

> 💡 Hoạt động mở rộng tuỳ chọn (không bắt buộc build): PPCT còn gợi ý
> "lắp ráp ngôi nhà thu nhỏ bằng bìa cứng" — về bản chất là cùng ý tưởng
> "nhiều mặt tường vuông góc sàn và với nhau" đã có trong vách kính Bước
> 3, nên không cần dựng thêm hoạt động riêng, có thể nhắc bằng lời ở
> phần tổng kết nếu muốn liên hệ thêm.

## Rủi ro kỹ thuật 3D

```
✅ An toàn: toàn bộ Module 2 (vách kính tĩnh + click chọn đường, đo góc
   hiển thị) — dùng `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3)
   đã verify, không cần pattern 3D mới.
```

---

> **Trạng thái:** Module 2 (Bài 25) đã có kịch bản đầy đủ 4 bước + Tổng
> hợp kiến thức, số liệu đã verify bằng Python (vách kính đúng, vách
> nghiêng 5°, giao tuyến 2 vách, bẫy đường chéo khung).
