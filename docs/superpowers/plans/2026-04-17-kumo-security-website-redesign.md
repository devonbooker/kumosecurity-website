# Kumo Security Website Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rebuild kumosecurity.com as a clean-light lead-gen landing page for Kumo Assess, the agentic SOC 2 compliance product, with a "Book a Call" CTA throughout.

**Architecture:** Static HTML site — one long-scroll `index.html` homepage plus a thin `/about/index.html`. Shared design tokens in `styles/brand.css`, shared components in `styles/components.css`, page-specific styles in inline `<style>` tags. No build process, no backend.

**Tech Stack:** HTML/CSS, Tailwind CDN (utility overrides only), Google Fonts (Inter + JetBrains Mono), Lucide icons CDN, Vanilla JS (hamburger only)

---

## File Map

| File | Action | What changes |
|------|--------|--------------|
| `styles/brand.css` | Rewrite | Design tokens: dark navy → clean light palette. IBM Plex Mono → JetBrains Mono. |
| `styles/components.css` | Rewrite | Nav, buttons, footer — all updated for light mode. Remove terminal/code component classes (not used on marketing site). |
| `index.html` | Rewrite | Full page — all 8 sections replaced with new light-mode design. |
| `about/index.html` | Rewrite | 4-section credibility page. |
| `brand_assets/kumo-security-brand-guidelines.md` | Edit | Add Kumo Assess marketing name. Retire Section 7 alias lockup. |

---

## Task 1: Rewrite brand.css — Light Mode Design Tokens

**Files:**
- Rewrite: `styles/brand.css`

- [ ] **Step 1: Check the dev server is running**

```bash
# In a separate terminal — only run if not already running
node serve.mjs
# Server starts at http://localhost:3000
```

- [ ] **Step 2: Rewrite styles/brand.css**

Replace the entire file with:

```css
/* =============================================================
   KUMO SECURITY — BRAND FOUNDATION
   Tokens, reset, and base typography.
   Import this on every page before components.css.
   ============================================================= */

@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap');

:root {
  /* Light mode palette */
  --bg:             #F8FAFC;
  --surface:        #FFFFFF;
  --border:         #E2E8F0;
  --border-strong:  #CBD5E1;
  --text:           #0F172A;
  --text-secondary: #475569;
  --text-muted:     #94A3B8;
  --navy:           #0B1A3E;   /* CTA block only — not the page base */
  --accent:         #3B82F6;
  --accent-hover:   #2563EB;
  --accent-bg:      #EFF6FF;
  --accent-border:  #BFDBFE;

  /* Status colors */
  --pass:           #16A34A;
  --pass-bg:        #F0FDF4;
  --pass-border:    #BBF7D0;
  --fail:           #DC2626;
  --fail-bg:        #FEF2F2;
  --fail-border:    #FECACA;
  --partial:        #D97706;
  --partial-bg:     #FFFBEB;
  --partial-border: #FDE68A;
  --unknown:        #64748B;
  --unknown-bg:     #F8FAFC;
  --unknown-border: #E2E8F0;

  /* Typography */
  --font-ui:   "Inter", -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono: "JetBrains Mono", "SFMono-Regular", Consolas, monospace;

  /* Shape */
  --radius-card:  8px;
  --radius-btn:   6px;
  --radius-badge: 4px;
  --transition:   150ms ease;
}

/* RESET */
*, *::before, *::after {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

/* BASE */
html {
  font-family: var(--font-ui);
  background: var(--bg);
  color: var(--text);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-size: 16px;
  line-height: 1.5;
}

a {
  color: inherit;
  text-decoration: none;
}

img {
  display: block;
  max-width: 100%;
}

/* Lucide icons — enforce brand stroke weight */
svg.lucide { stroke-width: 1.5; }
```

- [ ] **Step 3: Commit**

```bash
git add styles/brand.css
git commit -m "feat: rewrite brand.css for clean light design system"
```

---

## Task 2: Rewrite components.css — Nav, Buttons, Footer

**Files:**
- Rewrite: `styles/components.css`

- [ ] **Step 1: Rewrite styles/components.css**

Replace the entire file with:

```css
/* =============================================================
   KUMO SECURITY — COMPONENT LIBRARY
   Reusable UI patterns shared across all pages.
   Requires brand.css to be loaded first.
   ============================================================= */


/* ─── NAV ─────────────────────────────────────────────────── */
.nav {
  position: sticky;
  top: 0;
  z-index: 100;
  height: 52px;
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 24px;
}
.nav-left {
  display: flex;
  align-items: center;
  gap: 32px;
}
.nav-logo {
  display: flex;
  align-items: center;
}
.nav-logo img {
  height: 24px;
  width: auto;
}
.nav-links {
  display: flex;
  align-items: center;
  gap: 4px;
  list-style: none;
}
.nav-links a {
  font-size: 13.5px;
  color: var(--text-secondary);
  padding: 6px 10px;
  border-radius: var(--radius-btn);
  transition: color var(--transition), background var(--transition);
  font-weight: 500;
  letter-spacing: -0.01em;
}
.nav-links a:hover {
  color: var(--text);
  background: #F1F5F9;
}
.nav-right {
  display: flex;
  align-items: center;
  gap: 12px;
}
.nav-right a.nav-link-plain {
  font-size: 13.5px;
  color: var(--text-secondary);
  padding: 6px 10px;
  border-radius: var(--radius-btn);
  transition: color var(--transition);
}
.nav-right a.nav-link-plain:hover { color: var(--text); }

/* Hamburger */
.nav-hamburger {
  display: none;
  flex-direction: column;
  justify-content: center;
  gap: 5px;
  width: 36px;
  height: 36px;
  cursor: pointer;
  background: none;
  border: none;
  padding: 4px;
}
.nav-hamburger span {
  display: block;
  width: 20px;
  height: 1.5px;
  background: var(--text-muted);
  transition: transform 0.2s, opacity 0.2s;
}
.nav-hamburger.open span:nth-child(1) { transform: translateY(6.5px) rotate(45deg); }
.nav-hamburger.open span:nth-child(2) { opacity: 0; }
.nav-hamburger.open span:nth-child(3) { transform: translateY(-6.5px) rotate(-45deg); }

/* Mobile drawer */
.mobile-menu {
  display: none;
  position: fixed;
  top: 52px;
  left: 0;
  right: 0;
  background: var(--surface);
  border-bottom: 1px solid var(--border);
  z-index: 99;
  padding: 12px 0 20px;
}
.mobile-menu.open { display: block; }
.mobile-menu a {
  display: block;
  padding: 12px 24px;
  font-size: 14px;
  color: var(--text-secondary);
  font-weight: 500;
  transition: color var(--transition);
}
.mobile-menu a:hover { color: var(--text); }
.mobile-menu .mobile-divider {
  height: 1px;
  background: var(--border);
  margin: 8px 24px;
}
.mobile-menu .btn-primary {
  margin: 4px 24px 0;
  width: calc(100% - 48px);
  justify-content: center;
}


/* ─── BUTTONS ─────────────────────────────────────────────── */
.btn-primary {
  background: var(--accent);
  color: #FFFFFF;
  font-size: 13.5px;
  font-weight: 600;
  padding: 8px 16px;
  border-radius: var(--radius-btn);
  border: none;
  cursor: pointer;
  transition: background var(--transition);
  display: inline-flex;
  align-items: center;
  gap: 6px;
  letter-spacing: -0.01em;
  min-height: 36px;
}
.btn-primary:hover { background: var(--accent-hover); }
.btn-primary:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}

.btn-secondary {
  background: var(--surface);
  color: #374151;
  font-size: 13.5px;
  font-weight: 500;
  padding: 8px 16px;
  border-radius: var(--radius-btn);
  border: 1px solid var(--border);
  cursor: pointer;
  transition: background var(--transition), border-color var(--transition);
  display: inline-flex;
  align-items: center;
  gap: 6px;
  letter-spacing: -0.01em;
  min-height: 36px;
}
.btn-secondary:hover {
  background: #F1F5F9;
  border-color: var(--border-strong);
}
.btn-secondary:focus-visible {
  outline: 2px solid var(--accent);
  outline-offset: 2px;
}


/* ─── SECTION PRIMITIVES ──────────────────────────────────── */
.section {
  padding: 80px 24px;
  max-width: 1200px;
  margin: 0 auto;
}
.section-label {
  font-size: 11px;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 0.08em;
  color: var(--text-muted);
  margin-bottom: 12px;
  font-family: var(--font-mono);
}
.section-title {
  font-size: clamp(26px, 3.2vw, 40px);
  font-weight: 700;
  letter-spacing: -0.03em;
  line-height: 1.1;
  color: var(--text);
  margin-bottom: 16px;
}
.section-title span { color: var(--text-muted); }
.section-desc {
  font-size: 15px;
  color: var(--text-secondary);
  line-height: 1.7;
  max-width: 480px;
}


/* ─── STATUS BADGES ───────────────────────────────────────── */
.badge {
  display: inline-flex;
  align-items: center;
  font-family: var(--font-mono);
  font-size: 11px;
  font-weight: 500;
  letter-spacing: 0.04em;
  text-transform: uppercase;
  padding: 2px 6px;
  border-radius: var(--radius-badge);
  flex-shrink: 0;
}
.badge-pass    { background: var(--pass-bg);    color: var(--pass);    border: 1px solid var(--pass-border); }
.badge-fail    { background: var(--fail-bg);    color: var(--fail);    border: 1px solid var(--fail-border); }
.badge-partial { background: var(--partial-bg); color: var(--partial); border: 1px solid var(--partial-border); }
.badge-unknown { background: var(--unknown-bg); color: var(--unknown); border: 1px solid var(--unknown-border); }


/* ─── FOOTER ──────────────────────────────────────────────── */
footer {
  background: var(--surface);
  border-top: 1px solid var(--border);
  padding: 40px 24px 28px;
}
.footer-inner {
  max-width: 1200px;
  margin: 0 auto;
}
.footer-top {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 32px;
  padding-bottom: 32px;
  border-bottom: 1px solid var(--border);
  margin-bottom: 24px;
}
.footer-logo {
  display: flex;
  align-items: center;
}
.footer-logo img {
  height: 20px;
  width: auto;
}
.footer-nav {
  display: flex;
  gap: 28px;
  list-style: none;
  align-items: center;
  flex-wrap: wrap;
}
.footer-nav a {
  font-size: 13px;
  color: var(--text-muted);
  transition: color var(--transition);
}
.footer-nav a:hover { color: var(--text); }
.footer-bottom {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 16px;
}
.footer-bottom p {
  font-size: 12px;
  font-family: var(--font-mono);
  color: var(--text-muted);
}
.footer-bottom-links {
  display: flex;
  gap: 20px;
}
.footer-bottom-links a {
  font-size: 12px;
  color: var(--text-muted);
  transition: color var(--transition);
}
.footer-bottom-links a:hover { color: var(--text); }


/* ─── RESPONSIVE ──────────────────────────────────────────── */
@media (max-width: 768px) {
  .nav-links     { display: none; }
  .nav-right     { display: none; }
  .nav-hamburger { display: flex; }

  .section { padding: 56px 20px; }
  .section-title { font-size: 28px; }

  .footer-top    { flex-direction: column; gap: 20px; }
  .footer-bottom { flex-direction: column; gap: 12px; text-align: center; }
  .footer-bottom-links { justify-content: center; }
  footer { padding: 36px 20px 24px; }
}

@media (max-width: 480px) {
  .footer-nav { gap: 16px; }
}
```

- [ ] **Step 2: Commit**

```bash
git add styles/components.css
git commit -m "feat: rewrite components.css for light mode nav, buttons, footer"
```

---

## Task 3: Build index.html — Nav + Hero

**Files:**
- Rewrite: `index.html` (start with this task, add remaining sections in Tasks 4–6)

- [ ] **Step 1: Write index.html with the document shell, nav, mobile menu, and hero**

