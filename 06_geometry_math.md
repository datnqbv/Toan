# 📐 GEOMETRY MATH — Hàm toán thuần cho hình học không gian 3D

> **Mục đích:** Tập hợp MỌI hàm toán thuần (chỉ nhận/trả `Vector3`, `number`,
> object toạ độ — KHÔNG bao giờ tạo `THREE.Mesh`/`THREE.Line`, KHÔNG bao giờ
> gọi `scene.add()`) đã được viết và verify trong các file test thực tế.
> **Dùng kèm:** `05_threejs_engine.md` (pattern dựng mesh/tương tác dùng các hàm này)
> **Đọc file này khi:** cần 1 công thức hình học cụ thể (chiếu, khoảng cách,
> góc, giao tuyến, phân loại quan hệ) — copy đúng hàm, không tự viết lại.

---

## NGUYÊN TẮC TÁCH FILE — vì sao 06 khác 05

```
05_threejs_engine.md → PATTERN: cách dùng hàm toán để dựng mesh, xử lý
  input, đồng bộ label, tối ưu hiệu năng khi kéo — nhiều code trong 05
  gọi lại đúng các hàm ở đây, không viết lại công thức.

06_geometry_math.md (file này) → CÔNG THỨC THUẦN: mọi hàm ở đây có thể
  chạy trong Node.js trần, không cần THREE.WebGLRenderer, không cần DOM.
  Input/output chỉ là THREE.Vector3 (hoặc object chứa Vector3) và number.

Quy tắc phân loại 1 hàm thuộc file nào: nếu hàm có dòng `new THREE.Mesh`,
`new THREE.Line`, hoặc `scene.add()` → thuộc 05. Nếu không → thuộc 06.
```

> **Lưu ý về phụ thuộc biến toàn cục:** một số hàm trong file test gốc đọc
> trực tiếp biến toàn cục của app (`solidRenderer.vertices`, `currentSolidKey`,
> `currentRoundParams`) để tiện gọi. Ở đây mọi hàm được viết lại ở dạng
> **tổng quát** — nhận đủ tham số qua argument, không đọc global — để copy
> sang project khác dùng ngay, không cần bê theo biến toàn cục của app gốc.
> Phần "Cách dùng trong app thực tế" ở mỗi mục chỉ ra cách wrap lại nếu cần.

---

## PHẦN A — MẶT PHẲNG

### A.1 Định nghĩa mặt phẳng từ 3 điểm

```javascript
// Trả { normal, pointOnPlane } — normal ĐÃ NORMALIZE (n·n = 1)
// Trả null nếu 3 điểm thẳng hàng (không xác định mặt phẳng)
function definePlaneFromPoints(p1, p2, p3) {
  const v1 = new THREE.Vector3().subVectors(p2, p1);
  const v2 = new THREE.Vector3().subVectors(p3, p1);
  const normal = new THREE.Vector3().crossVectors(v1, v2);
  if (normal.lengthSq() < 1e-6) return null; // 3 điểm thẳng hàng
  normal.normalize();
  return { normal, pointOnPlane: p1.clone() };
}
```

> **Mọi hàm khác trong PHẦN A giả định `plane.normal` đã normalize.** Nếu tự
> tạo object `{normal, pointOnPlane}` bằng tay (không qua hàm này), PHẢI tự
> gọi `.normalize()` — thiếu bước này khiến `intersectionOfTwoPlanes` (A.6)
> tính sai hoàn toàn mà không có cảnh báo runtime.

### A.2 Chiếu điểm lên mặt phẳng

```javascript
// Trả { H, distance, signedDist }
// H: chân đường vuông góc từ M xuống mặt phẳng
// distance: |MH| — luôn ≥ 0, dùng để HIỂN THỊ
// signedDist: khoảng cách CÓ DẤU — dùng để TÍNH H, không hiển thị trực tiếp
function projectPointOntoPlane(M, plane) {
  const toPoint = new THREE.Vector3().subVectors(M, plane.pointOnPlane);
  const signedDist = toPoint.dot(plane.normal);
  const H = M.clone().sub(plane.normal.clone().multiplyScalar(signedDist));
  return { H, distance: Math.abs(signedDist), signedDist };
}
```

### A.3 Chiếu đường thẳng lên mặt phẳng

```javascript
// Trả { projStart, projEnd } — chiếu riêng 2 đầu mút, nối lại thành hình chiếu a'
function projectLineOntoPlane(lineStart, lineEnd, plane) {
  const { H: projStart } = projectPointOntoPlane(lineStart, plane);
  const { H: projEnd }   = projectPointOntoPlane(lineEnd, plane);
  return { projStart, projEnd };
}
```

> **Gotcha:** nếu đường nằm TRONG mặt phẳng (xem A.4 → `'contained'`),
> `projStart === lineStart` và `projEnd === lineEnd` — hình chiếu trùng đường
> gốc. Luôn gọi `classifyLineToPlane` trước khi vẽ hình chiếu để tránh vẽ
> đường trùng khít gây rối hình.

### A.4 Phân loại quan hệ đường thẳng – mặt phẳng

```javascript
// lineDir PHẢI đã normalize trước khi gọi — nếu chưa, ngưỡng 1e-4 sẽ sai
// Trả 'parallel' | 'intersects' | 'contained'
function classifyLineToPlane(lineStart, lineDir, plane) {
  const dot = Math.abs(lineDir.dot(plane.normal));
  if (dot > 1e-4) return 'intersects';

  // dot ≈ 0: hướng đường nằm trong mp → kiểm tra tiếp điểm có thuộc mp không
  const distPt = Math.abs(
    new THREE.Vector3().subVectors(lineStart, plane.pointOnPlane).dot(plane.normal)
  );
  return distPt < 1e-4 ? 'contained' : 'parallel';
}
```

> **`contained` ≠ `parallel`.** Cả 2 đều có `dot(dir, normal) ≈ 0`, khác nhau
> ở bước kiểm tra thứ 2. Bỏ qua bước 2 sẽ báo nhầm `parallel` cho đường thực
> ra nằm trong mặt phẳng — khoảng cách thật = 0 nhưng lại báo "có khoảng cách".

### A.5 Phân loại quan hệ 2 mặt phẳng

```javascript
// plane1.normal, plane2.normal phải đã normalize
// Trả 'parallel' | 'intersects'
function classifyTwoPlanes(plane1, plane2) {
  const cross = new THREE.Vector3().crossVectors(plane1.normal, plane2.normal);
  return cross.lengthSq() < 1e-6 ? 'parallel' : 'intersects';
}
```

### A.6 Giao tuyến 2 mặt phẳng cắt nhau

