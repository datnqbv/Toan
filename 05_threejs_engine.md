# 🧊 THREE.JS ENGINE — Hình học không gian 3D tương tác

> **Mục đích:** Patterns kỹ thuật cho simulation 3D — kéo điểm/đường, ràng buộc,
> click-to-select, dựng hình theo bước, label, mặt phẳng, nhập toạ độ số, raycasting
> **Dùng kèm:** `04_design_toan_3d.md` (UI/UX) + `06_geometry_math.md` (hàm toán thuần)
> **Đọc file này khi:** Làm hình học không gian / kéo thả 3D / đo góc / dựng song song / Three.js / OrbitControls

---

## 🤖 TRIGGER — AI ĐỌC FILE NÀY KHI NÀO

Đọc toàn bộ file này khi kịch bản có bất kỳ từ khoá sau:
- **3D:** "không gian", "3D", "Three.js", "xoay camera", "OrbitControls"
- **Input 3D:** "kéo điểm", "kéo đường", "drag 3D", "raycasting", "click chọn"
- **Hình học:** "mặt phẳng", "đường thẳng", "điểm thuộc", "giao tuyến", "đồng phẳng", "cạnh", "đỉnh"
- **Quan hệ:** "song song", "góc giữa", "vuông góc", "dựng hình", "chéo nhau"
- **Khoảng cách:** "khoảng cách", "chân đường vuông góc", "chiếu vuông góc", "hình chiếu"
- **Dữ liệu:** "nhập toạ độ", "ẩn hiện", "toạ độ chính xác"

Khác với `03_game_engine.md` (Canvas 2D — toạ độ màn hình `mx, my`), file này dùng
**toạ độ thế giới 3D** (`Vector3`) và **raycasting** để biến chuột 2D thành điểm 3D.
Hai hệ thống KHÔNG dùng chung công thức hit-detection — không copy nhầm pattern 2D sang đây.

---

## PHẦN 0 — SETUP BẮT BUỘC

```html
<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/build/three.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/three@0.128.0/examples/js/controls/OrbitControls.js"></script>
```

> Dùng đúng r128 — OrbitControls tách thành module riêng ở r142+, import map sẽ phức tạp
> hơn cho file HTML đơn không server. Không tự đổi version trừ khi đã test lại toàn bộ.

```javascript
const wrap = document.getElementById('canvas-wrap');
const scene = new THREE.Scene();
scene.background = new THREE.Color(0x0d1117);

const camera = new THREE.PerspectiveCamera(50, wrap.clientWidth / wrap.clientHeight, 0.1, 1000);
camera.position.set(6, 5, 8);
camera.lookAt(0, 0, 0);

const renderer = new THREE.WebGLRenderer({ antialias: true });
renderer.setSize(wrap.clientWidth, wrap.clientHeight);
wrap.appendChild(renderer.domElement);

window.addEventListener('resize', () => {
  camera.aspect = wrap.clientWidth / wrap.clientHeight;
  camera.updateProjectionMatrix();
  renderer.setSize(wrap.clientWidth, wrap.clientHeight);
});

scene.add(new THREE.AmbientLight(0xffffff, 0.7));
const dirLight = new THREE.DirectionalLight(0xffffff, 0.6);
dirLight.position.set(5, 10, 7);
scene.add(dirLight);

// Lưới sàn + trục toạ độ — giúp học sinh định hướng không gian,
// đặc biệt quan trọng vì SGK nhấn mạnh "nhìn từ phía sau" để hiểu hình
const gridHelper = new THREE.GridHelper(12, 12, 0x30363d, 0x21262d);
scene.add(gridHelper);
const axesHelper = new THREE.AxesHelper(2);
scene.add(axesHelper);

// QUAN TRỌNG: phải tắt orbitControls.enabled khi đang kéo điểm
// (xem PHẦN 2) — nếu không 2 hệ thống input giành quyền điều khiển chuột.
const orbitControls = new THREE.OrbitControls(camera, renderer.domElement);
orbitControls.enableDamping = true;
orbitControls.dampingFactor = 0.08;
```

---

## PHẦN 1 — ĐIỂM KÉO ĐƯỢC (DraggablePoint)

> Nguồn gốc của hầu hết lỗi trong simulation 3D là raycasting sai cách.
> Áp dụng đúng pattern dưới đây trước khi viết bất kỳ logic kéo-thả nào.

### 1.1 Cấu trúc 1 điểm — mesh thật + hit-area vô hình (BẮT BUỘC)

```
Lý do tách 2 mesh riêng:
  - mesh thật: nhỏ (bán kính ~0.09), để hình không bị "to quá khổ"
  - hitMesh vô hình: lớn hơn (~0.28), chỉ dùng cho raycaster.intersectObjects()

Nếu dùng chung 1 mesh cho cả hiển thị và hit-test, điểm phải vẽ to mới
dễ kéo — nhưng to thì hình mất tỉ lệ thật. Tách riêng giải quyết cả 2.
Quan trọng nhất với thiết bị chạm (iPad) vì đầu ngón tay che diện tích
lớn hơn con trỏ chuột nhiều.
```

```javascript
class DraggablePoint {
  constructor(position, color, label) {
    this.label = label;
    this.color = color;

    const geometry = new THREE.SphereGeometry(0.09, 24, 24);
    const material = new THREE.MeshStandardMaterial({ color, emissive: color, emissiveIntensity: 0.25 });
    this.mesh = new THREE.Mesh(geometry, material);
    this.mesh.position.copy(position);
    this.mesh.userData.draggable = this; // raycaster truy ngược lại object qua đây
    scene.add(this.mesh);

    // Hit-area vô hình LỚN HƠN mesh thật
    const hitGeo = new THREE.SphereGeometry(0.28, 8, 8);
    const hitMat = new THREE.MeshBasicMaterial({ visible: false });
    this.hitMesh = new THREE.Mesh(hitGeo, hitMat);
    this.hitMesh.position.copy(position);
    this.hitMesh.userData.draggable = this;
    scene.add(this.hitMesh);

    // Glow ring — feedback trực quan khi đang kéo
    const ringGeo = new THREE.RingGeometry(0.14, 0.18, 32);
    const ringMat = new THREE.MeshBasicMaterial({ color, transparent: true, opacity: 0, side: THREE.DoubleSide });
    this.ring = new THREE.Mesh(ringGeo, ringMat);
    this.ring.position.copy(position);
    scene.add(this.ring);
  }

  get position() { return this.mesh.position; }

  setDragging(active) {
    this.ring.material.opacity = active ? 0.8 : 0;
    this.mesh.material.emissiveIntensity = active ? 0.6 : 0.25;
  }

  syncRing() {
    this.ring.position.copy(this.mesh.position);
    this.ring.lookAt(camera.position); // ring luôn quay mặt về camera
    this.hitMesh.position.copy(this.mesh.position); // hit-area đi theo điểm thật
  }
}
```

### 1.2 Billboard drag-plane — chuyển chuột 2D thành điểm 3D (CỐT LÕI NHẤT)

```
Đây là bài toán kỹ thuật khó nhất của toàn bộ simulation 3D, và là chỗ
90% dự án giáo dục dạng này bị vướng (kéo bị "trôi", giật khi đổi góc camera).

NGUYÊN LÝ: chuột chỉ có 2 toạ độ (x, y màn hình) nhưng không gian có 3
chiều — thiếu 1 phương trình. Phải tự thêm 1 ràng buộc để giải được.
Ràng buộc đúng nhất cho "kéo tự do": 1 mặt phẳng vô hình VUÔNG GÓC VỚI
HƯỚNG NHÌN của camera, đi qua đúng vị trí hiện tại của điểm.

Vì mặt phẳng luôn "song song với màn hình" tại đúng độ sâu của điểm,
điểm di chuyển đúng theo cảm giác trực quan của chuột, không bị trôi
xa theo độ sâu khi camera ở góc nghiêng.
```

```javascript
const raycaster = new THREE.Raycaster();
const mouseNDC = new THREE.Vector2();

let dragState = {
  active: false,
  point: null,        // object đang kéo (DraggablePoint hoặc ConstrainedPoint)
  dragPlane: null     // THREE.Plane vô hình dùng để raycast lên khi kéo
};

function updateMouseNDC(event) {
  const rect = renderer.domElement.getBoundingClientRect();
  mouseNDC.x = ((event.clientX - rect.left) / rect.width) * 2 - 1;
  mouseNDC.y = -((event.clientY - rect.top) / rect.height) * 2 + 1;
}

function getPointerIntersect(meshList) {
  raycaster.setFromCamera(mouseNDC, camera);
  return raycaster.intersectObjects(meshList);
}

renderer.domElement.addEventListener('pointerdown', (event) => {
  updateMouseNDC(event);
  const hits = getPointerIntersect(allDraggableHitMeshes); // mảng hitMesh của mọi điểm

  if (hits.length > 0) {
    const hitPoint = hits[0].object.userData.draggable;
    dragState.active = true;
    dragState.point = hitPoint;

    // Tạo billboard drag-plane: pháp tuyến = hướng camera, đi qua vị trí điểm
    const camDir = new THREE.Vector3();
    camera.getWorldDirection(camDir);
    dragState.dragPlane = new THREE.Plane().setFromNormalAndCoplanarPoint(camDir, hitPoint.position);

    hitPoint.setDragging(true);
    orbitControls.enabled = false; // TẮT orbit — bắt buộc, xem giải thích PHẦN 0
  }
});

renderer.domElement.addEventListener('pointermove', (event) => {
  updateMouseNDC(event);
  if (!dragState.active || !dragState.point) {
    // Hover feedback khi không kéo
    const hits = getPointerIntersect(allDraggableHitMeshes);
    renderer.domElement.style.cursor = hits.length > 0 ? 'grab' : 'default';
    return;
  }

  raycaster.setFromCamera(mouseNDC, camera);
  const intersection = new THREE.Vector3();
  const hit = raycaster.ray.intersectPlane(dragState.dragPlane, intersection);

  if (hit) {
    dragState.point.mesh.position.copy(intersection); // điểm tự do: gán trực tiếp
    // (điểm bị ràng buộc dùng dragToward() — xem PHẦN 2, KHÔNG gán trực tiếp)
  }
});

renderer.domElement.addEventListener('pointerup', () => {
  if (dragState.active && dragState.point) dragState.point.setDragging(false);
  dragState.active = false;
  dragState.point = null;
  dragState.dragPlane = null;
  orbitControls.enabled = true; // BẬT lại orbit
});

// BẮT BUỘC — cancel an toàn khi chuột rời canvas giữa lúc đang kéo
renderer.domElement.addEventListener('pointerleave', () => {
  if (dragState.active && dragState.point) dragState.point.setDragging(false);
  dragState.active = false;
  dragState.point = null;
  orbitControls.enabled = true;
});
```

> **Touch support:** dùng `pointerdown/pointermove/pointerup` (Pointer Events API)
> thay vì `mousedown/mousemove/mouseup` — Pointer Events tự xử lý cả mouse và touch
> trong cùng 1 listener, không cần viết riêng `touchToMouse()` như ở Canvas 2D.

---

## PHẦN 2 — ĐIỂM RÀNG BUỘC (ConstrainedPoint)

> Pattern dùng cho ĐA SỐ bài tập SGK hình học không gian — "lấy điểm M thuộc
> cạnh SA", "M khác S và A". Khác hẳn PHẦN 1 (điểm bay tự do), điểm này chỉ
> có 1 BẬC TỰ DO: tham số `t` dọc theo đoạn thẳng (hoặc tổng quát hơn: trên
> mặt phẳng, trên mặt cầu — nguyên lý chiếu + clamp là giống nhau).

### 2.1 Vì sao không dùng chung billboard-plane như điểm tự do

```
Nếu gán trực tiếp intersection (kết quả raycast trên billboard-plane)
vào vị trí điểm, điểm sẽ BAY RA KHỎI đoạn thẳng ngay khi chuột di
chuyển không đúng hướng đoạn — vì billboard-plane không "biết" về
ràng buộc đoạn thẳng.

Giải pháp đúng: VẪN dùng billboard-plane để lấy 1 điểm 3D thô từ chuột
(bước 1, không đổi so với PHẦN 1) — nhưng sau đó CHIẾU điểm thô đó
xuống đoạn thẳng bằng phép chiếu vector, rồi CLAMP tham số t vào [0,1].
```

### 2.2 Code — class ConstrainedPoint

```javascript
class ConstrainedPoint {
  constructor(segStart, segEnd, t0, color, label) {
    this.segStart = segStart; // Vector3 cố định, không đổi khi kéo
    this.segEnd = segEnd;     // Vector3 cố định, không đổi khi kéo
    this.t = t0;              // tham số 0..1 dọc theo đoạn — ĐÂY là state thật,
                               // KHÔNG lưu vị trí Vector3 trực tiếp làm state
    this.color = color;
    this.label = label;
    this.isConstrained = true; // cờ phân biệt với DraggablePoint khi xử lý drag

    const geometry = new THREE.SphereGeometry(0.09, 24, 24);
    const material = new THREE.MeshStandardMaterial({ color, emissive: color, emissiveIntensity: 0.25 });
    this.mesh = new THREE.Mesh(geometry, material);
    this.mesh.userData.draggable = this;
    scene.add(this.mesh);

    const hitGeo = new THREE.SphereGeometry(0.28, 8, 8);
    const hitMat = new THREE.MeshBasicMaterial({ visible: false });
    this.hitMesh = new THREE.Mesh(hitGeo, hitMat);
    this.hitMesh.userData.draggable = this;
    scene.add(this.hitMesh);

    const ringGeo = new THREE.RingGeometry(0.14, 0.18, 32);
    const ringMat = new THREE.MeshBasicMaterial({ color, transparent: true, opacity: 0, side: THREE.DoubleSide });
    this.ring = new THREE.Mesh(ringGeo, ringMat);
    scene.add(this.ring);

    this.updateMeshPosition();
  }

  // Vị trí thật = nội suy tuyến tính giữa 2 đầu mút theo t.
  // Tính lại mỗi lần gọi, không cache — segStart/segEnd có thể đổi
  // nếu cạnh cha (ví dụ cạnh của hình chóp) bị kéo lại.
  get position() {
    return new THREE.Vector3().lerpVectors(this.segStart, this.segEnd, this.t);
  }

  updateMeshPosition() {
    const pos = this.position;
    this.mesh.position.copy(pos);
    this.hitMesh.position.copy(pos);
    this.ring.position.copy(pos);
  }

  // HÀM CỐT LÕI: nhận điểm 3D thô từ raycast chuột, chiếu lên đoạn
  // thẳng, clamp t vào [0,1], cập nhật vị trí. Gọi hàm này thay cho
  // "mesh.position.copy(intersection)" ở PHẦN 1.
  dragToward(rawPoint3D) {
    const segVec = new THREE.Vector3().subVectors(this.segEnd, this.segStart);
    const segLenSq = segVec.lengthSq();
    const toPoint = new THREE.Vector3().subVectors(rawPoint3D, this.segStart);

    let t = toPoint.dot(segVec) / segLenSq; // công thức chiếu vector chuẩn
    t = Math.max(0, Math.min(1, t));        // CLAMP — bắt buộc, không cho vượt 2 đầu mút

    this.t = t;
    this.updateMeshPosition();
  }

  setDragging(active) {
    this.ring.material.opacity = active ? 0.8 : 0;
    this.mesh.material.emissiveIntensity = active ? 0.6 : 0.25;
  }

  syncRing() {
    this.ring.lookAt(camera.position);
  }
}
```

### 2.3 Tích hợp vào hệ thống drag chung (PHẦN 1)

```
Điểm mấu chốt: ConstrainedPoint và DraggablePoint dùng CHUNG một hệ
thống pointerdown/pointermove/pointerup. Chỉ khác đúng 1 nhánh rẽ tại
bước cập nhật vị trí — kiểm tra cờ isConstrained. Đây là lý do nên
tách "input event" ra khỏi "constraint logic": thêm loại ràng buộc mới
(kéo trên mặt phẳng, kéo trên mặt cầu) sau này chỉ cần thêm class mới
+ 1 nhánh rẽ, không phải viết lại toàn bộ raycasting.
```

```javascript
// Trong pointermove handler ở PHẦN 1, thay đoạn gán trực tiếp bằng:
if (hit) {
  if (dragState.point.isConstrained) {
    dragState.point.dragToward(intersection); // chiếu + clamp
  } else {
    dragState.point.mesh.position.copy(intersection); // tự do
  }
}
```

### 2.4 Cạnh cố định (đoạn P-Q) làm khung tham chiếu

```javascript
// 2 đầu mút P, Q vẽ tĩnh — không kéo được, chỉ định nghĩa cạnh
function makeFixedMarker(pos, color, label) {
  const geo = new THREE.SphereGeometry(0.07, 16, 16);
  const mat = new THREE.MeshStandardMaterial({ color });
  const mesh = new THREE.Mesh(geo, mat);
  mesh.position.copy(pos);
  scene.add(mesh);
  return mesh;
}

const segP = new THREE.Vector3(-1.5, 0.3, 3);
const segQ = new THREE.Vector3(1.5, 3.2, 3);
const segGeo = new THREE.BufferGeometry().setFromPoints([segP, segQ]);
const segLine = new THREE.Line(segGeo, new THREE.LineBasicMaterial({ color: 0x8b949e }));
scene.add(segLine);

const pointM = new ConstrainedPoint(segP, segQ, 0.5, 0xEF9F27, 'M');
```

### 2.5 Điểm ràng buộc TRÊN MẶT PHẲNG (khác billboard — raycast thẳng vào mặt phẳng thật)

> Mở rộng tự nhiên của PHẦN 2: thay vì ràng buộc trên 1 ĐOẠN THẲNG (1 bậc
> tự do, tham số t), đây là ràng buộc trên 1 MẶT PHẲNG (2 bậc tự do). Dùng
> khi bài yêu cầu "kéo điểm M sao cho M luôn thuộc mặt phẳng (Q)" — đặc
> biệt khi (Q) bản thân cũng nghiêng/xoay được.

```
KHÁC BIỆT CỐT LÕI với billboard-plane (PHẦN 1.2):
  Billboard-plane LUÔN vuông góc hướng nhìn camera, đi qua vị trí hiện
  tại của điểm — dùng cho điểm TỰ DO, không ràng buộc gì.

  Ở đây, mặt phẳng dùng để raycast KHÔNG PHẢI billboard, mà CHÍNH LÀ
  mặt phẳng toán học (Q) mà điểm cần thuộc về. Vì vậy raycast luôn cho
  ra điểm NẰM ĐÚNG TRÊN (Q), bất kể (Q) đang nghiêng góc nào — không
  cần bước "chiếu lại" sau khi raycast như PHẦN 2.2 (ConstrainedPoint
  trên đoạn thẳng phải chiếu + clamp t; ở đây raycast trực tiếp vào mặt
  phẳng đã tự động cho kết quả đúng, không cần bước chiếu riêng).

LỖI THỰC TẾ ĐÃ GẶP khi build: mesh dùng để raycast (rayTargetMesh) mặc
định chỉ nhận va chạm từ 1 PHÍA (side: THREE.FrontSide, giá trị mặc
định của MeshBasicMaterial). Khi camera xoay sang phía "sau" mặt phẳng,
raycast trượt qua luôn — hit.length === 0, điểm đứng yên rồi "nhảy
cóc" khi raycast trúng lại ở góc khác, tạo cảm giác điểm tự trôi lung
tung thay vì dính đúng mặt. BẮT BUỘC set side: THREE.DoubleSide cho
mesh raycast (không phải mesh hiển thị — mesh hiển thị có thể giữ
FrontSide nếu muốn, đây là 2 mesh riêng biệt, xem bên dưới).
```

```javascript
// ===== MẶT PHẲNG (Q) — vừa hiển thị vừa dùng để raycast =====
let planeNormal = new THREE.Vector3(0, 1, 0);
let planeCenter = new THREE.Vector3(0, 0.8, 0);
let mathPlane = new THREE.Plane().setFromNormalAndCoplanarPoint(planeNormal, planeCenter);

// Mesh HIỂN THỊ — kích thước hữu hạn, người dùng nhìn thấy khung mặt phẳng
const planeGeo = new THREE.PlaneGeometry(6, 6);
const planeMat = new THREE.MeshStandardMaterial({
  color: 0x3b82f6, transparent: true, opacity: 0.28, side: THREE.DoubleSide, depthWrite: false
});
const planeMesh = new THREE.Mesh(planeGeo, planeMat);
scene.add(planeMesh);

// Mesh RAYCAST — LỚN HƠN NHIỀU (200x200) để "cảm giác vô hạn" khi điểm
// kéo ra gần mép khung hiển thị, và BẮT BUỘC DoubleSide (xem lỗi ở trên)
const rayTargetGeo = new THREE.PlaneGeometry(200, 200);
const rayTargetMat = new THREE.MeshBasicMaterial({ visible: false, side: THREE.DoubleSide });
const rayTargetMesh = new THREE.Mesh(rayTargetGeo, rayTargetMat);
scene.add(rayTargetMesh);

function updatePlaneTransform() {
  planeMesh.position.copy(planeCenter);
  planeMesh.lookAt(planeCenter.clone().add(planeNormal));
  rayTargetMesh.position.copy(planeCenter);
  rayTargetMesh.lookAt(planeCenter.clone().add(planeNormal));
  mathPlane.setFromNormalAndCoplanarPoint(planeNormal, planeCenter);
}
updatePlaneTransform();

// ===== KÉO ĐIỂM M — raycast thẳng vào rayTargetMesh, KHÔNG qua billboard =====
// (đặt trong pointermove handler, khi dragMode === 'point-constrained-on-plane')
function onDragPointOnPlane(raycaster, pointMesh) {
  const hit = raycaster.intersectObject(rayTargetMesh);
  if (hit.length > 0) {
    pointMesh.position.copy(hit[0].point); // LUÔN nằm đúng trên (Q), mọi góc nghiêng
  }
}

// ===== KHI MẶT PHẲNG (Q) ĐỔI HƯỚNG (bị nghiêng lại) =====
// Điểm M đã đặt trước đó PHẢI "dính" lại đúng mặt phẳng mới — dùng
// THREE.Plane.projectPoint(), không tự tính tay bằng công thức chiếu.
function reprojectPointAfterPlaneTilt(pointMesh) {
  const projected = new THREE.Vector3();
  mathPlane.projectPoint(pointMesh.position, projected);
  pointMesh.position.copy(projected);
}
```

> **Verify đã làm:** HUD hiển thị khoảng cách thật từ M tới (Q)
> (`Math.abs(toPoint.dot(planeNormal))`, phải luôn < 0.001) — dùng để phát
> hiện ngay nếu có sai sót raycast, không chỉ "nhìn bằng mắt thấy có vẻ
> đúng". Có nút test "nghiêng mặt phẳng ngẫu nhiên" để xác nhận M luôn tự
> dính lại đúng sau khi (Q) đổi hướng bất kỳ.

---

## PHẦN 2.6 — ĐIỂM RÀNG BUỘC XOAY TRÊN CUNG TRÒN quanh 1 TRỤC CỐ ĐỊNH (bản lề)

> Mở rộng khác của PHẦN 2: ràng buộc trên 1 CUNG TRÒN quanh 1 trục cố định
> (1 bậc tự do là GÓC, không phải tham số t dọc đoạn thẳng như PHẦN 2 gốc,
> cũng không phải 2 bậc tự do trên mặt phẳng như PHẦN 2.5). Dùng cho các
> tương tác kiểu "xoay tường/cửa/nắp quanh 1 bản lề cố định" — ví dụ Trạm 2
> game "Đền thờ Euclid" (07/2026): 2 bức tường xoay quanh chân tường cố
> định trên nền, tìm góc nghiêng đúng để giao tuyến chạm 1 điểm đích.
>
> **Không viết công thức xoay mới** — tái dùng đúng nguyên lý quaternion
> của `rotateLineAroundNormal` (PHẦN 4.14.1), chỉ khác ở BƯỚC NGƯỢC: từ
> điểm kéo thô (billboard raycast, PHẦN 1) suy ra GÓC bằng `atan2`, rồi
> áp dụng lại đúng góc đó để snap điểm về đúng cung tròn — giống tinh
> thần "chiếu + clamp" của `dragToward()` (PHẦN 2.2) nhưng ràng buộc là
> góc thay vì tham số t tuyến tính.

### 2.6.1 Nguyên lý: suy góc từ điểm kéo thô, rồi snap lại đúng cung

```javascript
// hingeBase: 1 điểm trên trục bản lề (VD chân tường trên nền)
// hingeAxisDir: hướng trục bản lề, ĐÃ NORMALIZE (VD (0,0,1) nếu bản lề dọc trục z)
// armLength: bán kính cung tay cầm quay quanh bản lề
// inward: +1 hoặc -1, quy định "góc tăng" làm tay cầm di chuyển về hướng nào
//   (VD +1 cho tường bên trái tilt vào giữa, -1 cho tường bên phải)
//
// Bước 1 — TỪ VỊ TRÍ KÉO THÔ suy ra góc: chỉ cần 2 thành phần vuông góc
// với trục bản lề (ở đây trục là (0,0,1) nên chỉ cần x,y — bỏ qua z vì
// góc không phụ thuộc học sinh kéo lệch dọc trục bao nhiêu)
function angleFromRawDrag(rawPoint3D, hingeBaseX, inward, thetaMin, thetaMax) {
  const dx = inward * (rawPoint3D.x - hingeBaseX);
  const dy = Math.max(0.2, rawPoint3D.y); // sàn dưới, tránh chia/atan2 tại gốc suy biến
  let theta = Math.atan2(dx, dy);
  return Math.max(thetaMin, Math.min(thetaMax, theta)); // CLAMP — bắt buộc, giống PHẦN 2.2
}

// Bước 2 — TỪ GÓC suy ra vị trí đúng trên cung tròn (hàm thuận,
// dùng CẢ khi khởi tạo vị trí ban đầu VÀ khi snap lại sau khi kéo)
function pointOnHingeArc(hingeBaseX, inward, theta, armLength, fixedY_axisCoord) {
  return new THREE.Vector3(
    hingeBaseX + inward * armLength * Math.sin(theta),
    armLength * Math.cos(theta),
    fixedY_axisCoord // toạ độ dọc theo trục bản lề — KHÔNG đổi theo theta
  );
}

// Bước 3 — trong pointermove: gán vị trí thô như điểm tự do (PHẦN 1),
// rồi NGAY SAU ĐÓ ghi đè lại bằng snap — visual không giật vì cùng 1 tick
window.__onDragUpdate = (pt) => {
  const theta = angleFromRawDrag(pt.mesh.position, hingeBaseX, inward, THETA_MIN, THETA_MAX);
  pt.mesh.position.copy(pointOnHingeArc(hingeBaseX, inward, theta, ARM_LENGTH, fixedAxisCoord));
  pt.hitMesh.position.copy(pt.mesh.position); // đồng bộ hit-area theo vị trí đã snap
  onThetaChanged(theta); // rebuild mặt phẳng/hình học phụ thuộc góc này
};
```

> **Vì sao KHÔNG dùng `ConstrainedPoint.dragToward()` (PHẦN 2.2) trực
> tiếp:** `dragToward()` chiếu điểm thô XUỐNG 1 ĐOẠN THẲNG (phép chiếu
> vector tuyến tính). Ở đây ràng buộc là 1 CUNG TRÒN — phép "chiếu" đúng
> về mặt hình học là suy góc bằng `atan2` rồi tính lại vị trí bằng
> sin/cos, không phải phép chiếu tuyến tính. Cùng TINH THẦN (chiếu +
> clamp trước khi gán vị trí, không gán trực tiếp `intersection` thô)
> nhưng công thức khác — không cố ép dùng lại `dragToward()` cho trường
> hợp này.

### 2.6.2 Kết hợp với thanh trượt số (đồng bộ 2 chiều)

```javascript
// Giống PHẦN 4.9 (nhập toạ độ số đồng bộ 2 chiều) nhưng cho góc:
// - Kéo chuột -> slider.value tự cập nhật theo theta vừa snap được
// - Kéo slider -> tính lại điểm bằng pointOnHingeArc(), KHÔNG animation
//   (học sinh cần thấy đúng số ngay, giống PHẦN 4.9)
function setThetaFromSlider(deg, hingeBaseX, inward, armLength, fixedAxisCoord) {
  const theta = Math.max(THETA_MIN, Math.min(THETA_MAX, deg * Math.PI / 180));
  const newPos = pointOnHingeArc(hingeBaseX, inward, theta, armLength, fixedAxisCoord);
  pt.mesh.position.copy(newPos);
  pt.hitMesh.position.copy(newPos);
  onThetaChanged(theta);
}
```

> **Lý do nên có cả 2 (kéo chuột VÀ slider số):** riêng kéo chuột tự do
> qua billboard-plane (PHẦN 1) rất khó để học sinh dừng đúng 1 góc chính
> xác — sai số vài độ dễ xảy ra do góc camera/độ nhạy chuột. Thanh trượt
> số cho phép chỉnh chính xác tới 0.5°, kéo chuột vẫn giữ lại để khám
> phá/cảm nhận trực quan trước. Đã áp dụng ở Trạm 2 game "Đền thờ Euclid"
> sau khi bản kéo-tự-do-3-chiều (không ràng buộc cung tròn) bị phản hồi
> là "quá khó, không thể điều khiển chính xác 1 góc nghiêng".

---

## PHẦN 2.7 — ĐIỂM RÀNG BUỘC XOAY TRÊN CUNG TRÒN quanh 1 TRỤC ĐỨNG (bản lề dọc, cung quét MẶT PHẲNG NGANG)

