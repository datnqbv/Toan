# 📚 KỊCH BẢN — Bài 25, Module 4: "Luyện tập tổng hợp — Kỹ sư giám sát công trình"

```
📖 PPCT: Tiết 73 — Chủ đề 9: Hai mặt phẳng vuông góc (Luyện tập tổng hợp)
🔗 Điều kiện tiên quyết: Module 1, 2, 3.
🎯 Vai trò: LUYỆN TẬP tổng hợp toàn bộ hệ thống định lí vuông góc (Bài
   22-25), nhập vai NGAY TỪ ĐẦU — học sinh là KỸ SƯ GIÁM SÁT CÔNG TRÌNH
   từ câu mở đầu, không phải giáo viên trình chiếu lỗi trước rồi mới
   giao vai.
🎯 Sai lầm nhắm tới (PPCT):
   (N) vẽ hình chồng chéo, khó nhận diện góc cần tính
   (O) áp nhầm công thức chóp đều cho chóp không đều
   (P) trình bày lan man, thiếu móc suy luận logic
   (Q) gắn nhầm định lí — ĐẶC BIỆT: áp tính chất hình phẳng vào không
       gian (VD "2 đường cùng ⊥ đường thứ 3 thì song song" — CHỈ đúng
       trong mặt phẳng, SAI trong không gian)
📁 File: Bai25_Toan3D_Module4_KySuGiamSat.html
```

> ⚠️ **Bối cảnh:** "Bộ phận Kiểm định Thiết kế" — 5 hồ sơ thiết kế có lỗi
> sai điển hình, mỗi hồ sơ gắn 1 bối cảnh xây dựng cụ thể, cần rà soát
> trước khi cho thi công thật. Ca 5 dùng độ dốc mái nhà (thoát nước
> mưa), phân biệt rõ mái tôn/ngói/bê tông cốt thép — đổi khỏi bối cảnh
> "đường dốc xe lăn" đã dùng ở Bài 24.

## Khung nhập vai (mở đầu module — vào vai ngay, không dẫn nhập dài dòng)

**Athena (mở màn trực tiếp bằng vai diễn):**

> "Chào kỹ sư! Hôm nay bộ phận kiểm định gửi lên 5 hồ sơ thiết kế cần
> rà soát trước khi cho thi công — đội thi công đã báo về vài dấu hiệu
> bất thường ở công trình thực tế, nghi ngờ có sai sót trong bản tính.
> Nhiệm vụ của bạn: đọc hồ sơ, XÁC ĐỊNH đúng lỗi sai, và ĐỀ XUẤT bản sửa
> lại chính xác trước khi phê duyệt thi công. Hồ sơ đầu tiên đã sẵn
> sàng."

**Cấu trúc lặp lại cho mỗi hồ sơ (5 hồ sơ):**
```
1. Hồ sơ thiết kế — hiện lời giải/bản tính SAI kèm hình vẽ 3D minh hoạ
   đúng lỗi đó
2. Dấu hiệu cảnh báo — Athena nêu 1 phản hồi bất thường từ thực tế thi
   công (kết quả vô lý/mâu thuẫn) để gợi ý có gì đó sai, KHÔNG nói thẳng
   lỗi ở đâu
3. Xác định lỗi sai — học sinh chọn ĐÚNG loại lỗi từ danh sách (trắc
   nghiệm nhiều lựa chọn, các lựa chọn là các loại sai lầm N-Q + phương
   án "không có lỗi, bản tính đúng" để tránh đoán mù)
4. Đề xuất bản sửa — học sinh tự sửa lại bước sai (nhập/chọn lại đúng),
   xem bản tính ĐÚNG hiện ra kèm hình minh hoạ đối chiếu
5. Phê duyệt thi công — Athena tổng kết ngắn lỗi này thuộc nhóm nào
   trong hệ thống, đã gặp ở module nào trước đó
```

---

## HỒ SƠ 1 — Góc dốc mái nhà (nhắm sai lầm N, và tái hiện sai lầm A/C từ Module 1)

