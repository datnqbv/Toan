# Module 1: Quy tắc cộng
### Bài 23 — Quy tắc đếm | Toán 10, Chương VIII | Chủ đề 47

---

**Mục tiêu:** Học sinh phát biểu và vận dụng đúng quy tắc cộng, nhận ra và giải thích được điều kiện bắt buộc "hai phương án phải rời nhau (không giao nhau)".

**Sai lầm cần giải quyết:** Cộng thẳng số phần tử của 2 tập hợp mà không trừ đi phần giao, khi 2 tập hợp đó không rời nhau.

**Loại simulation:** Khám phá tự do → dự đoán trước khi thấy kết quả → đối chất bằng đếm tay trực tiếp trên sơ đồ.

**Thời gian hoàn thành dự kiến:** ~8 phút.

**Dạy từ đầu hay tổng kết:** Dạy từ đầu, theo mạch Problem → khám phá → khái quát hoá (không đưa quy tắc trước).

---

## 🎬 Ảnh hook mở đầu — prompt tạo ảnh (dùng ảnh thật, không phải SVG)

```
A bright, realistic photo of a Vietnamese high school classroom from an elevated
angle, showing several rows of wooden student desks. On some desks there is a
small green sticky note or badge (representing Chess Club membership), on others
a small orange sticky note or badge (representing Music Club membership), and on
a few desks BOTH a green and an orange note are placed side by side — clearly
visible from above. Natural daylight coming through classroom windows, warm and
clean color tones, tidy and modern classroom, no visible faces or identifiable
students (desks can be shown empty or with students seen only from behind/above
to keep it anonymous). Documentary/editorial education-photography style, keep
the whole desk layout in sharp focus so all color tags are readable. Aspect
ratio 16:9.

Avoid: any text/writing on the notes, any branded logos, any blurry or unreadable
color tags, any student faces visible.
```

**Cách dùng trong module:** Ảnh hiện toàn màn hình (hoặc full-width trên mobile) làm màn hình đầu tiên khi mở module. Bên dưới ảnh là khung thoại Athena và 1 nút bấm để chuyển sang canvas tương tác.

**Lời thoại Athena tại hook (nguyên văn hiển thị):**
> "Đây là lớp 10A — chuẩn bị cho lễ ra mắt CLB, nhà trường cần in thẻ đại biểu cho các bạn tham gia ít nhất 1 trong 2 CLB Cờ vua hoặc Âm nhạc. Bạn giúp mình đếm xem cần in bao nhiêu thẻ nhé?"

**Nút chuyển màn hình:** `[ Bắt đầu đếm → ]` — bấm vào sẽ chuyển từ ảnh thật sang canvas tương tác (Bước 1).

---

## 🖼️ Phác thảo canvas — Sơ đồ lớp học tương tác (thay thế ảnh thật ở phần đếm)

> Từ Bước 1 trở đi, KHÔNG dùng ảnh thật nữa (ảnh thật chỉ để "vào bài") — chuyển sang canvas/HTML vẽ bằng code để có thể click, đổi trạng thái từng ô.

**Kích thước lưới:** 7 cột × 5 hàng = 35 ô bàn.
**Kích thước 1 ô (desktop):** 90×64px, bo góc `rx=8`, khoảng cách giữa các ô 14px.
**Kích thước 1 ô (mobile ≤767px):** thu nhỏ theo tỉ lệ để vừa 7 cột trong màn hình hẹp (khoảng 42×32px/ô), vẫn giữ đủ 7 cột — KHÔNG rút gọn xuống ít cột hơn để không làm sai cấu trúc lưới.

**Legend cố định phía trên canvas (có chữ, khác với ảnh hook nghệ thuật):**
`🟩 CLB Cờ vua` `🟧 CLB Âm nhạc` `🟨 Cả hai CLB` — hiển thị dạng 3 chip màu kèm nhãn chữ, đặt ngay trên lưới.

**4 trạng thái thị giác của 1 ô bàn:**
1. *Mặc định:* viền mờ `#D8C39A`, nền `#F6EAD6`, con trỏ bình thường.
2. *Hover (khi rê chuột, hoặc chạm trên mobile):* viền đậm hơn, đổi con trỏ thành pointer, nền sáng nhẹ hơn 5%.
3. *Đã click trong Bước 1/2 (đang đếm):* hiện dấu ✓ nhỏ góc trên-trái ô, không đổi màu nền.
4. *Đang bị highlight đối chất (Bước 4):* viền vàng `#F2C94C` nhấp nháy 3 lần trong 1.5 giây, sau đó tắt hiệu ứng.
5. *Đã đếm trong Bước 4:* nền mờ đi (opacity 0.5) + hiện số thứ tự nhỏ góc dưới-phải (1, 2, 3…) để học sinh tự theo dõi đã đếm đến đâu, tránh lỗi thao tác đếm trùng (không phải hỗ trợ hiểu bài).

