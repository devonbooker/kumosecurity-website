# Brand Guidelines: Kumo Security

---

## 0. Brand Context

**Brand Name:** Kumo Security

**What it is:** A personal engineering brand and technical portfolio built around cloud security, infrastructure-as-code, and AI-augmented security operations. Currently a platform for publishing technical projects, documentation, and original analysis. Designed to scale into a community or consultancy as the brand matures.

**Positioning:** Lean, builder-first, startup-native. Kumo Security signals depth over breadth - someone actively engineering in the space, not observing from the sidelines. The brand should read like the output of a future staff engineer, not a student or hobbyist.

**Primary Audience:**
- Startup hiring managers and engineering leads evaluating candidates
- Technical recruiters sourcing for cloud security and DevSecOps roles
- Peers in cloud security, platform engineering, and infrastructure

**Secondary Audience (future):**
- Engineers looking for community and learning resources
- Small teams evaluating security consulting partnerships

---

## 1. Brand Identity & Logo

The primary logo is the **Terminal Prompt** (`> _`), representing hands-on engineering, building infrastructure as code (Terraform/Ansible), and the core operating environment of a SysAdmin.

### Logo Variations:
- **Primary (Dark Mode):** Pure White (`#FFFFFF`) logo on a Security Navy (`#0B1A3E`) background. This is the preferred version for the website to mimic a terminal environment.
- **Secondary (Light Mode/Print):** Solid Security Navy (`#0B1A3E`) logo on a Soft Gray (`#F5F5F5`) background. Used for PDF resumes, physical documents, or light-themed materials.

---

## 2. Logo Clear Space

To maintain visual impact, the logo must always be surrounded by a minimum amount of "clear space."

**Rule:** The clear space on all sides must equal the height of the `>` glyph. No other text, graphics, or borders should enter this zone.

---

## 3. Brand Palette

A strict, high-contrast system designed for an "Enterprise Security" feel.

| Element | Color Code | Description & Usage |
| :--- | :--- | :--- |
| **Primary Background** | `#0B1A3E` | **Security Navy.** The authoritative dark mode base. |
| **Foreground / Accent** | `#FFFFFF` | **Pure White.** For the logo, headings, and high-priority text. |
| **Subtle UI / Border** | `#1E2D50` | A slightly lighter navy used for cards, boxes, or dividers. |
| **Body Text** | `#E0E6ED` | A light, cool gray to reduce eye strain against the navy background. |
| **Light Surface** | `#F5F5F5` | **Soft Gray.** Light-mode background for print, PDFs, and secondary logo lockup. |

---

## 4. Typography

The typography is designed to look "engineered" and clean, similar to Apple's San Francisco or Helvetica Now Display.

- **Primary Font (Headings/UI):** **Inter** (Variable).
    - *Styling:* Medium weight (500/600).
    - *Letter Spacing:* Reduced to `-0.02em` or `-1.5%` for a tight, startup look.
- **Monospaced Font (Technical/Code):** **IBM Plex Mono** or **JetBrains Mono**.
    - *Usage:* Used for the terminal prompt logo, code snippets, and technical status indicators.

---

## 5. UI & Button Style

Buttons emphasize precision and functionality over decoration.

- **Shape:** Rectangular with a minimal border radius (**2px - 4px**). Avoid rounded/pill shapes.
- **Primary Button:** White background with `#0B1A3E` text.
- **Secondary Button:** Transparent background with a 1px white border.
- **Hover State:** Subtle opacity change (e.g., 0.8) or a slight lightening of the background.

---

## 6. Iconography

- **Style:** Stroke-based line icons.
- **Weight:** The line weight of icons must be uniform and match the weight of the font being used.
- **Source:** Use libraries like **Lucide** or **Heroicons** for a clean, professional appearance.

---

## 7. Professional Alias & Lockup

When pairing the logo with text, use a lowercase, monospaced lockup:

`[alias] // cloud security`

*Example:* `devonbooker // cloud security`

---

## 8. Voice & Tone

The brand voice is **direct, technical, and confident without being arrogant.** Every piece of content should feel like it was written by someone who builds things, not someone who talks about building things.

### Principles:
- **Lead with the technical substance.** Start with what you built, what you found, or what you solved. Skip the preamble.
- **Write for engineers, but don't gate-keep.** A hiring manager or recruiter should be able to follow the narrative without needing to understand every Terraform block. Use technical language where it's precise - simplify where it's just jargon.
- **Show the work.** Default to specifics: tool names, architecture decisions, tradeoffs, failure modes. Vague claims ("improved security posture") are banned without supporting detail.
- **No hype. No fluff.** Words like "passionate," "innovative," "cutting-edge," and "leveraging" do not exist in this brand's vocabulary. Say what it does and why it matters.
- **Confident, not performative.** State what you know. Acknowledge what you don't. Never oversell.

### Headline Style:
- Short. Declarative. Lowercase unless starting a sentence.
- Examples:
  - `terraform-provisioned aws security baseline`
  - `why I went AWS-only`
  - `guardduty + cloudtrail: detection pipeline from scratch`
- Avoid question-format clickbait ("Is Your Cloud Secure?") and listicle framing ("5 Things I Learned About...").

### Writing Samples (Tone Reference):
- **Good:** "This module deploys a VPC with three private subnets, enables VPC Flow Logs to CloudWatch, and locks down the default security group. No public subnets. No NAT gateway unless you need one."
- **Bad:** "I'm passionate about building secure cloud architectures that leverage cutting-edge AWS services to help organizations improve their security posture."

---

## 9. Imagery & Visual Content

Visual content supports the writing. It never replaces it.

### Screenshots & Technical Visuals:
- **Preferred.** Terminal output, architecture diagrams, Terraform plan output, dashboards, and CLI workflows all reinforce the builder identity.
- **Treatment:** Use as-is with no decorative filters. If overlaid on the site, use a subtle drop shadow or the `#1E2D50` card background to frame them. No rounded corners beyond the UI button radius (2-4px).
- **Annotation:** When annotating screenshots, use the brand monospace font (IBM Plex Mono / JetBrains Mono) in Pure White or Body Text color. No red circles or arrows.

### Architecture Diagrams:
- Use the brand palette only. No AWS-orange or vendor-default colors.
- Clean lines, minimal labels, no decorative elements.
- Tools: Excalidraw (hand-drawn style for drafts), or SVG/Mermaid for polished versions.

### Photography:
- Not a core part of the brand. If used (headshots, event photos), apply a monochrome or desaturated treatment to keep visual consistency.
- Never use stock photography.

---

## 10. Do's and Don'ts

### Do:
- Use the defined palette exclusively. No additional colors.
- Keep layouts dense and information-rich. White space is intentional, not filler.
- Default to dark mode for all digital assets.
- Use monospace type for anything technical: project names, tool references, file paths.
- Let the content lead. If it reads well as plain text, the design is doing its job.

### Don't:
- Use gradients, glows, or decorative effects.
- Use colored backgrounds outside the brand palette.
- Use decorative or serif fonts.
- Use emoji in professional/published content.
- Use rounded/pill-shaped buttons or UI elements.
- Add "powered by" or tool badges unless they serve a technical purpose.
- Use marketing language: "revolutionary," "game-changing," "passionate," "innovative," "leveraging," "cutting-edge."