> **Thêm 08/2026** — PHẦN 2.6 ở trên mô hình bản lề NGANG (trục ngang,
> VD chân tường trên nền), cung quét trên MẶT PHẲNG ĐỨNG, và công thức
> `angleFromRawDrag` của 2.6 dùng `Math.max(0.2, rawPoint3D.y)` để ép dy
> luôn dương — điều này giới hạn góc CHỈ ĐƯỢC trong khoảng gần (−90°,90°),
> không đủ cho các ca cần bản lề ĐỨNG (trục dọc, VD cửa tủ quần áo, cần
> cẩu tháp) với cung quét trên MẶT PHẲNG NGANG, cần góc mở tới ~170° hoặc
> đủ 360°. ĐÂY LÀ PATTERN KHÁC, không phải chỉnh tham số của 2.6.
>
> ⚠️ **Sửa lại trích dẫn sai ở kịch bản Bài 23** (Module 1 Bước 1 — tủ
> quần áo; Module 2 Nhóm 3 — cần cẩu tháp): cả 2 đã trích dẫn nhầm PHẦN 2.6
> — phải dùng PHẦN 2.7 này mới đúng, vì bản lề của cả 2 ca đó đứng dọc, cung
> quét ngang, không phải bản lề ngang cung quét đứng như 2.6.

### 2.7.1 Nguyên lý: `atan2` KHÔNG ép dấu — cho phép quét gần hết vòng tròn

```javascript
// hingeBase: điểm chân bản lề (trên mặt đất/mặt ngang, VD chân cột)
// armLength: bán kính cung tay cầm (VD chiều rộng cửa tủ, chiều dài cần
//   cẩu)
// fixedY: chiều cao cố định của bản lề (không đổi khi xoay — bản lề đứng
//   dọc trục y, cung nằm ngang tại 1 độ cao fixedY)
//
// Bước 1 — TỪ VỊ TRÍ KÉO THÔ suy ra góc: dùng CẢ 2 thành phần ngang
// (x, z), KHÔNG ép dấu như 2.6 — atan2 cho kết quả đầy đủ (−180°,180°]
function angleFromRawDrag_Horizontal(rawPoint3D, hingeBase, thetaMinDeg, thetaMaxDeg) {
  const dx = rawPoint3D.x - hingeBase.x;
  const dz = rawPoint3D.z - hingeBase.z;
  let theta = Math.atan2(dz, dx); // KHÔNG clamp dz như 2.6 clamp dy — đây
                                    // là điểm khác biệt cốt lõi so với 2.6
  const thetaMin = thetaMinDeg * Math.PI / 180;
  const thetaMax = thetaMaxDeg * Math.PI / 180;
  return Math.max(thetaMin, Math.min(thetaMax, theta)); // vẫn CLAMP theo
                                    // khoảng cho phép — cửa tủ dùng
                                    // [0°,170°], cần cẩu dùng [-180°,180°]
                                    // (coi như không giới hạn thực tế)
}

// Bước 2 — TỪ GÓC suy ra vị trí trên cung (mặt phẳng NGANG, y cố định)
function pointOnHingeArc_Horizontal(hingeBase, theta, armLength, fixedY) {
  return new THREE.Vector3(
    hingeBase.x + armLength * Math.cos(theta),
    fixedY,
    hingeBase.z + armLength * Math.sin(theta)
  );
}
```

> **Vì sao KHÔNG tái dùng thẳng `angleFromRawDrag`/`pointOnHingeArc` của
> 2.6:** 2.6 gán y = f(theta) (biến đổi theo góc, dùng cho cung ĐỨNG); ở
> đây y CỐ ĐỊNH (`fixedY`, không đổi theo theta) vì cung nằm NGANG — đổi
> vai trò trục nào biến đổi/trục nào cố định, không chỉ đổi tên biến.

### 2.7.2 Áp dụng cụ thể — 2 ca dùng khác THETA_MIN/MAX

```javascript
// Ca 1 — Cửa tủ quần áo (Bài 23 Module 1 Bước 1): giới hạn 0°-170°,
// không cho mở quá (cửa chạm thân tủ)
const doorTheta = angleFromRawDrag_Horizontal(rawDragPoint, hingeBase, 0, 170);

// Ca 2 — Cần cẩu tháp (Bài 23 Module 2 Nhóm 3): xoay đủ vòng, không
// chặn — dùng khoảng [-180, 180] (atan2 tự nhiên đã nằm trong khoảng này,
// clamp ở đây chỉ mang tính hình thức, không thực sự giới hạn)
const craneTheta = angleFromRawDrag_Horizontal(rawDragPoint, hingeBase, -180, 180);
```

⚠️ **Chưa verify bằng file HTML thật** — pattern mới, viết theo đúng tinh
thần 2.6 nhưng đổi trục. Prototype nhỏ (1 thanh xoay quanh 1 điểm cố định
trên mặt phẳng ngang, kéo full vòng) trước khi build chính thức Bài 23.

---

## PHẦN 2.8 — NÓN CÁC HƯỚNG VUÔNG GÓC VỚI 1 ĐƯỜNG CHO TRƯỚC (xoay tự do trên nón)

> **Thêm 08/2026** — phục vụ Bài 23 Module 2 Nhóm 1 bước "bẫy" (cột đèn
> nghiêng tự do nhưng luôn vuông góc với 1 sợi dây điện cho trước — nhắm
> sai lầm D: "cùng vuông góc 1 đường thẳng chưa chắc song song"). Đây LÀ
> pattern MỚI hoàn toàn (không phải biến thể của pattern kéo-thả nào đã
> có) — nhưng KHÔNG viết code xoay mới, tái dùng đúng
> `rotateLineAroundNormal` (PHẦN 4.14.1) làm phần xoay, chỉ thêm bước khởi
> tạo điểm bắt đầu trên nón bằng `arbitraryPerpendicular`
> (06_geometry_math.md PHẦN C.4).

```javascript
// fixedLineDir: hướng đường cho trước (VD dây điện) — vectơ ĐÃ NORMALIZE
// pivot: điểm chân cột (gốc của nón)
// coneRadius: độ dài đoạn biểu diễn hướng cột trên nón

// Bước 1 — khởi tạo 1 điểm BẤT KỲ trên nón (chỉ cần 1 lần khi bắt đầu)
const initialPerp = arbitraryPerpendicular(fixedLineDir); // 06 PHẦN C.4
const initialConeTip = pivot.clone().add(initialPerp.clone().multiplyScalar(coneRadius));

// Bước 2 — khi học sinh kéo, XOAY điểm này quanh TRỤC = fixedLineDir
// (tái dùng nguyên hàm đã có, không viết lại)
function updateConeDrag(thetaDeg) {
  const { newP } = rotateLineAroundNormal(
    initialConeTip, initialConeTip, /* pivotM= */ pivot, /* normal= */ fixedLineDir, thetaDeg
  );
  // newP luôn cách pivot đúng coneRadius và luôn vuông góc fixedLineDir
  // với MỌI thetaDeg — đây chính là điều cần minh hoạ (nhắm sai lầm D)
  cotDen2Mesh.position.copy(newP);
}
```

> ⚠️ **Chưa verify bằng file HTML thật** — kết hợp 2 hàm đã có sẵn theo
> cách MỚI (chưa từng dùng cùng nhau trong kịch bản trước đây). Verify
> bằng script Node: kiểm tra `newP - pivot` luôn vuông góc `fixedLineDir`
> (dot ≈ 0) ở nhiều giá trị `thetaDeg` khác nhau, trước khi build.

---

## PHẦN 2.9 — TỊNH TIẾN THEO QUỸ ĐẠO, GIỮ NGUYÊN HƯỚNG (không tự xoay theo vị trí)

> **Thêm 08/2026** — phục vụ Bài 24 Module 2 Phần 4 (mô hình Trái Đất
> quay quanh Mặt Trời, trục nghiêng giữ PHƯƠNG CỐ ĐỊNH trong không gian).
> Đây LÀ pattern khác hẳn mọi pattern xoay-quanh-trục đã có (PHẦN 2.6,
> 2.7, 4.14.1) — ở đó vật/đường XOAY THEO tham số góc; ở đây vật DI
> CHUYỂN theo quỹ đạo nhưng HƯỚNG GẮN VỚI VẬT KHÔNG ĐỔI, dễ lẫn với
> trực giác sai "vật di chuyển quanh 1 tâm thì phải tự quay theo".

```javascript
// center: tâm quỹ đạo (VD Mặt Trời), radius: bán kính quỹ đạo
// phiDeg: vị trí góc trên quỹ đạo (0°-360°, tương ứng % năm đã qua)
// Quỹ đạo nằm trong mặt phẳng NGANG (y không đổi = center.y)
function pointOnOrbit(center, radius, phiDeg) {
  const phi = phiDeg * Math.PI / 180;
  return new THREE.Vector3(
    center.x + radius * Math.cos(phi),
    center.y,
    center.z + radius * Math.sin(phi)
  );
}

// axisDirFixed: hướng trục nghiêng — ĐẶT 1 LẦN DUY NHẤT khi khởi tạo,
// KHÔNG được tính lại theo phiDeg — đây chính là điểm dễ code sai nhất
const axisDirFixed = new THREE.Vector3(
  Math.sin(23.5 * Math.PI / 180),
  Math.cos(23.5 * Math.PI / 180),
  0
).normalize();

// Cập nhật mỗi khi slider đổi vị trí quỹ đạo — CHỈ đổi position, KHÔNG
// đụng vào hướng trục hiển thị (mesh trục con giữ nguyên rotation cố định
// từ lúc khởi tạo, chỉ mesh THÂN Trái Đất mới di chuyển theo earthGroup)
function updateEarthOrbitPosition(phiDeg) {
  const pos = pointOnOrbit(sunCenter, orbitRadius, phiDeg);
  earthGroup.position.copy(pos); // CHỈ set position
  // KHÔNG gọi earthGroup.lookAt(...) hay bất kỳ hàm xoay nào theo phiDeg —
  // đây là lỗi hay gặp nhất khi mới quen viết code quỹ đạo (nhầm với kiểu
  // Mặt Trăng luôn quay 1 mặt về Trái Đất — khác bản chất với Trái Đất
  // quanh Mặt Trời, trục KHÔNG tự động hướng theo tâm quỹ đạo)
}
```

> ⚠️ **Bẫy code hay gặp (ghi chú riêng vì rất dễ nhầm):** nếu lỡ gọi
> `earthGroup.lookAt(sunCenter)` hoặc bất kỳ hàm xoay-theo-vị-trí nào mỗi
> khi cập nhật `phiDeg`, trục nghiêng SẼ BỊ XOAY THEO vị trí quỹ đạo —
> cho ra kết quả SAI (góc trục-mặt phẳng quỹ đạo sẽ đổi theo `phiDeg`,
> trái với vật lý thật). Đây chính là lỗi cần tránh khi build, vì code
> quỹ đạo bằng Three.js theo bản năng thường "tiện tay" thêm `lookAt()`.

⚠️ **Chưa verify bằng file HTML thật** — đã verify công thức bằng Node
(`three` thật qua npm, xem log verify Bài 24 Module 2), góc trục-mặt
phẳng quỹ đạo giữ đúng 66,5° ở cả 4 vị trí test. Prototype nhỏ (1 hình
cầu tịnh tiến quanh 1 điểm, có 1 mũi tên chỉ hướng cố định gắn theo) trước
khi build chính thức.

---

## PHẦN 2.10 — KHUNG XOAY LỒNG NHAU (GIMBAL), VẬT TRONG GIỮ HƯỚNG CỐ ĐỊNH

> **Thêm 08/2026** — phục vụ Module mở rộng Bài 22-24, Tab 3 (con quay hồi
> chuyển) — khung ngoài (gimbal) xoay tự do nhiều lớp, nhưng trục/vật bên
> TRONG phải giữ đúng 1 hướng cố định trong không gian, KHÔNG xoay theo.
>
> Khác PHẦN 2.9 (tịnh tiến quỹ đạo, không xoay gì cả — object không có
> parent xoay) — ở đây object CÓ NHIỀU LỚP PARENT ĐANG XOAY (outerRing →
> middleRing → innerHolder), nên phải "trung hoà" (counter-rotate) lớp
> trong cùng bằng đúng NGHỊCH ĐẢO tích các quaternion của lớp cha, không
> thể chỉ "không làm gì" như PHẦN 2.9.

```javascript
// outerRing xoay quanh Y (do học sinh kéo), middleRing xoay quanh X
// (lớp lồng thứ 2) — innerHolder chứa vật cần giữ hướng cố định
// (mũi tên trục con quay)

function computeInnerHolderQuaternion(outerAngleRad, middleAngleRad) {
  const qOuter = new THREE.Quaternion().setFromEuler(new THREE.Euler(0, outerAngleRad, 0));
  const qMiddle = new THREE.Quaternion().setFromEuler(new THREE.Euler(middleAngleRad, 0, 0));
  // Nghịch đảo tích 2 quaternion cha — áp vào innerHolder để "trung hoà"
  return qOuter.clone().multiply(qMiddle).invert();
}

// Cập nhật mỗi khi học sinh kéo xoay 1 trong 2 khung ngoài:
function onGimbalDrag(outerAngleRad, middleAngleRad) {
  outerRing.rotation.y = outerAngleRad;
  middleRing.rotation.x = middleAngleRad;
  innerHolder.quaternion.copy(
    computeInnerHolderQuaternion(outerAngleRad, middleAngleRad)
  );
  // Kết quả: worldQuaternion của innerHolder = qOuter · qMiddle · (qOuter·qMiddle)⁻¹
  // = Identity — mũi tên trục bên trong LUÔN giữ đúng hướng cục bộ đã đặt
  // ban đầu, bất kể outerRing/middleRing xoay bao nhiêu.
}
```

> **Verify đã thực hiện:** chạy qua 5 tổ hợp góc (outer, middle) khác nhau
> bằng Node (`three` thật qua npm) — hướng thế giới (world direction) của
> mũi tên trục giữ ĐÚNG 1 giá trị duy nhất ở mọi tổ hợp, xác nhận công
> thức đúng. ⚠️ CHƯA verify bằng file HTML thật (chưa test tương tác kéo
> tay thật + hiệu ứng hình ảnh) — prototype trước khi build.

---

## PHẦN 2.11 — OVERLAY 2D ĐỘC LẬP VỚI SCENE 3D (kiểu "màn hình thiết bị")

> **Thêm 08/2026** — phục vụ Bài 24 Module 3 Domain 3 (màn hình radar mô
> phỏng, vòng quét xoay 360° liên tục, chấm sáng báo hiệu khi phát hiện
> máy bay). Đây KHÔNG phải vật thể trong scene Three.js (không có chiều
> sâu, không cần camera 3D) — mà là 1 lớp HTML/CSS hoặc canvas 2D riêng,
> ĐẶT ĐÈ lên khu vực scene 3D, hoạt động ĐỘC LẬP hoàn toàn với vòng lặp
> render Three.js.

```html
<!-- Đặt cùng cấp với canvas Three.js, absolute position đè lên góc màn hình -->
<div id="radar-overlay" style="position:absolute; width:160px; height:160px;
     border-radius:50%; background:var(--ink); overflow:hidden;">
  <div id="radar-sweep"></div> <!-- xoay bằng CSS animation, KHÔNG qua Three.js -->
  <div id="radar-blip" style="display:none;"></div> <!-- chấm sáng, JS toggle hiển thị -->
</div>
```

```css
/* Vòng quét — CSS animation riêng, chu kỳ độc lập với requestAnimationFrame của scene 3D */
#radar-sweep {
  position: absolute; width: 50%; height: 2px; top: 50%; left: 50%;
  background: linear-gradient(90deg, var(--jade), transparent);
  transform-origin: 0 50%;
  animation: radarSweep 2s linear infinite;
}
@keyframes radarSweep { from { transform: rotate(0deg); } to { transform: rotate(360deg); } }
```

```javascript
// Đồng bộ LOGIC (không phải đồng bộ animation-frame) giữa scene 3D và
// overlay 2D: khi vị trí máy bay trong scene 3D đạt 1 mốc đã định (VD
// sau animation bay xong), TOGGLE hiển thị blip — không cần 2 hệ animation
// chạy chung 1 vòng lặp, chỉ cần bắn 1 sự kiện tại đúng thời điểm.
function onFlightAnimationComplete() {
  document.getElementById('radar-blip').style.display = 'block';
  document.getElementById('radar-blip').textContent = 'Khoảng cách: 8,3 km';
}
```

> ⚠️ **Lưu ý cốt lõi:** KHÔNG cố gắng đồng bộ animation-frame-by-frame
> giữa overlay 2D và scene 3D (VD không cần vòng quét radar phải "biết"
> đúng vị trí máy bay trong từng khung hình) — chỉ cần đồng bộ ở các MỐC
> SỰ KIỆN rời rạc (bắt đầu bay, kết thúc bay, phát hiện mục tiêu). Cố
> đồng bộ chi tiết hơn mức cần thiết sẽ làm code phức tạp không cần thiết.

⚠️ **Chưa verify bằng file HTML thật** — đây là kết hợp 2 công nghệ khác
nhau (Three.js scene + CSS animation overlay), về mặt logic đơn giản
nhưng cần test thật để chắc z-index/positioning không bị lệch trên các
kích thước màn hình khác nhau, đặc biệt mobile.

---

## PHẦN 2.12 — DỰNG KINH TUYẾN / VĨ TUYẾN TRÊN HÌNH CẦU (dùng EllipseCurve)

> **Thêm 08/2026** — phục vụ Lab Bài 25, cảnh "Trái Đất & Kinh tuyến"
> (mô phỏng lại + làm rõ hơn Hình 7.57 SGK, xoay 3D tự do). Trái Đất là
> hình CẦU, không có `faces`/`edges` dạng đỉnh rời rạc như SOLID_LIBRARY
> — cần cách dựng đường tròn/nửa đường tròn lớn riêng, dùng
> `THREE.EllipseCurve` (có sẵn trong core Three.js, không cần thêm thư
> viện).

### 2.12.1 Kinh tuyến — nửa đường tròn lớn từ cực Nam đến cực Bắc, tại 1 kinh độ cố định

```javascript
// radius: bán kính mô hình Trái Đất
// longitudeDeg: kinh độ của kinh tuyến cần dựng (0° = kinh tuyến gốc)
function createMeridianLine(radius, longitudeDeg, color, segments = 64) {
  // EllipseCurve quét tự -90° đến 90° (tương đương cực Nam → cực Bắc),
  // 2 bán kính bằng nhau (radius, radius) nên thực chất là ĐƯỜNG TRÒN,
  // không phải ellipse thật — dùng EllipseCurve chỉ vì nó cho phép quét
  // 1 CUNG (startAngle→endAngle) thay vì bắt buộc vẽ cả vòng như
  // CircleGeometry.
  const curve = new THREE.EllipseCurve(
    0, 0, radius, radius,
    -Math.PI / 2, Math.PI / 2, // từ cực Nam đến cực Bắc
    false, 0
  );
  const points2D = curve.getPoints(segments);
  const lambda = longitudeDeg * Math.PI / 180;
  // Điểm 2D (x,y) của EllipseCurve → điểm 3D: x là "bán kính ngang" tại
  // vĩ độ đó (chiếu theo đúng kinh độ lambda), y giữ nguyên làm trục cực
  const points3D = points2D.map(p => new THREE.Vector3(
    p.x * Math.cos(lambda),
    p.y,
    p.x * Math.sin(lambda)
  ));
  const geometry = new THREE.BufferGeometry().setFromPoints(points3D);
  return new THREE.Line(geometry, new THREE.LineBasicMaterial({ color }));
}
```

### 2.12.2 Vĩ tuyến — đường tròn đầy đủ tại 1 vĩ độ cố định (xích đạo là ca đặc biệt vĩ độ = 0°)

```javascript
function createLatitudeCircle(radius, latitudeDeg, color, segments = 64) {
  const phi = latitudeDeg * Math.PI / 180;
  const r = radius * Math.cos(phi); // bán kính đường tròn tại vĩ độ này
                                      // — nhỏ dần khi ra gần 2 cực
  const y = radius * Math.sin(phi); // độ cao dọc trục cực
  const curve = new THREE.EllipseCurve(0, 0, r, r, 0, 2 * Math.PI, false, 0);
  const points2D = curve.getPoints(segments);
  const points3D = points2D.map(p => new THREE.Vector3(p.x, y, p.y));
  const geometry = new THREE.BufferGeometry().setFromPoints(points3D);
  return new THREE.Line(geometry, new THREE.LineBasicMaterial({ color }));
}

// Xích đạo = vĩ tuyến đặc biệt tại latitudeDeg = 0
const equator = createLatitudeCircle(R, 0, 0x3CA57A);
```

### 2.12.3 Cập nhật kinh tuyến động khi kéo slider kinh độ

```javascript
// Kinh tuyến qua P cần đổi lại MỖI KHI slider kinh độ đổi — chi phí
// thấp (chỉ 64 điểm), tạo lại đường mới và thay thế trong scene, KHÔNG
// cần animation phức tạp hay giữ lại geometry cũ để "biến hình"
let kinhTuyenP = null;
function updateKinhTuyenP(longitudeDeg) {
  if (kinhTuyenP) {
    scene.remove(kinhTuyenP);
    kinhTuyenP.geometry.dispose();
    kinhTuyenP.material.dispose();
  }
  kinhTuyenP = createMeridianLine(R, longitudeDeg, 0xE8A24A);
  scene.add(kinhTuyenP);
}
```

> **Verify đã thực hiện (Node, `three` thật qua npm):**
> - Điểm trên kinh tuyến gốc (0°) và kinh tuyến 45°, cùng tại xích đạo →
>   góc đo được giữa 2 điểm = đúng 45,0000° (khớp tuyệt đối).
> - Vĩ tuyến 30°: bán kính thực tế = R·cos(30°), độ cao = R·sin(30°) —
>   cả 2 khớp đúng công thức lý thuyết.
>
> ⚠️ Đã verify công thức bằng Node, **CHƯA verify bằng file HTML thật**
> (chưa test hiển thị/hiệu ứng ánh sáng lên các đường Line mảnh, và chưa
> test tương tác slider thật trên trình duyệt) — prototype nhỏ trước khi
> build chính thức vào Lab.

---

## PHẦN 2.13 — KHỐI NƯỚC ĐẶC TRONG CONTAINER (clipping plane) — bản đã sửa lỗi thật qua prototype

> **Thêm 08/2026, SỬA LẠI 08/2026 sau khi test prototype thật** — bản đầu
> tiên (đã xoá) dùng 1 mặt phẳng mỏng scale theo tiết diện để giả lập mực
> nước — nhìn "giả", không có cảm giác khối đặc. Bản này dùng
> **clipping plane cắt 1 khối đặc thật** (đúng hình dạng container), đã
> qua 3 vòng sửa lỗi thật dựa trên phản hồi hình ảnh trực tiếp — ghi lại
> đầy đủ NGUYÊN NHÂN + CÁCH SỬA để không lặp lại.

### 2.13.1 Nguyên tắc cốt lõi: 1 khối đặc + clipping, KHÔNG dùng mặt phẳng giả lập

```javascript
renderer.localClippingEnabled = true; // BẮT BUỘC set 1 lần khi khởi tạo renderer

// clipPlane: mặt phẳng NẰM NGANG, world space — dùng CHUNG cho cả khối
// container thật (nếu cần) và khối nước (bắt buộc)
const clipPlane = new THREE.Plane(new THREE.Vector3(0, -1, 0), 0);
// clipPlane.constant = fillRatio * H  → cập nhật mỗi khi mực nước đổi

function createWaterBody(bodyGeometry, clipPlane) {
  return new THREE.Mesh(bodyGeometry, new THREE.MeshStandardMaterial({
    color: 0x6fb3dd,              // xanh lam ĐẬM đủ để nổi bật (đã tăng
                                    // từ 0x9ecbe8 quá nhạt ở bản đầu)
    transparent: true, opacity: 0.78,   // đã tăng từ 0.42→0.78 sau khi
                                          // bản đầu "không phân biệt được
                                          // có nước hay không"
    side: THREE.FrontSide,        // ⚠️ XEM 2.13.2 — KHÔNG dùng DoubleSide
    depthWrite: false,            // ⚠️ XEM 2.13.3 — bắt buộc false
    clippingPlanes: [clipPlane]
  }));
}
```

- Với khối **chóp** (đỉnh dưới, miệng mở trên — xem 2.14.1 về hướng dựng
  đúng): dùng LẠI đúng geometry của container (`chopGeom.clone()`),
  clipping sẽ tự cho ra đúng hình frustum thu nhỏ dần — KHÔNG cần
  scale-hack thủ công.
- Với khối **lăng trụ** (tiết diện không đổi): dùng `BoxGeometry`, chỉ
  cần đổi `position.y` theo mực nước, KHÔNG cần đổi scale.

### 2.13.2 ⚠️ LỖI THẬT #1 — DoubleSide làm tường bình trông "xám đục"

**Hiện tượng quan sát được:** dựng container bằng `BoxGeometry` +
material `side: THREE.DoubleSide` (để nhìn được cả từ trong ra ngoài) →
tường bình hiện lên như 1 khối xám đục, không có cảm giác "trong như
kính", và khối nước bên trong gần như không thấy được (phải xoay camera
mới thấy).

**Nguyên nhân:** `DoubleSide` khiến CẢ mặt trước VÀ mặt sau của khối hộp
cùng được vẽ. Với vật liệu trong suốt, 2 lớp mờ (mặt trước + mặt sau)
CỘNG DỒN lại nhìn như 1 lớp đục hơn hẳn — không phải hiệu ứng "kính
trong" như mong đợi.

**Cách sửa:** đổi `side: THREE.DoubleSide` → `side: THREE.FrontSide`
cho MỌI vật liệu container/khối nước dạng khối kín (box, cone kín). Chỉ
dùng `DoubleSide` cho vật thể THỰC SỰ chỉ có 1 lớp mặt phẳng đơn (như mặt
nước gợn sóng dạng `PlaneGeometry`, xem 2.13.4).

### 2.13.3 ⚠️ LỖI THẬT #2 — depthWrite mặc định khiến vật trong suốt vẫn "che" nhau

**Hiện tượng quan sát được:** ngay cả sau khi đổi sang `FrontSide`, có
lúc khối nước bên trong vẫn không hiện ra dù đã đổ nước — phải xoay góc
camera khác mới thấy.

**Nguyên nhân:** `depthWrite` mặc định là `true` cho MỌI vật liệu, kể cả
vật liệu `transparent: true`. Nghĩa là 1 vật trong suốt vẫn GHI LẠI độ
sâu vào depth buffer như vật đặc — nếu tường container (vẽ trước) ghi độ
sâu của nó, khối nước (vẽ sau, ở vị trí xa camera hơn 1 chút) có thể bị
depth-test loại bỏ dù đáng lẽ phải nhìn xuyên qua tường để thấy được.

**Cách sửa:** thêm `depthWrite: false` cho MỌI vật liệu trong suốt xếp
lớp lên nhau (tường container, khối nước, mặt gợn sóng) — chỉ giữ
`depthWrite: true` (mặc định) cho các vật ĐẶC không xuyên thấu (nếu có).

### 2.13.4 renderOrder — đảm bảo thứ tự vẽ đúng, không phụ thuộc thứ tự add vào scene

```javascript
containerMesh.renderOrder = 0;   // tường bình — vẽ TRƯỚC
waterBodyMesh.renderOrder = 1;   // khối nước — vẽ SAU tường
rippleCapMesh.renderOrder = 2;   // mặt gợn sóng (nếu có) — vẽ SAU CÙNG
```

> Three.js không tự sắp xếp thứ tự vẽ giữa các vật trong suốt khác nhau
> theo độ sâu thật — phải set `renderOrder` thủ công khi có nhiều lớp
> trong suốt chồng nhau, nếu không thứ tự vẽ sẽ phụ thuộc thứ tự
> `scene.add()`, dễ cho kết quả không ổn định giữa các lần tải trang.

### 2.13.5 ⚠️ LỖI THẬT #3 — mặt phẳng "cap" gây hình chồng chéo trên container NGHIÊNG/CÓ TIẾT DIỆN ĐỔI

**Hiện tượng quan sát được:** thêm 1 mặt phẳng phẳng (`PlaneGeometry`,
xoay 45° khớp đáy vuông) làm "màng nước" tại miệng khối CHÓP → khi chóp
nghiêng (xem PHẦN 2.14), mặt phẳng này hiện thành hình đa giác xiên chồng
chéo, nhìn rất giả ("ghê" — phản hồi trực tiếp từ giáo viên).

**Nguyên nhân:** mặt cap phẳng đơn giản chỉ đúng hình khi container
KHÔNG nghiêng và có tiết diện không đổi theo chiều cao (như lăng trụ).
Với container CÓ TIẾT DIỆN ĐỔI (chóp) hoặc ĐANG NGHIÊNG, 1 mặt cap đơn
không còn khớp hình dạng miệng thật, gây artefact.

**Cách sửa — quy tắc áp dụng:**
- Container tiết diện KHÔNG đổi, KHÔNG nghiêng (lăng trụ, hộp): dùng mặt
  cap gợn sóng (`PlaneGeometry`, xem 2.13.6) — an toàn, hiệu ứng đẹp.
- Container tiết diện ĐỔI hoặc CÓ NGHIÊNG (chóp, đặc biệt khi có
  animation nghiêng như PHẦN 2.14): **KHÔNG dùng cap riêng** — chỉ dựa
  vào khối nước đặc (2.13.1) với clipping, đơn giản và không bị lỗi hình.

### 2.13.6 Mặt gợn sóng (cap) — CHỈ dùng cho container không nghiêng/tiết diện cố định

