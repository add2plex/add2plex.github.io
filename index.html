<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Dynamic Windows with URL Input</title>

<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
<meta http-equiv="Set-Cookie" content="SameSite=None; Secure">
<meta name="referrer" content="no-referrer-when-downgrade">

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@500;600&display=swap" rel="stylesheet">

<style>
/* ============================================================
   Design tokens — deep blue + slate grey, modern + sleek
   ============================================================ */
:root {
    /* Surface palette */
    --bg-0:           #050912;            /* deepest, body backdrop */
    --bg-1:           #0a1224;            /* widget canvas tone */
    --bg-2:           #0f1a30;            /* iframe + inner well */
    --surface:        #121c32;            /* solid — iframes don't play nice with translucency */
    --surface-solid:  #121c32;
    --surface-bar:    #0c1426;

    /* Strokes */
    --stroke:         rgba(148, 170, 210, 0.10);
    --stroke-strong:  rgba(148, 170, 210, 0.18);
    --stroke-focus:   rgba(120, 170, 255, 0.55);

    /* Text */
    --text-1:         #e6ecf7;
    --text-2:         #9aa8c4;
    --text-3:         #6a7896;

    /* Accents — deep blue family */
    --blue-100:       #cfe0ff;
    --blue-300:       #7da4ff;
    --blue-500:       #4a7dff;            /* primary accent */
    --blue-600:       #2f63e5;
    --blue-glow:      rgba(74, 125, 255, 0.35);

    /* Semantic */
    --danger:         #ff7a85;
    --hot:            #ff9a76;
    --cold:           #7eb3ff;

    /* Effects */
    --radius-lg:      16px;
    --radius-md:      12px;
    --radius-sm:      8px;
    --radius-pill:    999px;
    --blur:           saturate(140%) blur(20px);
    --shadow-1:       0 1px 0 rgba(255,255,255,0.04) inset, 0 12px 28px -12px rgba(0,0,0,0.7), 0 2px 8px rgba(0,0,0,0.35);
    --shadow-2:       0 1px 0 rgba(255,255,255,0.05) inset, 0 24px 60px -20px rgba(0,0,0,0.85), 0 8px 24px rgba(0,0,0,0.5);
    --ease:           cubic-bezier(.2,.7,.2,1);
}

* { box-sizing: border-box; }

