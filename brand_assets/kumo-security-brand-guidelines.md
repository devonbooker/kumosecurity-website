# Brand Guidelines: Kumo Security

---

## 0. Brand Context

**Brand Name:** Kumo Security

**What It Is:** A security brand spanning products, services, and technical work in cloud security, compliance automation, and AI-augmented security operations. The umbrella brand hosts a growing portfolio of products and offerings; the website and public surface are organized around Kumo Security, with individual products nested underneath.

**Positioning:** Lean, builder-first, startup-native. Kumo Security signals depth over breadth - built by engineers who ship in the space, not advisors watching from the sidelines. The brand should read like the output of a serious product company, not a hobbyist portfolio.

**Primary Audience:**
- Security and compliance leaders at SaaS startups evaluating tools and partners
- Startup hiring managers and engineering leads
- Peers in cloud security, platform engineering, and infrastructure

**Secondary Audience (future):**
- Engineers looking for community and learning resources
- Small teams evaluating security consulting partnerships

---

## 0.1 Product Portfolio

Kumo Security is the umbrella brand. Individual products and services live beneath it and inherit the brand's voice, palette, and visual language.

| Product / Service | Status | What It Is |
| :---------------- | :----- | :--------- |
| **kumo-assess** | Active | Agentic SOC 2 compliance assessment - read-only cloud environment scanning, control gap analysis, and scoring |
| *Additional products* | Planned | Reserved for future additions |

Naming rule: products use lowercase-hyphenated identifiers (`kumo-assess`) in code, technical copy, and UI. Marketing copy may use title case (`Kumo Assess`) where it reads more naturally in running prose, but the lowercase form is canonical.

Product UIs follow product-specific UI guidelines that extend this brand system. See Section 11.

---

## 1. Brand Identity & Logo

Kumo Security has two logo marks that work together:

1. **Wordmark** - "Kumo Security" lockup. The primary brand mark for marketing surfaces, the website, decks, and external communication. Canonical files live in `brand_assets/`:
   - `Kumo Security Logo - Black Text.png` - for light backgrounds
   - `Kumo Security Logo - White Text.png` - for dark or colored backgrounds
   - `Kumo Security Logo - Blue Background.png` - lockup on brand accent background
2. **Terminal Prompt** (`>_`) - secondary mark. Used for favicons, in-product nav marks (e.g., `>_ kumo-assess`), and technical contexts where the wordmark is too long. Represents the builder identity and hands-on engineering.

### Logo Variations

- **Primary (Light Mode):** Security Navy (`#0B1A3E`) or black wordmark on a white (`#FFFFFF`) or light gray (`#F8FAFC`) background. Default for the web, products, and documents.
- **Secondary (Dark Mode/Print):** Pure White (`#FFFFFF`) wordmark on a Security Navy (`#0B1A3E`) or brand-accent background. Used for dark-context placements, print on dark stock, or high-contrast materials.
- **Product nav:** `>_` mark + product name in JetBrains Mono (e.g., `>_ kumo-assess`). See product UI guidelines.

---

## 2. Logo Clear Space

To maintain visual impact, the logo must always be surrounded by a minimum amount of clear space.

**Rule:** The clear space on all sides must equal the height of the `>` glyph. No other text, graphics, or borders should enter this zone.

---

## 3. Brand Palette

A strict, high-contrast system. No additional colors outside this palette.

| Element | Hex | Usage |
| :--- | :--- | :--- |
| **Page Background** | `#F8FAFC` | Default background for all digital surfaces |
| **Surface** | `#FFFFFF` | Cards, panels, modals |
| **Border** | `#E2E8F0` | Dividers, card outlines, table lines |
| **Border Strong** | `#CBD5E1` | Input fields, focused elements |
| **Text Primary** | `#0F172A` | Headings, high-priority labels |
| **Text Secondary** | `#475569` | Body copy, descriptions |
| **Text Muted** | `#94A3B8` | Timestamps, metadata, placeholders |
| **Brand Navy** | `#0B1A3E` | Wordmark on light, dark-mode surfaces, high-contrast placements |
| **Accent / Interactive** | `#3B82F6` | Primary CTA background, links, focus rings, interactive highlights |
| **Accent Hover** | `#2563EB` | Primary CTA hover state |

### Status Colors

Status colors exist to convey state in product UIs and data visualizations. Do not use them decoratively on marketing surfaces.

| Status | Text | Background | Border |
| :----- | :--- | :--------- | :----- |
| Pass / Success | `#16A34A` | `#F0FDF4` | `#BBF7D0` |
| Fail / Error | `#DC2626` | `#FEF2F2` | `#FECACA` |
| Partial / Warning | `#D97706` | `#FFFBEB` | `#FDE68A` |
| Unknown / Neutral | `#64748B` | `#F8FAFC` | `#E2E8F0` |

---

## 4. Typography

The typography is designed to look engineered and clean - tight, legible, and information-dense.

- **Primary Font (Headings/UI):** **Inter** (Variable)
  - Weight: 400 (regular), 500 (medium), 600 (semibold), 700 (bold)
  - Letter Spacing: `-0.02em` on headings for a tight, startup look
