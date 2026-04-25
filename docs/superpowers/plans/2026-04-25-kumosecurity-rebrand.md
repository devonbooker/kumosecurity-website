# kumosecurity.com Rebrand Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Rewrite `index.html` to replace the "SOC 2 readiness consulting" positioning with the CEO-locked attack-path framing ("The Wedge"), strip all references to the now-private `kumo-security/kumo-assess` repo, and substitute the OSS trust signal with the layered (sample-report + IAM-role guarantee + named-consultant) replacement.

**Architecture:** Single-pass surgical Edit operations against `C:/Users/Devon/Documents/kumosecurity-website/index.html`. CSS untouched. Same nav, footer, and dashboard mockup HTML structure. Verification via grep (old strings gone, new strings present) plus screenshot QA on localhost per the website repo's `CLAUDE.md` workflow.

**Tech Stack:** Static HTML, inline CSS in `<style>`, Tailwind not used here, Lucide icons via CDN. Local dev server via `node serve.mjs` on port 3000. Screenshot tool via `node screenshot.mjs <url>`.

**Source spec:** `docs/superpowers/specs/2026-04-25-kumosecurity-rebrand-design.md`

---

## File Structure

**Modified:**
- `C:/Users/Devon/Documents/kumosecurity-website/index.html` — all 13 substantive edits land here

**Created (none):** No new files. CSS, brand assets, and sibling pages all stay as-is.

**Reference (read-only):**
- `C:/Users/Devon/Documents/kumosecurity-website/CLAUDE.md` — defines the screenshot QA loop the engineer will use
- `C:/Users/Devon/Documents/kumosecurity-website/serve.mjs` — local server entry
- `C:/Users/Devon/Documents/kumosecurity-website/screenshot.mjs` — screenshot tool entry
- `C:/Users/Devon/Documents/kumosecurity-website/docs/superpowers/specs/2026-04-25-kumosecurity-rebrand-design.md` — the spec being executed

---

## Task 0: Setup and baseline

**Files:**
- Read: `C:/Users/Devon/Documents/kumosecurity-website/CLAUDE.md`
- Read: `C:/Users/Devon/Documents/kumosecurity-website/index.html`

- [ ] **Step 1: Read the website repo's CLAUDE.md to confirm screenshot workflow**

```bash
cat C:/Users/Devon/Documents/kumosecurity-website/CLAUDE.md
```

Expected: file describes `node serve.mjs` to start dev server and `node screenshot.mjs http://localhost:3000` to take screenshots saved to `temporary screenshots/`.

- [ ] **Step 2: Confirm working tree is clean**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git status
```

Expected: `nothing to commit, working tree clean` (the spec from the prior commit is already landed).

- [ ] **Step 3: Start the dev server in the background**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node serve.mjs &
```

Expected: server logs that it's listening on port 3000. Leave it running for the rest of this plan.

- [ ] **Step 4: Take a baseline screenshot of the current site**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node screenshot.mjs http://localhost:3000 baseline-pre-rebrand
```

Expected: file written to `temporary screenshots/screenshot-N-baseline-pre-rebrand.png`. This is the "before" image for the QA pass at Task 13.

---

## Task 1: SEO meta — title and description

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 6-7)

- [ ] **Step 1: Edit the `<title>` tag**

Use Edit tool:

```
old_string:   <title>Devon Booker - SOC 2 readiness for AWS startups</title>
new_string:   <title>Kumo Security - AWS attack-path analysis for startups</title>
```

- [ ] **Step 2: Edit the `<meta name="description">`**

Use Edit tool:

```
old_string:   <meta name="description" content="I'm Devon, a security engineer. I assess your AWS environment for SOC 2 gaps and deliver the remediation code that closes them. Fixed-scope engagements, starting at $2,500." />
new_string:   <meta name="description" content="Find the AWS attack paths your compliance tool misses. Read-only assessment, prioritized findings, Terraform remediation. Works alongside Vanta and Drata. Starting at $2,500." />
```

- [ ] **Step 3: Verify both edits**

```bash
grep -n "<title>" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n "meta name=\"description\"" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: title shows `Kumo Security - AWS attack-path analysis for startups`, description shows the new content. No occurrences of `SOC 2 readiness for AWS startups` in `<title>`.

- [ ] **Step 4: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: update title and meta description to attack-path framing"
```

---

## Task 2: Hero copy — badge, h1, lead, CTAs, remove GitHub link

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 778-795)

- [ ] **Step 1: Replace hero badge**

Use Edit tool:

```
old_string:  <div class="hero-badge">SOC 2 consulting for AWS startups</div>
new_string:  <div class="hero-badge">Compliant but still vulnerable</div>
```

- [ ] **Step 2: Replace h1**

Use Edit tool:

```
old_string:  <h1>SOC 2 readiness for AWS startups.<br><span>In weeks, not months.</span></h1>
new_string:  <h1>Find the AWS attack paths<br><span>your compliance tool misses.</span></h1>
```

Note: the `<span>` styling renders the second line in muted color. Keeping that visual treatment by putting `your compliance tool misses` inside the span.

- [ ] **Step 3: Replace lead paragraph**

Use Edit tool:

```
old_string:  <p class="lead">I'm Devon, a security engineer. I'll assess your AWS environment, show you exactly where your SOC 2 gaps are, and deliver the remediation code that closes them.</p>
new_string:  <p class="lead">Before they hit production. Built for engineers, priced for startups, works alongside Vanta and Drata.</p>
```

- [ ] **Step 4: Punch line — verify it's unchanged**

```bash
grep -n "Powered by agents I built" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: line 781 (or near it) shows the original punch line `Powered by agents I built. Shipped by someone who actually reads your Terraform.` — no edit needed.

