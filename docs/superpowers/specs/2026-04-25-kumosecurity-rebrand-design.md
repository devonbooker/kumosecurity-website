# kumosecurity.com Rebrand — "The Wedge"

**Date:** 2026-04-25
**Status:** Spec — pending implementation plan
**Source positioning:** `~/.gstack/projects/kumo-security-kumo-assess/ceo-plans/2026-04-23-kumo-positioning.md`

## Why this work exists

CEO-locked positioning shifted on 2026-04-23 from "agentic SOC 2 assessment consulting" to "The Wedge" — AWS attack-path analysis for startup CTOs, priced between Vanta and Wiz, posture is **feeder into Vanta/Drata, never replacement**. The current site still markets the old positioning. Email #2 of the Path B outreach batch is blocked until the site stops contradicting the templates.

The Vesta cold email (sent 2026-04-22) already uses the new attack-path language and links to kumosecurity.com. A click today lands on a page selling "SOC 2 readiness consulting" with a hero that bashes Vanta/Drata in the problem section — that's a trust break the rewrite has to close.

This spec also reflects a session-time reversal of CEO-plan **E1 (open-core)**. The user dropped the open-source posture entirely. The repo `github.com/kumo-security/kumo-assess` will go private; the trust signal it currently carries on the site has to be replaced by other means.

## Decisions locked in this brainstorm

| # | Question | Decision |
|---|----------|----------|
| Q1 | Scope of rewrite | **Full rebrand pass** — hero through FAQ, all contradictions resolved |
| Q2 | (Made moot by Q3 → was about handling site/repo product gap) | — |
| Q3 | Trust signal replacement for OSS | **All three layered** — sample report (primary), read-only IAM role guarantee, named consultant |
| Q4 | Repo disposition | **Private + scrub all references** — Vesta link will 404, accept the breakage |
| Q5 | Pricing model | **Keep current consulting tiers, reframe wrapper** — $2.5k / $5k / $15k+ stay; labels and bullets shift to attack-path framing |
| Q6 | Hero hook placement | **Hook as badge, attack-path framing as h1** — "Compliant but still vulnerable" in the badge slot, elevator line in h1 |
| Q7 | Hero dashboard mockup | **Real engine output, attack-path wrapper** — same UI shape, finding rows relabeled as paths the engine actually produces today |
| Q8 | Vertical positioning | **Horizontal copy + fintech credibility moments** — defer hardcoded fintech-first until ICP verification calls happen |

## Out of scope (intentional)

