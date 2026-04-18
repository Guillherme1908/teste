<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>C.helena — Nail Designer Studio</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,500;1,300;1,400&family=Jost:wght@200;300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --cream: #F8F3EE;
    --ivory: #EDE8E1;
    --gold: #C9A96E;
    --gold-light: #E2C99A;
    --gold-dark: #9A7340;
    --obsidian: #0E0E0E;
    --charcoal: #1A1A1A;
    --warm-gray: #6B6360;
    --blush: #D4B8A8;
    --rose: #B07C6A;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--cream);
    color: var(--obsidian);
    font-family: 'Jost', sans-serif;
    font-weight: 300;
    overflow-x: hidden;
  }

  /* ─── CURSOR ─── */
  body { cursor: none; }
  #cursor {
    position: fixed; top: 0; left: 0; z-index: 9999;
    width: 10px; height: 10px;
    background: var(--gold);
    border-radius: 50%;
    pointer-events: none;
    transform: translate(-50%,-50%);
    transition: transform .15s ease, width .3s ease, height .3s ease, background .3s ease;
    mix-blend-mode: multiply;
  }
  #cursor.hover { width: 40px; height: 40px; background: var(--gold-light); }

  /* ─── LOADER ─── */
  #loader {
    position: fixed; inset: 0; z-index: 9990;
    background: var(--obsidian);
    display: flex; align-items: center; justify-content: center;
    flex-direction: column; gap: 20px;
    transition: opacity .8s ease, visibility .8s ease;
  }
  #loader.hidden { opacity: 0; visibility: hidden; }
  .loader-logo {
    font-family: 'Cormorant Garamond', serif;
    color: var(--gold);
    font-size: 2.8rem;
    letter-spacing: .3em;
    font-weight: 300;
    animation: fadeInUp .8s ease forwards;
  }
  .loader-bar {
    width: 200px; height: 1px;
    background: var(--charcoal);
    position: relative; overflow: hidden;
  }
  .loader-bar::after {
    content: '';
    position: absolute; top: 0; left: -100%;
    width: 100%; height: 100%;
    background: var(--gold);
    animation: loadBar 1.8s ease forwards .3s;
  }
  @keyframes loadBar { to { left: 0; } }
  @keyframes fadeInUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }

  /* ─── NAV ─── */
  nav {
    position: fixed; top: 0; width: 100%; z-index: 100;
    display: flex; align-items: center; justify-content: space-between;
    padding: 24px 60px;
    background: rgba(248,243,238,.92);
    backdrop-filter: blur(12px);
    border-bottom: 1px solid rgba(201,169,110,.2);
    transition: padding .3s ease;
  }
  nav.scrolled { padding: 14px 60px; }
  .nav-logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.5rem;
    font-weight: 400;
    letter-spacing: .25em;
    color: var(--obsidian);
    text-decoration: none;
  }
  .nav-logo span { color: var(--gold); }
  .nav-links { display: flex; gap: 40px; list-style: none; }
  .nav-links a {
    font-size: .78rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    color: var(--warm-gray);
    text-decoration: none;
    transition: color .3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--gold);
    transition: width .3s ease;
  }
  .nav-links a:hover { color: var(--obsidian); }
  .nav-links a:hover::after { width: 100%; }
  .nav-cta {
    background: var(--obsidian);
    color: var(--cream) !important;
    padding: 10px 28px;
    border-radius: 0 !important;
    letter-spacing: .15em !important;
    transition: background .3s !important;
  }
  .nav-cta::after { display: none !important; }
  .nav-cta:hover { background: var(--gold-dark) !important; color: var(--cream) !important; }

  /* ─── HERO ─── */
  #hero {
    height: 100vh;
    display: grid; grid-template-columns: 1fr 1fr;
    position: relative; overflow: hidden;
  }
  .hero-left {
    display: flex; flex-direction: column;
    justify-content: center;
    padding: 120px 60px 60px;
    position: relative; z-index: 2;
  }
  .hero-eyebrow {
    font-size: .72rem;
    letter-spacing: .35em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 28px;
    opacity: 0;
    animation: fadeInUp .8s ease forwards .5s;
  }
  .hero-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(3.5rem, 5vw, 6rem);
    line-height: 1.05;
    font-weight: 300;
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeInUp .8s ease forwards .7s;
  }
  .hero-title em { font-style: italic; color: var(--gold); }
  .hero-desc {
    font-size: .95rem;
    line-height: 1.9;
    color: var(--warm-gray);
    max-width: 380px;
    margin-bottom: 48px;
    opacity: 0;
    animation: fadeInUp .8s ease forwards .9s;
  }
  .hero-actions {
    display: flex; gap: 20px; align-items: center;
    opacity: 0;
    animation: fadeInUp .8s ease forwards 1.1s;
  }
  .btn-primary {
    background: var(--obsidian);
    color: var(--cream);
    padding: 16px 40px;
    font-family: 'Jost', sans-serif;
    font-size: .8rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    border: none;
    cursor: none;
    transition: background .3s, transform .3s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-primary:hover { background: var(--gold-dark); transform: translateY(-2px); }
  .btn-ghost {
    color: var(--warm-gray);
    font-size: .8rem;
    letter-spacing: .15em;
    text-transform: uppercase;
    text-decoration: none;
    display: flex; align-items: center; gap: 10px;
    transition: color .3s;
  }
  .btn-ghost::before {
    content: '';
    width: 30px; height: 1px;
    background: currentColor;
    transition: width .3s;
  }
  .btn-ghost:hover { color: var(--obsidian); }
  .btn-ghost:hover::before { width: 50px; }
  .hero-right {
    position: relative; overflow: hidden;
    opacity: 0;
    animation: fadeIn 1.2s ease forwards 1s;
  }
  @keyframes fadeIn { to { opacity: 1; } }
  .hero-image-bg {
    position: absolute; inset: 0;
    background: linear-gradient(135deg, #1a1a1a 0%, #2d2420 50%, #1a1a1a 100%);
  }
  .hero-image-overlay {
    position: absolute; inset: 0;
    background: 
      radial-gradient(ellipse at 30% 50%, rgba(201,169,110,.15) 0%, transparent 60%),
      radial-gradient(ellipse at 80% 20%, rgba(176,124,106,.1) 0%, transparent 50%);
  }
  .hero-nail-art {
    position: absolute; inset: 0;
    display: flex; align-items: center; justify-content: center;
  }
  .nail-showcase {
    display: grid; grid-template-columns: repeat(5, 1fr); gap: 12px;
    transform: rotate(-5deg) translateY(-20px);
  }
  .nail {
    width: 54px; height: 90px;
    border-radius: 50px 50px 20px 20px;
    position: relative;
    overflow: hidden;
    box-shadow: 0 8px 30px rgba(0,0,0,.4);
    animation: nailFloat 3s ease-in-out infinite alternate;
  }
  .nail:nth-child(2) { animation-delay: .3s; height: 100px; }
  .nail:nth-child(3) { animation-delay: .6s; height: 105px; }
  .nail:nth-child(4) { animation-delay: .9s; height: 96px; }
  .nail:nth-child(5) { animation-delay: 1.2s; height: 80px; }
  @keyframes nailFloat {
    from { transform: translateY(0); }
    to { transform: translateY(-10px); }
  }
  .nail-1 { background: linear-gradient(160deg, #C9A96E, #9A7340); }
  .nail-2 { background: linear-gradient(160deg, #D4B8A8, #B07C6A); }
  .nail-3 { background: linear-gradient(160deg, #2d2d2d, #1a1a1a); }
  .nail-4 { background: linear-gradient(160deg, #E8D5C4, #C9A96E); }
  .nail-5 { background: linear-gradient(160deg, #B07C6A, #8B5E52); }
  .nail::after {
    content: '';
    position: absolute; top: 8px; left: 50%; transform: translateX(-50%);
    width: 60%; height: 30%;
    background: rgba(255,255,255,.15);
    border-radius: 50%;
    filter: blur(4px);
  }
  .hero-stats {
    position: absolute; bottom: 60px; left: 60px;
    display: flex; gap: 50px;
    opacity: 0;
    animation: fadeInUp .8s ease forwards 1.4s;
  }
  .stat-item { text-align: left; }
  .stat-number {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2.4rem;
    font-weight: 300;
    color: var(--obsidian);
    line-height: 1;
  }
  .stat-label {
    font-size: .7rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    color: var(--gold);
    margin-top: 4px;
  }
  .hero-scroll {
    position: absolute; bottom: 30px; right: 60px;
    writing-mode: vertical-rl;
    font-size: .68rem;
    letter-spacing: .3em;
    text-transform: uppercase;
    color: var(--warm-gray);
    display: flex; align-items: center; gap: 16px;
    opacity: 0;
    animation: fadeIn 1s ease forwards 1.6s;
  }
  .hero-scroll::before {
    content: '';
    width: 1px; height: 60px;
    background: var(--gold);
    animation: scrollLine 2s ease-in-out infinite;
  }
  @keyframes scrollLine {
    0%,100% { height: 60px; opacity: 1; }
    50% { height: 30px; opacity: .5; }
  }

  /* ─── SECTION GENERIC ─── */
  section { padding: 120px 60px; }
  .section-eyebrow {
    font-size: .72rem;
    letter-spacing: .35em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 16px;
  }
  .section-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(2.5rem, 4vw, 4rem);
    font-weight: 300;
    line-height: 1.1;
    margin-bottom: 20px;
  }
  .section-title em { font-style: italic; color: var(--gold); }
  .section-divider {
    width: 60px; height: 1px;
    background: var(--gold);
    margin-bottom: 50px;
  }

  /* ─── SERVICES ─── */
  #services { background: var(--obsidian); color: var(--cream); }
  #services .section-title { color: var(--cream); }
  #services .section-divider { background: var(--gold); }
  .services-header { max-width: 600px; margin-bottom: 70px; }
  .services-header p { color: rgba(248,243,238,.6); line-height: 1.9; font-size: .95rem; }
  .services-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
    gap: 2px;
  }
  .service-card {
    background: var(--charcoal);
    padding: 48px 36px;
    position: relative; overflow: hidden;
    transition: transform .4s ease;
    cursor: none;
  }
  .service-card::before {
    content: '';
    position: absolute; bottom: 0; left: 0;
    width: 100%; height: 2px;
    background: var(--gold);
    transform: scaleX(0);
    transform-origin: left;
    transition: transform .4s ease;
  }
  .service-card:hover { transform: translateY(-6px); }
  .service-card:hover::before { transform: scaleX(1); }
  .service-icon {
    font-size: 2rem;
    margin-bottom: 24px;
    display: block;
  }
  .service-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.5rem;
    font-weight: 400;
    color: var(--cream);
    margin-bottom: 12px;
  }
  .service-desc {
    font-size: .88rem;
    color: rgba(248,243,238,.5);
    line-height: 1.8;
    margin-bottom: 28px;
  }
  .service-details { display: flex; justify-content: space-between; align-items: flex-end; }
  .service-price {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem;
    font-weight: 300;
    color: var(--gold);
    line-height: 1;
  }
  .service-price span {
    font-family: 'Jost', sans-serif;
    font-size: .75rem;
    letter-spacing: .1em;
    color: rgba(201,169,110,.6);
    display: block;
    margin-top: 2px;
  }
  .service-duration {
    font-size: .75rem;
    letter-spacing: .15em;
    text-transform: uppercase;
    color: rgba(248,243,238,.3);
    border: 1px solid rgba(248,243,238,.1);
    padding: 6px 14px;
  }
  .service-number {
    position: absolute; top: 24px; right: 28px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 4rem;
    font-weight: 300;
    color: rgba(255,255,255,.04);
    line-height: 1;
    user-select: none;
  }

  /* ─── BOOKING ─── */
  #booking {
    background: var(--ivory);
    display: grid; grid-template-columns: 1fr 1.2fr;
    gap: 80px; align-items: start;
    padding: 120px 60px;
  }
  .booking-info { position: sticky; top: 120px; }
  .booking-info p { color: var(--warm-gray); line-height: 1.9; font-size: .95rem; margin-bottom: 40px; }
  .booking-perks { list-style: none; display: flex; flex-direction: column; gap: 18px; }
  .booking-perks li {
    display: flex; align-items: flex-start; gap: 16px;
    font-size: .88rem; color: var(--warm-gray); line-height: 1.6;
  }
  .perk-dot {
    width: 6px; height: 6px; min-width: 6px;
    background: var(--gold);
    border-radius: 50%;
    margin-top: 8px;
  }

  /* FORM */
  .booking-form { display: flex; flex-direction: column; gap: 0; }
  .form-step {
    display: none;
    flex-direction: column; gap: 24px;
    animation: fadeInUp .5s ease forwards;
  }
  .form-step.active { display: flex; }
  .step-indicator {
    display: flex; gap: 8px; margin-bottom: 16px; align-items: center;
  }
  .step-dot {
    width: 28px; height: 2px;
    background: var(--ivory);
    border: 1px solid rgba(201,169,110,.3);
    transition: background .3s;
    position: relative;
  }
  .step-dot.active { background: var(--gold); border-color: var(--gold); }
  .step-dot.done { background: var(--gold-dark); border-color: var(--gold-dark); }
  .step-label {
    font-size: .7rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    color: var(--warm-gray);
    margin-left: 8px;
  }
  .step-label.active { color: var(--gold); }
  .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .form-group { display: flex; flex-direction: column; gap: 8px; }
  .form-group label {
    font-size: .72rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    color: var(--warm-gray);
  }
  .form-group input,
  .form-group select,
  .form-group textarea {
    background: transparent;
    border: none;
    border-bottom: 1px solid rgba(107,99,96,.3);
    padding: 12px 0;
    font-family: 'Jost', sans-serif;
    font-size: .95rem;
    font-weight: 300;
    color: var(--obsidian);
    outline: none;
    transition: border-color .3s;
    cursor: none;
    width: 100%;
    -webkit-appearance: none;
  }
  .form-group select {
    background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='10' height='6' viewBox='0 0 10 6'%3E%3Cpath d='M1 1l4 4 4-4' stroke='%23C9A96E' stroke-width='1.5' fill='none'/%3E%3C/svg%3E");
    background-repeat: no-repeat;
    background-position: right 0 center;
    padding-right: 20px;
    cursor: none;
  }
  .form-group input:focus,
  .form-group select:focus,
  .form-group textarea:focus { border-bottom-color: var(--gold); }
  .form-group textarea { resize: none; height: 80px; }

  /* SERVICE PICKER */
  .service-picker {
    display: grid; grid-template-columns: 1fr 1fr; gap: 12px;
  }
  .service-option {
    border: 1px solid rgba(107,99,96,.2);
    padding: 20px 18px;
    cursor: none;
    transition: all .3s;
    position: relative;
  }
  .service-option:hover { border-color: var(--gold); }
  .service-option.selected {
    border-color: var(--gold);
    background: rgba(201,169,110,.08);
  }
  .service-option.selected::after {
    content: '✓';
    position: absolute; top: 10px; right: 12px;
    font-size: .75rem;
    color: var(--gold);
  }
  .so-name { font-size: .9rem; margin-bottom: 4px; }
  .so-price { font-family: 'Cormorant Garamond', serif; font-size: 1.3rem; color: var(--gold); }
  .so-duration { font-size: .72rem; color: var(--warm-gray); letter-spacing: .1em; }

  /* DATE/TIME GRID */
  .date-grid {
    display: grid; grid-template-columns: repeat(7, 1fr); gap: 8px;
  }
  .date-cell {
    text-align: center; padding: 12px 6px;
    border: 1px solid rgba(107,99,96,.15);
    cursor: none;
    transition: all .3s;
    font-size: .85rem;
  }
  .date-cell.today { border-color: var(--gold-light); color: var(--gold-dark); }
  .date-cell:hover:not(.disabled) { border-color: var(--gold); background: rgba(201,169,110,.06); }
  .date-cell.selected { background: var(--gold); color: var(--cream); border-color: var(--gold); }
  .date-cell.disabled { opacity: .3; pointer-events: none; }
  .date-cell-day { font-size: .65rem; letter-spacing: .1em; text-transform: uppercase; color: var(--warm-gray); margin-bottom: 4px; }
  .date-cell.selected .date-cell-day { color: var(--cream); }
  .time-grid {
    display: grid; grid-template-columns: repeat(4, 1fr); gap: 10px;
  }
  .time-slot {
    text-align: center; padding: 10px;
    border: 1px solid rgba(107,99,96,.15);
    cursor: none; transition: all .3s;
    font-size: .82rem;
  }
  .time-slot:hover:not(.taken) { border-color: var(--gold); }
  .time-slot.selected { background: var(--obsidian); color: var(--cream); border-color: var(--obsidian); }
  .time-slot.taken { opacity: .3; pointer-events: none; text-decoration: line-through; }

  /* SUMMARY */
  .booking-summary {
    background: var(--obsidian);
    color: var(--cream);
    padding: 32px;
    margin-bottom: 24px;
  }
  .summary-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.2rem;
    color: var(--gold);
    margin-bottom: 24px;
    letter-spacing: .1em;
  }
  .summary-row {
    display: flex; justify-content: space-between; align-items: center;
    padding: 12px 0;
    border-bottom: 1px solid rgba(255,255,255,.06);
    font-size: .88rem;
  }
  .summary-row:last-child { border-bottom: none; }
  .summary-row .label { color: rgba(248,243,238,.5); font-size: .75rem; letter-spacing: .12em; text-transform: uppercase; }
  .summary-row .value { color: var(--cream); }
  .summary-total {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem;
    color: var(--gold);
  }

  .form-actions { display: flex; gap: 16px; justify-content: flex-end; margin-top: 8px; }
  .btn-next, .btn-prev, .btn-confirm {
    padding: 14px 36px;
    font-family: 'Jost', sans-serif;
    font-size: .78rem;
    letter-spacing: .2em;
    text-transform: uppercase;
    border: none;
    cursor: none;
    transition: all .3s;
  }
  .btn-next, .btn-confirm { background: var(--obsidian); color: var(--cream); }
  .btn-next:hover, .btn-confirm:hover { background: var(--gold-dark); }
  .btn-prev { background: transparent; border: 1px solid rgba(107,99,96,.3); color: var(--warm-gray); }
  .btn-prev:hover { border-color: var(--obsidian); color: var(--obsidian); }

  /* SUCCESS */
  .booking-success {
    display: none; flex-direction: column; align-items: center; justify-content: center;
    text-align: center; padding: 60px 40px;
    background: var(--obsidian);
    color: var(--cream);
  }
  .booking-success.show { display: flex; }
  .success-icon {
    width: 80px; height: 80px;
    border: 1px solid var(--gold);
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-size: 2rem;
    margin-bottom: 32px;
    animation: successPop .5s ease forwards;
  }
  @keyframes successPop {
    from { transform: scale(.7); opacity: 0; }
    to { transform: scale(1); opacity: 1; }
  }
  .success-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem; color: var(--gold);
    margin-bottom: 16px;
  }
  .success-msg { color: rgba(248,243,238,.6); line-height: 1.9; font-size: .9rem; }
  .success-code {
    margin-top: 32px;
    border: 1px solid rgba(201,169,110,.3);
    padding: 16px 32px;
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.5rem;
    color: var(--gold);
    letter-spacing: .3em;
  }

  /* ─── LOCATION ─── */
  #location {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 0; padding: 0;
    min-height: 600px;
  }
  .location-info {
    background: var(--obsidian);
    color: var(--cream);
    padding: 100px 70px;
    display: flex; flex-direction: column; justify-content: center;
  }
  .location-info .section-eyebrow { color: var(--gold); }
  .location-info .section-title { color: var(--cream); margin-bottom: 50px; }
  .location-details { display: flex; flex-direction: colum