- [ ] **Step 5: Remove the GitHub trust link below CTAs**

Use Edit tool to delete the entire `<a class="hero-github">` block:

```
old_string:  <a href="https://github.com/kumo-security/kumo-assess" target="_blank" rel="noopener" class="hero-github">
    <i data-lucide="github" style="width:13px;height:13px;"></i>
    The tool is open source. View kumo-assess on GitHub
    <i data-lucide="arrow-right" style="width:12px;height:12px;"></i>
  </a>

  <!-- Hero visual: photo + dashboard -->
new_string:  <!-- Hero visual: photo + dashboard -->
```

- [ ] **Step 6: Verify all hero edits**

```bash
grep -n "hero-badge\|hero-github\|<h1>\|<p class=\"lead\">" C:/Users/Devon/Documents/kumosecurity-website/index.html | head -20
```

Expected:
- `hero-badge` line shows `Compliant but still vulnerable`
- `<h1>` line shows `Find the AWS attack paths<br><span>your compliance tool misses.</span>`
- `<p class="lead">` line shows the new lead
- `hero-github` returns NO matches (block deleted)

- [ ] **Step 7: Re-screenshot and visual sanity check**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node screenshot.mjs http://localhost:3000 hero-rewrite
```

Open the screenshot. Confirm: badge text is the new hook, h1 is the new headline, no GitHub link below the CTAs, dashboard mockup still visible (it's the next task).

- [ ] **Step 8: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: hero badge, h1, lead — attack-path framing; remove GitHub link"
```

---

## Task 3: Hero dashboard mockup — re-content as attack-path findings

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 803-845)

- [ ] **Step 1: Replace the dashboard header title**

Use Edit tool:

```
old_string:        <span class="dashboard-title">kumo-assess &nbsp;·&nbsp; SOC 2 CC6+CC7 &nbsp;·&nbsp; aws/us-east-1</span>
new_string:        <span class="dashboard-title">kumo-assess &nbsp;·&nbsp; AWS attack-path scan &nbsp;·&nbsp; aws/us-east-1</span>
```

- [ ] **Step 2: Replace the 4 stat cards**

Use Edit tool to replace the entire `<div class="stat-row">` block:

```
old_string:        <div class="stat-row">
          <div class="stat-card stat-score">
            <div class="stat-number">35</div>
            <div class="stat-label">Score</div>
          </div>
          <div class="stat-card stat-pass">
            <div class="stat-number">0</div>
            <div class="stat-label">Pass</div>
          </div>
          <div class="stat-card stat-fail">
            <div class="stat-number">2</div>
            <div class="stat-label">Fail</div>
          </div>
          <div class="stat-card stat-partial">
            <div class="stat-number">4</div>
            <div class="stat-label">Partial</div>
          </div>
        </div>
new_string:        <div class="stat-row">
          <div class="stat-card stat-score">
            <div class="stat-number">35</div>
            <div class="stat-label">Score</div>
          </div>
          <div class="stat-card stat-fail">
            <div class="stat-number">3</div>
            <div class="stat-label">Critical paths</div>
          </div>
          <div class="stat-card stat-fail">
            <div class="stat-number">1</div>
            <div class="stat-label">Path to root</div>
          </div>
          <div class="stat-card stat-partial">
            <div class="stat-number">7</div>
            <div class="stat-label">Total findings</div>
          </div>
        </div>
```

