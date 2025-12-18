<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Widget Dashboard</title>
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
html, body {
    margin: 0;
    width: 100%;
    height: 100%;
    background: #0b132b;
    overflow: hidden;
    font-family: system-ui, sans-serif;
    touch-action: none;
}

/* ================= CORE WINDOW ================= */
.window,
.scratchpad-widget {
    position: absolute;
    background: #1a1f2e;
    border: 1px solid #2d3c66;
    border-radius: 12px;
    box-shadow: 0 20px 40px rgba(0,0,0,.8);
    display: flex;
    flex-direction: column;
    overflow: hidden;
}

.grab-bar,
.scratchpad-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: center;
}

.grab-bar::before,
.scratchpad-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    opacity: .6;
    letter-spacing: 2px;
}

.resize,
.scratchpad-resize {
    position: absolute;
    right: 0;
    bottom: 0;
    width: 22px;
    height: 22px;
    cursor: nwse-resize;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
}

/* ================= CLOCK ================= */
#clock {
    position: fixed;
    top: 20px;
    right: 20px;
    font-size: 42px;
    color: white;
    font-weight: bold;
    z-index: 9999;
}

/* ================= WEATHER ================= */
.weather {
    padding: 12px;
    color: white;
    font-size: 14px;
}

/* ================= SCRATCHPAD ================= */
.scratchpad-widget {
    width: 420px;
    height: 320px;
}

.scratchpad-toolbar {
    display: flex;
    align-items: center;
    gap: 8px;
    padding: 6px;
    background: #1a1f2e;
    border-bottom: 1px solid #2d3c66;
}

.color-gradient {
    width: 120px;
    height: 24px;
    border-radius: 6px;
    cursor: crosshair;
}

.eraser-toggle,
.clear-btn {
    font-size: 10px;
    padding: 4px 8px;
    border-radius: 6px;
    border: none;
    background: #2d3c66;
    color: white;
    cursor: pointer;
}

.eraser-toggle.active {
    background: #ffcc00;
    color: #000;
}

.thickness {
    width: 70px;
}

.scratchpad-canvas-wrap {
    flex: 1;
    background: white;
}

.draw-canvas {
    width: 100%;
    height: 100%;
    display: block;
}

/* ================= PLUS BUTTON ================= */
#addBtn {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%);
    width: 56px;
    height: 56px;
    border-radius: 50%;
    background: #4d79ff;
    color: white;
    font-size: 32px;
    border: none;
    cursor: pointer;
}
</style>
</head>

<body>

<div id="clock"></div>

<!-- WEATHER -->
<div class="window" style="left:20px;top:20px;width:220px;height:140px;">
    <div class="grab-bar"></div>
    <div class="weather">
        <b>Weather</b><br>
        Temp: 72°F<br>
        Clear skies
    </div>
    <div class="resize"></div>
</div>

<!-- RADAR -->
<div class="window" style="left:260px;top:20px;width:360px;height:260px;">
    <div class="grab-bar"></div>
    <iframe src="https://www.weather.gov" style="border:0;width:100%;height:100%;"></iframe>
    <div class="resize"></div>
</div>

<!-- SCRATCHPAD -->
<div class="scratchpad-widget" id="scratchpadWidget" style="left:200px;top:320px;">
    <div class="scratchpad-grab-bar"></div>

    <div class="scratchpad-toolbar">
        <canvas class="color-gradient"></canvas>
        <button class="eraser-toggle">ERASER</button>
        <input type="range" min="1" max="12" value="3" class="thickness">
        <button class="clear-btn">CLEAR</button>
    </div>

    <div class="scratchpad-canvas-wrap">
        <canvas class="draw-canvas"></canvas>
    </div>

    <div class="scratchpad-resize"></div>
</div>

<button id="addBtn">+</button>

<script>
let zIndex = 10;

/* ================= CLOCK ================= */
setInterval(() => {
    const d = new Date();
    document.getElementById('clock').textContent =
        d.toLocaleTimeString([], {hour:'2-digit',minute:'2-digit'});
}, 1000);

/* ================= DRAG / RESIZE ================= */
function enableDrag(win, handle) {
    handle.onpointerdown = e => {
        win.style.zIndex = ++zIndex;
        const sx = e.clientX, sy = e.clientY;
        const sl = win.offsetLeft, st = win.offsetTop;
        handle.setPointerCapture(e.pointerId);

        handle.onpointermove = ev => {
            win.style.left = sl + ev.clientX - sx + 'px';
            win.style.top  = st + ev.clientY - sy + 'px';
        };
        handle.onpointerup = () => handle.onpointermove = null;
    };
}

function enableResize(win, handle) {
    handle.onpointerdown = e => {
        win.style.zIndex = ++zIndex;
        const sx = e.clientX, sy = e.clientY;
        const sw = win.offsetWidth, sh = win.offsetHeight;
        handle.setPointerCapture(e.pointerId);

        handle.onpointermove = ev => {
            win.style.width  = Math.max(200, sw + ev.clientX - sx) + 'px';
            win.style.height = Math.max(150, sh + ev.clientY - sy) + 'px';
        };
        handle.onpointerup = () => handle.onpointermove = null;
    };
}

document.querySelectorAll('.window').forEach(w => {
    enableDrag(w, w.querySelector('.grab-bar'));
    enableResize(w, w.querySelector('.resize'));
});

/* ================= SCRATCHPAD ================= */
(() => {
    const w = document.getElementById('scratchpadWidget');
    const canvas = w.querySelector('.draw-canvas');
    const ctx = canvas.getContext('2d');
    const grad = w.querySelector('.color-gradient');
    const gctx = grad.getContext('2d');

    let drawing=false, erasing=false, color='#000', size=3;

    function resize() {
        canvas.width = canvas.offsetWidth;
        canvas.height = canvas.offsetHeight;
    }
    resize();

    const g = gctx.createLinearGradient(0,0,grad.width,0);
    ['red','yellow','lime','cyan','blue','magenta','red']
        .forEach((c,i)=>g.addColorStop(i/6,c));
    gctx.fillStyle=g; gctx.fillRect(0,0,grad.width,grad.height);

    grad.onpointerdown = e => {
        const r = grad.getBoundingClientRect();
        const d = gctx.getImageData(e.clientX-r.left,e.clientY-r.top,1,1).data;
        color=`rgb(${d[0]},${d[1]},${d[2]})`;
        erasing=false;
        w.querySelector('.eraser-toggle').classList.remove('active');
    };

    canvas.onpointerdown = e => {
        drawing=true;
        ctx.beginPath();
        ctx.moveTo(e.offsetX,e.offsetY);
    };

    canvas.onpointermove = e => {
        if(!drawing) return;
        ctx.lineWidth=size;
        ctx.lineCap='round';
        ctx.strokeStyle=color;
        ctx.globalCompositeOperation = erasing?'destination-out':'source-over';
        ctx.lineTo(e.offsetX,e.offsetY);
        ctx.stroke();
    };

    canvas.onpointerup = () => drawing=false;

    w.querySelector('.eraser-toggle').onclick = e=>{
        erasing=!erasing;
        e.target.classList.toggle('active',erasing);
    };

    w.querySelector('.thickness').oninput = e=>size=e.target.value;
    w.querySelector('.clear-btn').onclick = ()=>ctx.clearRect(0,0,canvas.width,canvas.height);

    enableDrag(w,w.querySelector('.scratchpad-grab-bar'));
    enableResize(w,w.querySelector('.scratchpad-resize'));
})();
</script>

</body>
</html>
