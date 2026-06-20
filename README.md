# Rotating Parts Storage Rack — Landing Page v2 (Figma-driven)

Pre-launch landing page for the **Rotating Parts Storage Rack**, rebuilt from the Figma design at [LAALAASENG](https://www.figma.com/design/E4Oj1C1sGVlp0ru6ugv9dG/LAALAASENG?node-id=55-178).

A self-contained, single-file static page — no build step, no external dependencies. Drop the folder on any static host (GitHub Pages, Netlify, Vercel, S3, or just open `index.html` in a browser).

---

## Project Structure

```
figma/
├── index.html              ← the page (35 KB, single file, inline CSS)
├── section-markers.json    ← 15 section markers, consumed by the validator
├── assets/                 ← 15 Figma originals (nav logo + 14 images), 77 MB
│   ├── nav-logo.svg
│   ├── hero-bg.jpg
│   ├── hero-underline.png
│   ├── hero2-bg.jpg
│   ├── intro-1.jpg
│   ├── strategy-01.jpg
│   ├── strategy-02.jpg
│   ├── strategy-03.jpg
│   ├── art-3d-printing.jpg
│   ├── art-lego.jpg
│   ├── art-jewelry.jpg
│   ├── art-woodworking.jpg
│   ├── diagram-form.jpg
│   ├── diagram-mold.jpg
│   └── diagram-material.jpg
├── README.md               ← this file
├── .gitignore
└── .github/
    └── workflows/
        └── deploy.yml      ← auto-deploy to GitHub Pages on push to main
```

---

## Quick Start

### Preview locally

```bash
cd figma/
python3 -m http.server 8000
# open http://localhost:8000/ in your browser
```

Or just double-click `index.html` (image paths are relative).

### Validate content

```bash
# from the landing-page-build/ root
python3 scripts/validate_copy.py figma/
# exit 0 = pass, exit 1 = has FAILs
```

The validator runs 8 hard rules + 2 brand-config rules:
- 禁用词扫描 (forbidden vocabulary — `大容量`, `收纳神器`, `完美`, etc.)
- 数字锚点白名单 (numbers ≥ 100 must be in `{17, 7, 120}` or be a year 2024–2030)
- 感叹号密度 (≤ 3 exclamation marks)
- 一级品牌词频次 (≥ 1 of `Workflow`, `Focus`, `Momentum`, `Creative Flow`, `Frictionless`, `Modular`)
- **15 section markers in order** (configured by `section-markers.json`)
- 视频嵌入 (autoplay + loop + muted + playsinline) — N/A for v2 (no videos)
- 视频文件 < 8MB — N/A for v2
- 单文件 HTML (no external CSS/JS, no external font loads)
- Brand §7 R1 (interruption / 打断 / 节奏 / rhythm ≥ 2)
- Brand §7 R4 (Spin Motion / Spin. Find. Done / One Spin / spin_motion ≥ 2)

---

## Section Structure (15 sections, in order)

| # | Section | Marker | Source |
|---|---|---|---|
| 1 | **S01 Hero** — *One Spin. Zero Search.* | `"Zero Search."` | Figma Hero 1 |
| 2 | **S02 Pain** — *Does This Look Familiar?* | `"Look Familiar"` | Figma intro 1 |
| 3 | **S03 Product Reveal** — *A Better Workflow Starts with a Spin* | `"Better Workflow"` | Figma intro 2 |
| 4 | **S04 Strategy 01** — *01 One Spin. Instant Access.* | `"Instant Access."` | Figma strategy 01 |
| 5 | **S05 Strategy 02** — *02 See Everything at a Glance.* | `"See Everything at a Glance."` | Figma strategy 02 |
| 6 | **S06 Strategy 03** — *03 Built Around Your Workflow.* | `"Built Around Your Workflow."` | Figma strategy 03 |
| 7 | **S07 Built for Creators** — 2×2 art direction grid | `"Built for Creators"` | Figma art direction |
| 8 | **S08 Prototype Story** + 3-up diagram | `"Prototype Story"` | Figma prototype |
| 9 | **S09 Join Early. Get More.** — perks list | `"Join Early"` | Figma perks table |
| 10 | **Rave Reviews** (placeholder, §6 Gap #3) | `"Rave Reviews"` | v1 placeholder |
| 11 | **S10 Product Information** — 9-image grid | `"Product Information"` | v1 (now using Figma photos) |
| 12 | **S11 Rewards** (placeholder, §6 Gap #1) | `"Rewards"` | v1 placeholder |
| 13 | **S12 Shipping Timeline** (placeholder, §6 Gap #2) | `"Shipping Timeline"` | v1 placeholder |
| 14 | **S13 Brand Story** — *Why Are We Here* (long body) | `"Why Are We Here"` | v1 long-form |
| 15 | **S14 Hero 2** — *Ready to Stop Searching?* (bottom CTA) | `"Stop Searching"` | Figma bottom CTA |

The placeholder sections (Rave Reviews, Rewards, Shipping Timeline) intentionally render as dashed-border cards with `§6 Gap #N` tags. Backfill the data later and replace the `<section class="placeholder">` block.

---

## Design System

Locked from the Figma design. Edit the `:root` block in `index.html` to change globally.

### Colors

| Token | Value | Use |
|---|---|---|
| `--color-accent` | `#F45F00` | primary brand orange (numbers, eyebrows) |
| `--color-button` | `#fe5000` | CTA button background |
| `--color-ink` | `#000` | body text |
| `--color-muted` | `#575757` | secondary text, supporting copy |
| `--color-bg` | `#fff` | page background |
| `--color-nav` | `#fffdf9` | nav cream (top of page) |
| `--color-divider` | `rgba(0,0,0,0.1)` | section dividers |

### Typography

Single family: `"Rethink Sans"` (Figma). Falls back to system sans-serif since Rule 8 forbids external font loads.

| Token | Spec |
|---|---|
| Heading 1 / 2 | 60px / 1.1 line-height / weight 500 / letter-spacing -0.6px (44px on mobile) |
| Heading 3 | 22px / 1.2 / weight 600 / letter-spacing -0.22px |
| Paragraph | 15px / 1.2 / weight 500 / letter-spacing -0.15px |
| Caption | 13px / 1.2 / weight 500 / letter-spacing -0.13px |

### Layout

- **Desktop** (≥ 1024px): 1280px max-width, 250px left rail, 720px hero, 1030px content
- **Pad** (default 500–1023px): 800px max-width, 540px hero, 736px content
- **Mobile** (≤ 500px): 375px width, 262px hero, single-column stack, 30px perks title
- **Section vertical padding**: 88px (desktop/pad), 32px (mobile)

### Responsive Breakpoint

Three CSS tiers, no JavaScript:
- `@media (min-width: 1024px)` — desktop
- default (500–1023px) — pad
- `@media (max-width: 500px)` — mobile

The same HTML adapts to all three breakpoints.

---

## Content Update Guide

| To change... | Edit... |
|---|---|
| Hero text or kicker | `<section class="hero">` in `index.html` |
| Section headings | the `<h1>` / `<h2>` in each `<section>` |
| Body copy | the `<div class="body">` blocks |
| Strategy images | `assets/strategy-0X.jpg` (keep filenames) |
| Art direction captions | the `<p>` inside `.creators-card` |
| Diagram titles | the `<h3>` and `<p>` in `.diagram-item` |
| Perks list | the `<ol class="perks-list">` items |
| Brand story body | the `<div class="body">` inside `.brand-story` |
| Section order or naming | `section-markers.json` (validator picks up automatically) |
| Rave Reviews / Rewards / Shipping content | replace the `<section class="placeholder">` with real markup |

After any change, re-run the validator:
```bash
python3 scripts/validate_copy.py figma/
```

---

## Deploying

### GitHub Pages (auto-deploy on push)

1. Push this folder to a GitHub repo (e.g. `github.com/yourorg/rotating-rack-landing`)
2. Repo Settings → Pages → Source: "GitHub Actions"
3. Push to `main` — workflow runs and publishes
4. Live at `https://<user>.github.io/<repo>/`

### Other static hosts

- **Netlify**: drag the `figma/` folder onto netlify.com/drop
- **Vercel**: `vercel deploy figma/ --prod`
- **Cloudflare Pages**: connect repo, set output dir to `figma/`
- **S3 + CloudFront**: `aws s3 sync figma/ s3://your-bucket/ --exclude ".git/*" --exclude ".github/*"`
- **Any web server**: copy `figma/` contents into your web root

No build step. No environment variables. No server-side code.

---

## History

### v1 → v2 (2026-06-19)

The v1 page (at `../page/index.html`) was hand-built from a DOCX brief, with 6 separate benefit sections (S04–S09) and 3 spin/lock motion videos. v2 was rebuilt from the Figma design and:

| Dimension | v1 | v2 (this folder) |
|---|---|---|
| Design source | hand-built from DOCX | Figma LAALAASENG |
| Section count | 15 (14 + Rave Reviews) | 15 (12 from Figma + 3 placeholders) |
| Benefit sections | 6 (Spin / Visible / Modular / Twist-Lock / Built to Hold / Looks Good) | 3 (Figma strategies 01/02/03) |
| New sections from Figma | — | Built for Creators, Join Early, Hero 2 CTA |
| Videos | 3 (spin_motion, twist_lock) | 0 (user chose static-only) |
| Accent color | `#D97B41` | `#F45F00` / `#fe5000` |
| Type family | Inter (system fallback) | Rethink Sans (system fallback) |
| Logo | text "LAALAASENG" | SVG wordmark from Figma |
| Responsive | single @media (max-width: 768px) | 3-tier (desktop/pad/mobile) |
| Validator | hardcoded markers | externalized to `section-markers.json` |

### Validator changes (2026-06-19)

`../scripts/validate_copy.py` was refactored to:
- Accept a path argument (default `page/` for v1, `figma/` for v2)
- Read section markers from `<path>/section-markers.json` instead of a hardcoded list
- Strip `<style>` blocks before searching for markers (CSS comments can match marker text and cause false positives)

Both v1 and v2 markers live in their respective folders; one script serves both.

### Figma source

- **Tablet (800×7030)**: [node 55-178](https://www.figma.com/design/E4Oj1C1sGVlp0ru6ugv9dG/LAALAASENG?node-id=55-178)
- **Desktop (1280-wide)**: node `4:137` in same file
- **Mobile (375-wide)**: node `56:2081` in same file

This v2 is single-file responsive — the same HTML adapts to all three breakpoints via media queries. If a host requires pixel-perfect parity with the Figma mobile and desktop frames, the design system tokens in `:root` can be re-tuned per breakpoint.

---

## Out of Scope (v2.1 backlog)

- Figma's 12 wordmark vectors + nav border — only the wordmark is inlined; the 12 vector sources are bundled as a single SVG
- Figma's prototype hero image slot (node 55:1183, 736×381) was empty in Figma too — left empty in v2
- 3 placeholder sections (Rave Reviews / Rewards / Shipping Timeline) data not yet backfilled
- The desktop (1280) and mobile (375) Figma frames are approximated via media queries; current responsive layout is single-source
- 77 MB of uncompressed JPGs in `assets/` — consider WebP conversion for production (would cut ~60%)
- No analytics, no form backend wired up — email forms are `onsubmit="event.preventDefault()"` placeholders
