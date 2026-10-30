# Production Stack Evidence: How Code-Made Visual Channels Actually Build Videos

## Principle established

Almost everything recommended is procedural/code-made (Blender + physics engines + real data), NOT AI video generation. Temporal consistency is impossible with gen-AI video (Veo/Kling cannot hold one deterministic world evolving coherently for minutes), which protects the niche as a moat. It also matters to strategy: the code route is nearly free (Blender $0, BCB $0, OSM/historical maps $0, Sketchfab CC models $0); costs are skill and render time only.

## Per-channel stacks (verified)

- EarthquakeSim: 100% Blender rigid-body physics; tsunami water simulated as thousands of transparent rigid spheres (creator explains: "single bubble looks almost invisible, but thousands overlap create darker layered blue"); structural collapse via free Bullet Constraints Builder (BCB) add-on by Kai Kostack. Numerical simulation AI video models cannot produce; featured by BBC and geophysicists.
- FilmCore: Blender 2.8/2.9 Eevee renders + Unreal Engine 4, After Effects compositing. Descriptions state it directly: "Animated in Blender 2.8, edited in Adobe CC", "Rendered in Eevee by Blender".
- CITY 3D TIMELAPSE: Blender hand-built from geodata; description literally says "No AI was used to create this Animation".
- Cornerstone Timelapse: Blender + real data: historical maps, topographic data, city open-data building footprints, Sketchfab CC-licensed landmark models. Documented by dougmahugh.com blog.
- MetaBallStudios: traditional 3D animation (true-scale cinematic scenes); free 3D asset credits (Sketchfab/CGTrader) in descriptions. Labels uploads "(3D without AI)" as an anti-AI selling point.
- RED SIDE: Unreal Engine 5.6 (+ ZBrush/CINEMA 4D).
- Timelapse Studio (EXCEPTION): actually AI-generated visuals (Higgsfield) + manual compositing and sound design; bio "Curated by humans, powered by AI". Hybrid approach reached 109K subs in 8 months.

## Asset library compounding principle

A city model "grows" with the channel: Cornerstone can rebuild the same NY scene for different eras; EarthquakeSim reuses buildings, bridges, terrain across 508 videos. An asset library compounds; AI generation credits do not. This is why quality + data accuracy separates a 9.7M-view video from a 141-view clone video at equal zero cost.

## Market timing signal

October 2026: Google's Gemini 4 Argon demo (agent writes Blender code, builds photoreal 3D temple from one prompt) hit 12.56M views in 2 weeks. Meta-signal: the cutting edge moved from "I make Blender videos" to "my agent writes the Blender code" - a frontier position on YouTube. Simultaneously, batch-producing bar-chart-race guides were published (Oct 8/14 2026), the same pre-clone-army "pipeline phase" city timelapses were in early 2025.