Replace the entire `index.html` with the following. Sections for social proof through footer will be added in Tasks 4–6 — use placeholder comments for now:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Kumo Security - Automated SOC 2 Compliance for SaaS Startups</title>
  <meta name="description" content="Kumo Assess connects to your AWS account and runs a full SOC 2 compliance scan — automated evidence collection, gap scoring, and remediation guidance." />
  <link rel="icon" type="image/png" href="/brand_assets/Kumo%20Security%20Logo%20-%20Black%20Text.png" />
  <link rel="stylesheet" href="styles/brand.css" />
  <link rel="stylesheet" href="styles/components.css" />
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
  <style>
    /* ── HERO ── */
    .hero {
      display: flex;
      flex-direction: column;
      align-items: center;
      text-align: center;
      padding: 88px 24px 0;
      max-width: 760px;
      margin: 0 auto;
    }
    .hero-badge {
      display: inline-flex;
      align-items: center;
      gap: 6px;
      background: var(--accent-bg);
      border: 1px solid var(--accent-border);
      border-radius: var(--radius-badge);
      padding: 4px 12px;
      font-size: 11px;
      font-family: var(--font-mono);
      color: var(--accent);
      letter-spacing: 0.06em;
      text-transform: uppercase;
      margin-bottom: 24px;
    }
    .hero h1 {
      font-size: clamp(36px, 5.5vw, 60px);
      font-weight: 700;
      letter-spacing: -0.03em;
      line-height: 1.05;
      color: var(--text);
      margin-bottom: 20px;
    }
    .hero h1 span { color: var(--text-muted); }
    .hero p {
      font-size: 17px;
      color: var(--text-secondary);
      max-width: 480px;
      line-height: 1.65;
      margin-bottom: 32px;
    }
    .hero-ctas {
      display: flex;
      align-items: center;
      gap: 12px;
      margin-bottom: 56px;
    }
    .hero-ctas .btn-primary  { font-size: 14px; padding: 10px 20px; }
    .hero-ctas .btn-secondary { font-size: 14px; padding: 10px 20px; }

    /* Dashboard card */
    .dashboard-card {
      width: 100%;
      max-width: 720px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      overflow: hidden;
      box-shadow: 0 4px 24px rgba(0,0,0,0.07);
    }
    .dashboard-header {
      padding: 10px 16px;
      border-bottom: 1px solid var(--border);
      background: var(--bg);
      display: flex;
      align-items: center;
      gap: 8px;
    }
    .dashboard-title {
      font-size: 12px;
      font-family: var(--font-mono);
      color: var(--text-muted);
      margin-left: 4px;
    }
    .dashboard-body { padding: 16px 20px 20px; }
    .stat-row {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 8px;
      margin-bottom: 12px;
    }
    .stat-card {
      border-radius: var(--radius-btn);
      padding: 10px 12px;
      text-align: center;
      border: 1px solid;
    }
    .stat-card.stat-score   { background: var(--pass-bg);    border-color: var(--pass-border); }
    .stat-card.stat-pass    { background: var(--pass-bg);    border-color: var(--pass-border); }
    .stat-card.stat-fail    { background: var(--fail-bg);    border-color: var(--fail-border); }
    .stat-card.stat-partial { background: var(--partial-bg); border-color: var(--partial-border); }
    .stat-number {
      font-size: 22px;
      font-weight: 700;
      font-family: var(--font-mono);
      line-height: 1;
      margin-bottom: 3px;
    }
    .stat-card.stat-score .stat-number,
    .stat-card.stat-pass .stat-number  { color: var(--pass); }
    .stat-card.stat-fail .stat-number    { color: var(--fail); }
    .stat-card.stat-partial .stat-number { color: var(--partial); }
    .stat-label {
      font-size: 11px;
      color: var(--text-secondary);
    }
    .control-list {
      display: flex;
      flex-direction: column;
      gap: 6px;
    }
    .control-row {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 8px 12px;
      border: 1px solid var(--border);
      border-radius: var(--radius-btn);
      border-left-width: 3px;
    }
    .control-row.control-pass    { border-left-color: var(--pass); }
    .control-row.control-fail    { border-left-color: var(--fail); }
    .control-row.control-partial { border-left-color: var(--partial); }
    .control-id {
      font-size: 13px;
      font-weight: 600;
      font-family: var(--font-mono);
      color: var(--text);
      flex-shrink: 0;
    }
    .control-desc {
      font-size: 13px;
      color: var(--text-muted);
      margin-left: auto;
    }

    /* ── RESPONSIVE ── */
    @media (max-width: 768px) {
      .hero { padding: 64px 20px 0; }
      .hero h1 { font-size: 36px; }
      .hero p { font-size: 15px; }
      .hero-ctas { flex-direction: column; width: 100%; }
      .hero-ctas .btn-primary,
      .hero-ctas .btn-secondary { width: 100%; justify-content: center; }
      .stat-row { grid-template-columns: repeat(2, 1fr); }
      .control-desc { display: none; }
    }
  </style>
</head>
<body>

<!-- NAVIGATION -->
<nav class="nav">
  <div class="nav-left">
    <a href="/" class="nav-logo">
      <img src="brand_assets/Kumo%20Security%20Logo%20-%20Black%20Text.png" alt="Kumo Security" />
    </a>
    <ul class="nav-links">
      <li><a href="#features">Products</a></li>
      <li><a href="/about/">About</a></li>
    </ul>
  </div>
  <div class="nav-right">
    <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary">
      Book a Call
      <i data-lucide="arrow-right" style="width:14px;height:14px;"></i>
    </a>
  </div>
  <button class="nav-hamburger" id="hamburger" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>

<!-- MOBILE MENU -->
<div class="mobile-menu" id="mobileMenu">
  <a href="#features">Products</a>
  <a href="/about/">About</a>
  <div class="mobile-divider"></div>
  <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary">Book a Call</a>
</div>

