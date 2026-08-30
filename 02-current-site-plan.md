# .Ricky — Current Site (photoreal, deployed)

Status: **built, verified, deployed.** This document describes what exists so
it can be rebuilt or handed over.

## Architecture

Scroll-scrubbed frame sequence on a `<canvas>`. Scroll position maps to a frame
index; nothing autoplays. Two frame sets are served, chosen by orientation:

- **desktop** `frames/desktop/d_0001.webp` … `d_0368.webp` — 1280×720, pure
  downscale from 1920×1080, **no crop**
- **mobile** `frames/mobile/m_0001.webp` … `m_0368.webp` — 540×960, 9:16 centre
  crop (keeps x 656–1264 of the 1920 source), so the sides are cut

368 frames each. WebP quality 82, method 4.

| | avg frame | total |
|---|---|---|
| desktop | 19.6 KB | 7.0 MB |
| mobile | 13.0 KB | 4.7 MB |

## Tuning dials

All in `template.html` / `index.html`. `template.html` is the source;
`index.html` is generated from it by substituting the frame-source expression.

```js
const PX      = 9;      // base scroll px per frame
const END_PX  = 1500;   // the coded closing beat
const HEAD    = 90;     // frames loaded sharp before first paint (~1.76 MB)
const MAXC    = 8;      // concurrent image requests
const INTRO_PX = 340;   // opening dock travel
const INTRO_FR = 10;    // frames consumed by the dock

const BEATS = [[-9,30],[30,71],[71,183],[183,294],[294,367]];
const SUN   = {x:0.497, y:0.512};

const PACE = [
  [1,   30, 1.00],   // canyon
  [30,  58, 1.55],   // the fork — hesitate here
  [58,  66, 0.65],   // dark corridor — least to look at
  [66,  80, 1.60],   // fastest camera move in the piece
  [80, 183, 1.00],   // cave
  [183,206, 1.40],   // emergence into open water
  [206,240, 0.95],   // open water
  [240,294, 0.68],   // fog
  [294,368, 1.15]    // the city
];
```

`PACE` is scroll cost per frame. Values above 1 stretch a moment out; below 1
races through. It exists because perceived speed is not camera speed — it is
how much the frame changes. Tight canyon walls rip past; open water barely
changes. Without weighting, the canyon feels frantic and the water feels dead.

Total scroll: sequence 3513 px + dock 250 + ending 1500 + contact 900.

## Beat boundaries, derived from content

| frame | event |
|---|---|
| 30 | canyon → the fork |
| 71 | cave mouth first visible |
| 183 | clip 2 → 3 junction; emergence into open water |
| 240 | fog bank |
| 294 | first tower ghosts through the haze |

## Source footage

Four Veo clips, 1920×1080, 24 fps, 192 frames each, chained: each clip's last
frame is the next clip's start frame. Assembled in DaVinci Resolve with
hand-built cross-dissolves at all three junctions (chaining does most of the
work, so the blends are between near-identical images). Fog section trimmed.

Result: `dotricky_me_mute.mov`, 736 frames, 30.667 s. Extracted every 2nd frame
→ 368 at 12 fps.

### Junction repair (important)

The clip 2 → 3 cross-dissolve ended one frame short. Measured across it, the
colour steps ran −8.0, −15.8, −18.9, −11.0, then **−25.6** in a single frame,
then flat. Brightness dropped 42% and hue flipped warm-gold to navy instantly.

Fixed at extraction, not in Resolve, by carrying the dissolve's own slope four
frames into clip 3. Weights on source frames 367–371: `.82, .34, .16, .06, .02`,
applied as a **highlight-preserving gain** — `out = x + (g-1)·x·(1 - x/255)` —
so pixels near 255 do not move and the horizon glow cannot clip.

Post-fix steps: −14.1, −17.4, −21.0, −19.8, −4.8. No outlier.

The cut is where it is because the **geometry** matches exactly at that point.
Moving it produced forward-then-back-then-forward tunnel motion, which is worse
than a tonal step. Do not move the cut.

## Decisions taken and their reasons

**Regenerated all four clips in a minimal style.** The original cracked-rock
canyon was dense high-frequency texture that crunched under WebP. The fix was
to change what the rock *is* — smooth sculpted sandstone, heavy haze, flat
shadow masses — not to de-sharpen. This is why frames now compress to 19.6 KB
instead of 47 KB.

**Rejected 1920×1080 frames.** Measured: hi-frequency energy rises 33–60%, but
most of that increase is h264 noise from the source, not detail. The downscale
to 1280 acts as a denoiser. Going to 1920 costs 60% more payload and
reintroduces the exact speckle the regeneration removed.

**Rejected posterising the footage to 4–5 colours.** Tested. Fog becomes two
flat bands with a ragged edge; the gold horizon becomes a hard ellipse. Also
counterintuitive: flat colour is *larger* in lossy WebP (186 KB vs 16 KB for a
canyon frame) because hard edges are high-frequency. Even in the right format
(WebP lossless, palette) the saving is only ~7 MB → ~4.5 MB.

**No low-resolution first pass.** `HEAD = 90` loads 90 sharp frames before
first paint. If a reader outruns the loader, the picture holds on the last
sharp frame rather than degrading.

## Known open items

- Archivo has never been visually verified — Google Fonts was blocked in the
  build sandbox, so all QA screenshots show system-sans fallback.
- Caption contrast over the brighter frames is marginal. Dial: `#veil` last
  radial stop `.62` → `.72`.
- A contact / WhatsApp button in accent gold is still on the table. Bottom-left
  is the recommended placement — clear on every viewport, natural thumb reach
  on mobile, and it does not collide with the frame counter or the watermark.
