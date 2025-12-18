<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dynamic Windows with Scratchpad</title>

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    background: #0b132b;
    overflow: hidden;
    touch-action: none;
    user-select: none;
    font-family: system-ui, sans-serif;
}

/* ================= WINDOW SYSTEM ================= */
.scratchpad-widget {
    position: absolute;
    width: 420px;
    height: 320px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    display: flex;
    flex-direction: column;
    touch-action: none;
    overflow: hidden;
}

.scratchpad-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: center;
}

.scratchpad-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.scratchpad-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
}

/* ================= TOOLBAR ================= */
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
    border: 1px solid #000;
}

.eraser-toggle,
.clear-btn {
    height: 24px;
    padding: 0 8px;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    font-size: 10px;
    font-weight: bold;
    color: #fff;
    background: #2d3c66;
}

.eraser-toggle.active {
    background: #ffcc00;
    color: #000;
}

.thickness {
    width: 70px;
}

/* ================= CANVAS ================= */
.scratchpad-canvas-wrap {
    flex: 1;
    background: #fff;
}

canvas {
    width: 100%;
    height: 100%;
    display: block;
}
</style>
</head>

<body>

<!-- ================= SCRATCHPAD ================= -->
<div class="scratchpad-widget" id="scratchpad">
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

<script>
let zIndex = 10;

/* ================= SCRATCHPAD LOGIC ================= */
(() => {
    const widget = document.getElementById('scratchpad');
    const drawCanvas = widget.querySelector('.draw-canvas');
    const drawCtx = drawCanvas.getContext('2d');

    const gradientCanvas = widget.querySelector('.color-gradient');
    const gradCtx = gradientCanvas.getContext('2d');

    let drawing = false;
    let penColor = '#000';
    let penSize = 3;
    let erasing = false;

    /* ----- Resize drawing canvas ----- */
    function resizeDrawCanvas() {
        const img = drawCtx.getImageData(0, 0, drawCanvas.width, drawCanvas.height);
        drawCanvas.width = drawCanvas.offsetWidth;
        drawCanvas.height = drawCanvas.offsetHeight;
        drawCtx.putImageData(img, 0, 0);
    }

    resizeDrawCanvas();
    window.addEventListener('resize', resizeDrawCanvas);

    /* ----- Build color gradient ----- */
    function buildGradient() {
        gradientCanvas.width = gradientCanvas.offsetWidth;
        gradientCanvas.height = gradientCanvas.offsetHeight;

        const g1 = gradCtx.createLinearGradient(0, 0, gradientCanvas.width, 0);
        g1.addColorStop(0, 'red');
        g1.addColorStop(0.17, 'yellow');
        g1.addColorStop(0.34, 'lime');
        g1.addColorStop(0.51, 'cyan');
        g1.addColorStop(0.68, 'blue');
        g1.addColorStop(0.85, 'magenta');
        g1.addColorStop(1, 'red');

        gradCtx.fillStyle = g1;
        gradCtx.fillRect(0, 0, gradientCanvas.width, gradientCanvas.height);

        const g2 = gradCtx.createLinearGradient(0, 0, 0, gradientCanvas.height);
        g2.addColorStop(0, 'rgba(255,255,255,1)');
        g2.addColorStop(0.5, 'rgba(255,255,255,0)');
        g2.addColorStop(0.5, 'rgba(0,0,0,0)');
        g2.addColorStop(1, 'rgba(0,0,0,1)');

        gradCtx.fillStyle = g2;
        gradCtx.fillRect(0, 0, gradientCanvas.width, gradientCanvas.height);
    }

    buildGradient();

    /* ----- Pick color from gradient ----- */
    gradientCanvas.addEventListener('pointerdown', e => {
        const r = gradientCanvas.getBoundingClientRect();
        const x = e.clientX - r.left;
        const y = e.clientY - r.top;
        const data = gradCtx.getImageData(x, y, 1, 1).data;
        penColor = `rgb(${data[0]},${data[1]},${data[2]})`;
        erasing = false;
        eraserBtn.classList.remove('active');
    });

    /* ----- Drawing ----- */
    function pos(e) {
        const r = drawCanvas.getBoundingClientRect();
        return { x: e.clientX - r.left, y: e.clientY - r.top };
    }

    drawCanvas.onpointerdown = e => {
        drawing = true;
        drawCtx.beginPath();
        const p = pos(e);
        drawCtx.moveTo(p.x, p.y);
    };

    drawCanvas.onpointermove = e => {
        if (!drawing) return;
        const p = pos(e);
        drawCtx.lineCap = 'round';
        drawCtx.lineWidth = penSize;
        drawCtx.strokeStyle = penColor;
        drawCtx.globalCompositeOperation = erasing ? 'destination-out' : 'source-over';
        drawCtx.lineTo(p.x, p.y);
        drawCtx.stroke();
    };

    drawCanvas.onpointerup = () => drawing = false;
    drawCanvas.onpointerleave = () => drawing = false;

    /* ----- Controls ----- */
    const eraserBtn = widget.querySelector('.eraser-toggle');
    eraserBtn.onclick = () => {
        erasing = !erasing;
        eraserBtn.classList.toggle('active', erasing);
    };

    widget.querySelector('.thickness').oninput = e =>
        penSize = +e.target.value;

    widget.querySelector('.clear-btn').onclick = () =>
        drawCtx.clearRect(0, 0, drawCanvas.width, drawCanvas.height);

    /* ----- Position + behavior ----- */
    widget.style.left = '500px';
    widget.style.top = '200px';
    widget.style.zIndex = ++zIndex;

    enableDrag(widget, widget.querySelector('.scratchpad-grab-bar'));
    enableResize(widget, widget.querySelector('.scratchpad-resize'));
})();

/* ================= DRAG / RESIZE ================= */
function enableDrag(win, handle) {
    handle.onpointerdown = e => {
        handle.setPointerCapture(e.pointerId);
        win.style.zIndex = ++zIndex;
        const sx = e.clientX, sy = e.clientY;
        const sl = win.offsetLeft, st = win.offsetTop;

        handle.onpointermove = ev => {
            win.style.left = sl + ev.clientX - sx + 'px';
            win.style.top = st + ev.clientY - sy + 'px';
        };
        handle.onpointerup = () => handle.onpointermove = null;
    };
}

function enableResize(win, handle) {
    handle.onpointerdown = e => {
        handle.setPointerCapture(e.pointerId);
        win.style.zIndex = ++zIndex;
        const sx = e.clientX, sy = e.clientY;
        const sw = win.offsetWidth, sh = win.offsetHeight;

        handle.onpointermove = ev => {
            win.style.width = Math.max(250, sw + ev.clientX - sx) + 'px';
            win.style.height = Math.max(200, sh + ev.clientY - sy) + 'px';
            const c = win.querySelector('.draw-canvas');
            c.width = c.offsetWidth;
            c.height = c.offsetHeight;
        };
        handle.onpointerup = () => handle.onpointermove = null;
    };
}
</script>

</body>
</html>