<!-- HERO -->
<section class="hero">
  <div class="hero-badge">Agentic SOC 2 Compliance</div>
  <h1>Know your SOC 2 posture<br><span>in hours, not months.</span></h1>
  <p>Kumo Assess connects to your AWS account and runs a full CC6+CC7 compliance scan — automated evidence collection, gap scoring, and remediation guidance.</p>
  <div class="hero-ctas">
    <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary">
      Book a Call
      <i data-lucide="arrow-right" style="width:14px;height:14px;"></i>
    </a>
    <a href="#how-it-works" class="btn-secondary">
      See how it works
      <i data-lucide="chevron-down" style="width:14px;height:14px;"></i>
    </a>
  </div>

  <!-- Dashboard Card -->
  <div class="dashboard-card">
    <div class="dashboard-header">
      <i data-lucide="terminal" style="width:13px;height:13px;color:var(--text-muted);"></i>
      <span class="dashboard-title">kumo-assess &nbsp;·&nbsp; SOC 2 CC6+CC7 &nbsp;·&nbsp; aws/us-east-1</span>
    </div>
    <div class="dashboard-body">
      <div class="stat-row">
        <div class="stat-card stat-score">
          <div class="stat-number">84</div>
          <div class="stat-label">Score</div>
        </div>
        <div class="stat-card stat-pass">
          <div class="stat-number">18</div>
          <div class="stat-label">Pass</div>
        </div>
        <div class="stat-card stat-fail">
          <div class="stat-number">4</div>
          <div class="stat-label">Fail</div>
        </div>
        <div class="stat-card stat-partial">
          <div class="stat-number">2</div>
          <div class="stat-label">Partial</div>
        </div>
      </div>
      <div class="control-list">
        <div class="control-row control-fail">
          <span class="badge badge-fail">FAIL</span>
          <span class="control-id">CC6.3</span>
          <span class="control-desc">Privileged access review missing</span>
        </div>
        <div class="control-row control-pass">
          <span class="badge badge-pass">PASS</span>
          <span class="control-id">CC6.1</span>
          <span class="control-desc">MFA enforced on all users</span>
        </div>
        <div class="control-row control-partial">
          <span class="badge badge-partial">PARTIAL</span>
          <span class="control-id">CC7.1</span>
          <span class="control-desc">Vulnerability scans incomplete</span>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PLACEHOLDER: social proof, features, how it works, credibility, CTA, footer (Tasks 4–6) -->

<script>
  lucide.createIcons();
  const hamburger = document.getElementById('hamburger');
  const mobileMenu = document.getElementById('mobileMenu');
  hamburger.addEventListener('click', () => {
    hamburger.classList.toggle('open');
    mobileMenu.classList.toggle('open');
  });
  mobileMenu.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      hamburger.classList.remove('open');
      mobileMenu.classList.remove('open');
    });
  });
</script>
</body>
</html>
```

- [ ] **Step 2: Screenshot the hero**

```bash
node screenshot.mjs http://localhost:3000
```

Read the saved PNG from `temporary screenshots/` and verify:
- Nav is white, sticky, height ~52px, black Kumo Security logo visible
- Hero has blue badge, large headline, subheadline, two CTA buttons
- Dashboard card shows 4 stat cards and 3 control rows with correct pass/fail/partial colors
- Page background is `#F8FAFC` (light gray), not dark navy

- [ ] **Step 3: Fix any visual mismatches, re-screenshot until correct**

- [ ] **Step 4: Commit**

```bash
git add index.html
git commit -m "feat: build homepage nav and hero with dashboard card"
```

---

## Task 4: Build index.html — Social Proof Strip + Features

**Files:**
- Modify: `index.html` (replace the placeholder comment with the two new sections)

- [ ] **Step 1: Replace the placeholder comment in index.html with the social proof strip and features section**

Replace the line:
```html
<!-- PLACEHOLDER: social proof, features, how it works, credibility, CTA, footer (Tasks 4–6) -->
```

With:

```html
<!-- SOCIAL PROOF STRIP -->
<div class="proof-strip">
  <div class="proof-inner">
    <div class="proof-stat">
      <div class="proof-number">$30–80k</div>
      <div class="proof-label">avg SOC 2 audit cost</div>
    </div>
    <div class="proof-divider"></div>
    <div class="proof-stat">
      <div class="proof-number">6–12 mo</div>
      <div class="proof-label">typical time to SOC 2</div>
    </div>
    <div class="proof-divider"></div>
    <div class="proof-stat proof-stat--accent">
      <div class="proof-number">&lt;24 hrs</div>
      <div class="proof-label">Kumo Assess turnaround</div>
    </div>
    <div class="proof-divider"></div>
    <div class="proof-stat">
      <div class="proof-number">47</div>
      <div class="proof-label">AWS services scanned</div>
    </div>
  </div>
</div>

<!-- FEATURES -->
<section class="features-section" id="features">
  <div class="features-inner">
    <div class="section-label">What you get</div>
    <h2 class="section-title">Evidence collection. Gap scoring.<br>Remediation guidance.</h2>
    <div class="features-grid">
      <div class="feature-card">
        <div class="feature-icon"><i data-lucide="database" style="width:16px;height:16px;stroke:var(--accent);"></i></div>
        <h3>Automated Evidence</h3>
        <p>Collects from 47 AWS services. No manual screenshots or CSV exports.</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon"><i data-lucide="check-circle" style="width:16px;height:16px;stroke:var(--accent);"></i></div>
        <h3>Control Scoring</h3>
        <p>Each SOC 2 control scored PASS / FAIL / PARTIAL with evidence citations.</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon"><i data-lucide="wrench" style="width:16px;height:16px;stroke:var(--accent);"></i></div>
        <h3>Remediation Guidance</h3>
        <p>Every gap gets a specific fix — not "implement MFA," but exactly which IAM policy to change.</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon"><i data-lucide="shield" style="width:16px;height:16px;stroke:var(--accent);"></i></div>
        <h3>Read-Only by Design</h3>
        <p>Assessment only. No agents writing to your infrastructure. Ever.</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon"><i data-lucide="clock" style="width:16px;height:16px;stroke:var(--accent);"></i></div>
        <h3>Scan History</h3>
        <p>Run scans over time. Track your score improving as you remediate gaps.</p>
      </div>
      <div class="feature-card">
        <div class="feature-icon"><i data-lucide="file-text" style="width:16px;height:16px;stroke:var(--accent);"></i></div>
        <h3>Downloadable Report</h3>
        <p>Export a full markdown report. Share with your auditor or board.</p>
      </div>
    </div>
  </div>
</section>

<!-- PLACEHOLDER: how it works, credibility, CTA, footer (Tasks 5–6) -->
```

- [ ] **Step 2: Add the proof strip and features styles inside the `<style>` tag in index.html**

Add after the `@media (max-width: 768px)` block, before the closing `</style>`:

