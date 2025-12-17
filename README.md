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
    display: flex;
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

<div class="clock" id="clock"></div>

<div class="weather-widget" id="weatherWidget">
    <div class="weather-grab-bar"></div>
    <div class="weather-iframe-wrap">
        <iframe src="https://weatherwidget.io/w/horizontal/?id=ww_3a60b29a54f44&t=horizontal&lang=en&sl_lpl=1&ids=%5B%5D&font=Arial&sl_ics=one_a&sl_sot=fahrenheit&cl_bkg=image&cl_font=%23FFFFFF&cl_cloud=%23FFFFFF&cl_persp=%2381D4FA&cl_sun=%23FFC107&cl_moon=%23FFC107&cl_thund=%23FF5722" frameborder="0"></iframe>
    </div>
    <div class="weather-resize"></div>
</div>

<button class="add-button" id="addBtn">+</button>

<script async src="https://app3.weatherwidget.org/js/?id=ww_3a60b29a54f44"></script>
<script async src="https://app3.weatherwidget.org/js/?id=ww_3a60b29a54f44"></script>
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
    
    document.getElementById('clock').innerHTML = `
        <div class="clock-time">${hours}:${minutesStr} ${ampm}</div>
        <div class="clock-date">${dayName}, ${monthName} ${date} ${year}</div>
    `;
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

document.getElementById("addBtn").addEventListener("click", createWindow);

// Create initial weather radar window
window.addEventListener('load', () => {
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

function createFullscreenWindow() {
    // Get all existing windows
    const allWindows = document.querySelectorAll('.window');
    const windowsWithContent = Array.from(allWindows).filter(w => {
        const iframe = w.querySelector('.iframe-wrap iframe');
        return iframe && iframe.src && iframe.src !== '';
    });

    // If no windows with content exist, create empty fullscreen window
    if (windowsWithContent.length === 0) {
        createEmptyFullscreenWindow();
        return;
    }

    // Pick a random window
    const randomWindow = windowsWithContent[Math.floor(Math.random() * windowsWithContent.length)];
    const randomIframe = randomWindow.querySelector('.iframe-wrap iframe');
    const url = randomIframe.src;

    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "0";
    win.style.top = "0";
    win.style.width = "100%";
    win.style.height = "100%";
    win.style.zIndex = ++zIndex;

    win.innerHTML = `
        <div class="input-bar">
            <button class="close-btn">×</button>
            <button class="refresh-btn">↻</button>
            <input type="text" placeholder="Enter URL or search term" value="${url}">
            <button>Go</button>
            <button class="new-tab-btn">↗</button>
        </div>
        <div class="iframe-wrap">
            <iframe allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera" 
                    credentials="include" 
                    referrerpolicy="no-referrer-when-downgrade"
                    allowfullscreen
                    src="${url}"></iframe>
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

function createEmptyFullscreenWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "0";
    win.style.top = "0";
    win.style.width = "100%";
    win.style.height = "100%";
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
    const goButton = win.querySelector(".input-bar button:last-child");
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

        // Set iframe attributes for better cross-domain support
        iframe.setAttribute('allow', 'autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera');
        iframe.setAttribute('credentials', 'include');
        iframe.setAttribute('referrerpolicy', 'no-referrer-when-downgrade');
        iframe.setAttribute('allowfullscreen', '');
        
        // Try to set custom user agent header (limited support)
        try {
            iframe.contentWindow.navigator.userAgent = navigator.userAgent.replace(/iframe/gi, '');
        } catch(e) {
            // User agent spoofing blocked by browser
        }
        
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
    let authPopup = null;

    // Close auth panel
    authCloseBtn.addEventListener("click", (e) => {
        e.stopPropagation();
        win.classList.remove("split-view");
        authIframeWrap.classList.remove("active");
        authIframe.src = "";
        if (authPopup && !authPopup.closed) {
            authPopup.close();
        }
    });

    // Intercept popup creation
    const originalOpen = window.open;
    
    // Listen for messages from authentication iframe
    window.addEventListener("message", (event) => {
        if (event.data && event.data.type === "auth-success") {
            console.log("Auth token received:", event.data.token);
            
            win.classList.remove("split-view");
            authIframeWrap.classList.remove("active");
            overlay.classList.remove("active");
            authIframe.src = "";
            
            if (authPopup && !authPopup.closed) {
                authPopup.close();
            }
            
            win.authToken = event.data.token;
            
            try {
                if (event.data.tokenType === "bearer") {
                    win.bearerToken = event.data.token;
                }
            } catch(e) {
                console.log("Cannot access iframe directly due to CORS");
            }
            
            if (iframe.src) {
                iframe.src = iframe.src;
            }
        } else if (event.data && event.data.type === "auth-failed") {
            console.error("Authentication failed:", event.data.error);
            win.classList.remove("split-view");
            authIframeWrap.classList.remove("active");
            overlay.classList.remove("active");
            if (authPopup && !authPopup.closed) {
                authPopup.close();
            }
        }
    });

    iframe.addEventListener('error', () => {
        console.warn("Iframe failed to load - may be blocked by X-Frame-Options or CSP");
    });

    // Monitor for popup attempts from the main iframe
    const checkForPopups = setInterval(() => {
        try {
            const iframeDoc = iframe.contentWindow || iframe.contentDocument;
            if (iframeDoc && iframeDoc.document) {
                // Override window.open in the iframe context
                iframeDoc.open = function(url, name, features) {
                    // Check if this looks like an auth popup
                    if (url && (url.includes('login') || url.includes('auth') || url.includes('oauth') || 
                        features && (features.includes('popup') || features.includes('width=') || features.includes('height=')))) {
                        
                        // Show in side panel instead
                        win.classList.add("split-view");
                        authIframeWrap.classList.add("active");
                        authIframe.src = url;
                        
                        return {
                            closed: false,
                            close: () => {
                                win.classList.remove("split-view");
                                authIframeWrap.classList.remove("active");
                                authIframe.src = "";
                            }
                        };
                    }
                    
                    // Otherwise use original open
                    return originalOpen.call(window, url, name, features);
                };
            }
        } catch(e) {
            // CORS prevents access, which is expected for cross-origin iframes
        }
    }, 1000);

    win.openAuthPopup = (authUrl, width = 500, height = 600) => {
        win.classList.add("split-view");
        authIframeWrap.classList.add("active");
        authIframe.src = authUrl;
    };
}

/* Dragging */
function enableDrag(win) {
    const bar = win.querySelector(".input-bar");
    const grabBar = win.querySelector(".grab-bar");
    
    // Use input bar if available, otherwise use grab bar, otherwise use window
    const dragTarget = bar || grabBar || win;

    dragTarget.onpointerdown = e => {
        // Don't drag if clicking buttons, input, iframe, or resize handle
        if (e.target.tagName === 'BUTTON' || e.target.tagName === 'INPUT' || 
            e.target.tagName === 'IFRAME' || e.target.classList.contains('resize')) return;
        
        bringToFront(win);
        dragTarget.setPointerCapture(e.pointerId);

        const sx = e.clientX;
        const sy = e.clientY;
        const sl = win.offsetLeft;
        const st = win.offsetTop;

        const move = ev => {
            const newLeft = sl + (ev.clientX - sx);
            const newTop = st + (ev.clientY - sy);
            
            // Constrain to keep grab bar visible (prevent going above screen)
            win.style.left = newLeft + "px";
            win.style.top = Math.max(0, newTop) + "px";
        };

        const up = () => dragTarget.onpointermove = null;

        dragTarget.onpointermove = move;
        dragTarget.onpointerup = up;
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
