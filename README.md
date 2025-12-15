<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<title>Movable Zoomable Weather Radar</title>

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
    }

    /* Window shell */
    .window {
        position: absolute;
        top: 5%;
        left: 5%;
        width: 90%;
        height: 85%;
        background: #000;
        border: 2px solid #1f2a44;
        border-radius: 10px;
        box-shadow: 0 15px 40px rgba(0,0,0,0.8);
        display: flex;
        flex-direction: column;
    }

    /* Title / grab bar */
    .title-bar {
        height: 44px;
        background: #121a33;
        color: #8fb4ff;
        font-size: 14px;
        display: flex;
        align-items: center;
        padding: 0 12px;
        gap: 12px;
        cursor: move;
        border-bottom: 1px solid #1f2a44;
        touch-action: none;
    }

    .title-text {
        flex: 1;
        white-space: nowrap;
    }

    /* Zoom control */
    .zoom-control {
        display: flex;
        align-items: center;
        gap: 6px;
        font-size: 12px;
        cursor: default;
    }

    .zoom-control input[type="range"] {
        width: 110px;
        touch-action: manipulation;
    }

    /* Iframe wrapper for scaling */
    .iframe-wrap {
        flex: 1;
        