Note: `stat-pass` class swapped to `stat-fail` for the second card (it's now "Critical paths" — a fail-colored count) and the third card uses `stat-fail` (Path to root is critical). Total findings keeps `stat-partial` as the neutral count.

- [ ] **Step 3: Replace the 3 control rows with 3 attack-path rows**

Use Edit tool to replace the entire `<div class="control-list">` block:

```
old_string:        <div class="control-list">
          <div class="control-row control-fail">
            <span class="badge badge-fail">FAIL</span>
            <span class="control-id">CC6.3</span>
            <span class="control-desc">Privileged access review not implemented</span>
          </div>
          <div class="control-row control-partial">
            <span class="badge badge-partial">PARTIAL</span>
            <span class="control-id">CC6.7</span>
            <span class="control-desc">KMS key rotation inconsistent</span>
          </div>
          <div class="control-row control-partial">
            <span class="badge badge-partial">PARTIAL</span>
            <span class="control-id">CC7.2</span>
            <span class="control-desc">CloudTrail alerting gaps</span>
          </div>
        </div>
new_string:        <div class="control-list">
          <div class="control-row control-fail">
            <span class="badge badge-fail">CRITICAL</span>
            <span class="control-id">PATH-01</span>
            <span class="control-desc">developer-role &rarr; iam:PassRole &rarr; admin-role <span style="color:var(--text-muted);font-family:var(--font-mono);font-size:11px;">(CC6.3)</span></span>
          </div>
          <div class="control-row control-partial">
            <span class="badge badge-partial">HIGH</span>
            <span class="control-id">PATH-02</span>
            <span class="control-desc">ec2-instance-profile &rarr; s3:* on cust-data-prod <span style="color:var(--text-muted);font-family:var(--font-mono);font-size:11px;">(CC6.7)</span></span>
          </div>
          <div class="control-row control-partial">
            <span class="badge badge-partial">HIGH</span>
            <span class="control-id">PATH-03</span>
            <span class="control-desc">ci-deploy-role &rarr; AssumeRole * &rarr; unrestricted <span style="color:var(--text-muted);font-family:var(--font-mono);font-size:11px;">(CC6.3, CC7.2)</span></span>
          </div>
        </div>
```

Note: `&rarr;` is the HTML entity for the right-arrow (→) used in attack chains. The CC tags are inline-styled (small mono muted) to match the spec without requiring CSS edits.

- [ ] **Step 4: Verify dashboard edits**

```bash
grep -n "PATH-01\|PATH-02\|PATH-03\|Critical paths\|attack-path scan" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: 5 lines returned (one per match). Old terms `KMS key rotation` and `CloudTrail alerting gaps` should be gone:

```bash
grep -n "KMS key rotation\|CloudTrail alerting gaps\|Privileged access review not implemented\|SOC 2 CC6+CC7" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: zero matches.

- [ ] **Step 5: Re-screenshot and visual check**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node screenshot.mjs http://localhost:3000 hero-dashboard
```

Open the screenshot. Confirm: dashboard header reads "AWS attack-path scan", four stat cards (Score / Critical paths / Path to root / Total findings), three rows showing PATH-01/02/03 with arrow chains. CC tags should be small muted text inline. If CC tag wraps awkwardly, that's acceptable — content is what matters.

- [ ] **Step 6: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: hero dashboard mockup — attack-path findings"
```

---

## Task 4: Case study hook copy

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (around line 859)

- [ ] **Step 1: Edit the case-study paragraph**

Use Edit tool:

```
old_string:      <p>It scored 35 out of 100. I wrote up every finding, the remediation, and what it cost to fix - Terraform diffs included. If you want to see what an honest SOC 2 readiness assessment actually looks like, read the writeup.</p>
new_string:      <p>It scored 35 out of 100. I wrote up every finding, the remediation, and what it cost to fix - Terraform diffs included. If you want to see what an honest AWS attack-path scan actually looks like, read the writeup.</p>
```

- [ ] **Step 2: Verify**

```bash
grep -n "honest AWS attack-path scan\|honest SOC 2 readiness assessment" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: one match for `honest AWS attack-path scan`, zero for the old SOC 2 phrasing.

- [ ] **Step 3: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: case study hook copy — attack-path framing"
```

---

## Task 5: Problem section — full rewrite (3 cards)

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 869-889)

This is the section that violates CEO Risk #4 ("feeder, not replacement"). Three cards get rewritten and the section title changes.

- [ ] **Step 1: Replace section title**

Use Edit tool:

```
old_string:    <h2 class="section-title">SOC 2 readiness is overpriced<br>and under-delivered.</h2>
new_string:    <h2 class="section-title">There's a gap between<br>compliance and security.</h2>
```

- [ ] **Step 2: Replace Card 1 (Traditional readiness → Compliance tools)**

Use Edit tool:

```
old_string:    <div class="problem-card">
      <span class="problem-stat">$15k-50k</span>
      <h3>Traditional readiness</h3>
      <p>Most consulting engagements take 6 to 12 weeks and cost $15k to $50k. Much of the time goes to evidence collection that could be automated.</p>
    </div>
    <div class="problem-card">
      <span class="problem-stat">$25k+/yr</span>
      <h3>Compliance SaaS</h3>
      <p>Vanta and Drata are priced for Series A and up. They're mostly dashboards. The AWS-technical work still falls on you.</p>
    </div>
    <div class="problem-card">
      <span class="problem-stat">Six figures</span>
      <h3>The hidden cost</h3>
      <p>Startups end up paying six figures combined before a single control is actually fixed in their infrastructure.</p>
    </div>
new_string:    <div class="problem-card">
      <span class="problem-stat">$5k-$30k/yr</span>
      <h3>Compliance tools</h3>
      <p>Vanta and Drata get you to SOC 2. Necessary - and they don't see your AWS attack surface. That's by design; they're audit infrastructure.</p>
    </div>
    <div class="problem-card">
      <span class="problem-stat">$50k-$200k+/yr</span>
      <h3>Enterprise CNAPP</h3>
      <p>Wiz and Orca find the paths. Priced for security teams with the headcount and budget you don't have yet.</p>
    </div>
    <div class="problem-card">
      <span class="problem-stat">The wedge</span>
      <h3>What's missing</h3>
      <p>A scan a startup CTO can act on - alongside the compliance tool you already pay for. That's where I sit.</p>
    </div>
```

