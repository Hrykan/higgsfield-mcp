# yuga.life Marketing Video — HyperFrames Build (v2)

Built: 2026-04-29 by autonomous build pass.
Output: `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/videos/joined-v2.mp4`
Project: `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/video-composition/`

---

## Render Result

| Metric           | Value                |
| ---------------- | -------------------- |
| Duration         | 29.000s              |
| Resolution       | 1344 x 768 (16:9)    |
| Frame rate       | 24 fps (696 frames)  |
| Video codec      | H.264 (libx264)      |
| Audio            | AAC, 48 kHz stereo   |
| File size        | 13.52 MB             |
| Render time      | ~71s on 10-core M-series |
| Lint status      | 0 errors, 1 informational warning (file length) |
| Layout inspect   | 0 issues across 9 timeline samples |

---

## Composition Structure

Single-file standalone composition (`video-composition/index.html`, 396 lines).
The brief's recommended sub-composition split was deferred — the timeline is one continuous
arc and splitting it adds complexity without testing benefit at this scale.

### Tracks

| Track | Content                      | Z-index purpose                           |
| ----- | ---------------------------- | ----------------------------------------- |
| 0     | clip-1a (real-world wide)    | Always-on base                            |
| 1     | clip-1b (phone close-up)     | Crossfades over 1A                        |
| 2     | clip-1c (teleport)           | Crossfades over 1B                        |
| 3     | clip-1d (domain reveal)      | Crossfades over 1C                        |
| 4     | afterglow backdrop div       | Holds warm world after 1D source ends     |
| 5     | radial vignette div          | Subtle full-time depth                    |
| 6     | corrected domain grid        | Animated overlay (24 tiles)               |
| 7     | bottom-left captions         | Challenge / Decide / Grow                 |
| 8     | yuga.life wordmark           | Final hero                                |
| 9     | audio bed `<audio>`          | Synth bed driving the arc                 |
| 11    | wordmark tagline             | "Learn what matters."                     |

`data-track-index` separates clips for the framework's mount/unmount logic. Visual layering
is handled by CSS `z-index`. CSS positions every element at its hero-frame state; GSAP
animates IN only — no exit tweens before transitions, per `house-style.md`.

---

## Timing Map

```
t=00.0 ─ clip-1a IN  (Challenge. caption fades in 0.4-1.0s)
t=07.5 ─ clip-1b OPACITY 0→1 over 0.5s (1A → 1B crossfade)
t=12.0 ─ clip-1b ENDS    (effective trim: data-media-start=3.5s, duration=4.5s)
t=11.5 ─ clip-1c OPACITY 0→1 over 0.5s (1B → 1C crossfade)
t=12.0 ─ Decide. caption fades in 0.5s
t=16.5 ─ clip-1c ENDS (5s effective length)
t=16.2 ─ clip-1d OPACITY 0→1 over 0.3s (1C → 1D crossfade)
t=17.0 ─ Grow. caption fades in (amber, 0.6s)
t=21.0 ─ Domain grid container fades in 0.7s + scale 0.94→1
t=21.15 ─ 24 tiles cascade IN, 50ms stagger, power3.out (~1.4s total)
t=23.7 ─ Afterglow backdrop fades in 0.6s (covers 1D source ending)
t=24.2 ─ clip-1d source ends (frozen frame is masked by afterglow)
t=25.0 ─ yuga.life wordmark scales in 0.9s (0.94→1)
t=25.0 ─ Domain grid eases to 0.32 opacity (still visible behind wordmark)
t=25.6 ─ "Learn what matters." tagline fades in 0.7s
t=29.0 ─ END
```

### Crossfades match the brief

| Transition          | Spec  | Built |
| ------------------- | ----- | ----- |
| 1A → 1B-trimmed     | 0.5s  | 0.5s  |
| 1B → 1C             | 0.5s  | 0.5s  |
| 1C → 1D             | 0.3s  | 0.3s  |

---

## Domain Grid (the critical fix)

