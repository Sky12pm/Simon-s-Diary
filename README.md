# Simon-s-Diary
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Diário de Pista</title>
<style>
  @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@500;700;900&family=Teko:wght@500;600;700&family=Caveat:wght@500;600;700&family=JetBrains+Mono:wght@500&display=swap');

  :root {
    --leather-dark: #3D1810;
    --leather: #5C2A1E;
    --leather-light: #7A3B28;
    --brass: #C9952C;
    --brass-bright: #E8B84B;
    --ember: #D98A1F;
    --racing-red: #B8201A;
    --table-dark: #1C1410;
    --table: #2B1D14;
    --table-light: #3E2A1B;
    --pad-yellow: #F5DD6E;
    --pad-yellow-edge: #E0C24E;
    --ink-pen: #1A2B4C;
    --ink-pencil: #5A5A5A;
  }

  * { box-sizing: border-box; -webkit-tap-highlight-color: transparent; }
  html, body {
    margin: 0; padding: 0; height: 100%; width: 100%;
    overflow: hidden;
    font-family: Georgia, serif;
  }

  body {
    background:
      radial-gradient(ellipse 120% 80% at 50% 20%, rgba(217,138,31,0.08), transparent 60%),
      linear-gradient(180deg, var(--table-dark) 0%, var(--table) 55%, var(--table-light) 100%);
    display: flex;
    align-items: center;
    justify-content: center;
    perspective: 1800px;
  }

  .table-surface {
    position: fixed; inset: 0;
    background-image:
      repeating-linear-gradient(90deg, rgba(0,0,0,0.12) 0px, transparent 2px, transparent 120px, rgba(0,0,0,0.12) 122px),
      repeating-linear-gradient(0deg, rgba(255,255,255,0.02) 0px, transparent 1px, transparent 3px);
    opacity: 0.6;
    pointer-events: none;
  }
  .table-vignette {
    position: fixed; inset: 0;
    background: radial-gradient(ellipse 90% 70% at 50% 50%, transparent 40%, rgba(0,0,0,0.55) 100%);
    pointer-events: none;
  }

  .scene {
    position: relative;
    width: min(94vw, 760px);
    height: min(82vh, 760px);
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .book-wrap {
    position: relative;
    width: 100%; height: 100%;
    display: flex; align-items: center; justify-content: center;
    transform-style: preserve-3d;
    will-change: transform;
    transition: transform 0.35s cubic-bezier(.25,.46,.45,.94);
    pointer-events: none;
  }
  .book-wrap > * { pointer-events: auto; }
  .book-wrap.resting { transform: rotateX(8deg) rotateZ(-1deg); }
  .book-wrap.open { transform: rotateX(2deg); }

  /* ===== CLOSED NOTEBOOK ===== */
  .notebook {
    position: relative;
    width: 100%; max-width: 420px;
    aspect-ratio: 3 / 4;
    cursor: pointer;
    transform: scale(1);
    transform-origin: 50% 50%;
    will-change: transform;
    transition: transform 0.18s cubic-bezier(.25,.46,.45,.94);
  }
  .notebook.zoomed { cursor: zoom-out; }

  .cover {
    position: absolute; inset: 0;
    border-radius: 6px 10px 10px 6px;
    background:
      radial-gradient(ellipse 140% 100% at 30% 0%, rgba(255,255,255,0.05), transparent 55%),
      repeating-linear-gradient(125deg, rgba(0,0,0,0.10) 0px, transparent 3px, transparent 7px),
      linear-gradient(135deg, var(--leather-light) 0%, var(--leather) 45%, var(--leather-dark) 100%);
    box-shadow: 0 2px 0 rgba(0,0,0,0.4) inset, 8px 18px 40px rgba(0,0,0,0.55), 0 0 0 1px rgba(0,0,0,0.3);
    overflow: hidden;
  }
  .cover::before {
    content: ""; position: absolute; inset: 0;
    background-image: radial-gradient(circle at 20% 30%, rgba(0,0,0,0.15) 0, transparent 2px),
      radial-gradient(circle at 60% 70%, rgba(0,0,0,0.12) 0, transparent 2px),
      radial-gradient(circle at 80% 20%, rgba(0,0,0,0.1) 0, transparent 1.5px),
      radial-gradient(circle at 40% 85%, rgba(0,0,0,0.13) 0, transparent 2px);
    background-size: 38px 38px, 44px 44px, 30px 30px, 50px 50px;
    opacity: 0.7; mix-blend-mode: multiply;
  }
  .cover-spine-shadow { position: absolute; left: 0; top: 0; bottom: 0; width: 14%; background: linear-gradient(90deg, rgba(0,0,0,0.45), transparent); }
  .cover-edge-worn { position: absolute; inset: 0; background: radial-gradient(ellipse 80% 80% at 50% 50%, transparent 55%, rgba(0,0,0,0.35) 100%); border-radius: inherit; }
  .corner-wear { position: absolute; width: 46px; height: 46px; background: radial-gradient(circle at 0 0, rgba(217,138,31,0.18), transparent 70%); }
  .corner-wear.tl { top: 0; left: 0; }
  .corner-wear.br { bottom: 0; right: 0; transform: rotate(180deg); }

  /* ===== BRASÃO S.R. ===== */
  .crest {
    position: absolute; top: 24%; left: 50%;
    transform: translate(-50%, -50%);
    width: 30%;
    aspect-ratio: 0.85;
    z-index: 2;
  }
  .crest-shield {
    width: 100%; height: 100%;
    background: linear-gradient(160deg, rgba(0,0,0,0.18), rgba(0,0,0,0.32));
    clip-path: polygon(50% 0%, 100% 14%, 100% 60%, 50% 100%, 0% 60%, 0% 14%);
    border: 2px solid var(--brass);
    box-shadow:
      0 1px 1px rgba(0,0,0,0.6),
      0 0 0 1px rgba(0,0,0,0.35) inset,
      0 2px 4px rgba(232,184,75,0.2) inset;
    display: flex; align-items: center; justify-content: center;
    position: relative;
  }
  .crest-shield-inner {
    width: 78%; height: 78%;
    clip-path: polygon(50% 0%, 100% 14%, 100% 60%, 50% 100%, 0% 60%, 0% 14%);
    border: 1px solid var(--ember);
    opacity: 0.75;
    display: flex; align-items: center; justify-content: center;
  }
  .crest-initials {
    font-family: 'Cinzel', serif;
    font-weight: 900;
    font-size: clamp(15px, 4vw, 20px);
    letter-spacing: 1px;
    color: var(--brass-bright);
    text-shadow: 0 1px 0 rgba(0,0,0,0.6), 0 0 10px rgba(217,138,31,0.3);
    opacity: 0.95;
  }

  /* ===== STICKERS (worn, slightly faded — pasted-on look) ===== */
  .sticker {
    position: absolute;
    z-index: 1;
    pointer-events: none;
    filter: drop-shadow(0 1px 2px rgba(0,0,0,0.4));
  }
  .img-sticker {
    position: absolute;
    z-index: 1;
    pointer-events: none;
    filter: drop-shadow(0 2px 5px rgba(0,0,0,0.55));
  }
  .skull-img { width: 22%; opacity: 0.95; }
  .ghost-img { width: 26%; opacity: 0.95; }
  .plate-img { width: 24%; opacity: 0.92; }

  .check-patch { width: 15%; aspect-ratio: 1.3; opacity: 0.55; }
  .check-flag-mini {
    width: 100%; height: 100%;
    background-image: linear-gradient(45deg, #0d0d0d 25%, transparent 25%, transparent 75%, #0d0d0d 75%), linear-gradient(45deg, #0d0d0d 25%, transparent 25%, transparent 75%, #0d0d0d 75%);
    background-size: 7px 7px;
    background-position: 0 0, 3.5px 3.5px;
    background-color: var(--brass-bright);
    border: 1px solid rgba(0,0,0,0.4);
    border-radius: 2px;
    mix-blend-mode: multiply;
  }

  .number-patch {
    font-family: 'Teko', sans-serif;
    font-weight: 700;
    font-size: clamp(22px, 6vw, 30px);
    color: var(--ember);
    opacity: 0.55;
    border: 2px solid var(--ember);
    border-radius: 4px;
    padding: 0 8px;
    line-height: 1.3;
  }

  .stripe-patch {
    width: 22%; height: 5px;
    background: var(--racing-red);
    opacity: 0.4;
    border-radius: 1px;
  }
  .stripe-patch.alt { background: var(--brass-bright); opacity: 0.3; }

  .handwriting {
    font-family: 'Caveat', cursive;
    font-size: clamp(15px, 4.2vw, 19px);
    color: var(--brass-bright);
    opacity: 0.55;
    white-space: nowrap;
  }

  .scratch-mark {
    width: 13%; height: 2px;
    background: rgba(0,0,0,0.35);
    border-radius: 1px;
  }
  .scratch-mark::before {
    content: "";
    position: absolute; top: 5px; left: 2px;
    width: 90%; height: 2px;
    background: rgba(0,0,0,0.25);
    border-radius: 1px;
  }

  .cover-title { position: absolute; top: 68%; left: 50%; transform: translate(-50%, 0%); width: 80%; text-align: center; z-index: 2; }
  .cover-title .line1 { font-family: 'Cinzel', serif; font-weight: 700; font-size: clamp(20px, 6vw, 28px); letter-spacing: 3px; color: var(--brass-bright); text-shadow: 0 1px 0 rgba(0,0,0,0.6), 0 0 18px rgba(217,138,31,0.25); margin: 0; }
  .cover-title .line2 { font-family: 'Cinzel', serif; font-weight: 500; font-size: clamp(11px, 2.6vw, 13px); letter-spacing: 4px; color: var(--ember); text-transform: uppercase; margin-top: 6px; opacity: 0.85; }

  .cover-rule { position: absolute; left: 12%; right: 12%; height: 1px; background: linear-gradient(90deg, transparent, var(--brass), transparent); opacity: 0.6; }
  .cover-rule.top { top: 16%; }
  .cover-rule.bottom { bottom: 14%; }

  .cord { position: absolute; top: 0; bottom: 0; right: 8%; width: 5px; background: linear-gradient(180deg, #2a1a10, #4a2c18, #2a1a10); box-shadow: -1px 0 2px rgba(0,0,0,0.4); border-radius: 3px; z-index: 3; }
  .cord-wrap { position: absolute; right: 6%; top: 46%; width: 30px; height: 14px; background: linear-gradient(180deg, #4a2c18, #2a1a10); border-radius: 7px; box-shadow: 0 2px 4px rgba(0,0,0,0.5); z-index: 4; }

  .zoom-hint { position: absolute; bottom: -34px; left: 50%; transform: translateX(-50%); font-family: 'JetBrains Mono', monospace; font-size: 11px; color: rgba(232,184,75,0.55); letter-spacing: 1px; white-space: nowrap; transition: opacity 0.3s ease; }

  /* ===== OPEN STAGE: book spread on the desk ===== */
  .pages-stage {
    position: absolute; inset: 0;
    display: none;
    align-items: center; justify-content: center;
  }
  .pages-stage.active { display: flex; }

  .spread-area { position: relative; }

  .spread {
    position: relative;
    display: flex;
    width: min(94vw, 760px);
    height: min(70vh, 520px);
    box-shadow: 0 18px 50px rgba(0,0,0,0.55), 0 0 0 1px rgba(0,0,0,0.15);
    border-radius: 4px;
    overflow: hidden;
  }

  .page-half {
    position: relative;
    flex: 1;
    background: var(--paper);
    overflow: hidden;
    padding: clamp(16px, 3vw, 30px) clamp(16px, 3vw, 26px);
    display: flex;
    flex-direction: column;
  }
  :root { --paper: #F2E8CE; }
  .page-half.left {
    border-radius: 4px 0 0 4px;
    box-shadow: inset -10px 0 24px -16px rgba(0,0,0,0.35);
  }
  .page-half.right {
    border-radius: 0 4px 4px 0;
    box-shadow: inset 10px 0 24px -16px rgba(0,0,0,0.35);
  }
  .page-half::before {
    content: "";
    position: absolute; inset: 0;
    background-image:
      repeating-linear-gradient(0deg, transparent, transparent 27px, rgba(140,110,30,0.14) 28px);
    background-position: 0 12px;
    pointer-events: none;
  }
  .page-half .content-scroll {
    position: relative;
    flex: 1;
    overflow-y: auto;
    padding-right: 4px;
    z-index: 1;
  }
  .page-half .content-scroll::-webkit-scrollbar { width: 4px; }
  .page-half .content-scroll::-webkit-scrollbar-thumb { background: rgba(92,42,30,0.25); border-radius: 3px; }

  .ink-text {
    font-family: 'Caveat', cursive;
    font-size: clamp(15px, 2.6vw, 19px);
    line-height: 28px;
    color: var(--ink-pen);
  }
  .ink-text p { margin: 0 0 4px; }
  .ink-text .gap { height: 14px; }
  .ink-text .sign { text-align: right; margin-top: 10px; font-size: 1.1em; }

  .page-tag {
    font-family: 'JetBrains Mono', monospace;
    font-size: 9.5px;
    color: rgba(92,42,30,0.45);
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-bottom: 8px;
    z-index: 1;
    position: relative;
  }

  /* ===== mixed-media page styles ===== */
  .doc-block {
    background: rgba(255,255,255,0.55);
    border: 1px solid rgba(92,42,30,0.25);
    box-shadow: 1px 2px 5px rgba(0,0,0,0.15);
    padding: 14px 16px;
    margin: 6px 0 14px;
  }
  .post-it {
    background: #FCEB7E;
    box-shadow: 2px 4px 8px rgba(0,0,0,0.25);
    padding: 14px 14px 18px;
    margin: 10px auto;
    max-width: 86%;
    font-family: 'Caveat', cursive;
    font-size: clamp(14px, 2.4vw, 18px);
    color: #2A1F14;
    line-height: 1.4;
  }
  .post-it.tilt-l { transform: rotate(-2.5deg); }
  .post-it.tilt-r { transform: rotate(2deg); }
  @media (max-width: 700px) {
    .post-it { font-size: 14px; line-height: 1.35; padding: 10px 12px 14px; }
  }

  /* Efeito de página com borda rasgada — fica dentro dos limites da página */
  .torn-page-left {
    position: relative;
  }
  .torn-page-left::before {
    content: "";
    position: absolute;
    top: 0; bottom: 0; left: 0;
    width: 10px;
    background: rgba(0,0,0,0.18);
    clip-path: polygon(
      100% 0%, 40% 5%, 90% 11%, 30% 17%, 95% 24%, 45% 30%,
      85% 37%, 25% 43%, 100% 49%, 50% 55%, 90% 61%, 35% 67%,
      95% 74%, 45% 80%, 85% 87%, 30% 93%, 100% 100%, 0% 100%, 0% 0%
    );
    z-index: 2;
  }
  .torn-page-left::after {
    content: "";
    position: absolute;
    top: 0; bottom: 0; left: 10px;
    width: 3px;
    background: linear-gradient(90deg, rgba(0,0,0,0.12), transparent);
    z-index: 2;
  }
  .torn-edge {
    position: relative;
    background: var(--paper);
    box-shadow: 1px 3px 6px rgba(0,0,0,0.2);
    padding: 14px 16px;
    margin: 8px 0 16px;
  }

  .tape {
    position: absolute;
    width: 56px; height: 22px;
    background: rgba(255,255,255,0.45);
    border: 1px solid rgba(255,255,255,0.6);
    box-shadow: 0 1px 3px rgba(0,0,0,0.2);
    z-index: 2;
  }

  .telemetry-card {
    background: #1C1C1C;
    color: #E8E8E8;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    padding: 14px 16px;
    margin: 8px 0 16px;
    box-shadow: 2px 4px 10px rgba(0,0,0,0.3);
    transform: rotate(-1.2deg);
  }
  .telemetry-card .tc-title { color: var(--brass-bright); letter-spacing: 1px; margin-bottom: 8px; font-size: 11px; }
  .telemetry-card .tc-row { display: flex; align-items: center; gap: 8px; margin-bottom: 5px; }
  .telemetry-card .tc-box { width: 12px; height: 12px; border: 1.5px solid #888; flex-shrink: 0; }
  .telemetry-card .tc-box.checked { background: var(--racing-red); border-color: var(--racing-red); position: relative; }
  .telemetry-card .tc-box.checked::after { content: "✓"; position: absolute; top: -3px; left: 1px; font-size: 10px; color: #fff; }
  .telemetry-card .tc-strike { text-decoration: line-through; text-decoration-color: var(--racing-red); text-decoration-thickness: 2px; }

  .scribble-overlay {
    position: relative;
    display: inline-block;
  }
  .scribble-overlay .strike-mark {
    position: absolute; left: -4%; right: -4%; height: 3px;
    background: var(--racing-red);
    top: 40%;
    transform: rotate(-3deg);
    opacity: 0.85;
  }
  .scribble-overlay .strike-mark.s2 { top: 55%; transform: rotate(2deg); }
  .scribble-overlay .strike-mark.s3 { top: 48%; transform: rotate(-6deg); }

  .photo-frame {
    background: #fff;
    padding: 8px 8px 26px;
    box-shadow: 2px 5px 12px rgba(0,0,0,0.3);
    margin: 8px auto 16px;
    max-width: 70%;
    transform: rotate(-1.5deg);
  }
  .photo-frame .photo-inner {
    width: 100%; aspect-ratio: 4/3;
    background: linear-gradient(135deg, #2b2b2b, #0d0d0d);
    position: relative;
    overflow: hidden;
  }
  .photo-frame .photo-cap {
    font-family: 'Caveat', cursive;
    font-size: 13px;
    color: #555;
    text-align: center;
    margin-top: 6px;
  }

  .page-number-corner {
    position: absolute;
    bottom: 10px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 9px;
    color: rgba(92,42,30,0.35);
    z-index: 1;
  }
  .page-half.left .page-number-corner { left: 16px; }
  .page-half.right .page-number-corner { right: 16px; }

  /* ===== NAV ARROWS ===== */
  .nav-arrow {
    position: absolute; top: 50%; transform: translateY(-50%);
    width: 46px; height: 46px; border-radius: 50%;
    background: rgba(0,0,0,0.35);
    border: 1px solid rgba(232,184,75,0.4);
    color: var(--brass-bright);
    font-size: 19px;
    display: flex; align-items: center; justify-content: center;
    cursor: pointer; z-index: 10;
    transition: background 0.2s ease, transform 0.2s ease;
  }
  .nav-arrow:hover { background: rgba(217,138,31,0.4); }
  .nav-arrow:active { transform: translateY(-50%) scale(0.92); }
  .nav-arrow.left { left: -54px; }
  .nav-arrow.right { right: -54px; }
  .nav-arrow:disabled { opacity: 0.25; cursor: not-allowed; }

  .page-counter {
    position: absolute; bottom: -32px; left: 50%; transform: translateX(-50%);
    font-family: 'JetBrains Mono', monospace; font-size: 11px;
    color: rgba(232,184,75,0.7); letter-spacing: 1px;
  }

  .close-book-btn {
    position: absolute; top: -36px; left: 50%; transform: translateX(-50%);
    font-family: 'JetBrains Mono', monospace; font-size: 11px;
    color: rgba(232,184,75,0.6);
    background: none; border: none; cursor: pointer; letter-spacing: 1px;
    white-space: nowrap;
  }
  .close-book-btn:hover { color: var(--brass-bright); }

  @media (max-width: 700px) {
    .spread { width: min(94vw, 700px); height: min(58vh, 420px); }
    .page-half { padding: clamp(12px, 2.5vw, 20px) clamp(12px, 2.5vw, 18px); }
    .nav-arrow.left { left: -2px; }
    .nav-arrow.right { right: -2px; }
    .nav-arrow { display: none; } /* navegação por arrastar no mobile */
  }

  @media (prefers-reduced-motion: reduce) {
    .book-wrap, .notebook { transition: none; }
  }
</style>
</head>
<body>

<div class="table-surface"></div>
<div class="table-vignette"></div>

<div class="scene">
  <div class="book-wrap resting" id="bookWrap">

    <div class="notebook" id="notebook">
      <div class="cover" id="cover">
        <div class="cover-spine-shadow"></div>
        <div class="corner-wear tl"></div>
        <div class="corner-wear br"></div>
        <div class="cover-rule top"></div>

        <!-- Brasão central S.R. -->
        <div class="crest">
          <div class="crest-shield">
            <div class="crest-shield-inner">
              <span class="crest-initials">S.R.</span>
            </div>
          </div>
        </div>

        <div class="cover-title">
          <div class="line1">DIARY</div>
          <div class="line2">Simon Riley</div>
        </div>
        <div class="cover-rule bottom"></div>

        <!-- Adesivos espalhados pela capa (imagens reais) -->

        <!-- Crânio rachado estilo grafite -->
        <img class="sticker img-sticker skull-img" style="top:5%; left:6%; transform:rotate(-9deg);"
             src="data:image/png;base64,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
