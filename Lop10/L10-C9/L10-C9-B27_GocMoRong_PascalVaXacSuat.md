# Góc mở rộng: Pascal và hành trình xác suất — từ trò chơi xúc xắc đến AI
### Dựa trên "Em có biết" — Bài 26, Bài 27 và Bài tập cuối Chương IX

---

**Vị trí trong chương trình:** Module mở rộng độc lập, KHÔNG thuộc chuỗi module bắt buộc của Bài 26/27 — dành cho học sinh muốn hiểu vì sao Xác suất trở thành 1 trong những ngành toán quan trọng nhất hiện nay.

**Mục tiêu:** Học sinh trải nghiệm lại đúng bài toán lịch sử đã khai sinh Lý thuyết Xác suất (bức thư gửi Pascal năm 1654), biết thêm về Pascal như 1 thiên tài đa lĩnh vực, và thấy được mạch phát triển của xác suất từ trò chơi may rủi đến vai trò nền tảng của AI/học máy hiện nay.

**Loại simulation:** Khám phá tự do (mô phỏng trò chơi lịch sử) + showcase thông tin (không chấm điểm nghiêm ngặt).

**Thời gian trải nghiệm dự kiến:** ~10 phút (không bắt buộc hoàn thành hết).

---

## Sổ tay kiến thức nền tảng

```
- Xác suất cổ điển P(E) = n(E)/n(Ω) — đã học ở Bài 26.
- Biến cố đối P(Ē) = 1 − P(E) — đã học ở Bài 26, Bài 27.
- Blaise Pascal (1623-1662): nhà toán học, vật lý học, triết học Pháp.
  Cùng Pierre de Fermat trao đổi thư từ năm 1654 để giải quyết 1 bài
  toán cờ bạc — sự kiện được coi là khởi đầu chính thức của Lý thuyết
  Xác suất.
```

---

## 🎬 Ảnh hero mở đầu module — prompt tạo ảnh

```
Style guide dùng chung cho cả bộ 4 ảnh trong module này: warm documentary/
editorial photography style, muted warm tones (browns, creams, soft golds)
cho các cảnh lịch sử, chuyển sang tông lạnh xanh/xanh ngọc cho các cảnh
công nghệ hiện đại, tỉ lệ khung hình 16:9 nhất quán, chi tiết cao, không
chữ/logo hiển thị trừ khi ghi chú khác.
```

```
A single wide artistic composite image, split diagonally into two halves
that blend smoothly into each other. Left half: a 17th-century wooden desk
scene in warm sepia tones — an old dice, a quill pen, a sealed handwritten
letter, aged parchment paper, soft candlelight. Right half: a modern,
softly glowing abstract neural network visualization in cool blue/teal
tones — thin glowing lines connecting nodes, resembling circuitry or a
constellation. The transition between the two halves should feel like a
gradient blending warm historical light into cool digital light, symbolizing
a journey from the 17th century to modern AI. No text, no human figures,
no faces. Aspect ratio 16:9.
```

**Lưu ý:** Pascal là nhân vật lịch sử thật — mọi ảnh trong module này chỉ mô tả bối cảnh/vật dụng thời đại, KHÔNG yêu cầu tạo khuôn mặt/chân dung giống Pascal, để tránh vấn đề chân dung người thật.

---

## Phần 1 — Bức thư định hình 1 ngành khoa học (1654)

### 🎬 Ảnh mở đầu Phần 1 — prompt tạo ảnh

```
A realistic flat-lay/genre-scene photo of a 17th-century writing desk,
shot at a slight angle. On the wooden desk: a pair of ivory dice, a
handwritten letter partially unrolled with elegant cursive (illegible,
decorative squiggles only, no real text), a wax seal and stamp, a quill
pen resting in an inkwell, a small candle holder with a lit candle. Warm,
soft window light from one side. No people, no faces, no visible modern
objects. Aspect ratio 16:9.

Avoid: any modern text, dates, or legible words on the letter; any human
figures or hands.
```

**Athena:** *"Năm 1654, một nhà quý tộc viết thư hỏi Pascal về 1 trò chơi xúc xắc, đưa ra 3 phương án cược, và hỏi nên chọn phương án nào để có tỉ lệ thắng cao nhất:"*

