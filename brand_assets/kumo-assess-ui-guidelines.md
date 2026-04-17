# UI Guidelines: kumo-assess

---

## 0. Context

**Product:** kumo-assess - agentic SOC 2 compliance assessment dashboard.

**Relationship to Kumo Security brand:** kumo-assess is a product built under the Kumo Security brand. The Kumo Security brand guidelines govern logo usage, voice, and external identity. These guidelines govern the product UI specifically - the dashboard, report views, and scan workflow.

**Design direction:** Clean Light. White-surface, Inter-based, startup-grade. Prioritizes readability and information density over atmosphere. The product handles serious compliance data - the UI should be calm, structured, and fast to scan.

---

## 1. Palette

A tight, high-contrast light-mode system. No additional colors.

| Role | Hex | Usage |
| :--- | :--- | :--- |
| **Background** | `#F8FAFC` | Page background |
| **Surface** | `#FFFFFF` | Cards, panels, modals |
| **Border** | `#E2E8F0` | Dividers, card borders, table lines |
| **Border Strong** | `#CBD5E1` | Inputs, focused elements |
| **Text Primary** | `#0F172A` | Headings, labels, control IDs |
| **Text Secondary** | `#475569` | Body text, descriptions |
| **Text Muted** | `#94A3B8` | Timestamps, metadata, placeholders |

### Status Colors (data visualization only)

These exist solely to convey compliance status. Do not use them for decoration.

| Status | Text | Background | Border |
| :----- | :--- | :--------- | :----- |
| Pass | `#16A34A` | `#F0FDF4` | `#BBF7D0` |
| Fail | `#DC2626` | `#FEF2F2` | `#FECACA` |
| Partial | `#D97706` | `#FFFBEB` | `#FDE68A` |
| Unknown | `#64748B` | `#F8FAFC` | `#E2E8F0` |

### Interactive States

| State | Value |
| :---- | :---- |
| Primary action hover | `#2563EB` background, white text |
| Primary action default | `#3B82F6` background, white text |
| Secondary hover | `#F1F5F9` background |
| Destructive | `#DC2626` |
| Focus ring | `2px solid #3B82F6`, `outline-offset: 2px` |

---

## 2. Typography

The type system is designed to feel like a high-quality SaaS product - tight, legible, and information-dense without feeling cramped.

### Fonts

