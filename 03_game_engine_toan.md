# 🎮 GAME ENGINE — Simulation Tương Tác & Vật Lý

> **Mục đích:** Patterns kỹ thuật cho simulation game-based — input, feedback, physics, isometric
> **Dùng kèm:** `01_scenario_builder.md` + `02_design_ly.md`
> **Đọc file này khi:** Làm game tương tác / drag & drop / vật lý / hình học không gian
> **Hệ thiết kế:** Toàn bộ màu sắc trong file này đã đồng bộ với `Quy_chuan_tao_HTML_Aiducation.pdf`
> (Haugomat editorial flat) và bảng vector ở `02_design_ly.md` mục 1.2. Các pattern kỹ thuật thuần
> (hit detection, drag & drop, state machine, RAF) không đổi vì không liên quan màu sắc.

---

## 🤖 TRIGGER — AI ĐỌC FILE NÀY KHI NÀO

Đọc toàn bộ file này khi kịch bản có bất kỳ từ khoá sau:
- **Input:** "kéo thả", "drag", "click chọn", "gắn vào", "thả vào"
- **Physics:** "lực", "vận tốc", "gia tốc", "mặt phẳng nghiêng", "chuyển động"
- **3D/Iso:** "hình học không gian", "hình hộp", "hình chóp", "3 chiều", "isometric"
- **Game:** "level", "mission", "score", "unlock", "game"

Chỉ đọc **PHẦN 4** khi có từ khoá về lực/vật lý.
Chỉ đọc **PHẦN 5** khi có từ khoá về 3D/không gian.
Toàn bộ màu dùng trong file: tra token ở `02_design_ly.md` PHẦN 1 — không tự thêm hex mới.

---

## PHẦN 1 — INPUT PATTERNS

> Đây là nguồn gốc của 80% lỗi trong simulation tương tác.
> Áp dụng đúng các pattern này trước khi viết bất kỳ logic game nào.

### 1.1 Hit Detection — Điểm chạm đường thẳng (BẮT BUỘC)

```javascript
// ❌ SAI — dùng distance point-to-point (Stage 3 bài Vector bị lỗi vì cách này)
const d = Math.sqrt((mx - vec.x)**2 + (my - vec.y)**2);

// ✅ ĐÚNG — distance from point to line SEGMENT
function hitSegment(mx, my, x1, y1, x2, y2, tolerance = 12) {
  const dx = x2 - x1, dy = y2 - y1;
  const lenSq = dx*dx + dy*dy;
  if (lenSq === 0) return Math.sqrt((mx-x1)**2 + (my-y1)**2) < tolerance;
  const t = Math.max(0, Math.min(1, ((mx-x1)*dx + (my-y1)*dy) / lenSq));
  const cx = x1 + t*dx, cy = y1 + t*dy;
  return Math.sqrt((mx-cx)**2 + (my-cy)**2) < tolerance;
}

vectors.forEach((v, i) => {
  if (hitSegment(mx, my, v.x1, v.y1, v.x2, v.y2, 14)) {
    hit = i;
  }
});

// Với vectơ-không (điểm): dùng hit circle
function hitCircle(mx, my, cx, cy, r = 14) {
  return Math.sqrt((mx-cx)**2 + (my-cy)**2) < r;
}
```

### 1.2 Drag & Drop từ Palette vào Canvas (BẮT BUỘC)

```
Nguyên nhân lỗi Stage 4 bài Vector: không có ghost vector,
pickup zone quá nhỏ, không cancel khi mouseleave.

Pattern đúng — 5 bước:
  1. mousedown → check hitbox palette items → set dragState
  2. mousemove → cập nhật dragPos → vẽ ghost (semi-transparent)
  3. Highlight drop zone khi ghost đủ gần
  4. mouseup → check drop zone → snap hoặc reject + feedback
  5. mouseleave canvas → cancel drag
```

```javascript
// ── STATE ──────────────────────────────────────────────
let drag = {
  active: false,
  item: null,
  pos: {x:0, y:0},
  origin: {x:0, y:0}
};

// ── PALETTE ITEMS (màu lấy từ bảng vector 02_design_ly.md 1.2) ──
// Mỗi item có: {id, cx, cy, radius, label, color, data}
const palette = [
  {id:'p', cx:0, cy:0, radius:32, label:'P⃗', color: VEC.P.color, data:{type:'weight'}},
  {id:'f', cx:0, cy:0, radius:32, label:'F⃗', color: VEC.F.color, data:{type:'lift'}},
];
// cx/cy được tính trong draw() theo CW/CH — không hardcode

// ── DROP ZONES (vùng chấp nhận thả) ────────────────────
const dropZones = [
  {id:'object', cx:0, cy:0, radius:55, label:'Thả vào đây'}
];

// ── EVENT HANDLERS ──────────────────────────────────────
canvas.addEventListener('mousedown', e => {
  const {mx, my} = getPos(e);
  for (const item of palette) {
    if (!item.placed && hitCircle(mx, my, item.cx, item.cy, item.radius)) {
      drag = {active:true, item, pos:{x:mx,y:my}, origin:{x:item.cx,y:item.cy}};
      canvas.style.cursor = 'grabbing';
      return;
    }
  }
});

canvas.addEventListener('mousemove', e => {
  const {mx, my} = getPos(e);
  if (drag.active) {
    drag.pos = {x:mx, y:my};
    dropZones.forEach(z => {
      const d = Math.sqrt((mx-z.cx)**2 + (my-z.cy)**2);
      z.highlighted = d < z.radius + 20;
    });
    draw();
    return;
  }
  const hovering = palette.some(p => !p.placed && hitCircle(mx, my, p.cx, p.cy, p.radius));
  canvas.style.cursor = hovering ? 'grab' : 'default';
});

canvas.addEventListener('mouseup', e => {
  if (!drag.active) return;
  const {mx, my} = getPos(e);
  let dropped = false;
  for (const zone of dropZones) {
    const d = Math.sqrt((mx-zone.cx)**2 + (my-zone.cy)**2);
    if (d < zone.radius) {
      onDrop(drag.item, zone);
      dropped = true;
      break;
    }
  }
  if (!dropped) onDropFail(drag.item);
  drag.active = false;
  canvas.style.cursor = 'default';
  draw();
});

canvas.addEventListener('mouseleave', () => {
  if (drag.active) {
    drag.active = false;
    draw();
  }
});

// ── TOUCH SUPPORT (học sinh iPad) ──────────────────────
function touchToMouse(e) {
  e.preventDefault();
  const touch = e.touches[0] || e.changedTouches[0];
  const rect = canvas.getBoundingClientRect();
  return {
    clientX: touch.clientX - rect.left,
    clientY: touch.clientY - rect.top
  };
}
canvas.addEventListener('touchstart', e => canvas.dispatchEvent(
  new MouseEvent('mousedown', touchToMouse(e))), {passive:false});
canvas.addEventListener('touchmove', e => canvas.dispatchEvent(
  new MouseEvent('mousemove', touchToMouse(e))), {passive:false});
canvas.addEventListener('touchend', e => canvas.dispatchEvent(
  new MouseEvent('mouseup', touchToMouse(e))), {passive:false});

// ── VẼ GHOST khi đang kéo ──────────────────────────────
function drawGhost(ctx) {
  if (!drag.active) return;
  ctx.save();
  ctx.globalAlpha = 0.65;
  drawPaletteItem(ctx, drag.item, drag.pos.x, drag.pos.y);
  ctx.globalAlpha = 1;
  ctx.restore();
}

// ── HELPER ─────────────────────────────────────────────
function getPos(e) {
  const rect = canvas.getBoundingClientRect();
  return {mx: e.clientX - rect.left, my: e.clientY - rect.top};
}
```

### 1.3 Kéo Điểm Cuối Vector (Rotate + Scale)

> **Cập nhật:** đổi từ `mousedown/mousemove/mouseup` sang **Pointer Events**
> (`pointerdown/pointermove/pointerup`) — bản `mouse*` cũ không đảm bảo chạy đúng trên thiết bị
> cảm ứng (một số trình duyệt mobile giả lập sự kiện chuột không nhất quán, dễ bị cuộn trang đè
> lên thao tác kéo). Pointer Events chạy đúng cho cả chuột lẫn chạm bằng cùng 1 bộ handler.

```javascript
// Dùng cho Stage 2 bài Vector — kéo endpoint để xoay và co giãn
// vecB = {x1, y1, x2, y2} — chỉ x2/y2 di chuyển được

let vecDrag = null; // 'end' | 'body' | null
let _dragOffX, _dragOffY;

canvas.style.touchAction = 'none'; // chặn cuộn trang khi đang kéo trên canvas

canvas.addEventListener('pointerdown', e => {
  const {mx, my} = getPos(e);
  const HANDLE = 16;

  if (dist(mx, my, vecB.x2, vecB.y2) < HANDLE) {
    vecDrag = 'end'; canvas.setPointerCapture(e.pointerId); return;
  }
  const midX = (vecB.x1+vecB.x2)/2, midY = (vecB.y1+vecB.y2)/2;
  if (dist(mx, my, midX, midY) < 28) {
    vecDrag = 'body';
    _dragOffX = mx - vecB.x1;
    _dragOffY = my - vecB.y1;
    canvas.setPointerCapture(e.pointerId);
    return;
  }
});

canvas.addEventListener('pointermove', e => {
  if (!vecDrag) return;
  const {mx, my} = getPos(e);
  if (vecDrag === 'end') {
    vecB.x2 = mx; vecB.y2 = my;
  } else if (vecDrag === 'body') {
    const dx = vecB.x2 - vecB.x1, dy = vecB.y2 - vecB.y1;
    vecB.x1 = mx - _dragOffX; vecB.y1 = my - _dragOffY;
    vecB.x2 = vecB.x1 + dx;  vecB.y2 = vecB.y1 + dy;
  }
  draw();
});

canvas.addEventListener('pointerup', () => { vecDrag = null; });
canvas.addEventListener('pointercancel', () => { vecDrag = null; });

function dist(ax,ay,bx,by){return Math.sqrt((ax-bx)**2+(ay-by)**2);}
function vecAngle(v){return Math.atan2(v.y2-v.y1, v.x2-v.x1);}
function vecLen(v){return dist(v.x1,v.y1,v.x2,v.y2);}
```

