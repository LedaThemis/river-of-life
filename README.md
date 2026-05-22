# River of Life

> ⚠️ **AI Usage** The majority of code in this codebase was written by Claude (Anthropic's `claude-opus-4-7` model).

A single-file, no-build web app that turns your life story into an animated cartoon boat journey — and into a printable bird's-eye map of all your milestones.

Built for the **River of Life** reflection exercise: imagine your life as a river that led you to this moment. Where did it start? Where is it leading? What rocks, bridges, forks, and bright moments shaped the path?

![status: works in any modern browser](https://img.shields.io/badge/runs%20in-any%20browser-1a5490)
![dependencies: none](https://img.shields.io/badge/dependencies-none-7cc4ee)

## What it does

**Setup** — Fill in a journey title, where your river started, where it's leading, and add as many milestones as you want. Each milestone has a title, a description, a kind (calm pool, rock, waterfall, bridge, island, person, bright moment, fork, dam, fallen tree), and a position on your 0–100% life timeline.

**Animated journey** — Hit *Start* and watch a cartoon boat sail through a hand-drawn river. Hills, sun, clouds, and parallax wave layers scroll past. Milestone scenery (rocks, bridges, people on the bank, sparkling stars, lily pads…) appears at the moments you set, while a styled speech-bubble pops in with the title and description. Day / sunset / starry-night themes and clear / cloudy / rainy moods.

**Video export** — Tick *Record a video while playing* and a `.webm` of the animation downloads when the journey ends. Drop it into iMovie / Premiere / Canva for a quick reflection clip.

**Map export** — Click *Generate Map* to render a 2800×1700 bird's-eye illustration of your river with every milestone laid out as a connected badge, plus start/end sticky notes, a compass rose, sun, clouds, and trees. Download as a high-res PNG to print or post.

## Run it

No build step, no dependencies — just serve the folder and open it.

```bash
cd river-of-life
python3 -m http.server 8000
# open http://localhost:8000
```

Recording uses the `MediaRecorder` API and works in Chrome, Edge, and Firefox. Safari is fine for everything except the video export.

## How it works

Everything lives in one file: [`index.html`](index.html).

- **Setup screen** — vanilla DOM form with a milestone editor that reorders and seeds defaults.
- **Simulation** — a `<canvas>` with layered drawing: sky gradient + sun + drifting clouds, two layers of parallax hills, grassy bank, base water, three depths of scrolling `river_part.png` waves, the boat (bobbing + tilting), per-milestone cartoon scene elements, animated speech-bubble popups, and a progress bar with milestone markers.
- **Video** — `canvas.captureStream(30)` piped into a `MediaRecorder` with VP9 → VP8 → default fallback.
- **Map** — an off-DOM canvas that paints a parchment background, a meandering river path (sine-wave with 3 humps), milestone badges in alternating lanes with collision-avoidance, sticky notes, compass, and decorations. `canvas.toBlob` produces the PNG download.

## Assets

- `assets/boat.png` — hand-drawn cartoon boat (side view)
- `assets/river_part.png` — sketched blue wave pattern, tiled for the river surface

## The exercise

> The River of Life is a story of someone's life using the metaphor of a river. Imagine your life as a river that led you to this program.
>
> Where did it start? Where is it leading? How has your journey to this moment shaped your goals, values and dreams?
>
> What experiences, people, places, ideas, and events have been the most influential? Were there calm pools? Times when you were blocked by obstacles — trees, rocks, dams? Times when you slipped down a waterfall? Forks where you had to decide? Who is on the riverbank, watching the river drift by?

Works for any onboarding, retreat, classroom, or storytelling activity where you want to share your story visually instead of with a slide deck.
