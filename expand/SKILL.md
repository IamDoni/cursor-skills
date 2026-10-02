---
name: expand
description: >-
  Answers the user's question about a pointed word or sentence by expanding
  it in the notes file. Source is only a reference; never paste source text
  without modification. Use when the user says expand, asks to unpack a hard
  sentence or word, asks what a word means here, search for what, or wants
  a difficult part explained in easier words.
---
# Expand

The main goal is to answer my question or do the things i asked.

instead of trying to paste from target.

paste without any modification is not allowed.

source is just where you can refer to.

Expand only the **mentioned** span **in the file**. Chat: one line after
the edit. Do not dump the expansion in chat.

## Target

The smallest thing pointed at: a selection, a quoted span, one sentence, or
one word in that sentence. Search the open, recently viewed, or `@` file.
No matching file → chat-only; do not create a file.

## Write

Read `Source:` if the notes file has one. Use it only to answer the question.

Write new sentences: what it means here, why it is there, how the pieces
connect. Short everyday sentences (TOEFL iBT 72). A word → that word in this
sentence. A sentence → that sentence only. No new claims.

Put the expansion next to the target:

```markdown
> **thought by you:** <span style="color:red"><the expansion></span>
```

## Reply

File edit: one short restatement, then which span and file.

No file:

```markdown
**Target:** "<exact word or sentence>"
**In simple words:** <span style="color:red"><plain meaning></span>
**Deeper:** <span style="color:red"><why it matters here></span>
```