### 1.4 Kéo Tới Đích + Snap Tolerance (kiểm tra nghiệm bằng kéo thả)

> Dùng khi bài yêu cầu học sinh **tự tạo ra 1 vector/điểm cụ thể** bằng cách kéo (khác 1.3 — 1.3
> là xoay/co giãn tự do không có đích, còn đây có 1 giá trị đúng để kiểm tra khớp hay chưa).
> **Kết hợp bắt buộc với Mục 2.5 (không auto-advance)** — khi khớp, hiện nút "Tiếp theo", không
> tự `setTimeout` chuyển màn.

```javascript
function checkSnap(studentVec, targetVec, tolerancePct = 0.08) {
  const dist = Math.hypot(studentVec.x - targetVec.x, studentVec.y - targetVec.y);
  const targetMag = Math.hypot(targetVec.x, targetVec.y);
  const tol = Math.max(0.25, targetMag * tolerancePct); // sàn tối thiểu — tránh đích quá nhỏ có
                                                          // dung sai gần như bằng 0
  return dist <= tol;
}

// Phân loại lỗi để phản hồi đúng caption state (2.1) thay vì chỉ báo "sai chung chung":
function classifyMismatch(studentVec, targetVec) {
  const dot = studentVec.x * targetVec.x + studentVec.y * targetVec.y;
  const sMag = Math.hypot(studentVec.x, studentVec.y) || 0.0001;
  const tMag = Math.hypot(targetVec.x, targetVec.y);
  const cosAngle = dot / (sMag * tMag);
  if (cosAngle < 0.3) return 'WRONG_DIRECTION';
  if (Math.abs(sMag - tMag) / tMag > 0.15) return 'WRONG_MAGNITUDE';
  return 'CLOSE';
}
```

### 1.5 Ghép Nhiều Vector Qua Slider (phân tích vector u = xa + yb)

> Dùng khi bài yêu cầu ghép 1 vector đích từ **tổ hợp tuyến tính của 2 vector cơ sở** — điều
> khiển bằng slider hệ số (không kéo tay trực tiếp trên canvas), có công thức đọc realtime.

```javascript
// a, b: vector cơ sở cố định {x,y}. x, y: hệ số từ 2 slider.
function buildChain(a, b, xCoef, yCoef) {
  const p1 = { x: a.x * xCoef, y: a.y * xCoef };           // mảnh 1: xa từ gốc O
  const tip = { x: p1.x + b.x * yCoef, y: p1.y + b.y * yCoef }; // mảnh 2: yb nối tiếp từ đầu p1
  return { p1, tip }; // vẽ: O→p1 (màu a), p1→tip (màu b), tip là điểm cần khớp với đích
}

// Cập nhật formula-readout mỗi lần slider đổi — dùng đúng dấu, không rút gọn số âm:
function formulaText(xCoef, yCoef) {
  return `u = ${xCoef.toFixed(1)}·a + ${yCoef.toFixed(1)}·b`;
}

// Kiểm tra khớp: dùng lại checkSnap (1.4) trên buildChain(...).tip so với vector đích.
```

---

## PHẦN 2 — FEEDBACK & ANIMATION

### 2.1 Caption State Machine (không để AI tự quyết định)

```javascript
// ❌ SAI — tự điền text mỗi lần, dễ nhầm trạng thái
setCaption('Đúng rồi!', 'green');

// ✅ ĐÚNG — định nghĩa trước tất cả states, dùng đúng token correct/wrong
const STATES = {
  IDLE:    {text:'Click vectơ để chọn.', type:''},
  CORRECT: {text:'Đúng! {detail}',       type:'correct'},
  WRONG:   {text:'{detail}',             type:'wrong'},
  NEAR:    {text:'Gần rồi! Tinh chỉnh thêm...', type:''},
  MATCH:   {text:'Khớp! {detail}',       type:'correct'},
  DONE:    {text:'Hoàn thành! {detail}', type:'correct'},
};

function setState(key, detail='') {
  const s = STATES[key];
  const text = s.text.replace('{detail}', detail);
  const el = document.getElementById('caption');
  el.className = 'sim-caption' + (s.type ? ' '+s.type : '');
  el.querySelector('span').textContent = text;
  el.querySelector('i').className =
    s.type==='correct' ? 'ti ti-check' :
    s.type==='wrong'   ? 'ti ti-x'     : 'ti ti-info-circle';
}

// Dùng:
setState('CORRECT', 'Vectơ cùng phương với A.');
setState('WRONG', 'Cùng giá nhưng mũi tên ngược chiều.');
setState('MATCH', `Độ dài = ${la}px · Góc = ${aa}°`);
```

```css
/* .sim-caption mặc định: nền jade-pale, border-left jade (xem 02_design_ly.md 3.1) */
.sim-caption.correct { background: var(--correct-bg); border-left-color: var(--correct); }
.sim-caption.wrong   { background: var(--wrong-bg);   border-left-color: var(--wrong); }
.sim-caption.correct .ti, .sim-caption.correct span { color: var(--jade-text); }
.sim-caption.wrong .ti, .sim-caption.wrong span     { color: var(--wrong); }
```

### 2.2 Shake Animation — Khi Sai (không đổi, không liên quan màu)

```javascript
/* CSS:
@keyframes shake {
  0%,100%{transform:translateX(0)}
  20%{transform:translateX(-6px)}
  40%{transform:translateX(6px)}
  60%{transform:translateX(-4px)}
  80%{transform:translateX(4px)}
}
.shake { animation: shake .4s ease; }
*/

function shakeCanvas(canvas) {
  let t = 0;
  const offsets = [0,-6,6,-4,4,-2,2,0];
  function frame() {
    if (t >= offsets.length) { canvas.style.transform=''; return; }
    canvas.style.transform = `translateX(${offsets[t]}px)`;
    t++;
    requestAnimationFrame(frame);
  }
  frame();
}

if (shakeTarget >= 0) {
  const off = Math.sin(shakeT * 1.8) * 5 * (1 - shakeT/12);
  ctx.save();
  ctx.translate(off, 0);
  drawVector(shakeTarget);
  ctx.restore();
  shakeT++;
  if (shakeT >= 12) shakeTarget = -1;
}
```

### 2.3 Snap + Pulse — Khi Gần Khớp (đổi tên từ "Glow", bỏ hiệu ứng phát sáng)

```javascript
// Kiểm tra "gần khớp" với tolerance — logic không đổi
function checkMatch(vA, vB, lenTol=0.07, angTol=7) {
  const la = vecLen(vA), lb = vecLen(vB);
  const aa = vecAngle(vA) * 180/Math.PI;
  const ab = vecAngle(vB) * 180/Math.PI;
  let adiff = Math.abs(aa - ab) % 360;
  if (adiff > 180) adiff = 360 - adiff;
  return {
    near:  Math.abs(la-lb)/la < lenTol*1.5 && adiff < angTol*1.5,
    match: Math.abs(la-lb)/la < lenTol     && adiff < angTol
  };
}

// FLAT PULSE — thay glow/blur bằng nét outline dày dao động độ mờ, không dùng shadowBlur
let pulsePhase = 0;
function drawPulse(ctx, x1, y1, x2, y2, isMatch) {
  pulsePhase = (pulsePhase + 0.08) % (Math.PI*2);
  const alpha = 0.35 + 0.25 * Math.sin(pulsePhase);
  ctx.save();
  ctx.strokeStyle = isMatch
    ? `rgba(45,139,111,${alpha})`   /* --correct */
    : `rgba(232,162,74,${alpha})`;  /* --accent — "gần đúng", không phải sai */
  ctx.lineWidth = 8; // dày vừa phải, KHÔNG dùng shadowBlur/glow filter
  ctx.lineCap = 'round';
  ctx.beginPath();
  ctx.moveTo(x1, y1);
  ctx.lineTo(x2, y2);
  ctx.stroke();
  ctx.restore();
}
// Gọi requestAnimationFrame khi near/match để pulse liên tục
```

### 2.4 Celebration — Đường Viền Xác Nhận (thay Confetti nhiều màu)

```
Confetti nhiều màu sặc sỡ KHÔNG phù hợp tinh thần "tiết chế, editorial" của Haugomat.
Thay bằng hiệu ứng nhẹ nhàng hơn: viền canvas sáng lên bằng --jade trong 400ms rồi tắt,
kết hợp icon check lớn mờ dần — vẫn tạo cảm giác "hoàn thành" mà không phá vỡ sự tiết chế.
```

