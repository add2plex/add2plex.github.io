<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Floating App Windows</title>

<meta name="viewport"
      content="width=device-width, height=device-height, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    background: #0b132b;
    overflow: hidden;
    touch-action: manipulation;
    user-select: none;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
}

/* Plus button */
.add-button {
    position: fixed;
    bottom: 24px;
    left: 50%;
    transform: translateX(-50%);
    width: 64px;
    height: 64px;
    border-radius: 50%;
    background: #1f2a44;
    color: #8fb4ff;
    font-size: 36px;
    font-weight: bold;
    border: none;
    cursor: pointer;
    z-index: 1000;
}

/* Window */
.window {
    position: absolute;
    width: 500px;
    height: 500px;
    background: #000;
    border-radius: 10px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
}

/* Drag bar */
.title-bar {
    height: 36px;
    background: #1a1f2e;
    cursor: move;
    border-bottom: 1px solid #2d3c66;
}

/* Content */
.iframe-wrap {
    flex: 1;
    overflow: hidden;
}

iframe {
    width: 100%;
    height: 100%;
    border: none;
    background: white;
}

/* Resize handle */
.resize {
    position: absolute;
    width: 20px;
    height: 20px;
    right: 0;
    bottom: 0;
    cursor: nwse-resize;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
}
</style>
</head>
<body>

<button class="add-button" id="addBtn">+</button>

<script>
let zIndex = 1;
const APP_URL = "http://192.168.1.69:3000";

document.getElementById("addBtn").onclick = createWindow;

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "60px";
    win.style.top = "60px";
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

    const bar = win.querySelector(".title-bar");
    const resize = win.querySelector(".resize");

    /* Drag */
    bar.onpointerdown = e => {
        bringToFront(win);
        let sx = e.clientX, sy = e.clientY;
        let sl = win.offsetLeft, st = win.offsetTop;
        bar.setPointerCapture(e.pointerId);

        bar.onpointermove = ev => {
            win.style.left = sl + (ev.clientX - sx) + "px";
            win.style.top  = st + (ev.clientY - sy) + "px";
        };

        bar.onpointerup = () => bar.onpointermove = null;
    };

    /* Resize */
    resize.onpointerdown = e => {
        bringToFront(win);
        let sx = e.clientX, sy = e.clientY;
        let sw = win.offsetWidth, sh = win.offsetHeight;
        resize.setPointerCapture(e.pointerId);

        resize.onpointermove = ev => {
            win.style.width  = Math.max(300, sw + (ev.clientX - sx)) + "px";
            win.style.height = Math.max(200, sh + (ev.clientY - sy)) + "px";
        };

        resize.onpointerup = () => resize.onpointermove = null;
    };

    win.onpointerdown = () => bringToFront(win);
}

function bringToFront(win) {
    win.style.zIndex = ++zIndex;
}
</script>

</body>
</html>
