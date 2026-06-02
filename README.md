<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Narendra Naguri — Portfolio</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=DM+Mono:ital,wght@0,300;0,400;1,300&display=swap" rel="stylesheet"/>
<style>
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

  :root {
    --bg: #0a0a0f;
    --surface: #111118;
    --border: #1e1e2e;
    --accent: #7cffd4;
    --accent2: #ff6b6b;
    --accent3: #ffd93d;
    --text: #e8e8f0;
    --muted: #666680;
    --font-head: 'Syne', sans-serif;
    --font-mono: 'DM Mono', monospace;
  }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: var(--font-mono);
    font-size: 14px;
    line-height: 1.7;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9999;
    transition: transform 0.15s ease, background 0.2s;
    transform: translate(-50%, -50%);
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid rgba(124,255,212,0.4);
    border-radius: 50%;
    position: fixed;
    pointer-events: none;
    z-index: 9998;
    transition: transform 0.4s ease, width 0.3s, height 0.3s, background 0.3s;
    transform: translate(-50%, -50%);
  }
  body:hover .cursor { opacity: 1; }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed;
    inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* ── NAV ── */
  nav {
    position: fixed; top: 0; left: 0; right: 0;
    z-index: 100;
    display: flex; justify-content: space-between; align-items: center;
    padding: 20px 48px;
    background: linear-gradient(to bottom, rgba(10,10,15,0.95), transparent);
    backdrop-filter: blur(8px);
  }
  .nav-logo {
    font-family: var(--font-head);
    font-size: 18px;
    font-weight: 800;
    color: var(--accent);
    letter-spacing: -0.5px;
  }
  .nav-links { display: flex; gap: 32px; list-style: none; }
  .nav-links a {
    color: var(--muted);
    text-decoration: none;
    font-size: 12px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    transition: color 0.2s;
    position: relative;
  }
  .nav-links a::after {
    content: '';
    position: absolute;
    bottom: -2px; left: 0; right: 0;
    height: 1px;
    background: var(--accent);
    transform: scaleX(0);
    transition: transform 0.3s;
  }
  .nav-links a:hover { color: var(--accent); }
  .nav-links a:hover::after { transform: scaleX(1); }

  /* ── HERO ── */
  #hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    align-items: center;
    padding: 100px 48px 60px;
    position: relative;
    overflow: hidden;
  }

  /* Animated grid bg */
  #hero::before {
    content: '';
    position: absolute;
    inset: 0;
    background-image:
      linear-gradient(rgba(124,255,212,0.04) 1px, transparent 1px),
      linear-gradient(90deg, rgba(124,255,212,0.04) 1px, transparent 1px);
    background-size: 64px 64px;
    animation: gridMove 20s linear infinite;
  }
  @keyframes gridMove { from { transform: translateY(0); } to { transform: translateY(64px); } }

  /* Glowing blob */
  #hero::after {
    content: '';
    position: absolute;
    width: 600px; height: 600px;
    right: -100px; top: 50%;
    transform: translateY(-50%);
    background: radial-gradient(circle, rgba(124,255,212,0.08) 0%, transparent 70%);
    pointer-events: none;
  }

  .hero-left { position: relative; z-index: 1; }
  .hero-tag {
    display: inline-block;
    font-size: 11px;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    border: 1px solid rgba(124,255,212,0.3);
    padding: 4px 12px;
    border-radius: 2px;
    margin-bottom: 24px;
    animation: fadeUp 0.6s ease both;
  }
  .hero-name {
    font-family: var(--font-head);
    font-size: clamp(48px, 6vw, 80px);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -2px;
    color: var(--text);
    animation: fadeUp 0.6s 0.1s ease both;
  }
  .hero-name span { color: var(--accent); }
  .hero-role {
    font-family: var(--font-head);
    font-size: clamp(18px, 2.5vw, 26px);
    color: var(--muted);
    font-weight: 400;
    margin: 12px 0 28px;
    animation: fadeUp 0.6s 0.2s ease both;
  }
  .hero-desc {
    max-width: 480px;
    color: var(--muted);
    font-size: 13px;
    line-height: 1.8;
    margin-bottom: 40px;
    animation: fadeUp 0.6s 0.3s ease both;
  }
  .hero-cta {
    display: flex; gap: 16px; flex-wrap: wrap;
    animation: fadeUp 0.6s 0.4s ease both;
  }
  .btn {
    padding: 12px 28px;
    font-family: var(--font-mono);
    font-size: 12px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    text-decoration: none;
    border-radius: 3px;
    transition: all 0.25s;
    cursor: none;
  }
  .btn-primary {
    background: var(--accent);
    color: var(--bg);
    font-weight: 400;
  }
  .btn-primary:hover {
    background: #5ae8bb;
    transform: translateY(-2px);
    box-shadow: 0 8px 24px rgba(124,255,212,0.25);
  }
  .btn-ghost {
    border: 1px solid var(--border);
    color: var(--muted);
  }
  .btn-ghost:hover {
    border-color: var(--accent);
    color: var(--accent);
    transform: translateY(-2px);
  }

  .hero-right {
    position: relative; z-index: 1;
    display: flex; justify-content: center; align-items: center;
    animation: fadeIn 1s 0.5s ease both;
  }

  .hero-terminal {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    width: 100%;
    max-width: 440px;
    overflow: hidden;
    box-shadow: 0 24px 80px rgba(0,0,0,0.5), 0 0 0 1px rgba(124,255,212,0.05);
  }
  .terminal-bar {
    padding: 12px 16px;
    background: #0d0d14;
    border-bottom: 1px solid var(--border);
    display: flex; align-items: center; gap: 8px;
  }
  .dot { width: 10px; height: 10px; border-radius: 50%; }
  .dot.r { background: #ff5f57; }
  .dot.y { background: #febc2e; }
  .dot.g { background: #28c840; }
  .terminal-title { font-size: 11px; color: var(--muted); margin-left: 8px; letter-spacing: 0.05em; }
  .terminal-body { padding: 20px 24px; font-size: 12.5px; line-height: 2; }
  .line { display: flex; gap: 10px; opacity: 0; animation: termLine 0.3s ease forwards; }
  .line:nth-child(1) { animation-delay: 0.8s; }
  .line:nth-child(2) { animation-delay: 1.2s; }
  .line:nth-child(3) { animation-delay: 1.6s; }
  .line:nth-child(4) { animation-delay: 2.0s; }
  .line:nth-child(5) { animation-delay: 2.4s; }
  .line:nth-child(6) { animation-delay: 2.8s; }
  .line:nth-child(7) { animation-delay: 3.2s; }
  .prompt { color: var(--accent); }
  .cmd { color: #aad4ff; }
  .output { color: var(--muted); padding-left: 0; }
  .val { color: var(--accent3); }
  .blink {
    display: inline-block;
    width: 8px; height: 14px;
    background: var(--accent);
    vertical-align: middle;
    animation: blink 1s step-end infinite;
    margin-left: 4px;
  }
  @keyframes blink { 0%,100% { opacity: 1; } 50% { opacity: 0; } }
  @keyframes termLine { to { opacity: 1; transform: none; } from { opacity: 0; transform: translateY(4px); } }

  /* ── SECTIONS ── */
  section { padding: 100px 48px; position: relative; }
  .section-label {
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 12px;
    display: flex;
    align-items: center; gap: 12px;
  }
  .section-label::after {
    content: '';
    display: block;
    height: 1px;
    width: 40px;
    background: var(--accent);
    opacity: 0.4;
  }
  .section-title {
    font-family: var(--font-head);
    font-size: clamp(32px, 4vw, 52px);
    font-weight: 800;
    letter-spacing: -1.5px;
    line-height: 1.05;
    color: var(--text);
    margin-bottom: 60px;
  }

  /* ── SKILLS ── */
  #skills { background: var(--surface); }
  .skills-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
    gap: 12px;
  }
  .skill-chip {
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    padding: 14px 18px;
    font-size: 12px;
    color: var(--muted);
    display: flex; align-items: center; gap: 10px;
    transition: all 0.25s;
    position: relative;
    overflow: hidden;
  }
  .skill-chip::before {
    content: '';
    position: absolute;
    left: 0; top: 0; bottom: 0;
    width: 3px;
    background: var(--accent);
    transform: scaleY(0);
    transition: transform 0.25s;
  }
  .skill-chip:hover {
    border-color: rgba(124,255,212,0.3);
    color: var(--text);
    transform: translateX(4px);
  }
  .skill-chip:hover::before { transform: scaleY(1); }
  .skill-icon { font-size: 16px; }

  /* ── PROJECTS ── */
  .projects-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 24px; }
  .project-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 36px;
    position: relative;
    overflow: hidden;
    transition: all 0.3s;
  }
  .project-card::after {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(circle at var(--mx,50%) var(--my,50%), rgba(124,255,212,0.06), transparent 60%);
    opacity: 0;
    transition: opacity 0.3s;
    pointer-events: none;
  }
  .project-card:hover { border-color: rgba(124,255,212,0.2); transform: translateY(-4px); }
  .project-card:hover::after { opacity: 1; }
  .project-num {
    font-size: 11px;
    color: var(--accent);
    letter-spacing: 0.15em;
    margin-bottom: 20px;
    opacity: 0.7;
  }
  .project-title {
    font-family: var(--font-head);
    font-size: 22px;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 14px;
    letter-spacing: -0.5px;
  }
  .project-desc {
    color: var(--muted);
    font-size: 12.5px;
    line-height: 1.8;
    margin-bottom: 24px;
  }
  .project-tags { display: flex; flex-wrap: wrap; gap: 8px; }
  .tag {
    font-size: 10px;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    padding: 4px 10px;
    border-radius: 2px;
    border: 1px solid var(--border);
    color: var(--muted);
  }
  .tag.featured { border-color: rgba(124,255,212,0.3); color: var(--accent); }
  .project-arrow {
    position: absolute;
    top: 36px; right: 36px;
    font-size: 20px;
    color: var(--border);
    transition: all 0.3s;
  }
  .project-card:hover .project-arrow { color: var(--accent); transform: translate(3px,-3px); }

  /* ── EDUCATION ── */
  #education { background: var(--surface); }
  .edu-timeline { position: relative; padding-left: 24px; }
  .edu-timeline::before {
    content: '';
    position: absolute;
    left: 0; top: 8px; bottom: 8px;
    width: 1px;
    background: linear-gradient(to bottom, var(--accent), transparent);
  }
  .edu-item {
    padding: 28px 0 28px 40px;
    position: relative;
    border-bottom: 1px solid var(--border);
  }
  .edu-item:last-child { border-bottom: none; }
  .edu-item::before {
    content: '';
    position: absolute;
    left: -5px; top: 38px;
    width: 10px; height: 10px;
    border-radius: 50%;
    background: var(--accent);
    box-shadow: 0 0 12px rgba(124,255,212,0.5);
  }
  .edu-year {
    font-size: 11px;
    letter-spacing: 0.12em;
    color: var(--accent);
    margin-bottom: 8px;
  }
  .edu-degree {
    font-family: var(--font-head);
    font-size: 18px;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 4px;
    letter-spacing: -0.3px;
  }
  .edu-school { color: var(--muted); font-size: 13px; margin-bottom: 4px; }
  .edu-grade {
    display: inline-block;
    margin-top: 8px;
    font-size: 11px;
    padding: 3px 10px;
    border-radius: 2px;
    background: rgba(124,255,212,0.08);
    color: var(--accent);
    border: 1px solid rgba(124,255,212,0.2);
  }

  /* ── CERTIFICATIONS ── */
  .certs-grid { display: grid; grid-template-columns: 1fr 1fr; gap: 16px; }
  .cert-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 24px 28px;
    display: flex; align-items: flex-start; gap: 16px;
    transition: all 0.25s;
  }
  .cert-card:hover { border-color: rgba(124,255,212,0.25); }
  .cert-icon {
    width: 40px; height: 40px;
    border-radius: 6px;
    background: rgba(124,255,212,0.08);
    display: flex; align-items: center; justify-content: center;
    font-size: 18px;
    flex-shrink: 0;
    border: 1px solid rgba(124,255,212,0.15);
  }
  .cert-name {
    font-family: var(--font-head);
    font-size: 15px;
    font-weight: 600;
    color: var(--text);
    margin-bottom: 4px;
    letter-spacing: -0.2px;
  }
  .cert-issuer { color: var(--muted); font-size: 12px; }

  /* ── CONTACT ── */
  #contact { background: var(--surface); text-align: center; }
  .contact-inner { max-width: 600px; margin: 0 auto; }
  .contact-intro { color: var(--muted); margin-bottom: 48px; font-size: 14px; line-height: 1.8; }
  .contact-links { display: flex; justify-content: center; gap: 20px; flex-wrap: wrap; }
  .contact-link {
    display: flex; align-items: center; gap: 10px;
    padding: 14px 24px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 4px;
    text-decoration: none;
    color: var(--muted);
    font-size: 12px;
    letter-spacing: 0.05em;
    transition: all 0.25s;
  }
  .contact-link:hover { border-color: var(--accent); color: var(--accent); transform: translateY(-2px); }
  .contact-link .icon { font-size: 16px; }

  /* ── FOOTER ── */
  footer {
    padding: 32px 48px;
    border-top: 1px solid var(--border);
    display: flex; justify-content: space-between; align-items: center;
    color: var(--muted); font-size: 11px; letter-spacing: 0.05em;
  }
  .footer-accent { color: var(--accent); }

  /* ── ANIMATIONS ── */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(20px); }
    to { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to { opacity: 1; }
  }

  .reveal {
    opacity: 0;
    transform: translateY(24px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .reveal.visible { opacity: 1; transform: none; }

  /* ── RESPONSIVE ── */
  @media (max-width: 900px) {
    #hero { grid-template-columns: 1fr; padding: 100px 24px 60px; gap: 60px; }
    .hero-right { display: none; }
    nav { padding: 16px 24px; }
    .nav-links { gap: 20px; }
    section { padding: 80px 24px; }
    .projects-grid, .certs-grid { grid-template-columns: 1fr; }
    footer { flex-direction: column; gap: 8px; text-align: center; }
  }
</style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- NAV -->
<nav>
  <div class="nav-logo">NN/</div>
  <ul class="nav-links">
    <li><a href="#skills">Skills</a></li>
    <li><a href="#projects">Projects</a></li>
    <li><a href="#education">Education</a></li>
    <li><a href="#contact">Contact</a></li>
  </ul>
</nav>

<!-- HERO -->
<section id="hero">
  <div class="hero-left">
    <div class="hero-tag">Available for opportunities</div>
    <h1 class="hero-name">Narendra<br><span>Naguri</span></h1>
    <p class="hero-role">Software Developer & CS Engineer</p>
    <p class="hero-desc">
      Entry-level graduate passionate about building software, exploring AI/ML,
      and solving real-world problems through clean code and thoughtful design.
    </p>
    <div class="hero-cta">
      <a href="#projects" class="btn btn-primary">View Projects</a>
      <a href="#contact" class="btn btn-ghost">Get in Touch</a>
    </div>
  </div>
  <div class="hero-right">
    <div class="hero-terminal">
      <div class="terminal-bar">
        <span class="dot r"></span>
        <span class="dot y"></span>
        <span class="dot g"></span>
        <span class="terminal-title">narendra ~ profile.json</span>
      </div>
      <div class="terminal-body">
        <div class="line"><span class="prompt">$</span><span class="cmd">cat profile.json</span></div>
        <div class="line output">{</div>
        <div class="line output">&nbsp;&nbsp;<span class="cmd">"name":</span> <span class="val">"Narendra Naguri"</span>,</div>
        <div class="line output">&nbsp;&nbsp;<span class="cmd">"role":</span> <span class="val">"CS Engineer (AI & ML)"</span>,</div>
        <div class="line output">&nbsp;&nbsp;<span class="cmd">"cgpa":</span> <span class="val">9.01</span>,</div>
        <div class="line output">&nbsp;&nbsp;<span class="cmd">"location":</span> <span class="val">"Tirupati, AP"</span>,</div>
        <div class="line output">&nbsp;&nbsp;<span class="cmd">"status":</span> <span class="val">"Seeking first role 🚀"</span></div>
        <div class="line output">}<span class="blink"></span></div>
      </div>
    </div>
  </div>
</section>

<!-- SKILLS -->
<section id="skills">
  <div class="section-label">Technical Skills</div>
  <h2 class="section-title reveal">What I work with</h2>
  <div class="skills-grid reveal">
    <div class="skill-chip"><span class="skill-icon">☕</span>Java</div>
    <div class="skill-chip"><span class="skill-icon">🐍</span>Python</div>
    <div class="skill-chip"><span class="skill-icon">📊</span>SQL</div>
    <div class="skill-chip"><span class="skill-icon">🌐</span>HTML & CSS</div>
    <div class="skill-chip"><span class="skill-icon">⚡</span>JavaScript</div>
    <div class="skill-chip"><span class="skill-icon">🗄️</span>MySQL</div>
    <div class="skill-chip"><span class="skill-icon">🔧</span>Git & GitHub</div>
    <div class="skill-chip"><span class="skill-icon">🔷</span>VS Code</div>
    <div class="skill-chip"><span class="skill-icon">🌳</span>Data Structures</div>
    <div class="skill-chip"><span class="skill-icon">🔑</span>Algorithms</div>
    <div class="skill-chip"><span class="skill-icon">📦</span>OOP</div>
    <div class="skill-chip"><span class="skill-icon">🗃️</span>DBMS</div>
  </div>
</section>

<!-- PROJECTS -->
<section id="projects">
  <div class="section-label">Projects</div>
  <h2 class="section-title reveal">Things I've built</h2>
  <div class="projects-grid">
    <div class="project-card reveal" onmousemove="trackMouse(event,this)">
      <div class="project-arrow">↗</div>
      <div class="project-num">01 / LIVE PROJECT</div>
      <h3 class="project-title">Food Web App</h3>
      <p class="project-desc">
        A fully responsive food ordering web application with a clean, intuitive UI.
        Features smooth navigation, interactive components, and a polished user experience
        built from scratch with vanilla web technologies.
      </p>
      <div class="project-tags">
        <span class="tag featured">HTML</span>
        <span class="tag featured">CSS</span>
        <span class="tag featured">JavaScript</span>
        <span class="tag">Responsive Design</span>
        <span class="tag">UI/UX</span>
      </div>
    </div>
    <div class="project-card reveal" onmousemove="trackMouse(event,this)">
      <div class="project-arrow">↗</div>
      <div class="project-num">02 / CONSOLE APP</div>
      <h3 class="project-title">Library Management System</h3>
      <p class="project-desc">
        A console-based library system handling complete book management operations — adding,
        searching by title/author, and issuing/returning books. Demonstrates strong OOP design
        principles and persistent file handling.
      </p>
      <div class="project-tags">
        <span class="tag featured">Java</span>
        <span class="tag featured">OOP</span>
        <span class="tag featured">File Handling</span>
        <span class="tag">Data Structures</span>
      </div>
    </div>
  </div>
</section>

<!-- EDUCATION -->
<section id="education">
  <div class="section-label">Education</div>
  <h2 class="section-title reveal">Academic Journey</h2>
  <div class="edu-timeline">
    <div class="edu-item reveal">
      <div class="edu-year">2022 — 2026</div>
      <div class="edu-degree">B.Tech — Computer Science & Engineering (AI & ML)</div>
      <div class="edu-school">Mohan Babu University</div>
      <span class="edu-grade">CGPA: 9.01 / 10</span>
    </div>
    <div class="edu-item reveal">
      <div class="edu-year">2020 — 2022</div>
      <div class="edu-degree">Board of Intermediate Education — MPC</div>
      <div class="edu-school">Sri Chaitanya Junior College</div>
      <span class="edu-grade">CGPA: 10.0 / 10</span>
    </div>
    <div class="edu-item reveal">
      <div class="edu-year">2019 — 2020</div>
      <div class="edu-degree">Board of Secondary Education</div>
      <div class="edu-school">Gopi Krishna High School</div>
      <span class="edu-grade">CGPA: 10.0 / 10</span>
    </div>
  </div>
</section>

<!-- CERTIFICATIONS -->
<section id="certifications" style="background: var(--bg);">
  <div class="section-label">Certifications</div>
  <h2 class="section-title reveal">Credentials</h2>
  <div class="certs-grid">
    <div class="cert-card reveal">
      <div class="cert-icon">🖥️</div>
      <div>
        <div class="cert-name">Full Stack Development</div>
        <div class="cert-issuer">Tap Academy</div>
      </div>
    </div>
    <div class="cert-card reveal">
      <div class="cert-icon">🌐</div>
      <div>
        <div class="cert-name">Python & Computer Networking</div>
        <div class="cert-issuer">CISCO</div>
      </div>
    </div>
  </div>
</section>

<!-- CONTACT -->
<section id="contact">
  <div class="contact-inner">
    <div class="section-label" style="justify-content:center">Contact</div>
    <h2 class="section-title reveal" style="margin-bottom:20px;">Let's Connect</h2>
    <p class="contact-intro reveal">
      I'm actively looking for my first professional opportunity. Whether you have a role, a
      project, or just want to connect — my inbox is open.
    </p>
    <div class="contact-links reveal">
      <a href="mailto:nnreddynaguri@gmail.com" class="contact-link">
        <span class="icon">✉️</span> nnreddynaguri@gmail.com
      </a>
      <a href="https://github.com/narendranaguri" target="_blank" class="contact-link">
        <span class="icon">🐙</span> narendranaguri
      </a>
      <a href="tel:+919703075305" class="contact-link">
        <span class="icon">📱</span> +91 97030 75305
      </a>
    </div>
  </div>
</section>

<!-- FOOTER -->
<footer>
  <span>© 2026 Narendra Naguri</span>
  <span>Built with <span class="footer-accent">HTML · CSS · JS</span></span>
  <span>Tirupati, AP 🇮🇳</span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    cursor.style.left = e.clientX + 'px';
    cursor.style.top = e.clientY + 'px';
    setTimeout(() => {
      ring.style.left = e.clientX + 'px';
      ring.style.top = e.clientY + 'px';
    }, 80);
  });

  document.querySelectorAll('a, button, .skill-chip, .project-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(2)';
      ring.style.width = '60px'; ring.style.height = '60px';
      ring.style.background = 'rgba(124,255,212,0.05)';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.transform = 'translate(-50%,-50%) scale(1)';
      ring.style.width = '36px'; ring.style.height = '36px';
      ring.style.background = 'none';
    });
  });

  // Scroll reveal
  const observer = new IntersectionObserver(entries => {
    entries.forEach((e, i) => {
      if (e.isIntersecting) {
        e.target.style.transitionDelay = (i * 0.05) + 's';
        e.target.classList.add('visible');
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.reveal').forEach(el => observer.observe(el));

  // Mouse tracking for project cards
  function trackMouse(e, el) {
    const rect = el.getBoundingClientRect();
    const x = ((e.clientX - rect.left) / rect.width * 100).toFixed(1);
    const y = ((e.clientY - rect.top) / rect.height * 100).toFixed(1);
    el.style.setProperty('--mx', x + '%');
    el.style.setProperty('--my', y + '%');
  }

  // Nav active state
  const sections = document.querySelectorAll('section[id]');
  const navLinks = document.querySelectorAll('.nav-links a');
  window.addEventListener('scroll', () => {
    let current = '';
    sections.forEach(s => {
      if (window.scrollY >= s.offsetTop - 200) current = s.id;
    });
    navLinks.forEach(a => {
      a.style.color = a.getAttribute('href') === '#' + current ? 'var(--accent)' : '';
    });
  });
</script>
</body>
</html>