html, body {
    width: 100%;
    height: 100%;
    margin: 0;
    color: var(--text-1);
    background:
        radial-gradient(1200px 700px at 12% -10%, rgba(74,125,255,0.10), transparent 60%),
        radial-gradient(900px 600px at 100% 110%, rgba(40,80,180,0.10), transparent 55%),
        linear-gradient(180deg, #060c1c 0%, #050912 100%);
    overflow: hidden;
    touch-action: none;
    user-select: none;
    font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif;
    font-feature-settings: "cv11","ss01","ss03";
    -webkit-font-smoothing: antialiased;
    text-rendering: optimizeLegibility;
}

/* faint dot grid wash on the desktop */
body::before {
    content: "";
    position: fixed;
    inset: 0;
    pointer-events: none;
    background-image: radial-gradient(rgba(120,150,200,0.06) 1px, transparent 1px);
    background-size: 28px 28px;
    mask-image: radial-gradient(ellipse at center, rgba(0,0,0,0.9), rgba(0,0,0,0.2) 70%, transparent);
    z-index: 0;
}

/* Floating clock (legacy, hidden by default) */
.clock {
    position: fixed;
    top: 24px;
    right: 24px;
    font-size: 48px;
    font-weight: 600;
    color: var(--text-1);
    letter-spacing: -0.02em;
    z-index: 1000;
    text-shadow: 0 4px 24px rgba(0,0,0,0.5);
    user-select: none;
    touch-action: none;
    cursor: grab;
    transition: transform 0.1s ease-out;
    display: none;
    flex-direction: column;
    align-items: flex-end;
}

.clock-time { line-height: 1; }
.clock-date { font-size: 0.3em; margin-top: 6px; opacity: 0.85; color: var(--text-2); }

/* ============================================================
   Window (URL window with input bar, and frameless iframe wins)
   ============================================================ */
.window {
    position: absolute;
    width: 500px;
    height: 500px;
    background: var(--surface);
    border-radius: var(--radius-lg);
    border: 1px solid var(--stroke);
    display: flex;
    flex-direction: column;
    box-shadow: var(--shadow-2);
    touch-action: none;
    overflow: hidden;
    z-index: 1;
}

.window.no-input-bar .iframe-wrap { border-radius: var(--radius-lg); }

.window.split-view {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-template-rows: 52px 1fr;
}
.window.split-view .input-bar { grid-column: 1 / -1; }
.window.split-view .iframe-wrap { border-right: 1px solid var(--stroke); }
.window.split-view .auth-iframe-wrap { display: flex; flex-direction: column; overflow: hidden; }

/* Grab bar — used on every widget */
.grab-bar,
.weather-grab-bar,
.forecast-grab-bar,
.cams-grab-bar,
.clock-widget-grab-bar,
.internet-speed-grab-bar,
.pup-pics-grab-bar,
.lights-grab-bar,
.overseerr-grab-bar {
    height: 30px;
    background: var(--surface-bar);
    border-bottom: 1px solid var(--stroke);
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 12px;
    position: relative;
}

.grab-bar:active,
.weather-grab-bar:active,
.forecast-grab-bar:active,
.cams-grab-bar:active,
.clock-widget-grab-bar:active,
.internet-speed-grab-bar:active,
.pup-pics-grab-bar:active,
.lights-grab-bar:active,
.overseerr-grab-bar:active { cursor: grabbing; }

/* dotted drag handle on the left */
.grab-bar::before,
.weather-grab-bar::before,
.forecast-grab-bar::before,
.cams-grab-bar::before,
.clock-widget-grab-bar::before,
.internet-speed-grab-bar::before,
.pup-pics-grab-bar::before,
.lights-grab-bar::before,
.overseerr-grab-bar::before {
    content: '';
    width: 18px;
    height: 8px;
    background-image: radial-gradient(circle, rgba(154,168,196,0.55) 1.2px, transparent 1.4px);
    background-size: 4px 4px;
    background-position: 0 0;
    opacity: 0.7;
}

/* ============================================================
   Input bar (URL window)
   ============================================================ */
.input-bar {
    height: 52px;
    display: flex;
    padding: 8px;
    gap: 8px;
    background: var(--surface-bar);
    border-bottom: 1px solid var(--stroke);
    align-items: center;
}

.input-bar button.icon-btn,
.close-btn,
.refresh-btn,
.new-tab-btn {
    width: 36px;
    height: 36px;
    border-radius: var(--radius-pill);
    border: 1px solid var(--stroke);
    background: rgba(255,255,255,0.02);
    color: var(--text-2);
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
    transition: background 0.16s var(--ease), color 0.16s var(--ease), border-color 0.16s var(--ease), transform 0.08s var(--ease);
    padding: 0;
}
.input-bar button.icon-btn:hover,
.close-btn:hover,
.refresh-btn:hover,
.new-tab-btn:hover {
    background: rgba(120,170,255,0.10);
    color: var(--blue-100);
    border-color: var(--stroke-strong);
}
.input-bar button.icon-btn:active,
.close-btn:active,
.refresh-btn:active,
.new-tab-btn:active { transform: scale(0.94); }

.close-btn { color: var(--danger); }
.close-btn:hover { background: rgba(255,122,133,0.12); color: var(--danger); border-color: rgba(255,122,133,0.35); }

.new-tab-btn { margin-left: auto; }

.input-bar button.icon-btn svg,
.close-btn svg, .refresh-btn svg, .new-tab-btn svg {
    width: 16px; height: 16px; stroke-width: 2;
}

.input-bar input {
    flex: 1;
    height: 36px;
    border-radius: var(--radius-pill);
    border: 1px solid var(--stroke);
    padding: 0 16px;
    font-size: 14px;
    font-family: inherit;
    background: rgba(5, 10, 22, 0.6);
    color: var(--text-1);
    outline: none;
    transition: border-color 0.16s var(--ease), box-shadow 0.16s var(--ease), background 0.16s var(--ease);
}
.input-bar input::placeholder { color: var(--text-3); }
.input-bar input:focus {
    border-color: var(--stroke-focus);
    background: rgba(5,10,22,0.9);
    box-shadow: 0 0 0 3px var(--blue-glow);
}

.input-bar button.go-btn {
    height: 36px;
    padding: 0 18px;
    border-radius: var(--radius-pill);
    border: 1px solid rgba(74,125,255,0.35);
    background: linear-gradient(180deg, rgba(74,125,255,0.22), rgba(74,125,255,0.10));
    color: var(--blue-100);
    font-size: 13px;
    font-weight: 600;
    font-family: inherit;
    letter-spacing: 0.02em;
    cursor: pointer;
    transition: background 0.16s var(--ease), border-color 0.16s var(--ease), transform 0.08s var(--ease);
}
.input-bar button.go-btn:hover {
    background: linear-gradient(180deg, rgba(74,125,255,0.32), rgba(74,125,255,0.18));
    border-color: rgba(120,170,255,0.55);
}
.input-bar button.go-btn:active { transform: scale(0.97); }

/* Iframe container */
.iframe-wrap {
    flex: 1;
    overflow: hidden;
    background: var(--bg-2);
}

iframe {
    width: 100%;
    height: 100%;
    border: none;
}

/* Auth popup overlay */
.auth-overlay {
    position: absolute;
    inset: 0;
    background: rgba(5, 10, 22, 0.92);
    display: none;
    align-items: center;
    justify-content: center;
    z-index: 10;
}
.auth-overlay.active { display: flex; }
.auth-message { color: var(--blue-100); font-size: 14px; text-align: center; }

.auth-iframe-wrap { display: none; flex-direction: column; }
.auth-iframe-wrap.active { display: flex; }

.auth-header {
    height: 40px;
    background: var(--surface-bar);
    border-bottom: 1px solid var(--stroke);
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 0 12px;
    color: var(--text-2);
    font-size: 12px;
    font-weight: 500;
    letter-spacing: 0.04em;
    text-transform: uppercase;
}

.auth-close-btn {
    width: 28px;
    height: 28px;
    border-radius: var(--radius-pill);
    border: 1px solid var(--stroke);
    background: rgba(255,255,255,0.02);
    color: var(--danger);
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    transition: background 0.16s var(--ease);
}
.auth-close-btn:hover { background: rgba(255,122,133,0.12); }

.auth-iframe-wrap iframe { flex: 1; width: 100%; height: 100%; border: none; }

/* Resize handle — common shared style */
.resize,
.weather-resize,
.forecast-resize,
.cams-resize,
.clock-widget-resize,
.internet-speed-resize,
.pup-pics-resize,
.lights-resize,
.overseerr-resize,
.search-resize {
    position: absolute;
    width: 22px;
    height: 22px;
    right: 4px;
    bottom: 4px;
    cursor: nwse-resize;
    touch-action: none;
    background: transparent;
    border-radius: 0;
    opacity: 0.5;
    transition: opacity 0.18s var(--ease);
}
.resize::before,
.weather-resize::before,
.forecast-resize::before,
.cams-resize::before,
.clock-widget-resize::before,
.internet-speed-resize::before,
.pup-pics-resize::before,
.lights-resize::before,
.overseerr-resize::before,
.search-resize::before {
    content: '';
    position: absolute;
    inset: 0;
    background-image:
        radial-gradient(circle, rgba(154,168,196,0.85) 1.2px, transparent 1.4px);
    background-size: 5px 5px;
    background-position: right bottom;
    -webkit-mask-image: linear-gradient(135deg, transparent 50%, #000 55%);
    mask-image: linear-gradient(135deg, transparent 50%, #000 55%);
}
.resize:hover,
.weather-resize:hover,
.forecast-resize:hover,
.cams-resize:hover,
.clock-widget-resize:hover,
.internet-speed-resize:hover,
.pup-pics-resize:hover,
.lights-resize:hover,
.overseerr-resize:hover,
.search-resize:hover { opacity: 1; }

/* ============================================================
   Shared widget shell — all widgets share these base styles
   ============================================================ */
.weather-widget,
.forecast-widget,
.cams-widget,
.clock-widget,
.internet-speed-widget,
.pup-pics-widget,
.lights-widget,
.overseerr-widget {
    position: absolute;
    background: var(--surface);
    border-radius: var(--radius-lg);
    border: 1px solid var(--stroke);
    display: flex;
    flex-direction: column;
    box-shadow: var(--shadow-1);
    touch-action: none;
    overflow: hidden;
    z-index: 1;
}

.widget-name {
    font-size: 10.5px;
    color: var(--text-2);
    font-weight: 600;
    letter-spacing: 0.12em;
    text-transform: uppercase;
}

/* ============================================================
   Weather Widget
   ============================================================ */
.weather-widget {
    width: 320px;
    height: 280px;
    container-type: size;
    container-name: weather;
}

.weather-content {
    flex: 1;
    padding: 6px;
    padding-top: 4px;
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
    font-weight: 700;
    color: var(--text-1);
    line-height: 1;
    letter-spacing: -0.03em;
    font-variant-numeric: tabular-nums;
}

.weather-icon {
    font-size: clamp(50px, 35cqw, 200px);
    animation: float 3s ease-in-out infinite;
    line-height: 1;
    filter: drop-shadow(0 4px 18px rgba(74,125,255,0.25));
}

@keyframes float {
    0%, 100% { transform: translateY(0px); }
    50% { transform: translateY(-8px); }
}

.weather-description {
    font-size: clamp(13px, 5.5cqw, 26px);
    color: var(--text-1);
    text-transform: capitalize;
    flex-shrink: 0;
    line-height: 1.2;
    text-align: center;
    font-weight: 500;
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
    font-size: clamp(9px, 3.5cqw, 14px);
    color: var(--text-3);
    text-transform: uppercase;
    letter-spacing: 0.08em;
    line-height: 1.2;
    font-weight: 600;
}

.weather-detail-value {
    font-size: clamp(16px, 6cqw, 28px);
    color: var(--text-1);
    font-weight: 600;
    line-height: 1.2;
    font-variant-numeric: tabular-nums;
}

.weather-location {
    font-size: clamp(10px, 4cqw, 16px);
    color: var(--text-2);
    text-align: center;
    font-weight: 500;
    letter-spacing: 0.04em;
    padding: 6px 0;
    border-top: 1px solid var(--stroke);
    border-bottom: 1px solid var(--stroke);
    line-height: 1.2;
    width: 100%;
}

.weather-clock {
    font-size: clamp(11px, 4.5cqw, 18px);
    color: var(--text-1);
    text-align: center;
    font-weight: 500;
    padding-bottom: 6px;
    border-bottom: 1px solid var(--stroke);
    width: 100%;
    display: flex;
    flex-direction: column;
    gap: 2px;
}
.weather-clock-time { font-size: clamp(22px, 15cqw, 72px); font-weight: 700; letter-spacing: -0.03em; }
.weather-clock-date { font-size: clamp(12px, 5cqw, 20px); color: var(--text-2); }

/* ============================================================
   5-Day Forecast Widget
   ============================================================ */
.forecast-widget {
    width: 307.2px;
    height: 98.304px;
    container-type: size;
    container-name: forecast;
    font-size: 0.512;
}

.forecast-content {
    flex: 1;
    padding: 6px;
    display: flex;
    gap: 5px;
    overflow: hidden;
    container-type: size;
}

@container (max-height: 150px) {
    .forecast-day {
        padding: 4px 8px;
    }
    .forecast-icon { flex-shrink: 0; }
}

.forecast-day {
    flex: 1;
    background: rgba(5,10,22,0.45);
    border-radius: var(--radius-md);
    border: 1px solid var(--stroke);
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    padding: clamp(2.56px, 2cqw, 7.68px);
    position: relative;
    gap: clamp(2.56px, 2cqw, 7.68px);
}

.forecast-info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;
    gap: clamp(1.28px, 1cqw, 3.84px);
}

.forecast-day-label {
    position: absolute;
    top: 6px;
    left: 8px;
    font-size: clamp(11px, 4.8cqw, 18px);
    font-weight: 700;
    color: var(--text-2);
    letter-spacing: 0.04em;
}

.forecast-icon {
    font-size: clamp(35px, 17.3cqw, 70px);
    animation: float 3s ease-in-out infinite;
    line-height: 1;
    flex-shrink: 0;
    filter: drop-shadow(0 2px 10px rgba(74,125,255,0.2));
}

.forecast-temps {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 2px;
}

.forecast-high {
    font-size: clamp(18px, 8cqw, 32px);
    font-weight: 700;
    color: var(--hot);
    line-height: 1;
    font-variant-numeric: tabular-nums;
}

.forecast-low {
    font-size: clamp(15px, 6.8cqw, 26px);
    font-weight: 600;
    color: var(--cold);
    line-height: 1;
    font-variant-numeric: tabular-nums;
}

.forecast-precip {
    font-size: clamp(12px, 5.4cqw, 20px);
    color: var(--text-2);
    line-height: 1;
    display: flex;
    align-items: center;
    gap: 2px;
    font-variant-numeric: tabular-nums;
}

.forecast-precip::before {
    content: '💧';
    font-size: clamp(10px, 4.5cqw, 18px);
    filter: drop-shadow(0 1px 4px rgba(126,179,255,0.4));
}

/* ============================================================
   Cams Widget
   ============================================================ */
.cams-widget {
    width: 400px;
    height: 500px;
}
.cams-content {
    flex: 1;
    overflow: hidden;
    background: var(--bg-2);
}
.cams-content iframe { width: 100%; height: 100%; border: none; display: block; }

/* ============================================================
   Padlock — bottom-left lock toggle
   ============================================================ */
.padlock-btn {
    position: fixed;
    bottom: 20px;
    left: 20px;
    width: 44px;
    height: 44px;
    border-radius: 14px;
    background: rgba(18, 28, 50, 0.92);
    border: 1px solid var(--stroke);
    color: var(--text-2);
    cursor: pointer;
    z-index: 999;
    transition: background 0.2s var(--ease), color 0.2s var(--ease), border-color 0.2s var(--ease);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0;
}
.padlock-btn:hover { background: rgba(30,42,68,0.85); color: var(--blue-100); border-color: var(--stroke-strong); }
.padlock-btn.locked { color: var(--blue-300); border-color: rgba(120,170,255,0.35); background: rgba(74,125,255,0.10); }
.padlock-btn svg { width: 18px; height: 18px; }

/* ============================================================
   Clock Widget
   ============================================================ */
.clock-widget {
    width: 300px;
    height: 200px;
}
.clock-widget-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 10px;
}
.clock-widget-time {
    font-size: clamp(36px, 10vw, 72px);
    font-weight: 700;
    letter-spacing: -0.03em;
    color: var(--text-1);
    line-height: 1;
    font-variant-numeric: tabular-nums;
}
.clock-widget-date {
    font-size: clamp(12px, 3vw, 18px);
    color: var(--text-2);
    text-align: center;
    font-weight: 500;
    letter-spacing: 0.04em;
    line-height: 1.2;
}

/* ============================================================
   Internet Speed / Pup Pics / Lights / Overseerr
   ============================================================ */
.internet-speed-widget,
.pup-pics-widget,
.lights-widget,
.overseerr-widget { width: 300px; height: 200px; }

.internet-speed-content,
.lights-content,
.overseerr-content {
    flex: 1;
    overflow: hidden;
    background: var(--bg-2);
}
.pup-pics-content {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background: var(--bg-2);
}
.internet-speed-content iframe { width: 100%; height: 100%; border: none; display: block; zoom: 0.5; }
.lights-content iframe,
.overseerr-content iframe { width: 100%; height: 100%; border: none; display: block; }

/* ============================================================
   Inline size +/- controls (used on clock widget header)
   ============================================================ */
.clock-size-controls,
.size-controls {
    display: flex;
    gap: 4px;
    align-items: center;
    flex-shrink: 0;
}

.clock-size-btn,
.size-btn {
    width: 22px;
    height: 22px;
    border: 1px solid var(--stroke);
    border-radius: 6px;
    background: rgba(255,255,255,0.02);
    color: var(--text-2);
    font-size: 13px;
    font-weight: 600;
    font-family: inherit;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    transition: background 0.16s var(--ease), color 0.16s var(--ease), border-color 0.16s var(--ease);
}
.clock-size-btn:hover,
.size-btn:hover {
    background: rgba(120,170,255,0.10);
    color: var(--blue-100);
    border-color: var(--stroke-strong);
}

.cursor-circle {
    position: fixed;
    border: 2px solid var(--blue-300);
    border-radius: 50%;
    pointer-events: none;
    z-index: 1001;
    display: none;
    opacity: 0.7;
}

.scratchpad-brush-preview {
    width: 40px;
    height: 40px;
    border: 1px solid var(--stroke);
    border-radius: var(--radius-sm);
    background: var(--bg-2);
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}

/* ============================================================
   Touch keyboard
   ============================================================ */
#touchKbd {
    position: fixed;
    left: 50%;
    bottom: 16px;
    transform: translate(-50%, 100%);
    width: min(1000px, calc(100vw - 32px));
    background: #0c1426;
    border: 1px solid var(--stroke);
    border-radius: 18px;
    box-shadow: var(--shadow-2);
    padding: 10px;
    z-index: 2000;
    opacity: 0;
    pointer-events: none;
    transition: transform 0.32s var(--ease), opacity 0.24s var(--ease);
    user-select: none;
    touch-action: none;
}
#touchKbd.show {
    transform: translate(-50%, 0);
    opacity: 1;
    pointer-events: auto;
}