- [ ] **Step 3: Verify the rewrite**

```bash
grep -n "There's a gap between\|Compliance tools\|Enterprise CNAPP\|The wedge" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n "they're mostly dashboards\|Compliance SaaS\|Traditional readiness\|Six figures" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: first grep returns 4 matches; second returns ZERO matches (all old anti-Vanta language is gone).

- [ ] **Step 4: Re-screenshot and visual check**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node screenshot.mjs http://localhost:3000 problem-section
```

Confirm: section title is "There's a gap between compliance and security", three cards render correctly, "The wedge" stat label displays without breaking the card visually (per spec, fall back to `$2k-$10k` as the stat if the label-as-stat looks broken — but try the label first).

- [ ] **Step 5: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: problem section — feeder posture, no anti-Vanta language"
```

---

## Task 6: Approach section — Step 01 and Step 02 copy

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 897-911)

- [ ] **Step 1: Replace Step 01 SCAN h3 and body**

Use Edit tool:

```
old_string:        <div class="step-content">
          <h3>Agent-driven assessment</h3>
          <p>I run a read-only scan of your AWS environment using agents I built. Thirty minutes. You approve the IAM role before anything starts.</p>
        </div>
new_string:        <div class="step-content">
          <h3>Agent-driven attack-path scan</h3>
          <p>I run a read-only scan that maps your IAM graph and surfaces the paths an attacker could actually chain. Thirty minutes. You approve the IAM role before anything starts.</p>
        </div>
```

- [ ] **Step 2: Replace Step 02 REVIEW h3 and body**

Use Edit tool:

```
old_string:        <div class="step-content">
          <h3>Walk every gap on a call</h3>
          <p>We go through every finding together. You get the full markdown report with evidence citations and priorities scored against your audit timeline.</p>
        </div>
new_string:        <div class="step-content">
          <h3>Walk every path on a call</h3>
          <p>We go through every path together, prioritized by blast radius. You get the full markdown report with evidence citations and severity scored against your audit timeline.</p>
        </div>
```

- [ ] **Step 3: Step 03 REMEDIATE — verify unchanged**

```bash
grep -n "Terraform, not slide decks" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: one match. No edit needed — this h3 is unchanged per the spec.

- [ ] **Step 4: Verify the rewrite**

```bash
grep -n "Agent-driven attack-path scan\|Walk every path on a call\|prioritized by blast radius" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n "Agent-driven assessment\|Walk every gap on a call" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: first grep returns 3 matches; second returns ZERO.

- [ ] **Step 5: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: approach section — attack-path scan + walk every path"
```

---

## Task 7: What's covered section — relabel

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 927-960)

- [ ] **Step 1: Replace section title**

Use Edit tool:

```
old_string:    <h2 class="section-title">The AWS-technical part of SOC 2,<br>where most startups fail.</h2>
new_string:    <h2 class="section-title">What kumo-assess looks for.</h2>
```

- [ ] **Step 2: Replace the 5 covered-row entries (CC6 through CC7)**

Use Edit tool:

```
old_string:    <div class="covered-list">
    <div class="covered-row">
      <span class="covered-id">CC6</span>
      <span class="covered-desc">Logical Access</span>
      <span class="covered-scope">IAM · MFA · password policy · least privilege</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC6.6</span>
      <span class="covered-desc">Boundary Protection</span>
      <span class="covered-scope">CloudTrail</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC6.7</span>
      <span class="covered-desc">Data Protection</span>
      <span class="covered-scope">S3 · KMS</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC6.8</span>
      <span class="covered-desc">Change Detection</span>
      <span class="covered-scope">Config · Security Hub</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC7</span>
      <span class="covered-desc">System Operations</span>
      <span class="covered-scope">monitoring · incident response</span>
    </div>
new_string:    <div class="covered-list">
    <div class="covered-row">
      <span class="covered-id">CC6</span>
      <span class="covered-desc">Privilege escalation</span>
      <span class="covered-scope">IAM · MFA · least privilege · PassRole abuse</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC6.6</span>
      <span class="covered-desc">Audit trail integrity</span>
      <span class="covered-scope">CloudTrail coverage · tamper resistance</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC6.7</span>
      <span class="covered-desc">Data exposure paths</span>
      <span class="covered-scope">S3 · KMS</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC6.8</span>
      <span class="covered-desc">Change detection coverage</span>
      <span class="covered-scope">Config · Security Hub</span>
    </div>
    <div class="covered-row">
      <span class="covered-id">CC7</span>
      <span class="covered-desc">Detection &amp; response</span>
      <span class="covered-scope">monitoring · incident response</span>
    </div>
```