```javascript
function celebrate(canvas) {
  canvas.style.transition = 'box-shadow 400ms ease';
  canvas.style.boxShadow = '0 0 0 3px var(--jade)';
  setTimeout(() => { canvas.style.boxShadow = 'none'; }, 500);

  // Icon check lớn, mờ dần giữa canvas — dùng DOM overlay, không phải particle system
  const check = document.createElement('div');
  check.innerHTML = '<i class="ti ti-circle-check"></i>';
  check.style.cssText = `
    position:absolute; inset:0; display:flex; align-items:center; justify-content:center;
    font-size:64px; color:var(--jade); opacity:0; pointer-events:none;
    transition: opacity 300ms ease, transform 300ms ease; transform: scale(0.8);
  `;
  canvas.parentElement.appendChild(check);
  requestAnimationFrame(() => { check.style.opacity = '1'; check.style.transform = 'scale(1)'; });
  setTimeout(() => {
    check.style.opacity = '0';
    setTimeout(() => check.remove(), 300);
  }, 900);

  document.getElementById('next-btn').style.display = 'inline-flex';
}
```

### 2.5 Quy Tắc Next Button (KHÔNG Auto-advance)

```
❌ SAI:
setTimeout(() => nextLevel(), 1800); // Stage 2 bài Vector gây UX tệ

✅ ĐÚNG — luôn dùng nút xác nhận:
  1. Khi match/complete: hiện nút "Tiếp theo" (nền --jade, chữ --cream, theo chuẩn 3.1)
  2. Celebration (2.4) chạy trong khi học sinh đọc caption
  3. Học sinh click nút → nextLevel() / nextMission()
  4. nextLevel(): ẩn nút, load level mới

Ngoại lệ duy nhất: animation "phản ứng hiện tượng" (vật di chuyển)
→ có thể auto sau 1.5-2s vì học sinh đang nhìn canvas, không đọc
```

### 2.6 Easing Functions (không đổi, không liên quan màu)

```javascript
const ease = {
  outQuad:   t => 1 - (1-t)**2,
  outCubic:  t => 1 - (1-t)**3,
  inOutSine: t => -(Math.cos(Math.PI*t) - 1) / 2,
  outBounce: t => {
    if (t < 1/2.75) return 7.5625*t*t;
    if (t < 2/2.75) return 7.5625*(t-=1.5/2.75)*t + 0.75;
    if (t < 2.5/2.75) return 7.5625*(t-=2.25/2.75)*t + 0.9375;
    return 7.5625*(t-=2.625/2.75)*t + 0.984375;
  }
};

let animT = 0, ANIM_FRAMES = 30;
function animateTo(fromX, fromY, toX, toY) {
  animT = 0;
  function frame() {
    animT++;
    const t = ease.outCubic(Math.min(animT/ANIM_FRAMES, 1));
    obj.x = fromX + (toX - fromX) * t;
    obj.y = fromY + (toY - fromY) * t;
    draw();
    if (animT < ANIM_FRAMES) requestAnimationFrame(frame);
  }
  frame();
}
```

---

## PHẦN 3 — GAME STRUCTURE

### 3.1 Level / Mission Data Format Chuẩn (không đổi, không liên quan màu)

```javascript
const LEVELS = [
  {
    id: 'l1',
    desc: 'Mô tả ngắn hiển thị cho học sinh',
    obj: 'plane',
    targets: [
      {type:'direction', dx:1, dy:0}
    ],
    choices: [
      {dx:1,dy:0}, {dx:-1,dy:0}, {dx:0.7,dy:-0.7}, {dx:0,dy:-1}
    ],
    feedback: {
      wrong_dir:  'Quan sát hướng chuyển động của vật...',
      wrong_place:'Vectơ lực phải đặt tại vật, không phải ngoài không khí!',
      hint:       'Gợi ý: mũi tên phải chỉ cùng hướng vật đang di chuyển.'
    },
    bonus: false
  },
];

const MISSIONS = [
  {
    id: 'collinear',
    label: 'Tìm tất cả vectơ CÙNG PHƯƠNG với vectơ A',
    check: (v, ref) => isCollinear(v, ref),
    feedback: {
      correct:  'Đúng! Giá song song hoặc trùng nhau.',
      wrong_opp:'Cùng giá — nhưng mũi tên ngược chiều. Đây là ngược hướng.',
      wrong_len:'Cùng hướng — nhưng độ dài khác. Bằng nhau cần cả hai.'
    }
  },
  {id:'same',     label:'Tìm tất cả vectơ CÙNG HƯỚNG với vectơ A',     check:(v,r)=>isSameDir(v,r)},
  {id:'opposite', label:'Tìm tất cả vectơ NGƯỢC HƯỚNG với vectơ A',    check:(v,r)=>isOpposite(v,r)},
  {id:'equal',    label:'Tìm tất cả vectơ BẰNG NHAU với vectơ A',      check:(v,r)=>isEqual(v,r)},
];

function isCollinear(v, ref, tol=0.15) {
  if (v.len === 0) return true;
  let diff = Math.abs(v.angle - ref.angle) % Math.PI;
  if (diff > Math.PI/2) diff = Math.PI - diff;
  return diff < tol;
}
function isSameDir(v, ref, tol=0.15) {
  if (v.len === 0) return true;
  let diff = Math.abs(v.angle - ref.angle) % (Math.PI*2);
  if (diff > Math.PI) diff = Math.PI*2 - diff;
  return diff < tol;
}
function isOpposite(v, ref, tol=0.15) {
  if (v.len === 0) return false;
  let diff = Math.abs(v.angle - ref.angle - Math.PI) % (Math.PI*2);
  if (diff > Math.PI) diff = Math.PI*2 - diff;
  return diff < tol;
}
function isEqual(v, ref, lenTol=5, angTol=0.15) {
  return isSameDir(v, ref, angTol) && Math.abs(v.len - ref.len) < lenTol;
}
```

### 3.2 Score & Progress Tracking (không đổi, không liên quan màu)

```javascript
const Score = {
  _data: {},

  add(stageId, pts) {
    if (!this._data[stageId]) this._data[stageId] = {points:0, stars:0, completed:false};
    this._data[stageId].points += pts;
    this.render(stageId);
  },

  complete(stageId) {
    this._data[stageId].completed = true;
    this._data[stageId].stars = this.calcStars(stageId);
    this.renderStars(stageId);
  },

  calcStars(stageId) {
    const pts = this._data[stageId]?.points || 0;
    if (pts >= 45) return 5;
    if (pts >= 35) return 4;
    if (pts >= 25) return 3;
    if (pts >= 15) return 2;
    return 1;
  },

  render(stageId) {
    const el = document.getElementById(`${stageId}-score`);
    if (el) el.textContent = this._data[stageId]?.points || 0;
    const ms = document.getElementById(`${stageId}-mscore`);
    if (ms) ms.textContent = this.getMissionScore(stageId);
  },

  getMissionScore(stageId) { return ''; },

  renderStars(stageId) {
    const n = this._data[stageId]?.stars || 0;
    const stars = document.querySelectorAll(`#${stageId}-stars .star`);
    stars.forEach((s,i) => {
      // Dùng icon Tabler thay emoji sao để đồng bộ icon set (xem 02_design_ly.md 1.5)
      s.className = 'ti ' + (i < n ? 'ti-star-filled' : 'ti-star') + ' star';
      s.style.color = i < n ? 'var(--accent)' : 'var(--paper-line)';
    });
  }
};
```

### 3.3 Stage Unlock Flow (không đổi, không liên quan màu)

```javascript
const StageManager = {
  unlocked: new Set([1]),
  current: 1,

  unlock(n) {
    if (this.unlocked.has(n)) return;
    this.unlocked.add(n);
    const sb = document.getElementById(`sb-s${n}`);
    if (sb) {
      sb.classList.remove('locked');
      sb.querySelector('.mod-badge').className = 'mod-badge mb-active';
      sb.querySelector('.mod-badge').textContent = 'Mới mở';
    }
    const banner = document.getElementById(`unlock-s${n}`);
    if (banner) banner.classList.add('show');
    this.updateProgress();
  },

  goto(n) {
    if (!this.unlocked.has(n)) return;
    this.current = n;
    document.querySelectorAll('.stage-section').forEach(s => s.classList.remove('active'));
    document.getElementById(`stage-${n}`).classList.add('active');
    document.querySelectorAll('.mod-item').forEach(m => m.classList.remove('active'));
    document.getElementById(`sb-s${n}`).classList.add('active');
    this.updateProgress();
    ({1:initS1, 2:initS2, 3:initS3, 4:initS4})[n]?.();
  },

  updateProgress() {
    const pct = Math.round(this.unlocked.size / 4 * 100);
    document.getElementById('prog-fill').style.width = pct + '%';
    document.getElementById('prog-pct').textContent = pct + '%';
  }
};
```

```css
/* Thanh progress — dùng jade thay vì màu mặc định */
#prog-fill { background: var(--jade); height: 100%; border-radius: 4px; transition: width 300ms ease; }
```

### 3.4 RAF Loop — Chỉ Khi Cần (không đổi, không liên quan màu)

```javascript
// ❌ SAI — loop liên tục kể cả khi không có gì thay đổi
function draw() {
  requestAnimationFrame(draw);
}

// ✅ ĐÚNG — phân biệt 3 loại draw

// Loại 1: On-demand
function draw() {
  ctx.clearRect(0,0,CW,CH);
  // KHÔNG gọi requestAnimationFrame
}