```css
    /* ── SOCIAL PROOF STRIP ── */
    .proof-strip {
      background: var(--surface);
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      padding: 28px 24px;
      margin-top: 48px;
    }
    .proof-inner {
      max-width: 900px;
      margin: 0 auto;
      display: flex;
      align-items: center;
      justify-content: space-around;
      gap: 16px;
      flex-wrap: wrap;
    }
    .proof-stat { text-align: center; }
    .proof-number {
      font-size: 20px;
      font-weight: 700;
      font-family: var(--font-mono);
      color: var(--text);
      letter-spacing: -0.02em;
      line-height: 1;
      margin-bottom: 4px;
    }
    .proof-stat--accent .proof-number { color: var(--accent); }
    .proof-label {
      font-size: 12px;
      color: var(--text-muted);
    }
    .proof-divider {
      width: 1px;
      height: 32px;
      background: var(--border);
      flex-shrink: 0;
    }

    /* ── FEATURES ── */
    .features-section {
      padding: 80px 24px;
      max-width: 1200px;
      margin: 0 auto;
    }
    .features-inner { }
    .features-grid {
      display: grid;
      grid-template-columns: repeat(3, 1fr);
      gap: 16px;
      margin-top: 40px;
    }
    .feature-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      padding: 24px;
      transition: border-color var(--transition);
    }
    .feature-card:hover { border-color: var(--border-strong); }
    .feature-icon {
      width: 32px;
      height: 32px;
      background: var(--accent-bg);
      border: 1px solid var(--accent-border);
      border-radius: var(--radius-btn);
      display: flex;
      align-items: center;
      justify-content: center;
      margin-bottom: 14px;
    }
    .feature-card h3 {
      font-size: 14px;
      font-weight: 600;
      letter-spacing: -0.01em;
      color: var(--text);
      margin-bottom: 6px;
    }
    .feature-card p {
      font-size: 13px;
      color: var(--text-secondary);
      line-height: 1.65;
    }

    @media (max-width: 900px) {
      .features-grid { grid-template-columns: repeat(2, 1fr); }
    }
    @media (max-width: 768px) {
      .proof-divider { display: none; }
      .proof-inner { gap: 24px; }
      .features-grid { grid-template-columns: 1fr; }
      .features-section { padding: 56px 20px; }
    }
```

- [ ] **Step 3: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000
```

Verify:
- Social proof strip appears below hero with 4 stats, `<24 hrs` in blue
- Features grid is 3 columns with 6 cards, light blue icon containers
- Background between sections transitions correctly

- [ ] **Step 4: Fix mismatches and re-screenshot if needed**

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add social proof strip and features section"
```

---

## Task 5: Build index.html — How It Works + Credibility

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the placeholder comment with the how-it-works and credibility sections**

Replace:
```html
<!-- PLACEHOLDER: how it works, credibility, CTA, footer (Tasks 5–6) -->
```

With:

```html
<!-- HOW IT WORKS -->
<section class="hiw-section" id="how-it-works">
  <div class="hiw-inner">
    <div class="section-label">How it works</div>
    <h2 class="section-title">Three steps to your<br>compliance posture.</h2>
    <div class="hiw-steps">
      <div class="hiw-step">
        <div class="step-num">01</div>
        <div class="step-content">
          <h3>Connect AWS</h3>
          <p>Add a read-only IAM role. Kumo Assess never modifies your environment.</p>
        </div>
      </div>
      <div class="hiw-arrow"><i data-lucide="arrow-right" style="width:20px;height:20px;stroke:var(--border-strong);"></i></div>
      <div class="hiw-step">
        <div class="step-num">02</div>
        <div class="step-content">
          <h3>Run a Scan</h3>
          <p>Select your control family (CC6, CC7). Agents collect evidence across 47 services.</p>
        </div>
      </div>
      <div class="hiw-arrow"><i data-lucide="arrow-right" style="width:20px;height:20px;stroke:var(--border-strong);"></i></div>
      <div class="hiw-step">
        <div class="step-num">03</div>
        <div class="step-content">
          <h3>Review &amp; Fix</h3>
          <p>Get your score, control breakdown, and specific remediation steps.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- CREDIBILITY -->
<section class="cred-section">
  <div class="cred-inner">
    <div class="cred-left">
      <div class="section-label">Why Kumo Security</div>
      <h2 class="section-title">Built by an engineer.<br><span>Not a compliance<br>checkbox factory.</span></h2>
      <p class="section-desc" style="margin-top:16px;">Kumo Assess is an agentic system — Claude-powered agents interpret evidence in context, not regex against config files. Every finding maps to a specific AWS API call.</p>
    </div>
    <div class="cred-right">
      <div class="cred-grid">
        <div class="cred-card">
          <h4>Read-Only by Design</h4>
          <p>Scoped IAM policy. Kumo Assess observes your environment. It never touches it.</p>
        </div>
        <div class="cred-card">
          <h4>Agentic, Not Scripted</h4>
          <p>Claude agents interpret evidence in context — not regex against config files.</p>
        </div>
        <div class="cred-card">
          <h4>AWS-Native</h4>
          <p>Every collector maps to a real AWS API call. No gray-area inference or guesswork.</p>
        </div>
        <div class="cred-card">
          <h4>Open Architecture</h4>
          <p>The assessment logic is transparent. You can inspect exactly what was checked and why.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<!-- PLACEHOLDER: CTA, footer (Task 6) -->
```

- [ ] **Step 2: Add styles for how-it-works and credibility inside the `<style>` tag**

Add after the previous responsive media queries:

```css
    /* ── HOW IT WORKS ── */
    .hiw-section {
      background: var(--surface);
      border-top: 1px solid var(--border);
      border-bottom: 1px solid var(--border);
      padding: 80px 24px;
    }
    .hiw-inner {
      max-width: 900px;
      margin: 0 auto;
    }
    .hiw-steps {
      display: flex;
      align-items: flex-start;
      gap: 16px;
      margin-top: 40px;
    }
    .hiw-step {
      flex: 1;
      background: var(--bg);
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      padding: 24px;
    }
    .step-num {
      font-size: 12px;
      font-weight: 600;
      font-family: var(--font-mono);
      color: var(--accent);
      margin-bottom: 10px;
      letter-spacing: 0.04em;
    }
    .hiw-step h3 {
      font-size: 15px;
      font-weight: 600;
      color: var(--text);
      letter-spacing: -0.01em;
      margin-bottom: 6px;
    }
    .hiw-step p {
      font-size: 13px;
      color: var(--text-secondary);
      line-height: 1.65;
    }
    .hiw-arrow {
      padding-top: 28px;
      flex-shrink: 0;
    }

    /* ── CREDIBILITY ── */
    .cred-section {
      padding: 80px 24px;
      background: var(--bg);
    }
    .cred-inner {
      max-width: 1200px;
      margin: 0 auto;
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 80px;
      align-items: start;
    }
    .cred-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 12px;
    }
    .cred-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: var(--radius-card);
      padding: 20px;
    }
    .cred-card h4 {
      font-size: 13px;
      font-weight: 600;
      color: var(--text);
      letter-spacing: -0.01em;
      margin-bottom: 6px;
    }
    .cred-card p {
      font-size: 12.5px;
      color: var(--text-secondary);
      line-height: 1.65;
    }

    @media (max-width: 768px) {
      .hiw-steps { flex-direction: column; gap: 12px; }
      .hiw-arrow { display: none; }
      .hiw-section { padding: 56px 20px; }
      .cred-inner { grid-template-columns: 1fr; gap: 40px; }
      .cred-section { padding: 56px 20px; }
    }
    @media (max-width: 480px) {
      .cred-grid { grid-template-columns: 1fr; }
    }
```

