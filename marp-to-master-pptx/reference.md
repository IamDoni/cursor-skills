# Marp → master PPTX — reference (WinPlace lab lessons)

Hard-won notes from converting `winplace_slides.md` + `seda_ppt_template.potx`
to PPTX for Mac PowerPoint (lab report, teacher requires native equations).

## Do not touch

For 黃雋凱: **never modify** `/Users/jyunkai/Downloads/revieiw/winplace_slides.pptx`
unless he explicitly asks. That path is his hand-maintained final.

## Failure timeline (what broke → what fixed it)

1. **Wrong fonts / title style** — Use Lucida Calligraphy `#002060` for content
   titles; Times New Roman for paper title + body. Title size **28**, body **20**.
2. **Images overlapping text** — Place images after measuring text; retire body
   placeholder; overlap checks.
3. **Tables full-column width** — User asked fit-to-text, no wrap. Size columns
   from cell string widths + pad.
4. **Equations blank on Mac** — Causes stacked:
   - Fancy Unicode alone without proper PPT wrappers
   - Malformed OMML (`m:box` / tag mismatch) — many slides failed XML parse
   - Bare `m:oMath` without **`a14:m`**
   - Only `m:rPr/a:rFonts` set → Mac still fell back to **Calibri**
   - Fix: `a14:m` + **`a:rPr` / `a:latin` Cambria Math** on every `m:r` + `ctrlPr`
5. **Italic TNR “fake” equations** — Teacher rejected. Always real OMML.
6. **Slide 67** — Must be master ending layout `1_標題及物件`, not a content
   “Thank You” title slide.
7. **Slide 66** — Five layouts in **one row** with captions under each (fig-row).
8. **Slides 59–61** — PDF is **1×4**, not 2×2. Never use `cols=2` for `n=4`.
9. **Slide 63 Ablation** — PDF is **2×4**, not 1×8.
10. **Eq-split slides** — PDF is two-column (eqs left, Symbol table right). Do not
    stack table under full-width equations. Affects e.g. 16, 18, 22, 25–27, 30,
    32–33, 35, 37, 40, 42, 46–48.

## User final vs agent draft (2026-09-20)

Compared read-only copy of user final vs last agent rebuild:

| Aspect | Agent draft | User final (prefer) |
|---|---|---|
| Slide count | 69 | **68** (dropped duplicate trailing appendix page) |
| Ending slide | `1_標題及物件` | Same |
| Symbol tables | Present on formulation slides | Same set of slides |
| Equation font markup | Cambria Math `a:rPr` | Same; **more** math-italic letters kept in `m:t` |
| `m:t` letters | Demathed to ASCII `H,V,E` | **Keep** Mathematical Alphanumeric / script forms when `a:rPr` is correct |
| Calibri in slide XML | 0 in slides | 0 in slides |
| Body TNR coverage | Present | Heavier / more consistent on runs |
| File size | ~4.4 MB | ~7.1 MB (re-saves / media) |
| Hand polish | Automated grid | Manual tweaks on some figures (e.g. empty leftover pics on one tree slide — avoid 0×0 pictures) |

**Target quality:** agent output should match user final structure and equation
behavior; drop the extra appendix page if Marp emits two nearly identical
appendix closers; keep eq-split and fig-grid faithful to PDF; do not demath
unless display fails.

## Implementation checklist

- [ ] Master layouts mapped (title / content / ending)
- [ ] Content title 28 Lucida Calligraphy `#002060`; body 20 TNR
- [ ] Every eq in `a14:m`; every `m:r` has Cambria Math `a:rPr`
- [ ] All slide XML parses
- [ ] fig-grid / fig-row cols match PDF (4→1×4, 8+4cols→2×4, 5→1×5)
- [ ] eq-split → two columns
- [ ] Tables fit-to-text
- [ ] Ending layout empty of fake Thank You placeholders
- [ ] Output path ≠ hand-maintained file unless user asked
- [ ] Spot-check Mac: formulas visible + font Cambria Math

## Tooling notes

- Python: `python-pptx`, `latex2mathml`, `mathml2omml`, `lxml`, Pillow (table width)
- Post-process zip XML after `prs.save` — python-pptx will not emit `a14:m` alone
- Optional: keep a `rebuild_pptx.py`-style builder next to the project; this skill
  is the **spec** the builder must obey
