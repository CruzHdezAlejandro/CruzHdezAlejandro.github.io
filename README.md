<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>¿Estás Desconectado de la Realidad? | ScrollTrap</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=DM+Sans:wght@300;400;500&family=Playfair+Display:ital,wght@1,700&display=swap" rel="stylesheet" />
  <style>
    :root {
      --rojo-vivo:   #E22227;
      --rojo-medio:  #C7080C;
      --rojo-oscuro: #6C0102;
      --rojo-negro:  #440101;
      --gris-oscuro: #222B31;
      --gris-medio:  #55666E;
      --blanco:      #F5F0EB;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background-color: var(--gris-oscuro);
      color: var(--blanco);
      font-family: 'DM Sans', sans-serif;
      overflow-x: hidden;
      cursor: crosshair;
    }

    /* ─── GRAIN OVERLAY ─── */
    body::before {
      content: '';
      position: fixed; inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 9999;
      opacity: 0.35;
    }

    /* ─── NAV ─── */
    nav {
      position: fixed; top: 0; left: 0; right: 0;
      z-index: 100;
      display: flex; align-items: center; justify-content: space-between;
      padding: 1.2rem 3rem;
      background: linear-gradient(to bottom, rgba(34,43,49,0.95), transparent);
      backdrop-filter: blur(4px);
    }
    .logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 4px;
      color: var(--rojo-vivo);
    }
    .logo span { color: var(--blanco); }
    nav a {
      color: var(--gris-medio);
      text-decoration: none;
      font-size: 0.8rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      transition: color 0.3s;
    }
    nav a:hover { color: var(--rojo-vivo); }

    /* ─── HERO ─── */
    #inicio {
      min-height: 100vh;
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 1fr;
      position: relative;
      overflow: hidden;
    }

    .hero-left {
      grid-column: 1;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding: 8rem 4rem 4rem 6rem;
      position: relative;
      z-index: 2;
    }

    .hero-eyebrow {
      font-size: 0.7rem;
      letter-spacing: 5px;
      text-transform: uppercase;
      color: var(--rojo-vivo);
      margin-bottom: 1.5rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.3s forwards;
    }

    .hero-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(4rem, 7vw, 7rem);
      line-height: 0.95;
      letter-spacing: 2px;
      color: var(--blanco);
      opacity: 0;
      animation: fadeUp 0.8s 0.5s forwards;
    }
    .hero-title .accent {
      color: var(--rojo-vivo);
      font-family: 'Playfair Display', serif;
      font-style: italic;
      display: block;
    }

    .hero-sub {
      margin-top: 2rem;
      font-size: 1rem;
      line-height: 1.7;
      color: var(--gris-medio);
      max-width: 420px;
      opacity: 0;
      animation: fadeUp 0.8s 0.7s forwards;
    }

    .hero-cta-group {
      margin-top: 3rem;
      display: flex;
      gap: 1.2rem;
      align-items: center;
      opacity: 0;
      animation: fadeUp 0.8s 0.9s forwards;
    }

    .btn-primary {
      background: var(--rojo-vivo);
      color: var(--blanco);
      font-family: 'DM Sans', sans-serif;
      font-weight: 500;
      font-size: 0.8rem;
      letter-spacing: 3px;
      text-transform: uppercase;
      text-decoration: none;
      padding: 1rem 2.5rem;
      border: none;
      position: relative;
      overflow: hidden;
      transition: background 0.3s, transform 0.2s;
      clip-path: polygon(0 0, calc(100% - 12px) 0, 100% 12px, 100% 100%, 12px 100%, 0 calc(100% - 12px));
    }
    .btn-primary:hover {
      background: var(--rojo-medio);
      transform: translateY(-2px);
    }

    .btn-secondary {
      color: var(--gris-medio);
      font-size: 0.8rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      text-decoration: none;
      border-bottom: 1px solid var(--rojo-oscuro);
      padding-bottom: 2px;
      transition: color 0.3s, border-color 0.3s;
    }
    .btn-secondary:hover { color: var(--blanco); border-color: var(--rojo-vivo); }

    /* ─── HERO RIGHT: PHONE MOCKUP ─── */
    .hero-right {
      grid-column: 2;
      display: flex;
      align-items: center;
      justify-content: center;
      padding: 8rem 4rem 4rem 2rem;
      position: relative;
    }

    .phone-wrapper {
      position: relative;
      opacity: 0;
      animation: fadeUp 1s 1s forwards;
    }

    .phone {
      width: 220px;
      height: 440px;
      background: var(--rojo-negro);
      border-radius: 36px;
      border: 3px solid var(--rojo-oscuro);
      display: flex;
      flex-direction: column;
      overflow: hidden;
      position: relative;
      box-shadow: 0 0 80px rgba(226,34,39,0.25), 0 0 200px rgba(68,1,1,0.3);
    }

    .phone-notch {
      width: 80px; height: 22px;
      background: var(--gris-oscuro);
      border-radius: 0 0 14px 14px;
      margin: 0 auto;
    }

    .phone-screen {
      flex: 1;
      padding: 0.8rem;
      display: flex;
      flex-direction: column;
      gap: 0.5rem;
      overflow: hidden;
    }

    .feed-item {
      background: var(--rojo-oscuro);
      border-radius: 8px;
      height: 70px;
      animation: pulse 2s infinite alternate;
      position: relative;
      overflow: hidden;
    }
    .feed-item::after {
      content: '';
      position: absolute;
      inset: 0;
      background: linear-gradient(135deg, transparent 60%, rgba(226,34,39,0.2));
    }
    .feed-item:nth-child(2) { height: 50px; animation-delay: 0.4s; }
    .feed-item:nth-child(3) { height: 90px; animation-delay: 0.8s; }
    .feed-item:nth-child(4) { height: 45px; animation-delay: 1.2s; }

    .phone-bar {
      width: 60px; height: 5px;
      background: var(--gris-medio);
      border-radius: 3px;
      margin: 0.8rem auto;
      opacity: 0.5;
    }

    /* Glitch lines floating around phone */
    .glitch-line {
      position: absolute;
      background: var(--rojo-vivo);
      opacity: 0.6;
      animation: glitchFloat 3s infinite;
    }
    .glitch-line:nth-child(1) { width: 60px; height: 2px; top: 30%; left: -30px; animation-delay: 0s; }
    .glitch-line:nth-child(2) { width: 40px; height: 1px; top: 50%; right: -20px; animation-delay: 1s; opacity: 0.4; }
    .glitch-line:nth-child(3) { width: 80px; height: 1px; bottom: 30%; left: -40px; animation-delay: 2s; }

    /* Hour counter */
    .counter-badge {
      position: absolute;
      top: -20px; right: -30px;
      background: var(--rojo-vivo);
      color: var(--blanco);
      font-family: 'Bebas Neue', sans-serif;
      font-size: 2.5rem;
      width: 90px; height: 90px;
      border-radius: 50%;
      display: flex;
      flex-direction: column;
      align-items: center;
      justify-content: center;
      line-height: 1;
      box-shadow: 0 0 30px rgba(226,34,39,0.5);
    }
    .counter-badge small {
      font-family: 'DM Sans', sans-serif;
      font-size: 0.5rem;
      letter-spacing: 1px;
      text-transform: uppercase;
      opacity: 0.85;
    }

    /* ─── DIVIDER ─── */
    .divider {
      height: 4px;
      background: linear-gradient(to right, var(--rojo-negro), var(--rojo-vivo), var(--rojo-negro));
    }

    /* ─── STATS STRIP ─── */
    .stats-strip {
      background: var(--rojo-negro);
      display: flex;
      justify-content: center;
      gap: 0;
    }
    .stat-block {
      flex: 1;
      max-width: 280px;
      text-align: center;
      padding: 3rem 2rem;
      border-right: 1px solid rgba(108,1,2,0.4);
    }
    .stat-block:last-child { border-right: none; }
    .stat-number {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 3.5rem;
      color: var(--rojo-vivo);
      line-height: 1;
    }
    .stat-label {
      font-size: 0.75rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--gris-medio);
      margin-top: 0.5rem;
    }

    /* ─── EFECTOS SECTION ─── */
    #efectos {
      padding: 8rem 6rem;
      position: relative;
      overflow: hidden;
    }

    #efectos::before {
      content: 'ALERTA';
      position: absolute;
      font-family: 'Bebas Neue', sans-serif;
      font-size: 20vw;
      color: transparent;
      -webkit-text-stroke: 1px rgba(108,1,2,0.12);
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      pointer-events: none;
      white-space: nowrap;
    }

    .section-header {
      display: grid;
      grid-template-columns: auto 1fr;
      gap: 2rem;
      align-items: end;
      margin-bottom: 5rem;
    }
    .section-number {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 5rem;
      color: var(--rojo-oscuro);
      line-height: 1;
    }
    .section-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(2.5rem, 4vw, 4rem);
      letter-spacing: 1px;
      color: var(--blanco);
      line-height: 1;
      padding-bottom: 1rem;
      border-bottom: 2px solid var(--rojo-oscuro);
    }
    .section-title em {
      color: var(--rojo-vivo);
      font-style: normal;
    }

    /* Effects grid - rule of thirds inspired */
    .effects-grid {
      display: grid;
      grid-template-columns: 2fr 1fr 1fr;
      grid-template-rows: auto auto;
      gap: 1.5px;
    }

    .effect-card {
      background: var(--rojo-negro);
      padding: 2.5rem;
      position: relative;
      overflow: hidden;
      transition: background 0.4s;
    }
    .effect-card:hover { background: #550102; }
    .effect-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0;
      width: 3px;
      height: 0;
      background: var(--rojo-vivo);
      transition: height 0.4s;
    }
    .effect-card:hover::before { height: 100%; }

    .effect-card.featured {
      grid-row: span 2;
      display: flex;
      flex-direction: column;
      justify-content: center;
      min-height: 400px;
      background: linear-gradient(to top, var(--rojo-negro) 40%, rgba(108,1,2,0.6));
      position: relative;
    }
    .effect-card.featured::after {
      content: '⚠';
      position: absolute;
      top: 2rem; right: 2rem;
      font-size: 3rem;
      opacity: 0.15;
    }

    .effect-icon {
      font-size: 2rem;
      margin-bottom: 1rem;
      display: block;
    }
    .effect-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.6rem;
      letter-spacing: 1px;
      color: var(--blanco);
      margin-bottom: 0.8rem;
    }
    .effect-desc {
      font-size: 0.85rem;
      line-height: 1.65;
      color: var(--gris-medio);
    }
    .effect-tag {
      display: inline-block;
      margin-top: 1rem;
      font-size: 0.65rem;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--rojo-vivo);
      border: 1px solid var(--rojo-oscuro);
      padding: 0.25rem 0.6rem;
    }

    /* ─── CTA SECTION ─── */
    #accion {
      background: linear-gradient(135deg, var(--rojo-negro) 0%, #350000 50%, var(--gris-oscuro) 100%);
      padding: 10rem 6rem;
      display: grid;
      grid-template-columns: 1.2fr 1fr;
      gap: 6rem;
      align-items: center;
      position: relative;
      overflow: hidden;
    }

    #accion::before {
      content: '';
      position: absolute;
      width: 600px; height: 600px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(226,34,39,0.12), transparent 70%);
      right: -100px; top: -100px;
      pointer-events: none;
    }

    .cta-eyebrow {
      font-size: 0.7rem;
      letter-spacing: 5px;
      text-transform: uppercase;
      color: var(--rojo-vivo);
      margin-bottom: 1.5rem;
    }

    .cta-title {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(3rem, 5vw, 5.5rem);
      line-height: 0.95;
      letter-spacing: 2px;
      color: var(--blanco);
      margin-bottom: 2rem;
    }
    .cta-title .red { color: var(--rojo-vivo); }
    .cta-title .italic {
      font-family: 'Playfair Display', serif;
      font-style: italic;
      font-size: 0.85em;
    }

    .cta-body {
      font-size: 1rem;
      line-height: 1.8;
      color: var(--gris-medio);
      margin-bottom: 3rem;
      max-width: 450px;
    }

    .cta-actions {
      display: flex;
      flex-direction: column;
      gap: 1rem;
      align-items: flex-start;
    }

    .btn-big {
      background: var(--rojo-vivo);
      color: var(--blanco);
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.4rem;
      letter-spacing: 4px;
      text-transform: uppercase;
      text-decoration: none;
      padding: 1.2rem 3rem;
      position: relative;
      overflow: hidden;
      transition: all 0.3s;
      clip-path: polygon(0 0, calc(100% - 16px) 0, 100% 16px, 100% 100%, 16px 100%, 0 calc(100% - 16px));
    }
    .btn-big::before {
      content: '';
      position: absolute;
      inset: 0;
      background: var(--rojo-medio);
      transform: translateX(-100%);
      transition: transform 0.4s;
    }
    .btn-big:hover::before { transform: translateX(0); }
    .btn-big span { position: relative; z-index: 1; }

    .btn-outline {
      background: transparent;
      color: var(--gris-medio);
      font-size: 0.8rem;
      letter-spacing: 3px;
      text-transform: uppercase;
      text-decoration: none;
      padding: 0.9rem 2rem;
      border: 1px solid var(--rojo-oscuro);
      transition: all 0.3s;
    }
    .btn-outline:hover {
      color: var(--blanco);
      border-color: var(--rojo-vivo);
      background: rgba(226,34,39,0.05);
    }

    /* CTA right - commitment cards */
    .commitment-stack {
      display: flex;
      flex-direction: column;
      gap: 1px;
    }
    .commit-item {
      background: rgba(68,1,1,0.35);
      border-left: 3px solid var(--rojo-oscuro);
      padding: 1.5rem 2rem;
      display: flex;
      align-items: center;
      gap: 1.5rem;
      transition: border-color 0.3s, background 0.3s;
    }
    .commit-item:hover {
      border-color: var(--rojo-vivo);
      background: rgba(108,1,2,0.3);
    }
    .commit-num {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 2rem;
      color: var(--rojo-oscuro);
      min-width: 50px;
      line-height: 1;
      transition: color 0.3s;
    }
    .commit-item:hover .commit-num { color: var(--rojo-vivo); }
    .commit-text strong {
      display: block;
      font-size: 0.85rem;
      letter-spacing: 1px;
      color: var(--blanco);
      margin-bottom: 0.3rem;
    }
    .commit-text p {
      font-size: 0.78rem;
      color: var(--gris-medio);
      line-height: 1.5;
    }

    /* ─── FOOTER ─── */
    footer {
      background: #12181c;
      padding: 3rem 6rem;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border-top: 1px solid rgba(68,1,1,0.5);
    }
    .footer-logo {
      font-family: 'Bebas Neue', sans-serif;
      font-size: 1.4rem;
      letter-spacing: 4px;
      color: var(--rojo-vivo);
    }
    .footer-logo span { color: var(--gris-medio); }
    footer p {
      font-size: 0.72rem;
      color: var(--gris-medio);
      letter-spacing: 1px;
    }
    .footer-line { color: var(--rojo-oscuro); margin: 0 0.5rem; }

    /* ─── SCROLL INDICATOR ─── */
    .scroll-hint {
      position: absolute;
      bottom: 2.5rem; left: 50%;
      transform: translateX(-50%);
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 0.5rem;
      opacity: 0;
      animation: fadeIn 1s 2s forwards;
    }
    .scroll-hint span {
      font-size: 0.6rem;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: var(--gris-medio);
    }
    .scroll-arrow {
      width: 1px;
      height: 40px;
      background: linear-gradient(to bottom, var(--rojo-vivo), transparent);
      animation: scrollDown 1.5s infinite;
    }

    /* ─── ANIMATIONS ─── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn {
      to { opacity: 1; }
    }
    @keyframes pulse {
      from { opacity: 0.5; }
      to   { opacity: 0.9; }
    }
    @keyframes glitchFloat {
      0%   { transform: translateX(0) scaleX(1); opacity: 0.6; }
      30%  { transform: translateX(10px) scaleX(0.8); opacity: 0.3; }
      60%  { transform: translateX(-5px) scaleX(1.2); opacity: 0.7; }
      100% { transform: translateX(0) scaleX(1); opacity: 0.6; }
    }
    @keyframes scrollDown {
      0%   { transform: scaleY(1) translateY(0); opacity: 1; }
      100% { transform: scaleY(0.3) translateY(20px); opacity: 0; }
    }

    /* ─── RESPONSIVE ─── */
    @media (max-width: 768px) {
      nav { padding: 1rem 1.5rem; }
      #inicio { grid-template-columns: 1fr; }
      .hero-left { padding: 7rem 2rem 2rem 2rem; }
      .hero-right { display: none; }
      #efectos { padding: 4rem 1.5rem; }
      .effects-grid { grid-template-columns: 1fr; }
      .effect-card.featured { grid-row: span 1; min-height: 220px; }
      #accion { grid-template-columns: 1fr; padding: 5rem 1.5rem; gap: 3rem; }
      .stats-strip { flex-wrap: wrap; }
      .stat-block { min-width: 45%; border-bottom: 1px solid rgba(108,1,2,0.3); }
      footer { flex-direction: column; gap: 1rem; text-align: center; padding: 2rem 1.5rem; }
      .section-header { grid-template-columns: 1fr; gap: 0.5rem; }
      .section-number { font-size: 3rem; }
    }
  </style>
