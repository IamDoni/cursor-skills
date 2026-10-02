# group_meeting — slide body (hand WinPlace style)

Gold: hand `winplace_slides.md` (not the verbose skill dump).
theme: default. No seda. No `_class`. One `M_` file.

## Front-matter

```
---
marp: true
theme: default
paginate: true
math: katex
---
```

## Section flow

opening → Motivation → Problem Formulation → Preliminary → Methodology
→ Experimental Setup → Experimental Results → Thank You.
Insert `# Outline` between major parts. Honour SCOPE; skip unused parts.

## Titles (hard rule)

Short **section names**, reused for every slide in that section
(`Motivation`, `Problem Formulation`, `Windowed Order Diversification`, …).
Typical title length ~1–4 words.

**Forbidden:** a new long claim-sentence as `# Title` on every slide
(e.g. “Sequential construction claims the canvas early”).
Claims go in bullets / 講稿 only.

## Opening slide

Bullets like:
- **Anonymous Author(s)** (or real authors)
- **From:** venue, year
- **Speaker:** 黃雋凱
- **Date:** …

講稿: greet + title + venue; may say「從論文名字可以看出來…」. No method punchline.

## Outline slides

Only section-name bullets; **bold** the current section.
講稿: **1–2 short lines** only (「我先講動機」「動機講完了。接下來講問題定義。」).
Do not narrate the whole outline.

## Bullets (sparse)

- Unordered `-` only. Nest rarely (Input/Output/Goal).
- Target **~1–3 bullets** per content slide (hand avg ~2.6). Not a paragraph farm.
- Complete English sentences; ~12–18 words; bold the key phrase.
- Same section may use **numbered** steps only when the paper is literally a
  pipeline sketch (e.g. Intuition 1/2/3) — default still `-`.
- Every 講稿 key point needs a matching bullet **or** is figure narration
  (figure slides may have 0–1 bullets).

## Figures (hand uses many)

- Include paper/note figures that teach the beat (~30–40% of slides often have one).
- Order: title → bullets → formula/table → **figure** → `<!-- 講稿 -->` (never figure at top).
- Size: `![h:300px](…)` / `![h:480px](…)` / `![w:720](…)` so it fits.
- Figure-led slide: 0–2 bullets + large image; 講稿 walks 左/右/顏色/框.

## Formulas + symbol table

When formulas appear:
1. 1–2 lead-in bullets.
2. Put **related** equations on the **same** slide when they are one idea
   (hand packs 2–3 eqs together). Do not over-split one idea across slides.
3. Symbol | Meaning for every on-slide symbol.
4. Use **eq-split** (formula left, table right) — copy this pattern:

```
<style scoped>
.eq-split { display: flex; align-items: flex-start; gap: 1.2em; }
.eq-split > div:first-child { flex: 1.15; }
.eq-split > div:last-child { flex: 1; }
.eq-split table { font-size: 0.7em; width: auto; }
</style>

<div class="eq-split">
<div>

$$ ... $$

</div>
<div>

| Symbol | Meaning |
| --- | --- |
| ... | ... |

</div>
</div>
```

## Overflow / split / merge

- Prefer **split slides** over deleting meaning.
- Crowded figure/formula page → fewer bullets on that page; continue next slide
  under the **same section title**.
- Do not invent a new claim-title when continuing.
- Flexible mix; continuity required (next slide continues, does not restart).

## Closing

`# Thank You` + one line. 講稿:「我的報告到這裡，謝謝各位。」
