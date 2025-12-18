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
    const weatherClockDate = document.querySelector('.weather-clock-date');
    if (weatherClockTime && weatherClockDate) {
        weatherClockTime.textContent = `${hours}:${minutesStr} ${ampm}`;
        weatherClockDate.textContent = `${dayName}, ${monthName} ${date} ${year}`;
    }
}

updateClock();
setInterval(updateClock, 1000);

// Pinch to zoom clock
const clockEl = document.getElementById('clock');

function getDistance(touches) {
    const dx = touches[0].clientX - touches[1].clientX;
    const dy = touches[0].clientY - touches[1].clientY;
    return Math.sqrt(dx * dx + dy * dy);
}

function isTouchingClock(touches) {
    const rect = clockEl.getBoundingClientRect();
    for (let touch of touches) {
        if (touch.clientX >= rect.left && touch.clientX <= rect.right &&
            touch.clientY >= rect.top && touch.clientY <= rect.bottom) {
            return true;
        }
    }
    return false;
}

// Drag clock
clockEl.addEventListener('pointerdown', (e) => {
    isDraggingClock = true;
    clockEl.setPointerCapture(e.pointerId);
    
    const rect = clockEl.getBoundingClientRect();
    clockStartX = e.clientX - rect.left;
    clockStartY = e.clientY - rect.top;
    
    clockEl.style.cursor = 'grabbing';
});

clockEl.addEventListener('pointermove', (e) => {
    if (isDraggingClock) {
        e.preventDefault();
        
        clockOffsetX = e.clientX - clockStartX;
        clockOffsetY = e.clientY - clockStartY;
        
        clockEl.style.left = clockOffsetX + 'px';
        clockEl.style.top = clockOffsetY + 'px';
        clockEl.style.right = 'auto';
        
        // Adjust text alignment based on position
        const screenWidth = window.innerWidth;
        const centerX = screenWidth / 2;
        const clockCenterX = clockOffsetX + (clockEl.offsetWidth / 2);
        
        if (Math.abs(clockCenterX - centerX) <= 20) {
            // Center
            clockEl.style.alignItems = 'center';
        } else if (clockCenterX < centerX) {
            // Left side
            clockEl.style.alignItems = 'flex-start';
        } else {
            // Right side
            clockEl.style.alignItems = 'flex-end';
        }
    }
});

clockEl.addEventListener('pointerup', () => {
    isDraggingClock = false;
    clockEl.style.cursor = 'grab';
});

clockEl.addEventListener('pointercancel', () => {
    isDraggingClock = false;
    clockEl.style.cursor = 'grab';
});

clockEl.addEventListener('touchstart', (e) => {
    if (e.touches.length === 2) {
        e.preventDefault();
        isDraggingClock = false;
        initialDistance = getDistance(e.touches);
        initialScale = clockScale;
    }
});

clockEl.addEventListener('touchmove', (e) => {
    if (e.touches.length === 2 && isTouchingClock(e.touches)) {
        e.preventDefault();
        const currentDistance = getDistance(e.touches);
        clockScale = initialScale * (currentDistance / initialDistance);
        clockScale = Math.max(0.5, Math.min(clockScale, 3)); // Limit between 0.5x and 3x
        clockEl.style.transform = `scale(${clockScale})`;
        clockEl.style.transformOrigin = 'top left';
    }
});

// Mouse wheel zoom for desktop
clockEl.addEventListener('wheel', (e) => {
    e.preventDefault();
    const delta = e.deltaY > 0 ? -0.1 : 0.1;
    clockScale += delta;
    clockScale = Math.max(0.5, Math.min(clockScale, 3));
    clockEl.style.transform = `scale(${clockScale})`;
    clockEl.style.transformOrigin = 'top left';
});

