# June Energy — Social Media Animation Guidelines

Guidelines for producing vertical short-form video content using the Remotion pipeline. Derived from the production codebase across all active short-video projects.

---

## 1. Format & Technical Specs

| Property | Value |
|---|---|
| Dimensions | 1080 × 1920 px |
| Aspect ratio | 9:16 (vertical) |
| Frame rate | 30 fps |
| Total duration | 1100–1200 frames (37–40 seconds) |
| Framework | Remotion 4.0.448 + React 19.2.3 |
| Styling | Inline React styles only (no Tailwind, no CSS files) |

> **Never use `landscape` or `square` formats** for social shorts. The 1080×1920 vertical format is the only production-approved canvas.

---

## 2. Brand Color System

Defined in `theme.ts` — shared identically across all projects.

```typescript
export const colors = {
  darkBg:    "#1e2d35",   // Primary background — dark teal-navy
  lightBg:   "#e8f5f4",   // Engagement scene background — mint
  green:     "#3bada8",   // June Green — primary accent
  red:       "#e85257",   // June Red — contrast/danger
  yellow:    "#fad145",   // Electricity
  blueWater: "#3087e8",   // Water energy type
  blueGas:   "#4abae0",   // Gas energy type
  white:     "#ffffff",
  muted:     "rgba(255,255,255,0.6)",
  mutedDark: "rgba(30,45,53,0.55)",
};
```

### Energy type color mapping

| Energy type | Color | Hex |
|---|---|---|
| Electricity | Yellow | `#fad145` |
| Gas | Picton Blue | `#4abae0` |
| Water | French Blue | `#3087e8` |
| Brand / savings | June Green | `#3bada8` |
| Danger / problem | June Red | `#e85257` |

### Card surfaces (on dark background)

```
background: rgba(accent, 0.10–0.15)
border: 1px solid rgba(accent, 0.35–0.40)
border-radius: 24px
```

### Scene background glows (radial gradient overlays on `#1e2d35`)

| Scene tone | Gradient |
|---|---|
| Problem / danger | `radial-gradient(ellipse at top right, rgba(232,82,87,0.10) 0%, transparent 55%)` |
| Solution / positive | `radial-gradient(ellipse at bottom center, rgba(59,173,168,0.12) 0%, transparent 65%)` |
| Gas | `radial-gradient(ellipse at top left, rgba(74,186,224,0.10) 0%, transparent 60%)` |
| Water | `radial-gradient(ellipse at bottom left, rgba(48,135,232,0.18) 0%, transparent 60%)` |

---

## 3. Typography

### Font families

- **Montserrat** (`@remotion/google-fonts/Montserrat`) — headlines, stats, labels, CTAs, everything with impact. Weight 700–800.
- **Open Sans** (`@remotion/google-fonts/OpenSans`) — body copy, captions, supporting text. Weight 400–600.

### Type scale

| Role | Font | Weight | Size (px) |
|---|---|---|---|
| Hero stat / countdown | Montserrat | 800 | 220–280 |
| Big stat (secondary) | Montserrat | 800 | 156 |
| Rule-of-thumb stat | Montserrat | 800 | 260 |
| Section headline | Montserrat | 700–800 | 52–76 |
| Sub-headline | Montserrat | 700–800 | 56–68 |
| Card label (uppercase) | Montserrat | 700–800 | 26–30 |
| Card value | Montserrat | 800 | 64–92 |
| CTA pill text | Montserrat | 700 | 52 |
| Logo URL text | Montserrat | 700 | 52–68 |
| Body / subhead | Open Sans | 400–500 | 36–46 |
| Muted label | Open Sans | 400–600 | 32–40 |
| Scene badge number | Montserrat | 700 | 38 |
| Gas meter digits | `ui-monospace, 'SF Mono', Menlo, monospace` | 700 | 92 |

### Text color rules

| Context | Color |
|---|---|
| Primary on dark bg | `#ffffff` |
| Muted on dark bg | `rgba(255,255,255,0.65)` |
| Very muted on dark bg | `rgba(255,255,255,0.50)` |
| Primary on light bg | `#1e2d35` |
| Muted on light bg | `rgba(30,45,53,0.55)` |

### Letter spacing

- UPPERCASE card labels: `letterSpacing: 1.5–3`
- URL text (`www.june.energy`): `letterSpacing: 1`
- Body copy: default / none

---

## 4. Narrative Structure

Every short follows the same **5-act arc**:

| Act | Scene | Duration | Background | Purpose |
|---|---|---|---|---|
| 1 | **Hook** | 135–195 frames (4.5–6.5s) | `#1e2d35` dark | Hero stat + floating icon + headline — grab attention |
| 2 | **EngagementTrigger** | 90–105 frames (3–3.5s) | `#e8f5f4` light | "Reageer" with keyword pill — drives comments |
| 3 | **Content Scene 1** | 270–330 frames (9–11s) | `#1e2d35` dark | Educational beats, one floating icon per beat |
| 4 | **Content Scene 2** | 270–330 frames (9–11s) | `#1e2d35` dark | Second educational section |
| 5 | **CTA** | 200–300 frames (6.7–10s) | `#1e2d35` dark | Floating icon + headline + pill + logo |

**Total: 1100–1200 frames (37–40 seconds)**

### EngagementTrigger scene rules
- Always uses light background `#e8f5f4`
- A 10px full-width green bar at the very top
- Logo switches to `variant="green"` (not white)
- The keyword pill has an **extremely bouncy** spring: `damping: 8, stiffness: 180, mass: 0.8`
- Text content: always a short action word in quotes, e.g. `"BESPAREN"`, `"AUTOMATISCH"`

### CTA scene rules
- Always ends with `CTAPill` containing `www.june.energy`
- Always ends with `JuneLogo variant="white"` at bottom center
- Always includes `BlobDecor` (red, partially off-screen bottom-right)

---

## 5. Layout & Safe Zones

**Canvas:** 1080 × 1920 px

**Horizontal safe zone:** 80px left and right gutters → **920px content width**

| Zone | Y position |
|---|---|
| Section badge + header | `top: 160–200` |
| Hero icon area | `top: 260–320` |
| Hero stat / main data | `top: 460–580` |
| Sub-headline / supporting text | `top: 820–920` |
| CTA pill | `bottom: 340` |
| June logo | `bottom: 120–150` |

**Grid math at 920px content width:**

| Division | Width |
|---|---|
| Full | 920px |
| Half | 440px |
| Third | ~287px |
| Card gap | 24px |
| Card border radius | 24px |

> Anchor key content in the **lower 60% of the frame**. Avoid vertically centering content — it reads poorly on mobile with UI chrome at top and bottom.

---

## 6. Animation Primitives

All motion must be driven by `useCurrentFrame()`. **Never use CSS `transition`, `animation`, or `@keyframes`** — they cause render flickering in Remotion.

### `spring()` — the primary motion tool

Use for all entrances, pops, and physical movements.

**Always clamp `interpolate()`:**
```typescript
interpolate(value, [in, out], [from, to], {
  extrapolateLeft: 'clamp',
  extrapolateRight: 'clamp',
})
```

**Spring presets by element type:**

| Element | damping | stiffness | mass | Notes |
|---|---|---|---|---|
| Default entrance (`FadeUp`, logo) | 80–100 | 120–160 | — | Most elements |
| `WordReveal` (words fly up) | 80 | 200 | — | Fast and snappy |
| `BigWordReveal` (large words) | 60 | 140 | 0.9 | Scale from 0.4 → 1 |
| Floating icon entrance | 55 | 110 | 1.2 | Bouncy, from below |
| `CTAPill` | 80 | 140 | — | Slides up 80px |
| `SceneBadge` (number circle) | 80 | 180 | — | Scale from 0.6 → 1 |
| `BlobDecor` | 80 | 120 | — | Scale from 0.3 → 1 |
| `LogoReveal` | 55 | 120 | 1.1 | Scale from 0.5 → 1 |
| Engagement keyword pill | 8 | 180 | 0.8 | Very bouncy — intentionally |
| `AnimatedBar` (progress bar) | 120 | 90 | 0.9 | Crisp fill, minimal bounce |
| `SavingsBar` | 120 | 70 | — | Slower fill |
| Line chart draw-on | 120 | 55 | — | Deliberate, slow draw |
| `CountUp` number | 100 | 70–80 | 1 | Slow build for big stats |
| Phone 3D entry | 52 | 62 | 1.6 | Very physical, weighted |

### Standard entrance pattern

```typescript
const enter = spring({ frame: frame - startFrame, fps, config: { damping: 80, stiffness: 140 } });

// Fade + slide up
opacity: enter
translateY: `${interpolate(enter, [0, 1], [40, 0])}px`

// Scale pop
scale: interpolate(enter, [0, 1], [0.6, 1])
```

### Universal scene exit