- [ ] **Step 3: Screenshot and verify**

```bash
node screenshot.mjs http://localhost:3000 hiw-cred
```

Verify:
- How it works shows 3 steps in a row with arrows between (arrows hidden on mobile)
- Credibility section is 2-column with 2×2 card grid on the right
- All backgrounds alternate correctly (white → light gray → white)

- [ ] **Step 4: Fix mismatches and re-screenshot if needed**

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: add how it works and credibility sections"
```

---

## Task 6: Build index.html — Final CTA + Footer

**Files:**
- Modify: `index.html`

- [ ] **Step 1: Replace the remaining placeholder with the CTA section and footer**

Replace:
```html
<!-- PLACEHOLDER: CTA, footer (Task 6) -->
```

With:

```html
<!-- FINAL CTA -->
<section class="cta-section">
  <div class="cta-icon">
    <i data-lucide="arrow-right" style="width:20px;height:20px;stroke:#fff;"></i>
  </div>
  <h2>Ready to see your compliance posture?</h2>
  <p>Book a call. We'll run your first Kumo Assess scan together.</p>
  <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary" style="font-size:14px;padding:11px 24px;">
    Book a Call
    <i data-lucide="arrow-right" style="width:14px;height:14px;"></i>
  </a>
</section>

<!-- FOOTER -->
<footer>
  <div class="footer-inner">
    <div class="footer-top">
      <a href="/" class="footer-logo">
        <img src="brand_assets/Kumo%20Security%20Logo%20-%20Black%20Text.png" alt="Kumo Security" />
      </a>
      <ul class="footer-nav">
        <li><a href="#features">Products</a></li>
        <li><a href="/about/">About</a></li>
        <li><a href="https://github.com/devonbooker" target="_blank" rel="noopener">GitHub</a></li>
        <li><a href="https://www.linkedin.com/in/devonbookerr/" target="_blank" rel="noopener">LinkedIn</a></li>
        <li><a href="mailto:devon@kumosecurity.com">Email</a></li>
      </ul>
    </div>
    <div class="footer-bottom">
      <p>© 2026 Kumo Security.</p>
      <div class="footer-bottom-links">
        <a href="mailto:devon@kumosecurity.com">Contact</a>
      </div>
    </div>
  </div>
</footer>
```

- [ ] **Step 2: Add CTA styles inside the `<style>` tag**

Add after the last responsive block:

```css
    /* ── FINAL CTA ── */
    .cta-section {
      background: var(--navy);
      padding: 96px 24px;
      text-align: center;
    }
    .cta-icon {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      width: 44px;
      height: 44px;
      background: rgba(255,255,255,0.1);
      border: 1px solid rgba(255,255,255,0.2);
      border-radius: var(--radius-btn);
      margin-bottom: 24px;
    }
    .cta-section h2 {
      font-size: clamp(28px, 3.5vw, 44px);
      font-weight: 700;
      letter-spacing: -0.03em;
      color: #FFFFFF;
      margin-bottom: 12px;
    }
    .cta-section p {
      font-size: 16px;
      color: rgba(255,255,255,0.6);
      margin-bottom: 32px;
    }

    @media (max-width: 768px) {
      .cta-section { padding: 72px 20px; }
    }
