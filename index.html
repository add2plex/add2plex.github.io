<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Radar + Clock Dashboard</title>

<meta name="viewport"
      content="width=device-width, height=device-height, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">

<style>
    html, body {
        width: 100%;
        height: 100%;
        margin: 0;
        background-color: #0b132b;
        overflow: hidden;
        touch-action: manipulation;
        user-select: none;
        -webkit-tap-highlight-color: transparent;
        font-family: Arial, sans-serif;
    }

    .window {
        position: absolute;
        background: #000;
        border: 2px solid #1f2a44;
        border-radius: 10px;
        box-shadow: 0 15px 40px rgba(0,0,0,0.8);
        display: flex;
        flex-direction: column;
    }

    .title-bar {
        height: 44px;
        background: #121a33;
        color: #8fb4ff;
        display: flex;
        align-items: center;
        padding: 0 10px;
        gap: 10px;
        cursor: move;
        border-bottom: 1px solid #1f2a44;
        touch-action: none;
        font-size: 14px;
    }

    .title-text {
        flex: 1;
        white-space: nowrap;
    }

    .zoom-btn {
        background: #1f2a44;
        color: #8fb4ff;
        border: 1px solid #2d3c66;
        border-radius: 6px;
        padding: 6px 10px;
        font-size: 12px;
        cursor: pointer;
    }

    .iframe-wrap {
        flex: 1;
        overflow: hidden;
        background: black;
    }

    iframe {
        width: 100%;
        height: 100%;
        border: none;
        transform-origin: top left;
        transition: transform 0.15s ease;
    }

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

<!-- RADAR WINDOW -->
<div class="window" id="radarWindow" style="top:5%; left:5%; width:70%; height:80%;">
    <div class="title-bar">
        <div class="title-text">NOAA Weather Radar</div>
        <button class="zoom-btn" id="zoomBtn">Zoom +10%</button>
    </div>

    <div class="iframe-wrap">
        <iframe
            id="radarFrame"
            src="https://radar.weather.gov/?settings=v1_eyJhZ2VuZGEiOnsiaWQiOiJ3ZWF0aGVyIiwiY2VudGVyIjpbLTg1LjczOSwzMC4xNDhdLCJsb2NhdGlvbiI6Wy04NS43MDEsMzAuMjQ1XSwiem9vbSI6Ny41NDQ1MTg3MjM5NDYwOSwibGF5ZXIiOiJicmVmX3FjZCJ9LCJhbmltYXRpbmciOnRydWUsImJhc2UiOiJzdGFuZGFyZCIsImFydGNjIjpmYWxzZSwiY291bnR5IjpmYWxzZSwiY3dhIjpmYWxzZSwiY3RhdGUiOmZhbHNlLCJtZW51Ijp0cnVlLCJzaG9ydEZ1c2VkT25seSI6dHJ1ZSwib3BhY2l0eSI6eyJhbGVydHMiOjAuOCwibG9jYWwiOjAuNiwibG9jYWxTdGF0aW9ucyI6MC44LCJuYXRpb25hbCI6MC42fX0%3D">
        </iframe>
    </div>

    <div class="resize-handle"></div>
</div>

<!-- CLOCK WINDOW -->
<div class="window" id="clockWindow" style="top:10%; left:78%; width:18%; height:20%;">
    <div class="title-bar">
        <div class="title-text">Central Time (CST)</div>
    </div>

    <div class="iframe-wrap">
        <iframe srcdoc="
<!DOCTYPE html>
<html>
<head>
<style>
    body {
        margin:0;
        background:#000;
        color:#8fb4ff;
        display:flex;
        align-items:center;
        justify-content:center;
        height:100%;
        font-family: Arial, sans-serif;
    }
    #clock {
        font-size:48px;
        font-weight:bold;
        letter-spacing:2px;
    }
</style>
</head>
<body>
<div id='clock'></div>

<script>
function updateClock() {
    const now = new Date();
    const options = {
        timeZone: 'America/Chicago',
        hour: '2-digit',
        minute: '2-digit',
        second: '2-digit',
        hour12: false
    };
    document.getElementById('clock').textContent =
        now.toLocaleTimeString('en-US', options);
}
setInterval(updateClock, 1000);
updateClock();
</script>
</body>
</html>
"></iframe>
    </div>

    <div class="resize-handle"></div>
</div>

<script>
function makeMovable(win) {
    const bar = win.querySelector(".title-bar");
    const resize = win.querySelector(".resize-handle");

    let sx, sy, sw, sh, sl, st;

    bar.addEventListener("pointerdown", e => {
        if (e.target.tagName === "BUTTON") return;
        sx = e.clientX; sy = e.clientY;
        sl = win.offsetLeft; st = win.offsetTop;
        bar.setPointerCapture(e.pointerId);

        const move = ev => {
            win.style.left = sl + (ev.clientX - sx) + "px";
            win.style.top  = st + (ev.clientY - sy) + "px";
        };

        bar.addEventListener("pointermove", move);
        bar.addEventListener("pointerup", () => {
            bar.removeEventListener("pointermove", move);
        }, { once:true });
    });

    resize.addEventListener("pointerdown", e => {
        sx = e.clientX; sy = e.clientY;
        sw = win.offsetWidth; sh = win.offsetHeight;
        resize.setPointerCapture(e.pointerId);

        const resizeMove = ev => {
            win.style.width  = Math.max(180, sw + (ev.clientX - sx)) + "px";
            win.style.height = Math.max(120, sh + (ev.clientY - sy)) + "px";
        };

        resize.addEventListener("pointermove", resizeMove);
        resize.addEventListener("pointerup", () => {
            resize.removeEventListener("pointermove", resizeMove);
        }, { once:true });
    });
}

makeMovable(document.getElementById("radarWindow"));
makeMovable(document.getElementById("clockWindow"));

/* Radar zoom button */
let zoomLevel = 0;
const radarFrame = document.getElementById("radarFrame");
const zoomBtn = document.getElementById("zoomBtn");

zoomBtn.addEventListener("click", e => {
    e.stopPropagation();
    zoomLevel += 10;
    if (zoomLevel > 50) zoomLevel = 0;
    radarFrame.style.transform = `scale(${1 + zoomLevel / 100})`;
    zoomBtn.textContent = zoomLevel === 0 ? "Zoom +10%" :
                          zoomLevel === 50 ? "Reset Zoom" :
                          `Zoom +${zoomLevel}%`;
});
</script>

</body>
</html>