</head>
<body>

  <!-- NAV -->
  <nav>
    <div class="logo">Scroll<span>Trap</span></div>
    <a href="#efectos">Consecuencias</a>
  </nav>

  <!-- ════════════════ HERO ════════════════ -->
  <section id="inicio">
    <div class="hero-left">
      <p class="hero-eyebrow">Campaña de Concientización · 2026</p>
      <h1 class="hero-title">
        ¿Cuántas horas<br>
        <span class="accent">perdiste hoy?</span>
      </h1>
      <p class="hero-sub">
        El uso excesivo de las redes sociales no es solo pérdida de tiempo. Es
        adicción, ansiedad, comparación constante y desconexión de la realidad.
        Es hora de mirar la pantalla de frente y hacer algo al respecto.
      </p>
      <div class="hero-cta-group">
        <a href="#efectos" class="btn-primary">Ver el impacto</a>
        <a href="#accion" class="btn-secondary">Tomar acción →</a>
      </div>
    </div>

    <div class="hero-right">
      <div class="phone-wrapper">
        <div class="glitch-line"></div>
        <div class="glitch-line"></div>
        <div class="glitch-line"></div>
        <div class="counter-badge">
          7<small>hrs / día</small>
        </div>
        <div class="phone">
          <div class="phone-notch"></div>
          <div class="phone-screen">
            <div class="feed-item"></div>
            <div class="feed-item"></div>
            <div class="feed-item"></div>
            <div class="feed-item"></div>
          </div>
          <div class="phone-bar"></div>
        </div>
      </div>
    </div>

    <div class="scroll-hint">
      <span>Descubre más</span>
      <div class="scroll-arrow"></div>
    </div>
  </section>

  <!-- DIVIDER -->
  <div class="divider"></div>

  <!-- STATS STRIP -->
  <div class="stats-strip">
    <div class="stat-block">
      <div class="stat-number">7 HRS</div>
      <div class="stat-label">promedio diario en pantallas</div>
    </div>
    <div class="stat-block">
      <div class="stat-number">40%</div>
      <div class="stat-label">más ansiedad en usuarios frecuentes</div>
    </div>
    <div class="stat-block">
      <div class="stat-number">2.5 B</div>
      <div class="stat-label">personas con uso problemático</div>
    </div>
    <div class="stat-block">
      <div class="stat-number">16+</div>
      <div class="stat-label">revisiones del teléfono por hora</div>
    </div>
  </div>

  <!-- ════════════════ EFECTOS ════════════════ -->
  <section id="efectos">
    <div class="section-header">
      <div class="section-number">01</div>
      <h2 class="section-title">Lo que nadie<br><em>quiere ver</em></h2>
    </div>

    <div class="effects-grid">

      <div class="effect-card featured">
        <span class="effect-icon">🧠</span>
        <div class="effect-title">Indicadores de Adicción</div>
        <p class="effect-desc">
          Los principales indicadores que permiten identificar una adicción a las redes sociales incluyen:<br>