Note: pending row stays untouched.

- [ ] **Step 3: Replace the footnote**

Use Edit tool:

```
old_string:  <p class="covered-footnote">Built on direct AWS API calls, not heuristics. Five collectors today: IAM, CloudTrail, S3, Security Hub, Config. The assessment logic is transparent and open source.</p>
new_string:  <p class="covered-footnote">Built on direct AWS API calls, not heuristics. Five collectors today: IAM, CloudTrail, S3, Security Hub, Config. Read-only by construction. Methodology documented in the sample report.</p>
```

- [ ] **Step 4: Verify**

```bash
grep -n "What kumo-assess looks for\|Privilege escalation\|Audit trail integrity\|Data exposure paths\|Detection &amp; response\|Read-only by construction" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n "Logical Access\|Boundary Protection\|Data Protection\|System Operations\|transparent and open source" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: first grep returns 6 matches; second returns ZERO.

- [ ] **Step 5: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: what's covered — attack-path categories, drop OSS reference in footnote"
```

---

## Task 8: Pricing tiers — rename and polish bullets

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 970-1006)

- [ ] **Step 1: Replace Tier 1 title and bullet**

Use Edit tool:

```
old_string:        <div class="package-name">Tier 1</div>
        <div class="package-title">Assessment</div>
        <div class="package-price">$2,500</div>
        <div class="package-price-note">Delivered in 48 hours</div>
        <div class="package-divider"></div>
        <ul class="package-features">
          <li>Full read-only scan of your AWS environment</li>
          <li>Markdown report with every gap scored and prioritized</li>
          <li>1-hour walkthrough call</li>
          <li>48-hour turnaround</li>
        </ul>
new_string:        <div class="package-name">Tier 1</div>
        <div class="package-title">Attack-path scan</div>
        <div class="package-price">$2,500</div>
        <div class="package-price-note">Delivered in 48 hours</div>
        <div class="package-divider"></div>
        <ul class="package-features">
          <li>Full read-only scan of your AWS environment</li>
          <li>Markdown report with every path scored and prioritized</li>
          <li>1-hour walkthrough call</li>
          <li>48-hour turnaround</li>
        </ul>
```

- [ ] **Step 2: Replace Tier 2 title and bullet**

Use Edit tool:

```
old_string:        <div class="package-name">Tier 2 · Most common</div>
        <div class="package-title">Assessment + Roadmap</div>
        <div class="package-price">$5,000</div>
        <div class="package-price-note">2-week engagement</div>
        <div class="package-divider"></div>
        <ul class="package-features">
          <li>Everything in Assessment</li>
          <li>Detailed remediation plan with effort estimates per gap</li>
          <li>IaC recommendations with Terraform module references</li>
          <li>2-week engagement</li>
        </ul>
new_string:        <div class="package-name">Tier 2 · Most common</div>
        <div class="package-title">Scan + remediation roadmap</div>
        <div class="package-price">$5,000</div>
        <div class="package-price-note">2-week engagement</div>
        <div class="package-divider"></div>
        <ul class="package-features">
          <li>Everything in the attack-path scan</li>
          <li>Detailed remediation plan with effort estimates per path</li>
          <li>IaC recommendations with Terraform module references</li>
          <li>2-week engagement</li>
        </ul>
```

- [ ] **Step 3: Replace Tier 3 title**

Use Edit tool:

```
old_string:        <div class="package-name">Tier 3</div>
        <div class="package-title">Full Engagement</div>
new_string:        <div class="package-name">Tier 3</div>
        <div class="package-title">Full remediation engagement</div>
```

- [ ] **Step 4: Verify**

```bash
grep -n "Attack-path scan\|Scan + remediation roadmap\|Full remediation engagement\|every path scored\|effort estimates per path" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n ">Assessment<\|>Assessment + Roadmap<\|>Full Engagement<\|every gap scored\|estimates per gap\|Everything in Assessment" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: first grep returns 5 matches; second returns ZERO.

- [ ] **Step 5: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: pricing tier names + bullet polish"
```

---

## Task 9: Why-me section — intro paragraph + cards 2/3/4

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 1019-1037)

- [ ] **Step 1: Rewrite the intro paragraph**

Use Edit tool:

```
old_string:      <p class="section-desc" style="margin-top:16px;">I built the tool I use. The whole pipeline - four tiers of Claude agents plus a deterministic rules engine - is on my GitHub, under test, read-only by construction. If you want to verify anything before trusting me with your environment, you can read the source.</p>
new_string:      <p class="section-desc" style="margin-top:16px;">I built the tool I use. Four tiers of Claude agents plus a deterministic rules engine, read-only by construction. If you want to verify the methodology before trusting me with your environment, the sample report shows every step.</p>
```

- [ ] **Step 2: Card 1 — verify unchanged**