> ⚠️ **ĐÃ SỬA LỖI (07/2026, phát hiện khi build game "Đền thờ Euclid"
> Trạm 2):** bản trước dùng `denom = n1n2² - 1`, SAI DẤU — điểm trả về là
> ẢNH ĐỐI XỨNG qua gốc toạ độ của điểm đúng, không nằm trên mặt phẳng nào
> cả. Verify bằng Node với 2 mặt phẳng có điểm giao biết trước (tính tay):
> công thức cũ cho residual (mức lệch khỏi mặt phẳng) ≈ 2.26 (sai hoàn
> toàn), công thức đã sửa cho residual ≈ 0. Chi tiết đầy đủ + cách verify:
> `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.11. **Nếu đã copy hàm này
> sang file/prototype khác trước 07/2026, PHẢI cập nhật lại theo bản dưới.**

```javascript
// Trả { point, dir } — 1 điểm bất kỳ trên giao tuyến + hướng giao tuyến (đã normalize)
// Trả null nếu 2 mặt phẳng song song
//
// NGUYÊN LÝ: hướng giao tuyến = cross(n1, n2). Điểm trên giao tuyến giải từ
// hệ n1·P = d1, n2·P = d2, đặt P = c1·n1 + c2·n2 (P nằm trong mặt phẳng
// span(n1,n2)) — dẫn tới hệ Cramer [[1,k],[k,1]]·[c1;c2] = [d1;d2] với
// k = n1·n2 (vì n1·n1 = n2·n2 = 1 sau normalize). Định thức hệ này là
// 1 - k², KHÔNG phải k² - 1 — công thức rút gọn dưới đây CHỈ ĐÚNG khi n1,
// n2 đã normalize (n·n = 1), nếu không denom sẽ tính sai.
function intersectionOfTwoPlanes(plane1, plane2) {
  const dir = new THREE.Vector3().crossVectors(plane1.normal, plane2.normal);
  if (dir.lengthSq() < 1e-6) return null; // song song
  dir.normalize();

  const n1 = plane1.normal, n2 = plane2.normal;
  const d1 = n1.dot(plane1.pointOnPlane);
  const d2 = n2.dot(plane2.pointOnPlane);
  const n1n2 = n1.dot(n2);
  const denom = 1 - n1n2 * n1n2; // = định thức hệ Cramer [[1,k],[k,1]] — ĐÃ SỬA, xem cảnh báo trên
  if (Math.abs(denom) < 1e-8) return null; // phòng thủ thêm

  const c1 = (d1 - d2 * n1n2) / denom;
  const c2 = (d2 - d1 * n1n2) / denom;
  const point = new THREE.Vector3().addScaledVector(n1, c1).addScaledVector(n2, c2);
  return { point, dir };
}
```

> **Verify bắt buộc sau khi dùng hàm này ở bất kỳ file mới nào:** kiểm
> tra `(point - plane1.pointOnPlane)·plane1.normal ≈ 0` VÀ tương tự với
> plane2 — nếu residual không ≈ 0, công thức đang chạy là bản lỗi.



```javascript
// Chiếu vector nối 2 điểm bất kỳ trên 2 mặt phẳng lên normal — ra khoảng cách vuông góc
function distanceBetweenParallelPlanes(plane1, plane2) {
  return Math.abs(
    new THREE.Vector3().subVectors(plane2.pointOnPlane, plane1.pointOnPlane).dot(plane1.normal)
  );
}
```

### A.8 Khoảng cách đường thẳng đến mặt phẳng song song

```javascript
// Điều kiện áp dụng: đường phải // mặt phẳng (kiểm tra bằng A.4 trước).
// Bản chất chỉ là A.2 lấy .distance — tách riêng để code gọi có tên rõ nghĩa hơn.
function distanceLineToPlane(linePoint, plane) {
  return projectPointOntoPlane(linePoint, plane).distance;
}
```

### A.9 Giao điểm của đường thẳng với mặt phẳng

```javascript
// Trả { point, t } — point là giao điểm, t là tham số vị trí trên đoạn
// [lineStart, lineEnd] (0 = lineStart, 1 = lineEnd; t NGOÀI [0,1] nghĩa
// là giao điểm nằm trên phần KÉO DÀI của đoạn, không phải trong đoạn thật)
// Trả null nếu đường thẳng song song với mặt phẳng (không có giao điểm
// duy nhất, kể cả trường hợp đường nằm trọn trong mặt phẳng)
//
// DÙNG KHI NÀO: đây là hàm ĐƠN GIẢN NHẤT khi mặt phẳng đã có sẵn 3 điểm
// xác định rõ ràng (VD mặt phẳng thiết diện (MNP) đã biết M, N, P) và
// cần tìm nó cắt 1 cạnh khác của khối ở đâu. KHÔNG cần dựng thêm "mặt
// phẳng phụ" trung gian nào trong trường hợp này — chỉ cần khi mặt
// phẳng CHƯA xác định rõ (ví dụ tìm giao của 1 đường với 1 mặt phẳng
// đề bài cho mà đường đó không nằm sẵn trong mặt nào, xem PHỤ LỤC E).
function lineIntersectPlane(lineStart, lineEnd, plane) {
  const lineDir = new THREE.Vector3().subVectors(lineEnd, lineStart);
  const denom = lineDir.dot(plane.normal);
  if (Math.abs(denom) < 1e-8) return null; // song song hoặc nằm trong mp

  const t = new THREE.Vector3().subVectors(plane.pointOnPlane, lineStart).dot(plane.normal) / denom;
  const point = lineStart.clone().add(lineDir.clone().multiplyScalar(t));
  return { point, t };
}
```

> **Bài học thực tế (đã xảy ra khi build prototype thiết diện trượt):**
> lần đầu viết sai bằng cách dựng "mặt phẳng phụ mp(M, P, S)" rồi tìm giao
> với cạnh SD — kết quả LUÔN cho giao điểm trùng đỉnh S bất kể M ở đâu,
> vì mp(M,P,S) luôn chứa S (do M, P nằm trên các cạnh xuất phát từ S) mà
> SD cũng xuất phát từ S. Đây không phải lỗi code mà là chọn sai mặt
> phẳng để giao — khi 3 điểm xác định mặt phẳng đã có sẵn (M, N, P), dùng
> thẳng `lineIntersectPlane` với `definePlaneFromPoints(M,N,P)`, không
> tự vẽ thêm mặt phẳng phụ nào nữa. Luôn verify bằng script Node độc lập
> (kiểm tra t thay đổi hợp lý theo vị trí điểm kéo) trước khi tin kết quả
> hiển thị trên canvas — canvas có thể "trông đúng" dù công thức sai.

---

## PHẦN B — ĐƯỜNG THẲNG

### B.1 Chiếu điểm lên đường thẳng (khác chiếu lên mặt phẳng ở PHẦN A.2)

```javascript
// Trả { H, distance, t } — H là chân đường vuông góc từ M đến đường thẳng
// linePoint: 1 điểm bất kỳ trên đường; lineDir: hướng đường (KHÔNG cần normalize trước)
// t: tham số vị trí H trên đường — t<0 hoặc t>1 nghĩa là H nằm NGOÀI đoạn
//    [linePoint, linePoint+lineDir] vì đường thẳng vô hạn, không bị clamp
//    (khác ConstrainedPoint trong 05_threejs_engine.md PHẦN 2 — đó có clamp)
function projectPointOntoLine(M, linePoint, lineDir) {
  const d = lineDir.clone().normalize();
  const t = new THREE.Vector3().subVectors(M, linePoint).dot(d);
  const H = linePoint.clone().add(d.clone().multiplyScalar(t));
  return { H, distance: M.distanceTo(H), t };
}
```

### B.2 Khoảng cách 2 đường thẳng chéo nhau

```javascript
// Trả { dist, H1, H2, cross } hoặc null nếu 2 đường KHÔNG chéo nhau
// (song song hoặc cắt nhau — cả 2 trường hợp đều cho cross ≈ 0, không phân
//  biệt tiếp ở đây; xem "Phân biệt" bên dưới nếu cần biết chính xác trường hợp nào)
// P1, P2: điểm bất kỳ trên mỗi đường; dir1, dir2: hướng (KHÔNG cần normalize trước)
// H1 ∈ đường 1, H2 ∈ đường 2 — 2 đầu của đoạn vuông góc chung, ngắn nhất
// nối 2 đường trong không gian.
function distanceSkewLines(P1, dir1, P2, dir2) {
  const d1 = dir1.clone().normalize();
  const d2 = dir2.clone().normalize();
  const cross = new THREE.Vector3().crossVectors(d1, d2);
  const crossLen = cross.length();

  if (crossLen < 1e-6) return null; // song song hoặc cắt nhau → không áp dụng

  const w = new THREE.Vector3().subVectors(P2, P1);
  const dist = Math.abs(w.dot(cross)) / crossLen;

  // Giải hệ từ điều kiện (H2-H1)⊥d1 và (H2-H1)⊥d2:
  // Đặt b=d1·d2, e=w·d1, f=w·d2 → t1=(e-b·f)/(1-b²), t2=-(f-b·e)/(1-b²)
  // LƯU Ý DẤU: t2 có dấu TRỪ ở đầu — chép nhầm dấu là lỗi hay gặp nhất khi
  // viết lại công thức này bằng tay.
  const b = d1.dot(d2);
  const denom = 1 - b * b; // = sin²(góc giữa 2 đường), luôn > 0 vì không song song
  const e = w.dot(d1), f = w.dot(d2);
  const t1 =  (e - b * f) / denom;
  const t2 = -(f - b * e) / denom;

  const H1 = P1.clone().add(d1.clone().multiplyScalar(t1));
  const H2 = P2.clone().add(d2.clone().multiplyScalar(t2));
  return { dist, H1, H2, cross: cross.normalize() };
}
```

> **Verify kết quả sau khi tính** (nên làm khi viết test mới):
> `(H2-H1).dot(d1) ≈ 0`, `(H2-H1).dot(d2) ≈ 0`, và `H1.distanceTo(H2) ≈ dist`.
>
> **Phân biệt song song vs cắt nhau** (nếu cần, hàm trên không tự phân biệt):
> cả 2 đều cho `crossLen ≈ 0` → return null. Muốn biết chính xác trường hợp
> nào, kiểm tra thêm: nếu 2 đường song song thì khoảng cách giữa chúng > 0
> (dùng A.2 chiếu 1 điểm của đường này lên "mặt phẳng chứa đường kia + hướng
> song song"); nếu cắt nhau thì khoảng cách = 0. Trong thực tế simulation,
> return null + thông báo "không áp dụng công thức chéo nhau" là đủ.

### B.3 Giao điểm của 2 đoạn thẳng hữu hạn (khác B.2 — đoạn có 2 đầu mút)

```javascript
// KHÁC BIỆT CỐT LÕI với distanceSkewLines (B.2): B.2 coi 2 đường thẳng
// là VÔ HẠN, chỉ trả khoảng cách nhỏ nhất giữa chúng. Hàm này xét ĐOẠN
// THẲNG có 2 đầu mút cụ thể — cần thêm bước kiểm tra điểm gần nhau nhất
// có thực sự nằm TRONG cả 2 đoạn hay không (tham số t, s ∈ [0,1]).
//
// Trả { intersects, point, t, s, distance, reason }
//   intersects: true nếu 2 đoạn thực sự cắt nhau (đồng phẳng + t,s trong [0,1])
//   reason: 'ok' | 'parallel' | 'skew' (chéo nhau, không đồng phẳng) |
//           'outside-segment' (2 đường vô hạn cắt nhau nhưng ngoài đoạn
//           hữu hạn — VD 2 đoạn ngắn, kéo dài ra mới gặp nhau) |
//           'degenerate' (1 trong 2 đoạn suy biến thành điểm)
//
// p1,p2: 2 đầu mút đoạn 1; p3,p4: 2 đầu mút đoạn 2; epsilon: ngưỡng
// coi là "đủ gần để tính là cắt nhau" (mặc định 0.05 đơn vị scene)
function segmentIntersection(p1, p2, p3, p4, epsilon = 0.05) {
  const d1 = new THREE.Vector3().subVectors(p2, p1);
  const d2 = new THREE.Vector3().subVectors(p4, p3);
  const r = new THREE.Vector3().subVectors(p1, p3);

  const a = d1.dot(d1);
  const e = d2.dot(d2);
  const f = d2.dot(r);

  if (a < 1e-10 || e < 1e-10) {
    return { intersects: false, point: null, t: null, s: null, distance: Infinity, reason: 'degenerate' };
  }

  const c = d1.dot(r);
  const b = d1.dot(d2);
  const denom = a * e - b * b;

  let t, s;
  if (Math.abs(denom) < 1e-8) {
    return { intersects: false, point: null, t: null, s: null, distance: null, reason: 'parallel' };
  }
  t = (b * f - c * e) / denom;
  s = (a * f - b * c) / denom;

  const ptOnLine1 = p1.clone().add(d1.clone().multiplyScalar(t));
  const ptOnLine2 = p3.clone().add(d2.clone().multiplyScalar(s));
  const distance = ptOnLine1.distanceTo(ptOnLine2);

  // Bước 1: 2 đường (vô hạn) có thực sự gặp nhau không?
  if (distance > epsilon) {
    return { intersects: false, point: null, t, s, distance, reason: 'skew' };
  }

  // Bước 2 — ĐIỂM KHÁC BIỆT CỐT LÕI so với công thức đường vô hạn:
  // t, s có nằm trong [0,1] không?
  const withinSegment1 = t >= -1e-4 && t <= 1 + 1e-4;
  const withinSegment2 = s >= -1e-4 && s <= 1 + 1e-4;

  if (!withinSegment1 || !withinSegment2) {
    const midpoint = ptOnLine1.clone().lerp(ptOnLine2, 0.5);
    return { intersects: false, point: midpoint, t, s, distance, reason: 'outside-segment' };
  }

  const point = ptOnLine1.clone().lerp(ptOnLine2, 0.5);
  return { intersects: true, point, t, s, distance, reason: 'ok' };
}
```

> **Verify đã làm (script Node độc lập, không cần THREE.js thật):** 4 case
> chuẩn — cắt trong đoạn / cắt ngoài đoạn (2 đường vô hạn giao nhau nhưng
> đoạn hữu hạn thì không) / chéo nhau (khác độ cao, không đồng phẳng) /
> song song — đều cho đúng `reason` tương ứng. Dùng khi: tìm điểm chung
> của 2 đường thẳng nằm trong 1 mặt phẳng đáy (VD tìm giao điểm BN và CM
> trên mặt đáy hình chóp để xác định giao tuyến 2 mặt phẳng chứa chúng).

### B.4 Giao điểm của 2 đường thẳng VÔ HẠN (biến thể của B.3 — bỏ bước kẹp
### đoạn, vì công cụ "Đường thẳng song song" trong GeoGebra dựng đường vô hạn)

```javascript
// P1,dir1 / P2,dir2: điểm bất kỳ trên đường + hướng (dir KHÔNG cần normalize trước)
// Trả { intersects, point, t, s, distance, reason }
// reason: 'ok' | 'parallel' | 'skew' (2 đường chéo nhau, không đồng phẳng —
// đây là trường hợp GIỐNG HỆT gotcha ở A.6/B.3: 2 đường trong không gian
// luôn có 1 cặp điểm "gần nhau nhất" dù không hề đồng phẳng — PHẢI kiểm tra
// distance giữa 2 điểm gần nhau nhất đó ≈ 0 mới được công nhận là giao điểm
// thật, không được chỉ dựa vào việc denom giải được là đủ)
function intersectionOfTwoLines(P1, dir1, P2, dir2, epsilon = 1e-4) {
  const d1 = dir1.clone().normalize();
  const d2 = dir2.clone().normalize();
  const r = new THREE.Vector3().subVectors(P1, P2);

  const a = d1.dot(d1), e = d2.dot(d2), f = d2.dot(r);
  const c = d1.dot(r), b = d1.dot(d2);
  const denom = a * e - b * b;

  if (Math.abs(denom) < 1e-8) {
    return { intersects: false, point: null, t: null, s: null, distance: null, reason: 'parallel' };
  }
  const t = (b * f - c * e) / denom;
  const s = (a * f - b * c) / denom;

  const ptOnLine1 = P1.clone().add(d1.clone().multiplyScalar(t));
  const ptOnLine2 = P2.clone().add(d2.clone().multiplyScalar(s));
  const distance = ptOnLine1.distanceTo(ptOnLine2);

  if (distance > epsilon) {
    return { intersects: false, point: null, t, s, distance, reason: 'skew' };
  }
  const point = ptOnLine1.clone().lerp(ptOnLine2, 0.5);
  return { intersects: true, point, t, s, distance, reason: 'ok' };
}
```

> **Verify đã làm (script Node, cài `three` thật qua npm — không dùng object
> `{x,y,z}` tự chế để tránh lệch API):** dựng lại đúng quy trình SGK "Vẽ
> vectơ tổng của ba vectơ trong không gian" — 4 điểm A,B,C,D bất kỳ (không
> đồng phẳng), dựng E theo quy tắc hình bình hành ABEC (từ B.4 + H.2), rồi
> dựng F từ E (cũng bằng B.4 + H.2) — kiểm tra bằng đại số độc lập
> `AF = AB+AC+AD` khớp chính xác. Cộng 3 case đối chứng: 2 đường chéo nhau
> → `reason:'skew'`, 2 đường song song → `reason:'parallel'`, và 1 cặp cắt
> nhau thật trong mặt phẳng nghiêng bất kỳ (không phải mặt toạ độ) → đúng.
> Toàn bộ 6/6 pass. Dùng khi: dựng đỉnh còn lại của hình bình hành/hình hộp
> từ các đỉnh đã có (quy tắc cộng vectơ bằng hình học dựng hình, không phải
> chỉ cộng toạ độ) — xem PHẦN H bên dưới cho quy trình đầy đủ.

---

## PHẦN C — GÓC

### C.1 Góc giữa đường thẳng và mặt phẳng

```javascript
// SGK định nghĩa: φ = góc giữa đường a và hình chiếu a' của a lên mặt phẳng.
// KHÔNG phải góc giữa a và normal — góc đó là (90° - φ).
// lineDir PHẢI normalize trước khi gọi (hoặc hàm tự normalize lại cho an toàn)
// Trả độ, trong khoảng [0°, 90°]
function angleLineToPlane(lineDir, planeNormal) {
  // sin(φ) = cos(góc giữa lineDir và normal) = |lineDir · normal|
  const sinPhi = Math.abs(lineDir.clone().normalize().dot(planeNormal.clone().normalize()));
  return Math.asin(Math.min(1, sinPhi)) * 180 / Math.PI;
}
// Trường hợp đặc biệt: a ⊥ mặt phẳng → φ = 90°; a // mặt phẳng → φ = 0°
```

### C.2 Góc nhị diện giữa 2 mặt phẳng

```javascript
// SGK định nghĩa: lấy O bất kỳ trên giao tuyến l, dựng Ox ⊥ l trong mặt
// phẳng 1, Oy ⊥ l trong mặt phẳng 2. Góc nhị diện = góc xOy — không phụ
// thuộc vị trí O trên l.
// intersect: kết quả từ A.6 intersectionOfTwoPlanes() — { point, dir }
// Trả { angleDeg, ox, oy } — ox, oy là 2 vector tia (đã normalize) để vẽ
function dihedralAngle(plane1, plane2, intersect) {
  const ox = new THREE.Vector3().crossVectors(intersect.dir, plane1.normal).normalize();
  const oy = new THREE.Vector3().crossVectors(intersect.dir, plane2.normal).normalize();
  const cosTheta = Math.max(-1, Math.min(1, ox.dot(oy))); // clamp — BẮT BUỘC,
                                                            // thiếu sẽ ra NaN
                                                            // khi sai số float
                                                            // đẩy dot > 1
  const angleDeg = Math.acos(cosTheta) * 180 / Math.PI;
  return { angleDeg, ox, oy };
}
```

> **Chiều ox/oy có thể lộn** (chỉ vào trong hay ra ngoài mặt phẳng, tuỳ thứ
> tự tham số truyền vào `crossVectors`). Nếu cần đảm bảo tia nằm đúng phía
> "trên" mặt phẳng, kiểm tra `ox.dot(plane1.normal)` — nếu âm thì
> `ox.negate()`. Áp dụng tương tự cho `oy`.

---

## PHẦN D — TOẠ ĐỘ BARYCENTRIC (điểm trong tam giác)

### D.1 Dựng điểm từ toạ độ barycentric (thuận)

```javascript
// P = (1-u-v)·V0 + u·V1 + v·V2 — công thức chuẩn, u=v=0 cho P=V0,
// u=1 cho P=V1, v=1 cho P=V2, u=v=1/3 cho TRỌNG TÂM tam giác
function pointFromBarycentric(v0, v1, v2, u, v) {
  const w = 1 - u - v;
  return new THREE.Vector3().addScaledVector(v0, w).addScaledVector(v1, u).addScaledVector(v2, v);
}
```

### D.2 Tính toạ độ barycentric từ 1 điểm cho trước (nghịch — dùng khi click chọn điểm trên mặt)

```javascript
// Tính (u,v) của điểm P trong tam giác (v0,v1,v2) — nghịch của D.1
function barycentricCoords(P, v0, v1, v2) {
  const e1 = new THREE.Vector3().subVectors(v1, v0);
  const e2 = new THREE.Vector3().subVectors(v2, v0);
  const ep = new THREE.Vector3().subVectors(P,  v0);
  const d00 = e1.dot(e1), d01 = e1.dot(e2), d11 = e2.dot(e2);
  const d02 = e1.dot(ep), d12 = e2.dot(ep);
  const inv = 1 / (d00 * d11 - d01 * d01);
  const u = (d11 * d02 - d01 * d12) * inv;
  const v = (d00 * d12 - d01 * d02) * inv;
  // Clamp để điểm luôn nằm trong tam giác dù click hơi lệch ra ngoài do sai số raycast
  return { u: Math.max(0, Math.min(1, u)), v: Math.max(0, Math.min(1 - u, v)) };
}
```

> **Cách dùng trong app thực tế** (ví dụ `solid_library.html`): điểm trên
> cạnh dùng `Vector3.lerpVectors(pA, pB, t)` (nội suy tuyến tính, xem
> `05_threejs_engine.md` PHẦN 2), điểm trên mặt tam giác dùng D.1 với
> `(u,v)` lưu trong state của điểm. Cả 2 đều được tính lại **mỗi frame** từ
> vị trí ĐỈNH HIỆN TẠI (không cache toạ độ world) — để điểm tự trôi theo
> đúng khi đỉnh bị kéo (EXPLORE) hoặc slider đổi kích thước khối.

---

## PHẦN E — PHÉP XOAY

### E.1 Xoay 1 đoạn thẳng quanh 1 trục đi qua điểm pivot

```javascript
// Xoay 2 đầu mút pP, pQ quanh trục (normal, đi qua pivotM) — dùng minh hoạ
// "xoay đường thẳng vẫn giữ song song với mặt phẳng" (trục = normal mặt phẳng)
// angleDeg: góc TUYỆT ĐỐI tính từ vị trí gốc — KHÔNG phải góc delta từng bước,
// để tránh trôi dạt (drift) khi gọi lại nhiều lần liên tiếp qua slider.
function rotateLineAroundNormal(pP, pQ, pivotM, normal, angleDeg) {
  const axis = normal.clone().normalize();
  const quat = new THREE.Quaternion().setFromAxisAngle(axis, angleDeg * Math.PI / 180);
  const newP = pP.clone().sub(pivotM).applyQuaternion(quat).add(pivotM);
  const newQ = pQ.clone().sub(pivotM).applyQuaternion(quat).add(pivotM);
  return { newP, newQ };
}
```

> **Dùng với slider góc tuyệt đối:** phải lưu `baseP`/`baseQ` (vị trí TRƯỚC
> khi bắt đầu xoay) và luôn tính `rotateLineAroundNormal(baseP, baseQ, ...)`
> — không xoay tiếp từ vị trí đã xoay trước đó (delta), nếu không sẽ tích
> luỹ sai số. Xem `05_threejs_engine.md` PHẦN 4.14 cho pattern đầy đủ + gotcha
> "nhảy vị trí" khi kéo tay xen giữa lúc dùng slider.

---

## PHẦN F — KHỐI TRÒN XOAY: THAM SỐ HOÁ MẶT CONG

> 3 hàm dựng điểm (thuận) + 1 hàm nghịch (từ điểm click ra tham số) cho mặt
> cầu, mặt xung quanh trụ, mặt xung quanh nón. Quy ước chung: trục quay là
> **trục Y**, đáy nằm tại **y=0** (khớp với `ROUND_LIBRARY` trong
> `05_threejs_engine.md` PHẦN 9).

### F.1 Điểm trên mặt cầu (từ toạ độ cầu)

```javascript
// theta: góc quanh trục Y (kinh độ, radian, mọi giá trị hợp lệ)
// phi: góc từ cực trên xuống (vĩ độ, radian, trong [0, π] — 0 là cực Bắc)
// R: bán kính cầu, tâm tại gốc toạ độ (0,0,0)
function pointOnSphere(theta, phi, R) {
  return new THREE.Vector3(
    R * Math.sin(phi) * Math.cos(theta),
    R * Math.cos(phi),
    R * Math.sin(phi) * Math.sin(theta)
  );
}

