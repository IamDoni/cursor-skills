---
name: marp-to-master-pptx
description: >-
  Turn Marp markdown + a lab slide master (.potx) into a Mac-ready PPTX.
  Use for Marp→PPTX, seda/lab master, or when layout must follow the Marp PDF.
---

# Marp → master PPTX

Build one PPTX from Marp `.md` + master `.potx` (+ images, optional PDF).
Ask once if md / master / **output path** is missing.

**Never overwrite** a hand-maintained file (e.g. `Downloads/revieiw/winplace_slides.pptx`)
unless the user explicitly names it as the output.

## Specs (lab default)

| Part | Rule |
|---|---|
| Layout truth | Marp **PDF** structure (grids, eq-split), not HTML chrome |
| Slide 1 | Layout `標題投影片`; paper title Times New Roman ~28 |
| Content | Layout `標題及物件`; title Lucida Calligraphy **28** `#002060`; body TNR |
| Body floors | **L0 = 20pt**, **L1 (tab) = 18pt**, L2 ~16 — **never shrink below** |
| Bullets | On `標題及物件`, bullets live in content PH **idx=1** (master glyphs) |
| Equations | No mid-formula wrap; wide eqs get enough width; no text↔eq overlap |
| Ending / Thank You | Layout `1_標題及物件` only — do **not** fill title/body text |
| Tables | Fit column width to text (no wrap); TNR ~13 |
| Notes | `<!-- … -->` → speaker notes |

## Layout from Marp

- `.fig-grid` + `N` columns → **N** cols (`n=4` ⇒ **1×4**, not 2×2; `n=8`+4cols ⇒ **2×4`)
- `.fig-row` → one row; captions under images when present; honor width %
- `.eq-split` → **two columns**: left eqs/bullets/image, right Symbol table
- Prefer taller PH / tighter spacing over font shrink when content is dense
- Drop a duplicate trailing appendix page if the md emits two near-identical closers

## Equations (Mac)

Native OMML only — no italic `a:t` fakes, no formula PNGs.

1. Wrap in **`a14:m`** (display: `oMathPara`; inline: `oMath`).
2. Slide: `xmlns:a14` `xmlns:m` `xmlns:mc` + `mc:Ignorable="a14"`.
3. Every `m:r`: Cambria Math via **`a:rPr`/`a:latin`** (and `ctrlPr`).
4. Keep math-italic letters in `m:t`. Demath to ASCII only if still blank after (3).
5. Math-only boxes: `word_wrap=False`; promote wide one-liners above two-col region.

## Steps

1. Work on a copy; open master; parse md slides.
2. Place title / body / eqs / tables / images per specs (bullets → content PH first).
3. Post-process XML (`a14:m`, Cambria Math `a:rPr`); parse-check all slides.
4. **QA loop (required)** — whole deck, every content slide:
   - (a) any body L0 run <20 or L1 <18 → fail
   - (b) `標題及物件` with bullets only in a free TextBox while content PH empty/retired → fail
   - (c) eq-split / two-col text↔eq overlap heuristic → fail
   - (d) known fig-grid counts when applicable → fail
   - If any fail → fix builder / layout, rebuild, re-check; repeat until clean or list unblockable slide numbers.
5. Write only to the **named** output path.

## Done

Mac PowerPoint: formulas visible/editable (Cambria Math); L0/L1 floors hold on **all** pages; grids/eq-split match PDF; ending uses master art; hand file untouched.