```bash
grep -n "4 years in IT, security analyst today" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: one match. No edit needed.

- [ ] **Step 3: Rewrite Card 2 body (drop "Every line on my GitHub")**

Use Edit tool:

```
old_string:      <div class="why-card">
        <h4>Built the whole tool solo</h4>
        <p>Four-tier agent pipeline plus a deterministic rules engine. Go API, React frontend. Every line on my GitHub.</p>
      </div>
new_string:      <div class="why-card">
        <h4>Built the whole tool solo</h4>
        <p>Go-based read-only collectors, deterministic scoring engine, agent-driven analysis. Built by one engineer who reads code, not status reports.</p>
      </div>
```

- [ ] **Step 4: Rewrite Card 3 body (emphasize IAM Terraform offer)**

Use Edit tool:

```
old_string:      <div class="why-card">
        <h4>Read-only by construction</h4>
        <p>Zero mutating API calls exist in any collector. The tool can only observe your environment. I can send you the IAM Terraform before we start.</p>
      </div>
new_string:      <div class="why-card">
        <h4>Read-only by construction</h4>
        <p>Zero mutating API calls exist in any collector. The tool can only observe your environment. I'll send you the IAM Terraform for the read-only role before the engagement starts so you can audit exactly what I can do.</p>
      </div>
```

- [ ] **Step 5: Rewrite Card 4 body (anchor to sample report)**

Use Edit tool:

```
old_string:      <div class="why-card">
        <h4>14 automated tests on the rules engine</h4>
        <p>The scoring logic is covered. You can see exactly what was checked and why. Show your work, not a black box.</p>
      </div>
new_string:      <div class="why-card">
        <h4>14 automated tests on the rules engine</h4>
        <p>The methodology is in the sample report. Every finding shows the underlying API call, the resource, and why it's a path. Show your work, not a black box.</p>
      </div>
```

- [ ] **Step 6: Verify all GitHub references in why-me are gone**

```bash
grep -n "is on my GitHub\|Every line on my GitHub\|you can read the source" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: zero matches.

- [ ] **Step 7: Verify new copy landed**

```bash
grep -n "the sample report shows every step\|reads code, not status reports\|audit exactly what I can do\|methodology is in the sample report" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: 4 matches.

- [ ] **Step 8: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: why-me section — drop GitHub references, lean on sample report + IAM role"
```

---

## Task 10: About Devon section — paragraph 1 edit

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (line 1051)

- [ ] **Step 1: Edit paragraph 1**

Use Edit tool:

```
old_string:      <p>I'm a security engineer based in the Bay Area, focused on AWS-native startups working toward SOC 2. I've spent the last four years in IT and security, and I'm currently a security analyst. On the side I build the tools I'd want to use in that role - like kumo-assess, which is the assessment engine behind this consulting practice.</p>
new_string:      <p>I'm a security engineer based in the Bay Area, focused on AWS-native startups working toward audit-ready security. I've spent the last four years in IT and security, and I'm currently a security analyst. On the side I build the tools I'd want to use in that role - like kumo-assess, the analysis engine I use on every engagement.</p>
```

- [ ] **Step 2: Verify**

```bash
grep -n "audit-ready security\|the analysis engine I use on every engagement" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n "working toward SOC 2\|assessment engine behind this consulting practice" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: first grep returns 2 matches; second returns ZERO.

- [ ] **Step 3: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: about section — drop SOC-2 framing, drop OSS connotation"
```

---

## Task 11: FAQ — full rewrite of #1, replacement of #3, reframe of #5, polish #2 and #4

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (lines 1073-1095)

- [ ] **Step 1: Replace FAQ #1 answer (Vanta/Drata posture)**

Use Edit tool:

```
old_string:    <div class="faq-item">
      <h3>Is this a replacement for Vanta or Drata?</h3>
      <p>No. Vanta and Drata are full compliance platforms that handle policies, training, employee onboarding, and evidence collection across multiple systems. I handle the AWS-technical portion of SOC 2, which is where most startups actually have gaps. Think of me as the specialist you hire alongside or instead of a compliance platform, depending on your stage.</p>
    </div>
new_string:    <div class="faq-item">
      <h3>Is this a replacement for Vanta or Drata?</h3>
      <p>No, and that's the point. Vanta and Drata are how you prove SOC 2 to auditors - they weren't built to find graph-based AWS attack paths. I work alongside them: I find the IAM and infrastructure paths an attacker could chain; you keep using Vanta/Drata for evidence collection and policy management.</p>
    </div>
```

- [ ] **Step 2: Polish FAQ #2 (sharpen first sentence)**

Use Edit tool:

```
old_string:    <div class="faq-item">
      <h3>How is this different from hiring a traditional compliance consultant?</h3>
      <p>Speed. A traditional readiness assessment takes 2 to 6 weeks. My scan takes 30 minutes. The agent-driven tool handles the data collection and analysis that consultants do manually, which means I can spend my time on the remediation work that actually matters. Same caliber output, delivered faster and at lower cost.</p>
    </div>
new_string:    <div class="faq-item">
      <h3>How is this different from hiring a traditional compliance consultant?</h3>
      <p>Speed and focus. A traditional readiness assessment takes 2 to 6 weeks and produces slide decks. My scan takes 30 minutes and produces Terraform. The agent-driven tool handles the data collection and analysis that consultants do manually, which means I can spend my time on the remediation work that actually matters.</p>
    </div>
```

