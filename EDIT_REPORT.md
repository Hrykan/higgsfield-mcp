# yuga.life Marketing Video — Stitch & Review Report

**Stitched output:** `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/videos/joined-v1.mp4`
**Total duration:** 29.37s (target was 29.2s, +0.17s rounding from final frame timing)
**Resolution / FPS:** 1280x720 @ 24fps
**Reviewer pass date:** 2026-04-29

---

## TL;DR

The clips stitch with **technically correct crossfades** but the join is undermined by **structural problems baked into the source clips themselves**, not the editing.

| Issue | Severity | Source |
|---|---|---|
| Clip-1B is ~50% redundant with Clip-1A (both show the same wide seated-figure shot for ~4s) | **Critical** | Source clip |
| Clip-1C ends with the full domain grid already revealed (last ~3s overlap conceptually with Clip-1D) | **Critical** | Source clip |
| Misspelled domain labels in 1D ("Engingsring", "Systeme", "Decision Msking", "Agriouture", "Crafte/Hralth") | **High** | Source clip |
| Time on phone clock regresses 9:41 → 9:40 between 1A/1B → 1C | Low | Source clip |
| 1A→1B crossfade is invisible because both sides show same composition | High | Editing approach |
| 1B→1C crossfade is excellent (phone screen dissolves to wide shot) | — | Working well |
| 1C→1D crossfade is smooth and effectively imperceptible | — | Working well |
| **No facial features visible at any reviewed frame** — pure black silhouette holds throughout | — | Working well |

**Overall flow rating: 5/10** — technically clean cut, but narrative pacing collapses because two transitions (1A→1B and 1C→1D) bridge clips that show nearly identical content.

---

## 1. Stitching Method

```bash
ffmpeg -y \
  -i clip-1a.mp4 \
  -i clip-1b.mp4 \
  -t 6.5 -i clip-1c.mp4 \
  -i clip-1d.mp4 \
  -filter_complex "
    [0:v][1:v]xfade=transition=fade:duration=0.5:offset=7.5[v01];
    [v01][2:v]xfade=transition=fade:duration=0.5:offset=15.0[v012];
    [v012][3:v]xfade=transition=fade:duration=0.3:offset=21.2[vout];
    [0:a][1:a]acrossfade=d=0.5[a01];
    [a01][2:a]acrossfade=d=0.5[a012];
    [a012][3:a]acrossfade=d=0.3[aout]
  " \
  -map "[vout]" -map "[aout]" \
  -c:v libx264 -preset medium -crf 18 -pix_fmt yuv420p \
  -c:a aac -b:a 192k \
  joined-v1.mp4
```

- Trim of 1c performed via `-t 6.5` on the input (lossless, no re-encode of source).
- Crossfade durations: 0.5s, 0.5s, 0.3s as specified.
- Cumulative offsets: 7.5s, 15.0s, 21.2s.
- Single-pass encode using libx264 CRF 18 for high visual fidelity, AAC 192k audio.

---

## 2. Frame-by-Frame Table (1 fps sample)

Frames extracted to `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/frames/joined-review/frame-NN.jpg`. Sub-second transition frames in the `transitions/` subdirectory.

