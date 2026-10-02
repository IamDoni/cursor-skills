---
name: group_meeting
description: >-
  Build one final Marp deck M_<name>.md for a group-meeting paper talk from a
  source Markdown. Match hand-slide style: short section titles, sparse English
  bullets, paper figures, eq-split symbol tables, dense oral 中文講稿. Use for
  /group_meeting.
---
# group_meeting

One output: `OUT = MD_DIR/M_<MD_NAME>`. No `S_` file. Overwrite OK.
No GOAL ask. Optional SCOPE in the prompt. Cover the whole paper if no SCOPE.

## Input

Source Markdown (+ figures). Optional SCOPE.
On-slide: English. 講稿: Traditional Chinese.
Speaker: 黃雋凱 (Jyun-kai).

## Before writing

Read beside this file:
1. `outline-and-notes.md` — slide structure (learn from hand WinPlace)
2. `tts-rules.md` — 講稿 voice
3. `refine.md` — second pass

## Run

1. Read source; index figures+captions, formulas, tables.
2. Write OUT per outline-and-notes.md + tts-rules.md (one pass).
3. Refine OUT in place per refine.md.
4. Report OUT. Stop.