```

- [ ] **Step 3: Take a full-page screenshot**

```bash
node screenshot.mjs http://localhost:3000 full
```

Read the screenshot and do a complete pass — verify every section from top to bottom:
- Nav: white, sticky, black logo, "Products" and "About" links, "Book a Call" button
- Hero: badge, headline, subheadline, CTAs, dashboard card with stat row and control rows
- Social proof: 4 stats, `<24 hrs` in blue
- Features: 6 cards in 3-col grid
- How it works: 3 steps with arrows
- Credibility: 2-col, 4 trust signal cards
- Final CTA: dark navy background, white text, blue button
- Footer: white bg, logo, nav links, copyright

- [ ] **Step 4: Fix any remaining mismatches, re-screenshot until clean**

- [ ] **Step 5: Commit**

```bash
git add index.html
git commit -m "feat: complete homepage with CTA and footer"
```

---

## Task 7: Build /about Page

**Files:**
- Rewrite: `about/index.html`

- [ ] **Step 1: Rewrite about/index.html**

Replace the entire file with:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>About - Kumo Security</title>
  <meta name="description" content="Kumo Security builds cloud security tools for SaaS startups. Kumo Assess is our agentic SOC 2 compliance assessment product." />
  <link rel="icon" type="image/png" href="/brand_assets/Kumo%20Security%20Logo%20-%20Black%20Text.png" />
  <link rel="stylesheet" href="/styles/brand.css" />
  <link rel="stylesheet" href="/styles/components.css" />
  <script src="https://unpkg.com/lucide@latest/dist/umd/lucide.js"></script>
  <style>
    .about-content {
      max-width: 680px;
      margin: 0 auto;
      padding: 72px 24px 96px;
    }
    .about-content h1 {
      font-size: clamp(28px, 4vw, 42px);
      font-weight: 700;
      letter-spacing: -0.03em;
      color: var(--text);
      margin-bottom: 16px;
    }
    .about-content .lead {
      font-size: 17px;
      color: var(--text-secondary);
      line-height: 1.7;
      margin-bottom: 48px;
      padding-bottom: 48px;
      border-bottom: 1px solid var(--border);
    }
    .about-section { margin-bottom: 48px; padding-bottom: 48px; border-bottom: 1px solid var(--border); }
    .about-section:last-of-type { border-bottom: none; }
    .about-section h2 {
      font-size: 16px;
      font-weight: 600;
      color: var(--text);
      letter-spacing: -0.01em;
      margin-bottom: 16px;
    }
    .about-section p {
      font-size: 14px;
      color: var(--text-secondary);
      line-height: 1.7;
      margin-bottom: 12px;
    }
    .about-section ul {
      list-style: none;
      display: flex;
      flex-direction: column;
      gap: 8px;
    }
    .about-section ul li {
      font-size: 14px;
      color: var(--text-secondary);
      display: flex;
      align-items: flex-start;
      gap: 8px;
      line-height: 1.6;
    }
    .about-section ul li::before {
      content: "—";
      color: var(--text-muted);
      font-family: var(--font-mono);
      flex-shrink: 0;
      margin-top: 1px;
    }
    .stack-tag {
      display: inline-flex;
      align-items: center;
      font-family: var(--font-mono);
      font-size: 12px;
      font-weight: 500;
      padding: 3px 8px;
      border-radius: var(--radius-badge);
      background: var(--bg);
      border: 1px solid var(--border);
      color: var(--text-secondary);
      margin: 2px;
    }
    .about-links {
      display: flex;
      gap: 12px;
      margin-top: 20px;
    }
    .roadmap-row {
      display: flex;
      align-items: center;
      gap: 10px;
      padding: 10px 0;
      border-bottom: 1px solid var(--border);
      font-size: 13px;
    }
    .roadmap-row:last-child { border-bottom: none; }
    .roadmap-status {
      font-family: var(--font-mono);
      font-size: 11px;
      font-weight: 600;
      padding: 2px 7px;
      border-radius: var(--radius-badge);
      flex-shrink: 0;
    }
    .roadmap-status.active   { background: var(--pass-bg);    color: var(--pass);    border: 1px solid var(--pass-border); }
    .roadmap-status.planned  { background: var(--bg);         color: var(--text-muted); border: 1px solid var(--border); }
    .roadmap-name { color: var(--text); font-weight: 500; }
    .roadmap-desc { color: var(--text-muted); margin-left: auto; font-size: 12px; }
    @media (max-width: 768px) {
      .about-content { padding: 56px 20px 72px; }
      .roadmap-desc { display: none; }
    }
  </style>
</head>
<body>

<!-- NAVIGATION -->
<nav class="nav">
  <div class="nav-left">
    <a href="/" class="nav-logo">
      <img src="/brand_assets/Kumo%20Security%20Logo%20-%20Black%20Text.png" alt="Kumo Security" />
    </a>
    <ul class="nav-links">
      <li><a href="/#features">Products</a></li>
      <li><a href="/about/" style="color:var(--text);">About</a></li>
    </ul>
  </div>
  <div class="nav-right">
    <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary">
      Book a Call
      <i data-lucide="arrow-right" style="width:14px;height:14px;"></i>
    </a>
  </div>
  <button class="nav-hamburger" id="hamburger" aria-label="Menu">
    <span></span><span></span><span></span>
  </button>
</nav>
<div class="mobile-menu" id="mobileMenu">
  <a href="/#features">Products</a>
  <a href="/about/">About</a>
  <div class="mobile-divider"></div>
  <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary">Book a Call</a>
</div>

<div class="about-content">

  <h1>About Kumo Security</h1>
  <p class="lead">Kumo Security builds cloud security tooling for SaaS startups. The first product is Kumo Assess — an agentic SOC 2 compliance assessment that connects to your AWS account and runs a full control gap analysis in hours, not months.</p>

  <div class="about-section">
    <h2>Background</h2>
    <ul>
      <li>Cloud and infrastructure security — AWS, Terraform, Ansible, Docker, Kubernetes</li>
      <li>Security engineering — container security, WAF, TLS/PKI, authentication and authorization</li>
      <li>Compliance frameworks — SOC 2, ISO 27001, CMMC, GDPR in cloud environments</li>
      <li>Observability and CI/CD — Grafana, Prometheus, GitHub Actions</li>
      <li>Languages — Go, TypeScript; AI tooling built on Anthropic/Claude</li>
    </ul>
    <div style="margin-top:16px;">
      <span class="stack-tag">AWS</span>
      <span class="stack-tag">Go</span>
      <span class="stack-tag">Terraform</span>
      <span class="stack-tag">Kubernetes</span>
      <span class="stack-tag">Claude API</span>
      <span class="stack-tag">SOC 2</span>
      <span class="stack-tag">CMMC</span>
    </div>
    <div class="about-links">
      <a href="https://github.com/devonbooker" target="_blank" rel="noopener" class="btn-secondary" style="font-size:13px;padding:7px 14px;">
        <i data-lucide="github" style="width:14px;height:14px;"></i> GitHub
      </a>
      <a href="https://www.linkedin.com/in/devonbookerr/" target="_blank" rel="noopener" class="btn-secondary" style="font-size:13px;padding:7px 14px;">
        <i data-lucide="linkedin" style="width:14px;height:14px;"></i> LinkedIn
      </a>
    </div>
  </div>

  <div class="about-section">
    <h2>What We're Building</h2>
    <p>Kumo Assess is an agentic compliance system. Claude agents collect evidence from your AWS environment, score each SOC 2 control, and generate specific remediation guidance — all in a single guided session. Currently covers SOC 2 CC6 (Logical Access) and CC7 (System Operations).</p>
    <p>Kumo Assess is not a checkbox tool. It's built on direct AWS API calls, not heuristics. The assessment logic is transparent and inspectable.</p>
    <div style="margin-top:20px;border:1px solid var(--border);border-radius:var(--radius-card);overflow:hidden;">
      <div class="roadmap-row" style="padding:10px 16px;background:var(--bg);border-bottom:1px solid var(--border);">
        <span style="font-size:11px;font-family:var(--font-mono);color:var(--text-muted);text-transform:uppercase;letter-spacing:0.06em;">Framework</span>
        <span class="roadmap-desc">Status</span>
      </div>
      <div class="roadmap-row" style="padding:10px 16px;">
        <span class="roadmap-status active">Active</span>
        <span class="roadmap-name">SOC 2</span>
        <span class="roadmap-desc">CC6 + CC7 (AWS)</span>
      </div>
      <div class="roadmap-row" style="padding:10px 16px;">
        <span class="roadmap-status planned">Planned</span>
        <span class="roadmap-name">ISO 27001</span>
        <span class="roadmap-desc">AWS controls mapping</span>
      </div>
      <div class="roadmap-row" style="padding:10px 16px;">
        <span class="roadmap-status planned">Planned</span>
        <span class="roadmap-name">CMMC</span>
        <span class="roadmap-desc">Level 2 (NIST SP 800-171)</span>
      </div>
    </div>
  </div>

  <div class="about-section">
    <h2>Contact</h2>
    <p>If you're a SaaS startup working toward SOC 2 and want to run a Kumo Assess scan on your AWS environment, book a 30-minute call.</p>
    <div style="display:flex;gap:12px;margin-top:20px;flex-wrap:wrap;">
      <a href="https://calendly.com/devon-kumosecurity/30min" target="_blank" rel="noopener" class="btn-primary" style="font-size:13px;padding:9px 18px;">
        Book a Call
        <i data-lucide="arrow-right" style="width:14px;height:14px;"></i>
      </a>
      <a href="mailto:devon@kumosecurity.com" class="btn-secondary" style="font-size:13px;padding:9px 18px;">
        <i data-lucide="mail" style="width:14px;height:14px;"></i>
        devon@kumosecurity.com
      </a>
    </div>
  </div>

</div>

<footer>
  <div class="footer-inner">
    <div class="footer-top">
      <a href="/" class="footer-logo">
        <img src="/brand_assets/Kumo%20Security%20Logo%20-%20Black%20Text.png" alt="Kumo Security" />
      </a>
      <ul class="footer-nav">
        <li><a href="/#features">Products</a></li>
        <li><a href="/about/">About</a></li>
        <li><a href="https://github.com/devonbooker" target="_blank" rel="noopener">GitHub</a></li>
        <li><a href="https://www.linkedin.com/in/devonbookerr/" target="_blank" rel="noopener">LinkedIn</a></li>
        <li><a href="mailto:devon@kumosecurity.com">Email</a></li>
      </ul>
    </div>
    <div class="footer-bottom">
      <p>© 2026 Kumo Security.</p>
      <div class="footer-bottom-links">
        <a href="mailto:devon@kumosecurity.com">Contact</a>
      </div>
    </div>
  </div>
</footer>

<script>
  lucide.createIcons();
  const hamburger = document.getElementById('hamburger');
  const mobileMenu = document.getElementById('mobileMenu');
  hamburger.addEventListener('click', () => {
    hamburger.classList.toggle('open');
    mobileMenu.classList.toggle('open');
  });
  mobileMenu.querySelectorAll('a').forEach(link => {
    link.addEventListener('click', () => {
      hamburger.classList.remove('open');
      mobileMenu.classList.remove('open');
    });
  });
</script>
</body>
</html>
```