**Hồ sơ thiết kế:** "Kỹ sư tính góc nhị diện giữa 2 mái dốc gặp nhau tại
nóc nhà. Lời giải dựng 2 tia KHÔNG vuông góc với đường nóc (giao tuyến),
mỗi tia lại xuất phát từ 2 điểm khác nhau trên nóc — hình vẽ dựng thêm
nhiều đường phụ chồng chéo, khó nhận ra tia nào dùng để tính góc."

**Dấu hiệu cảnh báo:** "Kết quả tính ra góc giữa 2 mái là 133,14° — đội
thi công phản hồi: nhìn thực tế 2 mái này KHÔNG hề mở rộng như vậy,
trông chỉ khoảng 50°."

- Verify Python: góc thật (dựng đúng, 2 tia vuông góc giao tuyến, cùng
  điểm) = 50°. Góc sai (2 tia xiên, không vuông góc giao tuyến) = 133,14°
  — sai lệch rất lớn, đúng như phản hồi thực tế.

**Xác định lỗi sai (chọn 1 trong 5):**
- A. Vẽ hình chồng chéo, không xác định đúng 2 tia cần dùng ✓ (đúng)
- B. Tính sai lượng giác
- C. Nhầm công thức lăng trụ
- D. Áp sai tính chất phẳng vào không gian
- E. Bản tính không có lỗi

**Đề xuất bản sửa:** học sinh tự dựng lại đúng 2 tia (vuông góc đường
nóc, cùng 1 điểm) trên hình 3D tương tác, hệ thống tính lại → 50°, khớp
với phản hồi thực tế.

---

## HỒ SƠ 2 — Vách nhà vuông góc sàn, đường chéo mái (tái hiện sai lầm G, Module 2)

**Hồ sơ thiết kế:** "Mái nhà đã được chứng minh vuông góc với tường. Kỹ
sư sau đó kết luận: đường chéo trên mặt mái ĐƯƠNG NHIÊN cũng vuông góc
với sàn nhà, vì 'mái đã vuông góc với tường rồi, mọi đường trong mái đều
vuông góc'."

**Dấu hiệu cảnh báo:** "Đường chéo mái đo thực tế nghiêng khoảng 45° so
với sàn, KHÔNG phải 90° như bản tính kết luận."

- Verify Python: đường chéo (không vuông góc đường nóc/giao tuyến) có
  tích vô hướng với pháp tuyến sàn = 1 (không phải 0) → không vuông góc
  sàn, xác nhận lỗi.

**Xác định lỗi sai:**
- Đáp án đúng: "Nhầm tưởng mọi đường trong 1 mặt đã vuông góc mặt kia
  đều vuông góc — CHỈ đường vuông góc với GIAO TUYẾN mới chắc chắn vuông
  góc mặt kia."

**Đề xuất bản sửa:** học sinh chỉ ra đúng đường nào trong mái (đường
vuông góc đường nóc) mới thực sự vuông góc sàn, đường chéo thì không.

---

## HỒ SƠ 3 — Khung nhà xưởng (tái hiện sai lầm I/K, Module 3)

**Hồ sơ thiết kế:** "Kỹ sư tính thể tích khung nhà xưởng bằng công thức
lăng trụ ĐỨNG (diện tích đáy × chiều cao cạnh bên), áp dụng cho khung có
cạnh bên NGHIÊNG 14° so với đáy (không phải vuông góc)."

**Dấu hiệu cảnh báo:** "Thể tích tính ra lớn hơn thể tích vật liệu thực
tế đã dùng để xây — chênh lệch đáng kể, kế toán vật tư báo động."

- Verify Python: cạnh bên khung nghiêng, tích vô hướng với pháp tuyến
  đáy = 0,97 (không phải 1) → nghiêng 14,04° so với vuông góc — đây là
  lăng trụ XIÊN, không phải đứng, nên công thức lăng trụ đứng áp sai.