**Bảng gán màu cụ thể cho 35 ô (hàng × cột) — đội build dùng đúng bảng này khi code:**

| | Cột 1 | Cột 2 | Cột 3 | Cột 4 | Cột 5 | Cột 6 | Cột 7 |
|---|---|---|---|---|---|---|---|
| **Hàng 1** | Xanh | Trống | **Cả hai** | Cam | Trống | Xanh | Trống |
| **Hàng 2** | Trống | Xanh | Xanh | Cam | Xanh | **Cả hai** | Trống |
| **Hàng 3** | **Cả hai** | Cam | Trống | Xanh | Trống | Cam | Trống |
| **Hàng 4** | Trống | Xanh | Cam | **Cả hai** | Trống | Trống | Xanh |
| **Hàng 5** | Cam | Trống | Xanh | Trống | Trống | Cam | **Cả hai** |

**Kiểm chứng số liệu (đã đối chiếu khớp bảng trên):**
- Xanh riêng (chỉ Cờ vua): 9 ô
- Cam riêng (chỉ Âm nhạc): 7 ô
- Cả hai: 5 ô (rải rác theo đường chéo, không ô nào liền kề ô "cả hai" khác — tránh học sinh đoán mò bằng mắt)
- Trống: 14 ô
- Tổng Cờ vua = 9 + 5 = **14**, Tổng Âm nhạc = 7 + 5 = **12**, Tổng có nhãn = 9+7+5 = **21**, Tổng lớp = 35 ✓

---

## Chi tiết từng bước (lời thoại Athena + hành vi canvas)

### Bước 1 — Đếm bàn "Cờ vua"

**Athena nói (nguyên văn):**
> "Bạn hãy click vào từng bàn có nhãn xanh lá — kể cả những bàn có cả 2 màu — để đếm số bạn tham gia CLB Cờ vua. Đếm xong thì nhấn Xác nhận nhé."

**Hành vi canvas:**
- Học sinh click vào 1 ô có nhãn xanh HOẶC ô "cả hai": ô hiện dấu ✓, số đếm ở panel bên phải (hoặc dưới lưới trên mobile) tăng dần theo thời gian thực, có hiệu ứng đếm số chạy (không giật cục).
- Click nhầm ô "Cam" hoặc "Trống": ô rung nhẹ 200ms, không tính vào số đếm, không có thông báo lỗi bằng chữ (để học sinh tự nhận ra qua hiệu ứng rung).
- Click lại 1 ô đã đếm rồi: bỏ đếm ô đó (toggle), số đếm giảm lại — cho phép học sinh tự sửa nếu bấm nhầm.
- Nút `[ Xác nhận ]` luôn bấm được (không khoá), khi bấm mà số đếm ≠ 14: hiện dòng nhỏ "Bạn thử đếm lại xem đã đủ chưa nhé" và cho đếm tiếp, không giới hạn số lần (đây là bước `explored`, không chấm điểm nghiêm ngặt).
- Khi đúng 14: chuyển tự động sang Bước 2, số đếm 14 được "khoá" hiển thị ở góc màn hình để đối chiếu về sau.

### Bước 2 — Đếm bàn "Âm nhạc"

**Athena nói (nguyên văn):**
> "Tốt lắm! Giờ bạn đếm tiếp những bàn có nhãn cam — kể cả những bàn có cả 2 màu — để ra số bạn tham gia CLB Âm nhạc."

**Hành vi canvas:** giống hệt cơ chế Bước 1 (áp dụng cho nhãn cam + ô "cả hai"), số đếm đúng cần đạt là 12.

### Bước 3 — Dự đoán tổng

**Athena nói (nguyên văn):**
> "Bạn vừa đếm được 14 bàn Cờ vua và 12 bàn Âm nhạc. Theo bạn, tổng cộng có bao nhiêu bạn tham gia ÍT NHẤT 1 trong 2 CLB? Nhập số và nhấn Kiểm tra."

**Hành vi canvas:**
- 1 ô input số (chỉ nhận số nguyên dương), nút `[ Kiểm tra ]`.
- Học sinh nhập rỗng hoặc không phải số: hiện lỗi đỏ nhỏ ngay dưới ô input "Nhập một số bạn nhé", không cho qua bước tiếp.
- Sau khi nhập hợp lệ và bấm Kiểm tra: **không hiện đúng/sai ngay** — chuyển thẳng sang Bước 4 kèm câu thoại nối tiếp:
> Athena: "Mình sẽ không nói đúng hay sai vội — mình cùng đếm lại thật kỹ trên sơ đồ nhé."

