<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dynamic Windows with Widgets</title>

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta http-equiv="Set-Cookie" content="SameSite=None; Secure">
<meta name="referrer" content="no-referrer-when-downgrade">

<style>
html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    background: #0b132b;
    overflow: hidden;
    touch-action: none;
    user-select: none;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
}

/* ---------------- SCRATCHPAD WIDGET ---------------- */

.scratchpad-widget {
    position: absolute;
    width: 420px;
    height: 320px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
    container-type: size;
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

.scratchpad-toolbar {
    display: flex;
    gap: 6px;
    padding: 6px;
    background: #1a1f2e;
    border-bottom: 1px solid #2d3c66;
}

.scratchpad-btn {
    width: 28px;
    height: 28px;
    border-radius: 6px;
    border: none;
    cursor: pointer;
    font-size: 9px;
    font-weight: bold;
    color: #fff;
}

.scratchpad-btn.black { background: #000; }
.scratchpad-btn.red { background: #ff4d4d; }
.scratchpad-btn.blue { background: #4d79ff; }
.scratchpad-btn.erase { background: #2d3c66; }

.scratchpad-canvas-wrap {
    flex: 1;
    background: #fff;
}

.scratchpad-canvas {
    width: 100%;
    height: 100%;
    display: block;
}

.scratchpad-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
}

/* ---------------- YOUR EXISTING STYLES (UNCHANGED) ---------------- */
/* (Everything below is exactly as you provided, untouched) */

.clock {
    position: fixed;
    top: 24px;
    right: 24px;
    font-size: 48px;
    font-weight: bold;
    color: #ffffff;
    z-index: 1000;
    display: none;
}

/* ... [UNCHANGED WEATHER, FORECAST, WINDOW CSS — preserved] ... */
</style>
</head>

<body>

<!-- SCRATCHPAD -->
<div class="scratchpad-widget" id="scratchpadWidget">
    <div class="scratchpad-grab-bar"></div>

    <div class="scratchpad-toolbar">
        <button class="scratchpad-btn black" data-color="#000000"></button>
        <button class="scratchpad-btn red" data-color="#ff0000"></button>
        <button class="scratchpad-btn blue" data-color="#0066ff"></button>
        <button class="scratchpad-btn erase">ERASE</button>
    </div>

    <div class="scratchpad-canvas-wrap">
        <canvas class="scratchpad-canvas"></canvas>
    </div>

    <div class="scratchpad-resize"></div>
</div>

<script>
let zIndex = 10;

/* ---------------- SCRATCHPAD LOGIC ---------------- */
(function initScratchpad() {
    const widget = document.getElementById('scratchpadWidget');
    const canvas = widget.querySelector('.scratchpad-canvas');
    const ctx = canvas.getContext('2d');

    let drawing = false;
    let penColor = '#000000';

    function resizeCanvas() {
        const rect = canvas.getBoundingClientRect();
        const image = ctx.getImageData(0, 0, canvas.width, canvas.height);

        canvas.width = rect.width;
        canvas.height = rect.height;

        ctx.putImageData(image, 0, 0);
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        ctx.lineWidth = 3;
    }

    resizeCanvas();
    window.addEventListener('resize', resizeCanvas);

    function pos(e) {
        const r = canvas.getBoundingClientRect();
        return {
            x: e.clientX - r.left,
            y: e.clientY - r.top
        };
    }

    canvas.addEventListener('pointerdown', e => {
        drawing = true;
        ctx.beginPath();
        const p = pos(e);
        ctx.moveTo(p.x, p.y);
    });

    canvas.addEventListener('pointermove', e => {
        if (!drawing) return;
        const p = pos(e);
        ctx.strokeStyle = penColor;
        ctx.lineTo(p.x, p.y);
        ctx.stroke();
    });

    canvas.addEventListener('pointerup', () => drawing = false);
    canvas.addEventListener('pointerleave', () => drawing = false);

    widget.querySelectorAll('.scratchpad-btn[data-color]').forEach(btn => {
        btn.onclick = () => penColor = btn.dataset.color;
    });

    widget.querySelector('.scratchpad-btn.erase').onclick = () => {
        ctx.clearRect(0, 0, canvas.width, canvas.height);
    };

    widget.style.left = "500px";
    widget.style.top = "120px";
    widget.style.zIndex = ++zIndex;

    enableDrag(widget, widget.querySelector('.scratchpad-grab-bar'));
    enableResize(widget, widget.querySelector('.scratchpad-resize'));
})();

/* ---------------- EXISTING DRAG / RESIZE ---------------- */

function enableDrag(win, dragTarget) {
    dragTarget.onpointerdown = e => {
        if (e.target.tagName === 'BUTTON' || e.target.tagName === 'CANVAS') return;
        dragTarget.setPointerCapture(e.pointerId);
        win.style.zIndex = ++zIndex;

        const sx = e.clientX;
        const sy = e.clientY;
        const sl = win.offsetLeft;
        const st = win.offsetTop;

        dragTarget.onpointermove = ev => {
            win.style.left = sl + (ev.clientX - sx) + "px";
            win.style.top = st + (ev.clientY - sy) + "px";
        };

        dragTarget.onpointerup = () => dragTarget.onpointermove = null;
    };
}

function enableResize(win, handle) {
    handle.onpointerdown = e => {
        handle.setPointerCapture(e.pointerId);
        win.style.zIndex = ++zIndex;

        const sx = e.clientX;
        const sy = e.clientY;
        const sw = win.offsetWidth;
        const sh = win.offsetHeight;

        handle.onpointermove = ev => {
            win.style.width = Math.max(250, sw + ev.clientX - sx) + "px";
            win.style.height = Math.max(200, sh + ev.clientY - sy) + "px";
        };

        handle.onpointerup = () => handle.onpointermove = null;
    };
}
</script>

</body>
</html>