// Nghịch: từ 1 điểm P trên mặt cầu (tâm tại gốc) → (theta, phi)
function sphereCoordsFromPoint(P, R) {
  const phi = Math.acos(Math.max(-1, Math.min(1, P.y / R)));
  const theta = Math.atan2(P.z, P.x);
  return { theta, phi };
}
```

### F.2 Điểm trên mặt xung quanh hình trụ

```javascript
// theta: góc quanh trục Y (radian)
// s: tham số chiều cao, 0 = đáy dưới (y=0), 1 = đáy trên (y=h) — bán kính không đổi
function pointOnCylinderSide(theta, s, r, h) {
  return new THREE.Vector3(r * Math.cos(theta), s * h, r * Math.sin(theta));
}

// Nghịch: từ điểm P trên mặt trụ → (theta, s)
function cylinderCoordsFromPoint(P, h) {
  const theta = Math.atan2(P.z, P.x);
  const s = Math.max(0, Math.min(1, P.y / h));
  return { theta, s };
}
```

### F.3 Điểm trên mặt xung quanh hình nón

```javascript
// theta: góc quanh trục Y (radian)
// s: tham số dọc đường sinh, 0 = đáy (y=0, bán kính=r), 1 = đỉnh (y=h, bán kính=0)
// Bán kính co dần TUYẾN TÍNH từ r về 0 — đây là tính chất hình học của nón,
// không phải xấp xỉ.
function pointOnConeSide(theta, s, r, h) {
  const radius = r * (1 - s);
  return new THREE.Vector3(radius * Math.cos(theta), s * h, radius * Math.sin(theta));
}

