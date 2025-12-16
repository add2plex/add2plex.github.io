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
    gap: 6px;
    cursor: move;
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

.go-btn {
    height: 30px;
    padding: 0 14px;
    border-radius: 15px;
    border: none;
    background: #2d3c66;
    color: #8fb4ff;
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
document.getElementById("addBtn").onclick = createWindow;

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "60px";
    win.style.top = "60px";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="title-bar">
            <input class="address" placeholder="Search Google or type a URL">
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

    function navigate() {
        let value = input.value.trim();
        if (!value) return;

        let url;

        // Detect URL vs search
        if (/^https?:\/\//i.test(value)) {
            url = value;
        } else if (value.includes(".") && !value.includes(" ")) {
            url = "https://" + value;
        } else {
            url = "https://www.google.com/search?q=" + encodeURIComponent(value);
        }

        iframe.src = url;
    }

    btn.onclick = navigate;
    input.onkeydown = e => e.key === "Enter" && navigate();

    bar.onpointerdown = e => {
        if (e.target.tagName === "INPUT") return;
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
