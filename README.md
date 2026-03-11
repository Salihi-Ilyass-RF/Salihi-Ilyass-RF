<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8"/>
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>Salihi-Ilyass-RF | GitHub README</title>
  <link href="https://fonts.googleapis.com/css2?family=Share+Tech+Mono&family=VT323&display=swap" rel="stylesheet"/>
  <style>
    :root {
      --bg: #020c02;
      --bg2: #040f04;
      --green: #00ff41;
      --green-dim: #00aa2a;
      --green-dark: #003310;
      --green-faint: rgba(0,255,65,0.06);
      --amber: #ffb000;
      --cyan: #00fff5;
      --muted: #2a5c2a;
      --border: #0d3d0d;
      --font: 'Share Tech Mono', monospace;
      --vt: 'VT323', monospace;
    }

    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--green);
      font-family: var(--font);
      font-size: 14px;
      line-height: 1.7;
      min-height: 100vh;
      cursor: none;
    }

    /* custom cursor */
    .cursor {
      position: fixed;
      width: 18px; height: 18px;
      border: 2px solid var(--green);
      border-radius: 0;
      pointer-events: none;
      z-index: 9999;
      transform: translate(-50%, -50%);
      transition: transform 0.05s;
      mix-blend-mode: screen;
    }

    /* scanlines */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background: repeating-linear-gradient(
        0deg,
        transparent,
        transparent 2px,
        rgba(0,0,0,0.18) 2px,
        rgba(0,0,0,0.18) 4px
      );
      pointer-events: none;
      z-index: 998;
    }

    /* screen flicker */
    body::after {
      content: '';
      position: fixed;
      inset: 0;
      background: rgba(0,255,65,0.015);
      pointer-events: none;
      z-index: 997;
      animation: flicker 8s infinite;
    }

    @keyframes flicker {
      0%,100% { opacity: 1; }
      92% { opacity: 1; }
      93% { opacity: 0.4; }
      94% { opacity: 1; }
      96% { opacity: 0.6; }
      97% { opacity: 1; }
    }

    .page {
      max-width: 860px;
      margin: 0 auto;
      padding: 40px 20px 100px;
    }

    /* ── TOP BAR ── */
    .topbar {
      display: flex;
      justify-content: space-between;
      align-items: center;
      border-bottom: 1px solid var(--border);
      padding-bottom: 12px;
      margin-bottom: 40px;
      font-size: 12px;
      color: var(--muted);
      animation: fadeIn 0.4s ease both;
    }

    .topbar-left { display: flex; gap: 24px; }
    .topbar-right { color: var(--green-dim); }

    .blink {
      animation: blink 1s step-end infinite;
    }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

    /* ── BOOT HEADER ── */
    .boot {
      border: 1px solid var(--border);
      background: var(--bg2);
      padding: 28px 32px;
      margin-bottom: 24px;
      position: relative;
      overflow: hidden;
      animation: fadeIn 0.5s 0.1s ease both;
    }

    .boot::before {
      content: '';
      position: absolute;
      inset: 0;
      background: radial-gradient(ellipse at top left, rgba(0,255,65,0.07) 0%, transparent 60%);
      pointer-events: none;
    }

    .boot-line {
      color: var(--muted);
      font-size: 12px;
      margin-bottom: 4px;
    }

    .boot-line .hl { color: var(--green); }
    .boot-line .am { color: var(--amber); }
    .boot-line .cy { color: var(--cyan); }

    .ascii-name {
      font-family: var(--vt);
      font-size: clamp(36px, 7vw, 68px);
      color: var(--green);
      line-height: 1;
      margin: 20px 0 8px;
      text-shadow: 0 0 20px rgba(0,255,65,0.5), 0 0 40px rgba(0,255,65,0.2);
      letter-spacing: 0.05em;
      animation: glow 3s ease-in-out infinite alternate;
    }

    @keyframes glow {
      from { text-shadow: 0 0 10px rgba(0,255,65,0.4), 0 0 20px rgba(0,255,65,0.1); }
      to   { text-shadow: 0 0 20px rgba(0,255,65,0.7), 0 0 40px rgba(0,255,65,0.3), 0 0 60px rgba(0,255,65,0.1); }
    }

    .prompt-tagline {
      font-size: 13px;
      color: var(--green-dim);
      margin-top: 6px;
    }

    .prompt-tagline .hl { color: var(--green); }

    /* ── TERMINAL BLOCK ── */
    .terminal {
      border: 1px solid var(--border);
      background: var(--bg2);
      margin-bottom: 20px;
      animation: fadeIn 0.5s ease both;
    }

    .terminal:nth-child(3) { animation-delay: 0.15s; }
    .terminal:nth-child(4) { animation-delay: 0.25s; }
    .terminal:nth-child(5) { animation-delay: 0.35s; }
    .terminal:nth-child(6) { animation-delay: 0.45s; }

    .term-header {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 8px 16px;
      border-bottom: 1px solid var(--border);
      background: rgba(0,255,65,0.04);
    }

    .term-dots { display: flex; gap: 6px; }
    .tdot { width: 9px; height: 9px; border-radius: 50%; }
    .td-r { background: #3d0d0d; }
    .td-y { background: #3d330d; }
    .td-g { background: #0d3d0d; }

    .term-title {
      font-size: 11px;
      color: var(--muted);
      letter-spacing: 0.1em;
      text-transform: uppercase;
    }

    .term-title .hl { color: var(--green); }

    .term-body {
      padding: 22px 28px;
    }

    /* ── PROMPT LINES ── */
    .cmd {
      display: flex;
      align-items: flex-start;
      gap: 0;
      margin-bottom: 4px;
      font-size: 13px;
    }

    .prompt-sym {
      color: var(--green-dim);
      margin-right: 8px;
      flex-shrink: 0;
    }

    .cmd-text { color: var(--amber); }

    .output {
      margin-bottom: 16px;
      padding-left: 20px;
      color: var(--green);
      font-size: 13px;
    }

    .output .label {
      color: var(--muted);
      display: inline-block;
      width: 80px;
    }

    .output .val { color: var(--green); }
    .output .val-cy { color: var(--cyan); }
    .output .val-am { color: var(--amber); }

    /* ── SKILLS GRID ── */
    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
      gap: 12px;
      margin-top: 4px;
    }

    .skill-group {
      background: var(--green-faint);
      border: 1px solid var(--border);
      padding: 14px 16px;
      position: relative;
      transition: border-color 0.2s, background 0.2s;
    }

    .skill-group:hover {
      border-color: var(--green-dim);
      background: rgba(0,255,65,0.1);
    }

    .skill-group::before {
      content: attr(data-cat);
      position: absolute;
      top: -1px; left: 10px;
      font-size: 9px;
      letter-spacing: 0.15em;
      text-transform: uppercase;
      color: var(--bg);
      background: var(--green-dim);
      padding: 1px 7px;
      transform: translateY(-50%);
    }

    .skill-list {
      margin-top: 6px;
      display: flex;
      flex-wrap: wrap;
      gap: 6px;
    }

    .skill-tag {
      font-size: 12px;
      padding: 2px 9px;
      border: 1px solid var(--green-dark);
      color: var(--green);
      background: transparent;
      letter-spacing: 0.04em;
      transition: all 0.15s;
    }

    .skill-tag:hover {
      background: var(--green);
      color: var(--bg);
    }

    /* ── PROGRESS BARS ── */
    .skill-bars { display: flex; flex-direction: column; gap: 10px; margin-top: 4px; }

    .bar-row { display: flex; flex-direction: column; gap: 3px; }

    .bar-label {
      display: flex;
      justify-content: space-between;
      font-size: 12px;
      color: var(--green-dim);
    }

    .bar-label span:last-child { color: var(--amber); }

    .bar-track {
      height: 6px;
      background: var(--green-dark);
      position: relative;
      overflow: hidden;
    }

    .bar-fill {
      height: 100%;
      background: linear-gradient(90deg, var(--green-dim), var(--green));
      position: relative;
      animation: barGrow 1.2s cubic-bezier(0.4,0,0.2,1) both;
      transform-origin: left;
    }

    .bar-fill::after {
      content: '';
      position: absolute;
      right: 0; top: 0; bottom: 0;
      width: 4px;
      background: #fff;
      opacity: 0.6;
      box-shadow: 0 0 6px var(--green);
    }

    @keyframes barGrow {
      from { width: 0 !important; }
    }

    /* ── CONTACT ── */
    .contact-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(240px, 1fr));
      gap: 10px;
      margin-top: 4px;
    }

    .contact-item {
      display: flex;
      align-items: center;
      gap: 12px;
      border: 1px solid var(--border);
      padding: 12px 16px;
      background: var(--green-faint);
      transition: border-color 0.2s, background 0.2s;
      text-decoration: none;
      color: var(--green);
    }

    .contact-item:hover {
      border-color: var(--green);
      background: rgba(0,255,65,0.1);
    }

    .contact-icon {
      font-size: 18px;
      width: 28px;
      text-align: center;
      flex-shrink: 0;
    }

    .contact-label { font-size: 11px; color: var(--muted); letter-spacing: 0.1em; text-transform: uppercase; }
    .contact-val   { font-size: 13px; color: var(--green); }

    /* ── FOOTER ── */
    .footer-term {
      border: 1px solid var(--border);
      background: var(--bg2);
      padding: 18px 28px;
      margin-top: 24px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      flex-wrap: wrap;
      gap: 10px;
      animation: fadeIn 0.5s 0.5s ease both;
    }

    .footer-left { font-size: 12px; color: var(--muted); }
    .footer-left span { color: var(--green); }

    .status-bar {
      display: flex;
      gap: 20px;
      font-size: 11px;
      color: var(--muted);
    }

    .status-bar .on { color: var(--green); }
    .status-bar .warn { color: var(--amber); }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to   { opacity: 1; transform: translateY(0); }
    }

    /* scrollbar */
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: var(--bg); }
    ::-webkit-scrollbar-thumb { background: var(--green-dark); }
  </style>