// Loại 2: Animation loop
let rafId = null;
function startLoop() {
  if (rafId) return;
  function loop() {
    update();
    draw();
    rafId = requestAnimationFrame(loop);
  }
  rafId = requestAnimationFrame(loop);
}
function stopLoop() {
  cancelAnimationFrame(rafId);
  rafId = null;
}

// Loại 3: Hybrid
let needsRedraw = false;
function requestDraw() { needsRedraw = true; }
function loop() {
  if (needsRedraw) { draw(); needsRedraw = false; }
  requestAnimationFrame(loop);
}
loop();
```

---

## PHẦN 4 — PHYSICS & FORCE PATTERNS

> Dùng cho: mặt phẳng nghiêng, tàu chịu gió, nhiều lực đồng thời, chuyển động có gia tốc
> Màu vector: luôn tra bảng `02_design_ly.md` mục 1.2 (VEC.F, VEC.P, VEC.N...), không tự đặt hex.

### 4.1 Vector Math Cơ Bản (không đổi)

```javascript
const Vec2 = {
  add:    (a,b) => ({x: a.x+b.x, y: a.y+b.y}),
  sub:    (a,b) => ({x: a.x-b.x, y: a.y-b.y}),
  scale:  (v,s) => ({x: v.x*s, y: v.y*s}),
  len:    v => Math.sqrt(v.x**2 + v.y**2),
  norm:   v => { const l=Vec2.len(v)||1; return {x:v.x/l, y:v.y/l}; },
  dot:    (a,b) => a.x*b.x + a.y*b.y,
  angle:  v => Math.atan2(v.y, v.x),
  fromAngle: (angle, len=1) => ({x: Math.cos(angle)*len, y: Math.sin(angle)*len}),
  rotate: (v, rad) => ({
    x: v.x*Math.cos(rad) - v.y*Math.sin(rad),
    y: v.x*Math.sin(rad) + v.y*Math.cos(rad)
  }),
  project: (v, u) => Vec2.scale(u, Vec2.dot(v, Vec2.norm(u))),
};

// Chuyển đổi: canvas Y-axis ngược (xuống = +y)
// Trong canvas: lực hấp dẫn = {x:0, y:+g} vì y tăng xuống dưới
```

### 4.2 Tổng Hợp Lực — Nhiều Lực Đồng Thời

```javascript
// Dùng cho: tàu chịu gió + động cơ + lực cản
// Màu lấy từ token thay vì hex tự đặt — tái dùng bảng vector 02_design_ly.md 1.2
const forces = {
  engine: {id:'engine', vec:{x:80,y:0},  color: VEC.F.color, label:'F_động cơ', placed:false},
  wind:   {id:'wind',   vec:{x:30,y:20}, color: VEC.T.color, label:'F_gió',     placed:false},
  drag:   {id:'drag',   vec:{x:-40,y:0}, color: VEC.f.color, label:'F_cản',     placed:false},
};

function calcResultant() {
  const active = Object.values(forces).filter(f => f.placed);
  return active.reduce((sum, f) => Vec2.add(sum, f.vec), {x:0, y:0});
}

function drawForceSystem(ctx, ox, oy) {
  const active = Object.values(forces).filter(f => f.placed);
  active.forEach(f => {
    drawForceArrow(ctx, ox, oy, f.vec, f.color, f.label);
  });
  if (active.length >= 2) {
    const R = calcResultant();
    // Lực tổng luôn dùng --accent + nét chấm-gạch để nổi bật nhưng vẫn tiết chế (xem 1.2)
    drawForceArrow(ctx, ox, oy, R, getVar('--accent'), 'F_tổng', 4);
  }
}

function drawForceArrow(ctx, ox, oy, vec, color, label, lw=2.5) {
  const SCALE = 1;
  const ex = ox + vec.x*SCALE, ey = oy + vec.y*SCALE;
  drawArrow(ctx, ox, oy, ex, ey, color, lw);
  const mx = (ox+ex)/2, my = (oy+ey)/2;
  drawVecLabel(ctx, mx+6, my-10, label, color);
}
```

### 4.3 Phân Tích Lực — Mặt Phẳng Nghiêng

```javascript
function inclinedForces(mass, theta, g=10) {
  const mg = mass * g;
  return {
    weight:   {x: 0,              y: mg},
    parallel: {x: -mg*Math.sin(theta), y: mg*Math.cos(theta)},
    normal:   {x: -mg*Math.sin(theta-Math.PI/2), y: mg*Math.cos(theta-Math.PI/2)},
    // P_song = mg.sin(θ) — dọc mặt phẳng, chiều xuống dốc
    // N = mg.cos(θ)      — vuông góc mặt phẳng, chiều ra ngoài
  };
}

// Vẽ mặt phẳng nghiêng + vật + các lực — schematic hoá theo 02_design_ly.md 1.7.6
function drawInclinedPlane(ctx, CW, CH, theta, forces) {
  ctx.save();
  const ox = CW*0.15, oy = CH*0.85;
  const len = CW*0.7;

  // Mặt phẳng — nét ink, không xám kỹ thuật
  ctx.strokeStyle = getVar('--ink'); ctx.lineWidth = 2.5; ctx.lineCap = 'round';
  ctx.beginPath();
  ctx.moveTo(ox, oy);
  ctx.lineTo(ox + len*Math.cos(theta), oy - len*Math.sin(theta));
  ctx.stroke();

  // Đáy
  ctx.strokeStyle = getVar('--paper-line'); ctx.lineWidth = 1.5;
  ctx.beginPath();
  ctx.moveTo(ox, oy);
  ctx.lineTo(ox + len*Math.cos(theta), oy);
  ctx.stroke();

  // Cung góc theta
  ctx.strokeStyle = getVar('--ink-2'); ctx.lineWidth = 1.5;
  ctx.beginPath();
  ctx.arc(ox, oy, 40, -theta, 0);
  ctx.stroke();
  ctx.fillStyle = getVar('--ink-2'); ctx.font = "12px 'Inconsolata', monospace";
  ctx.fillText('θ', ox+45, oy-12);

  const t = 0.4;
  const bx = ox + t*len*Math.cos(theta);
  const by = oy - t*len*Math.sin(theta);

  ctx.translate(bx, by);
  ctx.rotate(-theta);
  drawBox(ctx, 0, -20); // vật hộp flat — xem PHẦN 6
  ctx.rotate(theta);
  ctx.translate(-bx, -by);

  Object.entries(forces).forEach(([key, f]) => {
    if (!f.placed) return;
    drawForceArrow(ctx, bx, by, f.vec, f.color, f.label);
  });

  ctx.restore();
}

// a = g.sin(θ) − μ.g.cos(θ) — xuống dốc
function calcAcceleration(theta, mu=0, g=10) {
  return g * Math.sin(theta) - mu * g * Math.cos(theta);
}
```

### 4.4 Simple Physics Loop — Euler Integration

```javascript
// Đủ cho THPT với chuyển động thẳng/ném xiên. LƯU Ý: với dao động góc lớn (con lắc...),
// dùng Euler-Cromer (xem 02_design_ly.md mục 2.6 pendulumStep) thay vì Euler thường,
// vì Euler thường làm năng lượng hệ dao động tăng dần theo thời gian (không ổn định).

const PHYSICS = {
  dt: 1/60,
  g:  10,
  scale: 50,

  state: { x: 0, y: 0, vx: 0, vy: 0, ax: 0, ay: 0 },

  addForce(fx, fy, mass) {
    this.state.ax = fx / mass;
    this.state.ay = fy / mass;
  },

  step() {
    const s = this.state;
    s.vx += s.ax * this.dt;
    s.vy += s.ay * this.dt;
    s.x  += s.vx * this.dt;
    s.y  += s.vy * this.dt;
    s.vx *= 0.998;
    s.vy *= 0.998;
  },

  toCanvas(px, py, CW, CH) {
    return { cx: CW/2 + px * this.scale, cy: CH/2 - py * this.scale };
  },

  reset() {
    Object.assign(this.state, {x:0,y:0,vx:0,vy:0,ax:0,ay:0});
  }
};