// Nghịch: từ điểm P trên mặt nón → (theta, s) — CHÚ Ý: dùng chung công thức
// s = P.y / h với hình trụ (F.2), vì s chỉ phụ thuộc độ cao, không phụ
// thuộc bán kính tại độ cao đó
function coneCoordsFromPoint(P, h) {
  const theta = Math.atan2(P.z, P.x);
  const s = Math.max(0, Math.min(1, P.y / h));
  return { theta, s };
}
```

> **Cách dùng trong app thực tế:** khi click chuột lên mặt cong (raycast
> thẳng vào mesh — mesh cong CHÍNH LÀ ràng buộc, không cần công thức chiếu
> riêng như PHẦN A/B), lấy điểm giao `hit.point` rồi gọi hàm nghịch tương
> ứng (F.1/F.2/F.3) theo `type` của khối để ra `(theta, phi)` hoặc `(theta, s)`.
> Lưu tham số này làm state của điểm — mỗi frame gọi lại hàm thuận để tính
> vị trí world, tự động đúng khi bán kính/chiều cao đổi qua slider.

---

## PHẦN G — ĐA GIÁC PHẲNG (nhiều đỉnh, ví dụ thiết diện)

### G.1 Diện tích đa giác phẳng bất kỳ trong không gian 3D

```javascript
// Tính bằng fan triangulation từ đỉnh đầu tiên: chia đa giác n đỉnh
// thành (n-2) tam giác, cộng diện tích |cross product|/2 từng tam giác.
// Hoạt động đúng cho đa giác nằm trên MẶT PHẲNG NGHIÊNG BẤT KỲ trong
// không gian 3D (không chỉ đa giác phẳng trên trục toạ độ chuẩn) — đã
// verify bằng cách xoay 1 hình vuông quanh trục bất kỳ và xác nhận
// diện tích không đổi (bất biến dưới phép quay).
function polygonArea(vertices) {
  if (vertices.length < 3) return 0;
  let total = 0;
  const v0 = vertices[0];
  for (let i = 1; i < vertices.length - 1; i++) {
    const v1 = new THREE.Vector3().subVectors(vertices[i], v0);
    const v2 = new THREE.Vector3().subVectors(vertices[i+1], v0);
    total += v1.clone().cross(v2).length() / 2;
  }
  return total;
}
```

> ## ⚠️ CẢNH BÁO QUAN TRỌNG NHẤT CỦA HÀM NÀY — đọc kỹ trước khi dùng
>
> **`polygonArea` KHÔNG kiểm tra đa giác có tự cắt (self-intersecting)
> hay không.** Đã verify bằng Node: truyền 4 đỉnh của 1 hình vuông theo
> đúng thứ tự chu vi (M→N→P→Q) cho diện tích đúng; truyền CÙNG 4 điểm đó
> nhưng SAI thứ tự (M→P→N→Q, tạo hình "nơ bướm" tự cắt) vẫn cho ra **con
> số giống hệt** — hàm không hề báo lỗi hay cảnh báo gì. Đây là cạm bẫy
> ngầm nguy hiểm: code chạy được, không có exception, nhưng kết quả sai
> về bản chất hình học.
>
> **QUY TẮC BẮT BUỘC khi dùng hàm này:** đỉnh truyền vào PHẢI theo đúng
> thứ tự chu vi thực tế của đa giác — không đoán bằng cách nhìn tên biến
> hoặc thứ tự khai báo, phải đối chiếu đúng cấu trúc hình học của khối.
> Ví dụ cụ thể đã xảy ra: với thiết diện MNPQ của hình chóp S.ABCD (M
> trên cạnh SA, N trên SB, P trên SC, Q trên SD), thứ tự đúng là
> `[M, N, P, Q]` — vì đáy ABCD đi theo chu vi A→B→C→D→A, nên các điểm
> trên 4 cạnh bên tương ứng cũng phải nối theo đúng thứ tự đó
> (SA→SB→SC→SD). KHÔNG suy luận thứ tự bằng cách nhìn tên biến (dễ nhầm
> thành M→N→Q→P nếu chỉ dựa cảm tính).

### G.2 Bài học thực tế: lỗi tráo tham số qua tên biến trong chữ ký hàm

> Khi dựng mesh hiển thị cho thiết diện, chữ ký hàm khai báo tên tham số
> SAI thứ tự — ví dụ `function rebuildCrossSection(M, N, Q, P, ...)`
> thay vì đúng phải là `(M, N, P, Q, ...)` — trong khi phần thân hàm và
> lời gọi bên ngoài đều dùng đúng thứ tự M→N→P→Q. Vì JS truyền đối số
> theo vị trí, 2 giá trị P/Q bị tráo ngay từ đầu vào dù thân hàm "trông
> như đã đúng". Khi sửa lỗi thứ tự 1 bộ đỉnh dùng ở nhiều nơi (chữ ký
> hàm, lời gọi, hàm vẽ viền riêng, hàm tính diện tích...), phải grep
> kiểm tra ĐỒNG THỜI tất cả vị trí, không sửa 1 chỗ rồi tin đã xong.
> Tường thuật đầy đủ + cách verify: xem
> `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.10.