- [ ] **Step 3: Replace FAQ #3 (delete "Is the tool open source?", insert trust question)**

Use Edit tool:

```
old_string:    <div class="faq-item">
      <h3>Is the tool open source?</h3>
      <p>Yes. The full kumo-assess codebase is on <a href="https://github.com/kumo-security/kumo-assess" target="_blank" rel="noopener">GitHub</a>. You can run it yourself if you prefer. Most customers hire me because they want the remediation work done, not because they can't run the tool.</p>
    </div>
new_string:    <div class="faq-item">
      <h3>How do I know I can trust you with read-only AWS access?</h3>
      <p>Two ways. First, the sample report shows every step of the methodology end-to-end - I ran it on my own AWS account and wrote up every finding. Second, you create a read-only IAM role and I send you the Terraform for it before the engagement starts. The tool can only observe your environment; zero mutating API calls exist in any collector.</p>
    </div>
```

- [ ] **Step 4: Polish FAQ #4 (tighten phrasing)**

Use Edit tool:

```
old_string:    <div class="faq-item">
      <h3>Do you have access to my AWS account?</h3>
      <p>You create a read-only IAM role. The tool cannot modify anything in your environment - zero mutating API calls exist in the collectors. I can send you the relevant Terraform for the IAM role before the scan so you can review it.</p>
    </div>
new_string:    <div class="faq-item">
      <h3>Do you have access to my AWS account?</h3>
      <p>You create a read-only IAM role. The tool cannot modify anything in your environment - zero mutating API calls exist in any collector. I send you the Terraform for the role before the engagement starts so you can audit exactly what I can see.</p>
    </div>
```

- [ ] **Step 5: Reframe FAQ #5 (framework-agnostic)**

Use Edit tool:

```
old_string:    <div class="faq-item">
      <h3>What happens if I need a framework other than SOC 2?</h3>
      <p>CMMC, ISO 27001, PCI DSS, and HIPAA are on the roadmap. If you have an immediate need, <a href="mailto:devon@kumosecurity.com">email me directly</a>. Many controls map across frameworks, so I may be able to help already.</p>
    </div>
new_string:    <div class="faq-item">
      <h3>What happens if I need a framework other than SOC 2?</h3>
      <p>AWS attack paths are framework-agnostic - they're real risk regardless of what you're certifying. Findings map to SOC 2 (CC6, CC7), PCI, ISO 27001, and CMMC controls. If you have a specific framework need, <a href="mailto:devon@kumosecurity.com">email me directly</a>.</p>
    </div>
```

- [ ] **Step 6: FAQ #6, #7, #8 — verify unchanged**

```bash
grep -n "What environments do you support\|Can I see a sample report\|How do I get started" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: 3 matches. No edits needed.

- [ ] **Step 7: Verify FAQ rewrites**

```bash
grep -n "No, and that's the point\|Speed and focus\|How do I know I can trust you with read-only AWS access\|attack paths are framework-agnostic" C:/Users/Devon/Documents/kumosecurity-website/index.html
grep -n "Is the tool open source\|kumo-assess codebase is on\|Think of me as the specialist you hire alongside or instead" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: first grep returns 4 matches; second returns ZERO.

- [ ] **Step 8: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: FAQ — feeder posture, OSS replaced with trust-access answer, framework-agnostic"
```

---

## Task 12: Final CTA h2

**Files:**
- Modify: `C:/Users/Devon/Documents/kumosecurity-website/index.html` (line 1113)

- [ ] **Step 1: Edit final CTA headline**

Use Edit tool:

```
old_string:  <h2>Ready to see your AWS SOC 2 gaps?</h2>
new_string:  <h2>Ready to see your AWS attack paths?</h2>
```

- [ ] **Step 2: Verify**

```bash
grep -n "Ready to see your AWS attack paths\|Ready to see your AWS SOC 2 gaps" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: one match for the new line, zero for the old.

- [ ] **Step 3: Commit**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: final CTA — attack-path framing"
```

---

## Task 13: Full QA pass — final verification

**Files:**
- Read: `C:/Users/Devon/Documents/kumosecurity-website/index.html`

This task verifies the success criteria from the spec.

- [ ] **Step 1: Confirm all `kumo-security/kumo-assess` repo references are gone**

```bash
grep -n "kumo-security/kumo-assess" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: ZERO matches.

- [ ] **Step 2: Confirm primary SOC 2 framings are removed (allowing CC IDs to remain as secondary tags)**