- **Primary (UI + headings):** [Inter](https://fonts.google.com/specimen/Inter) (Variable)
  - Letter spacing: `-0.02em` on headings, `normal` on body
  - Weight range: 400 (regular), 500 (medium), 600 (semibold), 700 (bold)
- **Monospaced (IDs, code, technical values):** [JetBrains Mono](https://fonts.google.com/specimen/JetBrains+Mono)
  - Use for: control IDs (`CC6.1`), AWS profile names, region strings, scores, status badges
  - Weight: 400, 500

```css
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700&family=JetBrains+Mono:wght@400;500&display=swap');
```

### Type Scale

| Role | Size | Weight | Font | Tracking |
| :--- | :--- | :----- | :--- | :------- |
| Page heading | 1.25rem | 700 | Inter | -0.02em |
| Section heading | 0.9375rem | 600 | Inter | -0.01em |
| Body | 0.875rem | 400 | Inter | normal |
| Small / metadata | 0.8125rem | 400 | Inter | normal |
| Label (uppercase) | 0.6875rem | 600 | Inter | 0.06em |
| Control ID | 0.875rem | 600 | JetBrains Mono | normal |
| Status badge | 0.6875rem | 500 | JetBrains Mono | 0.04em |
| Score / numeric | varies | 700 | JetBrains Mono | normal |

---

## 3. Shape & Spacing

### Border Radius

| Element | Radius |
| :------ | :----- |
| Cards, panels | `8px` |
| Buttons, inputs | `6px` |
| Badges | `4px` |
| Tags, pills | `4px` |

No pill shapes (`border-radius: 9999px`) except loading skeletons.

### Spacing Scale

Use multiples of 4px. Common values: `4 8 12 16 20 24 32 40 48`.

### Elevation

No box shadows for structural elements. Use borders instead. Reserve subtle shadow for floating elements (dropdowns, tooltips):

```css
/* Floating only */
box-shadow: 0 4px 6px -1px rgb(0 0 0 / 0.07), 0 2px 4px -2px rgb(0 0 0 / 0.05);
```

---

## 4. Components

### Cards

```
background: #FFFFFF
border: 1px solid #E2E8F0
border-radius: 8px
padding: 16px 20px
```

No decorative effects. Left accent border (3px) is permitted on control cards to indicate status - use the status border color from the palette.

### Buttons

**Primary:**
```
background: #3B82F6  →  hover: #2563EB
color: #FFFFFF
border: none
border-radius: 6px
padding: 8px 16px
font: 500 0.875rem Inter
```

**Secondary:**
```
background: #FFFFFF  →  hover: #F1F5F9
color: #374151
border: 1px solid #E2E8F0  →  hover: #CBD5E1
border-radius: 6px
padding: 8px 16px
font: 500 0.875rem Inter
```

**Destructive / danger:** red variant of primary.

All buttons: `cursor: pointer`, `transition: 150ms`, `min-height: 36px`.

### Status Badges

Rectangular (4px radius). JetBrains Mono, uppercase, tight tracking. Background + text from the status color table. Always pair text + background - never color-only.

### Tables

- `border-collapse: collapse`
- Header row: `#F8FAFC` background, uppercase Inter label style
- Row borders: `1px solid #E2E8F0`
- Row hover: `#F8FAFC` background
- No zebra striping

### Form Inputs

```
background: #FFFFFF
border: 1px solid #CBD5E1  →  focus: #3B82F6 (2px)
border-radius: 6px
padding: 8px 12px
font: 0.875rem Inter, color #0F172A
placeholder: #94A3B8
```

---

## 5. Layout

### Navigation

- Height: `52px`, sticky
- Background: `#FFFFFF`, `border-bottom: 1px solid #E2E8F0`
- Logo: `>_` mark + `kumo-assess` in JetBrains Mono
- Nav links: Inter medium, `#475569` default, `#0F172A` active with `#F1F5F9` background

### Content Container

```
max-width: 960px
margin: 0 auto
padding: 32px 24px
```

### Dashboard Report Layout

The scan report uses a two-zone structure:

1. **Summary strip** - score ring + stat blocks in a single row, `#F8FAFC` background, `1px solid #E2E8F0` border
2. **Control list** - full-width, sorted fail-first, each control as a card with left accent border

---

## 6. Iconography

- **Library:** [Lucide](https://lucide.dev/) - stroke icons only
- **Stroke width:** `1.5px` uniform
- **Size:** `16px` standard, `14px` inline with text
- **Color:** inherits from text color of parent context
- No filled icons. No emojis.

---

## 7. Motion

Interactions only. No decorative animation.

| Use case | Duration | Easing |
| :------- | :------- | :----- |
| Hover state | `150ms` | `ease` |
| Expand/collapse | `200ms` | `ease` |
| Chevron rotate | `150ms` | `ease` |
| Score ring draw | `700ms` | `cubic-bezier(0.4, 0, 0.2, 1)` |

Respect `prefers-reduced-motion`: skip all transitions when set.

---

## 8. Do's and Don'ts

### Do

- Use `#F8FAFC` as the page background - not pure white
- Use borders (not shadows) to separate surfaces
- Use JetBrains Mono for anything technical: IDs, scores, profile names, regions
- Sort control results fail-first so the critical findings are immediately visible
- Keep the compliance score ring clean - no glow, no decorative effects
- Use Inter with negative tracking on headings (`-0.02em`)

### Don't

- Use gradients or glow effects
- Use pill-shaped buttons or badges
- Use color as the only status indicator - always pair with text label
- Use emojis as icons or status indicators
- Add decorative box shadows to cards or panels
- Use font sizes below `0.6875rem` (11px)
- Use more than two fonts on any single page
