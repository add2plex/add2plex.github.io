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
    overflow: hidden;
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
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
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
    border-radius: 0 0 12px 0;
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
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
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

.widget-name {
    font-size: 11px;
    color: #8fb4ff;
    font-weight: 600;
    opacity: 0.8;
    letter-spacing: 0.5px;
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
    width: 307.2px;
    height: 98.304px;
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
    font-size: 0.512;
}

.forecast-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
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
    padding: 5.12px;
    display: flex;
    gap: 3.84px;
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
    border-radius: 5.12px;
    border: 1px solid #2d3c66;
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
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
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

/* Padlock Icon */
.padlock-btn {
    position: fixed;
    bottom: 20px;
    left: 20px;
    background: none;
    border: none;
    font-size: 22.4px;
    cursor: pointer;
    z-index: 999;
    opacity: 0.5;
    transition: opacity 0.2s;
    filter: grayscale(1) brightness(0.7);
}

.padlock-btn:hover {
    opacity: 0.8;
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

/* Clock Widget */
.clock-widget {
    position: absolute;
    width: 300px;
    height: 200px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
}

.clock-widget-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
}

.clock-widget-grab-bar:active {
    cursor: grabbing;
}

.clock-widget-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.clock-widget-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;
}

.clock-widget-time {
    font-size: clamp(36px, 10vw, 72px);
    font-weight: bold;
    color: #ffffff;
    font-family: 'Segoe UI', 'Roboto', 'Helvetica Neue', sans-serif;
    line-height: 1;
}

.clock-widget-date {
    font-size: clamp(12px, 3vw, 18px);
    color: #8fb4ff;
    opacity: 0.9;
    text-align: center;
    font-weight: 500;
    line-height: 1.2;
}

.clock-widget-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
}

/* Internet Speed Widget */
.internet-speed-widget {
    position: absolute;
    width: 300px;
    height: 200px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
}

.internet-speed-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
}

.internet-speed-grab-bar:active {
    cursor: grabbing;
}

.internet-speed-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.internet-speed-content {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
}

.internet-speed-content iframe {
    width: 100%;
    height: 100%;
    border: none;
    zoom: 0.5;
}

.internet-speed-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
    border-radius: 0 0 12px 0;
}

/* Pup Pics Widget */
.pup-pics-widget {
    position: absolute;
    width: 300px;
    height: 200px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
}

.pup-pics-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
}

.pup-pics-grab-bar:active {
    cursor: grabbing;
}

.pup-pics-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.pup-pics-content {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background: #0f1320;
}

.pup-pics-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
    border-radius: 0 0 12px 0;
}

/* Lights Widget */
.lights-widget {
    position: absolute;
    width: 300px;
    height: 200px;
    background: #1a1f2e;
    border-radius: 12px;
    border: 1px solid #2d3c66;
    display: flex;
    flex-direction: column;
    box-shadow: 0 20px 40px rgba(0,0,0,0.8);
    touch-action: none;
    overflow: hidden;
}

.lights-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
}

.lights-grab-bar:active {
    cursor: grabbing;
}

.lights-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.lights-content {
    flex: 1;
    display: flex;
    align-items: center;
    justify-content: center;
    overflow: hidden;
    background: #0f1320;
}

.lights-content iframe {
    width: 100%;
    height: 100%;
    border: none;
}

.lights-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
    border-radius: 0 0 12px 0;
}

/* Overseerr Widget */
.overseerr-widget {
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

.overseerr-grab-bar {
    height: 24px;
    background: #0f1320;
    border-bottom: 1px solid #2d3c66;
    cursor: grab;
    display: flex;
    align-items: center;
    justify-content: space-between;
    flex-shrink: 0;
    padding: 0 8px;
}

.overseerr-grab-bar:active {
    cursor: grabbing;
}

.overseerr-grab-bar::before {
    content: '⋮⋮';
    color: #8fb4ff;
    font-size: 14px;
    letter-spacing: 2px;
    opacity: 0.5;
}

.overseerr-content {
    flex: 1;
    display: flex;
    flex-direction: column;
    overflow: hidden;
    background: #0a0f1a;
}

.overseerr-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
    border-radius: 0 0 12px 0;
}

