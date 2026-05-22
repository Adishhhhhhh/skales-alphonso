# CLAUDE.md — Website Build Rules

The control panel for building sites in this project. Auto-loaded every session. The deep design intelligence lives in the **design-orchestrator** skill (installed globally) — this file is the practical brief + workflow that points to it.

## Always do first
1. **Invoke the `design-orchestrator` skill.** It reads the brief, commits to a direction, and casts the right combination of design specialists for THIS job (frontend-design, impeccable, taste-skill, emil-design-eng, ui-ux-pro-max, typeui-fundamentals, web-design-guidelines, react-best-practices, image-to-code). No skill is privileged — the job decides which lead.
2. **Invoke the `frontend-design` skill** before writing any frontend code.
3. State the cast before building: register (brand/product), the three dials (VARIANCE / MOTION / DENSITY), which skills you're using and why, and which you're skipping.

## What I need from you (the brief)
Bring as much as you have — I'll fill gaps, but the more you bring, the less generic the result:
- **Copy/text** — headline, value proposition, section content, CTAs (rough is fine; I can refine).
- **Structure** — which pages/sections and in what order (or I propose, you approve).
- **Must-include** — features, social proof, pricing, FAQ, forms, etc.
- **Direction** — aesthetic/vibe, and any reference sites or screenshots you like.
- **Brand** — logo, exact colors, fonts (drop into `brand_assets/`).
- **Type of build** — simple static landing page, or an app with a backend (see Output Defaults).

## Reference images
- If a reference image is provided: match layout, spacing, typography, and color closely. Use placeholder content (`https://placehold.co/WIDTHxHEIGHT`, neutral copy). Do not add to or "improve" the design.
- If no reference: design from scratch with high craft (the orchestrator's craft bar + anti-slop canon apply).

## Local preview + screenshot loop
The self-correction loop that closes the gap between "code that should look right" and "code that does."
- **Always preview on a local server, never a `file:///` URL** (file:// renders inconsistently).
- Use whatever preview/screenshot tooling is available this session (the native preview tool, or a local dev server + a screenshot script). If none exists and screenshots are needed, set one up at project start.
- Loop: build → screenshot the localhost output → read the PNG → compare against the reference (or against the intent) → fix mismatches → re-screenshot. **At least 2 rounds.** Stop only when no visible differences remain or I say so.
- Be specific when comparing: "heading is 32px but reference shows ~24px", "card gap is 16px, should be 24px". Check spacing/padding, font size/weight/line-height, exact colors, alignment, radius, shadows, image sizing.

## Brand assets
- Always check `brand_assets/` before designing. If a logo/palette/style guide exists, use those exact values — never invent brand colors when real ones are defined.

## Output defaults
- **Simple static landing page** → single `index.html`, Tailwind via CDN (`<script src="https://cdn.tailwindcss.com"></script>`), styles inline. Easiest to build and deploy.
- **App, multi-page, or anything with a backend** (auth, forms that store data, dashboards, e-commerce) → Next.js + Tailwind (works best with Vercel + Supabase).
- Placeholder images: `https://placehold.co/WIDTHxHEIGHT`. Mobile-first responsive. `min-h-[100dvh]`, never `h-screen`.
- **Motion** → React/Next projects: use **Framer Motion** for animation (I run `npm install framer-motion` in the project if it's missing — it's a per-project package, not global). Static HTML pages: CSS animations only. Either way, animate only `transform`/`opacity` and respect `prefers-reduced-motion`. Deep motion craft lives in the `emil-design-eng` and `taste-skill` skills.

## Anti-generic quick check (full depth in design-orchestrator)
- No default Tailwind blue/indigo as primary; no AI purple gradients; no pure `#000`/`#fff` (tint neutrals).
- No Inter/Arial for premium — pair a distinctive display font with a clean body font.
- Layered, color-tinted shadows — never flat `shadow-md`.
- Animate only `transform`/`opacity`; never `transition-all`; respect `prefers-reduced-motion`.
- Every clickable element has hover, focus-visible, and active states.
- No 3-equal-card rows, no cards-inside-cards, no gradient text, no fake filler copy/brands/numbers.
- Ship loading, empty, and error states — not just the happy path.

## Hard rules
- Don't add sections/features/content not asked for or not in the reference.
- Don't "improve" a reference — match it.
- Don't stop after one screenshot pass.
- Don't use `transition-all` or default Tailwind blue/indigo as the primary color.

## Deploy (when ready)
- **GitHub** = source of truth (version control). **Vercel** = frontend hosting, connected to the repo: every `git push` to main auto-builds and updates the live site.
- **Supabase** = backend (Postgres database, auth, file storage) — only needed when the site stores or serves data. Pure marketing pages can skip it.
