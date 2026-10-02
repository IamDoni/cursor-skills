---
name: appendix
description: >-
  Creates or updates an Appendix section in a notes markdown file by
  comparing it with its source and listing content that exists only in the
  source. Use when the user says appendix, /appendix, leftover, remaining
  source, or wants unused source text collected at the end of the notes.
---
# Appendix

Compare the notes file with its source. Put **only-in-source** content into
an Appendix in the notes file.

## Files

Need the **notes** file (attached, `@path`, or the open notes file). Read
its first-line `Source:` link. If there is no notes file or no source link,
ask once.

Do not overwrite the source.

## Compare

Read the source and the notes.

List content that **exists in the source but not in the notes**.

Do not invent leftover. Skip ads, nav, and duplicate text. Do not quote
material already in the notes (including an existing Appendix).

## Write

Create or replace an `## Appendix` section at the **end** of the notes
file.

Put each leftover span in a quote block:

```markdown
## Appendix

> <remaining source text>
```

Several quotes are allowed, each in the Appendix. Do not scatter leftover
into earlier sections.

If nothing remains, say so in one chat line. Do not add an empty Appendix.

Match the language of the user's latest message. Keep source proper nouns.
Stay faithful. Do not silently rewrite quoted spans.

Chat: one short note naming the notes file.

## Example

User: `/appendix @winplace-notes.md`
→ Compare with the `Source:` file. Quote unused source spans under
`## Appendix` in `winplace-notes.md`.