### G.3 Bài học: chọn cấu hình khối sai khiến bài toán vô nghiệm

> Khi thiết kế 1 thiết diện có N, P là trung điểm 2 cạnh bên xuất phát
> từ cùng 1 đỉnh (ví dụ N trung điểm SB, P trung điểm SC trong tứ diện
> S.ABC), theo định lý đường trung bình tam giác, đoạn NP LUÔN song
> song với cạnh đáy BC — bất kể vị trí điểm thứ 3 (M) ở đâu. Hệ quả: nếu
> cần tìm giao điểm của mặt phẳng thiết diện với 1 cạnh khác mà cạnh đó
> lại song song với NP (ví dụ cố tìm giao với BC), phép tính LUÔN trả về
> "song song, vô nghiệm" — không phải lỗi code, mà là hệ quả hình học
> tất yếu của cấu hình đã chọn.
>
> Trong trường hợp cụ thể này, giải pháp là đổi sang khối có 1 cạnh ĐỘC
> LẬP không rơi vào ràng buộc song song đó — ví dụ hình chóp TỨ GIÁC
> S.ABCD có cạnh SD tách biệt hẳn khỏi cặp SB/SC, không bị chi phối bởi
> định lý đường trung bình liên quan tới N, P.
>
> **Nguyên tắc rút ra:** trước khi build 1 thiết diện với N, P cố định
> tại 1 tỉ lệ cụ thể trên 2 cạnh, LUÔN verify bằng cách quét toàn bộ
> khoảng giá trị của điểm còn lại (M), in ra kết quả giao điểm — nếu mọi
> giá trị M đều cho "song song/vô nghiệm" giống nhau, đó là dấu hiệu cấu
> hình khối đang chọn có ràng buộc hình học ngăn cản bài toán, cần đổi
> khối nền chứ không phải sửa công thức.