#touchKbd .kbd-header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 2px 8px 8px;
    cursor: grab;
}
#touchKbd .kbd-header:active { cursor: grabbing; }

#touchKbd .kbd-handle {
    width: 36px;
    height: 4px;
    border-radius: 2px;
    background: rgba(154,168,196,0.35);
    margin: 0 auto;
}

#touchKbd .kbd-title {
    font-size: 10.5px;
    font-weight: 600;
    color: var(--text-3);
    letter-spacing: 0.14em;
    text-transform: uppercase;
}

#touchKbd .kbd-hide {
    width: 28px;
    height: 28px;
    border-radius: 8px;
    background: rgba(255,255,255,0.02);
    border: 1px solid var(--stroke);
    color: var(--text-2);
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0;
}
#touchKbd .kbd-hide:hover { background: rgba(120,170,255,0.10); color: var(--blue-100); }
#touchKbd .kbd-hide svg { width: 14px; height: 14px; }

#touchKbd .kbd-row {
    display: flex;
    gap: 6px;
    margin-top: 6px;
    justify-content: center;
}

#touchKbd .key {
    flex: 1 1 0;
    height: 48px;
    min-width: 36px;
    border-radius: 10px;
    border: 1px solid var(--stroke);
    background: linear-gradient(180deg, rgba(255,255,255,0.04), rgba(255,255,255,0.01));
    color: var(--text-1);
    font-family: inherit;
    font-size: 16px;
    font-weight: 500;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0 6px;
    transition: background 0.08s var(--ease), border-color 0.12s var(--ease), transform 0.06s var(--ease);
    touch-action: manipulation;
}
#touchKbd .key:active,
#touchKbd .key.pressed {
    background: linear-gradient(180deg, rgba(74,125,255,0.30), rgba(74,125,255,0.14));
    border-color: rgba(120,170,255,0.55);
    transform: translateY(1px);
}

#touchKbd .key.wide { flex: 1.5 1 0; font-size: 12px; color: var(--text-2); font-weight: 600; letter-spacing: 0.04em; }
#touchKbd .key.space { flex: 6 1 0; font-size: 12px; color: var(--text-3); font-weight: 500; letter-spacing: 0.08em; text-transform: uppercase; }
#touchKbd .key.enter { flex: 2 1 0; color: var(--blue-100); border-color: rgba(120,170,255,0.35); background: linear-gradient(180deg, rgba(74,125,255,0.18), rgba(74,125,255,0.06)); font-size: 12px; font-weight: 600; letter-spacing: 0.04em; }
#touchKbd .key.shift.active { color: var(--blue-100); border-color: rgba(120,170,255,0.55); background: linear-gradient(180deg, rgba(74,125,255,0.24), rgba(74,125,255,0.10)); }
#touchKbd .key.layer.active { color: var(--blue-100); border-color: rgba(120,170,255,0.55); background: linear-gradient(180deg, rgba(74,125,255,0.24), rgba(74,125,255,0.10)); }

#touchKbd .key svg { width: 18px; height: 18px; }

/* ============================================================
   Service widget controls + fallback launcher
   (used by cams, lights, overseerr, internet-speed)
   ============================================================ */
.svc-controls {
    display: inline-flex;
    gap: 4px;
    align-items: center;
}
.svc-btn {
    width: 22px;
    height: 22px;
    border: 1px solid var(--stroke);
    border-radius: 6px;
    background: rgba(255,255,255,0.02);
    color: var(--text-2);
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    transition: background 0.16s var(--ease), color 0.16s var(--ease), border-color 0.16s var(--ease), transform 0.08s var(--ease);
}
.svc-btn:hover { background: rgba(120,170,255,0.10); color: var(--blue-100); border-color: var(--stroke-strong); }
.svc-btn:active { transform: scale(0.92); }
.svc-btn svg { width: 12px; height: 12px; stroke-width: 2; }