function gameLoop() {
  PHYSICS.step();
  const {cx, cy} = PHYSICS.toCanvas(PHYSICS.state.x, PHYSICS.state.y, CW, CH);
  draw(cx, cy);
  if (isRunning) requestAnimationFrame(gameLoop);
}
```

### 4.5 Vẽ Vectơ Lực Chuẩn (bỏ nền trắng bo góc sau label, dùng nền cream token)

```javascript
function drawForceVector(ctx, ox, oy, vec, color, label, opts={}) {
  const {
    lw = 2.8,
    scale = 1,
    showLabel = true,
    showValue = false,
    dashed = false,
  } = opts;

  const ex = ox + vec.x * scale;
  const ey = oy + vec.y * scale;
  const len = Math.sqrt(vec.x**2 + vec.y**2) * scale;
  if (len < 2) return;

  ctx.save();
  ctx.strokeStyle = color;
  ctx.lineWidth = lw;
  ctx.lineCap = 'round';
  if (dashed) ctx.setLineDash([6, 4]);
  ctx.beginPath();
  ctx.moveTo(ox, oy);
  const hs = Math.min(14, len*0.3);
  const nx = (ex-ox)/len*hs, ny = (ey-oy)/len*hs;
  ctx.lineTo(ex - nx*0.6, ey - ny*0.6);
  ctx.stroke();
  ctx.setLineDash([]);

  ctx.fillStyle = color;
  ctx.beginPath();
  ctx.moveTo(ex, ey);
  ctx.lineTo(ex - nx - ny*0.45, ey - ny + nx*0.45);
  ctx.lineTo(ex - nx + ny*0.45, ey - ny - nx*0.45);
  ctx.closePath();
  ctx.fill();

  // Điểm đặt — chấm đặc, KHÔNG có halo mờ xung quanh (bỏ glow)
  ctx.fillStyle = color;
  ctx.beginPath(); ctx.arc(ox, oy, 3.5, 0, Math.PI*2); ctx.fill();

  if (showLabel) {
    const lx = (ox+ex)/2 + ny*0.5 + 8;
    const ly = (oy+ey)/2 - nx*0.5 - 6;
    ctx.font = "bold 12px 'Inconsolata', monospace";
    const tw = ctx.measureText(label).width;
    // Nền nhãn: cream với alpha nhẹ, thay vì trắng cứng — hoà với nền canvas cream
    ctx.fillStyle = 'rgba(250,247,240,0.9)'; // --cream ở dạng rgba
    ctx.beginPath();
    ctx.roundRect(lx-4, ly-13, tw+8, 17, 3);
    ctx.fill();
    ctx.fillStyle = color;
    ctx.textAlign = 'left'; ctx.textBaseline = 'top';
    ctx.fillText(label, lx, ly-12);

    if (showValue) {
      const val = Math.round(Vec2.len(vec)) + ' N';
      ctx.font = "10px 'Inconsolata', monospace";
      ctx.fillStyle = color;
      ctx.fillText(val, lx, ly+3);
    }
  }

  ctx.restore();
}
```

---

## PHẦN 5 — ISOMETRIC & PSEUDO-3D

> Dùng cho: hình học không gian, hình hộp 3D, vectơ trong không gian

### 5.1 Khi Nào Dùng Gì (không đổi)

```
Mục tiêu giảng dạy          → Kỹ thuật phù hợp
─────────────────────────────────────────────────────
Lực 2D (mặt phẳng xy)       → Canvas 2D thuần (PHẦN 4)
Chuyển động 2D               → Canvas 2D thuần
Hình hộp, hình chóp nhìn    → Isometric 2D (PHẦN 5.2)
  từ góc cố định
Vectơ trong không gian       → Isometric 2D với trục xyz
Xoay vật 3D tự do            → Three.js (vượt scope file này)
Animation 3D phức tạp        → Three.js
Fluid simulation 3D          → KHÔNG làm trong HTML đơn

Quy tắc: nếu học sinh cần XEM từ một góc cố định → isometric
          nếu học sinh cần XOAY vật → Three.js
```

### 5.2 Isometric Projection Công Thức (không đổi — thuần toán học)

```javascript
const ISO = {
  project(x3d, y3d, z3d) {
    const px = (x3d - y3d) * Math.cos(Math.PI/6);
    const py = (x3d + y3d) * Math.sin(Math.PI/6) - z3d;
    return {x: px, y: py};
  },
  UNIT: 40,
  toCanvas(x3d, y3d, z3d, originX, originY) {
    const {x, y} = this.project(x3d, y3d, z3d);
    return { cx: originX + x * this.UNIT, cy: originY + y * this.UNIT };
  }
};

function drawIsoPoint(ctx, x3d, y3d, z3d, color, label) {
  const {cx, cy} = ISO.toCanvas(x3d, y3d, z3d, CW/2, CH*0.6);
  ctx.fillStyle = color;
  ctx.beginPath(); ctx.arc(cx, cy, 5, 0, Math.PI*2); ctx.fill();
  if (label) drawVecLabel(ctx, cx+7, cy-7, label, color);
}

function drawIsoVector(ctx, from3d, to3d, color, label) {
  const origin = {x: CW/2, y: CH*0.6};
  const p1 = ISO.toCanvas(from3d.x, from3d.y, from3d.z, origin.x, origin.y);
  const p2 = ISO.toCanvas(to3d.x,   to3d.y,   to3d.z,   origin.x, origin.y);
  drawArrow(ctx, p1.cx, p1.cy, p2.cx, p2.cy, color, 2.5);
  if (label) {
    const mx = (p1.cx+p2.cx)/2, my = (p1.cy+p2.cy)/2;
    drawVecLabel(ctx, mx+6, my-8, label, color);
  }
}
```

### 5.3 Vẽ Hình Hộp Isometric — FLAT (thay 3 tông nâu gradient bằng 3 sắc ink-alpha)

```javascript
// Hình hộp lw × ld × lh (ngang × sâu × cao)
// Đổ bóng 3 mặt bằng 3 mức alpha của --ink-2 trên nền --cream-2 — vẫn phẳng, KHÔNG gradient,
// chỉ là 3 mảng màu đặc khác độ đậm để gợi ánh sáng, đúng tinh thần "flat, editorial"
function drawIsoBox(ctx, x0, y0, z0, lw, ld, lh, colors) {
  const O = {x: CW/2, y: CH*0.6};
  const pts = [
    [x0,    y0,    z0   ], [x0+lw, y0,    z0   ],
    [x0+lw, y0+ld, z0   ], [x0,    y0+ld, z0   ],
    [x0,    y0,    z0+lh], [x0+lw, y0,    z0+lh],
    [x0+lw, y0+ld, z0+lh], [x0,    y0+ld, z0+lh],
  ].map(([x,y,z]) => ISO.toCanvas(x,y,z, O.x, O.y));

  const fill = colors || {
    top:   getVar('--cream-2'),          // mặt sáng nhất
    left:  'rgba(81,76,68,0.12)',        // --ink-2 nhạt
    right: 'rgba(81,76,68,0.22)',        // --ink-2 đậm hơn — mặt tối nhất
  };

  ctx.fillStyle = fill.top;
  ctx.beginPath();
  [4,5,6,7].forEach((i,j) => j===0 ? ctx.moveTo(pts[i].cx,pts[i].cy) : ctx.lineTo(pts[i].cx,pts[i].cy));
  ctx.closePath(); ctx.fill();

  ctx.fillStyle = fill.left;
  ctx.beginPath();
  [0,4,7,3].forEach((i,j) => j===0 ? ctx.moveTo(pts[i].cx,pts[i].cy) : ctx.lineTo(pts[i].cx,pts[i].cy));
  ctx.closePath(); ctx.fill();

  ctx.fillStyle = fill.right;
  ctx.beginPath();
  [1,5,6,2].forEach((i,j) => j===0 ? ctx.moveTo(pts[i].cx,pts[i].cy) : ctx.lineTo(pts[i].cx,pts[i].cy));
  ctx.closePath(); ctx.fill();

  // Viền — paper-line thay vì đen mờ
  ctx.strokeStyle = getVar('--paper-line'); ctx.lineWidth = 1;
  [[0,1],[1,2],[2,3],[3,0], [4,5],[5,6],[6,7],[7,4], [0,4],[1,5],[2,6],[3,7]]
    .forEach(([a,b]) => {
      ctx.beginPath();
      ctx.moveTo(pts[a].cx, pts[a].cy);
      ctx.lineTo(pts[b].cx, pts[b].cy);
      ctx.stroke();
    });
}

// Dùng: drawIsoBox(ctx, -1,-1,0, 2,2,2); // dùng màu mặc định flat ở trên
```

### 5.4 Hệ Trục Tọa Độ Isometric — màu theo token thay vì đỏ/xanh lá/xanh dương thật

```javascript
function drawIsoAxes(ctx, length=4, origin={x:CW/2, y:CH*0.65}) {
  const axes = [
    {to:[length,0,0], color: getVar('--jade'),      label:'x'},
    {to:[0,length,0], color: getVar('--jade-deep'), label:'y'},
    {to:[0,0,length], color: getVar('--ink'),        label:'z'},
  ];

  axes.forEach(({to, color, label}) => {
    const p2 = ISO.toCanvas(to[0], to[1], to[2], origin.x, origin.y);
    drawArrow(ctx, origin.x, origin.y, p2.cx, p2.cy, color, 2);
    ctx.fillStyle = color;
    ctx.font = "bold 13px 'Inconsolata', monospace";
    ctx.textAlign = 'left'; ctx.textBaseline = 'middle';
    ctx.fillText(label, p2.cx+5, p2.cy);
  });

  ctx.fillStyle = getVar('--ink');
  ctx.beginPath(); ctx.arc(origin.x, origin.y, 4, 0, Math.PI*2); ctx.fill();
  ctx.font = "12px 'Inconsolata', monospace";
  ctx.fillText('O', origin.x-14, origin.y-12);
}
```

### 5.5 Mặt Phẳng Lưới Isometric — lưới paper-line thay xanh đậm

```javascript
function drawIsoGrid(ctx, size=6, step=1, origin={x:CW/2, y:CH*0.7}) {
  ctx.strokeStyle = getVar('--paper-line');
  ctx.lineWidth = 0.8;

  for (let i=0; i<=size; i++) {
    const a = ISO.toCanvas(0, i*step, 0, origin.x, origin.y);
    const b = ISO.toCanvas(size*step, i*step, 0, origin.x, origin.y);
    ctx.beginPath(); ctx.moveTo(a.cx,a.cy); ctx.lineTo(b.cx,b.cy); ctx.stroke();

    const c = ISO.toCanvas(i*step, 0, 0, origin.x, origin.y);
    const d = ISO.toCanvas(i*step, size*step, 0, origin.x, origin.y);
    ctx.beginPath(); ctx.moveTo(c.cx,c.cy); ctx.lineTo(d.cx,d.cy); ctx.stroke();
  }
}
```

---

## PHẦN 6 — OBJECT LIBRARY (Haugomat flat — thay thế toàn bộ bản gradient/3D cũ)

> Tất cả hàm vẽ vật thể — tái dùng xuyên suốt các bài học

### Quy Tắc Vẽ Vật Thể (BẮT BUỘC — bản flat)

```
1. Luôn bọc ctx.save() / ctx.restore()
2. LUÔN dùng màu phẳng (1 mảng màu đặc) — KHÔNG dùng createRadialGradient/
   createLinearGradient để giả khối 3D
