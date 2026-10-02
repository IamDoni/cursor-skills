# 講稿 rules — hand WinPlace oral style

講稿 inside `<!-- -->` only. Traditional Chinese. On-slide stays English.
No invented results. TTS-safe. Sound like a student presenting in lab meeting,
**not** like a textbook or a tour guide reading an outline.

## Calibration (from hand vs bad skill dump)

| | Hand | Avoid |
|---|---|---|
| Outline note | ~10–60 chars | 200+ char outline tour |
| Content note | often ~250–500+ chars | thin 2-line captions |
| Results / setup storytelling | can be long if teaching | skipping “what is OpenROAD/PPA” |
| Title slide | short greet + title + venue | announcing the whole agenda |

## Voice

- 口語: 那 / 所以 / 另外 / 總的來說 / 剛剛講到 / 我們知道…
- English EDA terms inside Chinese (macro, netlist, bounding box, HPWL…).
- Opening may use「從論文名字可以看出來…」.
- Bridge: 但是 / 因此 / 接著 / 那麼 / 除此之外 / 動機講完了…
- After split: continue; do not re-dump the previous slide.

## Outline / section-break slides

**Very short.** One or two sentences. Example:「我先講這篇論文的動機」.
Never re-read every outline item.

## Content slides

Denser teaching so you can speak without only reading bullets.
Explain intuition → then mechanism → then what the slide shows.
Still one idea per slide; same order as bullets.

## Figure slides (required behavior)

Must walk the image:
「我畫了投影片中的圖片…」「從左走到右」「左邊…右邊…」
「黃色區域是…」「綠色框是…」
Then land the claim. Do not ignore the figure.

## Formula slides

1. Plain-words idea first.
2. Walk symbols aloud to match the Symbol|Meaning table
   (「對一個 net e，M e 是…，A e tot 是…」).
3. Do not only say「看公式」.

## Results / setup slides

If a term is easy to misunderstand (PPA, OpenROAD, end-to-end), teach it in
講稿 the way hand slides do — what it is, why it is in the pipeline — without
inventing tool details the paper never states.

## TTS-safe always

- De-index: 投影片中的圖片/表格… — never Fig. N.
- Line-break by sentence; blank line between sub-points.
- Math in 講稿 = spoken words (小於等於、B 1 到 B n). `$$` stays on-slide.
- Delete [12]-style citations.
- Soften hype; attribute to 論文 when needed.

## Punctuation (strict)

ONLY ， 。 ？
Rephrase away () ： ； 「」 / - — … % ° and math symbols in the note.

## Case / numbers

Acronyms UPPERCASE. NP-hard → NP hard.
Quantity digits together; label digits spaced (B 1).

## Align

Same key points as English bullets, same order.
Figure walkthrough may add visual detail; no new scientific claims.