**Xác định lỗi sai:**
- Đáp án đúng: "Áp nhầm công thức lăng trụ đứng cho lăng trụ xiên — cần
  dùng chiều cao THẬT (khoảng cách 2 đáy theo phương vuông góc), không
  phải độ dài cạnh bên."

**Đề xuất bản sửa:** học sinh tính lại chiều cao thật (hình chiếu cạnh
bên lên phương vuông góc đáy), thay vào công thức đúng.

---

## HỒ SƠ 4 — Hai thanh xà mái (nhắm TRỰC DIỆN sai lầm Q — quan trọng nhất)

**Hồ sơ thiết kế:** "Kỹ sư có: thanh xà 1 và thanh xà 2 của khung mái,
cả 2 đều đã được đo và xác nhận VUÔNG GÓC với 1 thanh giằng ngang chung.
Bản tính kết luận: 'Vậy xà 1 song song xà 2 — theo tính chất 2 đường
cùng vuông góc 1 đường thứ 3 thì song song.'"

**Dấu hiệu cảnh báo:** "Khi lắp thực tế, 2 thanh xà này KHÔNG nằm cùng 1
mặt phẳng và không song song — chúng bắt chéo nhau trong không gian,
đội lắp ráp báo lỗi không khớp được mối nối."

- Verify Python: xà 1 hướng (0,1,0), xà 2 hướng (0,1,1) chuẩn hoá — cả 2
  đều vuông góc giằng (1,0,0) (dot=0 cả 2), NHƯNG cross product của xà 1,
  xà 2 ≠ 0 → KHÔNG song song, chéo nhau thật.

**Xác định lỗi sai (đây là lỗi QUAN TRỌNG NHẤT, cho thêm thời gian,
không giới hạn lượt thử):**
- Đáp án đúng: "Áp sai tính chất HÌNH PHẲNG vào KHÔNG GIAN — '2 đường
  cùng vuông góc 1 đường thứ 3 thì song song' CHỈ đúng khi cả 3 đường
  cùng nằm trong 1 mặt phẳng. Trong không gian 3 chiều, 2 đường cùng
  vuông góc 1 đường có thể CHÉO NHAU (như xà 1, xà 2 ở đây)."

**Đề xuất bản sửa:** hệ thống cho xoay mô hình 3D của xà 1, xà 2, giằng
— học sinh tự quan sát xà 1, xà 2 không đồng phẳng, xác nhận trực quan
tại sao kết luận "song song" là sai.

> 💡 **Ghi chú thiết kế:** đây là lỗi tư duy SÂU nhất trong cả bài — nên
> đặt ở vị trí hồ sơ thứ 4 (không phải đầu hay cuối), sau khi học sinh đã
> "vào phong độ" với 3 hồ sơ trước nhưng vẫn còn tỉnh táo, tránh đặt cuối
> cùng lúc học sinh có thể đã mỏi.

---

## HỒ SƠ 5 — Độ dốc mái nhà: tôn, ngói, hay bê tông? (nhắm sai lầm F/M)

**Hồ sơ thiết kế:** "Nhà xưởng đo được: chiều cao mái H = 1,2m, chiều
dài mái theo phương ngang L = 8m. Kỹ sư tính độ dốc = H/L × 100% = 15%,
rồi kết luận LUÔN: 'Vậy góc dốc mái là 15°.'"

**Dấu hiệu cảnh báo:** "Đội thi công đo góc thật bằng thước đo góc, ra
kết quả khoảng 8,5° — chênh lệch gần 1 nửa so với con số 15° trong hồ
sơ."

- Verify Python: độ dốc 15% ≠ 15° — góc ĐÚNG = arctan(0,15) ≈ 8,53°,
  chênh lệch 6,47° so với số sai.

**Xác định lỗi sai:**
- Đáp án đúng: "Nhầm PHẦN TRĂM độ dốc với SỐ ĐO GÓC trực tiếp — % độ dốc
  là tỉ số H/L, phải dùng arctan để đổi ra độ, không được coi % = độ."