3. Shadow: 1 hình ellipse phẳng, màu rgba(26,26,26,0.1-0.15), KHÔNG blur — gợi vật "đứng"
   trên mặt phẳng mà vẫn phẳng
4. KHÔNG vẽ highlight stripe/specular sáng giả ánh sáng phản chiếu
5. Chi tiết nhỏ (cửa sổ, bánh xe, ống khói) vẽ bằng hình khối đơn giản, màu đặc — không cần
   quá chi tiết, ưu tiên silhouette rõ ràng dễ nhận diện
6. Điểm đặt lực = chấm đặc màu --accent, KHÔNG có halo mờ xung quanh (bỏ glow)
7. Toàn bộ màu tra bảng 02_design_ly.md PHẦN 1 — không tự đặt hex ngoài bảng
```

### drawPlane(ctx, x, y, angle=0)

```javascript
// Máy bay — silhouette flat, không gradient kim loại
function drawPlane(ctx, x, y, angle=0) {
  ctx.save();
  ctx.translate(x, y);
  ctx.rotate(angle);

  // Shadow — phẳng, không blur
  ctx.fillStyle = 'rgba(26,26,26,0.1)';
  ctx.beginPath(); ctx.ellipse(0,18,38,5,0,0,Math.PI*2); ctx.fill();

  // Thân máy bay — 1 màu đặc
  ctx.fillStyle = getVar('--ink-2');
  ctx.beginPath(); ctx.roundRect(-42,-9,84,18,9); ctx.fill();

  // Mũi
  ctx.fillStyle = getVar('--jade-deep');
  ctx.beginPath(); ctx.roundRect(30,-7,18,14,7); ctx.fill();

  // Cánh
  ctx.fillStyle = getVar('--sage');
  ctx.beginPath(); ctx.moveTo(-10,0); ctx.lineTo(15,0); ctx.lineTo(5,-22); ctx.lineTo(-15,-8); ctx.closePath(); ctx.fill();
  ctx.beginPath(); ctx.moveTo(-10,0); ctx.lineTo(15,0); ctx.lineTo(5,22); ctx.lineTo(-15,8); ctx.closePath(); ctx.fill();

  // Đuôi
  ctx.fillStyle = getVar('--ink-2');
  ctx.beginPath(); ctx.moveTo(-38,-2); ctx.lineTo(-25,-2); ctx.lineTo(-32,-14); ctx.closePath(); ctx.fill();

  // Cửa sổ — chấm đặc đơn giản
  ctx.fillStyle = getVar('--cream');
  [-20,-8,4,16].forEach(wx => { ctx.beginPath(); ctx.roundRect(wx,-5,9,7,3); ctx.fill(); });

  ctx.restore();
}
```

### drawShip(ctx, x, y)

```javascript
// Tàu thuỷ — nhìn ngang, flat
function drawShip(ctx, x, y) {
  ctx.save();
  // Shadow mặt nước
  ctx.fillStyle = 'rgba(26,26,26,0.1)';
  ctx.beginPath(); ctx.ellipse(x+5,y+32,72,7,0,0,Math.PI*2); ctx.fill();

  // Thân tàu — 1 màu đặc
  ctx.fillStyle = getVar('--ink');
  ctx.beginPath();
  ctx.moveTo(x-70,y); ctx.lineTo(x+80,y);
  ctx.lineTo(x+65,y+32); ctx.lineTo(x-55,y+32); ctx.closePath(); ctx.fill();

  // Vạch mớn nước
  ctx.fillStyle = getVar('--jade-deep'); ctx.fillRect(x-70,y+24,150,6);

  // Cabin
  ctx.fillStyle = getVar('--cream-2');
  ctx.strokeStyle = getVar('--paper-line'); ctx.lineWidth = 1;
  ctx.beginPath(); ctx.roundRect(x-35,y-36,85,38,5); ctx.fill(); ctx.stroke();

  // Cửa sổ
  ctx.fillStyle = getVar('--sage');
  [-20,0,20,40].forEach(wx => { ctx.beginPath(); ctx.roundRect(x+wx,y-26,12,9,2); ctx.fill(); });

  // Ống khói
  ctx.fillStyle = getVar('--ink-2'); ctx.fillRect(x+32,y-58,14,24);

  // Sóng — nét mảnh sage
  ctx.strokeStyle = getVar('--sage'); ctx.lineWidth = 1.5; ctx.lineCap = 'round';
  ctx.beginPath(); ctx.moveTo(x-80,y+30);
  for (let i=0;i<8;i++) ctx.quadraticCurveTo(x-80+i*20+10,y+26,x-80+i*20+20,y+30);
  ctx.stroke();
  ctx.restore();
}
```

### drawBox(ctx, x, y, showForcePoint=true)

```javascript
// Hộp hàng — flat, iso feel giữ nguyên qua hình khối chứ không qua gradient
function drawBox(ctx, x, y, showForcePoint=true) {
  ctx.save();
  ctx.fillStyle = 'rgba(26,26,26,0.1)';
  ctx.beginPath(); ctx.ellipse(x,y+40,36,5,0,0,Math.PI*2); ctx.fill();

  // Mặt trước — 1 màu đặc
  ctx.fillStyle = getVar('--sage');
  ctx.beginPath(); ctx.roundRect(x-32,y-38,64,76,4); ctx.fill();

  // Mặt trên — tông đậm hơn 1 chút (không gradient, chỉ đổi token)
  ctx.fillStyle = getVar('--jade-pale');
  ctx.beginPath();
  ctx.moveTo(x-32,y-38); ctx.lineTo(x+32,y-38);
  ctx.lineTo(x+40,y-50); ctx.lineTo(x-24,y-50); ctx.closePath(); ctx.fill();

  // Dây đai
  ctx.strokeStyle = getVar('--ink-2'); ctx.lineWidth = 2;
  ctx.beginPath(); ctx.moveTo(x-32,y); ctx.lineTo(x+32,y); ctx.stroke();
  ctx.beginPath(); ctx.moveTo(x,y-38); ctx.lineTo(x,y+38); ctx.stroke();

  // Nhãn
  ctx.fillStyle = getVar('--ink'); ctx.font = "bold 9px 'Be Vietnam Pro', sans-serif";
  ctx.textAlign = 'center'; ctx.textBaseline = 'middle'; ctx.fillText('HÀNG',x,y+14);

  if (showForcePoint) {
    ctx.fillStyle = getVar('--accent');
    ctx.beginPath(); ctx.arc(x,y,4,0,Math.PI*2); ctx.fill();
  }
  ctx.restore();
}
```

### drawBalloon(ctx, x, y)

```javascript
// Khinh khí cầu — cho bài lực đẩy vs trọng lực, flat 1 màu + múi phân đoạn bằng nét mảnh
function drawBalloon(ctx, x, y) {
  ctx.save();
  ctx.fillStyle = getVar('--jade');
  ctx.beginPath(); ctx.arc(x,y,52,0,Math.PI*2); ctx.fill();

  // Múi dọc — nét mảnh cùng tông đậm hơn, không phải bóng đổ
  ctx.strokeStyle = getVar('--jade-deep'); ctx.lineWidth = 1.5;
  [-22,0,22].forEach(dx => {
    ctx.beginPath(); ctx.moveTo(x+dx,y-52);
    ctx.quadraticCurveTo(x+dx+9,y,x+dx,y+52); ctx.stroke();
  });

  // Dây treo
  ctx.strokeStyle = getVar('--ink-2'); ctx.lineWidth = 1;
  [[-22,50],[0,54],[22,50]].forEach(([dx,dy]) => {
    ctx.beginPath(); ctx.moveTo(x+dx,y+dy); ctx.lineTo(x+dx*.3,y+82); ctx.stroke();
  });

  // Giỏ
  ctx.fillStyle = getVar('--ink-2');
  ctx.beginPath(); ctx.roundRect(x-20,y+80,40,24,5); ctx.fill();
  ctx.restore();
}
```

### drawCloud(ctx, x, y, size) — dùng làm mốc tham chiếu, không phải trang trí bầu trời màu

```javascript
function drawCloud(ctx, x, y, size=60) {
  ctx.fillStyle = getVar('--cream-2');
  ctx.strokeStyle = getVar('--paper-line'); ctx.lineWidth = 1;
  [[0,0,size*.5],[size*.35,-size*.2,size*.4],[size*.7,0,size*.45],[size*.15,size*.1,size*.35]]
    .forEach(([dx,dy,r]) => {
      ctx.beginPath(); ctx.arc(x+dx,y+dy,r,0,Math.PI*2); ctx.fill(); ctx.stroke();
    });
}
```

### drawBackground — SCHEMATIC HOÁ (thay hoàn toàn drawSkyBg/drawSeaBg/drawGroundBg cũ)

```javascript
// Quy tắc chung: nền luôn --cream + lưới toạ độ mờ --paper-line. Đường chân trời (nếu cần
// gợi ý "trên không" hay "trên biển") chỉ là 1 đường mảnh, KHÔNG tô màu nền khác biệt.

