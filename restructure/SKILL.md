---
name: restructure
description: >-
  Copy one file, then rewrite the copy as textbook teaching prose: one new
  idea per beat, everyday object before coined name, ≤1 hard term per
  paragraph; put each figure at its teaching-home. Never edit the original.
  Use for restructure, reorder, delete redundant, teach first, just-in-time,
  or sequence so A is clear before B.
---
# Restructure

**Never edit the original.** Copy first, then rewrite only the copy.

1. Target = attached / `@path` / focused file. No file → ask which; do not invent one.
2. `OUT = same-dir/R_<original-filename>` (keep extension). If `OUT` exists, overwrite the copy only.
3. Copy original → `OUT`, then run the pipeline on `OUT`.
4. Leave the original bytes unchanged.

Meaning unchanged. Voice: patient textbook. Each sentence earns the next.

## Pipeline (only this order)

1. **Atomize** — one claim / step / definition per beat.
2. **Dedupe** — explain each idea once; later = short recall only.
3. **Order** (tie-break): causality → knowledge (object before name) → coarse-to-fine.
4. **House** — new purpose headings; nest; drop stock titles (`緒論`, `相關工作`,
   `Introduction`, …) and hollow skeletons. Arc: known picture → felt problem →
   one hard name → next dependency → use/limits.
5. **Figures** — move each figure to its own section; unit =
   setup → figure+caption → read-out. Just-in-time; never a pile at top/end;
   caption adds no extra hard-name dump.
6. **Polish** — ≤1 new coined name per paragraph; keep eq+symbols together;
   delete "see Section N" leftovers.
7. **Test** — term before picture, two hard names in one paragraph, section k
   not preparing k+1, or figure before its setup → fix.

## Homes

No topic jumping: do not define C inside B. Opening = problem only.

## Example

Bad: `視窗化初始化先掃描序佇列…`
Good: order queue → window → windowed init.

## Reply

Report `OUT` path. What moved, what you cut, where figures went, new arc — one short note.