- **Monospaced Font (Technical/Code):** **JetBrains Mono**
  - Usage: Terminal prompt logo, code snippets, technical IDs, status indicators, numeric values

---

## 5. UI & Button Style

Buttons emphasize precision and functionality over decoration.

- **Shape:** Rectangular with a minimal border radius. Cards: **8px**. Buttons and inputs: **6px**. Badges and tags: **4px**. No rounded or pill shapes (except loading skeletons).
- **Primary Button:** `#3B82F6` background, white text. Hover: `#2563EB`.
- **Secondary Button:** White background, `1px solid #E2E8F0` border, `#374151` text. Hover: `#F1F5F9` background.
- **Destructive Button:** Red variant of primary (`#DC2626`).
- **Hover State:** `150ms ease` transition. No opacity tricks - use explicit color changes.

Component-level specifications (cards, tables, form inputs, status badges, dashboard layouts) live in product UI guidelines. See Section 11.

---

## 6. Iconography

- **Style:** Stroke-based line icons only.
- **Weight:** 1.5px stroke, uniform across all icons.
- **Source:** **Lucide** (preferred) or Heroicons.
- No filled icons. No emoji as icons.

---

## 7. Professional Alias & Lockup

When pairing the logo with text, use a monospaced lockup:

`[alias] // cloud security`

*Example:* `devonbooker // cloud security`

---

## 8. Voice & Tone

The brand voice is **direct, technical, and confident without being arrogant.** Every piece of content should feel like it was written by someone who builds things, not someone who talks about building things.

### Principles

- **Lead with the technical substance.** Start with what you built, what you found, or what you solved. Skip the preamble.
- **Write for engineers, but don't gate-keep.** A hiring manager or recruiter should be able to follow the narrative without needing to understand every Terraform block. Use technical language where it's precise - simplify where it's just jargon.
- **Show the work.** Default to specifics: tool names, architecture decisions, tradeoffs, failure modes. Vague claims ("improved security posture") are banned without supporting detail.
- **No hype. No fluff.** Words like "passionate," "innovative," "cutting-edge," and "leveraging" do not exist in this brand's vocabulary. Say what it does and why it matters.
- **Confident, not performative.** State what you know. Acknowledge what you don't. Never oversell.

### Headline Style

- Short and declarative. Standard title capitalization.
- Examples:
  - `Terraform-Provisioned AWS Security Baseline`
  - `Why I Went AWS-Only`
  - `GuardDuty + CloudTrail: Detection Pipeline from Scratch`
- Avoid question-format clickbait ("Is Your Cloud Secure?") and listicle framing ("5 Things I Learned About...").

### Writing Samples (Tone Reference)

- **Good:** "This module deploys a VPC with three private subnets, enables VPC Flow Logs to CloudWatch, and locks down the default security group. No public subnets. No NAT gateway unless you need one."
- **Bad:** "I'm passionate about building secure cloud architectures that leverage cutting-edge AWS services to help organizations improve their security posture."

---

## 9. Imagery & Visual Content

Visual content supports the writing. It never replaces it.

### Screenshots & Technical Visuals

- **Preferred.** Terminal output, architecture diagrams, Terraform plan output, dashboards, and CLI workflows all reinforce the builder identity.
- **Treatment:** Use as-is with no decorative filters. Frame with a `1px solid #E2E8F0` border on a white card background. No rounded corners beyond the button radius (6px).
- **Annotation:** Use JetBrains Mono in `#0F172A` or `#475569`. No red circles or arrows.

### Architecture Diagrams

- Use the brand palette only. No AWS orange or vendor-default colors.
- Clean lines, minimal labels, no decorative elements.
- Tools: Excalidraw for drafts, SVG or Mermaid for polished versions.

### Photography

- Not a core part of the brand. If used (headshots, event photos), apply a monochrome or desaturated treatment to keep visual consistency.
- Never use stock photography.

---

## 10. Do's and Don'ts

### Do

- Use the defined palette exclusively. No additional colors.
- Keep layouts dense and information-rich. White space is intentional, not filler.
- Use monospace type for anything technical: project names, tool references, file paths, IDs.
- Let the content lead. If it reads well as plain text, the design is doing its job.
- Use standard capitalization in all published content and UI.

### Don't

- Use gradients, glows, or decorative effects.
- Use colors outside the brand palette.
- Use decorative or serif fonts.
- Use emoji in professional or published content.
- Use rounded or pill-shaped buttons and UI elements.
- Add "powered by" or tool badges unless they serve a technical purpose.
- Use marketing language: "revolutionary," "game-changing," "passionate," "innovative," "leveraging," "cutting-edge."
- Default to dark mode - light mode is now the primary surface.

---

## 11. Product UI Guidelines

Product surfaces (dashboards, in-app UI, admin panels) extend this brand system with component-level specs. The brand doc governs identity, palette, typography, voice, and marketing surfaces. Product UI docs govern component behavior, layout, motion, and detailed patterns.

| Product | Guidelines |
| :------ | :--------- |
| kumo-assess | [`kumo-assess-ui-guidelines.md`](./kumo-assess-ui-guidelines.md) |

When the two conflict, the product UI doc wins within that product's surface. When building a new product, create a sibling UI doc that inherits this brand system and extends it with product-specific components.