// Fetch weather data
async function fetchWeather() {
    try {
        // Use Open-Meteo API (no API key required)
        const lat = 30.1588;
        const lon = -85.6602;
        
        const response = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current=temperature_2m,relative_humidity_2m,precipitation,weather_code&temperature_unit=fahrenheit&wind_speed_unit=mph&precipitation_unit=inch&timezone=America%2FChicago`);
        const data = await response.json();
        
        const temp = Math.round(data.current.temperature_2m);
        const humidity = data.current.relative_humidity_2m;
        const precipitation = data.current.precipitation || 0;
        const weatherCode = data.current.weather_code;
        
        // Map weather codes to descriptions and icons
        const weatherInfo = getWeatherInfo(weatherCode);
        
        // Update widget
        document.querySelector('.weather-temp').textContent = `${temp}°F`;
        document.querySelector('.weather-icon').textContent = weatherInfo.icon;
        document.querySelector('.weather-description').textContent = weatherInfo.description;
        document.querySelector('.weather-details .weather-detail:nth-child(1) .weather-detail-value').textContent = `${humidity}%`;
        document.querySelector('.weather-details .weather-detail:nth-child(2) .weather-detail-value').textContent = `${(precipitation * 100).toFixed(0)}%`;
    } catch (error) {
        console.error('Error fetching weather:', error);
        document.querySelector('.weather-description').textContent = 'Unable to load weather';
    }
}

function getWeatherInfo(code) {
    // WMO Weather interpretation codes
    const weatherMap = {
        0: { description: 'Clear sky', icon: '☀️' },
        1: { description: 'Mainly clear', icon: '🌤️' },
        2: { description: 'Partly cloudy', icon: '⛅' },
        3: { description: 'Overcast', icon: '☁️' },
        45: { description: 'Foggy', icon: '🌫️' },
        48: { description: 'Foggy', icon: '🌫️' },
        51: { description: 'Light drizzle', icon: '🌦️' },
        53: { description: 'Drizzle', icon: '🌦️' },
        55: { description: 'Heavy drizzle', icon: '🌧️' },
        61: { description: 'Light rain', icon: '🌦️' },
        63: { description: 'Rain', icon: '🌧️' },
        65: { description: 'Heavy rain', icon: '⛈️' },
        71: { description: 'Light snow', icon: '🌨️' },
        73: { description: 'Snow', icon: '❄️' },
        75: { description: 'Heavy snow', icon: '❄️' },
        77: { description: 'Snow grains', icon: '❄️' },
        80: { description: 'Light showers', icon: '🌦️' },
        81: { description: 'Showers', icon: '🌧️' },
        82: { description: 'Heavy showers', icon: '⛈️' },
        85: { description: 'Light snow showers', icon: '🌨️' },
        86: { description: 'Snow showers', icon: '❄️' },
        95: { description: 'Thunderstorm', icon: '⛈️' },
        96: { description: 'Thunderstorm with hail', icon: '⛈️' },
        99: { description: 'Thunderstorm with hail', icon: '⛈️' }
    };
    
    return weatherMap[code] || { description: 'Unknown', icon: '🌡️' };
}

// Fetch 5-day forecast data
async function fetchForecast() {
    try {
        const lat = 30.1588;
        const lon = -85.6602;
        
        const response = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&daily=weather_code,temperature_2m_max,temperature_2m_min,precipitation_probability_max&temperature_unit=fahrenheit&wind_speed_unit=mph&precipitation_unit=inch&timezone=America%2FChicago&forecast_days=5`);
        const data = await response.json();
        
        const forecastDays = document.querySelectorAll('.forecast-day');
        const days = ['S', 'M', 'T', 'W', 'T', 'F', 'S'];
        const today = new Date();
        
        forecastDays.forEach((dayEl, index) => {
            const date = new Date(today);
            date.setDate(today.getDate() + index);
            const dayLetter = days[date.getDay()];
            
            const high = Math.round(data.daily.temperature_2m_max[index]);
            const low = Math.round(data.daily.temperature_2m_min[index]);
            const precip = data.daily.precipitation_probability_max[index] || 0;
            const weatherCode = data.daily.weather_code[index];
            const weatherInfo = getWeatherInfo(weatherCode);
            
            dayEl.querySelector('.forecast-day-label').textContent = dayLetter;
            dayEl.querySelector('.forecast-icon').textContent = weatherInfo.icon;
            dayEl.querySelector('.forecast-high').textContent = `${high}°`;
            dayEl.querySelector('.forecast-low').textContent = `${low}°`;
            dayEl.querySelector('.forecast-precip').textContent = `${precip}%`;
        });
    } catch (error) {
        console.error('Error fetching forecast:', error);
    }
}

