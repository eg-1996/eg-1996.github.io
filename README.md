<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Un regalo para Daniela 🎶</title>
<style>
@import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Lora:ital,wght@0,400;0,500;1,400&display=swap');

/* ── reset & base ── */
* { box-sizing: border-box; margin: 0; padding: 0; }
html, body {
  font-family: 'Lora', Georgia, serif;
  background: #EDE0C8;
  min-height: 100vh;
  display: flex; align-items: flex-start; justify-content: center;
  padding: 1.5rem 1rem 2rem;
}

/* ── main container ── */
#app {
  width: 100%; max-width: 460px;
  position: relative;
}

/* ══════════════════════════════════════════
   PART 1 — QUIZ
══════════════════════════════════════════ */
.quiz-root {
  background: #F5ECD7;
  border-radius: 18px;
  position: relative;
  overflow: hidden;
  display: none;
}
.quiz-root.active { display: block; }

.grain {
  position: absolute; inset: 0;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.08'/%3E%3C/svg%3E");
  pointer-events: none; z-index: 0; opacity: 0.5;
}
.deco-vinyl {
  position: absolute; right: -28px; top: -28px;
  width: 110px; height: 110px; border-radius: 50%;
  background: radial-gradient(circle at 50%,#3D1F0A 28%,#2C1A0E 29%,#2C1A0E 44%,#8B4513 45%,#8B4513 46%,#2C1A0E 47%,#2C1A0E 100%);
  opacity: 0.13; z-index: 0;
}

.qscreen { display: none; position: relative; z-index: 1; padding: 2.5rem 2rem; animation: fadeUp 0.5s ease; }
.qscreen.active { display: block; }
@keyframes fadeUp { from { opacity:0; transform:translateY(12px); } to { opacity:1; transform:translateY(0); } }

.badge {
  display: inline-block; font-family: 'Lora', serif;
  font-size: 11px; letter-spacing: 0.12em; text-transform: uppercase;
  color: #8B4513; background: #E8D5B0; border: 1px solid #C4A87A;
  border-radius: 20px; padding: 4px 14px; margin-bottom: 1.2rem;
}
h1.title { font-family:'Playfair Display',serif; font-size:2rem; font-weight:600; color:#1C0F05; line-height:1.25; margin-bottom:0.5rem; }
h1.title em { font-style:italic; color:#8B4513; }
.subtitle { font-size:0.95rem; color:#6B4423; line-height:1.7; margin-bottom:2rem; font-style:italic; }
.vinyl-icon { width:56px; height:56px; margin:0 auto 1.5rem; display:block; }

.btn-primary {
  display: inline-block; background:#8B4513; color:#F5ECD7;
  font-family:'Lora',serif; font-size:0.95rem; font-weight:500;
  padding:12px 32px; border-radius:40px; border:none; cursor:pointer;
  letter-spacing:0.04em; transition:background 0.2s,transform 0.1s; margin-top:0.5rem;
}
.btn-primary:hover { background:#6B3410; }
.btn-primary:active { transform:scale(0.97); }

.question-label { font-family:'Playfair Display',serif; font-size:1.35rem; font-weight:600; color:#1C0F05; margin-bottom:0.4rem; line-height:1.35; }
.question-sub { font-size:0.88rem; color:#8B6A4A; font-style:italic; margin-bottom:1.6rem; }

.options-grid { display:grid; grid-template-columns:1fr 1fr; gap:12px; margin-bottom:1.8rem; }
.option-card {
  background:#FDF6E8; border:1.5px solid #D4B896; border-radius:12px;
  padding:1rem 0.9rem; cursor:pointer; transition:all 0.18s; text-align:left; font-family:'Lora',serif;
}
.option-card:hover { border-color:#8B4513; background:#FFF8EE; }
.option-card.selected { border-color:#8B4513; background:#8B4513; color:#F5ECD7; }
.option-card.selected .opt-name, .option-card.selected .opt-name a { color:#F5ECD7; }
.option-card.selected .opt-desc { color:#F0D9C0; }
.opt-icon { font-size:22px; margin-bottom:6px; display:block; }
.opt-name { font-size:0.9rem; font-weight:500; color:#1C0F05; margin-bottom:2px; }
.opt-name a { color:inherit; text-decoration:underline; text-underline-offset:2px; }
.opt-desc { font-size:0.78rem; color:#8B6A4A; line-height:1.45; font-style:italic; }

.progress-bar { display:flex; gap:6px; margin-bottom:1.8rem; }
.prog-dot { height:4px; border-radius:4px; flex:1; background:#D4B896; transition:background 0.3s; }
.prog-dot.done { background:#8B4513; }

.btn-back {
  background:none; border:1.5px solid #8B4513; color:#1C0F05;
  font-family:'Lora',serif; font-size:0.88rem; cursor:pointer;
  padding:10px 20px; border-radius:40px; font-style:italic;
  margin-right:0.75rem; transition:background 0.18s;
}
.btn-back:hover { background:#E8D5B0; }
.btn-row { display:flex; align-items:center; margin-top:0.5rem; }

/* confirm screen */
.confirm-summary { background:#FDF6E8; border:1.5px solid #C4A87A; border-radius:12px; padding:1.2rem 1.4rem; margin-bottom:1.6rem; }
.confirm-row { display:flex; align-items:flex-start; gap:10px; margin-bottom:0.9rem; }
.confirm-row:last-child { margin-bottom:0; }
.confirm-icon { font-size:18px; margin-top:1px; }
.confirm-label { font-size:0.75rem; text-transform:uppercase; letter-spacing:0.1em; color:#8B6A4A; margin-bottom:2px; }
.confirm-value { font-size:0.92rem; font-weight:500; color:#1C0F05; }
.confirm-divider { border:none; border-top:1px dashed #C4A87A; margin:0.9rem 0; }

/* quiz gift card (shown before twist) */
.card-wrap {
  background:#FDF6E8; border:1.5px solid #C4A87A; border-radius:14px;
  padding:1.8rem 1.6rem; position:relative; overflow:hidden; margin-bottom:1.5rem;
}
.card-wrap::before {
  content:''; position:absolute; top:0; left:0; right:0; height:6px;
  background:repeating-linear-gradient(90deg,#8B4513 0,#8B4513 20px,#C4A87A 20px,#C4A87A 40px);
}
.gift-for { font-size:0.78rem; text-transform:uppercase; letter-spacing:0.15em; color:#8B6A4A; margin-bottom:0.3rem; margin-top:0.5rem; }
.gift-name { font-family:'Playfair Display',serif; font-size:2.2rem; font-weight:600; color:#1C0F05; font-style:italic; line-height:1.1; margin-bottom:1.2rem; }
.gift-items { border-top:1px dashed #C4A87A; padding-top:1rem; }
.gift-item { display:flex; align-items:flex-start; gap:10px; margin-bottom:0.75rem; }
.gift-item-icon { font-size:18px; margin-top:1px; }
.gift-item-text { font-size:0.88rem; color:#2C1A0E; line-height:1.5; }
.gift-item-text strong { display:block; font-weight:500; color:#1C0F05; }
.gift-item-text span { color:#6B4423; font-style:italic; }
.card-footer { display:flex; justify-content:space-between; align-items:flex-end; margin-top:1.2rem; padding-top:1rem; border-top:1px dashed #C4A87A; }
.card-code { font-size:0.75rem; letter-spacing:0.18em; color:#8B4513; font-family:'Courier New',monospace; }
.card-stamp { width:52px; height:52px; border-radius:50%; border:2px solid #8B4513; display:flex; align-items:center; justify-content:center; flex-direction:column; }
.stamp-text { font-size:7px; text-transform:uppercase; letter-spacing:0.08em; color:#8B4513; font-family:'Lora',serif; }
.stamp-year { font-size:11px; font-weight:600; color:#8B4513; font-family:'Playfair Display',serif; }
.confetti-row { font-size:22px; letter-spacing:4px; margin-bottom:0.8rem; }
.reward-subtitle { font-size:0.88rem; color:#6B4423; font-style:italic; line-height:1.7; margin-bottom:1.5rem; }

/* ══════════════════════════════════════════
   PART 2 — TWIST SCREEN
══════════════════════════════════════════ */
#twist-screen {
  display: none;
  background: #1C0F05;
  border-radius: 18px;
  padding: 3rem 2rem;
  text-align: center;
  animation: fadeUp 0.6s ease;
  position: relative;
  overflow: hidden;
}
#twist-screen.active { display: block; }

.twist-vinyl {
  width: 90px; height: 90px; border-radius: 50%; margin: 0 auto 2rem;
  background: radial-gradient(circle at 50%,#5A3010 28%,#2C1A0E 29%,#2C1A0E 44%,#8B4513 45%,#8B4513 46%,#2C1A0E 47%,#2C1A0E 100%);
  animation: spin 4s linear infinite;
  border: 3px solid #8B4513;
}
@keyframes spin { from { transform:rotate(0deg); } to { transform:rotate(360deg); } }

.twist-emoji { font-size: 2.5rem; margin-bottom: 1rem; display: block; }
.twist-title {
  font-family: 'Playfair Display', serif; font-size: 1.7rem;
  font-weight: 600; color: #F5ECD7; line-height: 1.3; margin-bottom: 1rem;
}
.twist-title em { color: #C4A87A; font-style: italic; }
.twist-sub {
  font-size: 0.9rem; color: #A08060; font-style: italic;
  line-height: 1.7; margin-bottom: 2rem; max-width: 320px; margin-left: auto; margin-right: auto;
}
.btn-twist {
  background: #8B4513; color: #F5ECD7;
  font-family: 'Lora', serif; font-size: 1rem; font-weight: 500;
  padding: 14px 36px; border-radius: 40px; border: none; cursor: pointer;
  letter-spacing: 0.04em; transition: background 0.2s, transform 0.1s;
}
.btn-twist:hover { background: #C4A87A; color: #1C0F05; }
.btn-twist:active { transform: scale(0.97); }

/* decorative lines */
.twist-lines {
  position: absolute; inset: 0; pointer-events: none; opacity: 0.07;
  background: repeating-linear-gradient(0deg, #C4A87A 0, #C4A87A 1px, transparent 1px, transparent 32px);
}

/* ══════════════════════════════════════════
   PART 3 — FLAPPY GAME
══════════════════════════════════════════ */
#game-section {
  display: none;
  animation: fadeUp 0.5s ease;
}
#game-section.active { display: block; }

#question-bar {
  background: #2C1A0E; color: #F5ECD7;
  padding: 10px 16px; border-radius: 10px 10px 0 0;
  font-family: 'Lora', serif; font-size: 0.85rem;
  text-align: center; line-height: 1.45; min-height: 52px;
  display: flex; align-items: center; justify-content: center;
  border: 2px solid #C4A87A; border-bottom: none;
}
canvas { display:block; width:100%; border-left:2px solid #C4A87A; border-right:2px solid #C4A87A; }
#score-bar {
  display:flex; justify-content:space-between; align-items:center;
  padding:6px 12px; background:#E8D5B0;
  border-radius:0 0 10px 10px;
  font-family:'Lora',serif; font-size:0.8rem; color:#6B4423; font-style:italic;
  border:2px solid #C4A87A; border-top:none;
}
#feedback-banner {
  position:absolute; left:2px; right:2px; top:52px;
  text-align:center; font-size:1.1rem;
  font-family:'Lora',serif; font-weight:bold;
  padding:11px 16px; pointer-events:none;
  opacity:0; transition:opacity 0.15s; z-index:10;
}
#feedback-banner.show { opacity:1; }
#feedback-banner.correct { background:rgba(50,150,50,0.9); color:#fff; }
#feedback-banner.wrong   { background:rgba(180,40,40,0.9); color:#fff; }

#game-wrap { position:relative; }

/* game overlay (start/end screens) */
#game-overlay {
  position:absolute; left:2px; right:2px; top:52px; bottom:28px;
  display:flex; flex-direction:column;
  align-items:center; justify-content:center;
  background:rgba(245,236,215,0.96);
  text-align:center; padding:1.5rem 1.2rem;
  overflow-y:auto; border-radius: 0;
}
#game-overlay h2 { font-family:'Playfair Display',serif; font-size:1.3rem; color:#1C0F05; margin-bottom:0.4rem; }
#game-overlay .sub { font-family:'Lora',serif; font-size:0.85rem; color:#6B4423; font-style:italic; margin-bottom:1.2rem; line-height:1.6; }

.gbtn {
  background:#8B4513; color:#F5ECD7; border:none; border-radius:40px;
  padding:10px 26px; font-size:0.9rem; font-family:'Lora',serif;
  cursor:pointer; transition:background 0.2s; margin:4px;
}
.gbtn:hover { background:#6B3410; }
.gbtn-outline {
  background:none; color:#8B4513; border:1.5px solid #8B4513; border-radius:40px;
  padding:9px 22px; font-size:0.85rem; font-family:'Lora',serif; font-style:italic;
  cursor:pointer; transition:background 0.2s; margin:4px;
}
.gbtn-outline:hover { background:#E8D5B0; }

/* final gift card (after flappy) */
.fcard-wrap {
  background:#FDF6E8; border:1.5px solid #C4A87A; border-radius:12px;
  padding:1.2rem 1.2rem 1rem; position:relative; overflow:hidden;
  width:100%; margin-bottom:1rem; text-align:left;
}
.fcard-wrap::before {
  content:''; position:absolute; top:0; left:0; right:0; height:5px;
  background:repeating-linear-gradient(90deg,#8B4513 0,#8B4513 18px,#C4A87A 18px,#C4A87A 36px);
}
.fcard-for { font-size:0.7rem; text-transform:uppercase; letter-spacing:0.14em; color:#8B6A4A; margin-top:0.4rem; }
.fcard-name { font-family:'Playfair Display',serif; font-size:1.7rem; font-weight:bold; color:#1C0F05; font-style:italic; line-height:1.1; margin-bottom:0.9rem; }
.fgift-row { display:flex; align-items:center; gap:8px; margin-bottom:0.6rem; }
.fgift-icon { font-size:16px; flex-shrink:0; }
.fgift-text { font-size:0.82rem; color:#1C0F05; line-height:1.4; flex:1; }
.fgift-text strong { display:block; font-weight:600; }
.fgift-text span { color:#6B4423; font-style:italic; font-size:0.78rem; }
.fgift-row.failed .fgift-text strong { color:#9B2020; text-decoration:line-through; opacity:0.7; }
.fgift-row.failed .fgift-text span { color:#9B2020; opacity:0.7; }
.fail-badge { background:#9B2020; color:#fff; border-radius:50%; width:22px; height:22px; display:flex; align-items:center; justify-content:center; font-size:12px; font-weight:bold; flex-shrink:0; }
.fcard-divider { border:none; border-top:1px dashed #C4A87A; margin:0.8rem 0; }
.fcard-footer { display:flex; justify-content:space-between; align-items:flex-end; }
.fcard-code { font-size:0.7rem; letter-spacing:0.16em; color:#8B4513; font-family:'Courier New',monospace; }
.fcard-stamp { width:44px; height:44px; border-radius:50%; border:2px solid #8B4513; display:flex; align-items:center; justify-content:center; flex-direction:column; }
.fstamp-sm { font-size:6px; text-transform:uppercase; letter-spacing:0.07em; color:#8B4513; }
.fstamp-yr { font-size:10px; font-weight:bold; color:#8B4513; }
.retry-msg { background:#FFF3CD; border:1px solid #C4A87A; border-radius:10px; padding:0.8rem 1rem; font-size:0.82rem; color:#6B3A00; line-height:1.55; margin-bottom:1rem; font-style:italic; width:100%; text-align:center; }
.gbtn-row { display:flex; flex-wrap:wrap; justify-content:center; gap:6px; }

/* also show the quiz selections on final card */
.quiz-selections { background:#F0E8D0; border-radius:8px; padding:0.8rem 1rem; margin-bottom:0.8rem; }
.qs-label { font-size:0.7rem; text-transform:uppercase; letter-spacing:0.12em; color:#8B6A4A; margin-bottom:0.5rem; }
.qs-item { font-size:0.82rem; color:#2C1A0E; margin-bottom:0.2rem; }
.qs-item strong { font-weight:600; }

/* ── gift list modal ── */
#gift-modal-overlay {
  display: none; position: fixed; inset: 0;
  background: rgba(28,15,5,0.7); z-index: 100;
  align-items: center; justify-content: center; padding: 1.5rem 1rem;
}
#gift-modal-overlay.open { display: flex; }
#gift-modal {
  background: #F5ECD7; border-radius: 18px; width: 100%; max-width: 440px;
  max-height: 88vh; overflow-y: auto; padding: 2rem 1.6rem;
  position: relative; box-shadow: 0 8px 40px rgba(0,0,0,0.35);
}
.gm-close {
  position: absolute; top: 14px; right: 16px;
  background: none; border: none; font-size: 1.4rem; cursor: pointer;
  color: #8B4513; line-height: 1;
}
.gm-close:hover { color: #1C0F05; }
.gm-title { font-family: 'Playfair Display', serif; font-size: 1.4rem; font-weight: 600; color: #1C0F05; margin-bottom: 0.25rem; }
.gm-sub { font-size: 0.85rem; color: #6B4423; font-style: italic; margin-bottom: 1.6rem; }
.gm-section { margin-bottom: 1.4rem; }
.gm-section-label {
  font-size: 0.7rem; text-transform: uppercase; letter-spacing: 0.14em;
  color: #8B6A4A; margin-bottom: 0.7rem; border-bottom: 1px dashed #C4A87A; padding-bottom: 0.4rem;
}
.gm-item {
  display: flex; align-items: center; gap: 10px;
  background: #FDF6E8; border: 1.5px solid #D4B896; border-radius: 10px;
  padding: 0.7rem 0.9rem; margin-bottom: 0.5rem;
}
.gm-item-icon { font-size: 18px; flex-shrink: 0; }
.gm-item-name { font-size: 0.88rem; font-weight: 500; color: #1C0F05; flex: 1; }
.gm-item-link {
  font-size: 0.78rem; background: #8B4513; color: #F5ECD7;
  padding: 5px 12px; border-radius: 20px; text-decoration: none;
  white-space: nowrap; flex-shrink: 0; font-family: 'Lora', serif;
}
.gm-item-link:hover { background: #6B3410; }
.gm-item-nolink { font-size: 0.78rem; color: #8B6A4A; font-style: italic; flex-shrink: 0; }
.btn-all-gifts {
  display: inline-block; background: none; border: 1.5px solid #8B4513;
  color: #8B4513; font-family: 'Lora', serif; font-size: 0.88rem;
  padding: 10px 22px; border-radius: 40px; cursor: pointer;
  font-style: italic; transition: background 0.18s; margin: 4px;
}
.btn-all-gifts:hover { background: #E8D5B0; }
</style>
</head>
<body>
<div id="app">

  <!-- ══ PART 1: QUIZ ══ -->
  <div class="quiz-root active" id="quiz-root">
    <div class="grain"></div>
    <div class="deco-vinyl"></div>

    <!-- Intro -->
    <div class="qscreen active" id="qscreen-intro">
      <div style="text-align:center;padding-top:0.5rem">
        <svg class="vinyl-icon" viewBox="0 0 56 56" fill="none" xmlns="http://www.w3.org/2000/svg">
          <circle cx="28" cy="28" r="27" fill="#2C1A0E"/>
          <circle cx="28" cy="28" r="19" fill="none" stroke="#8B4513" stroke-width="1"/>
          <circle cx="28" cy="28" r="12" fill="none" stroke="#8B4513" stroke-width="0.8"/>
          <circle cx="28" cy="28" r="6" fill="none" stroke="#8B4513" stroke-width="0.8"/>
          <circle cx="28" cy="28" r="3" fill="#C4A87A"/>
          <line x1="28" y1="1" x2="28" y2="4" stroke="#8B4513" stroke-width="0.8"/>
          <line x1="28" y1="52" x2="28" y2="55" stroke="#8B4513" stroke-width="0.8"/>
          <line x1="1" y1="28" x2="4" y2="28" stroke="#8B4513" stroke-width="0.8"/>
          <line x1="52" y1="28" x2="55" y2="28" stroke="#8B4513" stroke-width="0.8"/>
        </svg>
        <div class="badge">Un regalo te espera</div>
        <h1 class="title">Hola Daniela,<br><em>¿lista para descubrirlo?</em></h1>
        <p class="subtitle" style="max-width:320px;margin:0.5rem auto 2rem">Algo especial te espera.<br>Responde dos preguntas rápidas para reclamarlo.</p>
        <button class="btn-primary" onclick="qGoTo('qscreen-q1')">Abre tu regalo →</button>
      </div>
    </div>

    <!-- Q1: Speakers -->
    <div class="qscreen" id="qscreen-q1">
      <div class="progress-bar"><div class="prog-dot done"></div><div class="prog-dot"></div></div>
      <div class="badge">Pregunta 1 de 2</div>
      <p class="question-label">Elige tus parlantes.</p>
      <p class="question-sub">¿Qué par habla a tu alma?</p>
      <div class="options-grid" id="q1-options"></div>
      <div class="btn-row">
        <button class="btn-back" onclick="qGoTo('qscreen-intro')">← Atrás</button>
        <button class="btn-primary" id="q1-next" onclick="qGoTo('qscreen-q2')" style="display:none">Siguiente →</button>
      </div>
    </div>

    <!-- Q2: Furniture -->
    <div class="qscreen" id="qscreen-q2">
      <div class="progress-bar"><div class="prog-dot done"></div><div class="prog-dot done"></div></div>
      <div class="badge">Pregunta 2 de 2</div>
      <p class="question-label">Elige tus muebles.</p>
      <p class="question-sub">¿Dónde vivirá tu equipo?</p>
      <div class="options-grid" id="q2-options"></div>
      <div class="btn-row">
        <button class="btn-back" onclick="qGoTo('qscreen-q1')">← Atrás</button>
        <button class="btn-primary" id="q2-next" onclick="showConfirm()" style="display:none">Siguiente →</button>
      </div>
    </div>

    <!-- Confirm -->
    <div class="qscreen" id="qscreen-confirm">
      <div class="badge">Un momento...</div>
      <h1 class="title">¿Estás segura de<br><em>tu elección?</em></h1>
      <p class="question-sub" style="margin-bottom:1.6rem">Esto es lo que elegiste — confirmá antes de continuar.</p>
      <div class="confirm-summary">
        <div class="confirm-row">
          <span class="confirm-icon">🔊</span>
          <div><div class="confirm-label">Parlantes</div><div class="confirm-value" id="confirm-speakers">—</div></div>
        </div>
        <hr class="confirm-divider">
        <div class="confirm-row">
          <span class="confirm-icon">🪵</span>
          <div><div class="confirm-label">Mueble</div><div class="confirm-value" id="confirm-furniture">—</div></div>
        </div>
      </div>
      <div class="btn-row">
        <button class="btn-back" onclick="qRestart()">↩ Empezar de nuevo</button>
        <button class="btn-primary" onclick="showFakeGiftCard()">¡Sí, es mi elección! 🎁</button>
      </div>
    </div>

    <!-- Fake reward (shown before twist) -->
    <div class="qscreen" id="qscreen-reward">
      <div class="confetti-row" style="text-align:center">🎉 🎶 🎁</div>
      <h1 class="title" style="text-align:center;margin-bottom:0.3rem">Es tuyo, Daniela.</h1>
      <p class="reward-subtitle" style="text-align:center">Tu gusto es impecable. Esto es lo que viene para ti —</p>
      <div class="card-wrap">
        <div class="gift-for">Certificado de regalo para</div>
        <div class="gift-name">Daniela</div>
        <div class="gift-items">
          <div class="gift-item">
            <span class="gift-item-icon">🎵</span>
            <div class="gift-item-text"><strong>Tocadiscos</strong><span>Un set de vinilo completo, solo para ti</span></div>
          </div>
          <div class="gift-item">
            <span class="gift-item-icon">🔊</span>
            <div class="gift-item-text"><strong id="reward-speakers">—</strong><span>Tus parlantes elegidos</span></div>
          </div>
          <div class="gift-item">
            <span class="gift-item-icon">🪵</span>
            <div class="gift-item-text"><strong id="reward-furniture">—</strong><span>Tus muebles elegidos</span></div>
          </div>
        </div>
        <div class="card-footer">
          <div class="card-code">VINYL-DANIELA-2025</div>
          <div class="card-stamp">
            <span class="stamp-text">Canjeado</span>
            <span class="stamp-year">2025</span>
            <span class="stamp-text">con amor</span>
          </div>
        </div>
      </div>
      <div style="text-align:center">
        <button class="btn-primary" onclick="goToTwist()">Canjear mi regalo →</button>
        <br>
        <button class="btn-all-gifts" style="margin-top:0.75rem" onclick="openGiftModal()">Ver todos los regalos 🔗</button>
      </div>
    </div>
  </div><!-- end quiz-root -->

  <!-- ══ PART 2: TWIST ══ -->
  <div id="twist-screen">
    <div class="twist-lines"></div>
    <div class="twist-vinyl"></div>
    <span class="twist-emoji">😈</span>
    <h2 class="twist-title">¿Pensabas que sería<br><em>así de fácil?</em></h2>
    <p class="twist-sub">Elegiste bien... pero para recibir tus regalos<br>¡necesitás ganar un juego primero!</p>
    <button class="btn-twist" onclick="goToGame()">Acepto el desafío 🎮</button>
  </div>

  <!-- ══ PART 3: FLAPPY GAME ══ -->
  <div id="game-section">
    <div id="game-wrap">
      <div id="question-bar">Toca o presiona espacio para comenzar</div>
      <canvas id="gc" width="460" height="380"></canvas>
      <div id="feedback-banner"></div>
      <div id="score-bar">
        <span id="score-txt">Pregunta 1 de 3</span>
        <span id="lives-txt">❤️ ❤️ ❤️</span>
      </div>
      <div id="game-overlay">
        <h2>¡Último desafío!</h2>
        <p class="sub">Vuela hacia la respuesta correcta.<br>3 preguntas — ¡buena suerte!</p>
        <button class="gbtn" onclick="startGame()">¡Empezar! →</button>
      </div>
    </div>
    <div id="result-screen" style="display:none;background:#F5ECD7;border-radius:18px;padding:2rem 1.5rem;margin-top:0;"></div>
  </div>

</div><!-- end app -->

<!-- ══ GIFT LIST MODAL ══ -->
<div id="gift-modal-overlay" onclick="if(event.target===this)closeGiftModal()">
  <div id="gift-modal">
    <button class="gm-close" onclick="closeGiftModal()">✕</button>
    <div class="gm-title">Todos los regalos</div>
    <p class="gm-sub">Todas las opciones para que puedas revisarlas cuando quieras.</p>

    <div class="gm-section">
      <div class="gm-section-label">🎵 Tocadiscos</div>
      <div class="gm-item">
        <span class="gm-item-icon">🎵</span>
        <span class="gm-item-name">Tocadiscos + set de vinilo</span>
        <span class="gm-item-nolink">incluido</span>
      </div>
    </div>

    <div class="gm-section">
      <div class="gm-section-label">🔊 Parlantes</div>
      <div id="gm-speakers"></div>
    </div>

    <div class="gm-section">
      <div class="gm-section-label">🪵 Muebles</div>
      <div id="gm-furniture"></div>
    </div>
  </div>
</div>

<script>
/* ══════════════════════════════════════════════
   GIFT DATA — single source of truth
══════════════════════════════════════════════ */
const GIFT_DATA = {
  speakers: [
    { icon: '🔊', name: 'Edifier Mr3',               desc: 'Buena marca y se ve bien!', url: 'https://www.mercadolibre.com.ar/p/MLA46450496' },
    { icon: '🎛️', name: 'Edifier R1280T',            desc: 'Estos son mi recomndacion pero maybe you hate the color', url: 'https://www.mercadolibre.com.ar/p/MLA44709581' },
    { icon: '🎶', name: 'Edifier R1100',              desc: 'Por si quieres solo negros', url: 'https://www.mercadolibre.com.ar/p/MLA11913666' },
    { icon: '🎵', name: 'Parlantes Hypersound SP-X2', desc: 'Si me quieres ahorrar algunos pesitos', url: 'https://www.mercadolibre.com.ar/p/MLA20011733' },
  ],
  furniture: [
    { icon: '🪵', name: 'Rack de TV MT4000',    desc: 'Este me lo recomendó ML mientras veia tu wishlist', url: 'https://www.mercadolibre.com.ar/p/MLA23348633' },
    { icon: '📦', name: 'Rack Maximo Milan',     desc: 'en mi opinión, el mas interesante', url: 'https://www.mercadolibre.com.ar/up/MLAU3208494865' },
    { icon: '🌿', name: 'Mueble Rack Dielfe',   desc: 'si quieres algo mas simple', url: 'https://www.mercadolibre.com.ar/p/MLA47772582' },
    { icon: '🧱', name: 'Choose Your own!',     desc: 'Nadie tiene mejor gusto que tu!', url: null },
  ],
};

function renderQuizOptions() {
  function optionCard(q, g) {
    const nameHtml = g.url
      ? `<a href="${g.url}" target="_blank" onclick="event.stopPropagation()">${g.name}</a>`
      : g.name;
    return `<div class="option-card" data-q="${q}" data-name="${g.name}" onclick="qSelect(this.dataset.q,this,this.dataset.name)">
      <span class="opt-icon">${g.icon}</span>
      <div class="opt-name">${nameHtml}</div>
      <div class="opt-desc">${g.desc}</div>
    </div>`;
  }
  document.getElementById('q1-options').innerHTML = GIFT_DATA.speakers.map(g => optionCard('q1', g)).join('');
  document.getElementById('q2-options').innerHTML = GIFT_DATA.furniture.map(g => optionCard('q2', g)).join('');
}

function renderGiftModalSections() {
  function modalItem(g) {
    const linkHtml = g.url
      ? `<a class="gm-item-link" href="${g.url}" target="_blank">Ver →</a>`
      : `<span class="gm-item-nolink">próximamente</span>`;
    return `<div class="gm-item">
      <span class="gm-item-icon">${g.icon}</span>
      <span class="gm-item-name">${g.name}</span>
      ${linkHtml}
    </div>`;
  }
  document.getElementById('gm-speakers').innerHTML  = GIFT_DATA.speakers.map(modalItem).join('');
  document.getElementById('gm-furniture').innerHTML = GIFT_DATA.furniture.map(modalItem).join('');
}

/* ══════════════════════════════════════════════
   QUIZ LOGIC
══════════════════════════════════════════════ */
const qAnswers = { q1: null, q2: null };

function qGoTo(id) {
  document.querySelectorAll('.qscreen').forEach(s => s.classList.remove('active'));
  document.getElementById(id).classList.add('active');
}

function qSelect(q, el, value) {
  document.getElementById(q+'-options').querySelectorAll('.option-card').forEach(c => c.classList.remove('selected'));
  el.classList.add('selected');
  qAnswers[q] = value;
  const btn = document.getElementById(q+'-next');
  if (btn) btn.style.display = 'inline-block';
}

function qRestart() {
  qAnswers.q1 = null; qAnswers.q2 = null;
  document.querySelectorAll('.option-card').forEach(c => c.classList.remove('selected'));
  document.getElementById('q1-next').style.display = 'none';
  document.getElementById('q2-next').style.display = 'none';
  qGoTo('qscreen-intro');
}

function showConfirm() {
  document.getElementById('confirm-speakers').textContent = qAnswers.q1 || '—';
  document.getElementById('confirm-furniture').textContent = qAnswers.q2 || '—';
  qGoTo('qscreen-confirm');
}

function showFakeGiftCard() {
  document.getElementById('reward-speakers').textContent = qAnswers.q1 || '—';
  document.getElementById('reward-furniture').textContent = qAnswers.q2 || '—';
  qGoTo('qscreen-reward');
}
function goToTwist() {
  document.getElementById('quiz-root').classList.remove('active');
  const twist = document.getElementById('twist-screen');
  twist.classList.add('active');
  twist.style.display = 'block';
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function goToGame() {
  document.getElementById('twist-screen').style.display = 'none';
  document.getElementById('game-section').classList.add('active');
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

/* ══════════════════════════════════════════════
   FLAPPY GAME LOGIC
══════════════════════════════════════════════ */
const canvas = document.getElementById('gc');
const ctx = canvas.getContext('2d');
const W = 460, H = 380;

const ALL_QUESTIONS = [
  { text:"Pregunta 1: En el momento en el que estoy escribiendo esta pregunta, ¿cuántos mensajes hay en nuestro chat de telegram?", answers:[{label:"700mil",color:"#8B4513",correct:true},{label:"500mil",color:"#2C5F8B",correct:false}] },
  { text:"Pregunta 2: ¿Dónde fue nuestra pirmera selfie?", answers:[{label:"Grama",color:"#2C5F8B",correct:false},{label:"El Punto",color:"#3A8B2C",correct:true}] },
  { text:"Pregunta 3: ¿Qué palabra se ha dicho mas en nuestro chat?", answers:[{label:"Daniela",color:"#8B6A2C",correct:true},{label:"Marico",color:"#8B2C2C",correct:false}] },
  { text:"Pregunta 4: ¿Quién ha escrito más mensajes? (puntos extras si me dices el % de mensajes que escribio esa persona)", answers:[{label:"Eduardo",color:"#3A8B2C",correct:true},{label:"Daniela",color:"#8B4513",correct:false}] },
  { text:"Pregunta 5: ¿Quién grita mas?", answers:[{label:"Daniela",color:"#8B2C2C",correct:false},{label:"Eduardo",color:"#2C5F8B",correct:true}] },
  { text:"Pregunta 6: ¿Quién manda mas mensajes de 1 sola palabra?", answers:[{label:"Daniela",color:"#5A3A8B",correct:true},{label:"Eduardo",color:"#3A8B2C",correct:false}] },
  { text:"Pregunta 7: Tengo una lista de todas las palabras de nuestro chat, ¿qué nombre de hombre aparece más?", answers:[{label:"Eduardo",color:"#8B4513",correct:false},{label:"Rafael",color:"#8B6A2C",correct:true}] },
  { text:"Pregunta 8: La mayor cantidad de mensajes en 1 hora en el chat fue de 675, ¿qué evento marcó este hito?", answers:[{label:"TLOAS release",color:"#2C5F8B",correct:true},{label:"Manifesting NYC",color:"#8B2C2C",correct:false}] },
  { text:"Pregunta 9: El día que nos mandamos más mensajes, nos mandamos 2346 mensajes, ¿qué pasó ese día?", answers:[{label:"Eduardo emigró a NYC",color:"#3A8B2C",correct:true},{label:"Literalmente a random tuesday",color:"#5A3A8B",correct:false}] }
];

function pickRandom(arr, n) { return [...arr].sort(()=>Math.random()-0.5).slice(0,n); }

let gQuestions, bird, pipes, qIdx, lives, gameState, lastTime, rafId, gResults;

function initGame() {
  gQuestions = pickRandom(ALL_QUESTIONS, 3);
  gResults = [];
  bird = { x:80, y:H/2, vy:0, r:16 };
  pipes = [];
  qIdx = 0; lives = 3;
  gameState = 'waiting';
  lastTime = null;
  updateQBar(); updateHUD();
  spawnPipe();
  if (rafId) cancelAnimationFrame(rafId);
  rafId = requestAnimationFrame(gLoop);
}

function updateQBar(extra) {
  document.getElementById('question-bar').textContent =
    gQuestions[Math.min(qIdx, gQuestions.length-1)].text + (extra||'');
}
function updateHUD() {
  document.getElementById('score-txt').textContent = `Pregunta ${Math.min(qIdx+1,gQuestions.length)} de ${gQuestions.length}`;
  document.getElementById('lives-txt').textContent = Array(3).fill(null).map((_,i)=>i<lives?'❤️':'🖤').join(' ');
}

function measureBox(label, font, maxW) {
  ctx.save(); ctx.font = font;
  const words = label.split(' ');
  const lines = []; let cur = '';
  for (const w of words) {
    const test = cur ? cur+' '+w : w;
    if (ctx.measureText(test).width > maxW - 16) { if(cur) lines.push(cur); cur = w; }
    else cur = test;
  }
  if (cur) lines.push(cur);
  const lineH = 15;
  const textW = Math.max(...lines.map(l => ctx.measureText(l).width));
  ctx.restore();
  return { lines, w: Math.max(80, textW + 24), h: Math.max(44, lines.length * lineH + 20) };
}

function spawnPipe() {
  const q = gQuestions[qIdx];
  const font = 'bold 12px Georgia';
  const m0 = measureBox(q.answers[0].label, font, 160);
  const m1 = measureBox(q.answers[1].label, font, 160);
  const w = Math.max(m0.w, m1.w);
  const h0 = m0.h, h1 = m1.h;
  const topY = 60 + Math.random()*70;
  const gap = 60;
  pipes.push({ x:W+10, topY, botY:topY + Math.max(h0,h1) + gap + Math.max(h0,h1), w, h0, h1, gap, answered:false, answers:q.answers, hit:null, lines0:m0.lines, lines1:m1.lines });
}

function gFlap() {
  if (gameState==='waiting') { gameState='playing'; updateQBar(); }
  if (gameState!=='playing') return;
  bird.vy = -7;
}
canvas.addEventListener('click', gFlap);
canvas.addEventListener('touchstart', e=>{ e.preventDefault(); gFlap(); }, {passive:false});
document.addEventListener('keydown', e=>{ if(e.code==='Space'){ e.preventDefault(); gFlap(); } });

function gLoop(ts) {
  if (gameState==='over'||gameState==='won') { gDraw(); return; }
  const dt = lastTime ? Math.min((ts-lastTime)/16,3) : 1;
  lastTime = ts;
  if (gameState==='playing') gUpdate(dt);
  gDraw();
  rafId = requestAnimationFrame(gLoop);
}

function gUpdate(dt) {
  bird.vy += 0.38*dt; bird.y += bird.vy*dt;
  if (bird.y-bird.r<0) { bird.y=bird.r; bird.vy=0; }
  if (bird.y+bird.r>H) { onGround(); return; }
  for (let p of pipes) {
    p.x -= 2.2*dt;
    if (!p.answered) {
      if (rCircle(p.x,p.topY,p.w,p.h0,bird.x,bird.y,bird.r)) { p.answered=true; p.hit='top'; onAnswer(p.answers[0]); return; }
      if (rCircle(p.x,p.topY+p.h0+p.gap,p.w,p.h1,bird.x,bird.y,bird.r)) { p.answered=true; p.hit='bot'; onAnswer(p.answers[1]); return; }
    }
  }
  pipes = pipes.filter(p=>p.x+p.w>-10);
}

function rCircle(rx,ry,rw,rh,cx,cy,cr) {
  const nx=Math.max(rx,Math.min(cx,rx+rw)), ny=Math.max(ry,Math.min(cy,ry+rh));
  const dx=cx-nx, dy=cy-ny; return dx*dx+dy*dy<cr*cr;
}

function showFeedback(correct) {
  const el = document.getElementById('feedback-banner');
  el.textContent = correct ? '✓ ¡Correcto!' : '✗ Incorrecto';
  el.className = 'show '+(correct?'correct':'wrong');
  setTimeout(()=>{ el.className=''; }, 1100);
}

function onAnswer(answer) {
  gameState='pause';
  showFeedback(answer.correct);
  gResults.push({ question:gQuestions[qIdx], correct:answer.correct });
  setTimeout(advance, 1200);
}

function onGround() {
  if (gameState!=='playing') return;
  gameState='pause';
  showFeedback(false);
  gResults.push({ question:gQuestions[qIdx], correct:false });
  lives = Math.max(0, lives-1);
  updateHUD();
  setTimeout(advance, 1200);
}

function advance() {
  qIdx++;
  if (qIdx>=gQuestions.length) { gameState='done'; showResultScreen(); return; }
  pipes=[]; bird.y=H/2; bird.vy=-3;
  spawnPipe(); gameState='waiting';
  updateHUD(); updateQBar(' — ¡Toca para continuar!');
  lastTime=null; rafId=requestAnimationFrame(gLoop);
}

function showResultScreen() {
  const anyWrong = gResults.some(r=>!r.correct);
  const allCorrect = gResults.every(r=>r.correct);

  // Hide the game UI entirely
  document.getElementById('game-wrap').style.display = 'none';

  // The real gifts are the quiz selections — map question index to the actual gift
  const realGifts = [
    { icon: '🎵', name: 'Tocadiscos',        desc: 'Un set de vinilo completo, solo para ti' },
    { icon: '🔊', name: qAnswers.q1 || '—',  desc: 'Tus parlantes elegidos' },
    { icon: '🪵', name: qAnswers.q2 || '—',  desc: 'Tu mueble elegido' },
  ];

  const giftRows = gResults.map((r, i) => {
    const g = realGifts[i] || realGifts[realGifts.length - 1];
    return r.correct
      ? `<div class="fgift-row"><span class="fgift-icon">${g.icon}</span><div class="fgift-text"><strong>${g.name}</strong><span>${g.desc}</span></div></div>`
      : `<div class="fgift-row failed"><span class="fgift-icon" style="opacity:0.4">${g.icon}</span><div class="fgift-text"><strong>${g.name}</strong><span>${g.desc}</span></div><div class="fail-badge">✕</div></div>`;
  }).join('<hr class="fcard-divider">');

  const retryBlock = anyWrong ? `
    <div class="retry-msg">¿Querés más regalos? Intentá respondiendo nuevas preguntas 🎁</div>
    <div class="gbtn-row">
      <button class="gbtn" onclick="startGame()">¡Nuevas preguntas! →</button>
    </div>` : `<div class="gbtn-row"><button class="gbtn" onclick="startGame()">Jugar de nuevo →</button></div>`;

  const heading = allCorrect ? '🎉 ¡Lo lograste todo!' : '🎶 ¡Aquí está tu resultado!';

  const rs = document.getElementById('result-screen');
  rs.innerHTML = `
    <div class="confetti-row" style="text-align:center;margin-bottom:1rem">${allCorrect ? '🎉 🎶 🎁' : '🎶 🎁'}</div>
    <h2 style="font-family:'Playfair Display',serif;font-size:1.4rem;color:#1C0F05;text-align:center;margin-bottom:1.2rem">${heading}</h2>
    <div class="fcard-wrap">
      <div class="fcard-for">Certificado de regalo para</div>
      <div class="fcard-name">Daniela</div>
      <div style="border-top:1px dashed #C4A87A;padding-top:0.8rem">${giftRows}</div>
      <hr class="fcard-divider">
      <div class="fcard-footer">
        <div class="fcard-code">VINYL-DANIELA-2025</div>
        <div class="fcard-stamp"><span class="fstamp-sm">Canjeado</span><span class="fstamp-yr">2025</span><span class="fstamp-sm">con amor</span></div>
      </div>
    </div>
    ${retryBlock}
    <div style="text-align:center;margin-top:0.75rem">
      <button class="btn-all-gifts" onclick="openGiftModal()">Ver todos los regalos 🔗</button>
    </div>`;
  rs.style.display = 'block';
  window.scrollTo({ top: 0, behavior: 'smooth' });
}

function startGame() {
  document.getElementById('result-screen').style.display = 'none';
  document.getElementById('game-wrap').style.display = 'block';
  document.getElementById('game-overlay').style.display = 'none';
  initGame();
}

/* ── DRAWING ── */
function gDraw() {
  ctx.clearRect(0,0,W,H);
  ctx.fillStyle='#C8E6F0'; ctx.fillRect(0,0,W,H);
  drawCloud(70,55,0.7); drawCloud(240,38,0.9); drawCloud(380,75,0.6);
  ctx.fillStyle='#8B7355'; ctx.fillRect(0,H-24,W,24);
  ctx.fillStyle='#6B5B45'; ctx.fillRect(0,H-24,W,4);

  if (gameState==='waiting') {
    ctx.save(); ctx.fillStyle='rgba(44,26,14,0.55)';
    ctx.font='13px Lora,Georgia,serif'; ctx.textAlign='center';
    ctx.fillText('↑ toca para volar', bird.x, bird.y-28); ctx.restore();
  }

  for (let p of pipes) {
    ctx.fillStyle='#5A8A3A';
    ctx.fillRect(p.x+p.w/2-8, p.topY+p.h0, 16, p.gap);
    drawBox(p.x, p.topY, p.w, p.h0, p.answers[0], p.answered&&p.hit==='top', p.lines0);
    drawBox(p.x, p.topY+p.h0+p.gap, p.w, p.h1, p.answers[1], p.answered&&p.hit==='bot', p.lines1);
  }
  drawBird(bird.x, bird.y, bird.vy);
}

function drawBox(x,y,w,h,answer,hit,lines) {
  ctx.save();
  ctx.fillStyle = hit ? '#FFD700' : answer.color;
  rr(x,y,w,h,10); ctx.fill();
  ctx.strokeStyle = hit ? '#B8860B' : 'rgba(0,0,0,0.2)';
  ctx.lineWidth=2; ctx.stroke();
  ctx.fillStyle='#fff'; ctx.font='bold 12px Georgia'; ctx.textAlign='center'; ctx.textBaseline='middle';
  const lineH = 15;
  const startY = y + h/2 - (lines.length-1)*lineH/2;
  for (let i=0; i<lines.length; i++) ctx.fillText(lines[i], x+w/2, startY + i*lineH);
  ctx.restore();
}

function drawBird(x,y,vy) {
  ctx.save(); ctx.translate(x,y); ctx.rotate(Math.max(-0.4,Math.min(0.6,vy*0.06)));
  ctx.fillStyle='#F5C842'; ctx.beginPath(); ctx.ellipse(0,0,16,13,0,0,Math.PI*2); ctx.fill();
  ctx.strokeStyle='#C8972A'; ctx.lineWidth=1.5; ctx.stroke();
  ctx.fillStyle='#E8B030'; ctx.beginPath(); ctx.ellipse(-4,3,9,5,-0.3,0,Math.PI*2); ctx.fill();
  ctx.fillStyle='#1C0F05'; ctx.beginPath(); ctx.arc(7,-3,3,0,Math.PI*2); ctx.fill();
  ctx.fillStyle='#fff'; ctx.beginPath(); ctx.arc(8,-4,1.2,0,Math.PI*2); ctx.fill();
  ctx.fillStyle='#E05A00'; ctx.beginPath(); ctx.moveTo(13,-1); ctx.lineTo(20,1); ctx.lineTo(13,3); ctx.closePath(); ctx.fill();
  ctx.restore();
}

function drawCloud(x,y,s) {
  ctx.save(); ctx.translate(x,y); ctx.scale(s,s);
  ctx.fillStyle='rgba(255,255,255,0.78)';
  ctx.beginPath(); ctx.arc(0,0,20,0,Math.PI*2); ctx.arc(22,-5,16,0,Math.PI*2); ctx.arc(40,0,18,0,Math.PI*2); ctx.arc(20,8,15,0,Math.PI*2);
  ctx.fill(); ctx.restore();
}

function rr(x,y,w,h,r) {
  ctx.beginPath(); ctx.moveTo(x+r,y); ctx.lineTo(x+w-r,y); ctx.quadraticCurveTo(x+w,y,x+w,y+r);
  ctx.lineTo(x+w,y+h-r); ctx.quadraticCurveTo(x+w,y+h,x+w-r,y+h);
  ctx.lineTo(x+r,y+h); ctx.quadraticCurveTo(x,y+h,x,y+h-r);
  ctx.lineTo(x,y+r); ctx.quadraticCurveTo(x,y,x+r,y); ctx.closePath();
}

/* ── Init ── */
renderQuizOptions();
renderGiftModalSections();

gDraw();

/* ── GIFT LIST MODAL ── */
function openGiftModal() {
  document.getElementById('gift-modal-overlay').classList.add('open');
}
function closeGiftModal() {
  document.getElementById('gift-modal-overlay').classList.remove('open');
}
document.addEventListener('keydown', e => { if (e.key === 'Escape') closeGiftModal(); });
</script>
</body>
</html>
