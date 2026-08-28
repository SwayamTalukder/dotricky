.ricky — scroll sequence

  index.html          the scroll-scrubbed sequence
  contact.html        standalone contact page
  frames/desktop/     351 frames, 1280x720   landscape, full res
  frames/mobile/      351 frames,  540x960   portrait, full res
  frames/low-d/       351 frames,  360x203   landscape, first pass
  frames/low-m/       351 frames,  202x360   portrait, first pass

Open index.html in a browser. Scroll drives everything; nothing plays
on its own. To host, upload this folder as-is.

LOADING
  Two passes. The small set loads first so the whole journey is
  scrubbable within a second or two, then the full-resolution set
  streams in nearest-to-the-playhead first and replaces it. If someone
  scrolls faster than the download, they see soft frames rather than
  blank ones. Do not delete the low-* folders.

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