• Incremento progresivo del tiempo de uso para experimentar satisfacción.<br>
• Manifestación de ansiedad o irritabilidad ante la ausencia de conexión a internet.<br>
• Incapacidad para regular el tiempo destinado al uso de plataformas digitales.<br>
• Conflictos en el entorno familiar, escolar o social derivados del uso excesivo.<br>
• Fluctuaciones frecuentes en el estado anímico.


        </p>
        <span class="effect-tag">Más común en adolescentes</span>
      </div>

      <div class="effect-card">
        <span class="effect-icon">⚠</span>
        <div class="effect-title">Factores de Riesgo</div>
        <p class="effect-desc">
• Trastorno de ansiedad generalizada.<br>
• Deterioro de la autoestima.<br>
• Aislamiento del entorno social inmediato.<br>
• Experimentación persistente de sentimientos de soledad.<br>
• Disminución progresiva de las habilidades de interacción social.<br>

        </p>
        <span class="effect-tag">Efectos a Largo Plazo</span>
      </div>

      <div class="effect-card">
        <span class="effect-icon">👁️</span>
        <div class="effect-title">Batalla contra Plataformas Tecnológicas
</div>
        <p class="effect-desc">
          Diversas instituciones universitarias públicas de Estados Unidos han iniciado procesos legales contra las principales empresas tecnológicas. 
