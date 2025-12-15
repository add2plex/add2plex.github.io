<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Movable Weather Radar</title>

<meta name="viewport"
      content="width=device-width, height=device-height, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
    html, body {
        width: 100%;
        height: 100%;
        margin: 0;
        background-color: #0b132b; /* dark near-black blue */
        overflow: hidden;

        touch-action: manipulation;
        -webkit-user-select: none;
        user-select: none;
        -webkit-tap-highlight-color: transparent;
    }

    /* Window shell */
    .window {
        position: absolute;
        top: 5%;
        left: 5%;
        width: 90%;
        height: 85%;
        background: #000;
        border: 2px solid #1f2a44;
        border-radius: 10px;
        box-shadow: 0 15px 40px rgba(0,0,0,0.8);
        display: flex;
        flex-direction: column;
    }

    /* Drag handle */
    .title-bar {
        height: 40px;
        background: #121a33;
        color: #8fb4ff;
        font-size: 14px;
        display: flex;
        align-items: center;
        padding: 0 12px;
        cursor: move;
        border-bottom: 1px solid #1f2a44;
        touch-action: none;
    }

    iframe {
        flex: 1;
        border: none;
    }

    /* Resize handle */
    .resize-handle {
        position: absolute;
        width: 22px;
        height: 22px;
        right: 0;
        bottom: 0;
        cursor: nwse-resize;
        background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
        touch-action: none;
    }
</style>
</head>
<body>

<div class="window" id="window">
    <div class="title-bar" id="dragHandle">
        NOAA Weather Radar
    </div>

    <iframe
        src="https://radar.weather.gov/?settings=v1_eyJhZ2VuZGEiOnsiaWQiOiJ3ZWF0aGVyIiwiY2VudGVyIjpbLTg1LjczOSwzMC4xNDhdLCJsb2NhdGlvbiI6Wy04NS43MDEsMzAuMjQ1XSwiem9vbSI6Ny41NDQ1MTg3MjM5NDYwOSwibGF5ZXIiOiJicmVmX3FjZCJ9LCJhbmltYXRpbmciOnRydWUsImJhc2UiOiJzdGFuZGFyZCIsImFydGNjIjpmYWxzZSwiY291bnR5IjpmYWxzZSwiY3dhIjpmYWxzZSwicmZjIjpmYWxzZSwiY3RhdGUiOmZhbHNlLCJtZW51Ijp0cnVlLCJzaG9ydEZ1c2VkT25seSI6dHJ1ZSwib3BhY2l0eSI6eyJhbGVydHMiOjAuOCwibG9jYWwiOjAuNiwibG9jYWxTdGF0aW9ucyI6MC44LCJuYXRpb25hbCI6MC42fX0%3D">
    </iframe>

    <div class="resize-handle" id="resizeHandle"></div>
</div>

<script>
const win = document.getElementById("window");
const drag = document.getElementById("dragHandle");
const resize = document.getElementById("resizeHandle");

let startX, startY, startW, startH, startL, startT;

/* Dragging */
drag.addEventListener("pointerdown", e => {
    startX = e.clientX;
    startY = e.clientY;
    startL = win.offsetLeft;
    startT = win.offsetTop;
    drag.setPointerCapture(e.pointerId);

    const move = ev => {
        win.style.left = startL + (ev.clientX - startX) + "px";
        win.style.top  = startT + (ev.clientY - startY) + "px";
    };

    drag.addEventListener("pointermove", move);
    drag.addEventListener("pointerup", () => {
        drag.removeEventListener("pointermove", move);
    }, { once: true });
});

/* Resizing */
resize.addEventListener("pointerdown", e => {
    startX = e.clientX;
    startY = e.clientY;
    startW = win.offsetWidth;
    startH = win.offsetHeight;
    resize.setPointerCapture(e.pointerId);

    const resizeMove = ev => {
        win.style.width  = Math.max(300, startW + (ev.clientX - startX)) + "px";
        win.style.height = Math.max(200, startH + (ev.clientY - startY)) + "px";
    };

    resize.addEventListener("pointermove", resizeMove);
    resize.addEventListener("pointerup", () => {
        resize.removeEventListener("pointermove", resizeMove);
    }, { once: true });
});
</script>

</body>
</html>
