<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Touch Window Launcher</title>

<meta name="viewport"
      content="width=device-width, height=device-height,
               initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    background: #0b132b;
    overflow: hidden;

    /* CRITICAL for touch reliability */
    touch-action: none;
    overscroll-behavior: none;
    user-select: none;
    -webkit-user-select: none;
    -webkit-touch-callout: none;

    font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
}

/* Add button */
.add-button {
    position: fixed;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%);
    width: 72px;
    height: 72px;
    border-radius: 50%;
    background: #1f2a44;
    color: #8fb4ff;
    font-size: 42px;
    font-weight: bold;
    border: none;
    z-index: 1000;

    display: flex;
    align-items: center;
    justify-content: center;

    touch-action: manipulation;
    cursor: pointer;
}

/* Window */
.window {
    position: absolute;
    width: 500px;
    height: 500px;
    background: #000;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);

    touch-action: none;
}

/* Drag bar (BIG for fingers) */
.title-bar {
    height: 48px;
    background: #1a1f2e;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;

    touch-action: none;
}

/* Content */
.iframe-wrap {
    flex: 1;
    background: black;
}

iframe {
    width: 100%;
    height: 100%;
    border: none;
}

/* Resize handle (BIG corner) */
.resize {
    position: absolute;
    width: 36px;
    height: 36px;
    right: 0;
    bottom: 0;
    background:
        linear-gradient(135deg,
            transparent 50%,
            #8fb4ff 50%);
    cursor: nwse-resize;

    touch-action: none;
}
</style>
</head>
<body>

<button class="add-button" id="addBtn">+</button>

<script>
const APP_URL = "http://192.168.1.69:3000";
let zIndex = 1;

document.getElementById("addBtn").addEventListener("click", createWindow);

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "40px";
    win.style.top = "40px";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="title-bar"></div>
        <div class="iframe-wrap">
            <iframe src="${APP_URL}"></iframe>
        </div>
        <div class="resize"></div>
    `;

    document.body.appendChild(win);
    bringToFront(win);

    enableDrag(win);
    enableResize(win);
}

/* Bring window to top */
function bringToFront(win) {
    win.style.zIndex = ++zIndex;
}

/* DRAGGING (touch-safe) */
function enableDrag(win) {
    const bar = win.querySelector(".title-bar");

    bar.addEventListener("pointerdown", e => {
        bringToFront(win);
        bar.setPointerCapture(e.pointerId);

        const startX = e.clientX;
        const startY = e.clientY;
        const startL = win.offsetLeft;
        const startT = win.offsetTop;

        const move = ev => {
            win.style.left = startL + (ev.clientX - startX) + "px";
            win.style.top  = startT + (ev.clientY - startY) + "px";
        };

        const up = () => {
            bar.releasePointerCapture(e.pointerId);
            bar.removeEventListener("pointermove", move);
            bar.removeEventListener("pointerup", up);
        };

        bar.addEventListener("pointermove", move);
        bar.addEventListener("pointerup", up);
    });
}

/* RESIZING (touch-safe) */
function enableResize(win) {
    const handle = win.querySelector(".resize");

    handle.addEventListener("pointerdown", e => {
        bringToFront(win);
        handle.setPointerCapture(e.pointerId);

        const startX = e.clientX;
        const startY = e.clientY;
        const startW = win.offsetWidth;
        const startH = win.offsetHeight;

        const move = ev => {
            win.style.width =
                Math.max(320, startW + (ev.clientX - startX)) + "px";
            win.style.height =
                Math.max(240, startH + (ev.clientY - startY)) + "px";
        };

        const up = () => {
            handle.releasePointerCapture(e.pointerId);
            handle.removeEventListener("pointermove", move);
            handle.removeEventListener("pointerup", up);
        };

        handle.addEventListener("pointermove", move);
        handle.addEventListener("pointerup", up);
    });
}
</script>

</body>
</html>
