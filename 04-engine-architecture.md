# Custom Engine Architecture: How the Render Factory Works

## One idea underneath everything

A city timelapse is not a video you edit - it is a dataset you render. The city is a spreadsheet: every building is a row stating its footprint polygon, birth year, death year, height, type. The video is a script walking through time asking, per frame: "As of this year in history, which buildings exist and how tall are they?" Change the dataset, get a different video from the same code.

## The 6 stages of the pipeline

[1. Data] -> [2. Time slices] -> [3. 3D City] -> [4. Camera] -> [5. Voice] -> [6. Render]

### Stage 1 - Data collection (input)

Three free machine-readable kinds per city:
- Modern reality: OpenStreetMap building footprints (downloadable per city)
- Historical shape: old maps (1700s/1800s/1900s) georeferenced to align with today's map
- Historical facts: which buildings existed when (Wikipedia, city archives, archaeological reports) converted into rows

### Stage 2 - The time-sliced dataset (the engine's heart)

Merged records like: building_id | footprint polygon | built_year | destroyed_year | height | type. Every building gets a birth year and sometimes a death year; destroyed-and-rebuilt plots carry two rows. Narration lines map directly to queries (e.g. "fire of 64 AD destroyed the district" = WHERE destroyed_year = 64 AND cause = fire - the engine makes exactly those buildings burn). This is the HARD engineering problem: deriving existed-in-1800-at-height from old maps. The rest is plumbing. Planned split: easy start vs deep mode so the first city ships while the deep system matures.

### Stage 3 - Growing the 3D city

Generator script drives Blender from the spreadsheet: extrude footprints to height animated by built_year (buildings grow out of the ground in their birth year); buildings past their death year get destroyed (burn/crumble/demolish, optionally rigid-body physics for drama). One scene object holds 2,000 years of change; scrub through it.

### Stage 4 - Camera choreography (new layer from the documentary niche)

Camera is authored, not fixed: a path with keyframes per chapter. Rise acts sweep over the growing city; fall acts revisit the same streets. Automated via keyframes defined per video.

### Stage 5 - Narration and sync (second new layer)

Runs opposite of usual workflow: AUDIO FIRST, visuals second. Write script -> record VO or generate TTS -> read timestamps -> engine assigns each sentence to a camera-position + time-slice pair (e.g. "at 07:24 the city is at year 1697, camera over the harbor"). Guarantee: when the narrator speaks about the Great Fire, the visual IS the Great Fire. The sync file is the bridge: narration text mapped to (year, camera) pairs.

### Stage 6 - Render and assembly

EEVEE (fast, light enough for city scale). Downstream ffmpeg/Resolve: subtitles, date stamps, music bed, title card.

## Two engine-wide principles

1. Reusability of the build: expensive part is Stage 1-2 per city; downstream is cheap and repeatable. Cities stored as reusable assets on disk - required for the flywheel (build Rome once, print 5+ videos).
2. Separation of concerns: data/ (per city) -> timeline builder (per city) -> city generator (per city) -> camera choreography (per video) -> sync (per video) -> render (shared). New city touches only the data layer; new video touches only camera+sync.

## What "custom engine" concretely means

~60% existing free tech wired together (Blender, OSM, Python); ~30% glue code written once (footprint importer, year-driven growth, timeline builder, sync mapper); ~10% per-video creative work (script, camera keyframes, story choice).
