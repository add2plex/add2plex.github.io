<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Mini Chrome Browser</title>

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
    touch-action: none;
    user-select: none;
    font-family: system-ui, -apple-system, BlinkMacSystemFont, sans-serif;
}

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
}

.window {
    position: absolute;
    width: 500px;
    height: 500px;
    background: #111;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
}

.toolbar {
    height: 48px;
    background: #1a1f2e;
    display: flex;
    align-items: center;
    padding: 6px;
    gap: 6px;
    border-bottom: 1px solid #2d3c66;
}

.tool-btn {
    width: 32px;
    height: 32px;
    border-radius: 50%;
    border: none;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 16px;
}

.address {
    flex: 1;
    height: 32px;
    border-radius: 16px;
    border: none;
    padding: 0 14px;
    background: #0f1320;
    color: white;
    font-size: 14px;
    outline: none;
}

.iframe-wrap {
    flex: 1;
    background: black;
}

iframe {
    width: 100%;
    height: 100%;
    border: none;
}

.resize {
    position: absolute;
    width: 36px;
    height: 36px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    touch-action: none;
}
</style>
</head>
<body>

<button class="add-button" id="addBtn">+</button>

<script>
let zIndex = 1;

document.getElementById("addBtn").onclick = createWindow;

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "40px";
    win.style.top = "40px";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="toolbar">
            <button class="tool-btn back">◀</button>
            <button class="tool-btn forward">▶</button>
            <button class="tool-btn reload">⟳</button>
            <input class="address" placeholder="Search or type URL">
        </div>
        <div class="iframe-wrap">
            <iframe></iframe>
        </div>
        <div class="resize"></div>
    `;

    document.body.appendChild(win);
    bringToFront(win);

    enableDrag(win);
    enableResize(win);
    enableBrowser(win);
}

function enableBrowser(win) {
    const iframe = win.querySelector("iframe");
    const input = win.querySelector(".address");
    const back = win.querySelector(".back");
    const forward = win.querySelector(".forward");
    const reload = win.querySelector(".reload");

    let history = [];
    let index = -1;

    function navigate(value) {
        let url;
        if (/^https?:\/\//i.test(value)) {
            url = value;
        } else if (value.includes(".") && !value.includes(" ")) {
            url = "https://" + value;
        } else {
            url = "https://www.google.com/search?q=" + encodeURIComponent(value);
        }

        iframe.src = url;
        history = history.slice(0, index + 1);
        history.push(url);
        index++;
        input.value = url;
    }

    input.addEventListener("keydown", e => {
        if (e.key === "Enter") navigate(input.value);
    });

    back.onclick = () => {
        if (index > 0) iframe.src = history[--index];
    };

    forward.onclick = () => {
        if (index < history.length - 1) iframe.src = history[++index];
    };

    reload.onclick = () => iframe.src = iframe.src;
}

function enableDrag(win) {
    const bar = win.querySelector(".toolbar");

    bar.onpointerdown = e => {
        if (e.target.tagName === "INPUT" || e.target.tagName === "BUTTON") return;
        bringToFront(win);
        bar.setPointerCapture(e.pointerId);

        const sx = e.clientX, sy = e.clientY;
        const sl = win.offsetLeft, st = win.offsetTop;

        bar.onpointermove = ev => {
            win.style.left = sl + (ev.clientX - sx) + "px";
            win.style.top  = st + (ev.clientY - sy) + "px";
        };

        bar.onpointerup = () => bar.onpointermove = null;
    };
}

function enableResize(win) {
    const handle = win.querySelector(".resize");

    handle.onpointerdown = e => {
        bringToFront(win);
        handle.setPointerCapture(e.pointerId);

        const sx = e.clientX, sy = e.clientY;
        const sw = win.offsetWidth, sh = win.offsetHeight;

        handle.onpointermove = ev => {
            win.style.width  = Math.max(320, sw + (ev.clientX - sx)) + "px";
            win.style.height = Math.max(240, sh + (ev.clientY - sy)) + "px";
        };

        handle.onpointerup = () => handle.onpointermove = null;
    };
}

function bringToFront(win) {
    win.style.zIndex = ++zIndex;
}
</script>

</body>
</html>