Every scene wrapper fades out over its final **20 frames**:

```typescript
const exit = interpolate(
  frame,
  [durationInFrames - 20, durationInFrames],
  [1, 0],
  { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' }
);
opacity: exit
```

---

## 7. Floating Animation System

Icons and graphic elements float continuously after their spring entrance — this is the core "alive" motion pattern.

### Floating icon formula

```typescript
const t = (frame - beatStart) * 0.055 + floatPhase;
const settle = interpolate(enter, [0.75, 1], [0, 1], { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' });

const floatY   = Math.sin(t) * 38 * settle;          // 38px vertical amplitude
const floatX   = Math.cos(t * 0.6) * 17 * settle;    // ~45% of vertical (17px)
const floatRot = Math.sin(t * 0.5) * 3 * settle;     // ±3 degrees rotation
```

- `floatPhase` is unique per icon to prevent sync
- Float amplitude grows in only after the spring entrance settles (`settle` easing)

### Graphic element (brand shapes) float formula

Used for bolt, flame, water, sphere brand graphics — each with unique frequency parameters so elements never move in sync:

```typescript
const t = frame / fps; // time in seconds

const floatY   = Math.sin(t * a) * ampY;    // a = 0.6–2.0
const floatX   = Math.cos(t * b) * ampX;    // b = 0.4–1.5
const rotate   = Math.sin(t * c) * maxDeg;  // c = 0.3–1.8
```

Assign unique `a`, `b`, `c` to every element. Never use the same values for two elements in the same scene.

### Blob wobble

```typescript
const wobble = Math.sin((frame - startFrame) / 30) * 3; // ±3 degrees, period = 1s
```

---

## 8. Floating Icon Beat Pattern

Content scenes are built as a series of icon "beats" — one icon at a time, never simultaneous.

**Per beat:**
- Icon springs in (see Section 6 spring presets)
- A label appears beneath the icon
- Icon floats for 70–90 frames
- Icon fades out over 15 frames (unless `stays=true` on last beat)
- Next icon enters

**Beat length:** ~90–105 frames per icon (~3–3.5s)

**Last icon in any scene:** set `stays=true` — no exit fade, it stays until the scene wrapper fades out.

```typescript
// Icon exit (all except last)
const iconExit = interpolate(
  frame,
  [beatEnd - 15, beatEnd],
  [1, 0],
  { extrapolateLeft: 'clamp', extrapolateRight: 'clamp' }
);
```

---

## 9. Stagger Timing Reference

| Element type | Entrance duration | Stagger between items |
|---|---|---|
| Section header | 20 frames | — |
| Stat card | 25 frames | 15 frames |
| Bar chart item | 20 frames | 6–8 frames |
| Body text | 15 frames | 8 frames |
| Caption | 15 frames | — |
| `WordReveal` word | — | 4–5 frames per word |
| `BigWordReveal` word | — | 7 frames per word |

---

## 10. Reusable Component Library

Located in `src/components/` in each project.

| Component | Purpose | Key defaults |
|---|---|---|
| `FadeUp` | Fade + slide-up entrance wrapper | `distance=40`, `damping=100`, `stiffness=160` |
| `WordReveal` | Word-by-word fly-up headline | `stagger=5`, supports `accentWord` + `accentColor` |
| `BigWordReveal` | Large word-by-word with scale pop + exit | `stagger=7`, per-word color and size |
| `CountUp` | Animated number count-up | `prefix`, `suffix`, `decimals`, `nl-BE` locale |
| `CTAPill` | Rounded CTA button with slide-up | See Section 11 |
| `JuneLogo` | Animated June logo | `variant="white/green/black/pink"`, `width=160` |
| `FloatingIcon` | Icon with spring entrance + float + beat exit | `icon`, `beatStart`, `beatEnd`, `filter`, `size=320` |
| `BlobDecor` | Organic blob decorative shape | `size=260`, `color`, wobble motion |
| `DotGrid` | Halftone dot pattern | `cols=8`, `rows=8`, `gap=16`, `radius=3` |
| `ZigzagLine` | Wavy underline draw-on | `color=#fad145`, SVG stroke-dashoffset animation |
| `SceneBadge` | Numbered circle scene badge | 88×88px, `color=#3bada8`, scale from 0.6 |
| `StatCard` | Card with label + CountUp + optional icon | Accent tints bg 12%, border 35% |
| `ComparisonCard` | Two-column comparison card | Same tinting as StatCard |
| `SavingsBar` | Multi-segment horizontal progress bar | Color-coded segments, animated fill |
| `AnimatedBar` | Single animated progress bar | `value 0–100`, optional marker |
| `LineChart` | SVG line chart with draw-on | `points[]`, `fill`, `axisLabels` |
| `MeterDisplay` | Gas meter digits with ellipse highlight | Monospace, `highlightColor=#4abae0`, red ellipse |
| `TypeIn` | Character-by-character typewriter | `charsPerFrame=0.6`, blinking caret |
| `LogoReveal` | Large logo + URL with underline draw-on | `logoStart=200`, `urlStart=215` |
| `FloatingElement` | Brand graphic element with continuous float | `a/b/c` frequency params, `ampX/ampY`, `maxDeg` |