function drawSchematicBg(ctx, CW, CH, gridStep = 40) {
  ctx.fillStyle = getVar('--cream');
  ctx.fillRect(0, 0, CW, CH);
  ctx.strokeStyle = getVar('--paper-line');
  ctx.lineWidth = 1;
  for (let x = 0; x < CW; x += gridStep) {
    ctx.beginPath(); ctx.moveTo(x, 0); ctx.lineTo(x, CH); ctx.stroke();
  }
  for (let y = 0; y < CH; y += gridStep) {
    ctx.beginPath(); ctx.moveTo(0, y); ctx.lineTo(CW, y); ctx.stroke();
  }
}

// Đường chân trời mảnh — dùng cho máy bay/khinh khí cầu (không tô trời xanh)
function drawHorizonLine(ctx, CW, CH, ratio = 0.7) {
  ctx.strokeStyle = getVar('--paper-line'); ctx.lineWidth = 1.5;
  ctx.beginPath(); ctx.moveTo(0, CH*ratio); ctx.lineTo(CW, CH*ratio); ctx.stroke();
}

// Dải mặt đất/mặt sàn — 1 khối đặc cream-2 viền paper-line, KHÔNG gradient xanh lá
function drawGroundBar(ctx, CW, CH, ratio = 0.85) {
  ctx.fillStyle = getVar('--cream-2');
  ctx.strokeStyle = getVar('--paper-line'); ctx.lineWidth = 1;
  ctx.fillRect(0, CH*ratio, CW, CH*(1-ratio));
  ctx.beginPath(); ctx.moveTo(0, CH*ratio); ctx.lineTo(CW, CH*ratio); ctx.stroke();
}

// Sóng biển — nét mảnh sage, không tô mảng nước xanh đậm
function drawWaveLines(ctx, CW, CH, ratio = 0.75, rows = 3) {
  ctx.strokeStyle = getVar('--sage'); ctx.lineWidth = 1.2; ctx.lineCap = 'round';
  for (let i = 0; i < rows; i++) {
    ctx.beginPath(); ctx.moveTo(0, CH*(ratio + i*0.05));
    for (let x = 0; x < CW; x += 60) {
      ctx.quadraticCurveTo(x+30, CH*(ratio - 0.02 + i*0.05), x+60, CH*(ratio + i*0.05));
    }
    ctx.stroke();
  }
}

// Dùng phối hợp, ví dụ cho bài máy bay:
// drawSchematicBg(ctx, CW, CH); drawHorizonLine(ctx, CW, CH, 0.65); drawCloud(ctx, CW*.2, CH*.15, 50);
```

---

## PHẦN 7 — HỆ THỐNG MINH HOẠ TÌNH HUỐNG & CẢNH BÁO (BẮT BUỘC)

> Dùng cho: bài an toàn thí nghiệm, phân loại tình huống đúng/sai, minh hoạ quy trình, và mọi
> bài cần vẽ "tình huống" thay vì vector/lực. Đây là phần khắc phục lỗi phổ biến nhất của dạng
> bài này: mỗi cảnh tự bịa 1 kiểu cảnh báo riêng, màu không gắn nghĩa cố định, không có điểm nhấn
> rõ ràng khiến sản phẩm trông rối và không trực quan dù từng hình vẽ riêng lẻ không xấu.

### 7.1 Nguyên tắc cốt lõi (đọc trước khi vẽ bất kỳ cảnh nào)

```
1. MÀU GẮN CỐ ĐỊNH VỚI 1 NGHĨA DUY NHẤT — xem bảng SIGNAL ở 7.2. Không dùng --jade
   cho "nước trong ly" ở cảnh này rồi lại dùng --jade cho "mũi tên tăng dần" ở cảnh khác.
   Nếu 1 màu đã gắn nghĩa "an toàn", nó chỉ được dùng cho ý nghĩa an toàn xuyên suốt toàn bài.

2. MỖI CẢNH CHỈ CÓ 1 ĐIỂM NHẤN (focal point) — vật thể/hành động liên quan trực tiếp đến bài học
   được vẽ full chi tiết + màu đúng token SIGNAL. Mọi thứ còn lại là bối cảnh phụ, vẽ nhạt hơn
   (xem 7.4 applyBackgroundDim). Không để 2-3 điểm cùng "gào" thị giác ngang nhau trong 1 cảnh.

3. 1 KÝ HIỆU CHO 1 Ý NGHĨA, DÙNG LẶP LẠI XUYÊN SUỐT — không tự bịa cách cảnh báo mới cho mỗi
   cảnh. Dùng đúng hàm drawSignalMark() ở 7.2 cho mọi tình huống nguy hiểm/an toàn/lưu ý, để học
   sinh nhận diện được pattern lặp lại thay vì phải diễn giải lại từ đầu mỗi màn.

4. KHÔNG dùng emoji trong canvas (fillText('⚠️',...)) — emoji phụ thuộc font hệ điều hành, render
   không nhất quán giữa các máy/trình duyệt. Luôn vẽ icon bằng path (xem drawSignalMark 7.2).

5. KHÔNG dùng halo/glow nhiều lớp rgba chồng nhau để nhấn mạnh — thay bằng 1 vòng outline mảnh
   (xem drawFocusRing ở 2.3 "Snap + Pulse", tái dùng cho mọi mục đích nhấn mạnh, không chỉ khớp/sai).

6. MỨC ĐỘ CHI TIẾT ĐỒNG ĐỀU — dùng đúng 3 tier ở 7.5, không để cảnh này chi tiết như tranh vẽ,
   cảnh khác chỉ 2 hình tròn sơ sài.
```

### 7.2 Bảng SIGNAL — màu gắn nghĩa cố định (dựa trên token đã có, không thêm hex mới)

```javascript
// Định nghĩa 1 lần, dùng xuyên suốt toàn bộ file HTML — không định nghĩa lại ở từng cảnh
const SIGNAL = {
  danger:  { color: getVar('--wrong'),    bg: getVar('--wrong-bg') },   // nguy hiểm, sai, cảnh báo
  safe:    { color: getVar('--correct'),  bg: getVar('--correct-bg') }, // an toàn, đúng quy trình
  info:    { color: getVar('--jade-text'),bg: getVar('--jade-pale') },  // lưu ý trung tính, hướng dẫn
  neutral: { color: getVar('--ink-2'),    bg: getVar('--cream-2') },    // vật thể/bối cảnh phụ
};

// Icon vẽ bằng path — KHÔNG dùng emoji, KHÔNG phụ thuộc webfont trong canvas
// type: 'danger' | 'safe' | 'info'
function drawSignalMark(ctx, x, y, type, size = 22) {
  const s = SIGNAL[type];
  ctx.save();
  ctx.translate(x, y);

  // Nền tròn — luôn 1 màu đặc, không gradient
  ctx.fillStyle = s.bg;
  ctx.beginPath(); ctx.arc(0, 0, size, 0, Math.PI * 2); ctx.fill();
  ctx.strokeStyle = s.color; ctx.lineWidth = 2;
  ctx.beginPath(); ctx.arc(0, 0, size, 0, Math.PI * 2); ctx.stroke();

  ctx.strokeStyle = s.color; ctx.fillStyle = s.color;
  ctx.lineWidth = 2.5; ctx.lineCap = 'round'; ctx.lineJoin = 'round';

  if (type === 'danger') {
    // Dấu chấm than trong tam giác — vẽ path, không emoji
    const r = size * 0.55;
    ctx.beginPath();
    ctx.moveTo(0, -r); ctx.lineTo(r * 0.87, r * 0.6); ctx.lineTo(-r * 0.87, r * 0.6);
    ctx.closePath(); ctx.stroke();
    ctx.beginPath(); ctx.moveTo(0, -r * 0.15); ctx.lineTo(0, r * 0.2); ctx.stroke();
    ctx.beginPath(); ctx.arc(0, r * 0.4, 1.6, 0, Math.PI * 2); ctx.fill();
  } else if (type === 'safe') {
    // Dấu check
    const r = size * 0.5;
    ctx.beginPath();
    ctx.moveTo(-r, 0); ctx.lineTo(-r * 0.2, r * 0.7); ctx.lineTo(r, -r * 0.6);
    ctx.stroke();
  } else if (type === 'info') {
    // Chữ "i" — vẽ bằng chấm + đường thẳng, không dùng font
    const r = size * 0.45;
    ctx.beginPath(); ctx.arc(0, -r * 0.55, 1.8, 0, Math.PI * 2); ctx.fill();
    ctx.beginPath(); ctx.moveTo(0, -r * 0.1); ctx.lineTo(0, r * 0.6); ctx.stroke();
  }
  ctx.restore();
}

