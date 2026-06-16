# yuga.life Marketing Video — Session State

## Active Jobs (waiting in queue)
- Clip 1A: `6240e264-2bc8-4432-baa9-c2a18e618020` — Lost → Yuga words
- Clip 1B: `57d95aaa-6176-4cd0-bd0e-8e68328bd3f7` — Yuga words → clicks app
- Clip 1C: `5d2e3819-95c2-4705-893d-f32f1a2a2da3` — Clicks app → teleport to app world
- Clip 1D: `3cc9f8b1-5876-4b1f-b736-252b8e7729c9` — App world → domain grid reveals

## Uploaded Media IDs
- ref-character:    5dfb3a8e-6b19-46eb-87cb-8b15bce36b29
- ref-world-real:   cfba77f8-070d-4de9-8144-69b8e6e303eb
- ref-domain-grid:  5aac2603-7df6-48b7-9b54-76610a60e243
- ref-guruji:       340c342a-721f-4497-a7c0-5d7220e8642b
- scene-01:         fff047d4-f407-4049-aff4-3280d5c39942
- end-1a:           05721770-ab29-4b3f-8c2b-17fa8689a0b1
- end-1b:           7d203022-c2e0-4a00-8f92-1590a0fa8fbe
- end-1c:           b4e39c61-fdf6-4f86-9666-1f5226768429
- end-1d:           ca966249-bed7-4351-b2ab-f1d93b481d32

## Reference Files
All in: /Users/mukulkulkarni/VS Code Projects/higgsfield-mcp/assets/frames/
- scene-01.png         — start frame, lost figure, cold blue
- ref-character.png    — character two lighting states
- ref-world-real.png   — empty office, navy blue, no laptop
- ref-world-app.png    — app world environment
- ref-domain-grid.png  — actual 24 domain icons (source of truth)
- ref-ui-card.png      — challenge card UI
- ref-guruji-sheet.png — Guruji character sheet
- ref-guruji.jpg       — original Guruji photo
- end-1a.png           — 4 Yuga words orbiting figure
- end-1b.png           — YL app on phone screen
- end-1c.png           — silhouette in awe, domain grid behind
- end-1d.png           — full readable domain grid

## Act 2/3 Production (2026-06-11)
### Uploaded Media IDs
- act2-start (joined-v6 last frame): d6eb1cd9-79dd-4aaa-8978-83974ee98e24
- ref-ui-card:      c3483836-abde-42d3-a899-705cefafb6d3
- ref-world-app:    1aacdbbc-a03f-4f73-8f1f-816faa3b8572
- ref-guruji-sheet: 696a63e5-abb0-45e2-bd20-b740b27df59c
- joined-v6 video:  e16786e7-30df-4608-825c-ce00291ac4fa

### End Frame Job IDs (use as medias value directly)
- end-2a (challenge card scene, gpt_image_2): d1c37d27-1ed5-48cb-880c-ef0aed6338d8
- end-2b (decision tap, seedream_v4_5):       a0b669c0-4586-4dc4-b390-ae83657450a6
- end-3a (Guruji appears, seedream_v4_5):     7aeac11d-2a1a-497f-94fa-bf188adffd3c
- end-3b (yuga.life wordmark, gpt_image_2):   8e9f265a-3cc4-4b9e-b898-13d5c386c80d

### Video Clip Job IDs (seedance_2_0 std 720p)
- clip-2a (8s, grid → challenge card):  ced52b57-1bfd-4a69-9ca3-242390995e59
- clip-2b (4s, decision tap):           5822fe5a-cd70-49b7-8539-7ee80caddeb7
- clip-3a (8s, card → Guruji):          4c33da5b-c484-4f25-86bf-416627a24384
- clip-3b (8s, blessing → wordmark):    4b260bda-d099-4035-b167-f7d92f256411

### Notes
- nano_banana_flash/nano_banana_2 REMOVED from API catalog — use seedream_v4_5 (precise/transform) or seedream_v5_lite (instruction edit) instead
- Video analysis of joined-v6: clean 4-scene ad structure, no inconsistencies flagged

## Delivery Cuts (2026-06-16)
### Music bed
- sonilo_music job: cd6751db-22b9-45e4-86a0-93ab8c9b5f7e (52s, full emotional arc)
- File: assets/audio/music-bed-v1.m4a

### Output files (all in assets/videos/)
- final-v1.mp4          — source 51.8s narrative (mixed Seedance audio)
- final-v1-music.mp4    — MARKETING/YouTube cut: music bed replaces Seedance audio,
                          fade in/out, loudnorm I=-14 TP=-1.5 (measured ~-12.3 LUFS)
- final-v1-scroll.mp4   — landing-page scroll variant, SILENT (audio stream stripped)
- final-v1-scroll.webm  — same, VP9 CRF 32 (~5.9MB)

### Landing-page deploy
- Yuga-odysseys-v1/.../landing-page/assets/videos/user-journey.{mp4,webm} replaced
  with the silent scroll variants. Originals saved as *.bak alongside.
- Page <video> is muted+loop+playsinline, plays on scroll-into-view (IntersectionObserver,
  animations.js). Full 51.8s kept per decision; GSAP timeline holds ~4s of it on scroll-past.

### Committed
- github.com/Hrykan/higgsfield-mcp @ b908082 — curated source assets (clips, ref/end frames,
  final cuts, music bed, HyperFrames project). *-review/ QA frames gitignored.
