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

**Step 1 · Tension → decoupled 3×3 menu board.** Read the full text, extract the core tension, and decouple **scene narrative, lens geometry, and color formula** into a **3×3 menu board** (with each category highlighting a `★ Recommended` pick):
1. **Visual tension (A / B / C)**: suspended disaster / absurd labor / chic dissonance (structured as `<absurd prop> + <facial expression> + <tension metaphor>`)
2. **Lens geometry (① / ② / ③)**: three contrasting lenses selected from the 6 physical optics profiles
3. **Color formula (Ⅰ / Ⅱ / Ⅲ)**: three distinct colorways drawn from the Top 8 solid sweeps and 5 clash formulas

The single 🔴 CHECKPOINT in between:
- **Express path**: Reply "default" or "ok" to compile directly with the three `★ Recommended` choices;
- **Custom remix**: Reply with a 3-character code (e.g., `B2Ⅱ`) or specify target aspect ratio (`2.35:1` / `16:9` / `3:4` / `1:1`).

**Step 2 · Compilation & deterministic self-correction gates.** Assemble the prompt along the five-layer skeleton (identity locking → lens geometry → prop deformation → specular material → lighting & clean backdrop invariant).
Before delivery, the prompt must pass **three deterministic self-correction gates**:
- **Limb boundary lock**: Explicitly declare crop boundaries or single-limb status for any partial anatomy to prevent models from generating extra deformed limbs;
- **Material-subject decoupling**: Adverbs and high-gloss textures stay strictly adjacent to target props, preventing global bleeding onto seamless paper sweeps;
- **Positive-only assertion**: Zero `no / without / avoid` exclusion phrases; all cleanliness requirements are unified into the positive seamless paper invariant.

Final delivery includes four items: full English prompt, three decisive optical mechanisms, one-line test prompt, and downstream safe-area guidelines.

## Example

Theme: "the to-do list never ends."

**Step 1 Generated 3×3 Menu Board**:

| Column | Option 1 | Option 2 | Option 3 |
| :--- | :--- | :--- | :--- |
| **Visual Tension** | **A. Suspended Disaster (★ Recommended)**<br>A to-do tower built from lemon jelly tips over, blank paper slips suspended inside (campy shock) | **B. Absurd Labor**<br>A chef stitches a single 1cm cherry tomato with surgical tweezers (deadpan) | **C. Chic Dissonance**<br>A mint-green resin pill larger than the marble tray it rests on (manic smile) |
| **Lens Profile** | **① 24mm Wide-Angle Micro-Distortion (★ Recommended)**<br>25cm distance, subtle barrel bulging to break personal space | **② 100mm 1:1 Macro Compression**<br>4cm distance, physical compression pressed against frame border | **③ 90° Overhead Flat-Lay**<br>Surgical geometric order and cold judgment |
| **Color Formula** | **Ⅰ. Formula 2 Warm Hard Clash (★ Recommended)**<br>Solar yellow `#FDCF00` against tomato red `#E4471D` | **Ⅱ. Solid Ice Cyan**<br>Classic `#DCF0F6` ice cyan paper sweep | **Ⅲ. Formula 5 Luminance Drop**<br>Solid black `#020202` with lit pale subject |

Selecting **`B2Ⅱ`** (Absurd Labor + Macro Compression + Ice Cyan Sweep) compiles into:

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