| t (s) | Clip | What's visible | Issues |
|---|---|---|---|
| 01 | 1A | Wide seated figure with phone, deep navy room, no Yuga words yet | Clean. Mood-setting. |
| 02 | 1A | Same composition, no Yuga words | Slight static — figure barely moves between 01/02 |
| 03 | 1A | Same — small distant detail change in window | Static |
| 04 | 1A | First Yuga words appear (3 instances) with sparkle trails | Motion begins. Strong moment |
| 05 | 1A | Yuga words intensify, figure leans forward | Strong |
| 06 | 1A | Yuga words drift, figure slightly forward | Strong |
| 07 | 1A | Yuga words at peak, figure leaning further forward | Strong — last clean 1A beat |
| 08 | **1A→1B** crossfade end (figure seated, hand reaching down, table front row) | Figure pose changes mid-frame — "looking down at phone" pose. **Crossfade present but visually invisible** because 1B continues with the same seated figure |
| 09 | 1B (early) | Wide seated figure with Yuga words — visually identical to 1A frames 5–7 | **Redundant content** — 1B opens with the same composition |
| 10 | 1B | Wide seated figure, Yuga words rotating | **Redundant** — 4 seconds in and we're still in clip-1A's composition |
| 11 | 1B | Wide seated figure (now from a *very slightly* lower camera angle) | Pose shifts to two-handed phone grip, but read as the same scene |
| 12 | 1B | **Hard cut INSIDE 1B** — close-up of two hands holding phone, yuga.life icon glowing, Yuga word overlays still visible | This is the real "composition jump" — it lives **inside** clip-1B around its own ~3.5s mark. No crossfade can fix it; it's a source-side cut. |
| 13 | 1B | Pure phone close-up. Status bar **9:41**. yuga.life icon highlighted at center-left. Background pure navy #0a1a2e. Hands clearly outlined | Strong frame. Brand visible. |
| 14 | 1B | Same close-up, finger reaching toward the icon | Strong |
| 15 | 1B | Same close-up, status bar reads **9:40** (regressed from 9:41) | **Continuity error in the source clip** — clock should never go backwards |
| 16 | **1B→1C** crossfade (15.0–15.5) | Phone outline ghosting over seated figure with desk and Yuga words | **Crossfade working beautifully** — the phone dissolves into the wide shot. Best transition in the cut |
| 17 | 1C | Wide seated figure with thick amber rim-light, table glowing, Yuga words still visible, sparkle field appearing | Excellent — amber teleport begins |
| 18 | 1C | Amber sparkle field intensifies, Yuga words gone, room dissolving into starfield | Visually beautiful. Pure black silhouette. Face clean |
| 19 | 1C | Peak amber light, table glowing brightly, sparkles fill frame, app-icon row appears on right edge sliding in | Strong. Face still clean (no features) |
| 20 | 1C/1D border | App icons sliding in from both sides, figure standing now (not seated), amber backlight | Note: figure has stood up. Face still clean. Subtle pose continuity break with 1B (he was seated handheld phone, now standing arms-down) |
| 21 | 1D (early) | Full domain grid revealed, figure with arms outstretched, amber halo behind | Note: domain grid appears here BEFORE the explicit 1C→1D crossfade because clip-1c's late frames already show the grid emerging |
| 22 | **1C→1D** crossfade (21.2–21.5) | Domain grid icons momentarily ghosted/dimmed, figure outline strong | Crossfade working but largely imperceptible because both clips show the same content here |
| 23 | 1D | Full grid steady, figure arms-out, clean black silhouette | Strong |
| 24 | 1D | Same — slight zoom or push-in begins | Strong. **Misspellings visible**: "Engingsring", "Ethics" -> "Etti..." |
| 25 | 1D | Push-in continues. Labels: "Systeme Thinking", "Decision Msking", "Engingsring", "Food & Agrioutiure", "Crafternanship" | **Severe text errors in source** — 5+ misspelled labels |
| 26 | 1D | Mid push-in. "Civic Sense", "Govemance", "Systeme Thinking", "Decision Msking" | More misspellings: Govemance (should be Governance) |
| 27 | 1D | Closer push-in. "Engingsring", "Systeme Thinking", "Decision Msking" still visible | Misspellings persist |
| 28 | 1D | Title "24 Domains of Knowledge" visible at top, "Choose your" tagline starts to render. Misspellings still present | Title is clean. Tagline incomplete. |
| 29 | 1D (final) | Full title + tagline "Choose your path" visible. All 24 icons in 4×6 grid. Centered figure, head intact, no face. **Final hold frame** | Strong closing. Misspellings dominant: Systeme, Msking, Mathmatics, Engingsring, Agrioutiure, Crafternanship, Hralth, Govemance, Wisdam. **9 of 24 labels misspelled or distorted** |

---

## 3. Transition Quality Assessment

### 3.1 Clip 1A → Clip 1B (crossfade 7.5s–8.0s)

