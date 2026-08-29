.ricky — scroll-scrubbed site
=============================

Upload the whole contents of this folder to your web root.

  index.html        the scroll journey
  contact.html      standalone contact page
  frames/desktop/   368 frames, 1280x720
  frames/mobile/    368 frames, 540x960 (9:16 centre crop)

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


--- rebuild, 29 Aug ---
Frames regenerated from the assembled cut (dotricky_me_mute.mov, 736 src
frames @24fps -> 368 extracted @12fps).

Junction repair baked into extraction: the clip 2 -> 3 cross-dissolve ended
one frame short, leaving a 25.6-point colour step where the neighbouring
steps were 11. fix.py carries the dissolve's own slope four frames into
clip 3 (weights .82/.34/.16/.06/.02) using a highlight-preserving gain, so
the horizon glow does not clip. Steps across the junction now read
-14.1, -17.4, -21.0, -19.8, -4.8.

WebP quality 82, method 4. Measured against source: compression adds under
7% to temporal difference in flat fog and leaves spatial detail unchanged,
so there is no shimmer to spend more bytes on.

PACE gained a [66,80,1.60] band. That stretch is the fastest camera move
in the piece (roughly 4x the average frame-to-frame change); without extra
scroll weight it races past everything around it.

Payload: desktop 7.0 MB / 368 frames (avg 19.6 KB), mobile 4.7 MB
(avg 13.0 KB). Previous build was 16.1 MB / 10.7 MB.
