<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>C.Helena — Nail Designer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Raleway:wght@200;300;400;500&display=swap" rel="stylesheet">
<style>
  :root {
    --cream: #F5EFE6;
    --gold: #C9A96E;
    --gold-light: #E8D5B0;
    --gold-dark: #9B7940;
    --black: #0A0A0A;
    --charcoal: #1A1A1A;
    --text-dark: #2C2C2C;
    --text-muted: #7A6E62;
    --rose: #D4A5A0;
    --rose-dark: #B87E78;
    --white: #FDFAF6;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    font-family: 'Raleway', sans-serif;
    background: var(--black);
    color: var(--cream);
    overflow-x: hidden;
    cursor: none;
  }

  /* CUSTOM CURSOR */
  .cursor {
    width: 8px; height: 8px;
    background: var(--gold);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9999;
    transform: translate(-50%,-50%);
    transition: transform 0.1s;
  }
  .cursor-ring {
    width: 30px; height: 30px;
    border: 1px solid var(--gold);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none; z-index: 9998;
    transform: translate(-50%,-50%);
    transition: all 0.3s ease;
    opacity: 0.6;
  }

  /* SCROLLBAR */
  ::-webkit-scrollbar { width: 4px; }
  ::-webkit-scrollbar-track { background: var(--black); }
  ::-webkit-scrollbar-thumb { background: var(--gold); }

  /* NAV */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 1000;
    padding: 24px 60px;
    display: flex; justify-content: space-between; align-items: center;
    transition: all 0.5s ease;
  }
  nav.scrolled {
    background: rgba(10,10,10,0.95);
    backdrop-filter: blur(20px);
    padding: 16px 60px;
    border-bottom: 1px solid rgba(201,169,110,0.2);
  }
  .nav-logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem;
    font-weight: 300;
    letter-spacing: 0.15em;
    color: var(--gold);
    text-decoration: none;
  }
  .nav-logo span { font-style: italic; color: var(--cream); }
  .nav-links {
    display: flex; gap: 40px; list-style: none;
    align-items: center;
  }
  .nav-links a {
    font-family: 'Raleway', sans-serif;
    font-size: 0.7rem;
    font-weight: 400;
    letter-spacing: 0.25em;
    text-transform: uppercase;
    color: var(--cream);
    text-decoration: none;
    opacity: 0.7;
    transition: all 0.3s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute; bottom: -4px; left: 0;
    width: 0; height: 1px;
    background: var(--gold);
    transition: width 0.3s;
  }
  .nav-links a:hover { opacity: 1; color: var(--gold); }
  .nav-links a:hover::after { width: 100%; }
  .nav-cta {
    background: transparent;
    border: 1px solid var(--gold);
    color: var(--gold) !important;
    opacity: 1 !important;
    padding: 10px 28px;
    letter-spacing: 0.2em;
    font-size: 0.65rem !important;
    transition: all 0.3s !important;
  }
  .nav-cta:hover {
    background: var(--gold) !important;
    color: var(--black) !important;
  }
  .nav-cta::after { display: none !important; }

  /* HERO */
  .hero {
    min-height: 100vh;
    display: flex; align-items: center;
    position: relative; overflow: hidden;
    background: var(--black);
  }
  .hero-bg {
    position: absolute; inset: 0;
    background: radial-gradient(ellipse at 70% 50%, rgba(201,169,110,0.07) 0%, transparent 60%),
                radial-gradient(ellipse at 20% 80%, rgba(212,165,160,0.05) 0%, transparent 50%);
  }
  .hero-lines {
    position: absolute; inset: 0;
    background-image:
      linear-gradient(rgba(201,169,110,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(201,169,110,0.03) 1px, transparent 1px);
    background-size: 80px 80px;
  }
  .hero-content {
    position: relative; z-index: 2;
    padding: 0 60px;
    max-width: 700px;
  }
  .hero-tag {
    font-size: 0.65rem;
    letter-spacing: 0.35em;
    text-transform: uppercase;
    color: var(--gold);
    margin-bottom: 28px;
    display: flex; align-items: center; gap: 16px;
    opacity: 0;
    animation: fadeUp 1s 0.3s forwards;
  }
  .hero-tag::before { content: ''; width: 40px; height: 1px; background: var(--gold); }
  .hero-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(4rem, 8vw, 7rem);
    font-weight: 300;
    line-height: 0.95;
    margin-bottom: 8px;
    opacity: 0;
    animation: fadeUp 1s 0.5s forwards;
  }
  .hero-title em {
    font-style: italic;
    color: var(--gold);
    display: block;
  }
  .hero-subtitle {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(1rem, 2vw, 1.4rem);
    font-weight: 300;
    color: var(--text-muted);
    letter-spacing: 0.1em;
    margin: 24px 0 48px;
    line-height: 1.7;
    opacity: 0;
    animation: fadeUp 1s 0.7s forwards;
  }
  .hero-actions {
    display: flex; gap: 20px; align-items: center;
    opacity: 0;
    animation: fadeUp 1s 0.9s forwards;
  }
  .btn-primary {
    background: var(--gold);
    color: var(--black);
    border: none;
    padding: 16px 44px;
    font-family: 'Raleway', sans-serif;
    font-size: 0.65rem;
    font-weight: 500;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    cursor: none;
    transition: all 0.4s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-primary:hover {
    background: var(--gold-dark);
    transform: translateY(-2px);
    box-shadow: 0 20px 40px rgba(201,169,110,0.3);
  }
  .btn-ghost {
    background: transparent;
    color: var(--cream);
    border: 1px solid rgba(245,239,230,0.3);
    padding: 16px 44px;
    font-family: 'Raleway', sans-serif;
    font-size: 0.65rem;
    font-weight: 400;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    cursor: none;
    transition: all 0.4s;
    text-decoration: none;
    display: inline-block;
  }
  .btn-ghost:hover {
    border-color: var(--gold);
    color: var(--gold);
  }
  .hero-image-side {
    position: absolute; right: 0; top: 0; bottom: 0;
    width: 45%;
    overflow: hidden;
  }
  .hero-image-side::before {
    content: '';
    position: absolute; left: 0; top: 0; bottom: 0;
    width: 200px;
    background: linear-gradient(to right, var(--black), transparent);
    z-index: 2;
  }
  .hero-image-placeholder {
    width: 100%; height: 100%;
    background: linear-gradient(135deg, #1a1510 0%, #2a1f15 40%, #1a1208 100%);
    display: flex; align-items: center; justify-content: center;
    flex-direction: column; gap: 16px;
  }
  .nail-art-grid {
    display: grid; grid-template-columns: 1fr 1fr;
    gap: 3px; width: 100%; height: 100%;
    opacity: 0; animation: fadeIn 1.5s 1.2s forwards;
  }
  .nail-cell {
    background: linear-gradient(135deg, #2a1f15, #1a1208);
    display: flex; align-items: center; justify-content: center;
    font-size: 4rem;
    transition: all 0.5s;
  }
  .nail-cell:nth-child(1) { background: linear-gradient(135deg, #2C1810, #4A2E1A); font-size: 5rem; }
  .nail-cell:nth-child(2) { background: linear-gradient(135deg, #1A1208, #2E1F0A); }
  .nail-cell:nth-child(3) { background: linear-gradient(135deg, #0A0806, #1A1510); }
  .nail-cell:nth-child(4) { background: linear-gradient(135deg, #1E0E12, #2E1518); font-size: 5rem; }
  .hero-scroll {
    position: absolute; bottom: 40px; left: 60px;
    display: flex; align-items: center; gap: 16px;
    font-size: 0.6rem; letter-spacing: 0.3em; text-transform: uppercase;
    color: var(--text-muted); opacity: 0;
    animation: fadeIn 1s 1.5s forwards;
  }
  .scroll-line {
    width: 1px; height: 50px;
    background: linear-gradient(to bottom, transparent, var(--gold));
    animation: scrollLine 2s infinite;
  }
  @keyframes scrollLine {
    0% { transform: scaleY(0); transform-origin: top; }
    50% { transform: scaleY(1); transform-origin: top; }
    51% { transform-origin: bottom; }
    100% { transform: scaleY(0); transform-origin: bottom; }
  }

  /* SECTIONS */
  section { position: relative; }
  .section-label {
    font-size: 0.6rem; letter-spacing: 0.4em;
    text-transform: uppercase; color: var(--gold);
    margin-bottom: 20px;
    display: flex; align-items: center; gap: 16px;
  }
  .section-label::before { content: ''; width: 30px; height: 1px; background: var(--gold); }
  .section-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: clamp(2.5rem, 5vw, 4rem);
    font-weight: 300;
    line-height: 1.1;
    margin-bottom: 24px;
  }
  .section-title em { font-style: italic; color: var(--gold); }

  /* ABOUT */
  #sobre {
    padding: 120px 60px;
    background: var(--charcoal);
  }
  .about-grid {
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: center;
  }
  .about-image-wrap {
    position: relative;
  }
  .about-img-frame {
    width: 100%; aspect-ratio: 3/4;
    background: linear-gradient(135deg, #2a1f15, #1a1208);
    display: flex; align-items: center; justify-content: center;
    font-size: 8rem;
    position: relative; overflow: hidden;
  }
  .about-img-frame::before {
    content: '';
    position: absolute; inset: 0;
    background: linear-gradient(135deg, rgba(201,169,110,0.1), transparent);
  }
  .about-frame-deco {
    position: absolute;
    top: -20px; right: -20px;
    width: 60%; height: 60%;
    border: 1px solid rgba(201,169,110,0.3);
    pointer-events: none;
  }
  .about-stats {
    display: grid; grid-template-columns: 1fr 1fr; gap: 24px; margin-top: 40px;
  }
  .stat-item {
    border: 1px solid rgba(201,169,110,0.2);
    padding: 24px;
    transition: all 0.3s;
  }
  .stat-item:hover { border-color: var(--gold); background: rgba(201,169,110,0.05); }
  .stat-num {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2.5rem; font-weight: 300;
    color: var(--gold); line-height: 1;
  }
  .stat-label { font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--text-muted); margin-top: 8px; }
  .about-text { color: rgba(245,239,230,0.7); line-height: 1.9; font-size: 0.95rem; font-weight: 300; }
  .signature {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem; font-style: italic;
    color: var(--gold); margin-top: 32px;
  }

  /* SERVICES */
  #servicos {
    padding: 120px 60px;
    background: var(--black);
  }
  .services-header { max-width: 1200px; margin: 0 auto 60px; }
  .services-grid {
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: repeat(3, 1fr); gap: 2px;
  }
  .service-card {
    background: var(--charcoal);
    padding: 48px 36px;
    position: relative; overflow: hidden;
    transition: all 0.5s;
    cursor: none;
  }
  .service-card::before {
    content: '';
    position: absolute; bottom: 0; left: 0; right: 0; height: 2px;
    background: linear-gradient(to right, transparent, var(--gold), transparent);
    transform: scaleX(0); transition: transform 0.5s;
  }
  .service-card:hover::before { transform: scaleX(1); }
  .service-card:hover { background: #1e1e1e; transform: translateY(-4px); }
  .service-icon {
    font-size: 2.5rem; margin-bottom: 24px;
    display: block;
  }
  .service-name {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.5rem; font-weight: 400;
    margin-bottom: 12px; color: var(--cream);
  }
  .service-desc {
    font-size: 0.85rem; color: var(--text-muted);
    line-height: 1.8; font-weight: 300;
    margin-bottom: 24px;
  }
  .service-price {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.8rem; color: var(--gold);
    font-weight: 300;
  }
  .service-price span { font-size: 0.8rem; color: var(--text-muted); font-family: 'Raleway', sans-serif; }

  /* PORTFOLIO */
  #portfolio {
    padding: 120px 60px;
    background: var(--charcoal);
  }
  .portfolio-header { max-width: 1200px; margin: 0 auto 60px; display: flex; justify-content: space-between; align-items: flex-end; }
  .portfolio-filter {
    display: flex; gap: 8px;
  }
  .filter-btn {
    background: transparent; border: 1px solid rgba(201,169,110,0.3);
    color: var(--text-muted); padding: 8px 20px;
    font-family: 'Raleway', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    cursor: none; transition: all 0.3s;
  }
  .filter-btn.active, .filter-btn:hover {
    border-color: var(--gold); color: var(--gold);
    background: rgba(201,169,110,0.08);
  }
  .portfolio-masonry {
    max-width: 1200px; margin: 0 auto;
    columns: 3; column-gap: 4px;
  }
  .portfolio-item {
    break-inside: avoid; margin-bottom: 4px;
    position: relative; overflow: hidden;
    cursor: none;
  }
  .portfolio-img {
    width: 100%; display: block;
    background: linear-gradient(135deg, #2a1f15, #1a1208);
    transition: transform 0.6s cubic-bezier(0.25,0.46,0.45,0.94);
  }
  .portfolio-item:hover .portfolio-img { transform: scale(1.05); }
  .portfolio-overlay {
    position: absolute; inset: 0;
    background: linear-gradient(to top, rgba(0,0,0,0.8) 0%, transparent 60%);
    opacity: 0; transition: opacity 0.4s;
    display: flex; align-items: flex-end;
    padding: 24px;
  }
  .portfolio-item:hover .portfolio-overlay { opacity: 1; }
  .portfolio-info h4 {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.2rem; color: var(--cream); font-weight: 300;
  }
  .portfolio-info p { font-size: 0.7rem; color: var(--gold); letter-spacing: 0.2em; }

  /* PROMOÇÕES */
  #promocoes {
    padding: 120px 60px;
    background: linear-gradient(135deg, #0d0a06 0%, #1a1208 50%, #0d0a06 100%);
  }
  .promo-header { max-width: 1200px; margin: 0 auto 60px; }
  .promo-grid {
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: repeat(2, 1fr); gap: 24px;
  }
  .promo-card {
    position: relative; overflow: hidden;
    border: 1px solid rgba(201,169,110,0.2);
    padding: 48px;
    transition: all 0.4s;
  }
  .promo-card::before {
    content: '';
    position: absolute; top: 0; left: 0; right: 0; height: 1px;
    background: linear-gradient(to right, transparent, var(--gold), transparent);
  }
  .promo-card:hover { border-color: rgba(201,169,110,0.5); background: rgba(201,169,110,0.04); }
  .promo-badge {
    display: inline-block; background: var(--gold);
    color: var(--black); padding: 4px 16px;
    font-size: 0.6rem; font-weight: 600; letter-spacing: 0.2em;
    text-transform: uppercase; margin-bottom: 24px;
  }
  .promo-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.8rem; font-weight: 300; margin-bottom: 16px;
  }
  .promo-desc { font-size: 0.85rem; color: var(--text-muted); line-height: 1.8; margin-bottom: 24px; }
  .promo-price-row { display: flex; align-items: center; gap: 16px; margin-bottom: 24px; }
  .promo-original {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.2rem; color: var(--text-muted);
    text-decoration: line-through;
  }
  .promo-new {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem; color: var(--gold);
  }
  .promo-expiry { font-size: 0.65rem; color: var(--text-muted); letter-spacing: 0.1em; }

  /* AGENDAMENTO */
  #agendar {
    padding: 120px 60px;
    background: var(--charcoal);
  }
  .booking-wrap {
    max-width: 1000px; margin: 0 auto;
  }
  .booking-header { margin-bottom: 60px; text-align: center; }
  .booking-form {
    display: grid; grid-template-columns: 1fr 1fr; gap: 24px;
  }
  .form-full { grid-column: 1/-1; }
  .form-group { display: flex; flex-direction: column; gap: 10px; }
  .form-group label {
    font-size: 0.65rem; letter-spacing: 0.25em; text-transform: uppercase;
    color: var(--gold);
  }
  .form-group input,
  .form-group select,
  .form-group textarea {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(201,169,110,0.2);
    color: var(--cream); padding: 16px 20px;
    font-family: 'Raleway', sans-serif;
    font-size: 0.85rem; font-weight: 300;
    outline: none; transition: all 0.3s;
    cursor: none;
  }
  .form-group input:focus,
  .form-group select:focus,
  .form-group textarea:focus {
    border-color: var(--gold);
    background: rgba(201,169,110,0.05);
  }
  .form-group select option { background: var(--charcoal); }
  .form-group textarea { resize: vertical; min-height: 100px; }

  /* UPLOAD REFERÊNCIAS */
  .upload-zone {
    border: 1px dashed rgba(201,169,110,0.4);
    padding: 48px; text-align: center;
    transition: all 0.3s; cursor: none;
    background: rgba(201,169,110,0.02);
  }
  .upload-zone:hover { border-color: var(--gold); background: rgba(201,169,110,0.05); }
  .upload-icon { font-size: 2.5rem; margin-bottom: 16px; display: block; }
  .upload-text { font-size: 0.8rem; color: var(--text-muted); line-height: 1.7; }
  .upload-previews { display: flex; flex-wrap: wrap; gap: 8px; margin-top: 16px; }
  .preview-thumb {
    width: 80px; height: 80px; object-fit: cover;
    border: 1px solid rgba(201,169,110,0.3);
  }
  .booking-submit { margin-top: 16px; width: 100%; padding: 20px; }

  /* LIGHTBOX */
  .lightbox {
    display: none; position: fixed; inset: 0;
    background: rgba(0,0,0,0.95); z-index: 2000;
    align-items: center; justify-content: center;
  }
  .lightbox.open { display: flex; }
  .lightbox-inner {
    max-width: 600px; width: 90%;
    background: var(--charcoal);
    border: 1px solid rgba(201,169,110,0.2);
    padding: 48px; position: relative;
  }
  .lightbox-close {
    position: absolute; top: 20px; right: 20px;
    background: none; border: none; color: var(--gold);
    font-size: 1.5rem; cursor: none;
  }

  /* CONTACT */
  #contato {
    padding: 120px 60px;
    background: var(--black);
  }
  .contact-grid {
    max-width: 1200px; margin: 0 auto;
    display: grid; grid-template-columns: 1fr 1fr; gap: 80px; align-items: start;
  }
  .contact-info h2 { font-family: 'Cormorant Garamond', serif; font-size: 3rem; font-weight: 300; margin-bottom: 32px; }
  .contact-info h2 em { font-style: italic; color: var(--gold); }
  .contact-items { display: flex; flex-direction: column; gap: 24px; }
  .contact-item {
    display: flex; align-items: flex-start; gap: 20px;
    border-bottom: 1px solid rgba(201,169,110,0.1);
    padding-bottom: 24px;
  }
  .contact-icon { font-size: 1.5rem; color: var(--gold); flex-shrink: 0; }
  .contact-detail h4 { font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--gold); margin-bottom: 6px; }
  .contact-detail p { font-size: 0.9rem; color: var(--text-muted); font-weight: 300; }
  .social-links { display: flex; gap: 16px; margin-top: 40px; }
  .social-btn {
    border: 1px solid rgba(201,169,110,0.3);
    padding: 14px 24px;
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    color: var(--cream); text-decoration: none;
    transition: all 0.3s;
  }
  .social-btn:hover { border-color: var(--gold); color: var(--gold); background: rgba(201,169,110,0.05); }

  /* ADMIN PANEL */
  #admin-btn {
    position: fixed; bottom: 30px; right: 30px;
    background: var(--charcoal);
    border: 1px solid rgba(201,169,110,0.3);
    color: var(--gold); padding: 14px 20px;
    font-size: 0.6rem; letter-spacing: 0.2em; text-transform: uppercase;
    font-family: 'Raleway', sans-serif;
    cursor: none; z-index: 500;
    transition: all 0.3s; display: flex; gap: 8px; align-items: center;
  }
  #admin-btn:hover { background: var(--gold); color: var(--black); }

  .admin-modal {
    display: none; position: fixed; inset: 0;
    background: rgba(0,0,0,0.97); z-index: 3000;
    overflow-y: auto;
  }
  .admin-modal.open { display: block; }
  .admin-inner {
    max-width: 900px; margin: 60px auto;
    background: var(--charcoal);
    border: 1px solid rgba(201,169,110,0.3);
    padding: 60px;
  }
  .admin-header {
    display: flex; justify-content: space-between; align-items: center;
    margin-bottom: 48px;
    border-bottom: 1px solid rgba(201,169,110,0.2);
    padding-bottom: 24px;
  }
  .admin-title {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem; font-weight: 300; color: var(--gold);
  }
  .admin-close {
    background: none; border: 1px solid rgba(201,169,110,0.3);
    color: var(--cream); padding: 10px 20px;
    font-family: 'Raleway', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.2em;
    cursor: none; transition: all 0.3s;
  }
  .admin-close:hover { border-color: var(--rose); color: var(--rose); }
  .admin-tabs { display: flex; gap: 2px; margin-bottom: 40px; }
  .admin-tab {
    background: rgba(255,255,255,0.03);
    border: none; border-bottom: 2px solid transparent;
    color: var(--text-muted); padding: 14px 28px;
    font-family: 'Raleway', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.2em; text-transform: uppercase;
    cursor: none; transition: all 0.3s;
  }
  .admin-tab.active { border-bottom-color: var(--gold); color: var(--gold); background: rgba(201,169,110,0.05); }
  .admin-section { display: none; }
  .admin-section.active { display: block; }
  .admin-form { display: flex; flex-direction: column; gap: 20px; }
  .admin-form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 20px; }
  .admin-form input,
  .admin-form select,
  .admin-form textarea {
    background: rgba(255,255,255,0.04);
    border: 1px solid rgba(201,169,110,0.2);
    color: var(--cream); padding: 14px 18px;
    font-family: 'Raleway', sans-serif; font-size: 0.85rem;
    outline: none; width: 100%; transition: all 0.3s;
  }
  .admin-form input:focus,
  .admin-form select:focus,
  .admin-form textarea:focus { border-color: var(--gold); }
  .admin-form textarea { resize: vertical; min-height: 80px; }
  .admin-form label { font-size: 0.6rem; letter-spacing: 0.2em; text-transform: uppercase; color: var(--gold); display: block; margin-bottom: 8px; }
  .admin-submit {
    background: var(--gold); border: none; color: var(--black);
    padding: 16px 40px; font-family: 'Raleway', sans-serif;
    font-size: 0.65rem; letter-spacing: 0.3em; text-transform: uppercase;
    cursor: none; transition: all 0.3s; font-weight: 600;
    align-self: flex-start;
  }
  .admin-submit:hover { background: var(--gold-dark); }
  .admin-list { display: flex; flex-direction: column; gap: 12px; margin-top: 24px; }
  .admin-list-item {
    display: flex; justify-content: space-between; align-items: center;
    padding: 16px 20px;
    border: 1px solid rgba(201,169,110,0.15);
    transition: all 0.3s;
  }
  .admin-list-item:hover { border-color: rgba(201,169,110,0.4); }
  .admin-list-info h4 { font-size: 0.85rem; color: var(--cream); margin-bottom: 4px; }
  .admin-list-info p { font-size: 0.75rem; color: var(--text-muted); }
  .admin-list-actions { display: flex; gap: 8px; }
  .admin-del {
    background: none; border: 1px solid rgba(212,165,160,0.3);
    color: var(--rose); padding: 6px 16px;
    font-size: 0.6rem; letter-spacing: 0.1em; cursor: none;
    font-family: 'Raleway', sans-serif; transition: all 0.3s;
  }
  .admin-del:hover { background: rgba(212,165,160,0.1); }
  .admin-login {
    max-width: 400px; margin: 0 auto; text-align: center;
    padding: 40px;
  }
  .admin-login h3 {
    font-family: 'Cormorant Garamond', serif;
    font-size: 1.5rem; color: var(--gold); margin-bottom: 32px;
  }
  .admin-msg {
    padding: 14px 20px; margin-top: 16px;
    font-size: 0.75rem; letter-spacing: 0.1em;
    display: none;
  }
  .admin-msg.success { background: rgba(201,169,110,0.1); color: var(--gold); border: 1px solid rgba(201,169,110,0.3); display: block; }
  .admin-msg.error { background: rgba(212,165,160,0.1); color: var(--rose); border: 1px solid rgba(212,165,160,0.3); display: block; }

  /* FOOTER */
  footer {
    padding: 60px;
    background: #050505;
    border-top: 1px solid rgba(201,169,110,0.1);
  }
  .footer-inner {
    max-width: 1200px; margin: 0 auto;
    display: flex; justify-content: space-between; align-items: center;
  }
  .footer-logo {
    font-family: 'Cormorant Garamond', serif;
    font-size: 2rem; font-weight: 300;
    color: var(--gold); letter-spacing: 0.15em;
  }
  .footer-copy { font-size: 0.7rem; color: var(--text-muted); letter-spacing: 0.1em; }
  .footer-links { display: flex; gap: 24px; }
  .footer-links a { font-size: 0.65rem; color: var(--text-muted); text-decoration: none; letter-spacing: 0.1em; transition: color 0.3s; }
  .footer-links a:hover { color: var(--gold); }

  /* ANIMATIONS */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(30px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }
  .reveal {
    opacity: 0; transform: translateY(40px);
    transition: all 0.8s cubic-bezier(0.25,0.46,0.45,0.94);
  }
  .reveal.visible { opacity: 1; transform: translateY(0); }

  /* GOLD LINE DIVIDER */
  .gold-divider {
    width: 60px; height: 1px;
    background: linear-gradient(to right, var(--gold), transparent);
    margin: 32px 0;
  }

  /* NOTIFICATION */
  .notification {
    position: fixed; bottom: 90px; right: 30px;
    background: var(--charcoal); border: 1px solid var(--gold);
    padding: 16px 24px; z-index: 4000;
    font-size: 0.75rem; color: var(--cream);
    letter-spacing: 0.1em;
    transform: translateX(120%); transition: transform 0.4s ease;
  }
  .notification.show { transform: translateX(0); }

  /* MOBILE MENU */
  .menu-toggle {
    display: none; flex-direction: column; gap: 5px;
    cursor: none; background: none; border: none; padding: 4px;
  }
  .menu-toggle span { display: block; width: 24px; height: 1px; background: var(--cream); transition: all 0.3s; }

  @media (max-width: 900px) {
    nav { padding: 20px 24px; }
    nav.scrolled { padding: 14px 24px; }
    .nav-links { display: none; }
    .nav-links.open {
      display: flex; flex-direction: column; align-items: flex-start;
      position: fixed; top: 0; left: 0; right: 0;
      background: var(--charcoal); padding: 100px 40px 40px;
      gap: 24px;
    }
    .menu-toggle { display: flex; }
    .hero { min-height: 100svh; }
    .hero-content { padding: 0 24px; }
    .hero-image-side { display: none; }
    .about-grid, .contact-grid { grid-template-columns: 1fr; gap: 48px; }
    .services-grid { grid-template-columns: 1fr; }
    .promo-grid { grid-template-columns: 1fr; }
    .portfolio-masonry { columns: 2; }
    .booking-form { grid-template-columns: 1fr; }
    #sobre, #servicos, #portfolio, #promocoes, #agendar, #contato { padding: 80px 24px; }
    footer { padding: 40px 24px; }
    .footer-inner { flex-direction: column; gap: 24px; text-align: center; }
    .admin-inner { padding: 30px 20px; margin: 20px; }
    .admin-form-row { grid-template-columns: 1fr; }
  }
</style>
</head>
<body>

<!-- CURSOR -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NOTIFICATION -->
<div class="notification" id="notification"></div>

<!-- NAV -->
<nav id="navbar">
  <a href="#" class="nav-logo">C.<span>Helena</span></a>
  <button class="menu-toggle" id="menuToggle" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
  <ul class="nav-links" id="navLinks">
    <li><a href="#sobre">Sobre</a></li>
    <li><a href="#servicos">Serviços</a></li>
    <li><a href="#portfolio">Portfólio</a></li>
    <li><a href="#promocoes">Promoções</a></li>
    <li><a href="#agendar" class="nav-cta">Agendar</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-lines"></div>
  <div class="hero-content">
    <div class="hero-tag">Nail Designer Especialista</div>
    <h1 class="hero-title">
      Arte em<br>
      <em>cada detalhe</em>
    </h1>
    <p class="hero-subtitle">
      Transformando unhas em obras de arte.<br>Sofisticação e exclusividade em cada atendimento.
    </p>
    <div class="hero-actions">
      <a href="#agendar" class="btn-primary">Agendar Horário</a>
      <a href="#portfolio" class="btn-ghost">Ver Portfólio</a>
    </div>
  </div>
  <div class="hero-image-side">
    <div class="nail-art-grid">
      <div class="nail-cell">💅</div>
      <div class="nail-cell">✨</div>
      <div class="nail-cell">🌹</div>
      <div class="nail-cell">💅</div>
    </div>
  </div>
  <div class="hero-scroll">
    <div class="scroll-line"></div>
    Rolar para explorar
  </div>
</section>

<!-- SOBRE -->
<section id="sobre">
  <div class="about-grid">
    <div class="about-image-wrap reveal">
      <div class="about-img-frame">💅</div>
      <div class="about-frame-deco"></div>
      <div class="about-stats">
        <div class="stat-item">
          <div class="stat-num" id="c1">0</div>
          <div class="stat-label">Clientes Atendidas</div>
        </div>
        <div class="stat-item">
          <div class="stat-num" id="c2">0</div>
          <div class="stat-label">Anos de Experiência</div>
        </div>
        <div class="stat-item">
          <div class="stat-num" id="c3">0</div>
          <div class="stat-label">Designs Criados</div>
        </div>
        <div class="stat-item">
          <div class="stat-num" id="c4">0</div>
          <div class="stat-label">Certificações</div>
        </div>
      </div>
    </div>
    <div class="reveal" style="transition-delay: 0.2s">
      <div class="section-label">Sobre mim</div>
      <h2 class="section-title">Helena <em>Perdomo</em></h2>
      <div class="gold-divider"></div>
      <p class="about-text">
        Com mais de 8 anos dedicados à arte das unhas, Helena Perdomo transformou sua paixão em uma especialidade de alto padrão. Especialista em nail art sofisticada, gel, acrílico e técnicas contemporâneas.
      </p>
      <p class="about-text" style="margin-top: 16px">
        Cada atendimento é único. Cada detalhe é pensado. Cada unha é uma tela em branco esperando para se tornar uma obra de arte exclusiva. O estúdio C.Helena é o espaço onde luxo, criatividade e cuidado se encontram.
      </p>
      <div class="signature">Helena Perdomo</div>
      <a href="#agendar" class="btn-primary" style="margin-top: 32px; display: inline-block">Conhecer Serviços</a>
    </div>
  </div>
</section>

<!-- SERVIÇOS -->
<section id="servicos">
  <div class="services-header reveal">
    <div class="section-label">O que ofereço</div>
    <h2 class="section-title">Nossos <em>Serviços</em></h2>
  </div>
  <div class="services-grid" id="servicesGrid">
    <!-- populado por JS -->
  </div>
</section>

<!-- PORTFÓLIO -->
<section id="portfolio">
  <div class="portfolio-header reveal">
    <div>
      <div class="section-label">Trabalhos realizados</div>
      <h2 class="section-title">Port<em>fólio</em></h2>
    </div>
    <div class="portfolio-filter">
      <button class="filter-btn active" data-filter="all">Todos</button>
      <button class="filter-btn" data-filter="gel">Gel</button>
      <button class="filter-btn" data-filter="acrilico">Acrílico</button>
      <button class="filter-btn" data-filter="arte">Nail Art</button>
    </div>
  </div>
  <div class="portfolio-masonry reveal" id="portfolioGrid">
    <!-- populado por JS -->
  </div>
</section>

<!-- PROMOÇÕES -->
<section id="promocoes">
  <div class="promo-header reveal">
    <div class="section-label">Ofertas exclusivas</div>
    <h2 class="section-title">Pro<em>moções</em></h2>
  </div>
  <div class="promo-grid" id="promoGrid">
    <!-- populado por JS -->
  </div>
</section>

<!-- AGENDAMENTO -->
<section id="agendar">
  <div class="booking-wrap">
    <div class="booking-header reveal">
      <div class="section-label">Reserve seu horário</div>
      <h2 class="section-title">Faça seu <em>Agendamento</em></h2>
      <p style="color: var(--text-muted); font-size: 0.9rem; font-weight: 300; margin-top: 16px">
        Preencha o formulário e entraremos em contato para confirmar seu horário
      </p>
    </div>
    <div class="booking-form reveal" id="bookingForm">
      <div class="form-group">
        <label>Nome Completo</label>
        <input type="text" id="bName" placeholder="Seu nome">
      </div>
      <div class="form-group">
        <label>Telefone / WhatsApp</label>
        <input type="tel" id="bPhone" placeholder="(00) 00000-0000">
      </div>
      <div class="form-group">
        <label>Serviço Desejado</label>
        <select id="bService">
          <option value="">Selecione o serviço</option>
          <option>Gel Claro</option>
          <option>Gel com Decoração</option>
          <option>Acrílico Natural</option>
          <option>Nail Art Personalizada</option>
          <option>Manutenção</option>
          <option>Remoção</option>
        </select>
      </div>
      <div class="form-group">
        <label>Data Preferida</label>
        <input type="date" id="bDate">
      </div>
      <div class="form-group">
        <label>Horário Preferido</label>
        <select id="bTime">
          <option value="">Selecione o horário</option>
          <option>09:00</option>
          <option>10:00</option>
          <option>11:00</option>
          <option>13:00</option>
          <option>14:00</option>
          <option>15:00</option>
          <option>16:00</option>
          <option>17:00</option>
        </select>
      </div>
      <div class="form-group">
        <label>Observações</label>
        <textarea id="bNotes" placeholder="Conte-me sobre o que você deseja..."></textarea>
      </div>
      <div class="form-group form-full">
        <label>Referências de Unhas (opcional)</label>
        <div class="upload-zone" id="uploadZone" onclick="document.getElementById('fileInput').click()">
          <span class="upload-icon">🖼️</span>
          <div class="upload-text">
            <strong style="color: var(--gold)">Clique para enviar imagens</strong><br>
            Referências, inspirações, fotos de unhas que você deseja<br>
            <span style="font-size: 0.7rem">JPG, PNG, WEBP — Máximo 5 imagens</span>
          </div>
          <div class="upload-previews" id="uploadPreviews"></div>
        </div>
        <input type="file" id="fileInput" accept="image/*" multiple style="display:none">
      </div>
      <div class="form-full">
        <button class="btn-primary booking-submit" onclick="submitBooking()">
          Solicitar Agendamento
        </button>
      </div>
    </div>
  </div>
</section>

<!-- CONTATO -->
<section id="contato">
  <div class="contact-grid">
    <div class="reveal">
      <div class="section-label">Fale conosco</div>
      <h2 class="contact-info"><span class="section-title">Entre em <em>Contato</em></span></h2>
      <div class="gold-divider"></div>
      <div class="contact-items">
        <div class="contact-item">
          <div class="contact-icon">📍</div>
          <div class="contact-detail">
            <h4>Localização</h4>
            <p>Rua das Flores, 123 — Belo Horizonte, MG</p>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon">📱</div>
          <div class="contact-detail">
            <h4>WhatsApp</h4>
            <p>(31) 99999-9999</p>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon">🕐</div>
          <div class="contact-detail">
            <h4>Horário de Atendimento</h4>
            <p>Terça a Sábado: 9h às 18h</p>
          </div>
        </div>
        <div class="contact-item">
          <div class="contact-icon">✉️</div>
          <div class="contact-detail">
            <h4>E-mail</h4>
            <p>contato@chelena.com.br</p>
          </div>
        </div>
      </div>
      <div class="social-links">
        <a href="#" class="social-btn">Instagram</a>
        <a href="#" class="social-btn">WhatsApp</a>
        <a href="#" class="social-btn">TikTok</a>
      </div>
    </div>
    <div class="reveal" style="transition-delay: 0.2s">
      <div class="about-img-frame" style="aspect-ratio: 4/3; font-size: 6rem; background: linear-gradient(135deg, #1a0f0a, #2a1a10)">
        🌹
      </div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="footer-logo">C.Helena</div>
    <div class="footer-copy">© 2025 C.Helena Nail Designer — Helena Perdomo</div>
    <div class="footer-links">
      <a href="#sobre">Sobre</a>
      <a href="#servicos">Serviços</a>
      <a href="#portfolio">Portfólio</a>
    </div>
  </div>
</footer>

<!-- ADMIN BUTTON -->
<button id="admin-btn" onclick="openAdmin()">⚙ Área Admin</button>

<!-- ADMIN MODAL -->
<div class="admin-modal" id="adminModal">
  <div class="admin-inner">
    <div id="adminLoginSection" class="admin-login">
      <h3>Acesso Restrito</h3>
      <div class="form-group">
        <label>Senha de acesso</label>
        <input type="password" id="adminPass" placeholder="Digite a senha" onkeydown="if(event.key==='Enter')loginAdmin()">
      </div>
      <button class="admin-submit" style="margin-top: 20px; width: 100%; align-self: auto" onclick="loginAdmin()">Entrar</button>
      <div class="admin-msg" id="adminMsg"></div>
      <button onclick="closeAdmin()" style="background:none;border:none;color:var(--text-muted);margin-top:20px;font-size:0.75rem;cursor:none;text-decoration:underline;font-family:'Raleway',sans-serif">Cancelar</button>
    </div>
    <div id="adminPanel" style="display:none">
      <div class="admin-header">
        <div class="admin-title">Painel C.Helena</div>
        <button class="admin-close" onclick="closeAdmin()">✕ Fechar</button>
      </div>
      <div class="admin-tabs">
        <button class="admin-tab active" onclick="switchTab('agendamentos')">Agendamentos</button>
        <button class="admin-tab" onclick="switchTab('portfolio')">Portfólio</button>
        <button class="admin-tab" onclick="switchTab('promocoes')">Promoções</button>
        <button class="admin-tab" onclick="switchTab('servicos')">Serviços</button>
      </div>

      <!-- Agendamentos -->
      <div class="admin-section active" id="tab-agendamentos">
        <h3 style="font-family:'Cormorant Garamond',serif;font-size:1.4rem;color:var(--gold);margin-bottom:24px;font-weight:300">
          Solicitações de Agendamento
        </h3>
        <div class="admin-list" id="adminBookings"></div>
      </div>

      <!-- Portfolio -->
      <div class="admin-section" id="tab-portfolio">
        <h3 style="font-family:'Cormorant Garamond',serif;font-size:1.4rem;color:var(--gold);margin-bottom:24px;font-weight:300">
          Adicionar ao Portfólio
        </h3>
        <div class="admin-form">
          <div class="admin-form-row">
            <div>
              <label>Título da Imagem</label>
              <input type="text" id="pTitle" placeholder="Ex: Gel Rosa Nude">
            </div>
            <div>
              <label>Categoria</label>
              <select id="pCategory">
                <option value="gel">Gel</option>
                <option value="acrilico">Acrílico</option>
                <option value="arte">Nail Art</option>
              </select>
            </div>
          </div>
          <div>
            <label>Emoji / Ícone representativo</label>
            <input type="text" id="pEmoji" placeholder="💅 ou 🌹 ou ✨">
          </div>
          <div>
            <label>Cores (estilo CSS gradiente para o preview)</label>
            <select id="pColor">
              <option value="linear-gradient(135deg,#2a1f15,#4a3020)">Tom dourado</option>
              <option value="linear-gradient(135deg,#1E0E12,#3E2020)">Tom rosé</option>
              <option value="linear-gradient(135deg,#0A0818,#1A1030)">Tom vinho</option>
              <option value="linear-gradient(135deg,#0A1020,#101830)">Tom azul</option>
              <option value="linear-gradient(135deg,#101810,#202820)">Tom esmeralda</option>
            </select>
          </div>
          <div>
            <label>Altura do item (pequeno / médio / grande)</label>
            <select id="pHeight">
              <option value="160px">Pequeno (160px)</option>
              <option value="220px" selected>Médio (220px)</option>
              <option value="300px">Grande (300px)</option>
            </select>
          </div>
          <button class="admin-submit" onclick="addPortfolioItem()">+ Adicionar ao Portfólio</button>
        </div>
        <div class="admin-list" id="adminPortfolioList" style="margin-top:32px"></div>
      </div>

      <!-- Promoções -->
      <div class="admin-section" id="tab-promocoes">
        <h3 style="font-family:'Cormorant Garamond',serif;font-size:1.4rem;color:var(--gold);margin-bottom:24px;font-weight:300">
          Gerenciar Promoções
        </h3>
        <div class="admin-form">
          <div class="admin-form-row">
            <div>
              <label>Nome da Promoção</label>
              <input type="text" id="promoName" placeholder="Ex: Combo Inverno">
            </div>
            <div>
              <label>Badge</label>
              <input type="text" id="promoBadge" placeholder="Ex: OFERTA ESPECIAL">
            </div>
          </div>
          <div>
            <label>Descrição</label>
            <textarea id="promoDesc" placeholder="Descreva a promoção..."></textarea>
          </div>
          <div class="admin-form-row">
            <div>
              <label>Preço Original (R$)</label>
              <input type="number" id="promoOriginal" placeholder="150">
            </div>
            <div>
              <label>Preço Promocional (R$)</label>
              <input type="number" id="promoNew" placeholder="120">
            </div>
          </div>
          <div>
            <label>Válido até</label>
            <input type="date" id="promoDate">
          </div>
          <button class="admin-submit" onclick="addPromo()">+ Publicar Promoção</button>
        </div>
        <div class="admin-list" id="adminPromoList" style="margin-top:32px"></div>
      </div>

      <!-- Serviços -->
      <div class="admin-section" id="tab-servicos">
        <h3 style="font-family:'Cormorant Garamond',serif;font-size:1.4rem;color:var(--gold);margin-bottom:24px;font-weight:300">
          Gerenciar Serviços
        </h3>
        <div class="admin-form">
          <div class="admin-form-row">
            <div>
              <label>Nome do Serviço</label>
              <input type="text" id="svcName" placeholder="Ex: Gel Claro">
            </div>
            <div>
              <label>Ícone (emoji)</label>
              <input type="text" id="svcIcon" placeholder="💅">
            </div>
          </div>
          <div>
            <label>Descrição</label>
            <textarea id="svcDesc" placeholder="Descrição do serviço..."></textarea>
          </div>
          <div>
            <label>Preço (R$)</label>
            <input type="number" id="svcPrice" placeholder="0">
          </div>
          <button class="admin-submit" onclick="addService()">+ Adicionar Serviço</button>
        </div>
        <div class="admin-list" id="adminServiceList" style="margin-top:32px"></div>
      </div>
    </div>
  </div>
</div>

<script>
// ————— DATA STATE —————
const state = {
  bookings: JSON.parse(localStorage.getItem('chelena_bookings') || '[]'),
  portfolio: JSON.parse(localStorage.getItem('chelena_portfolio') || JSON.stringify([
    { id: 1, title: 'Gel Rosé Nude', category: 'gel', emoji: '💅', color: 'linear-gradient(135deg,#2a1018,#4a2030)', height: '220px' },
    { id: 2, title: 'Nail Art Floral', category: 'arte', emoji: '🌸', color: 'linear-gradient(135deg,#1a0818,#3a1028)', height: '300px' },
    { id: 3, title: 'Acrílico Natural', category: 'acrilico', emoji: '✨', color: 'linear-gradient(135deg,#1a1510,#2a2010)', height: '160px' },
    { id: 4, title: 'Gel Bordô', category: 'gel', emoji: '🍷', color: 'linear-gradient(135deg,#200808,#401010)', height: '220px' },
    { id: 5, title: 'Nail Art Geométrica', category: 'arte', emoji: '◇', color: 'linear-gradient(135deg,#080820,#181838)', height: '300px' },
    { id: 6, title: 'Francesinha Dourada', category: 'gel', emoji: '✨', color: 'linear-gradient(135deg,#1a1208,#2a2010)', height: '160px' },
    { id: 7, title: 'Acrílico Almendrado', category: 'acrilico', emoji: '💎', color: 'linear-gradient(135deg,#0a1220,#141c30)', height: '220px' },
    { id: 8, title: 'Nail Art Marmorizada', category: 'arte', emoji: '🤍', color: 'linear-gradient(135deg,#1a1a1a,#2a2a2a)', height: '260px' },
  ])),
  promos: JSON.parse(localStorage.getItem('chelena_promos') || JSON.stringify([
    { id: 1, name: 'Combo Outono', badge: 'OFERTA ESPECIAL', desc: 'Gel completo com nail art personalizada e esmaltação das mãos. Perfeito para renovar o look.', original: 180, novo: 140, date: '2025-09-30' },
    { id: 2, name: 'Manutenção Express', badge: 'PROMOÇÃO RELÂMPAGO', desc: 'Manutenção completa do gel com refile e uma decoração surpresa inclusa. Agende até domingo!', original: 120, novo: 89, date: '2025-08-15' },
  ])),
  services: JSON.parse(localStorage.getItem('chelena_services') || JSON.stringify([
    { id: 1, name: 'Gel Claro & Nude', icon: '💅', desc: 'Extensão de gel nas tonalidades claro e nude. Alta durabilidade e acabamento impecável.', price: 120 },
    { id: 2, name: 'Nail Art Personalizada', icon: '🎨', desc: 'Criações exclusivas com designs sob medida para o seu estilo.', price: 160 },
    { id: 3, name: 'Acrílico Premium', icon: '💎', desc: 'Extensão acrílica com acabamento natural e longa duração.', price: 140 },
    { id: 4, name: 'Gel com Decoração', icon: '✨', desc: 'Gel colorido com decorações artísticas, glitter e pedrarias.', price: 150 },
    { id: 5, name: 'Manutenção Gel', icon: '🔄', desc: 'Refile e retoque do crescimento com pintura nova.', price: 80 },
    { id: 6, name: 'Remoção Segura', icon: '🌿', desc: 'Remoção profissional sem danos à lâmina natural.', price: 60 },
  ])),
};

function save() {
  localStorage.setItem('chelena_bookings', JSON.stringify(state.bookings));
  localStorage.setItem('chelena_portfolio', JSON.stringify(state.portfolio));
  localStorage.setItem('chelena_promos', JSON.stringify(state.promos));
  localStorage.setItem('chelena_services', JSON.stringify(state.services));
}

// ————— CURSOR —————
const cursor = document.getElementById('cursor');
const ring = document.getElementById('cursorRing');
document.addEventListener('mousemove', e => {
  cursor.style.left = e.clientX + 'px';
  cursor.style.top = e.clientY + 'px';
  ring.style.left = e.clientX + 'px';
  ring.style.top = e.clientY + 'px';
});

// ————— NAV SCROLL —————
window.addEventListener('scroll', () => {
  document.getElementById('navbar').classList.toggle('scrolled', window.scrollY > 60);
});

// ————— MOBILE MENU —————
document.getElementById('menuToggle').addEventListener('click', function() {
  const links = document.getElementById('navLinks');
  links.classList.toggle('open');
});
document.querySelectorAll('.nav-links a').forEach(a => {
  a.addEventListener('click', () => document.getElementById('navLinks').classList.remove('open'));
});

// ————— REVEAL ON SCROLL —————
const io = new IntersectionObserver(entries => {
  entries.forEach(e => { if (e.isIntersecting) e.target.classList.add('visible'); });
}, { threshold: 0.1 });
document.querySelectorAll('.reveal').forEach(el => io.observe(el));

// ————— COUNTER ANIMATION —————
function animateCounter(el, target, suffix='') {
  let start = 0;
  const step = Math.ceil(target / 60);
  const timer = setInterval(() => {
    start += step;
    if (start >= target) { start = target; clearInterval(timer); }
    el.textContent = start + suffix;
  }, 30);
}
const counterIO = new IntersectionObserver(entries => {
  entries.forEach(e => {
    if (e.isIntersecting) {
      animateCounter(document.getElementById('c1'), 500, '+');
      animateCounter(document.getElementById('c2'), 8);
      animateCounter(document.getElementById('c3'), 1200, '+');
      animateCounter(document.getElementById('c4'), 12);
      counterIO.disconnect();
    }
  });
});
counterIO.observe(document.getElementById('sobre'));

// ————— RENDER SERVICES —————
function renderServices() {
  const grid = document.getElementById('servicesGrid');
  grid.innerHTML = state.services.map(s => `
    <div class="service-card reveal">
      <span class="service-icon">${s.icon}</span>
      <div class="service-name">${s.name}</div>
      <div class="service-desc">${s.desc}</div>
      <div class="service-price">R$ ${s.price}<span>,00</span></div>
    </div>
  `).join('');
  document.querySelectorAll('.service-card').forEach(el => io.observe(el));
}

// ————— RENDER PORTFOLIO —————
function renderPortfolio(filter = 'all') {
  const grid = document.getElementById('portfolioGrid');
  const items = filter === 'all' ? state.portfolio : state.portfolio.filter(p => p.category === filter);
  grid.innerHTML = items.map(p => `
    <div class="portfolio-item" data-category="${p.category}">
      <div class="portfolio-img" style="height:${p.height};background:${p.color};display:flex;align-items:center;justify-content:center;font-size:3rem;">${p.emoji}</div>
      <div class="portfolio-overlay">
        <div class="portfolio-info">
          <h4>${p.title}</h4>
          <p>${p.category.toUpperCase()}</p>
        </div>
      </div>
    </div>
  `).join('');
}
document.querySelectorAll('.filter-btn').forEach(btn => {
  btn.addEventListener('click', function() {
    document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
    this.classList.add('active');
    renderPortfolio(this.dataset.filter);
  });
});

// ————— RENDER PROMOS —————
function renderPromos() {
  const grid = document.getElementById('promoGrid');
  if (!state.promos.length) {
    grid.innerHTML = '<div style="color:var(--text-muted);font-size:0.9rem;padding:40px 0">Nenhuma promoção ativa no momento.</div>';
    return;
  }
  grid.innerHTML = state.promos.map(p => `
    <div class="promo-card reveal">
      <span class="promo-badge">${p.badge}</span>
      <div class="promo-title">${p.name}</div>
      <div class="promo-desc">${p.desc}</div>
      <div class="promo-price-row">
        <div class="promo-original">R$ ${p.original},00</div>
        <div class="promo-new">R$ ${p.novo},00</div>
      </div>
      <div class="promo-expiry">Válido até ${p.date ? new Date(p.date + 'T12:00').toLocaleDateString('pt-BR') : '—'}</div>
      <a href="#agendar" class="btn-primary" style="margin-top:24px;display:inline-block;font-size:0.6rem">Aproveitar</a>
    </div>
  `).join('');
  document.querySelectorAll('.promo-card').forEach(el => io.observe(el));
}

// ————— UPLOAD REFERENCES —————
document.getElementById('fileInput').addEventListener('change', function() {
  const container = document.getElementById('uploadPreviews');
  container.innerHTML = '';
  Array.from(this.files).slice(0,5).forEach(file => {
    const reader = new FileReader();
    reader.onload = e => {
      const img = document.createElement('img');
      img.src = e.target.result; img.className = 'preview-thumb';
      container.appendChild(img);
    };
    reader.readAsDataURL(file);
  });
});

// ————— BOOKING SUBMIT —————
function submitBooking() {
  const name = document.getElementById('bName').value.trim();
  const phone = document.getElementById('bPhone').value.trim();
  const service = document.getElementById('bService').value;
  const date = document.getElementById('bDate').value;
  const time = document.getElementById('bTime').value;
  if (!name || !phone || !service || !date || !time) {
    showNotification('Por favor, preencha todos os campos obrigatórios.');
    return;
  }
  const booking = { id: Date.now(), name, phone, service, date, time, notes: document.getElementById('bNotes').value, timestamp: new Date().toLocaleString('pt-BR'), status: 'Aguardando' };
  state.bookings.unshift(booking);
  save();
  showNotification('✨ Agendamento solicitado com sucesso! Entraremos em contato.');
  ['bName','bPhone','bNotes'].forEach(id => document.getElementById(id).value = '');
  ['bService','bDate','bTime'].forEach(id => document.getElementById(id).value = '');
  document.getElementById('uploadPreviews').innerHTML = '';
}

// ————— NOTIFICATION —————
function showNotification(msg) {
  const el = document.getElementById('notification');
  el.textContent = msg; el.classList.add('show');
  setTimeout(() => el.classList.remove('show'), 4000);
}

// ————— ADMIN —————
const ADMIN_PASS = 'chelena2025';
function openAdmin() {
  document.getElementById('adminModal').classList.add('open');
}
function closeAdmin() {
  document.getElementById('adminModal').classList.remove('open');
  document.getElementById('adminPanel').style.display = 'none';
  document.getElementById('adminLoginSection').style.display = 'block';
  document.getElementById('adminPass').value = '';
  document.getElementById('adminMsg').className = 'admin-msg';
}
function loginAdmin() {
  const pass = document.getElementById('adminPass').value;
  if (pass === ADMIN_PASS) {
    document.getElementById('adminLoginSection').style.display = 'none';
    document.getElementById('adminPanel').style.display = 'block';
    renderAdminBookings(); renderAdminPortfolio(); renderAdminPromos(); renderAdminServices();
  } else {
    const msg = document.getElementById('adminMsg');
    msg.textContent = 'Senha incorreta. Tente novamente.';
    msg.className = 'admin-msg error';
  }
}
function switchTab(tab) {
  document.querySelectorAll('.admin-tab').forEach(t => t.classList.remove('active'));
  document.querySelectorAll('.admin-section').forEach(s => s.classList.remove('active'));
  event.target.classList.add('active');
  document.getElementById('tab-'+tab).classList.add('active');
}

function renderAdminBookings() {
  const el = document.getElementById('adminBookings');
  if (!state.bookings.length) { el.innerHTML = '<p style="color:var(--text-muted);font-size:0.85rem">Nenhum agendamento recebido ainda.</p>'; return; }
  el.innerHTML = state.bookings.map(b => `
    <div class="admin-list-item">
      <div class="admin-list-info">
        <h4>${b.name} — ${b.service}</h4>
        <p>${b.date} às ${b.time} · ${b.phone} · ${b.timestamp}</p>
        ${b.notes ? `<p style="margin-top:4px;font-style:italic">Obs: ${b.notes}</p>` : ''}
      </div>
      <div class="admin-list-actions">
        <button class="admin-del" onclick="deleteBooking(${b.id})">Remover</button>
      </div>
    </div>
  `).join('');
}
function deleteBooking(id) {
  state.bookings = state.bookings.filter(b => b.id !== id); save(); renderAdminBookings();
}

function renderAdminPortfolio() {
  const el = document.getElementById('adminPortfolioList');
  el.innerHTML = state.portfolio.map(p => `
    <div class="admin-list-item">
      <div class="admin-list-info">
        <h4>${p.emoji} ${p.title}</h4>
        <p>${p.category}</p>
      </div>
      <button class="admin-del" onclick="deletePortfolio(${p.id})">Remover</button>
    </div>
  `).join('');
}
function addPortfolioItem() {
  const title = document.getElementById('pTitle').value.trim();
  const emoji = document.getElementById('pEmoji').value.trim() || '💅';
  if (!title) { alert('Informe o título'); return; }
  state.portfolio.push({ id: Date.now(), title, category: document.getElementById('pCategory').value, emoji, color: document.getElementById('pColor').value, height: document.getElementById('pHeight').value });
  save(); renderPortfolio(); renderAdminPortfolio();
  document.getElementById('pTitle').value = ''; document.getElementById('pEmoji').value = '';
  showNotification('✨ Item adicionado ao portfólio!');
}
function deletePortfolio(id) {
  state.portfolio = state.portfolio.filter(p => p.id !== id); save(); renderPortfolio(); renderAdminPortfolio();
}

function renderAdminPromos() {
  const el = document.getElementById('adminPromoList');
  if (!state.promos.length) { el.innerHTML = '<p style="color:var(--text-muted);font-size:0.85rem">Sem promoções cadastradas.</p>'; return; }
  el.innerHTML = state.promos.map(p => `
    <div class="admin-list-item">
      <div class="admin-list-info">
        <h4>${p.name}</h4>
        <p>De R$ ${p.original} por R$ ${p.novo} · Até ${p.date ? new Date(p.date+'T12:00').toLocaleDateString('pt-BR') : '—'}</p>
      </div>
      <button class="admin-del" onclick="deletePromo(${p.id})">Remover</button>
    </div>
  `).join('');
}
function addPromo() {
  const name = document.getElementById('promoName').value.trim();
  if (!name) { alert('Informe o nome'); return; }
  state.promos.unshift({ id: Date.now(), name, badge: document.getElementById('promoBadge').value || 'PROMOÇÃO', desc: document.getElementById('promoDesc').value, original: +document.getElementById('promoOriginal').value, novo: +document.getElementById('promoNew').value, date: document.getElementById('promoDate').value });
  save(); renderPromos(); renderAdminPromos();
  ['promoName','promoBadge','promoDesc','promoOriginal','promoNew','promoDate'].forEach(id => document.getElementById(id).value = '');
  showNotification('🎉 Promoção publicada!');
}
function deletePromo(id) {
  state.promos = state.promos.filter(p => p.id !== id); save(); renderPromos(); renderAdminPromos();
}

function renderAdminServices() {
  const el = document.getElementById('adminServiceList');
  el.innerHTML = state.services.map(s => `
    <div class="admin-list-item">
      <div class="admin-list-info">
        <h4>${s.icon} ${s.name}</h4>
        <p>R$ ${s.price},00</p>
      </div>
      <button class="admin-del" onclick="deleteService(${s.id})">Remover</button>
    </div>
  `).join('');
}
function addService() {
  const name = document.getElementById('svcName').value.trim();
  if (!name) { alert('Informe o nome'); return; }
  state.services.push({ id: Date.now(), name, icon: document.getElementById('svcIcon').value || '💅', desc: document.getElementById('svcDesc').value, price: +document.getElementById('svcPrice').value });
  save(); renderServices(); renderAdminServices();
  ['svcName','svcIcon','svcDesc','svcPrice'].forEach(id => document.getElementById(id).value = '');
  showNotification('✅ Serviço adicionado!');
}
function deleteService(id) {
  state.services = state.services.filter(s => s.id !== id); save(); renderServices(); renderAdminServices();
}

// ————— INIT —————
renderServices();
renderPortfolio();
renderPromos();

// Set min date for booking
const today = new Date().toISOString().split('T')[0];
document.getElementById('bDate').setAttribute('min', today);

// Booking service sync with services list
function syncServiceOptions() {
  const sel = document.getElementById('bService');
  const val = sel.value;
  sel.innerHTML = '<option value="">Selecione o serviço</option>' + state.services.map(s => `<option>${s.name}</option>`).join('');
  sel.value = val;
}
syncServiceOptions();
</script>
</body>
</html>