</head>
<body>

<div class="cursor" id="cursor"></div>

<div class="page">

  <!-- TOP BAR -->
  <div class="topbar">
    <div class="topbar-left">
      <span>TERMINAL v1.0</span>
      <span>SESSION: ACTIVE</span>
      <span>UMP-OUJDA</span>
    </div>
    <div class="topbar-right">
      <span id="clock">--:--:--</span> &nbsp;|&nbsp; MOROCCO
    </div>
  </div>

  <!-- BOOT HEADER -->
  <div class="boot">
    <div class="boot-line">[<span class="hl">BOOT</span>] Initializing profile... <span class="am">OK</span></div>
    <div class="boot-line">[<span class="hl">LOAD</span>] Reading user data... <span class="am">OK</span></div>
    <div class="boot-line">[<span class="hl">AUTH</span>] Identity confirmed &gt; <span class="cy">Salihi-Ilyass-RF</span></div>
    <div class="ascii-name">ILYASS&nbsp;SALIHI</div>
    <div class="prompt-tagline">
      <span class="hl">~/</span> MIP Student · UMP Morocco ·
      <span class="hl">{ Math · CS · Physics }</span>
      <span class="blink">_</span>
    </div>
  </div>

  <!-- ABOUT ME -->
  <div class="terminal">
    <div class="term-header">
      <div class="term-dots">
        <div class="tdot td-r"></div><div class="tdot td-y"></div><div class="tdot td-g"></div>
      </div>
      <div class="term-title">bash &mdash; <span class="hl">whoami</span></div>
    </div>
    <div class="term-body">
      <div class="cmd"><span class="prompt-sym">root@ump:~$</span><span class="cmd-text"> cat about.txt</span></div>
      <div class="output">
        <div><span class="label">NAME</span>     <span class="val">Ilyass Salihi</span></div>
        <div><span class="label">ALIAS</span>    <span class="val-cy">Salihi-Ilyass-RF</span></div>
        <div><span class="label">PROGRAM</span> <span class="val">MIP — Mathematics, Computer Science, Physics</span></div>
        <div><span class="label">UNIV</span>     <span class="val">Université Mohammed Premier — Oujda, Morocco</span></div>
        <div><span class="label">STATUS</span>  <span class="val-am">Student · Builder · Explorer</span></div>
        <div style="margin-top:10px; color: #2a5c2a;"># Passionate about bridging theory and practice —</div>
        <div style="color: #2a5c2a;"># from mathematical proofs to low-level systems.</div>
      </div>
      <div class="cmd"><span class="prompt-sym">root@ump:~$</span><span class="cmd-text blink"> </span></div>
    </div>
  </div>

  <!-- SKILLS -->
  <div class="terminal">
    <div class="term-header">
      <div class="term-dots">
        <div class="tdot td-r"></div><div class="tdot td-y"></div><div class="tdot td-g"></div>
      </div>
      <div class="term-title">bash &mdash; <span class="hl">skills --list</span></div>
    </div>
    <div class="term-body">
      <div class="cmd"><span class="prompt-sym">root@ump:~$</span><span class="cmd-text"> ./skills.sh --display</span></div>
      <div class="output" style="padding-left:0; margin-top: 10px;">
        <div class="skills-grid">

          <div class="skill-group" data-cat="Web">
            <div class="skill-list">
              <span class="skill-tag">HTML</span>
              <span class="skill-tag">CSS</span>
              <span class="skill-tag">JavaScript</span>
              <span class="skill-tag">PHP</span>
            </div>
          </div>

          <div class="skill-group" data-cat="Languages">
            <div class="skill-list">
              <span class="skill-tag">Python</span>
              <span class="skill-tag">C</span>
              <span class="skill-tag">C++</span>
            </div>
          </div>

          <div class="skill-group" data-cat="Systems">
            <div class="skill-list">
              <span class="skill-tag">Linux</span>
              <span class="skill-tag">Bash</span>
              <span class="skill-tag">Sys Config</span>
            </div>
          </div>

          <div class="skill-group" data-cat="Hardware">
            <div class="skill-list">
              <span class="skill-tag">PC Build</span>
              <span class="skill-tag">Diagnostics</span>
              <span class="skill-tag">Networking</span>
            </div>
          </div>

        </div>

        <div style="margin-top: 22px;">
          <div class="cmd"><span class="prompt-sym">root@ump:~$</span><span class="cmd-text"> ./skills.sh --proficiency</span></div>
          <div style="margin-top: 12px;">
            <div class="skill-bars">
              <div class="bar-row">
                <div class="bar-label"><span>HTML / CSS</span><span>90%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:90%"></div></div>
              </div>
              <div class="bar-row">
                <div class="bar-label"><span>JavaScript</span><span>75%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:75%"></div></div>
              </div>
              <div class="bar-row">
                <div class="bar-label"><span>Python</span><span>80%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:80%"></div></div>
              </div>
              <div class="bar-row">
                <div class="bar-label"><span>C / C++</span><span>70%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:70%"></div></div>
              </div>
              <div class="bar-row">
                <div class="bar-label"><span>PHP</span><span>65%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:65%"></div></div>
              </div>
              <div class="bar-row">
                <div class="bar-label"><span>Linux &amp; Systems</span><span>85%</span></div>
                <div class="bar-track"><div class="bar-fill" style="width:85%"></div></div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>

  <!-- CONTACT -->
  <div class="terminal">
    <div class="term-header">
      <div class="term-dots">
        <div class="tdot td-r"></div><div class="tdot td-y"></div><div class="tdot td-g"></div>
      </div>
      <div class="term-title">bash &mdash; <span class="hl">contact --info</span></div>
    </div>
    <div class="term-body">
      <div class="cmd"><span class="prompt-sym">root@ump:~$</span><span class="cmd-text"> cat /etc/contact.conf</span></div>
      <div class="output" style="padding-left:0; margin-top:12px;">
        <div class="contact-grid">

          <a class="contact-item" href="https://github.com/Salihi-Ilyass-RF" target="_blank">
            <div class="contact-icon">⌥</div>
            <div>
              <div class="contact-label">GitHub</div>
              <div class="contact-val">Salihi-Ilyass-RF</div>
            </div>
          </a>

          <a class="contact-item" href="#" target="_blank">
            <div class="contact-icon">✉</div>
            <div>
              <div class="contact-label">Email</div>
              <div class="contact-val"><span class="__cf_email__" data-cfemail="7801170d0a381d15191114561b1715">[email&#160;protected]</span></div>
            </div>
          </a>

          <a class="contact-item" href="https://www.linkedin.com/in/ilyass-salihi-307193352/" target="_blank">
            <div class="contact-icon">in</div>
            <div>
              <div class="contact-label">LinkedIn</div>
              <div class="contact-val">ilyass-salihi</div>
            </div>
          </a>

        </div>
      </div>
    </div>
  </div>

  <!-- FOOTER -->
  <div class="footer-term">
    <div class="footer-left">
      [<span>PROCESS COMPLETE</span>] &nbsp;·&nbsp; profile loaded for <span>Salihi-Ilyass-RF</span>
    </div>
    <div class="status-bar">
      <span class="on">● ONLINE</span>
      <span class="warn">▲ OPEN TO COLLAB</span>
      <span>© 2024</span>
    </div>
  </div>

</div>

<script data-cfasync="false" src="/cdn-cgi/scripts/5c5dd728/cloudflare-static/email-decode.min.js"></script><script>
  // cursor
  const cur = document.getElementById('cursor');
  document.addEventListener('mousemove', e => {
    cur.style.left = e.clientX + 'px';
    cur.style.top  = e.clientY + 'px';
  });

  // live clock
  function tick() {
    const now = new Date();
    document.getElementById('clock'
