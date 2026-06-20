# BRAC Student AI Solutions Lab — landing page notes

## Approach (read this first)

**motherfuckingwebsite.com + banger aesthetics.**

- Clarity, pragmatism, simplicity. No premature optimization, no scaffolding for
  hypothetical future scale, no kitchen-sink layering.
- If something's over-built, **throw it away and rebuild simple** — don't add on top.
- Frameworks are allowed *if they genuinely help*. For a static page with one
  interactive canvas, plain HTML/CSS/JS is the clearest thing — so that's what this is.
- Form over content. The aesthetic *is* the point. Keep copy minimal — no taglines,
  no marketing boilerplate. Ideally one solid paragraph and the essentials.

> History: this started as a React-via-Babel + Three.js + GSAP + Lenis build.
> That was the bloat. It's now a single ~380-line `index.html` (75KB → 13KB).

## Current state

Single file: `index.html`. No build step. One external script: Tone.js (audio).

- **White bg + light-blue gridlines** (40px), BRAC pink `#ec008c`, accent blue `#3b6fe0`.
- **Pixel headings** via the Silkscreen font (`BRAC` wordmark + section labels).
- **One `<canvas>`** runs an ambient, self-sustaining Conway's Game of Life that is
  ALSO a playable instrument:
  - hover highlights a cell,
  - click / hold-drag plays notes (C-major pentatonic, diagonal pitch gradient so
    any sweep is musical),
  - playing seeds a glider + a pink ripple,
  - sound = Tone.js Salamander piano samples (loaded from Tone's CDN) with a Web
    Audio oscillator fallback.
- Content is click-through so the whole page is playable behind the text; only
  links opt back in.

## Design tokens / knobs (all in `index.html`)

| Knob | Current | Where |
|---|---|---|
| Cell size | `40px` | `SZ` + `--cell` / gridline `background-size` |
| Tick speed | `600ms` | `STEP` |
| Density ceiling | `~13%` | `step()` rain/glider caps |
| Cell color | faint blue `0.10–0.14` | `draw()` live-cell fillStyle |
| Note scale | C-major pentatonic | `PENTA` + `noteFor()` |
| Play mark | streams a glider | `playCell()` |
| Sound | Tone.js piano + fallback | `Sound` module |

## What we want next (open / undecided)

Grid feel — to dial in:
- [ ] Life **more visible (bolder)** vs. stay whisper-faint?
- [ ] **Faster / slower** tick?
- [ ] **Busier / sparser** density?
- [ ] Hover highlights a whole **row + column** (ACP "instrument panel" feel) vs.
      single cell?
- [ ] Ripple/flash style on play.

Sound:
- [ ] Second instrument mapped to grid regions (ACP uses multiple synths)?

Type / layout:
- [ ] `BRAC` is currently the Silkscreen *font*. If we want **chunkier true-pixel
      blocks**, render it on a low-res canvas and upscale (`image-rendering: pixelated`).
- [ ] Hero spacing, gridline strength, etc.

Content:
- [ ] Trim further toward "one solid paragraph and that's all"?
- [ ] Confirm structure / timeline / contact copy.

Scope:
- [ ] Keep the instrument full-page, or confine it to the hero?

## Deploy

`origin` = `github.com/Shreas173/bracai`, auto-deploys to **bracai.vercel.app** from `main`.
