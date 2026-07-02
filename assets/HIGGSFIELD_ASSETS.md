# Higgsfield asset slots — how to drop your own visuals in

The site currently ships **self-contained** (light theme, hand-built CSS/SVG mockups,
a real portrait, and a rendered OG cover). No AI-generated imagery is used.

When **you** generate assets in Higgsfield yourself and approve them, they can be
dropped into the slots below with no redesign. Art direction for each lives in your
local `CLAUDE_HIGGSFIELD_PROMPTS.md` brief (kept out of the repo). Keep text as real
HTML — never bake copy into an image. Compress everything to WebP/AVIF and keep it fast.

---

## 1. Floating hero portrait (the main one) — READY

**File:** `assets/portrait-cutout.webp` (transparent background, subject only)
**Recommended size:** ~760×950, transparent PNG → convert to WebP
**Art direction:** `CLAUDE_HIGGSFIELD_PROMPTS.md` → *Prompt 2: Transparent Portrait Cutout*.
Safest generation path is Higgsfield **`remove_background`** on the existing portrait
(keeps the real face) rather than a generative face prompt.

**To enable (3 steps, no other change needed):**
1. Put the cutout at `assets/portrait-cutout.webp`.
2. In `index.html`, on the hero `<div class="hero-visual …">`, change
   `data-portrait="framed"` → `data-portrait="cutout"`.
3. Uncomment the `<source srcset="assets/portrait-cutout.webp" …>` line just below it.

The CSS already handles cutout mode: the frame/border/location-pill drop away and the
cutout floats on the existing soft glow (`.hero-glow`) with a drop-shadow.
The current framed portrait stays as the automatic fallback if the file is missing.

## 2. Open Graph cover — OPTIONAL (already have a real one)

**File:** `assets/og-cover.png` (1200×630) — currently a real render of the hero.
Replace this file only if you want a Higgsfield version.
**Art direction:** *Prompt 6: Open Graph Cover*. Keep title text as a safe zone.

## 3. System visuals (dashboard / CRM / workflow) — OPTIONAL, not recommended

These are currently **CSS/SVG mockups** inside `index.html` (crisp, responsive, real
readable labels, ~0 KB). Higgsfield raster versions risk fake unreadable microtext and
add page weight, so CSS/SVG is the intended default.

If you still want to swap one in later, add e.g. `assets/system-dashboard.webp` and
replace the corresponding `.sys-visual` block's `.mock` with an `<img>`. Art direction:
*Prompt 3 (finance/ops dashboard)*, *Prompt 4 (CRM/follow-up)*, *Prompt 5 (workflow)*.

---

### Rules for any dropped-in asset
- Responsive (`max-width:100%`), meaningful `alt` text, WebP/AVIF, reasonable file size.
- Don't rely on an image to communicate core copy.
- Use the shared **negative prompt** in `CLAUDE_HIGGSFIELD_PROMPTS.md` for all generations.