- [ ] **Step 2: Screenshot and verify the about page**

```bash
node screenshot.mjs http://localhost:3000/about/ about
```

Verify:
- Nav matches homepage nav, "About" link is active (darker text)
- Background is `#F8FAFC`, all text is dark on light
- 3 sections: Background (skills + stack tags + links), What We're Building (roadmap table), Contact (CTA buttons)
- Footer matches homepage footer

- [ ] **Step 3: Fix mismatches and re-screenshot if needed**

- [ ] **Step 4: Commit**

```bash
git add about/index.html
git commit -m "feat: build /about credibility page"
```

---

## Task 8: Update Brand Guidelines

**Files:**
- Modify: `brand_assets/kumo-security-brand-guidelines.md`

- [ ] **Step 1: Update Section 0.1 to add Kumo Assess marketing name**

In `brand_assets/kumo-security-brand-guidelines.md`, find the product table row for kumo-assess:

```markdown
| **kumo-assess** | Active | Agentic SOC 2 compliance assessment - read-only cloud environment scanning, control gap analysis, and scoring |
```

Replace with:

```markdown
| **Kumo Assess** | Active | Agentic SOC 2 compliance assessment - read-only cloud environment scanning, control gap analysis, and scoring. Repo: `kumo-assess`. |
```

And update the naming rule paragraph to read:

```markdown
Naming rule: the product's marketing name is **Kumo Assess** (title case, two words). The repo is `kumo-assess` (lowercase-hyphenated). Use `Kumo Assess` in all external copy, the website, and UI labels. Use `kumo-assess` only in code, CLI references, and technical documentation.
```

- [ ] **Step 2: Update Section 7 to retire the personal alias lockup from the website**

Find and replace Section 7:

```markdown
## 7. Professional Alias & Lockup

When pairing the logo with text, use a monospaced lockup:

`[alias] // cloud security`

*Example:* `devonbooker // cloud security`
```

Replace with:

```markdown
## 7. Professional Alias & Lockup

> **Note:** This lockup is retired from kumosecurity.com as of the 2026 redesign. It may still be used on personal profiles (GitHub bio, LinkedIn headline).

When used on personal profiles (not the main website), the monospaced lockup format is:

`[alias] // cloud security`

*Example:* `devonbooker // cloud security`
```

- [ ] **Step 3: Commit**

```bash
git add brand_assets/kumo-security-brand-guidelines.md
git commit -m "docs: update brand guidelines — Kumo Assess name, retire alias lockup from site"
```

---

## Task 9: Final Screenshot Pass

- [ ] **Step 1: Screenshot the full homepage**

```bash
node screenshot.mjs http://localhost:3000 final-home
```

- [ ] **Step 2: Screenshot the about page**

```bash
node screenshot.mjs http://localhost:3000/about/ final-about
```

- [ ] **Step 3: Do a final visual review of both screenshots**

Check for:
- No dark navy backgrounds on the page except the final CTA block
- Logo is the black-text variant (readable on white/light-gray backgrounds)
- Calendly URL appears on all "Book a Call" buttons (check nav, hero, CTA block, about page)
- No references to CMMC anywhere on either page
- Fonts loading: Inter for headings/body, JetBrains Mono for badges/IDs/code
- Mobile: take a second screenshot with `node screenshot.mjs http://localhost:3000 final-mobile` and check the responsive layout is clean

- [ ] **Step 4: Fix any issues found, re-screenshot until clean**

- [ ] **Step 5: Final commit**

```bash
git add -A
git commit -m "feat: complete Kumo Security website redesign — clean light, Kumo Assess positioning"
```
