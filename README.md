<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dynamic Windows with URL Input</title>

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

/* Clock */
.clock {
    position: fixed;
    top: 24px;
    right: 24px;
    font-size: 48px;
    font-weight: bold;
    color: #ffffff;
    font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
    z-index: 1000;
    text-shadow: 0 2px 8px rgba(0,0,0,0.5);
    user-select: none;
    touch-action: none;
    cursor: grab;
    transition: transform 0.1s ease-out;
    display: none;
    flex-direction: column;
    align-items: flex-end;
}

.clock-time {
    line-height: 1;
}

.clock-date {
    font-size: 0.3em;
    margin-top: 4px;
    opacity: 0.95;
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

.window.no-input-bar .iframe-wrap {
    border-radius: 12px;
}

.window.split-view {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 48px 1fr;
}

.window.split-view .input-bar {
    grid-column: 1 / -1;
}

.window.split-view .iframe-wrap {
    border-right: 1px solid #2d3c66;
}

.window.split-view .auth-iframe-wrap {
    display: flex;
    flex-direction: column;
    overflow: hidden;
}

/* Grab bar for windows without input bar */
.grab-bar {
    height: 24px;
    background: #1a1f2e;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.grab-bar:active {
    cursor: grabbing;
}

.grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
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

.refresh-btn {
    width: 32px;
    height: 32px;
    border-radius: 16px;
    border: none;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 16px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.new-tab-btn {
    width: 32px;
    height: 32px;
    border-radius: 16px;
    border: none;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 14px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    margin-left: auto;
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
}

/* Auth popup overlay */
.auth-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(11, 19, 43, 0.95);
    display: none;
    align-items: center;
    justify-content: center;
    z-index: 10;
}

.auth-overlay.active {
    display: flex;
}

.auth-message {
    color: #8fb4ff;
    font-size: 14px;
    text-align: center;
}

.auth-iframe-wrap {
    display: none;
    flex-direction: column;
}

.auth-iframe-wrap.active {
    display: flex;
}

.auth-header {
    height: 36px;
    background: #1a1f2e;
    border-bottom: 1px solid #2d3c66;
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 12px;
    color: #8fb4ff;
    font-size: 12px;
}

.auth-close-btn {
    width: 24px;
    height: 24px;
    border-radius: 12px;
    border: none;
    background: #2d3c66;
    color: #ff6b6b;
    font-size: 16px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.auth-iframe-wrap iframe {
    flex: 1;
    width: 100%;
    height: 100%;
    border: none;
}

/* Resize handle */
.resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
}

/* Weather Widget */
.weather-widget {
    position: absolute;
    width: 320px;
    height: 280px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
    container-type: size;
    container-name: weather;
}

.weather-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.weather-grab-bar:active {
    cursor: grabbing;
}

.weather-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.weather-content {
    flex: 1;
    padding: 4px 4px 4px 4px;
    padding-top: 2px;
    display: flex;
    flex-direction: column;
    gap: 4px;
    overflow: hidden;
    align-items: center;
    justify-content: space-evenly;
}

.weather-main {
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    gap: clamp(8px, 3cqw, 20px);
}

.weather-temp {
    font-size: clamp(22px, 15cqw, 72px);
    font-weight: bold;
    color: #8fb4ff;
    line-height: 1;
}

.weather-icon {
    font-size: clamp(50px, 35cqw, 200px);
    animation: float 3s ease-in-out infinite;
    line-height: 1;
}

@keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-10px); }
}

.weather-description {
    font-size: clamp(13px, 5.5cqw, 26px);
    color: #ffffff;
    text-transform: capitalize;
    flex-shrink: 0;
    line-height: 1.2;
    text-align: center;
}

.weather-details {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
    gap: 2px;
    flex-wrap: wrap;
    flex-shrink: 0;
    width: 100%;
    text-align: center;
}

.weather-detail {
    display: flex;
    flex-direction: column;
    gap: 4px;
    align-items: center;
}

.weather-detail-label {
    font-size: clamp(9px, 3.5cqw, 16px);
    color: #8fb4ff;
    opacity: 0.7;
    text-transform: uppercase;
    line-height: 1.2;
}

.weather-detail-value {
    font-size: clamp(16px, 6cqw, 28px);
    color: #ffffff;
    font-weight: bold;
    line-height: 1.2;
}

.weather-location {
    font-size: clamp(10px, 4cqw, 17px);
    color: #8fb4ff;
    opacity: 0.9;
    text-align: center;
    font-weight: 500;
    padding: 4px 0;
    border-top: 1px solid #2d3c66;
    border-bottom: 1px solid #2d3c66;
    line-height: 1.2;
    width: 100%;
}

.weather-clock {
    font-size: clamp(11px, 4.5cqw, 18px);
    color: #ffffff;
    opacity: 0.95;
    text-align: center;
    font-weight: 500;
    padding-bottom: 4px;
    border-bottom: 1px solid #2d3c66;
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 2px;
}

