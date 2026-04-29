<!DOCTYPE html>
<html lang="en" data-theme="light">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Ong Hui Zhen — UI/UX Designer</title>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
  <link href="https://fonts.googleapis.com/css2?family=Cormorant+Garamond:ital,wght@0,300;0,400;0,600;1,300;1,400&family=DM+Sans:wght@300;400;500&display=swap" rel="stylesheet" />
  <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css" />

  <style>
    /* ─── Design Tokens ─────────────────────────────────── */
    :root {
      --bg:        #F7F4F0;
      --surface:   #EDEAE4;
      --border:    #D8D2C8;
      --text:      #1A1714;
      --muted:     #7A7267;
      --accent:    #B07D4F;
      --accent2:   #6E8C6E;
      --white:     #FFFFFF;
      --nav-h:     64px;
      --radius:    4px;
      --transition: 0.35s cubic-bezier(0.4, 0, 0.2, 1);
    }
    [data-theme="dark"] {
      --bg:       #141210;
      --surface:  #1E1C19;
      --border:   #2E2B26;
      --text:     #EDE9E3;
      --muted:    #7A7267;
      --accent:   #C99B6A;
      --accent2:  #82A882;
      --white:    #1E1C19;
    }

    /* ─── Reset ──────────────────────────────────────────── */
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
    html { scroll-behavior: smooth; font-size: 16px; }
    body {
      font-family: 'DM Sans', sans-serif;
      background: var(--bg);
      color: var(--text);
      transition: background var(--transition), color var(--transition);
      overflow-x: hidden;
    }
    a { color: inherit; text-decoration: none; }
    img { display: block; max-width: 100%; }
    ul { list-style: none; }

    /* ─── Nav ────────────────────────────────────────────── */
    nav {
      position: fixed;
      top: 0; left: 0; right: 0;
      height: var(--nav-h);
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 5vw;
      z-index: 100;
      background: var(--bg);
      border-bottom: 1px solid transparent;
      transition: border-color var(--transition), background var(--transition);
    }
    nav.scrolled { border-bottom-color: var(--border); }
    .nav-logo {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.3rem;
      font-weight: 600;
      letter-spacing: 0.02em;
    }
    .nav-logo span { color: var(--accent); }
    .nav-links {
      display: flex;
      gap: 2rem;
      align-items: center;
    }
    .nav-links a {
      font-size: 0.8rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      color: var(--muted);
      transition: color 0.2s;
    }
    .nav-links a:hover { color: var(--text); }
    .theme-toggle {
      background: none;
      border: 1px solid var(--border);
      color: var(--muted);
      width: 34px; height: 34px;
      border-radius: 50%;
      cursor: pointer;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 0.8rem;
      transition: border-color 0.2s, color 0.2s, background 0.2s;
    }
    .theme-toggle:hover { border-color: var(--accent); color: var(--accent); }

    /* Hamburger */
    .hamburger {
      display: none;
      flex-direction: column;
      gap: 5px;
      cursor: pointer;
      background: none;
      border: none;
      padding: 4px;
    }
    .hamburger span {
      display: block;
      width: 22px;
      height: 2px;
      background: var(--text);
      transition: transform 0.3s, opacity 0.3s;
      border-radius: 2px;
    }
    .hamburger.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
    .hamburger.open span:nth-child(2) { opacity: 0; }
    .hamburger.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

    .mobile-menu {
      display: none;
      position: fixed;
      top: var(--nav-h);
      left: 0; right: 0;
      background: var(--bg);
      border-bottom: 1px solid var(--border);
      padding: 1.5rem 5vw 2rem;
      z-index: 99;
      flex-direction: column;
      gap: 1.2rem;
    }
    .mobile-menu.open { display: flex; }
    .mobile-menu a {
      font-size: 0.85rem;
      font-weight: 500;
      letter-spacing: 0.1em;
      text-transform: uppercase;
      color: var(--muted);
      transition: color 0.2s;
    }
    .mobile-menu a:hover { color: var(--text); }

    /* ─── Sections ───────────────────────────────────────── */
    section { padding: 100px 5vw; }

    /* ─── Hero ───────────────────────────────────────────── */
    #hero {
      min-height: 100vh;
      display: flex;
      flex-direction: column;
      justify-content: center;
      padding-top: calc(var(--nav-h) + 60px);
      position: relative;
      overflow: hidden;
    }
    .hero-eyebrow {
      font-size: 0.72rem;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: var(--accent);
      font-weight: 500;
      margin-bottom: 1.5rem;
      opacity: 0;
      animation: fadeUp 0.8s 0.2s forwards;
    }
    .hero-name {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(3.5rem, 9vw, 8rem);
      font-weight: 300;
      line-height: 1;
      letter-spacing: -0.01em;
      margin-bottom: 0.2em;
      opacity: 0;
      animation: fadeUp 0.9s 0.4s forwards;
    }
    .hero-name em {
      font-style: italic;
      color: var(--accent);
    }
    .hero-title {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(1.4rem, 3vw, 2.4rem);
      font-weight: 300;
      color: var(--muted);
      margin-bottom: 2rem;
      opacity: 0;
      animation: fadeUp 0.9s 0.55s forwards;
    }
    .hero-tagline {
      font-size: clamp(0.95rem, 1.5vw, 1.1rem);
      color: var(--muted);
      max-width: 42ch;
      line-height: 1.7;
      margin-bottom: 3rem;
      opacity: 0;
      animation: fadeUp 0.9s 0.7s forwards;
    }
    .hero-cta {
      display: inline-flex;
      align-items: center;
      gap: 0.6rem;
      padding: 0.85rem 2rem;
      background: var(--accent);
      color: #fff;
      font-size: 0.78rem;
      font-weight: 500;
      letter-spacing: 0.12em;
      text-transform: uppercase;
      border-radius: var(--radius);
      transition: background 0.2s, transform 0.2s;
      opacity: 0;
      animation: fadeUp 0.9s 0.85s forwards;
    }
    .hero-cta:hover { background: var(--text); transform: translateY(-2px); }
    .hero-scroll {
      position: absolute;
      bottom: 2.5rem;
      right: 5vw;
      writing-mode: vertical-rl;
      font-size: 0.7rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--muted);
      display: flex;
      align-items: center;
      gap: 0.8rem;
      opacity: 0;
      animation: fadeUp 1s 1.2s forwards;
    }
    .hero-scroll::before {
      content: '';
      display: block;
      width: 1px;
      height: 60px;
      background: var(--border);
    }
    /* Decorative blob */
    .hero-blob {
      position: absolute;
      top: 10%;
      right: -10%;
      width: min(600px, 60vw);
      height: min(600px, 60vw);
      border-radius: 50%;
      background: radial-gradient(circle, color-mix(in srgb, var(--accent) 12%, transparent), transparent 70%);
      pointer-events: none;
      opacity: 0;
      animation: fadeIn 2s 0.5s forwards;
    }

    /* ─── About ──────────────────────────────────────────── */
    #about { background: var(--surface); transition: background var(--transition); }
    .about-grid {
      display: grid;
      grid-template-columns: 1fr 2fr;
      gap: 4rem;
      align-items: start;
    }
    .section-label {
      font-size: 0.7rem;
      letter-spacing: 0.22em;
      text-transform: uppercase;
      color: var(--accent);
      font-weight: 500;
      margin-bottom: 1rem;
    }
    .section-heading {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2rem, 4vw, 3.2rem);
      font-weight: 300;
      line-height: 1.15;
    }
    .about-left { position: sticky; top: calc(var(--nav-h) + 2rem); }
    .about-divider {
      width: 40px;
      height: 1px;
      background: var(--accent);
      margin: 1.5rem 0;
    }
    .about-body p {
      font-size: 1rem;
      line-height: 1.8;
      color: var(--muted);
      margin-bottom: 1.2rem;
    }
    .about-body p strong { color: var(--text); font-weight: 500; }

    /* ─── Skills ─────────────────────────────────────────── */
    .skills-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 2rem;
      margin-top: 3rem;
    }
    .skill-card {
      padding: 2rem;
      border: 1px solid var(--border);
      border-radius: calc(var(--radius) * 2);
      transition: border-color 0.2s, transform 0.2s;
    }
    .skill-card:hover { border-color: var(--accent); transform: translateY(-3px); }
    .skill-card-icon {
      font-size: 1.4rem;
      color: var(--accent);
      margin-bottom: 1rem;
    }
    .skill-card h3 {
      font-size: 0.75rem;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      font-weight: 500;
      margin-bottom: 1rem;
      color: var(--text);
    }
    .skill-tags {
      display: flex;
      flex-wrap: wrap;
      gap: 0.5rem;
    }
    .tag {
      font-size: 0.78rem;
      padding: 0.3rem 0.75rem;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 100px;
      color: var(--muted);
      transition: background 0.2s, color 0.2s;
    }
    [data-theme="dark"] .tag { background: var(--bg); }
    .tag:hover { background: var(--accent); color: #fff; border-color: var(--accent); }

    /* ─── Projects ───────────────────────────────────────── */
    #projects { background: var(--surface); transition: background var(--transition); }
    .projects-header {
      display: flex;
      justify-content: space-between;
      align-items: flex-end;
      margin-bottom: 3rem;
    }
    .projects-grid {
      display: grid;
      grid-template-columns: repeat(2, 1fr);
      gap: 1.5rem;
    }
    .project-card {
      background: var(--bg);
      border: 1px solid var(--border);
      border-radius: calc(var(--radius) * 2);
      overflow: hidden;
      transition: transform 0.3s, box-shadow 0.3s;
    }
    .project-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 20px 40px -10px rgba(0,0,0,0.12);
    }
    .project-thumb {
      height: 220px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 3rem;
      position: relative;
      overflow: hidden;
    }
    .project-thumb .proj-icon {
      position: relative;
      z-index: 1;
      opacity: 0.85;
    }
    .project-body { padding: 1.5rem; }
    .project-type {
      font-size: 0.68rem;
      letter-spacing: 0.18em;
      text-transform: uppercase;
      color: var(--accent);
      font-weight: 500;
      margin-bottom: 0.5rem;
    }
    .project-body h3 {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      font-weight: 400;
      margin-bottom: 0.6rem;
    }
    .project-body p {
      font-size: 0.88rem;
      line-height: 1.7;
      color: var(--muted);
    }
    .project-footer {
      padding: 1rem 1.5rem;
      border-top: 1px solid var(--border);
      display: flex;
      gap: 0.5rem;
      flex-wrap: wrap;
    }
    .project-tag {
      font-size: 0.72rem;
      padding: 0.2rem 0.6rem;
      background: var(--surface);
      border-radius: 100px;
      color: var(--muted);
    }
    [data-theme="dark"] .project-tag { background: var(--border); }

    /* ─── Experience ─────────────────────────────────────── */
    .experience-list { margin-top: 3rem; }
    .exp-item {
      display: grid;
      grid-template-columns: 180px 1fr;
      gap: 2rem;
      padding: 2.5rem 0;
      border-bottom: 1px solid var(--border);
      position: relative;
    }
    .exp-item:first-child { border-top: 1px solid var(--border); }
    .exp-meta { padding-top: 0.2rem; }
    .exp-period {
      font-size: 0.75rem;
      letter-spacing: 0.08em;
      color: var(--accent);
      font-weight: 500;
      margin-bottom: 0.4rem;
    }
    .exp-company {
      font-size: 0.8rem;
      color: var(--muted);
    }
    .exp-role {
      font-family: 'Cormorant Garamond', serif;
      font-size: 1.4rem;
      font-weight: 400;
      margin-bottom: 0.8rem;
    }
    .exp-bullets {
      list-style: none;
    }
    .exp-bullets li {
      font-size: 0.88rem;
      line-height: 1.7;
      color: var(--muted);
      padding-left: 1rem;
      position: relative;
      margin-bottom: 0.4rem;
    }
    .exp-bullets li::before {
      content: '—';
      position: absolute;
      left: 0;
      color: var(--accent);
      font-size: 0.7rem;
      top: 0.25em;
    }

    /* ─── Contact / Footer ───────────────────────────────── */
    #contact {
      background: var(--text);
      color: var(--bg);
      text-align: center;
      transition: background var(--transition), color var(--transition);
    }
    [data-theme="dark"] #contact {
      background: var(--surface);
      color: var(--text);
    }
    .contact-heading {
      font-family: 'Cormorant Garamond', serif;
      font-size: clamp(2.5rem, 6vw, 5rem);
      font-weight: 300;
      line-height: 1.1;
      margin-bottom: 1.5rem;
    }
    .contact-heading em { font-style: italic; color: var(--accent); }
    .contact-sub {
      font-size: 0.95rem;
      opacity: 0.6;
      margin-bottom: 2.5rem;
      max-width: 40ch;
      margin-left: auto;
      margin-right: auto;
      line-height: 1.7;
    }
    .contact-email {
      display: inline-block;
      font-size: 1rem;
      font-weight: 500;
      letter-spacing: 0.04em;
      color: var(--accent);
      border-bottom: 1px solid var(--accent);
      padding-bottom: 2px;
      margin-bottom: 3rem;
      transition: opacity 0.2s;
    }
    .contact-email:hover { opacity: 0.7; }
    .social-links {
      display: flex;
      justify-content: center;
      gap: 1.2rem;
      margin-bottom: 4rem;
    }
    .social-links a {
      width: 44px; height: 44px;
      border-radius: 50%;
      border: 1px solid rgba(255,255,255,0.2);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 1rem;
      opacity: 0.7;
      transition: opacity 0.2s, border-color 0.2s, transform 0.2s;
    }
    [data-theme="dark"] .social-links a { border-color: var(--border); color: var(--text); }
    .social-links a:hover { opacity: 1; border-color: var(--accent); transform: translateY(-3px); }
    .footer-copy {
      font-size: 0.72rem;
      letter-spacing: 0.1em;
      opacity: 0.35;
      text-transform: uppercase;
    }

    /* ─── Animations ─────────────────────────────────────── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to   { opacity: 1; transform: translateY(0); }
    }
    @keyframes fadeIn {
      from { opacity: 0; }
      to   { opacity: 1; }
    }
    .reveal {
      opacity: 0;
      transform: translateY(24px);
      transition: opacity 0.7s ease, transform 0.7s ease;
    }
    .reveal.visible {
      opacity: 1;
      transform: translateY(0);
    }

    /* ─── Responsive ─────────────────────────────────────── */
    @media (max-width: 900px) {
      .about-grid { grid-template-columns: 1fr; }
      .about-left { position: static; }
      .skills-grid { grid-template-columns: repeat(2, 1fr); }
      .projects-grid { grid-template-columns: 1fr; }
      .exp-item { grid-template-columns: 1fr; gap: 0.5rem; }
      .exp-meta { padding-top: 0; }
    }
    @media (max-width: 640px) {
      section { padding: 70px 5vw; }
      .nav-links { display: none; }
      .hamburger { display: flex; }
      .skills-grid { grid-template-columns: 1fr; }
      .hero-scroll { display: none; }
      .projects-header { flex-direction: column; align-items: flex-start; gap: 1rem; }
    }
  </style>
