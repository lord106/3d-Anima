# Project Context

## What this project is

The long-term goal is a reusable, data-driven 3D filmmaking pipeline for faceless history documentaries, especially narrated “Rise and Fall of X” stories. The user wants to provide a topic, voiceover, and timestamps; the system should handle research/data preparation, story beats, visual planning, animation, and video rendering with as little manual work as practical.

The intended videos need frequent, narration-led scene changes. Each spoken event should produce a clear visual action: for example, an army approaches a city, enters it, damages buildings, and later the city expands again. The user wants persistent worlds and objects whose states change over time, cinematic camera paths, narration synchronization, realistic atmosphere (sky, sun, shadows, fog, rivers, smoke), and automated rendering. Rendering goals include headless Chrome, multiple workers for speed, and visible frame-progress counts. Do not add human characters as a requirement; the user explicitly said they are not needed for this engine concept.

## Current state and important distinction

`knowledge/01`–`05` contain the current market, niche, production, architecture, and channel strategy. The chosen direction is narrated 3D history documentaries built from reusable worlds and time-based events. The pilot city is not decided; Rome, Constantinople, and Detroit are candidates. Research accuracy and historically grounded visual data are central goals.

`Old Engine/` is a prior, working Three.js tactical/military documentary engine, not yet the city-history engine described in the strategy. It has a deterministic frame renderer, terrain and unit registries, camera and overlay systems, a voiceover/timestamp input flow, and a CLI pipeline (`beats`, `vocab`, `build`, `render`). Its current vocabulary is oriented around battles and military maps. Treat it as a technical reference and reusable starting point; do not silently assume city growth/destruction simulation, historical datasets, multiple render workers, or the complete topic-to-video automation already exist.

The detailed technical input is `Pormpt.txt`. It describes the desired persistent-world, procedural-generation, timeline/state, simulation, camera, narration-sync, and rendering architecture. The root `knowledge/04-engine-architecture.md` adds a city-data model and staged pipeline. `Old Engine/AGENTS.md` gives operational rules for that old engine; it applies when working inside `Old Engine/`, unless the user gives a newer instruction.

## Working with the user

- Treat the user as the director and product owner. The user supplies the subject and narration assets; the assistant should make concrete visual/story decisions and prepare the machine-readable plan when asked.
- Preserve the goal of a mostly automated pipeline and explain manual inputs or gaps plainly.
- Favor frequent visual beats tied to the narration, with specific on-screen actions rather than generic scene changes.
- Keep the world persistent and deterministic so a frame can be reconstructed at any timestamp and the same assets can serve multiple videos.
- Prioritize historical accuracy. Never invent narration timestamps or claim historical data is verified when it is not.
- Inspect the existing engine before proposing a replacement. Keep the current engine intact unless a requested change requires editing it.
- When authoring a video plan for `Old Engine/`, follow its local `AGENTS.md`: load the director skill, use the `beats` and `vocab` commands, write only `input/plan.json` for direction, and run `build` to validate. Render only when the user requests rendering. Load the engine-extender skill before changing its engine files.

## Key files

- `Pormpt.txt` — direct statement of the desired automation and engine behavior.
- `knowledge/01-market-research.md` — market and format research.
- `knowledge/02-niche-decision.md` — selected niche and pilot candidates.
- `knowledge/03-production-stack.md` — evidence and production-stack rationale.
- `knowledge/04-engine-architecture.md` — proposed architecture and data flow.
- `knowledge/05-strategy-flywheel.md` — channel strategy, formats, and roadmap.
- `Old Engine/AGENTS.md` — instructions for operating the existing tactical engine.
- `Old Engine/tools/pipeline.js` — current command-line workflow and validation pipeline.
- `claude-fable-5.md` — a large external assistant prompt/configuration dump; it is not a project specification or a source of project facts.

## Open decisions

The city-history engine has not yet been implemented as a complete pipeline. Key decisions still open in the notes include the first pilot city, the tools for procedural growth (Python vs. Geometry Nodes), render approach (Eevee vs. Cycles), narration source (recorded voice vs. TTS), and how historical facts and dates will be verified. Resolve these with the user or through evidence when they become relevant; do not present them as already decided.