```javascript
function createRippleCap(width, depth, segments = 14) {
  const geo = new THREE.PlaneGeometry(width, depth, segments, segments);
  geo.rotateX(-Math.PI / 2);
  const mat = new THREE.MeshStandardMaterial({
    color: 0xbfe0f2, transparent: true, opacity: 0.85,
    side: THREE.DoubleSide, depthWrite: false // Plane đơn — DoubleSide ở
                                                 // đây AN TOÀN (không phải
                                                 // khối kín như 2.13.2)
  });
  return new THREE.Mesh(geo, mat);
}
function updateRipple(mesh, t) {
  const pa = mesh.geometry.attributes.position;
  for (let i = 0; i < pa.count; i++) {
    const x = pa.getX(i), z = pa.getZ(i);
    pa.setY(i, Math.sin(x*0.9 + t*0.0025)*0.05 + Math.sin(z*1.1 + t*0.0018)*0.03);
  }
  pa.needsUpdate = true;
}
```

> **Verify đã thực hiện:** đã chạy qua prototype thật (trình duyệt),
> điều chỉnh 3 vòng dựa trên phản hồi hình ảnh trực tiếp — hiện tại
> (08/2026) đã đạt yêu cầu hiển thị rõ ràng, không cần xoay camera mới
> thấy khối nước, tường bình không còn "xám đục".

---

## PHẦN 2.14 — ANIMATION NGHIÊNG BÌNH ĐỔ NƯỚC (tilt thật + dòng rơi cong xuống) — bản đã sửa lỗi thật

> **Thêm 08/2026, SỬA LẠI 08/2026 sau 2 vòng phản hồi thật** — bản đầu
> dùng dòng hạt nước bay theo cung Bezier NHÔ LÊN giữa 2 container ĐỨNG
> YÊN cách xa nhau — phản hồi: "trông như bắn pháo hoa, phi vật lý". Bản
> này: container NGHIÊNG THẬT + DI CHUYỂN lại gần mục tiêu + dòng nước rơi
> CONG XUỐNG (đúng trọng lực).

### 2.14.1 Dựng container "chóp" đúng hướng — đỉnh DƯỚI, miệng mở TRÊN

```javascript
// ⚠️ QUAN TRỌNG: THREE.ConeGeometry mặc định có ĐỈNH ở TRÊN, ĐÁY TRÒN ở
// DƯỚI — NGƯỢC với 1 cái ly/bình hình chóp thật (đỉnh nhọn dưới, miệng
// mở trên, để đổ nước vào từ trên). Đã verify bằng Node: cần translate +
// rotateX(π) + translate lại để lật đúng hướng.
function buildChopGeometry(circumRadius, H) {
  const geo = new THREE.ConeGeometry(circumRadius, H, 4, 1, true); // openEnded=true — miệng KHÔNG có nắp, mở thật
  geo.translate(0, H/2, 0);
  geo.rotateX(Math.PI);      // LẬT NGƯỢC — đỉnh xuống dưới
  geo.translate(0, H, 0);    // đưa về đúng khoảng [0, H]: đỉnh ở y=0, miệng ở y=H
  geo.rotateY(Math.PI/4);    // xoay 45° để 1 mặt bên hướng thẳng về mục tiêu đổ
  return geo;
}
```

### 2.14.2 Nghiêng quanh 1 điểm PIVOT tuỳ ý (không phải gốc toạ độ) — dùng 2 Group lồng nhau

```javascript
// Muốn xoay quanh 1 điểm KHÔNG phải gốc toạ độ cục bộ (ở đây: mép miệng
// container, phía hướng về mục tiêu đổ) — dùng 2 Group lồng nhau:
const hinge = new THREE.Group();  // đặt ĐÚNG tại vị trí pivot world
const inner = new THREE.Group();  // chứa mesh, offset NGƯỢC lại pivot
hinge.add(inner);
scene.add(hinge);

const pivotLocal = new THREE.Vector3(circumRadius, H, 0); // mép miệng, phía +X
hinge.position.set(CONTAINER_X + pivotLocal.x, pivotLocal.y, pivotLocal.z);
inner.position.set(-pivotLocal.x, -pivotLocal.y, -pivotLocal.z);

// Xoay: chỉ cần đổi hinge.rotation — điểm pivot LUÔN đứng yên (đã verify
// bằng Node ở nhiều góc nghiêng, world position của pivot không đổi).
hinge.rotation.z = -tiltDeg * Math.PI/180;
```

> ⚠️ **Lỗi thật đã gặp:** lần đầu dùng 1 điểm KHÁC (không phải pivot
> chính xác) làm "điểm rót nước", tính qua `matrixWorld` — điểm đó BAY
> LÊN vô lý khi nghiêng (do chọn nhầm điểm). **Cách sửa:** điểm rót nước
> PHẢI CHÍNH LÀ điểm pivot (`hinge.position`) — điểm này đứng yên theo
> định nghĩa của phép xoay, không cần tính lại qua ma trận mỗi frame.

### 2.14.3 Dòng nước rơi CONG XUỐNG (đúng trọng lực) — KHÔNG dùng hạt rời rạc

> ⚠️ **Lỗi thật đã gặp (2 lần):** (1) dùng nhiều "viên nước" hình cầu bay
> rời rạc theo cung Bezier NHÔ LÊN — phản hồi: "trông như bắn pháo hoa,
> vèo vèo, ghê". (2) Sửa thành ellipsoid + tune hướng — vẫn còn cảm giác
> "bắn" vì vẫn là các vật rời rạc riêng lẻ, không phải dòng liên tục.
>
> **Cách sửa cuối cùng:** BỎ HẲN hạt rời rạc — dùng đúng 1 dòng LIÊN TỤC
> (`TubeGeometry` dọc theo cung), và bắt buộc control point cung Bezier
> NẰM DƯỚI đường thẳng nối 2 đầu (võng xuống, đúng trọng lực) — KHÔNG
> NẰM TRÊN (nhô lên, sai vật lý, gây cảm giác "pháo hoa/bắn").

```javascript
function fallingBezierPoint(p0, p2, sagDepth, t) {
  const mid = p0.clone().add(p2).multiplyScalar(0.5);
  mid.y -= sagDepth; // ⚠️ TRỪ, không phải CỘNG — võng XUỐNG dưới trọng lực
  const x=(1-t)*(1-t)*p0.x+2*(1-t)*t*mid.x+t*t*p2.x;
  const y=(1-t)*(1-t)*p0.y+2*(1-t)*t*mid.y+t*t*p2.y;
  const z=(1-t)*(1-t)*p0.z+2*(1-t)*t*mid.z+t*t*p2.z;
  return new THREE.Vector3(x,y,z);
}

// Dòng nước MỌC DẦN từ điểm rót ra tới đích (growFrac 0→1), rồi RÚT NGẮN
// lại khi kết thúc — KHÔNG bật/tắt đột ngột
function updateStreamGeometry(scene, streamMeshRef, p0, p2, sagDepth, growFrac) {
  const segments = 24;
  const pts = [];
  const visibleLen = Math.max(0.02, growFrac);
  for (let i=0;i<=segments;i++) pts.push(fallingBezierPoint(p0, p2, sagDepth, (i/segments)*visibleLen));
  const curve = new THREE.CatmullRomCurve3(pts);
  const geo = new THREE.TubeGeometry(curve, segments, 0.045, 6, false);
  if (streamMeshRef.mesh) { scene.remove(streamMeshRef.mesh); streamMeshRef.mesh.geometry.dispose(); }
  streamMeshRef.mesh = new THREE.Mesh(geo, new THREE.MeshStandardMaterial({
    color: 0x9ecbe8, transparent: true, opacity: 0.75, depthWrite: false
  }));
  scene.add(streamMeshRef.mesh);
}
```

### 2.14.4 ⚠️ LỖI THẬT #4 — quỹ đạo lướt chéo xa (container đứng cố định cách xa mục tiêu)

**Hiện tượng quan sát được:** dù đã sửa cung rơi cong xuống, dòng nước
vẫn "lướt chéo" 1 quãng dài (container đặt cố định cách mục tiêu 6 đơn
vị) — không giống cảm giác rót thật (đưa 2 miệng bình lại gần trước khi
đổ).

**Cách sửa:** container phải DI CHUYỂN lại gần mục tiêu trong lúc
nghiêng (không chỉ xoay tại chỗ) — animate cả `hinge.position` (không
chỉ `hinge.rotation`) theo 3 pha:

```javascript
const originalPivot = new THREE.Vector3(CONTAINER_X + circumRadius, H, 0);
const pourPivot = new THREE.Vector3(TARGET_X - 0.3, H + 1.2, 0); // sát
                                    // miệng mục tiêu — verify Node: tỉ lệ
                                    // ngang/dọc quỹ đạo rơi chỉ ~0,2 (gần
                                    // thẳng đứng), so với ~1,4 nếu để
                                    // container cố định tại chỗ

function runOnePour(t) { // t: 0→1 trong suốt thời gian 1 lần đổ
  if (t < 0.22) {                         // Pha A — nghiêng lên + di chuyển lại gần
    const pt = Ease.easeInOut(t/0.22);
    tiltDeg = lerp(0, TILT_MAX_DEG, pt);
    hinge.position.lerpVectors(originalPivot, pourPivot, pt);
  } else if (t < 0.82) {                  // Pha B — giữ nghiêng + vị trí, rót
    tiltDeg = TILT_MAX_DEG;
    hinge.position.copy(pourPivot);
    // ... giảm fillRatio nguồn, tăng fillRatio đích (xem PHẦN 2.13)
  } else {                                // Pha C — nghiêng về + di chuyển trả lại
    const pt = Ease.easeInOut((t-0.82)/0.18);
    tiltDeg = lerp(TILT_MAX_DEG, 0, pt);
    hinge.position.lerpVectors(pourPivot, originalPivot, pt);
  }
  hinge.rotation.z = -tiltDeg * Math.PI/180;
}
```

> **Đơn giản hoá có chủ đích (ghi nhận rõ, không phải lỗi):** mực nước
> bên trong container khi ĐÃ NGHIÊNG vẫn tính theo hệ toạ độ CỤC BỘ của
> container (không phải mặt nước ngang tuyệt đối theo trọng lực thật) —
> mô phỏng mặt nước ngang thật khi vật nghiêng là bài toán vật lý chất
> lỏng phức tạp hơn nhiều, không cần thiết cho mục đích minh hoạ toán học
> (thể tích, tỉ lệ 1:3), không phải mô phỏng vật lý chính xác.

⚠️ **Đã verify qua prototype HTML thật** (không chỉ Node) — đã sửa qua 4
vòng phản hồi hình ảnh trực tiếp (droplet giả → dòng liên tục; cung nhô
lên → cong xuống; đứng cố định → di chuyển lại gần; DoubleSide xám đục →
FrontSide+depthWrite:false+renderOrder). Khi build cho bài học cụ thể,
vẫn cần đối chiếu lại tỉ lệ hình học đúng bài (bán kính đáy, chiều cao,
khoảng cách 2 khối) — các số trong ví dụ trên chỉ mang tính minh hoạ.

---

## PHẦN 2.15 — KHAI TRIỂN PHẲNG KHỐI CHÓP CỤT ĐỀU (gấp/mở lưới phẳng)

> **Thêm 08/2026** — phục vụ Bài 27 Module 2 Bước 3 (khuôn bánh cô Mai —
> khối chóp cụt đều). Đây là animation "mở bung" 1 khối 3D thành hình
> khai triển phẳng (net) và ngược lại — KHÔNG viết pattern hoàn toàn
> mới, mà TÁI DÙNG 2 kỹ thuật đã có: (1) xoay quanh bản lề (giống PHẦN
> 2.6/2.7) áp đồng thời cho 4 mặt bên, (2) cách tính góc gấp dựa trên
> khoảng cách/toạ độ tương đối (cùng tinh thần "Đo góc nhị diện" ở Lab
> Bài 25).

### 2.15.1 Nguyên lý: mỗi mặt bên là 1 "cánh" (flap) tự xoay quanh cạnh đáy nhỏ

```javascript
// Đáy nhỏ (a') CỐ ĐỊNH tại y=0, không tham gia khai triển.
// Mỗi mặt bên (hình thang cân) đặt trong 1 Group riêng ("flap"), pivot
// tại 1 điểm TRÊN cạnh đáy nhỏ tương ứng — xoay quanh CHÍNH cạnh đó.
//
// Toạ độ LOCAL của mỗi flap được định nghĩa ở TRẠNG THÁI TRẢI PHẲNG
// (rotation = 0) — animation chỉ cần đổi 1 giá trị rotation duy nhất
// mỗi flap, không cần tính lại vertex mỗi frame.

const foldedAngleRad = Math.atan2(h, (a-ap)/2); // góc gấp — GIỐNG NHAU
                          // cho cả 4 mặt vì khối chóp cụt ĐỀU (đối xứng)
const slantLen = Math.sqrt(((a-ap)/2)**2 + h**2); // cạnh bên — khoảng
                          // cách từ bản lề tới điểm ngoài, KHÔNG ĐỔI khi
                          // xoay (đặc trưng của phép xoay cứng)
```

### 2.15.2 Dựng 1 "cánh" — ví dụ mặt hướng +X (bản lề dọc trục Z)

```javascript
function buildFlap(hingeAxis, hingeSign) {
  // hingeAxis: 'x' | 'z' — trục mà CẠNH BẢN LỀ chạy dọc theo (do đáy
  //   hình vuông, chỉ có 2 hướng cạnh: dọc x hoặc dọc z)
  // hingeSign: +1 | -1 — bản lề ở phía nào của trục kia
  const hinge = new THREE.Group();
  if (hingeAxis === 'z') hinge.position.set(hingeSign * halfAp, 0, 0);
  else hinge.position.set(0, 0, hingeSign * halfAp);
  scene.add(hinge);

  // Toạ độ LOCAL ở trạng thái TRẢI PHẲNG (rotation=0): 2 điểm bản lề +
  // 2 điểm ngoài (cách bản lề đúng slantLen, nằm trong mặt y=0)
  let pos;
  if (hingeAxis === 'z') {
    pos = new Float32Array([
      0,0,-halfAp,  0,0,halfAp,  hingeSign*slantLen,0,halfA,
      0,0,-halfAp,  hingeSign*slantLen,0,halfA,  hingeSign*slantLen,0,-halfA,
    ]);
  } else {
    pos = new Float32Array([
      -halfAp,0,0,  halfAp,0,0,  halfA,0,hingeSign*slantLen,
      -halfAp,0,0,  halfA,0,hingeSign*slantLen,  -halfA,0,hingeSign*slantLen,
    ]);
  }
  const geo = new THREE.BufferGeometry();
  geo.setAttribute('position', new THREE.BufferAttribute(pos, 3));
  geo.computeVertexNormals();
  hinge.add(new THREE.Mesh(geo, new THREE.MeshStandardMaterial({ color: 0xe8d9a0, side: THREE.DoubleSide })));

  return { hinge, axis: hingeAxis, hingeSign };
}

const flaps = [
  buildFlap('z', +1), buildFlap('z', -1), // mặt +X, -X
  buildFlap('x', +1), buildFlap('x', -1), // mặt +Z, -Z
];
```

### 2.15.3 ⚠️ LỖI THẬT — sai dấu góc xoay khiến mặt gập XUỐNG thay vì LÊN

**Hiện tượng phát hiện được (qua verify bằng Node, KHÔNG chờ tới khi
build xong mới thấy):** dùng 1 công thức dấu cố định `rotation.z =
-angle` cho MỌI mặt trục `z` → tại trạng thái gấp hoàn toàn (progress=0,
đáng lẽ phải khớp đúng hình chóp cụt thật), toạ độ Y của điểm ngoài ra
**−8** thay vì **+8** — mặt gập lộn xuống dưới sàn, sai hoàn toàn.

**Nguyên nhân:** chiều xoay dương/âm của `rotation.z` và `rotation.x`
trong Three.js phụ thuộc hướng bản lề đang xét (`hingeSign`) theo quy tắc
KHÁC NHAU giữa 2 trục — không thể dùng 1 dấu cố định cho cả 4 mặt.

**Cách sửa (đã verify đúng bằng Node ở cả 4 mặt, progress 0/0,5/1):**

```javascript
function updateUnfold(flaps, progress, foldedAngleRad) {
  const angle = (1 - progress) * foldedAngleRad; // progress=0→gấp hết,
                                                     // progress=1→trải phẳng
  flaps.forEach(f => {
    // ⚠️ QUY TẮC DẤU BẮT BUỘC — khác nhau giữa 2 trục:
    const rotSign = (f.axis === 'z') ? f.hingeSign : -f.hingeSign;
    if (f.axis === 'z') f.hinge.rotation.z = rotSign * angle;
    else f.hinge.rotation.x = rotSign * angle;
  });
}
```

> **Verify đã thực hiện (Node, `three` thật qua npm):** với khuôn bánh
> a=18, a'=10, h=8 — góc gấp = 63,435°, cạnh bên (slantLen) = 8,944. Tại
> progress=0, cả 4 điểm ngoài đều đúng y=+8, toạ độ (x,z) khớp đúng hình
> chóp cụt thật ((9,8,9), (−9,8,9), (9,8,9), (9,8,−9) theo từng mặt). Tại
> progress=1, cả 4 điểm về đúng y=0, xoè ra 4 hướng, cách bản lề đúng
> 8,944 — khớp lý thuyết.

⚠️ **Đã verify qua prototype HTML thật** (không chỉ Node) — có slider
kéo tay + nút tự động gấp/mở lặp lại, chạy qua bài kiểm tra thực thi mô
phỏng DOM (không chỉ soát cú pháp) — không phát sinh lỗi runtime. Khi
build cho bài học cụ thể khác (kích thước khác), CHỈ cần đổi `a, ap, h`
— công thức `foldedAngleRad`/`slantLen`/quy tắc dấu giữ nguyên.

> 💡 **Đây vẫn là phần TUỲ CHỌN** (theo đúng ghi chú gốc ở kịch bản Bài
> 27 Module 2 Bước 3) — có thể bỏ nếu đội build thấy độ khó không tương
> xứng giá trị sư phạm, dù giờ đã có sẵn code tham khảo đầy đủ, verify kỹ.

---

## PHẦN 3 — LABEL: HTML OVERLAY vs SPRITE 3D

> Đã test cả 2 cách trực tiếp. Kết luận: **dùng HTML overlay làm chuẩn**
> cho tên điểm và số đo (chữ Việt có dấu sắc nét, dễ style theo design
> system, dễ đổi text động). Chỉ dùng Sprite khi cần occlusion thật
> (label phải bị che đúng khi nằm sau 1 mặt đặc, ví dụ bên trong hình chóp).

### 3.1 Bảng so sánh (từ kết quả test thật)

| | HTML overlay | Sprite 3D |
|---|---|---|
| Độ sắc nét chữ | Cao ở mọi mức zoom | Cần tăng độ phân giải canvas texture, vẫn hơi mờ khi zoom gần |
| Chữ Việt có dấu | Tốt (font hệ thống) | Phải vẽ lại texture, dễ lỗi font nếu canvas font không hỗ trợ dấu |
| Occlusion (bị che bởi vật cản) | Không tự có — phải tự xử lý hoặc bỏ qua | Có sẵn, miễn phí (depth test thật của WebGL) |
| Đổi text động (số đo góc, khoảng cách) | Rẻ — chỉ set `textContent` | Tốn — phải dựng lại texture mỗi lần đổi |
| Đồng bộ vị trí | Phải tự gọi `project()` mỗi frame | Tự động theo `position` trong scene |

### 3.2 HTML overlay — code đã verify

```css
/* Container chứa toàn bộ label, đè lên canvas */
#label-layer {
  position: absolute; top: 0; left: 0; width: 100%; height: 100%;
  pointer-events: none; overflow: hidden;
}
.pt-label {
  position: absolute; top: 0; left: 0;
  font-size: 14px; font-weight: 700; color: #fff;
  text-shadow: 0 1px 3px rgba(0,0,0,0.8), 0 0 8px rgba(0,0,0,0.5);
  white-space: nowrap;
  will-change: transform; /* dùng transform, KHÔNG dùng left/top, để
                              tránh browser tính lại layout mỗi frame */
}
```

```javascript
// Tạo 1 lần khi khởi tạo điểm
this.htmlLabel = document.createElement('div');
this.htmlLabel.className = 'pt-label';
this.htmlLabel.textContent = label;
this.htmlLabel.style.color = `#${color.toString(16).padStart(6, '0')}`;
document.getElementById('label-layer').appendChild(this.htmlLabel);

// Gọi mỗi frame trong render loop — HÀM CỐT LÕI để đồng bộ HTML lên vị trí 3D
syncHtmlLabel() {
  const labelWorldPos = this.mesh.position.clone().add(new THREE.Vector3(0, 0.22, 0));
  const screenPos = labelWorldPos.project(camera); // 3D world -> NDC [-1, 1]

  const rect = renderer.domElement.getBoundingClientRect();
  const x = (screenPos.x * 0.5 + 0.5) * rect.width;
  const y = (-screenPos.y * 0.5 + 0.5) * rect.height; // Y bị đảo (NDC ngược với DOM)

  // screenPos.z > 1 nghĩa là điểm đang ở SAU camera — PHẢI ẩn label,
  // nếu không label "dính ngược" lên màn hình khi xoay quá xa (lỗi rất khó debug
  // vì trông như label bị kẹt, không liên quan gì đến code label).
  const isBehindCamera = screenPos.z > 1;
  this.htmlLabel.style.display = isBehindCamera ? 'none' : 'block';
  this.htmlLabel.style.transform = `translate(${x}px, ${y}px) translate(-50%, -150%)`;
}
```

### 3.3 Sprite 3D — code đã verify (dùng khi cần occlusion thật)

```javascript
makeTextSprite(text, color) {
  const canvas = document.createElement('canvas');
  const size = 128; // độ phân giải cao để chữ không răng cưa khi zoom
  canvas.width = size; canvas.height = size;
  const ctx = canvas.getContext('2d');
  ctx.fillStyle = '#ffffff';
  ctx.font = 'bold 64px sans-serif';
  ctx.textAlign = 'center';
  ctx.textBaseline = 'middle';
  ctx.shadowColor = 'rgba(0,0,0,0.8)';
  ctx.shadowBlur = 8;
  ctx.fillText(text, size / 2, size / 2);

  const texture = new THREE.CanvasTexture(canvas);
  const material = new THREE.SpriteMaterial({ map: texture, depthTest: true, sizeAttenuation: false });
  const sprite = new THREE.Sprite(material);
  sprite.scale.set(0.08, 0.08, 1); // sizeAttenuation=false -> scale cố định theo màn hình
  return sprite;
}
// Cập nhật vị trí mỗi frame: sprite.position.copy(mesh.position).add(offset)
// KHÔNG cần project() hay xử lý occlusion tay — WebGL tự depth-test.
```

### 3.4 Label số đo động (khoảng cách, góc) — giữa 2 điểm

```javascript
function updateDistanceLabel(pointA, pointB, labelEl) {
  const dist = pointA.position.distanceTo(pointB.position);
  const midpoint = new THREE.Vector3().addVectors(pointA.position, pointB.position).multiplyScalar(0.5);
  const screenPos = midpoint.clone().project(camera);

  const rect = renderer.domElement.getBoundingClientRect();
  const x = (screenPos.x * 0.5 + 0.5) * rect.width;
  const y = (-screenPos.y * 0.5 + 0.5) * rect.height;

  labelEl.style.display = screenPos.z > 1 ? 'none' : 'block';
  labelEl.style.transform = `translate(${x}px, ${y}px) translate(-50%, -50%)`;
  labelEl.textContent = `AB = ${dist.toFixed(2)}`; // chỉ set textContent — rẻ, không dựng lại gì
}
```

---

## PHẦN 4 — DỰNG MẶT PHẲNG TỪ 3 ĐIỂM (real-time theo drag)

> Ví dụ áp dụng trực tiếp: tiên đề SGK "1 mặt phẳng qua 3 điểm không
> thẳng hàng". Phần này minh hoạ cách TÁCH lớp Computation (toán thuần,
> chỉ nhận/trả `Vector3`) khỏi lớp Rendering — nguyên tắc áp dụng cho
> mọi hàm hình học khác (giao tuyến, khoảng cách, góc — xem `06_geometry_math.md`).

```javascript
function buildPlaneFromPoints(p1, p2, p3, size = 6) {
  const v1 = new THREE.Vector3().subVectors(p2, p1);
  const v2 = new THREE.Vector3().subVectors(p3, p1);
  const normal = new THREE.Vector3().crossVectors(v1, v2).normalize();

  // 3 điểm gần thẳng hàng -> normal suy biến ~ (0,0,0) -> không vẽ được mặt phẳng.
  // BẮT BUỘC kiểm tra, nếu không PlaneGeometry.lookAt() sẽ lỗi hướng ngẫu nhiên.
  if (normal.lengthSq() < 1e-6) return null;

  const centroid = new THREE.Vector3().addVectors(p1, p2).add(p3).divideScalar(3);

  const geometry = new THREE.PlaneGeometry(size, size);
  const material = new THREE.MeshStandardMaterial({
    color: 0x7F77DD, transparent: true, opacity: 0.35,
    side: THREE.DoubleSide, depthWrite: false // depthWrite:false để mặt phẳng
                                                // trong suốt không che lẫn nhau sai thứ tự
  });
  const mesh = new THREE.Mesh(geometry, material);
  mesh.position.copy(centroid);
  mesh.lookAt(centroid.clone().add(normal));
  return mesh;
}

// Gọi lại mỗi khi 1 trong 3 điểm bị kéo — dispose() mesh cũ trước khi
// tạo mới để tránh memory leak khi kéo liên tục nhiều phút.
function updatePlane(planeMesh, pointA, pointB, pointC) {
  if (planeMesh) {
    scene.remove(planeMesh);
    planeMesh.geometry.dispose();
    planeMesh.material.dispose();
  }
  return buildPlaneFromPoints(pointA.position, pointB.position, pointC.position);
}
```

---

## PHẦN 4.5 — KÉO ĐẦU MÚT ĐỂ BIẾN ĐỔI ĐƯỜNG THẲNG

> Khác với PHẦN 1 (kéo 1 điểm độc lập), đây là kéo 1 ĐẦU MÚT thuộc về
> 1 đường thẳng có nhãn/màu/hit-area riêng — kéo xong phải dựng lại
> TOÀN BỘ mesh phụ thuộc (line vẽ thật, hit-cylinder, glow-tube), không
> chỉ di chuyển 1 điểm đơn lẻ.

### 4.5.1 Cấu trúc: SelectableLine có 2 endpoint handle

```javascript
class SelectableLine {
  constructor(p1, p2, color, label) {
    this.p1 = p1.clone();
    this.p2 = p2.clone();
    // ... line, hitMesh (cylinder), glowMesh dựng như PHẦN "click-to-select" ...

    // 2 ĐẦU MÚT KÉO ĐƯỢC — tách biệt khỏi hitMesh của thân đường
    this.endpointStart = this.makeEndpointHandle(this.p1, 'start');
    this.endpointEnd = this.makeEndpointHandle(this.p2, 'end');
  }

  makeEndpointHandle(pos, which) {
    const geometry = new THREE.SphereGeometry(0.07, 16, 16);
    const material = new THREE.MeshStandardMaterial({ color: this.color, emissive: this.color, emissiveIntensity: 0.2 });
    const mesh = new THREE.Mesh(geometry, material);
    mesh.position.copy(pos);
    scene.add(mesh);

    const hitGeo = new THREE.SphereGeometry(0.24, 8, 8);
    const hitMat = new THREE.MeshBasicMaterial({ visible: false });
    const hitMesh = new THREE.Mesh(hitGeo, hitMat);
    hitMesh.position.copy(pos);
    hitMesh.userData.endpointOf = this;
    hitMesh.userData.which = which; // 'start' hoặc 'end' — biết kéo đầu nào
    scene.add(hitMesh);

    return { mesh, hitMesh };
  }

  // BẮT BUỘC gọi mỗi khi p1/p2 đổi — dispose mesh cũ, dựng lại MỌI mesh
  // phụ thuộc (không chỉ di chuyển position, vì hit-cylinder và glow-tube
  // có HƯỚNG và ĐỘ DÀI phụ thuộc p1/p2, không thể chỉ .position.copy()).
  rebuildGeometry() {
    this.line.geometry.dispose();
    this.line.geometry = new THREE.BufferGeometry().setFromPoints([this.p1, this.p2]);

    scene.remove(this.hitMesh);
    this.hitMesh.geometry.dispose();
    this.hitMesh = this.makeHitCylinder(); // dựng lại cylinder mới đúng hướng/độ dài
    this.hitMesh.userData.selectable = this;
    scene.add(this.hitMesh);

    scene.remove(this.glowMesh);
    this.glowMesh.geometry.dispose();
    this.glowMesh.material.dispose();
    this.glowMesh = this.makeGlowTube();
    this.glowMesh.visible = this.selected;
    scene.add(this.glowMesh);

    this.endpointStart.mesh.position.copy(this.p1);
    this.endpointStart.hitMesh.position.copy(this.p1);
    this.endpointEnd.mesh.position.copy(this.p2);
    this.endpointEnd.hitMesh.position.copy(this.p2);
  }

  setEndpoint(which, newPos) {
    if (which === 'start') this.p1.copy(newPos);
    else this.p2.copy(newPos);
    this.rebuildGeometry();
  }
}
```

### 4.5.2 Drag handler — dùng lại billboard-plane từ PHẦN 1

```javascript
let draggingEndpoint = null; // { line: SelectableLine, which: 'start'|'end' }
let dragPlaneEndpoint = null;

renderer.domElement.addEventListener('pointerdown', (event) => {
  updateMouseNDC(event);
  raycaster.setFromCamera(mouseNDC, camera);
  const allEndpointHitMeshes = allLines.flatMap(l => [l.endpointStart.hitMesh, l.endpointEnd.hitMesh]);
  const hits = raycaster.intersectObjects(allEndpointHitMeshes);
  if (hits.length === 0) return;

  const hitMesh = hits[0].object;
  draggingEndpoint = { line: hitMesh.userData.endpointOf, which: hitMesh.userData.which };

  const currentPos = draggingEndpoint.which === 'start' ? draggingEndpoint.line.p1 : draggingEndpoint.line.p2;
  const camDir = new THREE.Vector3();
  camera.getWorldDirection(camDir);
  dragPlaneEndpoint = new THREE.Plane().setFromNormalAndCoplanarPoint(camDir, currentPos);
  orbitControls.enabled = false;
});

