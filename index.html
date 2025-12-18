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
    /* Allow forms, scripts, popups, and same-origin for authentication flows */
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

/* Scratch Pad Widget */
.scratchpad-widget {
    position: absolute;
    width: 400px;
    height: 500px;
    background: #1a1f2e;
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

.scratchpad-grab-bar:active {
    cursor: grabbing;
}

.scratchpad-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.scratchpad-toolbar {
    height: 60px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    display: flex;
    align-items: center;
    gap: 12px;
    padding: 8px 12px;
    flex-wrap: wrap;
}

.scratchpad-color-bar {
    display: flex;
    align-items: center;
    gap: 8px;
    flex-shrink: 0;
}

.scratchpad-gradient-bar {
    width: 120px;
    height: 24px;
    border-radius: 4px;
    border: 2px solid #8fb4ff;
    background: linear-gradient(to right, #ff0000, #ffff00, #00ff00, #00ffff, #0000ff, #ff00ff, #ff0000);
    cursor: crosshair;
}

.scratchpad-color-preview {
    width: 24px;
    height: 24px;
    border-radius: 4px;
    border: 2px solid #8fb4ff;
    background: #ff0000;
    flex-shrink: 0;
}

.scratchpad-bw-buttons {
    display: flex;
    gap: 4px;
    flex-shrink: 0;
}

.scratchpad-bw-btn {
    width: 24px;
    height: 24px;
    border-radius: 4px;
    border: 2px solid transparent;
    cursor: pointer;
    transition: border-color 0.2s;
    flex-shrink: 0;
}

.scratchpad-bw-btn.active {
    border-color: #8fb4ff;
}

#blackBtn {
    background: #000000;
}

#whiteBtn {
    background: #ffffff;
}

.scratchpad-thickness-container {
    display: flex;
    align-items: center;
    gap: 6px;
    flex-shrink: 0;
}

.scratchpad-thickness-slider {
    width: 60px;
    height: 4px;
    cursor: pointer;
}

.scratchpad-thickness-label {
    font-size: 12px;
    color: #8fb4ff;
    width: 20px;
    text-align: center;
}

.scratchpad-btn {
    height: 28px;
    padding: 0 10px;
    border-radius: 4px;
    border: 1px solid #2d3c66;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 12px;
    cursor: pointer;
    flex-shrink: 0;
    transition: background 0.2s;
}

.scratchpad-btn:hover {
    background: #3d4c76;
}

.scratchpad-canvas-wrap {
    flex: 1;
    overflow: hidden;
    background: #3a4a7a;
    position: relative;
}

#scratchpadCanvas {
    display: block;
    cursor: crosshair;
    touch-action: none;
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
</head>
<body>

<div class="clock" id="clock"></div>

<div class="weather-widget" id="weatherWidget">
    <div class="weather-grab-bar"></div>
    <div class="weather-content">
        <div class="weather-clock" id="weatherClock">
            <div class="weather-clock-time">--:-- --</div>
            <div class="weather-clock-date">Loading...</div>
        </div>
        <div class="weather-main">
            <div class="weather-temp">--°F</div>
            <div class="weather-icon">☀️</div>
        </div>
        <div class="weather-description">Loading weather...</div>
        <div class="weather-location">Panama City, FL</div>
        <div class="weather-details">
            <div class="weather-detail">
                <div class="weather-detail-label">Humidity</div>
                <div class="weather-detail-value">--%</div>
            </div>
            <div class="weather-detail">
                <div class="weather-detail-label">Precipitation</div>
                <div class="weather-detail-value">--%</div>
            </div>
        </div>
    </div>
    <div class="weather-resize"></div>
</div>