/* Launcher tile shown when iframe is blocked / empty */
.svc-fallback {
    position: absolute;
    inset: 0;
    background:
        radial-gradient(600px 280px at 50% -10%, rgba(74,125,255,0.14), transparent 70%),
        linear-gradient(180deg, rgba(10,18,36,0.5), rgba(10,18,36,0.85));
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 14px;
    padding: 20px;
    z-index: 1;
    pointer-events: auto;
}
.svc-fallback-icon {
    width: 56px;
    height: 56px;
    border-radius: 16px;
    background: linear-gradient(180deg, rgba(74,125,255,0.20), rgba(74,125,255,0.06));
    border: 1px solid rgba(120,170,255,0.35);
    display: inline-flex;
    align-items: center;
    justify-content: center;
    color: var(--blue-100);
    box-shadow: 0 8px 24px -10px rgba(74,125,255,0.45);
}
.svc-fallback-icon svg { width: 26px; height: 26px; stroke-width: 1.75; }
.svc-fallback-title {
    font-size: 15px;
    font-weight: 600;
    color: var(--text-1);
    letter-spacing: -0.01em;
    text-align: center;
}
.svc-fallback-sub {
    font-size: 12px;
    color: var(--text-3);
    text-align: center;
    line-height: 1.5;
    max-width: 240px;
}
.svc-fallback-sub code {
    font-family: 'JetBrains Mono', ui-monospace, Menlo, monospace;
    font-size: 11px;
    color: var(--blue-300);
    background: rgba(74,125,255,0.10);
    padding: 1px 6px;
    border-radius: 4px;
}
.svc-fallback-actions {
    display: flex;
    gap: 8px;
    flex-wrap: wrap;
    justify-content: center;
}
.svc-fallback-btn {
    height: 34px;
    padding: 0 14px;
    border-radius: var(--radius-pill);
    border: 1px solid rgba(74,125,255,0.35);
    background: linear-gradient(180deg, rgba(74,125,255,0.22), rgba(74,125,255,0.10));
    color: var(--blue-100);
    font-family: inherit;
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.02em;
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    gap: 6px;
    transition: background 0.16s var(--ease), border-color 0.16s var(--ease), transform 0.08s var(--ease);
}
.svc-fallback-btn:hover {
    background: linear-gradient(180deg, rgba(74,125,255,0.32), rgba(74,125,255,0.18));
    border-color: rgba(120,170,255,0.55);
}
.svc-fallback-btn:active { transform: scale(0.97); }
.svc-fallback-btn.ghost {
    background: rgba(255,255,255,0.02);
    border-color: var(--stroke-strong);
    color: var(--text-2);
}
.svc-fallback-btn.ghost:hover { color: var(--blue-100); background: rgba(120,170,255,0.10); }
.svc-fallback-btn svg { width: 12px; height: 12px; stroke-width: 2; }

/* Small floating "open externally" hint inside iframe area */
.svc-corner-launch {
    position: absolute;
    right: 8px;
    bottom: 8px;
    width: 28px;
    height: 28px;
    border-radius: 8px;
    border: 1px solid var(--stroke);
    background: rgba(10,18,36,0.7);
    backdrop-filter: blur(8px);
    -webkit-backdrop-filter: blur(8px);
    color: var(--text-2);
    cursor: pointer;
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    opacity: 0;
    transform: translateY(4px);
    transition: opacity 0.18s var(--ease), transform 0.18s var(--ease), background 0.16s var(--ease);
    z-index: 2;
    pointer-events: auto;
}
.svc-corner-launch.visible { opacity: 1; transform: translateY(0); }
.svc-corner-launch:hover { background: rgba(74,125,255,0.18); color: var(--blue-100); border-color: var(--stroke-strong); }
.svc-corner-launch svg { width: 13px; height: 13px; stroke-width: 2; }

/* iframe wrapper needs relative for the overlay positioning */
.cams-content,
.lights-content,
.overseerr-content,
.internet-speed-content { position: relative; }
</style>
</head>
<body>

<button class="padlock-btn" id="padlockBtn" aria-label="Lock layout" title="Lock layout">
    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
        <rect x="4" y="11" width="16" height="10" rx="2"></rect>
        <path d="M8 11V8a4 4 0 0 1 8 0v3"></path>
    </svg>
</button>

<div class="cursor-circle" id="cursorCircle"></div>

<div class="clock" id="clock"></div>

<div class="weather-widget" id="weatherWidget">
    <div class="weather-grab-bar">
        <span class="widget-name">Weather</span>
    </div>
    <div class="weather-content">
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
    <div class="forecast-grab-bar">
        <span class="widget-name">Forecast</span>
    </div>
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

<div class="cams-widget" id="camsWidget">
    <div class="cams-grab-bar">
        <span class="widget-name">Cams</span>
    </div>
    <div class="cams-content">
        <iframe src="https://cams.add2plex.com" allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media" credentials="include" referrerpolicy="no-referrer-when-downgrade" allowfullscreen></iframe>
    </div>
    <div class="cams-resize"></div>
</div>

<div class="clock-widget" id="clockWidget">
    <div class="clock-widget-grab-bar">
        <span class="widget-name">Clock</span>
        <div class="clock-size-controls">
            <button class="clock-size-btn" id="clockMinusBtn">−</button>
            <button class="clock-size-btn" id="clockPlusBtn">+</button>
        </div>
    </div>
    <div class="clock-widget-content">
        <div class="clock-widget-time" id="clockWidgetTime">--:-- --</div>
        <div class="clock-widget-date" id="clockWidgetDate">Loading...</div>
    </div>
    <div class="clock-widget-resize"></div>
</div>

<div class="internet-speed-widget" id="internetSpeedWidget">
    <div class="internet-speed-grab-bar">
        <span class="widget-name">Internet Speed</span>
    </div>
    <div class="internet-speed-content">
        <iframe src="https://speed.add2plex.com/" allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media" credentials="include" referrerpolicy="no-referrer-when-downgrade" allowfullscreen></iframe>
    </div>
    <div class="internet-speed-resize"></div>
</div>

<div class="pup-pics-widget" id="pupPicsWidget">
    <div class="pup-pics-grab-bar">
        <span class="widget-name">Pup Pics</span>
    </div>
    <div class="pup-pics-content" id="pupPicsContent">
        <img id="pupPicsImage" alt="Cute Dog Picture" style="width: 100%; height: 100%; object-fit: cover; opacity: 0;">
    </div>
    <div class="pup-pics-resize"></div>
</div>

<div class="lights-widget" id="lightsWidget">
    <div class="lights-grab-bar">
        <span class="widget-name">Lights</span>
    </div>
    <div class="lights-content">
        <iframe src="https://192.168.1.168:5000/" allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media" credentials="include" referrerpolicy="no-referrer-when-downgrade" allowfullscreen></iframe>
    </div>
    <div class="lights-resize"></div>
</div>

<div class="overseerr-widget" id="overseerrWidget">
    <div class="overseerr-grab-bar">
        <span class="widget-name">Overseerr</span>
    </div>
    <div class="overseerr-content">
        <iframe src="https://192.168.1.168:5055" allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media" credentials="include" referrerpolicy="no-referrer-when-downgrade" allowfullscreen></iframe>
    </div>
    <div class="overseerr-resize"></div>
</div>

<script>
// Enable third-party cookies and credentials globally
document.cookie = "cookiesEnabled=true; SameSite=None; Secure";

let zIndex = 1;
let isLocked = false;
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
    hours = hours ? hours : 12;
    const minutesStr = minutes < 10 ? '0' + minutes : minutes;
    
    const days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];
    const months = ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'];
    
    const dayName = days[now.getDay()];
    const monthName = months[now.getMonth()];
    const date = now.getDate();
    const year = now.getFullYear();
    
    const clockWidgetTime = document.getElementById('clockWidgetTime');
    const clockWidgetDate = document.getElementById('clockWidgetDate');
    if (clockWidgetTime && clockWidgetDate) {
        clockWidgetTime.textContent = `${hours}:${minutesStr} ${ampm}`;
        clockWidgetDate.textContent = `${dayName}, ${monthName} ${date} ${year}`;
    }
}

updateClock();
setInterval(updateClock, 1000);

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
        const screenWidth = window.innerWidth;
        const centerX = screenWidth / 2;
        const clockCenterX = clockOffsetX + (clockEl.offsetWidth / 2);
        if (Math.abs(clockCenterX - centerX) <= 20) {
            clockEl.style.alignItems = 'center';
        } else if (clockCenterX < centerX) {
            clockEl.style.alignItems = 'flex-start';
        } else {
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
        clockScale = Math.max(0.5, Math.min(clockScale, 3));
        clockEl.style.transform = `scale(${clockScale})`;
        clockEl.style.transformOrigin = 'top left';
    }
});

clockEl.addEventListener('wheel', (e) => {
    e.preventDefault();
    const delta = e.deltaY > 0 ? -0.1 : 0.1;
    clockScale += delta;
    clockScale = Math.max(0.5, Math.min(clockScale, 3));
    clockEl.style.transform = `scale(${clockScale})`;
    clockEl.style.transformOrigin = 'top left';
});