renderer.domElement.addEventListener('pointermove', (event) => {
  if (!draggingEndpoint) return;
  updateMouseNDC(event);
  raycaster.setFromCamera(mouseNDC, camera);
  const intersection = new THREE.Vector3();
  if (raycaster.ray.intersectPlane(dragPlaneEndpoint, intersection)) {
    draggingEndpoint.line.setEndpoint(draggingEndpoint.which, intersection); // tự rebuildGeometry()
  }
});

renderer.domElement.addEventListener('pointerup', () => {
  draggingEndpoint = null;
  dragPlaneEndpoint = null;
  orbitControls.enabled = true;
});
```

> **Xung đột với click-to-select:** nếu cùng 1 file vừa có "kéo đầu mút"
> vừa có "click chọn thân đường" (PHẦN 4.7), PHẢI giới hạn thời điểm
> cho phép kéo (ví dụ chỉ ở bước "chưa chọn gì" của state machine).
> Nếu không, click vào thân đường để chọn dễ vô tình trúng đầu mút và
> kéo lệch đường ngoài ý muốn.

---

## PHẦN 4.6 — MẶT PHẲNG PHỤ TRỢ GIỮA 2 ĐƯỜNG CẮT NHAU

> Dùng khi cần MINH HOẠ trực quan rằng 2 đường thẳng đồng phẳng (ví dụ
> sau khi dựng `d₂'` song song với `d₂` qua điểm O trên `d₁`, `d₁` và
> `d₂'` cắt nhau tại O nên luôn tạo ra đúng 1 mặt phẳng). Khác PHẦN 4
> (mặt phẳng từ 3 điểm), ở đây input là 1 điểm chung + 2 vector chỉ phương.

```javascript
// CHỈ vẽ mặt phẳng chứa CHÍNH 2 đường liên quan trực tiếp đến kết quả
// cần minh hoạ (ví dụ góc vừa đo) — KHÔNG vẽ thêm mặt phẳng phụ khác
// (ví dụ mặt phẳng chứa cặp song song gốc) nếu không cần, để tránh
// cảnh rậm rạp làm học sinh khó tập trung vào đúng phần đang học.
function buildPlaneFromIntersectingLines(O, dir1, dir2, sizeHint) {
  const normal = new THREE.Vector3().crossVectors(dir1, dir2).normalize();

  // 2 đường song song (góc 0°) -> không tạo mặt phẳng xác định -> không vẽ
  if (normal.lengthSq() < 1e-6) return null;

  const geometry = new THREE.PlaneGeometry(sizeHint, sizeHint);
  const material = new THREE.MeshStandardMaterial({
    color: 0xFAC775, transparent: true, opacity: 0.18, // opacity thấp hơn
    side: THREE.DoubleSide, depthWrite: false           // mặt phẳng chính (PHẦN 4)
  });                                                     // vì đây chỉ là phụ trợ
  const mesh = new THREE.Mesh(geometry, material);
  mesh.position.copy(O);
  mesh.lookAt(O.clone().add(normal));
  return mesh;
}
```

---

## PHẦN 4.7 — ẨN/HIỆN ĐỐI TƯỢNG (CÓ LỌC RAYCAST)

> Lỗi hay gặp nhất khi làm tính năng ẩn/hiện: chỉ set `mesh.visible = false`
> cho phần NHÌN THẤY mà quên `hitMesh.visible = false` cho phần BẮT CHUỘT.
> Hậu quả: học sinh click vào khoảng KHÔNG GIAN TRỐNG (vì đường đã ẩn)
> nhưng vẫn "chọn được" đường đó — rất khó debug vì không có gì để nhìn,
> chỉ thấy hành vi vô lý.

### 4.7.1 setVisible() phải ẩn TOÀN BỘ mesh phụ thuộc cùng lúc

```javascript
class SelectableLine {
  // ...
  get isVisible() { return this.line.visible; }

  setVisible(visible) {
    this.line.visible = visible;        // phần NHÌN THẤY
    this.hitMesh.visible = visible;     // phần BẮT CHUỘT — dễ quên nhất
    this.glowMesh.visible = visible && this.selected;
    this.endpointStart.mesh.visible = visible;
    this.endpointStart.hitMesh.visible = visible;
    this.endpointEnd.mesh.visible = visible;
    this.endpointEnd.hitMesh.visible = visible;
    this.htmlLabel.style.display = visible ? 'block' : 'none';
  }
}
```

### 4.7.2 PHẢI lọc theo trạng thái hiện TRƯỚC mọi raycast

```javascript
// Helper dùng chung — MỌI nơi raycast (click-to-select, kéo đầu mút,
// hover cursor) phải lọc qua hàm này trước khi đưa vào intersectObjects().
function visibleLines() {
  return allLines.filter(l => l.isVisible);
}

// Sai: raycaster.intersectObjects(allLines.map(l => l.hitMesh))
// Đúng:
const hits = raycaster.intersectObjects(visibleLines().map(l => l.hitMesh));
```

### 4.7.3 syncLabel() phải tôn trọng trạng thái ẩn

```javascript
syncLabel() {
  // BẮT BUỘC return sớm nếu đang ẩn — nếu không, đoạn code set
  // display dựa vào screenPos.z (occlusion theo camera) ở dưới sẽ
  // GHI ĐÈ display:none mà setVisible() vừa đặt, làm label "tự hiện
  // lại" một cách khó hiểu mỗi frame.
  if (!this.line.visible) return;

  const screenPos = this.midpoint.clone().project(camera);
  // ... phần còn lại tính toán + set display như PHẦN 3.2 ...
}
```

> **Trạng thái ẩn/hiện độc lập với mọi state machine khác** (ví dụ quy
> trình chọn-dựng-đo ở PHẦN 4.8) — không tự động hiện lại khi reset
> 1 quy trình khác. Học sinh ẩn 1 đường để dọn hình, làm lại bài tập
> mới thì đường đó vẫn nên giữ ẩn cho đến khi họ tự bấm hiện lại.

---

## PHẦN 4.8 — STATE MACHINE NHIỀU BƯỚC (chọn → dựng → đo)

> Khi 1 bài cần đúng thứ tự các bước (ví dụ SGK: chọn `d₁` → chọn `d₂`
> → chọn điểm O → dựng đường song song qua O → đo góc tại O), không
> nên xử lý bằng nhiều cờ boolean rời rạc — dễ rơi vào trạng thái mâu
> thuẫn (vừa "đã chọn d1" vừa "chưa chọn gì" do quên đồng bộ 1 cờ).
> Dùng 1 object `flow` với field `step` (số nguyên) làm nguồn sự thật
> duy nhất, mọi nhánh xử lý rẽ theo đúng `flow.step` hiện tại.

```javascript
let flow = {
  step: 1,             // số nguyên — NGUỒN SỰ THẬT DUY NHẤT của tiến trình
  lineD1: null,
  lineD2: null,
  pointO: null,         // ConstrainedPoint trên lineD1 (xem PHẦN 2)
  parallelLine: null    // THREE.Line dựng động bằng animation
};

renderer.domElement.addEventListener('pointerdown', (event) => {
  // ... raycast ...
  if (flow.step === 1) {
    // chỉ xử lý chọn d1, ngó lơ mọi click khác
  } else if (flow.step === 2) {
    // chỉ xử lý chọn d2, loại d1 ra khỏi candidate để không tự chọn lại
  } else if (flow.step === 3) {
    // chỉ xử lý chọn/kéo điểm O
  }
  // flow.step luôn TĂNG DẦN qua mỗi bước hợp lệ, không bao giờ giảm
  // trừ khi resetFlow() được gọi tường minh (nút "Làm lại từ đầu")
});

function resetFlow() {
  // Dọn dẹp mesh động (dispose geometry/material trước khi remove),
  // rồi gán lại flow = { step: 1, ...null hết }.
  // KHÔNG động vào trạng thái ẩn/hiện (PHẦN 4.7) hay vị trí p1/p2 đã
  // kéo (PHẦN 4.5) — reset chỉ xoá TIẾN TRÌNH LOGIC, không xoá HÌNH.
}
```

### Animation dựng hình theo bước (không xuất hiện ngay)

```javascript
// requestAnimationFrame timeline — KHÔNG dùng CSS animation vì đây là
// BufferGeometry 3D thật, không phải DOM. Vẽ dần từ điểm gốc ra 2 đầu,
// dùng easing để có cảm giác "chốt" rõ ràng lúc kết thúc.
function animateBuildParallelLine(originPoint, targetStart, targetEnd, onComplete) {
  const geometry = new THREE.BufferGeometry().setFromPoints([originPoint.clone(), originPoint.clone()]);
  const line = new THREE.Line(geometry, new THREE.LineBasicMaterial({ color: 0xFAC775 }));
  scene.add(line);

  const duration = 900; // ms — đủ chậm để thấy quá trình, không quá lâu gây sốt ruột
  const startTime = performance.now();

  function step() {
    const progress = Math.min(1, (performance.now() - startTime) / duration);
    const eased = 1 - Math.pow(1 - progress, 3); // ease-out cubic

    const currentStart = new THREE.Vector3().lerpVectors(originPoint, targetStart, eased);
    const currentEnd = new THREE.Vector3().lerpVectors(originPoint, targetEnd, eased);
    line.geometry.setFromPoints([currentStart, currentEnd]);

    if (progress < 1) requestAnimationFrame(step);
    else onComplete();
  }
  requestAnimationFrame(step);
}
```

---

## PHẦN 4.9 — NHẬP TOẠ ĐỘ SỐ (đáp ứng bài tập SGK cho sẵn A, B, C)

> Bài tập SGK thường cho sẵn toạ độ cụ thể (ví dụ A(1,2,3), B(0,1,-2)).
> Kéo bằng mắt không đủ chính xác cho trường hợp này — cần panel nhập
> số, đồng bộ 2 CHIỀU với việc kéo chuột.

### Thiết kế 2 chiều

```
- Kéo chuột -> số tự đổ vào ô input (để học sinh thấy số khi tự khám phá)
- Nhập số + bấm "Áp dụng" -> điểm nhảy NGAY tới vị trí đó, KHÔNG animation
  (khác PHẦN 4.8 — animation dùng khi cần THẤY QUÁ TRÌNH dựng hình; ở đây
  học sinh chỉ cần ĐÚNG SỐ ngay, nhập sai sửa lại tức khắc)
```

```javascript
// Đổ giá trị hiện tại vào input — gọi mỗi khi kéo chuột xong (trong
// updateHUD(), không gọi mỗi frame của animate() vì lãng phí và không
// cần thiết — chỉ cần đồng bộ SAU một thay đổi vị trí thật).
function syncInputsFromPoints() {
  coordInputs.A.x.value = pointA.position.x.toFixed(2);
  coordInputs.A.y.value = pointA.position.y.toFixed(2);
  coordInputs.A.z.value = pointA.position.z.toFixed(2);
  // ... lặp lại cho B, C ...
}

// Đọc số từ input -> validate kỹ -> gán thẳng vào vị trí (không animation)
function applyCoordsFromInputs() {
  const parsed = {};
  for (const label of ['A', 'B', 'C']) {
    const x = parseFloat(coordInputs[label].x.value);
    const y = parseFloat(coordInputs[label].y.value);
    const z = parseFloat(coordInputs[label].z.value);

    // BẮT BUỘC validate từng ô — để trống/gõ chữ -> NaN -> phải báo lỗi
    // RÕ RÀNG, không để mặt phẳng "biến mất" âm thầm không lý do.
    if (Number.isNaN(x) || Number.isNaN(y) || Number.isNaN(z)) {
      coordErrorEl.textContent = `Toạ độ điểm ${label} chưa hợp lệ — cần nhập đủ 3 số.`;
      return; // dừng NGAY, không áp dụng phần nào nếu có 1 điểm lỗi
    }
    parsed[label] = new THREE.Vector3(x, y, z);
  }

  // Kiểm tra 3 điểm thẳng hàng TRƯỚC khi gán — đây là tình huống sư
  // phạm quan trọng (SGK: "3 điểm thẳng hàng không xác định mặt phẳng"),
  // nên báo RÕ LÝ DO thay vì để mặt phẳng tự nhiên không hiện ra.
  const v1 = new THREE.Vector3().subVectors(parsed.B, parsed.A);
  const v2 = new THREE.Vector3().subVectors(parsed.C, parsed.A);
  if (new THREE.Vector3().crossVectors(v1, v2).lengthSq() < 1e-6) {
    coordErrorEl.textContent = 'Cảnh báo: 3 điểm đang thẳng hàng — không tạo được mặt phẳng xác định.';
  } else {
    coordErrorEl.textContent = '';
  }

  pointA.mesh.position.copy(parsed.A);
  pointB.mesh.position.copy(parsed.B);
  pointC.mesh.position.copy(parsed.C);
  updatePlane();
  updateHUD(); // gọi lại syncInputsFromPoints() để chuẩn hoá hiển thị số (ví dụ "2" -> "2.00")
}

// Cho phép Enter để áp dụng — tiện khi nhập nhiều bài liên tiếp,
// không cần click chuột ra nút mỗi lần.
document.querySelectorAll('#coord-input-panel input').forEach(input => {
  input.addEventListener('keydown', (e) => {
    if (e.key === 'Enter') applyCoordsFromInputs();
  });
});
```

---

## PHẦN 4.10 — KHOẢNG CÁCH ĐIỂM ĐẾN MẶT PHẲNG (chiếu vuông góc)

> SGK định nghĩa khoảng cách từ M đến mặt phẳng (P) bằng đoạn MH vuông
> góc, H là chân đường vuông góc thuộc (P) — KHÔNG phải 1 con số trừu
> tượng. Học sinh phải THẤY đoạn MH thật và xác nhận nó vuông góc, không
> chỉ đọc kết quả số (cùng nguyên tắc với PHẦN 4.8 — góc giữa 2 đường
> phải thấy phép dựng, không nhảy thẳng tới số).

### 4.10.1 Biểu diễn mặt phẳng cho TÍNH TOÁN (khác với biểu diễn để VẼ)

```javascript
// Mặt phẳng cho mục đích TÍNH TOÁN chỉ cần normal + 1 điểm bất kỳ trên
// mặt phẳng — khác với buildPlaneFromPoints() (PHẦN 4) cần thêm centroid +
// kích thước để VẼ. Tách riêng 2 hàm này: 1 cho Computation (thuần,
// không Three.Mesh), 1 cho Rendering — đúng nguyên tắc PHẦN 4.
function definePlaneFromPoints(p1, p2, p3) {
  const v1 = new THREE.Vector3().subVectors(p2, p1);
  const v2 = new THREE.Vector3().subVectors(p3, p1);
  const normal = new THREE.Vector3().crossVectors(v1, v2);
  if (normal.lengthSq() < 1e-6) return null; // 3 điểm thẳng hàng
  normal.normalize();
  return { normal, pointOnPlane: p1.clone() };
}
```

### 4.10.2 Công thức chiếu vuông góc — HÀM TOÁN CỐT LÕI

```javascript
// H = chân đường vuông góc từ M xuống mặt phẳng (normal, pointOnPlane)
// distance = độ dài MH = khoảng cách cần tìm
//
// NGUYÊN LÝ: "khoảng cách có dấu" = (M - pointOnPlane) · normal cho biết
// M lệch khỏi mặt phẳng bao nhiêu THEO HƯỚNG NORMAL (dấu + hoặc - tuỳ
// M nằm phía nào). Lùi M lại đúng đoạn đó theo hướng normal sẽ ra H —
// đây chính là phép chiếu trực giao (orthogonal projection) cơ bản nhất
// của hình học giải tích, áp dụng được cho mọi bài toán "chiếu lên mặt
// phẳng" khác (ví dụ chiếu 1 đường thẳng lên mặt phẳng).
function projectPointOntoPlane(M, plane) {
  const toPoint = new THREE.Vector3().subVectors(M, plane.pointOnPlane);
  const signedDist = toPoint.dot(plane.normal);
  const H = M.clone().sub(plane.normal.clone().multiplyScalar(signedDist));
  return { H, distance: Math.abs(signedDist), signedDist };
}
```

> **Trường hợp biên PHẢI kiểm tra:** nếu A, B, C gần thẳng hàng,
> `definePlaneFromPoints()` trả về `null` — toàn bộ chuỗi tính toán
> phía sau (chiếu, vẽ MH, hiện số) phải kiểm tra `null` này và báo rõ
> "chưa xác định mặt phẳng" trong HUD, không để âm thầm lỗi hoặc hiện
> số sai (ví dụ NaN hoặc khoảng cách = 0 giả).

### 4.10.3 Vẽ đoạn MH bằng NÉT ĐỨT — quy ước SGK cho đường phụ trợ

```javascript
// Nét đứt = đường DỰNG THÊM để giải (khác cạnh hình thật vẽ nét liền).
// LƯU Ý KỸ THUẬT: BẮT BUỘC gọi computeLineDistances() sau khi tạo Line
// với LineDashedMaterial — nếu quên, Three.js sẽ vẽ NHƯ NÉT LIỀN dù
// material đã set dashSize/gapSize đúng. Đây là lỗi rất dễ bỏ qua vì
// không có cảnh báo console, chỉ âm thầm vẽ sai.
function buildMHSegment(M, H) {
  const geometry = new THREE.BufferGeometry().setFromPoints([M, H]);
  const material = new THREE.LineDashedMaterial({ color: 0xFAC775, dashSize: 0.12, gapSize: 0.08, linewidth: 2 });
  const line = new THREE.Line(geometry, material);
  line.computeLineDistances(); // BẮT BUỘC — thiếu dòng này nét đứt sẽ thành nét liền
  return line;
}
```

### 4.10.4 Dấu góc vuông tại H — xác nhận trực quan MH ⊥ (P)

```javascript
// Dấu góc vuông (hình chữ L nhỏ) đúng quy ước vẽ tay SGK: 1 cạnh nằm
// TRONG mặt phẳng, cạnh kia dọc theo hướng MH. KHÔNG chỉ vẽ đoạn MH
// rồi hiện số — phải có dấu này để học sinh xác nhận bằng mắt rằng
// đoạn vừa dựng THẬT SỰ vuông góc, không phải đoạn nối tuỳ ý.
function buildRightAngleMark(H, normal, M) {
  const size = 0.28;
  // Lấy 1 vector bất kỳ TRONG mặt phẳng (vuông góc với normal) làm cạnh ngang.
  // Mẹo chọn arbitrary vector: nếu normal gần trục Y thì dùng trục X làm
  // "vector bất kỳ", ngược lại dùng trục Y — tránh trường hợp suy biến khi
  // normal song song với vector tham chiếu (cross product sẽ ra ~0).
  const arbitrary = Math.abs(normal.y) < 0.9 ? new THREE.Vector3(0, 1, 0) : new THREE.Vector3(1, 0, 0);
  const inPlaneDir = new THREE.Vector3().crossVectors(normal, arbitrary).normalize();
  const upDir = new THREE.Vector3().subVectors(M, H).normalize(); // hướng dọc theo MH

  const p0 = H.clone().add(inPlaneDir.clone().multiplyScalar(size));
  const p1 = p0.clone().add(upDir.clone().multiplyScalar(size));
  const p2 = H.clone().add(upDir.clone().multiplyScalar(size));

  const geo = new THREE.BufferGeometry().setFromPoints([p0, p1, p2]);
  return new THREE.Line(geo, new THREE.LineBasicMaterial({ color: 0xFAC775, linewidth: 2 }));
}
```

### 4.10.5 Gom toàn bộ luồng cập nhật vào 1 hàm `refreshAll()`

```javascript
// Khi 1 điểm bất kỳ (A, B, C, hoặc M) đổi vị trí — do kéo chuột HOẶC
// nhập số (PHẦN 4.9) — phải chạy lại TOÀN BỘ chuỗi: dựng lại mặt
// phẳng, tính lại H + distance, vẽ lại MH + dấu góc vuông, cập nhật
// HUD. Gom thành 1 hàm refreshAll() để mọi nơi gây thay đổi (drag
// handler, nút Áp dụng toạ độ) chỉ cần gọi đúng 1 hàm này, tránh quên
// đồng bộ 1 bước nào đó khi code phát triển thêm.
let lastResult = null;
function refreshAll() {
  updatePlaneMesh();
  lastResult = updatePerpendicularSegment(); // dựng lại MH + dấu góc vuông, trả {H, distance}
  updateHUD(lastResult ? lastResult.distance : null);
}
```

---

## PHẦN 5 — RENDER LOOP CHUẨN

```javascript
function animate() {
  requestAnimationFrame(animate);
  orbitControls.update();          // bắt buộc khi enableDamping = true
  points.forEach(p => p.syncRing()); // đồng bộ ring + hitMesh + label mỗi frame
  renderer.render(scene, camera);
}
animate();
```

---

## PHẦN 6 — KHI NÀO DÙNG THREE.JS, KHI NÀO DÙNG CANVAS 2D

```
Dùng Three.js (file này) khi:
  - Học sinh cần XOAY vật thể tự do để nhìn nhiều góc (OrbitControls)
  - Bài có khái niệm thật sự 3 chiều: mặt phẳng, giao tuyến, góc nhị diện,
    khoảng cách trong không gian — những thứ không vẽ đúng bằng phối cảnh giả 2D
  - Kéo điểm/đường có ràng buộc không gian (trên cạnh, trên mặt)

Dùng Canvas 2D (xem 03_game_engine.md) khi:
  - Chỉ cần nhìn từ góc cố định, không cần xoay
  - Bài thuộc các môn/chủ đề khác: vật lý phẳng, đồ thị hàm số, mặt phẳng nghiêng
  - File HTML đơn, học sinh dùng thiết bị cũ (Three.js nặng hơn ~600KB)

KHÔNG trộn 2 hệ thống input trong cùng 1 file — hit-detection 2D
(point-to-segment trên mx,my) và raycasting 3D (Vector3 + Plane) là
2 mô hình toán khác nhau, copy nhầm công thức từ file kia sẽ sai hoàn toàn.
```

---

## PHẦN 4.11 — CHIẾU ĐƯỜNG THẲNG LÊN MẶT PHẲNG (hình chiếu a')

> Ứng dụng trực tiếp từ `projectPointOntoPlane` (PHẦN 4.10.2): chiếu từng
> đầu mút riêng, nối lại → hình chiếu a'. Khi a // (α), hình chiếu a' nằm
> trong (α) và song song với a — cần vẽ kéo dài ra 2 phía để học sinh thấy
> rõ a' là đường thẳng, không phải đoạn con (dùng `buildExtendedLine`).

```javascript
// Trả { projStart, projEnd } — 2 chân chiếu của 2 đầu mút lên mặt phẳng
function projectLineOntoPlane(lineStart, lineEnd, plane) {
  const { H: projStart } = projectPointOntoPlane(lineStart, plane);
  const { H: projEnd }   = projectPointOntoPlane(lineEnd, plane);
  return { projStart, projEnd };
}

// Vẽ đường kéo dài ra 2 phía — dùng cho hình chiếu a' để rõ là đường thẳng
function buildExtendedLine(p1, p2, color, ext = 1.5) {
  const dir = new THREE.Vector3().subVectors(p2, p1).normalize();
  const start = p1.clone().sub(dir.clone().multiplyScalar(ext));
  const end   = p2.clone().add(dir.clone().multiplyScalar(ext));
  const geo = new THREE.BufferGeometry().setFromPoints([start, end]);
  const line = new THREE.Line(geo, new THREE.LineBasicMaterial({ color }));
  scene.add(line);
  return line;
}
```

> **Gotcha:** Nếu a nằm TRONG mặt phẳng (`contained`), `projStart === lineStart`
> và `projEnd === lineEnd` — hình chiếu trùng với đường gốc. Phải kiểm tra
> `classifyLineToPlane` trước để tránh vẽ đường chiếu trùng khít gây nhầm lẫn.

---

## PHẦN 4.12 — PHÂN LOẠI QUAN HỆ ĐƯỜNG THẲNG – MẶT PHẲNG

> Ba quan hệ có thể xảy ra: song song / cắt / nằm trong. Phân biệt dựa vào
> 2 bước: (1) dot product hướng đường với normal, (2) nếu song song hướng thì
> kiểm tra tiếp điểm có thuộc mặt phẳng không.

```javascript
// Trả 'parallel' | 'intersects' | 'contained'
// lineDir phải là vector ĐÃ normalize — nếu chưa normalize, ngưỡng 1e-4 sẽ sai
function classifyLineToPlane(lineStart, lineDir, plane) {
  const dot = Math.abs(lineDir.dot(plane.normal));

  // dot ≈ 1: đường gần vuông góc mp → chắc chắn cắt
  // dot > 1e-4: đường có thành phần theo normal → cắt mp
  if (dot > 1e-4) return 'intersects';

  // dot ≈ 0: đường song song với mp (hướng nằm trong mp)
  // → kiểm tra tiếp: điểm trên đường có thuộc mp không?
  const distPt = Math.abs(
    new THREE.Vector3().subVectors(lineStart, plane.pointOnPlane).dot(plane.normal)
  );
  return distPt < 1e-4 ? 'contained' : 'parallel';
}
```

> **Quan trọng:** `contained` ≠ `parallel`. Cả 2 đều có `dot(dir, normal) ≈ 0`
> nhưng `contained` thêm điều kiện điểm trên đường thuộc mặt phẳng. Nếu chỉ
> kiểm tra dot product mà không kiểm tra tiếp, sẽ báo nhầm `parallel` cho
> đường nằm trong mặt phẳng — khoảng cách thật = 0 nhưng báo có khoảng cách.

---

## PHẦN 4.13 — QUAN HỆ 2 MẶT PHẲNG + GIAO TUYẾN

> Hai mặt phẳng hoặc song song (normal cùng hướng) hoặc cắt nhau (sinh ra
> giao tuyến). Pattern này dùng cho B2 (2 mp song song) và bất kỳ bài nào
> cần tìm giao tuyến theo quy trình SGK.

### 4.13.1 Phân loại + khoảng cách 2 mặt phẳng song song

```javascript
// Trả 'parallel' | 'intersects'
// plane1.normal và plane2.normal phải đã normalize (definePlaneFromPoints đảm bảo điều này)
function classifyTwoPlanes(plane1, plane2) {
  const cross = new THREE.Vector3().crossVectors(plane1.normal, plane2.normal);
  // cross ≈ (0,0,0) khi 2 normal cùng hướng (song song hoặc trùng nhau)
  return cross.lengthSq() < 1e-6 ? 'parallel' : 'intersects';
}

// Khoảng cách giữa 2 mặt phẳng song song
// Chiếu vecto nối 2 điểm bất kỳ trên 2 mp lên normal — đây là khoảng cách vuông góc
function distanceBetweenParallelPlanes(plane1, plane2) {
  return Math.abs(
    new THREE.Vector3()
      .subVectors(plane2.pointOnPlane, plane1.pointOnPlane)
      .dot(plane1.normal)
  );
}
```

### 4.13.2 Giao tuyến 2 mặt phẳng cắt nhau

> ⚠️ **ĐÃ SỬA LỖI (07/2026):** bản trước dùng `denom = n1n2² - 1`, SAI
> DẤU — xem cảnh báo đầy đủ + cách verify ở `06_geometry_math.md` PHẦN
> A.6 (nguồn chuẩn duy nhất của hàm này) và `01_scenario_builder_3d_
> addendum.md` PHỤ LỤC E.11. Bản dưới đã sửa.

```javascript
// Trả { point, dir } — 1 điểm trên giao tuyến + hướng giao tuyến
// Trả null nếu 2 mp song song
//
// NGUYÊN LÝ: giao tuyến có hướng = cross(n1, n2). Tìm 1 điểm trên giao tuyến
// bằng cách giải hệ n1·P = d1, n2·P = d2 với ràng buộc P ⊥ dir (cross product).
// Công thức rút gọn (chỉ đúng khi n1, n2 đã normalize — n·n = 1):
function intersectionOfTwoPlanes(plane1, plane2) {
  const dir = new THREE.Vector3().crossVectors(plane1.normal, plane2.normal);
  if (dir.lengthSq() < 1e-6) return null; // song song
  dir.normalize();

  const n1 = plane1.normal, n2 = plane2.normal;
  const d1 = n1.dot(plane1.pointOnPlane);
  const d2 = n2.dot(plane2.pointOnPlane);
  const n1n2 = n1.dot(n2);
  // denom = định thức hệ Cramer [[1,k],[k,1]] = 1 - k² (k = n1·n2, vì n·n=1
  // sau normalize) — ĐÃ SỬA, bản cũ viết ngược dấu thành "k²-1"
  const denom = 1 - n1n2 * n1n2;
  if (Math.abs(denom) < 1e-8) return null; // phòng thủ thêm

  const c1 = (d1 - d2 * n1n2) / denom;
  const c2 = (d2 - d1 * n1n2) / denom;
  const point = new THREE.Vector3()
    .addScaledVector(n1, c1)
    .addScaledVector(n2, c2);
  return { point, dir };
}

// Vẽ giao tuyến kéo dài ra 2 phía từ điểm gốc
function buildIntersectionLine(intersect, ext = 5, color = 0x34d399) {
  const lp1 = intersect.point.clone().sub(intersect.dir.clone().multiplyScalar(ext));
  const lp2 = intersect.point.clone().add(intersect.dir.clone().multiplyScalar(ext));
  const geo = new THREE.BufferGeometry().setFromPoints([lp1, lp2]);
  const line = new THREE.Line(geo, new THREE.LineBasicMaterial({ color }));
  scene.add(line);
  return line;
}
```

