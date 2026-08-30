# .Ricky — Vector Version Plan

Status: **not built.** Two approaches attempted and rejected; this documents
what was learned so the next attempt does not repeat it.

## Why consider vector at all

- Payload collapses. The failed parametric proof was **13 KB for the entire
  journey** against 12.4 MB for the photoreal build. No loader, no `HEAD`, no
  head-start problem.
- Motion becomes continuous rather than quantised to 12 fps. Slow scrubbing is
  perfectly smooth instead of stepping.
- Sharp at any resolution forever.
- Every beat becomes editable — move a rock, retime a transition — without
  regenerating anything.
- No AI-generation watermark, because nothing is generated footage.

## Attempt 1 — parametric tunnel. FAILED.

**Idea:** the whole journey as one tunnel of pierced planes. Each gate a solid
plane with a hole cut through it, drawn far-to-near so you see through each
hole to the next. The hole's shape — width, height, roundness, roughness, a
centre pier for the fork — interpolated along the journey. Canyon becomes cave
becomes horizon with no cut, because there are no scenes to cut between.

**Why it failed:** the architecture was chosen for elegance, then the design
was forced to serve it. Two consequences:

1. A pierced plane can only ever be a hole, so everything is radially
   symmetric and dead-centre. Real landscape needs a ground plane and
   asymmetry — a canyon reads because a left wall overlaps a right wall at a
   *different distance*.
2. The beats became indistinguishable, because they were the same object at
   different settings. Restless and Curiosity are not separable when both are
   "the hole, slightly wider."

The only part that read was the city — and that is precisely the part that
stopped using the parametric system and drew an actual composition: horizon
line, skyline, sun.

**Lesson: compose scenes, do not derive them.**

## Attempt 2 — faceted canyon. CLOSER, STILL SHORT.

Rebuilt from flat-illustration references. Correct principles, identified by
studying them:

- **Facets.** Every rock mass is 2–3 flat angular tones — a lit face turned
  toward the light, a mid body, a dark face turned away. Single-tone silhouettes
  read as blobs; faceting is what makes rock read as rock.
- **Asymmetry and overlap.** Left and right walls are different shapes at
  different distances. Never mirrored, never a symmetric funnel. Offsetting the
  two walls by half a depth step helps.
- **A floor.** A sand or water wash running to the vanishing point. Without it
  there is no ground and no scale.
- **Atmospheric perspective.** Far rock desaturates toward the sky colour.
- **Light from the far end.** This is the one that was got wrong first: near
  masses are in deep shadow, the lit warm faces are in the **middle** distance,
  far masses are hazy and pale. Brightest-nearest flattens the whole image.
- **Off-centre vanishing point.**

**Why it is still short:** procedurally generated masses come out as slabs.
The references are hand-composed illustrations with varied organic-but-angular
forms and internal detail lines. Parameter-tuning converges slowly toward
something that always looks like a generated approximation of the art rather
than the art.

## Palette

**Five colours is not achievable.** Faceting needs three tones per mass × three
depth bands, plus sky and floor. The references use ten to twelve. Ramp derived
from the brand — navy in shadow, gold in light:

```
sky      #16203A  #4B4A6B  #B98A4E  #E8C88A   (top → hot horizon)
far      lit #B3AEA6   mid #918F9C   dark #6A6E88
mid      lit #DE9A3E   mid #9C5F2C   dark #4A3128
near     lit #3A2A2C   mid #241C26   dark #12101A
floor    #6E4B2C  #8A6540  #C6A473  #E2C692
brand    gold #D4AF37   paper #E8E4DC
```

Tone ramp: `u < 0.30` blends far→mid; `u ≥ 0.30` blends mid→near, where `u` is
0 at the vanishing point and 1 at the camera.

## Recommended approach for a third attempt

1. **Five separately composed scenes**, each drawn to read as what it is.
   Not one system with settings.
2. **Parallax layers inside each scene** — near, mid, far masses scaling and
   translating at different rates on scroll. Forward motion comes from
   parallax, not playback.
3. **Real transitions between scenes** — this is the hard part, and the vector
   equivalent of the Resolve overlap problem. A near mass of scene N sweeping
   past the camera can mask the handoff to scene N+1.
4. **Chrome ports unchanged.** The opening dock, beat captions, progress bar,
   closing contraction, and contact section are all independent of how the
   background is drawn. They transfer as-is from the current build.
5. **Author the art rather than generate it.** Draw the five scenes in
   Figma/Illustrator as layered SVG, export layers, and animate the layers in
   code. This is where the previous attempts broke down.

## What must survive any treatment

- The five beats in order, each visually distinguishable.
- Continuous forward motion. No cuts.
- The fork as a real, readable moment.
- The closing contraction: glow → dot → dot rises → `.ricky` resolves around it.
- Scroll as the only transport.
