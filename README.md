<?xml version="1.0" encoding="UTF-8"?>
<svg width="980" height="160" viewBox="0 0 980 160" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink">
  <defs>
    <!-- Fundo -->
    <linearGradient id="bg" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0%" stop-color="#0a0f1f"/>
      <stop offset="100%" stop-color="#0d1226"/>
    </linearGradient>

    <!-- Dots -->
    <symbol id="dot" viewBox="0 0 8 8">
      <circle cx="4" cy="4" r="3" fill="#ffd54a"/>
    </symbol>

    <!-- Caminho zigue-zague (ida) -->
    <!-- Alterna entre Y=40, 80 e 120 enquanto avança no X -->
    <path id="track-forward" d="
      M40,40
      L180,40
      L180,80
      L320,80
      L320,120
      L460,120
      L460,40
      L600,40
      L600,120
      L740,120
      L740,80
      L920,80
    " fill="none" stroke="none"/>

    <!-- Caminho zigue-zague (volta) - exatamente o inverso -->
    <path id="track-backward" d="
      M920,80
      L740,80
      L740,120
      L600,120
      L600,40
      L460,40
      L460,120
      L320,120
      L320,80
      L180,80
      L180,40
      L40,40
    " fill="none" stroke="none"/>

    <!-- Pac-Man: fechado e aberto -->
    <g id="pacman-closed">
      <circle cx="0" cy="0" r="18" fill="#ffeb3b" stroke="#f5d10a" stroke-width="2"/>
      <circle cx="5" cy="-7" r="3" fill="#222"/>
    </g>
    <g id="pacman-open">
      <path d="M0,0 L18,0 A18,18 0 1 0 18,0 Z" fill="#ffeb3b" stroke="#f5d10a" stroke-width="2"/>
      <circle cx="5" cy="-7" r="3" fill="#222"/>
    </g>

    <!-- Clip da moldura/maze -->
    <clipPath id="maze-clip">
      <rect x="20" y="20" width="940" height="120" rx="14" ry="14"/>
      <rect x="180" y="20" width="16" height="120"/>
      <rect x="320" y="20" width="16" height="120"/>
      <rect x="460" y="20" width="16" height="120"/>
      <rect x="600" y="20" width="16" height="120"/>
      <rect x="740" y="20" width="16" height="120"/>
    </clipPath>
  </defs>

  <!-- Fundo -->
  <rect width="100%" height="100%" fill="url(#bg)"/>

  <!-- Moldura/maze -->
  <g clip-path="url(#maze-clip)">
    <rect x="20" y="20" width="940" height="120" rx="14" ry="14" fill="none" stroke="#2b3a8a" stroke-width="6"/>
    <g stroke="#2b3a8a" stroke-width="10" opacity="0.5">
      <line x1="188" y1="20" x2="188" y2="140"/>
      <line x1="328" y1="20" x2="328" y2="140"/>
      <line x1="468" y1="20" x2="468" y2="140"/>
      <line x1="608" y1="20" x2="608" y2="140"/>
      <line x1="748" y1="20" x2="748" y2="140"/>
    </g>
  </g>

  <!-- Dots distribuídos próximo ao caminho -->
  <g id="dots">
    <!-- Linha 1 (y=36) -->
    <use href="#dot" x="60"  y="36"/><use href="#dot" x="95" y="36"/><use href="#dot" x="130" y="36"/><use href="#dot" x="165" y="36"/>
    <!-- Segmento vertical 1 (x=180, y 48..76) -->
    <use href="#dot" x="176" y="56"/><use href="#dot" x="176" y="72"/>
    <!-- Linha 2 (y=76) -->
    <use href="#dot" x="200" y="76"/><use href="#dot" x="235" y="76"/><use href="#dot" x="270" y="76"/><use href="#dot" x="305" y="76"/>
    <!-- Vertical (x=320) -->
    <use href="#dot" x="316" y="92"/><use href="#dot" x="316" y="108"/>
    <!-- Linha 3 (y=116) -->
    <use href="#dot" x="340" y="116"/><use href="#dot" x="375" y="116"/><use href="#dot" x="410" y="116"/><use href="#dot" x="445" y="116"/>
    <!-- Vertical (x=460) -->
    <use href="#dot" x="456" y="100"/><use href="#dot" x="456" y="84"/>
    <!-- Linha 4 (y=36) -->
    <use href="#dot" x="480" y="36"/><use href="#dot" x="515" y="36"/><use href="#dot" x="550" y="36"/><use href="#dot" x="585" y="36"/>
    <!-- Vertical (x=600) -->
    <use href="#dot" x="596" y="52"/><use href="#dot" x="596" y="68"/>
    <!-- Linha 5 (y=116) -->
    <use href="#dot" x="620" y="116"/><use href="#dot" x="655" y="116"/><use href="#dot" x="690" y="116"/><use href="#dot" x="725" y="116"/>
    <!-- Vertical (x=740) -->
    <use href="#dot" x="736" y="100"/><use href="#dot" x="736" y="92"/>
    <!-- Linha 6 (y=76) -->
    <use href="#dot" x="760" y="76"/><use href="#dot" x="795" y="76"/><use href="#dot" x="830" y="76"/><use href="#dot" x="865" y="76"/><use href="#dot" x="900" y="76"/>
  </g>

  <!-- Título -->
  <g font-family="Segoe UI, Roboto, Arial, sans-serif" font-size="24" fill="#e6ecff" text-anchor="middle">
    <text x="490" y="48">CASSIO SOARES MISQUITA — README</text>
  </g>

  <!-- Runners: ida e volta (ping-pong) -->
  <!-- Cada runner alterna visibilidade; as animações encadeiam: forward -> backward -> forward ... -->
  <g id="runnerF" opacity="1">
    <!-- Boca animando -->
    <use href="#pacman-open">
      <animate attributeName="display" values="inline;none" dur="0.18s" repeatCount="indefinite"/>
    </use>
    <use href="#pacman-closed">
      <animate attributeName="display" values="none;inline" dur="0.18s" repeatCount="indefinite"/>
    </use>
    <!-- Movimento (ida) -->
    <animateMotion id="amF" dur="6s" rotate="auto" fill="freeze" begin="0s;amB.end">
      <mpath xlink:href="#track-forward" href="#track-forward"/>
    </animateMotion>
    <!-- Visibilidade do runner F -->
    <animate attributeName="opacity" values="1;1;0" keyTimes="0;0.99;1" dur="6s" begin="0s;amB.end" fill="freeze"/>
  </g>

  <g id="runnerB" opacity="0">
    <!-- Boca animando -->
    <use href="#pacman-open">
      <animate attributeName="display" values="inline;none" dur="0.18s" repeatCount="indefinite"/>
    </use>
    <use href="#pacman-closed">
      <animate attributeName="display" values="none;inline" dur="0.18s" repeatCount="indefinite"/>
    </use>
    <!-- Movimento (volta) -->
    <animateMotion id="amB" dur="6s" rotate="auto" fill="freeze" begin="amF.end">
      <mpath xlink:href="#track-backward" href="#track-backward"/>
    </animateMotion>
    <!-- Visibilidade do runner B -->
    <animate attributeName="opacity" values="0;1;1" keyTimes="0;0.01;1" dur="6s" begin="amF.end" fill="freeze"/>
  </g>
</svg>