// Create initial weather radar window
window.addEventListener('load', () => {
    // Position weather widget
    const weatherWidget = document.getElementById('weatherWidget');
    weatherWidget.style.left = "50px";
    weatherWidget.style.top = "150px";
    weatherWidget.style.zIndex = ++zIndex;
    
    enableDrag(weatherWidget, weatherWidget.querySelector('.weather-grab-bar'));
    enableResize(weatherWidget, weatherWidget.querySelector('.weather-resize'));
    
    // Fetch weather data
    fetchWeather();
    setInterval(fetchWeather, 600000); // Update every 10 minutes
    
    // Position forecast widget
    const forecastWidget = document.getElementById('forecastWidget');
    forecastWidget.style.left = "50px";
    forecastWidget.style.top = "480px";
    forecastWidget.style.zIndex = ++zIndex;
    
    enableDrag(forecastWidget, forecastWidget.querySelector('.forecast-grab-bar'));
    enableResize(forecastWidget, forecastWidget.querySelector('.forecast-resize'));
    
    // Fetch forecast data
    fetchForecast();
    setInterval(fetchForecast, 600000); // Update every 10 minutes
    
    const radarWin = document.createElement("div");
    radarWin.className = "window no-input-bar";
    radarWin.style.left = "100px";
    radarWin.style.top = "100px";
    radarWin.style.width = "800px";
    radarWin.style.height = "600px";
    radarWin.style.zIndex = ++zIndex;

    radarWin.innerHTML = `
        <div class="grab-bar"></div>
        <div class="iframe-wrap">
            <iframe allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera" 
                    credentials="include" 
                    referrerpolicy="no-referrer-when-downgrade"
                    allowfullscreen
                    src="https://radar.weather.gov/?settings=v1_eyJhZ2VuZGEiOnsiaWQiOiJsb2NhbCIsImNlbnRlciI6Wy04NS42NTcsMzAuMTU5XSwiem9vbSI6OH0sImJhc2UiOiJzdGFuZGFyZCIsImNvdW50eSI6ZmFsc2UsImN3YSI6ZmFsc2UsInN0YXRlIjpmYWxzZSwibWVudSI6dHJ1ZSwic2hvcnRGdXNlZE9ubHkiOmZhbHNlfQ%3D%3D"></iframe>
        </div>
        <div class="resize"></div>
    `;

    document.body.appendChild(radarWin);
    bringToFront(radarWin);

    enableDrag(radarWin);
    enableResize(radarWin);
});

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "40px";
    win.style.top = "40px";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="input-bar">
            <button class="close-btn">×</button>
            <button class="refresh-btn">↻</button>
            <input type="text" placeholder="Enter URL or search term">
            <button>Go</button>
            <button class="new-tab-btn">↗</button>
        </div>
        <div class="iframe-wrap">
            <iframe allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera" 
                    credentials="include" 
                    referrerpolicy="no-referrer-when-downgrade"
                    allowfullscreen
                    src=""></iframe>
        </div>
        <div class="auth-iframe-wrap">
            <div class="auth-header">
                <span>Login</span>
                <button class="auth-close-btn">×</button>
            </div>
            <iframe allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera" 
                    credentials="include" 
                    referrerpolicy="no-referrer-when-downgrade"
                    allowfullscreen
                    src=""></iframe>
        </div>
        <div class="auth-overlay">
            <div class="auth-message">Waiting for authentication...</div>
        </div>
        <div class="resize"></div>
    `;

    document.body.appendChild(win);
    bringToFront(win);

    enableDrag(win);
    enableResize(win);
    enableInput(win);
    enableClose(win);
    enableRefresh(win);
    enableNewTab(win);
    enableAuth(win);
}

function enableInput(win) {
    const input = win.querySelector(".input-bar input");
    const goButton = win.querySelector(".input-bar button:last-of-type");
    const iframe = win.querySelector("iframe");

    function navigate(e) {
        if (e) e.stopPropagation();
        let value = input.value.trim();
        if (!value) return;

        let url;
        if (/^https?:\/\//i.test(value)) {
            url = value;
        } else if (value.startsWith("localhost") || value.startsWith("127.0.0.1") || /^localhost:/i.test(value) || /^127\.0\.0\.1:/i.test(value)) {
            url = "http://" + value;
        } else if (/^192\.168\.\d{1,3}\.\d{1,3}(:\d+)?$/.test(value) || /^10\.\d{1,3}\.\d{1,3}\.\d{1,3}(:\d+)?$/.test(value) || /^172\.(1[6-9]|2\d|3[0-1])\.\d{1,3}\.\d{1,3}(:\d+)?$/.test(value)) {
            url = "http://" + value;
        } else if (value.includes(".") && !value.includes(" ")) {
            url = "https://" + value;
        } else {
            url = "https://www.google.com/search?q=" + encodeURIComponent(value);
        }

        iframe.setAttribute('allow', 'autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera');
        iframe.setAttribute('credentials', 'include');
        iframe.setAttribute('referrerpolicy', 'no-referrer-when-downgrade');
        iframe.setAttribute('allowfullscreen', '');
        
        iframe.src = url;
    }

    goButton.addEventListener("click", navigate);
    goButton.addEventListener("touchend", navigate);
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

function enableRefresh(win) {
    const refreshBtn = win.querySelector(".refresh-btn");
    const iframe = win.querySelector("iframe");
    refreshBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        if (iframe.src) {
            iframe.src = iframe.src;
        }
    });
}

function enableNewTab(win) {
    const newTabBtn = win.querySelector(".new-tab-btn");
    const iframe = win.querySelector("iframe");
    newTabBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        if (iframe.src) {
            window.open(iframe.src, "_blank");
        }
    });
}

function enableAuth(win) {
    const iframe = win.querySelector(".iframe-wrap iframe");
    const authIframeWrap = win.querySelector(".auth-iframe-wrap");
    const authIframe = win.querySelector(".auth-iframe-wrap iframe");
    const authCloseBtn = win.querySelector(".auth-close-btn");
    const overlay = win.querySelector(".auth-overlay");

    authCloseBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        win.classList.remove("split-view");
        authIframeWrap.classList.remove("active");
        authIframe.src = "";
    });

    window.addEventListener("message", (event) => {
        if (event.data && event.data.type === "auth-success") {
            win.classList.remove("split-view");
            authIframeWrap.classList.remove("active");
            overlay.classList.remove("active");
            authIframe.src = "";
            
            win.authToken = event.data.token;
            
            if (iframe.src) {
                iframe.src = iframe.src;
            }
        }
    });
}

/* Dragging */
function enableDrag(win, dragTarget) {
    if (!dragTarget) {
        const bar = win.querySelector(".input-bar");
        const grabBar = win.querySelector(".grab-bar");
        dragTarget = bar || grabBar || win;
    }

    dragTarget.onpointerdown = e => {
        if (e.target.tagName === 'BUTTON' || e.target.tagName === 'INPUT' || 
            e.target.tagName === 'IFRAME' || e.target.classList.contains('resize') ||
            e.target.classList.contains('weather-resize')) return;
        
        bringToFront(win);
        dragTarget.setPointerCapture(e.pointerId);

        const sx = e.clientX;
        const sy = e.clientY;
        const sl = win.offsetLeft;
        const st = win.offsetTop;

        const move = ev => {
            const newLeft = sl + (ev.clientX - sx);
            const newTop = st + (ev.clientY - sy);
            
            win.style.left = newLeft + "px";
            win.style.top = Math.max(0, newTop) + "px";
        };

        const up = () => dragTarget.onpointermove = null;

        dragTarget.onpointermove = move;
        dragTarget.onpointerup = up;
    };
}

/* Resizing */
function enableResize(win, handle) {
    if (!handle) {
        handle = win.querySelector(".resize");
    }

    handle.onpointerdown = e => {
        bringToFront(win);
        handle.setPointerCapture(e.pointerId);

        const sx = e.clientX;
        const sy = e.clientY;
        const sw = win.offsetWidth;
        const sh = win.offsetHeight;

        const move = ev => {
            const isForecast = win.classList.contains('forecast-widget');
            const minWidth = isForecast ? 400 : 250;
            const minHeight = isForecast ? 140 : 200;
            
            win.style.width  = Math.max(minWidth, sw + (ev.clientX - sx)) + "px";
            win.style.height = Math.max(minHeight, sh + (ev.clientY - sy)) + "px";
        };

        const up = () => handle.onpointermove = null;

        handle.onpointermove = move;
        handle.onpointerup = up;
    };
}
</script>

</body>
</html>
