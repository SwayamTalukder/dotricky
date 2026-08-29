.ricky — scroll-scrubbed site
=============================

Upload the whole contents of this folder to your web root.

  index.html        the scroll journey
  contact.html      standalone contact page
  frames/desktop/   351 frames, 1280x720
  frames/mobile/    351 frames, 540x960 (9:16 centre crop)

Serve over HTTPS with normal static hosting. No build step, no
dependencies. Set a long cache lifetime on frames/ — they never change.

Tuning dials, all at the top of the script in index.html:

  HEAD       frames loaded sharp before anything paints (16)
  INTRO_PX   scroll length of the opening dock (340)
  INTRO_FR   frames the dock consumes (10)
  PX         base scroll pixels per frame (9)
  PACE       per-section scroll weighting, tuned to the footage
  END_PX     scroll length of the closing unzip (1500)
  MAXC       concurrent frame requests (8)
  BEATS      frame ranges for the five RICKY values
  SUN        where the closing sun starts, measured off the last frame

There is no low-resolution pass. Frames are only ever shown sharp; if
a reader outruns the loader the picture holds on the last sharp frame.
