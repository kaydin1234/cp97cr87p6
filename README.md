#<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Flavor of Heaven — American Cafe</title>
<link href="https://fonts.googleapis.com/css2?family=Playfair+Display:ital,wght@0,400;0,700;0,900;1,400&family=Russo+One&family=Bebas+Neue&family=Oswald:wght@400;700&display=swap" rel="stylesheet">
<style>
  :root {
    --navy: #1B2A4A;
    --crimson: #C41E3A;
    --cream: #FFF8E7;
    --gold: #D4A843;
    --gold-light: #F0D078;
    --brown: #5C3317;
    --warm-white: #FFFDF5;
    --deep-red: #8B1A2B;
  }

  * { margin: 0; padding: 0; box-sizing: border-box; }

  body {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    background: var(--navy);
    overflow: hidden;
    font-family: 'Oswald', sans-serif;
  }

  /* Checkerboard background */
  .bg-pattern {
    position: fixed;
    inset: 0;
    z-index: 0;
    opacity: 0.06;
    background-image:
      linear-gradient(45deg, #fff 25%, transparent 25%),
      linear-gradient(-45deg, #fff 25%, transparent 25%),
      linear-gradient(45deg, transparent 75%, #fff 75%),
      linear-gradient(-45deg, transparent 75%, #fff 75%);
    background-size: 40px 40px;
    background-position: 0 0, 0 20px, 20px -20px, -20px 0px;
  }

  /* Ambient glow */
  .ambient-glow {
    position: fixed;
    z-index: 0;
    border-radius: 50%;
    filter: blur(120px);
    pointer-events: none;
  }
  .glow-1 {
    width: 600px; height: 600px;
    background: radial-gradient(circle, rgba(196,30,58,0.25), transparent 70%);
    top: -10%; left: -10%;
    animation: floatGlow 8s ease-in-out infinite;
  }
  .glow-2 {
    width: 500px; height: 500px;
    background: radial-gradient(circle, rgba(212,168,67,0.2), transparent 70%);
    bottom: -10%; right: -10%;
    animation: floatGlow 10s ease-in-out infinite reverse;
  }
  .glow-3 {
    width: 400px; height: 400px;
    background: radial-gradient(circle, rgba(196,30,58,0.15), transparent 70%);
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    animation: pulseGlow 4s ease-in-out infinite;
  }

  @keyframes floatGlow {
    0%, 100% { transform: translate(0, 0); }
    50% { transform: translate(30px, -20px); }
  }
  @keyframes pulseGlow {
    0%, 100% { opacity: 0.5; transform: translate(-50%, -50%) scale(1); }
    50% { opacity: 1; transform: translate(-50%, -50%) scale(1.1); }
  }

  /* Main logo container */
  .logo-showcase {
    position: relative;
    z-index: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 40px;
    padding: 20px;
  }

  /* SVG Logo */
  .logo-svg {
    width: min(90vw, 600px);
    height: auto;
    filter: drop-shadow(0 8px 30px rgba(0,0,0,0.5));
    animation: logoEntrance 1.2s cubic-bezier(0.16, 1, 0.3, 1) both;
  }

  @keyframes logoEntrance {
    0% { opacity: 0; transform: scale(0.7) translateY(30px); }
    100% { opacity: 1; transform: scale(1) translateY(0); }
  }

  /* Rotating outer ring */
  .ring-rotate {
    animation: rotateRing 60s linear infinite;
    transform-origin: 300px 300px;
  }
  @keyframes rotateRing {
    from { transform: rotate(0deg); }
    to { transform: rotate(360deg); }
  }

  /* Star twinkle */
  .star-twinkle {
    animation: twinkle 2s ease-in-out infinite;
  }
  .star-twinkle:nth-child(2) { animation-delay: 0.3s; }
  .star-twinkle:nth-child(3) { animation-delay: 0.6s; }
  .star-twinkle:nth-child(4) { animation-delay: 0.9s; }
  .star-twinkle:nth-child(5) { animation-delay: 1.2s; }

  @keyframes twinkle {
    0%, 100% { opacity: 1; }
    50% { opacity: 0.4; }
  }

  /* Steam animation */
  .steam {
    animation: steamRise 2.5s ease-out infinite;
    opacity: 0;
  }
  .steam:nth-child(1) { animation-delay: 0s; }
  .steam:nth-child(2) { animation-delay: 0.8s; }
  .steam:nth-child(3) { animation-delay: 1.6s; }

  @keyframes steamRise {
    0% { opacity: 0; transform: translateY(0) scaleX(1); }
    20% { opacity: 0.7; }
    60% { opacity: 0.3; transform: translateY(-30px) scaleX(1.3); }
    100% { opacity: 0; transform: translateY(-55px) scaleX(0.8); }
  }

  /* Banner text glow pulse */
  .banner-text-glow {
    animation: textGlow 3s ease-in-out infinite;
  }
  @keyframes textGlow {
    0%, 100% { filter: drop-shadow(0 0 2px rgba(212,168,67,0.3)); }
    50% { filter: drop-shadow(0 0 8px rgba(212,168,67,0.7)); }
  }

  /* Badge shine sweep */
  .badge-shine {
    animation: shineSweep 4s ease-in-out infinite;
  }
  @keyframes shineSweep {
    0%, 70%, 100% { opacity: 0; }
    30% { opacity: 0.3; }
  }

  /* Tagline area */
  .tagline-area {
    text-align: center;
    animation: fadeUp 1s 0.6s cubic-bezier(0.16, 1, 0.3, 1) both;
  }
  .tagline-area p {
    font-family: 'Oswald', sans-serif;
    color: var(--gold);
    font-size: clamp(14px, 2.5vw, 20px);
    letter-spacing: 6px;
    text-transform: uppercase;
    opacity: 0.7;
  }

  @keyframes fadeUp {
    0% { opacity: 0; transform: translateY(20px); }
    100% { opacity: 1; transform: translateY(0); }
  }

  /* Variant showcase */
  .variants {
    display: flex;
    gap: 40px;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 20px;
    animation: fadeUp 1s 1s cubic-bezier(0.16, 1, 0.3, 1) both;
  }
  .variant-card {
    background: rgba(255,255,255,0.03);
    border: 1px solid rgba(212,168,67,0.15);
    border-radius: 16px;
    padding: 30px;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 12px;
    transition: all 0.3s ease;
    cursor: pointer;
    backdrop-filter: blur(10px);
  }
  .variant-card:hover {
    border-color: rgba(212,168,67,0.5);
    background: rgba(255,255,255,0.06);
    transform: translateY(-4px);
    box-shadow: 0 12px 40px rgba(0,0,0,0.3);
  }
  .variant-card .label {
    font-family: 'Oswald', sans-serif;
    color: var(--gold);
    font-size: 13px;
    letter-spacing: 3px;
    text-transform: uppercase;
    opacity: 0.6;
  }
  .variant-card svg {
    width: 140px;
    height: 140px;
  }

  /* Floating particles */
  .particle {
    position: fixed;
    z-index: 0;
    width: 3px;
    height: 3px;
    border-radius: 50%;
    background: var(--gold);
    opacity: 0;
    pointer-events: none;
    animation: particleFloat linear infinite;
  }

  @keyframes particleFloat {
    0% { opacity: 0; transform: translateY(100vh) rotate(0deg); }
    10% { opacity: 0.6; }
    90% { opacity: 0.3; }
    100% { opacity: 0; transform: translateY(-10vh) rotate(360deg); }
  }

  /* Responsive */
  @media (max-width: 600px) {
    .variants { gap: 20px; }
    .variant-card { padding: 20px; }
    .variant-card svg { width: 100px; height: 100px; }
  }

  @media (prefers-reduced-motion: reduce) {
    *, *::before, *::after {
      animation-duration: 0.01ms !important;
      animation-iteration-count: 1 !important;
      transition-duration: 0.01ms !important;
    }
  }
</style>
</head>
<body>

<div class="bg-pattern"></div>
<div class="ambient-glow glow-1"></div>
<div class="ambient-glow glow-2"></div>
<div class="ambient-glow glow-3"></div>

<!-- Floating particles -->
<div id="particles"></div>

<div class="logo-showcase">

  <!-- Main Logo SVG -->
  <svg class="logo-svg" viewBox="0 0 600 600" xmlns="http://www.w3.org/2000/svg">
    <defs>
      <!-- Crimson gradient -->
      <radialGradient id="bgGrad" cx="50%" cy="45%" r="55%">
        <stop offset="0%" stop-color="#D4293E"/>
        <stop offset="70%" stop-color="#C41E3A"/>
        <stop offset="100%" stop-color="#8B1A2B"/>
      </radialGradient>

      <!-- Gold gradient -->
      <linearGradient id="goldGrad" x1="0%" y1="0%" x2="100%" y2="100%">
        <stop offset="0%" stop-color="#F0D078"/>
        <stop offset="50%" stop-color="#D4A843"/>
        <stop offset="100%" stop-color="#B8912E"/>
      </linearGradient>

      <!-- Gold rim gradient -->
      <linearGradient id="rimGrad" x1="0%" y1="0%" x2="0%" y2="100%">
        <stop offset="0%" stop-color="#F0D078"/>
        <stop offset="30%" stop-color="#D4A843"/>
        <stop offset="70%" stop-color="#B8912E"/>
        <stop offset="100%" stop-color="#F0D078"/>
      </linearGradient>

      <!-- Navy gradient -->
      <radialGradient id="navyGrad" cx="50%" cy="50%" r="50%">
        <stop offset="0%" stop-color="#2A3F6E"/>
        <stop offset="100%" stop-color="#1B2A4A"/>
      </radialGradient>

      <!-- Shine sweep -->
      <linearGradient id="shineGrad" x1="0%" y1="0%" x2="100%" y2="0%">
        <stop offset="0%" stop-color="rgba(255,255,255,0)" />
        <stop offset="50%" stop-color="rgba(255,255,255,0.4)" />
        <stop offset="100%" stop-color="rgba(255,255,255,0)" />
      </linearGradient>

      <!-- Drop shadow filter -->
      <filter id="shadow" x="-10%" y="-10%" width="130%" height="130%">
        <feDropShadow dx="0" dy="3" stdDeviation="4" flood-color="#000" flood-opacity="0.4"/>
      </filter>

      <filter id="innerShadow" x="-5%" y="-5%" width="110%" height="110%">
        <feDropShadow dx="0" dy="1" stdDeviation="2" flood-color="#000" flood-opacity="0.3"/>
      </filter>

      <!-- Text arc path -->
      <path id="topArc" d="M 100,300 A 200,200 0 0,1 500,300" fill="none"/>
      <path id="bottomArc" d="M 110,320 A 190,190 0 0,0 490,320" fill="none"/>

      <!-- Clip for shine -->
      <clipPath id="badgeClip">
        <circle cx="300" cy="280" r="185"/>
      </clipPath>
    </defs>

    <!-- Outer gold ring -->
    <circle cx="300" cy="280" r="240" fill="none" stroke="url(#rimGrad)" stroke-width="6" opacity="0.8"/>

    <!-- Decorative dashed outer ring that rotates -->
    <g class="ring-rotate" opacity="0.3">
      <circle cx="300" cy="280" r="250" fill="none" stroke="url(#goldGrad)" stroke-width="1" stroke-dasharray="4 12"/>
    </g>

    <!-- Small decorative dots around rim -->
    <g opacity="0.5">
      <circle cx="300" cy="36" r="2.5" fill="#D4A843"/>
      <circle cx="380" cy="46" r="2" fill="#D4A843"/>
      <circle cx="220" cy="46" r="2" fill="#D4A843"/>
      <circle cx="450" cy="80" r="2.5" fill="#D4A843"/>
      <circle cx="150" cy="80" r="2.5" fill="#D4A843"/>
      <circle cx="510" cy="140" r="2" fill="#D4A843"/>
      <circle cx="90" cy="140" r="2" fill="#D4A843"/>
      <circle cx="540" cy="210" r="2.5" fill="#D4A843"/>
      <circle cx="60" cy="210" r="2.5" fill="#D4A843"/>
      <circle cx="544" cy="280" r="2" fill="#D4A843"/>
      <circle cx="56" cy="280" r="2" fill="#D4A843"/>
      <circle cx="540" cy="350" r="2.5" fill="#D4A843"/>
      <circle cx="60" cy="350" r="2.5" fill="#D4A843"/>
      <circle cx="510" cy="420" r="2" fill="#D4A843"/>
      <circle cx="90" cy="420" r="2" fill="#D4A843"/>
      <circle cx="450" cy="480" r="2.5" fill="#D4A843"/>
      <circle cx="150" cy="480" r="2.5" fill="#D4A843"/>
      <circle cx="380" cy="514" r="2" fill="#D4A843"/>
      <circle cx="220" cy="514" r="2" fill="#D4A843"/>
    </g>

    <!-- Main badge circle - Navy background -->
    <circle cx="300" cy="280" r="215" fill="url(#navyGrad)" stroke="url(#rimGrad)" stroke-width="4"/>

    <!-- Inner crimson ring -->
    <circle cx="300" cy="280" r="195" fill="none" stroke="#C41E3A" stroke-width="2" opacity="0.6"/>

    <!-- Crimson banner area -->
    <ellipse cx="300" cy="280" rx="185" ry="185" fill="url(#bgGrad)" opacity="0.15"/>

    <!-- Stars along the top - left side -->
    <g class="star-twinkle">
      <polygon points="155,135 158,143 167,143 160,148 163,157 155,152 147,157 150,148 143,143 152,143" fill="#D4A843"/>
    </g>
    <g class="star-twinkle">
      <polygon points="200,100 202,107 210,107 204,111 206,118 200,114 194,118 196,111 190,107 198,107" fill="#D4A843"/>
    </g>
    <g class="star-twinkle">
      <polygon points="250,82 252,89 260,89 254,93 256,100 250,96 244,100 246,93 240,89 248,89" fill="#D4A843"/>
    </g>
    <g class="star-twinkle">
      <polygon points="350,82 352,89 360,89 354,93 356,100 350,96 344,100 346,93 340,89 348,89" fill="#D4A843"/>
    </g>
    <g class="star-twinkle">
      <polygon points="400,100 402,107 410,107 404,111 406,118 400,114 394,118 396,111 390,107 398,107" fill="#D4A843"/>
    </g>
    <g class="star-twinkle">
      <polygon points="445,135 448,143 457,143 450,148 453,157 445,152 437,157 440,148 433,143 442,143" fill="#D4A843"/>
    </g>

    <!-- Curved top text: FLAVOR -->
    <text filter="url(#shadow)" font-family="'Bebas Neue', sans-serif" font-size="52" fill="url(#goldGrad)" letter-spacing="14">
      <textPath href="#topArc" startOffset="50%" text-anchor="middle">FLAVOR</textPath>
    </text>

    <!-- Curved bottom text: OF HEAVEN -->
    <text filter="url(#shadow)" font-family="'Bebas Neue', sans-serif" font-size="36" fill="url(#goldGrad)" letter-spacing="8">
      <textPath href="#bottomArc" startOffset="50%" text-anchor="middle">OF HEAVEN</textPath>
    </text>

    <!-- Center emblem - Coffee cup -->
    <g transform="translate(300, 290)" filter="url(#shadow)">
      <!-- Cup body -->
      <path d="M -45,0 L -38,-55 L 38,-55 L 45,0 Z" fill="url(#goldGrad)" stroke="#B8912E" stroke-width="1.5"/>
      <!-- Cup rim -->
      <ellipse cx="0" cy="-55" rx="40" ry="8" fill="#F0D078" stroke="#B8912E" stroke-width="1"/>
      <!-- Cup bottom -->
      <ellipse cx="0" cy="0" rx="46" ry="6" fill="#B8912E" opacity="0.5"/>

      <!-- Saucer -->
      <ellipse cx="0" cy="8" rx="60" ry="10" fill="none" stroke="url(#goldGrad)" stroke-width="2.5"/>

      <!-- Handle -->
      <path d="M 45,-40 C 70,-40 70,-10 45,-10" fill="none" stroke="url(#goldGrad)" stroke-width="4" stroke-linecap="round"/>

      <!-- Coffee liquid -->
      <ellipse cx="0" cy="-52" rx="33" ry="5" fill="#5C3317" opacity="0.7"/>

      <!-- Steam lines -->
      <g>
        <path class="steam" d="M -12,-68 C -15,-80 -8,-88 -12,-100" fill="none" stroke="#FFF8E7" stroke-width="2" stroke-linecap="round" opacity="0"/>
        <path class="steam" d="M 2,-68 C -1,-82 6,-90 2,-102" fill="none" stroke="#FFF8E7" stroke-width="2" stroke-linecap="round" opacity="0"/>
        <path class="steam" d="M 16,-68 C 13,-80 20,-88 16,-100" fill="none" stroke="#FFF8E7" stroke-width="2" stroke-linecap="round" opacity="0"/>
      </g>
    </g>

    <!-- Decorative wings left -->
    <g transform="translate(120, 290)" opacity="0.7">
      <path d="M 0,0 C -20,-30 -60,-50 -80,-35 C -60,-25 -40,-10 -30,5 C -40,-5 -65,-15 -80,-5 C -55,10 -30,20 -15,25 Z" fill="url(#goldGrad)"/>
    </g>

    <!-- Decorative wings right -->
    <g transform="translate(480, 290)" opacity="0.7">
      <path d="M 0,0 C 20,-30 60,-50 80,-35 C 60,-25 40,-10 30,5 C 40,-5 65,-15 80,-5 C 55,10 30,20 15,25 Z" fill="url(#goldGrad)"/>
    </g>

    <!-- EST. text -->
    <text x="300" y="400" text-anchor="middle" font-family="'Oswald', sans-serif" font-size="14" fill="url(#goldGrad)" letter-spacing="4" opacity="0.8">EST. 2024</text>

    <!-- Decorative line separators -->
    <line x1="220" y1="408" x2="260" y2="408" stroke="url(#goldGrad)" stroke-width="1" opacity="0.5"/>
    <line x1="340" y1="408" x2="380" y2="408" stroke="url(#goldGrad)" stroke-width="1" opacity="0.5"/>
    <circle cx="300" cy="408" r="2" fill="#D4A843" opacity="0.5"/>

    <!-- American diner sub-text -->
    <text x="300" y="435" text-anchor="middle" font-family="'Oswald', sans-serif" font-size="16" fill="#FFF8E7" letter-spacing="6" opacity="0.6">AMERICAN CAFE</text>

    <!-- Shine sweep effect -->
    <g clip-path="url(#badgeClip)" class="badge-shine">
      <rect x="-200" y="80" width="120" height="400" fill="url(#shineGrad)" transform="rotate(-25, 300, 280)">
        <animate attributeName="x" from="-200" to="600" dur="4s" repeatCount="indefinite"/>
      </rect>
    </g>

    <!-- Bottom star cluster -->
    <g transform="translate(300, 465)">
      <polygon points="0,-10 3,-3 10,-3 4,2 6,10 0,5 -6,10 -4,2 -10,-3 -3,-3" fill="#D4A843" opacity="0.7"/>
    </g>

    <!-- Laurel left -->
    <g transform="translate(200, 440)" opacity="0.4">
      <path d="M 0,0 C 5,-15 15,-25 10,-40 C 5,-25 -5,-20 0,0" fill="#D4A843"/>
      <path d="M 8,5 C 15,-10 25,-18 22,-33 C 15,-18 5,-15 8,5" fill="#D4A843"/>
      <path d="M 14,12 C 22,-2 32,-8 30,-23 C 22,-8 12,-5 14,12" fill="#D4A843"/>
    </g>

    <!-- Laurel right -->
    <g transform="translate(400, 440)" opacity="0.4">
      <path d="M 0,0 C -5,-15 -15,-25 -10,-40 C -5,-25 5,-20 0,0" fill="#D4A843"/>
      <path d="M -8,5 C -15,-10 -25,-18 -22,-33 C -15,-18 -5,-15 -8,5" fill="#D4A843"/>
      <path d="M -14,12 C -22,-2 -32,-8 -30,-23 C -22,-8 -12,-5 -14,12" fill="#D4A843"/>
    </g>

  </svg>

  <!-- Tagline -->
  <div class="tagline-area">
    <p>Where Every Bite Is Divine</p>
  </div>

  <!-- Logo Variants -->
  <div class="variants">
    <!-- Minimal variant -->
    <div class="variant-card" id="variantDark">
      <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <linearGradient id="goldGrad2" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stop-color="#F0D078"/>
            <stop offset="100%" stop-color="#D4A843"/>
          </linearGradient>
        </defs>
        <circle cx="100" cy="100" r="90" fill="#1B2A4A" stroke="url(#goldGrad2)" stroke-width="3"/>
        <text x="100" y="82" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="24" fill="url(#goldGrad2)" letter-spacing="4">FLAVOR</text>
        <text x="100" y="108" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="14" fill="url(#goldGrad2)" letter-spacing="3">OF HEAVEN</text>
        <line x1="55" y1="118" x2="145" y2="118" stroke="#D4A843" stroke-width="0.5" opacity="0.5"/>
        <text x="100" y="135" text-anchor="middle" font-family="'Oswald', sans-serif" font-size="8" fill="#FFF8E7" letter-spacing="3" opacity="0.6">AMERICAN CAFE</text>
        <path d="M 88,145 L 92,140 L 96,145 L 100,138 L 104,145 L 108,140 L 112,145" fill="none" stroke="#D4A843" stroke-width="1" opacity="0.5"/>
      </svg>
      <span class="label">Badge</span>
    </div>

    <!-- Light variant -->
    <div class="variant-card" id="variantLight">
      <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
        <defs>
          <linearGradient id="crimsonGrad" x1="0%" y1="0%" x2="100%" y2="100%">
            <stop offset="0%" stop-color="#D4293E"/>
            <stop offset="100%" stop-color="#8B1A2B"/>
          </linearGradient>
        </defs>
        <circle cx="100" cy="100" r="90" fill="#FFF8E7" stroke="url(#crimsonGrad)" stroke-width="3"/>
        <circle cx="100" cy="100" r="82" fill="none" stroke="#C41E3A" stroke-width="0.5" opacity="0.3"/>
        <text x="100" y="82" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="24" fill="#C41E3A" letter-spacing="4">FLAVOR</text>
        <text x="100" y="108" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="14" fill="#1B2A4A" letter-spacing="3">OF HEAVEN</text>
        <line x1="55" y1="118" x2="145" y2="118" stroke="#C41E3A" stroke-width="0.5" opacity="0.4"/>
        <text x="100" y="135" text-anchor="middle" font-family="'Oswald', sans-serif" font-size="8" fill="#1B2A4A" letter-spacing="3" opacity="0.7">AMERICAN CAFE</text>
        <polygon points="100,145 103,152 110,152 104,156 106,163 100,159 94,163 96,156 90,152 97,152" fill="#C41E3A" opacity="0.6"/>
      </svg>
      <span class="label">Light</span>
    </div>

    <!-- Flat variant -->
    <div class="variant-card" id="variantFlat">
      <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
        <rect x="10" y="10" width="180" height="180" rx="12" fill="#C41E3A"/>
        <rect x="16" y="16" width="168" height="168" rx="8" fill="none" stroke="#FFF8E7" stroke-width="0.5" opacity="0.3"/>
        <text x="100" y="78" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="30" fill="#FFF8E7" letter-spacing="5">FLAVOR</text>
        <text x="100" y="100" text-anchor="middle" font-family="'Playfair Display', serif" font-size="12" fill="#F0D078" font-style="italic" letter-spacing="2">of</text>
        <text x="100" y="122" text-anchor="middle" font-family="'Bebas Neue', sans-serif" font-size="26" fill="#FFF8E7" letter-spacing="5">HEAVEN</text>
        <line x1="50" y1="134" x2="150" y2="134" stroke="#F0D078" stroke-width="1" opacity="0.6"/>
        <text x="100" y="155" text-anchor="middle" font-family="'Oswald', sans-serif" font-size="9" fill="#FFF8E7" letter-spacing="4" opacity="0.7">AMERICAN CAFE</text>
      </svg>
      <span class="label">Flat</span>
    </div>
  </div>

</div>

<script>
  // Create floating particles
  const particlesContainer = document.getElementById('particles');
  const particleCount = 25;

  for (let i = 0; i < particleCount; i++) {
    const particle = document.createElement('div');
    particle.classList.add('particle');
    particle.style.left = Math.random() * 100 + 'vw';
    particle.style.width = (Math.random() * 3 + 1) + 'px';
    particle.style.height = particle.style.width;
    particle.style.animationDuration = (Math.random() * 10 + 8) + 's';
    particle.style.animationDelay = (Math.random() * 10) + 's';
    particle.style.opacity = '0';
    // Alternate between gold and cream particles
    particle.style.background = Math.random() > 0.5 ? '#D4A843' : '#FFF8E7';
    particlesContainer.appendChild(particle);
  }

  // Add subtle parallax to logo on mouse move
  const logoSvg = document.querySelector('.logo-svg');
  document.addEventListener('mousemove', (e) => {
    const centerX = window.innerWidth / 2;
    const centerY = window.innerHeight / 2;
    const moveX = (e.clientX - centerX) / centerX * 5;
    const moveY = (e.clientY - centerY) / centerY * 5;

    logoSvg.style.transform = `perspective(1000px) rotateY(${moveX * 0.3}deg) rotateX(${-moveY * 0.3}deg)`;
  });

  document.addEventListener('mouseleave', () => {
    logoSvg.style.transform = 'perspective(1000px) rotateY(0deg) rotateX(0deg)';
  });

  // Variant cards click — download as PNG
  document.querySelectorAll('.variant-card').forEach(card => {
    card.addEventListener('click', () => {
      const svg = card.querySelector('svg');
      const label = card.querySelector('.label').textContent;

      // Serialize SVG to canvas and download
      const svgData = new XMLSerializer().serializeToString(svg);
      const canvas = document.createElement('canvas');
      canvas.width = 600;
      canvas.height = 600;
      const ctx = canvas.getContext('2d');
      const img = new Image();

      img.onload = () => {
        ctx.drawImage(img, 0, 0, 600, 600);
        const a = document.createElement('a');
        a.download = `flavor-of-heaven-${label.toLowerCase()}.png`;
        a.href = canvas.toDataURL('image/png');
        a.click();
      };

      img.src = 'data:image/svg+xml;base64,' + btoa(unescape(encodeURIComponent(svgData)));

      // Show inline toast
      showToast(`${label} variant downloaded!`);
    });
  });

  // Toast notification
  function showToast(message) {
    const existing = document.querySelector('.toast');
    if (existing) existing.remove();

    const toast = document.createElement('div');
    toast.className = 'toast';
    toast.textContent = message;
    Object.assign(toast.style, {
      position: 'fixed',
      bottom: '30px',
      left: '50%',
      transform: 'translateX(-50%) translateY(20px)',
      background: 'rgba(27,42,74,0.95)',
      color: '#F0D078',
      padding: '12px 28px',
      borderRadius: '8px',
      fontFamily: "'Oswald', sans-serif",
      fontSize: '14px',
      letterSpacing: '2px',
      textTransform: 'uppercase',
      border: '1px solid rgba(212,168,67,0.3)',
      zIndex: '100',
      opacity: '0',
      transition: 'all 0.4s cubic-bezier(0.16,1,0.3,1)',
      backdropFilter: 'blur(10px)',
    });
    document.body.appendChild(toast);

    requestAnimationFrame(() => {
      toast.style.opacity = '1';
      toast.style.transform = 'translateX(-50%) translateY(0)';
    });

    setTimeout(() => {
      toast.style.opacity = '0';
      toast.style.transform = 'translateX(-50%) translateY(20px)';
      setTimeout(() => toast.remove(), 400);
    }, 2500);
  }
</script>

</body>
</html>