</head>
<body>

  <!-- ─── Nav ─────────────────────────────── -->
  <nav id="navbar">
    <div class="nav-logo">Hui <span>Zhen</span></div>
    <div class="nav-links">
      <a href="#about">About</a>
      <a href="#skills">Skills</a>
      <a href="#projects">Projects</a>
      <a href="#experience">Experience</a>
      <a href="#contact">Contact</a>
      <button class="theme-toggle" id="themeToggle" aria-label="Toggle theme">
        <i class="fa-solid fa-moon"></i>
      </button>
    </div>
    <button class="hamburger" id="hamburger" aria-label="Menu">
      <span></span><span></span><span></span>
    </button>
  </nav>

  <div class="mobile-menu" id="mobileMenu">
    <a href="#about"      onclick="closeMobile()">About</a>
    <a href="#skills"     onclick="closeMobile()">Skills</a>
    <a href="#projects"   onclick="closeMobile()">Projects</a>
    <a href="#experience" onclick="closeMobile()">Experience</a>
    <a href="#contact"    onclick="closeMobile()">Contact</a>
  </div>

  <!-- ─── Hero ─────────────────────────────── -->
  <section id="hero">
    <div class="hero-blob"></div>
    <p class="hero-eyebrow">Portfolio — UI/UX Design</p>
    <h1 class="hero-name">Ong <em>Hui</em><br>Zhen</h1>
    <p class="hero-title">UI/UX Designer &amp; Visual Storyteller</p>
    <p class="hero-tagline">Bridging the gap between beautiful design and meaningful user experience — one pixel, one interaction at a time.</p>
    <a href="#projects" class="hero-cta">View Projects <i class="fa-solid fa-arrow-right"></i></a>
    <span class="hero-scroll">Scroll</span>
  </section>

  <!-- ─── About ─────────────────────────────── -->
  <section id="about">
    <div class="about-grid">
      <div class="about-left reveal">
        <p class="section-label">About Me</p>
        <h2 class="section-heading">Design that<br><em style="font-style:italic;color:var(--accent);">thinks</em><br>and feels.</h2>
        <div class="about-divider"></div>
      </div>
      <div class="about-body reveal">
        <p>Hello, my name is <strong>Ong Hui Zhen</strong>! I'm a UI/UX designer with a background in graphic design and <strong>over 4 years of experience</strong> creating visually engaging, brand-aligned work across digital and print.</p>
        <p>Currently transitioning into UI/UX, I've built a strong foundation in user-centered design through formal training in UX and product management. I'm passionate about <strong>understanding user needs</strong> and translating them into intuitive, accessible, and meaningful digital experiences.</p>
        <p>With a keen eye for visual detail and a growing focus on usability and interaction design, I aim to create solutions that are not only aesthetically strong but also <strong>functional and impactful</strong>.</p>
      </div>
    </div>
  </section>

  <!-- ─── Skills ─────────────────────────────── -->
  <section id="skills">
    <p class="section-label reveal">Expertise</p>
    <h2 class="section-heading reveal">What I bring<br>to the table.</h2>

    <div class="skills-grid">
      <div class="skill-card reveal">
        <div class="skill-card-icon"><i class="fa-solid fa-pen-nib"></i></div>
        <h3>Design Tools</h3>
        <div class="skill-tags">
          <span class="tag">Figma</span>
          <span class="tag">Adobe Photoshop</span>
          <span class="tag">Illustrator</span>
          <span class="tag">InDesign</span>
          <span class="tag">Premiere Pro</span>
          <span class="tag">Canva</span>
          <span class="tag">3Ds Max</span>
          <span class="tag">Blender</span>
        </div>
      </div>
      <div class="skill-card reveal">
        <div class="skill-card-icon"><i class="fa-solid fa-users"></i></div>
        <h3>Core UX Skills</h3>
        <div class="skill-tags">
          <span class="tag">Wireframing</span>
          <span class="tag">Prototyping</span>
          <span class="tag">User Research</span>
          <span class="tag">Usability Testing</span>
          <span class="tag">Design Thinking</span>
          <span class="tag">Information Architecture</span>
          <span class="tag">User Flows</span>
          <span class="tag">Personas</span>
          <span class="tag">Journey Mapping</span>
          <span class="tag">Competitive Analysis</span>
        </div>
      </div>
      <div class="skill-card reveal">
        <div class="skill-card-icon"><i class="fa-solid fa-palette"></i></div>
        <h3>Visual &amp; Design</h3>
        <div class="skill-tags">
          <span class="tag">Visual Branding</span>
          <span class="tag">Typography</span>
          <span class="tag">Layout Design</span>
          <span class="tag">Packaging Design</span>
          <span class="tag">Video Editing</span>
        </div>
      </div>
    </div>
  </section>

  <!-- ─── Projects ─────────────────────────────── -->
  <section id="projects">
    <div class="projects-header">
      <div>
        <p class="section-label reveal">Selected Work</p>
        <h2 class="section-heading reveal">Projects.</h2>
      </div>
    </div>

    <div class="projects-grid">

      <div class="project-card reveal">
        <div class="project-thumb" style="background: linear-gradient(135deg, #E8DDD4 0%, #C9B49A 100%);">
          <span class="proj-icon">🛒</span>
        </div>
        <div class="project-body">
          <p class="project-type">UI/UX Design · Mobile App</p>
          <h3>E-Commerce Redesign</h3>
          <p>End-to-end redesign of a retail shopping app focused on reducing checkout friction and improving product discoverability through better IA and navigation patterns.</p>
        </div>
        <div class="project-footer">
          <span class="project-tag">Figma</span>
          <span class="project-tag">User Research</span>
          <span class="project-tag">Prototyping</span>
          <span class="project-tag">Usability Testing</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-thumb" style="background: linear-gradient(135deg, #D4E8D8 0%, #8AA88E 100%);">
          <span class="proj-icon">🌿</span>
        </div>
        <div class="project-body">
          <p class="project-type">Brand Identity · Visual Design</p>
          <h3>Wellness Brand System</h3>
          <p>Created a cohesive brand identity for a wellness startup — including logo, colour palette, typography system, and digital/print collateral across social, packaging, and web.</p>
        </div>
        <div class="project-footer">
          <span class="project-tag">Illustrator</span>
          <span class="project-tag">InDesign</span>
          <span class="project-tag">Visual Branding</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-thumb" style="background: linear-gradient(135deg, #D4DCE8 0%, #8896B0 100%);">
          <span class="proj-icon">📊</span>
        </div>
        <div class="project-body">
          <p class="project-type">Product Design · Dashboard</p>
          <h3>Analytics Dashboard UI</h3>
          <p>Designed a data-dense yet readable analytics dashboard for a SaaS product, applying hierarchy principles and progressive disclosure to surface key insights at a glance.</p>
        </div>
        <div class="project-footer">
          <span class="project-tag">Figma</span>
          <span class="project-tag">Information Architecture</span>
          <span class="project-tag">Design System</span>
        </div>
      </div>

      <div class="project-card reveal">
        <div class="project-thumb" style="background: linear-gradient(135deg, #E8D4DC 0%, #B08898 100%);">
          <span class="proj-icon">🎬</span>
        </div>
        <div class="project-body">
          <p class="project-type">Motion · Print</p>
          <h3>Campaign Visual Suite</h3>
          <p>Produced a multi-channel campaign package including motion graphics, social assets, and printed collateral for a product launch — from concept through final delivery.</p>
        </div>
        <div class="project-footer">
          <span class="project-tag">Premiere Pro</span>
          <span class="project-tag">Photoshop</span>
          <span class="project-tag">Canva</span>
        </div>
      </div>

    </div>
  </section>

  <!-- ─── Experience ─────────────────────────────── -->
  <section id="experience">
    <p class="section-label reveal">Career</p>
    <h2 class="section-heading reveal">Experience.</h2>

    <div class="experience-list">

      <div class="exp-item reveal">
        <div class="exp-meta">
          <p class="exp-period">2022 – Present</p>
          <p class="exp-company">Freelance / Contract</p>
        </div>
        <div class="exp-detail">
          <h3 class="exp-role">UI/UX &amp; Graphic Designer</h3>
          <ul class="exp-bullets">
            <li>Delivered end-to-end UX design projects — from discovery and user research through wireframing, prototyping, and handoff to development.</li>
            <li>Produced brand identity systems, marketing collateral, and social media visuals for clients across retail, F&amp;B, and lifestyle sectors.</li>
            <li>Conducted usability testing sessions and synthesised findings into actionable design improvements.</li>
            <li>Collaborated with product managers and developers to align design decisions with technical constraints.</li>
          </ul>
        </div>
      </div>

      <div class="exp-item reveal">
        <div class="exp-meta">
          <p class="exp-period">2020 – 2022</p>
          <p class="exp-company">Design Studio</p>
        </div>
        <div class="exp-detail">
          <h3 class="exp-role">Graphic Designer</h3>
          <ul class="exp-bullets">
            <li>Created and maintained brand-aligned visual assets for digital and print campaigns, ensuring consistency across touchpoints.</li>
            <li>Designed packaging, editorial layouts, and promotional materials for consumer product brands.</li>
            <li>Managed multiple concurrent projects, liaising with clients to gather briefs and incorporate feedback.</li>
            <li>Produced video content and motion graphics for social media platforms using Premiere Pro.</li>
          </ul>
        </div>
      </div>

      <div class="exp-item reveal">
        <div class="exp-meta">
          <p class="exp-period">2019 – 2020</p>
          <p class="exp-company">Agency</p>
        </div>
        <div class="exp-detail">
          <h3 class="exp-role">Junior Designer</h3>
          <ul class="exp-bullets">
            <li>Supported the senior design team on branding, advertising, and digital campaigns for local and regional clients.</li>
            <li>Assisted in the creation of visual concepts from moodboards through to final art-worked files.</li>
            <li>Developed proficiency in Adobe Creative Suite through hands-on, deadline-driven project work.</li>
          </ul>
        </div>
      </div>

    </div>
  </section>

  <!-- ─── Contact ─────────────────────────────── -->
  <section id="contact">
    <h2 class="contact-heading reveal">Let's make<br>something <em>great</em>.</h2>
    <p class="contact-sub reveal">Open to full-time UI/UX roles, freelance projects, and interesting collaborations. Let's talk.</p>
    <a href="mailto:huizhenong@gmail.com" class="contact-email reveal">huizhenong@gmail.com</a>

    <div class="social-links reveal">
      <a href="https://linkedin.com/in/huizhenong" target="_blank" rel="noopener" aria-label="LinkedIn">
        <i class="fa-brands fa-linkedin-in"></i>
      </a>
      <a href="https://github.com/huizhenong" target="_blank" rel="noopener" aria-label="GitHub">
        <i class="fa-brands fa-github"></i>
      </a>
      <a href="mailto:huizhenong@gmail.com" aria-label="Email">
        <i class="fa-solid fa-envelope"></i>
      </a>
    </div>

    <p class="footer-copy reveal">© 2025 Ong Hui Zhen — Designed &amp; built with care.</p>
  </section>

  <!-- ─── Script ─────────────────────────────── -->
  <script>
    // Theme toggle
    const toggle = document.getElementById('themeToggle');
    const html   = document.documentElement;
    const icon   = toggle.querySelector('i');

    function applyTheme(t) {
      html.setAttribute('data-theme', t);
      icon.className = t === 'dark' ? 'fa-solid fa-sun' : 'fa-solid fa-moon';
      localStorage.setItem('theme', t);
    }

    const saved = localStorage.getItem('theme') ||
      (window.matchMedia('(prefers-color-scheme: dark)').matches ? 'dark' : 'light');
    applyTheme(saved);

    toggle.addEventListener('click', () => {
      applyTheme(html.getAttribute('data-theme') === 'dark' ? 'light' : 'dark');
    });

    // Nav scroll border
    const navbar = document.getElementById('navbar');
    window.addEventListener('scroll', () => {
      navbar.classList.toggle('scrolled', window.scrollY > 20);
    }, { passive: true });

    // Hamburger / mobile menu
    const hamburger   = document.getElementById('hamburger');
    const mobileMenu  = document.getElementById('mobileMenu');

    hamburger.addEventListener('click', () => {
      hamburger.classList.toggle('open');
      mobileMenu.classList.toggle('open');
    });

    function closeMobile() {
      hamburger.classList.remove('open');
      mobileMenu.classList.remove('open');
    }

    // Scroll reveal
    const reveals = document.querySelectorAll('.reveal');
    const io = new IntersectionObserver((entries) => {
      entries.forEach(e => {
        if (e.isIntersecting) {
          e.target.classList.add('visible');
          io.unobserve(e.target);
        }
      });
    }, { threshold: 0.12 });
    reveals.forEach(el => io.observe(el));
  </script>
</body>
</html>
