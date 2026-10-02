---
name: contract
description: >-
  Contracts the exact word or sentence the user points to. Keeps the most
  important concept for that paragraph's purpose. Does not use harder words
  just to reduce length. Use when the user says contract, tighten, shorten,
  cut redundancy, or wants a padded part said in fewer words.
---

# Contract

Contract only the mentioned span. Keep its most important concept for
that part's purpose in the file. Do not use a harder word just to shorten.
Do not add ideas or change that meaning.

If the target is in a file (selection, `@path`, or a quoted span), edit
that file now. Chat-only quote → do not create a file.

## Target

The smallest thing pointed at: a selection, a quote, one sentence, or one
word in that sentence. Do not contract the rest. Read nearby lines for
purpose (section title, why this span is here).

## How

1. Name the purpose (contrast, method step, limit, baseline, claim).
2. Keep only the concept that serves that purpose. Names, citations, extra
   methods, and other details may go if they are not that concept.
3. Cut filler and restatement. Repeated similar sentences → keep once.
4. Same everyday words. A slightly longer easy sentence is better than a
   short hard one.

- Word: shorter stand-in, or `drop` if filler. Do not explain (`expand`).
- Sentence: that sentence only. Do not merge later paragraphs.
- Everyday English (TOEFL iBT 72). Traditional Chinese gloss only for a
  hard leftover word.

This skill overrides short-reply rules for the contraction itself.

## Reply

One short restatement of the ask, then only:

```markdown
**Target:** "<exact word or sentence>"
**Purpose:** <why this span is in the file, in one short line>
**Contracted:** <shorter version, or `drop` if filler>
**Cut:** <what did not serve the purpose, in one short line>
```

No extra sections. File target → this shape after the file already has
the contracted span.