---

## 11. CTA Design System

### CTAPill defaults

```typescript
background:    "#3bada8"             // June Green (use #4abae0 for gas-themed videos)
color:         "#ffffff"
fontFamily:    "Montserrat"
fontWeight:    700
fontSize:      52
padding:       "22px 52px"
borderRadius:  80                    // Fully rounded pill
boxShadow:     "0 20px 50px rgba(59,173,168,0.4)"
gap:           14                    // Between icon and text
```

**Animation:** spring `damping=80, stiffness=140`, slides up 80px from below.

**URL text:** Always `www.june.energy` — no other domain.

### EngagementTrigger pill

```typescript
fontSize:      68
padding:       "18px 44px"
borderRadius:  80
spring:        { damping: 8, stiffness: 180, mass: 0.8 }  // Very bouncy — by design
```

---

## 12. Icon System

**Base URL:** `https://raw.githubusercontent.com/grgslbn/June-brand-assets/main/`

**Icon folder:** `June_icons/` — 180+ PNG icons (UI-style, black/white source)

### CSS filter tints (from `theme.ts`)

| Token | Color | Filter |
|---|---|---|
| `tint.whiteSolid` | White | `brightness(0) invert(1)` |
| `tint.green` | June Green | `brightness(0) saturate(100%) invert(58%) sepia(60%) saturate(400%) hue-rotate(130deg) brightness(95%)` |
| `tint.yellow` | Electricity | `brightness(0) saturate(100%) invert(89%) sepia(57%) saturate(900%) hue-rotate(350deg) brightness(100%)` |
| `tint.blueWater` | Water | `brightness(0) saturate(100%) invert(39%) sepia(95%) saturate(1800%) hue-rotate(200deg) brightness(95%)` |
| `tint.blueGas` | Gas | `brightness(0) saturate(100%) invert(70%) sepia(45%) saturate(800%) hue-rotate(160deg) brightness(98%)` |
| `tint.red` | June Red | `brightness(0) saturate(100%) invert(43%) sepia(82%) saturate(3000%) hue-rotate(334deg) brightness(97%)` |

### Icon sizing

| Context | Size |
|---|---|
| Main floating icon | 280–320px |
| Hero icon (Hook / CTA) | 180–200px |
| Secondary ghost icon | 140px at 55% opacity |
| Small card icon | 60–80px |

### Brand graphic elements

```
graphic elements/Bliksem.png     → Lightning bolt (electricity)
graphic elements/Vlam.png        → Flame (gas)
graphic elements/Water.png       → Water drop
graphic elements/H20bol.png      → Water sphere
graphic elements/Bol rood.png    → Red sphere (June Red accent)
graphic elements/Bol blauw.png   → Blue sphere (gas / water)
graphic elements/Bol pattern.png → Patterned sphere (background decoration)
graphic elements/Wist je dat.png → "Did you know" badge (Hook scenes)
graphic elements/Karteling.png   → Zigzag wave
```

---

## 13. Logo Rules

### Asset URLs

```
White:  .../logo/June_logo_white.svg   → on dark background (#1e2d35)
Green:  .../logo/June_logo_green.svg   → on light background (#e8f5f4) only
Black:  .../logo/June_logo_black.svg
Pink:   .../logo/June_logo_pink.svg
```

### Usage rules

- **White** on all dark scenes (Hook, Content 1, Content 2, CTA)
- **Green** only on the EngagementTrigger light scene
- Always bottom-center: `bottom: 120–150px`
- Default size: `width: 140–160px`
- In closing `LogoReveal`: `width: 320px`
- Never overlap with data, charts, or text

### Logo animation

```typescript
// spring damping=80, stiffness=120
translateY: `${(1 - enter) * 12}px`   // 12px slide up
opacity: enter
```

