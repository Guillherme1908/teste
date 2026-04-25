
<!DOCTYPE html>
<html lang="pt-BR">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0">
<title>C.Helena — Nail Designer</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=Raleway:wght@200;300;400;500&display=swap" rel="stylesheet">
<style>
/* ===== RESET & ROOT ===== */
:root {
  --cream: #F5EFE6;
  --gold: #C9A96E;
  --gold-dark: #9B7940;
  --black: #0A0A0A;
  --charcoal: #1A1A1A;
  --text-muted: #7A6E62;
  --rose: #D4A5A0;
  --nav-h: 68px;
}
*, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
html { scroll-behavior: smooth; -webkit-text-size-adjust: 100%; }
body { font-family: 'Raleway', sans-serif; background: var(--black); color: var(--cream); overflow-x: hidden; }
img { max-width: 100%; display: block; }
a { text-decoration: none; color: inherit; }
button { font-family: 'Raleway', sans-serif; }
::-webkit-scrollbar { width: 3px; }
::-webkit-scrollbar-track { background: var(--black); }
::-webkit-scrollbar-thumb { background: var(--gold); }

/* ===== CURSOR — desktop only ===== */
@media (pointer: fine) {
  body { cursor: none; }
  .cursor { width:8px;height:8px;background:var(--gold);border-radius:50%;position:fixed;top:0;left:0;pointer-events:none;z-index:9999;transform:translate(-50%,-50%);transition:transform .1s; }
  .cursor-ring { width:30px;height:30px;border:1px solid var(--gold);border-radius:50%;position:fixed;top:0;left:0;pointer-events:none;z-index:9998;transform:translate(-50%,-50%);transition:all .3s ease;opacity:.6; }
}

/* ===== NOTIFICATION ===== */
.notification {
  position:fixed;bottom:80px;left:16px;right:16px;
  background:var(--charcoal);border:1px solid var(--gold);
  padding:13px 18px;z-index:4000;font-size:.75rem;color:var(--cream);
  letter-spacing:.08em;text-align:center;
  transform:translateY(160%);transition:transform .4s ease;
}
.notification.show { transform:translateY(0); }
@media(min-width:560px){ .notification{left:auto;width:360px;right:20px;text-align:left;} }

/* ===== NAV ===== */
nav {
  position:fixed;top:0;left:0;right:0;z-index:1000;height:var(--nav-h);
  padding:0 20px;display:flex;justify-content:space-between;align-items:center;
  transition:background .4s,border-color .4s;
}
nav.scrolled { background:rgba(10,10,10,.96);backdrop-filter:blur(20px);border-bottom:1px solid rgba(201,169,110,.2); }
.nav-logo { font-family:'Cormorant Garamond',serif;font-size:1.75rem;font-weight:300;letter-spacing:.15em;color:var(--gold);flex-shrink:0; }
.nav-logo span { font-style:italic;color:var(--cream); }
.nav-links { display:flex;gap:28px;list-style:none;align-items:center; }
.nav-links a { font-size:.67rem;font-weight:400;letter-spacing:.22em;text-transform:uppercase;color:var(--cream);opacity:.75;transition:all .3s;position:relative; }
.nav-links a::after { content:'';position:absolute;bottom:-3px;left:0;width:0;height:1px;background:var(--gold);transition:width .3s; }
.nav-links a:hover { opacity:1;color:var(--gold); }
.nav-links a:hover::after { width:100%; }
.nav-cta { background:transparent;border:1px solid var(--gold);color:var(--gold)!important;opacity:1!important;padding:9px 22px;letter-spacing:.18em;font-size:.62rem!important; }
.nav-cta:hover { background:var(--gold)!important;color:var(--black)!important; }
.nav-cta::after { display:none!important; }
/* hamburger */
.menu-toggle { display:none;flex-direction:column;justify-content:center;gap:5px;background:none;border:none;padding:6px;cursor:pointer;z-index:1100; }
.menu-toggle span { display:block;width:22px;height:1px;background:var(--cream);transition:all .3s; }
.menu-toggle.open span:nth-child(1) { transform:translateY(6px) rotate(45deg); }
.menu-toggle.open span:nth-child(2) { opacity:0; }
.menu-toggle.open span:nth-child(3) { transform:translateY(-6px) rotate(-45deg); }
@media(max-width:860px){
  .menu-toggle { display:flex; }
  .nav-links { display:none;flex-direction:column;align-items:flex-start;position:fixed;inset:0;background:rgba(10,10,10,.98);padding:calc(var(--nav-h) + 32px) 32px 40px;gap:28px;z-index:1050; }
  .nav-links.open { display:flex; }
  .nav-links a { font-size:1.05rem;letter-spacing:.2em;opacity:1; }
  .nav-cta { padding:14px 32px;font-size:.8rem!important; }
}
@media(min-width:861px){ nav { padding:0 52px; } }

/* ===== BUTTONS ===== */
.btn-primary { display:inline-block;background:var(--gold);color:var(--black);border:none;padding:14px 34px;font-size:.64rem;font-weight:500;letter-spacing:.28em;text-transform:uppercase;transition:all .4s;white-space:nowrap; }
.btn-primary:hover { background:var(--gold-dark);transform:translateY(-2px);box-shadow:0 16px 36px rgba(201,169,110,.3); }
.btn-ghost { display:inline-block;background:transparent;color:var(--cream);border:1px solid rgba(245,239,230,.3);padding:14px 34px;font-size:.64rem;font-weight:400;letter-spacing:.28em;text-transform:uppercase;transition:all .4s;white-space:nowrap; }
.btn-ghost:hover { border-color:var(--gold);color:var(--gold); }

/* ===== SECTION COMMON ===== */
section { position:relative; }
.section-label { font-size:.58rem;letter-spacing:.38em;text-transform:uppercase;color:var(--gold);margin-bottom:14px;display:flex;align-items:center;gap:12px; }
.section-label::before { content:'';width:26px;height:1px;background:var(--gold);flex-shrink:0; }
.section-title { font-family:'Cormorant Garamond',serif;font-size:clamp(2rem,6vw,3.8rem);font-weight:300;line-height:1.1;margin-bottom:18px; }
.section-title em { font-style:italic;color:var(--gold); }
.gold-divider { width:52px;height:1px;background:linear-gradient(to right,var(--gold),transparent);margin:24px 0; }
.reveal { opacity:0;transform:translateY(32px);transition:all .8s cubic-bezier(.25,.46,.45,.94); }
.reveal.visible { opacity:1;transform:translateY(0); }
@keyframes fadeUp { from{opacity:0;transform:translateY(26px)}to{opacity:1;transform:translateY(0)} }
@keyframes fadeIn  { from{opacity:0}to{opacity:1} }
@keyframes scrollLine {
  0%   { transform:scaleY(0);transform-origin:top; }
  50%  { transform:scaleY(1);transform-origin:top; }
  51%  { transform-origin:bottom; }
  100% { transform:scaleY(0);transform-origin:bottom; }
}