- **Mechanically correct** — sub-second frames at t=7.4, 7.6, 7.8 show clean dissolve with the second figure ghosting in.
- **Visually undermined by source content** — clip-1B's first ~4 seconds repeat clip-1A's wide-seated-figure composition. The fade dissolves something into something nearly identical, so the viewer perceives no transition at all.
- **Real "hard cut" lives inside clip-1B** at approximately its own 3.5s–4s mark, where the wide shot snaps to the close-up of hands. This is **inside the clip and not crossable** by any join-time crossfade.
- **Rating: 4/10** — the crossfade does what it was asked to do, but it's pointed at the wrong seam.

### 3.2 Clip 1B → Clip 1C (crossfade 15.0s–15.5s)

- **The strongest transition in the whole cut.**
- The close-up phone screen dissolves to the wide shot of the figure — and because the dissolving phone overlay frames the wide-shot figure, the viewer reads it as "we are pulling out of the phone screen back into the world." Narratively perfect.
- Color blend is clean (deep navy on both sides, both warming toward amber).
- No facial features appear at any point.
- **Rating: 9/10**.

### 3.3 Clip 1C → Clip 1D (crossfade 21.2s–21.5s)

- **Mechanically correct** but visually imperceptible — clip-1c's last 2–3 seconds already show the domain grid revealed, so the crossfade is dissolving "grid + amber room" into "grid + amber room."
- The 1.5s trim of clip-1c removed only the very tail; the grid-reveal had already begun before the trim.
- **Rating: 7/10** — clean and unobjectionable, but adding zero narrative value.

### 3.4 Face / Silhouette Integrity Check

**Reviewed every base frame (1–29) and every transition sub-frame (t=7.4, 7.6, 7.8, 8.0, 8.1, 8.5, 9.0, 10.0, 11.0, 14.8, 15.0, 15.2, 15.4, 21.0, 21.2, 21.4, 21.5).**

- **No facial features visible at any frame.** The figure maintains pure-black silhouette (`#000`) with hair-line, jaw-line, neck-line, and shirt collar visible only as edge contour.
- The "face visible at seconds 5–6 of clip-1c" warning in the brief was **not observed** in the trimmed output. Either the trim removed it, or it wasn't as severe as initially flagged.
- **PASS** on the most critical brand requirement.

---

## 4. Color & Style Consistency

| Section | Expected | Actual |
|---|---|---|
| Real world (1A, 1B-wide) | Deep navy #0a1a2e, cold blue, no warm tones | ✅ Match. Slight warm Yuga word glows are intentional |
| Phone close-up (1B-close) | Pure navy background, amber app glow | ✅ Match. Clean separation of cold bg vs warm screen |
| Teleport (1C) | Cold blue → amber bridge | ✅ Match. Amber sparkles take over progressively |
| App world (1D) | Dark warm brown #1a1008, golden amber #e08c47 | ✅ Match. Background reads correctly warm |
| Character | Pure black silhouette, no face | ✅ Holds across all 29 base frames |

---

## 5. Specific Recommended Fixes

Listed by priority.

### Priority 1 — Source-clip regenerations (cannot be fixed in edit)

1. **Regenerate Clip-1B** to skip its first 3–4 seconds of redundant wide-seated-figure content. The clip should open *already* on the close-up of hands holding the phone. This eliminates frames 9–11 of the joined output, which currently feel like dead time.
   - Suggested 1B duration: 4–5s instead of 8s.
   - Or alternatively, trim clip-1b's first 3.5s before stitching: `ffmpeg -i clip-1b.mp4 -ss 3.5 -c copy clip-1b-trimmed.mp4`. This is a one-line fix that recovers 3.5s of pacing.