**Đề xuất bản sửa (mở rộng thêm — phân biệt 3 loại mái):**
- Sau khi sửa đúng góc = 8,53°, Athena hỏi tiếp: "Với góc dốc 8,53° này,
  mái nhà nên lợp bằng vật liệu gì trong 3 lựa chọn sau, để đảm bảo thoát
  nước đúng chuẩn kỹ thuật?"
  - A. Mái tôn (độ dốc phổ biến 10%-30%, tương đương ~6°-17°)
  - B. Mái ngói (độ dốc phổ biến 30%-60%, tương đương ~17°-31°)
  - C. Mái bê tông cốt thép (độ dốc phổ biến 5%-8%, tương đương ~2,9°-4,6°)
  - `dap_an_dung`: A (mái tôn) — vì 8,53° nằm trong khoảng 6°-17° của
    tôn, không đủ dốc cho ngói (cần ≥17°) và dốc hơn hẳn mức bê tông
    (chỉ 2,9°-4,6°).
  - ⚠️ Lưu ý hiển thị cho học sinh: đây là **hướng dẫn kỹ thuật phổ biến**
    trong xây dựng (dao động theo nguồn/công trình cụ thể), KHÔNG phải 1
    quy chuẩn pháp lý cố định duy nhất (khác chuẩn đường dốc xe lăn
    QCVN đã học ở Bài 24).

---

## TỔNG HỢP KIẾN THỨC (đóng Module 4 — đóng cả 4 module Bài 25)

| Hồ sơ | Lỗi sai | Nhắc lại từ |
|---|---|---|
| 1 | Vẽ hình chồng chéo, chọn sai 2 tia dựng góc nhị diện | Module 1 |
| 2 | Nghĩ mọi đường trong mặt đã ⊥ đều tự động ⊥ mặt kia | Module 2 |
| 3 | Áp nhầm công thức lăng trụ đứng cho lăng trụ xiên | Module 3 |
| 4 | **Áp sai tính chất hình phẳng vào không gian** (quan trọng nhất) | Tổng hợp toàn bài |
| 5 | Nhầm % độ dốc với số đo góc trực tiếp | Ứng dụng thực tế |

**Athena (đóng vai, chốt lại buổi kiểm định):** "Cảm ơn kỹ sư đã hoàn
thành rà soát 5 hồ sơ hôm nay! Điều quan trọng nhất rút ra: trong không
gian 3 chiều, một số 'lẽ thường' quen thuộc từ hình học phẳng (như '2
đường cùng vuông góc 1 đường thì song song') KHÔNG còn đúng nữa — luôn
cần kiểm tra kỹ trước khi phê duyệt thi công."

## Rủi ro kỹ thuật 3D

```
✅ An toàn: cả 5 hồ sơ (hiện bản tính sai + hình minh hoạ tĩnh + trắc
   nghiệm xác định lỗi + sửa lại) — không cần pattern 3D mới, tái dùng
   toàn bộ `isPerpendicular`/`angleBetweenLines` (06 PHẦN C.3) đã verify.
✅ An toàn: Hồ sơ 4 (xoay mô hình 3D xà 1, xà 2, giằng để quan sát không
   đồng phẳng) — chỉ cần OrbitControls cơ bản, không cần tương tác kéo
   thả.
```

---

> **Trạng thái:** Module 4 (Bài 25) đã có kịch bản đầy đủ 5 hồ sơ thiết
> kế, nhập vai kỹ sư giám sát công trình ngay từ đầu, số liệu đã verify
> bằng Python. Hồ sơ 4 (áp sai tính chất phẳng vào không gian) được
> thiết kế kỹ nhất theo đúng yêu cầu "làm kỹ" đã đề ra từ đầu Bài 22. Lab
> (mở rộng solid_library.html) sẽ ra kịch bản ở phiên tiếp theo — hoàn
> tất toàn bộ Bài 25.