---

## 14. Decorative Elements

### DotGrid

```typescript
cols=8, rows=8, gap=16–18, radius=3
color: colors.green | colors.yellow  // Match energy type
opacity: 0.5 (wrapper)
position: top-left or top-right corner of scene
animation: damping=80, stiffness=120 → opacity: 0.55
```

### BlobDecor

```typescript
color: colors.red   // Always red (#e85257)
size: 380px (CTA scenes)
position: { bottom: -80, right: -80 }   // Partially off-screen
opacity: 0.85–0.9
shape: borderRadius: "60% 40% 55% 45% / 50% 60% 40% 50%"
wobble: Math.sin((frame - startFrame) / 30) * 3  // ±3°, 1s period
scale: spring from 0.3 → 1
```

### ZigzagLine

```typescript
color: colors.yellow   // Always yellow (#fad145)
width: 260–380px
height: 22–24px
strokeWidth: 5
// Animated via SVG stroke-dashoffset draw-on
// Place under key phrases in headline sections
```

---

## 15. Background System

| Background | Value | Used in |
|---|---|---|
| Dark brand (default) | `#1e2d35` | Hook, Content 1, Content 2, CTA |
| Light brand | `#e8f5f4` | EngagementTrigger only |
| Gradient dark | `linear-gradient(135deg, #1e2d35 0%, #0d2233 40%, #1a3040 100%)` | Alternative to flat dark |
| Dark scrim overlay | `rgba(30,45,53,0.82)` | Overlay scenes (e.g. RuleOfThumb) |

Light background scenes always include a **10px full-width green bar** (`#3bada8`) at the very top.

---

## 16. Number Formatting

CountUp uses `nl-BE` locale:

```typescript
Number(value).toLocaleString("nl-BE", {
  minimumFractionDigits: decimals,
  maximumFractionDigits: decimals,
})
```

This produces Belgian Dutch formatting: period as thousands separator, comma as decimal (e.g. `€2.847` not `€2,847`).

---

## 17. Anti-Patterns — Never Do These

| Anti-pattern | Why |
|---|---|
| CSS `transition`, `animation`, `@keyframes` | Causes render flickering — Remotion renders frame-by-frame |
| `Math.random()` or `Date.now()` | Non-deterministic — breaks frame-perfect rendering |
| `useEffect` / `useState` for animation values | Use frame math directly instead |
| `interpolate()` without `extrapolateLeft/Right: 'clamp'` | Values blow up outside the input range |
| Multiple icons visible simultaneously | One icon per beat — always |
| Vertically centering key content | Reads poorly with mobile UI chrome; anchor to lower 60% |
| Overlapping scenes by more than 20 frames | Previous content still reading = feels cluttered |
| Any URL other than `www.june.energy` in CTA | Brand consistency |
| Red shapes alongside `Junior_Rood` character | Color clash |

---

## 18. Creating a New Short — Checklist

- [ ] Composition: 1080×1920, 30fps
- [ ] Load Montserrat + Open Sans via `@remotion/google-fonts`
- [ ] Import `colors` and `tint` from `theme.ts`
- [ ] Scene 1 (Hook): hero stat or question, floating icon, Montserrat 800 headline
- [ ] Scene 2 (EngagementTrigger): light bg `#e8f5f4`, green top bar, logo green, bouncy keyword pill
- [ ] Scenes 3–4 (Content): one floating icon per beat, 90–105 frames each, scene badge numbered
- [ ] Scene 5 (CTA): headline WordReveal, `CTAPill` with `www.june.energy`, `JuneLogo variant="white"`, BlobDecor
- [ ] Every scene wrapper has a 20-frame exit fade
- [ ] All icon tints sourced from `tint` constants — no hardcoded filter strings
- [ ] Numbers formatted with `nl-BE` locale
- [ ] Total duration: 1100–1200 frames
- [ ] No CSS transitions anywhere
- [ ] All `interpolate()` calls clamped

---

## 19. Reference Files

| File | Contents |
|---|---|
| `src/theme.ts` | Canonical colors, tint filters, typography constants |
| `src/components/` | All reusable animation components |
| `remotion.config.ts` | Composition registration |
| `src/Root.tsx` | Composition entry point |
| `Remotion/June_BrandBook_NEW_2018.pdf` | 2018 brand book (historical reference; `theme.ts` is authoritative) |
| `https://github.com/grgslbn/June-brand-assets` | All icons, logos, and graphic elements |