The previous v1 build kept clip-1d's misspelled labels visible
("Engingsring", "Systeme", "Decision Msking", "Agriouture", "Crafte/Hralth").

v2 overlays a corrected 4×6 HTML grid:

| Row | 1 | 2 | 3 | 4 | 5 | 6 |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Ethics | Critical Thinking | Systems Thinking | Decision Making | Psychology | Clear Thinking |
| 2 | Communication | Conflict Resolution | Civic Sense | Governance | Digital Literacy | Economics |
| 3 | Mathematics | Engineering | Food & Agriculture | Energy | Craftsmanship | Health |
| 4 | Medicine | Natural Sciences | Ecology | Philosophy | History | Timeless Wisdom |

The grid sits on a dark warm backing panel (`rgba(20,12,6,0.86)`, 1280px wide, 24px radius,
backdrop-blur 6px) with an amber glow and inset rim. This panel covers most of the source
clip's mistyped labels; only the "24 Domains of Knowledge" header and a faint bottom row
peek through, which read as background tone rather than competing text.

Tiles are cream `#f4ead6` with deep brown text `#2a1a0a`, soft drop shadow, 14px radius —
matching the `end-1d.png` aesthetic from the prompt assets.

---

## Audio Sources

The audio bed is **procedurally synthesized** with `ffmpeg lavfi` (no licensing concerns,
fully reproducible). Source files live in `video-composition/audio/`.

| Section                    | Time  | Source                                                                        | Volume |
| -------------------------- | ----- | ----------------------------------------------------------------------------- | ------ |
| Dark ambient pad           | 0-12s | sine 110 Hz + 164.81 Hz + 82.41 Hz mixed, lowpass 900 Hz, fade-in 1.5s        | ~0.3   |
| UI tap (E6+E7)             | 10s   | sine 1318.51 Hz + 2637 Hz, 0.18s burst, 0.6 mix                               | spike  |
| UI tap echo                | 10.4s | same, lower volume                                                            | 0.4    |
| Brown-noise whoosh         | 12.5s | `anoisesrc=color=brown` + bandpass 400-2400 Hz, 2.5s sweep                    | 0.55   |
| Harmonic rise              | 12-17s | sine 220+329.63+440 Hz (A3-E4-A4)                                            | ~0.5   |
| Warm triumphant chord      | 17-29s | sine 130.81+196+261.63+329.63 Hz (C3-G3-C4-E4 maj), lowpass 2200, fade-out 2.5s | ~0.5   |

The three sections are concatenated with 0.5s `acrossfade=tri`, then mixed with the tap
and whoosh via `amix=normalize=0`. Final encoded as AAC 192 kbps in `audio/bed.m4a` and
attached as a single `<audio class="clip">` track.

The brief's preference of "subtle UI tap + tonal shift rising" during the close-up is
delivered by the tap pair at 10s/10.4s landing right before the rise begins at 12s.

---

## Style / Design

Generated `video-composition/DESIGN.md` before any HTML. Locked palette:

- Real-world: `#0a1a2e` deep navy, `#1c2e4a` cool ambient
- App-world: `#1a1008` dark warm brown, `#e08c47` golden amber
- Domain tile: `#f4ead6` cream / `#2a1a0a` deep brown text
- Captions: white `#ffffff` with text-shadow; "Grow." in amber `#f0a86a`
- Final wordmark: `#f0a86a` with double amber glow (32px + 80px text-shadow)

Typography: Inter — 700 wordmark, 500 captions/tiles, 400 tagline. Letter-spacing -0.025em
on the wordmark for the tight modern brand feel. The HyperFrames compiler embedded Inter
automatically (1 font family) — no external link required.

Motion follows house-style defaults: `power2.inOut` for crossfades, `power3.out` for
entrances, restraint over bounce, no exit tweens before transitions (per the
non-negotiable rules in `SKILL.md`).

---

## Deviations from the Brief

1. **`npm install` skipped.** `npx hyperframes init` does not generate a `package.json` —
   `npx hyperframes` is invoked directly. No deviation impact.