### G.4 Dựng đa giác thiết diện TỪ MẶT PHẲNG (không cần biết trước thứ tự đỉnh)

> **Verify trong `solid_library.html` (07/2026)**, giải quyết đúng cái bẫy
> đã cảnh báo ở G.1 ("`polygonArea` không tự phát hiện đỉnh sai thứ tự") —
> nhưng bằng cách khác: thay vì yêu cầu người gọi hàm tự suy luận đúng thứ
> tự chu vi (dễ sai như G.1/G.2 đã gặp), hàm này tự tính lại thứ tự từ
> hình học, không phụ thuộc thứ tự đầu vào.

```javascript
function computeSectionPolygon(p0, p1, p2, vertices, edges) {
  const v1 = new THREE.Vector3().subVectors(p1, p0);
  const v2 = new THREE.Vector3().subVectors(p2, p0);
  const normal = new THREE.Vector3().crossVectors(v1, v2);
  if (normal.lengthSq() < 1e-8) return null;
  normal.normalize();
  const d0 = -normal.dot(p0);
  const signedDist = (v) => normal.dot(v) + d0;

  const EPS = 1e-4;
  const raw = [];
  edges.forEach(([na, nb]) => {
    const A = vertices[na], B = vertices[nb];
    const dA = signedDist(A), dB = signedDist(B);
    if (Math.abs(dA) < EPS)      raw.push(A.clone());
    else if (Math.abs(dB) < EPS) raw.push(B.clone());
    else if ((dA > 0) !== (dB > 0)) {
      const t = dA / (dA - dB);
      raw.push(new THREE.Vector3().lerpVectors(A, B, t));
    }
  });

  const pts = [];
  raw.forEach(p => { if (!pts.some(q => q.distanceTo(p) < 1e-3)) pts.push(p); });
  if (pts.length < 3) return null;

  const centroid = pts.reduce((s, p) => s.add(p), new THREE.Vector3()).multiplyScalar(1 / pts.length);
  const u = new THREE.Vector3().subVectors(pts[0], centroid).normalize();
  const v = new THREE.Vector3().crossVectors(normal, u).normalize();
  pts.sort((a, b) => {
    const da = new THREE.Vector3().subVectors(a, centroid);
    const db = new THREE.Vector3().subVectors(b, centroid);
    return Math.atan2(da.dot(v), da.dot(u)) - Math.atan2(db.dot(v), db.dot(u));
  });
  return pts; // sẵn sàng truyền thẳng vào polygonArea() (G.1) hoặc dựng mesh tam giác quạt
}
```

