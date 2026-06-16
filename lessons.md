# Lessons

### 2026-06-16 — One sonilo_music prompt with timecoded beats gives a usable continuous bed

**Pattern**: For a music bed matching a narrative arc, write ONE `sonilo_music` prompt that spells out the emotional beats with explicit timecodes (e.g. "lost 0-9s … awe 13-22s … calm resolution 48-52s"). The RMS energy profile tracked the requested arc on the first generation — no segment-stitching needed. Cost ~3 credits for 52s.
**Rule**: ALWAYS describe the full arc with timecodes in a single music prompt and verify the result with an RMS/loudness profile before muxing; don't pre-build per-segment beds.
**Why**: The old 29s bed was hand-stitched from seg1/seg2/seg3 + SFX; the single-prompt 52s bed was cleaner and faster, and `loudnorm I=-14` landed it in YouTube range.

### 2026-06-16 — gitignore review-frame extractions before committing a media repo

**Pattern**: ffmpeg `fps=N` review extractions accumulate fast (309MB / 426 frames here). They're re-derivable QA artifacts, not source. Gitignore `**/review/` and `*-review/` so only the reference bible, clips, and final cuts get committed.
**Rule**: NEVER commit extracted review frames to a media repo — gitignore them; keep ref/end frames, clips, and final cuts.
**Why**: Kept the public higgsfield-mcp commit at 185MB instead of 490MB, all files <16MB (under GitHub's 100MB limit).

### 2026-06-16 — nano_banana models removed from MCP catalog

**Pattern**: `nano_banana_flash`/`nano_banana_2` no longer exist in the Higgsfield MCP — calls error "unknown model". Use `seedream_v4_5` for reference/composition-continuation and `seedream_v5_lite` for instruction edits.
**Rule**: ALWAYS run `models_explore(action:'list')` when a model errors as unknown; never assume the catalog is static.
**Why**: Lost a call mid-production to the error; the skill's default model table was stale.

### 2026-06-16 — End-frame chaining makes cuts seamless by construction

**Pattern**: Generate every end frame first (gpt_image_2 for text, seedream_v4_5 for motion poses), then pass start_image+end_image to Seedance. End frame of clip N = start frame of clip N+1.
**Rule**: ALWAYS pre-generate and approve both endpoints before animating; review the joined cut boundaries after concat.
**Why**: All four Act 2/3 cuts joined with zero composition jumps on the first stitch — no re-renders needed.

### 2026-06-16 — Hide HTML video fallback on `playing` + readyState, not just `canplay`

**Pattern**: A `{once:true}` `canplay` listener is racy with cached/fast-loading sources — it can fire before the listener attaches, leaving the fallback card covering a playing video. Add a `playing` listener and an immediate `readyState >= 3` check.
**Rule**: NEVER rely on a single `canplay` listener to reveal video / hide a poster fallback.
**Why**: New 51.8s cut played underneath but the white fallback stayed visible until this fix.

### 2026-06-11 — Review generated media before presenting

**Pattern**: Extract frames with ffmpeg (`fps=1` minimum, `fps=4` near cuts) and inspect every generated image/video before showing the user.
**Rule**: ALWAYS review Higgsfield/Seedance output frame-by-frame before declaring it done.
**Why**: Duotone aesthetic was silently dropped in one generation; misspelled domain labels appeared in another. User had to catch both.

### 2026-06-11 — Style constants live in the start frame, not the prompt

**Pattern**: Enforce character silhouette, duotone palette, and world style by passing reference images / start frames; keep prompts lean (motion + camera only).
**Rule**: NEVER re-describe character features or palette in the video prompt when a start frame already encodes them.
**Why**: Prompt re-descriptions drift; frames don't. Seedance follows the pixels over the words.

### 2026-06-11 — Seedance 2.0 silently drops unsupported params

**Pattern**: `multi_shots` / `multi_prompt` are not supported in any Seedance 2.0 mode — the request succeeds but the params are ignored.
**Rule**: ALWAYS express multi-beat scenes as sequential "then" beats in a single prompt, or as separate chained clips.
**Why**: Silent dropping wastes a paid generation and looks like a model failure.

### 2026-06-11 — NSFW filter triggers on close-up dark hands

**Pattern**: Close-up shots of dark/silhouette hands holding objects trigger the NSFW filter; words like "erupts"/"blinding" also flag.
**Rule**: NEVER use close-up dark-hand start frames; use wide shots and replace "erupts/blinding" with "expands/warm".
**Why**: clip-1c was blocked twice until the start frame was swapped to a wide seated shot.

### 2026-06-11 — HyperFrames studio edits can destroy the composition

**Pattern**: A "remove this part" selection in the studio wiped five clips and injected a wrong-path video element.
**Rule**: ALWAYS snapshot/copy index.html before letting the studio apply destructive edits; verify src paths after any studio write.
**Why**: Lost the whole multi-clip timeline at 0:06; only the rendered joined-v6.mp4 preserved the edit decisions.

### 2026-06-11 — Trim unwanted mid-clip motion with ffmpeg splits

**Pattern**: When a clip has good bookends but unwanted motion in the middle, split it into parts with ffmpeg and re-sequence in HyperFrames instead of regenerating.
**Rule**: ALWAYS try a split/trim before paying for a regeneration.
**Why**: Removed the character's get-up motion in clip-1c (t=3.5–5s) for free.
