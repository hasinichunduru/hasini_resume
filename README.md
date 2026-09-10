<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <meta name="theme-color" content="#07101f" />
  <meta name="description" content="Hasini Chunduri — Computer Science Engineering student and aspiring software developer portfolio." />
  <title>Hasini Chunduri | Software Developer Portfolio</title>

  <style>
    /* =========================================================
       HASINI CHUNDURI — SINGLE-FILE PORTFOLIO
       No build tools. No separate assets. GitHub Pages ready.
       ========================================================= */

    :root {
      --bg: #050912;
      --bg-2: #091323;
      --panel: rgba(12, 23, 40, 0.68);
      --panel-solid: #0c1728;
      --line: rgba(117, 170, 255, 0.18);
      --text: #f5f8ff;
      --muted: #91a3bd;
      --blue: #2d8cff;
      --cyan: #50d7ff;
      --violet: #8068ff;
      --glow: rgba(45, 140, 255, 0.35);
      --radius: 24px;
      --max: 1180px;
      --ease: cubic-bezier(.2,.8,.2,1);
    }

    * { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      min-height: 100vh;
      overflow-x: hidden;
      color: var(--text);
      background:
        radial-gradient(circle at 15% 15%, rgba(45,140,255,.12), transparent 28%),
        radial-gradient(circle at 85% 10%, rgba(128,104,255,.10), transparent 25%),
        linear-gradient(135deg, #040812, #07101e 55%, #050a13);
      font-family: Inter, ui-sans-serif, system-ui, -apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif;
      line-height: 1.6;
    }

    body::before {
      content: "";
      position: fixed;
      inset: 0;
      z-index: -3;
      pointer-events: none;
      opacity: .35;
      background-image:
        linear-gradient(rgba(255,255,255,.025) 1px, transparent 1px),
        linear-gradient(90deg, rgba(255,255,255,.025) 1px, transparent 1px);
      background-size: 55px 55px;
      mask-image: linear-gradient(to bottom, black, transparent 90%);
    }

    a { color: inherit; text-decoration: none; }
    button, a { -webkit-tap-highlight-color: transparent; }

    /* ---------- Loader ---------- */
    .loader {
      position: fixed;
      inset: 0;
      z-index: 9999;
      display: grid;
      place-items: center;
      background: #040812;
      transition: opacity .7s var(--ease), visibility .7s;
    }

    .loader.hidden { opacity: 0; visibility: hidden; }

    .loader-core {
      width: 74px;
      height: 74px;
      position: relative;
      transform-style: preserve-3d;
      animation: loaderSpin 2s linear infinite;
    }

    .loader-core::before,
    .loader-core::after {
      content: "";
      position: absolute;
      inset: 8px;
      border: 2px solid transparent;
      border-top-color: var(--cyan);
      border-right-color: var(--blue);
      border-radius: 50%;
      box-shadow: 0 0 28px var(--glow);
    }

    .loader-core::after {
      inset: 18px;
      border-top-color: var(--violet);
      border-right-color: var(--cyan);
      animation: loaderSpin 1.2s linear reverse infinite;
    }

    @keyframes loaderSpin { to { transform: rotate(360deg); } }

    /* ---------- Custom cursor ---------- */
    .cursor-dot,
    .cursor-ring {
      position: fixed;
      top: 0;
      left: 0;
      z-index: 10000;
      pointer-events: none;
      border-radius: 50%;
      transform: translate(-50%, -50%);
    }

    .cursor-dot {
      width: 6px;
      height: 6px;
      background: white;
      box-shadow: 0 0 18px var(--cyan);
    }

    .cursor-ring {
      width: 34px;
      height: 34px;
      border: 1px solid rgba(80,215,255,.65);
      transition: width .2s, height .2s, border-color .2s, background .2s;
    }

    body.cursor-active .cursor-ring {
      width: 58px;
      height: 58px;
      border-color: rgba(45,140,255,.95);
      background: rgba(45,140,255,.07);
    }

    @media (pointer: coarse) {
      .cursor-dot, .cursor-ring { display: none; }
    }

    /* ---------- Canvas ---------- */
    #space {
      position: fixed;
      inset: 0;
      z-index: -2;
      pointer-events: none;
      opacity: .75;
    }

    /* ---------- Navigation ---------- */
    .nav {
      position: fixed;
      top: 18px;
      left: 50%;
      z-index: 1000;
      width: min(calc(100% - 28px), 1080px);
      transform: translateX(-50%);
      padding: 10px 12px 10px 18px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      border: 1px solid rgba(117,170,255,.16);
      border-radius: 999px;
      background: rgba(5, 10, 20, .68);
      backdrop-filter: blur(18px);
      box-shadow: 0 18px 55px rgba(0,0,0,.22);
    }

    .brand {
      display: flex;
      align-items: center;
      gap: 11px;
      font-weight: 800;
      letter-spacing: -.02em;
    }

    .brand-mark {
      width: 35px;
      height: 35px;
      display: grid;
      place-items: center;
      border-radius: 50%;
      color: white;
      font-size: .8rem;
      background: linear-gradient(135deg, var(--blue), var(--violet));
      box-shadow: 0 0 22px rgba(45,140,255,.3);
    }

    .nav-links {
      display: flex;
      align-items: center;
      gap: 4px;
    }

    .nav-links a {
      position: relative;
      padding: 9px 13px;
      color: #aab8ca;
      font-size: .83rem;
      border-radius: 999px;
      transition: color .25s, background .25s;
    }

    .nav-links a:hover,
    .nav-links a.active {
      color: white;
      background: rgba(45,140,255,.11);
    }

    .nav-cta {
      padding: 10px 16px !important;
      color: white !important;
      background: linear-gradient(135deg, var(--blue), #1261ce) !important;
      box-shadow: 0 8px 25px rgba(45,140,255,.22);
    }

    .menu-btn {
      display: none;
      border: 0;
      color: white;
      background: transparent;
      font-size: 1.35rem;
      cursor: pointer;
    }

    /* ---------- Shared ---------- */
    main { overflow: hidden; }

    section {
      position: relative;
      width: min(calc(100% - 40px), var(--max));
      margin: 0 auto;
      padding: 105px 0;
    }

    .section-kicker {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      margin-bottom: 12px;
      color: var(--cyan);
      font-size: .73rem;
      font-weight: 800;
      letter-spacing: .16em;
      text-transform: uppercase;
    }

    .section-kicker::before {
      content: "";
      width: 28px;
      height: 1px;
      background: linear-gradient(90deg, transparent, var(--cyan));
    }

    .section-title {
      max-width: 720px;
      font-size: clamp(2rem, 4vw, 3.55rem);
      line-height: 1.05;
      letter-spacing: -.045em;
    }

    .section-title span {
      color: transparent;
      background: linear-gradient(90deg, var(--blue), var(--cyan), #fff);
      background-clip: text;
      -webkit-background-clip: text;
    }

    .section-copy {
      max-width: 670px;
      margin-top: 18px;
      color: var(--muted);
    }

    .reveal {
      opacity: 0;
      transform: translateY(35px);
      transition: opacity .8s var(--ease), transform .8s var(--ease);
    }

    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ---------- Hero ---------- */
    .hero {
      min-height: 100svh;
      width: 100%;
      max-width: none;
      padding: 150px max(20px, calc((100% - var(--max)) / 2)) 85px;
      display: grid;
      place-items: center;
      isolation: isolate;
    }

    .hero::before {
      content: "";
      position: absolute;
      width: 520px;
      height: 520px;
      right: -160px;
      top: 10%;
      border: 1px solid rgba(45,140,255,.12);
      border-radius: 50%;
      box-shadow:
        0 0 0 55px rgba(45,140,255,.018),
        0 0 0 120px rgba(45,140,255,.012);
      animation: orbit 18s linear infinite;
      pointer-events: none;
    }

    @keyframes orbit { to { transform: rotate(360deg); } }

    .hero-grid {
      width: min(100%, var(--max));
      display: grid;
      grid-template-columns: 1.08fr .92fr;
      align-items: center;
      gap: 65px;
    }

    .hero-eyebrow {
      display: inline-flex;
      align-items: center;
      gap: 9px;
      padding: 7px 12px;
      border: 1px solid rgba(80,215,255,.2);
      border-radius: 999px;
      color: #c9eaff;
      background: rgba(45,140,255,.06);
      font-size: .74rem;
      font-weight: 700;
      letter-spacing: .04em;
    }

    .pulse-dot {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: #5cff9a;
      box-shadow: 0 0 0 0 rgba(92,255,154,.6);
      animation: pulse 1.7s infinite;
    }

    @keyframes pulse {
      70% { box-shadow: 0 0 0 9px transparent; }
      100% { box-shadow: 0 0 0 0 transparent; }
    }

    .hero h1 {
      margin-top: 22px;
      font-size: clamp(3.1rem, 7vw, 6.8rem);
      line-height: .88;
      letter-spacing: -.075em;
      max-width: 850px;
    }

    .hero h1 .line { display: block; }

    .gradient-text {
      color: transparent;
      background: linear-gradient(110deg, #fff 5%, var(--cyan) 42%, var(--blue) 72%, #8d7dff);
      background-size: 200% auto;
      background-clip: text;
      -webkit-background-clip: text;
      animation: shine 6s linear infinite;
    }

    @keyframes shine { to { background-position: 200% center; } }

    .hero-subtitle {
      margin-top: 25px;
      max-width: 650px;
      color: #a9b7c9;
      font-size: clamp(1rem, 1.7vw, 1.2rem);
    }

    .hero-actions {
      display: flex;
      flex-wrap: wrap;
      gap: 13px;
      margin-top: 30px;
    }

    .btn {
      position: relative;
      display: inline-flex;
      align-items: center;
      justify-content: center;
      gap: 9px;
      min-height: 48px;
      padding: 0 20px;
      overflow: hidden;
      border: 1px solid rgba(117,170,255,.2);
      border-radius: 13px;
      color: white;
      font: inherit;
      font-weight: 750;
      font-size: .86rem;
      cursor: pointer;
      background: rgba(255,255,255,.035);
      transition: transform .25s var(--ease), border-color .25s, box-shadow .25s;
    }

    .btn::before {
      content: "";
      position: absolute;
      inset: 0;
      background: linear-gradient(110deg, transparent 20%, rgba(255,255,255,.15), transparent 80%);
      transform: translateX(-120%);
      transition: transform .7s;
    }

    .btn:hover::before { transform: translateX(120%); }
    .btn:hover { transform: translateY(-3px); border-color: rgba(80,215,255,.45); }

    .btn-primary {
      border-color: transparent;
      background: linear-gradient(135deg, var(--blue), #155dce);
      box-shadow: 0 14px 35px rgba(45,140,255,.22);
    }

    .btn-primary:hover { box-shadow: 0 18px 42px rgba(45,140,255,.34); }

    .btn-outline { background: rgba(10,21,37,.5); }

    .hero-stats {
      display: flex;
      flex-wrap: wrap;
      gap: 28px;
      margin-top: 42px;
    }

    .stat strong {
      display: block;
      font-size: 1.45rem;
      letter-spacing: -.04em;
    }

    .stat span {
      display: block;
      margin-top: 2px;
      color: #72839a;
      font-size: .7rem;
      text-transform: uppercase;
      letter-spacing: .12em;
    }

    /* ---------- 3D Hero Object ---------- */
    .hero-visual {
      min-height: 560px;
      display: grid;
      place-items: center;
      perspective: 1100px;
    }

    .scene {
      width: min(410px, 78vw);
      aspect-ratio: 1;
      position: relative;
      transform-style: preserve-3d;
      animation: float 6s ease-in-out infinite;
    }

    @keyframes float {
      0%,100% { transform: translateY(0) rotateX(2deg) rotateY(-5deg); }
      50% { transform: translateY(-18px) rotateX(-2deg) rotateY(5deg); }
    }

    .orb {
      position: absolute;
      inset: 17%;
      border-radius: 50%;
      background:
        radial-gradient(circle at 32% 26%, #dff8ff 0 1%, #7eeaff 5%, #1d8bff 28%, #123d9b 55%, #07102b 75%);
      box-shadow:
        inset -28px -35px 60px rgba(0,0,0,.45),
        inset 20px 18px 45px rgba(255,255,255,.14),
        0 0 80px rgba(45,140,255,.28),
        0 0 180px rgba(45,140,255,.1);
      transform-style: preserve-3d;
    }

    .orb::before {
      content: "";
      position: absolute;
      inset: 12%;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,.22);
      transform: translateZ(35px);
    }

    .ring {
      position: absolute;
      inset: 4%;
      border: 1px solid rgba(80,215,255,.5);
      border-radius: 50%;
      transform: rotateX(67deg) rotateY(-15deg) translateZ(35px);
      box-shadow: 0 0 20px rgba(80,215,255,.2);
      animation: ring1 9s linear infinite;
    }

    .ring:nth-child(2) {
      inset: 10%;
      border-color: rgba(128,104,255,.5);
      transform: rotateY(67deg) rotateX(20deg) translateZ(20px);
      animation: ring2 12s linear infinite reverse;
    }

    .ring:nth-child(3) {
      inset: 18%;
      border-color: rgba(255,255,255,.22);
      transform: rotateX(70deg) rotateY(30deg);
      animation: ring1 14s linear infinite;
    }

    @keyframes ring1 { to { transform: rotateX(67deg) rotateY(-15deg) translateZ(35px) rotateZ(360deg); } }
    @keyframes ring2 { to { transform: rotateY(67deg) rotateX(20deg) translateZ(20px) rotateZ(360deg); } }

    .orb-code {
      position: absolute;
      inset: 0;
      display: grid;
      place-items: center;
      z-index: 3;
      transform: translateZ(75px);
    }

    .orb-code span {
      display: block;
      font-family: ui-monospace, SFMono-Regular, Menlo, monospace;
      font-size: clamp(2.2rem, 6vw, 3.6rem);
      font-weight: 900;
      letter-spacing: -.1em;
      text-shadow: 0 0 28px rgba(80,215,255,.65);
    }

    .float-card {
      position: absolute;
      z-index: 5;
      min-width: 125px;
      padding: 13px 15px;
      border: 1px solid rgba(117,170,255,.2);
      border-radius: 15px;
      background: rgba(7,15,28,.72);
      backdrop-filter: blur(15px);
      box-shadow: 0 20px 50px rgba(0,0,0,.28);
      transform: translateZ(90px);
    }

    .float-card small {
      color: #73869f;
      font-size: .63rem;
      text-transform: uppercase;
      letter-spacing: .1em;
    }

    .float-card strong {
      display: block;
      margin-top: 2px;
      font-size: .9rem;
    }

    .fc-1 { top: 11%; right: -2%; animation: floatCard 4.2s ease-in-out infinite; }
    .fc-2 { left: -7%; bottom: 18%; animation: floatCard 5.2s ease-in-out .4s infinite; }
    .fc-3 { right: 7%; bottom: 2%; animation: floatCard 4.8s ease-in-out .8s infinite; }

    @keyframes floatCard {
      50% { transform: translateZ(110px) translateY(-9px); }
    }

    /* ---------- About ---------- */
    .about-grid {
      display: grid;
      grid-template-columns: .75fr 1.25fr;
      gap: 60px;
      align-items: start;
    }

    .about-card {
      position: relative;
      min-height: 350px;
      padding: 28px;
      overflow: hidden;
      border: 1px solid var(--line);
      border-radius: var(--radius);
      background: linear-gradient(145deg, rgba(21,42,69,.72), rgba(7,14,25,.75));
      transform-style: preserve-3d;
    }

    .about-card::before {
      content: "";
      position: absolute;
      width: 230px;
      height: 230px;
      right: -100px;
      top: -100px;
      border-radius: 50%;
      background: rgba(45,140,255,.14);
      filter: blur(20px);
    }

    .avatar {
      width: 125px;
      height: 125px;
      display: grid;
      place-items: center;
      border: 1px solid rgba(255,255,255,.22);
      border-radius: 50%;
      background: linear-gradient(145deg, #0d66d8, #061a38);
      box-shadow: inset 12px 12px 30px rgba(255,255,255,.08), 0 0 45px rgba(45,140,255,.2);
      font-size: 2.2rem;
      font-weight: 900;
      letter-spacing: -.08em;
      transform: translateZ(40px);
    }

    .about-card h3 { margin-top: 24px; font-size: 1.35rem; }
    .about-card p { margin-top: 7px; color: var(--muted); font-size: .9rem; }

    .about-copy h3 { font-size: 1.7rem; letter-spacing: -.03em; }
    .about-copy p { margin-top: 17px; color: var(--muted); }
    .about-copy p:first-of-type { margin-top: 14px; }

    .chip-row {
      display: flex;
      flex-wrap: wrap;
      gap: 9px;
      margin-top: 22px;
    }

    .chip {
      padding: 7px 11px;
      border: 1px solid rgba(80,215,255,.15);
      border-radius: 999px;
      color: #9edfff;
      background: rgba(45,140,255,.055);
      font-size: .72rem;
      font-weight: 700;
    }

    /* ---------- Skills ---------- */
    .skills-wrap {
      margin-top: 42px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }

    .skill-card {
      padding: 20px;
      border: 1px solid var(--line);
      border-radius: 18px;
      background: rgba(9,19,33,.56);
      transition: transform .3s var(--ease), border-color .3s;
    }

    .skill-card:hover {
      transform: translateY(-5px);
      border-color: rgba(80,215,255,.32);
    }

    .skill-head {
      display: flex;
      justify-content: space-between;
      gap: 12px;
      font-size: .85rem;
      font-weight: 800;
    }

    .skill-head span:last-child { color: var(--cyan); }

    .bar {
      height: 6px;
      margin-top: 12px;
      overflow: hidden;
      border-radius: 999px;
      background: #172437;
    }

    .bar i {
      display: block;
      width: 0;
      height: 100%;
      border-radius: inherit;
      background: linear-gradient(90deg, var(--blue), var(--cyan));
      box-shadow: 0 0 16px rgba(45,140,255,.45);
      transition: width 1.4s var(--ease);
    }

    .skills-wrap.visible .bar i { width: var(--level); }

    /* ---------- Projects ---------- */
    .project-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 22px;
      margin-top: 45px;
    }

    .project {
      position: relative;
      min-height: 340px;
      padding: 27px;
      overflow: hidden;
      border: 1px solid var(--line);
      border-radius: var(--radius);
      background: linear-gradient(145deg, rgba(14,28,48,.78), rgba(6,12,22,.72));
      transform-style: preserve-3d;
      transition: border-color .35s, box-shadow .35s;
    }

    .project:hover {
      border-color: rgba(80,215,255,.38);
      box-shadow: 0 28px 75px rgba(0,0,0,.3);
    }

    .project::after {
      content: "";
      position: absolute;
      width: 210px;
      height: 210px;
      right: -90px;
      bottom: -90px;
      border-radius: 50%;
      background: radial-gradient(circle, rgba(45,140,255,.17), transparent 68%);
      pointer-events: none;
    }

    .project-number {
      position: absolute;
      right: 23px;
      top: 17px;
      color: rgba(255,255,255,.05);
      font-size: 4.5rem;
      line-height: 1;
      font-weight: 900;
    }

    .project-icon {
      width: 52px;
      height: 52px;
      display: grid;
      place-items: center;
      border: 1px solid rgba(80,215,255,.18);
      border-radius: 15px;
      color: var(--cyan);
      background: rgba(45,140,255,.08);
      font-size: 1.35rem;
      transform: translateZ(35px);
    }

    .project h3 {
      margin-top: 24px;
      font-size: 1.25rem;
      letter-spacing: -.025em;
      transform: translateZ(28px);
    }

    .project p {
      max-width: 560px;
      margin-top: 9px;
      color: var(--muted);
      font-size: .88rem;
      transform: translateZ(18px);
    }

    .project .chip-row { transform: translateZ(25px); }

    .project-link {
      position: absolute;
      left: 27px;
      bottom: 25px;
      color: #aeeaff;
      font-size: .8rem;
      font-weight: 800;
    }

    .project-link::after {
      content: " ↗";
      color: var(--cyan);
      transition: margin-left .2s;
    }

    .project:hover .project-link::after { margin-left: 5px; }

    /* ---------- Timeline ---------- */
    .timeline {
      position: relative;
      margin-top: 48px;
      margin-left: 12px;
      padding-left: 35px;
      border-left: 1px solid rgba(80,215,255,.24);
    }

    .timeline-item {
      position: relative;
      padding: 0 0 40px 0;
    }

    .timeline-item:last-child { padding-bottom: 0; }

    .timeline-item::before {
      content: "";
      position: absolute;
      left: -41px;
      top: 3px;
      width: 11px;
      height: 11px;
      border: 3px solid #08101d;
      border-radius: 50%;
      background: var(--cyan);
      box-shadow: 0 0 18px rgba(80,215,255,.55);
    }

    .timeline-meta {
      color: var(--cyan);
      font-size: .7rem;
      font-weight: 800;
      letter-spacing: .13em;
      text-transform: uppercase;
    }

    .timeline h3 { margin-top: 6px; font-size: 1.15rem; }
    .timeline p { margin-top: 7px; color: var(--muted); max-width: 720px; }

    /* ---------- Certifications ---------- */
    .cert-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 16px;
      margin-top: 38px;
    }

    .cert {
      min-height: 150px;
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;
      text-align: center;
      padding: 22px;
      border: 1px solid var(--line);
      border-radius: 18px;
      background: rgba(9,19,33,.56);
      transition: transform .3s var(--ease), background .3s;
    }

    .cert:hover {
      transform: translateY(-6px) rotateX(3deg);
      background: rgba(15,34,57,.72);
    }

    .cert strong { color: #9fe4ff; }
    .cert span { margin-top: 5px; color: #70839b; font-size: .73rem; }

    /* ---------- Contact ---------- */
    .contact-box {
      position: relative;
      overflow: hidden;
      padding: clamp(28px, 6vw, 60px);
      border: 1px solid rgba(80,215,255,.18);
      border-radius: 30px;
      background:
        radial-gradient(circle at 85% 20%, rgba(45,140,255,.16), transparent 28%),
        linear-gradient(145deg, rgba(13,29,50,.9), rgba(5,12,22,.9));
    }

    .contact-box::before,
    .contact-box::after {
      content: "";
      position: absolute;
      border: 1px solid rgba(80,215,255,.08);
      border-radius: 50%;
      pointer-events: none;
    }

    .contact-box::before { width: 300px; height: 300px; right: -140px; top: -170px; }
    .contact-box::after { width: 500px; height: 500px; right: -260px; top: -270px; }

    .contact-grid {
      position: relative;
      z-index: 2;
      display: grid;
      grid-template-columns: 1.1fr .9fr;
      gap: 50px;
      align-items: end;
    }

    .contact-box h2 { max-width: 700px; font-size: clamp(2rem, 5vw, 4.3rem); line-height: .98; letter-spacing: -.06em; }

    .contact-box h2 span {
      color: transparent;
      background: linear-gradient(90deg, var(--cyan), var(--blue));
      background-clip: text;
      -webkit-background-clip: text;
    }

    .contact-box p { max-width: 620px; margin-top: 17px; color: var(--muted); }

    .contact-links {
      display: grid;
      gap: 10px;
    }

    .contact-link {
      display: flex;
      align-items: center;
      justify-content: space-between;
      gap: 12px;
      padding: 14px 16px;
      border: 1px solid var(--line);
      border-radius: 13px;
      color: #b9c7d9;
      background: rgba(255,255,255,.025);
      transition: transform .25s, border-color .25s, color .25s;
    }

    .contact-link:hover {
      transform: translateX(5px);
      color: white;
      border-color: rgba(80,215,255,.36);
    }

    .contact-link small {
      display: block;
      color: #657991;
      font-size: .65rem;
      text-transform: uppercase;
      letter-spacing: .1em;
    }

    .contact-link strong { display: block; margin-top: 2px; font-size: .82rem; }

    /* ---------- Footer ---------- */
    footer {
      width: min(calc(100% - 40px), var(--max));
      margin: 0 auto;
      padding: 25px 0 40px;
      display: flex;
      justify-content: space-between;
      gap: 20px;
      color: #596b82;
      font-size: .72rem;
      border-top: 1px solid rgba(117,170,255,.1);
    }

    .back-top {
      color: #9ccfff;
      cursor: pointer;
    }

    /* ---------- Scroll progress ---------- */
    .progress {
      position: fixed;
      z-index: 1001;
      left: 0;
      top: 0;
      height: 2px;
      width: 0;
      background: linear-gradient(90deg, var(--blue), var(--cyan));
      box-shadow: 0 0 15px var(--cyan);
    }

    /* ---------- Responsive ---------- */
    @media (max-width: 900px) {
      .hero-grid,
      .about-grid,
      .contact-grid { grid-template-columns: 1fr; }

      .hero { padding-top: 135px; }
      .hero-visual { min-height: 470px; }
      .hero-grid { gap: 20px; }
      .about-grid { gap: 30px; }
      .contact-grid { gap: 35px; }
    }

    @media (max-width: 720px) {
      section { width: min(calc(100% - 28px), var(--max)); padding: 80px 0; }

      .nav {
        width: calc(100% - 18px);
        top: 9px;
      }

      .nav-links {
        position: absolute;
        left: 0;
        right: 0;
        top: calc(100% + 9px);
        display: grid;
        gap: 3px;
        padding: 8px;
        border: 1px solid var(--line);
        border-radius: 20px;
        background: rgba(5,10,20,.92);
        backdrop-filter: blur(20px);
        opacity: 0;
        visibility: hidden;
        transform: translateY(-8px);
        transition: .25s var(--ease);
      }

      .nav-links.open {
        opacity: 1;
        visibility: visible;
        transform: translateY(0);
      }

      .nav-links a { padding: 12px; }
      .nav-cta { text-align: center; }

      .menu-btn { display: block; }
      .nav > .nav-cta { display: none; }

      .hero h1 { font-size: clamp(3.3rem, 17vw, 5.6rem); }
      .hero-visual { min-height: 390px; }

      .scene { width: min(335px, 88vw); }
      .fc-1 { right: -1%; }
      .fc-2 { left: -2%; }
      .fc-3 { right: 2%; }

      .skills-wrap,
      .project-grid { grid-template-columns: 1fr; }

      .cert-grid { grid-template-columns: 1fr; }
      .cert { min-height: 120px; }

      footer { flex-direction: column; }
    }

    @media (max-width: 430px) {
      .hero-actions .btn { width: 100%; }
      .hero-stats { gap: 18px; }
      .float-card { transform: scale(.88) translateZ(70px); }
      .fc-1 { top: 7%; right: -9%; }
      .fc-2 { left: -10%; bottom: 18%; }
      .fc-3 { right: -5%; }
    }

    /* ---------- Reduced motion ---------- */
    @media (prefers-reduced-motion: reduce) {
      *, *::before, *::after {
        animation-duration: .01ms !important;
        animation-iteration-count: 1 !important;
        scroll-behavior: auto !important;
        transition-duration: .01ms !important;
      }
    }
  </style>
</head>

<body>
  <div class="loader" id="loader" aria-hidden="true">
    <div class="loader-core"></div>
  </div>

  <div class="progress" id="progress"></div>
  <canvas id="space"></canvas>
  <div class="cursor-dot" id="cursorDot"></div>
  <div class="cursor-ring" id="cursorRing"></div>

  <!-- Navigation -->
  <nav class="nav" aria-label="Primary navigation">
    <a class="brand magnetic" href="#home" aria-label="Hasini home">
      <span class="brand-mark">HC</span>
      <span>HASINI<span style="color:var(--cyan)">.</span></span>
    </a>

    <div class="nav-links" id="navLinks">
      <a href="#home">Home</a>
      <a href="#about">About</a>
      <a href="#skills">Skills</a>
      <a href="#projects">Projects</a>
      <a href="#education">Journey</a>
      <a href="#contact">Contact</a>
    </div>

    <a class="btn nav-cta magnetic" href="#contact">Let's talk ↗</a>
    <button class="menu-btn" id="menuBtn" aria-label="Open menu" aria-expanded="false">☰</button>
  </nav>

  <main>
    <!-- HERO -->
    <section class="hero" id="home">
      <div class="hero-grid">
        <div class="hero-copy reveal">
          <div class="hero-eyebrow">
            <span class="pulse-dot"></span>
            Available for opportunities
          </div>

          <h1>
            <span class="line">HASINI</span>
            <span class="line gradient-text">CHUNDURI.</span>
          </h1>

          <p class="hero-subtitle">
            Computer Science Engineering student crafting intelligent, practical
            digital experiences with Python, Java, machine learning and modern web technologies.
          </p>

          <div class="hero-actions">
            <a class="btn btn-primary magnetic" href="#projects">Explore my work <span>↓</span></a>
            <button class="btn btn-outline magnetic" id="resumeBtn">Download resume <span>↓</span></button>
          </div>

          <div class="hero-stats">
            <div class="stat"><strong>9.0/10</strong><span>CGPA</span></div>
            <div class="stat"><strong>06+</strong><span>Core skills</span></div>
            <div class="stat"><strong>02</strong><span>Featured projects</span></div>
          </div>
        </div>

        <div class="hero-visual reveal">
          <div class="scene" id="scene">
            <div class="orb"></div>
            <div class="ring"></div>
            <div class="ring"></div>
            <div class="ring"></div>

            <div class="orb-code">
              <span>&lt;/HC&gt;</span>
            </div>

            <div class="float-card fc-1">
              <small>Focus</small>
              <strong>Machine Learning</strong>
            </div>
            <div class="float-card fc-2">
              <small>Build with</small>
              <strong>Python · Java</strong>
            </div>
            <div class="float-card fc-3">
              <small>Mindset</small>
              <strong>Learn → Build → Grow</strong>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about">
      <div class="about-grid">
        <div class="about-card reveal tilt">
          <div class="avatar">HC</div>
          <h3>Computer Science<br>Engineering</h3>
          <p>Student • Problem Solver • Future Software Developer</p>
          <div class="chip-row">
            <span class="chip">Python</span>
            <span class="chip">Java</span>
            <span class="chip">ML</span>
            <span class="chip">Web</span>
          </div>
        </div>

        <div class="about-copy reveal">
          <div class="section-kicker">About me</div>
          <h2 class="section-title">Building skills that turn <span>ideas into impact.</span></h2>
          <p>
            I’m Hasini Chunduri, a Computer Science Engineering student with a strong
            foundation in Python, Java, HTML, machine learning and problem solving.
          </p>
          <p>
            I enjoy exploring software development, intelligent systems and web technologies.
            My goal is to keep learning, build useful products and gain real-world engineering
            experience through meaningful projects.
          </p>
          <div class="chip-row">
            <span class="chip">Software Development</span>
            <span class="chip">Machine Learning</span>
            <span class="chip">Problem Solving</span>
            <span class="chip">Teamwork</span>
          </div>
        </div>
      </div>
    </section>

    <!-- SKILLS -->
    <section id="skills">
      <div class="reveal">
        <div class="section-kicker">Technical toolkit</div>
        <h2 class="section-title">Skills with <span>room to grow.</span></h2>
        <p class="section-copy">
          A practical skill set focused on programming, intelligent systems, web technologies
          and the problem-solving mindset needed to keep improving.
        </p>
      </div>

      <div class="skills-wrap reveal" id="skillsWrap">
        <div class="skill-card">
          <div class="skill-head"><span>Python</span><span>85%</span></div>
          <div class="bar"><i style="--level:85%"></i></div>
        </div>
        <div class="skill-card">
          <div class="skill-head"><span>Java</span><span>75%</span></div>
          <div class="bar"><i style="--level:75%"></i></div>
        </div>
        <div class="skill-card">
          <div class="skill-head"><span>HTML / Web</span><span>90%</span></div>
          <div class="bar"><i style="--level:90%"></i></div>
        </div>
        <div class="skill-card">
          <div class="skill-head"><span>Machine Learning</span><span>70%</span></div>
          <div class="bar"><i style="--level:70%"></i></div>
        </div>
        <div class="skill-card">
          <div class="skill-head"><span>Problem Solving</span><span>80%</span></div>
          <div class="bar"><i style="--level:80%"></i></div>
        </div>
        <div class="skill-card">
          <div class="skill-head"><span>Teamwork</span><span>85%</span></div>
          <div class="bar"><i style="--level:85%"></i></div>
        </div>
      </div>
    </section>

    <!-- PROJECTS -->
    <section id="projects">
      <div class="reveal">
        <div class="section-kicker">Selected work</div>
        <h2 class="section-title">Projects that <span>solve problems.</span></h2>
        <p class="section-copy">
          Two featured projects from my learning journey, presented as practical engineering
          work rather than just coursework.
        </p>
      </div>

      <div class="project-grid">
        <article class="project tilt reveal">
          <div class="project-number">01</div>
          <div class="project-icon">⌁</div>
          <h3>Network Intrusion Detection System</h3>
          <p>
            A machine-learning based cybersecurity project designed to analyze network traffic
            and identify potentially malicious activity. The workflow combines data processing,
            feature handling and classification.
          </p>
          <div class="chip-row">
            <span class="chip">Python</span>
            <span class="chip">Machine Learning</span>
            <span class="chip">Cyber Security</span>
          </div>
          <a class="project-link" href="#contact">Discuss project</a>
        </article>

        <article class="project tilt reveal">
          <div class="project-number">02</div>
          <div class="project-icon">▣</div>
          <h3>Credit Card Fraud Detection</h3>
          <p>
            A data-driven fraud detection project focused on preprocessing, classification
            and identifying suspicious transaction patterns using Python and machine learning.
          </p>
          <div class="chip-row">
            <span class="chip">Python</span>
            <span class="chip">ML</span>
            <span class="chip">Data Processing</span>
          </div>
          <a class="project-link" href="#contact">Discuss project</a>
        </article>
      </div>
    </section>

    <!-- EDUCATION / EXPERIENCE -->
    <section id="education">
      <div class="reveal">
        <div class="section-kicker">Education & journey</div>
        <h2 class="section-title">Learning is the <span>main project.</span></h2>
      </div>

      <div class="timeline">
        <div class="timeline-item reveal">
          <div class="timeline-meta">Current • B.Tech</div>
          <h3>Dhanekula Institute of Engineering and Technology</h3>
          <p>B.Tech — Computer Science Engineering · CGPA: 9.0 / 10</p>
        </div>

        <div class="timeline-item reveal">
          <div class="timeline-meta">Intermediate</div>
          <h3>Narayana Junior College</h3>
          <p>Intermediate · 92%</p>
        </div>

        <div class="timeline-item reveal">
          <div class="timeline-meta">SSC</div>
          <h3>St. Mary's English Medium High School</h3>
          <p>SSC · 90%</p>
        </div>
      </div>

      <div class="reveal" style="margin-top:85px;">
        <div class="section-kicker">Certifications</div>
        <h2 class="section-title">Small milestones, <span>real progress.</span></h2>
      </div>

      <div class="cert-grid">
        <div class="cert reveal"><strong>Google</strong><span>Certification</span></div>
        <div class="cert reveal"><strong>Microsoft</strong><span>Certification</span></div>
        <div class="cert reveal"><strong>SkillEarn</strong><span>Certification</span></div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact">
      <div class="contact-box reveal">
        <div class="contact-grid">
          <div>
            <div class="section-kicker">Get in touch</div>
            <h2>Let’s build something <span>meaningful.</span></h2>
            <p>
              Interested in software development, machine learning or collaborative projects?
              I’m always open to learning, connecting and exploring new opportunities.
            </p>
            <div class="hero-actions">
              <a class="btn btn-primary magnetic" href="mailto:hasinichunduru100@gmail.com">Send an email ↗</a>
              <a class="btn btn-outline magnetic" href="#home">Back to top ↑</a>
            </div>
          </div>

          <div class="contact-links">
            <!-- Replace the placeholder URLs below with your real profiles before publishing. -->
            <a class="contact-link magnetic" href="mailto:hasinichunduru100@gmail.com">
              <span><small>Email</small><strong>hasinichunduru100@gmail.com</strong></span>
              <span>↗</span>
            </a>
            <a class="contact-link magnetic" href="https://www.linkedin.com/" target="_blank" rel="noopener">
              <span><small>LinkedIn</small><strong>Connect professionally</strong></span>
              <span>↗</span>
            </a>
            <a class="contact-link magnetic" href="https://github.com/" target="_blank" rel="noopener">
              <span><small>GitHub</small><strong>Explore my code</strong></span>
              <span>↗</span>
            </a>
            <a class="contact-link magnetic" href="https://www.google.com/maps/search/?api=1&query=Gannavaram%2C%20Vijayawada%2C%20Andhra%20Pradesh" target="_blank" rel="noopener">
              <span><small>Location</small><strong>Gannavaram, Vijayawada</strong></span>
              <span>↗</span>
            </a>
          </div>
        </div>
      </div>
    </section>
  </main>

  <footer>
    <span>© <span id="year"></span> Hasini Chunduri. Designed & developed with curiosity.</span>
    <a class="back-top" href="#home">Return to top ↑</a>
  </footer>

  <script>
    /* =========================================================
       Interactive portfolio engine
       ========================================================= */

    const $ = (selector, parent = document) => parent.querySelector(selector);
    const $$ = (selector, parent = document) => [...parent.querySelectorAll(selector)];

    // Loader
    window.addEventListener("load", () => {
      setTimeout(() => $("#loader").classList.add("hidden"), 450);
    });

    // Current year
    $("#year").textContent = new Date().getFullYear();

    // Mobile navigation
    const menuBtn = $("#menuBtn");
    const navLinks = $("#navLinks");

    menuBtn.addEventListener("click", () => {
      const open = navLinks.classList.toggle("open");
      menuBtn.setAttribute("aria-expanded", open);
      menuBtn.textContent = open ? "×" : "☰";
    });

    $$("#navLinks a").forEach(link => {
      link.addEventListener("click", () => {
        navLinks.classList.remove("open");
        menuBtn.setAttribute("aria-expanded", "false");
        menuBtn.textContent = "☰";
      });
    });

    // Scroll progress
    const progress = $("#progress");
    const updateProgress = () => {
      const scrollTop = window.scrollY;
      const height = document.documentElement.scrollHeight - window.innerHeight;
      progress.style.width = height > 0 ? `${(scrollTop / height) * 100}%` : "0%";
    };
    window.addEventListener("scroll", updateProgress, { passive: true });
    updateProgress();

    // Reveal on scroll
    const observer = new IntersectionObserver((entries) => {
      entries.forEach(entry => {
        if (entry.isIntersecting) entry.target.classList.add("visible");
      });
    }, { threshold: 0.12 });

    $$(".reveal").forEach(el => observer.observe(el));

    // Activate skill bars when their container becomes visible
    const skillsObserver = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (entry.isIntersecting) entry.target.classList.add("visible");
      });
    }, { threshold: .3 });
    skillsObserver.observe($("#skillsWrap"));

    // Active navigation link
    const sections = $$("main section[id]");
    const navAnchors = $$("#navLinks a");

    const sectionObserver = new IntersectionObserver(entries => {
      entries.forEach(entry => {
        if (!entry.isIntersecting) return;
        navAnchors.forEach(a => a.classList.remove("active"));
        const active = $(`#navLinks a[href="#${entry.target.id}"]`);
        if (active) active.classList.add("active");
      });
    }, { rootMargin: "-35% 0px -55% 0px", threshold: 0 });

    sections.forEach(section => sectionObserver.observe(section));

    // Custom cursor
    const dot = $("#cursorDot");
    const ring = $("#cursorRing");
    let mouseX = innerWidth / 2, mouseY = innerHeight / 2;
    let ringX = mouseX, ringY = mouseY;

    window.addEventListener("mousemove", e => {
      mouseX = e.clientX;
      mouseY = e.clientY;
      dot.style.left = mouseX + "px";
      dot.style.top = mouseY + "px";
    });

    function cursorLoop() {
      ringX += (mouseX - ringX) * .14;
      ringY += (mouseY - ringY) * .14;
      ring.style.left = ringX + "px";
      ring.style.top = ringY + "px";
      requestAnimationFrame(cursorLoop);
    }
    cursorLoop();

    $$("a, button, .project, .skill-card, .cert").forEach(el => {
      el.addEventListener("mouseenter", () => document.body.classList.add("cursor-active"));
      el.addEventListener("mouseleave", () => document.body.classList.remove("cursor-active"));
    });

    // 3D tilt cards
    $$(".tilt").forEach(card => {
      card.addEventListener("mousemove", e => {
        if (matchMedia("(pointer: coarse)").matches) return;
        const rect = card.getBoundingClientRect();
        const x = (e.clientX - rect.left) / rect.width;
        const y = (e.clientY - rect.top) / rect.height;
        const rotateX = (0.5 - y) * 9;
        const rotateY = (x - 0.5) * 11;
        card.style.transform = `perspective(900px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) translateY(-4px)`;
      });

      card.addEventListener("mouseleave", () => {
        card.style.transform = "";
      });
    });

    // Magnetic buttons
    $$(".magnetic").forEach(el => {
      el.addEventListener("mousemove", e => {
        if (matchMedia("(pointer: coarse)").matches) return;
        const rect = el.getBoundingClientRect();
        const x = e.clientX - rect.left - rect.width / 2;
        const y = e.clientY - rect.top - rect.height / 2;
        el.style.transform = `translate(${x * .08}px, ${y * .08}px)`;
      });
      el.addEventListener("mouseleave", () => {
        el.style.transform = "";
      });
    });

    // Interactive hero scene
    const scene = $("#scene");
    if (scene) {
      scene.addEventListener("mousemove", e => {
        if (matchMedia("(pointer: coarse)").matches) return;
        const rect = scene.getBoundingClientRect();
        const x = (e.clientX - rect.left) / rect.width - .5;
        const y = (e.clientY - rect.top) / rect.height - .5;
        scene.style.animationPlayState = "paused";
        scene.style.transform = `rotateX(${y * -8}deg) rotateY(${x * 10}deg)`;
      });
      scene.addEventListener("mouseleave", () => {
        scene.style.animationPlayState = "";
        scene.style.transform = "";
      });
    }

    // Resume button: creates a clean printable resume from the same single file.
    $("#resumeBtn").addEventListener("click", () => {
      const resume = `
HASINI CHUNDURI
Computer Science Engineering Student | Aspiring Software Developer

PROFILE
Computer Science Engineering student with a strong foundation in Python, Java, HTML,
machine learning and problem solving. Interested in software development, intelligent
systems and web technologies.

SKILLS
Python 85% | Java 75% | HTML/Web 90% | Machine Learning 70%
Problem Solving 80% | Teamwork 85%

PROJECTS
1. Network Intrusion Detection System
Machine-learning based cybersecurity project for analyzing network traffic and identifying
potentially malicious activity using Python, data processing and classification.

2. Credit Card Fraud Detection
Data-driven fraud detection project focused on preprocessing, classification and identifying
suspicious transaction patterns using Python and machine learning.

EDUCATION
Dhanekula Institute of Engineering and Technology
B.Tech — Computer Science Engineering | CGPA: 9.0 / 10

Narayana Junior College
Intermediate | 92%

St. Mary's English Medium High School
SSC | 90%

CERTIFICATIONS
Google Certification | Microsoft Certification | SkillEarn Certification

CONTACT
Email: hasinichunduru100@gmail.com
Location: Gannavaram, Vijayawada
      `.trim();

      const blob = new Blob([resume], { type: "text/plain;charset=utf-8" });
      const url = URL.createObjectURL(blob);
      const a = document.createElement("a");
      a.href = url;
      a.download = "Hasini-Chunduri-Resume.txt";
      document.body.appendChild(a);
      a.click();
      a.remove();
      URL.revokeObjectURL(url);
    });

    // Particle / star field — lightweight canvas, no library required.
    const canvas = $("#space");
    const ctx = canvas.getContext("2d");
    let particles = [];
    let w = 0, h = 0;
    const reducedMotion = matchMedia("(prefers-reduced-motion: reduce)").matches;

    function resizeCanvas() {
      const dpr = Math.min(devicePixelRatio || 1, 2);
      w = canvas.clientWidth = innerWidth;
      h = canvas.clientHeight = innerHeight;
      canvas.width = w * dpr;
      canvas.height = h * dpr;
      ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

      const count = Math.min(100, Math.floor((w * h) / 15000));
      particles = Array.from({ length: count }, () => ({
        x: Math.random() * w,
        y: Math.random() * h,
        r: Math.random() * 1.6 + .25,
        a: Math.random() * .55 + .1,
        s: Math.random() * .22 + .03,
        drift: (Math.random() - .5) * .08
      }));
    }

    function drawParticles() {
      ctx.clearRect(0, 0, w, h);
      for (const p of particles) {
        p.y -= p.s;
        p.x += p.drift;
        if (p.y < -5) p.y = h + 5;
        if (p.x < -5) p.x = w + 5;
        if (p.x > w + 5) p.x = -5;

        ctx.beginPath();
        ctx.arc(p.x, p.y, p.r, 0, Math.PI * 2);
        ctx.fillStyle = `rgba(130, 200, 255, ${p.a})`;
        ctx.fill();
      }
      if (!reducedMotion) requestAnimationFrame(drawParticles);
    }

    addEventListener("resize", resizeCanvas);
    resizeCanvas();
    drawParticles();
  </script>
</body>
</html>