> **Điều kiện áp dụng — CHỈ đúng với khối LỒI.** Với khối lõm, 1 mặt phẳng
> có thể cắt tạo ra NHIỀU đa giác tách rời — sort-theo-góc-quanh-1-tâm sẽ
> ghép nhầm các mảnh rời thành 1 vòng. Mọi khối trong `SOLID_LIBRARY` hiện
> tại đều lồi nên chưa gặp vấn đề này.
>
> **Chưa áp dụng được cho mặt cong** (cầu/trụ/nón) — giao tuyến với mặt
> cong là đường conic (tròn/elip/parabol/hyperbol tuỳ góc cắt), cần thuật
> toán riêng, chưa viết.

---

## PHẦN H — VECTƠ

> Dùng cho các bài dựng vectơ tổng/hiệu bằng CÁCH DỰNG HÌNH (quy tắc hình
> bình hành / hình hộp), khác với việc chỉ cộng toạ độ 2 vectơ bằng số —
> mục tiêu sư phạm của hoạt động "Vẽ vectơ tổng của ba vectơ trong không
> gian bằng GeoGebra" là học sinh tự tay dựng, không phải xem kết quả có
> sẵn.

### H.1 Dựng vectơ từ 2 điểm

```javascript
// Trả { origin, dir (đã normalize), length, raw } — dùng dựng THREE.ArrowHelper
// trong 05_threejs_engine.md: new THREE.ArrowHelper(dir, origin, length, color)
function vectorFromPoints(A, B) {
  const raw = new THREE.Vector3().subVectors(B, A);
  const length = raw.length();
  const dir = length < 1e-9 ? new THREE.Vector3(0, 0, 0) : raw.clone().normalize();
  return { origin: A.clone(), dir, length, raw };
}
```

### H.2 Đường thẳng qua 1 điểm, song song 1 vectơ cho trước

```javascript
// Trả { P0, dir (đã normalize) } — dùng làm input trực tiếp cho
// intersectionOfTwoLines (B.4) để tìm giao điểm 2 đường song song vừa dựng
function lineThroughPointParallelTo(P, v) {
  return { P0: P.clone(), dir: v.clone().normalize() };
}
```

### H.3 Quy trình dựng vectơ tổng 3 vectơ bằng quy tắc hình hộp (2 bước lặp lại)

> Ghép H.1 + H.2 + B.4 thành đúng quy trình 6 bước SGK (trang 92-93): với
> 4 điểm A, B, C, D không đồng phẳng, dựng $\vec{AF} = \vec{AB}+\vec{AC}+\vec{AD}$.

```javascript
// Bước 1 — dựng E theo quy tắc hình bình hành ABEC: AE = AB + AC
function buildParallelogramSum(A, B, C) {
  const vAB = new THREE.Vector3().subVectors(B, A);
  const vAC = new THREE.Vector3().subVectors(C, A);
  const lineFromB = lineThroughPointParallelTo(B, vAC); // qua B, song song AC
  const lineFromC = lineThroughPointParallelTo(C, vAB); // qua C, song song AB
  const res = intersectionOfTwoLines(lineFromB.P0, lineFromB.dir, lineFromC.P0, lineFromC.dir);
  return res.intersects ? res.point : null; // null nếu A,B,C thẳng hàng (suy biến)
}

// Bước 2 — gọi lại ĐÚNG hàm bước 1 với (A, E, D) thay vì viết logic mới:
// buildParallelogramSum(A, E, D) → dựng F sao cho AF = AE + AD = AB+AC+AD
```

> **Verify:** xem khối verify ở B.4 — đã dựng đúng quy trình 2 bước này và
> đối chiếu bằng đại số `AF = AB+AC+AD`, khớp chính xác (6/6 test pass, gồm
> cả 2 case đối chứng "không được có giao điểm" — xem B.4).
>
> **Gotcha giống hệt G.3 (chọn cấu hình khối vi phạm định lý, khiến bài
> toán vô nghiệm):** nếu 3 điểm dùng để dựng hình bình hành THẲNG HÀNG (VD
> lỡ chọn A, B, D cùng nằm trên 1 đường vừa dựng ở bước trước), `dir` của 2
> đường sẽ song song nhau → `intersectionOfTwoLines` trả `reason:'parallel'`,
> `buildParallelogramSum` trả `null` — không phải lỗi code, là hệ quả hình
> học tất yếu của việc chọn 3 điểm thẳng hàng. Khi ràng buộc học sinh kéo
> điểm A,B,C,D tự do trên mặt phẳng nền (theo đúng SGK), PHẢI xử lý
> `null` bằng cách báo học sinh "3 điểm đang thẳng hàng, hãy kéo lại" thay
> vì để giao diện đơ hoặc vẽ nhầm điểm `(0,0,0)`.

---

## PHỤ LỤC — BẢNG QUY CHIẾU: hàm nào dùng ở đâu