.search-resize {
    position: absolute;
    width: 25px;
    height: 25px;
    right: 0;
    bottom: 0;
    background: linear-gradient(135deg, transparent 50%, #8fb4ff 50%);
    cursor: nwse-resize;
    touch-action: none;
    border-radius: 0 0 12px 0;
}

.clock-size-controls {
    display: flex;
    gap: 4px;
    align-items: center;
    flex-shrink: 0;
}

.clock-size-btn {
    width: 18px;
    height: 18px;
    border: none;
    border-radius: 3px;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 12px;
    font-weight: bold;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    transition: background 0.2s;
}

.clock-size-btn:hover {
    background: #3d4c76;
}

.size-controls {
    display: flex;
    gap: 4px;
    align-items: center;
    flex-shrink: 0;
}

.size-btn {
    width: 18px;
    height: 18px;
    border: none;
    border-radius: 3px;
    background: #2d3c66;
    color: #8fb4ff;
    font-size: 12px;
    font-weight: bold;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 0;
    transition: background 0.2s;
}

.size-btn:hover {
    background: #3d4c76;
}

.cursor-circle {
    position: fixed;
    border: 2px solid #8fb4ff;
    border-radius: 50%;
    pointer-events: none;
    z-index: 1001;
    display: none;
    opacity: 0.7;
}

.scratchpad-brush-preview {
    width: 40px;
    height: 40px;
    border: 1px solid #2d3c66;
    border-radius: 4px;
    background: #0f1320;
    display: flex;
    align-items: center;
    justify-content: center;
    flex-shrink: 0;
}
</style>
</head>
<body>

<button class="padlock-btn" id="padlockBtn">🔓</button>

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

<div class="scratchpad-widget" id="scratchpadWidget">
    <div class="scratchpad-grab-bar">
        <span class="widget-name">Draw</span>
    </div>
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
        <div class="scratchpad-brush-preview" id="brushPreview"></div>
        <button class="scratchpad-btn" id="eraserBtn">✏️ Eraser</button>
        <button class="scratchpad-btn" id="clearBtn">Clear</button>
    </div>
    <div class="scratchpad-canvas-wrap">
        <canvas id="scratchpadCanvas"></canvas>
    </div>
    <div class="scratchpad-resize"></div>
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
        <img id="pupPicsImage" src="" alt="Cute Dog Picture" style="width: 100%; height: 100%; object-fit: cover;">
    </div>
    <div class="pup-pics-resize"></div>
</div>

<div class="lights-widget" id="lightsWidget">
    <div class="lights-grab-bar">
        <span class="widget-name">Lights</span>
    </div>
    <div class="lights-content">
        <iframe src="http://192.168.1.168:5000/" allow="autoplay; fullscreen; picture-in-picture; popups; same-origin; scripts; forms; encrypted-media" credentials="include" referrerpolicy="no-referrer-when-downgrade" allowfullscreen></iframe>
    </div>
    <div class="lights-resize"></div>
</div>

<div class="overseerr-widget" id="overseerrWidget">
    <div class="overseerr-grab-bar">
        <span class="widget-name">Overseerr</span>
    </div>
    <div class="overseerr-content" id="overseerrContent">
        <!-- Overseerr app renders here -->
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
let scratchpadResizeObserver = null;
let nextPupPicsUrl = null;
let isLoadingNextImage = false;
let preloadRetryId = null;

function initPupPics() {
    loadNextPupPic();
    const pupPicsWidget = document.getElementById('pupPicsWidget');
    pupPicsObserver = new ResizeObserver(() => {
        loadNextPupPic();
    });
    pupPicsObserver.observe(pupPicsWidget);
}

function getAspectRatio() {
    const widget = document.getElementById('pupPicsWidget');
    const width = widget.offsetWidth;
    const height = widget.offsetHeight - 24;
    return width / height;
}

function preloadNextImage() {
    if (isLoadingNextImage) return;
    isLoadingNextImage = true;
    fetch('https://random.dog/woof.json')
        .then(response => response.json())
        .then(data => {
            if (data && data.url) {
                const imageUrl = data.url;
                if (imageUrl.toLowerCase().endsWith('.mp4') || imageUrl.toLowerCase().endsWith('.webm')) {
                    isLoadingNextImage = false;
                    preloadRetryId = setTimeout(preloadNextImage, 200);
                    return;
                }
                nextPupPicsUrl = imageUrl;
                isLoadingNextImage = false;
            } else {
                isLoadingNextImage = false;
            }
        })
        .catch(error => {
            console.error('Error preloading dog pic:', error);
            isLoadingNextImage = false;
        });
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

function loadNextPupPic() {
    if (pupPicsIntervalId) {
        clearTimeout(pupPicsIntervalId);
    }
    if (preloadRetryId) {
        clearTimeout(preloadRetryId);
        preloadRetryId = null;
    }
    fetch('https://random.dog/woof.json')
        .then(response => response.json())
        .then(data => {
            if (data && data.url) {
                const imageUrl = data.url;
                if (imageUrl.toLowerCase().endsWith('.mp4') || imageUrl.toLowerCase().endsWith('.webm')) {
                    pupPicsIntervalId = setTimeout(loadNextPupPic, 300);
                    return;
                }
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
            }
        })
        .catch(error => {
            console.error('Error loading dog pic:', error);
            pupPicsIntervalId = setTimeout(loadNextPupPic, 2000);
        });
}

function saveWidgetLayout() {
    const layout = {};
    const widgets = [
        { id: 'weatherWidget', type: 'standard' },
        { id: 'forecastWidget', type: 'standard' },
        { id: 'radarWin', type: 'window' },
        { id: 'scratchpadWidget', type: 'standard' },
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
                height: el.style.height
            };
        }
    });
    const expiryDate = new Date();
    expiryDate.setFullYear(expiryDate.getFullYear() + 1);
    document.cookie = `widgetLayout=${encodeURIComponent(JSON.stringify(layout))}; expires=${expiryDate.toUTCString()}; path=/`;
}

function loadWidgetLayout() {
    const cookieValue = document.cookie.split('; ').find(row => row.startsWith('widgetLayout='));
    if (!cookieValue) return;
    try {
        const layout = JSON.parse(decodeURIComponent(cookieValue.split('=')[1]));
        Object.keys(layout).forEach(widgetId => {
            const el = document.getElementById(widgetId);
            if (el && layout[widgetId]) {
                el.style.left = layout[widgetId].left;
                el.style.top = layout[widgetId].top;
                el.style.width = layout[widgetId].width;
                el.style.height = layout[widgetId].height;
            }
        });
    } catch (error) {
        console.error('Error loading widget layout:', error);
    }
}

