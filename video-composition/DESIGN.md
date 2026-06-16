# DESIGN.md — yuga.life Marketing Video v2

The visual identity gate. Every color, font, motion choice in `index.html` traces back here.

## Style Prompt

Cinematic two-world brand spot for yuga.life. Opens in a cold, navy-blue real world — a faceless silhouette weighed down by abstract Sanskrit-rooted "Yuga" words. The figure taps the yuga.life app and is teleported through an amber light into a warm, golden-brown app world where 24 learning domains reveal as a structured grid. The piece is restrained, emotional, and modern — a slow camera pull, soft particles, and amber glow do the heavy lifting. No photorealism, no neon, no faces. Black silhouettes only.

## Colors

| Role                       | Hex       | Notes                                                  |
| -------------------------- | --------- | ------------------------------------------------------ |
| Real-world bg (deep navy)  | `#0a1a2e` | Background of clips 1A/1B                              |
| Real-world ambient (cool)  | `#1c2e4a` | Mid-tone navy for soft bokeh / particle glow           |
| Transition amber (mid)     | `#c47435` | Warm amber used during the teleport                    |
| App-world bg (warm brown)  | `#1a1008` | Background of clips 1C/1D                              |
| Golden amber (accent)      | `#e08c47` | Headlines, "yuga.life" wordmark, highlight glow        |
| Golden amber (light hover) | `#f0a86a` | Hover/active tint on domain tiles                      |
| Tile cream (light)         | `#f4ead6` | Domain tile fill — warm parchment, NOT pure white      |
| Tile shadow (deep)         | `#3a2010` | Soft drop-shadow under domain tiles                    |
| Foreground text            | `#ffffff` | Body / captions on dark background (use sparingly)     |
| Subdued text               | `rgba(255,255,255,0.78)` | Subtitle / context labels                  |

## Typography

- **Display / wordmark:** Inter, weight 600-700, letter-spacing -0.02em ("yuga.life")
- **Body / overlays:** Inter, weight 400-500, 22-28px on overlays
- **Domain tiles:** Inter, weight 500, 16-18px, tracking 0
- No serif. No script. No banned fonts (Roboto, default system-ui falls back to Inter).

## Motion

- 0.5s GSAP crossfades between video clips (ease `power2.inOut`).
- Domain grid tiles enter staggered (60ms apart, `power3.out`, y: 24, opacity: 0).
- Text overlays: 0.6s fade + 12px y-rise on entry; final wordmark scales from 0.94 to 1.
- No bouncy elastic — restraint matches the cinematic mood.

## What NOT to Do

1. **No face features.** The character is a pure black silhouette — collar/hair edge only.
2. **No pure `#000` or `#fff`** for backgrounds or large fills — always tint toward navy or amber.
3. **No green or pink accents** — palette is locked to navy / amber / cream.
4. **No photorealistic textures.** Stay illustrative, slightly stylized.
5. **No neon glow / cyan / purple gradients** — the standard AI-vibe defaults.
6. **No misspelled domain labels.** All 24 must read clean and correctly.
