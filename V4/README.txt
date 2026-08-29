.ricky — scroll sequence

  index.html          the scroll-scrubbed sequence
  contact.html        standalone contact page
  frames/desktop/     351 frames, 1280x720   landscape, full res
  frames/mobile/      351 frames,  540x960   portrait, full res
  frames/low-d/       351 frames,  560x315   landscape, first pass
  frames/low-m/       351 frames,  315x560   portrait, first pass

Open index.html in a browser. Scroll drives everything; nothing plays
on its own. To host, upload this folder as-is.

LOADING
  Two passes. The small set loads first so the whole journey is
  scrubbable within a second or two, then the full-resolution set
  streams in nearest-to-the-playhead first and replaces it. If someone
  scrolls faster than the download, they see soft frames rather than
  blank ones. Do not delete the low-* folders.

  The sharp pass runs strictly forward from wherever the reader is.
  Frames already scrolled past are backfilled last, since nobody
  scrolls back up to admire one.

  Frames are already lossy WebP at maximum encoder effort. Do not run
  them through another compressor — re-encoding a lossy file costs
  quality and saves almost nothing.

CHROME
  Top-left is the brand: .ricky in Archivo, gold period. The five letters
  of "ricky" double as the position indicator — the letter of the value
  you are inside lights gold. There is no separate progress strip.
  Top-right is the live Johannesburg clock; bottom rail carries the
  copyright and the frame counter. Each bar has its own scrim because the
  footage runs from blown-out sand to night water.

TYPE — matches dotricky.me
  --display  Archivo, wght 800, font-variation-settings "wdth" 120
  --mono     IBM Plex Mono   (progress strip, eyebrows, buttons)
  --sans     Karla           (body copy)
  --gold     #D4AF37, glow rgba(212,175,55,.35)

  The closing dot lands on the wordmark's real Archivo period. Its
  position and size are measured from the glyph at runtime, so
  changing the display face does not break the landing.

TUNING (top of the <script> block in index.html)
  PACE     scroll cost per frame — >1 stretches a moment, <1 races through
  PX       base scroll pixels per frame (9). Raise for a longer scroll.
  END_PX   length of the coded closing beat (1500)
  MAXC     concurrent frame requests (8)
  BEATS    frame ranges for the five RICKY values
  SUN      where the glow starts contracting, measured off the last frame