<div class="forecast-widget" id="forecastWidget">
    <div class="forecast-grab-bar"></div>
    <div class="forecast-content">
        <div class="forecast-day">
            <div class="forecast-day-label">T</div>
            <div class="forecast-icon">☀️</div>
            <div class="forecast-info">
                <div class="forecast-temps">
                    <div class="forecast-high">--°</div>
                    <div class="forecast-low">--°</div>
                </div>
                <div class="forecast-precip">--%</div>
            </div>
        </div>
        <div class="forecast-day">
            <div class="forecast-day-label">-</div>
            <div class="forecast-icon">☀️</div>
            <div class="forecast-info">
                <div class="forecast-temps">
                    <div class="forecast-high">--°</div>
                    <div class="forecast-low">--°</div>
                </div>
                <div class="forecast-precip">--%</div>
            </div>
        </div>
        <div class="forecast-day">
            <div class="forecast-day-label">-</div>
            <div class="forecast-icon">☀️</div>
            <div class="forecast-info">
                <div class="forecast-temps">
                    <div class="forecast-high">--°</div>
                    <div class="forecast-low">--°</div>
                </div>
                <div class="forecast-precip">--%</div>
            </div>
        </div>
        <div class="forecast-day">
            <div class="forecast-day-label">-</div>
            <div class="forecast-icon">☀️</div>
            <div class="forecast-info">
                <div class="forecast-temps">
                    <div class="forecast-high">--°</div>
                    <div class="forecast-low">--°</div>
                </div>
                <div class="forecast-precip">--%</div>
            </div>
        </div>
        <div class="forecast-day">
            <div class="forecast-day-label">-</div>
            <div class="forecast-icon">☀️</div>
            <div class="forecast-info">
                <div class="forecast-temps">
                    <div class="forecast-high">--°</div>
                    <div class="forecast-low">--°</div>
                </div>
                <div class="forecast-precip">--%</div>
            </div>
        </div>
    </div>
    <div class="forecast-resize"></div>
</div>

<div class="scratchpad-widget" id="scratchpadWidget">
    <div class="scratchpad-grab-bar"></div>
    <div class="scratchpad-toolbar">
        <div class="scratchpad-color-bar">
            <div class="scratchpad-gradient-bar" id="gradientBar"></div>
            <div class="scratchpad-color-preview" id="colorPreview"></div>
            <div class="scratchpad-bw-buttons">
                <button class="scratchpad-bw-btn" id="blackBtn"></button>
                <button class="scratchpad-bw-btn" id="whiteBtn"></button>
            </div>
        </div>
        <div class="scratchpad-thickness-container">
            <label class="scratchpad-thickness-label">Size:</label>
            <input type="range" class="scratchpad-thickness-slider" id="thicknessSlider" min="1" max="50" value="3">
        </div>
        <button class="scratchpad-btn" id="eraserBtn">✏️ Eraser</button>
        <button class="scratchpad-btn" id="clearBtn">Clear</button>
    </div>
    <div class="scratchpad-canvas-wrap">
        <canvas id="scratchpadCanvas"></canvas>
    </div>
    <div class="scratchpad-resize"></div>
</div>

<script>
// Enable third-party cookies and credentials globally
document.cookie = "cookiesEnabled=true; SameSite=None; Secure";

let zIndex = 1;
let clockScale = 1;
let initialDistance = 0;
let initialScale = 1;
let isDraggingClock = false;
let clockStartX = 0;
let clockStartY = 0;
let clockOffsetX = 0;
let clockOffsetY = 0;

// Update clock
function updateClock() {
    const now = new Date();
    let hours = now.getHours();
    const minutes = now.getMinutes();
    const ampm = hours >= 12 ? 'PM' : 'AM';
    
    hours = hours % 12;
    hours = hours ? hours : 12; // 0 should be 12
    const minutesStr = minutes < 10 ? '0' + minutes : minutes;
    
    const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
    
    const dayName = days[now.getDay()];
    const monthName = months[now.getMonth()];
    const date = now.getDate();
    const year = now.getFullYear();
    
    // Update weather widget clock
    const weatherClockTime = document.querySelector('.weather-clock-time');
    const weatherClockDate = document.query