Los demandantes argumentan que las redes sociales comprometen la salud mental de los estudiantes, 
señalando que estas plataformas implementan algoritmos específicamente diseñados para prolongar el tiempo de conexión de los usuarios jóvenes, con el propósito de maximizar sus ingresos publicitarios.

        </p>
        <span class="effect-tag">Acciones llevadas a cabo</span>
      </div>

      <div class="effect-card">
        <span class="effect-icon">🔗</span>
        <div class="effect-title">Riesgo de los Desafíos Virales</div>
        <p class="effect-desc">
          Un factor de riesgo adicional identificado corresponde a la proliferación de desafíos virales en las plataformas digitales. Estos fenómenos han motivado conductas peligrosas que han ocasionado daños tanto físicos como emocionales en la población adolescente, grupo particularmente vulnerable ante la presión social y la necesidad de aceptación en los entornos virtuales.

        </p>
        <span class="effect-tag">Peligro social</span>
      </div>

      <div class="effect-card">
        <span class="effect-icon">🤯</span>
        <div class="effect-title">Realidad de Nuestra Conexión</div>
        <p class="effect-desc">
          El impacto es especialmente profundo en las nuevas generaciones; mientras el usuario promedio dedica unas 23 horas al mes a las redes sociales, los jóvenes de la Generación Z alcanzan las 48 horas mensuales.

        </p>
        <span class="effect-tag">Daño cognitivo</span>
      </div>

    </div>
  </section>

  <!-- DIVIDER -->
  <div class="divider"></div>

  <!-- ════════════════ CTA ════════════════ -->
  <section id="accion">
    <div>
      <p class="cta-eyebrow">02 — Llamado a la acción</p>
      <h2 class="cta-title">
        Es hora de<br>
        <span class="red"><span class="italic">reconectar</span><br>con lo real.</span>
      </h2>
      <p class="cta-body">
        No se trata de eliminar las redes sociales. Se trata de recuperar el control.
        Tú decides cuándo, cómo y por qué las usas. Tu atención es el recurso más valioso
        que tienes y miles de algoritmos compiten por ella cada segundo.
      </p>
      <div class="cta-actions">
        <a href="#inicio" class="btn-big"><span>Comparte esta campaña</span></a>
        <a href="#efectos" class="btn-outline">Revisa los efectos</a>
      </div>
    </div>

    <div class="commitment-stack">
      <div class="commit-item">
        <span class="commit-num">01</span>
        <div class="commit-text">
          <strong>El Cerebro en la Era del Scroll</strong>
          <p>Las plataformas están diseñadas bajo la lógica de la economía de la atención, utilizando mecanismos como el scroll infinito y recompensas variables para activar la liberación de dopamina en el cerebro.</p>
        </div>
      </div>
      <div class="commit-item">
        <span class="commit-num">02</span>
        <div class="commit-text">
          <strong>Lo que el Cuerpo Siente</strong>
          <p>El fenómeno conocido como Text Neck revela que inclinar la cabeza 60 grados para mirar el celular ejerce una presión de casi 30 kilos sobre las vértebras cervicales, lo que deriva en contracturas, cefaleas crónicas e incluso daño nervioso.</p>
        </div>
      </div>
      <div class="commit-item">
        <span class="commit-num">03</span>
        <div class="commit-text">
          <strong>El Costo Psicológico y Social</strong>
          <p>El Síndrome FOMO (Fear of Missing Out) mantiene a los usuarios en un estado de ansiedad persistente por miedo a perderse experiencias gratificantes que otros muestran de forma idealizada.</p>
        </div>
      </div>
      <div class="commit-item">
        <span class="commit-num">04</span>
        <div class="commit-text">
          <strong>Consejos sobre el control de la Tecnología</strong>
          <p>• Regla 20-20-20: Para evitar la fatiga visual, descansa la vista cada 20 minutos mirando a lo lejos por 20 segundos. <br>
• Higiene del sueño: Establecer una desconexión total al menos dos horas antes de dormir y dejar los dispositivos fuera de la habitación. <br>
• Postura ergonómica
</p>
        </div>
      </div>
    </div>
  </section>

  <!-- ════════════════ FOOTER ════════════════ -->
  <footer>
    <div class="footer-logo">Scroll<span>Trap</span></div>
    <p>Diseño Digital <span class="footer-line">|</span> Campaña Equipo 4: Uso excesivo de redes sociales <span class="footer-line">|</span> 2026</p>
    <p>Hecho con Intención — No con Adición.</p>
  </footer>

</body>
</html>