.weather-clock-time {
    font-size: clamp(22px, 15cqw, 72px);
    font-weight: bold;
}

.weather-clock-date {
    font-size: clamp(12px, 5cqw, 20px);
    opacity: 0.85;
}

.weather-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
}

/* 5-Day Forecast Widget */
.forecast-widget {
    position: absolute;
    width: 600px;
    height: 192px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
    container-type: size;
    container-name: forecast;
}

.forecast-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

.forecast-grab-bar:active {
    cursor: grabbing;
}

.forecast-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.forecast-content {
    flex: 1;
    padding: 8px;
    display: flex;
    gap: 6px;
    overflow: hidden;
    container-type: size;
}

@container (max-height: 150px) {
    .forecast-day {
        padding: 4px 8px;
    }
    
    .forecast-icon {
        flex-shrink: 0;
    }
}

.forecast-day {
    flex: 1;
    background: #0f1320;
    border-radius: 8px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    padding: clamp(4px, 2cqw, 12px);
    position: relative;
    gap: clamp(4px, 2cqw, 12px);
}

.forecast-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: clamp(2px, 1cqw, 6px);
}

.forecast-day-label {
    position: absolute;
    top: 4px;
    left: 6px;
    font-size: clamp(14px, 5.8cqw, 23px);
    font-weight: bold;
    color: #8fb4ff;
    opacity: 0.8;
}

.forecast-icon {
    font-size: clamp(35px, 17.3cqw, 70px);
    animation: float 3s ease-in-out infinite;
    line-height: 1;
    flex-shrink: 0;
}

.forecast-temps {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
}

.forecast-high {
    font-size: clamp(20px, 8.6cqw, 35px);
    font-weight: bold;
    color: #ff8080;
    line-height: 1;
}

.forecast-low {
    font-size: clamp(17px, 7.2cqw, 29px);
    font-weight: bold;
    color: #80b3ff;
    line-height: 1;
}

.forecast-precip {
    font-size: clamp(14px, 5.8cqw, 23px);
    color: #8fb4ff;
    line-height: 1;
    display: flex;
    align-items: center;
    gap: 2px;
}

.forecast-precip::before {
    content: '💧';
    font-size: clamp(12px, 5cqw, 20px);
}

.forecast-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
}

/* --------------------- */
/* SCRATCHPAD WIDGET CSS */
.scratchpad-widget {
    position: absolute;
    width: 400px;
    height: 400px;
    background: #1a203d; /* lighter than main page */
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
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
    flex-shrink: 0;
}
.scratchpad-grab-bar:active { cursor: grabbing; }
.scratchpad-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.scratchpad-controls {
    display: flex;
    gap: 6px;
    padding: 4px;
    align-items: center;
    background: #0f1320;
}

#scratchpadCanvas {
    flex: 1;
    touch-action: none;
    cursor: crosshair;
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
</style>
<body>

<div class="clock" id="clock"></div>

<div class="weather-widget" id="weatherWidget">
    <div class="weather-grab-bar"></div>
    <div class="weather-content">
        <!-- Your weather content here -->
    </div>
    <div class="weather-resize"></div>
</div>

<div class="forecast-widget" id="forecastWidget">
    <div class="forecast-grab-bar"></div>
    <div class="forecast-content">
        <!-- Your forecast content here -->
    </div>
    <div class="forecast-resize"></div>
</div>

<!-- SCRATCHPAD WIDGET -->
<div class="scratchpad-widget" id="scratchpadWidget">
    <div class="scratchpad-grab-bar"></div>
    <div class="scratchpad-controls">
        <canvas id="colorGradient" width="150" height="24"></canvas>
        <button id="eraserBtn">Eraser</button>
        <button id="clearBtn">Clear</button>
        <label>Thickness: <input type="range" id="thicknessSlider" min="1" max="30" value="5"></label>
    </div>
    <canvas id="scratchpadCanvas"></canvas>
    <div class="scratchpad-resize"></div>
</div>

<script>
// Utility for drag & resize
let zIndex = 1000;

function enableDrag(el, handle) {
    let offsetX, offsetY;
    handle.addEventListener('pointerdown', e => {
        zIndex++;
        el.style.zIndex = zIndex;
        offsetX = e.clientX - el.getBoundingClientRect().left;
        offsetY = e.clientY - el.getBoundingClientRect().top;
        const move = e => {
            el.style.left = e.clientX - offsetX + 'px';
            el.style.top = e.clientY - offsetY + 'px';
        };
        const up = () => {
            window.removeEventListener('pointermove', move);
            window.removeEventListener('pointerup', up);
        };
        window.addEventListener('pointermove', move);
        window.addEventListener('pointerup', up);
    });
}