/* ===== HERO ===== */
.hero { min-height:100svh;display:flex;align-items:center;position:relative;overflow:hidden;background:var(--black);padding-top:var(--nav-h); }
.hero-bg { position:absolute;inset:0;background:radial-gradient(ellipse at 70% 50%,rgba(201,169,110,.07) 0%,transparent 60%),radial-gradient(ellipse at 20% 80%,rgba(212,165,160,.05) 0%,transparent 50%); }
.hero-lines { position:absolute;inset:0;background-image:linear-gradient(rgba(201,169,110,.03) 1px,transparent 1px),linear-gradient(90deg,rgba(201,169,110,.03) 1px,transparent 1px);background-size:70px 70px; }
.hero-content { position:relative;z-index:2;padding:40px 24px 80px;width:100%; }
.hero-tag { font-size:.58rem;letter-spacing:.35em;text-transform:uppercase;color:var(--gold);margin-bottom:22px;display:flex;align-items:center;gap:12px;opacity:0;animation:fadeUp 1s .3s forwards; }
.hero-tag::before { content:'';width:32px;height:1px;background:var(--gold);flex-shrink:0; }
.hero-title { font-family:'Cormorant Garamond',serif;font-size:clamp(3rem,10vw,6rem);font-weight:300;line-height:.95;opacity:0;animation:fadeUp 1s .5s forwards; }
.hero-title em { font-style:italic;color:var(--gold);display:block; }
.hero-subtitle { font-family:'Cormorant Garamond',serif;font-size:clamp(.9rem,2.5vw,1.25rem);font-weight:300;color:var(--text-muted);letter-spacing:.07em;margin:18px 0 36px;line-height:1.75;opacity:0;animation:fadeUp 1s .7s forwards; }
.hero-actions { display:flex;gap:14px;flex-wrap:wrap;align-items:center;opacity:0;animation:fadeUp 1s .9s forwards; }
.hero-image-side { position:absolute;right:0;top:0;bottom:0;width:42%;overflow:hidden; }
.hero-image-side::before { content:'';position:absolute;left:0;inset-y:0;width:160px;background:linear-gradient(to right,var(--black),transparent);z-index:2; }
.nail-art-grid { display:grid;grid-template-columns:1fr 1fr;gap:3px;width:100%;height:100%;opacity:0;animation:fadeIn 1.5s 1.2s forwards; }
.nail-cell { background:linear-gradient(135deg,#2a1f15,#1a1208);display:flex;align-items:center;justify-content:center;font-size:3.6rem; }
.nail-cell:nth-child(1){ background:linear-gradient(135deg,#2C1810,#4A2E1A);font-size:4.5rem; }
.nail-cell:nth-child(2){ background:linear-gradient(135deg,#1A1208,#2E1F0A); }
.nail-cell:nth-child(3){ background:linear-gradient(135deg,#0A0806,#1A1510); }
.nail-cell:nth-child(4){ background:linear-gradient(135deg,#1E0E12,#2E1518);font-size:4.5rem; }
.hero-scroll { position:absolute;bottom:28px;left:24px;display:flex;align-items:center;gap:12px;font-size:.56rem;letter-spacing:.26em;text-transform:uppercase;color:var(--text-muted);opacity:0;animation:fadeIn 1s 1.5s forwards; }
.scroll-line { width:1px;height:40px;background:linear-gradient(to bottom,transparent,var(--gold));animation:scrollLine 2s infinite; }
@media(max-width:860px){ .hero-image-side{display:none;} }
@media(min-width:861px){ .hero-content{padding:0 60px;max-width:680px;} .hero-scroll{left:60px;} }

/* ===== ABOUT ===== */
#sobre { padding:clamp(60px,10vw,110px) clamp(20px,5vw,60px);background:var(--charcoal); }
.about-grid { max-width:1200px;margin:0 auto;display:grid;grid-template-columns:1fr;gap:44px;align-items:center; }
@media(min-width:860px){ .about-grid{grid-template-columns:1fr 1fr;gap:68px;} }
.about-image-wrap { position:relative; }
.about-img-frame { width:100%;aspect-ratio:3/4;background:linear-gradient(135deg,#2a1f15,#1a1208);display:flex;align-items:center;justify-content:center;font-size:6rem;position:relative;overflow:hidden; }
.about-img-frame::before { content:'';position:absolute;inset:0;background:linear-gradient(135deg,rgba(201,169,110,.1),transparent); }
.about-frame-deco { position:absolute;top:-16px;right:-16px;width:52%;height:52%;border:1px solid rgba(201,169,110,.3);pointer-events:none; }
.about-stats { display:grid;grid-template-columns:1fr 1fr;gap:14px;margin-top:28px; }
.stat-item { border:1px solid rgba(201,169,110,.2);padding:18px 14px;transition:all .3s; }
.stat-item:hover { border-color:var(--gold);background:rgba(201,169,110,.05); }
.stat-num { font-family:'Cormorant Garamond',serif;font-size:2rem;font-weight:300;color:var(--gold);line-height:1; }
.stat-label { font-size:.58rem;letter-spacing:.16em;text-transform:uppercase;color:var(--text-muted);margin-top:5px; }
.about-text { color:rgba(245,239,230,.72);line-height:1.9;font-size:.91rem;font-weight:300; }
.signature { font-family:'Cormorant Garamond',serif;font-size:1.8rem;font-style:italic;color:var(--gold);margin-top:24px; }

/* ===== SERVICES ===== */
#servicos { padding:clamp(60px,10vw,110px) clamp(20px,5vw,60px);background:var(--black); }
.services-header { max-width:1200px;margin:0 auto 44px; }
.services-grid { max-width:1200px;margin:0 auto;display:grid;grid-template-columns:1fr;gap:2px; }
@media(min-width:580px){ .services-grid{grid-template-columns:repeat(2,1fr);} }
@media(min-width:1000px){ .services-grid{grid-template-columns:repeat(3,1fr);} }
.service-card { background:var(--charcoal);padding:36px 28px;position:relative;overflow:hidden;transition:all .5s; }
.service-card::before { content:'';position:absolute;bottom:0;left:0;right:0;height:2px;background:linear-gradient(to right,transparent,var(--gold),transparent);transform:scaleX(0);transition:transform .5s; }
.service-card:hover::before { transform:scaleX(1); }
.service-card:hover { background:#1e1e1e;transform:translateY(-3px); }
.service-icon { font-size:2.2rem;margin-bottom:18px;display:block; }
.service-name { font-family:'Cormorant Garamond',serif;font-size:1.35rem;font-weight:400;margin-bottom:9px;color:var(--cream); }
.service-desc { font-size:.82rem;color:var(--text-muted);line-height:1.8;font-weight:300;margin-bottom:18px; }
.service-price { font-family:'Cormorant Garamond',serif;font-size:1.65rem;color:var(--gold);font-weight:300; }
.service-price span { font-size:.73rem;color:var(--text-muted);font-family:'Raleway',sans-serif; }

/* ===== PORTFOLIO ===== */
#portfolio { padding:clamp(60px,10vw,110px) clamp(20px,5vw,60px);background:var(--charcoal); }
.portfolio-header { max-width:1200px;margin:0 auto 36px;display:flex;flex-direction:column;gap:20px; }
@media(min-width:680px){ .portfolio-header{flex-direction:row;justify-content:space-between;align-items:flex-end;} }
.portfolio-filter { display:flex;flex-wrap:wrap;gap:8px; }
.filter-btn { background:transparent;border:1px solid rgba(201,169,110,.3);color:var(--text-muted);padding:8px 16px;font-size:.61rem;letter-spacing:.17em;text-transform:uppercase;cursor:pointer;transition:all .3s; }
.filter-btn.active,.filter-btn:hover { border-color:var(--gold);color:var(--gold);background:rgba(201,169,110,.08); }
.portfolio-masonry { max-width:1200px;margin:0 auto;columns:2;column-gap:4px; }
@media(min-width:860px){ .portfolio-masonry{columns:3;} }
.portfolio-item { break-inside:avoid;margin-bottom:4px;position:relative;overflow:hidden; }
.portfolio-img { width:100%;display:block;transition:transform .6s cubic-bezier(.25,.46,.45,.94); }
.portfolio-item:hover .portfolio-img,.portfolio-item:active .portfolio-img { transform:scale(1.05); }
.portfolio-overlay { position:absolute;inset:0;background:linear-gradient(to top,rgba(0,0,0,.8) 0%,transparent 60%);opacity:0;transition:opacity .4s;display:flex;align-items:flex-end;padding:18px; }
.portfolio-item:hover .portfolio-overlay,.portfolio-item:active .portfolio-overlay { opacity:1; }
.portfolio-info h4 { font-family:'Cormorant Garamond',serif;font-size:1.05rem;color:var(--cream);font-weight:300; }
.portfolio-info p { font-size:.62rem;color:var(--gold);letter-spacing:.16em; }

/* ===== PROMOS ===== */
#promocoes { padding:clamp(60px,10vw,110px) clamp(20px,5vw,60px);background:linear-gradient(135deg,#0d0a06 0%,#1a1208 50%,#0d0a06 100%); }
.promo-header { max-width:1200px;margin:0 auto 44px; }
.promo-grid { max-width:1200px;margin:0 auto;display:grid;grid-template-columns:1fr;gap:18px; }
@media(min-width:768px){ .promo-grid{grid-template-columns:repeat(2,1fr);} }
.promo-card { position:relative;overflow:hidden;border:1px solid rgba(201,169,110,.2);padding:clamp(24px,5vw,44px);transition:all .4s; }
.promo-card::before { content:'';position:absolute;top:0;left:0;right:0;height:1px;background:linear-gradient(to right,transparent,var(--gold),transparent); }
.promo-card:hover { border-color:rgba(201,169,110,.5);background:rgba(201,169,110,.04); }
.promo-badge { display:inline-block;background:var(--gold);color:var(--black);padding:4px 13px;font-size:.57rem;font-weight:600;letter-spacing:.19em;text-transform:uppercase;margin-bottom:18px; }
.promo-title { font-family:'Cormorant Garamond',serif;font-size:1.65rem;font-weight:300;margin-bottom:12px; }
.promo-desc { font-size:.82rem;color:var(--text-muted);line-height:1.8;margin-bottom:18px; }
.promo-price-row { display:flex;align-items:center;gap:14px;margin-bottom:18px;flex-wrap:wrap; }
.promo-original { font-family:'Cormorant Garamond',serif;font-size:1.1rem;color:var(--text-muted);text-decoration:line-through; }
.promo-new { font-family:'Cormorant Garamond',serif;font-size:1.8rem;color:var(--gold); }
.promo-expiry { font-size:.61rem;color:var(--text-muted);letter-spacing:.09em; }

/* ===== AGENDAR ===== */
#agendar { padding:clamp(60px,10vw,110px) clamp(20px,5vw,60px);background:var(--charcoal); }
.booking-wrap { max-width:920px;margin:0 auto; }
.booking-header { margin-bottom:44px;text-align:center; }
.booking-form { display:grid;grid-template-columns:1fr;gap:18px; }
@media(min-width:600px){ .booking-form{grid-template-columns:1fr 1fr;} .form-full{grid-column:1/-1;} }
.form-group { display:flex;flex-direction:column;gap:7px; }
.form-group label { font-size:.61rem;letter-spacing:.22em;text-transform:uppercase;color:var(--gold); }
.form-group input,.form-group select,.form-group textarea {
  background:rgba(255,255,255,.03);border:1px solid rgba(201,169,110,.2);color:var(--cream);
  padding:13px 16px;font-family:'Raleway',sans-serif;font-size:.87rem;font-weight:300;
  outline:none;transition:all .3s;width:100%;
  appearance:none;-webkit-appearance:none;border-radius:0;
}
.form-group input:focus,.form-group select:focus,.form-group textarea:focus { border-color:var(--gold);background:rgba(201,169,110,.05); }
.form-group select option { background:var(--charcoal); }
.form-group textarea { resize:vertical;min-height:92px; }
.upload-zone { border:1px dashed rgba(201,169,110,.4);padding:clamp(24px,5vw,44px);text-align:center;transition:all .3s;cursor:pointer;background:rgba(201,169,110,.02); }
.upload-zone:hover,.upload-zone:focus { border-color:var(--gold);background:rgba(201,169,110,.05);outline:none; }
.upload-icon { font-size:2rem;margin-bottom:12px;display:block; }
.upload-text { font-size:.76rem;color:var(--text-muted);line-height:1.7; }
.upload-previews { display:flex;flex-wrap:wrap;gap:8px;margin-top:14px;justify-content:center; }
.preview-thumb { width:68px;height:68px;object-fit:cover;border:1px solid rgba(201,169,110,.3); }
.booking-submit { margin-top:6px;width:100%;padding:17px;font-size:.66rem;letter-spacing:.27em; }

/* ===== CONTACT ===== */
#contato { padding:clamp(60px,10vw,110px) clamp(20px,5vw,60px);background:var(--black); }
.contact-grid { max-width:1200px;margin:0 auto;display:grid;grid-template-columns:1fr;gap:44px;align-items:start; }
@media(min-width:860px){ .contact-grid{grid-template-columns:1fr 1fr;gap:68px;} }
.contact-items { display:flex;flex-direction:column;gap:18px; }
.contact-item { display:flex;align-items:flex-start;gap:16px;border-bottom:1px solid rgba(201,169,110,.1);padding-bottom:18px; }
.contact-icon { font-size:1.35rem;color:var(--gold);flex-shrink:0; }
.contact-detail h4 { font-size:.61rem;letter-spacing:.19em;text-transform:uppercase;color:var(--gold);margin-bottom:4px; }
.contact-detail p { font-size:.86rem;color:var(--text-muted);font-weight:300; }
.social-links { display:flex;gap:10px;margin-top:28px;flex-wrap:wrap; }
.social-btn { border:1px solid rgba(201,169,110,.3);padding:11px 18px;font-size:.61rem;letter-spacing:.17em;text-transform:uppercase;color:var(--cream);transition:all .3s; }
.social-btn:hover { border-color:var(--gold);color:var(--gold);background:rgba(201,169,110,.05); }
.contact-img-frame { width:100%;aspect-ratio:4/3;background:linear-gradient(135deg,#1a0f0a,#2a1a10);display:flex;align-items:center;justify-content:center;font-size:5.5rem; }

/* ===== ADMIN BTN ===== */
#admin-btn {
  position:fixed;bottom:16px;right:14px;
  background:var(--charcoal);border:1px solid rgba(201,169,110,.3);
  color:var(--gold);padding:11px 14px;font-size:.57rem;letter-spacing:.16em;text-transform:uppercase;
  cursor:pointer;z-index:500;transition:all .3s;display:flex;gap:5px;align-items:center;
}
#admin-btn:hover { background:var(--gold);color:var(--black); }

/* ===== ADMIN MODAL ===== */
.admin-modal { display:none;position:fixed;inset:0;background:rgba(0,0,0,.97);z-index:3000;overflow-y:auto; }
.admin-modal.open { display:block; }
.admin-inner { max-width:840px;margin:0 auto;background:var(--charcoal);border:1px solid rgba(201,169,110,.3);padding:clamp(18px,4vw,52px);min-height:100vh; }
@media(min-width:600px){ .admin-inner{margin:36px auto;min-height:auto;} }
.admin-header { display:flex;justify-content:space-between;align-items:center;margin-bottom:32px;border-bottom:1px solid rgba(201,169,110,.2);padding-bottom:18px;gap:10px;flex-wrap:wrap; }
.admin-title { font-family:'Cormorant Garamond',serif;font-size:1.6rem;font-weight:300;color:var(--gold); }
.admin-close { background:none;border:1px solid rgba(201,169,110,.3);color:var(--cream);padding:8px 16px;font-size:.6rem;letter-spacing:.16em;cursor:pointer;transition:all .3s; }
.admin-close:hover { border-color:var(--rose);color:var(--rose); }
.admin-tabs { display:flex;gap:2px;margin-bottom:28px;flex-wrap:wrap; }
.admin-tab { background:rgba(255,255,255,.03);border:none;border-bottom:2px solid transparent;color:var(--text-muted);padding:11px 16px;font-size:.6rem;letter-spacing:.16em;text-transform:uppercase;cursor:pointer;transition:all .3s; }
.admin-tab.active { border-bottom-color:var(--gold);color:var(--gold);background:rgba(201,169,110,.05); }
.admin-section { display:none; }
.admin-section.active { display:block; }
.admin-section-title { font-family:'Cormorant Garamond',serif;font-size:1.3rem;color:var(--gold);margin-bottom:22px;font-weight:300; }
.admin-form { display:flex;flex-direction:column;gap:16px; }
.admin-form-row { display:grid;grid-template-columns:1fr;gap:16px; }
@media(min-width:540px){ .admin-form-row{grid-template-columns:1fr 1fr;} }
.admin-form label { font-size:.57rem;letter-spacing:.17em;text-transform:uppercase;color:var(--gold);display:block;margin-bottom:6px; }
.admin-form input,.admin-form select,.admin-form textarea { background:rgba(255,255,255,.04);border:1px solid rgba(201,169,110,.2);color:var(--cream);padding:12px 14px;font-family:'Raleway',sans-serif;font-size:.84rem;outline:none;width:100%;transition:all .3s;appearance:none;-webkit-appearance:none;border-radius:0; }
.admin-form input:focus,.admin-form select:focus,.admin-form textarea:focus { border-color:var(--gold); }
.admin-form textarea { resize:vertical;min-height:74px; }
.admin-submit { background:var(--gold);border:none;color:var(--black);padding:13px 34px;font-size:.61rem;letter-spacing:.27em;text-transform:uppercase;cursor:pointer;transition:all .3s;font-weight:600;align-self:flex-start; }
.admin-submit:hover { background:var(--gold-dark); }
.admin-submit-full { align-self:stretch;padding:15px; }
.admin-list { display:flex;flex-direction:column;gap:9px;margin-top:22px; }
.admin-list-item { display:flex;justify-content:space-between;align-items:flex-start;padding:13px 14px;border:1px solid rgba(201,169,110,.15);transition:all .3s;gap:10px;flex-wrap:wrap; }
.admin-list-item:hover { border-color:rgba(201,169,110,.4); }
.admin-list-info { flex:1;min-width:0; }
.admin-list-info h4 { font-size:.82rem;color:var(--cream);margin-bottom:3px;word-break:break-word; }
.admin-list-info p { font-size:.71rem;color:var(--text-muted);word-break:break-word;margin-top:2px; }
.admin-list-actions { display:flex;gap:6px;flex-shrink:0; }
.admin-del { background:none;border:1px solid rgba(212,165,160,.3);color:var(--rose);padding:6px 13px;font-size:.57rem;letter-spacing:.1em;cursor:pointer;font-family:'Raleway',sans-serif;transition:all .3s;white-space:nowrap; }
.admin-del:hover { background:rgba(212,165,160,.1); }
.admin-login { max-width:360px;margin:0 auto;text-align:center;padding:28px 0; }
.admin-login h3 { font-family:'Cormorant Garamond',serif;font-size:1.45rem;color:var(--gold);margin-bottom:26px; }
.admin-msg { padding:11px 14px;margin-top:12px;font-size:.71rem;letter-spacing:.08em;display:none; }
.admin-msg.success { background:rgba(201,169,110,.1);color:var(--gold);border:1px solid rgba(201,169,110,.3);display:block; }
.admin-msg.error { background:rgba(212,165,160,.1);color:var(--rose);border:1px solid rgba(212,165,160,.3);display:block; }

/* ===== FOOTER ===== */
footer { padding:clamp(32px,5vw,52px) clamp(20px,5vw,60px);background:#050505;border-top:1px solid rgba(201,169,110,.1); }
.footer-inner { max-width:1200px;margin:0 auto;display:flex;flex-direction:column;gap:18px;align-items:center;text-align:center; }
@media(min-width:680px){ .footer-inner{flex-direction:row;justify-content:space-between;text-align:left;} }
.footer-logo { font-family:'Cormorant Garamond',serif;font-size:1.75rem;font-weight:300;color:var(--gold);letter-spacing:.15em; }
.footer-copy { font-size:.66rem;color:var(--text-muted);letter-spacing:.07em; }
.footer-links { display:flex;gap:18px;flex-wrap:wrap;justify-content:center; }
.footer-links a { font-size:.61rem;color:var(--text-muted);letter-spacing:.09em;transition:color .3s; }
.footer-links a:hover { color:var(--gold); }

/* ===== TOUCH POINTER — restore cursor ===== */
@media(pointer:coarse){
  .filter-btn,.btn-primary,.btn-ghost,.booking-submit,
  .admin-submit,.admin-del,.admin-close,.admin-tab,
  #admin-btn,.upload-zone,.menu-toggle { cursor:pointer; }
}
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>
<div class="notification" id="notification"></div>

<!-- NAV -->
<nav id="navbar">
  <a href="#home" class="nav-logo">C.<span>Helena</span></a>
  <button class="menu-toggle" id="menuToggle" aria-label="Abrir menu" aria-expanded="false">
    <span></span><span></span><span></span>
  </button>
  <ul class="nav-links" id="navLinks">
    <li><a href="#sobre"     onclick="closeMenu()">Sobre</a></li>
    <li><a href="#servicos"  onclick="closeMenu()">Serviços</a></li>
    <li><a href="#portfolio" onclick="closeMenu()">Portfólio</a></li>
    <li><a href="#promocoes" onclick="closeMenu()">Promoções</a></li>
    <li><a href="#agendar"  class="nav-cta" onclick="closeMenu()">Agendar</a></li>
  </ul>
</nav>

<!-- HERO -->
<section class="hero" id="home">
  <div class="hero-bg"></div>
  <div class="hero-lines"></div>
  <div class="hero-content">
    <div class="hero-tag">Nail Designer Especialista</div>
    <h1 class="hero-title">Arte em<br><em>cada detalhe</em></h1>
    <p class="hero-subtitle">Transformando unhas em obras de arte.<br>Sofisticação e exclusividade em cada atendimento.</p>
    <div class="hero-actions">
      <a href="#agendar"  class="btn-primary">Agendar Horário</a>
      <a href="#portfolio" class="btn-ghost">Ver Portfólio</a>
    </div>
  </div>
  <div class="hero-image-side" aria-hidden="true">
    <div class="nail-art-grid">
      <div class="nail-cell">💅</div><div class="nail-cell">✨</div>
      <div class="nail-cell">🌹</div><div class="nail-cell">💅</div>
    </div>
  </div>
  <div class="hero-scroll" aria-hidden="true">
    <div class="scroll-line"></div>Rolar para explorar
  </div>
</section>

<!-- SOBRE -->
<section id="sobre">
  <div class="about-grid">
    <div class="about-image-wrap reveal">
      <div class="about-img-frame">💅</div>
      <div class="about-frame-deco"></div>
      <div class="about-stats">
        <div class="stat-item"><div class="stat-num" id="c1">0</div><div class="stat-label">Clientes Atendidas</div></div>
        <div class="stat-item"><div class="stat-num" id="c2">0</div><div class="stat-label">Anos de Experiência</div></div>
        <div class="stat-item"><div class="stat-num" id="c3">0</div><div class="stat-label">Designs Criados</div></div>
        <div class="stat-item"><div class="stat-num" id="c4">0</div><div class="stat-label">Certificações</div></div>
      </div>
    </div>
    <div class="reveal" style="transition-delay:.2s">
      <div class="section-label">Sobre mim</div>
      <h2 class="section-title">Helena <em>Perdomo</em></h2>
      <div class="gold-divider"></div>
      <p class="about-text">Com mais de 8 anos dedicados à arte das unhas, Helena Perdomo transformou sua paixão em uma especialidade de alto padrão. Especialista em nail art sofisticada, gel, acrílico e técnicas contemporâneas.</p>
      <p class="about-text" style="margin-top:13px">Cada atendimento é único. Cada detalhe é pensado. O estúdio C.Helena é o espaço onde luxo, criatividade e cuidado se encontram.</p>
      <div class="signature">Helena Perdomo</div>
      <a href="#agendar" class="btn-primary" style="margin-top:26px;display:inline-block">Ver Serviços</a>
    </div>
  </div>
</section>

<!-- SERVIÇOS -->
<section id="servicos">
  <div class="services-header reveal">
    <div class="section-label">O que ofereço</div>
    <h2 class="section-title">Nossos <em>Serviços</em></h2>
  </div>
  <div class="services-grid" id="servicesGrid"></div>
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
  <div class="portfolio-masonry reveal" id="portfolioGrid"></div>
</section>

<!-- PROMOÇÕES -->
<section id="promocoes">
  <div class="promo-header reveal">
    <div class="section-label">Ofertas exclusivas</div>
    <h2 class="section-title">Pro<em>moções</em></h2>
  </div>
  <div class="promo-grid" id="promoGrid"></div>
</section>

<!-- AGENDAMENTO -->
<section id="agendar">
  <div class="booking-wrap">
    <div class="booking-header reveal">
      <div class="section-label" style="justify-content:center">Reserve seu horário</div>
      <h2 class="section-title">Faça seu <em>Agendamento</em></h2>
      <p style="color:var(--text-muted);font-size:.88rem;font-weight:300;margin-top:11px">Preencha o formulário e entraremos em contato para confirmar seu horário</p>
    </div>
    <div class="booking-form reveal">
      <div class="form-group">
        <label for="bName">Nome Completo</label>
        <input type="text" id="bName" placeholder="Seu nome" autocomplete="name">
      </div>
      <div class="form-group">
        <label for="bPhone">Telefone / WhatsApp</label>
        <input type="tel" id="bPhone" placeholder="(00) 00000-0000" autocomplete="tel">
      </div>
      <div class="form-group">
        <label for="bService">Serviço Desejado</label>
        <select id="bService"><option value="">Selecione o serviço</option></select>
      </div>
      <div class="form-group">
        <label for="bDate">Data Preferida</label>
        <input type="date" id="bDate">
      </div>
      <div class="form-group">
        <label for="bTime">Horário Preferido</label>
        <select id="bTime">
          <option value="">Selecione o horário</option>
          <option>09:00</option><option>10:00</option><option>11:00</option>
          <option>13:00</option><option>14:00</option><option>15:00</option>
          <option>16:00</option><option>17:00</option>
        </select>
      </div>
      <div class="form-group">
        <label for="bNotes">Observações</label>
        <textarea id="bNotes" placeholder="Conte-me sobre o que você deseja..."></textarea>
      </div>
      <div class="form-group form-full">
        <label>Referências de Unhas (opcional)</label>
        <div class="upload-zone" id="uploadZone" role="button" tabindex="0"
             onclick="document.getElementById('fileInput').click()"
             onkeydown="if(event.key==='Enter'||event.key===' ')this.click()">
          <span class="upload-icon">🖼️</span>
          <div class="upload-text">
            <strong style="color:var(--gold)">Toque aqui para enviar imagens</strong><br>
            Referências, inspirações e fotos que você deseja<br>
            <span style="font-size:.66rem">JPG, PNG, WEBP — Máx. 5 imagens</span>
          </div>
          <div class="upload-previews" id="uploadPreviews"></div>
        </div>
        <input type="file" id="fileInput" accept="image/*" multiple style="display:none">
      </div>
      <div class="form-full">
        <button class="btn-primary booking-submit" onclick="submitBooking()">Solicitar Agendamento</button>
      </div>
    </div>
  </div>
</section>

<!-- CONTATO -->
<section id="contato">
  <div class="contact-grid">
    <div class="reveal">
      <div class="section-label">Fale conosco</div>
      <h2 class="section-title">Entre em <em>Contato</em></h2>
      <div class="gold-divider"></div>
      <div class="contact-items">
        <div class="contact-item"><div class="contact-icon">📍</div><div class="contact-detail"><h4>Localização</h4><p>Rua das Flores, 123 — Belo Horizonte, MG</p></div></div>
        <div class="contact-item"><div class="contact-icon">📱</div><div class="contact-detail"><h4>WhatsApp</h4><p>(31) 99999-9999</p></div></div>
        <div class="contact-item"><div class="contact-icon">🕐</div><div class="contact-detail"><h4>Horário de Atendimento</h4><p>Terça a Sábado: 9h às 18h</p></div></div>
        <div class="contact-item"><div class="contact-icon">✉️</div><div class="contact-detail"><h4>E-mail</h4><p>contato@chelena.com.br</p></div></div>
      </div>
      <div class="social-links">
        <a href="#" class="social-btn">Instagram</a>
        <a href="#" class="social-btn">WhatsApp</a>
        <a href="#" class="social-btn">TikTok</a>
      </div>
    </div>
    <div class="reveal" style="transition-delay:.2s">
      <div class="contact-img-frame">🌹</div>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="footer-logo">C.Helena</div>
    <div class="footer-copy">© 2025 C.Helena Nail Designer — Helena Perdomo</div>
    <div class="footer-links">
      <a href="#sobre">Sobre</a><a href="#servicos">Serviços</a><a href="#portfolio">Portfólio</a>
    </div>
  </div>
</footer>

<!-- ADMIN BTN -->
<button id="admin-btn" onclick="openAdmin()">⚙ Admin</button>

<!-- ADMIN MODAL -->
<div class="admin-modal" id="adminModal" role="dialog" aria-modal="true" aria-label="Painel Administrativo">
  <div class="admin-inner">

    <!-- LOGIN -->
    <div id="adminLoginSection" class="admin-login">
      <h3>Acesso Restrito</h3>
      <div class="admin-form" style="text-align:left">
        <div>
          <label for="adminPass">Senha de acesso</label>
          <input type="password" id="adminPass" placeholder="Digite a senha" onkeydown="if(event.key==='Enter')loginAdmin()">
        </div>
        <button class="admin-submit admin-submit-full" onclick="loginAdmin()">Entrar</button>
        <div class="admin-msg" id="adminMsg"></div>
      </div>
      <button onclick="closeAdmin()" style="background:none;border:none;color:var(--text-muted);margin-top:18px;font-size:.73rem;cursor:pointer;text-decoration:underline;font-family:'Raleway',sans-serif">Cancelar</button>
    </div>

    <!-- PANEL -->
    <div id="adminPanel" style="display:none">
      <div class="admin-header">
        <div class="admin-title">Painel C.Helena</div>
        <button class="admin-close" onclick="closeAdmin()">✕ Fechar</button>
      </div>
      <div class="admin-tabs">
        <button class="admin-tab active" onclick="switchTab('agendamentos',this)">Agendamentos</button>
        <button class="admin-tab" onclick="switchTab('portfolio',this)">Portfólio</button>
        <button class="admin-tab" onclick="switchTab('promocoes',this)">Promoções</button>
        <button class="admin-tab" onclick="switchTab('servicos',this)">Serviços</button>
      </div>

      <!-- AGENDAMENTOS TAB -->
      <div class="admin-section active" id="tab-agendamentos">
        <p class="admin-section-title">Solicitações de Agendamento</p>
        <div class="admin-list" id="adminBookings"></div>
      </div>

      <!-- PORTFOLIO TAB -->
      <div class="admin-section" id="tab-portfolio">
        <p class="admin-section-title">Adicionar ao Portfólio</p>
        <div class="admin-form">
          <div class="admin-form-row">
            <div><label>Título</label><input type="text" id="pTitle" placeholder="Ex: Gel Rosa Nude"></div>
            <div><label>Categoria</label><select id="pCategory"><option value="gel">Gel</option><option value="acrilico">Acrílico</option><option value="arte">Nail Art</option></select></div>
          </div>
          <div><label>Emoji / Ícone</label><input type="text" id="pEmoji" placeholder="💅 ou 🌹 ou ✨"></div>
          <div><label>Cor de fundo</label>
            <select id="pColor">
              <option value="linear-gradient(135deg,#2a1f15,#4a3020)">Tom dourado</option>
              <option value="linear-gradient(135deg,#1E0E12,#3E2020)">Tom rosé</option>
              <option value="linear-gradient(135deg,#0A0818,#1A1030)">Tom vinho</option>
              <option value="linear-gradient(135deg,#0A1020,#101830)">Tom azul</option>
              <option value="linear-gradient(135deg,#101810,#202820)">Tom esmeralda</option>
            </select>
          </div>
          <div><label>Tamanho do card</label><select id="pHeight"><option value="130px">Pequeno</option><option value="190px" selected>Médio</option><option value="270px">Grande</option></select></div>
          <button class="admin-submit" onclick="addPortfolioItem()">+ Adicionar ao Portfólio</button>
        </div>
        <div class="admin-list" id="adminPortfolioList" style="margin-top:22px"></div>
      </div>

      <!-- PROMOS TAB -->
      <div class="admin-section" id="tab-promocoes">
        <p class="admin-section-title">Gerenciar Promoções</p>
        <div class="admin-form">
          <div class="admin-form-row">
            <div><label>Nome da Promoção</label><input type="text" id="promoName" placeholder="Ex: Combo Inverno"></div>
            <div><label>Badge</label><input type="text" id="promoBadge" placeholder="Ex: OFERTA ESPECIAL"></div>
          </div>
          <div><label>Descrição</label><textarea id="promoDesc" placeholder="Descreva a promoção..."></textarea></div>
          <div class="admin-form-row">
            <div><label>Preço Original (R$)</label><input type="number" id="promoOriginal" placeholder="150"></div>
            <div><label>Preço Promocional (R$)</label><input type="number" id="promoNew" placeholder="120"></div>
          </div>
          <div><label>Válido até</label><input type="date" id="promoDate"></div>
          <button class="admin-submit" onclick="addPromo()">+ Publicar Promoção</button>
        </div>
        <div class="admin-list" id="adminPromoList" style="margin-top:22px"></div>
      </div>

      <!-- SERVIÇOS TAB -->
      <div class="admin-section" id="tab-servicos">
        <p class="admin-section-title">Gerenciar Serviços</p>
        <div class="admin-form">
          <div class="admin-form-row">
            <div><label>Nome do Serviço</label><input type="text" id="svcName" placeholder="Ex: Gel Claro"></div>
            <div><label>Ícone (emoji)</label><input type="text" id="svcIcon" placeholder="💅"></div>
          </div>
          <div><label>Descrição</label><textarea id="svcDesc" placeholder="Descrição do serviço..."></textarea></div>
          <div><label>Preço (R$)</label><input type="number" id="svcPrice" placeholder="0"></div>
          <button class="admin-submit" onclick="addService()">+ Adicionar Serviço</button>
        </div>
        <div class="admin-list" id="adminServiceList" style="margin-top:22px"></div>
      </div>
    </div><!-- /adminPanel -->
  </div>
</div>

<script>
/* == DATA == */
const state = {
  bookings: JSON.parse(localStorage.getItem('ch_bookings')||'[]'),
  portfolio: JSON.parse(localStorage.getItem('ch_portfolio')||JSON.stringify([
    {id:1,title:'Gel Rosé Nude',category:'gel',emoji:'💅',color:'linear-gradient(135deg,#2a1018,#4a2030)',height:'190px'},
    {id:2,title:'Nail Art Floral',category:'arte',emoji:'🌸',color:'linear-gradient(135deg,#1a0818,#3a1028)',height:'270px'},
    {id:3,title:'Acrílico Natural',category:'acrilico',emoji:'✨',color:'linear-gradient(135deg,#1a1510,#2a2010)',height:'130px'},
    {id:4,title:'Gel Bordô',category:'gel',emoji:'🍷',color:'linear-gradient(135deg,#200808,#401010)',height:'190px'},
    {id:5,title:'Nail Art Geométrica',category:'arte',emoji:'◇',color:'linear-gradient(135deg,#080820,#181838)',height:'270px'},
    {id:6,title:'Francesinha Dourada',category:'gel',emoji:'✨',color:'linear-gradient(135deg,#1a1208,#2a2010)',height:'130px'},
    {id:7,title:'Acrílico Almendrado',category:'acrilico',emoji:'💎',color:'linear-gradient(135deg,#0a1220,#141c30)',height:'190px'},
    {id:8,title:'Nail Art Marmorizada',category:'arte',emoji:'🤍',color:'linear-gradient(135deg,#1a1a1a,#2a2a2a)',height:'250px'},
  ])),
  promos: JSON.parse(localStorage.getItem('ch_promos')||JSON.stringify([
    {id:1,name:'Combo Outono',badge:'OFERTA ESPECIAL',desc:'Gel completo com nail art personalizada e esmaltação das mãos.',original:180,novo:140,date:'2025-09-30'},
    {id:2,name:'Manutenção Express',badge:'PROMOÇÃO RELÂMPAGO',desc:'Manutenção completa do gel com refile e decoração surpresa inclusa.',original:120,novo:89,date:'2025-08-15'},
  ])),
  services: JSON.parse(localStorage.getItem('ch_services')||JSON.stringify([
    {id:1,name:'Gel Claro & Nude',icon:'💅',desc:'Extensão de gel nas tonalidades claro e nude. Alta durabilidade e acabamento impecável.',price:120},
    {id:2,name:'Nail Art Personalizada',icon:'🎨',desc:'Criações exclusivas com designs sob medida para o seu estilo.',price:160},
    {id:3,name:'Acrílico Premium',icon:'💎',desc:'Extensão acrílica com acabamento natural e longa duração.',price:140},
    {id:4,name:'Gel com Decoração',icon:'✨',desc:'Gel colorido com decorações artísticas, glitter e pedrarias.',price:150},
    {id:5,name:'Manutenção Gel',icon:'🔄',desc:'Refile e retoque do crescimento com pintura nova.',price:80},
    {id:6,name:'Remoção Segura',icon:'🌿',desc:'Remoção profissional sem danos à lâmina natural.',price:60},
  ])),
};
function save(){
  localStorage.setItem('ch_bookings',JSON.stringify(state.bookings));
  localStorage.setItem('ch_portfolio',JSON.stringify(state.portfolio));
  localStorage.setItem('ch_promos',JSON.stringify(state.promos));
  localStorage.setItem('ch_services',JSON.stringify(state.services));
}

/* == CURSOR == */
if(window.matchMedia('(pointer:fine)').matches){
  const cur=document.getElementById('cursor'),ring=document.getElementById('cursorRing');
  if(cur&&ring) document.addEventListener('mousemove',e=>{
    cur.style.cssText=`left:${e.clientX}px;top:${e.clientY}px`;
    ring.style.cssText=`left:${e.clientX}px;top:${e.clientY}px`;
  });
}

/* == NAV == */
window.addEventListener('scroll',()=>{ document.getElementById('navbar').classList.toggle('scrolled',scrollY>60); },{passive:true});
const menuToggle=document.getElementById('menuToggle'),navLinks=document.getElementById('navLinks');
menuToggle.addEventListener('click',()=>{
  const o=navLinks.classList.toggle('open');
  menuToggle.classList.toggle('open',o);
  menuToggle.setAttribute('aria-expanded',o);
  document.body.style.overflow=o?'hidden':'';
});
function closeMenu(){
  navLinks.classList.remove('open');menuToggle.classList.remove('open');
  menuToggle.setAttribute('aria-expanded','false');document.body.style.overflow='';
}

/* == REVEAL == */
const io=new IntersectionObserver(e=>e.forEach(x=>{if(x.isIntersecting)x.target.classList.add('visible');}),{threshold:.08});
document.querySelectorAll('.reveal').forEach(el=>io.observe(el));

/* == COUNTERS == */
function animCount(el,target,sfx=''){
  let n=0;const s=Math.ceil(target/55);
  const t=setInterval(()=>{n+=s;if(n>=target){n=target;clearInterval(t);}el.textContent=n+sfx;},28);
}
new IntersectionObserver((e,obs)=>{if(e[0].isIntersecting){
  animCount(document.getElementById('c1'),500,'+');animCount(document.getElementById('c2'),8);
  animCount(document.getElementById('c3'),1200,'+');animCount(document.getElementById('c4'),12);
  obs.disconnect();}},{threshold:.2}).observe(document.getElementById('sobre'));

/* == RENDER == */
function renderServices(){
  document.getElementById('servicesGrid').innerHTML=state.services.map(s=>`
    <div class="service-card reveal">
      <span class="service-icon">${s.icon}</span>
      <div class="service-name">${s.name}</div>
      <div class="service-desc">${s.desc}</div>
      <div class="service-price">R$ ${s.price}<span>,00</span></div>
    </div>`).join('');
  document.getElementById('servicesGrid').querySelectorAll('.reveal').forEach(el=>io.observe(el));
  syncServiceOptions();
}
function renderPortfolio(filter='all'){
  const items=filter==='all'?state.portfolio:state.portfolio.filter(p=>p.category===filter);
  document.getElementById('portfolioGrid').innerHTML=items.map(p=>`
    <div class="portfolio-item">
      <div class="portfolio-img" style="height:${p.height};background:${p.color};display:flex;align-items:center;justify-content:center;font-size:2.8rem">${p.emoji}</div>
      <div class="portfolio-overlay"><div class="portfolio-info"><h4>${p.title}</h4><p>${p.category.toUpperCase()}</p></div></div>
    </div>`).join('');
}
document.querySelectorAll('.filter-btn').forEach(btn=>{
  btn.addEventListener('click',function(){
    document.querySelectorAll('.filter-btn').forEach(b=>b.classList.remove('active'));
    this.classList.add('active');renderPortfolio(this.dataset.filter);
  });
});
function renderPromos(){
  const g=document.getElementById('promoGrid');
  if(!state.promos.length){g.innerHTML='<p style="color:var(--text-muted);font-size:.88rem;padding:28px 0">Nenhuma promoção ativa no momento.</p>';return;}
  g.innerHTML=state.promos.map(p=>`
    <div class="promo-card reveal">
      <span class="promo-badge">${p.badge}</span>
      <div class="promo-title">${p.name}</div>
      <div class="promo-desc">${p.desc}</div>
      <div class="promo-price-row"><div class="promo-original">R$ ${p.original},00</div><div class="promo-new">R$ ${p.novo},00</div></div>
      <div class="promo-expiry">Válido até ${p.date?new Date(p.date+'T12:00').toLocaleDateString('pt-BR'):'—'}</div>
      <a href="#agendar" class="btn-primary" style="margin-top:18px;display:inline-block;font-size:.6rem">Aproveitar</a>
    </div>`).join('');
  g.querySelectorAll('.reveal').forEach(el=>io.observe(el));
}

/* == UPLOAD == */
document.getElementById('fileInput').addEventListener('change',function(){
  const c=document.getElementById('uploadPreviews');c.innerHTML='';
  Array.from(this.files).slice(0,5).forEach(f=>{
    const r=new FileReader();
    r.onload=e=>{const img=document.createElement('img');img.src=e.target.result;img.className='preview-thumb';c.appendChild(img);};
    r.readAsDataURL(f);
  });
});

/* == BOOKING == */
function syncServiceOptions(){
  const sel=document.getElementById('bService'),val=sel.value;
  sel.innerHTML='<option value="">Selecione o serviço</option>'+state.services.map(s=>`<option>${s.name}</option>`).join('');
  sel.value=val;
}
function submitBooking(){
  const n=document.getElementById('bName').value.trim(),ph=document.getElementById('bPhone').value.trim(),
        sv=document.getElementById('bService').value,dt=document.getElementById('bDate').value,
        tm=document.getElementById('bTime').value;
  if(!n||!ph||!sv||!dt||!tm){showNotification('Por favor, preencha todos os campos obrigatórios.');return;}
  state.bookings.unshift({id:Date.now(),name:n,phone:ph,service:sv,date:dt,time:tm,
    notes:document.getElementById('bNotes').value,timestamp:new Date().toLocaleString('pt-BR'),status:'Aguardando'});
  save();showNotification('✨ Agendamento solicitado! Entraremos em contato em breve.');
  ['bName','bPhone','bNotes'].forEach(id=>document.getElementById(id).value='');
  ['bService','bDate','bTime'].forEach(id=>document.getElementById(id).value='');
  document.getElementById('uploadPreviews').innerHTML='';
}

/* == NOTIFICATION == */
function showNotification(msg){
  const el=document.getElementById('notification');
  el.textContent=msg;el.classList.add('show');
  setTimeout(()=>el.classList.remove('show'),4500);
}

/* == ADMIN == */
const PASS='chelena2025';
function openAdmin(){document.getElementById('adminModal').classList.add('open');document.body.style.overflow='hidden';}
function closeAdmin(){
  document.getElementById('adminModal').classList.remove('open');document.body.style.overflow='';
  document.getElementById('adminPanel').style.display='none';
  document.getElementById('adminLoginSection').style.display='block';
  document.getElementById('adminPass').value='';document.getElementById('adminMsg').className='admin-msg';
}
function loginAdmin(){
  if(document.getElementById('adminPass').value===PASS){
    document.getElementById('adminLoginSection').style.display='none';
    document.getElementById('adminPanel').style.display='block';
    renderAdminBookings();renderAdminPortfolio();renderAdminPromos();renderAdminServices();
  }else{const m=document.getElementById('adminMsg');m.textContent='Senha incorreta.';m.className='admin-msg error';}
}
function switchTab(tab,btn){
  document.querySelectorAll('.admin-tab').forEach(t=>t.classList.remove('active'));
  document.querySelectorAll('.admin-section').forEach(s=>s.classList.remove('active'));
  btn.classList.add('active');document.getElementById('tab-'+tab).classList.add('active');
}
function renderAdminBookings(){
  const el=document.getElementById('adminBookings');
  if(!state.bookings.length){el.innerHTML='<p style="color:var(--text-muted);font-size:.82rem">Nenhum agendamento ainda.</p>';return;}
  el.innerHTML=state.bookings.map(b=>`
    <div class="admin-list-item">
      <div class="admin-list-info">
        <h4>${b.name} — ${b.service}</h4>
        <p>${b.date} às ${b.time} · ${b.phone}</p>
        <p>${b.timestamp}</p>
        ${b.notes?`<p style="font-style:italic;opacity:.8">Obs: ${b.notes}</p>`:''}
      </div>
      <div class="admin-list-actions"><button class="admin-del" onclick="deleteBooking(${b.id})">Remover</button></div>
    </div>`).join('');
}
function deleteBooking(id){state.bookings=state.bookings.filter(b=>b.id!==id);save();renderAdminBookings();}
function renderAdminPortfolio(){
  const el=document.getElementById('adminPortfolioList');
  if(!state.portfolio.length){el.innerHTML='<p style="color:var(--text-muted);font-size:.82rem">Portfólio vazio.</p>';return;}
  el.innerHTML=state.portfolio.map(p=>`
    <div class="admin-list-item">
      <div class="admin-list-info"><h4>${p.emoji} ${p.title}</h4><p>${p.category}</p></div>
      <button class="admin-del" onclick="deletePortfolio(${p.id})">Remover</button>
    </div>`).join('');
}
function addPortfolioItem(){
  const t=document.getElementById('pTitle').value.trim();if(!t){alert('Informe o título');return;}
  state.portfolio.push({id:Date.now(),title:t,category:document.getElementById('pCategory').value,
    emoji:document.getElementById('pEmoji').value.trim()||'💅',
    color:document.getElementById('pColor').value,height:document.getElementById('pHeight').value});
  save();renderPortfolio();renderAdminPortfolio();
  document.getElementById('pTitle').value='';document.getElementById('pEmoji').value='';
  showNotification('✨ Item adicionado ao portfólio!');
}
function deletePortfolio(id){state.portfolio=state.portfolio.filter(p=>p.id!==id);save();renderPortfolio();renderAdminPortfolio();}
function renderAdminPromos(){
  const el=document.getElementById('adminPromoList');
  if(!state.promos.length){el.innerHTML='<p style="color:var(--text-muted);font-size:.82rem">Sem promoções.</p>';return;}
  el.innerHTML=state.promos.map(p=>`
    <div class="admin-list-item">
      <div class="admin-list-info"><h4>${p.name}</h4><p>De R$ ${p.original} por R$ ${p.novo} · Até ${p.date?new Date(p.date+'T12:00').toLocaleDateString('pt-BR'):'—'}</p></div>
      <button class="admin-del" onclick="deletePromo(${p.id})">Remover</button>
    </div>`).join('');
}
function addPromo(){
  const n=document.getElementById('promoName').value.trim();if(!n){alert('Informe o nome');return;}
  state.promos.unshift({id:Date.now(),name:n,badge:document.getElementById('promoBadge').value||'PROMOÇÃO',
    desc:document.getElementById('promoDesc').value,original:+document.getElementById('promoOriginal').value,
    novo:+document.getElementById('promoNew').value,date:document.getElementById('promoDate').value});
  save();renderPromos();renderAdminPromos();
  ['promoName','promoBadge','promoDesc','promoOriginal','promoNew','promoDate'].forEach(id=>document.getElementById(id).value='');
  showNotification('🎉 Promoção publicada!');
}
function deletePromo(id){state.promos=state.promos.filter(p=>p.id!==id);save();renderPromos();renderAdminPromos();}
function renderAdminServices(){
  document.getElementById('adminServiceList').innerHTML=state.services.map(s=>`
    <div class="admin-list-item">
      <div class="admin-list-info"><h4>${s.icon} ${s.name}</h4><p>R$ ${s.price},00</p></div>
      <button class="admin-del" onclick="deleteService(${s.id})">Remover</button>
    </div>`).join('');
}
function addService(){
  const n=document.getElementById('svcName').value.trim();if(!n){alert('Informe o nome');return;}
  state.services.push({id:Date.now(),name:n,icon:document.getElementById('svcIcon').value||'💅',
    desc:document.getElementById('svcDesc').value,price:+document.getElementById('svcPrice').value});
  save();renderServices();renderAdminServices();
  ['svcName','svcIcon','svcDesc','svcPrice'].forEach(id=>document.getElementById(id).value='');
  showNotification('✅ Serviço adicionado!');
}
function deleteService(id){state.services=state.services.filter(s=>s.id!==id);save();renderServices();renderAdminServices();}

/* == INIT == */
renderServices();renderPortfolio();renderPromos();
document.getElementById('bDate').setAttribute('min',new Date().toISOString().split('T')[0]);
</script>
</body>
</html>