async function fetchWeather() {
    try {
        const lat = 30.1588;
        const lon = -85.6602;
        const response = await fetch(`https://api.open-meteo.com/v1/forecast?latitude=${lat}&longitude=${lon}&current=temperature_2m,relative_humidity_2m,precipitation,weather_code&daily=sunrise,sunset&temperature_unit=fahrenheit&wind_speed_unit=mph&precipitation_unit=inch&timezone=America%2FChicago`);
        const data = await response.json();
        
        const temp = Math.round(data.current.temperature_2m);
        const humidity = data.current.relative_humidity_2m;
        const precipitation = data.current.precipitation || 0;
        const weatherCode = data.current.weather_code;
        
        const localNow = new Date();
        const currentHour = localNow.getHours();
        const currentMin = localNow.getMinutes();
        
        const today = localNow.toISOString().split('T')[0];
        const dailyIndex = data.daily.time.indexOf(today);
        
        let isNightTime = false;
        
        if (dailyIndex >= 0 && data.daily.sunrise && data.daily.sunset) {
            const sunriseStr = data.daily.sunrise[dailyIndex];
            const sunsetStr = data.daily.sunset[dailyIndex];
            const sunriseHourMin = sunriseStr.substring(11, 16);
            const sunsetHourMin = sunsetStr.substring(11, 16);
            const currentHourMin = currentHour.toString().padStart(2, '0') + ':' + currentMin.toString().padStart(2, '0');
            isNightTime = currentHourMin > sunsetHourMin || currentHourMin < sunriseHourMin;
        }
        
        const weatherInfo = getWeatherInfo(weatherCode);
        let finalIcon = weatherInfo.icon;
        if (isNightTime) {
            finalIcon = '🌙';
        }
        
        document.querySelector('.weather-temp').textContent = `${temp}°F`;
        document.querySelector('.weather-icon').textContent = finalIcon;
        document.querySelector('.weather-description').textContent = weatherInfo.description;
        document.querySelector('.weather-details .weather-detail:nth-child(1) .weather-detail-value').textContent = `${humidity}%`;
        document.querySelector('.weather-details .weather-detail:nth-child(2) .weather-detail-value').textContent = `${(precipitation * 100).toFixed(0)}%`;
    } catch (error) {
        console.error('Error fetching weather:', error);
        document.querySelector('.weather-description').textContent = 'Unable to load weather';
    }
}

let pupPicsIntervalId = null;
let pupPicsObserver = null;
let nextPupPicsUrl = null;
let isLoadingNextImage = false;
let preloadRetryId = null;

// Multiple dog image API sources
const dogApiSources = [
    {
        name: 'random.dog',
        fetch: async () => {
            const response = await fetch('https://random.dog/woof.json');
            const data = await response.json();
            if (data && data.url) {
                const url = data.url.toLowerCase();
                if (url.endsWith('.mp4') || url.endsWith('.webm') || url.endsWith('.gif')) {
                    return null; // Skip videos and gifs
                }
                return data.url;
            }
            return null;
        }
    },
    {
        name: 'dog.ceo',
        fetch: async () => {
            const response = await fetch('https://dog.ceo/api/breeds/image/random');
            const data = await response.json();
            if (data && data.status === 'success' && data.message) {
                return data.message;
            }
            return null;
        }
    },
    {
        name: 'thedogapi',
        fetch: async () => {
            const response = await fetch('https://api.thedogapi.com/v1/images/search?size=med&mime_types=jpg,png');
            const data = await response.json();
            if (data && data.length > 0 && data[0].url) {
                return data[0].url;
            }
            return null;
        }
    },
    {
        name: 'shibe.online',
        fetch: async () => {
            const response = await fetch('https://shibe.online/api/shibes?count=1&urls=true');
            const data = await response.json();
            if (data && data.length > 0) {
                return data[0];
            }
            return null;
        }
    },
    {
        name: 'place.dog',
        fetch: async () => {
            // Generate random dimensions for variety
            const width = 400 + Math.floor(Math.random() * 200);
            const height = 400 + Math.floor(Math.random() * 200);
            return `https://place.dog/${width}/${height}?random=${Date.now()}`;
        }
    }
];

let lastDogSourceIndex = -1;

async function getRandomDogImage() {
    // Rotate through sources to ensure variety
    let attempts = 0;
    while (attempts < dogApiSources.length * 2) {
        // Pick a different source than last time if possible
        let sourceIndex;
        do {
            sourceIndex = Math.floor(Math.random() * dogApiSources.length);
        } while (sourceIndex === lastDogSourceIndex && dogApiSources.length > 1 && attempts < dogApiSources.length);
        
        lastDogSourceIndex = sourceIndex;
        const source = dogApiSources[sourceIndex];
        
        try {
            const url = await source.fetch();
            if (url) {
                console.log(`Dog pic from: ${source.name}`);
                return url;
            }
        } catch (error) {
            console.error(`Error fetching from ${source.name}:`, error);
        }
        attempts++;
    }
    return null;
}

function initPupPics() {
    loadNextPupPic();
    const pupPicsWidget = document.getElementById('pupPicsWidget');
    pupPicsObserver = new ResizeObserver(() => {
        // Don't reload on resize, just let CSS handle it
    });
    pupPicsObserver.observe(pupPicsWidget);
}

function getAspectRatio() {
    const widget = document.getElementById('pupPicsWidget');
    const width = widget.offsetWidth;
    const height = widget.offsetHeight - 24;
    return width / height;
}

async function preloadNextImage() {
    if (isLoadingNextImage) return;
    isLoadingNextImage = true;
    
    try {
        const imageUrl = await getRandomDogImage();
        if (imageUrl) {
            nextPupPicsUrl = imageUrl;
        }
    } catch (error) {
        console.error('Error preloading dog pic:', error);
    } finally {
        isLoadingNextImage = false;
    }
}

function displayNextImage() {
    if (preloadRetryId) {
        clearTimeout(preloadRetryId);
        preloadRetryId = null;
    }
    if (nextPupPicsUrl) {
        const img = document.getElementById('pupPicsImage');
        const imageUrl = nextPupPicsUrl;
        nextPupPicsUrl = null;
        img.style.transition = 'opacity 1s ease-in-out';
        img.style.opacity = '0';
        setTimeout(() => {
            img.src = imageUrl;
            img.alt = 'Cute dog picture';
            img.style.opacity = '1';
            preloadNextImage();
            pupPicsIntervalId = setTimeout(displayNextImage, 20000);
        }, 1000);
    } else {
        loadNextPupPic();
    }
}

async function loadNextPupPic() {
    if (pupPicsIntervalId) {
        clearTimeout(pupPicsIntervalId);
    }
    if (preloadRetryId) {
        clearTimeout(preloadRetryId);
        preloadRetryId = null;
    }
    
    try {
        const imageUrl = await getRandomDogImage();
        if (imageUrl) {
            const img = document.getElementById('pupPicsImage');
            img.style.transition = 'opacity 1s ease-in-out';
            img.style.opacity = '0';
            setTimeout(() => {
                img.src = imageUrl;
                img.alt = 'Cute dog picture';
                img.style.opacity = '1';
                preloadNextImage();
                pupPicsIntervalId = setTimeout(displayNextImage, 20000);
            }, 1000);
        } else {
            // Retry after 2 seconds if no image found
            pupPicsIntervalId = setTimeout(loadNextPupPic, 2000);
        }
    } catch (error) {
        console.error('Error loading dog pic:', error);
        pupPicsIntervalId = setTimeout(loadNextPupPic, 2000);
    }
}

function saveWidgetLayout() {
    const layout = {};
    const widgets = [
        { id: 'weatherWidget', type: 'standard' },
        { id: 'forecastWidget', type: 'standard' },
        { id: 'radarWin', type: 'window' },
        { id: 'camsWidget', type: 'standard' },
        { id: 'clockWidget', type: 'standard' },
        { id: 'internetSpeedWidget', type: 'standard' },
        { id: 'pupPicsWidget', type: 'standard' },
        { id: 'lightsWidget', type: 'standard' },
        { id: 'overseerrWidget', type: 'standard' }
    ];
    widgets.forEach(widget => {
        const el = document.getElementById(widget.id);
        if (el) {
            layout[widget.id] = {
                left: el.style.left,
                top: el.style.top,
                width: el.style.width,
                height: el.style.height,
                zIndex: el.style.zIndex
            };
        }
    });
    localStorage.setItem('widgetLayout', JSON.stringify(layout));
    localStorage.setItem('widgetLayoutLocked', 'true');
    console.log('Widget layout saved to localStorage');
}

function loadWidgetLayout() {
    const savedLayout = localStorage.getItem('widgetLayout');
    const isLocked = localStorage.getItem('widgetLayoutLocked') === 'true';
    
    if (!savedLayout || !isLocked) return false;
    
    try {
        const layout = JSON.parse(savedLayout);
        Object.keys(layout).forEach(widgetId => {
            const el = document.getElementById(widgetId);
            if (el && layout[widgetId]) {
                if (layout[widgetId].left) el.style.left = layout[widgetId].left;
                if (layout[widgetId].top) el.style.top = layout[widgetId].top;
                if (layout[widgetId].width) el.style.width = layout[widgetId].width;
                if (layout[widgetId].height) el.style.height = layout[widgetId].height;
                if (layout[widgetId].zIndex) el.style.zIndex = layout[widgetId].zIndex;
            }
        });
        console.log('Widget layout restored from localStorage');
        return true;
    } catch (error) {
        console.error('Error loading widget layout:', error);
        return false;
    }
}

