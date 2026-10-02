---
name: keynote
description: >-
  Creates a new markdown notes file that starts with a source link and
  pastes only the key point of a source. Use when the user says keynote,
  /keynote, teach, /teach, learn, study, 教我, or 學習, or wants notes that
  begin from a paper, website, file, or other source.
---
# Keynote

Make **one new** markdown file from a source. Paste only the **key point**.
Do not overwrite the source. Do not dump the lesson in chat.

## Source

Need a **source**: `@path`, URL, PDF/markdown, or pasted text. If none, ask
once.

Put a **source link on the first line** of the new file:

- File: `Source: [@path](path)`
- URL: `Source: <url>`

## File

- Next to the source if the source is a file.
- Else in the folder the user named, or the workspace root.
- Name: short topic slug, e.g. `winplace-notes.md`.

On the first turn only:

1. Read the source (fetch a URL if needed).
2. Write the source link, then paste **one portion**: the key point of the
   source, not the whole source.
3. Stop.

Match the language of the user's latest message. Keep source proper nouns.
Stay faithful when pasting. Do not silently rewrite pasted spans.

Chat: one short note naming the notes file.

## Example

User: `/keynote @paper.md`
→ Create `paper-notes.md` that starts with `Source: [@paper.md](paper.md)`
and the key point only.
