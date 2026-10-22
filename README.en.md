# soft-toiletpaper

> An agent skill that turns the measured visual grammar of *TOILETPAPER* magazine into **word-free, high-contrast pop art** image prompts.

[中文](README.md) · [Install](#install) · [Workflow](#workflow) · [Scope](#scope) · [Data](#data)

Markdown-only agent skill. It reads an article, extracts the underlying tension, proposes three absurd-object scenes, and compiles one into a single-paragraph English prompt for FLUX / GPT Image / NanoBanana.

Everything it produces is a **pure visual plate** — no headline, masthead, stamp, tape label, or UI in frame. Typography belongs to a downstream cover skill.

## What makes it different from "make it pop art"

Three rules backed by measurements, not adjectives:

| Rule | Evidence |
| :--- | :--- |
| The seamless solid-color sweep is the main arena | Among 311 core magazine plates, saturated solid paper is **35.0%**; studio monochrome totals **39.5%**; chromatic preference inside that subset is **88.62%** |
| Backgrounds are a cyan/red double peak, not "some bright color" | Cyan **44.6%** + red **17.5%** ≈ 62%; top cluster is `#DCF0F6` ice cyan (41.0%) |
| Hard light means a steep edge, not "high contrast" | Shadow 10%→90% transition median **8.5 px** (P10 2.5 px) — nothing like a softbox falloff |

Two corollaries that are not negotiable:

- **Clash does not mean complementary.** Corpus hue-difference median is 114°; strong complements (ΔH ≥ 140°) are only **17.7%** of core plates. Warm analogous clash (ΔH ≈ 38°) and pure luminance drop (ΔL\* ≈ 46) are equally legitimate.
- **Describe only what is observable.** No color temperature, fixture model, camera position, or shadow angle — the source files carry no EXIF, and the old "45° shadow" was an artifact of a filter window.

## Install

```bash
git clone https://github.com/Joffoo/soft-toiletpaper.git \
  "<your skills dir>/soft-toiletpaper"
```

| Host | Skills directory |
| :--- | :--- |
| Claude Code | `~/.claude/skills/` |
| Codex | `~/.codex/skills/` |
| Gemini CLI | `~/.gemini/skills/` |
| Project-level | `<vault>/.agents/skills/` |

No dependencies. Copy and go.

## Workflow

Two steps, one checkpoint.

**Step 1 · Tension → scenes.** Read the full text, extract the core tension, then emit three absurd-object scenes as one line each:

```
<absurd prop> — <tension metaphor> — <facial expression> — <preset: formula # or solid # / lens # / aspect>
```

The three scenes take three distinct dramatic routes — suspended disaster, absurd labor, chic dissonance — and must not reuse a background color. The palette gets exercised during ideation, not after.

**Step 2 · Compile and deliver.** Five-layer assembly into one paragraph: lens and geometry → prop and physical deformation → material and specular → lighting and negative space. Deliver the prompt, three decisive optical mechanisms, a one-line test prompt, and downstream safe-area guidance.

The single 🔴 CHECKPOINT sits between the two steps.

## Example

Theme: "the to-do list never ends."

| | Scene | Preset |
| :--- | :--- | :--- |
| A | A to-do tower built from lemon jelly tips over, blank paper slips suspended inside | Formula 2 (`#FDCF00` + `#E4471D`) \| Lens 4 \| 3:4 |
| B | A chef stitches a single cherry tomato with surgical tweezers | Solid `#DCF0F6` \| Lens 2 \| 1:1 |
| C | A mint-green resin pill larger than the marble tray it rests on | Formula 5 (`#020202` + lit pale subject) \| Lens 3 \| 2.35:1 |

Compiled from B:

```text
extreme macro lens perspective focused at ultra-close 4cm distance, physical compression
with subject pressed hard against the frame boundary, visible dermal pressure blanching,
glistening specular micro-droplets, razor-sharp shallow focal plane with subject dominating
80% of canvas, clean background perimeter, stainless steel tweezers stitching a single
cherry tomato with translucent surgical thread, tomato skin denting under the tweezer tips,
cold porcelain enamel tray, small-source bare-bulb flash, razor-sharp contact drop shadow,
completely blank featureless seamless paper sweep in one flat solid saturated color (#DCF0F6),
uniform matte studio surface, razor-sharp clean silhouette contour with crisp edge separation,
cutout-ready high-contrast isolation, square 1:1 framing, bold centered pop composition,
uniform negative space all around
```

## Scope

- **Solid studio sweeps only.** 60.4% of core plates are real locations and sets; that branch is out of scope. Ask for it directly instead of forcing a paper backdrop.
- **Prompts only.** No image generation unless you explicitly ask.
- **No typography.** Headlines, mastheads, stamps and tape labels belong to a downstream cover skill.
- **No words in frame.** Typography never enters the prompt; blankness is claimed with positive spatial description, never with negative exclusions.

## Data

Measured on 3,440 images (311 core magazine plates): CIELab K-Means clustering plus physical optics quantification. `references/` is authoritative; the numbers above are a summary.

- **`references/color_palette.md`** — corpus topology, eight hue bands, Top 8 palette, five clash formulas, optical measurements, material lexicon
- **`references/lenses.md`** — six dramatic physical lenses with prompt snippets, to be used verbatim

Why there is no 5600K, no 24.91% highlight figure and no 45° shadow in this repo: all three were disproven on the full corpus. They survive only as errata, never as parameters.

## License

MIT © 2026 Joffoo