> **CRITICAL:** `intersectionOfTwoPlanes` giả định `plane.normal` đã normalize
> (`n·n = 1`). `definePlaneFromPoints` (PHẦN 4.10.1) đảm bảo điều này. Nếu
> truyền vào normal thô từ `crossVectors()` chưa normalize, `denom` sẽ tính
> sai và `point` trả về hoàn toàn lệch — không có cảnh báo runtime, chỉ thấy
> giao tuyến vẽ sai vị trí. **Lưu ý:** đây là gotcha KHÁC với lỗi sai dấu đã
> sửa ở trên — thiếu normalize vẫn sai dù công thức đúng; công thức sai dấu
> thì sai LUÔN CẢ KHI đã normalize đúng. Verify bằng cách kiểm tra
> `(point - plane1.pointOnPlane)·plane1.normal ≈ 0` với CẢ 2 mặt phẳng sau
> khi gọi hàm — nếu không ≈ 0, một trong 2 nguyên nhân trên đang xảy ra.

---

## PHẦN 4.14 — XOAY ĐƯỜNG THẲNG GIỮ SONG SONG + HỆ THỐNG VẾT

> Pattern sư phạm: xoay đường a quanh trục vuông góc với (α) → hướng đường
> thay đổi nhưng khoảng cách đến (α) không đổi. Kết hợp "chụp vết" hình
> chiếu cho học sinh thấy nhiều đường a' song song nhau trong (α).

### 4.14.1 Xoay đường quanh trục normal(α) qua điểm M

```javascript
// Xoay 2 đầu mút pP, pQ quanh trục (normal của mp, đi qua pivotM)
// → đường a thay đổi hướng nhưng LUÔN giữ khoảng cách đến mp
// angleDeg: góc tuyệt đối tính từ vị trí gốc (KHÔNG phải delta)
//
// THIẾT KẾ: slider trả về góc tuyệt đối, hàm này xoay từ baseP/baseQ
// (lưu trước khi bắt đầu xoay). Không xoay delta từng bước — tránh
// drift tích luỹ sau nhiều lần gọi.
function rotateLineAroundNormal(pP, pQ, pivotM, normal, angleDeg) {
  const axis = normal.clone().normalize();
  const quat = new THREE.Quaternion().setFromAxisAngle(axis, angleDeg * Math.PI / 180);
  const newP = pP.clone().sub(pivotM).applyQuaternion(quat).add(pivotM);
  const newQ = pQ.clone().sub(pivotM).applyQuaternion(quat).add(pivotM);
  return { newP, newQ };
}

// Áp dụng vào slider — cập nhật vị trí P và Q, rồi gọi refreshAll()
// baseP/baseQ là vị trí TRƯỚC khi bắt đầu dùng slider (lưu 1 lần)
function applyRotation(angleDeg) {
  const { newP, newQ } = rotateLineAroundNormal(
    baseP, baseQ, ptM.position, currentPlane.normal, angleDeg
  );
  ptP.mesh.position.copy(newP);
  ptQ.mesh.position.copy(newQ);
  refreshAll();
}
```

> **Lưu ý khi kéo tay P/Q sau khi đã xoay:** sau khi học sinh kéo tay điểm
> P hoặc Q, `baseP`/`baseQ` cần được reset về vị trí hiện tại và slider về
> 0° — nếu không, lần slider kéo tiếp theo sẽ "nhảy" về vị trí cũ trước
> khi xoay. Gọi `resetRotationBase()` trong `pointerup` handler khi kéo điểm.

### 4.14.2 Hệ thống vết hình chiếu (tối đa 3 vết)

```javascript
// Màu + opacity cho 3 vết — đậm → mờ dần để phân biệt thứ tự
const TRAIL_COLORS   = [0x34d399, 0xfb923c, 0xe879f9]; // xanh ngọc, cam, hồng tím
const TRAIL_OPACITIES = [0.85,    0.6,      0.4];

// Chụp 1 vết: lưu hình chiếu a' hiện tại với màu riêng
// Gọi khi học sinh bấm nút "Chụp vết" — KHÔNG tự động
function captureTrail(trails, ptP, ptQ, plane) {
  if (trails.length >= 3) return; // tối đa 3 vết
  const idx   = trails.length;
  const color   = TRAIL_COLORS[idx];
  const opacity = TRAIL_OPACITIES[idx];

  const resP = projectPointOntoPlane(ptP.position, plane);
  const resQ = projectPointOntoPlane(ptQ.position, plane);
  const { projStart, projEnd } = projectLineOntoPlane(ptP.position, ptQ.position, plane);

  // Đường chiếu a' kéo dài, màu riêng, transparent
  const dir = new THREE.Vector3().subVectors(projEnd, projStart).normalize();
  const ext = 1.8;
  const s = projStart.clone().sub(dir.clone().multiplyScalar(ext));
  const e = projEnd.clone().add(dir.clone().multiplyScalar(ext));
  const geo = new THREE.BufferGeometry().setFromPoints([s, e]);
  const line = new THREE.Line(geo,
    new THREE.LineBasicMaterial({ color, transparent: true, opacity })
  );
  scene.add(line);

  // Nét đứt mờ từ P/Q xuống chiếu — opacity thấp hơn đường chiếu
  const dashP = buildDashedLine(ptP.position.clone(), resP.H, color);
  dashP.material.opacity = opacity * 0.7; dashP.material.transparent = true;
  const dashQ = buildDashedLine(ptQ.position.clone(), resQ.H, color);
  dashQ.material.opacity = opacity * 0.7; dashQ.material.transparent = true;

  trails.push({ line, dashP, dashQ, projStart: s, projEnd: e,
                color, angle: currentAngleDeg }); // lưu góc tại thời điểm chụp
}

// Xoá toàn bộ vết — dispose mesh, xoá label
function clearTrails(trails) {
  trails.forEach(t => {
    [t.line, t.dashP, t.dashQ].forEach(m => {
      scene.remove(m); m.geometry.dispose(); m.material.dispose();
    });
    if (t.label) t.label.remove();
  });
  trails.length = 0; // xoá in-place để giữ reference
}

// Sync label vết mỗi frame trong animate() — camera có thể xoay
// Gọi trong render loop: trails.forEach((t, i) => syncTrailLabel(t, i))
function syncTrailLabel(trail, idx) {
  syncMidLabel(trail.label, trail.projStart, trail.projEnd,
    `a'${idx + 1} (${trail.angle.toFixed(0)}°)`);
}
```

> **Tại sao "Chụp vết" thủ công, không tự động?** Nếu lưu vết mỗi frame
> hoặc mỗi khi slider thay đổi, vết sẽ dày đặc và che nhau. Để học sinh
> chủ động: xoay đến góc muốn → quan sát → bấm chụp → xoay tiếp.
> Tối đa 3 vết giúp canvas không rậm rạp, vừa đủ để thấy nhiều a'
> song song nhau trong (α).

---

## PHẦN 4.15 — GÓC GIỮA ĐƯỜNG THẲNG VÀ MẶT PHẲNG

> SGK định nghĩa: góc φ giữa đường a và mặt phẳng (α) = góc giữa a và hình
> chiếu a' của a lên (α). Đo tại chân chiếu của 1 đầu mút. Không phải góc
> giữa a và normal (góc bù 90° mới là φ).
> Trường hợp đặc biệt: a ⊥ (α) → φ = 90°; a // (α) → φ = 0°.

```javascript
// lineDir phải normalize trước khi truyền vào
// Trả degrees [0°, 90°]
function angleLineToPlane(lineDir, planeNormal) {
  // sin(φ) = |cos(góc giữa lineDir và normal)| = |lineDir · normal|
  // vì φ = 90° - (góc giữa đường và normal)
  const sinPhi = Math.abs(lineDir.clone().normalize().dot(planeNormal.clone().normalize()));
  return Math.asin(Math.min(1, sinPhi)) * 180 / Math.PI;
}
```

> **Vẽ cung góc φ:** dùng `buildArc(origin, dir1, dir2, radius, color)` (PHẦN 4.16)
> với origin = chân chiếu Q', dir1 = hướng đường a từ Q' về P, dir2 = hướng
> hình chiếu a' từ Q'. Cung nằm trong mặt phẳng chứa a và a'.

---

## PHẦN 4.16 — VẼ CUNG GÓC (buildArc)

> Dùng cho cả góc đường–mặt phẳng (C1), góc nhị diện (C2), và bất kỳ
> bài nào cần minh hoạ góc bằng cung thay vì chỉ hiện số.

```javascript
// Vẽ cung từ dir1 đến dir2 tại origin, bán kính radius
// Tự tính góc giữa dir1 và dir2 — không cần truyền vào
// Trả null nếu 2 vector trùng nhau (góc = 0)
function buildArc(origin, dir1, dir2, radius, color, segments) {
  segments = segments || 24;
  const cosA = Math.max(-1, Math.min(1, dir1.dot(dir2)));
  const totalAngle = Math.acos(cosA);
  if (totalAngle < 1e-4) return null;

  // Hệ toạ độ local: u dọc dir1, v vuông góc dir1 trong mặt phẳng dir1-dir2
  const u = dir1.clone().normalize();
  const vRaw = dir2.clone().sub(u.clone().multiplyScalar(dir2.dot(u)));
  if (vRaw.lengthSq() < 1e-8) return null;
  const v = vRaw.normalize();

  const points = [];
  for (let i = 0; i <= segments; i++) {
    const t = (i / segments) * totalAngle;
    points.push(origin.clone()
      .add(u.clone().multiplyScalar(Math.cos(t) * radius))
      .add(v.clone().multiplyScalar(Math.sin(t) * radius)));
  }
  const geo = new THREE.BufferGeometry().setFromPoints(points);
  const arc = new THREE.Line(geo, new THREE.LineBasicMaterial({ color }));
  scene.add(arc);
  return arc;
}
```

> **Gotcha:** dir1 và dir2 phải là vector đơn vị (**normalize trước**) và phải
> nằm trong cùng mặt phẳng của cung cần vẽ. Nếu truyền nhầm hướng ngược
> (ví dụ hướng từ Q về P thay vì P về Q), cung sẽ vẽ phía đối diện.
> Kiểm tra bằng cách nhìn cung có nằm trong góc cần đo không.

---

## PHẦN 4.17 — GÓC NHỊ DIỆN GIỮA 2 MẶT PHẲNG

> SGK định nghĩa: lấy O bất kỳ trên giao tuyến l, dựng Ox ⊥ l trong α,
> Oy ⊥ l trong β. Góc nhị diện = góc xOy. Kết quả không phụ thuộc vị trí O.

```javascript
// Tính góc nhị diện + trả 2 vector tia Ox, Oy để vẽ
// intersect = { point, dir } từ intersectionOfTwoPlanes() (PHẦN 4.13)
function dihedralAngle(plane1, plane2, intersect) {
  // Ox: trong α, vuông góc với giao tuyến l
  const ox = new THREE.Vector3()
    .crossVectors(intersect.dir, plane1.normal).normalize();
  // Oy: trong β, vuông góc với l
  const oy = new THREE.Vector3()
    .crossVectors(intersect.dir, plane2.normal).normalize();

  const cosTheta = Math.max(-1, Math.min(1, ox.dot(oy)));
  const angleDeg = Math.acos(cosTheta) * 180 / Math.PI;
  return { angleDeg, ox, oy };
}

// Tìm điểm O "đẹp" trên giao tuyến — chiếu gốc toạ độ lên giao tuyến
function findOOnIntersectLine(intersect) {
  const t = new THREE.Vector3()
    .subVectors(new THREE.Vector3(0,0,0), intersect.point)
    .dot(intersect.dir);
  return intersect.point.clone().add(intersect.dir.clone().multiplyScalar(t));
}
```

> **Lưu ý chiều ox/oy:** `crossVectors(dir, normal)` cho ra vector trong mặt
> phẳng vuông góc với giao tuyến, nhưng chiều có thể lộn (chỉ vào trong hay
> ra ngoài mp). Kiểm tra `ox.dot(plane1.normal)` — nếu âm thì negate ox để
> đảm bảo tia nằm đúng phía "trên" mặt phẳng. Tương tự với oy.

---

## PHẦN 4.18 — KHOẢNG CÁCH ĐIỂM ĐẾN ĐƯỜNG THẲNG

> Khác PHẦN 4.10 (chiếu lên mặt phẳng) — đây là chiếu lên **đường thẳng**.
> Tham số t không bị clamp — H có thể nằm ngoài đoạn PQ (vì đường thẳng
> vô hạn), không phải ConstrainedPoint trên đoạn.

```javascript
// Trả { H, distance, t } — H là chân đường vuông góc từ M đến đường thẳng
// linePoint: 1 điểm bất kỳ trên đường; lineDir: hướng đường (chưa cần normalize)
// t: tham số vị trí H trên đường (t < 0 hoặc t > 1 nghĩa là H ngoài đoạn PQ)
function projectPointOntoLine(M, linePoint, lineDir) {
  const d = lineDir.clone().normalize();
  const t = new THREE.Vector3().subVectors(M, linePoint).dot(d);
  const H = linePoint.clone().add(d.clone().multiplyScalar(t));
  return { H, distance: M.distanceTo(H), t };
}
```

> **Dấu góc vuông tại H:** dùng `buildRightAngleMark(H, lineDir, HM_dir, size)`
> với `lineDir` là hướng đường a (refDir "ngang") và `HM_dir` là hướng từ H
> lên M (upDir "đứng"). Khác PHẦN 4.10.4 — ở đó refDir là vector trong mặt
> phẳng, ở đây refDir là hướng đường thẳng.

---

## PHẦN 4.19 — KHOẢNG CÁCH 2 ĐƯỜNG CHÉO NHAU

> Pattern khó nhất nhóm D. Công thức: d = |(P₂ − P₁) · n̂| với n = d₁ × d₂.
> Đồng thời tìm H₁ ∈ d₁, H₂ ∈ d₂ để vẽ đoạn vuông góc chung.

```javascript
// Trả { dist, H1, H2, cross } hoặc null nếu 2 đường không chéo nhau
// P1, P2: điểm bất kỳ trên mỗi đường; dir1, dir2: hướng (chưa cần normalize)
function distanceSkewLines(P1, dir1, P2, dir2) {
  const d1 = dir1.clone().normalize();
  const d2 = dir2.clone().normalize();
  const cross = new THREE.Vector3().crossVectors(d1, d2);
  const crossLen = cross.length();

  // crossLen ≈ 0: 2 đường song song hoặc cắt nhau → không áp dụng
  if (crossLen < 1e-6) return null;

  const w = new THREE.Vector3().subVectors(P2, P1);

  // Khoảng cách: chiếu w lên hướng vuông góc chung
  const dist = Math.abs(w.dot(cross)) / crossLen;

  // Tìm H1, H2: giải hệ từ điều kiện (H2 - H1) ⊥ d1 và (H2 - H1) ⊥ d2
  // Đặt b = d1·d2, e = w·d1, f = w·d2
  // → t1 = (e - b*f) / (1 - b²),  t2 = -(f - b*e) / (1 - b²)
  const b = d1.dot(d2);
  const denom = 1 - b * b; // = sin²(θ) — luôn > 0 vì 2 đường không song song
  const t1 =  (w.dot(d1) - b * w.dot(d2)) / denom;
  const t2 = -(w.dot(d2) - b * w.dot(d1)) / denom;

  const H1 = P1.clone().add(d1.clone().multiplyScalar(t1));
  const H2 = P2.clone().add(d2.clone().multiplyScalar(t2));

  return { dist, H1, H2, cross: cross.normalize() };
}
```

> **Verify kết quả:** sau khi tính H1, H2, kiểm tra:
> - `(H2-H1).dot(d1) ≈ 0` — H1H2 ⊥ d1 ✓
> - `(H2-H1).dot(d2) ≈ 0` — H1H2 ⊥ d2 ✓
> - `H1H2.length() ≈ dist` ✓
>
> **Phân biệt "chéo nhau" vs "song song" vs "cắt nhau":**
> - `crossLen < 1e-6` → song song hoặc cắt nhau (cả 2 đều return null)
> - Để phân biệt tiếp: nếu song song thì `dist > 0`, nếu cắt thì `dist ≈ 0`
> - Trong thực tế simulation, return null và hiện thông báo "không áp dụng"
>   là đủ — không cần phân biệt song song vs cắt nhau ở bước này.

---

## PHẦN 4.20 — OCCLUSION TỰ ĐỘNG (cạnh bị khối che → tự động vẽ nét đứt)

> Khác `buildDashedGuideLine` (nếu có trong PHẦN 4.x khác — đường phụ vẽ
> SẴN là nét đứt để phân biệt với đường chính) — ở đây trạng thái nét
> liền/nét đứt của MỖI CẠNH ĐƯỢC TÍNH LẠI MỖI FRAME dựa trên góc camera
> hiện tại, mô phỏng đúng quy ước vẽ hình không gian trên giấy (cạnh nhìn
> thấy = nét liền, cạnh bị khối che = nét đứt). Đây là biến thể PHẠM VI
> HẸP của "X-Ray" (từng đánh dấu ❌ chưa có pattern trong PHỤ LỤC A,
> `01_scenario_builder_3d_addendum.md`) — X-Ray đầy đủ còn cần ẩn/hiện
> TOÀN BỘ mặt ngoài + click chọn cạnh bên trong có glow đúng/sai, phạm vi
> rộng hơn nhiều so với chỉ "tô nét liền/nét đứt" ở đây.

> **Màu sắc khi build thật:** `04_design_toan_3d.md` đã định nghĩa sẵn 2
> màu riêng biệt cho việc này — `COLOR_EDGE_SOLID = 0xe6edf3` (trắng sáng,
> cạnh nhìn thấy) và `COLOR_EDGE_HIDDEN = 0x444d56` (xám tối, opacity 0.5,
> cạnh bị khuất). Prototype ở đây dùng chung 1 màu cho cả 2 trạng thái để
> tập trung verify đúng LOGIC occlusion trước — khi build simulation thật,
> dùng đúng 2 màu đã định nghĩa sẵn, không lặp lại 1 màu.

### 4.20.1 Nguyên lý — raycast từ camera tới trung điểm cạnh

```
Bắn 1 tia từ camera tới TRUNG ĐIỂM của cạnh cần kiểm tra. Nếu tia này
va chạm với khối đặc (solidMesh) TRƯỚC KHI tới trung điểm — tức có 1
mặt khác của khối đang "chắn" giữa camera và cạnh — thì cạnh coi như bị
che, vẽ nét đứt. Nếu tia đi thẳng không bị chặn, cạnh nhìn thấy được,
vẽ nét liền.

GOTCHA đã lường trước: trung điểm 1 cạnh của khối LUÔN nằm TRÊN bề mặt
khối (cạnh là giao của 2 mặt) — raycast từ chính điểm đó ra sẽ luôn "tự
va" vào bề mặt chứa nó (khoảng cách ~0, do sai số dấu phẩy động). Phải
OFFSET nhẹ điểm test về phía camera trước khi bắn tia, và giới hạn
raycaster.far đúng bằng khoảng cách tới điểm test (trừ epsilon nhỏ) —
nếu không, va chạm với chính mặt chứa cạnh đó sẽ luôn bị tính nhầm là
"bị che bởi mặt khác".
```

```javascript
function isEdgeOccluded(p1, p2, camera, solidMesh) {
  const midpoint = new THREE.Vector3().addVectors(p1, p2).multiplyScalar(0.5);

  // Offset nhẹ về phía camera — tránh raycaster tự va vào chính bề mặt
  // chứa midpoint do sai số dấu phẩy động
  const toCam = new THREE.Vector3().subVectors(camera.position, midpoint).normalize();
  const testPoint = midpoint.clone().add(toCam.clone().multiplyScalar(0.01));

  const rayDir = new THREE.Vector3().subVectors(camera.position, testPoint).normalize();
  const distToCam = testPoint.distanceTo(camera.position);

  // far = khoảng cách tới camera trừ epsilon — nếu có va chạm nào TRƯỚC
  // camera trong khoảng này, đó chính là mặt khác đang chắn cạnh
  const ray = new THREE.Raycaster(testPoint, rayDir, 0, distToCam - 0.02);
  const hits = ray.intersectObject(solidMesh);

  return hits.length > 0; // true = bị che → nét đứt
}
```

### 4.20.2 Áp dụng cho toàn bộ 8 (hoặc N) cạnh — tính lại mỗi frame

```javascript
// Mỗi cạnh giữ 2 phiên bản mesh: nét liền (solid) và nét đứt (dashed),
// toggle visible qua lại tuỳ kết quả occlusion. KHÔNG dùng 1 mesh đổi
// material vì LineDashedMaterial cần computeLineDistances() ngay sau
// khi TẠO geometry — đổi material sau không tự động tính lại (xem gotcha
// "nét đứt hiện như nét liền" trong PHỤ LỤC lỗi thường gặp cuối file).
function buildEdgePair(p1, p2, color) {
  const geoSolid = new THREE.BufferGeometry().setFromPoints([p1, p2]);
  const lineSolid = new THREE.Line(geoSolid, new THREE.LineBasicMaterial({ color, linewidth: 2 }));
  scene.add(lineSolid);

  const geoDashed = new THREE.BufferGeometry().setFromPoints([p1, p2]);
  const lineDashed = new THREE.Line(geoDashed, new THREE.LineDashedMaterial({ color, dashSize: 0.12, gapSize: 0.08 }));
  lineDashed.computeLineDistances(); // BẮT BUỘC — không có cảnh báo runtime nếu thiếu
  lineDashed.visible = false;
  scene.add(lineDashed);

  return { p1, p2, lineSolid, lineDashed, isDashed: false };
}

function updateEdgeVisibility(edges, camera, solidMesh) {
  edges.forEach(edge => {
    const occluded = isEdgeOccluded(edge.p1, edge.p2, camera, solidMesh);
    edge.isDashed = occluded;
    edge.lineSolid.visible = !occluded;
    edge.lineDashed.visible = occluded;
  });
}
// Gọi updateEdgeVisibility() trong render loop (PHẦN 5), MỖI FRAME —
// đủ nhẹ cho khối đơn giản (~8-12 cạnh), không cần throttle.
```

> **Phương án dự phòng (rủi ro thấp hơn, dùng khi occlusion tự động chưa
> kịp verify hoặc quá phức tạp cho phạm vi bài):** hardcode sẵn danh sách
> cạnh nét đứt đúng cho ĐÚNG 1 góc camera đã khoá (không cần tổng quát mọi
> góc xoay) — chỉ khả thi khi bài đã chủ động khoá gần cứng camera về 1
> góc chuẩn (ví dụ đối chiếu đúng hình vẽ SGK). Đây là lựa chọn hợp lý khi
> phạm vi bài không cần học sinh tự xoay tự do kiểm tra mọi góc.

---

> Nhóm PHẦN 7 khác biệt hẳn PHẦN 4: PHẦN 4 xử lý đối tượng hình học phẳng
> (điểm/đường/mặt phẳng đơn lẻ, thường tự dựng bằng tay). PHẦN 7 xử lý
> **khối 3D hoàn chỉnh** (hình chóp, lăng trụ, tứ diện) — nhiều đỉnh, nhiều
> cạnh, nhiều mặt cùng lúc, cần 1 engine chung đọc config thay vì viết code
> riêng cho từng khối.

### 7.1 Kiến trúc SOLID_LIBRARY — config-driven, không hardcode mesh

> Mỗi khối là 1 object khai báo: hàm sinh đỉnh theo tham số, danh sách cạnh,
> danh sách mặt (tam giác hoá), và **`explore`** — quy định đỉnh nào kéo tự
> do, đỉnh nào trượt trên mặt phẳng đáy. Thêm khối mới = thêm 1 object, không
> viết thêm dòng code render nào.

```javascript
const SOLID_LIBRARY = {
  pyramid_quad: {
    info: { name: 'Hình chóp tứ giác S.ABCD', notation: 'S.ABCD', desc: '...' },
    params: [
      { id:'h', label:'Chiều cao (h)', min:.5, max:5, step:.1, val:3 },
      { id:'a', label:'Cạnh đáy (a)',  min:.5, max:4, step:.1, val:2 }
    ],
    // Hàm SINH đỉnh — nhận params hiện tại, trả toạ độ [x,y,z] thô
    vertices(p) {
      const half = p.a / 2;
      return {
        S: [0, p.h, 0],
        A: [-half, 0, -half], B: [half, 0, -half],
        C: [half, 0, half],   D: [-half, 0, half]
      };
    },
    edges: [['S','A'],['S','B'],['S','C'],['S','D'],
            ['A','B'],['B','C'],['C','D'],['D','A']],
    // Mặt LUÔN tam giác hoá — tứ giác đáy tách thành 2 tam giác chung 1 đường chéo
    faces: [['S','A','B'],['S','B','C'],['S','C','D'],['S','D','A'],
            ['A','B','C'],['A','C','D']],
    // EXPLORE: đỉnh nào 'free' (kéo tự do 3D), đỉnh nào 'floor' (trượt y=0)
    explore: { S:'free', A:'floor', B:'floor', C:'floor', D:'floor' }
  }
  // Thêm khối khác chỉ cần thêm object mới cùng cấu trúc
};
```

> **Gotcha — tam giác hoá tứ giác:** mặt tứ giác `[A,B,C,D]` phải tách thành
> `[A,B,C]` + `[A,C,D]` (chung đường chéo AC) khi build `BufferGeometry`,
> KHÔNG dùng index `[0,1,2,3]` trực tiếp — WebGL chỉ vẽ tam giác. Chọn đường
> chéo nào tách ảnh hưởng đến việc mặt có "gãy" hay không khi 4 điểm không
> đồng phẳng do kéo EXPLORE — với tứ giác gần vuông chọn đường chéo bất kỳ
> đều được, nhưng ghi rõ trong `faces` để nhất quán.

### 7.2 SolidRenderer — class render dùng chung cho mọi khối

```javascript
class SolidRenderer {
  constructor() {
    this.group = new THREE.Group(); scene.add(this.group);
    this.faceMeshes = [];   // Mesh Phong shading, trong suốt
    this.allEdgeLines = []; // [{lineV, lineH, nameA, nameB}] — cặp nét liền/đứt
    this.vtxLabels = [];    // [{el, name}] — label HTML overlay
    this.vertices = {};     // {tênĐỉnh: THREE.Vector3} — nguồn sự thật duy nhất
    this.config = null;
  }

  load(solidKey, params) {
    this.clear();
    this.config = SOLID_LIBRARY[solidKey];
    const raw = this.config.vertices(params);
    this.vertices = {};
    for (const [name, pos] of Object.entries(raw))
      this.vertices[name] = new THREE.Vector3(...pos);

    // Mỗi mặt → 1 Mesh Phong, opacity thấp, depthWrite:false (nhìn xuyên được)
    this.config.faces.forEach((face, idx) => {
      const pts = face.map(n => this.vertices[n]);
      const geo = new THREE.BufferGeometry().setFromPoints(pts);
      geo.setIndex(face.length === 3 ? [0,1,2] : [0,1,2,0,2,3]);
      geo.computeVertexNormals();
      const mat = new THREE.MeshPhongMaterial({
        color: this._faceColor(Math.floor(idx/2)), transparent: true,
        opacity: 0.28, side: THREE.DoubleSide, depthWrite: false, shininess: 60
      });
      const mesh = new THREE.Mesh(geo, mat);
      this.group.add(mesh); this.faceMeshes.push(mesh);
    });

    // Mỗi cạnh → LUÔN tạo CẢ 2 line (nét liền + nét đứt), ẩn 1 trong 2
    // tuỳ góc camera — xem 7.3 updateVisibility()
    this.config.edges.forEach(([a, b]) => {
      const pA = this.vertices[a], pB = this.vertices[b];
      const lineV = new THREE.Line(
        new THREE.BufferGeometry().setFromPoints([pA.clone(), pB.clone()]),
        new THREE.LineBasicMaterial({ color: 0xe6edf3 }));
      const lineH = new THREE.Line(
        new THREE.BufferGeometry().setFromPoints([pA.clone(), pB.clone()]),
        new THREE.LineDashedMaterial({ color: 0x444d56, dashSize:.15, gapSize:.1,
          transparent: true, opacity: 0.6 }));
      lineH.computeLineDistances(); lineH.visible = false;
      this.group.add(lineV); this.group.add(lineH);
      this.allEdgeLines.push({ lineV, lineH, nameA: a, nameB: b });
    });
  }
}
```

### 7.3 Cạnh thấy/khuất tự động — thuật toán dot-product với normal mặt

> Đây là phần khó nhất của PHẦN 7. Quy tắc: 1 cạnh **thấy** nếu ít nhất 1
> trong các mặt chứa nó đang "quay mặt" về phía camera. Tính lại **mỗi
> frame** vì camera xoay liên tục qua OrbitControls.

```javascript
// Gọi trong animate() mỗi frame — KHÔNG gọi 1 lần lúc load()
updateVisibility() {
  const camDir = new THREE.Vector3();
  camera.getWorldDirection(camDir);

  // Normal của từng mặt — tính lại mỗi frame vì EXPLORE có thể đổi hình dạng
  const faceNormals = this.config.faces.map(face => {
    const [p0,p1,p2] = face.map(n => this.vertices[n]);
    const v1 = new THREE.Vector3().subVectors(p1, p0);
    const v2 = new THREE.Vector3().subVectors(p2, p0);
    return new THREE.Vector3().crossVectors(v1, v2).normalize();
  });

  // Map cạnh → các mặt chứa nó (1 cạnh biên chỉ thuộc 1 mặt → luôn thấy)
  const edgeFaceMap = {};
  this.config.faces.forEach((face, fi) => {
    for (let i = 0; i < face.length; i++) {
      const key = [face[i], face[(i+1) % face.length]].sort().join('-');
      (edgeFaceMap[key] ||= []).push(fi);
    }
  });

  this.allEdgeLines.forEach(({ lineV, lineH, nameA, nameB }) => {
    const faceIdxs = edgeFaceMap[[nameA, nameB].sort().join('-')] || [];
    if (faceIdxs.length <= 1) { lineV.visible = true; lineH.visible = false; return; }
    // dot(normal, camDir) < 0 nghĩa là mặt đang quay VỀ phía camera
    const anyFront = faceIdxs.some(fi => faceNormals[fi].dot(camDir) < 0);
    lineV.visible = anyFront; lineH.visible = !anyFront;
  });
}
```

> **Gotcha:** `edgeFaceMap` group theo key `[a,b].sort().join('-')` để
> `A-B` và `B-A` map về cùng 1 key — nếu quên `.sort()`, mỗi cạnh sẽ có 2
> key khác nhau và thuật toán luôn coi là "cạnh biên" (chỉ 1 mặt), mất
> hoàn toàn khả năng phát hiện cạnh khuất.

### 7.4 EXPLORE mode — kéo đỉnh với ràng buộc floor/free

> **Ghi chú phạm vi áp dụng (thêm 07/2026):** Pattern này vẫn là 1 tính
> năng hợp lệ và nên giữ trong tài liệu dùng chung cho Hình học không
> gian — không phải lỗi thời, không xoá. Tuy nhiên **công cụ
> `solid_library.html` (Kho Khối Hình) hiện KHÔNG dùng pattern này** và
> đã gỡ bỏ mode này khỏi toolbar của nó. Lý do: Kho Khối Hình phục vụ
> mục đích dựng lại CHÍNH XÁC hình theo số liệu đề bài cho sẵn (SGK/đề
> thi) — kéo tự do dễ làm sai tỉ lệ so với đề, nên công cụ đó thay bằng
> sửa toạ độ trực tiếp qua ô nhập số (xem 7.10 bên dưới) thay vì kéo
> chuột. EXPLORE mode vẫn phù hợp cho một công cụ khác có mục tiêu khác:
> cho học sinh **tập vẽ hình tự do, rèn cảm giác không gian 3D** (không
> ràng buộc đúng-sai theo đề bài, không phải công cụ dạy/kiểm tra) — nếu
> về sau xây công cụ dạng đó, dùng lại nguyên pattern này.

> Không phải mọi đỉnh kéo tự do đều hợp lý sư phạm — kéo đỉnh ĐÁY của hình
> chóp lên khỏi mặt đáy sẽ phá vỡ khái niệm "đáy". Field `explore` trong
> config quy định từng đỉnh dùng constraint nào.

```javascript
// 'free': drag plane = mặt phẳng vuông góc hướng camera (kéo tự do mọi hướng)
// 'floor': drag plane = mặt phẳng y=0 cố định (chỉ trượt ngang, giữ đáy phẳng)
function startExploreDrag(vertexName, currentPos) {
  const constraint = SOLID_LIBRARY[currentSolidKey].explore[vertexName];
  if (constraint === 'floor') {
    return new THREE.Plane(new THREE.Vector3(0,1,0), 0); // y=0 cố định
  }
  const camDir = new THREE.Vector3(); camera.getWorldDirection(camDir);
  return new THREE.Plane().setFromNormalAndCoplanarPoint(camDir, currentPos);
}