### Bước 4 — Đối chất bằng đếm tay

**Athena nói (nguyên văn):**
> "Sơ đồ vừa nhấp nháy vàng ở một số ô đặc biệt. Bạn hãy click ĐÚNG 1 LẦN vào mỗi bàn có nhãn (bất kỳ màu nào) để đếm lại tổng số bạn có nhãn trên toàn bộ lớp."

**Hành vi canvas:**
1. Ngay khi vào bước này, 5 ô "cả hai" tự động nhấp nháy viền vàng 3 lần trong 1.5 giây rồi tắt (không giải thích lý do bằng chữ).
2. Học sinh click từng ô có nhãn (xanh/cam/cả hai) — mỗi ô click lần đầu: mờ đi (opacity 0.5) + hiện số thứ tự đếm góc dưới-phải; số đếm tổng bên panel tăng dần.
3. Nếu học sinh click lại 1 ô đã mờ (đã đếm): hiện dòng nhỏ dưới ô "Bàn này đã được đếm rồi, bạn có chắc muốn đếm thêm không?" kèm 2 nút `[ Đếm lại ]` / `[ Bỏ qua ]` — không tự động chặn, để học sinh tự quyết định (đúng tinh thần "tự đối chất", không phải hệ thống chỉ lỗi hộ).
4. Khi đã click đủ 21 ô có nhãn: nút `[ Xong, tôi đã đếm lại ]` sáng lên, học sinh bấm để sang Bước 5.

### Bước 5 — Nhập lại đáp án đúng

**Athena nói (nguyên văn):**
> "Bạn vừa đếm lại được [số học sinh vừa đếm ở Bước 4] bàn có nhãn. So với dự đoán ban đầu là [số ở Bước 3], hai số này có khớp nhau không? Bạn hãy nhập lại đáp án đúng nhé."

**Hành vi canvas:** 1 ô input số + nút `[ Kiểm tra ]`, áp dụng đúng 3-strike:
- **Lần sai 1:** ô input rung nhẹ, không có gợi ý chữ.
- **Lần sai 2:** Athena hiện gợi ý (nguyên văn): *"Bạn thử nhìn lại: trong 21 bàn có nhãn, có bàn nào mang cả 2 màu không? Nếu dự đoán ban đầu bạn cộng 14 + 12, mỗi bàn 2 màu đó bị tính mấy lần?"*
- **Lần sai 3:** hiện đáp án đúng kèm giải thích đầy đủ (nguyên văn): *"Đáp án đúng là 21. Vì 14 + 12 = 26, nhưng 5 bạn tham gia cả hai CLB đã bị cộng 2 lần trong phép tính này — nên phải trừ đi: 14 + 12 − 5 = 21."*
- **Trả lời đúng (ở bất kỳ lần thử nào):** *"Chính xác! Bạn vừa tự phát hiện ra: khi 2 nhóm có phần chung, không thể cộng thẳng hai số — phải trừ đi phần đã đếm trùng."*

### Bước 6 — Athena khái quát hoá thành quy tắc

**Athena nói (nguyên văn):**
> "Từ bài toán lớp học vừa rồi, mình rút ra được: nếu một công việc có thể thực hiện theo 1 trong 2 phương án hoàn toàn tách biệt nhau (không trùng), số cách thực hiện bằng tổng số cách của từng phương án — đây gọi là quy tắc cộng. Nhưng nếu 2 phương án có phần chung, như 2 CLB có bạn tham gia cả hai, bạn phải trừ đi phần chung đó trước khi cộng."

Sổ tay kiến thức xuất hiện từ đây (bấm gọi lại được ở module sau):
```
- Quy tắc cộng: nếu công việc có n₁ cách theo phương án 1, n₂ cách theo
  phương án 2, và 2 phương án KHÔNG trùng nhau, thì có n₁ + n₂ cách.
- Nếu 2 phương án có phần chung: phải trừ đi phần chung trước khi cộng.
```

### Bước 7 — Mở rộng (không bắt buộc)

**Athena nói (nguyên văn):**
> "Nếu muốn thử áp dụng ngay, bạn có thể làm thêm 1 tình huống nữa — hoặc bấm Hoàn thành để qua phần tiếp theo."