- Sibling pages (`about/index.html`, `services/index.html`, `projects/index.html`, `certifications/index.html`) — flagged for follow-up if their copy contradicts after this pass; not in this rewrite
- Blog post `blog/i-ran-this-on-my-own-aws-account/` — content stays, gets promoted to primary trust signal but doesn't get rewritten
- CSS files (`styles/brand.css`, `styles/components.css`) — untouched; all changes are HTML/copy
- Vesta follow-up email policy decision — separate decision
- Email template rewrites (`marketing/preliminary-notes/vesta/*` in the kumo-assess repo) — separate task; flagged as a downstream dependency of this rewrite (templates currently reference the GitHub repo that's about to go private)
- CEO plan + memory updates to reflect the E1 reversal — separate task; should happen after this session

## Architecture

- Single edit pass on `C:/Users/Devon/Documents/kumosecurity-website/index.html`
- CSS untouched
- Same nav, footer, page anatomy, dashboard mockup structure
- All `kumo-security/kumo-assess` repo references stripped (hero GitHub link, Why-me copy, FAQ #3, footer if present)
- Personal GitHub `@devonbooker` references stay (identity, not the repo)
- `<title>` and `<meta name="description">` updated to attack-path framing

## Section-by-section spec

### Hero

**Badge** (mono small caps): `COMPLIANT BUT STILL VULNERABLE`

**H1**: `Find the AWS attack paths your compliance tool misses.`

**Lead**: `Before they hit production. Built for engineers, priced for startups, works alongside Vanta and Drata.`

**Punch line** (unchanged): `Powered by agents I built. Shipped by someone who actually reads your Terraform.`

**CTAs**:
- Primary: `Book a scoping call →` (Calendly link unchanged)
- Secondary: `See a sample report` (anchor to the blog post — same as today)

**GitHub trust link**: REMOVED entirely.

**`<title>`**: `Kumo Security - AWS attack-path analysis for startups`

**`<meta name="description">`**: `Find the AWS attack paths your compliance tool misses. Read-only assessment, prioritized findings, Terraform remediation. Works alongside Vanta and Drata. Starting at $2,500.`

### Hero dashboard mockup

Replace SOC 2 control rows with attack-path-framed findings.

Header line: `kumo-assess · AWS attack-path scan · aws/us-east-1`

Stat row (4 cards):
- `35` Score
- `3` Critical paths
- `1` Path to root
- `7` Total findings

Finding rows (replace the current 3 control rows):

| Severity | ID | Body |
|---|---|---|
| CRITICAL | PATH-01 | `developer-role → iam:PassRole → admin-role` (3 hops to root) |
| HIGH | PATH-02 | `ec2-instance-profile → s3:* on cust-data-prod` |
| HIGH | PATH-03 | `ci-deploy-role → AssumeRole * → unrestricted` |

Each row gets a small mono CC tag underneath in muted color (`var(--text-muted)`) to keep the SOC 2 thread visible without making it the headline:
- PATH-01 → `CC6.3`
- PATH-02 → `CC6.7`
- PATH-03 → `CC6.3, CC7.2`

CSS classes (`stat-card`, `control-row`, badge variants) stay; only labels and content change. Badge variants: `badge-fail` → reused for CRITICAL severity, `badge-partial` → reused for HIGH. New CSS not required.

### Case study hook

Section structure unchanged. One copy edit:

`If you want to see what an honest SOC 2 readiness assessment actually looks like, read the writeup.`
→ `If you want to see what an honest AWS attack-path scan actually looks like, read the writeup.`

This section becomes more load-bearing post-rewrite (Trust Signal A from Q3). No structural changes; the existing `case-study` styling carries it.

### Problem section

**Section title**: `SOC 2 readiness is overpriced and under-delivered.` → `There's a gap between compliance and security.`

**Three cards rewritten** (CSS structure unchanged — same `problem-card` and `problem-stat` classes):

| Card | Stat | H3 | Body |
|------|------|-----|------|
| 1 | `$5k-$30k/yr` | Compliance tools | Vanta and Drata get you to SOC 2. Necessary - and they don't see your AWS attack surface. That's by design; they're audit infrastructure. |
| 2 | `$50k-$200k+/yr` | Enterprise CNAPP | Wiz and Orca find the paths. Priced for security teams with the headcount and budget you don't have yet. |
| 3 | `The wedge` | What's missing | A scan a startup CTO can act on - alongside the compliance tool you already pay for. That's where I sit. |

Note on Card 3: the stat field becomes a label rather than a dollar value. If the visual breaks, fall back to `$2k-$10k` as the stat with body adjusted.

This rewrite directly addresses CEO Risk #4 ("feeder, not replacement"). The compliance card no longer says "they're mostly dashboards."

### Approach section

Section title `Scan. Review. Remediate.` and the 3-step structure unchanged.

**Step 01 — SCAN**
- H3: `Agent-driven assessment` → `Agent-driven attack-path scan`
- Body: `I run a read-only scan that maps your IAM graph and surfaces the paths an attacker could actually chain. Thirty minutes. You approve the IAM role before anything starts.`

**Step 02 — REVIEW**
- H3: `Walk every gap on a call` → `Walk every path on a call`
- Body: `We go through every path together, prioritized by blast radius. You get the full markdown report with evidence citations and severity scored against your audit timeline.`

**Step 03 — REMEDIATE**
- H3: `Terraform, not slide decks` — unchanged (this line is doing real work)
- Body unchanged

### What's covered section

**Section title**: `The AWS-technical part of SOC 2, where most startups fail.` → `What kumo-assess looks for.`

Row structure unchanged. Re-label `covered-desc` column with attack-path language; `covered-id` column keeps CC IDs as secondary signal.

| ID (mono) | Desc | Scope (mono) |
|-----------|------|--------------|
| CC6 | Privilege escalation | `IAM · MFA · least privilege · PassRole abuse` |
| CC6.6 | Audit trail integrity | `CloudTrail coverage · tamper resistance` |
| CC6.7 | Data exposure paths | `S3 · KMS` |
| CC6.8 | Change detection coverage | `Config · Security Hub` |
| CC7 | Detection & response | `monitoring · incident response` |
| CC1, CC2, CC8, A1, C1 | additional families | `expanding quarterly` |

**Footnote**: `Built on direct AWS API calls, not heuristics. Five collectors today: IAM, CloudTrail, S3, Security Hub, Config. The assessment logic is transparent and open source.`
→ `Built on direct AWS API calls, not heuristics. Five collectors today: IAM, CloudTrail, S3, Security Hub, Config. Read-only by construction. Methodology documented in the sample report.`

### Pricing section

Section title `Three tiers. Fixed scope, fixed price.`, label `Packaging`, layout, and featured-tier styling unchanged.

| Tier | Price | New name | New punch (price-note) |
|------|-------|----------|------------------------|
| 1 | $2,500 | Attack-path scan | Delivered in 48 hours |
| 2 (featured) | $5,000 | Scan + remediation roadmap | 2-week engagement |
| 3 | From $15,000 | Full remediation engagement | 4 to 6 weeks |

Bullet copy gets a light pass: replace any "SOC 2 gap" / "gap" terminology with "attack path" / "finding" where it appears. Specific examples:
- Tier 1 bullet "Markdown report with every gap scored and prioritized" → "Markdown report with every path scored and prioritized"
- Tier 2 bullet "Detailed remediation plan with effort estimates per gap" → "Detailed remediation plan with effort estimates per path"

The $2k-$10k/yr CEO-plan price point is **not** reflected on the page. That price is the long-term subscription target; the consulting tiers reflect what's deliverable today.

### Why-me section

**Section title**: `Built by an engineer. Not a compliance checkbox factory.` — unchanged.

**Intro paragraph rewrite** (drops "is on my GitHub" and "you can read the source"):
> I built the tool I use. Four tiers of Claude agents plus a deterministic rules engine, read-only by construction. If you want to verify the methodology before trusting me with your environment, the sample report shows every step.

**Card 1** (`4 years in IT, security analyst today`) — unchanged.

**Card 2** (`Built the whole tool solo`) — body rewrite:
> Go-based read-only collectors, deterministic scoring engine, agent-driven analysis. Built by one engineer who reads code, not status reports.

**Card 3** (`Read-only by construction`) — body rewrite (slight emphasis on the IAM Terraform offer, which becomes Trust Signal B):
> Zero mutating API calls exist in any collector. The tool can only observe your environment. I'll send you the IAM Terraform for the read-only role before the engagement starts so you can audit exactly what I can do.

**Card 4** (`14 automated tests on the rules engine`) — body rewrite (anchors to sample report instead of public source):
> The methodology is in the sample report. Every finding shows the underlying API call, the resource, and why it's a path. Show your work, not a black box.

### About Devon section

**H2** unchanged: `I'm Devon Booker.`

**Paragraph 1 edit**: `working toward SOC 2` → `working toward audit-ready security`. Replace `kumo-assess, which is the assessment engine behind this consulting practice` → `kumo-assess, the analysis engine I use on every engagement`.

**Paragraph 2** unchanged.

**Links row** unchanged — personal GitHub (`@devonbooker`), LinkedIn, Email all stay.

### FAQ rewrites

**#1 — Replacement for Vanta or Drata?** — full rewrite (fixes Risk #4 violation):
> No, and that's the point. Vanta and Drata are how you prove SOC 2 to auditors - they weren't built to find graph-based AWS attack paths. I work alongside them: I find the IAM and infrastructure paths an attacker could chain; you keep using Vanta/Drata for evidence collection and policy management.

**#2 — Different from a traditional compliance consultant?** — light tweak. Keep the speed/automation angle. Sharpen first sentence to: `Speed and focus. A traditional readiness assessment takes 2 to 6 weeks and produces slide decks. My scan takes 30 minutes and produces Terraform.`

**#3 — Is the tool open source?** — **DELETE entirely.** Replace with a new question that operationalizes Trust Signals A + B from Q3:
> **How do I know I can trust you with read-only AWS access?**
>
> Two ways. First, the sample report shows every step of the methodology end-to-end - I ran it on my own AWS account and wrote up every finding. Second, you create a read-only IAM role and I send you the Terraform for it before the engagement starts. The tool can only observe your environment; zero mutating API calls exist in any collector.

**#4 — Do you have access to my AWS account?** — keep, with one tightening edit:
> You create a read-only IAM role. The tool cannot modify anything in your environment - zero mutating API calls exist in any collector. I send you the Terraform for the role before the engagement starts so you can audit exactly what I can see.

**#5 — What happens if I need a framework other than SOC 2?** — reframe:
> AWS attack paths are framework-agnostic - they're real risk regardless of what you're certifying. Findings map to SOC 2 (CC6, CC7), PCI, ISO 27001, and CMMC controls. If you have a specific framework need, [email me directly](mailto:devon@kumosecurity.com).

**#6 — What environments do you support?** — unchanged.

**#7 — Can I see a sample report?** — unchanged. The link gets implicitly more important post-rewrite (Trust Signal A).

**#8 — How do I get started?** — unchanged.

### Final CTA

H2: `Ready to see your AWS SOC 2 gaps?` → `Ready to see your AWS attack paths?`

Subtext and CTA button unchanged.

### Footer

Unchanged. Personal GitHub link stays. The `kumo-security/kumo-assess` repo is not currently linked from the footer (verified — only hero, FAQ, and Why-me reference it), so no edit needed.

## Cross-page references that need cleanup separately

The following references to the now-private repo live outside `index.html`. They are **out of scope** for this rewrite but tracked here as known follow-ups:

- `marketing/preliminary-notes/vesta/preliminary-note.md` (in kumo-assess repo) — references the GitHub repo
- `marketing/preliminary-notes/vesta/cold-email.md` (in kumo-assess repo) — references the GitHub repo, used as the template for emails #2-10
- The Vesta email already in flight (sent 2026-04-22) — link will 404 once the repo flips private; accept the breakage per Q4

## Risk register

| Risk | Mitigation |
|------|------------|
| Site claims attack-path scanning, kumo-assess doesn't fully implement graph-based attack paths until Phase 1 (weeks 1-2) | Dashboard mockup uses findings the engine actually produces today (over-permissive IAM, role chains). Sample report is real output. Honest about current capability without overselling. |
| Repo flip to private breaks Vesta email link | Accepted (Q4 = A). Vesta follow-up policy is a separate decision. |
| GRC reader hits the page and reacts to "Compliant but still vulnerable" | Hook is in the badge slot (small mono), not the h1. h1 is constructive ("Find the AWS attack paths…"). Lead reassures with "works alongside Vanta and Drata." |
| Fintech-first ICP doesn't survive verification calls | Site copy is horizontal (Q8 = B). No expensive rewrite if ICP shifts. |
| Pricing on the page ($2.5k-$15k+ one-time) doesn't match CEO-plan target ($2k-$10k/yr subscription) | Acknowledged. Subscription pricing requires shipped continuous monitoring (Phase 3, weeks 5-8 minimum). Page reflects what's deliverable today. |

## Success criteria

- All occurrences of "SOC 2 readiness" / "SOC 2 gaps" / "SOC 2 consulting" as the primary frame are removed from `index.html`
- All references to `github.com/kumo-security/kumo-assess` are removed from `index.html`
- The "feeder not replacement" posture is internally consistent: no copy on the page describes Kumo as an alternative to Vanta/Drata
- Hero badge, h1, lead, dashboard mockup, and section titles all consistently use attack-path framing
- Existing CSS classes carry all changes — no new CSS required
- Page renders correctly on mobile (existing responsive breakpoints handle the new copy lengths)
- All Calendly, mailto, LinkedIn, and personal GitHub links continue to work

## Implementation handoff

Next step: writing-plans skill produces the implementation plan. The plan should sequence:
1. SEO/title/meta updates
2. Hero copy + CTA cleanup (remove GitHub link)
3. Hero dashboard mockup re-content
4. Case study hook copy edit
5. Problem section rewrite (3 cards)
6. Approach section copy edits
7. What's covered section relabel
8. Pricing tier renames + bullet polish
9. Why-me intro + cards 2/3/4 rewrites
10. About paragraph 1 edits
11. FAQ #1 full rewrite, #3 replacement, #5 reframe, others left alone or lightly polished
12. Final CTA h2 edit
13. Local screenshot QA pass against the spec (per `kumosecurity-website/CLAUDE.md` workflow)

Implementation should follow the screenshot-and-compare loop in the website repo's `CLAUDE.md` (start `node serve.mjs`, screenshot on localhost, compare).