function clearWidgetLayout() {
    localStorage.removeItem('widgetLayoutLocked');
    console.log('Widget layout unlocked');
}

function getWeatherInfo(code) {
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

/* ============================================================
   Service widget chrome — reload + launch buttons in the
   header, and a fallback "Open externally" launcher tile
   for iframes that get refused by X-Frame-Options /
   frame-ancestors (common for Overseerr et al).
   ============================================================ */
function setupServiceWidget(widgetId, opts) {
    const widget = document.getElementById(widgetId);
    if (!widget) return;
    const iframe = widget.querySelector('iframe');
    const grabBar = widget.querySelector('[class*="grab-bar"]');
    const content = iframe ? iframe.parentElement : null;
    if (!iframe || !grabBar || !content) return;

    const url = opts.url || iframe.getAttribute('src');
    const label = opts.label || 'Service';
    const hint = opts.hint || url;

    // --- Header controls ---
    const controls = document.createElement('div');
    controls.className = 'svc-controls';
    controls.innerHTML = `
        <button class="svc-btn" data-svc="reload" title="Reload" aria-label="Reload ${label}">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M21 12a9 9 0 1 1-3-6.7"></path>
                <path d="M21 4v5h-5"></path>
            </svg>
        </button>
        <button class="svc-btn" data-svc="launch" title="Open in new window" aria-label="Open ${label} in new window">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M14 4h6v6"></path>
                <path d="M20 4L10 14"></path>
                <path d="M19 13v6a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1h6"></path>
            </svg>
        </button>
    `;
    grabBar.appendChild(controls);

    function reload() {
        clearFallback();
        cornerBtn.classList.remove('visible');
        // setting src to itself forces a reload while preserving the cache key
        const cur = iframe.getAttribute('src');
        iframe.removeAttribute('src');
        // re-add on next tick
        setTimeout(() => { iframe.setAttribute('src', cur || url); scheduleCheck(); }, 30);
    }
    function launch() { window.open(url, '_blank', 'noopener,noreferrer'); }

    controls.querySelector('[data-svc="reload"]').addEventListener('click', (e) => { e.stopPropagation(); reload(); });
    controls.querySelector('[data-svc="launch"]').addEventListener('click', (e) => { e.stopPropagation(); launch(); });

    // --- Corner "open externally" hint (always available) ---
    const cornerBtn = document.createElement('button');
    cornerBtn.type = 'button';
    cornerBtn.className = 'svc-corner-launch';
    cornerBtn.setAttribute('aria-label', `Open ${label} in new window`);
    cornerBtn.title = `Open ${label} in new window`;
    cornerBtn.innerHTML = `
        <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
            <path d="M14 4h6v6"></path>
            <path d="M20 4L10 14"></path>
            <path d="M19 13v6a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1h6"></path>
        </svg>
    `;
    cornerBtn.addEventListener('click', (e) => { e.stopPropagation(); launch(); });
    content.appendChild(cornerBtn);
    // Reveal the corner hint after a short delay
    setTimeout(() => cornerBtn.classList.add('visible'), 1500);

    // --- Fallback tile (shown behind iframe so it's only visible if iframe is blocked/empty) ---
    let fallbackEl = null;
    function showFallback(reason) {
        if (fallbackEl) return;
        fallbackEl = document.createElement('div');
        fallbackEl.className = 'svc-fallback';
        fallbackEl.innerHTML = `
            <div class="svc-fallback-icon">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                    <path d="M14 4h6v6"></path>
                    <path d="M20 4L10 14"></path>
                    <path d="M19 13v6a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1h6"></path>
                </svg>
            </div>
            <div class="svc-fallback-title">${label}</div>
            <div class="svc-fallback-sub">
                Can't embed this app in a frame. Open it directly to use it.<br>
                <code>${hint}</code>
            </div>
            <div class="svc-fallback-actions">
                <button class="svc-fallback-btn" data-fb="launch">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                        <path d="M14 4h6v6"></path><path d="M20 4L10 14"></path>
                        <path d="M19 13v6a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1h6"></path>
                    </svg>
                    Launch
                </button>
                <button class="svc-fallback-btn ghost" data-fb="retry">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                        <path d="M21 12a9 9 0 1 1-3-6.7"></path><path d="M21 4v5h-5"></path>
                    </svg>
                    Retry
                </button>
            </div>
        `;
        fallbackEl.querySelector('[data-fb="launch"]').addEventListener('click', launch);
        fallbackEl.querySelector('[data-fb="retry"]').addEventListener('click', reload);
        // Sit behind the iframe so a working iframe covers it
        iframe.style.position = 'relative';
        iframe.style.zIndex = '2';
        content.appendChild(fallbackEl);
    }
    function clearFallback() {
        if (fallbackEl) { fallbackEl.remove(); fallbackEl = null; }
    }

    // Heuristic: if iframe never fires load within 5s OR shortly after firing we
    // can confirm the document is blocked, show the fallback. We can't reliably
    // distinguish a cross-origin SUCCESS from an XFO BLOCK from JS, so we keep
    // the fallback behind the iframe — a working iframe will paint over it.
    let loadFired = false;
    let timeoutId = null;
    function scheduleCheck() {
        loadFired = false;
        clearTimeout(timeoutId);
        // Pre-show the fallback behind the iframe — harmless if the iframe loads
        showFallback('preempt');
        timeoutId = setTimeout(() => {
            if (!loadFired) {
                // Iframe never loaded — definitely show fallback
                showFallback('timeout');
            }
        }, 5000);
    }
    iframe.addEventListener('load', () => {
        loadFired = true;
    });
    iframe.addEventListener('error', () => showFallback('error'));

    scheduleCheck();
}

window.addEventListener('load', () => {
    const padding = 20;
    const windowWidth = window.innerWidth;
    const numWidgets = 9;
    const widgetWidth = (windowWidth - (padding * (numWidgets + 1))) / numWidgets;
    const widgetHeight = widgetWidth;
    let leftPosition = padding;
    
    // Check if we have a saved layout to restore
    const hasSavedLayout = localStorage.getItem('widgetLayout') && localStorage.getItem('widgetLayoutLocked') === 'true';
    
    // Set initial lock state based on saved preference
    if (hasSavedLayout) {
        isLocked = true;
        document.getElementById('padlockBtn').classList.add('locked');
    }
    
    const weatherWidget = document.getElementById('weatherWidget');
    if (!hasSavedLayout) {
        weatherWidget.style.left = leftPosition + "px";
        weatherWidget.style.top = padding + "px";
        weatherWidget.style.width = widgetWidth + "px";
        weatherWidget.style.height = widgetHeight + "px";
    }
    weatherWidget.style.zIndex = ++zIndex;
    enableDrag(weatherWidget, weatherWidget.querySelector('.weather-grab-bar'));
    enableResize(weatherWidget, weatherWidget.querySelector('.weather-resize'));
    fetchWeather();
    setInterval(fetchWeather, 600000);
    leftPosition += widgetWidth + padding;
    
    const forecastWidget = document.getElementById('forecastWidget');
    if (!hasSavedLayout) {
        forecastWidget.style.left = leftPosition + "px";
        forecastWidget.style.top = padding + "px";
        forecastWidget.style.width = widgetWidth + "px";
        forecastWidget.style.height = widgetHeight + "px";
    }
    forecastWidget.style.zIndex = ++zIndex;
    enableDrag(forecastWidget, forecastWidget.querySelector('.forecast-grab-bar'));
    enableResize(forecastWidget, forecastWidget.querySelector('.forecast-resize'));
    fetchForecast();
    setInterval(fetchForecast, 600000);
    leftPosition += widgetWidth + padding;
    
    const radarWin = document.createElement("div");
    radarWin.className = "window no-input-bar";
    radarWin.id = "radarWin";
    radarWin.style.zIndex = ++zIndex;
    radarWin.innerHTML = `
        <div class="grab-bar">
            <span class="widget-name">Radar</span>
        </div>
        <div class="iframe-wrap" style="overflow:hidden;">
            <iframe id="radarIframe" allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera" 
                    credentials="include" 
                    referrerpolicy="no-referrer-when-downgrade"
                    allowfullscreen
                    src="http://localhost:3000"></iframe>
        </div>
        <div class="resize"></div>
    `;
    document.body.appendChild(radarWin);
    
    if (!hasSavedLayout) {
        radarWin.style.left = leftPosition + "px";
        radarWin.style.top = padding + "px";
        radarWin.style.width = widgetWidth + "px";
        radarWin.style.height = widgetHeight + "px";
    }
    
    bringToFront(radarWin);
    enableDrag(radarWin);
    enableResize(radarWin);
    
    leftPosition += widgetWidth + padding;
    
    const camsWidget = document.getElementById('camsWidget');
    if (!hasSavedLayout) {
        camsWidget.style.left = leftPosition + "px";
        camsWidget.style.top = padding + "px";
        camsWidget.style.width = widgetWidth + "px";
        camsWidget.style.height = widgetHeight + "px";
    }
    camsWidget.style.zIndex = ++zIndex;
    enableDrag(camsWidget, camsWidget.querySelector('.cams-grab-bar'));
    enableResize(camsWidget, camsWidget.querySelector('.cams-resize'));
    leftPosition += widgetWidth + padding;
    
    const clockWidget = document.getElementById('clockWidget');
    if (!hasSavedLayout) {
        clockWidget.style.left = leftPosition + "px";
        clockWidget.style.top = padding + "px";
        clockWidget.style.width = widgetWidth + "px";
        clockWidget.style.height = widgetHeight + "px";
    }
    clockWidget.style.zIndex = ++zIndex;
    enableDrag(clockWidget, clockWidget.querySelector('.clock-widget-grab-bar'));
    enableResize(clockWidget, clockWidget.querySelector('.clock-widget-resize'));
    
    let clockFontSizeMultiplier = 1;
    const clockMinusBtn = document.getElementById('clockMinusBtn');
    const clockPlusBtn = document.getElementById('clockPlusBtn');
    const clockWidgetTime = document.getElementById('clockWidgetTime');
    const clockWidgetDate = document.getElementById('clockWidgetDate');
    function updateClockFontSize() {
        clockWidgetTime.style.fontSize = `clamp(36px, ${clockFontSizeMultiplier * 10}vw, ${clockFontSizeMultiplier * 72}px)`;
        clockWidgetDate.style.fontSize = `clamp(12px, ${clockFontSizeMultiplier * 3}vw, ${clockFontSizeMultiplier * 18}px)`;
    }
    if (clockMinusBtn) {
        clockMinusBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            if (clockFontSizeMultiplier > 0.5) {
                clockFontSizeMultiplier -= 0.1;
                updateClockFontSize();
            }
        });
    }
    if (clockPlusBtn) {
        clockPlusBtn.addEventListener('click', (e) => {
            e.stopPropagation();
            if (clockFontSizeMultiplier < 2) {
                clockFontSizeMultiplier += 0.1;
                updateClockFontSize();
            }
        });
    }
    leftPosition += widgetWidth + padding;
    
    const internetSpeedWidget = document.getElementById('internetSpeedWidget');
    if (!hasSavedLayout) {
        internetSpeedWidget.style.left = leftPosition + "px";
        internetSpeedWidget.style.top = padding + "px";
        internetSpeedWidget.style.width = widgetWidth + "px";
        internetSpeedWidget.style.height = widgetHeight + "px";
    }
    internetSpeedWidget.style.zIndex = ++zIndex;
    enableDrag(internetSpeedWidget, internetSpeedWidget.querySelector('.internet-speed-grab-bar'));
    enableResize(internetSpeedWidget, internetSpeedWidget.querySelector('.internet-speed-resize'));
    leftPosition += widgetWidth + padding;
    
    const pupPicsWidget = document.getElementById('pupPicsWidget');
    if (!hasSavedLayout) {
        pupPicsWidget.style.left = leftPosition + "px";
        pupPicsWidget.style.top = padding + "px";
        pupPicsWidget.style.width = widgetWidth + "px";
        pupPicsWidget.style.height = widgetHeight + "px";
    }
    pupPicsWidget.style.zIndex = ++zIndex;
    enableDrag(pupPicsWidget, pupPicsWidget.querySelector('.pup-pics-grab-bar'));
    enableResize(pupPicsWidget, pupPicsWidget.querySelector('.pup-pics-resize'));
    initPupPics();
    leftPosition += widgetWidth + padding;
    
    const lightsWidget = document.getElementById('lightsWidget');
    if (!hasSavedLayout) {
        lightsWidget.style.left = leftPosition + "px";
        lightsWidget.style.top = padding + "px";
        lightsWidget.style.width = widgetWidth + "px";
        lightsWidget.style.height = widgetHeight + "px";
    }
    lightsWidget.style.zIndex = ++zIndex;
    enableDrag(lightsWidget, lightsWidget.querySelector('.lights-grab-bar'));
    enableResize(lightsWidget, lightsWidget.querySelector('.lights-resize'));
    leftPosition += widgetWidth + padding;
    
    // Position Overseerr widget
    const overseerrWidget = document.getElementById('overseerrWidget');
    if (!hasSavedLayout) {
        overseerrWidget.style.left = leftPosition + "px";
        overseerrWidget.style.top = padding + "px";
        overseerrWidget.style.width = widgetWidth + "px";
        overseerrWidget.style.height = widgetHeight + "px";
    }
    overseerrWidget.style.zIndex = ++zIndex;
    enableDrag(overseerrWidget, overseerrWidget.querySelector('.overseerr-grab-bar'));
    enableResize(overseerrWidget, overseerrWidget.querySelector('.overseerr-resize'));
    
    // Now restore saved layout if it exists (after all widgets are created)
    if (hasSavedLayout) {
        loadWidgetLayout();
    }

    // Wire up service widgets — adds reload/launch buttons + fallback tile
    // for iframes that get refused by X-Frame-Options (Overseerr, etc).
    setupServiceWidget('camsWidget',         { label: 'Cams',       url: 'https://cams.add2plex.com',     hint: 'cams.add2plex.com' });
    setupServiceWidget('internetSpeedWidget',{ label: 'Speed Test', url: 'https://speed.add2plex.com/',   hint: 'speed.add2plex.com' });
    setupServiceWidget('lightsWidget',       { label: 'Lights',     url: 'http://192.168.1.168:5000/',    hint: '192.168.1.168:5000' });
    setupServiceWidget('overseerrWidget',    { label: 'Overseerr',  url: 'http://192.168.1.168:5055',     hint: '192.168.1.168:5055' });
    
    const padlockBtn = document.getElementById('padlockBtn');
    padlockBtn.addEventListener('click', () => {
        isLocked = !isLocked;
        padlockBtn.classList.toggle('locked', isLocked);
        padlockBtn.setAttribute('title', isLocked ? 'Layout locked — tap to unlock' : 'Lock layout');
        if (isLocked) {
            saveWidgetLayout();
        } else {
            clearWidgetLayout();
        }
    });
});