// Dùng thống nhất cho MỌI cảnh — thay toàn bộ emoji/halo tự chế cũ:
// drawSignalMark(ctx, dangerX, dangerY, 'danger');
// drawSignalMark(ctx, safeX, safeY, 'safe');
```

### 7.3 Nhấn mạnh điểm nguy hiểm — thay halo nhiều lớp bằng 1 outline pulse

```javascript
// Tái dùng đúng drawPulse() ở PHẦN 2.3, chỉ đổi input theo SIGNAL thay vì near/match
// Ví dụ: khoanh vùng nguy hiểm quanh 1 vật thể (thay cho vòng nét đứt + emoji rời rạc cũ)
function drawDangerZone(ctx, x, y, radius) {
  pulsePhase = (pulsePhase + 0.06) % (Math.PI * 2);
  const alpha = 0.5 + 0.3 * Math.sin(pulsePhase);
  ctx.save();
  ctx.strokeStyle = `rgba(193,95,60,${alpha})`; // --wrong ở dạng rgba
  ctx.lineWidth = 2.5;
  ctx.setLineDash([6, 4]);
  ctx.beginPath(); ctx.arc(x, y, radius, 0, Math.PI * 2); ctx.stroke();
  ctx.setLineDash([]);
  ctx.restore();
  // Gắn kèm 1 drawSignalMark('danger') tại rìa vòng tròn — KHÔNG chồng thêm lớp halo rgba mờ nào khác
}
```

### 7.4 Phân cấp thị giác — 1 điểm nhấn, phần còn lại làm nền mờ hơn

```javascript
// Bọc mọi lệnh vẽ bối cảnh/vật phụ trong applyBackgroundDim() để chúng lùi về sau thị giác,
// nhường điểm nhấn (focal object) nổi bật rõ ràng
function withDim(ctx, drawFn, alpha = 0.55) {
  ctx.save();
  ctx.globalAlpha = alpha;
  drawFn();
  ctx.restore();
}

// Mẫu dùng trong 1 hàm draw() của 1 cảnh:
// draw: function(ctx, w, h) {
//   drawBaseLabBackground(ctx, w, h);                 // nền — mặc định
//   withDim(ctx, () => drawShelf(ctx, w, h));          // vật phụ — làm mờ 45%
//   withDim(ctx, () => drawOtherStudent(ctx, w, h));   // vật phụ — làm mờ 45%
//   drawFlaskBeingHeld(ctx, focalX, focalY);           // FOCAL — vẽ full alpha, full chi tiết
//   drawSignalMark(ctx, focalX + 30, focalY - 30, 'safe'); // ký hiệu gắn ngay tại điểm nhấn
// }
```

### 7.5 3 Tier chi tiết — đảm bảo đồng đều giữa các cảnh

```
Tier "silhouette" (bối cảnh/vật phụ, KHÔNG phải trọng tâm bài học):
  - Tối đa 1-2 lệnh vẽ (1 shape + 1 outline)
  - Luôn bọc trong withDim()
  - Ví dụ: bàn thí nghiệm phía sau, bạn học đứng cạnh, giá đỡ dụng cụ

Tier "functional" (vật thể liên quan nhưng không phải trọng tâm trực tiếp):
  - 3-5 lệnh vẽ, đủ để nhận diện rõ vật là gì
  - Màu neutral (--ink-2) trừ khi bản thân vật đó mang tín hiệu SIGNAL
  - Ví dụ: đèn cồn khi trọng tâm là "cách cầm kẹp", kính bảo hộ khi trọng tâm là "đang đun bình"

Tier "focal" (ĐÚNG 1 vật/hành động mỗi cảnh — trọng tâm bài học):
  - 5-8 lệnh vẽ, chi tiết nhất trong cảnh, màu full theo SIGNAL nếu liên quan an toàn
  - Luôn có 1 drawSignalMark() gắn kèm để xác nhận ý nghĩa (an toàn/nguy hiểm/lưu ý)
  - Ví dụ: tay đang gắp bình bằng kẹp (không phải cả cái bình hay cả đèn cồn)

Quy tắc nhanh: trước khi build 1 cảnh, tự hỏi "trọng tâm bài học là GÌ, cụ thể đến mức nào?"
Nếu câu trả lời mơ hồ ("cảnh làm thí nghiệm nhiệt") → cảnh sẽ vẽ dàn trải, không có tier "focal"
rõ ràng. Nếu cụ thể ("tay dùng kẹp gắp bình, không cầm tay không") → tier focal rõ ràng ngay.
```

### 7.6 Font & số liệu trong canvas — áp dụng cho mọi loại bài, không riêng Vật Lý

```javascript
// Đồng bộ với 02_design_ly.md mục 1.3 — áp dụng cho MỌI canvas, kể cả bài an toàn/kỹ năng:
// - Nhãn số liệu (điện áp, thời gian, %...) → LUÔN 'Inconsolata', monospace, tabular-nums
// - Nhãn tên vật thể/hướng dẫn ngắn → 'Be Vietnam Pro' (đúng font UI toàn LMS — KHÔNG Playfair Display)
// - KHÔNG dùng Courier New hay Plus Jakarta Sans như file cũ — chỉ 2 font này, đúng vai trò cố định

ctx.font = "bold 11px 'Inconsolata', monospace";     // dùng cho: "12V", "85%", "t=3.2s"...
ctx.font = "bold 13px 'Be Vietnam Pro', sans-serif";  // dùng cho: "TĂNG TỪ TỪ", "KÍNH BẢO HỘ"...
```

### 7.7 Checklist riêng cho bài tình huống/an toàn (bổ sung checklist 2.8 của design_ly.md)

```
- [ ] Toàn bài chỉ dùng 1 hàm drawSignalMark() cho mọi cảnh báo — không có emoji hay
      halo/glow tự chế riêng lẻ ở bất kỳ cảnh nào
- [ ] Mỗi cảnh xác định rõ đúng 1 focal object, vật phụ đều bọc trong withDim()
- [ ] Màu SIGNAL (danger/safe/info) dùng đúng nghĩa cố định xuyên suốt, không tái dùng cho nghĩa khác
- [ ] Mức chi tiết theo đúng 3 tier ở 7.5, không có cảnh nào "công phu hẳn" hoặc "sơ sài hẳn" bất thường
- [ ] Font canvas chỉ Inconsolata (số liệu) + Be Vietnam Pro (nhãn) — không Courier New/Plus Jakarta Sans/Playfair Display
```

---

## PHỤ LỤC — REFERENCES

### Kỹ thuật canvas — nguồn đáng tin

```
MDN Canvas API Tutorial:
  developer.mozilla.org/en-US/docs/Web/API/Canvas_API/Tutorial
  → Hit detection, path, compositing, transforms

Redblobgames (Amit Patel):
  redblobgames.com
  → Thuật toán: point-to-segment, A*, hex grid, isometric

GitHub gist — Canvas Optimization:
  gist.github.com/jaredwilli/5469626
  → Redraw regions, offscreen canvas, best practices
```

### Simulation vật lý tham khảo

```
Walter Fendt Physics HTML5:
  walter-fendt.de/html5/phen
  → Mặt phẳng nghiêng, lực, dao động — xem cách họ làm (tham khảo LOGIC, không copy màu/style)

Open Source Physics @ Singapore:
  sg.iwant2study.org/ospsg
  → Simulation miễn phí, có source code, CC license

PhysicsClassroom Interactive:
  physicsclassroom.com/Physics-Interactives
  → Tham khảo UX và pedagogy cho simulation lực
```

### Khi nào cần Three.js

```
Dùng Three.js khi:
  - Học sinh cần XOAY vật 3D tự do (OrbitControls)
  - Animation 3D phức tạp (keyframe, skinning)
  - Hiệu ứng ánh sáng thật (physically based rendering)

CDN: cdn.jsdelivr.net/npm/three@0.128.0/build/three.min.js
     (dùng r128 — OrbitControls tách riêng ở r142+)

KHÔNG dùng Three.js khi:
  - Chỉ cần nhìn từ góc cố định → Isometric 2D đủ
  - File HTML đơn không có server → Three.js module cần import map
  - Học sinh dùng thiết bị cũ → Three.js nặng (~600KB)

Lưu ý: nếu dùng Three.js, vật liệu (material) nên dùng MeshBasicMaterial/MeshLambertMaterial
phẳng với màu token, tránh MeshPhysicalMaterial/bóng gương phản chiếu — giữ đúng tinh thần flat.
```

---

> **Phiên bản:** 2.1 — hợp nhất với `Quy_chuan_tao_HTML_Aiducation.pdf` (Haugomat editorial flat)
> **Thay đổi so với 1.0:** bỏ toàn bộ `createRadialGradient`/`createLinearGradient`/glow/highlight
> giả 3D trong Object Library và Isometric; confetti nhiều màu → hiệu ứng viền + icon check tiết chế;
> mọi màu vector/lực tra token ở `02_design_ly.md`; bối cảnh nền (trời/biển/đất) schematic hoá hoàn
> toàn bằng nền cream + lưới paper-line; font canvas đổi sang Inconsolata; các pattern kỹ thuật thuần
> (hit detection, drag & drop, state machine, RAF, vector math, Euler loop) giữ nguyên không đổi.
> **Mới ở 2.1:** thêm PHẦN 7 — Hệ thống minh hoạ tình huống & cảnh báo (bảng SIGNAL gắn màu cố định
> với nghĩa, drawSignalMark() thay emoji/halo tự chế, phân cấp thị giác 1 điểm nhấn/cảnh, 3 tier chi
> tiết đồng đều) — khắc phục lỗi "không trực quan, không nhất quán" ở các bài tình huống/an toàn.
> **Dùng cùng:** `02_design_ly.md` (design tokens + layout/CSS)
