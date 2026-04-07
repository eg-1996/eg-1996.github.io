
<style>
  @import url('https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,600;1,400&family=Lora:ital,wght@0,400;0,500;1,400&display=swap');

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body, .quiz-root {
    font-family: 'Lora', Georgia, serif;
    color: #2C1A0E;
  }

  .quiz-root {
    min-height: 520px;
    background: #F5ECD7;
    border-radius: 16px;
    position: relative;
    overflow: hidden;
    padding: 0;
  }

  .grain {
    position: absolute; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.08'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 0;
    opacity: 0.5;
  }

  .screen { display: none; position: relative; z-index: 1; padding: 2.5rem 2rem; animation: fadeIn 0.5s ease; }
  .screen.active { display: block; }

  @keyframes fadeIn { from { opacity: 0; transform: translateY(12px); } to { opacity: 1; transform: translateY(0); } }

  .badge {
    display: inline-block;
    font-family: 'Lora', serif;
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    color: #8B4513;
    background: #E8D5B0;
    border: 1px solid #C4A87A;
    border-radius: 20px;
    padding: 4px 14px;
    margin-bottom: 1.2rem;
  }

  h1.title {
    font-family: 'Playfair Display', Georgia, serif;
    font-size: 2rem;
    font-weight: 600;
    color: #1C0F05;
    line-height: 1.25;
    margin-bottom: 0.5rem;
  }

  h1.title em { font-style: italic; color: #8B4513; }

  .subtitle {
    font-size: 0.95rem;
    color: #6B4423;
    line-height: 1.7;
    margin-bottom: 2rem;
    font-style: italic;
  }

  .vinyl-icon {
    width: 56px; height: 56px;
    margin: 0 auto 1.5rem;
    display: block;
  }

  .btn-primary {
    display: inline-block;
    background: #8B4513;
    color: #F5ECD7;
    font-family: 'Lora', serif;
    font-size: 0.95rem;
    font-weight: 500;
    padding: 12px 32px;
    border-radius: 40px;
    border: none;
    cursor: pointer;
    letter-spacing: 0.04em;
    transition: background 0.2s, transform 0.1s;
    margin-top: 0.5rem;
  }
  .btn-primary:hover { background: #6B3410; }
  .btn-primary:active { transform: scale(0.97); }

  .question-label {
    font-family: 'Playfair Display', serif;
    font-size: 1.35rem;
    font-weight: 600;
    color: #1C0F05;
    margin-bottom: 0.4rem;
    line-height: 1.35;
  }

  .question-sub {
    font-size: 0.88rem;
    color: #8B6A4A;
    font-style: italic;
    margin-bottom: 1.6rem;
  }

  .options-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
    margin-bottom: 1.8rem;
  }

  .option-card {
    background: #FDF6E8;
    border: 1.5px solid #D4B896;
    border-radius: 12px;
    padding: 1rem 0.9rem;
    cursor: pointer;
    transition: all 0.18s;
    text-align: left;
    font-family: 'Lora', serif;
  }
  .option-card:hover { border-color: #8B4513; background: #FFF8EE; }
  .option-card.selected { border-color: #8B4513; background: #8B4513; color: #F5ECD7; }
  .option-card.selected .opt-name { color: #F5ECD7; }
  .option-card.selected .opt-desc { color: #F0D9C0; }

  .opt-icon { font-size: 22px; margin-bottom: 6px; display: block; }
  .opt-name { font-size: 0.9rem; font-weight: 500; color: #1C0F05; margin-bottom: 2px; }
  .opt-desc { font-size: 0.78rem; color: #8B6A4A; line-height: 1.45; font-style: italic; }

  .progress-bar {
    display: flex; gap: 6px; margin-bottom: 1.8rem;
  }
  .prog-dot {
    height: 4px; border-radius: 4px; flex: 1;
    background: #D4B896;
    transition: background 0.3s;
  }
  .prog-dot.done { background: #8B4513; }

  .btn-back {
    background: none;
    border: 1.5px solid #8B4513;
    color: #1C0F05;
    font-family: 'Lora', serif;
    font-size: 0.88rem;
    cursor: pointer;
    padding: 10px 20px;
    border-radius: 40px;
    font-style: italic;
    margin-right: 0.75rem;
    transition: background 0.18s, color 0.18s;
  }
  .btn-back:hover { background: #E8D5B0; color: #1C0F05; }

  .btn-row { display: flex; align-items: center; margin-top: 0.5rem; }

  .card-wrap {
    background: #FDF6E8;
    border: 1.5px solid #C4A87A;
    border-radius: 14px;
    padding: 1.8rem 1.6rem;
    position: relative;
    overflow: hidden;
    margin-bottom: 1.5rem;
  }
  .card-wrap::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 6px;
    background: repeating-linear-gradient(90deg, #8B4513 0, #8B4513 20px, #C4A87A 20px, #C4A87A 40px);
  }

  .gift-for { font-size: 0.78rem; text-transform: uppercase; letter-spacing: 0.15em; color: #8B6A4A; margin-bottom: 0.3rem; margin-top: 0.5rem; }
  .gift-name { font-family: 'Playfair Display', serif; font-size: 2.2rem; font-weight: 600; color: #1C0F05; font-style: italic; line-height: 1.1; margin-bottom: 1.2rem; }

  .gift-items { border-top: 1px dashed #C4A87A; padding-top: 1rem; }
  .gift-item { display: flex; align-items: flex-start; gap: 10px; margin-bottom: 0.75rem; }
  .gift-item-icon { font-size: 18px; margin-top: 1px; }
  .gift-item-text { font-size: 0.88rem; color: #2C1A0E; line-height: 1.5; }
  .gift-item-text strong { display: block; font-weight: 500; color: #1C0F05; }
  .gift-item-text span { color: #6B4423; font-style: italic; }

  .card-footer { display: flex; justify-content: space-between; align-items: flex-end; margin-top: 1.2rem; padding-top: 1rem; border-top: 1px dashed #C4A87A; }
  .card-code { font-size: 0.75rem; letter-spacing: 0.18em; color: #8B4513; font-family: 'Courier New', monospace; }
  .card-stamp {
    width: 52px; height: 52px; border-radius: 50%;
    border: 2px solid #8B4513;
    display: flex; align-items: center; justify-content: center;
    flex-direction: column;
  }
  .stamp-text { font-size: 7px; text-transform: uppercase; letter-spacing: 0.08em; color: #8B4513; font-family: 'Lora', serif; }
  .stamp-year { font-size: 11px; font-weight: 600; color: #8B4513; font-family: 'Playfair Display', serif; }

  .confetti-row { font-size: 22px; letter-spacing: 4px; margin-bottom: 0.8rem; }

  .reward-subtitle { font-size: 0.88rem; color: #6B4423; font-style: italic; line-height: 1.7; margin-bottom: 1.5rem; }

  .deco-vinyl {
    position: absolute; right: -28px; top: -28px;
    width: 110px; height: 110px;
    border-radius: 50%;
    background: radial-gradient(circle at 50%, #3D1F0A 28%, #2C1A0E 29%, #2C1A0E 44%, #8B4513 45%, #8B4513 46%, #2C1A0E 47%, #2C1A0E 100%);
    opacity: 0.13;
    z-index: 0;
  }
</style>

<div class="quiz-root">
  <div class="grain"></div>
  <div class="deco-vinyl"></div>

  <div class="screen active" id="screen-intro">
    <div style="text-align:center; padding-top:0.5rem;">
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
      <p class="subtitle" style="max-width:320px;margin:0.5rem auto 2rem;">Algo especial te espera.<br>Responde dos preguntas rápidas para reclamarlo.</p>
      <button class="btn-primary" onclick="goTo('screen-q1')">Abre tu regalo →</button>
    </div>
  </div>

  <div class="screen" id="screen-q1">
    <div class="progress-bar">
      <div class="prog-dot done"></div>
      <div class="prog-dot"></div>
    </div>
    <div class="badge">Pregunta 1 de 2</div>
    <p class="question-label">Elige tus parlantes.</p>
    <p class="question-sub">¿Qué par habla a tu alma?</p>
    <div class="options-grid" id="q1-options">
      <div class="option-card" onclick="selectOption('q1', this, 'Edifier Mr3')">
        <span class="opt-icon">🔊</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/p/MLA46450496" target="_blank">Edifier Mr3</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
      <div class="option-card" onclick="selectOption('q1', this, 'Edifier R1280T')">
        <span class="opt-icon">🎛️</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/p/MLA44709581" target="_blank">Edifier R1280T</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
      <div class="option-card" onclick="selectOption('q1', this, 'Edifier R1100')">
        <span class="opt-icon">🎶</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/p/MLA11913666" target="_blank">Edifier R1100</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
      <div class="option-card" onclick="selectOption('q1', this, 'KEF Q150')">
        <span class="opt-icon">🎵</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/p/MLA20011733" target="_blank">Parlantes Hypersound SP-X2</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
    </div>
    <div class="btn-row">
      <button class="btn-back" onclick="goTo('screen-intro')">← Atrás</button>
      <button class="btn-primary" id="q1-next" onclick="goTo('screen-q2')" style="display:none">Siguiente →</button>
    </div>
  </div>

  <div class="screen" id="screen-q2">
    <div class="progress-bar">
      <div class="prog-dot done"></div>
      <div class="prog-dot done"></div>
    </div>
    <div class="badge">Pregunta 2 de 2</div>
    <p class="question-label">Elige tus muebles.</p>
    <p class="question-sub">¿Dónde vivirá tu equipo?</p>
    <div class="options-grid" id="q2-options">
      <div class="option-card" onclick="selectOption('q2', this, 'Rack de TV MT4000')">
        <span class="opt-icon">🪵</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/p/MLA23348633" target="_blank">Rack de TV MT4000</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
      <div class="option-card" onclick="selectOption('q2', this, 'Mesa Para Tv Rack Maximo Milan')">
        <span class="opt-icon">📦</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/up/MLAU3208494865" target="_blank">Mesa Para Tv Rack Maximo Milan</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
      <div class="option-card" onclick="selectOption('q2', this, 'Mueble De Tv Rack Dielfe')">
        <span class="opt-icon">🌿</span>
        <div class="opt-name"><a href="https://www.mercadolibre.com.ar/p/MLA47772582" target="_blank">Mueble De Tv Rack Dielfe</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
      <div class="option-card" onclick="selectOption('q2', this, 'Estante de pared flotante personalizado')">
        <span class="opt-icon">🧱</span>
        <div class="opt-name"><a href="javascript:void(0)" target="_blank">TBD</a></div>
        <div class="opt-desc">Description TBD</div>
      </div>
    </div>
    <div class="btn-row">
      <button class="btn-back" onclick="goTo('screen-q1')">← Atrás</button>
      <button class="btn-primary" id="q2-next" onclick="revealGift()" style="display:none">Reclama mi regalo 🎁</button>
    </div>
  </div>

  <div class="screen" id="screen-reward">
    <div class="confetti-row" style="text-align:center">🎉 🎶 🎁</div>
    <h1 class="title" style="text-align:center;margin-bottom:0.3rem;">Es tuyo, Daniela.</h1>
    <p class="reward-subtitle" style="text-align:center">Tu gusto es impecable. Esto es lo que viene para ti —</p>

    <div class="card-wrap">
      <div class="gift-for">Certificado de regalo para</div>
      <div class="gift-name">Daniela</div>
      <div class="gift-items">
        <div class="gift-item">
          <span class="gift-item-icon">🎵</span>
          <div class="gift-item-text">
            <strong>Tocadiscos</strong>
            <span>Un set de vinilo completo, solo para ti</span>
          </div>
        </div>
        <div class="gift-item">
          <span class="gift-item-icon">🔊</span>
          <div class="gift-item-text">
            <strong id="reward-speakers">—</strong>
            <span>Tus parlantes elegidos</span>
          </div>
        </div>
        <div class="gift-item">
          <span class="gift-item-icon">🪵</span>
          <div class="gift-item-text">
            <strong id="reward-furniture">—</strong>
            <span>Tus muebles elegidos</span>
          </div>
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

    <p style="text-align:center; font-size:0.82rem; color:#8B6A4A; font-style:italic;">Muestra esta pantalla para canjear tu regalo 🎶</p>
  </div>
</div>

<script>
  const answers = { q1: null, q2: null };

  function goTo(id) {
    document.querySelectorAll('.screen').forEach(s => s.classList.remove('active'));
    document.getElementById(id).classList.add('active');
  }

  function selectOption(q, el, value) {
    const container = document.getElementById(q + '-options');
    container.querySelectorAll('.option-card').forEach(c => c.classList.remove('selected'));
    el.classList.add('selected');
    answers[q] = value;
    const btn = document.getElementById(q + '-next');
    if (btn) btn.style.display = 'inline-block';
  }

  function revealGift() {
    document.getElementById('reward-speakers').textContent = answers.q1 || '—';
    document.getElementById('reward-furniture').textContent = answers.q2 || '—';
    goTo('screen-reward');
  }
</script>