- **Phương án 1:** Gieo xúc xắc cân đối liên tiếp 6 lần. Thắng nếu có ÍT NHẤT 1 lần ra mặt 6.
- **Phương án 2:** Gieo liên tiếp 12 lần. Thắng nếu có ÍT NHẤT 2 lần ra mặt 6.
- **Phương án 3:** Gieo liên tiếp 18 lần. Thắng nếu có ÍT NHẤT 3 lần ra mặt 6.

**Canvas:** 3 nút chọn phương án, mỗi nút kèm nút "Chơi thử nhanh 1000 lượt" — mô phỏng ngay 1000 lượt chơi theo đúng phương án đã chọn, hiện tỉ lệ thắng thực nghiệm (%) cập nhật theo thời gian thực trong lúc mô phỏng.

**Athena:** *"Bạn hãy thử cả 3 phương án, so sánh tỉ lệ thắng thực nghiệm — phương án nào có tỉ lệ thắng cao nhất?"*

- Học sinh tự thử, sẽ thấy Phương án 1 có tỉ lệ thắng thực nghiệm cao nhất (≈66-67%), tiếp theo Phương án 2 (≈61-62%), thấp nhất là Phương án 3 (≈59-60%).

**Athena chốt (đã kiểm chứng bằng tính toán chính xác — không chỉ mô phỏng):**

> *"Pascal đã tính CHÍNH XÁC (không cần mô phỏng, chỉ dùng toán học) 3 tỉ lệ thắng này: Phương án 1 ≈ 0,6651; Phương án 2 ≈ 0,6187; Phương án 3 ≈ 0,5973. Ông khuyên nhà quý tộc chọn Phương án 1. Chính bức thư trao đổi giữa Pascal và Fermat để giải bài toán này được coi là sự kiện khai sinh Lý thuyết Xác suất."*

> ✅ Đã kiểm chứng bằng Python trước khi đưa vào kịch bản: dùng phân phối nhị thức B(n, 1/6), tính P(X≥k) cho (n,k) = (6,1), (12,2), (18,3) — kết quả khớp đúng 0,6651 / 0,6187 / 0,5973 như SGK đã nêu.

---

## Phần 2 — Pascal: thiên tài đa lĩnh vực

### 🎬 Ảnh mở đầu Phần 2 — prompt tạo ảnh

```
A realistic still-life photo arranged on an antique wooden table, shot
from directly above (flat-lay). Three objects arranged with visual balance:
(1) an old geometric diagram on yellowed parchment showing a hexagon
inscribed with intersecting lines (evoking 17th-century geometry, no
legible text), (2) a small antique brass mechanical calculating device
with dials and gears (evoking an early mechanical calculator), (3) an old
leather-bound book lying open with blank/illegible pages, a quill resting
on top. Warm sepia and gold tones, soft directional lighting, slightly
dramatic shadows. No people, no faces, no legible modern text.

Avoid: any portrait, face, or human figure; any modern branding.
```

**Canvas:** dòng thời gian tuổi tác của Pascal, mỗi mốc là 1 thẻ thông tin học sinh bấm vào để mở rộng:

| Tuổi | Thành tựu |
|---|---|
| 16 | Công bố công trình về thiết diện đường conic — sau này gọi là "Định lí Pascal về lục giác thần kì", rút ra được 400 hệ quả hình học. |
| 17 | Chế tạo chiếc máy tính cơ học đầu tiên trong lịch sử nhân loại — làm được 4 phép tính cộng, trừ, nhân, chia. |
| 28 | Toán học hoá các trò chơi may rủi — khai sinh Lý thuyết Xác suất. |

**Athena:** *"Ngoài toán học, Pascal còn là nhà vật lý, triết học, và nhà văn. 2 câu nói nổi tiếng của ông:"*

> *"Con người chỉ là một cây sậy, một vật rất yếu đuối của tự nhiên, nhưng là một cây sậy biết suy nghĩ."*
>
> *"Trái tim có những lí lẽ mà lí trí không giải thích được."*

---

## Phần 3 — Từ trò chơi may rủi đến AI hiện đại

### 🎬 Ảnh mở đầu Phần 3 — prompt tạo ảnh

