<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dynamic Windows with URL Input</title>

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
    font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
}

/* Plus button */
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

/* Input bar */
.input-bar {
    height: 48px;
    display: flex;
    padding: 6px;
    gap: 6px;
    background: #1a1f2e;
    border-bottom: 1px solid #2d3c66;
    align-items: center;
}

.close-btn {
    width: 32px;
    height: 32px;
    border-radius: 16px;
    border: none;
    background: #2d3c66;
    color: #ff6b6b;
    font-size: 18px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.input-bar input {
    flex: 1;
    height: 32px;
    border-radius: 16px;
    border: none;
    padding: 0 12px;
    font-size: 14px;
    background: #0f1320;
    color: #fff;
    outline: none;
}

.input-bar button {
    height: 32px;
    padding: 0 14px;
    border-radius: 16px;
    border: none;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 14px;
    cursor: pointer;
}

/* Iframe container */
.iframe-wrap {
    flex: 1;
    overflow: hidden;
}

iframe {
    width: 100%;
    height: 100%;
    border: none;
}

iframe[sandbox] {
    /* Allow forms, scripts, popups, and same-origin for authentication flows */
}

/* Resize handle */
.resize {
    position: absolute;
    width: 36px;
    height: 36px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
}
</style>
</head>
<body>

<button class="add-button" id="addBtn">+</button>

<script>
let zIndex = 1;

document.getElementById("addBtn").addEventListener("click", createWindow);

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "40px";
    win.style.top = "40px";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="input-bar">
            <button class="close-btn">×</button>
            <input type="text" placeholder="Enter URL or search term">
            <button>Go</button>
        </div>
        <div class="iframe-wrap">
            <iframe sandbox="allow-same-origin allow-scripts allow-forms allow-popups allow-popups-to-escape-sandbox allow-top-navigation-by-user-activation" src=""></iframe>
        </div>
        <div class="resize"></div>
    `;

    document.body.appendChild(win);
    bringToFront(win);

    enableDrag(win);
    enableResize(win);
    enableInput(win);
    enableClose(win);
}

function enableInput(win) {
    const input = win.querySelector(".input-bar input");
    const button = win.querySelector(".input-bar button:not(.close-btn)");
    const iframe = win.querySelector("iframe");

    function navigate() {
        let value = input.value.trim();
        if (!value) return;

        let url;
        if (/^https?:\/\//i.test(value)) {
            url = value;
        } else if (value.startsWith("localhost") || value.startsWith("127.0.0.1") || /^localhost:/i.test(value) || /^127\.0\.0\.1:/i.test(value)) {
            url = "http://" + value;
        } else if (value.includes(".") && !value.includes(" ")) {
            url = "https://" + value;
        } else {
            url = "https://www.google.com/search?q=" + encodeURIComponent(value);
        }

        iframe.src = url;
    }

    button.addEventListener("click", navigate);
    input.addEventListener("keydown", e => { if(e.key === "Enter") navigate(); });
}

function bringToFront(win) {
    win.style.zIndex = ++zIndex;
}

function enableClose(win) {
    const closeBtn = win.querySelector(".close-btn");
    closeBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        win.remove();
    });
}

/* Dragging */
function enableDrag(win) {
    const bar = win.querySelector(".input-bar");

    bar.onpointerdown = e => {
        // Don't drag if clicking the close button
        if (e.target.classList.contains('close-btn')) return;
        
        bringToFront(win);
        bar.setPointerCapture(e.pointerId);

        const sx = e.clientX;
        const sy = e.clientY;
        const sl = win.offsetLeft;
        const st = win.offsetTop;

        const move = ev => {
            win.style.left = sl + (ev.clientX - sx) + "px";
            win.style.top  = st + (ev.clientY - sy) + "px";
        };

        const up = () => bar.onpointermove = null;

        bar.onpointermove = move;
        bar.onpointerup = up;
    };
}

/* Resizing */
function enableResize(win) {
    const handle = win.querySelector(".resize");

    handle.onpointerdown = e => {
        bringToFront(win);
        handle.setPointerCapture(e.pointerId);

        const sx = e.clientX;
        const sy = e.clientY;
        const sw = win.offsetWidth;
        const sh = win.offsetHeight;

        const move = ev => {
            win.style.width  = Math.max(320, sw + (ev.clientX - sx)) + "px";
            win.style.height = Math.max(240, sh + (ev.clientY - sy)) + "px";
        };

        const up = () => handle.onpointermove = null;

        handle.onpointermove = move;
        handle.onpointerup = up;
    };
}
</script>

</body>
</html>