**Tình huống:** Lớp 10B có 30 học sinh, CLB Mỹ thuật 10 bạn, CLB Cầu lông 9 bạn, 3 bạn tham gia cả hai → đáp án 16. Chỉ 1 ô input, có 3-strike như Bước 5 nhưng **không có canvas minh hoạ** (chỉ là bài toán chữ để luyện áp dụng thuần tuý). Không hoàn thành bước này cũng không chặn nút Hoàn thành module.

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Hook ảnh thật chiếm toàn màn hình ở bước 0. Từ Bước 1 trở đi: lưới 35 ô đặt bên trái (~65% chiều rộng), panel bên phải (35%) cố định gồm khung thoại Athena, số liệu đếm real-time, ô nhập đáp án.

**Mobile (≤767px):** Bước 0 hook ảnh full-width. Từ Bước 1: xếp dọc — lưới 35 ô hiện TRƯỚC (giữ đủ 7 cột, thu nhỏ theo tỉ lệ), khung thoại Athena + số liệu đếm + ô nhập đáp án xuống SAU. Không cần layout lướt ngang vì đây không phải dạng nhiều thẻ bước khoá dần cạnh 1 canvas cố định — chỉ có 1 canvas xuyên suốt cả module.

---

## 🔗 Athena Context & Tích hợp LMS

### `structure[]`

```javascript
structure: [
  { id: 'm1_dem_xanh',       type: 'explored', required: true },
  { id: 'm1_dem_cam',        type: 'explored', required: true },
  { id: 'm1_du_doan',        type: 'answered', required: true },
  { id: 'm1_doi_chat',       type: 'explored', required: true },
  { id: 'm1_dap_an_dung',    type: 'answered', required: true },
  { id: 'm1_mo_rong',        type: 'answered', required: false }
]
```

`progress total = 5` (không tính `m1_mo_rong`, required:false).

### Sự kiện LMS theo từng bước

| Bước | Sự kiện | Ghi chú |
|---|---|---|
| 1, 2 | `LMS().event('explored', {id, trial})` | Đếm quan sát, không có khái niệm đúng/sai |
| 3 | `LMS().event('answered', {id: 'm1_du_doan', value})` | Lần dự đoán đầu tiên — vẫn ghi nhận dù sẽ sai |
| 4 | `LMS().event('explored', {id: 'm1_doi_chat', trial})` | Đếm lại bằng click — khám phá, không chấm điểm |
| 5 | `LMS().event('answered', {id: 'm1_dap_an_dung', tries})` | Đáp án cuối cùng, đếm số lần thử (tối đa 3) |
| 7 | `LMS().event('answered', {id: 'm1_mo_rong', required:false})` | Không chặn `LMS().complete()` |

`LMS().complete()` gọi ngay sau khi Bước 5 đạt đúng, không phụ thuộc Bước 7.

### `athenaGuidance` (nguyên văn, khớp đúng 5 mục bắt buộc)

```
1. m1_dem_xanh / m1_dem_cam: Athena chỉ xác nhận học sinh đã đếm đủ số
   bàn có nhãn tương ứng trên sơ đồ (14 bàn xanh gồm cả ô "cả hai", 12
   bàn cam gồm cả ô "cả hai"). Không gợi ý trước về việc có ô trùng.
2. m1_du_doan: nếu học sinh hỏi gợi ý ở bước này, Athena chỉ được hỏi
   ngược: "Bạn thử nghĩ xem, cách bạn vừa đếm ở 2 bước trước có bỏ sót
   hay tính trùng bàn nào không?" — KHÔNG được nói trước đáp án 21 hay
   nhắc tới con số 5 bàn trùng.
3. m1_doi_chat: Athena chỉ nhắc lại đúng câu: "Bạn hãy click đúng 1 lần
   vào mỗi bàn có nhãn để đếm lại." Không giải thích thêm lý do vì sao.
4. m1_dap_an_dung: gợi ý ở lần sai thứ 2 CHỈ được dùng đúng câu:
   "Bạn thử nhìn lại: trong 21 bàn có nhãn, có bàn nào mang cả 2 màu
   không? Nếu dự đoán ban đầu bạn cộng 14 + 12, mỗi bàn 2 màu đó bị
   tính mấy lần?" — không được nói thẳng đáp án 21 ở gợi ý này.
5. m1_mo_rong: bước không bắt buộc, Athena có thể nhắc học sinh có thể
   bỏ qua bước này nếu muốn hoàn thành module ngay.
```

---

## Tổng kết kiến thức

> **Quy tắc cộng:** Nếu một công việc có thể thực hiện theo một trong hai phương án khác nhau, phương án một có n₁ cách, phương án hai có n₂ cách, và **hai phương án này không có cách nào chung nhau**, thì công việc đó có n₁ + n₂ cách thực hiện.
>
> ⚠️ Nếu hai phương án có phần chung (như ví dụ 2 CLB có bạn tham gia cả hai), phải trừ đi số cách bị đếm trùng trước khi cộng.