function enableResize(el, handle) {
    handle.addEventListener('pointerdown', e => {
        e.preventDefault();
        const startWidth = el.offsetWidth;
        const startHeight = el.offsetHeight;
        const startX = e.clientX;
        const startY = e.clientY;
        const move = e => {
            el.style.width = startWidth + (e.clientX - startX) + 'px';
            el.style.height = startHeight + (e.clientY - startY) + 'px';
        };
        const up = () => {
            window.removeEventListener('pointermove', move);
            window.removeEventListener('pointerup', up);
        };
        window.addEventListener('pointermove', move);
        window.addEventListener('pointerup', up);
    });
}

// Apply drag & resize to all widgets
enableDrag(document.getElementById('weatherWidget'), document.querySelector('#weatherWidget .weather-grab-bar'));
enableResize(document.getElementById('weatherWidget'), document.querySelector('#weatherWidget .weather-resize'));

enableDrag(document.getElementById('forecastWidget'), document.querySelector('#forecastWidget .forecast-grab-bar'));
enableResize(document.getElementById('forecastWidget'), document.querySelector('#forecastWidget .forecast-resize'));

enableDrag(document.getElementById('scratchpadWidget'), document.querySelector('#scratchpadWidget .scratchpad-grab-bar'));
enableResize(document.getElementById('scratchpadWidget'), document.querySelector('#scratchpadWidget .scratchpad-resize'));

// SCRATCHPAD FUNCTIONALITY
(function(){
    const widget = document.getElementById('scratchpadWidget');
    widget.style.left = "50px";
    widget.style.top = "50px";

    const canvas = document.getElementById('scratchpadCanvas');
    const ctx = canvas.getContext('2d');
    const gradientCanvas = document.getElementById('colorGradient');
    const gradientCtx = gradientCanvas.getContext('2d');
    const eraserBtn = document.getElementById('eraserBtn');
    const clearBtn = document.getElementById('clearBtn');
    const thicknessSlider = document.getElementById('thicknessSlider');

    function resizeCanvas() {
        canvas.width = widget.clientWidth;
        canvas.height = widget.clientHeight - widget.querySelector('.scratchpad-controls').offsetHeight - 24;
    }
    resizeCanvas();
    window.addEventListener('resize', resizeCanvas);

    const grad = gradientCtx.createLinearGradient(0, 0, gradientCanvas.width, 0);
    grad.addColorStop(0, 'red');
    grad.addColorStop(0.17, 'orange');
    grad.addColorStop(0.34, 'yellow');
    grad.addColorStop(0.51, 'green');
    grad.addColorStop(0.68, 'cyan');
    grad.addColorStop(0.85, 'blue');
    grad.addColorStop(1, 'magenta');
    gradientCtx.fillStyle = grad;
    gradientCtx.fillRect(0, 0, gradientCanvas.width, gradientCanvas.height);

    let penColor = 'white';
    let penThickness = thicknessSlider.value;
    let erasing = false;
    let drawing = false;
    let lastPos = null;

    function getPointerPos(e){
        const rect = canvas.getBoundingClientRect();
        return {
            x: (e.clientX || e.touches[0].clientX) - rect.left,
            y: (e.clientY || e.touches[0].clientY) - rect.top
        };
    }

    function startDraw(e){
        drawing = true;
        lastPos = getPointerPos(e);
    }

    function draw(e){
        if(!drawing) return;
        const pos = getPointerPos(e);
        ctx.strokeStyle = erasing ? widget.style.background : penColor;
        ctx.lineWidth = penThickness;
        ctx.lineCap = 'round';
        ctx.beginPath();
        ctx.moveTo(lastPos.x, lastPos.y);
        ctx.lineTo(pos.x, pos.y);
        ctx.stroke();
        lastPos = pos;
    }

    function endDraw(){ drawing=false; lastPos=null; }

    canvas.addEventListener('pointerdown', startDraw);
    canvas.addEventListener('pointermove', draw);
    canvas.addEventListener('pointerup', endDraw);
    canvas.addEventListener('pointerleave', endDraw);
    canvas.addEventListener('touchstart', startDraw, {passive:false});
    canvas.addEventListener('touchmove', draw, {passive:false});
    canvas.addEventListener('touchend', endDraw);

    gradientCanvas.addEventListener('pointerdown', e=>{
        const rect = gradientCanvas.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const data = gradientCtx.getImageData(x,1,1,1).data;
        penColor = `rgb(${data[0]},${data[1]},${data[2]})`;
        erasing = false;
    });

    eraserBtn.addEventListener('click', ()=>erasing=true);
    clearBtn.addEventListener('click', ()=>ctx.clearRect(0,0,canvas.width,canvas.height));
    thicknessSlider.addEventListener('input', e=>penThickness=e.target.value);
})();
</script>

</body>
</html>