```
A realistic, modern photo composite showing 3 small vignettes arranged
side by side, all in cool blue and white tones with a clean tech aesthetic:
(1) a self-driving car's dashboard display showing an abstract probability
visualization (soft glowing bars, no legible text or numbers), (2) a close-up
of a smartphone screen showing an abstract chat interface with soft glowing
suggestion bubbles (no legible text), (3) an abstract visualization of a
neural network as glowing interconnected dots and lines in 3D space. Clean,
minimal, professional tech-editorial photography style. Aspect ratio 16:9.

Avoid: any real brand logos, any legible text/UI labels, any human faces.
```

**Canvas:** dòng thời gian 4 mốc (1654 Pascal-Fermat → 1814 Laplace định nghĩa cổ điển của xác suất → đầu thế kỉ 20 ứng dụng vào di truyền học và bảo hiểm → hiện nay AI/học máy).

**Athena:** *"Sau Pascal, nhà toán học Laplace hệ thống hoá thành định nghĩa cổ điển bạn đang học ở Bài 26. Sang thế kỉ 20, xác suất trở thành công cụ cho di truyền học (nhớ lại định luật Hardy-Weinberg ở Bài 24) và ngành bảo hiểm. Ngày nay, mọi mô hình AI — từ xe tự lái đến chatbot dự đoán từ tiếp theo — đều vận hành dựa trên việc tính toán và so sánh XÁC SUẤT. Không có bức thư năm 1654 giữa Pascal và Fermat, có thể chúng ta sẽ không có nền tảng toán học cho AI hiện đại."*

---

## Bố cục giao diện — Desktop & Mobile

**Desktop (≥1024px):** Mỗi Phần là 1 khối lớn xếp dọc. Phần 1 có canvas mô phỏng bên trái ~65%, khung thoại bên phải ~35%. Phần 2, 3 là dòng thời gian full-width, các thẻ mốc xếp ngang.

**Mobile (≤767px):** Giữ nguyên thứ tự dọc. Dòng thời gian ở Phần 2, 3 đổi thành xếp dọc (mỗi mốc 1 thẻ, xếp từ trên xuống) thay vì ngang, vì ngang sẽ quá chật trên màn hình hẹp. Vùng chạm mỗi nút/thẻ ≥44px.

---

## 🔗 Athena Context & Tích hợp LMS

Vì đây là module MỞ RỘNG, không bắt buộc, TOÀN BỘ sự kiện đánh dấu `required:false`.

### `structure[]`
```javascript
structure: [
  { id: 'mr_choi_thu_pa1', type: 'explored', required: false },
  { id: 'mr_choi_thu_pa2', type: 'explored', required: false },
  { id: 'mr_choi_thu_pa3', type: 'explored', required: false },
  { id: 'mr_pascal_thanh_tuu', type: 'explored', required: false },
  { id: 'mr_dong_thoi_gian_ai', type: 'explored', required: false }
]
```
`progress total = 0`.

### `athenaGuidance`
```
1-3. mr_choi_thu_pa1..3: chỉ khuyến khích thử đủ cả 3 phương án trước
   khi so sánh, không tiết lộ số liệu chính xác của Pascal trước khi
   học sinh tự mô phỏng xong cả 3.
4-5. mr_pascal_thanh_tuu, mr_dong_thoi_gian_ai: đây là nội dung đọc
   thông tin (showcase), Athena chỉ trả lời câu hỏi nếu học sinh hỏi
   thêm, không cần gợi ý/chấm điểm.
```

---

## Tổng kết kiến thức

> Lý thuyết Xác suất không phải sinh ra từ 1 phòng thí nghiệm, mà từ 1 bức thư năm 1654 giữa 2 nhà toán học Pascal và Fermat, xuất phát từ câu hỏi rất đời thường: "nên chọn phương án cờ bạc nào?". Từ đó, xác suất phát triển qua Laplace, ứng dụng vào di truyền học và bảo hiểm, và ngày nay trở thành nền tảng toán học cho toàn bộ các mô hình AI và học máy hiện đại — một minh chứng cho việc những câu hỏi toán học đơn giản nhất đôi khi lại mở ra những ngành khoa học quan trọng nhất.
