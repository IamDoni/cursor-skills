---
name: illustrate
description: >-
  Adds a schematic example figure under the mentioned paragraph. Use when the
  user says illustrate, add a figure, add a picture, 加图片, 示例图片, or attaches a
  span and wants an example image below it.
---

# Illustrate

Turn the **mentioned** span into one schematic example figure. Put the figure
**under that span**. Do not rewrite the span except a short figure cite.

## Find the target

Same targeting as `expand`:

| User points at | Illustrate this |
|---|---|
| A sentence or paragraph in a file | That span |
| A selection or quote | That quote |
| No file | The mentioned sentence in the chat |

Do not illustrate the rest of the file.

Read nearby lines only for meaning. Stay faithful: the figure may only show
claims the target already makes. No extra methods, metrics, or results.

## What to draw

One idea, easy to read at a glance:

- Prefer a **2-panel contrast** when the text compares two cases (random vs
  prior, before vs after, source vs target).
- Prefer **3 panels** for a time path (`t=0`, mid, `t=1`).
- Label panels `(a)`, `(b)`, `(c)`. Short titles. Little text.
- Paper look: white background, equal-aspect canvases, colorblind-friendly
  colors, no 3D, no photorealism, no decorative clutter.
- Everyday labels. No Traditional Chinese inside a paper file.

## How to generate

Prefer **matplotlib** for paper schematics (placement canvases, particles,
arrows, masks). Use GenerateImage only if the figure is not a diagram.

Save to `<markdown-dir>/images/<short-slug>.png`. Create `images/` if needed.

Python: try `python3` with numpy+matplotlib; if missing, use
`~/miniconda3/envs/ml_eda/bin/python`. `dpi=200`, `bbox_inches="tight"`.

Look at the saved PNG. If labels collide or the idea is unclear, fix and
re-save once.

## Where to insert (file target)

Insert **immediately after** the target span, still in that file:

```markdown
![](images/<short-slug>.png)
Figure N. <one-line caption that matches the target>.
```

- Keep the original paragraph. Do not replace it with the figure.
- If the document already numbers figures, this new one is the next number
  **at this location**. Bump later figure numbers (highest first, e.g. 5→6
  then 4→5) and in-text cites.
- Add one short cite in the target span if it has none, e.g. `Figure N
  illustrates this.`
- Match nearby caption voice (paper prose in a paper).

## Chat target

No file edit. Generate the figure and show:

```markdown
**Target:** "<exact span>"
**Figure:** <one-line caption>
```

## Reply (file target)

One short corrected restatement of the user's ask, then one line: which
figure number, which file, what the panels show.

## Examples

**Paragraph in a paper**
User attaches the boundary-bias paragraph.
→ Draw random vs boundary-biased macros. Insert under that paragraph.
Renumber later figures.

**Chat only**
User types: illustrate "particles flow from noise to two moons"
→ No file. Draw the three-time schematic in chat.
