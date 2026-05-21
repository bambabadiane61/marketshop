<!DOCTYPE html>
<html lang="fr">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=yes">
    <title>KBmarketplace - KhadimBadiane</title>

    <!-- ── PWA META ─────────────────────────── -->
    <meta name="application-name" content="KBmarketplace">
    <meta name="description" content="KBmarketplace — Your Favour Design by KhadimBadiane">
    <meta name="theme-color" content="#06080f">
    <meta name="background-color" content="#06080f">
    <meta name="mobile-web-app-capable" content="yes">

    <!-- iOS Safari PWA -->
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
    <meta name="apple-mobile-web-app-title" content="KBmarket">

    <!-- iOS icons (inline SVG data URIs — no external files needed) -->
    <link rel="apple-touch-icon" href="data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 180 180'%3E%3Crect width='180' height='180' rx='40' fill='%2306080f'/%3E%3Crect x='10' y='10' width='160' height='160' rx='32' fill='%230d1220'/%3E%3Crect x='24' y='24' width='132' height='132' rx='28' fill='%2322dd3b' opacity='.12'/%3E%3Ctext x='90' y='115' font-family='monospace' font-size='72' font-weight='700' fill='%2322dd3b' text-anchor='middle'%3EKB%3C/text%3E%3C/svg%3E">

    <!-- Manifest (inline via JS blob — no server needed) -->
    <link rel="manifest" id="pwa-manifest">

    <!-- Open Graph -->
    <meta property="og:title" content="KBmarketplace">
    <meta property="og:description" content="Your Favour Design — Mode, Style & Livraison Gambie">
    <meta property="og:type" content="website">

    <link href="https://fonts.googleapis.com/css2?family=Fraunces:ital,opsz,wght@0,9..144,300;0,9..144,700;0,9..144,900;1,9..144,400&family=Outfit:wght@300;400;500;600;700&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet">
    <style>
        *, *::before, *::after {
            margin: 0; padding: 0; box-sizing: border-box;
        }

        :root {
            --bg:        #06080f;
            --surface:   #0d1220;
            --surface2:  #111827;
            --glass:     rgba(255,255,255,0.04);
            --glass-b:   rgba(255,255,255,0.08);
            --accent:    #22dd3b;
            --accent-dim:#16a32a;
            --accent-glow: rgba(34,221,59,0.25);
            --gold:      #f5a623;
            --gold-dim:  #d4891a;
            --white:     #ffffff;
            --off-white: #e8eaf0;
            --muted:     #6b7a96;
            --border:    rgba(255,255,255,0.07);
            --border-hover: rgba(34,221,59,0.3);
            --danger:    #f43f5e;
            --radius-sm: 12px;
            --radius:    20px;
            --radius-lg: 32px;
            --radius-xl: 48px;
            --shadow:    0 8px 32px rgba(0,0,0,0.4);
            --shadow-lg: 0 24px 60px rgba(0,0,0,0.5);
            --glow:      0 0 40px rgba(34,221,59,0.15);
        }

        html { scroll-behavior: smooth; }

        body {
            font-family: 'Outfit', sans-serif;
            background: var(--bg);
            color: var(--off-white);
            min-height: 100vh;
            overflow-x: hidden;
        }

        /* ── ANIMATED BACKGROUND ─────────────── */
        .animated-bg {
            position: fixed; inset: 0; z-index: 0; overflow: hidden;
            background: radial-gradient(ellipse 120% 80% at 10% 0%, #0a2416 0%, transparent 60%),
                        radial-gradient(ellipse 80% 80% at 90% 100%, #1a1230 0%, transparent 60%),
                        linear-gradient(160deg, #06080f 0%, #0a0e1a 100%);
        }

        .orb {
            position: absolute; border-radius: 50%; filter: blur(80px);
            animation: driftOrb 25s ease-in-out infinite alternate;
        }
        .orb-1 { width: 600px; height: 600px; top: -200px; left: -150px; background: radial-gradient(circle, rgba(34,221,59,0.08), transparent 70%); animation-duration: 28s; }
        .orb-2 { width: 500px; height: 500px; bottom: -100px; right: -100px; background: radial-gradient(circle, rgba(245,166,35,0.07), transparent 70%); animation-duration: 22s; animation-delay: -8s; }
        .orb-3 { width: 300px; height: 300px; top: 40%; left: 50%; background: radial-gradient(circle, rgba(120,80,220,0.05), transparent 70%); animation-duration: 35s; animation-delay: -12s; }

        @keyframes driftOrb {
            0%   { transform: translate(0,0) scale(1); }
            100% { transform: translate(60px, 40px) scale(1.15); }
        }

        /* Noise grain overlay */
        .animated-bg::after {
            content: ''; position: absolute; inset: 0;
            background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
            opacity: 0.4; pointer-events: none;
        }

        .content-overlay {
            position: relative; z-index: 1; min-height: 100vh;
        }

        /* ── NAVBAR ──────────────────────────── */
        #nav-bar {
            position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
            height: 72px;
            background: rgba(6,8,15,0.75);
            backdrop-filter: blur(20px) saturate(180%);
            -webkit-backdrop-filter: blur(20px) saturate(180%);
            border-bottom: 1px solid var(--border);
            display: flex; align-items: center; justify-content: space-between;
            padding: 0 2rem;
            transition: background 0.3s;
        }

        #nav-bar::after {
            content: ''; position: absolute; bottom: 0; left: 10%; right: 10%; height: 1px;
            background: linear-gradient(90deg, transparent, rgba(34,221,59,0.2), transparent);
        }

        .custom-logo {
            display: flex; align-items: center; gap: 14px; cursor: pointer;
            text-decoration: none;
        }

        .logo-image {
            width: 44px; height: 44px;
            background: linear-gradient(135deg, var(--accent), var(--accent-dim));
            border-radius: 14px;
            display: flex; align-items: center; justify-content: center;
            font-family: 'Space Mono', monospace;
            font-weight: 700; font-size: 1rem;
            color: var(--bg);
            box-shadow: 0 4px 20px var(--accent-glow), inset 0 1px 0 rgba(255,255,255,0.2);
            letter-spacing: -1px;
        }

        .logo-text-wrap { display: flex; flex-direction: column; }

        .logo-kb {
            font-family: 'Fraunces', serif;
            font-size: 1.35rem; font-weight: 900;
            color: var(--white); line-height: 1;
        }
        .logo-kb span { color: var(--accent); }

        .logo-tagline {
            font-size: 0.5rem; letter-spacing: 2.5px; text-transform: uppercase;
            color: var(--muted); margin-top: 2px;
        }

        .nav-tabs {
            display: flex; gap: 6px;
            background: rgba(255,255,255,0.04);
            padding: 4px; border-radius: 50px;
            border: 1px solid var(--border);
        }

        .nav-tab {
            padding: 7px 20px; border-radius: 40px; cursor: pointer;
            color: var(--muted); font-weight: 500; font-size: 0.88rem;
            background: transparent; transition: all 0.2s; border: none;
            font-family: 'Outfit', sans-serif;
        }

        .nav-tab:hover { color: var(--white); }

        .nav-tab.active {
            background: var(--accent);
            color: var(--bg);
            box-shadow: 0 2px 12px var(--accent-glow);
            font-weight: 600;
        }

        .cart-btn {
            background: rgba(255,255,255,0.06);
            border: 1px solid var(--border);
            color: var(--off-white);
            width: 44px; height: 44px;
            border-radius: 50%; cursor: pointer; font-size: 1.1rem;
            position: relative; transition: all 0.2s;
            display: flex; align-items: center; justify-content: center;
        }

        .cart-btn:hover {
            background: var(--accent); color: var(--bg);
            border-color: var(--accent);
            box-shadow: 0 0 20px var(--accent-glow);
        }

        .cart-badge {
            position: absolute; top: -5px; right: -5px;
            background: var(--gold); border-radius: 50%;
            width: 20px; height: 20px; font-size: 10px;
            display: flex; align-items: center; justify-content: center;
            border: 2px solid var(--bg); font-weight: 700;
            color: var(--bg); font-family: 'Space Mono', monospace;
        }

        /* ── MARQUEE BANNER ──────────────────── */
        .marquee-banner {
            margin: 88px 1.5rem 0;
            border-radius: var(--radius);
            overflow: hidden;
            background: linear-gradient(90deg, var(--accent-dim), #0f7a1c, var(--accent-dim));
            background-size: 200% auto;
            animation: shimmerBanner 4s linear infinite;
            padding: 11px 0;
            box-shadow: 0 4px 24px var(--accent-glow);
        }

        @keyframes shimmerBanner {
            0% { background-position: 0% center; }
            100% { background-position: 200% center; }
        }

        .marquee-content {
            display: inline-block;
            animation: scrollMarquee 30s linear infinite;
            white-space: nowrap; padding-left: 100%;
        }

        .marquee-content span {
            margin-right: 60px; display: inline-flex; align-items: center; gap: 14px;
            font-size: 0.88rem; font-weight: 600; letter-spacing: 0.3px;
            color: white;
        }

        .marquee-content img { height: 28px; border-radius: 6px; }

        @keyframes scrollMarquee {
            0%   { transform: translateX(0); }
            100% { transform: translateX(-50%); }
        }

        /* ── HERO ─────────────────────────────── */
        .hero {
            margin: 1.5rem 1.5rem 0;
            padding: 5rem 3rem 4rem;
            border-radius: var(--radius-lg);
            background: linear-gradient(135deg,
                rgba(13,18,32,0.95) 0%,
                rgba(10,36,22,0.9) 50%,
                rgba(13,18,32,0.95) 100%);
            border: 1px solid var(--border);
            position: relative; overflow: hidden; text-align: center;
            box-shadow: var(--shadow);
        }

        .hero::before {
            content: ''; position: absolute; inset: 0;
            background: radial-gradient(ellipse 80% 60% at 50% 0%, rgba(34,221,59,0.08), transparent 70%);
            pointer-events: none;
        }

        .hero-label {
            display: inline-flex; align-items: center; gap: 8px;
            background: rgba(34,221,59,0.1); border: 1px solid rgba(34,221,59,0.2);
            padding: 5px 16px; border-radius: 40px;
            font-size: 0.75rem; letter-spacing: 2px; text-transform: uppercase;
            color: var(--accent); margin-bottom: 1.5rem;
            font-weight: 600;
        }

        .hero h1 {
            font-family: 'Fraunces', serif;
            font-size: clamp(2.4rem, 6vw, 4.5rem);
            font-weight: 900; line-height: 1.05;
            color: var(--white); margin-bottom: 1rem;
        }

        .hero h1 em {
            font-style: italic; color: var(--accent);
        }

        .hero p {
            font-size: 1.05rem; color: var(--muted);
            max-width: 480px; margin: 0 auto 2.5rem;
            line-height: 1.6;
        }

        .hero-cta {
            display: inline-flex; align-items: center; gap: 10px;
            background: var(--accent); color: var(--bg);
            padding: 13px 32px; border-radius: 50px; border: none;
            font-weight: 700; font-size: 0.95rem; cursor: pointer;
            transition: all 0.25s; font-family: 'Outfit', sans-serif;
            box-shadow: 0 8px 32px var(--accent-glow);
        }

        .hero-cta:hover {
            background: #30f04a; transform: translateY(-2px);
            box-shadow: 0 12px 40px var(--accent-glow);
        }

        .hero-stats {
            display: flex; gap: 3rem; justify-content: center;
            margin-top: 3rem; padding-top: 2rem;
            border-top: 1px solid var(--border);
        }

        .stat { text-align: center; }

        .stat-num {
            font-family: 'Space Mono', monospace;
            font-size: 1.8rem; font-weight: 700; color: var(--accent);
            line-height: 1;
        }

        .stat-label {
            font-size: 0.75rem; letter-spacing: 1.5px; text-transform: uppercase;
            color: var(--muted); margin-top: 4px;
        }

        /* ── FILTER BAR ───────────────────────── */
        .filter-bar {
            margin: 1.5rem 1.5rem 0;
            padding: 10px 14px;
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius-xl);
            display: flex; flex-wrap: wrap; gap: 6px; align-items: center;
        }

        .filter-btn {
            padding: 8px 18px; border-radius: 40px; border: none;
            background: transparent; color: var(--muted);
            font-weight: 500; cursor: pointer; font-size: 0.85rem;
            transition: all 0.2s; font-family: 'Outfit', sans-serif;
        }

        .filter-btn:hover { color: var(--off-white); background: var(--glass-b); }

        .filter-btn.active {
            background: var(--accent); color: var(--bg);
            font-weight: 600;
            box-shadow: 0 2px 12px var(--accent-glow);
        }

        .search-wrap {
            margin-left: auto;
        }

        .search-wrap input {
            background: rgba(255,255,255,0.06);
            border: 1px solid var(--border);
            padding: 9px 20px;
            border-radius: 40px;
            width: 220px; color: var(--off-white);
            font-family: 'Outfit', sans-serif; font-size: 0.88rem;
            transition: 0.2s;
            outline: none;
        }

        .search-wrap input:focus {
            border-color: var(--accent);
            background: rgba(34,221,59,0.05);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }

        .search-wrap input::placeholder { color: var(--muted); }

        /* ── PRODUCTS GRID ────────────────────── */
        .products-grid {
            display: grid;
            grid-template-columns: repeat(auto-fill, minmax(270px, 1fr));
            gap: 1.4rem;
            padding: 1.5rem 1.5rem 2rem;
        }

        .product-card {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            overflow: hidden;
            transition: all 0.3s cubic-bezier(0.34,1.56,0.64,1);
            cursor: pointer; position: relative;
        }

        .product-card:hover {
            transform: translateY(-8px) scale(1.01);
            border-color: var(--border-hover);
            box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 0 1px rgba(34,221,59,0.1);
        }

        .product-card:hover .product-img-wrap::after {
            opacity: 1;
        }

        .product-img-wrap {
            position: relative; overflow: hidden;
        }

        .product-img-wrap::after {
            content: ''; position: absolute; inset: 0;
            background: linear-gradient(to top, rgba(6,8,15,0.6) 0%, transparent 50%);
            opacity: 0; transition: 0.3s;
        }

        .product-img {
            height: 220px;
            background: linear-gradient(135deg, #111827, #1a2235);
            display: flex; align-items: center; justify-content: center;
            font-size: 4.5rem; transition: transform 0.4s ease;
        }

        .product-card:hover .product-img { transform: scale(1.05); }

        .product-img img {
            width: 100%; height: 100%; object-fit: cover;
        }

        .product-badge {
            position: absolute; top: 14px; left: 14px; z-index: 2;
            padding: 4px 12px; border-radius: 30px;
            font-size: 0.65rem; font-weight: 700; letter-spacing: 1.5px;
            text-transform: uppercase;
        }

        .badge-new  { background: rgba(34,221,59,0.15); color: var(--accent); border: 1px solid rgba(34,221,59,0.25); }
        .badge-sale { background: rgba(245,166,35,0.15); color: var(--gold); border: 1px solid rgba(245,166,35,0.25); }
        .badge-hot  { background: rgba(244,63,94,0.15); color: #fb7185; border: 1px solid rgba(244,63,94,0.25); }

        .product-info { padding: 1.2rem 1.3rem 1.3rem; }

        .product-cat {
            font-size: 0.72rem; letter-spacing: 1.5px; text-transform: uppercase;
            color: var(--accent); font-weight: 600; margin-bottom: 4px;
        }

        .product-name {
            font-weight: 600; font-size: 0.97rem; color: var(--white);
            line-height: 1.3; margin-bottom: 4px;
        }

        .product-desc {
            font-size: 0.8rem; color: var(--muted); margin-bottom: 14px;
        }

        .product-footer {
            display: flex; justify-content: space-between; align-items: center;
        }

        .product-price {
            font-family: 'Space Mono', monospace;
            font-weight: 700; font-size: 1.1rem; color: var(--accent);
        }

        .add-cart-btn {
            width: 38px; height: 38px; border-radius: 50%;
            background: rgba(34,221,59,0.12); color: var(--accent);
            border: 1px solid rgba(34,221,59,0.25);
            cursor: pointer; font-size: 1.3rem; font-weight: 300;
            transition: all 0.25s;
            display: flex; align-items: center; justify-content: center;
        }

        .add-cart-btn:hover {
            background: var(--accent); color: var(--bg);
            box-shadow: 0 4px 20px var(--accent-glow);
            transform: scale(1.1);
        }

        /* ── FOOTER ──────────────────────────── */
        .footer-social {
            margin: 0 1.5rem 1.5rem;
            padding: 2.5rem;
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            text-align: center;
        }

        .footer-logo {
            font-family: 'Fraunces', serif;
            font-size: 1.8rem; font-weight: 900;
            color: var(--white); margin-bottom: 0.5rem;
        }

        .footer-logo span { color: var(--accent); }

        .footer-divider {
            width: 60px; height: 2px;
            background: linear-gradient(90deg, var(--accent), var(--gold));
            margin: 1rem auto;
            border-radius: 2px;
        }

        .social-links { margin: 1rem 0; }

        .social-links a {
            display: inline-flex; align-items: center; gap: 6px;
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--border);
            padding: 8px 20px; border-radius: 40px;
            margin: 4px; text-decoration: none; color: var(--off-white);
            font-size: 0.85rem; transition: all 0.2s;
        }

        .social-links a:hover {
            background: var(--accent); color: var(--bg);
            border-color: var(--accent);
        }

        .shop-info {
            font-size: 0.8rem; color: var(--muted); margin-top: 0.8rem;
            line-height: 1.8;
        }

        /* ── CART PANEL ──────────────────────── */
        #cart-panel {
            position: fixed; right: 0; top: 0; bottom: 0; width: 400px;
            background: var(--surface2);
            border-left: 1px solid var(--border);
            z-index: 2001;
            transform: translateX(100%); transition: transform 0.35s cubic-bezier(0.4,0,0.2,1);
            display: flex; flex-direction: column;
            border-radius: 0;
        }

        #cart-panel.open { transform: translateX(0); }

        .cart-header {
            padding: 1.4rem 1.5rem;
            border-bottom: 1px solid var(--border);
            display: flex; justify-content: space-between; align-items: center;
        }

        .cart-header h3 {
            font-family: 'Fraunces', serif;
            font-size: 1.3rem; font-weight: 700; color: var(--white);
        }

        .close-cart-btn {
            background: rgba(255,255,255,0.06); border: 1px solid var(--border);
            color: var(--muted); width: 36px; height: 36px;
            border-radius: 50%; font-size: 1rem; cursor: pointer;
            display: flex; align-items: center; justify-content: center;
            transition: 0.2s;
        }

        .close-cart-btn:hover { background: var(--danger); color: white; border-color: var(--danger); }

        #cart-items-list { flex: 1; overflow-y: auto; padding: 1.2rem; }

        #cart-items-list::-webkit-scrollbar { width: 4px; }
        #cart-items-list::-webkit-scrollbar-track { background: transparent; }
        #cart-items-list::-webkit-scrollbar-thumb { background: var(--border); border-radius: 4px; }

        .cart-footer {
            padding: 1.4rem 1.5rem;
            border-top: 1px solid var(--border);
            background: rgba(0,0,0,0.2);
        }

        .cart-totals { margin-bottom: 1rem; }

        .cart-row {
            display: flex; justify-content: space-between; align-items: center;
            padding: 4px 0; font-size: 0.9rem; color: var(--muted);
        }

        .cart-row.total {
            font-weight: 700; font-size: 1.05rem; color: var(--white);
            border-top: 1px solid var(--border); padding-top: 10px; margin-top: 6px;
        }

        .cart-row.total span:last-child {
            font-family: 'Space Mono', monospace; color: var(--accent);
        }

        .checkout-btn {
            width: 100%; background: var(--accent); color: var(--bg);
            border: none; padding: 14px; border-radius: 50px;
            font-weight: 700; font-size: 0.95rem; cursor: pointer;
            transition: all 0.25s; font-family: 'Outfit', sans-serif;
            box-shadow: 0 6px 24px var(--accent-glow);
        }

        .checkout-btn:hover {
            background: #30f04a; transform: translateY(-1px);
            box-shadow: 0 10px 32px var(--accent-glow);
        }

        /* ── MODALS ──────────────────────────── */
        .modal-backdrop {
            display: none; position: fixed; inset: 0;
            background: rgba(0,0,0,0.75);
            backdrop-filter: blur(8px);
            z-index: 5000; align-items: center; justify-content: center;
        }

        .login-card {
            background: var(--surface2);
            border: 1px solid var(--border);
            width: 420px; max-width: 92%;
            border-radius: var(--radius-lg);
            padding: 2.5rem 2rem;
            box-shadow: var(--shadow-lg);
        }

        .login-card h2 {
            font-family: 'Fraunces', serif;
            font-size: 1.8rem; font-weight: 700;
            color: var(--white); margin-bottom: 1.8rem;
            text-align: center;
        }

        .login-input {
            width: 100%; padding: 13px 18px;
            margin: 8px 0;
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--border);
            border-radius: 50px; font-size: 0.93rem;
            color: var(--off-white); font-family: 'Outfit', sans-serif;
            transition: 0.2s; outline: none;
        }

        .login-input:focus {
            border-color: var(--accent);
            background: rgba(34,221,59,0.05);
            box-shadow: 0 0 0 3px var(--accent-glow);
        }

        .login-input::placeholder { color: var(--muted); }

        .remember-row {
            display: flex; align-items: center; justify-content: space-between;
            margin: 14px 0 20px; font-size: 0.83rem; color: var(--muted);
        }

        .login-btn {
            width: 100%; padding: 14px;
            background: var(--accent); color: var(--bg);
            font-weight: 700; border: none; border-radius: 50px;
            cursor: pointer; font-family: 'Outfit', sans-serif; font-size: 0.95rem;
            transition: all 0.2s;
            box-shadow: 0 6px 24px var(--accent-glow);
        }

        .login-btn:hover { background: #30f04a; transform: translateY(-1px); }

        .forgot-link, .create-link {
            color: var(--accent); text-decoration: none; font-size: 0.83rem;
            cursor: pointer; transition: color 0.2s;
        }

        .forgot-link:hover, .create-link:hover { color: var(--white); }

        .separator { color: var(--muted); margin: 0 6px; }

        .back-link {
            margin-top: 1rem; display: inline-block;
            color: var(--muted); font-size: 0.8rem; cursor: pointer;
            transition: color 0.2s;
        }

        .back-link:hover { color: var(--off-white); }

        /* Checkout modal */
        #checkout-modal {
            display: none; position: fixed; inset: 0;
            background: rgba(0,0,0,0.75); backdrop-filter: blur(8px);
            z-index: 3000; align-items: center; justify-content: center;
        }

        .checkout-box {
            background: var(--surface2);
            border: 1px solid var(--border);
            border-radius: var(--radius-lg);
            padding: 2.5rem 2rem;
            max-width: 520px; width: 92%;
            box-shadow: var(--shadow-lg);
        }

        .checkout-box h3 {
            font-family: 'Fraunces', serif;
            font-size: 1.5rem; font-weight: 700; color: var(--white);
            margin-bottom: 1.5rem;
        }

        .checkout-grid {
            display: grid; grid-template-columns: 1fr 1fr; gap: 10px;
        }

        .checkout-input {
            width: 100%; padding: 12px 16px;
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm); font-size: 0.88rem;
            color: var(--off-white); font-family: 'Outfit', sans-serif;
            outline: none; transition: 0.2s;
        }

        .checkout-input:focus {
            border-color: var(--accent);
            background: rgba(34,221,59,0.05);
        }

        .checkout-input::placeholder { color: var(--muted); }

        .checkout-input.full { grid-column: 1/-1; }

        #payment-methods-list {
            grid-column: 1/-1; margin: 4px 0;
            padding: 12px 16px; background: rgba(34,221,59,0.05);
            border: 1px solid rgba(34,221,59,0.15);
            border-radius: var(--radius-sm); font-size: 0.85rem;
            color: var(--off-white); line-height: 1.8;
        }

        #checkout-summary {
            grid-column: 1/-1; font-size: 0.85rem; color: var(--muted);
        }

        .checkout-actions {
            grid-column: 1/-1; display: flex; gap: 10px; margin-top: 8px;
        }

        .btn-cancel {
            flex: 1; padding: 12px; background: rgba(255,255,255,0.06);
            border: 1px solid var(--border); border-radius: 50px; color: var(--muted);
            cursor: pointer; font-family: 'Outfit', sans-serif; font-weight: 500;
            transition: 0.2s;
        }

        .btn-cancel:hover { color: var(--white); background: rgba(255,255,255,0.1); }

        .btn-confirm {
            flex: 2; padding: 12px; background: var(--accent); color: var(--bg);
            border: none; border-radius: 50px; font-weight: 700; cursor: pointer;
            font-family: 'Outfit', sans-serif; transition: 0.2s;
            box-shadow: 0 4px 20px var(--accent-glow);
        }

        .btn-confirm:hover { background: #30f04a; }

        /* ── ADMIN ────────────────────────────── */
        #page-admin { display: none; }

        .admin-layout { display: flex; flex-wrap: wrap; min-height: calc(100vh - 72px); padding-top: 72px; }

        .admin-sidebar {
            width: 240px; background: var(--surface);
            border-right: 1px solid var(--border);
            padding: 1.5rem 1rem; position: sticky; top: 72px;
            height: calc(100vh - 72px); overflow-y: auto;
        }

        .admin-sidebar-title {
            font-size: 0.65rem; letter-spacing: 2px; text-transform: uppercase;
            color: var(--muted); padding: 0 14px; margin-bottom: 12px;
        }

        .admin-menu-item {
            padding: 11px 16px; border-radius: var(--radius-sm);
            color: var(--muted); cursor: pointer; margin-bottom: 4px;
            transition: all 0.15s; font-size: 0.88rem; font-weight: 500;
            display: flex; align-items: center; gap: 10px;
        }

        .admin-menu-item:hover { color: var(--off-white); background: var(--glass-b); }

        .admin-menu-item.active {
            background: rgba(34,221,59,0.1); color: var(--accent);
            font-weight: 600;
        }

        .admin-content { flex: 1; padding: 2rem; min-width: 0; }

        .admin-section { display: none; }
        .admin-section.active { display: block; }

        .admin-card {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 1.5rem; margin-bottom: 1.5rem;
            box-shadow: var(--shadow);
        }

        .admin-card h3 {
            font-family: 'Fraunces', serif;
            font-size: 1.1rem; font-weight: 700; color: var(--white);
            margin-bottom: 1.2rem;
        }

        .stats-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px,1fr)); gap: 1rem; margin-bottom: 1.5rem; }

        .stat-card {
            background: var(--surface);
            border: 1px solid var(--border);
            border-radius: var(--radius);
            padding: 1.3rem; font-size: 0.9rem;
            color: var(--off-white); font-weight: 500;
            transition: 0.2s;
        }

        .stat-card:hover { border-color: var(--border-hover); }

        /* Admin tables */
        table { width: 100%; border-collapse: collapse; }
        th { text-align: left; padding: 10px 14px; font-size: 0.75rem; letter-spacing: 1px; text-transform: uppercase; color: var(--muted); border-bottom: 1px solid var(--border); }
        td { padding: 12px 14px; border-bottom: 1px solid rgba(255,255,255,0.04); font-size: 0.88rem; color: var(--off-white); }
        tr:last-child td { border-bottom: none; }
        tr:hover td { background: rgba(255,255,255,0.02); }

        /* Admin forms */
        .admin-input, .admin-select, .admin-textarea {
            width: 100%; padding: 11px 14px;
            background: rgba(255,255,255,0.05);
            border: 1px solid var(--border);
            border-radius: var(--radius-sm); color: var(--off-white);
            font-family: 'Outfit', sans-serif; font-size: 0.88rem;
            outline: none; transition: 0.2s;
        }

        .admin-input:focus, .admin-select:focus, .admin-textarea:focus {
            border-color: var(--accent); background: rgba(34,221,59,0.04);
        }

        .admin-input::placeholder, .admin-textarea::placeholder { color: var(--muted); }
        .admin-select option { background: var(--surface2); }

        .img-upload-zone {
            border: 2px dashed rgba(255,255,255,0.1);
            border-radius: var(--radius-sm);
            padding: 1.5rem; text-align: center;
            background: rgba(255,255,255,0.02);
            cursor: pointer; transition: 0.2s; color: var(--muted);
        }

        .img-upload-zone:hover, .img-upload-zone.dragover {
            border-color: var(--accent);
            background: rgba(34,221,59,0.04);
            color: var(--accent);
        }

        /* Admin buttons */
        .btn-primary {
            background: var(--accent); color: var(--bg);
            border: none; padding: 10px 22px;
            border-radius: 50px; font-weight: 700; cursor: pointer;
            font-family: 'Outfit', sans-serif; font-size: 0.88rem;
            transition: 0.2s; box-shadow: 0 4px 16px var(--accent-glow);
        }

        .btn-primary:hover { background: #30f04a; }

        .btn-danger {
            background: rgba(244,63,94,0.1); color: #fb7185;
            border: 1px solid rgba(244,63,94,0.2);
            padding: 5px 12px; border-radius: 40px; cursor: pointer;
            border: none; font-size: 0.82rem; transition: 0.2s;
            font-family: 'Outfit', sans-serif;
        }

        .btn-danger:hover { background: var(--danger); color: white; }

        .btn-edit {
            background: rgba(255,255,255,0.06); color: var(--muted);
            border: 1px solid var(--border);
            padding: 5px 12px; border-radius: 40px; cursor: pointer;
            font-size: 0.82rem; transition: 0.2s;
            font-family: 'Outfit', sans-serif;
        }

        .btn-edit:hover { color: var(--white); background: rgba(255,255,255,0.1); }

        select { background: var(--surface2); color: var(--off-white); padding: 6px 10px; border: 1px solid var(--border); border-radius: 40px; }

        /* ── TOAST ──────────────────────────── */
        .toast {
            position: fixed; bottom: 28px; right: 28px;
            background: var(--surface2);
            border: 1px solid var(--border);
            color: var(--off-white);
            padding: 12px 28px; border-radius: 50px; z-index: 9999;
            opacity: 0; transition: all 0.3s; pointer-events: none;
            font-size: 0.88rem; font-weight: 500;
            box-shadow: var(--shadow);
            transform: translateY(10px);
        }

        .toast.show {
            opacity: 1; transform: translateY(0);
            border-color: rgba(34,221,59,0.3);
        }

        /* ── PAGE / LAYOUT ───────────────────── */
        .page { padding-top: 72px; }
        .page.active { display: block; }

        /* ── SOCIAL CONNECT CARDS ─────────────── */
        .social-connect-grid {
            display: grid; grid-template-columns: 1fr 1fr 1fr; gap: 1rem; margin-bottom: 1rem;
        }

        .social-platform-card {
            border-radius: var(--radius); padding: 1.4rem 1.2rem;
            border: 1px solid var(--border);
            display: flex; flex-direction: column; gap: 10px;
            transition: all 0.25s; position: relative; overflow: hidden;
        }
        .social-platform-card::before {
            content: ''; position: absolute; inset: 0; opacity: 0.04;
            transition: opacity 0.25s;
        }
        .social-platform-card.wa { background: rgba(37,211,102,0.06); border-color: rgba(37,211,102,0.2); }
        .social-platform-card.wa::before { background: #25d366; }
        .social-platform-card.wa:hover { border-color: rgba(37,211,102,0.4); box-shadow: 0 0 24px rgba(37,211,102,0.1); }
        .social-platform-card.fb { background: rgba(24,119,242,0.06); border-color: rgba(24,119,242,0.2); }
        .social-platform-card.fb::before { background: #1877f2; }
        .social-platform-card.fb:hover { border-color: rgba(24,119,242,0.4); box-shadow: 0 0 24px rgba(24,119,242,0.1); }
        .social-platform-card.tt { background: rgba(255,0,80,0.06); border-color: rgba(255,0,80,0.2); }
        .social-platform-card.tt::before { background: #ff0050; }
        .social-platform-card.tt:hover { border-color: rgba(255,0,80,0.4); box-shadow: 0 0 24px rgba(255,0,80,0.1); }

        .social-card-header {
            display: flex; align-items: center; gap: 10px;
        }
        .social-icon-wrap {
            width: 42px; height: 42px; border-radius: 12px;
            display: flex; align-items: center; justify-content: center;
            font-size: 1.4rem; flex-shrink: 0;
        }
        .wa .social-icon-wrap { background: rgba(37,211,102,0.15); }
        .fb .social-icon-wrap { background: rgba(24,119,242,0.15); }
        .tt .social-icon-wrap { background: rgba(255,0,80,0.12); }

        .social-card-label { font-weight: 700; font-size: 0.95rem; color: var(--white); }
        .social-card-sub { font-size: 0.72rem; color: var(--muted); margin-top: 1px; }

        .social-status-dot {
            width: 8px; height: 8px; border-radius: 50%;
            background: var(--muted); margin-left: auto; flex-shrink: 0;
            transition: background 0.3s;
        }
        .social-status-dot.connected { background: var(--accent); box-shadow: 0 0 8px var(--accent-glow); }

        .social-input-row { display: flex; gap: 8px; align-items: center; }
        .social-input-row .admin-input { flex: 1; font-size: 0.82rem; padding: 9px 14px; }

        .social-action-btns { display: grid; grid-template-columns: 1fr 1fr; gap: 6px; }
        .btn-social-save {
            grid-column: 1 / -1;
            padding: 9px 0; border-radius: 40px; border: none;
            font-weight: 700; font-size: 0.82rem; cursor: pointer;
            font-family: 'Outfit', sans-serif; transition: 0.2s;
        }
        .wa .btn-social-save { background: rgba(37,211,102,0.15); color: #25d366; }
        .wa .btn-social-save:hover { background: #25d366; color: #fff; }
        .fb .btn-social-save { background: rgba(24,119,242,0.15); color: #1877f2; }
        .fb .btn-social-save:hover { background: #1877f2; color: #fff; }
        .tt .btn-social-save { background: rgba(255,0,80,0.12); color: #ff0050; }
        .tt .btn-social-save:hover { background: #ff0050; color: #fff; }

        .btn-social-test {
            padding: 9px 10px; border-radius: 40px; border: 1px solid var(--border);
            background: transparent; color: var(--muted); font-size: 0.78rem;
            cursor: pointer; font-family: 'Outfit', sans-serif; transition: 0.2s;
            text-align: center;
        }
        .btn-social-test:hover { color: var(--white); border-color: rgba(255,255,255,0.2); }

        .btn-social-clear {
            padding: 9px 10px; border-radius: 40px; border: none;
            background: rgba(244,63,94,0.1); color: #fb7185;
            font-size: 0.82rem; cursor: pointer; transition: 0.2s;
            text-align: center;
        }
        .btn-social-clear:hover { background: var(--danger); color: #fff; }

        .social-preview-bar {
            border-radius: var(--radius-sm); padding: 1rem 1.2rem;
            background: rgba(255,255,255,0.02); border: 1px solid var(--border);
            display: flex; align-items: center; gap: 12px; flex-wrap: wrap;
            margin-top: 0.5rem;
        }
        .social-preview-label { font-size: 0.78rem; color: var(--muted); flex-shrink: 0; }
        .social-preview-links { display: flex; gap: 8px; flex-wrap: wrap; }
        .social-pill {
            display: inline-flex; align-items: center; gap: 6px;
            padding: 6px 14px; border-radius: 40px; font-size: 0.82rem;
            font-weight: 600; text-decoration: none; transition: 0.2s;
            cursor: pointer; border: none;
        }
        .social-pill.wa-pill { background: rgba(37,211,102,0.12); color: #25d366; border: 1px solid rgba(37,211,102,0.25); }
        .social-pill.fb-pill { background: rgba(24,119,242,0.12); color: #74b3ff; border: 1px solid rgba(24,119,242,0.25); }
        .social-pill.tt-pill { background: rgba(255,0,80,0.1); color: #ff6b9d; border: 1px solid rgba(255,0,80,0.2); }
        .social-pill:hover { filter: brightness(1.2); transform: translateY(-1px); }
        .no-social-msg { font-size: 0.8rem; color: var(--muted); font-style: italic; }

        /* Floating social bar client side */
        .floating-social {
            position: fixed; right: 20px; bottom: 80px; z-index: 900;
            display: flex; flex-direction: column; gap: 10px;
        }
        .floating-social a {
            width: 46px; height: 46px; border-radius: 50%;
            display: flex; align-items: center; justify-content: center;
            font-size: 1.25rem; text-decoration: none;
            box-shadow: 0 4px 20px rgba(0,0,0,0.4);
            transition: all 0.25s; border: 1px solid transparent;
        }
        .float-wa { background: #25d366; color: #fff; }
        .float-wa:hover { transform: scale(1.12); box-shadow: 0 6px 28px rgba(37,211,102,0.4); }
        .float-fb { background: #1877f2; color: #fff; }
        .float-fb:hover { transform: scale(1.12); box-shadow: 0 6px 28px rgba(24,119,242,0.4); }
        .float-tt { background: #111; color: #fff; border-color: rgba(255,0,80,0.4); }
        .float-tt:hover { transform: scale(1.12); box-shadow: 0 6px 28px rgba(255,0,80,0.3); }

        /* ── LANGUAGE SWITCHER ───────────────── */
        .lang-switcher {
            display: flex; gap: 4px;
            background: rgba(255,255,255,0.04);
            padding: 4px; border-radius: 50px;
            border: 1px solid var(--border);
        }
        .lang-btn {
            padding: 5px 12px; border-radius: 40px; cursor: pointer;
            color: var(--muted); font-weight: 600; font-size: 0.78rem;
            background: transparent; transition: all 0.2s; border: none;
            font-family: 'Outfit', sans-serif; letter-spacing: 0.5px;
        }
        .lang-btn:hover { color: var(--white); }
        .lang-btn.active {
            background: var(--accent);
            color: var(--bg);
            box-shadow: 0 2px 12px var(--accent-glow);
        }
        [dir="rtl"] { direction: rtl; text-align: right; }
        [dir="rtl"] #nav-bar { flex-direction: row-reverse; }
        [dir="rtl"] .nav-right { flex-direction: row-reverse; }
        [dir="rtl"] .marquee-content { animation-direction: reverse; }
        [dir="rtl"] .search-wrap { margin-left: 0; margin-right: auto; }
        [dir="rtl"] .product-footer { flex-direction: row-reverse; }
        [dir="rtl"] .cart-header { flex-direction: row-reverse; }
        [dir="rtl"] .cart-row { flex-direction: row-reverse; }
        [dir="rtl"] .admin-layout { flex-direction: row-reverse; }
        [dir="rtl"] .footer-social { direction: rtl; }

        /* ── RESPONSIVE ─────────────────────── */
        /* ══════════════════════════════════════
           RESPONSIVE — TABLET (≤1024px)
        ══════════════════════════════════════ */
        @media (max-width: 1024px) {
            /* Navbar */
            #nav-bar { padding: 0 1.2rem; }
            .logo-tagline { display: none; }

            /* Admin sidebar becomes top bar */
            .admin-layout { flex-direction: column; }
            .admin-sidebar {
                width: 100%; height: auto; position: static;
                padding: 0.6rem 1rem;
                display: flex; flex-direction: row; flex-wrap: wrap;
                gap: 4px; border-right: none;
                border-bottom: 1px solid var(--border);
            }
            .admin-sidebar-title { display: none; }
            .admin-menu-item {
                padding: 7px 14px; font-size: 0.82rem;
                margin-bottom: 0;
            }
            .admin-content { padding: 1.2rem; }

            /* Social grid */
            .social-connect-grid { grid-template-columns: 1fr 1fr; }

            /* Products */
            .products-grid { grid-template-columns: repeat(auto-fill, minmax(200px,1fr)); gap: 1.2rem; }

            /* Cart */
            #cart-panel { width: 380px; }

            /* Hero */
            .hero { padding: 4rem 2rem 3rem; }

            /* Stats grid */
            .stats-grid { grid-template-columns: repeat(auto-fill, minmax(150px,1fr)); }
        }

        /* ══════════════════════════════════════
           RESPONSIVE — MOBILE (≤640px)
        ══════════════════════════════════════ */
        @media (max-width: 640px) {
            /* Navbar */
            #nav-bar { padding: 0 1rem; height: 60px; }
            .logo-kb { font-size: 1.1rem; }
            .logo-image { width: 36px; height: 36px; font-size: 0.85rem; }
            .custom-logo { gap: 9px; }
            .nav-tabs { display: none; }
            #mobile-nav-toggle { display: flex !important; }
            .search-wrap { display: none; } /* search moved to filter bar */
            .lang-switcher { gap: 2px; }
            .lang-btn { padding: 4px 8px; font-size: 0.7rem; }

            /* Page offset for shorter navbar */
            .page { padding-top: 60px; }
            .admin-layout { padding-top: 60px; }
            .marquee-banner { margin: 72px 0.75rem 0; }

            /* Hero */
            .hero {
                margin: 0.75rem 0.75rem 0;
                padding: 2.8rem 1.2rem 2.2rem;
                border-radius: var(--radius);
            }
            .hero h1 { font-size: clamp(1.8rem, 8vw, 2.8rem); }
            .hero p { font-size: 0.9rem; margin-bottom: 1.8rem; }
            .hero-stats { gap: 1.2rem; flex-wrap: wrap; margin-top: 2rem; padding-top: 1.5rem; }
            .stat-num { font-size: 1.4rem; }

            /* Filter bar */
            .filter-bar {
                margin: 0.75rem 0.75rem 0;
                padding: 8px 10px; gap: 5px;
                border-radius: var(--radius);
                flex-wrap: wrap;
            }
            .filter-btn { padding: 6px 12px; font-size: 0.8rem; }

            /* Search inside filter bar on mobile */
            .search-wrap { display: block; width: 100%; margin-left: 0; margin-top: 4px; }
            .search-wrap input { width: 100%; }

            /* Products */
            .products-grid {
                grid-template-columns: repeat(2, 1fr);
                gap: 0.75rem;
                padding: 0.75rem 0.75rem 5rem;
            }

            /* Product card compact */
            .product-card { border-radius: var(--radius-sm); }

            /* Cart */
            #cart-panel {
                width: 100%; border-radius: 20px 20px 0 0;
                bottom: 0; top: auto; max-height: 85vh; overflow-y: auto;
            }

            /* Admin sidebar — scrollable horizontal strip */
            .admin-sidebar {
                flex-wrap: nowrap; overflow-x: auto;
                padding: 0.5rem 0.75rem;
                -webkit-overflow-scrolling: touch;
                scrollbar-width: none;
            }
            .admin-sidebar::-webkit-scrollbar { display: none; }
            .admin-menu-item { white-space: nowrap; flex-shrink: 0; font-size: 0.8rem; padding: 6px 12px; }
            .admin-content { padding: 0.75rem; }
            .admin-card { padding: 1rem; border-radius: var(--radius-sm); }
            .admin-card h3 { font-size: 1rem; margin-bottom: 1rem; }

            /* Social cards — single column */
            .social-connect-grid { grid-template-columns: 1fr; }

            /* Stats grid */
            .stats-grid { grid-template-columns: 1fr 1fr; gap: 0.75rem; }
            .stat-card { padding: 1rem; font-size: 0.82rem; }

            /* Tables — horizontal scroll */
            .admin-card > table { display: block; overflow-x: auto; -webkit-overflow-scrolling: touch; }

            /* Checkout */
            .checkout-box { padding: 1.5rem 1rem; border-radius: var(--radius); }
            .checkout-grid { grid-template-columns: 1fr; }
            .checkout-input.full { grid-column: 1; }
            .checkout-actions { flex-direction: column; }

            /* Toast */
            .toast { right: 12px; left: 12px; text-align: center; bottom: 80px; }

            /* Floating social */
            #floating-social { bottom: 14px; left: 14px; gap: 8px; }
            .float-wa, .float-fb, .float-tt { width: 40px; height: 40px; font-size: 1.1rem; }

            /* Footer */
            .site-footer { padding: 1.5rem 1rem; text-align: center; }
            #social-links-container { flex-direction: column; align-items: center; gap: 8px; }

            /* Login modal */
            .login-card { padding: 1.8rem 1.2rem; margin: 1rem; border-radius: var(--radius); }
        }

        /* ══════════════════════════════════════
           RESPONSIVE — VERY SMALL (≤360px)
        ══════════════════════════════════════ */
        @media (max-width: 360px) {
            .products-grid { grid-template-columns: 1fr; }
            .stats-grid { grid-template-columns: 1fr; }
            .hero h1 { font-size: 1.6rem; }
        }

        /* Cart overlay */
        #cart-overlay {
            display: none; position: fixed; inset: 0;
            background: rgba(0,0,0,0.6); z-index: 2000;
            backdrop-filter: blur(4px);
        }
    </style>
</head>
<body>

<!-- Animated Background -->
<div class="animated-bg">
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>
</div>

<div class="content-overlay">

    <!-- ─── MODALS ─────────────────────────────── -->

    <!-- Admin Setup Modal -->
    <div id="admin-setup-modal" class="modal-backdrop" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.8);backdrop-filter:blur(8px);z-index:6000;align-items:center;justify-content:center">
        <div class="login-card">
            <h2>🔐 Créer un compte Admin</h2>
            <input type="email" id="setup-email" class="login-input" placeholder="Email administrateur">
            <input type="password" id="setup-pwd" class="login-input" placeholder="Mot de passe (min 4)">
            <input type="password" id="setup-pwd-confirm" class="login-input" placeholder="Confirmer le mot de passe">
            <button onclick="createAdminAccount()" class="login-btn" style="margin-top:8px">Créer mon compte</button>
            <div class="back-link" onclick="closeSetupModal()">← Retour à la connexion</div>
            <p id="setup-error" style="color:#fb7185;font-size:0.8rem;margin-top:8px"></p>
        </div>
    </div>

    <!-- Admin Login Modal -->
    <div id="admin-login" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.8);backdrop-filter:blur(8px);z-index:5000;align-items:center;justify-content:center">
        <div class="login-card">
            <h2>Connexion Admin</h2>
            <input type="text" id="admin-email" class="login-input" placeholder="Email / Identifiant">
            <input type="password" id="admin-pwd" class="login-input" placeholder="Mot de passe">
            <div class="remember-row">
                <label style="display:flex;align-items:center;gap:6px;cursor:pointer">
                    <input type="checkbox" id="remember-checkbox"> Se souvenir
                </label>
                <div>
                    <a href="#" onclick="showForgotPassword()" class="forgot-link">Mot de passe oublié ?</a>
                    <span class="separator">|</span>
                    <a href="#" onclick="showSetupFromLogin()" class="create-link">Créer un compte</a>
                </div>
            </div>
            <button onclick="checkAdminPwd()" class="login-btn">Se connecter</button>
            <p id="login-error" style="color:#fb7185;font-size:0.8rem;margin-top:12px;display:none">Identifiants incorrects</p>
        </div>
    </div>

    <!-- Forgot Password Modal -->
    <div id="forgot-modal" style="display:none;position:fixed;inset:0;background:rgba(0,0,0,0.85);backdrop-filter:blur(8px);z-index:7000;align-items:center;justify-content:center">
        <div class="login-card">
            <h2>🔁 Réinitialiser</h2>
            <input type="email" id="forgot-email" class="login-input" placeholder="Email admin">
            <input type="password" id="forgot-new-pwd" class="login-input" placeholder="Nouveau mot de passe (min 4)">
            <input type="password" id="forgot-confirm-pwd" class="login-input" placeholder="Confirmer">
            <button onclick="resetAdminPassword()" class="login-btn" style="margin-top:8px">Réinitialiser</button>
            <div class="back-link" onclick="closeForgotModal()">← Retour à la connexion</div>
            <p id="forgot-error" style="color:#fb7185;margin-top:8px;font-size:0.83rem"></p>
        </div>
    </div>

    <!-- ─── NAVBAR ──────────────────────────── -->
    <nav id="nav-bar">
        <div class="custom-logo" onclick="showPage('client')">
            <div class="logo-image">KB</div>
            <div class="logo-text-wrap">
                <div class="logo-kb">KB<span>market</span></div>
                <div class="logo-tagline">KHADIMBADIANE · YOUR FAVOR DESIGN</div>
            </div>
        </div>
        <div class="nav-tabs">
            <button class="nav-tab active" data-page="client">🛍️ Boutique</button>
            <button class="nav-tab" id="admin-nav-btn" data-page="admin" style="display:none">⚙️ Admin</button>
        </div>
        <!-- Mobile nav toggle -->
        <button id="mobile-nav-toggle" onclick="toggleMobileNav()" style="display:none;background:rgba(255,255,255,0.06);border:1px solid var(--border);color:var(--off-white);width:38px;height:38px;border-radius:50%;cursor:pointer;font-size:1.1rem;align-items:center;justify-content:center;">☰</button>
        <!-- Mobile nav dropdown -->
        <div id="mobile-nav-dropdown" style="display:none;position:fixed;top:60px;left:0;right:0;background:rgba(6,8,15,0.97);backdrop-filter:blur(20px);border-bottom:1px solid var(--border);z-index:999;padding:0.75rem 1rem;flex-direction:column;gap:6px;">
            <button class="nav-tab active" onclick="showPage('client');closeMobileNav()" style="width:100%;text-align:left;padding:12px 16px;border-radius:12px;">🛍️ Boutique</button>
            <button id="admin-nav-btn-mobile" onclick="showPage('admin');closeMobileNav()" class="nav-tab" style="display:none;width:100%;text-align:left;padding:12px 16px;border-radius:12px;">⚙️ Admin</button>
        </div>
        <div class="nav-right" style="display:flex;align-items:center;gap:10px">
            <div class="lang-switcher" id="lang-switcher">
                <button class="lang-btn active" onclick="setLang('fr')">🇫🇷 FR</button>
                <button class="lang-btn" onclick="setLang('en')">🇬🇧 EN</button>
                <button class="lang-btn" onclick="setLang('ar')">🇸🇦 AR</button>
            </div>
            <button class="cart-btn" id="cart-icon">🛒<span class="cart-badge" id="cart-count">0</span></button>
        </div>
    </nav>

    <!-- ─── CART ────────────────────────────── -->
    <div id="cart-overlay"></div>
    <div id="cart-panel">
        <div class="cart-header">
            <h3>🛒 Mon Panier</h3>
            <button class="close-cart-btn">✕</button>
        </div>
        <div id="cart-items-list"></div>
        <div class="cart-footer">
            <div class="cart-totals">
                <div class="cart-row"><span>Sous-total</span><span id="cart-subtotal">0 GMD</span></div>
                <div class="cart-row total"><span>Total</span><span id="cart-total-val">0 GMD</span></div>
            </div>
            <button class="checkout-btn">Commander →</button>
        </div>
    </div>

    <!-- ─── CHECKOUT MODAL ───────────────────── -->
    <div id="checkout-modal">
        <div class="checkout-box">
            <h3>📦 Finaliser la commande</h3>
            <div id="checkout-form-wrap">
                <div class="checkout-grid">
                    <input id="c-fname" class="checkout-input" placeholder="Prénom">
                    <input id="c-lname" class="checkout-input" placeholder="Nom">
                    <input id="c-email" class="checkout-input full" placeholder="Email">
                    <input id="c-phone" class="checkout-input full" placeholder="Téléphone">
                    <input id="c-addr" class="checkout-input full" placeholder="Adresse de livraison">
                    <div id="payment-methods-list"></div>
                    <div style="grid-column:1/-1;font-size:0.85rem;color:var(--muted)">Récapitulatif : <span id="checkout-summary" style="color:var(--accent);font-weight:600"></span></div>
                    <div class="checkout-actions">
                        <button class="btn-cancel" onclick="closeCheckout()">Annuler</button>
                        <button class="btn-confirm" onclick="placeOrder()">✓ Confirmer la commande</button>
                    </div>
                </div>
            </div>
        </div>
    </div>

    <!-- ─── CLIENT PAGE ─────────────────────── -->
    <div id="page-client" class="page active">

        <!-- Marquee Banner -->
        <div id="marquee-banner" class="marquee-banner" style="display:block">
            <div class="marquee-content" id="marquee-text"></div>
        </div>

        <!-- Hero -->
        <div class="hero">
            <div class="hero-label">✦ Nouvelle collection disponible</div>
            <h1>Votre style,<br><em>notre passion</em></h1>
            <p>Découvrez les créations uniques signées <strong>YOUR FAVOR DESIGN</strong> — mode, beauté et lifestyle sélectionnés pour vous.</p>
            <button class="hero-cta" onclick="scrollToProducts()">
                Explorer la boutique <span>↓</span>
            </button>
            <div class="hero-stats">
                <div class="stat">
                    <div class="stat-num" id="stat-products">0</div>
                    <div class="stat-label">Produits</div>
                </div>
                <div class="stat">
                    <div class="stat-num" id="stat-clients">0</div>
                    <div class="stat-label">Clients</div>
                </div>
                <div class="stat">
                    <div class="stat-num">5 ⭐</div>
                    <div class="stat-label">Note</div>
                </div>
            </div>
        </div>

        <!-- Filter Bar -->
        <div class="filter-bar">
            <button class="filter-btn active" data-cat="all">Tous</button>
            <button class="filter-btn" data-cat="Électronique">📱 Électronique</button>
            <button class="filter-btn" data-cat="Mode">👗 Mode</button>
            <button class="filter-btn" data-cat="Maison">🏠 Maison</button>
            <button class="filter-btn" data-cat="Beauté">💄 Beauté</button>
            <button class="filter-btn" data-cat="Alimentation">🍎 Alimentation</button>
            <div class="search-wrap">
                <input type="text" id="search-input" placeholder="🔍 Rechercher...">
            </div>
        </div>

        <!-- Products Grid -->
        <div class="products-grid" id="products-grid"></div>

        <!-- Footer -->
        <div class="footer-social">
            <div class="footer-logo">KB<span>market</span></div>
            <div class="footer-divider"></div>
            <div class="social-links" id="social-links-container"></div>
            <div class="shop-info" id="shop-info-footer"></div>
        </div>
    </div>

    <!-- ─── ADMIN PAGE ───────────────────────── -->
    <div id="page-admin"></div>

    <!-- Floating Social Bar (client side) -->
    <div class="floating-social" id="floating-social"></div>

    <!-- Toast -->
    <div id="toast" class="toast"></div>
</div>

<script>
    // ========== JSONBIN CLOUD ==========
    const JSONBIN_KEY = '$2a$10$jr0ch3RCMICzqVMuGZxtnu3SKu9MQ9Bl6fcMoFCP3r.S4UuLeEWXW';
    const JSONBIN_ID  = '6a0e5c06ee5a733b12f2f1ae';
    const JSONBIN_URL = `https://api.jsonbin.io/v3/b/${JSONBIN_ID}`;

    async function loadProductsFromCloud() {
        try {
            const res = await fetch(`${JSONBIN_URL}/latest`, {
                headers: {
                    'X-Master-Key': JSONBIN_KEY,
                    'X-Bin-Meta': 'false'
                }
            });
            if (!res.ok) throw new Error('HTTP ' + res.status);
            const data = await res.json();
            const prods = data.products || (data.record && data.record.products);
            if (Array.isArray(prods) && prods.length > 0) {
                products = prods;
                localStorage.setItem('kb_products', JSON.stringify(products));
                return;
            }
        } catch(e) {
            console.warn('JSONBin load failed, using localStorage:', e);
        }
        // Fallback : localStorage
        const saved = localStorage.getItem('kb_products');
        if (saved) {
            try { const p = JSON.parse(saved); if (p.length > 0) products = p; } catch(e) {}
        }
    }

    async function saveProductsToCloud() {
        // Sauvegarde locale immédiate
        localStorage.setItem('kb_products', JSON.stringify(products));
        // Sauvegarde cloud
        try {
            const res = await fetch(JSONBIN_URL, {
                method: 'PUT',
                headers: {
                    'Content-Type': 'application/json',
                    'X-Master-Key': JSONBIN_KEY
                },
                body: JSON.stringify({ products })
            });
            if (!res.ok) throw new Error('HTTP ' + res.status);
            return true;
        } catch(e) {
            console.error('JSONBin save failed:', e);
            showToast('⚠️ Sauvegardé localement seulement');
            return false;
        }
    }

    // ========== I18N ==========
    const i18n = {
        fr: {
            dir: "ltr",
            shopBtn: "🛍️ Boutique", adminBtn: "⚙️ Admin",
            heroLabel: "✦ Nouvelle collection disponible",
            heroTitle: "Votre style,<br><em>notre passion</em>",
            heroDesc: "Découvrez les créations uniques signées <strong>YOUR FAVOR DESIGN</strong> — mode, beauté et lifestyle sélectionnés pour vous.",
            heroCta: "Explorer la boutique ↓",
            statProducts: "Produits", statClients: "Clients", statRating: "Note",
            filterAll: "Tous", filterElec: "📱 Électronique", filterMode: "👗 Mode",
            filterMaison: "🏠 Maison", filterBeaute: "💄 Beauté", filterFood: "🍎 Alimentation",
            searchPlaceholder: "🔍 Rechercher...",
            cartTitle: "🛒 Mon Panier",
            cartSubtotal: "Sous-total", cartTotal: "Total",
            checkoutBtn: "Commander →",
            cartEmpty: "🛒 Votre panier est vide",
            addedToCart: "✓ Ajouté au panier",
            checkoutTitle: "📦 Finaliser la commande",
            fnameHolder: "Prénom", lnameHolder: "Nom", emailHolder: "Email",
            phoneHolder: "Téléphone", addrHolder: "Adresse de livraison",
            cancelBtn: "Annuler", confirmBtn: "✓ Confirmer la commande",
            recapLabel: "Récapitulatif : ",
            paymentLabel: "💰 Moyens de paiement :",
            cartEmptyMsg: "Panier vide !",
            fillFields: "Remplissez tous les champs",
            orderPlaced: "✓ Commande enregistrée !",
            followUs: "Suivez-nous bientôt",
            adminSetupTitle: "🔐 Créer un compte Admin",
            emailAdmin: "Email administrateur", pwdHolder: "Mot de passe (min 4)",
            pwdConfirmHolder: "Confirmer le mot de passe",
            createAccount: "Créer mon compte",
            backLogin: "← Retour à la connexion",
            adminLoginTitle: "Connexion Admin",
            emailIdHolder: "Email / Identifiant", pwdLoginHolder: "Mot de passe",
            rememberMe: "Se souvenir", forgotPwd: "Mot de passe oublié ?",
            createLink: "Créer un compte", connectBtn: "Se connecter",
            loginError: "Identifiants incorrects",
            resetTitle: "🔁 Réinitialiser", emailAdminReset: "Email admin",
            newPwdHolder: "Nouveau mot de passe (min 4)", confirmPwdHolder: "Confirmer",
            resetBtn: "Réinitialiser",
            noProductFound: "Aucun produit trouvé",
            adminMenu: "Menu", adminDash: "📊 Tableau de bord", adminProd: "📦 Produits",
            adminOrders: "🛒 Commandes", adminClients: "👥 Clients",
            adminSettings: "⚙️ Paramètres", adminLogout: "🚪 Déconnexion",
            addProductBtn: "+ Ajouter un produit",
            shopInfoTitle: "🏢 Informations boutique", shopNameHolder: "Nom de la boutique",
            shopAddrHolder: "Adresse", shopPhoneHolder: "Téléphone", shopEmailHolder: "Email de contact",
            saveBoutique: "💾 Sauvegarder",
            marqueeTitle: "📢 Bandeau défilant", marqueeTextHolder: "Texte du bandeau",
            marqueeImgHolder: "URL image (optionnel)", marqueeEnable: "Activer le bandeau",
            marqueeSave: "Appliquer",
            paymentTitle: "💳 Moyens de paiement", pmNameHolder: "Nom (Wave, Orange…)",
            pmNumberHolder: "Numéro", pmAdd: "➕ Ajouter",
            adminCredsTitle: "🔐 Identifiants admin", adminEmailHolder: "Email admin",
            adminPwdHolder: "Nouveau mot de passe (min 4)", adminCredsUpdate: "Mettre à jour",
            dashRevenues: "💰 Revenus", dashOrders: "🛒 Commandes",
            dashProducts: "📦 Produits", dashClients: "👥 Clients",
            recentOrdersTitle: "Commandes récentes",
            colId: "#ID", colClient: "Client", colTotal: "Total", colStatus: "Statut",
            colProduct: "Produit", colStock: "Stock", colActions: "Actions",
            editBtn: "✏️ Modifier", noProducts: "Aucun produit",
            noOrders: "Aucune commande", noClients: "Aucun client",
            statusUpdated: "Statut mis à jour", shopSaved: "Boutique sauvegardée",
            marqueeSaved: "Bandeau mis à jour", pmAdded: "Méthode ajoutée",
            pmRemoved: "Supprimé", credUpdated: "Identifiants mis à jour",
            productSaved: "✓ Produit sauvegardé", productDeleted: "Produit supprimé",
            deleteConfirm: "Supprimer ce produit ?",
            nameRequired: "Nom et prix requis", pmRequired: "Nom et numéro requis",
            emailRequired: "Email requis", pwdMinError: "Mot de passe min 4",
            setupError: "Email valide et mot de passe (min 4) identique requis",
            accountCreated: "Compte créé ! Veuillez vous connecter.",
            noAccount: "Aucun compte, créez-en un",
            articleLabel: "article(s)", maxSize: "Max 5 Mo",
            articlesSummary: (n, total) => `${n} article(s) — ${total.toLocaleString()} GMD`,
            productFormTitle: "Produit", pNameHolder: "Nom du produit",
            pPriceHolder: "Prix (GMD)", pStockHolder: "Stock",
            pEmojiHolder: "Emoji (ex: 📱)", pBadgeNone: "Aucun badge",
            pBadgeNew: "Nouveau", pBadgeSale: "Promo", pBadgeHot: "Populaire",
            uploadZone: "🖼️ Glisser-déposer ou cliquer pour une image (max 5 Mo)",
            pImgUrlHolder: "Ou URL de l'image", pDescHolder: "Description",
            cancelFormBtn: "Annuler", saveFormBtn: "💾 Enregistrer",
            removeImgBtn: "✕ Supprimer",
            listProductsTitle: "Liste des produits",
            clientsTitle: "Clients",
            allOrdersTitle: "Toutes les commandes",
            badgeNew: "NOUVEAU", badgeSale: "PROMO", badgeHot: "🔥 TOP",
        },
        en: {
            dir: "ltr",
            shopBtn: "🛍️ Shop", adminBtn: "⚙️ Admin",
            heroLabel: "✦ New collection available",
            heroTitle: "Your style,<br><em>our passion</em>",
            heroDesc: "Discover unique creations by <strong>YOUR FAVOR DESIGN</strong> — fashion, beauty and lifestyle curated for you.",
            heroCta: "Explore the shop ↓",
            statProducts: "Products", statClients: "Customers", statRating: "Rating",
            filterAll: "All", filterElec: "📱 Electronics", filterMode: "👗 Fashion",
            filterMaison: "🏠 Home", filterBeaute: "💄 Beauty", filterFood: "🍎 Food",
            searchPlaceholder: "🔍 Search...",
            cartTitle: "🛒 My Cart",
            cartSubtotal: "Subtotal", cartTotal: "Total",
            checkoutBtn: "Order →",
            cartEmpty: "🛒 Your cart is empty",
            addedToCart: "✓ Added to cart",
            checkoutTitle: "📦 Complete order",
            fnameHolder: "First name", lnameHolder: "Last name", emailHolder: "Email",
            phoneHolder: "Phone", addrHolder: "Delivery address",
            cancelBtn: "Cancel", confirmBtn: "✓ Confirm order",
            recapLabel: "Summary: ",
            paymentLabel: "💰 Payment methods:",
            cartEmptyMsg: "Cart is empty!",
            fillFields: "Please fill all fields",
            orderPlaced: "✓ Order placed!",
            followUs: "Follow us soon",
            adminSetupTitle: "🔐 Create Admin Account",
            emailAdmin: "Admin email", pwdHolder: "Password (min 4)",
            pwdConfirmHolder: "Confirm password",
            createAccount: "Create account",
            backLogin: "← Back to login",
            adminLoginTitle: "Admin Login",
            emailIdHolder: "Email / Username", pwdLoginHolder: "Password",
            rememberMe: "Remember me", forgotPwd: "Forgot password?",
            createLink: "Create account", connectBtn: "Sign in",
            loginError: "Incorrect credentials",
            resetTitle: "🔁 Reset password", emailAdminReset: "Admin email",
            newPwdHolder: "New password (min 4)", confirmPwdHolder: "Confirm",
            resetBtn: "Reset",
            noProductFound: "No products found",
            adminMenu: "Menu", adminDash: "📊 Dashboard", adminProd: "📦 Products",
            adminOrders: "🛒 Orders", adminClients: "👥 Customers",
            adminSettings: "⚙️ Settings", adminLogout: "🚪 Logout",
            addProductBtn: "+ Add product",
            shopInfoTitle: "🏢 Shop information", shopNameHolder: "Shop name",
            shopAddrHolder: "Address", shopPhoneHolder: "Phone", shopEmailHolder: "Contact email",
            saveBoutique: "💾 Save",
            marqueeTitle: "📢 Scrolling banner", marqueeTextHolder: "Banner text",
            marqueeImgHolder: "Image URL (optional)", marqueeEnable: "Enable banner",
            marqueeSave: "Apply",
            paymentTitle: "💳 Payment methods", pmNameHolder: "Name (Wave, Orange…)",
            pmNumberHolder: "Number", pmAdd: "➕ Add",
            adminCredsTitle: "🔐 Admin credentials", adminEmailHolder: "Admin email",
            adminPwdHolder: "New password (min 4)", adminCredsUpdate: "Update",
            dashRevenues: "💰 Revenue", dashOrders: "🛒 Orders",
            dashProducts: "📦 Products", dashClients: "👥 Customers",
            recentOrdersTitle: "Recent orders",
            colId: "#ID", colClient: "Customer", colTotal: "Total", colStatus: "Status",
            colProduct: "Product", colStock: "Stock", colActions: "Actions",
            editBtn: "✏️ Edit", noProducts: "No products",
            noOrders: "No orders", noClients: "No customers",
            statusUpdated: "Status updated", shopSaved: "Shop saved",
            marqueeSaved: "Banner updated", pmAdded: "Method added",
            pmRemoved: "Removed", credUpdated: "Credentials updated",
            productSaved: "✓ Product saved", productDeleted: "Product deleted",
            deleteConfirm: "Delete this product?",
            nameRequired: "Name and price required", pmRequired: "Name and number required",
            emailRequired: "Email required", pwdMinError: "Password min 4",
            setupError: "Valid email and matching password (min 4) required",
            accountCreated: "Account created! Please sign in.",
            noAccount: "No account, please create one",
            articleLabel: "item(s)", maxSize: "Max 5 MB",
            articlesSummary: (n, total) => `${n} item(s) — ${total.toLocaleString()} GMD`,
            productFormTitle: "Product", pNameHolder: "Product name",
            pPriceHolder: "Price (GMD)", pStockHolder: "Stock",
            pEmojiHolder: "Emoji (e.g. 📱)", pBadgeNone: "No badge",
            pBadgeNew: "New", pBadgeSale: "Sale", pBadgeHot: "Popular",
            uploadZone: "🖼️ Drag & drop or click to upload image (max 5 MB)",
            pImgUrlHolder: "Or image URL", pDescHolder: "Description",
            cancelFormBtn: "Cancel", saveFormBtn: "💾 Save",
            removeImgBtn: "✕ Remove",
            listProductsTitle: "Products list",
            clientsTitle: "Customers",
            allOrdersTitle: "All orders",
            badgeNew: "NEW", badgeSale: "SALE", badgeHot: "🔥 HOT",
        },
        ar: {
            dir: "rtl",
            shopBtn: "🛍️ المتجر", adminBtn: "⚙️ الإدارة",
            heroLabel: "✦ مجموعة جديدة متاحة",
            heroTitle: "أسلوبك،<br><em>شغفنا</em>",
            heroDesc: "اكتشف الإبداعات الفريدة من <strong>YOUR FAVOR DESIGN</strong> — موضة وجمال ونمط حياة مختار خصيصاً لك.",
            heroCta: "استكشف المتجر ↓",
            statProducts: "المنتجات", statClients: "العملاء", statRating: "التقييم",
            filterAll: "الكل", filterElec: "📱 الإلكترونيات", filterMode: "👗 الموضة",
            filterMaison: "🏠 المنزل", filterBeaute: "💄 الجمال", filterFood: "🍎 الغذاء",
            searchPlaceholder: "🔍 بحث...",
            cartTitle: "🛒 سلتي",
            cartSubtotal: "المجموع الفرعي", cartTotal: "الإجمالي",
            checkoutBtn: "طلب →",
            cartEmpty: "🛒 سلتك فارغة",
            addedToCart: "✓ تمت الإضافة إلى السلة",
            checkoutTitle: "📦 إتمام الطلب",
            fnameHolder: "الاسم الأول", lnameHolder: "اللقب", emailHolder: "البريد الإلكتروني",
            phoneHolder: "الهاتف", addrHolder: "عنوان التسليم",
            cancelBtn: "إلغاء", confirmBtn: "✓ تأكيد الطلب",
            recapLabel: "ملخص: ",
            paymentLabel: "💰 طرق الدفع:",
            cartEmptyMsg: "السلة فارغة!",
            fillFields: "يرجى ملء جميع الحقول",
            orderPlaced: "✓ تم تسجيل الطلب!",
            followUs: "تابعونا قريبًا",
            adminSetupTitle: "🔐 إنشاء حساب مدير",
            emailAdmin: "البريد الإلكتروني للمدير", pwdHolder: "كلمة المرور (4 على الأقل)",
            pwdConfirmHolder: "تأكيد كلمة المرور",
            createAccount: "إنشاء الحساب",
            backLogin: "← العودة لتسجيل الدخول",
            adminLoginTitle: "تسجيل دخول المدير",
            emailIdHolder: "البريد / المعرّف", pwdLoginHolder: "كلمة المرور",
            rememberMe: "تذكرني", forgotPwd: "نسيت كلمة المرور؟",
            createLink: "إنشاء حساب", connectBtn: "دخول",
            loginError: "بيانات الاعتماد غير صحيحة",
            resetTitle: "🔁 إعادة التعيين", emailAdminReset: "بريد المدير",
            newPwdHolder: "كلمة مرور جديدة (4 على الأقل)", confirmPwdHolder: "تأكيد",
            resetBtn: "إعادة التعيين",
            noProductFound: "لم يتم العثور على منتجات",
            adminMenu: "القائمة", adminDash: "📊 لوحة التحكم", adminProd: "📦 المنتجات",
            adminOrders: "🛒 الطلبات", adminClients: "👥 العملاء",
            adminSettings: "⚙️ الإعدادات", adminLogout: "🚪 تسجيل الخروج",
            addProductBtn: "+ إضافة منتج",
            shopInfoTitle: "🏢 معلومات المتجر", shopNameHolder: "اسم المتجر",
            shopAddrHolder: "العنوان", shopPhoneHolder: "الهاتف", shopEmailHolder: "البريد الإلكتروني للتواصل",
            saveBoutique: "💾 حفظ",
            marqueeTitle: "📢 الشريط المتحرك", marqueeTextHolder: "نص الشريط",
            marqueeImgHolder: "رابط الصورة (اختياري)", marqueeEnable: "تفعيل الشريط",
            marqueeSave: "تطبيق",
            paymentTitle: "💳 طرق الدفع", pmNameHolder: "الاسم (Wave, Orange…)",
            pmNumberHolder: "الرقم", pmAdd: "➕ إضافة",
            adminCredsTitle: "🔐 بيانات المدير", adminEmailHolder: "بريد المدير",
            adminPwdHolder: "كلمة مرور جديدة (4 على الأقل)", adminCredsUpdate: "تحديث",
            dashRevenues: "💰 الإيرادات", dashOrders: "🛒 الطلبات",
            dashProducts: "📦 المنتجات", dashClients: "👥 العملاء",
            recentOrdersTitle: "الطلبات الأخيرة",
            colId: "#المعرف", colClient: "العميل", colTotal: "الإجمالي", colStatus: "الحالة",
            colProduct: "المنتج", colStock: "المخزون", colActions: "الإجراءات",
            editBtn: "✏️ تعديل", noProducts: "لا توجد منتجات",
            noOrders: "لا توجد طلبات", noClients: "لا يوجد عملاء",
            statusUpdated: "تم تحديث الحالة", shopSaved: "تم حفظ المتجر",
            marqueeSaved: "تم تحديث الشريط", pmAdded: "تمت إضافة الطريقة",
            pmRemoved: "تم الحذف", credUpdated: "تم تحديث بيانات الاعتماد",
            productSaved: "✓ تم حفظ المنتج", productDeleted: "تم حذف المنتج",
            deleteConfirm: "حذف هذا المنتج؟",
            nameRequired: "الاسم والسعر مطلوبان", pmRequired: "الاسم والرقم مطلوبان",
            emailRequired: "البريد الإلكتروني مطلوب", pwdMinError: "كلمة المرور 4 على الأقل",
            setupError: "بريد إلكتروني صحيح وكلمة مرور متطابقة (4 على الأقل) مطلوبة",
            accountCreated: "تم إنشاء الحساب! يرجى تسجيل الدخول.",
            noAccount: "لا يوجد حساب، يرجى إنشاء حساب",
            articleLabel: "عنصر(عناصر)", maxSize: "الحد الأقصى 5 ميغابايت",
            articlesSummary: (n, total) => `${n} عنصر — ${total.toLocaleString()} GMD`,
            productFormTitle: "المنتج", pNameHolder: "اسم المنتج",
            pPriceHolder: "السعر (GMD)", pStockHolder: "المخزون",
            pEmojiHolder: "رمز تعبيري (مثل 📱)", pBadgeNone: "بدون شارة",
            pBadgeNew: "جديد", pBadgeSale: "تخفيض", pBadgeHot: "رائج",
            uploadZone: "🖼️ اسحب وأفلت أو انقر لتحميل صورة (الحد الأقصى 5 ميغابايت)",
            pImgUrlHolder: "أو رابط الصورة", pDescHolder: "الوصف",
            cancelFormBtn: "إلغاء", saveFormBtn: "💾 حفظ",
            removeImgBtn: "✕ حذف",
            listProductsTitle: "قائمة المنتجات",
            clientsTitle: "العملاء",
            allOrdersTitle: "جميع الطلبات",
            badgeNew: "جديد", badgeSale: "تخفيض", badgeHot: "🔥 رائج",
        }
    };

    let currentLang = 'fr';

    function setLang(lang) {
        currentLang = lang;
        const t = i18n[lang];

        // Update html dir
        document.documentElement.setAttribute('dir', t.dir);
        document.documentElement.setAttribute('lang', lang);

        // Language buttons
        document.querySelectorAll('.lang-btn').forEach(btn => {
            btn.classList.toggle('active', btn.getAttribute('onclick').includes(`'${lang}'`));
        });

        // Navbar tabs
        const tabs = document.querySelectorAll('.nav-tab');
        if (tabs[0]) tabs[0].textContent = t.shopBtn;
        if (tabs[1]) tabs[1].textContent = t.adminBtn;

        // Hero
        const heroLabel = document.querySelector('.hero-label');
        if (heroLabel) heroLabel.textContent = t.heroLabel;
        const heroH1 = document.querySelector('.hero h1');
        if (heroH1) heroH1.innerHTML = t.heroTitle;
        const heroP = document.querySelector('.hero p');
        if (heroP) heroP.innerHTML = t.heroDesc;
        const heroCta = document.querySelector('.hero-cta');
        if (heroCta) heroCta.innerHTML = t.heroCta;

        // Stat labels
        const statLabels = document.querySelectorAll('.stat-label');
        if (statLabels[0]) statLabels[0].textContent = t.statProducts;
        if (statLabels[1]) statLabels[1].textContent = t.statClients;
        if (statLabels[2]) statLabels[2].textContent = t.statRating;

        // Filter buttons
        const filterBtns = document.querySelectorAll('.filter-btn');
        const filterTexts = [t.filterAll, t.filterElec, t.filterMode, t.filterMaison, t.filterBeaute, t.filterFood];
        filterBtns.forEach((btn, i) => { if (filterTexts[i]) btn.textContent = filterTexts[i]; });

        // Search input
        const searchInput = document.getElementById('search-input');
        if (searchInput) searchInput.placeholder = t.searchPlaceholder;

        // Cart
        const cartHeader = document.querySelector('.cart-header h3');
        if (cartHeader) cartHeader.textContent = t.cartTitle;
        const cartRows = document.querySelectorAll('.cart-row');
        if (cartRows[0]) cartRows[0].querySelector('span:first-child').textContent = t.cartSubtotal;
        if (cartRows[1]) cartRows[1].querySelector('span:first-child').textContent = t.cartTotal;
        const checkoutBtn = document.querySelector('.checkout-btn');
        if (checkoutBtn) checkoutBtn.textContent = t.checkoutBtn;

        // Checkout modal
        const checkoutTitle = document.querySelector('.checkout-box h3');
        if (checkoutTitle) checkoutTitle.textContent = t.checkoutTitle;
        const checkoutInputs = ['c-fname','c-lname','c-email','c-phone','c-addr'];
        const checkoutPlaceholders = [t.fnameHolder, t.lnameHolder, t.emailHolder, t.phoneHolder, t.addrHolder];
        checkoutInputs.forEach((id, i) => {
            const el = document.getElementById(id);
            if (el) el.placeholder = checkoutPlaceholders[i];
        });
        const cancelCheckoutBtn = document.querySelector('.btn-cancel[onclick="closeCheckout()"]');
        if (cancelCheckoutBtn) cancelCheckoutBtn.textContent = t.cancelBtn;
        const confirmCheckoutBtn = document.querySelector('.btn-confirm');
        if (confirmCheckoutBtn) confirmCheckoutBtn.textContent = t.confirmBtn;

        // Modals
        const setupTitle = document.querySelector('#admin-setup-modal h2');
        if (setupTitle) setupTitle.textContent = t.adminSetupTitle;
        const setupEmail = document.getElementById('setup-email');
        if (setupEmail) setupEmail.placeholder = t.emailAdmin;
        const setupPwd = document.getElementById('setup-pwd');
        if (setupPwd) setupPwd.placeholder = t.pwdHolder;
        const setupPwdC = document.getElementById('setup-pwd-confirm');
        if (setupPwdC) setupPwdC.placeholder = t.pwdConfirmHolder;
        const setupCreateBtn = document.querySelector('#admin-setup-modal .login-btn');
        if (setupCreateBtn) setupCreateBtn.textContent = t.createAccount;
        const setupBack = document.querySelector('#admin-setup-modal .back-link');
        if (setupBack) setupBack.textContent = t.backLogin;

        const loginTitle = document.querySelector('#admin-login h2');
        if (loginTitle) loginTitle.textContent = t.adminLoginTitle;
        const adminEmail = document.getElementById('admin-email');
        if (adminEmail) adminEmail.placeholder = t.emailIdHolder;
        const adminPwdIn = document.getElementById('admin-pwd');
        if (adminPwdIn) adminPwdIn.placeholder = t.pwdLoginHolder;
        const rememberLabel = document.querySelector('#admin-login label');
        if (rememberLabel) { const cb = rememberLabel.querySelector('input'); rememberLabel.innerHTML = ''; if(cb) rememberLabel.appendChild(cb); rememberLabel.append(' ' + t.rememberMe); }
        const forgotLink = document.querySelector('.forgot-link');
        if (forgotLink) forgotLink.textContent = t.forgotPwd;
        const createLinkEl = document.querySelector('.create-link');
        if (createLinkEl) createLinkEl.textContent = t.createLink;
        const connectBtnEl = document.querySelector('#admin-login .login-btn');
        if (connectBtnEl) connectBtnEl.textContent = t.connectBtn;
        const loginErrorEl = document.getElementById('login-error');
        if (loginErrorEl) loginErrorEl.textContent = t.loginError;

        const resetTitleEl = document.querySelector('#forgot-modal h2');
        if (resetTitleEl) resetTitleEl.textContent = t.resetTitle;
        const forgotEmail = document.getElementById('forgot-email');
        if (forgotEmail) forgotEmail.placeholder = t.emailAdminReset;
        const forgotNewPwd = document.getElementById('forgot-new-pwd');
        if (forgotNewPwd) forgotNewPwd.placeholder = t.newPwdHolder;
        const forgotConfirm = document.getElementById('forgot-confirm-pwd');
        if (forgotConfirm) forgotConfirm.placeholder = t.confirmPwdHolder;
        const resetBtnEl = document.querySelector('#forgot-modal .login-btn');
        if (resetBtnEl) resetBtnEl.textContent = t.resetBtn;
        const forgotBack = document.querySelector('#forgot-modal .back-link');
        if (forgotBack) forgotBack.textContent = t.backLogin;

        // Re-render dynamic content with new lang
        renderCartUI();
        renderProducts(applyFilterAndSearch());
        if (adminLoggedIn) {
            // re-render admin interface with new lang
            const adminContainer = document.getElementById("page-admin");
            adminContainer.innerHTML = "";
            loadAdminInterface();
            renderAdminTables();
        }
    }

    function T(key, ...args) {
        const t = i18n[currentLang];
        if (typeof t[key] === 'function') return t[key](...args);
        return t[key] || i18n['fr'][key] || key;
    }

    // ========== DATA ==========
    let products = [
        { id: 1, name: "Smartphone Samsung A54", cat: "Électronique", price: 8500, stock: 15, emoji: "📱", badge: "hot", desc: "Écran 6.4\", 128GB", image: null },
        { id: 2, name: "Robe Ankara Femme", cat: "Mode", price: 1200, stock: 30, emoji: "👗", badge: "new", desc: "Tissu wax authentique", image: null },
        { id: 3, name: "Ventilateur de Table", cat: "Maison", price: 950, stock: 25, emoji: "🌀", badge: "", desc: "3 vitesses", image: null },
        { id: 4, name: "Crème Karité Pure", cat: "Beauté", price: 400, stock: 50, emoji: "🧴", badge: "new", desc: "100% naturel", image: null },
        { id: 5, name: "Écouteurs Bluetooth", cat: "Électronique", price: 3200, stock: 20, emoji: "🎧", badge: "sale", desc: "Réduction de bruit", image: null }
    ];
    let cart = [], orders = [], customers = [];
    let editingProductId = null, adminLoggedIn = false, currentImageData = null;
    let currentFilter = 'all', searchTerm = '';

    let shopConfig = {
        name: "KBmarketplace", address: "Banjul, Gambie", phone: "+220 7121858", contactEmail: "bambabadiane61@gmail.com",
        whatsapp: "", facebook: "", tiktok: "",
        whatsappEnabled: true, facebookEnabled: true, tiktokEnabled: true,
        paymentMethods: [{ name: "Wave", number: "2207121858" }],
        marquee: { text: "✨ Livraison gratuite ✨ | -20% sur la première commande | Paiement sécurisé", image: "", enabled: true }
    };
    let adminCreds = null;

    // ========== SESSION ==========
    function loadSession() {
        const savedAdmin = localStorage.getItem("kb_admin_creds");
        if (savedAdmin) adminCreds = JSON.parse(savedAdmin);
        const remember = localStorage.getItem("kb_admin_remember") === "true";
        const logged = localStorage.getItem("kb_admin_logged_in") === "true";
        if (remember && logged && adminCreds) {
            adminLoggedIn = true;
            // Show admin button in navbar for returning admin session
            const adminBtn = document.getElementById("admin-nav-btn");
            if (adminBtn) adminBtn.style.display = "";
            const adminBtnMob = document.getElementById("admin-nav-btn-mobile");
            if (adminBtnMob) adminBtnMob.style.display = "";
            if (document.getElementById("page-admin").style.display !== "none") {
                loadAdminInterface();
                renderAdminTables();
            }
        } else {
            adminLoggedIn = false;
            localStorage.removeItem("kb_admin_logged_in");
        }
    }

    function saveSession(remember) {
        if (remember) {
            localStorage.setItem("kb_admin_remember", "true");
            localStorage.setItem("kb_admin_logged_in", "true");
        } else {
            localStorage.setItem("kb_admin_remember", "false");
            localStorage.setItem("kb_admin_logged_in", "true");
        }
    }

    function clearSession() {
        localStorage.removeItem("kb_admin_logged_in");
        localStorage.removeItem("kb_admin_remember");
        adminLoggedIn = false;
    }

    // ========== CONFIGURATION ==========
    function loadConfig() {
        const savedShop = localStorage.getItem("kb_shop_config");
        if (savedShop) {
            const p = JSON.parse(savedShop);
            shopConfig = { ...shopConfig, ...p, paymentMethods: p.paymentMethods || [], marquee: { ...shopConfig.marquee, ...(p.marquee || {}) }, tiktok: p.tiktok || "",
                whatsappEnabled: p.whatsappEnabled !== undefined ? p.whatsappEnabled : true,
                facebookEnabled: p.facebookEnabled !== undefined ? p.facebookEnabled : true,
                tiktokEnabled: p.tiktokEnabled !== undefined ? p.tiktokEnabled : true
            };
        }
        updateFooterSocial();
        updateMarquee();
    }

    function saveShopSettings() {
        shopConfig.name = document.getElementById("shop-name")?.value || shopConfig.name;
        shopConfig.address = document.getElementById("shop-address")?.value || shopConfig.address;
        shopConfig.phone = document.getElementById("shop-phone")?.value || shopConfig.phone;
        shopConfig.contactEmail = document.getElementById("shop-contact-email")?.value || shopConfig.contactEmail;
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        updateFooterSocial();
        showToast(T('shopSaved'));
    }

    function saveMarqueeSettings() {
        shopConfig.marquee.text = document.getElementById("marquee-text-input")?.value || "";
        shopConfig.marquee.image = document.getElementById("marquee-image-url")?.value || "";
        shopConfig.marquee.enabled = document.getElementById("marquee-enabled")?.checked || false;
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        updateMarquee();
        showToast(T('marqueeSaved'));
    }

    function updateMarquee() {
        const banner = document.getElementById("marquee-banner");
        const content = document.getElementById("marquee-text");
        if (!banner || !content) return;
        if (shopConfig.marquee.enabled && shopConfig.marquee.text) {
            banner.style.display = "block";
            let imgHtml = shopConfig.marquee.image ? `<img src="${shopConfig.marquee.image}" onerror="this.style.display='none'" alt="">` : "";
            const fullText = `${imgHtml} ${shopConfig.marquee.text}`;
            content.innerHTML = `<span>${fullText}</span><span>${fullText}</span><span>${fullText}</span>`;
        } else {
            banner.style.display = "none";
        }
    }

    function updateFooterSocial() {
        const container = document.getElementById("social-links-container");
        let html = "";
        if (shopConfig.whatsapp && shopConfig.whatsappEnabled) html += `<a href="${shopConfig.whatsapp}" target="_blank">💬 WhatsApp</a>`;
        if (shopConfig.facebook && shopConfig.facebookEnabled) html += `<a href="${shopConfig.facebook}" target="_blank">📘 Facebook</a>`;
        if (shopConfig.tiktok && shopConfig.tiktokEnabled) html += `<a href="${shopConfig.tiktok}" target="_blank">🎵 TikTok</a>`;
        container.innerHTML = html || `<span style='color:var(--muted);font-size:0.85rem'>${T('followUs')}</span>`;
        const infoDiv = document.getElementById("shop-info-footer");
        if (infoDiv) infoDiv.innerHTML = `${shopConfig.address} &nbsp;|&nbsp; 📞 ${shopConfig.phone} &nbsp;|&nbsp; 📧 ${shopConfig.contactEmail}`;
        // Update floating social bar
        const floatBar = document.getElementById("floating-social");
        if (floatBar) {
            let fhtml = "";
            if (shopConfig.whatsapp && shopConfig.whatsappEnabled) fhtml += `<a href="${shopConfig.whatsapp}" target="_blank" class="float-wa" title="WhatsApp">💬</a>`;
            if (shopConfig.facebook && shopConfig.facebookEnabled) fhtml += `<a href="${shopConfig.facebook}" target="_blank" class="float-fb" title="Facebook">📘</a>`;
            if (shopConfig.tiktok && shopConfig.tiktokEnabled) fhtml += `<a href="${shopConfig.tiktok}" target="_blank" class="float-tt" title="TikTok">🎵</a>`;
            floatBar.innerHTML = fhtml;
        }
        // Update social preview bar in admin if open
        renderSocialPreview();
    }

    function renderSocialPreview() {
        const bar = document.getElementById("social-admin-preview");
        if (!bar) return;
        const links = document.getElementById("social-preview-links-inner");
        if (!links) return;
        let html = "";
        if (shopConfig.whatsapp) html += `<a href="${shopConfig.whatsapp}" target="_blank" class="social-pill wa-pill">💬 WhatsApp</a>`;
        if (shopConfig.facebook) html += `<a href="${shopConfig.facebook}" target="_blank" class="social-pill fb-pill">📘 Facebook</a>`;
        if (shopConfig.tiktok) html += `<a href="${shopConfig.tiktok}" target="_blank" class="social-pill tt-pill">🎵 TikTok</a>`;
        links.innerHTML = html || `<span class="no-social-msg">Aucun réseau configuré</span>`;
        // Update status dots
        updateSocialDot("wa-dot", shopConfig.whatsapp);
        updateSocialDot("fb-dot", shopConfig.facebook);
        updateSocialDot("tt-dot", shopConfig.tiktok);
    }
    function updateSocialDot(id, val) {
        const dot = document.getElementById(id);
        if (dot) dot.className = "social-status-dot" + (val ? " connected" : "");
    }
    function saveSocial(platform) {
        const input = document.getElementById(`social-input-${platform}`);
        if (!input) return;
        const raw = input.value.trim();
        // Auto-format helpers
        let url = raw;
        if (platform === "whatsapp" && raw) {
            const num = raw.replace(/\D/g, "");
            url = num ? `https://wa.me/${num}` : raw;
            if (raw.startsWith("http")) url = raw;
        }
        if (platform === "facebook" && raw && !raw.startsWith("http")) {
            url = `https://facebook.com/${raw}`;
        }
        if (platform === "tiktok" && raw && !raw.startsWith("http")) {
            url = `https://tiktok.com/@${raw.replace(/^@/,"")}`;
        }
        if (platform === "whatsapp") shopConfig.whatsapp = url;
        if (platform === "facebook") shopConfig.facebook = url;
        if (platform === "tiktok") shopConfig.tiktok = url;
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        input.value = url;
        // Update dot immediately
        const dotMap = { whatsapp: "wa-dot", facebook: "fb-dot", tiktok: "tt-dot" };
        updateSocialDot(dotMap[platform], url);
        updateFooterSocial();
        showToast(url ? `✓ ${platform.charAt(0).toUpperCase()+platform.slice(1)} connecté !` : `${platform} déconnecté`);
    }
    function toggleSocialEnabled(platform) {
        const key = platform + "Enabled";
        shopConfig[key] = !shopConfig[key];
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        updateFooterSocial();
        // Update toggle button appearance
        const btn = document.getElementById(`social-toggle-${platform}`);
        if (btn) {
            btn.textContent = shopConfig[key] ? "👁️ Visible" : "🙈 Masqué";
            btn.style.background = shopConfig[key] ? "rgba(34,221,59,0.15)" : "rgba(255,255,255,0.05)";
            btn.style.color = shopConfig[key] ? "var(--accent)" : "var(--muted)";
        }
        showToast(shopConfig[key] ? `${platform} affiché sur le site` : `${platform} masqué du site`);
    }
    function testSocial(platform) {
        let url = "";
        if (platform === "whatsapp") url = shopConfig.whatsapp;
        if (platform === "facebook") url = shopConfig.facebook;
        if (platform === "tiktok") url = shopConfig.tiktok;
        if (url) window.open(url, "_blank");
        else showToast("Aucun lien configuré", "error");
    }
    function clearSocial(platform) {
        if (platform === "whatsapp") shopConfig.whatsapp = "";
        if (platform === "facebook") shopConfig.facebook = "";
        if (platform === "tiktok") shopConfig.tiktok = "";
        const input = document.getElementById(`social-input-${platform}`);
        if (input) input.value = "";
        const dotMap = { whatsapp: "wa-dot", facebook: "fb-dot", tiktok: "tt-dot" };
        updateSocialDot(dotMap[platform], "");
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        updateFooterSocial();
        showToast("Lien supprimé");
    }
    function showSetupFromLogin() {
        document.getElementById("admin-login").style.display = "none";
        document.getElementById("admin-setup-modal").style.display = "flex";
    }
    function closeSetupModal() {
        document.getElementById("admin-setup-modal").style.display = "none";
        document.getElementById("admin-login").style.display = "flex";
    }
    function createAdminAccount() {
        const email = document.getElementById("setup-email").value.trim();
        const pwd = document.getElementById("setup-pwd").value;
        const confirm = document.getElementById("setup-pwd-confirm").value;
        if (!email || pwd.length < 4 || pwd !== confirm) {
            document.getElementById("setup-error").innerText = T('setupError');
            return;
        }
        adminCreds = { email, password: pwd };
        localStorage.setItem("kb_admin_creds", JSON.stringify(adminCreds));
        document.getElementById("admin-setup-modal").style.display = "none";
        showToast(T('accountCreated'));
        document.getElementById("admin-login").style.display = "flex";
    }
    function checkAdminPwd() {
        if (!adminCreds) {
            const saved = localStorage.getItem("kb_admin_creds");
            if (saved) adminCreds = JSON.parse(saved);
            else { showToast(T('noAccount'), "error"); return; }
        }
        const email = document.getElementById("admin-email").value;
        const pwd = document.getElementById("admin-pwd").value;
        const remember = document.getElementById("remember-checkbox").checked;
        if (email === adminCreds.email && pwd === adminCreds.password) {
            adminLoggedIn = true;
            saveSession(remember);
            document.getElementById("admin-login").style.display = "none";
            // Reveal admin button in navbar
            const adminBtn = document.getElementById("admin-nav-btn");
            if (adminBtn) adminBtn.style.display = "";
            const adminBtnMob = document.getElementById("admin-nav-btn-mobile");
            if (adminBtnMob) adminBtnMob.style.display = "";
            loadAdminInterface();
            showPage("admin");
            renderAdminTables();
        } else {
            document.getElementById("login-error").style.display = "block";
        }
    }
    function showForgotPassword() {
        document.getElementById("admin-login").style.display = "none";
        document.getElementById("forgot-modal").style.display = "flex";
    }
    function closeForgotModal() {
        document.getElementById("forgot-modal").style.display = "none";
        document.getElementById("admin-login").style.display = "flex";
    }
    function resetAdminPassword() {
        const email = document.getElementById("forgot-email").value.trim();
        const newPwd = document.getElementById("forgot-new-pwd").value;
        const confirm = document.getElementById("forgot-confirm-pwd").value;
        if (!adminCreds) {
            const saved = localStorage.getItem("kb_admin_creds");
            if (saved) adminCreds = JSON.parse(saved);
            else { showToast("Aucun compte", "error"); return; }
        }
        if (email !== adminCreds.email) { document.getElementById("forgot-error").innerText = "Email incorrect"; return; }
        if (newPwd.length < 4) { document.getElementById("forgot-error").innerText = "Min 4 caractères"; return; }
        if (newPwd !== confirm) { document.getElementById("forgot-error").innerText = "Les mots de passe diffèrent"; return; }
        adminCreds.password = newPwd;
        localStorage.setItem("kb_admin_creds", JSON.stringify(adminCreds));
        showToast("Mot de passe réinitialisé");
        closeForgotModal();
        if (adminLoggedIn) logoutAdmin();
    }
    function logoutAdmin() {
        adminLoggedIn = false;
        clearSession();
        const adminContainer = document.getElementById("page-admin");
        if (adminContainer) adminContainer.innerHTML = "";
        document.getElementById("page-admin").style.display = "none";
        // Hide admin button again for visitors
        const adminBtn = document.getElementById("admin-nav-btn");
        if (adminBtn) { adminBtn.style.display = "none"; adminBtn.classList.remove("active"); }
        const adminBtnMob = document.getElementById("admin-nav-btn-mobile");
        if (adminBtnMob) adminBtnMob.style.display = "none";
        showPage("client");
        showToast("Déconnecté");
    }
    function showPage(page) {
        if (page === "client") {
            document.getElementById("page-client").style.display = "block";
            document.getElementById("page-admin").style.display = "none";
            document.querySelector(".nav-tab[data-page='client']").classList.add("active");
            const adminBtn = document.getElementById("admin-nav-btn");
            if (adminBtn) adminBtn.classList.remove("active");
        } else if (page === "admin") {
            if (!adminLoggedIn) {
                const exists = localStorage.getItem("kb_admin_creds");
                if (!exists) document.getElementById("admin-setup-modal").style.display = "flex";
                else document.getElementById("admin-login").style.display = "flex";
                return;
            }
            document.getElementById("page-client").style.display = "none";
            document.getElementById("page-admin").style.display = "block";
            const adminBtn = document.getElementById("admin-nav-btn");
            if (adminBtn) { adminBtn.style.display = ""; adminBtn.classList.add("active"); }
            const adminBtnMob = document.getElementById("admin-nav-btn-mobile");
            if (adminBtnMob) adminBtnMob.style.display = "";
            document.querySelector(".nav-tab[data-page='client']").classList.remove("active");
            renderAdminTables();
        }
    }

    // ── Secret admin access ──────────────────
    // Method 1: triple-click on logo
    let logoClickCount = 0, logoClickTimer = null;
    document.querySelector(".custom-logo").addEventListener("click", function(e) {
        logoClickCount++;
        clearTimeout(logoClickTimer);
        logoClickTimer = setTimeout(() => { logoClickCount = 0; }, 600);
        if (logoClickCount >= 3) {
            logoClickCount = 0;
            showPage("admin");
        }
    });
    // Method 2: ?admin or #admin in URL
    if (location.search.includes("admin") || location.hash === "#admin") {
        showPage("admin");
    }

    // ========== ADMIN INTERFACE ==========
    function loadAdminInterface() {
        const adminContainer = document.getElementById("page-admin");
        if (adminContainer.innerHTML.trim() !== "") return;
        adminContainer.innerHTML = `
            <div class="admin-layout">
                <div class="admin-sidebar">
                    <div class="admin-sidebar-title">${T('adminMenu')}</div>
                    <div class="admin-menu-item active" data-admin="dashboard">${T('adminDash')}</div>
                    <div class="admin-menu-item" data-admin="products-admin">${T('adminProd')}</div>
                    <div class="admin-menu-item" data-admin="orders">${T('adminOrders')}</div>
                    <div class="admin-menu-item" data-admin="customers">${T('adminClients')}</div>
                    <div class="admin-menu-item" data-admin="settings">${T('adminSettings')}</div>
                    <div class="admin-menu-item" onclick="logoutAdmin()">${T('adminLogout')}</div>
                </div>
                <div class="admin-content">
                    <div class="admin-section active" id="admin-dashboard">
                        <div class="stats-grid" id="admin-stats"></div>
                        <div class="admin-card">
                            <h3>${T('recentOrdersTitle')}</h3>
                            <table><thead><tr><th>${T('colId')}</th><th>${T('colClient')}</th><th>${T('colTotal')}</th><th>${T('colStatus')}</th></tr></thead><tbody id="recent-orders-table"></tbody></table>
                        </div>
                    </div>

                    <div class="admin-section" id="admin-products-admin">
                        <button class="btn-primary" onclick="showAddProductForm()">${T('addProductBtn')}</button>
                        <div id="add-product-form-card" style="display:none;margin-top:1.5rem" class="admin-card">
                            <h3>${T('productFormTitle')}</h3>
                            <div style="display:grid;grid-template-columns:1fr 1fr;gap:1rem">
                                <input id="p-name" class="admin-input" placeholder="${T('pNameHolder')}">
                                <select id="p-cat" class="admin-select"><option>Électronique</option><option>Mode</option><option>Maison</option><option>Beauté</option><option>Alimentation</option></select>
                                <input id="p-price" class="admin-input" placeholder="${T('pPriceHolder')}">
                                <input id="p-stock" class="admin-input" placeholder="${T('pStockHolder')}">
                                <input id="p-emoji" class="admin-input" placeholder="${T('pEmojiHolder')}">
                                <select id="p-badge" class="admin-select"><option value="">${T('pBadgeNone')}</option><option value="new">${T('pBadgeNew')}</option><option value="sale">${T('pBadgeSale')}</option><option value="hot">${T('pBadgeHot')}</option></select>
                                <div class="img-upload-zone" id="upload-zone" ondragover="handleDragOver(event)" ondragleave="handleDragLeave(event)" ondrop="handleDrop(event)" style="grid-column:1/-1">
                                    <input type="file" id="p-img-file" accept="image/*" onchange="handleFileSelect(event)" style="display:none">
                                    <div onclick="document.getElementById('p-img-file').click()">${T('uploadZone')}</div>
                                </div>
                                <div id="img-preview-wrap" style="display:none;align-items:center;gap:10px;grid-column:1/-1">
                                    <img id="img-preview-thumb" width="60" style="border-radius:10px">
                                    <button onclick="removeImage()" class="btn-danger">${T('removeImgBtn')}</button>
                                </div>
                                <input id="p-img-url" class="admin-input" placeholder="${T('pImgUrlHolder')}" oninput="handleUrlInput(this.value)" style="grid-column:1/-1">
                                <textarea id="p-desc" class="admin-textarea" placeholder="${T('pDescHolder')}" rows="3" style="grid-column:1/-1"></textarea>
                                <div style="grid-column:1/-1;display:flex;gap:10px">
                                    <button onclick="cancelProductForm()" class="btn-cancel" style="flex:1;padding:10px;border-radius:50px;cursor:pointer">${T('cancelFormBtn')}</button>
                                    <button onclick="saveProduct()" class="btn-primary" style="flex:2">${T('saveFormBtn')}</button>
                                </div>
                            </div>
                        </div>
                        <div class="admin-card" style="margin-top:1.5rem">
                            <h3>${T('listProductsTitle')}</h3>
                            <table><thead><tr><th>${T('colProduct')}</th><th>${T('colTotal')}</th><th>${T('colStock')}</th><th>${T('colActions')}</th></tr></thead><tbody id="admin-products-table"></tbody></table>
                        </div>
                    </div>

                    <div class="admin-section" id="admin-orders">
                        <div class="admin-card">
                            <h3>${T('allOrdersTitle')}</h3>
                            <table><thead><tr><th>${T('colId')}</th><th>${T('colClient')}</th><th>${T('colTotal')}</th><th>${T('colStatus')}</th></tr></thead><tbody id="all-orders-table"></tbody></table>
                        </div>
                    </div>

                    <div class="admin-section" id="admin-customers">
                        <div class="admin-card">
                            <h3>${T('clientsTitle')}</h3>
                            <table><thead><tr><th>${T('colClient')}</th><th>Email</th><th>${T('dashOrders')}</th><th>${T('colTotal')}</th></tr></thead><tbody id="customers-table"></tbody></table>
                        </div>
                    </div>

                    <div class="admin-section" id="admin-settings">
                        <div class="admin-card">
                            <h3>📲 Réseaux sociaux</h3>
                            <div class="social-connect-grid">
                                <!-- WhatsApp -->
                                <div class="social-platform-card wa">
                                    <div class="social-card-header">
                                        <div class="social-icon-wrap">💬</div>
                                        <div>
                                            <div class="social-card-label">WhatsApp</div>
                                            <div class="social-card-sub">Numéro ou lien wa.me</div>
                                        </div>
                                        <div class="social-status-dot${shopConfig.whatsapp ? ' connected' : ''}" id="wa-dot"></div>
                                    </div>
                                    <div class="social-input-row">
                                        <input id="social-input-whatsapp" class="admin-input" placeholder="+220 7121858 ou wa.me/..." value="${shopConfig.whatsapp.replace(/"/g,'&quot;')}">
                                    </div>
                                    <div class="social-action-btns">
                                        <button class="btn-social-save" onclick="saveSocial('whatsapp')">💾 Connecter</button>
                                        <button class="btn-social-test" onclick="testSocial('whatsapp')">🔗 Tester</button>
                                        <button id="social-toggle-whatsapp" onclick="toggleSocialEnabled('whatsapp')" class="btn-social-test" style="background:${shopConfig.whatsappEnabled ? 'rgba(34,221,59,0.15)' : 'rgba(255,255,255,0.05)'};color:${shopConfig.whatsappEnabled ? 'var(--accent)' : 'var(--muted)'}">${shopConfig.whatsappEnabled ? '👁️ Visible' : '🙈 Masqué'}</button>
                                        <button class="btn-social-clear" onclick="clearSocial('whatsapp')">✕</button>
                                    </div>
                                </div>
                                <!-- Facebook -->
                                <div class="social-platform-card fb">
                                    <div class="social-card-header">
                                        <div class="social-icon-wrap">📘</div>
                                        <div>
                                            <div class="social-card-label">Facebook</div>
                                            <div class="social-card-sub">Nom de page ou URL complète</div>
                                        </div>
                                        <div class="social-status-dot${shopConfig.facebook ? ' connected' : ''}" id="fb-dot"></div>
                                    </div>
                                    <div class="social-input-row">
                                        <input id="social-input-facebook" class="admin-input" placeholder="nom-page ou facebook.com/..." value="${shopConfig.facebook.replace(/"/g,'&quot;')}">
                                    </div>
                                    <div class="social-action-btns">
                                        <button class="btn-social-save" onclick="saveSocial('facebook')">💾 Connecter</button>
                                        <button class="btn-social-test" onclick="testSocial('facebook')">🔗 Tester</button>
                                        <button id="social-toggle-facebook" onclick="toggleSocialEnabled('facebook')" class="btn-social-test" style="background:${shopConfig.facebookEnabled ? 'rgba(34,221,59,0.15)' : 'rgba(255,255,255,0.05)'};color:${shopConfig.facebookEnabled ? 'var(--accent)' : 'var(--muted)'}">${shopConfig.facebookEnabled ? '👁️ Visible' : '🙈 Masqué'}</button>
                                        <button class="btn-social-clear" onclick="clearSocial('facebook')">✕</button>
                                    </div>
                                </div>
                                <!-- TikTok -->
                                <div class="social-platform-card tt">
                                    <div class="social-card-header">
                                        <div class="social-icon-wrap">🎵</div>
                                        <div>
                                            <div class="social-card-label">TikTok</div>
                                            <div class="social-card-sub">@nomutilisateur ou URL</div>
                                        </div>
                                        <div class="social-status-dot${shopConfig.tiktok ? ' connected' : ''}" id="tt-dot"></div>
                                    </div>
                                    <div class="social-input-row">
                                        <input id="social-input-tiktok" class="admin-input" placeholder="@moncompte ou tiktok.com/@..." value="${shopConfig.tiktok ? shopConfig.tiktok.replace(/"/g,'&quot;') : ''}">
                                    </div>
                                    <div class="social-action-btns">
                                        <button class="btn-social-save" onclick="saveSocial('tiktok')">💾 Connecter</button>
                                        <button class="btn-social-test" onclick="testSocial('tiktok')">🔗 Tester</button>
                                        <button id="social-toggle-tiktok" onclick="toggleSocialEnabled('tiktok')" class="btn-social-test" style="background:${shopConfig.tiktokEnabled ? 'rgba(34,221,59,0.15)' : 'rgba(255,255,255,0.05)'};color:${shopConfig.tiktokEnabled ? 'var(--accent)' : 'var(--muted)'}">${shopConfig.tiktokEnabled ? '👁️ Visible' : '🙈 Masqué'}</button>
                                        <button class="btn-social-clear" onclick="clearSocial('tiktok')">✕</button>
                                    </div>
                                </div>
                            </div>
                            <!-- Preview bar -->
                            <div class="social-preview-bar" id="social-admin-preview">
                                <span class="social-preview-label">Aperçu :</span>
                                <div class="social-preview-links" id="social-preview-links-inner"></div>
                            </div>
                        </div>
                        <div class="admin-card">
                            <h3>${T('shopInfoTitle')}</h3>
                            <div style="display:grid;gap:0.8rem">
                                <input id="shop-name" class="admin-input" placeholder="${T('shopNameHolder')}" value="${shopConfig.name.replace(/"/g, '&quot;')}">
                                <input id="shop-address" class="admin-input" placeholder="${T('shopAddrHolder')}" value="${shopConfig.address.replace(/"/g, '&quot;')}">
                                <input id="shop-phone" class="admin-input" placeholder="${T('shopPhoneHolder')}" value="${shopConfig.phone}">
                                <input id="shop-contact-email" class="admin-input" placeholder="${T('shopEmailHolder')}" value="${shopConfig.contactEmail}">
                                <button onclick="saveShopSettings()" class="btn-primary">${T('saveBoutique')}</button>
                            </div>
                        </div>
                        <div class="admin-card">
                            <h3>${T('marqueeTitle')}</h3>
                            <div style="display:grid;gap:0.8rem">
                                <input type="text" id="marquee-text-input" class="admin-input" placeholder="${T('marqueeTextHolder')}" value="${shopConfig.marquee.text.replace(/"/g, '&quot;')}">
                                <input type="text" id="marquee-image-url" class="admin-input" placeholder="${T('marqueeImgHolder')}" value="${shopConfig.marquee.image}">
                                <label style="display:flex;align-items:center;gap:8px;cursor:pointer;color:var(--off-white)">
                                    <input type="checkbox" id="marquee-enabled" ${shopConfig.marquee.enabled ? 'checked' : ''}> ${T('marqueeEnable')}
                                </label>
                                <button onclick="saveMarqueeSettings()" class="btn-primary">${T('marqueeSave')}</button>
                            </div>
                        </div>
                        <div class="admin-card">
                            <h3>${T('paymentTitle')}</h3>
                            <div id="payment-methods-admin-list"></div>
                            <div style="display:flex;gap:0.6rem;margin-top:1rem;flex-wrap:wrap">
                                <input id="new-pm-name" class="admin-input" placeholder="${T('pmNameHolder')}" style="flex:1;min-width:120px">
                                <input id="new-pm-number" class="admin-input" placeholder="${T('pmNumberHolder')}" style="flex:1;min-width:120px">
                                <button onclick="addPaymentMethod()" class="btn-primary">${T('pmAdd')}</button>
                            </div>
                        </div>
                        <div class="admin-card">
                            <h3>${T('adminCredsTitle')}</h3>
                            <div style="display:grid;gap:0.8rem">
                                <input id="admin-email-settings" class="admin-input" placeholder="${T('adminEmailHolder')}" value="${adminCreds ? adminCreds.email : ''}">
                                <input id="admin-pwd-settings" class="admin-input" type="password" placeholder="${T('adminPwdHolder')}">
                                <button onclick="saveAdminCredentials()" class="btn-primary">${T('adminCredsUpdate')}</button>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        `;
        document.querySelectorAll(".admin-menu-item").forEach(menu => {
            if (menu.getAttribute("data-admin")) {
                menu.addEventListener("click", () => {
                    document.querySelectorAll(".admin-section").forEach(s => s.classList.remove("active"));
                    document.getElementById(`admin-${menu.getAttribute("data-admin")}`).classList.add("active");
                    document.querySelectorAll(".admin-menu-item").forEach(m => m.classList.remove("active"));
                    menu.classList.add("active");
                });
            }
        });
        renderPaymentMethodsAdmin();
        renderSocialPreview();
    }

    function renderPaymentMethodsAdmin() {
        const container = document.getElementById("payment-methods-admin-list");
        if (!container) return;
        container.innerHTML = "";
        (shopConfig.paymentMethods || []).forEach((pm, idx) => {
            const div = document.createElement("div");
            div.style.cssText = "display:flex;justify-content:space-between;align-items:center;background:rgba(255,255,255,0.04);border:1px solid rgba(255,255,255,0.07);padding:10px 16px;border-radius:12px;margin-bottom:8px";
            div.innerHTML = `<span style="color:var(--off-white)"><strong style="color:var(--accent)">${pm.name}</strong> : ${pm.number}</span><button onclick="removePaymentMethod(${idx})" class="btn-danger">🗑️</button>`;
            container.appendChild(div);
        });
        if (container.children.length === 0) container.innerHTML = `<div style='color:var(--muted);font-size:0.85rem'>${T('noProducts')} de paiement.</div>`;
    }

    function addPaymentMethod() {
        const name = document.getElementById("new-pm-name")?.value.trim();
        const number = document.getElementById("new-pm-number")?.value.trim();
        if (!name || !number) { showToast(T('pmRequired'), "error"); return; }
        shopConfig.paymentMethods.push({ name, number });
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        renderPaymentMethodsAdmin();
        document.getElementById("new-pm-name").value = ""; document.getElementById("new-pm-number").value = "";
        showToast(T('pmAdded'));
    }

    function removePaymentMethod(idx) {
        shopConfig.paymentMethods.splice(idx, 1);
        localStorage.setItem("kb_shop_config", JSON.stringify(shopConfig));
        renderPaymentMethodsAdmin();
        showToast(T('pmRemoved'));
    }

    function saveAdminCredentials() {
        const newEmail = document.getElementById("admin-email-settings")?.value.trim();
        const newPwd = document.getElementById("admin-pwd-settings")?.value;
        if (!newEmail) return showToast(T('emailRequired'), "error");
        if (newPwd && newPwd.length < 4) return showToast(T('pwdMinError'), "error");
        const updated = { email: newEmail, password: newPwd || (adminCreds ? adminCreds.password : "admin123") };
        localStorage.setItem("kb_admin_creds", JSON.stringify(updated));
        adminCreds = updated;
        if (adminLoggedIn) localStorage.setItem("kb_admin_logged_in", "true");
        showToast(T('credUpdated'));
    }

    // ========== PRODUITS & PANIER ==========
    function applyFilterAndSearch() {
        let f = [...products];
        if (currentFilter !== "all") f = f.filter(p => p.cat === currentFilter);
        if (searchTerm) f = f.filter(p => p.name.toLowerCase().includes(searchTerm));
        return f;
    }
    function filterProducts(cat, btn) {
        currentFilter = cat;
        document.querySelectorAll(".filter-btn").forEach(b => b.classList.remove("active"));
        btn.classList.add("active");
        renderProducts(applyFilterAndSearch());
    }
    function searchProducts(term) {
        searchTerm = term.toLowerCase();
        renderProducts(applyFilterAndSearch());
    }

    function getBadgeClass(badge) {
        if (badge === "new") return "badge-new";
        if (badge === "sale") return "badge-sale";
        if (badge === "hot") return "badge-hot";
        return "";
    }
    function getBadgeLabel(badge) {
        const t = i18n[currentLang];
        if (badge === "new") return t.badgeNew || "NOUVEAU";
        if (badge === "sale") return t.badgeSale || "PROMO";
        if (badge === "hot") return t.badgeHot || "🔥 TOP";
        return badge;
    }

    function renderProducts(prods) {
        const grid = document.getElementById("products-grid");
        if (!prods.length) {
            grid.innerHTML = `<div style='text-align:center;padding:4rem;color:var(--muted);grid-column:1/-1'>${T('noProductFound')}</div>`;
            return;
        }
        grid.innerHTML = prods.map(p => `
            <div class="product-card">
                <div class="product-img-wrap">
                    ${p.badge ? `<span class="product-badge ${getBadgeClass(p.badge)}">${getBadgeLabel(p.badge)}</span>` : ""}
                    <div class="product-img">${p.image ? `<img src="${p.image}" onerror="this.parentElement.innerHTML='<span style=font-size:4rem>${p.emoji || "📦"}</span>'">` : p.emoji || "📦"}</div>
                </div>
                <div class="product-info">
                    <div class="product-cat">${p.cat}</div>
                    <div class="product-name">${p.name}</div>
                    ${p.desc ? `<div class="product-desc">${p.desc}</div>` : ""}
                    <div class="product-footer">
                        <span class="product-price">${p.price.toLocaleString()} <span style="font-size:0.75rem;opacity:0.6">GMD</span></span>
                        <button class="add-cart-btn" onclick="addToCart(${p.id})">+</button>
                    </div>
                </div>
            </div>
        `).join("");
        document.getElementById("stat-products").innerText = products.length;
        document.getElementById("stat-clients").innerText = customers.length;
    }

    function addToCart(id) {
        const p = products.find(x => x.id === id);
        if (p) {
            let ex = cart.find(x => x.id === id);
            if (ex) ex.qty++;
            else cart.push({ ...p, qty: 1 });
            updateCartUI();
            showToast(T('addedToCart'));
        }
    }
    function updateCartUI() {
        const count = cart.reduce((s, x) => s + x.qty, 0);
        document.getElementById("cart-count").innerText = count;
        renderCartUI();
    }
    function renderCartUI() {
        const list = document.getElementById("cart-items-list");
        if (!cart.length) {
            list.innerHTML = `<div style='text-align:center;padding:3rem;color:var(--muted)'>${T('cartEmpty')}</div>`;
        } else {
            list.innerHTML = cart.map(i => `
                <div style="display:flex;gap:12px;margin-bottom:14px;padding-bottom:14px;border-bottom:1px solid rgba(255,255,255,0.06)">
                    <div style="width:56px;height:56px;background:var(--surface);border-radius:12px;display:flex;align-items:center;justify-content:center;font-size:1.6rem;flex-shrink:0;border:1px solid var(--border);overflow:hidden">
                        ${i.image ? `<img src="${i.image}" style="width:100%;height:100%;object-fit:cover">` : i.emoji}
                    </div>
                    <div style="flex:1;min-width:0">
                        <div style="font-weight:600;font-size:0.88rem;color:var(--white);white-space:nowrap;overflow:hidden;text-overflow:ellipsis">${i.name}</div>
                        <div style="font-family:'Space Mono',monospace;color:var(--accent);font-size:0.82rem;margin:2px 0">${i.price.toLocaleString()} GMD</div>
                        <div style="display:flex;align-items:center;gap:8px;margin-top:6px">
                            <button class="qty-minus" data-id="${i.id}" style="width:26px;height:26px;background:rgba(255,255,255,0.08);border:1px solid var(--border);border-radius:50%;cursor:pointer;color:var(--off-white)">-</button>
                            <span style="font-size:0.88rem;font-weight:600;min-width:16px;text-align:center">${i.qty}</span>
                            <button class="qty-plus" data-id="${i.id}" style="width:26px;height:26px;background:rgba(255,255,255,0.08);border:1px solid var(--border);border-radius:50%;cursor:pointer;color:var(--off-white)">+</button>
                        </div>
                    </div>
                    <button class="remove-item" data-id="${i.id}" style="background:none;border:none;color:var(--muted);cursor:pointer;font-size:1.1rem;align-self:start;padding:4px;transition:color 0.2s" onmouseover="this.style.color='#fb7185'" onmouseout="this.style.color='var(--muted)'">🗑</button>
                </div>
            `).join("");
            document.querySelectorAll(".qty-minus").forEach(btn => btn.addEventListener("click", () => changeQty(parseInt(btn.dataset.id), -1)));
            document.querySelectorAll(".qty-plus").forEach(btn => btn.addEventListener("click", () => changeQty(parseInt(btn.dataset.id), 1)));
            document.querySelectorAll(".remove-item").forEach(btn => btn.addEventListener("click", () => removeFromCart(parseInt(btn.dataset.id))));
        }
        const total = cart.reduce((s, x) => s + x.price * x.qty, 0);
        document.getElementById("cart-subtotal").textContent = total.toLocaleString() + " GMD";
        document.getElementById("cart-total-val").textContent = total.toLocaleString() + " GMD";
    }
    function changeQty(id, delta) {
        let item = cart.find(x => x.id === id);
        if (item) {
            item.qty += delta;
            if (item.qty <= 0) cart = cart.filter(x => x.id !== id);
            updateCartUI();
        }
    }
    function removeFromCart(id) {
        cart = cart.filter(x => x.id !== id);
        updateCartUI();
    }
    function openCart() {
        const overlay = document.getElementById("cart-overlay");
        const panel = document.getElementById("cart-panel");
        if (!panel.classList.contains("open")) {
            panel.classList.add("open");
            overlay.style.display = "block";
        }
    }
    function closeCart() {
        const overlay = document.getElementById("cart-overlay");
        const panel = document.getElementById("cart-panel");
        if (panel.classList.contains("open")) {
            panel.classList.remove("open");
            overlay.style.display = "none";
        }
    }
    function toggleCart() {
        const panel = document.getElementById("cart-panel");
        if (panel.classList.contains("open")) closeCart();
        else openCart();
    }
    document.addEventListener("click", function(event) {
        const panel = document.getElementById("cart-panel");
        const cartIcon = document.getElementById("cart-icon");
        const overlay = document.getElementById("cart-overlay");
        if (panel.classList.contains("open")) {
            if (!panel.contains(event.target) && event.target !== cartIcon && !cartIcon.contains(event.target) && event.target !== overlay) {
                closeCart();
            }
        }
    });
    document.getElementById("cart-overlay").addEventListener("click", closeCart);
    document.querySelector(".close-cart-btn").addEventListener("click", closeCart);
    document.getElementById("cart-icon").addEventListener("click", (e) => { e.stopPropagation(); toggleCart(); });
    document.querySelector(".checkout-btn").addEventListener("click", openCheckout);

    function openCheckout() {
        if (!cart.length) { showToast(T('cartEmptyMsg'), "error"); return;
        }
        closeCart();
        const total = cart.reduce((s, x) => s + x.price * x.qty, 0);
        document.getElementById("checkout-summary").innerText = T('articlesSummary', cart.length, total);
        const pmDiv = document.getElementById("payment-methods-list");
        let html = `<strong style='color:var(--off-white)'>${T('paymentLabel')}</strong><br>`;
        (shopConfig.paymentMethods || []).forEach(pm => { html += `<span style='color:var(--accent)'>✅</span> ${pm.name} : <strong>${pm.number}</strong><br>`; });
        pmDiv.innerHTML = html || T('noOrders');
        document.getElementById("checkout-modal").style.display = "flex";
    }
    function closeCheckout() { document.getElementById("checkout-modal").style.display = "none"; }
    function placeOrder() {
        const fname = document.getElementById("c-fname").value, lname = document.getElementById("c-lname").value,
            email = document.getElementById("c-email").value, phone = document.getElementById("c-phone").value,
            addr = document.getElementById("c-addr").value;
        if (!fname || !lname || !email || !phone || !addr) { showToast(T('fillFields'), "error"); return; }
        const order = {
            id: "KB" + Date.now().toString().slice(-6), client: fname + " " + lname,
            email, phone, addr, items: [...cart],
            total: cart.reduce((s, x) => s + x.price * x.qty, 0),
            status: "pending", date: new Date().toLocaleDateString()
        };
        orders.unshift(order);
        let existing = customers.find(c => c.email === email);
        if (existing) { existing.orders++; existing.total += order.total; }
        else customers.push({ name: order.client, email, phone, city: addr.split(",").pop(), orders: 1, total: order.total });
        cart = []; updateCartUI(); closeCheckout(); showToast(T('orderPlaced'));
        if (adminLoggedIn) renderAdminTables();
    }

    // ========== ADMIN TABLES ==========
    function renderAdminTables() {
        if (!adminLoggedIn) return;
        renderAdminStats(); renderAdminProducts(); renderAllOrders(); renderCustomers(); renderRecentOrders();
    }
    function renderAdminStats() {
        const rev = orders.reduce((s, o) => s + o.total, 0);
        const statsDiv = document.getElementById("admin-stats");
        if (statsDiv) statsDiv.innerHTML = `
            <div class="stat-card">📦 <strong>${T('dashProducts')}</strong><br><span style="font-size:1.5rem;font-family:'Space Mono',monospace;color:var(--accent)">${products.length}</span></div>
            <div class="stat-card">🛒 <strong>${T('dashOrders')}</strong><br><span style="font-size:1.5rem;font-family:'Space Mono',monospace;color:var(--gold)">${orders.length}</span></div>
            <div class="stat-card">💰 <strong>${T('dashRevenues')}</strong><br><span style="font-size:1.2rem;font-family:'Space Mono',monospace;color:var(--accent)">${rev.toLocaleString()} GMD</span></div>
            <div class="stat-card">👥 <strong>${T('dashClients')}</strong><br><span style="font-size:1.5rem;font-family:'Space Mono',monospace;color:var(--gold)">${customers.length}</span></div>
        `;
    }
    function renderAdminProducts() {
        const tbody = document.getElementById("admin-products-table");
        if (tbody) tbody.innerHTML = products.map(p => `
            <tr>
                <td><div style="display:flex;align-items:center;gap:10px">
                    <div style="width:36px;height:36px;background:var(--surface2);border-radius:8px;display:flex;align-items:center;justify-content:center;font-size:1.2rem;border:1px solid var(--border);overflow:hidden">
                        ${p.image ? `<img src="${p.image}" style="width:100%;height:100%;object-fit:cover">` : p.emoji}
                    </div>
                    ${p.name}
                </div></td>
                <td style="font-family:'Space Mono',monospace;color:var(--accent)">${p.price.toLocaleString()} GMD</td>
                <td>${p.stock}</td>
                <td style="display:flex;gap:6px;padding:8px 14px">
                    <button onclick="editProduct(${p.id})" class="btn-edit">${T('editBtn')}</button>
                    <button onclick="deleteProduct(${p.id})" class="btn-danger">🗑️</button>
                </td>
            </tr>
        `).join("") || `<tr><td colspan='4' style='color:var(--muted);text-align:center;padding:2rem'>${T('noProducts')}</td></tr>`;
    }
    function renderAllOrders() {
        const t = document.getElementById("all-orders-table");
        if (t) t.innerHTML = orders.map(o => `
            <tr>
                <td style="font-family:'Space Mono',monospace;color:var(--accent)">#${o.id}</td>
                <td>${o.client}</td>
                <td style="font-family:'Space Mono',monospace">${o.total.toLocaleString()} GMD</td>
                <td><select onchange="updateOrderStatus('${o.id}',this.value)" style="padding:6px 10px;border-radius:40px;border:1px solid var(--border);background:var(--surface2);color:var(--off-white);font-family:'Outfit',sans-serif">
                    <option ${o.status==="pending"?"selected":""}>pending</option>
                    <option ${o.status==="confirmed"?"selected":""}>confirmed</option>
                    <option ${o.status==="delivered"?"selected":""}>delivered</option>
                </select></td>
            </tr>
        `).join("") || `<tr><td colspan='4' style='color:var(--muted);text-align:center;padding:2rem'>${T('noOrders')}</td></tr>`;
    }
    function renderCustomers() {
        const t = document.getElementById("customers-table");
        if (t) t.innerHTML = customers.map(c => `<tr><td>${c.name}</td><td style="color:var(--muted)">${c.email}</td><td>${c.orders}</td><td style="font-family:'Space Mono',monospace;color:var(--accent)">${c.total.toLocaleString()} GMD</td></tr>`).join("") || `<tr><td colspan='4' style='color:var(--muted);text-align:center;padding:2rem'>${T('noClients')}</td></tr>`;
    }
    function renderRecentOrders() {
        const t = document.getElementById("recent-orders-table");
        if (t) t.innerHTML = orders.slice(0,5).map(o => `<tr><td style="font-family:'Space Mono',monospace;color:var(--accent)">#${o.id}</td><td>${o.client}</td><td style="font-family:'Space Mono',monospace">${o.total.toLocaleString()} GMD</td><td><span style="background:rgba(34,221,59,0.1);color:var(--accent);padding:4px 12px;border-radius:30px;font-size:0.75rem">${o.status}</span></td></tr>`).join("") || `<tr><td colspan='4' style='color:var(--muted);text-align:center;padding:2rem'>${T('noOrders')}</td></tr>`;
    }
    function updateOrderStatus(id, st) {
        const o = orders.find(x => x.id === id);
        if (o) o.status = st;
        showToast(T('statusUpdated'));
        renderAdminTables();
    }

    // ========== PRODUCT MANAGEMENT ==========
    function showAddProductForm() {
        editingProductId = null; currentImageData = null; removeImage();
        document.getElementById("add-product-form-card").style.display = "block";
    }
    function editProduct(id) {
        const p = products.find(x => x.id === id);
        if (p) {
            editingProductId = id;
            document.getElementById("p-name").value = p.name;
            document.getElementById("p-cat").value = p.cat;
            document.getElementById("p-price").value = p.price;
            document.getElementById("p-stock").value = p.stock;
            document.getElementById("p-emoji").value = p.emoji;
            document.getElementById("p-desc").value = p.desc || "";
            document.getElementById("p-badge").value = p.badge || "";
            currentImageData = p.image;
            if (p.image) showImagePreview(p.image);
            document.getElementById("add-product-form-card").style.display = "block";
        }
    }
    function saveProduct() {
        const name = document.getElementById("p-name").value, cat = document.getElementById("p-cat").value,
            price = parseInt(document.getElementById("p-price").value), stock = parseInt(document.getElementById("p-stock").value),
            emoji = document.getElementById("p-emoji").value || "📦", desc = document.getElementById("p-desc").value,
            badge = document.getElementById("p-badge").value;
        if (!name || !price) return showToast(T('nameRequired'), "error");
        const image = currentImageData || null;
        if (editingProductId) {
            const p = products.find(x => x.id === editingProductId);
            Object.assign(p, { name, cat, price, stock, emoji, desc, badge, image });
        } else {
            products.push({ id: Date.now(), name, cat, price, stock, emoji, desc, badge, image });
        }
        cancelProductForm();
        renderProducts(applyFilterAndSearch());
        renderAdminProducts();
        showToast('⏳ Enregistrement...');
        saveProductsToCloud().then(ok => { if (ok) showToast(T('productSaved')); });
    }
    function deleteProduct(id) {
        if (confirm(T('deleteConfirm'))) {
            products = products.filter(x => x.id !== id);
            renderProducts(applyFilterAndSearch());
            renderAdminProducts();
            saveProductsToCloud().then(ok => { if (ok) showToast(T('productDeleted')); });
        }
    }
    function cancelProductForm() {
        document.getElementById("add-product-form-card").style.display = "none";
        editingProductId = null;
        removeImage();
    }

    // ========== IMAGE HANDLERS ==========
    function handleDragOver(e) { e.preventDefault(); document.getElementById("upload-zone")?.classList.add("dragover"); }
    function handleDragLeave(e) { document.getElementById("upload-zone")?.classList.remove("dragover"); }
    function handleDrop(e) { e.preventDefault(); const file = e.dataTransfer.files[0]; if (file && file.type.startsWith("image/")) processImageFile(file); }
    function handleFileSelect(e) { if (e.target.files[0]) processImageFile(e.target.files[0]); }
    function processImageFile(file) { if (file.size > 5*1024*1024) { showToast(T('maxSize'), "error"); return; } const reader = new FileReader(); reader.onload = (e) => { currentImageData = e.target.result; showImagePreview(e.target.result); }; reader.readAsDataURL(file); }
    function handleUrlInput(url) { if (url && url.match(/^https?:\/\/.+/)) { currentImageData = url; showImagePreview(url); } else if (!url) removeImage(); }
    function showImagePreview(src) { const wrap = document.getElementById("img-preview-wrap"); if (wrap) { wrap.style.display = "flex"; document.getElementById("img-preview-thumb").src = src; } }
    function removeImage() { currentImageData = null; const wrap = document.getElementById("img-preview-wrap"); if (wrap) wrap.style.display = "none"; if (document.getElementById("p-img-file")) document.getElementById("p-img-file").value = ""; if (document.getElementById("p-img-url")) document.getElementById("p-img-url").value = ""; }
    function scrollToProducts() { document.querySelector(".products-grid").scrollIntoView({ behavior: "smooth" }); }
    function showToast(msg) { const t = document.getElementById("toast"); t.innerText = msg; t.classList.add("show"); setTimeout(() => t.classList.remove("show"), 2500); }

    // ========== INIT ==========
    window.addEventListener("DOMContentLoaded", async () => {
        loadConfig();
        loadSession();
        await loadProductsFromCloud();
        renderProducts(applyFilterAndSearch());
        updateCartUI();
        document.querySelectorAll(".nav-tab[data-page]").forEach(t => t.addEventListener("click", () => showPage(t.getAttribute("data-page"))));
        document.querySelectorAll(".filter-btn").forEach(btn => { btn.addEventListener("click", () => filterProducts(btn.getAttribute("data-cat"), btn)); });
        document.getElementById("search-input")?.addEventListener("input", e => searchProducts(e.target.value));
    });

    // Expose globals
    window.saveSocial = saveSocial;
    window.testSocial = testSocial;
    window.clearSocial = clearSocial;
    window.toggleSocialEnabled = toggleSocialEnabled;

    // Mobile nav
    function toggleMobileNav() {
        const dd = document.getElementById("mobile-nav-dropdown");
        dd.style.display = dd.style.display === "flex" ? "none" : "flex";
    }
    function closeMobileNav() {
        document.getElementById("mobile-nav-dropdown").style.display = "none";
    }
    window.toggleMobileNav = toggleMobileNav;
    window.closeMobileNav = closeMobileNav;
    window.addToCart = addToCart;
    window.checkAdminPwd = checkAdminPwd;
    window.logoutAdmin = logoutAdmin;
    window.showAddProductForm = showAddProductForm;
    window.saveProduct = saveProduct;
    window.editProduct = editProduct;
    window.deleteProduct = deleteProduct;
    window.cancelProductForm = cancelProductForm;
    window.updateOrderStatus = updateOrderStatus;
    window.handleDrop = handleDrop;
    window.handleDragOver = handleDragOver;
    window.handleDragLeave = handleDragLeave;
    window.handleFileSelect = handleFileSelect;
    window.handleUrlInput = handleUrlInput;
    window.removeImage = removeImage;
    window.scrollToProducts = scrollToProducts;
    window.saveShopSettings = saveShopSettings;
    window.saveAdminCredentials = saveAdminCredentials;
    window.saveMarqueeSettings = saveMarqueeSettings;
    window.createAdminAccount = createAdminAccount;
    window.showForgotPassword = showForgotPassword;
    window.closeForgotModal = closeForgotModal;
    window.resetAdminPassword = resetAdminPassword;
    window.addPaymentMethod = addPaymentMethod;
    window.removePaymentMethod = removePaymentMethod;
    window.showSetupFromLogin = showSetupFromLogin;
    window.closeSetupModal = closeSetupModal;
    window.placeOrder = placeOrder;
    window.closeCheckout = closeCheckout;
    window.openCheckout = openCheckout;
</script>

<!-- ── PWA — MANIFEST + SERVICE WORKER ──────────────────── -->
<script>
(function() {
    // ── 1. Inline Manifest (blob URL — no server needed) ──
    const manifest = {
        name: "KBmarketplace",
        short_name: "KBmarket",
        description: "Your Favour Design — Mode & Livraison Gambie",
        start_url: "./",
        display: "standalone",
        orientation: "portrait-primary",
        background_color: "#06080f",
        theme_color: "#06080f",
        lang: "fr",
        categories: ["shopping", "lifestyle"],
        icons: [
            {
                src: "data:image/svg+xml," + encodeURIComponent(`<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 512 512'><rect width='512' height='512' rx='100' fill='%2306080f'/><rect x='28' y='28' width='456' height='456' rx='80' fill='%230d1220'/><rect x='60' y='60' width='392' height='392' rx='60' fill='%2322dd3b' opacity='.1'/><text x='256' y='320' font-family='monospace' font-size='220' font-weight='700' fill='%2322dd3b' text-anchor='middle'>KB</text></svg>`),
                sizes: "512x512", type: "image/svg+xml", purpose: "any maskable"
            },
            {
                src: "data:image/svg+xml," + encodeURIComponent(`<svg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 192 192'><rect width='192' height='192' rx='40' fill='%2306080f'/><text x='96' y='130' font-family='monospace' font-size='96' font-weight='700' fill='%2322dd3b' text-anchor='middle'>KB</text></svg>`),
                sizes: "192x192", type: "image/svg+xml", purpose: "any"
            }
        ],
        shortcuts: [
            { name: "Boutique", url: "./?page=client", description: "Voir les produits" },
            { name: "Mon panier", url: "./?page=cart", description: "Voir le panier" }
        ]
    };

    const blob = new Blob([JSON.stringify(manifest)], { type: "application/json" });
    const manifestURL = URL.createObjectURL(blob);
    document.getElementById("pwa-manifest").setAttribute("href", manifestURL);

    // ── 2. Service Worker (inline blob) ──
    if ("serviceWorker" in navigator) {
        const swCode = `
const CACHE = "kb-market-v1";
const SHELL = ["/"];

self.addEventListener("install", e => {
    e.waitUntil(
        caches.open(CACHE).then(c => c.addAll(SHELL)).then(() => self.skipWaiting())
    );
});

self.addEventListener("activate", e => {
    e.waitUntil(
        caches.keys().then(keys =>
            Promise.all(keys.filter(k => k !== CACHE).map(k => caches.delete(k)))
        ).then(() => self.clients.claim())
    );
});

self.addEventListener("fetch", e => {
    if (e.request.method !== "GET") return;
    e.respondWith(
        fetch(e.request)
            .then(res => {
                const clone = res.clone();
                caches.open(CACHE).then(c => c.put(e.request, clone));
                return res;
            })
            .catch(() => caches.match(e.request))
    );
});
        `;
        const swBlob = new Blob([swCode], { type: "application/javascript" });
        const swURL = URL.createObjectURL(swBlob);
        navigator.serviceWorker.register(swURL).catch(() => {});
    }

    // ── 3. Install Banner ──
    let deferredPrompt = null;
    const banner = document.getElementById("pwa-install-banner");
    const installBtn = document.getElementById("pwa-install-btn");
    const dismissBtn = document.getElementById("pwa-dismiss-btn");

    window.addEventListener("beforeinstallprompt", e => {
        e.preventDefault();
        deferredPrompt = e;
        if (banner && !localStorage.getItem("kb_pwa_dismissed")) {
            banner.style.display = "flex";
        }
    });

    if (installBtn) {
        installBtn.addEventListener("click", async () => {
            if (!deferredPrompt) return;
            deferredPrompt.prompt();
            const { outcome } = await deferredPrompt.userChoice;
            if (outcome === "accepted") localStorage.setItem("kb_pwa_installed", "1");
            deferredPrompt = null;
            banner.style.display = "none";
        });
    }
    if (dismissBtn) {
        dismissBtn.addEventListener("click", () => {
            banner.style.display = "none";
            localStorage.setItem("kb_pwa_dismissed", "1");
        });
    }

    // ── 4. iOS Safari install hint ──
    const isIOS = /iphone|ipad|ipod/i.test(navigator.userAgent);
    const isStandalone = ("standalone" in navigator) && navigator.standalone;
    const iosBanner = document.getElementById("pwa-ios-hint");
    if (isIOS && !isStandalone && !localStorage.getItem("kb_ios_dismissed") && iosBanner) {
        iosBanner.style.display = "flex";
        document.getElementById("pwa-ios-close").onclick = () => {
            iosBanner.style.display = "none";
            localStorage.setItem("kb_ios_dismissed", "1");
        };
    }
})();
</script>

<!-- ── INSTALL BANNER (Android/Chrome) ── -->
<div id="pwa-install-banner" style="
    display:none; position:fixed; bottom:0; left:0; right:0; z-index:99999;
    background:linear-gradient(135deg,#0d1220,#111827);
    border-top:1px solid rgba(34,221,59,0.25);
    padding:14px 16px; align-items:center; gap:12px;
    box-shadow:0 -8px 32px rgba(0,0,0,0.5);
">
    <div style="width:44px;height:44px;background:linear-gradient(135deg,#22dd3b,#16a32a);border-radius:12px;display:flex;align-items:center;justify-content:center;font-family:monospace;font-weight:700;color:#06080f;font-size:0.95rem;flex-shrink:0">KB</div>
    <div style="flex:1;min-width:0">
        <div style="font-weight:700;color:#fff;font-size:0.92rem">Installer KBmarketplace</div>
        <div style="color:#6b7a96;font-size:0.78rem;margin-top:2px">Accès rapide depuis votre écran d'accueil</div>
    </div>
    <button id="pwa-install-btn" style="background:#22dd3b;color:#06080f;border:none;padding:9px 18px;border-radius:50px;font-weight:700;font-size:0.82rem;cursor:pointer;font-family:'Outfit',sans-serif;white-space:nowrap">Installer</button>
    <button id="pwa-dismiss-btn" style="background:transparent;border:none;color:#6b7a96;font-size:1.3rem;cursor:pointer;padding:4px;line-height:1">×</button>
</div>

<!-- ── IOS INSTALL HINT ── -->
<div id="pwa-ios-hint" style="
    display:none; position:fixed; bottom:0; left:0; right:0; z-index:99999;
    background:linear-gradient(135deg,#0d1220,#111827);
    border-top:1px solid rgba(34,221,59,0.25);
    padding:14px 16px; align-items:flex-start; gap:12px;
    box-shadow:0 -8px 32px rgba(0,0,0,0.5);
">
    <div style="width:44px;height:44px;background:linear-gradient(135deg,#22dd3b,#16a32a);border-radius:12px;display:flex;align-items:center;justify-content:center;font-family:monospace;font-weight:700;color:#06080f;font-size:0.95rem;flex-shrink:0">KB</div>
    <div style="flex:1">
        <div style="font-weight:700;color:#fff;font-size:0.92rem">Installer sur iPhone / iPad</div>
        <div style="color:#6b7a96;font-size:0.78rem;margin-top:4px;line-height:1.5">
            Appuyez sur <strong style="color:#22dd3b">⬆️ Partager</strong> dans Safari,<br>
            puis <strong style="color:#22dd3b">« Sur l'écran d'accueil »</strong>
        </div>
    </div>
    <button id="pwa-ios-close" style="background:transparent;border:none;color:#6b7a96;font-size:1.3rem;cursor:pointer;padding:4px;line-height:1">×</button>
</div>

</body>
</html>