```bash
grep -n "SOC 2 readiness\|SOC 2 gaps\|SOC 2 consulting\|SOC 2 CC6+CC7" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: ZERO matches. CC IDs (e.g., `CC6.3`) and references like `prove SOC 2 to auditors` are intentionally kept — they're now secondary signals, not the primary frame.

- [ ] **Step 3: Confirm "feeder, not replacement" posture is internally consistent**

```bash
grep -n "instead of a compliance platform\|they're mostly dashboards\|priced for Series A and up" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: ZERO matches. Anti-Vanta language is gone.

- [ ] **Step 4: Confirm attack-path framing is present in all expected sections**

```bash
grep -n "attack path\|attack-path\|attack paths" C:/Users/Devon/Documents/kumosecurity-website/index.html
```

Expected: at least 8 matches across hero, dashboard, case study, what's covered, FAQ, and final CTA.

- [ ] **Step 5: Take final desktop screenshot**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node screenshot.mjs http://localhost:3000 final-rebrand-desktop
```

- [ ] **Step 6: Take final mobile screenshot**

If `screenshot.mjs` supports a viewport flag, use it. Otherwise resize the headless viewport in `screenshot.mjs` temporarily to 375x812 (iPhone) before this step, then restore. Read the README in the website repo for the supported invocation.

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && node screenshot.mjs http://localhost:3000 final-rebrand-mobile
```

- [ ] **Step 7: Visual review against the spec**

Open `temporary screenshots/screenshot-N-final-rebrand-desktop.png` and `temporary screenshots/screenshot-N-baseline-pre-rebrand.png` side by side. Confirm:
- Hero badge reads "Compliant but still vulnerable"
- Hero h1 reads "Find the AWS attack paths your compliance tool misses." (line break per spec)
- Lead reads "Before they hit production. Built for engineers, priced for startups, works alongside Vanta and Drata."
- Punch line "Powered by agents I built..." still present
- No GitHub trust link below the CTA buttons
- Dashboard mockup shows PATH-01/02/03 with arrow chains and CC tags
- Problem section title is "There's a gap between compliance and security."
- Three problem cards show "Compliance tools / Enterprise CNAPP / What's missing"
- Approach Step 01 reads "Agent-driven attack-path scan"
- What's covered section title is "What kumo-assess looks for."
- Pricing tier titles read "Attack-path scan / Scan + remediation roadmap / Full remediation engagement"
- Why-me Card 2 no longer mentions GitHub
- FAQ #3 is the trust question, not the OSS question
- Final CTA h2 reads "Ready to see your AWS attack paths?"

If any item is off, return to the relevant task and fix.

- [ ] **Step 8: Stop the dev server**

Find and stop the `node serve.mjs` background process.

- [ ] **Step 9: Confirm clean working tree (all changes committed)**

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git status && git log --oneline -15
```

Expected: working tree clean. `git log` shows ~12 rebrand commits since the spec commit (one per task above), each prefixed `rebrand:`.

- [ ] **Step 10: Final commit if any QA fix-ups happened**

If Step 7 surfaced visual issues that needed fix-up, commit with:

```bash
cd C:/Users/Devon/Documents/kumosecurity-website && git add index.html && git commit -m "rebrand: QA fixups from screenshot pass"
```

If no fixups needed, skip this step.

---

## Out-of-band follow-ups (not part of this plan, but track them)

These are surfaced in the spec and remain Devon's call to schedule:

1. **Flip `github.com/kumo-security/kumo-assess` repo to private.** Once the page no longer references it, the repo can flip without breaking the site. The Vesta cold email link will 404 — accepted per Q4.
2. **Rewrite the Vesta cold-email + preliminary-note templates** in the kumo-assess repo to drop the GitHub repo reference before email #2 is sent.
3. **Update CEO plan + memory** (`positioning.md`, `business_plan.md`) to record the E1 (open-core) reversal.
4. **Push `kumosecurity-website` main** when Devon is ready (`git push origin main`). Do not push from this plan — Devon explicitly approves pushes.
5. **Sweep sibling pages** (`about/`, `services/`, `projects/`, `certifications/`) for residual SOC-2-only framing as a follow-up rebrand pass.

---

## Self-review notes

- **Spec coverage:** all 13 spec sections (hero, dashboard, case study, problem, approach, what's covered, pricing, why-me, about, FAQ #1/2/3/4/5, final CTA, footer-as-no-op) map to a task above. The footer is intentionally not a task — it requires no edit.
- **Type/identifier consistency:** CSS class names referenced in the plan (`hero-badge`, `hero-github`, `package-card`, `package-features`, `problem-card`, `problem-stat`, `covered-row`, `covered-id`, `covered-desc`, `covered-scope`, `why-card`, `faq-item`, `stat-card`, `stat-fail`, `stat-partial`, `stat-score`, `control-row`, `badge-fail`, `badge-partial`, `dashboard-title`) all exist in the source HTML — verified during read-through.
- **Placeholder scan:** no TBDs, TODOs, "implement later," or vague handwaves. Each Edit step contains the exact `old_string` / `new_string` to apply. Each verification step contains the exact grep command and expected count.
