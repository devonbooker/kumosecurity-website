# Kumo Security Website Redesign

**Date:** 2026-04-17
**Status:** Approved - ready for implementation planning
**Goal:** Rebuild kumosecurity.com as a lead-gen landing page for Kumo Assess — the agentic SOC 2 compliance product.

---

## Context

The current site is positioned as CMMC consulting for defense contractors. This redesign is a pivot: CMMC consulting is dropped, and the site becomes a marketing + lead-gen surface for Kumo Assess (agentic SOC 2 compliance assessment).

**Kumo Security** is the umbrella brand. **Kumo Assess** is the first product (repo: `kumo-assess`). Future products will live under the same brand.

The primary conversion action is a discovery call booking. Kumo Assess is not yet self-serve — visitors book a call and run their first assessment guided by Devon. The site positions it as product access/onboarding, not consulting engagement. This framing is honest and sets up a clean pivot to self-serve when the product is ready.

---

## Goals

- Replace CMMC consulting positioning with Kumo Assess product positioning
- Generate qualified leads (SOC 2-bound SaaS startups) who book discovery calls
- Establish Kumo Security as a product company brand, not a personal portfolio
- Match the visual system established in `brand_assets/kumo-security-brand-guidelines.md` and `brand_assets/kumo-assess-ui-guidelines.md`

---

## Constraints

- Static HTML (single `index.html` per directory), served via `node serve.mjs`
- Tailwind CSS via CDN, all styles inline or in `<style>` tag
- No backend — all "Book a Call" buttons link to `https://calendly.com/devon-kumosecurity/30min`
- Mobile-first responsive
- Must use assets from `brand_assets/` (logos, brand palette)

---

## Visual Direction

**Mode:** Clean Light (not dark navy)
**Background:** `#F8FAFC`
**Surface:** `#FFFFFF`
**Primary text:** `#0F172A`
**Accent / CTA:** `#3B82F6` → hover `#2563EB`
**Brand Navy:** `#0B1A3E` — used only for the final CTA block, not as the page base. Footer is white.
**Typography:** Inter (headings + UI) + JetBrains Mono (IDs, code, technical labels)
**Icons:** Lucide, 1.5px stroke, 16px
**Border radius:** Cards 8px, buttons/inputs 6px, badges 4px
**Shadows:** None on structural elements. Floating shadow only on the hero dashboard card: `0 4px 24px rgba(0,0,0,0.07)`

Full palette and component specs: `brand_assets/kumo-security-brand-guidelines.md` + `brand_assets/kumo-assess-ui-guidelines.md`

---

## Site Architecture

```
/               - Homepage (long-scroll, all sections)
/about/         - About page (thin credibility page)
```

Nav links: **Products** (anchor to features section) · **About** (/about/)
Nav CTA: **Book a Call** (primary button, right-aligned)

The archive, certifications, projects, and services directories are retired. They can be left in place but are not linked from the new nav.

---

## Homepage — Section by Section

### 1. Navigation

- Sticky, height 52px, `background: #FFFFFF`, `border-bottom: 1px solid #E2E8F0`
- Left: Kumo Security wordmark (`Kumo Security Logo - White Text.png` is wrong here — use `Kumo Security Logo - Black Text.png` on light bg)
- Center/left: nav links — Products (smooth-scrolls to features), About (/about/)
- Right: Book a Call (primary button, links to booking)
- Mobile: hamburger collapses to full-width mobile menu

### 2. Hero

**Layout:** Centered, max-width 760px, padding 80px top

**Badge:** Small monospace label above headline — `AGENTIC SOC 2 COMPLIANCE` in blue (`#3B82F6`), uppercase, tracked

**Headline:** `Know your SOC 2 posture` / `in hours, not months.` — "in hours, not months." in `#94A3B8` muted color. Font: Inter 700, `clamp(36px, 5vw, 60px)`, tracking `-0.03em`

**Subheadline:** "Kumo Assess connects to your AWS account and runs a full CC6+CC7 compliance scan — automated evidence collection, gap scoring, and remediation guidance." — Inter 400, 17px, `#475569`, max-width 480px

**CTAs:**
- Primary: `Book a Call →` — `#3B82F6`, links to booking
- Secondary: `See how it works ↓` — outlined, smooth-scrolls to How It Works section

**Dashboard card:** White card with subtle shadow, max-width 720px, centered below CTAs. Shows:
- Score + stat row: four mini cards (Score/Pass/Fail/Partial) using status color palette from `kumo-assess-ui-guidelines.md`
- 3 control rows below: FAIL/PASS/PARTIAL with left accent border, control ID (JetBrains Mono), and description
- Styled exactly per `kumo-assess-ui-guidelines.md` — this is a live preview of the actual product UI

### 3. Social Proof Strip

White background, `border-top` + `border-bottom: 1px solid #E2E8F0`, padding 28px vertical.

Four stats separated by vertical dividers:

| Stat | Label |
|------|-------|
| `$30–80k` | avg SOC 2 audit cost |
| `6–12 mo` | typical time to SOC 2 |
| `<24 hrs` | Kumo Assess turnaround |
| `47` | AWS services scanned |

The `<24 hrs` stat uses accent blue `#3B82F6` to make it stand out as the differentiator. All numbers in JetBrains Mono.

### 4. Features

**Label:** `WHAT YOU GET`
**Headline:** `Evidence collection. Gap scoring.` / `Remediation guidance.`

Six-card grid (3×2 desktop, 2×3 tablet, 1×6 mobile). Each card: white background, `1px solid #E2E8F0` border, 8px radius, 24px padding. Section element has `id="features"` — this is the anchor target for the "Products" nav link.

| Feature | Description |
|---------|-------------|
| Automated Evidence | Collects from 47 AWS services. No manual screenshots or CSV exports. |
| Control Scoring | Each SOC 2 control scored PASS / FAIL / PARTIAL with evidence citations. |
| Remediation Guidance | Every gap gets a specific fix — not "implement MFA," but exactly which IAM policy to change. |
| Read-Only by Design | Assessment only. No agents writing to your infrastructure. Ever. |
| Scan History | Run scans over time. Track your score improving as you remediate gaps. |
| Downloadable Report | Export a full markdown report. Share with your auditor or board. |

### 5. How It Works

**Label:** `HOW IT WORKS`
**Headline:** `Three steps to your compliance posture.`

Three-step horizontal row (desktop), stacked on mobile. Each step: numbered badge (JetBrains Mono, `#3B82F6`), title, description. Arrows between steps on desktop.

| Step | Title | Description |
|------|-------|-------------|
| 01 | Connect AWS | Add a read-only IAM role. Kumo Assess never modifies your environment. |
| 02 | Run a Scan | Select your control family (CC6, CC7). Agents collect evidence across 47 services. |
| 03 | Review & Fix | Get your score, control breakdown, and specific remediation steps. |

### 6. Credibility

**Label:** `WHY KUMO SECURITY`
**Headline:** `Built by an engineer.` / `Not a compliance checkbox factory.`

Two-column layout (desktop), stacked mobile. Left: headline + 2-sentence description of the approach (agentic, AWS-native, open architecture). Right: 2×2 grid of trust signal cards.

| Signal | Description |
|--------|-------------|
| Read-Only by Design | Scoped IAM policy. Observes only. Never touches. |
| Agentic, Not Scripted | Claude agents interpret evidence in context — not regex against config files. |
| AWS-Native | Every collector maps to a real AWS API call. No gray-area inference. |
| Open Architecture | The assessment logic is transparent. You can inspect what was checked and why. |

No Devon photo or name. Kumo Security is the entity.

### 7. Final CTA

**Background:** Brand Navy `#0B1A3E` (the only dark section on the page)
**Headline:** `Ready to see your compliance posture?`
**Subtext:** `Book a call. We'll run your first Kumo Assess scan together.`
**CTA:** `Book a Call →` — primary blue button

### 8. Footer

White background, `border-top: 1px solid #E2E8F0`

- Left: Kumo Security wordmark (black text logo)
- Center/right: Products · About · GitHub · LinkedIn · Email
- Bottom row: `© 2026 Kumo Security` + Contact link only (no Privacy page exists)

**No personal alias lockup.** The `devonbooker // cloud security` pattern from the old brand guidelines is retired in this redesign.

---

## /about Page

Thin, minimal. Purpose: credibility for visitors who want to vet before booking.

**Sections:**
1. **Header** — "About Kumo Security" + 1-paragraph summary of what Kumo Security is and what Kumo Assess does
2. **Background** — Devon's engineering background (AWS, Go, cloud security, AI). Bullet list format, no fluff. Links to GitHub and LinkedIn.
3. **What We're Building** — Short section on Kumo Assess and the roadmap (SOC 2 now, ISO 27001 / CMMC planned)
4. **Contact** — Email + Book a Call CTA

No photo required. No personal essay. Just the technical facts a buyer needs to decide if Devon is credible enough to talk to.

---

## Brand Updates Required

Two small updates to `brand_assets/kumo-security-brand-guidelines.md` should be made alongside this redesign:

1. **Section 0.1 Product Portfolio** — Add note that `kumo-assess` (repo name) uses `Kumo Assess` as the marketing/product name
2. **Section 7 Professional Alias & Lockup** — Retire or scope this section. The `devonbooker // cloud security` lockup was part of the personal portfolio positioning and is not used in the new site. May still apply to personal GitHub profile, LinkedIn, etc. — but not to kumosecurity.com.

---

## Out of Scope

- Authentication / user accounts
- Self-serve sign-up flow
- Pricing page
- Blog / content section
- Projects or certifications pages (retired from nav, files can stay on disk)
- Dark mode variant
- Any backend or form handling (CTA is mailto or Calendly link)
