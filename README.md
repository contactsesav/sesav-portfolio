<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>SESAV — Creative Web Developer & UI Designer</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com"/>
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin/>
  <link href="https://fonts.googleapis.com/css2?family=Bebas+Neue&family=Outfit:wght@300;400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap" rel="stylesheet"/>
  <style>
    /* ─── DESIGN TOKENS ─────────────────────────────── */
    :root {
      --bg:        #04040A;
      --bg-card:   #080810;
      --bg-card2:  #0C0C18;
      --purple:    #C44DFF;
      --purple-2:  #9B18E8;
      --purple-dim:#6B10B0;
      --glow-sm:   0 0 20px rgba(196,77,255,0.35);
      --glow-md:   0 0 40px rgba(196,77,255,0.4), 0 0 80px rgba(196,77,255,0.15);
      --glow-lg:   0 0 60px rgba(196,77,255,0.5), 0 0 120px rgba(196,77,255,0.2);
      --line:      rgba(196,77,255,0.18);
      --text-mute: #5A5A7A;
      --text-sub:  #9090B0;
    }

    /* ─── BASE ──────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      font-family: 'Outfit', sans-serif;
      color: #E2E2F0;
      overflow-x: hidden;
      cursor: none;
    }

    /* ─── CUSTOM CURSOR ─────────────────────────────── */
    #cursor {
      width: 12px; height: 12px;
      background: var(--purple);
      border-radius: 50%;
      position: fixed;
      top: 0; left: 0;
      pointer-events: none;
      z-index: 99999;
      transform: translate(-50%,-50%);
      transition: transform 0.1s, width 0.3s, height 0.3s, opacity 0.3s;
      box-shadow: var(--glow-sm);
    }
    #cursor-ring {
      width: 36px; height: 36px;
      border: 1px solid rgba(196,77,255,0.5);
      border-radius: 50%;
      position: fixed;
      top: 0; left: 0;
      pointer-events: none;
      z-index: 99998;
      transform: translate(-50%,-50%);
      transition: all 0.15s ease;
    }
    body:has(a:hover) #cursor, body:has(button:hover) #cursor {
      width: 20px; height: 20px;
    }

    /* ─── SCROLLBAR ──────────────────────────────────── */
    ::-webkit-scrollbar { width: 3px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--purple-2); border-radius: 3px; }

    /* ─── NOISE OVERLAY ──────────────────────────────── */
    #noise {
      position: fixed; inset: 0; z-index: 9997; pointer-events: none;
      opacity: 0.035;
      background-image: url("data:image/svg+xml,%3Csvg xmlns='http://www.w3.org/2000/svg' width='300' height='300'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.75' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='300' height='300' filter='url(%23n)'/%3E%3C/svg%3E");
    }

    /* ─── SCANLINES ──────────────────────────────────── */
    #scanlines {
      position: fixed; inset: 0; z-index: 9996; pointer-events: none;
      background: repeating-linear-gradient(
        to bottom,
        transparent 0px, transparent 2px,
        rgba(0,0,0,0.06) 2px, rgba(0,0,0,0.06) 4px
      );
    }

    /* ─── GRID BACKGROUND ────────────────────────────── */
    .grid-bg {
      background-image:
        linear-gradient(rgba(196,77,255,0.04) 1px, transparent 1px),
        linear-gradient(90deg, rgba(196,77,255,0.04) 1px, transparent 1px);
      background-size: 72px 72px;
    }

    /* ─── TYPOGRAPHY ─────────────────────────────────── */
    .font-bebas  { font-family: 'Bebas Neue', sans-serif; }
    .font-outfit { font-family: 'Outfit', sans-serif; }
    .font-mono   { font-family: 'JetBrains Mono', monospace; }

    /* ─── GLOW UTILITIES ─────────────────────────────── */
    .glow-text {
      color: var(--purple);
      text-shadow: 0 0 30px rgba(196,77,255,0.7), 0 0 60px rgba(196,77,255,0.3);
    }
    .glow-border {
      border: 1px solid var(--line);
      box-shadow: inset 0 0 30px rgba(196,77,255,0.03);
    }
    .glow-btn {
      background: linear-gradient(135deg, var(--purple), var(--purple-2));
      box-shadow: var(--glow-md);
      transition: all 0.35s cubic-bezier(0.34,1.56,0.64,1);
    }
    .glow-btn:hover {
      box-shadow: var(--glow-lg);
      transform: translateY(-3px) scale(1.03);
    }
    .outline-btn {
      border: 1px solid var(--line);
      background: transparent;
      transition: all 0.3s ease;
    }
    .outline-btn:hover {
      border-color: var(--purple);
      background: rgba(196,77,255,0.07);
      box-shadow: var(--glow-sm);
      transform: translateY(-2px);
    }

    /* ─── NAV ─────────────────────────────────────────── */
    nav {
      background: rgba(4,4,10,0.8);
      backdrop-filter: blur(24px);
      -webkit-backdrop-filter: blur(24px);
      border-bottom: 1px solid rgba(196,77,255,0.08);
    }
    .nav-link {
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.7rem;
      color: var(--text-sub);
      letter-spacing: 0.12em;
      text-transform: uppercase;
      position: relative;
      transition: color 0.3s;
    }
    .nav-link::before {
      content: '';
      position: absolute;
      bottom: -4px; left: 0;
      width: 0; height: 1px;
      background: var(--purple);
      box-shadow: var(--glow-sm);
      transition: width 0.35s ease;
    }
    .nav-link:hover { color: var(--purple); }
    .nav-link:hover::before { width: 100%; }

    /* ─── HERO ────────────────────────────────────────── */
    .hero-headline {
      font-family: 'Bebas Neue', sans-serif;
      font-size: clamp(4rem, 12vw, 9rem);
      line-height: 0.92;
      letter-spacing: 0.02em;
    }

    /* Animated gradient border */
    @keyframes borderSpin {
      0%   { background-position: 0% 50%; }
      50%  { background-position: 100% 50%; }
      100% { background-position: 0% 50%; }
    }
    .gradient-border {
      position: relative;
      border-radius: 1.25rem;
    }
    .gradient-border::before {
      content: '';
      position: absolute;
      inset: -1px;
      border-radius: inherit;
      background: linear-gradient(135deg, var(--purple), transparent, var(--purple-2), transparent, var(--purple));
      background-size: 300% 300%;
      animation: borderSpin 6s ease infinite;
      z-index: 0;
      opacity: 0.7;
    }
    .gradient-border > * { position: relative; z-index: 1; }
    .gradient-border-inner {
      background: var(--bg-card);
      border-radius: calc(1.25rem - 1px);
    }

    /* ─── FLOATING ELEMENTS ───────────────────────────── */
    @keyframes float1 {
      0%,100% { transform: translateY(0) rotate(0deg); }
      50%      { transform: translateY(-18px) rotate(1deg); }
    }
    @keyframes float2 {
      0%,100% { transform: translateY(0) rotate(0deg); }
      50%      { transform: translateY(-12px) rotate(-1deg); }
    }
    .float1 { animation: float1 7s ease-in-out infinite; }
    .float2 { animation: float2 5s ease-in-out infinite; }

    /* ─── SECTION REVEALS ─────────────────────────────── */
    .reveal {
      opacity: 0;
      transform: translateY(36px);
      transition: opacity 0.8s cubic-bezier(0.16,1,0.3,1),
                  transform 0.8s cubic-bezier(0.16,1,0.3,1);
    }
    .reveal.in { opacity: 1; transform: translateY(0); }

    /* ─── SERVICE CARDS ───────────────────────────────── */
    .service-card {
      background: var(--bg-card);
      border: 1px solid rgba(196,77,255,0.12);
      transition: all 0.45s cubic-bezier(0.16,1,0.3,1);
      position: relative;
      overflow: hidden;
    }
    .service-card::after {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(196,77,255,0.07), transparent 65%);
      opacity: 0;
      transition: opacity 0.4s;
    }
    .service-card:hover::after { opacity: 1; }
    .service-card:hover {
      border-color: rgba(196,77,255,0.45);
      transform: translateY(-10px);
      box-shadow: 0 24px 60px rgba(196,77,255,0.12);
    }

    /* ─── TECH STACK ──────────────────────────────────── */
    .tech-pill {
      border: 1px solid rgba(196,77,255,0.18);
      background: rgba(196,77,255,0.05);
      transition: all 0.3s cubic-bezier(0.34,1.56,0.64,1);
    }
    .tech-pill:hover {
      border-color: var(--purple);
      background: rgba(196,77,255,0.12);
      box-shadow: var(--glow-sm);
      transform: scale(1.06) translateY(-3px);
    }

    /* ─── ORBS ────────────────────────────────────────── */
    .orb {
      position: absolute;
      border-radius: 50%;
      filter: blur(90px);
      pointer-events: none;
      will-change: transform;
    }

    /* ─── TAG ─────────────────────────────────────────── */
    .tag {
      background: rgba(196,77,255,0.1);
      border: 1px solid rgba(196,77,255,0.25);
      color: var(--purple);
      font-family: 'JetBrains Mono', monospace;
      font-size: 0.65rem;
      letter-spacing: 0.08em;
    }

    /* ─── ACCENT LINE ─────────────────────────────────── */
    .accent-line {
      height: 1px;
      background: linear-gradient(90deg, transparent 0%, var(--purple) 50%, transparent 100%);
      opacity: 0.3;
    }

    /* ─── STAT CARD ───────────────────────────────────── */
    .stat-card {
      border-left: 1px solid var(--line);
      padding-left: 1.5rem;
    }

    /* ─── MOBILE MENU ─────────────────────────────────── */
    #mob-menu {
      transition: max-height 0.5s cubic-bezier(0.16,1,0.3,1), opacity 0.4s ease;
      max-height: 0; opacity: 0; overflow: hidden;
    }
    #mob-menu.open { max-height: 360px; opacity: 1; }

    /* ─── MARQUEE ─────────────────────────────────────── */
    @keyframes marquee {
      0%   { transform: translateX(0); }
      100% { transform: translateX(-50%); }
    }
    .marquee-inner { animation: marquee 22s linear infinite; width: max-content; }

    /* ─── PROJECT HOVER ───────────────────────────────── */
    .proj-img { transition: transform 0.6s cubic-bezier(0.16,1,0.3,1); }
    .proj-wrap:hover .proj-img { transform: scale(1.05); }
    .proj-overlay {
      background: linear-gradient(180deg, transparent 40%, rgba(4,4,10,0.95) 100%);
    }

    /* ─── PULSING RING ─────────────────────────────────── */
    @keyframes pulseRing {
      0%   { transform: scale(1); opacity: 0.6; }
      100% { transform: scale(2.2); opacity: 0; }
    }
    .pulse-ring {
      position: absolute; inset: 0; border-radius: 50%;
      background: rgba(74,222,128,0.3);
      animation: pulseRing 2s ease-out infinite;
    }

    /* ─── HERO ENTER ANIMATION ──────────────────────────── */
    @keyframes heroIn {
      from { opacity: 0; transform: translateY(30px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    .hero-in { animation: heroIn 1s cubic-bezier(0.16,1,0.3,1) forwards; }
    .hero-in-1 { animation-delay: 0.1s; opacity: 0; }
    .hero-in-2 { animation-delay: 0.3s; opacity: 0; }
    .hero-in-3 { animation-delay: 0.5s; opacity: 0; }
    .hero-in-4 { animation-delay: 0.7s; opacity: 0; }
    .hero-in-5 { animation-delay: 0.9s; opacity: 0; }
  </style>
</head>
<body>

<!-- Cursor -->
<div id="cursor"></div>
<div id="cursor-ring"></div>

<!-- Overlays -->
<div id="noise"></div>
<div id="scanlines"></div>

<!-- ═══════════════════════════════════════════════════
     NAV
═══════════════════════════════════════════════════ -->
<nav class="fixed top-0 left-0 right-0 z-50 px-6 md:px-16 py-4">
  <div class="max-w-7xl mx-auto flex items-center justify-between">

    <!-- Logo -->
    <a href="#hero" class="flex items-center gap-3 group">
      <div class="w-8 h-8 rounded-lg flex items-center justify-center glow-btn text-xs font-bebas text-white tracking-wider">S</div>
      <span class="font-bebas text-2xl tracking-widest text-white group-hover:glow-text transition-colors duration-300">SESAV</span>
    </a>

    <!-- Desktop links -->
    <div class="hidden md:flex items-center gap-10">
      <a href="#services" class="nav-link">Services</a>
      <a href="#work"     class="nav-link">Work</a>
      <a href="#stack"    class="nav-link">Stack</a>
      <a href="#contact"  class="nav-link">Contact</a>
    </div>

    <!-- CTA desktop -->
    <a href="#contact" class="hidden md:inline-flex items-center gap-2 glow-btn text-white font-outfit font-semibold text-sm px-6 py-2.5 rounded-full">
      <span class="w-2 h-2 rounded-full bg-green-400 relative"><span class="pulse-ring" style="inset:-2px;position:absolute;"></span></span>
      Hire Me
    </a>

    <!-- Hamburger -->
    <button id="ham-btn" onclick="toggleMob()" class="md:hidden flex flex-col gap-1.5 p-2" aria-label="Menu">
      <span id="h1" class="block w-6 h-px bg-gray-400 transition-all duration-300 origin-center"></span>
      <span id="h2" class="block w-6 h-px bg-gray-400 transition-all duration-300"></span>
      <span id="h3" class="block w-6 h-px bg-gray-400 transition-all duration-300 origin-center"></span>
    </button>
  </div>

  <!-- Mobile menu -->
  <div id="mob-menu" class="md:hidden border-t mt-3" style="border-color:rgba(196,77,255,0.1);">
    <div class="py-4 flex flex-col gap-1 px-2">
      <a onclick="toggleMob()" href="#services" class="nav-link block py-3 px-2 border-b" style="border-color:rgba(255,255,255,0.04);">Services</a>
      <a onclick="toggleMob()" href="#work"     class="nav-link block py-3 px-2 border-b" style="border-color:rgba(255,255,255,0.04);">Work</a>
      <a onclick="toggleMob()" href="#stack"    class="nav-link block py-3 px-2 border-b" style="border-color:rgba(255,255,255,0.04);">Stack</a>
      <a onclick="toggleMob()" href="#contact"  class="nav-link block py-3 px-2">Contact</a>
      <a onclick="toggleMob()" href="#contact"  class="glow-btn text-white font-semibold text-sm px-6 py-3 rounded-full text-center mt-3">Hire Me</a>
    </div>
  </div>
</nav>


<!-- ═══════════════════════════════════════════════════
     HERO
═══════════════════════════════════════════════════ -->
<section id="hero" class="relative min-h-screen flex items-center pt-28 pb-20 px-6 md:px-16 overflow-hidden grid-bg">

  <!-- Ambient orbs -->
  <div class="orb w-[600px] h-[600px] bg-purple-700 opacity-10 -top-40 -right-40"></div>
  <div class="orb w-[400px] h-[400px] opacity-10" style="background:#3B006B; bottom:-80px; left:-100px;"></div>
  <div class="orb w-[300px] h-[300px] opacity-8 top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2" style="background:#6B10B0; filter:blur(120px);"></div>

  <!-- Vertical lines decorative -->
  <div class="absolute top-0 bottom-0 left-1/4 w-px opacity-5" style="background:linear-gradient(to bottom, transparent, var(--purple), transparent);"></div>
  <div class="absolute top-0 bottom-0 right-1/4 w-px opacity-5" style="background:linear-gradient(to bottom, transparent, var(--purple), transparent);"></div>

  <div class="max-w-7xl mx-auto w-full relative z-10">
    <div class="grid lg:grid-cols-5 gap-16 items-center">

      <!-- LEFT CONTENT — 3 cols -->
      <div class="lg:col-span-3">
        <!-- Status badge -->
        <div class="hero-in hero-in-1 inline-flex items-center gap-2.5 rounded-full px-4 py-2 mb-8 text-xs font-mono" style="background:rgba(196,77,255,0.07); border:1px solid rgba(196,77,255,0.2);">
          <span class="relative flex items-center justify-center w-2 h-2">
            <span class="pulse-ring" style="inset:-1px;position:absolute;"></span>
            <span class="w-2 h-2 rounded-full bg-green-400 block relative z-10"></span>
          </span>
          <span class="text-gray-400">Available for new projects</span>
        </div>

        <!-- Headline -->
        <h1 class="hero-in hero-in-2 hero-headline text-white mb-6">
          Turning<br/>
          <span class="glow-text">Ideas</span><br/>
          into Digital<br/>
          Reality
        </h1>

        <!-- Subtext -->
        <p class="hero-in hero-in-3 font-outfit font-light text-lg leading-relaxed mb-10 max-w-lg" style="color:var(--text-sub);">
          I craft immersive web experiences and pixel-perfect interfaces that don't just look stunning — they <em style="color:#DDD;font-style:normal;font-weight:500;">convert.</em>
        </p>

        <!-- CTAs -->
        <div class="hero-in hero-in-4 flex flex-wrap gap-4 mb-14">
          <a href="#work" class="glow-btn text-white font-outfit font-semibold px-8 py-4 rounded-full text-sm tracking-wide flex items-center gap-2">
            View My Work
            <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
          </a>
          <a href="#contact" class="outline-btn text-white font-outfit font-semibold px-8 py-4 rounded-full text-sm tracking-wide">
            Let's Talk
          </a>
        </div>

        <!-- Stats -->
        <div class="hero-in hero-in-5 flex flex-wrap gap-6 pt-8" style="border-top:1px solid rgba(255,255,255,0.06);">
          <div class="stat-card">
            <div class="font-bebas text-4xl glow-text">0</div>
            <div class="text-xs font-mono mt-1" style="color:var(--text-mute);">Projects Done</div>
          </div>
          <div class="stat-card">
            <div class="font-bebas text-4xl text-white leading-none">AI-Powered</div>
            <div class="text-xs font-mono mt-1" style="color:var(--text-mute);">Workflow</div>
          </div>
          <div class="stat-card">
            <div class="font-bebas text-4xl glow-text">100%</div>
            <div class="text-xs font-mono mt-1" style="color:var(--text-mute);">Client Sat.</div>
          </div>
        </div>
      </div>

      <!-- RIGHT VISUAL — 2 cols -->
      <div class="lg:col-span-2 flex justify-center items-center">
        <div class="relative w-full max-w-sm">

          <!-- Main card -->
          <div class="gradient-border float1">
            <div class="gradient-border-inner overflow-hidden rounded-[1.2rem]">
              <img
                src="https://images.unsplash.com/photo-1555396273-367ea4eb4db5?w=700&q=80"
                alt="The Spice Hub Project Preview"
                class="w-full object-cover"
                style="height:240px;"
              />
              <div class="p-5" style="background:var(--bg-card);">
                <div class="flex justify-between items-center mb-2">
                  <span class="tag px-2 py-1 rounded">Featured Project</span>
                  <span class="text-xs font-mono glow-text font-medium">● LIVE</span>
                </div>
                <div class="font-bebas text-2xl text-white tracking-wide mt-3">The Spice Hub</div>
                <div class="text-xs font-outfit mt-1" style="color:var(--text-mute);">Luxury Digital Menu · WhatsApp Ordering</div>
                <div class="flex gap-2 mt-3">
                  <span class="tag px-2 py-1 rounded-full">Tailwind</span>
                  <span class="tag px-2 py-1 rounded-full">JS</span>
                  <span class="tag px-2 py-1 rounded-full">AI</span>
                </div>
              </div>
            </div>
          </div>

          <!-- Floating badge top-right -->
          <div class="absolute -top-4 -right-4 float2 glow-border rounded-2xl p-3 text-center z-10" style="background:rgba(8,8,16,0.97); min-width:90px;">
            <div class="font-bebas text-xl glow-text">✦</div>
            <div class="text-xs font-mono mt-0.5" style="color:var(--text-mute);">SESAV</div>
          </div>

          <!-- Floating badge bottom-left -->
          <div class="absolute -bottom-4 -left-4 float1" style="animation-delay:-2.5s;">
            <div class="glow-border rounded-xl px-4 py-3" style="background:rgba(8,8,16,0.97);">
              <div class="text-xs font-mono" style="color:var(--text-mute);">Built with</div>
              <div class="text-sm font-outfit font-semibold text-white mt-0.5">AI × Design</div>
            </div>
          </div>

        </div>
      </div>
    </div>
  </div>

  <!-- Scroll indicator -->
  <div class="absolute bottom-8 left-1/2 -translate-x-1/2 flex flex-col items-center gap-2">
    <span class="font-mono text-xs" style="color:var(--text-mute);">scroll</span>
    <div class="w-px h-14" style="background:linear-gradient(to bottom, var(--purple), transparent);"></div>
  </div>
</section>

<!-- Marquee divider -->
<div class="py-5 overflow-hidden" style="background:rgba(196,77,255,0.05); border-top:1px solid var(--line); border-bottom:1px solid var(--line);">
  <div class="marquee-inner flex items-center gap-10 whitespace-nowrap">
    <template id="marquee-tpl">
      <span class="font-bebas text-lg tracking-widest glow-text">SESAV</span>
      <span class="font-mono text-xs" style="color:var(--text-mute);">✦</span>
      <span class="font-bebas text-lg tracking-widest" style="color:var(--text-sub);">CREATIVE WEB DEVELOPER</span>
      <span class="font-mono text-xs" style="color:var(--text-mute);">✦</span>
      <span class="font-bebas text-lg tracking-widest" style="color:var(--text-sub);">UI DESIGNER</span>
      <span class="font-mono text-xs" style="color:var(--text-mute);">✦</span>
      <span class="font-bebas text-lg tracking-widest glow-text">DIGITAL MENUS</span>
      <span class="font-mono text-xs" style="color:var(--text-mute);">✦</span>
      <span class="font-bebas text-lg tracking-widest" style="color:var(--text-sub);">LANDING PAGES</span>
      <span class="font-mono text-xs" style="color:var(--text-mute);">✦</span>
      <span class="font-bebas text-lg tracking-widest" style="color:var(--text-sub);">AI-POWERED WORKFLOW</span>
      <span class="font-mono text-xs" style="color:var(--text-mute);">✦</span>
    </template>
  </div>
</div>


<!-- ═══════════════════════════════════════════════════
     SERVICES
═══════════════════════════════════════════════════ -->
<section id="services" class="py-28 px-6 md:px-16 relative overflow-hidden">
  <div class="orb w-96 h-96 opacity-8 -top-20 -right-20" style="background:var(--purple-dim);"></div>

  <div class="max-w-7xl mx-auto">
    <!-- Header -->
    <div class="reveal mb-20 grid md:grid-cols-2 gap-6 items-end">
      <div>
        <span class="font-mono text-xs glow-text tracking-widest uppercase">— What I Build</span>
        <h2 class="font-bebas text-6xl md:text-7xl text-white mt-3 leading-none">
          Services<br/>Built for<br/>Impact
        </h2>
      </div>
      <p class="font-outfit font-light text-base leading-relaxed md:text-right" style="color:var(--text-sub);">
        Every project is approached with obsessive attention to craft, speed, and conversion-first design thinking.
      </p>
    </div>

    <!-- Cards -->
    <div class="grid md:grid-cols-3 gap-5">

      <!-- S1 -->
      <div class="reveal service-card rounded-2xl p-8 group">
        <div class="w-12 h-12 rounded-xl flex items-center justify-center text-2xl mb-7" style="background:rgba(196,77,255,0.1); border:1px solid rgba(196,77,255,0.2);">🍽️</div>
        <div class="font-mono text-xs glow-text mb-2 tracking-wider">01</div>
        <h3 class="font-bebas text-3xl text-white mb-3 tracking-wide">Digital Menus for Restaurants</h3>
        <p class="font-outfit font-light text-sm leading-relaxed" style="color:var(--text-sub);">
          QR-accessible, WhatsApp-integrated digital menus with beautiful typography, mobile-first layouts, and real-time order routing — built to elevate every dining moment.
        </p>
        <div class="mt-8 flex items-center gap-2 font-mono text-xs" style="color:var(--purple);">
          <span>Explore</span>
          <svg class="w-3 h-3 transition-transform group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
        </div>
      </div>

      <!-- S2 — highlighted -->
      <div class="reveal service-card rounded-2xl p-8 group" style="background:linear-gradient(145deg, rgba(155,24,232,0.15), rgba(8,8,16,1)); border-color:rgba(196,77,255,0.35);">
        <div class="absolute inset-0 rounded-2xl opacity-0 group-hover:opacity-100 transition-opacity duration-500" style="background:radial-gradient(circle at 50% 0, rgba(196,77,255,0.12), transparent 70%);"></div>
        <div class="relative z-10">
          <div class="flex justify-between items-start mb-7">
            <div class="w-12 h-12 rounded-xl flex items-center justify-center text-2xl" style="background:rgba(196,77,255,0.2); border:1px solid rgba(196,77,255,0.4);">🚀</div>
            <span class="tag px-3 py-1 rounded-full text-xs font-mono">Most Popular</span>
          </div>
          <div class="font-mono text-xs glow-text mb-2 tracking-wider">02</div>
          <h3 class="font-bebas text-3xl text-white mb-3 tracking-wide">Premium Landing Pages</h3>
          <p class="font-outfit font-light text-sm leading-relaxed" style="color:var(--text-sub);">
            Conversion-engineered, visually breathtaking landing pages that hook visitors in under 3 seconds and guide them seamlessly toward action.
          </p>
          <div class="mt-8 flex items-center gap-2 font-mono text-xs" style="color:var(--purple);">
            <span>Explore</span>
            <svg class="w-3 h-3 transition-transform group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
          </div>
        </div>
      </div>

      <!-- S3 -->
      <div class="reveal service-card rounded-2xl p-8 group">
        <div class="w-12 h-12 rounded-xl flex items-center justify-center text-2xl mb-7" style="background:rgba(196,77,255,0.1); border:1px solid rgba(196,77,255,0.2);">🎨</div>
        <div class="font-mono text-xs glow-text mb-2 tracking-wider">03</div>
        <h3 class="font-bebas text-3xl text-white mb-3 tracking-wide">UI/UX Design</h3>
        <p class="font-outfit font-light text-sm leading-relaxed" style="color:var(--text-sub);">
          From wireframes to polished high-fidelity prototypes — interfaces that feel intuitive, breathe beautifully, and make users fall in love at first scroll.
        </p>
        <div class="mt-8 flex items-center gap-2 font-mono text-xs" style="color:var(--purple);">
          <span>Explore</span>
          <svg class="w-3 h-3 transition-transform group-hover:translate-x-1" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
        </div>
      </div>
    </div>
  </div>
</section>

<div class="accent-line"></div>


<!-- ═══════════════════════════════════════════════════
     WORK / PORTFOLIO
═══════════════════════════════════════════════════ -->
<section id="work" class="py-28 px-6 md:px-16 relative overflow-hidden">
  <div class="orb w-[500px] h-[500px] opacity-8 -bottom-40 -left-40" style="background:var(--purple-2);"></div>

  <div class="max-w-7xl mx-auto">
    <!-- Header -->
    <div class="reveal mb-16 flex flex-col md:flex-row md:items-end justify-between gap-6">
      <div>
        <span class="font-mono text-xs glow-text tracking-widest uppercase">— Featured Work</span>
        <h2 class="font-bebas text-6xl md:text-7xl text-white mt-3 leading-none">The Flagship<br/>Project</h2>
      </div>
      <a href="#contact" class="outline-btn text-white font-outfit font-semibold text-sm px-6 py-3 rounded-full self-start md:self-end flex items-center gap-2">
        See Full Portfolio
        <svg class="w-3 h-3" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5"><path stroke-linecap="round" stroke-linejoin="round" d="M17 8l4 4m0 0l-4 4m4-4H3"/></svg>
      </a>
    </div>

    <!-- Featured project card -->
    <div class="reveal gradient-border rounded-[1.5rem] overflow-hidden">
      <div class="gradient-border-inner grid lg:grid-cols-2 min-h-[480px]">

        <!-- Image -->
        <div class="proj-wrap relative overflow-hidden" style="min-height:320px;">
          <img
            src="https://images.unsplash.com/photo-1414235077428-338989a2e8c0?w=900&q=80"
            alt="The Spice Hub — Luxury Digital Menu"
            class="proj-img w-full h-full object-cover absolute inset-0"
          />
          <div class="proj-overlay absolute inset-0"></div>

          <!-- Floating label on image -->
          <div class="absolute top-5 left-5">
            <span class="tag px-3 py-1.5 rounded-full font-mono text-xs backdrop-blur-sm" style="background:rgba(4,4,10,0.7);">✦ Flagship Project</span>
          </div>
          <div class="absolute bottom-5 left-5 flex gap-2">
            <span class="tag px-2.5 py-1 rounded-full">Restaurant Tech</span>
            <span class="tag px-2.5 py-1 rounded-full">WhatsApp Ordering</span>
          </div>
        </div>

        <!-- Details -->
        <div class="p-10 lg:p-14 flex flex-col justify-between" style="background:var(--bg-card);">
          <div>
            <div class="flex items-center gap-3 mb-6">
              <div class="relative flex items-center justify-center w-2.5 h-2.5">
                <span class="pulse-ring" style="inset:-1px;position:absolute;"></span>
                <span class="w-2.5 h-2.5 rounded-full bg-green-400 block relative z-10"></span>
              </div>
              <span class="font-mono text-xs" style="color:var(--text-mute);">Live & Deployed</span>
            </div>

            <h3 class="font-bebas text-5xl text-white leading-none mb-1 tracking-wide">The Spice Hub</h3>
            <p class="font-bebas text-xl glow-text tracking-wider mb-6">Luxury Digital Menu</p>

            <p class="font-outfit font-light text-sm leading-7 mb-8" style="color:var(--text-sub);">
              A full-stack premium web solution for an upscale restaurant — featuring an interactive digital menu, seamless WhatsApp ordering integration, animated hero, gallery, and reservation system. Designed to communicate luxury from the very first pixel, and built to drive orders directly through WhatsApp without friction.
            </p>

            <!-- Features list -->
            <div class="grid grid-cols-2 gap-3 mb-8">
              <div class="flex items-center gap-2 text-xs font-outfit" style="color:var(--text-sub);">
                <span class="w-1 h-1 rounded-full bg-purple-400"></span>WhatsApp ordering
              </div>
              <div class="flex items-center gap-2 text-xs font-outfit" style="color:var(--text-sub);">
                <span class="w-1 h-1 rounded-full bg-purple-400"></span>QR code menu
              </div>
              <div class="flex items-center gap-2 text-xs font-outfit" style="color:var(--text-sub);">
                <span class="w-1 h-1 rounded-full bg-purple-400"></span>Mobile-first design
              </div>
              <div class="flex items-center gap-2 text-xs font-outfit" style="color:var(--text-sub);">
                <span class="w-1 h-1 rounded-full bg-purple-400"></span>Gallery & reservations
              </div>
            </div>

            <!-- Tags -->
            <div class="flex flex-wrap gap-2 mb-10">
              <span class="tag px-3 py-1.5 rounded-full">HTML5</span>
              <span class="tag px-3 py-1.5 rounded-full">Tailwind CSS</span>
              <span class="tag px-3 py-1.5 rounded-full">JavaScript</span>
              <span class="tag px-3 py-1.5 rounded-full">AI-Driven</span>
              <span class="tag px-3 py-1.5 rounded-full">WhatsApp API</span>
            </div>
          </div>

          <div class="flex flex-wrap gap-3">
            <a href="#" class="glow-btn text-white font-outfit font-semibold px-7 py-3 rounded-full text-sm flex items-center gap-2">
              View Project
              <svg class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2"><path stroke-linecap="round" stroke-linejoin="round" d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"/></svg>
            </a>
            <a href="#" class="outline-btn text-white font-outfit font-semibold px-7 py-3 rounded-full text-sm">
              Case Study
            </a>
          </div>
        </div>
      </div>
    </div>

    <!-- More work note -->
    <div class="reveal mt-8 text-center">
      <p class="font-mono text-xs" style="color:var(--text-mute);">More projects available on request —
        <a href="#contact" class="glow-text hover:underline ml-1">reach out to see the full portfolio →</a>
      </p>
    </div>
  </div>
</section>

<div class="accent-line"></div>


<!-- ═══════════════════════════════════════════════════
     TECH STACK
═══════════════════════════════════════════════════ -->
<section id="stack" class="py-28 px-6 md:px-16 relative overflow-hidden">
  <div class="orb w-80 h-80 opacity-8 top-1/2 -right-20 -translate-y-1/2" style="background:var(--purple-dim);"></div>

  <div class="max-w-7xl mx-auto">
    <!-- Header -->
    <div class="reveal mb-20 text-center">
      <span class="font-mono text-xs glow-text tracking-widest uppercase">— Tech Stack</span>
      <h2 class="font-bebas text-6xl md:text-7xl text-white mt-3 leading-none">Tools of the Craft</h2>
      <p class="font-outfit font-light text-base mt-4 max-w-md mx-auto" style="color:var(--text-sub);">The weapons I use to build extraordinary digital products, fast.</p>
    </div>

    <!-- 4-column stack grid -->
    <div class="grid grid-cols-2 md:grid-cols-4 gap-5">

      <!-- HTML5 -->
      <div class="reveal tech-pill rounded-2xl p-8 text-center cursor-pointer group">
        <div class="text-5xl mb-5 transition-transform group-hover:scale-110 duration-300">🌐</div>
        <div class="font-bebas text-2xl text-white tracking-wider">HTML5</div>
        <div class="font-mono text-xs mt-2" style="color:var(--text-mute);">Semantic & Accessible</div>
        <div class="mt-4 rounded-full overflow-hidden" style="background:rgba(255,255,255,0.05); height:2px;">
          <div class="h-full rounded-full" style="width:96%; background:linear-gradient(90deg, var(--purple), var(--purple-2));"></div>
        </div>
        <div class="font-mono text-xs glow-text mt-1">96%</div>
      </div>

      <!-- Tailwind -->
      <div class="reveal tech-pill rounded-2xl p-8 text-center cursor-pointer group">
        <div class="text-5xl mb-5 transition-transform group-hover:scale-110 duration-300">🎨</div>
        <div class="font-bebas text-2xl text-white tracking-wider">Tailwind CSS</div>
        <div class="font-mono text-xs mt-2" style="color:var(--text-mute);">Utility-First Styling</div>
        <div class="mt-4 rounded-full overflow-hidden" style="background:rgba(255,255,255,0.05); height:2px;">
          <div class="h-full rounded-full" style="width:93%; background:linear-gradient(90deg, var(--purple), var(--purple-2));"></div>
        </div>
        <div class="font-mono text-xs glow-text mt-1">93%</div>
      </div>

      <!-- JavaScript -->
      <div class="reveal tech-pill rounded-2xl p-8 text-center cursor-pointer group">
        <div class="text-5xl mb-5 transition-transform group-hover:scale-110 duration-300">⚡</div>
        <div class="font-bebas text-2xl text-white tracking-wider">JavaScript</div>
        <div class="font-mono text-xs mt-2" style="color:var(--text-mute);">Dynamic & Interactive</div>
        <div class="mt-4 rounded-full overflow-hidden" style="background:rgba(255,255,255,0.05); height:2px;">
          <div class="h-full rounded-full" style="width:88%; background:linear-gradient(90deg, var(--purple), var(--purple-2));"></div>
        </div>
        <div class="font-mono text-xs glow-text mt-1">88%</div>
      </div>

      <!-- AI-Driven -->
      <div class="reveal rounded-2xl p-8 text-center cursor-pointer group relative overflow-hidden" style="background:linear-gradient(145deg,rgba(155,24,232,0.18),var(--bg-card)); border:1px solid rgba(196,77,255,0.35);">
        <div class="absolute top-0 left-0 right-0 h-px" style="background:linear-gradient(90deg, transparent, var(--purple), transparent);"></div>
        <div class="text-5xl mb-5 transition-transform group-hover:scale-110 duration-300 relative z-10">🤖</div>
        <div class="font-bebas text-2xl text-white tracking-wider relative z-10">AI-Driven Dev</div>
        <div class="font-mono text-xs mt-2 relative z-10" style="color:var(--text-mute);">Claude & GPT Powered</div>
        <div class="mt-4 rounded-full overflow-hidden relative z-10" style="background:rgba(255,255,255,0.05); height:2px;">
          <div class="h-full rounded-full" style="width:99%; background:linear-gradient(90deg, var(--purple), var(--purple-2));"></div>
        </div>
        <div class="font-mono text-xs glow-text mt-1 relative z-10">∞</div>
      </div>
    </div>
  </div>
</section>

<div class="accent-line"></div>


<!-- ═══════════════════════════════════════════════════
     CONTACT
═══════════════════════════════════════════════════ -->
<section id="contact" class="py-28 px-6 md:px-16 relative overflow-hidden">
  <div class="orb w-[700px] h-[700px] opacity-[0.08] top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2" style="background:var(--purple-2); filter:blur(120px);"></div>
  <!-- Grid bg for contact -->
  <div class="absolute inset-0 opacity-[0.03]" style="background-image: radial-gradient(circle, rgba(196,77,255,1) 1px, transparent 1px); background-size:40px 40px;"></div>

  <div class="max-w-4xl mx-auto text-center relative z-10">
    <div class="reveal">
      <span class="font-mono text-xs glow-text tracking-widest uppercase">— Get In Touch</span>
      <h2 class="font-bebas text-6xl md:text-8xl text-white mt-3 leading-none mb-6">
        Let's Build<br/>Something <span class="glow-text">Great</span>
      </h2>
      <p class="font-outfit font-light text-lg leading-relaxed mb-12 max-w-2xl mx-auto" style="color:var(--text-sub);">
        Have a project, idea, or just want to say hi? I'm currently accepting new clients. Let's turn your vision into a digital masterpiece — fast, premium, and built to grow.
      </p>

      <!-- Buttons -->
      <div class="flex flex-col sm:flex-row gap-4 justify-center mb-14">

        <!-- WhatsApp -->
        <a
          href="https://wa.me/91XXXXXXXXXX"
          target="_blank"
          rel="noopener"
          class="glow-btn text-white font-outfit font-semibold px-10 py-5 rounded-full text-base flex items-center justify-center gap-3 group"
        >
          <svg class="w-5 h-5 transition-transform group-hover:scale-110" fill="currentColor" viewBox="0 0 24 24">
            <path d="M17.472 14.382c-.297-.149-1.758-.867-2.03-.967-.273-.099-.471-.148-.67.15-.197.297-.767.966-.94 1.164-.173.199-.347.223-.644.075-.297-.15-1.255-.463-2.39-1.475-.883-.788-1.48-1.761-1.653-2.059-.173-.297-.018-.458.13-.606.134-.133.298-.347.446-.52.149-.174.198-.298.298-.497.099-.198.05-.371-.025-.52-.075-.149-.669-1.612-.916-2.207-.242-.579-.487-.5-.669-.51-.173-.008-.371-.01-.57-.01-.198 0-.52.074-.792.372-.272.297-1.04 1.016-1.04 2.479 0 1.462 1.065 2.875 1.213 3.074.149.198 2.096 3.2 5.077 4.487.709.306 1.262.489 1.694.625.712.227 1.36.195 1.871.118.571-.085 1.758-.719 2.006-1.413.248-.694.248-1.289.173-1.413-.074-.124-.272-.198-.57-.347m-5.421 7.403h-.004a9.87 9.87 0 01-5.031-1.378l-.361-.214-3.741.982.998-3.648-.235-.374a9.86 9.86 0 01-1.51-5.26c.001-5.45 4.436-9.884 9.888-9.884 2.64 0 5.122 1.03 6.988 2.898a9.825 9.825 0 012.893 6.994c-.003 5.45-4.437 9.884-9.885 9.884m8.413-18.297A11.815 11.815 0 0012.05 0C5.495 0 .16 5.335.157 11.892c0 2.096.547 4.142 1.588 5.945L.057 24l6.305-1.654a11.882 11.882 0 005.683 1.448h.005c6.554 0 11.89-5.335 11.893-11.893a11.821 11.821 0 00-3.48-8.413z"/>
          </svg>
          WhatsApp Me
        </a>

        <!-- Email -->
        <a
          href="mailto:hello@sesav.dev"
          class="outline-btn text-white font-outfit font-semibold px-10 py-5 rounded-full text-base flex items-center justify-center gap-3 group"
        >
          <svg class="w-5 h-5 transition-transform group-hover:scale-110" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
            <path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/>
          </svg>
          Send an Email
        </a>
      </div>

      <!-- Trust signals -->
      <div class="flex flex-col sm:flex-row gap-4 justify-center">
        <div class="glow-border rounded-2xl px-6 py-4 inline-flex items-center gap-3" style="background:var(--bg-card);">
          <span class="text-xl">⚡</span>
          <div class="text-left">
            <div class="font-outfit font-semibold text-white text-sm">Fast Response</div>
            <div class="font-mono text-xs" style="color:var(--text-mute);">Within 24 hours</div>
          </div>
        </div>
        <div class="glow-border rounded-2xl px-6 py-4 inline-flex items-center gap-3" style="background:var(--bg-card);">
          <span class="text-xl">🔒</span>
          <div class="text-left">
            <div class="font-outfit font-semibold text-white text-sm">100% Committed</div>
            <div class="font-mono text-xs" style="color:var(--text-mute);">Your success = My goal</div>
          </div>
        </div>
        <div class="glow-border rounded-2xl px-6 py-4 inline-flex items-center gap-3" style="background:var(--bg-card);">
          <span class="text-xl">🤝</span>
          <div class="text-left">
            <div class="font-outfit font-semibold text-white text-sm">Fresh & Innovative</div>
            <div class="font-mono text-xs" style="color:var(--text-mute);">AI-powered approach</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</section>


<!-- ═══════════════════════════════════════════════════
     FOOTER
═══════════════════════════════════════════════════ -->
<footer style="border-top:1px solid rgba(255,255,255,0.04);" class="py-8 px-6 md:px-16">
  <div class="max-w-7xl mx-auto flex flex-col md:flex-row items-center justify-between gap-4">
    <div class="flex items-center gap-3">
      <div class="w-7 h-7 rounded-lg flex items-center justify-center glow-btn text-xs font-bebas text-white">S</div>
      <span class="font-bebas text-xl tracking-widest text-white">SESAV</span>
    </div>
    <p class="font-mono text-xs" style="color:var(--text-mute);">© 2025 SESAV · Crafted with 💜 &amp; Electric Obsession</p>
    <a href="#hero" class="font-mono text-xs flex items-center gap-2 hover:glow-text transition-colors" style="color:var(--text-mute);">
      Back to top ↑
    </a>
  </div>
</footer>


<!-- ═══════════════════════════════════════════════════
     SCRIPTS
═══════════════════════════════════════════════════ -->
<script>
  /* ── CURSOR ─────────────────────────────────────────── */
  const cursor = document.getElementById('cursor');
  const ring   = document.getElementById('cursor-ring');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top  = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top  = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  /* Cursor hide on mobile */
  if ('ontouchstart' in window) {
    cursor.style.display = 'none';
    ring.style.display = 'none';
    document.body.style.cursor = 'auto';
  }

  /* ── MOBILE NAV ──────────────────────────────────────── */
  function toggleMob() {
    const m  = document.getElementById('mob-menu');
    const h1 = document.getElementById('h1');
    const h2 = document.getElementById('h2');
    const h3 = document.getElementById('h3');
    const open = m.classList.toggle('open');
    h1.style.transform = open ? 'translateY(6px) rotate(45deg)' : '';
    h2.style.opacity   = open ? '0' : '1';
    h3.style.transform = open ? 'translateY(-6px) rotate(-45deg)' : '';
  }

  /* Close mobile menu on link click */
  document.querySelectorAll('#mob-menu a').forEach(a => {
    a.addEventListener('click', () => {
      const m = document.getElementById('mob-menu');
      m.classList.remove('open');
    });
  });

  /* ── SCROLL REVEAL ───────────────────────────────────── */
  const io = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        entry.target.style.transitionDelay = (entry.target.dataset.delay || 0) + 'ms';
        entry.target.classList.add('in');
        io.unobserve(entry.target);
      }
    });
  }, { threshold: 0.1, rootMargin: '0px 0px -40px 0px' });

  document.querySelectorAll('.reveal').forEach((el, i) => {
    el.dataset.delay = (i % 4) * 90;
    io.observe(el);
  });

  /* ── SERVICE CARD MOUSE GLOW ─────────────────────────── */
  document.querySelectorAll('.service-card').forEach(card => {
    card.addEventListener('mousemove', e => {
      const r = card.getBoundingClientRect();
      card.style.setProperty('--mx', ((e.clientX - r.left) / r.width  * 100) + '%');
      card.style.setProperty('--my', ((e.clientY - r.top)  / r.height * 100) + '%');
    });
  });

  /* ── MARQUEE DUPLICATION ─────────────────────────────── */
  const tpl   = document.getElementById('marquee-tpl');
  const inner = document.querySelector('.marquee-inner');
  if (tpl && inner) {
    const clone = tpl.content.cloneNode(true);
    const clone2 = tpl.content.cloneNode(true);
    inner.appendChild(clone);
    inner.appendChild(clone2);
  }

  /* ── SMOOTH SCROLL ───────────────────────────────────── */
  document.querySelectorAll('a[href^="#"]').forEach(a => {
    a.addEventListener('click', e => {
      const target = document.querySelector(a.getAttribute('href'));
      if (target) {
        e.preventDefault();
        target.scrollIntoView({ behavior: 'smooth', block: 'start' });
      }
    });
  });

  /* ── PARALLAX ORBS ───────────────────────────────────── */
  document.addEventListener('mousemove', e => {
    const orbs = document.querySelectorAll('.orb');
    orbs.forEach((orb, i) => {
      const speed = (i % 3 + 1) * 0.006;
      const ox = (e.clientX - window.innerWidth  / 2) * speed;
      const oy = (e.clientY - window.innerHeight / 2) * speed;
      orb.style.transform = `translate(${ox}px, ${oy}px)`;
    });
  });
</script>
</body>
</html>