2. **Render flags `--width` / `--height`.** The brief command included `--width 1344
   --height 768`. The current `hyperframes render` CLI does not accept those flags;
   composition dimensions come from `data-width`/`data-height` on the root div, which I
   set to 1344 x 768. The output matches the requested resolution exactly.

3. **WebAudio API rejected for the audio bed.** Generating tones via WebAudio at runtime
   is non-deterministic in the headless render harness — the recorder samples
   `<audio>`-element output, not WebAudio graph output, which would produce silence in
   the MP4. I pre-rendered a deterministic synth bed via `ffmpeg lavfi` instead. Same
   sonic intent, reliable capture.

4. **Sub-composition split skipped.** The lint warns the 396-line file could be split.
   For a single-scene narrative arc with shared timing, a split adds cognitive cost
   without isolation benefit. Re-evaluate if this becomes a recurring asset.

5. **clip-1d source labels not fully hidden.** The corrected grid backing panel covers
   ~92% of the source. Top-row "24 Domains of Knowledge" header and a sliver of the
   bottom row remain visible at the edges. They read as background atmosphere; the
   misspellings the brief flagged ("Engingsring", "Systeme", etc.) are entirely covered
   by my overlay tiles. To fully kill the source, I'd add a full-frame dark wash at 23s
   or stretch the panel to the full canvas — both would lose the cinematic pull-back
   feel of the source clip's reveal.

6. **No procedural noise-grit overlay.** The brief implies particles / soft blue bokeh
   via the source clips alone — they already include subtle bokeh in the navy world,
   which carries the mood without an additional CSS particle field. Added a radial
   vignette layer for cinematic depth instead.

---

## Verification

```bash
ffprobe -v quiet -print_format json -show_format \
  "/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/videos/joined-v2.mp4"
# → Duration: 29.000000  Size: 14177587 (≈ 13.52 MB)
```

Lint and inspect:

```bash
cd "/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/video-composition"
npx hyperframes lint     # 0 errors, 1 informational warning
npx hyperframes inspect  # 0 layout issues across 9 samples
```

Visual spot-check via 3.5s-interval thumbnails confirmed:

- t≈3s: silhouette in navy world, bokeh visible, "Challenge." caption present
- t≈10.5s: phone close-up, yuga.life icon glowing amber
- t≈14s: teleport amber transition, silhouette in mid-shift
- t≈17.5s: app-world figure, source domain tiles starting to reveal, "Decide." → "Grow."
- t≈21s: silhouette arms-spread, source grid revealed (overlay just entering)
- t≈24.5s: corrected 24-tile grid centered, dark backing panel covering source labels
- t≈28s: "yuga.life — Learn what matters." in amber over dimmed grid backing

---

## Files Created / Modified

```
video-composition/
├── DESIGN.md              # Visual identity (palette, motion, anti-patterns)
├── index.html             # The composition
├── hyperframes.json       # Auto-generated by `init`
├── meta.json              # Auto-generated
├── AGENTS.md / CLAUDE.md  # Auto-generated guidance
├── audio/
│   ├── bed.m4a            # AAC, 29s — the final audio bed
│   └── bed_final.wav      # Source WAV (kept for re-encoding)
└── snapshots/             # 6 PNG layout-verification snapshots

assets/videos/
└── joined-v2.mp4          # The render

HYPERFRAMES_BUILD.md       # This file
```

---

## Follow-up Suggestions

1. **Replace synth audio with licensed track** — the procedural synth bed is functional
   but reads as "tonal demo". A brand spot benefits from a custom score; the timing map
   above can be handed to a composer.
2. **Re-render at 1920x1080** — bump `data-width`/`data-height` to 1920/1080. Source
   clips upscale acceptably from 1280x720 with `object-fit: cover`.
3. **Fade clip-1d to black at 23-24s** — would eliminate the last sliver of source
   header text bleed-through behind the grid panel. Trade-off: loses the seamless arc.
4. **Consider a 60 fps render** — at 24 fps the captions and tiles' fine motion can show
   light judder on certain displays. 60 fps would smooth the staggered tile entrance.
