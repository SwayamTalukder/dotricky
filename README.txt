.ricky — scroll sequence

  index.html          the scroll-scrubbed sequence
  contact.html        standalone contact page
  frames/desktop/     351 frames, 1600x900   (landscape viewports)
  frames/mobile/      351 frames, 600x1067   (portrait viewports)

Open index.html in a browser. Scroll drives everything; nothing plays
on its own. The page picks a frame set on load by comparing viewport
width and height. To host, upload this folder as-is.

FONT
  Both pages set --mono and --sans at the top of their <style> block.
  Swap "JetBrains Mono" for the face used on dotricky.me and update the
  Google Fonts <link> to match. Nothing else needs touching.

TUNING (top of the <script> block in index.html)
  PACE     scroll cost per frame — >1 stretches a moment, <1 races through
  PX       base scroll pixels per frame (9). Raise for a longer scroll.
  END_PX   length of the coded closing beat (1500)
  BEATS    frame ranges for the five RICKY values
  SUN      where the glow starts contracting, measured off the last frame