function createWindow() {
    const win = document.createElement("div");
    win.className = "window";
    win.style.left = "40px";
    win.style.top = "40px";
    win.style.zIndex = ++zIndex;
    win.innerHTML = `
        <div class="input-bar">
            <button class="close-btn" aria-label="Close window">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                    <path d="M6 6l12 12M18 6L6 18"></path>
                </svg>
            </button>
            <button class="refresh-btn" aria-label="Reload">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                    <path d="M21 12a9 9 0 1 1-3-6.7"></path>
                    <path d="M21 4v5h-5"></path>
                </svg>
            </button>
            <input type="text" placeholder="Enter URL or search term">
            <button class="go-btn">Go</button>
            <button class="new-tab-btn" aria-label="Open in new tab">
                <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                    <path d="M14 4h6v6"></path>
                    <path d="M20 4L10 14"></path>
                    <path d="M19 13v6a1 1 0 0 1-1 1H5a1 1 0 0 1-1-1V6a1 1 0 0 1 1-1h6"></path>
                </svg>
            </button>
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
                <button class="auth-close-btn" aria-label="Close login">
                    <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                        <path d="M6 6l12 12M18 6L6 18"></path>
                    </svg>
                </button>
            </div>
            <iframe allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media; microphone; camera" 
                    credentials="include" 
                    referrerpolicy="no-referrer-when-downgrade"
                    allowfullscreen
                    src=""></iframe>
        </div>
        <div class="auth-overlay">
            <div class="auth-message">Waiting for authentication…</div>
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
    const goButton = win.querySelector(".input-bar .go-btn");
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

function enableDrag(win, dragTarget) {
    if (!dragTarget) {
        const bar = win.querySelector(".input-bar");
        const grabBar = win.querySelector(".grab-bar");
        dragTarget = bar || grabBar || win;
    }
    dragTarget.onpointerdown = e => {
        if (isLocked) return;
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

function enableResize(win, handle) {
    if (!handle) {
        handle = win.querySelector(".resize");
    }
    handle.onpointerdown = e => {
        if (isLocked) return;
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

<div id="touchKbd" aria-hidden="true">
    <div class="kbd-header">
        <span class="kbd-title">Keyboard</span>
        <div class="kbd-handle"></div>
        <button class="kbd-hide" id="kbdHide" aria-label="Hide keyboard">
            <svg viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
                <path d="M6 9l6 6 6-6"></path>
            </svg>
        </button>
    </div>
    <div class="kbd-rows" id="kbdRows"></div>
</div>

<script>
/* ============================================================
   Touch keyboard — auto-pops when an input/textarea is focused.
   Writes via standard input + keydown events so existing logic
   (e.g. Enter-to-navigate on the URL window) keeps working.
   ============================================================ */
(function(){
    const root = document.getElementById('touchKbd');
    const rowsEl = document.getElementById('kbdRows');
    const hideBtn = document.getElementById('kbdHide');
    if (!root || !rowsEl) return;

    let targetEl = null;
    let isShift = false;
    let capsLock = false;
    let layer = 'letters'; // letters | symbols
    let lastShiftTap = 0;
    let suppressHideUntil = 0;

    const LAYOUTS = {
        letters: [
            ['1','2','3','4','5','6','7','8','9','0'],
            ['q','w','e','r','t','y','u','i','o','p'],
            ['a','s','d','f','g','h','j','k','l'],
            ['{shift}','z','x','c','v','b','n','m','{back}'],
            ['{sym}',',','{space}','.','/','{enter}']
        ],
        symbols: [
            ['1','2','3','4','5','6','7','8','9','0'],
            ['!','@','#','$','%','^','&','*','(',')'],
            ['-','_','=','+','[',']','{','}','\\'],
            ['{shift}',';',':','\'','"','<','>','?','{back}'],
            ['{abc}',',','{space}','.','/','{enter}']
        ]
    };

    function isEditable(el) {
        if (!el) return false;
        if (el.tagName === 'TEXTAREA') return true;
        if (el.tagName !== 'INPUT') return false;
        const t = (el.type || 'text').toLowerCase();
        return ['text','search','url','email','tel','password','number'].includes(t);
    }

    function build() {
        rowsEl.innerHTML = '';
        const rows = LAYOUTS[layer];
        rows.forEach(row => {
            const r = document.createElement('div');
            r.className = 'kbd-row';
            row.forEach(k => {
                const btn = document.createElement('button');
                btn.type = 'button';
                btn.className = 'key';
                btn.dataset.key = k;
                let label = k;
                if (k === '{shift}') { btn.classList.add('wide','shift'); label = '⇧'; }
                else if (k === '{back}') { btn.classList.add('wide'); label = '⌫'; }
                else if (k === '{sym}') { btn.classList.add('wide','layer'); label = '?123'; }
                else if (k === '{abc}') { btn.classList.add('wide','layer'); label = 'ABC'; }
                else if (k === '{space}') { btn.classList.add('space'); label = 'space'; }
                else if (k === '{enter}') { btn.classList.add('enter'); label = '⏎ Go'; }
                else if (layer === 'letters' && /[a-z]/.test(k)) {
                    label = (isShift || capsLock) ? k.toUpperCase() : k;
                }
                btn.textContent = label;
                btn.addEventListener('pointerdown', (e) => {
                    e.preventDefault();
                    suppressHideUntil = Date.now() + 200;
                    btn.classList.add('pressed');
                });
                btn.addEventListener('pointerup', (e) => {
                    e.preventDefault();
                    btn.classList.remove('pressed');
                    handleKey(k);
                });
                btn.addEventListener('pointerleave', () => btn.classList.remove('pressed'));
                btn.addEventListener('pointercancel', () => btn.classList.remove('pressed'));
                r.appendChild(btn);
            });
            rowsEl.appendChild(r);
        });
        refreshShiftUI();
    }

    function refreshShiftUI() {
        const shiftBtns = rowsEl.querySelectorAll('.key.shift');
        shiftBtns.forEach(b => b.classList.toggle('active', isShift || capsLock));
        if (layer === 'letters') {
            rowsEl.querySelectorAll('.key').forEach(b => {
                const k = b.dataset.key;
                if (k && k.length === 1 && /[a-z]/.test(k)) {
                    b.textContent = (isShift || capsLock) ? k.toUpperCase() : k;
                }
            });
        }
        rowsEl.querySelectorAll('.key.layer').forEach(b => {
            b.classList.toggle('active', layer === 'symbols');
        });
    }

    function insertText(s) {
        if (!targetEl) return;
        if (typeof targetEl.setRangeText === 'function') {
            const start = targetEl.selectionStart ?? targetEl.value.length;
            const end = targetEl.selectionEnd ?? targetEl.value.length;
            targetEl.setRangeText(s, start, end, 'end');
        } else {
            targetEl.value = (targetEl.value || '') + s;
        }
        targetEl.dispatchEvent(new Event('input', { bubbles: true }));
    }

    function backspace() {
        if (!targetEl) return;
        const start = targetEl.selectionStart ?? targetEl.value.length;
        const end = targetEl.selectionEnd ?? targetEl.value.length;
        if (start !== end) {
            targetEl.setRangeText('', start, end, 'end');
        } else if (start > 0) {
            targetEl.setRangeText('', start - 1, end, 'end');
        }
        targetEl.dispatchEvent(new Event('input', { bubbles: true }));
    }

    function pressEnter() {
        if (!targetEl) return;
        const ev = new KeyboardEvent('keydown', {
            key: 'Enter', code: 'Enter', keyCode: 13, which: 13, bubbles: true, cancelable: true
        });
        targetEl.dispatchEvent(ev);
        try {
            const form = targetEl.form;
            if (form && !ev.defaultPrevented) form.requestSubmit?.();
        } catch(_){}
    }

    function handleKey(k) {
        if (!targetEl) return;
        if (k === '{shift}') {
            const now = Date.now();
            if (now - lastShiftTap < 350) {
                capsLock = !capsLock;
                isShift = false;
            } else {
                isShift = !isShift;
                capsLock = false;
            }
            lastShiftTap = now;
            refreshShiftUI();
            return;
        }
        if (k === '{back}') { backspace(); return; }
        if (k === '{sym}') { layer = 'symbols'; build(); return; }
        if (k === '{abc}') { layer = 'letters'; build(); return; }
        if (k === '{space}') { insertText(' '); return; }
        if (k === '{enter}') { pressEnter(); hide(); return; }

        let ch = k;
        if (layer === 'letters' && /[a-z]/.test(ch) && (isShift || capsLock)) {
            ch = ch.toUpperCase();
        }
        insertText(ch);
        if (isShift && !capsLock) {
            isShift = false;
            refreshShiftUI();
        }
    }

    function show(el) {
        targetEl = el;
        root.classList.add('show');
        root.setAttribute('aria-hidden', 'false');
    }
    function hide() {
        root.classList.remove('show');
        root.setAttribute('aria-hidden', 'true');
        targetEl = null;
        isShift = false;
        capsLock = false;
        layer = 'letters';
        build();
    }

    document.addEventListener('focusin', (e) => {
        const el = e.target;
        if (isEditable(el)) {
            // suppress the native virtual keyboard on touch devices that have one
            try { el.setAttribute('inputmode', 'none'); } catch(_){}
            show(el);
        }
    });

    document.addEventListener('focusout', (e) => {
        // Use a short delay so keypresses on the kbd that re-focus don't immediately hide
        setTimeout(() => {
            if (Date.now() < suppressHideUntil) return;
            const active = document.activeElement;
            if (!isEditable(active)) hide();
        }, 80);
    });

    // Re-show if the user taps a focused input again
    document.addEventListener('pointerdown', (e) => {
        const el = e.target;
        if (isEditable(el)) {
            // ensure we reopen if previously hidden
            if (!root.classList.contains('show')) {
                setTimeout(() => show(el), 0);
            } else {
                targetEl = el;
            }
        }
    });

    hideBtn.addEventListener('click', (e) => {
        e.preventDefault();
        e.stopPropagation();
        hide();
    });

    // Drag the keyboard by its header
    (function enableKbdDrag(){
        const header = root.querySelector('.kbd-header');
        let sx = 0, sy = 0, sl = 0, st = 0, dragging = false;
        header.addEventListener('pointerdown', (e) => {
            if (e.target.closest('#kbdHide')) return;
            dragging = true;
            header.setPointerCapture(e.pointerId);
            const rect = root.getBoundingClientRect();
            sx = e.clientX; sy = e.clientY;
            sl = rect.left; st = rect.top;
            root.style.transition = 'none';
            root.style.left = sl + 'px';
            root.style.top = st + 'px';
            root.style.bottom = 'auto';
            root.style.transform = 'none';
        });
        header.addEventListener('pointermove', (e) => {
            if (!dragging) return;
            const nl = sl + (e.clientX - sx);
            const nt = st + (e.clientY - sy);
            root.style.left = Math.max(8, Math.min(window.innerWidth - root.offsetWidth - 8, nl)) + 'px';
            root.style.top  = Math.max(8, Math.min(window.innerHeight - root.offsetHeight - 8, nt)) + 'px';
        });
        const stop = () => { dragging = false; root.style.transition = ''; };
        header.addEventListener('pointerup', stop);
        header.addEventListener('pointercancel', stop);
    })();

    // initial build
    build();
})();
</script>

</body>
</html>