function clearWidgetLayout() {
    document.cookie = 'widgetLayout=; expires=Thu, 01 Jan 1970 00:00:00 UTC; path=/';
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

window.addEventListener('load', () => {
    loadWidgetLayout();
    const padding = 20;
    const windowWidth = window.innerWidth;
    const numWidgets = 9;
    const widgetWidth = (windowWidth - (padding * (numWidgets + 1))) / numWidgets;
    const widgetHeight = widgetWidth;
    let leftPosition = padding;
    
    const weatherWidget = document.getElementById('weatherWidget');
    weatherWidget.style.left = leftPosition + "px";
    weatherWidget.style.top = padding + "px";
    weatherWidget.style.width = widgetWidth + "px";
    weatherWidget.style.height = widgetHeight + "px";
    weatherWidget.style.zIndex = ++zIndex;
    enableDrag(weatherWidget, weatherWidget.querySelector('.weather-grab-bar'));
    enableResize(weatherWidget, weatherWidget.querySelector('.weather-resize'));
    fetchWeather();
    setInterval(fetchWeather, 600000);
    leftPosition += widgetWidth + padding;
    
    const forecastWidget = document.getElementById('forecastWidget');
    forecastWidget.style.left = leftPosition + "px";
    forecastWidget.style.top = padding + "px";
    forecastWidget.style.width = widgetWidth + "px";
    forecastWidget.style.height = widgetHeight + "px";
    forecastWidget.style.zIndex = ++zIndex;
    enableDrag(forecastWidget, forecastWidget.querySelector('.forecast-grab-bar'));
    enableResize(forecastWidget, forecastWidget.querySelector('.forecast-resize'));
    fetchForecast();
    setInterval(fetchForecast, 600000);
    leftPosition += widgetWidth + padding;
    
    const radarWin = document.createElement("div");
    radarWin.className = "window no-input-bar";
    radarWin.id = "radarWin";
    radarWin.style.left = leftPosition + "px";
    radarWin.style.top = padding + "px";
    radarWin.style.width = widgetWidth + "px";
    radarWin.style.height = widgetHeight + "px";
    radarWin.style.zIndex = ++zIndex;
    radarWin.innerHTML = `
        <div class="grab-bar">
            <span class="widget-name">Radar</span>
        </div>
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
    leftPosition += widgetWidth + padding;
    
    const scratchpadWidget = document.getElementById('scratchpadWidget');
    scratchpadWidget.style.left = leftPosition + "px";
    scratchpadWidget.style.top = padding + "px";
    scratchpadWidget.style.width = widgetWidth + "px";
    scratchpadWidget.style.height = widgetHeight + "px";
    scratchpadWidget.style.zIndex = ++zIndex;
    initScratchpad();
    leftPosition += widgetWidth + padding;
    
    const clockWidget = document.getElementById('clockWidget');
    clockWidget.style.left = leftPosition + "px";
    clockWidget.style.top = padding + "px";
    clockWidget.style.width = widgetWidth + "px";
    clockWidget.style.height = widgetHeight + "px";
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
    internetSpeedWidget.style.left = leftPosition + "px";
    internetSpeedWidget.style.top = padding + "px";
    internetSpeedWidget.style.width = widgetWidth + "px";
    internetSpeedWidget.style.height = widgetHeight + "px";
    internetSpeedWidget.style.zIndex = ++zIndex;
    enableDrag(internetSpeedWidget, internetSpeedWidget.querySelector('.internet-speed-grab-bar'));
    enableResize(internetSpeedWidget, internetSpeedWidget.querySelector('.internet-speed-resize'));
    leftPosition += widgetWidth + padding;
    
    const pupPicsWidget = document.getElementById('pupPicsWidget');
    pupPicsWidget.style.left = leftPosition + "px";
    pupPicsWidget.style.top = padding + "px";
    pupPicsWidget.style.width = widgetWidth + "px";
    pupPicsWidget.style.height = widgetHeight + "px";
    pupPicsWidget.style.zIndex = ++zIndex;
    enableDrag(pupPicsWidget, pupPicsWidget.querySelector('.pup-pics-grab-bar'));
    enableResize(pupPicsWidget, pupPicsWidget.querySelector('.pup-pics-resize'));
    initPupPics();
    leftPosition += widgetWidth + padding;
    
    const lightsWidget = document.getElementById('lightsWidget');
    lightsWidget.style.left = leftPosition + "px";
    lightsWidget.style.top = padding + "px";
    lightsWidget.style.width = widgetWidth + "px";
    lightsWidget.style.height = widgetHeight + "px";
    lightsWidget.style.zIndex = ++zIndex;
    enableDrag(lightsWidget, lightsWidget.querySelector('.lights-grab-bar'));
    enableResize(lightsWidget, lightsWidget.querySelector('.lights-resize'));
    leftPosition += widgetWidth + padding;
    
    // Position Overseerr widget
    const overseerrWidget = document.getElementById('overseerrWidget');
    overseerrWidget.style.left = leftPosition + "px";
    overseerrWidget.style.top = padding + "px";
    overseerrWidget.style.width = widgetWidth + "px";
    overseerrWidget.style.height = widgetHeight + "px";
    overseerrWidget.style.zIndex = ++zIndex;
    enableDrag(overseerrWidget, overseerrWidget.querySelector('.overseerr-grab-bar'));
    enableResize(overseerrWidget, overseerrWidget.querySelector('.overseerr-resize'));
    initOverseerr();
    
    const padlockBtn = document.getElementById('padlockBtn');
    padlockBtn.addEventListener('click', () => {
        isLocked = !isLocked;
        padlockBtn.textContent = isLocked ? '🔒' : '🔓';
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

function initScratchpad() {
    const scratchpadWidget = document.getElementById('scratchpadWidget');
    const canvas = document.getElementById('scratchpadCanvas');
    const ctx = canvas.getContext('2d');
    const gradientBar = document.getElementById('gradientBar');
    const colorPreview = document.getElementById('colorPreview');
    const blackBtn = document.getElementById('blackBtn');
    const whiteBtn = document.getElementById('whiteBtn');
    const thicknessSlider = document.getElementById('thicknessSlider');
    const eraserBtn = document.getElementById('eraserBtn');
    const clearBtn = document.getElementById('clearBtn');
    const brushPreview = document.getElementById('brushPreview');
    
    let isDrawing = false;
    let isErasing = false;
    let currentColor = '#ff0000';
    let currentThickness = 3;
    
    function updateBrushPreview() {
        brushPreview.innerHTML = '';
        const previewCircle = document.createElement('div');
        previewCircle.style.width = Math.min(currentThickness, 30) + 'px';
        previewCircle.style.height = Math.min(currentThickness, 30) + 'px';
        previewCircle.style.borderRadius = '50%';
        if (isErasing) {
            previewCircle.style.border = '2px solid #8fb4ff';
            previewCircle.style.backgroundColor = 'transparent';
        } else {
            previewCircle.style.backgroundColor = currentColor;
        }
        brushPreview.appendChild(previewCircle);
    }
    
    function setColor(color) {
        currentColor = color;
        colorPreview.style.background = color;
        isErasing = false;
        eraserBtn.style.opacity = '0.7';
        blackBtn.classList.remove('active');
        whiteBtn.classList.remove('active');
        if (color === '#000000') {
            blackBtn.classList.add('active');
        } else if (color === '#ffffff') {
            whiteBtn.classList.add('active');
        }
        updateBrushPreview();
    }
    
    function resizeCanvas() {
        const wrap = scratchpadWidget.querySelector('.scratchpad-canvas-wrap');
        canvas.width = wrap.clientWidth;
        canvas.height = wrap.clientHeight;
        ctx.fillStyle = '#3a4a7a';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
    }
    
    resizeCanvas();
    window.addEventListener('resize', resizeCanvas);
    
    if (scratchpadResizeObserver) {
        scratchpadResizeObserver.disconnect();
    }
    scratchpadResizeObserver = new ResizeObserver(() => {
        resizeCanvas();
    });
    scratchpadResizeObserver.observe(scratchpadWidget.querySelector('.scratchpad-canvas-wrap'));
    
    gradientBar.addEventListener('click', (e) => {
        const rect = gradientBar.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const width = rect.width;
        const tempCanvas = document.createElement('canvas');
        tempCanvas.width = width;
        tempCanvas.height = 1;
        const tempCtx = tempCanvas.getContext('2d');
        const gradient = tempCtx.createLinearGradient(0, 0, width, 0);
        gradient.addColorStop(0, '#ff0000');
        gradient.addColorStop(0.17, '#ffff00');
        gradient.addColorStop(0.33, '#00ff00');
        gradient.addColorStop(0.5, '#00ffff');
        gradient.addColorStop(0.67, '#0000ff');
        gradient.addColorStop(0.83, '#ff00ff');
        gradient.addColorStop(1, '#ff0000');
        tempCtx.fillStyle = gradient;
        tempCtx.fillRect(0, 0, width, 1);
        const imageData = tempCtx.getImageData(Math.floor(x), 0, 1, 1);
        const data = imageData.data;
        const color = `rgb(${data[0]}, ${data[1]}, ${data[2]})`;
        setColor(color);
    });
    
    blackBtn.addEventListener('click', () => { setColor('#000000'); });
    whiteBtn.addEventListener('click', () => { setColor('#ffffff'); });
    
    thicknessSlider.addEventListener('input', (e) => {
        currentThickness = e.target.value;
        updateBrushPreview();
    });
    
    eraserBtn.addEventListener('click', () => {
        isErasing = !isErasing;
        eraserBtn.style.opacity = isErasing ? '1' : '0.7';
        if (!isErasing) {
            colorPreview.style.background = currentColor;
        } else {
            colorPreview.style.background = '#2a3050';
        }
        blackBtn.classList.remove('active');
        whiteBtn.classList.remove('active');
        updateBrushPreview();
    });
    
    clearBtn.addEventListener('click', () => {
        ctx.fillStyle = '#3a4a7a';
        ctx.fillRect(0, 0, canvas.width, canvas.height);
    });
    
    function startDrawing(e) {
        isDrawing = true;
        const rect = canvas.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const cursorCircle = document.getElementById('cursorCircle');
        cursorCircle.style.display = 'block';
        cursorCircle.style.left = (e.clientX - currentThickness / 2) + 'px';
        cursorCircle.style.top = (e.clientY - currentThickness / 2) + 'px';
        cursorCircle.style.width = currentThickness + 'px';
        cursorCircle.style.height = currentThickness + 'px';
        ctx.beginPath();
        ctx.moveTo(x, y);
    }
    
    function draw(e) {
        if (!isDrawing) return;
        const rect = canvas.getBoundingClientRect();
        const x = e.clientX - rect.left;
        const y = e.clientY - rect.top;
        const cursorCircle = document.getElementById('cursorCircle');
        cursorCircle.style.left = (e.clientX - currentThickness / 2) + 'px';
        cursorCircle.style.top = (e.clientY - currentThickness / 2) + 'px';
        cursorCircle.style.width = currentThickness + 'px';
        cursorCircle.style.height = currentThickness + 'px';
        ctx.lineWidth = currentThickness;
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        if (isErasing) {
            ctx.clearRect(x - currentThickness / 2, y - currentThickness / 2, currentThickness, currentThickness);
        } else {
            ctx.strokeStyle = currentColor;
            ctx.lineTo(x, y);
            ctx.stroke();
        }
    }
    
    function stopDrawing() {
        isDrawing = false;
        ctx.closePath();
        const cursorCircle = document.getElementById('cursorCircle');
        cursorCircle.style.display = 'none';
    }
    
    function getTouchPos(touch) {
        const rect = canvas.getBoundingClientRect();
        return { x: touch.clientX - rect.left, y: touch.clientY - rect.top };
    }
    
    function startTouchDrawing(e) {
        e.preventDefault();
        const touch = e.touches[0];
        isDrawing = true;
        const pos = getTouchPos(touch);
        const cursorCircle = document.getElementById('cursorCircle');
        cursorCircle.style.display = 'block';
        cursorCircle.style.left = (touch.clientX - currentThickness / 2) + 'px';
        cursorCircle.style.top = (touch.clientY - currentThickness / 2) + 'px';
        cursorCircle.style.width = currentThickness + 'px';
        cursorCircle.style.height = currentThickness + 'px';
        ctx.beginPath();
        ctx.moveTo(pos.x, pos.y);
    }
    
    function touchDraw(e) {
        e.preventDefault();
        if (!isDrawing) return;
        const touch = e.touches[0];
        const pos = getTouchPos(touch);
        const cursorCircle = document.getElementById('cursorCircle');
        cursorCircle.style.left = (touch.clientX - currentThickness / 2) + 'px';
        cursorCircle.style.top = (touch.clientY - currentThickness / 2) + 'px';
        cursorCircle.style.width = currentThickness + 'px';
        cursorCircle.style.height = currentThickness + 'px';
        ctx.lineWidth = currentThickness;
        ctx.lineCap = 'round';
        ctx.lineJoin = 'round';
        if (isErasing) {
            ctx.clearRect(pos.x - currentThickness / 2, pos.y - currentThickness / 2, currentThickness, currentThickness);
        } else {
            ctx.strokeStyle = currentColor;
            ctx.lineTo(pos.x, pos.y);
            ctx.stroke();
        }
    }
    
    function stopTouchDrawing(e) {
        e.preventDefault();
        isDrawing = false;
        ctx.closePath();
        const cursorCircle = document.getElementById('cursorCircle');
        cursorCircle.style.display = 'none';
    }
    
    canvas.addEventListener('mousedown', startDrawing);
    canvas.addEventListener('mousemove', draw);
    canvas.addEventListener('mouseup', stopDrawing);
    canvas.addEventListener('mouseout', stopDrawing);
    canvas.addEventListener('touchstart', startTouchDrawing);
    canvas.addEventListener('touchmove', touchDraw);
    canvas.addEventListener('touchend', stopTouchDrawing);
    
    enableDrag(scratchpadWidget, scratchpadWidget.querySelector('.scratchpad-grab-bar'));
    enableResize(scratchpadWidget, scratchpadWidget.querySelector('.scratchpad-resize'));
    updateBrushPreview();
}

// Overseerr Widget
function initOverseerr() {
    const container = document.getElementById('overseerrContent');
    
    // State
    let connected = false;
    let config = JSON.parse(localStorage.getItem('overseerrConfig') || '{"serverUrl":"","apiKey":""}');
    let api = null;
    let currentUser = null;
    let activeTab = 'discover';
    let trending = [];
    let requests = [];
    let searchResults = [];
    let selectedMedia = null;
    
    // API Client
    const createApiClient = (baseUrl, apiKey) => {
        const cleanUrl = baseUrl?.replace(/\/$/, '') || '';
        
        const fetchApi = async (endpoint, options = {}) => {
            const response = await fetch(`${cleanUrl}/api/v1${endpoint}`, {
                ...options,
                headers: {
                    'X-Api-Key': apiKey,
                    'Content-Type': 'application/json',
                    ...options.headers,
                },
            });
            if (!response.ok) throw new Error(`API Error: ${response.status}`);
            return response.json();
        };
        
        return {
            getStatus: () => fetchApi('/status'),
            getCurrentUser: () => fetchApi('/auth/me'),
            getTrending: (page = 1) => fetchApi(`/discover/trending?page=${page}`),
            search: (query, page = 1) => fetchApi(`/search?query=${encodeURIComponent(query)}&page=${page}`),
            getMovie: (id) => fetchApi(`/movie/${id}`),
            getTv: (id) => fetchApi(`/tv/${id}`),
            getRequests: (page = 1) => fetchApi(`/request?take=10&skip=${(page - 1) * 10}&sort=added`),
            createRequest: (mediaType, mediaId, seasons) => fetchApi('/request', {
                method: 'POST',
                body: JSON.stringify({ mediaType, mediaId, seasons }),
            }),
        };
    };
    
    // Render functions
    function render() {
        if (!connected) {
            renderConnectionScreen();
        } else {
            renderMainApp();
        }
    }
    
    function renderConnectionScreen() {
        container.innerHTML = `
            <div style="display:flex;flex-direction:column;align-items:center;justify-content:center;height:100%;padding:16px;background:linear-gradient(to bottom right,#030712,#1e1b4b);">
                <div style="width:48px;height:48px;border-radius:12px;background:linear-gradient(to bottom right,#6366f1,#9333ea);display:flex;align-items:center;justify-content:center;margin-bottom:12px;">
                    <svg width="24" height="24" fill="none" stroke="white" stroke-width="2" viewBox="0 0 24 24"><path d="M7 4v16M17 4v16M3 8h4m10 0h4M3 12h18M3 16h4m10 0h4M4 20h16a1 1 0 001-1V5a1 1 0 00-1-1H4a1 1 0 00-1 1v14a1 1 0 001 1z"/></svg>
                </div>
                <h2 style="color:white;font-size:16px;font-weight:bold;margin-bottom:4px;">Overseerr</h2>
                <p style="color:#9ca3af;font-size:11px;margin-bottom:16px;">Connect to your server</p>
                <input type="url" id="overseerrUrl" placeholder="https://overseerr.example.com" value="${config.serverUrl}" style="width:100%;padding:8px 12px;margin-bottom:8px;border-radius:8px;border:1px solid #374151;background:#1f2937;color:white;font-size:12px;outline:none;">
                <input type="password" id="overseerrKey" placeholder="API Key" value="${config.apiKey}" style="width:100%;padding:8px 12px;margin-bottom:12px;border-radius:8px;border:1px solid #374151;background:#1f2937;color:white;font-size:12px;outline:none;">
                <button id="overseerrConnect" style="width:100%;padding:8px 12px;border-radius:8px;border:none;background:linear-gradient(to right,#6366f1,#9333ea);color:white;font-size:12px;font-weight:500;cursor:pointer;">Connect</button>
                <p id="overseerrError" style="color:#f87171;font-size:11px;margin-top:8px;display:none;"></p>
            </div>
        `;
        
        document.getElementById('overseerrConnect').onclick = handleConnect;
        document.getElementById('overseerrUrl').onkeydown = (e) => e.key === 'Enter' && handleConnect();
        document.getElementById('overseerrKey').onkeydown = (e) => e.key === 'Enter' && handleConnect();
    }
    
    async function handleConnect() {
        const serverUrl = document.getElementById('overseerrUrl').value.trim();
        const apiKey = document.getElementById('overseerrKey').value.trim();
        const errorEl = document.getElementById('overseerrError');
        
        if (!serverUrl || !apiKey) {
            errorEl.textContent = 'Please enter both URL and API key';
            errorEl.style.display = 'block';
            return;
        }
        
        try {
            api = createApiClient(serverUrl, apiKey);
            await api.getStatus();
            currentUser = await api.getCurrentUser();
            config = { serverUrl, apiKey };
            localStorage.setItem('overseerrConfig', JSON.stringify(config));
            connected = true;
            render();
            loadData();
        } catch (err) {
            errorEl.textContent = 'Connection failed. Check URL and API key.';
            errorEl.style.display = 'block';
        }
    }
    
    async function loadData() {
        try {
            const trendingData = await api.getTrending();
            trending = trendingData.results || [];
            const requestsData = await api.getRequests();
            requests = requestsData.results || [];
            renderContent();
        } catch (err) {
            console.error('Failed to load data:', err);
        }
    }
    
    function renderMainApp() {
        container.innerHTML = `
            <div style="display:flex;flex-direction:column;height:100%;background:#030712;">
                <div style="display:flex;border-bottom:1px solid #1f2937;background:#0f172a;">
                    <button class="overseerr-tab ${activeTab === 'discover' ? 'active' : ''}" data-tab="discover" style="flex:1;padding:8px;border:none;background:${activeTab === 'discover' ? '#6366f1' : 'transparent'};color:${activeTab === 'discover' ? 'white' : '#9ca3af'};font-size:11px;cursor:pointer;">Discover</button>
                    <button class="overseerr-tab ${activeTab === 'requests' ? 'active' : ''}" data-tab="requests" style="flex:1;padding:8px;border:none;background:${activeTab === 'requests' ? '#6366f1' : 'transparent'};color:${activeTab === 'requests' ? 'white' : '#9ca3af'};font-size:11px;cursor:pointer;">Requests</button>
                    <button class="overseerr-tab ${activeTab === 'search' ? 'active' : ''}" data-tab="search" style="flex:1;padding:8px;border:none;background:${activeTab === 'search' ? '#6366f1' : 'transparent'};color:${activeTab === 'search' ? 'white' : '#9ca3af'};font-size:11px;cursor:pointer;">Search</button>
                </div>
                <div style="padding:8px;border-bottom:1px solid #1f2937;display:flex;gap:8px;">
                    <input type="text" id="overseerrSearch" placeholder="Search..." style="flex:1;padding:6px 10px;border-radius:6px;border:1px solid #374151;background:#1f2937;color:white;font-size:11px;outline:none;">
                    <button id="overseerrDisconnect" style="padding:6px 10px;border-radius:6px;border:none;background:#dc2626;color:white;font-size:10px;cursor:pointer;">✕</button>
                </div>
                <div id="overseerrContentArea" style="flex:1;overflow-y:auto;padding:8px;"></div>
            </div>
        `;
        
        document.querySelectorAll('.overseerr-tab').forEach(btn => {
            btn.onclick = () => {
                activeTab = btn.dataset.tab;
                renderMainApp();
                renderContent();
            };
        });
        
        document.getElementById('overseerrSearch').onkeydown = async (e) => {
            if (e.key === 'Enter') {
                const query = e.target.value.trim();
                if (query) {
                    activeTab = 'search';
                    try {
                        const data = await api.search(query);
                        searchResults = data.results || [];
                    } catch (err) {
                        searchResults = [];
                    }
                    renderMainApp();
                    renderContent();
                }
            }
        };
        
        document.getElementById('overseerrDisconnect').onclick = () => {
            connected = false;
            localStorage.removeItem('overseerrConfig');
            render();
        };
        
        renderContent();
    }
    
    function renderContent() {
        const area = document.getElementById('overseerrContentArea');
        if (!area) return;
        
        if (activeTab === 'discover') {
            area.innerHTML = `
                <h3 style="color:white;font-size:12px;font-weight:bold;margin-bottom:8px;">🔥 Trending</h3>
                <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(80px,1fr));gap:8px;">
                    ${trending.slice(0, 12).map(item => renderMediaCard(item)).join('')}
                </div>
            `;
        } else if (activeTab === 'requests') {
            area.innerHTML = `
                <h3 style="color:white;font-size:12px;font-weight:bold;margin-bottom:8px;">📋 Recent Requests</h3>
                <div style="display:flex;flex-direction:column;gap:8px;">
                    ${requests.length > 0 ? requests.slice(0, 10).map(req => renderRequestCard(req)).join('') : '<p style="color:#9ca3af;font-size:11px;">No requests</p>'}
                </div>
            `;
        } else if (activeTab === 'search') {
            area.innerHTML = `
                <h3 style="color:white;font-size:12px;font-weight:bold;margin-bottom:8px;">🔍 Search Results</h3>
                <div style="display:grid;grid-template-columns:repeat(auto-fill,minmax(80px,1fr));gap:8px;">
                    ${searchResults.length > 0 ? searchResults.slice(0, 12).map(item => renderMediaCard(item)).join('') : '<p style="color:#9ca3af;font-size:11px;">Search for movies or TV shows</p>'}
                </div>
            `;
        }
        
        // Add click handlers for media cards
        document.querySelectorAll('.overseerr-media-card').forEach(card => {
            card.onclick = () => showMediaDetail(JSON.parse(card.dataset.item));
        });
    }
    
    function renderMediaCard(item) {
        const title = item.title || item.name || 'Unknown';
        const poster = item.posterPath ? `https://image.tmdb.org/t/p/w200${item.posterPath}` : '';
        const type = item.mediaType === 'tv' ? 'TV' : 'Movie';
        const status = item.mediaInfo?.status;
        const statusBadge = status === 5 ? '✓' : status === 2 ? '⏳' : '';
        
        return `
            <div class="overseerr-media-card" data-item='${JSON.stringify(item).replace(/'/g, "\\'")}' style="cursor:pointer;border-radius:8px;overflow:hidden;background:#1f2937;transition:transform 0.2s;">
                <div style="position:relative;aspect-ratio:2/3;background:#374151;">
                    ${poster ? `<img src="${poster}" alt="${title}" style="width:100%;height:100%;object-fit:cover;">` : `<div style="width:100%;height:100%;display:flex;align-items:center;justify-content:center;color:#6b7280;">🎬</div>`}
                    <span style="position:absolute;top:4px;left:4px;padding:2px 4px;background:${item.mediaType === 'tv' ? '#3b82f6' : '#f59e0b'};color:white;font-size:8px;border-radius:4px;">${type}</span>
                    ${statusBadge ? `<span style="position:absolute;top:4px;right:4px;padding:2px 4px;background:#22c55e;color:white;font-size:8px;border-radius:4px;">${statusBadge}</span>` : ''}
                </div>
                <div style="padding:6px;">
                    <p style="color:white;font-size:10px;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">${title}</p>
                </div>
            </div>
        `;
    }
    
    function renderRequestCard(req) {
        const media = req.media;
        const title = media?.title || media?.name || 'Unknown';
        const status = req.status === 1 ? '⏳ Pending' : req.status === 2 ? '✓ Approved' : '✗ Declined';
        const statusColor = req.status === 1 ? '#eab308' : req.status === 2 ? '#22c55e' : '#ef4444';
        
        return `
            <div style="display:flex;gap:8px;padding:8px;background:#1f2937;border-radius:8px;">
                <div style="width:40px;height:60px;background:#374151;border-radius:4px;overflow:hidden;">
                    ${media?.posterPath ? `<img src="https://image.tmdb.org/t/p/w200${media.posterPath}" style="width:100%;height:100%;object-fit:cover;">` : ''}
                </div>
                <div style="flex:1;min-width:0;">
                    <p style="color:white;font-size:11px;font-weight:500;white-space:nowrap;overflow:hidden;text-overflow:ellipsis;">${title}</p>
                    <p style="color:${statusColor};font-size:10px;">${status}</p>
                    <p style="color:#6b7280;font-size:9px;">${new Date(req.createdAt).toLocaleDateString()}</p>
                </div>
            </div>
        `;
    }
    
    async function showMediaDetail(item) {
        const area = document.getElementById('overseerrContentArea');
        area.innerHTML = `<div style="display:flex;align-items:center;justify-content:center;height:100%;"><p style="color:#9ca3af;">Loading...</p></div>`;
        
        try {
            const details = item.mediaType === 'tv' ? await api.getTv(item.id) : await api.getMovie(item.id);
            const title = details.title || details.name;
            const year = (details.releaseDate || details.firstAirDate)?.split('-')[0];
            const backdrop = details.backdropPath ? `https://image.tmdb.org/t/p/w780${details.backdropPath}` : '';
            const poster = details.posterPath ? `https://image.tmdb.org/t/p/w200${details.posterPath}` : '';
            const status = details.mediaInfo?.status;
            const isAvailable = status === 5;
            const isPending = status === 2 || status === 3;
            
            area.innerHTML = `
                <div style="position:relative;">
                    <button id="overseerrBack" style="position:absolute;top:8px;left:8px;z-index:10;padding:4px 8px;background:rgba(0,0,0,0.5);border:none;border-radius:4px;color:white;font-size:10px;cursor:pointer;">← Back</button>
                    ${backdrop ? `<div style="height:120px;background:url('${backdrop}') center/cover;position:relative;"><div style="position:absolute;inset:0;background:linear-gradient(to top,#030712,transparent);"></div></div>` : ''}
                    <div style="padding:12px;margin-top:${backdrop ? '-40px' : '0'};position:relative;">
                        <div style="display:flex;gap:12px;">
                            <div style="width:80px;flex-shrink:0;">
                                ${poster ? `<img src="${poster}" style="width:100%;border-radius:8px;box-shadow:0 4px 6px rgba(0,0,0,0.5);">` : ''}
                            </div>
                            <div style="flex:1;min-width:0;">
                                <h2 style="color:white;font-size:14px;font-weight:bold;margin-bottom:4px;">${title}</h2>
                                <p style="color:#9ca3af;font-size:11px;margin-bottom:8px;">${year || ''} • ${item.mediaType === 'tv' ? 'TV Show' : 'Movie'}</p>
                                ${isAvailable ? `<span style="display:inline-block;padding:4px 8px;background:#22c55e33;color:#22c55e;font-size:10px;border-radius:4px;">✓ Available</span>` : 
                                  isPending ? `<span style="display:inline-block;padding:4px 8px;background:#eab30833;color:#eab308;font-size:10px;border-radius:4px;">⏳ Requested</span>` :
                                  `<button id="overseerrRequest" style="padding:6px 12px;background:#6366f1;border:none;border-radius:6px;color:white;font-size:11px;cursor:pointer;">✨ Request</button>`}
                            </div>
                        </div>
                        ${details.overview ? `<p style="color:#d1d5db;font-size:11px;margin-top:12px;line-height:1.4;">${details.overview.substring(0, 200)}${details.overview.length > 200 ? '...' : ''}</p>` : ''}
                    </div>
                </div>
            `;
            
            document.getElementById('overseerrBack').onclick = () => {
                renderMainApp();
                renderContent();
            };
            
            const requestBtn = document.getElementById('overseerrRequest');
            if (requestBtn) {
                requestBtn.onclick = async () => {
                    requestBtn.disabled = true;
                    requestBtn.textContent = 'Requesting...';
                    try {
                        await api.createRequest(item.mediaType, item.id, item.mediaType === 'tv' ? [{ seasonNumber: 1 }] : undefined);
                        requestBtn.textContent = '✓ Requested!';
                        requestBtn.style.background = '#22c55e';
                        loadData();
                    } catch (err) {
                        requestBtn.textContent = 'Failed';
                        requestBtn.style.background = '#ef4444';
                    }
                };
            }
        } catch (err) {
            area.innerHTML = `<p style="color:#ef4444;font-size:11px;">Failed to load details</p>`;
        }
    }
    
    // Auto-connect if config exists
    if (config.serverUrl && config.apiKey) {
        api = createApiClient(config.serverUrl, config.apiKey);
        api.getStatus().then(() => {
            return api.getCurrentUser();
        }).then(user => {
            currentUser = user;
            connected = true;
            render();
            loadData();
        }).catch(() => {
            render();
        });
    } else {
        render();
    }
}
</script>

</body>
</html>
