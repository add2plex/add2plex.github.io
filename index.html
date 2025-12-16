<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Floating Browser Windows</title>

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
    display: flex;
    align-items: center;
    justify-content: center;
    box-shadow: 0 6px 18px rgba(0,0,0,0.7);
    z-index: 1000;
}

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

.title-bar {
    height: 42px;
    background: #1a1f2e;
    display: flex;
    align-items: center;
    padding: 6px;
    cursor: move;
    gap: 6px;
}

.address {
    flex: 1;
    height: 30px;
    border-radius: 15px;
    border: none;
    padding: 0 14px;
    background: #0f1320;
    color: #fff;
    font-size: 14px;
    outline: none;
}

.address::placeholder {
    color: #888;
}

.go-btn {
    height: 30px;
    padding: 0 14px;
    border-radius: 15px;
    border: none;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 13px;
    cursor: pointer;
}

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

document.getElementById("addBtn").addEventListener("click", createWindow);

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "50px";
    win.style.top = "50px";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="title-bar">
            <input class="address" placeholder="https://example.com">
            <button class="go-btn">Go</button>
        </div>
        <div class="iframe-wrap">
            <iframe></iframe>
        </div>
        <div class="resize"></div>
    `;

    document.body.appendChild(win);
    bringToFront(win);

    const bar = win.querySelector(".title-bar");
    const resize = win.querySelector(".resize");
    const input = win.querySelector(".address");
    const btn = win.querySelector(".go-btn");
    const iframe = win.querySelector("iframe");

    /* Load URL */
    btn.onclick = () => loadURL();
    input.onkeydown = e => e.key === "Enter" && loadURL();

    function loadURL() {
        let url = input.value.trim();
        if (!url) return;
        if (!/^https?:\/\//i.test(url)) url = "https://" + url;
        iframe.src = url;
    }

    /* Drag */
    bar.onpointerdown = e => {
        if (e.target.tagName === "INPUT") return;

        bringToFront(win);
        let startX = e.clientX;
        let startY = e.clientY;
        let startL = win.offsetLeft;
        let startT = win.offsetTop;

        bar.setPointerCapture(e.pointerId);

        bar.onpointermove = ev => {
            win.style.left = startL + (ev.clientX - startX) + "px";
            win.style.top  = startT + (ev.clientY - startY) + "px";
        };

        bar.onpointerup = () => bar.onpointermove = null;
    };

    /* Resize */
    resize.onpointerdown = e => {
        bringToFront(win);
        let startX = e.clientX;
        let startY = e.clientY;
        let startW = win.offsetWidth;
        let startH = win.offsetHeight;

        resize.setPointerCapture(e.pointerId);

        resize.onpointermove = ev => {
            win.style.width  = Math.max(300, startW + (ev.clientX - startX)) + "px";
            win.style.height = Math.max(200, startH + (ev.clientY - startY)) + "px";
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