| Hàm | Định nghĩa gốc trong | Dùng lại ở |
|---|---|---|
| `definePlaneFromPoints` | test_b_parallel.html | test_c/d, solid_library.html |
| `projectPointOntoPlane` | test_b_parallel.html | test_c/d, solid_library.html |
| `projectLineOntoPlane` | test_b_parallel.html | test_c_angles.html |
| `classifyLineToPlane` | test_b_parallel.html | test_d_distances.html |
| `classifyTwoPlanes` | test_b_parallel.html | — |
| `distanceBetweenParallelPlanes` | test_b_parallel.html | — |
| `intersectionOfTwoPlanes` | test_b_parallel.html | test_c_angles.html |
| `distanceLineToPlane` | test_d_distances.html | — |
| `lineIntersectPlane` | prototype4_sliding_cross_section.html (07/2026) | Tab 4B/5B thiết diện, Bài 10 Simulation 2 |
| `projectPointOntoLine` | test_c_angles.html | test_d_distances.html |
| `distanceSkewLines` | test_d_distances.html | — |
| `segmentIntersection` | prototype1_segment_intersection.html (07/2026) | Tab 1/2/4A/5A/5B, Bài 10 Simulation 2 |
| `polygonArea` | prototype5_section_area_match.html (07/2026) | Trạm 4 game Đền thờ Euclid ("Kho tri thức") |
| `angleLineToPlane` | test_c_angles.html | — |
| `dihedralAngle` | test_c_angles.html | — |
| `barycentricCoords` | solid_library.html | — |
| `rotateLineAroundNormal` | test_b_parallel.html | — |
| `pointOnSphere/Cylinder/ConeSide` + nghịch | tổng quát hoá từ `calcSphereSurfPos` v.v. trong solid_library.html | — |
| `intersectionOfTwoLines` (B.4) | verify Node độc lập, cài `three` qua npm (08/2026) | Hoạt động thực hành "Vẽ vectơ tổng ba vectơ" |
| `vectorFromPoints` (H.1) | verify Node độc lập, cài `three` qua npm (08/2026) | Hoạt động thực hành "Vẽ vectơ tổng ba vectơ" |
| `lineThroughPointParallelTo` (H.2) | verify Node độc lập, cài `three` qua npm (08/2026) | Hoạt động thực hành "Vẽ vectơ tổng ba vectơ" |
| `buildParallelogramSum` (H.3) | verify Node độc lập, cài `three` qua npm (08/2026) | Hoạt động thực hành "Vẽ vectơ tổng ba vectơ" |

> Các hàm **vẽ** cùng tên/chủ đề (không thuộc file này) — `buildPlaneMesh`,
> `buildRightAngleMark`, `buildArc`, `buildDihedralArc`, `buildMHSegment` —
> nằm trong `05_threejs_engine.md`. Nếu tìm 1 hàm mà không thấy ở đây, khả
> năng nó là hàm vẽ, tìm trong file 05.

---

> **Phiên bản:** 1.4
> **Ngày tạo:** 07/2026 — viết sau khi đã có 4+ file test/tool thực tế
> (`test_b_parallel.html`, `test_c_angles.html`, `test_d_distances.html`,
> `solid_library.html`), tách các hàm toán thuần trùng lặp giữa chúng thành
> 1 nguồn tham chiếu duy nhất. Mọi hàm đã verify chạy đúng trong ít nhất 1
> file thực tế trước khi đưa vào đây — không có hàm lý thuyết chưa kiểm chứng.
> **Cập nhật 07/2026 (v1.1):** thêm A.9 `lineIntersectPlane` và B.3
> `segmentIntersection`, cả 2 verify bằng script Node độc lập trước khi
> đưa vào file — xem PHỤ LỤC E trong `01_scenario_builder_3d_addendum.md`
> cho bài học prototype (lỗi chọn sai mặt phẳng phụ khiến giao điểm
> luôn trùng 1 đỉnh cố định).
> **Cập nhật 07/2026 (v1.2):** thêm PHẦN G (đa giác phẳng) — hàm
> `polygonArea` (G.1) + 2 bài học build thật (G.2: tráo tham số qua chữ
> ký hàm; G.3: chọn cấu hình khối vi phạm định lý đường trung bình khiến
> bài toán vô nghiệm). Cả G.1/G.2 liên quan trực tiếp tới lỗi
> `pointer-events`/tráo tham số đã ghi đầy đủ ở
> `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.9–E.10 — 2 loại lỗi này
> không bắt được bằng `node --check` hay verify Node độc lập, chỉ lộ ra
> khi có người dùng thật thao tác trên trình duyệt.
> **Đã đối chiếu:** các hàm cùng tên giữa nhiều file (`definePlaneFromPoints`,
> `projectPointOntoPlane`...) được so sánh từng dòng — xác nhận giống nhau
> hoàn toàn, không có bản lệch/bản lỗi nào bị chọn nhầm làm chuẩn.
> **Cập nhật 07/2026 (v1.3) — QUAN TRỌNG:** sửa lỗi thật trong `A.6
> intersectionOfTwoPlanes` — `denom` bị sai dấu (`n1n2²-1` thay vì đúng
> `1-n1n2²`), khiến điểm trả về luôn là ảnh đối xứng qua gốc toạ độ của
> điểm đúng, KHÔNG nằm trên mặt phẳng nào cả. Lỗi này từng bị đánh dấu
> "đã verify" trong bản v1.2 trở về trước — thực ra chưa được verify bằng
> 1 test case có điểm giao biết trước từ tính tay, chỉ được đọc code thấy
> "có vẻ đúng". Phát hiện khi build Trạm 2 game "Đền thờ Euclid" (2 mặt
> phẳng không thể nào giao đúng bệ thờ bất kể chỉnh góc thế nào). Xem đầy
> đủ: `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.11. **Nếu đã copy hàm
> A.6 sang bất kỳ file/prototype nào trước mốc này, phải rà lại và sửa.**
> **Cập nhật 08/2026 (v1.4):** thêm B.4 `intersectionOfTwoLines` (giao điểm
> 2 đường thẳng VÔ HẠN — biến thể của B.3 bỏ kẹp đoạn [0,1]) và PHẦN H —
> VECTƠ (`vectorFromPoints`, `lineThroughPointParallelTo`,
> `buildParallelogramSum`), phục vụ hoạt động thực hành "Vẽ vectơ tổng của
> ba vectơ trong không gian". Verify bằng script Node **cài `three` thật
> qua npm** (không dùng object `{x,y,z}` tự chế như các lần verify trước —
> để tránh lệch API `.clone()/.sub()/.normalize()` giữa bản test và bản
> thật), dựng đúng quy trình 2 bước SGK và đối chiếu đại số
> `AF = AB+AC+AD`, cộng 3 case đối chứng (skew/parallel/cắt nhau trong mặt
> phẳng nghiêng) — 6/6 pass.
> **Dùng cùng:** `05_threejs_engine.md` (pattern dựng mesh + tương tác)
