# Glowup-makeup-store
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>GlowUp – Makeup Store</title>
  <link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet"/>
  <style>
    /* ===== RESET & ROOT ===== */
    *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }
    :root {
      --rose:    #e8556d;
      --blush:   #f9c6d0;
      --cream:   #fff8f5;
      --nude:    #f4e4d8;
      --plum:    #6b2d5e;
      --gold:    #c89b6e;
      --dark:    #2a1a24;
      --white:   #ffffff;
      --shadow:  0 8px 32px rgba(107,45,94,0.12);
    }
    html { scroll-behavior: smooth; }
    body { font-family: 'DM Sans', sans-serif; background: var(--cream); color: var(--dark); overflow-x: hidden; }
 
    /* ===== NAVBAR ===== */
    nav {
      position: fixed; top: 0; left: 0; right: 0; z-index: 1000;
      background: rgba(255,248,245,0.92); backdrop-filter: blur(12px);
      border-bottom: 1px solid #f4d0d8;
      display: flex; align-items: center; justify-content: space-between;
      padding: 0 40px; height: 68px;
    }
    .logo { font-family: 'Playfair Display', serif; font-size: 28px; color: var(--rose); letter-spacing: 1px; }
    .logo span { color: var(--plum); font-style: italic; }
    .nav-links { display: flex; gap: 28px; list-style: none; }
    .nav-links a { text-decoration: none; color: var(--dark); font-size: 14px; font-weight: 500; transition: color .2s; }
    .nav-links a:hover { color: var(--rose); }
    .nav-right { display: flex; gap: 14px; align-items: center; }
    .nav-right button {
      background: none; border: none; cursor: pointer;
      font-size: 20px; color: var(--dark); transition: color .2s; position: relative;
    }
    .nav-right button:hover { color: var(--rose); }
    #cart-count {
      position: absolute; top: -6px; right: -8px;
      background: var(--rose); color: #fff; font-size: 10px;
      border-radius: 50%; width: 18px; height: 18px; display: flex;
      align-items: center; justify-content: center; font-weight: 700;
    }
 
    /* ===== SEARCH BAR ===== */
    .search-wrap {
      display: flex; align-items: center;
      background: var(--nude); border-radius: 30px;
      padding: 6px 16px; gap: 8px; border: 1.5px solid transparent;
      transition: border .2s;
    }
    .search-wrap:focus-within { border-color: var(--rose); }
    .search-wrap input {
      border: none; background: none; outline: none;
      font-family: 'DM Sans', sans-serif; font-size: 14px; width: 160px; color: var(--dark);
    }
    .search-wrap span { color: #b08090; font-size: 16px; }
 
    /* ===== HERO SLIDER ===== */
    .slider { position: relative; margin-top: 68px; height: 520px; overflow: hidden; }
    .slide {
      position: absolute; inset: 0;
      display: flex; align-items: center; justify-content: center;
      opacity: 0; transition: opacity .8s ease;
      flex-direction: column; text-align: center; padding: 40px;
    }
    .slide.active { opacity: 1; }
    .slide-1 { background: linear-gradient(135deg, #f9c6d0 0%, #f7e0ea 50%, #fff8f5 100%); }
    .slide-2 { background: linear-gradient(135deg, #d4b0e0 0%, #f0c8d8 50%, #fff0f5 100%); }
    .slide-3 { background: linear-gradient(135deg, #c8dff0 0%, #e8d0f0 50%, #fff5f8 100%); }
    .slide-emoji { font-size: 90px; margin-bottom: 16px; animation: float 3s ease-in-out infinite; }
    @keyframes float { 0%,100%{transform:translateY(0)} 50%{transform:translateY(-12px)} }
    .slide h1 { font-family: 'Playfair Display', serif; font-size: 48px; color: var(--plum); margin-bottom: 10px; }
    .slide p { font-size: 18px; color: #7a4060; margin-bottom: 24px; max-width: 480px; }
    .btn {
      display: inline-block; padding: 13px 36px; border-radius: 40px;
      background: var(--rose); color: #fff; font-size: 15px; font-weight: 500;
      text-decoration: none; border: none; cursor: pointer; transition: transform .2s, box-shadow .2s;
      font-family: 'DM Sans', sans-serif;
    }
    .btn:hover { transform: translateY(-2px); box-shadow: 0 8px 24px rgba(232,85,109,.35); }
    .btn-outline {
      background: transparent; border: 2px solid var(--rose); color: var(--rose);
    }
    .btn-outline:hover { background: var(--rose); color: #fff; }
    .slider-dots { position: absolute; bottom: 20px; left: 50%; transform: translateX(-50%); display: flex; gap: 8px; }
    .dot {
      width: 10px; height: 10px; border-radius: 50%; background: #d4a0b0;
      cursor: pointer; transition: background .3s, transform .3s;
    }
    .dot.active { background: var(--rose); transform: scale(1.3); }
    .slider-btn {
      position: absolute; top: 50%; transform: translateY(-50%);
      background: rgba(255,255,255,.7); border: none; border-radius: 50%;
      width: 44px; height: 44px; font-size: 20px; cursor: pointer;
      display: flex; align-items: center; justify-content: center;
      transition: background .2s; color: var(--plum);
    }
    .slider-btn:hover { background: #fff; }
    .slider-prev { left: 16px; }
    .slider-next { right: 16px; }
 
    /* ===== SECTIONS ===== */
    section { padding: 70px 40px; }
    .section-title {
      font-family: 'Playfair Display', serif;
      font-size: 38px; color: var(--plum); margin-bottom: 8px; text-align: center;
    }
    .section-sub { text-align: center; color: #9a6070; margin-bottom: 40px; font-size: 15px; }
 
    /* ===== CATEGORIES ===== */
    .cats { background: var(--nude); }
    .cat-grid { display: flex; gap: 20px; justify-content: center; flex-wrap: wrap; }
    .cat-card {
      background: #fff; border-radius: 20px; padding: 30px 22px;
      text-align: center; cursor: pointer; transition: transform .25s, box-shadow .25s;
      width: 130px; box-shadow: var(--shadow);
    }
    .cat-card:hover { transform: translateY(-8px); box-shadow: 0 16px 40px rgba(107,45,94,.18); }
    .cat-card div { font-size: 40px; margin-bottom: 10px; }
    .cat-card p { font-size: 13px; font-weight: 500; color: var(--plum); }
 
    /* ===== PRODUCTS ===== */
    .prod-grid { display: grid; grid-template-columns: repeat(auto-fill, minmax(220px, 1fr)); gap: 24px; }
    .prod-card {
      background: #fff; border-radius: 20px; overflow: hidden;
      box-shadow: var(--shadow); transition: transform .25s, box-shadow .25s; position: relative;
    }
    .prod-card:hover { transform: translateY(-6px); box-shadow: 0 20px 44px rgba(107,45,94,.18); }
    .prod-img {
      height: 200px; display: flex; align-items: center; justify-content: center;
      font-size: 80px; position: relative;
    }
    .badge {
      position: absolute; top: 12px; left: 12px;
      background: var(--rose); color: #fff; font-size: 11px;
      padding: 3px 10px; border-radius: 20px; font-weight: 600;
    }
    .badge.new { background: var(--plum); }
    .badge.sale { background: var(--gold); }
    .prod-info { padding: 16px; }
    .prod-info h3 { font-size: 15px; font-weight: 600; margin-bottom: 4px; color: var(--dark); }
    .prod-info .brand { font-size: 12px; color: #b08090; margin-bottom: 8px; }
    .stars { color: var(--gold); font-size: 13px; margin-bottom: 10px; }
    .price-row { display: flex; align-items: center; justify-content: space-between; }
    .price { font-size: 18px; font-weight: 700; color: var(--rose); }
    .price-old { font-size: 13px; color: #bbb; text-decoration: line-through; margin-left: 6px; }
    .add-btn {
      background: var(--plum); color: #fff; border: none; border-radius: 50%;
      width: 36px; height: 36px; font-size: 18px; cursor: pointer;
      transition: background .2s, transform .2s; display: flex; align-items: center; justify-content: center;
    }
    .add-btn:hover { background: var(--rose); transform: scale(1.12); }
 
    /* ===== TOAST ===== */
    #toast {
      position: fixed; bottom: 28px; right: 28px; z-index: 9999;
      background: var(--plum); color: #fff; padding: 14px 24px;
      border-radius: 12px; font-size: 14px; opacity: 0; pointer-events: none;
      transition: opacity .3s; box-shadow: var(--shadow);
    }
    #toast.show { opacity: 1; }
 
    /* ===== CART SIDEBAR ===== */
    .cart-overlay {
      position: fixed; inset: 0; background: rgba(30,10,24,.4);
      z-index: 2000; opacity: 0; pointer-events: none; transition: opacity .3s;
    }
    .cart-overlay.open { opacity: 1; pointer-events: all; }
    .cart-panel {
      position: fixed; top: 0; right: -420px; width: 400px; max-width: 95vw;
      height: 100vh; background: #fff; z-index: 2001;
      box-shadow: -4px 0 40px rgba(107,45,94,.18);
      transition: right .35s cubic-bezier(.4,0,.2,1);
      display: flex; flex-direction: column; padding: 28px;
    }
    .cart-panel.open { right: 0; }
    .cart-head { display: flex; align-items: center; justify-content: space-between; margin-bottom: 24px; }
    .cart-head h2 { font-family: 'Playfair Display', serif; font-size: 24px; color: var(--plum); }
    .close-cart { background: none; border: none; font-size: 24px; cursor: pointer; color: var(--dark); }
    #cart-items { flex: 1; overflow-y: auto; display: flex; flex-direction: column; gap: 14px; }
    .cart-item {
      display: flex; align-items: center; gap: 14px;
      background: var(--cream); border-radius: 14px; padding: 12px;
    }
    .cart-item-emoji { font-size: 36px; }
    .cart-item-info { flex: 1; }
    .cart-item-info strong { font-size: 14px; display: block; color: var(--dark); }
    .cart-item-info span { font-size: 13px; color: var(--rose); font-weight: 600; }
    .remove-btn { background: none; border: none; color: #e0a0b0; cursor: pointer; font-size: 18px; }
    .cart-total { margin-top: 20px; padding-top: 16px; border-top: 1px solid #f0d0da; }
    .cart-total p { font-size: 18px; font-weight: 700; color: var(--plum); margin-bottom: 14px; }
    .cart-empty { text-align: center; color: #c0a0b0; font-size: 15px; margin-top: 60px; }
    .cart-empty div { font-size: 60px; margin-bottom: 16px; }
 
    /* ===== REGISTER FORM ===== */
    .register { background: linear-gradient(135deg, #f9c6d0, #f0d8f0); }
    .form-card {
      background: #fff; border-radius: 24px; max-width: 520px;
      margin: 0 auto; padding: 48px 40px; box-shadow: var(--shadow);
    }
    .form-card h2 { font-family: 'Playfair Display', serif; font-size: 30px; color: var(--plum); margin-bottom: 6px; }
    .form-card p { color: #9a6070; font-size: 14px; margin-bottom: 28px; }
    .form-group { margin-bottom: 18px; }
    .form-group label { display: block; font-size: 13px; font-weight: 500; color: var(--plum); margin-bottom: 6px; }
    .form-group input, .form-group select {
      width: 100%; padding: 12px 16px; border: 1.5px solid #f0d0da;
      border-radius: 12px; font-size: 14px; font-family: 'DM Sans', sans-serif;
      color: var(--dark); background: var(--cream); outline: none;
      transition: border .2s;
    }
    .form-group input:focus, .form-group select:focus { border-color: var(--rose); }
    .form-row { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
    .form-msg { font-size: 13px; margin-top: 14px; color: var(--rose); text-align: center; display: none; }
    .form-success { color: #5a8f5a; }
 
    /* ===== FOOTER ===== */
    footer {
      background: var(--dark); color: #e0c0cc; text-align: center;
      padding: 36px 40px; font-size: 14px;
    }
    footer .foot-logo { font-family: 'Playfair Display', serif; font-size: 28px; color: var(--rose); margin-bottom: 8px; }
    footer p { color: #9a7080; font-size: 13px; margin-top: 8px; }
 
    /* ===== SEARCH RESULTS ===== */
    #search-results {
      position: absolute; top: 100%; right: 0; width: 280px;
      background: #fff; border-radius: 16px; box-shadow: var(--shadow);
      max-height: 300px; overflow-y: auto; z-index: 999; display: none; padding: 10px 0;
    }
    .search-result-item {
      display: flex; align-items: center; gap: 12px;
      padding: 10px 18px; cursor: pointer; transition: background .15s;
    }
    .search-result-item:hover { background: var(--cream); }
    .search-result-item span { font-size: 28px; }
    .search-result-item div strong { font-size: 13px; display: block; color: var(--dark); }
    .search-result-item div small { color: var(--rose); font-size: 12px; }
    .search-wrap-pos { position: relative; }
 
    /* ===== RESPONSIVE ===== */
    @media(max-width: 700px) {
      nav { padding: 0 16px; }
      .nav-links { display: none; }
      .slide h1 { font-size: 30px; }
      .slider { height: 400px; }
      section { padding: 50px 20px; }
      .form-card { padding: 30px 20px; }
      .form-row { grid-template-columns: 1fr; }
    }
  </style>
</head>
<body>
 
<!-- NAVBAR -->
<nav>
  <div class="logo">Glow<span>Up</span> 💄</div>
  <ul class="nav-links">
    <li><a href="#products">Products</a></li>
    <li><a href="#categories">Categories</a></li>
    <li><a href="#register">Register</a></li>
  </ul>
  <div class="nav-right">
    <div class="search-wrap-pos">
      <div class="search-wrap">
        <span>🔍</span>
        <input type="text" id="search-input" placeholder="Search products…" autocomplete="off"/>
      </div>
      <div id="search-results"></div>
    </div>
    <button onclick="openCart()" title="Cart" style="position:relative">
      🛒<span id="cart-count">0</span>
    </button>
  </div>
</nav>
 
<!-- HERO SLIDER -->
<div class="slider">
  <div class="slide slide-1 active">
    <div class="slide-emoji">💋</div>
    <h1>Be Boldly Beautiful</h1>
    <p>Explore our luxurious lip collections — from nudes to neons, every shade tells your story.</p>
    <a href="#products" class="btn">Shop Lips</a>
  </div>
  <div class="slide slide-2">
    <div class="slide-emoji">✨</div>
    <h1>Glow Like Never Before</h1>
    <p>Highlighters, bronzers & blushes that give you that runway-ready radiance every day.</p>
    <a href="#products" class="btn">Shop Glow</a>
  </div>
  <div class="slide slide-3">
    <div class="slide-emoji">👁️</div>
    <h1>Eyes That Mesmerize</h1>
    <p>Drama-worthy eyeshadows, liners & mascaras for looks from subtle to sensational.</p>
    <a href="#products" class="btn">Shop Eyes</a>
  </div>
  <button class="slider-btn slider-prev" onclick="prevSlide()">&#8592;</button>
  <button class="slider-btn slider-next" onclick="nextSlide()">&#8594;</button>
  <div class="slider-dots">
    <div class="dot active" onclick="goSlide(0)"></div>
    <div class="dot" onclick="goSlide(1)"></div>
    <div class="dot" onclick="goSlide(2)"></div>
  </div>
</div>
 
<!-- CATEGORIES -->
<section class="cats" id="categories">
  <h2 class="section-title">Shop by Category</h2>
  <p class="section-sub">Find exactly what you're looking for</p>
  <div class="cat-grid">
    <div class="cat-card" onclick="filterProducts('lips')"><div>💋</div><p>Lips</p></div>
    <div class="cat-card" onclick="filterProducts('eyes')"><div>👁️</div><p>Eyes</p></div>
    <div class="cat-card" onclick="filterProducts('face')"><div>✨</div><p>Face</p></div>
    <div class="cat-card" onclick="filterProducts('skincare')"><div>🌸</div><p>Skincare</p></div>
    <div class="cat-card" onclick="filterProducts('nails')"><div>💅</div><p>Nails</p></div>
    <div class="cat-card" onclick="filterProducts('all')"><div>🛍️</div><p>All</p></div>
  </div>
</section>
 
<!-- PRODUCTS -->
<section id="products">
  <h2 class="section-title">Our Products</h2>
  <p class="section-sub">Handpicked bestsellers & new arrivals just for you</p>
  <div class="prod-grid" id="prod-grid"></div>
</section>
 
<!-- REGISTER -->
<section class="register" id="register">
  <div class="form-card">
    <h2>Join GlowUp 💄</h2>
    <p>Create your account to unlock exclusive deals & early access to new arrivals!</p>
    <div class="form-row">
      <div class="form-group">
        <label>First Name</label>
        <input type="text" id="fname" placeholder="Priya"/>
      </div>
      <div class="form-group">
        <label>Last Name</label>
        <input type="text" id="lname" placeholder="Sharma"/>
      </div>
    </div>
    <div class="form-group">
      <label>Email Address</label>
      <input type="email" id="email" placeholder="you@email.com"/>
    </div>
    <div class="form-group">
      <label>Phone Number</label>
      <input type="tel" id="phone" placeholder="+91 98765 43210"/>
    </div>
    <div class="form-group">
      <label>Skin Type</label>
      <select id="skin">
        <option value="">Select skin type…</option>
        <option>Oily</option>
        <option>Dry</option>
        <option>Combination</option>
        <option>Normal</option>
        <option>Sensitive</option>
      </select>
    </div>
    <div class="form-group">
      <label>Password</label>
      <input type="password" id="pass" placeholder="Create a password"/>
    </div>
    <button class="btn" style="width:100%;font-size:16px" onclick="registerUser()">Create My Account ✨</button>
    <p class="form-msg" id="form-msg"></p>
  </div>
</section>
 
<!-- FOOTER -->
<footer>
  <div class="foot-logo">GlowUp 💄</div>
  <p>Your one-stop beauty destination — Shimmer, Shine & Slay Every Day!</p>
  <p style="margin-top:16px">Made with 💗 · College Project · 2024</p>
</footer>
 
<!-- CART SIDEBAR -->
<div class="cart-overlay" id="cart-overlay" onclick="closeCart()"></div>
<div class="cart-panel" id="cart-panel">
  <div class="cart-head">
    <h2>Your Bag 🛍️</h2>
    <button class="close-cart" onclick="closeCart()">✕</button>
  </div>
  <div id="cart-items"></div>
  <div class="cart-total" id="cart-total" style="display:none">
    <p id="total-price">Total: ₹0</p>
    <button class="btn" style="width:100%" onclick="checkout()">Checkout 💳</button>
  </div>
</div>
 
<!-- TOAST -->
<div id="toast"></div>
 
<script>
  /* ===== PRODUCTS DATA ===== */
  const products = [
    { id:1, name:"Velvet Matte Lipstick", brand:"L'Oréal", emoji:"💄", cat:"lips", price:649, old:899, badge:"bestseller", stars:5 },
    { id:2, name:"Glossy Lip Plumper", brand:"NYX", emoji:"💋", cat:"lips", price:499, old:null, badge:"new", stars:4 },
    { id:3, name:"Liquid Matte Lip", brand:"Maybelline", emoji:"🫦", cat:"lips", price:399, old:550, badge:"sale", stars:4 },
    { id:4, name:"Smoky Eye Palette", brand:"Urban Decay", emoji:"🎨", cat:"eyes", price:1299, old:1800, badge:"bestseller", stars:5 },
    { id:5, name:"Volumising Mascara", brand:"Lakme", emoji:"👁️", cat:"eyes", price:349, old:null, badge:"new", stars:4 },
    { id:6, name:"Kohl Kajal Liner", brand:"Himalaya", emoji:"✏️", cat:"eyes", price:249, old:null, badge:null, stars:5 },
    { id:7, name:"Dewy Foundation", brand:"MAC", emoji:"🪆", cat:"face", price:1499, old:1999, badge:"sale", stars:5 },
    { id:8, name:"Rose Gold Highlighter", brand:"Fenty Beauty", emoji:"✨", cat:"face", price:999, old:null, badge:"new", stars:5 },
    { id:9, name:"Peachy Blush Palette", brand:"Nars", emoji:"🌸", cat:"face", price:799, old:1100, badge:"sale", stars:4 },
    { id:10, name:"Glow Serum Primer", brand:"Smashbox", emoji:"💧", cat:"skincare", price:849, old:null, badge:"new", stars:4 },
    { id:11, name:"Rose Face Mist", brand:"Mario Badescu", emoji:"🌹", cat:"skincare", price:649, old:850, badge:"sale", stars:5 },
    { id:12, name:"Glitter Nail Set", brand:"OPI", emoji:"💅", cat:"nails", price:599, old:null, badge:"new", stars:4 },
  ];
 
  let cart = [];
  let currentSlide = 0;
 
  /* ===== RENDER PRODUCTS ===== */
  function renderProducts(list) {
    const grid = document.getElementById('prod-grid');
    grid.innerHTML = '';
    if (!list.length) {
      grid.innerHTML = '<p style="text-align:center;color:#b08090;grid-column:1/-1">No products found 😔</p>';
      return;
    }
    list.forEach(p => {
      const stars = '★'.repeat(p.stars) + '☆'.repeat(5 - p.stars);
      const badge = p.badge ? `<div class="badge ${p.badge}">${p.badge.toUpperCase()}</div>` : '';
      const old = p.old ? `<span cla