2. **Regenerate Clip-1D label text**. At least 9 of 24 domain labels are misspelled or visually distorted. This is unshippable for a marketing video. Critical examples:
   - Engingsring → Engineering
   - Systeme Thinking → Systems Thinking
   - Decision Msking → Decision Making
   - Govemance → Governance
   - Hralth → Health
   - Crafternanship / Crafsmanship / Crafismanship → Craftsmanship
   - Agrioutiure / Agriculture (sometimes Agrioulture) → Agriculture
   - Mathmatics → Mathematics
   - Timeless Wisdam → Timeless Wisdom
   - Etting / Ethics → Ethics
   - Conflict Resaltution / Resoltion → Conflict Resolution
   - **Recommendation:** post-process the grid labels in compositing rather than re-running generation, or generate without text and add text in After Effects / Premiere as an overlay.

3. **Resolve clip-1c grid-reveal overlap with clip-1d**. Trim clip-1c more aggressively (cut the last 2.5–3s, not 1.5s) so 1c ends at the *amber-light peak* before the grid materializes. Let 1d own the grid reveal entirely. Update offsets accordingly:
   - 1c trimmed to ~5.0s instead of 6.5s
   - New offsets: 7.5, 14.5, 19.2 (instead of 7.5, 15.0, 21.2)

### Priority 2 — Edit-side improvements

4. **Replace the 1A→1B crossfade with a hard cut at the real composition jump.** Trim clip-1b to start at its 3.5s mark, then do a 0.3s crossfade between 1A's last frame and 1B's new first frame (close-up of hands). This makes the transition meaningful.

5. **Fix the 9:41 → 9:40 clock regression.** Either:
   - Replace 1B's status bar via masked overlay (frame-accurate clock graphic), or
   - Accept the inconsistency (it's only 1s of screen time and easy to miss).

6. **Add an audio bed.** All current audio is just the source clips' generated audio (likely silence or ambient). For a marketing video, layer:
   - Cold synth pad over 1A
   - UI tap + tonal shift at the 1B close-up
   - Whoosh / harmonic rise across the 1C teleport
   - Triumphant chord landing on 1D's grid reveal

### Priority 3 — Polish

7. **Slight desaturation pass on clip-1A** — currently the navy is rich; pulling -3 saturation creates more contrast with the warm 1D destination.

8. **Subtle vignette on clip-1D's grid** to draw the eye to the central figure rather than the perimeter labels (which is where the misspellings live and where the eye currently lands).

9. **Hold the final frame +0.5s** for marketing CTA / logo card overlay if needed downstream.

---

## 6. What's Working Well

- **Character silhouette discipline holds across the entire 29.37s.** Zero face leaks, zero feature drift. This is the highest-stakes element of the brief and it's clean.
- **Color story arc is correctly executed** — the cold-navy-to-amber-warm progression reads as intended, and the 1B→1C transition is a genuinely strong piece of cinematic editing where the phone screen "becomes" the world.
- **No jarring resolution / framerate / aspect changes** — all four clips are 1280x720 @ 24fps, encoder produced clean output without temporal artifacts.
- **The Yuga-word swirl in 1A** is the strongest standalone visual moment; it lands well as an intro hook.
- **The 1D final hold frame** with title "24 Domains of Knowledge" and tagline "Choose your path" is the strongest closing frame and would work well as a thumbnail / poster image (provided the labels get fixed).

---

## 7. Asset Inventory

| File | Path |
|---|---|
| Stitched output | `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/videos/joined-v1.mp4` |
| Source clips | `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/videos/clip-1{a,b,c,d}.mp4` |
| 1 fps base frames (1–29) | `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/frames/joined-review/frame-NN.jpg` |
| Sub-second transition frames | `/Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/frames/joined-review/transitions/` |

---

## 8. Recommended Next Action

**Recommended:** Do **not** ship `joined-v1.mp4` as-is. The misspelled domain labels in 1D alone block this from being a marketing-quality asset.

Highest leverage fixes in order:
1. Regenerate or text-replace clip-1d's domain labels (1 hour).
2. Trim clip-1b to start at its 3.5s mark to remove redundant wide shot (5 minutes).
3. Re-stitch with adjusted timings (5 minutes).
4. Add audio bed (separate task).

Estimated total time to a shippable v2: **~90 minutes** assuming label regeneration is the long pole.