// Trong pointermove — sau khi có intersection từ raycaster.ray.intersectPlane():
function applyExploreDrag(vertexName, intersection) {
  const constraint = SOLID_LIBRARY[currentSolidKey].explore[vertexName];
  if (constraint === 'floor') intersection.y = 0; // ép cứng, phòng sai số float
  solidRenderer.vertices[vertexName].copy(intersection);
  solidRenderer.rebuildFromVertices(); // xem 7.5 — KHÔNG gọi lại load()
}
```

> **Tứ diện tùy ý:** đặt cả 4 đỉnh `explore: {A:'free',B:'free',C:'free',D:'free'}`
> — không đỉnh nào ràng buộc mặt đáy, vì tứ diện không có "đáy" cố định,
> mọi mặt đều có thể coi là đáy (đúng tính chất SGK).

### 7.5 rebuildFromVertices() — update mesh không rebuild từ đầu

> Khi kéo EXPLORE, gọi lại `load()` (rebuild toàn bộ) mỗi frame sẽ dispose +
> tạo mới hàng chục mesh/geometry → giật lag rõ rệt. Thay vào đó, chỉ ghi
> lại buffer position của mesh đã có.

```javascript
rebuildFromVertices() {
  // Update từng face mesh — ghi trực tiếp vào buffer, không tạo Geometry mới
  this.faceMeshes.forEach((mesh, i) => {
    const pts = this.config.faces[i].map(n => this.vertices[n]);
    const posAttr = mesh.geometry.attributes.position;
    pts.forEach((p, j) => posAttr.setXYZ(j, p.x, p.y, p.z));
    posAttr.needsUpdate = true;               // BẮT BUỘC — thiếu dòng này mesh đứng im
    mesh.geometry.computeVertexNormals();      // shading lại theo hình dạng mới
  });
  // Update cạnh — setFromPoints tạo lại buffer nhỏ, chấp nhận được vì ít điểm
  this.allEdgeLines.forEach(({ lineV, lineH, nameA, nameB }) => {
    const pA = this.vertices[nameA], pB = this.vertices[nameB];
    lineV.geometry.setFromPoints([pA.clone(), pB.clone()]);
    lineH.geometry.setFromPoints([pA.clone(), pB.clone()]);
    lineH.computeLineDistances(); // phải gọi lại mỗi lần setFromPoints cho nét đứt
  });
}
```

## PHẦN 7.4-BIS — KÉO CẢ KHỐI (RIGID GROUP DRAG)

> **Thêm 08/2026** — phục vụ Bài 22 (Hai đường thẳng vuông góc) Module 2
> Tab 1b: 3 kim tự tháp thật đặt cạnh nhau, học sinh kéo dịch từng khối để
> tự kiểm chứng góc không đổi qua phép tịnh tiến.
>
> Khác PHẦN 1 (kéo 1 điểm) và PHẦN 7.4 (kéo 1 ĐỈNH làm biến dạng khối) — ở
> đây TOÀN BỘ khối (mesh + cạnh + label) di chuyển cùng nhau như 1 vật rắn,
> hình dạng không đổi. Dùng khi có nhiều đối tượng cùng loại đặt cạnh nhau
> và cho học sinh tự sắp xếp lại.
>
> ⚠️ **CHƯA VERIFY bằng file HTML thật** — pattern mới, viết theo đúng
> nguyên lý đã có (billboard-plane PHẦN 1.2, ràng buộc 'floor' PHẦN 7.4)
> nhưng ở cấp Group thay vì cấp điểm/đỉnh. Bắt buộc prototype nhỏ (3 khối
> lập phương đơn giản, không phải kim tự tháp thật) trước khi build chính
> thức — xem cảnh báo cuối mục.

### 7.4-BIS.1 Cấu trúc — mỗi khối gói trong 1 THREE.Group

```javascript
function createDraggableSolidGroup(solidConfig, position, labelText) {
  const group = new THREE.Group();
  group.position.copy(position);
  // ... build mesh khối + cạnh + label như PHẦN 7 bình thường, add vào group
  group.userData.draggableRigid = true;
  group.userData.label = labelText;
  return group;
}

// Mảng RIÊNG — khác allDraggableHitMeshes (PHẦN 1, đó là hit-mesh cấp ĐIỂM)
let draggableRigidGroups = [];
```

### 7.4-BIS.2 Drag-plane cố định = mặt đất (tái dùng nguyên lý 'floor' ở 7.4)

> Khác billboard theo hướng camera (PHẦN 1.2, dùng cho kéo tự do trong
> không gian) — ở đây BẮT BUỘC dùng mặt phẳng `y = groundY` cố định, vì
> khối đang "đặt trên đất", chỉ tịnh tiến ngang.

```javascript
const groundPlane = new THREE.Plane(new THREE.Vector3(0, 1, 0), 0); // y = 0

let rigidDragState = {
  active: false,
  group: null,
  grabOffset: new THREE.Vector3() // lệch giữa điểm click và group.position —
                                    // giữ nguyên khi kéo, tránh khối "nhảy"
                                    // để tâm về đúng vị trí con trỏ
};

renderer.domElement.addEventListener('pointerdown', (event) => {
  updateMouseNDC(event);
  raycaster.setFromCamera(mouseNDC, camera);
  // Raycast vào TOÀN BỘ mesh con của mọi group (khác PHẦN 1: ở đó raycast
  // vào 1 hit-mesh nhỏ riêng của từng điểm)
  const allMeshes = draggableRigidGroups.flatMap(g => g.children.filter(c => c.isMesh));
  const hits = raycaster.intersectObjects(allMeshes);
  if (hits.length > 0) {
    const group = hits[0].object.parent; // mesh con → group cha
    const hitPoint3D = new THREE.Vector3();
    raycaster.ray.intersectPlane(groundPlane, hitPoint3D);
    rigidDragState = {
      active: true,
      group,
      grabOffset: group.position.clone().sub(hitPoint3D)
    };
    orbitControls.enabled = false; // BẮT BUỘC — giống PHẦN 1.2
  }
});

renderer.domElement.addEventListener('pointermove', (event) => {
  if (!rigidDragState.active) return;
  updateMouseNDC(event);
  raycaster.setFromCamera(mouseNDC, camera);
  const hit3D = new THREE.Vector3();
  if (!raycaster.ray.intersectPlane(groundPlane, hit3D)) return;
  const target = hit3D.add(rigidDragState.grabOffset);
  target.y = 0; // ép cứng — giảm bậc tự do, không cho nhấc lên/xuống
  const snapped = snapToGrid(target, 20);
  if (!wouldOverlap(snapped, rigidDragState.group, 15)) {
    rigidDragState.group.position.copy(snapped);
    syncGroupLabel(rigidDragState.group); // label HTML overlay đi theo group
  }
});

renderer.domElement.addEventListener('pointerup', () => {
  rigidDragState.active = false;
  rigidDragState.group = null;
  orbitControls.enabled = true;
});

// BẮT BUỘC theo checklist Bước 6 (04_design_toan_3d.md) — cancel an toàn
renderer.domElement.addEventListener('pointercancel', () => {
  rigidDragState.active = false;
  rigidDragState.group = null;
  orbitControls.enabled = true;
});
```

### 7.4-BIS.3 Snap lưới + chống đè nhau

```javascript
function snapToGrid(pos, cellSize) {
  return new THREE.Vector3(
    Math.round(pos.x / cellSize) * cellSize,
    0,
    Math.round(pos.z / cellSize) * cellSize
  );
}

// Nếu vị trí sau snap quá gần 1 group khác → GIỮ vị trí cũ (không snap đè)
function wouldOverlap(candidatePos, movingGroup, minDist) {
  return draggableRigidGroups.some(g =>
    g !== movingGroup && g.position.distanceTo(candidatePos) < minDist
  );
}
```

### 7.4-BIS.4 Cleanup — bổ sung vào clearScene() đã có

> KHÔNG viết `clearScene()` riêng — chỉ chèn thêm đoạn dispose Group này vào
> hàm `clearScene()` gốc (04_design_toan_3d.md PHẦN 3.6), cùng cấp với các
> mảng `activePoints`/`activeLines`/`activePlanes` đã có.

```javascript
draggableRigidGroups.forEach(g => {
  g.traverse(obj => {
    if (obj.isMesh) { obj.geometry.dispose(); obj.material.dispose(); }
  });
  scene.remove(g);
});
draggableRigidGroups = [];
```

> ⚠️ **Trước khi build Bài 22 Tab 1b:** prototype riêng bằng 3 khối lập
> phương đơn giản (không phải kim tự tháp thật), kéo qua kéo lại nhiều lần,
> kiểm tra không giật/không "nhảy" khi nhả chuột, snap không đè nhau — đúng
> quy trình prototype-trước-khi-build đã áp dụng ở Phụ lục E
> (`01_scenario_builder_3d_addendum.md`).

---

### 7.6 Unified Point Pool — đỉnh gốc + điểm cạnh + điểm mặt cùng 1 hệ

> Để "nối 2 điểm bất kỳ" (đỉnh gốc lẫn điểm tự thêm) hoạt động, mọi điểm
> phải vào **1 pool chung** với interface giống nhau — khác biệt duy nhất
> là cách tính `getPos()`.

```javascript
// 3 loại điểm, cùng field getPos() nhưng công thức khác nhau:
// kind='vertex' → getPos() đọc trực tiếp từ solidRenderer.vertices[name]
// kind='edge'   → getPos() = lerp(A, B, t)
// kind='face'   → getPos() = toạ độ barycentric trong tam giác

function calcEdgePos(nameA, nameB, t) {
  const pA = solidRenderer.vertices[nameA], pB = solidRenderer.vertices[nameB];
  return new THREE.Vector3().lerpVectors(pA, pB, t);
}

// P = (1-u-v)·V0 + u·V1 + v·V2 — công thức chuẩn dựng điểm từ barycentric
function calcFacePos(faceIdx, bary) {
  const face = SOLID_LIBRARY[currentSolidKey].faces[faceIdx];
  const [v0,v1,v2] = face.map(n => solidRenderer.vertices[n]);
  const w = 1 - bary.u - bary.v;
  return new THREE.Vector3().addScaledVector(v0,w).addScaledVector(v1,bary.u).addScaledVector(v2,bary.v);
}
```

> **Tại sao cần pool chung thay vì 2 hệ riêng (đỉnh gốc / điểm tự thêm)?**
> Nếu tách riêng, logic "nối 2 điểm" phải viết 3 lần (vertex-vertex,
> vertex-free, free-free) và dễ bug khi quên 1 trường hợp. Pool chung +
> `getPos()` polymorphic giải quyết 1 lần cho mọi tổ hợp.

### 7.7 Toạ độ Barycentric từ điểm click trên mặt

```javascript
// Tính (u,v) của điểm P trong tam giác (v0,v1,v2) — P = v0 khi u=v=0
function barycentricCoords(P, v0, v1, v2) {
  const e1 = new THREE.Vector3().subVectors(v1, v0);
  const e2 = new THREE.Vector3().subVectors(v2, v0);
  const ep = new THREE.Vector3().subVectors(P,  v0);
  const d00 = e1.dot(e1), d01 = e1.dot(e2), d11 = e2.dot(e2);
  const d02 = e1.dot(ep), d12 = e2.dot(ep);
  const inv = 1 / (d00 * d11 - d01 * d01);
  const u = (d11 * d02 - d01 * d12) * inv;
  const v = (d00 * d12 - d01 * d02) * inv;
  // Clamp để điểm luôn nằm trong tam giác dù click hơi ra ngoài do sai số raycast
  return { u: Math.max(0, Math.min(1, u)), v: Math.max(0, Math.min(1 - u, v)) };
}

// Tâm tam giác = bary (1/3, 1/3) — dùng cho nút "G mặt" tính nhanh trọng tâm
function addFaceCentroid(faceIdx) { addFacePoint(faceIdx, { u: 1/3, v: 1/3 }); }
```

### 7.8 Mode system — khoá tương tác theo chế độ rõ ràng

> Bài học từ thực tế: nếu 1 click có thể vừa thêm điểm, vừa chọn, vừa kéo
> tuỳ ngữ cảnh, học sinh sẽ vô tình thêm điểm khi chỉ muốn xoay camera.
> Giải pháp: **float toolbar cố định trên canvas**, mỗi thời điểm chỉ 1
> mode active, mỗi mode chỉ cho phép 1 loại hành động.

```javascript
// 5 mode cho hệ thống khối: view / explore / point / connect / delete
// Khi đổi mode: LUÔN clearSelection() + đưa orbitControls.enabled về đúng trạng thái
function setMode(mode) {
  currentMode = mode;
  document.querySelectorAll('.mode-btn').forEach(b => b.classList.remove('active'));
  document.getElementById(MODE_META[mode].btn).classList.add('active');
  clearSelection();          // bỏ chọn điểm đang chờ nối từ mode trước
  orbitControls.enabled = true; // reset — mode nào cần tắt sẽ tự tắt khi drag
}

// Trong pointerdown: orbitControls.enabled = false NGAY khi bắt đầu bất kỳ
// tương tác nào không phải 'view' — tránh vừa kéo điểm vừa xoay camera cùng lúc
```

> **Phân biệt click vs drag bằng khoảng cách chuột:** nếu không phân biệt,
> mọi lần kéo camera nhẹ (dù chỉ 2-3px) cũng bị hiểu thành "click thêm điểm".

```javascript
let pointerDownXY = null;
const CLICK_MAX_DIST = 6; // px — dưới ngưỡng này mới coi là click, không phải drag

renderer.domElement.addEventListener('pointerdown', e => {
  pointerDownXY = { x: e.clientX, y: e.clientY };
  // ... xử lý bắt đầu drag nếu trúng điểm ...
});

renderer.domElement.addEventListener('pointerup', e => {
  const dx = e.clientX - (pointerDownXY?.x ?? e.clientX);
  const dy = e.clientY - (pointerDownXY?.y ?? e.clientY);
  const isClick = Math.hypot(dx, dy) < CLICK_MAX_DIST;
  if (!isClick) { /* đó là drag, không xử lý như click */ return; }
  // ... xử lý logic click theo mode ...
});
```

### 7.9 Hit-mesh riêng cho cạnh (cylinder mỏng) và mặt (mesh vô hình)

> Để phân biệt "click cạnh" vs "click mặt" khi 2 vùng này gần nhau, hit-mesh
> của cạnh phải **mỏng** (r ≈ 0.07) — nếu để to (r ≈ 0.11+) sẽ che mất phần
> lớn diện tích mặt gần cạnh, khiến click giữa mặt vẫn bị raycast trúng cạnh.

```javascript
function buildEdgeHitCylinder(nameA, nameB) {
  const pA = solidRenderer.vertices[nameA], pB = solidRenderer.vertices[nameB];
  const dir = new THREE.Vector3().subVectors(pB, pA);
  const len = dir.length();
  const geo = new THREE.CylinderGeometry(0.07, 0.07, len, 6); // mỏng — không che mặt
  const mesh = new THREE.Mesh(geo, new THREE.MeshBasicMaterial({ visible: false }));
  mesh.position.copy(pA).add(pB).multiplyScalar(0.5);
  mesh.quaternion.setFromUnitVectors(new THREE.Vector3(0,1,0), dir.normalize());
  mesh.userData = { kind: 'edge', nameA, nameB };
  return mesh;
}

// raycaster.params.Line.threshold cũng cần thu nhỏ nếu dùng THREE.Line làm hit-target
raycaster.params.Line = { threshold: 0.05 };
```

> **Thứ tự ưu tiên khi raycast trúng cả cạnh và mặt** (hiếm nhưng có thể ở
> góc nhìn thẳng theo cạnh): luôn xử lý cạnh TRƯỚC, mặt SAU — vì đặt điểm
> đúng trên cạnh có giá trị sư phạm cao hơn (dễ tính tỉ lệ AM/AB) so với đặt
> gần cạnh nhưng trên mặt.

### 7.10 Sửa toạ độ đỉnh gốc trực tiếp qua ô nhập số (khác EXPLORE — không kéo chuột)

> **Verify trong `solid_library.html` (07/2026).** Đây là lựa chọn thay thế
> cho EXPLORE (7.4) khi công cụ cần độ chính xác tuyệt đối thay vì thao tác
> kéo tự do: học sinh gõ thẳng số x/y/z vào 3 ô input trong bảng điểm, không
> dùng chuột. Ghi đè trực tiếp lên `vertices` rồi gọi lại `rebuildFromVertices()`
> (đã có sẵn ở 7.5, tái dùng nguyên hàm — không viết hàm rebuild riêng).

```javascript
function applyVertexXYZ(vertexName, axis, rawVal) {
  const num = parseFloat(rawVal);
  if (Number.isNaN(num)) { updatePtsSidebar(); return; } // gõ dở/rỗng → bỏ qua, vẽ lại UI cũ
  const v = solidRenderer.vertices[vertexName];
  if (!v) return;
  v[axis] = num;                    // ghi đè trực tiếp 1 trục (x/y/z)
  solidRenderer.rebuildFromVertices(); // dùng lại hàm ở 7.5 — không dispose/tạo lại
  buildInteractionMeshes();         // cạnh/mặt hit-mesh phải dựng lại theo vị trí đỉnh mới
  updatePtsSidebar();
}
```

> **Đánh đổi cần biết trước khi dùng pattern này:** vì `vertices` vốn được
> TÍNH LẠI từ công thức + tham số slider mỗi khi slider đổi (xem PHẦN 7.1),
> sửa tay 1 đỉnh sẽ bị **ghi đè mất** ngay khi người dùng kéo slider kích
> thước lần tiếp theo — y hệt hạn chế của EXPLORE. Khác biệt duy nhất so với
> EXPLORE là INPUT (gõ số vs kéo chuột), không phải kiến trúc lưu trữ bên
> dưới — cả 2 đều là "override tạm thời lên vertices, mất khi rebuild từ
> params". Nếu cần giữ chỉnh tay qua nhiều lần đổi slider, phải tách hẳn
> một field `vertexOverrides` độc lập khỏi luồng tính từ params — chưa làm,
> ghi chú lại để tránh nhầm là đã có.
>
> Đi kèm bắt buộc: có nút "↺ Reset" gọi lại `loadSolid()` để đưa khối về
> đúng công thức gốc khi học sinh chỉnh nhầm.

---

## PHẦN 8 — HẠ ĐƯỜNG CAO TỪ ĐIỂM XUỐNG MẶT PHẲNG (đáy hoặc mặt bên)

> Ứng dụng trực tiếp `definePlaneFromPoints` + `projectPointOntoPlane` (đã có ở
> PHẦN 4.10) lên hệ khối đa diện của PHẦN 7. Khác biệt: mặt phẳng không cố
> định — phải tính lại **mỗi frame** từ tên đỉnh, vì EXPLORE hoặc slider có
> thể đổi vị trí đỉnh bất kỳ lúc nào.

### 8.1 Field `baseVertices` — khai báo "đáy" cho từng khối

```javascript
// Thêm vào mỗi entry trong SOLID_LIBRARY (chỉ khối có đáy rõ ràng mới có field này)
// Chỉ cần 3 tên đầu để định nghĩa mặt phẳng — tên còn lại (nếu là đáy tứ giác)
// PHẢI đồng phẳng theo thiết kế ban đầu của vertices()
pyramid_quad_like: {
  // ...
  baseVertices: ['A', 'B', 'C', 'D']  // đáy tứ giác — dùng A,B,C để định nghĩa mặt phẳng
}

// Khối không có đáy tự nhiên (tứ diện đều/thường) — KHÔNG khai báo field này
// → sidebar sẽ chỉ hiện nút "Xuống mặt XYZ" cho từng mặt, không có nút "Xuống đáy"
```

> **Trường hợp đặc biệt — bát diện đều:** không có mặt "đáy" thật (8 mặt đều
> là tam giác bên), nhưng 4 đỉnh "xích đạo" A,B,C,D vẫn đồng phẳng về mặt
> hình học. Khai báo `baseVertices: ['A','B','C','D']` vẫn hợp lệ — đây là
> mặt phẳng đối xứng, không phải 1 mặt trong `faces[]`, nhưng vẫn dùng được
> để minh hoạ "đường cao từ S xuống mặt phẳng ABCD" mang tính sư phạm.

### 8.2 Tính mặt phẳng từ tên đỉnh — luôn tính lại, không cache

```javascript
// Lấy 3 tên đầu trong danh sách, tính plane từ vị trí HIỆN TẠI của solidRenderer.vertices
// Gọi lại hàm này mỗi frame — không lưu kết quả vì EXPLORE có thể đã đổi vị trí
function planeFromVertexNames(names) {
  const pts = names.slice(0, 3).map(n => solidRenderer.vertices[n]);
  if (pts.some(p => !p)) return null;
  return definePlaneFromPoints(pts[0], pts[1], pts[2]);
}
```

### 8.3 Luồng UX — chọn điểm nguồn trước, chọn mặt đích sau (không click 3D 2 lần)

> Quan trọng: đích hạ đường cao chọn qua **nút trong sidebar**, không phải
> click thêm lần 2 vào mặt phẳng trong scene 3D. Lý do: click vào mặt cong/
> mặt nghiêng trong không gian 3D dễ trúng nhầm mặt khác do góc camera,
> trong khi danh sách nút text luôn rõ ràng, không mơ hồ.

```javascript
let heightSourceId = null; // id điểm nguồn đang chọn (từ pointPool — vertex hoặc điểm tự thêm)

// Bước 1: click 1 điểm bất kỳ trong pointPool → lưu làm nguồn, highlight ring
function selectHeightSource(id) {
  heightSourceId = (heightSourceId === id) ? null : id; // click lại chính nó → bỏ chọn
  pointPool.forEach(pt => {
    const on = pt.id === heightSourceId;
    pt.ring.material.opacity = on ? 0.85 : 0;
  });
  updatePtsSidebar(); // sidebar tự hiện danh sách nút đích tương ứng
}

// Bước 2: sidebar hiện nút "Xuống đáy (...)" (nếu có baseVertices) + nút
// "Xuống mặt XYZ" cho từng mặt KHÔNG trùng đáy — loại trùng bằng cách kiểm
// tra mọi đỉnh của mặt có đều nằm trong baseVertices không
const baseSet = new Set(cfg.baseVertices || []);
const faceBtns = cfg.faces.filter(face => !(cfg.baseVertices && face.every(n => baseSet.has(n))));
```

### 8.4 Vẽ đường cao — dùng geometry cập nhật, KHÔNG dispose/tạo lại mỗi frame

> Bài học từ PHẦN 7.5: dispose + tạo mới mesh mỗi frame gây giật. Dấu góc
> vuông (3 điểm gấp khúc) và nét đứt đều dùng `geometry.setFromPoints()` để
> cập nhật tại chỗ.

```javascript
// Dấu góc vuông — tạo 1 lần, update points mỗi frame (không tạo lại Line)
function makeRightAngleGeo(color) {
  const geo = new THREE.BufferGeometry().setFromPoints([
    new THREE.Vector3(), new THREE.Vector3(), new THREE.Vector3()
  ]);
  const line = new THREE.Line(geo, new THREE.LineBasicMaterial({ color }));
  scene.add(line);
  return line;
}

function updateRightAngleGeo(line, H, refDir, upDir, size = 0.22) {
  const r = refDir.clone().normalize(), u = upDir.clone().normalize();
  const p0 = H.clone().add(r.clone().multiplyScalar(size));
  const p1 = p0.clone().add(u.clone().multiplyScalar(size));
  const p2 = H.clone().add(u.clone().multiplyScalar(size));
  line.geometry.setFromPoints([p0, p1, p2]); // ghi đè buffer, không tạo geometry mới
}

// Sync mỗi frame — plane, foot H, nét đứt, dấu vuông, label đều tính lại
function syncHeights() {
  heights.forEach(h => {
    const plane = planeFromVertexNames(h.planeNames);
    if (!plane) return;
    const M = h.sourcePt.getPos();
    const { H, distance } = projectPointOntoPlane(M, plane);
    h.dashLine.geometry.setFromPoints([M.clone(), H.clone()]);
    h.dashLine.computeLineDistances(); // BẮT BUỘC lại mỗi lần setFromPoints cho nét đứt
    h.footMarker.position.copy(H);
    // refDir lấy từ planeNames[1]-planeNames[0] — hướng bất kỳ trong mặt phẳng
    const refDir = new THREE.Vector3().subVectors(
      solidRenderer.vertices[h.planeNames[1]], solidRenderer.vertices[h.planeNames[0]]);
    const upDir = new THREE.Vector3().subVectors(M, H);
    if (refDir.lengthSq() > 1e-6 && upDir.lengthSq() > 1e-6)
      updateRightAngleGeo(h.raMark, H, refDir, upDir, 0.2);
    h.label.textContent = `h = ${distance.toFixed(2)}`;
  });
}
```

> **Gotcha:** nếu điểm nguồn đã nằm trên mặt đích (`distance < 0.03`), KHÔNG
> vẽ — nét đứt độ dài ~0 sẽ nhấp nháy vô nghĩa trên màn hình. Kiểm tra
> ngưỡng này ngay khi tạo, không cần kiểm tra lại mỗi frame (nếu distance
> giảm về 0 sau khi đã vẽ do EXPLORE, chấp nhận hiển thị đường cao ngắn —
> đó là phản hồi trực quan đúng, không phải lỗi).

---

## PHẦN 9 — KHỐI TRÒN XOAY (RoundSolidRenderer) — mặt cong, KHÔNG dùng vertices/edges/faces

> Khác biệt gốc rễ với PHẦN 7: khối tròn xoay (cầu, trụ, nón) không có đỉnh
> rời rạc — dùng geometry dựng sẵn của Three.js (`SphereGeometry`,
> `CylinderGeometry`, `ConeGeometry`) thay vì tự dựng từ danh sách đỉnh.
> Vì vậy **không tái sử dụng được** hệ EXPLORE/point-on-edge/point-on-face
> của PHẦN 7 — đây là lý do cần 1 class hoàn toàn riêng.

### 9.1 ROUND_LIBRARY — cấu trúc tối giản, không cần edges/faces

```javascript
const ROUND_LIBRARY = {
  khoi_tru: {
    info: { name: 'Khối trụ', notation: '', desc: '...' },
    type: 'cylinder', // 'sphere' | 'cylinder' | 'cone' — dùng để switch trong renderer
    params: [
      { id:'r', label:'Bán kính đáy (r)', min:.5, max:3, step:.1, val:1.5 },
      { id:'h', label:'Chiều cao (h)',    min:.5, max:5, step:.1, val:3 }
    ]
  }
  // Không có vertices()/edges/faces — hình dựng trực tiếp bằng geometry có sẵn
};
```

### 9.2 Vòng tròn viền (rim circle) — vẽ tay bằng tham số hoá, không dùng EdgesGeometry

> `THREE.EdgesGeometry` trên `CylinderGeometry` sẽ vẽ TẤT CẢ các đường chia
> lưới (radialSegments), tạo hiệu ứng "múi bưởi" xấu — không giống hình vẽ
> SGK chỉ có 2 vòng tròn viền (đáy trên/dưới). Phải tự vẽ vòng tròn bằng
> tham số hoá góc.

```javascript
// Vòng tròn nằm ngang (mặt phẳng XZ) tại độ cao cy — dùng cho đáy trụ/nón
_ellipseXZ(cy, rx, rz, color) {
  const pts = [];
  for (let i = 0; i <= 64; i++) {
    const t = (i / 64) * Math.PI * 2;
    pts.push(new THREE.Vector3(rx * Math.cos(t), cy, rz * Math.sin(t)));
  }
  const line = new THREE.Line(
    new THREE.BufferGeometry().setFromPoints(pts),
    new THREE.LineBasicMaterial({ color })
  );
  this.group.add(line);
  return line;
}
```

> **Giới hạn đã biết (v1):** vòng tròn vẽ toàn bộ 1 màu, KHÔNG tách nét đứt
> cho phần bị che phía sau như quy ước SGK vẽ tay (nửa xa camera thường nét
> đứt). Để làm đúng cần tính góc silhouette theo hướng camera mỗi frame —
> để lại cho phiên sau, đây không phải lỗi mà là phạm vi cố ý chưa làm.

### 9.3 Điểm tham chiếu tĩnh — không dùng pointPool, không cần EXPLORE

```javascript
// refPoints là object tĩnh — vị trí không đổi trừ khi rebuild qua slider
// KHÔNG cần đăng ký vào pointPool (PHẦN 7.6) vì v1 không hỗ trợ Nối/Xoá cho khối tròn xoay
load(key, params) {
  // ...
  if (type === 'cylinder') {
    this.refPoints['O']  = new THREE.Vector3(0, 0, 0);   // tâm đáy dưới
    this.refPoints["O'"] = new THREE.Vector3(0, params.h, 0); // tâm đáy trên
  }
  // Label HTML tạo 1 lần trong load(), sync vị trí mỗi frame qua syncLabels()
}
```

### 9.4 Dispatch giữa 2 renderer — SOLID_LIBRARY (đa diện) vs ROUND_LIBRARY (tròn xoay)

> Cả 2 hệ dùng chung `scene`, `camera`, `pointPool`, `segments` toàn cục —
> phải dọn sạch hệ cũ triệt để khi chuyển qua hệ khác, và **guard mọi hàm
> đọc `solidRenderer.vertices`/`config`** để không crash khi đối tượng đó
> đang trống (do đã `clear()`).

```javascript
let isRoundActive = false; // cờ toàn cục — mọi nơi cần biết đang ở hệ nào

