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
            <button class="refresh-btn">↻</button>
            <input type="text" placeholder="Enter URL or search term">
            <button>Go</button>
        </div>
        <div class="iframe-wrap">
            <iframe allow="popups" credentials="include" src=""></iframe>
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

function enableAuth(win) {
    const iframe = win.querySelector("iframe");
    const overlay = win.querySelector(".auth-overlay");
    let authPopup = null;

    // Listen for messages from authentication popup
    window.addEventListener("message", (event) => {
        // Validate message origin for security (adjust as needed)
        // if (event.origin !== "https://your-auth-provider.com") return;
        
        if (event.data && event.data.type === "auth-success") {
            // Authentication successful
            console.log("Auth token received:", event.data.token);
            
            // Hide overlay
            overlay.classList.remove("active");
            
            // Close popup if still open
            if (authPopup && !authPopup.closed) {
                authPopup.close();
            }
            
            // Store token (in memory for this session)
            win.authToken = event.data.token;
            
            // Refresh iframe to use new auth
            if (iframe.src) {
                iframe.src = iframe.src;
            }
        } else if (event.data && event.data.type === "auth-failed") {
            console.error("Authentication failed:", event.data.error);
            overlay.classList.remove("active");
            if (authPopup && !authPopup.closed) {
                authPopup.close();
            }
        }
    });

    // Expose auth function for iframe to call
    win.openAuthPopup = (authUrl, width = 500, height = 600) => {
        const left = (screen.width - width) / 2;
        const top = (screen.height - height) / 2;
        
        overlay.classList.add("active");
        
        authPopup = window.open(
            authUrl,
            "auth-popup",
            `width=${width},height=${height},left=${left},top=${top},popup=yes`
        );
        
        // Check if popup was blocked
        if (!authPopup || authPopup.closed) {
            overlay.classList.remove("active");
            alert("Popup blocked. Please allow popups for authentication.");
            return;
        }
        
        // Poll to detect when popup closes
        const checkClosed = setInterval(() => {
            if (authPopup.closed) {
                clearInterval(checkClosed);
                overlay.classList.remove("active");
            }
        }, 500);
    };
}

/* Dragging */
function enableDrag(win) {
    const bar = win.querySelector(".input-bar");

    bar.onpointerdown = e => {
        // Don't drag if clicking buttons or input
        if (e.target.tagName === 'BUTTON' || e.target.tagName === 'INPUT') return;
        
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