function loadRoundSolid(key) {
  // Dọn TOÀN BỘ trạng thái đa diện trước khi chuyển
  [...pointPool.filter(p => p.kind !== 'vertex')].forEach(p => removePoint(p.id));
  segments.forEach(/* dispose */); segments = [];
  clearAllHeights();
  pointPool = [];
  solidRenderer.clear(); // quan trọng — nếu không clear, mesh đa diện cũ vẫn còn trong scene

  isRoundActive = true;
  roundRenderer.load(key, currentRoundParams); // currentRoundParams đọc từ ROUND_LIBRARY[key].params
  updateModeBarVisibility(); // ẩn nút Kéo đỉnh/Thêm điểm/Nối/Xoá/Hạ đường cao
  setMode('view'); // luôn về view khi chuyển hệ
}

// setMode() phải guard mọi logic đặc thù đa diện bằng isRoundActive —
// nếu không, setMode('view') gọi từ loadRoundSolid() sẽ vô tình rebuild
// solidRenderer với currentSolidKey CŨ (khối đa diện trước đó), tạo lại
// mesh đa diện chồng lên khối tròn xoay vừa load
function setMode(mode) {
  // ... phần chung (cập nhật active button, hint, clearSelection) ...
  if (!isRoundActive) {
    // Chỉ rebuild solidRenderer khi đang ở hệ đa diện
    if (mode !== 'explore') solidRenderer.rebuildGeometry(currentSolidKey, currentParams);
    // ...
  }
}
```

> **Đây là lỗi thực tế đã xảy ra khi tích hợp lần đầu:** `setMode()` viết
> cho hệ đa diện gọi `solidRenderer.rebuildGeometry()` không điều kiện. Khi
> `loadRoundSolid()` gọi `setMode('view')` ở cuối, hàm rebuild lại chạy với
> `currentSolidKey` là khối đa diện được xem TRƯỚC ĐÓ — nếu không thêm guard
> `isRoundActive`, khối đa diện cũ sẽ hiện lại đè lên khối tròn xoay.

### 9.5 CATALOG với cờ `round` — sidebar biết tra thư viện nào

```javascript
const CATALOG = [
  { label: 'Hình chóp', keys: ['pyramid_tri', 'pyramid_quad' /* , ... các khối khác */] }, // → SOLID_LIBRARY
  { label: 'Khối tròn xoay', keys: ['khoi_cau','khoi_tru','khoi_non'], round: true },       // → ROUND_LIBRARY
];

// buildCatalog() chọn thư viện theo cờ, và chọn hàm load tương ứng
function buildCatalog(query) {
  CATALOG.forEach(g => {
    const lib = g.round ? ROUND_LIBRARY : SOLID_LIBRARY;
    // ...
    btn.onclick = () => g.round ? loadRoundSolid(key) : loadSolid(key);
  });
}
```

---

## PHẦN 10 — MẶT BẬC HAI (QuadricRenderer) — mặt cong tham số, KHÔNG dùng geometry dựng sẵn

> **Thêm 08/2026**, code trích thật từ module "Em có biết — 6 mặt bậc hai"
> (Toán 12, Bài 14 mở rộng) — đã build, verify, và chạy được. Khác biệt gốc
> rễ với cả PHẦN 7 và PHẦN 9: mặt bậc hai (ellipsoid, hyperboloid, nón
> elliptic, paraboloid...) là **mặt cong liên tục theo phương trình tham
> số** — không có đỉnh-cạnh-mặt rời rạc như PHẦN 7, và cũng KHÔNG có
> geometry dựng sẵn của Three.js như PHẦN 9 (`SphereGeometry` chỉ dùng
> được cho riêng ellipsoid qua phép scale, 5 mặt còn lại phải tự dựng lưới
> đỉnh bằng tay). Vì vậy đây là **hệ renderer thứ 3** (tạm gọi "Nhánh C"),
> không tái sử dụng được state machine của PHẦN 7 hay ROUND_LIBRARY của
> PHẦN 9.

### 10.1 QUADRIC_LIBRARY — mỗi khối tự định nghĩa hàm `build()` riêng

> Khác PHẦN 7 (`vertices()/edges/faces` dùng chung 1 khuôn) và PHẦN 9
> (`type` dùng để switch trong 1 renderer chung) — ở đây mỗi mặt bậc hai
> có công thức tham số khác nhau hoàn toàn, nên để mỗi entry tự định nghĩa
> hàm `build(params)` riêng, trả về `BufferGeometry` (hoặc `Group` nếu cần
> nhiều lưới tách biệt — xem 10.3).

```javascript
const QUADRIC_LIBRARY = {
  ellipsoid: {
    name: 'Mặt Ellipsoid (mặt trái xoan)',
    notation: 'x²/a² + y²/b² + z²/c² = 1',
    params: { a: 1.6, b: 1.1, c: 1.3 },
    color: 0x7FCBA4,
    build(p) {
      // Cách rẻ nhất — KHÔNG tự dựng lưới tham số. Ellipsoid = hình cầu
      // scale không đều 3 trục.
      const geo = new THREE.SphereGeometry(1, 48, 32);
      geo.scale(p.a, p.c, p.b); // trục cao SGK (z) map vào Y của Three.js
      return geo;
    }
  },
  hyperboloid1: {
    name: 'Mặt Hyperboloid một tầng',
    notation: 'x²/a² + y²/b² − z²/c² = 1',
    params: { a: 1.1, b: 1.1, c: 1, vmax: 1.1 },
    color: 0x4CAF7D,
    build(p) {
      const segU = 48, segV = 24;
      const positions = []; const idx = [];
      for (let i = 0; i <= segV; i++) {
        const v = -p.vmax + (2 * p.vmax * i) / segV;
        for (let j = 0; j <= segU; j++) {
          const theta = (2 * Math.PI * j) / segU;
          positions.push(
            p.a * Math.cosh(v) * Math.cos(theta),  // x
            p.c * Math.sinh(v),                     // y (= trục cao SGK)
            p.b * Math.cosh(v) * Math.sin(theta)    // z
          );
        }
      }
      idx.push(...triangulateGrid(segU, segV));
      const geo = new THREE.BufferGeometry();
      geo.setIndex(idx);
      geo.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
      geo.computeVertexNormals();
      return geo;
    }
  },
  // hyperboloid2 (2 tầng), cone, paraboloidE, paraboloidH: xem PHẦN 10.3 —
  // các hàm build() còn lại theo đúng công thức đã verify ở
  // 04_design_toan_3d.md PHẦN 3.8.
};
const QUADRIC_ORDER = ['ellipsoid','hyperboloid1','hyperboloid2','cone','paraboloidE','paraboloidH'];
```

### 10.2 Khung tam giác hoá dùng chung — `triangulateGrid`

> Hàm DUY NHẤT dùng lại cho cả 5 mặt tham số (không dùng cho ellipsoid vì
> đó là `SphereGeometry` có sẵn). Copy nguyên vẹn từ `04_design_toan_3d.md`
> PHẦN 3.8 — không viết lại khác đi.

```javascript
function triangulateGrid(segU, segV) {
  const idx = [];
  for (let i = 0; i < segV; i++) {
    for (let j = 0; j < segU; j++) {
      const a0 = i * (segU + 1) + j;
      const b0 = a0 + 1;
      const c0 = a0 + (segU + 1);
      const d0 = c0 + 1;
      idx.push(a0, c0, b0, b0, c0, d0);
    }
  }
  return idx;
}
```

### 10.3 Trường hợp đặc biệt — khi KHÔNG được dùng 1 lưới liên tục

> 2 lỗi thực tế đã gặp khi build — cả 2 đều do cố dùng 1
> `BufferGeometry`/1 `triangulateGrid()` liên tục cho thứ vốn KHÔNG liên
> tục về mặt hình học:

**Nón elliptic — PHẢI tách 2 lớp trên/dưới đỉnh, không nối chung:**
```javascript
cone: {
  name: 'Mặt nón Elliptic',
  notation: 'x²/a² + y²/b² − z²/c² = 0',
  params: { a: 1, b: 0.7, smax: 1.6 },
  color: 0x159957,
  build(p) {
    const segU = 40;
    const positions = []; const idx = [];
    const sVals = [-p.smax, 0, p.smax]; // 3 lớp: dưới đỉnh, đỉnh, trên đỉnh
    for (const s of sVals) {
      for (let j = 0; j <= segU; j++) {
        const theta = (2 * Math.PI * j) / segU;
        positions.push(p.a * s * Math.cos(theta), s, p.b * s * Math.sin(theta));
      }
    }
    // 2 lớp riêng (layer 0-1 và layer 1-2), KHÔNG nối layer 0 thẳng qua layer 2
    for (let layer = 0; layer < 2; layer++) {
      const base = layer * (segU + 1);
      for (let j = 0; j < segU; j++) {
        const a0 = base + j, b0 = base + j + 1;
        const c0 = base + (segU + 1) + j, d0 = c0 + 1;
        idx.push(a0, c0, b0, b0, c0, d0);
      }
    }
    const geo = new THREE.BufferGeometry();
    geo.setIndex(idx);
    geo.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
    geo.computeVertexNormals();
    return geo;
  }
}
```
> **Lỗi nếu làm sai:** nối lưới bán kính 0 (đỉnh, s=0) thẳng vào lưới bán
> kính khác 0 (s=±smax) qua CÙNG 1 `triangulateGrid()` liên tục sẽ tạo tam
> giác "xoắn" quanh điểm suy biến — mặt nón bị méo tại đỉnh.

**Hyperboloid 2 tầng — PHẢI 2 `BufferGeometry` độc lập trong 1 `Group`:**
```javascript
hyperboloid2: {
  name: 'Mặt Hyperboloid hai tầng',
  notation: 'x²/a² + y²/b² − z²/c² = −1',
  params: { a: 1, b: 1, c: 1.2, vmax: 1.15 },
  color: 0x2E8B57,
  isGroup: true,
  build(p) {
    const group = new THREE.Group();
    const segU = 40, segV = 18;
    [1, -1].forEach(sign => {
      const positions = [];
      for (let i = 0; i <= segV; i++) {
        const v = (p.vmax * i) / segV;
        for (let j = 0; j <= segU; j++) {
          const theta = (2 * Math.PI * j) / segU;
          positions.push(
            p.a * Math.sinh(v) * Math.cos(theta),
            sign * p.c * Math.cosh(v),
            p.b * Math.sinh(v) * Math.sin(theta)
          );
        }
      }
      const geo = new THREE.BufferGeometry();
      geo.setIndex(triangulateGrid(segU, segV));
      geo.setAttribute('position', new THREE.Float32BufferAttribute(positions, 3));
      geo.computeVertexNormals(); // tính riêng cho MỖI geometry — xem lỗi dưới
      const mat = new THREE.MeshPhongMaterial({ color: p.color ?? 0x2E8B57, transparent: true, opacity: 0.88, side: THREE.DoubleSide });
      group.add(new THREE.Mesh(geo, mat));
    });
    return group;
  }
}
```
> **Lỗi nếu làm sai:** dùng CHUNG 1 `BufferGeometry` cho cả 2 tấm (nối
> `positions` của tấm trên và tấm dưới vào 1 mảng liên tục) khiến
> `computeVertexNormals()` tính sai pháp tuyến ở biên giữa 2 tấm — dù 2
> tấm không thực sự chạm nhau trong không gian, chúng vẫn liên tiếp nhau
> VỀ CHỈ SỐ mảng, nên thuật toán tính normal coi chúng là 1 mặt liên tục.
> Bắt buộc 2 `BufferGeometry` tách biệt, gộp bằng `THREE.Group`.

### 10.4 buildMesh() — dispatch build() + material + wireframe, xử lý cả trường hợp Group

```javascript
function buildQuadricMesh(key, params) {
  const cfg = QUADRIC_LIBRARY[key];
  const built = cfg.build(params);

  function makeMeshWithWireframe(geo, color) {
    const mat = new THREE.MeshPhongMaterial({
      color, transparent: true, opacity: 0.88,
      side: THREE.DoubleSide, shininess: 25, specular: 0x336644,
    });
    const mesh = new THREE.Mesh(geo, mat);
    const wire = new THREE.LineSegments(
      new THREE.WireframeGeometry(geo),
      new THREE.LineBasicMaterial({ color: 0x0E5C38, transparent: true, opacity: 0.3 })
    );
    const group = new THREE.Group();
    group.add(mesh); group.add(wire);
    return group;
  }

  if (cfg.isGroup) return built; // hyperboloid2 tự tạo Group kèm material trong build()
  return makeMeshWithWireframe(built, cfg.color);
}
```

### 10.5 Cleanup — `clearScene()` dispose đúng cả trường hợp Group lồng nhau

```javascript
let currentQuadricMesh = null;
function clearQuadricScene() {
  if (!currentQuadricMesh) return;
  currentQuadricMesh.traverse(o => {
    if (o.geometry) o.geometry.dispose();
    if (o.material) o.material.dispose();
  });
  scene.remove(currentQuadricMesh);
  currentQuadricMesh = null;
}
```
> `traverse()` là bắt buộc (không phải `.geometry?.dispose()` đơn lẻ) vì
> kết quả `buildQuadricMesh()` luôn là `Group` (dù chứa 1 hay nhiều mesh
> con) — dispose trực tiếp trên `Group` không làm gì cả vì `Group` không
> có `.geometry`/`.material` của riêng nó.

### 10.6 Ánh sáng & vật liệu bắt buộc — KHÁC quy tắc mặc định PHẦN 0

> Mặt bậc hai thường dùng với Preset 4 (Cream & Green,
> `04_design_toan_3d.md` PHẦN 1.3-BIS) — nền sáng cần ánh sáng hướng để
> lộ gradient trên mặt cong, khác quy tắc "chỉ AmbientLight" cho mặt
> phẳng/đường ở các PHẦN trước.

```javascript
scene.add(new THREE.AmbientLight(0xffffff, 0.55));
const dirLight = new THREE.DirectionalLight(0xFFF4E0, 0.95); // ánh sáng ấm
dirLight.position.set(4, 6, 5);
scene.add(dirLight);
```

### 10.7 Dispatch 3 hệ renderer — thêm cờ `quadric` vào CATALOG

```javascript
const CATALOG = [
  { label: 'Hình chóp',        keys: ['pyramid_tri', 'pyramid_quad'] },                      // → SOLID_LIBRARY (PHẦN 7)
  { label: 'Khối tròn xoay',   keys: ['khoi_cau','khoi_tru','khoi_non'], round: true },        // → ROUND_LIBRARY (PHẦN 9)
  { label: 'Mặt bậc hai',      keys: QUADRIC_ORDER, quadric: true },                           // → QUADRIC_LIBRARY (PHẦN 10)
];

function buildCatalog(query) {
  CATALOG.forEach(g => {
    const lib = g.round ? ROUND_LIBRARY : g.quadric ? QUADRIC_LIBRARY : SOLID_LIBRARY;
    // ...
    btn.onclick = () => {
      if (g.round) return loadRoundSolid(key);
      if (g.quadric) return loadQuadricSolid(key); // dọn sạch 2 hệ còn lại trước khi load
      return loadSolid(key);
    };
  });
}
```
> Áp dụng đúng nguyên tắc đã cảnh báo ở PHẦN 9.4 (lỗi thực tế
> `isRoundActive`) — với 3 hệ, cần 1 biến trạng thái duy nhất
> (`activeSystem: 'solid' | 'round' | 'quadric'`) thay vì 1 cờ boolean,
> và MỌI hàm rebuild phải guard theo đúng biến này trước khi chạy, để
> tránh 1 trong 3 hệ vô tình rebuild đè lên hệ đang hiển thị.

---

## PHỤ LỤC — LỖI HAY GẶP

```
- Điểm "trôi" xa khi kéo ở góc camera nghiêng
  → Kiểm tra dragPlane có dùng đúng camera.getWorldDirection() làm
    pháp tuyến, đi qua ĐÚNG vị trí hiện tại của điểm (không phải gốc toạ độ)

- Kéo điểm vô tình xoay cả camera (giật, 2 input giành nhau)
  → Kiểm tra orbitControls.enabled = false đã chạy TRƯỚC khi raycast,
    và = true đã chạy ở CẢ pointerup và pointerleave

- Label "dính ngược" lên màn hình khi xoay quá xa
  → Kiểm tra điều kiện screenPos.z > 1 để ẩn label khi điểm ở sau camera

- ConstrainedPoint bay ra khỏi đoạn thẳng khi kéo nhanh
  → Kiểm tra đã gọi dragToward() (chiếu + clamp), không gán trực tiếp
    intersection vào mesh.position như điểm tự do

- Mặt phẳng từ 3 điểm bị "lật" hướng ngẫu nhiên khi 3 điểm gần thẳng hàng
  → Kiểm tra normal.lengthSq() < 1e-6 đã return null đúng chỗ trước
    khi gọi mesh.lookAt()

- Hiệu năng giảm dần sau khi kéo nhiều phút (memory leak)
  → Kiểm tra mọi mesh bị remove khỏi scene đều gọi .geometry.dispose()
    và .material.dispose() trước khi tạo mesh thay thế

- Mặt nón elliptic bị méo/xoắn tại đỉnh (PHẦN 10.3)
  → Kiểm tra đỉnh (s=0) và 2 lớp bán kính khác 0 có đang bị tam giác hoá
    LIÊN TỤC bằng 1 triangulateGrid() duy nhất không — phải tách 2 lớp
    riêng, mỗi lớp tự tam giác hoá, KHÔNG share index qua điểm đỉnh

- Hyperboloid 2 tầng: pháp tuyến sai ở gần "khoảng trống" giữa 2 tầng
  (dù 2 tầng không hề chạm nhau trong không gian) (PHẦN 10.3)
  → Kiểm tra có đang dùng CHUNG 1 BufferGeometry cho cả 2 tầng không —
    computeVertexNormals() coi 2 mảng positions nối tiếp là 1 mặt liên
    tục dù toạ độ cách xa. Bắt buộc 2 BufferGeometry độc lập trong 1 Group

- clearScene() không xoá hết mesh khi chuyển giữa mặt bậc hai (PHẦN 10.5)
  → Kiểm tra đang gọi .traverse() để dispose từng mesh CON, không gọi
    .geometry.dispose() trực tiếp trên Group (Group không có .geometry)

- Mesh rebuild real-time mỗi frame khi kéo (VD thiết diện đổi hình dạng
  theo điểm đang kéo) để lại "vệt" nhiều lớp chồng lên nhau, không xoá
  lớp cũ dù code CÓ gọi scene.remove()
  → LỖI THỰC TẾ: gán mesh phụ (VD đường viền) vào thuộc tính của chính
    mesh chính (`crossSectionMesh.borderLine = borderLine`), rồi kiểm
    tra "có viền cũ chưa" bằng `if (crossSectionMesh.borderLine)` NGAY
    SAU KHI đã tạo `crossSectionMesh` MỚI ở phía trên — dòng kiểm tra
    đó luôn đọc trên object mới toanh (chưa từng có thuộc tính này),
    nên viền của FRAME TRƯỚC không bao giờ bị remove, cứ thế cộng dồn
    qua mỗi frame kéo. SỬA: tách mesh phụ thành BIẾN Ở SCOPE NGOÀI, độc
    lập hoàn toàn với vòng đời của mesh chính — dispose cả 2 biến riêng
    biệt TRƯỚC KHI tạo bất cứ gì mới trong mỗi lần rebuild, không gán
    lồng vào nhau qua thuộc tính động.
  → Nếu mesh phụ là 1 THREE.Group chứa nhiều children (VD viền vẽ bằng
    nhiều CylinderGeometry ghép lại thay vì 1 Line, để viền "dày" hơn
    giới hạn 1px của LineBasicMaterial trên nhiều driver WebGL) — PHẢI
    dispose TỪNG CHILD bên trong Group (`group.children.forEach(c =>
    {c.geometry.dispose(); c.material.dispose();})`), Group không có
    thuộc tính `.geometry`/`.material` trực tiếp như Mesh đơn, gọi
    `.geometry.dispose()` thẳng trên Group sẽ ném lỗi hoặc âm thầm
    không dọn được gì.

- Click vào khoảng trống vẫn "chọn được" 1 đường đã ẩn (PHẦN 4.7)
  → Kiểm tra setVisible() đã set CẢ hitMesh.visible, không chỉ
    line.visible — và mọi raycast đã lọc qua visibleLines() trước khi
    đưa vào intersectObjects()

- Click chọn thân đường vô tình kéo lệch đầu mút (PHẦN 4.5 xung đột PHẦN 4.7/4.8)
  → Kiểm tra đã giới hạn thời điểm cho phép kéo đầu mút (ví dụ chỉ ở
    flow.step === 1, trước khi bắt đầu chọn đường) — nếu không giới
    hạn, 2 hệ thống raycast (chọn thân đường vs kéo đầu mút) sẽ tranh
    nhau xử lý cùng 1 sự kiện pointerdown

- ReferenceError: "biến X is not defined" sau khi sửa code bằng str_replace/
  chỉnh tay 1 đoạn lớn
  → Đây là lỗi THỰC TẾ đã gặp khi chèn class mới ngay trước dòng khai
    báo biến — thao tác thay thế 1 đoạn text vô tình xoá luôn dòng
    khai báo nằm sát ranh giới đoạn cũ/mới. Sau MỌI lần chỉnh sửa lớn,
    BẮT BUỘC kiểm tra lại bằng cách liệt kê toàn bộ `const`/`let` cấp
    cao nhất theo số dòng (ví dụ `grep -n "^const \|^let "`) và xác
    nhận thứ tự khai báo trước-dùng-sau vẫn đúng

- ReferenceError: biến cục bộ trong 1 hàm/closure bị dùng ở 1 hàm khác
  không cùng scope (ví dụ "halfLen is not defined")
  → Hàm callback truyền vào animateBuildParallelLine() hoặc tương tự
    chỉ có quyền truy cập biến trong closure CHỨA nó, không tự động
    thấy biến cục bộ của 1 hàm top-level riêng được định nghĩa ở nơi
    khác. Nếu 1 hàm cần dữ liệu từ "ngoài", PHẢI truyền qua tham số
    hoặc tự tính lại bên trong hàm đó, không giả định biến cùng tên
    sẽ "tự nhiên có mặt"

- Trước khi gửi file cho người dùng sau bất kỳ chỉnh sửa lớn nào
  → Luôn kiểm tra cú pháp bằng cách trích nội dung <script> và chạy
    qua `new Function(scriptContent)` trong Node — bắt được lỗi cú
    pháp và biến chưa khai báo ở cấp ngoài cùng TRƯỚC khi người dùng
    mở file và gặp lỗi runtime

- Nét đứt (LineDashedMaterial) hiển thị NHƯ NÉT LIỀN, dù đã set đúng
  dashSize/gapSize
  → Kiểm tra đã gọi line.computeLineDistances() NGAY SAU khi tạo
    THREE.Line — không có cảnh báo console nào báo lỗi này, chỉ âm
    thầm vẽ sai, rất dễ bỏ qua khi review code

- Khoảng cách điểm-mặt phẳng ra số âm hoặc NaN
  → Kiểm tra đã lấy Math.abs() của "khoảng cách có dấu" (PHẦN 4.10.2)
    trước khi hiển thị — dấu của signedDist chỉ dùng để TÍNH chân
    đường vuông góc H, không dùng trực tiếp làm kết quả khoảng cách.
    NaN thường do A,B,C thẳng hàng (definePlaneFromPoints trả về null)
    mà code phía sau không kiểm tra null trước khi .normal/.pointOnPlane

- intersectionOfTwoPlanes() trả về điểm sai vị trí (giao tuyến lệch, hoặc
  điểm không nằm trên mặt phẳng nào cả — kiểm tra bằng
  `(point - plane.pointOnPlane)·plane.normal`, phải ≈ 0)
  → CÓ 2 NGUYÊN NHÂN KHÁC NHAU, cần phân biệt:
    (1) `plane.normal` chưa normalize trước khi truyền vào — hàm giả định
        n·n = 1. Nếu truyền normal thô từ crossVectors() chưa normalize,
        denom tính sai. definePlaneFromPoints() (PHẦN 4.10.1) đã gọi
        .normalize() — chỉ lỗi nếu tự tạo plane object thủ công mà quên.
    (2) LỖI CÔNG THỨC THẬT đã tồn tại trong tài liệu này tới 07/2026: dòng
        `denom = n1n2*n1n2 - 1` bị SAI DẤU, đúng phải là `1 - n1n2*n1n2`
        (định thức hệ Cramer [[1,k],[k,1]]). Lỗi này khiến điểm trả về LUÔN
        là ảnh đối xứng qua gốc toạ độ của điểm đúng — SAI NGAY CẢ KHI đã
        normalize đúng normal, không liên quan gì tới nguyên nhân (1). Đã
        sửa ở PHẦN 4.13.2 (bản trong file này) và `06_geometry_math.md`
        PHẦN A.6 (nguồn chuẩn). Nếu code đang chạy vẫn cho kết quả sai dù
        đã normalize đúng, RÀ LẠI xem bản hàm đang dùng có phải bản cũ
        (chưa sửa) không — đặc biệt nếu đã copy hàm này ra 1 file riêng
        trước 07/2026. Chi tiết phát hiện + verify:
        `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.11.

- classifyLineToPlane() báo 'parallel' cho đường nằm TRONG mặt phẳng
  → Đây là hành vi đúng nếu chỉ kiểm tra dot(dir, normal). Phải kiểm tra
    thêm bước 2: distanceTo(plane) của 1 điểm trên đường. Nếu < 1e-4 thì
    'contained', ngược lại mới là 'parallel'. Xem PHẦN 4.12 — hai trường
    hợp này có ý nghĩa sư phạm khác nhau (contained: d=0, không phải song song).

- Đường xoay bằng slider bị "nhảy" về vị trí cũ sau khi kéo tay P/Q
  → Slider dùng góc tuyệt đối so với baseP/baseQ. Sau khi học sinh kéo
    tay P hoặc Q, phải reset baseP/baseQ về vị trí hiện tại và slider
    value về 0 — nếu không, lần slider kéo tiếp theo sẽ xoay từ vị trí
    cũ (baseP/baseQ chưa cập nhật) gây nhảy vị trí đột ngột. Gọi hàm
    resetRotationBase() trong pointerup handler khi drag kết thúc.

- distanceSkewLines() trả về dist đúng nhưng H1, H2 sai vị trí
  → Kiểm tra dấu t2: công thức đúng là t2 = -(f - b*e)/denom, không phải
    t2 = (f - b*e)/denom. Dấu âm hay bị mất khi viết lại công thức tay.
    Verify bằng cách check (H2-H1).dot(d2) ≈ 0 sau khi tính.

- buildArc() vẽ cung sai phía (nửa còn lại của góc)
  → dir1 hoặc dir2 truyền vào ngược chiều. Nếu cung vẽ phần bù 180°-φ
    thay vì φ, negate 1 trong 2 dir. Kiểm tra bằng mắt: cung phải nằm
    trong khe góc cần đo, không phải phần còn lại.

- Góc nhị diện tính ra NaN
  → dihedralAngle() dùng arccos(ox·oy). Nếu ox hoặc oy chưa normalize,
    dot product có thể > 1 → arccos trả NaN. Hàm đã dùng Math.max(-1,
    Math.min(1, ...)) để clamp, nhưng nếu tự viết lại cần thêm clamp này.

- buildRightAngleMark() dấu góc vuông vẽ sai mặt phẳng
  → PHẦN 4.10.4 dùng refDir = vector trong mp (α); PHẦN 4.18 dùng refDir
    = hướng đường thẳng a. Cùng hàm nhưng ý nghĩa refDir khác nhau — đừng
    nhầm. Kiểm tra: dấu □ phải nằm trong mặt phẳng chứa cả M và đường a.

- Khối 3D hoàn toàn không hiển thị, không có lỗi console rõ ràng
  → new Function(scriptContent) trong Node KHÔNG detect được lỗi cú pháp
    nằm trong class methods hoặc lỗi thiếu 1 dòng khai báo function nếu
    phần thân hàm vẫn "trông hợp lệ" về brace-matching tổng thể. Dùng
    `node --check file.js` (sau khi trích script ra .js riêng) — đây mới
    là parser V8 đầy đủ, bắt được lỗi mà new Function() bỏ lỡ. Đây là lỗi
    THỰC TẾ đã xảy ra: 1 lần chèn 2 hàm mới trước hàm makeHitSphere() bằng
    str_replace đã vô tình xoá dòng `function makeHitSphere(...) {`, để
    lại phần thân hàm mồ côi — new Function() báo "OK" sai, chỉ
    node --check mới phát hiện `Unexpected token '}'`.

- Cạnh khuất không bao giờ hiện nét đứt, luôn hiện nét liền dù xoay góc nào
  → edgeFaceMap dùng key ghép tên đỉnh phải .sort() trước .join('-').
    Thiếu sort() khiến 'A-B' và 'B-A' thành 2 key khác nhau, mỗi cạnh bị
    coi là "cạnh biên" (faceIdxs.length <= 1) → luôn trả visible=true.

- Kéo EXPLORE bị giật/lag rõ rệt, đặc biệt với khối nhiều mặt
  → Đang gọi lại solidRenderer.load() (rebuild toàn bộ mesh) mỗi frame
    trong pointermove, thay vì rebuildFromVertices() (chỉ ghi buffer).
    load() dispose + tạo mới tất cả geometry/material — quá nặng cho
    60fps. rebuildFromVertices() chỉ set lại position attribute.

- Sau khi kéo EXPLORE, mesh đứng im không di chuyển dù vertices đã đổi
  → Thiếu dòng `posAttr.needsUpdate = true` sau khi setXYZ() vào buffer
    attribute. Three.js không tự phát hiện buffer đã bị ghi đè, phải báo
    thủ công. Đây khác geometry.setFromPoints() (tự động flag update).

- Click vào giữa mặt tam giác vẫn bị nhận nhầm thành click cạnh
  → Hit-cylinder của cạnh bán kính quá lớn (r ≥ 0.11) che mất vùng gần
    cạnh của mặt. Thu nhỏ về r ≈ 0.07 và set raycaster.params.Line.threshold
    nhỏ nếu cần — xem PHẦN 7.9.

- Xoay/zoom camera nhẹ cũng bị hiểu thành "click thêm điểm" ở mode ĐIỂM
  → Thiếu bước phân biệt click vs drag bằng khoảng cách di chuyển chuột
    (PHẦN 7.8, CLICK_MAX_DIST). Không thể chỉ dựa vào pointerdown/pointerup
    liên tiếp vì OrbitControls cũng phát pointerdown/pointerup khi xoay.

- Chuyển từ khối đa diện sang khối tròn xoay → khối đa diện cũ hiện đè lên
  → setMode() viết cho hệ đa diện gọi solidRenderer.rebuildGeometry() vô
    điều kiện mỗi lần đổi mode. loadRoundSolid() gọi setMode('view') ở cuối
    → rebuild chạy lại với currentSolidKey CŨ. Phải thêm cờ isRoundActive
    và guard MỌI logic đọc/rebuild solidRenderer bằng cờ này — xem PHẦN 9.4.
    Đặt isRoundActive = true TRƯỚC khi gọi setMode(), không phải sau.

- Vòng tròn viền khối trụ/nón vẽ ra hình "múi bưởi" nhiều đường chằng chịt
  → Dùng THREE.EdgesGeometry trên CylinderGeometry/ConeGeometry sẽ vẽ hết
    các đường chia lưới radialSegments, không phải chỉ 2 vòng tròn viền như
    hình SGK. Phải tự tham số hoá vòng tròn bằng vòng lặp cos/sin — xem
    PHẦN 9.2. Không có cách nào lọc riêng "đường viền" từ EdgesGeometry của
    geometry cong.

- Kéo 1 điểm bằng raycast intersectObject() gần như không phản hồi, hoặc
  chỉ thỉnh thoảng mới "bắt" được — cảm giác như "không kéo được"
  → Hitbox (mesh vô hình dùng để raycast) quá nhỏ so với khoảng cách
    camera thực tế đang dùng trong bài. Bán kính hiển thị đẹp về mặt
    thẩm mỹ (VD 0.09-0.15) gần như luôn quá nhỏ để click trúng chính
    xác — LUÔN tách hit-area riêng, lớn hơn đáng kể (0.28 trở lên, có
    thể cần 0.4-0.55 nếu camera đặt xa khối lớn), theo đúng pattern
    PHẦN 1.1. Nếu vẫn khó bắt trúng sau khi tăng hitbox, thêm
    `depthTest: false` + `renderOrder` cao cho vật liệu hitbox để đảm
    bảo nó luôn được raycast/render ưu tiên, không bị mesh khác (khối
    đặc, mặt phẳng mờ) che khuất tia click.

- Điểm ràng buộc trượt DỌC 1 CẠNH (không dùng ConstrainedPoint sẵn có mà
  tự viết raycast-to-line riêng) chỉ kéo được về 1 hướng, hướng còn lại
  gần như đứng yên hoặc bị "kẹp cứng" ở 1 đầu bất kể kéo thế nào
  → LỖI THỰC TẾ: công thức "điểm gần nhau nhất giữa tia chuột và đường
    thẳng" (closest point between 2 lines/rays) rất dễ SAI DẤU khi viết
    tay — cụ thể vector `w0` phải là `(rayOrigin - linePoint)`, viết
    nhầm thành `(linePoint - rayOrigin)` khiến tham số t tính ra bị
    NGƯỢC DẤU hoàn toàn. Nếu sau đó code có `Math.max(min, Math.min(max,
    t))` để giới hạn t trong khoảng hợp lệ, giá trị âm/lệch dấu đó lập
    tức bị kẹp cứng về biên ngay từ đầu, tạo cảm giác "kéo 1 chiều không
    được" dù bản chất là lỗi dấu chứ không phải lỗi giới hạn. VERIFY
    bằng round-trip test trong Node: giả lập 1 điểm THẬT trên đường
    (biết trước t), dựng ray từ 1 vị trí camera giả định hướng thẳng
    tới điểm đó, chạy công thức ngược lại xem t tính ra có khớp t đã
    biết không — nếu lệch dấu, round-trip sẽ lộ ra ngay (t tính ra
    ngược dấu hoặc lệch hẳn), không cần đoán mò qua nhiều lần sửa code
    rồi test lại trên trình duyệt.

- Nút bấm / ô nhập liệu trong 1 panel overlay (VD #hud) HOÀN TOÀN KHÔNG
  PHẢN HỒI CLICK, không có lỗi Console, code JS test độc lập vẫn đúng
  → Panel đó có `pointer-events: none` sót lại từ thời chỉ hiển thị
    text (để chuột "xuyên qua" xuống canvas 3D), quên gỡ khi nâng cấp
    thêm input/button thật. Lỗi này xảy ra ở tầng browser xử lý sự
    kiện chuột, TRƯỚC KHI JS chạy — không bắt được bằng Console hay
    Node/jsdom, chỉ lộ ra khi click thật trên trình duyệt. Chi tiết đầy
    đủ + quy trình debug: xem `01_scenario_builder_3d_addendum.md`
    PHỤ LỤC E.9.

- Hàm vẽ nhiều đỉnh (VD mesh thiết diện 4 đỉnh) vẫn vẽ SAI dù đã sửa
  đúng thứ tự đỉnh ở lời gọi hàm và ở phần thân hàm
  → Chữ ký hàm khai báo TÊN THAM SỐ sai thứ tự, ví dụ
    `function rebuildMesh(M, N, Q, P, ...)` thay vì `(M, N, P, Q, ...)`.
    JS truyền đối số theo vị trí, nên 2 giá trị bị tráo ngay từ đầu vào
    dù thân hàm "trông như đã đúng". Khi sửa lỗi thứ tự 1 bộ đỉnh dùng ở
    nhiều nơi, phải grep kiểm tra ĐỒNG THỜI cả chữ ký hàm, lời gọi, và
    mọi hàm phụ trợ khác dùng cùng bộ đỉnh đó — không chỉ sửa 1 chỗ rồi
    tin đã xong. Chi tiết đầy đủ: xem `01_scenario_builder_3d_addendum.md`
    PHỤ LỤC E.10.

- intersectionOfTwoPlanes() SAI dù đã normalize đúng plane.normal
  → Xem mục riêng phía trên (2 nguyên nhân khác nhau) — đây là lỗi CÔNG
    THỨC trong chính tài liệu này (denom sai dấu), không phải lỗi dùng
    sai hàm. Đã sửa ở PHẦN 4.13.2 07/2026. Chi tiết:
    `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.11.

- 1 chuỗi tương tác (kéo-thả, click-to-select...) tự nhiên NGỪNG hoạt
  động sau khi chuyển qua bước/scene khác rồi quay lại — không lỗi
  Console, mọi phần tử vẫn hiển thị đúng
  → Event listener (`click`, `pointerdown`...) gắn vào 1 phần tử DÙNG
    CHUNG cho nhiều bước/module (VD `canvas` hoặc `window`) nhưng KHÔNG
    được gỡ (`removeEventListener`) khi chuyển sang bước/module khác —
    listener cũ vẫn tồn tại, tranh chấp hoặc gọi nhầm logic đã lỗi thời
    của bước trước. Với file nhiều bước/nhiều "trạm" trong 1 canvas dùng
    chung (kiểu game nhiều màn), BẮT BUỘC theo pattern: lưu tham chiếu
    handler đang active vào 1 biến toàn cục (VD `window.__activeClickHandler`),
    gỡ handler cũ TRƯỚC khi gắn handler mới mỗi lần vào 1 bước/trạm:
    ```javascript
    if (window.__activeClickHandler) {
      canvas.removeEventListener('click', window.__activeClickHandler);
    }
    canvas.addEventListener('click', newHandler);
    window.__activeClickHandler = newHandler;
    ```
    Áp dụng tương tự cho mọi listener gắn vào `window`/`document` dùng
    chung qua nhiều bước (không chỉ `canvas`).

- Gọi `someArray.push()` (quên truyền tham số) để "đánh dấu" 1 phần tử
  không nằm trong 1 nhóm dùng chung (VD nhóm mesh dùng cho raycast
  kéo-thả) — về sau raycast/loop qua mảng đó lỗi khó hiểu hoặc bỏ sót
  → `push()` không tham số đẩy `undefined` vào mảng — nếu mảng đó được
    dùng làm input cho `raycaster.intersectObjects(array)` hay tương tự,
    phần tử `undefined` có thể gây lỗi runtime hoặc hành vi không xác
    định tuỳ engine. Nếu chỉ muốn "không thêm phần tử này vào nhóm X vì
    nó thuộc nhóm khác", ĐỪNG gọi `push()` rỗng làm placeholder — chỉ
    đơn giản KHÔNG gọi `push()` ở nhánh đó, kèm 1 dòng comment giải
    thích tại sao (để người đọc sau không tưởng bị quên).

- Trang hiện đúng ảnh/tĩnh nhưng MỌI nút/tương tác đều "đơ" hoàn toàn,
  không có lỗi gì hiện ra màn hình (chỉ thấy trong DevTools Console nếu
  mở lên)
  → Kiểm tra Console trước tiên — nếu thấy lỗi tải script (VD 404 từ
    CDN do sai định dạng URL, ví dụ dùng `.../three.js/0.128.0/...`
    trong khi cdnjs đặt tên thư mục phiên bản là `.../three.js/r128/...`),
    lệnh khởi tạo phụ thuộc thư viện đó (VD `new THREE.OrbitControls(...)`)
    sẽ ném lỗi ngay khi script chạy, dừng cứng TOÀN BỘ phần code phía
    sau trong cùng file — kể cả code không liên quan gì tới thư viện đó.
    Vì HTML/CSS đã render xong trước khi script chạy, người dùng thấy
    đúng giao diện tĩnh (kể cả giá trị mặc định viết cứng trong HTML)
    nhưng không nút nào phản hồi. THÊM 1 guard đầu script để tránh lặp
    lại: `if (typeof THREE === 'undefined') { hiện thông báo lỗi rõ
    ràng lên màn hình; throw ...; }` — không để lỗi tải tài nguyên gây
    "đơ im lặng" không dấu vết.

- 1 hàm dùng `document.getElementById('tên-id')` trả về `null` dù chắc
  chắn phần tử đó "có trong HTML", gây lỗi tiếp theo kiểu
  `Cannot set properties of null (setting 'textContent')` — LỖI NÀY CÓ
  THỂ LÀM DỪNG CỨNG TOÀN BỘ HÀM đang chạy tại đúng dòng đó, mọi code sau
  dòng lỗi (kể cả hiện overlay tổng kết, load leaderboard...) không bao
  giờ chạy
  → Kiểm tra thẻ HTML có bị viết TRÙNG 2 THUỘC TÍNH `id` khác nhau trên
    CÙNG 1 THẺ không, ví dụ:
    ```html
    <div id="ending-stat" id="final-rank-line">Rank: —</div>
    ```
    HTML không hợp lệ — trình duyệt chỉ giữ giá trị ĐẦU TIÊN
    (`ending-stat`), bỏ qua giá trị sau, nên `getElementById('final-
    rank-line')` trả về `null`. Đây thường xảy ra khi 1 thẻ vừa cần 1
    `id` riêng để JS truy cập, vừa cần style dùng chung với các thẻ
    khác — SỬA bằng cách dùng `class` cho style dùng chung, giữ `id`
    riêng biệt duy nhất cho mục đích JS:
    ```html
    <div class="ending-stat" id="final-rank-line">Rank: —</div>
    ```
    Sau khi sửa 1 chỗ, RÀ LẠI TOÀN FILE bằng regex tìm mọi thẻ có ≥2
    thuộc tính `id` (`grep -n 'id="[^"]*"[^>]*id="'`) — lỗi này thường
    xảy ra lặp lại ở nhiều thẻ tương tự nếu do copy-paste 1 khối HTML.
```

---

> **Phiên bản:** 10.0
> **Cập nhật:** 07/2026 — bổ sung PHẦN 8 hạ đường cao từ điểm xuống mặt
> phẳng (baseVertices field 8.1, tính plane không cache mỗi frame 8.2, luồng
> chọn nguồn→đích qua sidebar 8.3, geometry cập nhật không dispose 8.4) và
> PHẦN 9 khối tròn xoay hoàn toàn mới — RoundSolidRenderer không dùng
> vertices/edges/faces (9.1), vòng viền tham số hoá thay EdgesGeometry (9.2),
> điểm tham chiếu tĩnh không qua pointPool (9.3), dispatch 2 renderer với cờ
> isRoundActive (9.4), CATALOG với cờ round (9.5). Thêm 2 lỗi mới trong Phụ
> lục — đáng chú ý: thứ tự set cờ isRoundActive TRƯỚC khi gọi setMode().
> **Cập nhật 07/2026 (v8.0):** thêm PHẦN 2.5 (điểm ràng buộc trên mặt
> phẳng) và PHẦN 4.20 (occlusion tự động). Thêm 3 bài học vào Phụ lục
> lỗi thường gặp: dispose Group nhiều children, hitbox quá nhỏ, sai dấu
> công thức closest-point-between-2-lines.
> **Cập nhật 07/2026 (v9.0):** thêm 2 mục vào Phụ lục lỗi hay gặp —
> `pointer-events: none` chặn click và tráo tham số qua chữ ký hàm.
> Cả 2 lỗi này KHÔNG bắt được bằng `node --check` hay verify Node độc
> lập, chỉ lộ ra khi người dùng thật thao tác trên trình duyệt — xem
> tường thuật đầy đủ ở `01_scenario_builder_3d_addendum.md` PHỤ LỤC E.9–E.10.
> **Cập nhật 07/2026 (v10.0) — QUAN TRỌNG:** sửa lỗi công thức thật trong
> PHẦN 4.13.2 `intersectionOfTwoPlanes` (denom sai dấu — xem `06_geometry_
> math.md` PHẦN A.6 là nguồn chuẩn, PHỤ LỤC E.11 trong addendum). Thêm
> PHẦN 2.6 (điểm ràng buộc xoay trên cung tròn quanh 1 trục cố định/bản
> lề — tái dùng nguyên lý `rotateLineAroundNormal` PHẦN 4.14, kết hợp
> `atan2` để suy góc từ điểm kéo thô). Thêm 4 mục vào Phụ lục lỗi hay
> gặp: mở rộng mục intersectionOfTwoPlanes (2 nguyên nhân khác nhau),
> event listener không gỡ khi chuyển bước/scene, `push()` rỗng đẩy
> `undefined` vào mảng dùng chung, và trùng thuộc tính `id` trên 1 thẻ
> HTML khiến `getElementById` trả `null` (dừng cứng cả hàm đang chạy tại
> đúng dòng đó, không có cảnh báo Console rõ ràng). Cả 4 lỗi phát hiện
> khi build + sửa qua nhiều vòng test thật với người dùng cho game "Đền
> thờ Euclid" — xem tường thuật đầy đủ ở PHỤ LỤC E.11–E.13 trong addendum.
> **Nguồn:** Rút ra từ test_drag_3d.html, test_click_select_angle.html,
> test_parallel_construction.html, test_point_plane_distance.html,
> test_b_parallel.html, test_c_angles.html, test_d_distances.html,
> solid_demo.html, solid_library.html, prototype1-5 (Bài 10 Simulation 2
> và game Đền thờ Euclid, 07/2026) — mọi pattern trong file này đã chạy
> thật và verify, không phải lý thuyết chưa kiểm chứng.
> **Dùng cùng:** `04_design_toan_3d.md` (UI/UX) + `06_geometry_math.md` (hàm toán thuần)
> **Cập nhật thêm (07/2026):** `06_geometry_math.md` đã được viết — toàn bộ
> hàm toán thuần tham chiếu trong file này (definePlaneFromPoints,
> projectPointOntoPlane, distanceSkewLines, dihedralAngle, barycentricCoords,
> rotateLineAroundNormal, và bộ tham số hoá mặt cong cho khối tròn xoay) giờ
> có 1 nguồn duy nhất, không còn ghi chú "chưa viết".
> **Cập nhật 08/2026 (v11.0):** thêm PHẦN 7.4-BIS — KÉO CẢ KHỐI (rigid group
> drag), phục vụ Bài 22 Module 2 Tab 1b (3 kim tự tháp thật kéo dịch được).
> Khác PHẦN 1 (kéo điểm) và PHẦN 7.4 (kéo đỉnh biến dạng khối) — ở đây kéo
> nguyên 1 `THREE.Group` không đổi hình dạng, ràng buộc mặt đất `y=0`, có
> snap lưới + chống đè nhau. ⚠️ **CHƯA VERIFY bằng file HTML thật** — pattern
> mới viết dựa trên nguyên lý đã có (billboard-plane 1.2, ràng buộc 'floor'
> 7.4) áp ở cấp Group; bắt buộc prototype nhỏ trước khi build chính thức,
> theo đúng quy trình E (addendum).
> **Cập nhật 08/2026 (v12.0):** thêm PHẦN 2.7 — XOAY QUANH BẢN LỀ ĐỨNG
> (cung quét mặt phẳng ngang, dùng `atan2` không ép dấu) và PHẦN 2.8 —
> NÓN CÁC HƯỚNG VUÔNG GÓC VỚI 1 ĐƯỜNG CHO TRƯỚC (kết hợp
> `arbitraryPerpendicular` 06 PHẦN C.4 + `rotateLineAroundNormal` 4.14.1
> đã có) — phục vụ Bài 23 (cửa tủ quần áo, cần cẩu tháp, cột đèn bẫy sai
> lầm D). ⚠️ Sửa lại 1 lỗi trích dẫn: kịch bản Bài 23 ban đầu trích PHẦN
> 2.6 cho cửa tủ/cần cẩu, nhưng 2.6 là bản lề NGANG/cung ĐỨNG (dùng
> `Math.max(0.2,y)` ép góc trong khoảng ~±90°) — không đủ cho cửa tủ cần
> mở tới 170° hay cần cẩu xoay đủ vòng. PHẦN 2.7 mới là bản lề ĐỨNG/cung
> NGANG, dùng đúng cho 2 ca này. CẢ 2 PHẦN MỚI CHƯA VERIFY bằng file HTML
> thật (đã verify công thức bằng Python) — bắt buộc prototype trước khi
> build.
> **Cập nhật 08/2026 (v13.0):** thêm PHẦN 2.9 — TỊNH TIẾN THEO QUỸ ĐẠO,
> GIỮ NGUYÊN HƯỚNG (không tự xoay theo vị trí) — phục vụ Bài 24 Module 2
> Phần 4 (Trái Đất quay quanh Mặt Trời, trục nghiêng giữ phương cố định).
> Khác hẳn mọi pattern xoay-quanh-trục đã có (2.6, 2.7, 4.14.1) — ở đây
> KHÔNG xoay vật theo tham số, chỉ tịnh tiến vị trí, hướng gắn với vật giữ
> nguyên từ lúc khởi tạo. Đã verify công thức bằng Node (three thật qua
> npm) — góc trục/mặt phẳng quỹ đạo giữ đúng 66,5° ở mọi vị trí test.
> ⚠️ CHƯA verify bằng file HTML thật, và có 1 bẫy code hay gặp đã ghi chú
> riêng (tránh gọi `lookAt()` nhầm làm trục tự xoay theo vị trí).
> **Cập nhật 08/2026 (v14.0):** thêm PHẦN 2.10 — KHUNG XOAY LỒNG NHAU
> (GIMBAL), dùng kỹ thuật counter-rotation (nghịch đảo tích quaternion cha)
> để giữ hướng vật bên trong cố định dù khung ngoài xoay — phục vụ Module
> mở rộng Tab 3 (con quay hồi chuyển). Đã verify công thức bằng Node (5 tổ
> hợp góc, world direction luôn giữ nguyên). Và PHẦN 2.11 — OVERLAY 2D ĐỘC
> LẬP VỚI SCENE 3D (màn hình radar dạng CSS/HTML riêng, chỉ đồng bộ ở mốc
> sự kiện rời rạc, không đồng bộ animation-frame-by-frame) — phục vụ Bài
> 24 Module 3 Domain 3. Cả 2 PHẦN MỚI CHƯA verify bằng file HTML thật.
> **Cập nhật 08/2026 (v15.0):** thêm PHẦN 2.12 — DỰNG KINH TUYẾN/VĨ
> TUYẾN TRÊN HÌNH CẦU dùng `THREE.EllipseCurve` (core, không cần thư
> viện thêm) — phục vụ Lab Bài 25, cảnh "Trái Đất & Kinh tuyến". Gồm
> `createMeridianLine` (nửa đường tròn lớn, cực Nam→cực Bắc, tại 1 kinh
> độ) và `createLatitudeCircle` (đường tròn đầy đủ tại 1 vĩ độ, xích đạo
> là ca đặc biệt vĩ độ=0°), cùng cách cập nhật động khi kéo slider kinh
> độ. Đã verify bằng Node (three thật qua npm): góc giữa kinh tuyến
> gốc/45° tại xích đạo = đúng 45,0000°; vĩ tuyến 30° khớp đúng bán kính
> và độ cao lý thuyết. ⚠️ CHƯA verify bằng file HTML thật.
> **Cập nhật 08/2026 (v16.0):** thêm PHẦN 2.13 — MỰC NƯỚC DÂNG DẦN
> TRONG KHỐI RỖNG (3D) — phục vụ Bài 27 Module 1 Bước 2 (thí nghiệm đong
> nước chóp/lăng trụ). KHÔNG viết từ đầu — chuyển thể trực tiếp từ thư
> viện Vật Lý `04a_nhiet_hoc.md` (`animateCalorimeter`/`animateBoiling`,
> 2D Canvas) sang lưới `PlaneGeometry` 3D, giữ nguyên công thức sin tạo
> gợn sóng. Tái dùng THẲNG `Ease`/`lerp` từ `04d_daodong_helpers.md`
> (thuần toán, không phụ thuộc Canvas). Thêm công thức riêng cho ca khối
> CHÓP (tiết diện co theo tỉ lệ (H−y)/H, khác lăng trụ tiết diện không
> đổi). Đã verify bằng Node: tỉ lệ tiết diện khớp đúng ở 7 mốc chiều
> cao; Ease/lerp cho fillRatio tăng mượt đúng 0→1. ⚠️ CHƯA verify bằng
> file HTML thật, và phần "trút nước giữa 2 khối" cần thêm 1 lớp
> animation riêng (gợi ý: quả cầu nhỏ rơi + đồng thời đổi fillRatio 2
> bên) — chưa thiết kế chi tiết.
> **Cập nhật 08/2026 (v17.0):** thêm PHẦN 2.14 — ANIMATION "TRÚT NƯỚC"
> GIỮA 2 KHỐI, đặc tả ĐẦY ĐỦ (không để ngỏ cho đội build tự quyết, theo
> yêu cầu giảm rủi ro) — dòng hạt nước bay theo cung Bezier bậc 2 (chọn
> thay cho mô phỏng nghiêng bình vật lý thật — rủi ro thấp hơn hẳn),
> đồng bộ 3 lớp trong 1 hàm điều phối duy nhất `runOnePour`: mực nước
> chóp giảm (PHẦN 2.13.3), mực nước lăng trụ tăng đúng 1/3 mỗi lần đổ,
> và dòng hạt nước spawn liên tục. Đã verify bằng Node: quỹ đạo cung
> đúng hình dạng kỳ vọng, 3 lần đổ liên tiếp cho lăng trụ đúng
> 0→1/3→2/3→1. ⚠️ CHƯA verify bằng file HTML thật.
> ⚠️ **v16.0 và v17.0 ở trên ĐÃ ĐƯỢC THAY THẾ HOÀN TOÀN bởi v18.0 ngay
> dưới đây** — sau khi build prototype HTML thật và nhận phản hồi hình
> ảnh trực tiếp qua 4 vòng sửa, cách làm mô tả ở v16/v17 (mặt phẳng scale
> giả lập mực nước, dòng hạt cầu bay theo cung nhô lên, 2 khối đứng cố
> định cách xa) đều bị bỏ. Giữ lại 2 mục changelog cũ này chỉ để LƯU VẾT
> lịch sử, KHÔNG dùng làm tài liệu triển khai — nội dung PHẦN 2.13, 2.14
> trong file (đã cập nhật) phản ánh đúng bản v18.0.
> **Cập nhật 08/2026 (v18.0) — VIẾT LẠI HOÀN TOÀN PHẦN 2.13 + 2.14 sau
> khi test prototype HTML thật qua 4 vòng phản hồi hình ảnh trực tiếp:**
> (1) Đổi cơ chế mực nước từ "mặt phẳng scale giả lập" sang "khối đặc +
> clipping plane" thật. (2) Phát hiện + sửa 2 lỗi Three.js kinh điển:
> `DoubleSide` làm tường bình "xám đục" (→ đổi `FrontSide`), `depthWrite`
> mặc định `true` khiến vật trong suốt che nhau (→ set `false` + thêm
> `renderOrder` rõ ràng). (3) Bỏ hẳn "mặt cap" trên container CHÓP/NGHIÊNG
> (gây hình chồng chéo giả) — chỉ dùng cap cho container tiết diện cố
> định, không nghiêng (lăng trụ). (4) Bỏ hẳn dòng hạt cầu rời rạc (gây
> cảm giác "bắn pháo hoa") — đổi sang 1 dòng `TubeGeometry` liên tục,
> cung Bezier VÕNG XUỐNG (đúng trọng lực, không nhô lên). (5) Container
> giờ NGHIÊNG THẬT quanh 1 pivot (2 Group lồng nhau) VÀ DI CHUYỂN lại gần
> mục tiêu trong lúc nghiêng (không đứng cố định cách xa) — quỹ đạo rơi
> ngắn, gần thẳng đứng, đúng cảm giác rót thật. Đã verify bằng Node
> (nhiều lượt) VÀ bằng prototype HTML thật chạy trên trình duyệt qua
> nhiều vòng chỉnh sửa dựa trên phản hồi hình ảnh trực tiếp.
> **Cập nhật 08/2026 (v19.0):** thêm PHẦN 2.15 — KHAI TRIỂN PHẲNG KHỐI
> CHÓP CỤT ĐỀU (gấp/mở lưới phẳng) — phục vụ Bài 27 Module 2 Bước 3
> (khuôn bánh cô Mai, TUỲ CHỌN — không bắt buộc build). Tái dùng 2 kỹ
> thuật đã có: xoay quanh bản lề (PHẦN 2.6/2.7) áp cho 4 mặt bên đồng
> thời + cách tính góc dựa trên toạ độ tương đối. Phát hiện + sửa 1 lỗi
> thật: quy tắc dấu xoay KHÁC NHAU giữa bản lề trục x và trục z (dùng 1
> dấu cố định cho cả 4 mặt khiến 2 mặt gập lộn xuống dưới sàn) — công
> thức đúng: `rotSign = hingeSign` cho trục z, `rotSign = -hingeSign`
> cho trục x. Đã verify bằng Node (4 mặt, 3 mốc progress) VÀ bằng
> prototype HTML thật (slider + tự động gấp/mở, qua bài kiểm tra thực
> thi mô phỏng DOM, không lỗi runtime).
