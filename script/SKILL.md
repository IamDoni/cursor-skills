---
name: script
description: >
  Generate a Marp-ready Markdown slide deck (speaker-notes + images only) from a
  source Markdown paper, written as a TTS-friendly Traditional-Chinese presentation
  script. Use when the user invokes /script with a Markdown path, e.g.
  "/script @game_theory/Game_Theory_placement/auto/C_Game_Theory_placement.md"
  or "/script @paper.md focus on the methodology". The optional trailing text is a
  scope/emphasis hint.
allowed-tools: Read, Write
---

# script

Turn one source Markdown paper into a **Marp** slide deck whose content per slide is a
**speaker-note comment** (`<!-- ... -->`) plus, when relevant, the **images, formulas, and
tables** from the source that the narration on that slide explains. The notes are a spoken
Traditional-Chinese presentation script that will be **read aloud by a text-to-speech (TTS)
AI**, so the wording must obey strict TTS-safety rules below. The on-slide formulas and
tables are **visual aids** — they are shown on screen, while the note still speaks them in
TTS-safe words.

Do **exactly** the steps below and **nothing else** — no running the file, no summarizing,
no opening the result, no extra files.

## Input

The user supplies one Markdown path (e.g. `@dir/foo.md` or `dir/foo.md`), optionally
followed by free-text **scope/emphasis notes** (e.g. "多講 methodology", "只做到
experimental setup"). Let:
- `MD_DIR`  = the folder containing the Markdown file
- `MD_NAME` = the filename only, no directory (e.g. `foo.md`)
- `OUT`     = `MD_DIR/S_<MD_NAME>` (the original name with `S_` prepended, same folder)
- `SCOPE`   = the optional trailing text; if present, let it steer which parts get more
  detail or where to stop. If absent, cover the whole paper.

## Procedure

1. **Read** the entire source Markdown file. Note every `![](images/...)` link and what
   each figure/table depicts, and every formula (`$...$` / `$$...$$`) and Markdown table and
   what each one expresses.
2. **Reorganize** the paper's content into the fixed presentation outline (below),
   following **Knowledge order**.
3. **Write** `OUT` as a Marp deck: front-matter, then one `---`-separated slide per beat
   of the script, each slide containing the relevant visual aids (image(s), formula(s),
   and/or table(s)) when any, plus a `<!-- ... -->` speaker note written under the TTS rules.

If `OUT` already exists, overwrite it.

## Marp file format

Begin the file with this exact front-matter, then the slides:

```
---
marp: true
theme: default
paginate: true
math: katex
---
```

Each slide after the front-matter:
- Is separated from the next by a line containing only `---`.
- Contains, in this order, whichever **visual aids** that slide's narration explains —
  image line(s) `![](images/...)`, displayed formula(s) (`$$ ... $$`), and/or Markdown
  table(s) — followed by the speaker note as an HTML comment. A slide may carry any
  combination of these, or none (just the note).
- Has **no title, no headings, no bullet points, no body prose** — title/bullets are
  intentionally left empty. The formulas and tables are the only non-image visual content
  allowed, and they are placed as bare `$$...$$` blocks / Markdown tables, not under a
  heading or inside a sentence.

Example of one slide (image + formula + note):

```
![](images/afc43552a2ba58ce2d4295af484e29c0ccd2ca50c0503e95377be2ed317cc79a.jpg)

$$
Global\_cost(F) = \alpha L(F) + (1 - \alpha) A(F)
$$

<!--
這裡是這一頁要唸的講稿，每一句或每個語意段落換行，讓講稿比較好讀。

不同的小重點之間，用空行隔開。

接著用一個連接詞接回去，繼續往下講。
-->

---
```

(The note above shows the per-slide formatting rule — line breaks between sentences and a
blank line between sub-points — described in **Note formatting** below.)

Place each source image on the slide whose narration actually explains that figure.
Slides that have no natural figure (e.g. the opening, motivation) carry just the note.

**Formulas.** Put the source's significant formulas — especially displayed `$$ ... $$`
equations and the key defining equations — on the slide whose narration actually explains
that formula, copied **character-for-character** from the source as a bare `$$ ... $$`
block (the front-matter's `math: katex` renders them). Do not put every trivial inline
symbol on its own line; show the equations that the narration walks through. Crucially, the
on-slide formula does **not** change the note: the speaker note still describes that formula
in spoken, TTS-safe words per the math rules below (symbols never appear in the note). So the
formula is seen on screen and heard as words.

**Tables.** Put each source Markdown table on the slide whose narration explains it, copied
as-is using Markdown table syntax (keep its contents; do not redraw it as an image). As with
figures, de-index it in the note — refer to it deictically (「投影片中的表格…」), never by its
`Table N` number — and fold the table's point into the narration in TTS-safe words.

**Multi-image figures and uncaptioned images.** Before assigning images to slides, work
out which caption belongs to which image:
- A figure may be made of **several images that share one caption** (in the source the
  images sit next to each other and only one `Fig. N …` line follows them). Treat these as
  **one figure**: keep all of its images on the **same** slide, and fold that single caption
  into that slide's note. Do **not** split such images across slides — that orphans the
  images that have no caption of their own. A slide may therefore carry more than one
  `![](images/...)` line when they form one captioned figure.
- If an image genuinely has **no caption** anywhere in the source, do not invent one and do
  not leave the slide's note unrelated to it — describe it deictically from the surrounding
  body text (「投影片中的圖片…」) so the narration still matches what is on screen.

## Slide length — split and merge

Control how much narration lands on each slide by the **character count of its speaker note**
(count the spoken note text — Chinese characters, English words, and numbers; ignore the
`<!-- -->` markers, whitespace, and any on-slide image/formula/table lines).

- **Hard upper limit: 900 characters per slide.** If the narration you want on one slide
  would exceed **900** characters, **split it into two (or more) slides**, each within the
  limit. Break at a natural boundary (between sub-points, between steps, before a new figure)
  so each resulting slide is still one coherent beat, and carry an image/formula onto
  whichever slide actually discusses it.
- **Merge short same-topic slides: ≤ 600 characters combined.** If two adjacent slides cover
  the **same topic/beat** and their notes **combined are ≤ 600** characters, **merge them
  into one slide**. Only merge when the topic is genuinely the same — do not glue together
  unrelated beats just because they are short.
- **Worked example.** Explaining an algorithm's four steps: if all four steps together are
  ≤ 600 characters, narrate them on **one** slide; if covering them would push a slide over
  900 characters, **split** them across slides at a step boundary.
- Between 600 and 900 characters, leave the slide as it is — neither split nor merge.

## Presentation outline (fixed order)

Rearrange the source material into these sections, in this order. Use one or more slides
per section as needed:

1. **開場** — greet the audience, introduce the speaker by name, state the paper's title,
   and then explain in one or two plain sentences what the title tells us the paper is
   about. Frame this as something inferred from the title — open with a phrase like
   「從論文名字看出來，這篇論文…」 rather than 「這個題目的意思是…」. The speaker's name is
   unknown, so use the placeholder `大家好，我是 [請填入姓名]`.
2. **動機 (motivation)** — why this problem matters in the real world.
3. **想解決的問題 (problem formulation)** — the concrete problem, inputs and outputs, the
   objective being optimized.
4. **intuition** — the core idea / insight behind the paper's approach, in plain words.
5. **preliminary** — the background concepts the audience must understand before the method.
6. **methodology** — the theory of the paper's main method, in detail.
7. **implementation details** — practical/implementation tricks and small optimizations
   (e.g. training parameters, how training is done, candidate-selection tweaks in an FM
   algorithm, acceptance probabilities, schedules, etc.).
8. **experimental setup** — test-benches, parameters, baselines, how experiments were run.
9. **experimental result** — the findings and what they show.

If `SCOPE` asks to stop early or to expand a section, honour it. Otherwise keep every
section roughly proportional to the source.

## Knowledge order (always applied)

整個演講順序要注意知識的順序，不要一次講很多知識再分別述說，而是要先建立大觀念，然後每次挑其中的一個重點慢慢講深入進去。

This governs **how** the outline is filled, not whether the nine sections are used. Keep
those sections in the fixed order above, but inside each section:

- **One idea per beat.** Do not announce a list of contributions, constraints, graphs, or
  algorithm pieces and then explain them later. Name a piece only when the following slides
  will actually go into it.
- **Big picture first, then one deep dive.** Open a section with a short, plain map of what
  this part is for, in one or two sentences. Then pick **one** point and finish it before
  starting the next.
- **Introduce a tool only when it is about to be used.** Preliminary should teach only what
  the immediately following method beat needs. Delay matching, dual-graph details, layer
  assignment, and similar machinery until the methodology slide that actually uses them.
- **Roadmap figures stay light.** If a flow figure names several stages, say the map in one
  short beat and immediately dive into the first stage only. Do not recap every box on that
  same slide.

Worked anti-pattern: listing four contributions in the intro, then restating them in
methodology. Fold each contribution in at the slide that actually explains that idea.

Worked pattern: problem formulation states inputs, outputs, and the objective first; then
one constraint family per beat, such as design rules, then manual constraints, then
differential-pair wiring — not a seven-item dump.

## How to write the speaker notes

The note content **follows the source's meaning closely** — do not invent results and do
not heavily rewrite the argument. The job is to (a) make it sound spoken, (b) make it
TTS-safe, (c) de-index figures, (d) keep the whole deck flowing slide-to-slide, and (e)
format the note for readability. Five rule groups:

### 1. Make it conversational (de-formalize)

Loosen stiff, written-style phrasing and connectors into natural spoken Chinese, keeping
the meaning. Examples:
- 「這篇論文令 (0, 0) 為左下角」→「這篇論文把座標 0 0 定在左下角」
- 「形式上，此問題的一個實例由以下定義：一組 n 個待放置於晶片上的 block {B1,B2,…,Bn}」
  →「我用數學來定義這個問題，假設今天有一組 n 個待放置於晶片上的 block，標示為 B 1，
  B 2，一直到 B n」
- Drop bookish connectors like 「形式上」「具體而言」「儘管如此」when a spoken bridge
  («也就是說»、«換句話說»、«那») reads more naturally.
- **Replace literary / 書面 single words, not just connectors and sentence structure.**
  De-formalizing also means swapping out individual formal or 文言 vocabulary words for the
  everyday spoken word that means the same thing — this is the most commonly missed case, so
  check every word, not only the sentence shape. If a word is one you would write in a paper
  but would not actually say out loud when explaining to a friend, replace it. Examples:
  「指涉」→「指」或「提到」(e.g.「每當論文要指涉 block 中的某個位置時」→「每當論文要指 block
  中的某個位置時」);「旨在」→「目的是」;「藉由」→「透過」或「用」;「諸如」→「像是」;「乃至」
  →「甚至」;「闡述」→「說明」;「即」→「也就是」;「故」→「所以」;「其」→「它的」. When unsure
  whether a word is too 文言, assume it is and pick the plainer spoken word.
- **Make possessives explicit.** Whenever a noun belongs to someone or something other
  than the speaker («我»/«我們»), state the owner out loud — do not leave it implied.
  Most often the owner is the paper itself, so write 「這篇論文的…」. Examples:
  「我們先談動機」→「我們先談這篇論文的動機」;「接下來看方法」→「接下來看這篇論文的方法」.
  Only drop the owner when it genuinely belongs to the speaker (e.g. 「我先說明…」).
- **State the subject when it changes between clauses.** (Same spirit as the possessive
  rule.) When two adjacent clauses have different subjects, do not let the second clause
  silently inherit the first one's subject — name the new subject explicitly. Example:
  「VLSI 實體設計非常複雜，因此發展出一套設計流程」→「VLSI 實體設計非常複雜，因此，業界
  發展出一套設計流程」(the second clause's subject is 業界, not VLSI 實體設計, so it is
  written out).
- **Use the full noun, not a pronoun / short form / co-reference, when the link is weak.**
  A short reference (代名詞 like 它/這個, a 簡寫 like calling 組合最佳化問題 just 問題, or a
  bare 複指) is fine **only** when the listener just heard the full term and can effortlessly
  connect them. Before using any short reference, check the text **between** it and the full
  term it points back to. If **any** of these is true, write the full noun instead:
  - Another word that could also be called by that same short form appears in between (e.g.
    another thing that could be called 「問題」).
  - The topic changed in between.
  - It crosses a paragraph or **slide** boundary, or there is at least one full sentence in
    between.

  Examples — OK to abbreviate (same slide, immediately after, nothing in between):「論文把它
  描述成一個組合最佳化問題。問題裡的元件…」. Not OK (new slide, listener can no longer tell
  which 問題):「這個問題的一個實例，由兩個部分來定義」→「這個組合最佳化問題的一個實例，由
  兩個部分來定義」.

  **Trigger — how to *catch* a short reference in the first place.** The check above only
  helps if you notice the short reference, and the dangerous ones read as perfectly natural,
  grammatically complete Chinese, so they slip past. So mechanically flag, and run through
  the 3-condition check, **every** 「這個 / 那個 / 該 + 名詞」 (這個問題, 那個方法, 該演算法…)
  **and** every bare category noun used referentially (問題, 方法, 演算法, 階段, 模型, 函數,
  參數…). Do not assume 「這個問題」 is fine just because it sounds natural — it is a short
  reference. Whenever such a reference crosses a **slide boundary**, default to expanding it
  to the full noun (「這個問題」→「這個組合最佳化問題」) unless the full term was named on the
  very same slide just before it.
- **Tone down exaggerated modifiers.** Keep the original meaning, but soften hyperbolic
  or overly dramatic wording into a calmer, more understated phrasing. Examples:
  「是多麼地關鍵」→「是很關鍵的」;「極其龐大」→「相當大」;「完全無法」→「不容易」.
  Aim for a measured, matter-of-fact tone rather than emphatic exclamation.
- **Attribute subjective claims (be objective).** When the source states an opinion or
  value judgement as if it were fact — whether something is good, acceptable, sufficient,
  significant, etc. — do not assert it directly. Attribute it to the paper instead.
  Example:「這樣的結果是可以接受的」→「論文認為這樣的結果是可以接受的」. Use openers like
  「論文認為…」「作者主張…」「論文指出…」so the judgement is presented as the paper's view.

### 2. Make it TTS-safe (this is the strict part)

The TTS voice has four hard quirks. Write so it never trips on them:

**(a) Punctuation.** The ONLY punctuation the voice handles correctly is the **comma
(，)**, **period (。)**, and **question mark (？)**. Every other mark causes errors and
must be removed or rephrased away — including:
parentheses `（）()`, colon `：:`, semicolon `；;`, brackets `【】[]`, quotes `「」『』""`,
slash `/`, hyphen/dash `-—`, ellipsis `…`, percent `%`, degree `°`, and all math symbols.
- Parenthetical asides → fold into the sentence with a comma or with 「也就是」.
- Slash like 「Gate array / FPGA」→「Gate array 或 FPGA」.
- Citation markers like `[13]`, `[20, 23]` → **delete entirely** (never spoken).

**(b) English letter case.** Uppercase English is read letter-by-letter; lowercase English
is pronounced as a word.
- Keep **acronyms uppercase** so they are spelled out correctly: VLSI, FPGA, IC, SA, BRD,
  NE, GLS, FLS, etc. — this is desired.
- Write `NP-hard` as `NP hard` (no hyphen): `NP` spelled, `hard` spoken.
- Keep ordinary technical terms in **lowercase** so they are pronounced as words
  (placement, swap, block, cooperative). Do not uppercase them.
- For a mixed-case proper noun the voice should say as a word (e.g. Nash, Metropolis),
  keep normal capitalization.
- **Do not translate EDA / physical-design vocabulary into Chinese — keep the English.**
  This applies not only to named proper nouns but also to the everyday domain vocabulary of
  EDA and VLSI physical design. These terms read more naturally to the audience in English,
  so leave them in their original English form (lowercase, as above) rather than translating.
  Examples of terms to keep in English: `critical path` (不要寫「關鍵路徑」), `placement`
  (不要寫「擺放」), `routability` (不要寫「繞線性」), `wire` (不要寫「導線」), `buffer`
  (不要寫「緩衝器」), `bounding box` (不要寫「邊界框」), `die` (不要寫「晶粒」), `congestion`
  (不要寫「壅塞」), `overlap` (不要寫「重疊」), `routing`, `floorplan`, `netlist`, `net`,
  `wirelength`, `layer`, `timing`, `slack`, `cell`, `pin`, `macro`, etc.
- **This rule is strong, and it catches plain everyday words too — not just the obvious
  jargon.** The most commonly missed case is a short, ordinary-looking word that you would
  naturally translate on autopilot because a perfectly good Chinese word exists — e.g. `wire`
  → 導線, `buffer` → 緩衝器, `net` → 網路, `layer` → 層, `overlap` → 重疊. **Do not** translate
  these; keep the English. Whenever the source's Chinese word denotes an EDA / physical-design
  concept, replace it back with its standard English term. The bar is: if it is a concept an
  EDA engineer would normally say in English, write the English word, even if it looks mundane
  and even if the source markdown already gave it in Chinese. When in doubt, keep English.
- **Also keep algorithm & data-structure vocabulary in English — do not translate.** The
  same rule extends to the everyday vocabulary of algorithms and data structures: keep terms
  like `cost` (不要寫「成本」), `cost function` (不要寫「成本函數」), `stack` (不要寫「堆疊」),
  `queue` (不要寫「佇列」), `heap` (不要寫「堆積」), `tree` (不要寫「樹」), `node`
  (不要寫「節點」), `edge`, `array`, `hash`, `pointer`, `graph`, `search space`,
  `local search`, `local minimum` / `local minima`, `greedy`, `heuristic`, `recursion`,
  `swap`, `complexity`, etc. in English (lowercase, so the voice says them as words). As with
  the EDA terms, this catches plain everyday words with a perfectly good Chinese equivalent
  (`cost`→成本, `stack`→堆疊, `node`→節點) — keep the English anyway. When in doubt, keep
  English.

**(c) Math → plain words.** Replace every formula, symbol, subscript, superscript and
operator with spoken Chinese plus only safe punctuation. Reference table:

| source | spoken |
|---|---|
| `$1 \leq i \leq n$` | i 大於等於 1，小於等於 n |
| `$\leq$ / $\geq$` | 小於等於 / 大於等於 |
| `$<$ / $>$` | 小於 / 大於 |
| `$=$ / $\neq$` | 等於 / 不等於 |
| `$+$ / `−` / `$\times$` / `$/$`(除)` | 加 / 減 / 乘以 / 除以 |
| `$B_1, B_2, \ldots, B_n$` | B 1，B 2，一直到 B n |
| `$T_n^c$` | T 上標 c 下標 n（用文字描述，不要符號） |
| `$\alpha$ / $\beta$` | alpha / beta（小寫，當作單字唸） |
| `$\alpha = 0.9$` | alpha 等於 零點九 |
| `$L(F)$` | 描述成文字，例如「擺放 F 的總導線長度」，不要用括號 |
| `90°` / `$2 \times 2$` | 九十度 / 二乘以二 |
| `$x^2$` | x 平方 |
| 數字小數 `0.3` | 零點三 |

Always express a formula by **what it means in words**, not by transliterating symbols.

**(d) Numbers — choose the reading via digit spacing, you need not spell them in Chinese.**
The voice reads **consecutive digits as one whole number** (`256` → 「兩百五十六」) and
**space-separated digits one at a time** (`2 5 6` → 「二五六」). So you do **not** have to
convert numbers into Chinese characters at all — keep the Arabic digits, but decide which
reading is intended and **format the spacing to force it**:
- **Read as a whole quantity → keep the digits together.** Use this for any real value,
  count, size, measurement, or coefficient: `40` 個 block, 快 `5` 倍, `30` 到 `80` 像素,
  alpha 等於 `0.9`, 旋轉 `180` 度. (Writing `0.9` is fine; you don't need 「零點九」.)
- **Read digit-by-digit → put a space between each digit.** Use this when the number is an
  identifier, index, or label that is spoken as a string of separate digits rather than a
  magnitude — e.g. a subscript index `B_1` → `B 1`, or a coordinate origin said as separate
  digits `(0,0)` → 「座標 0 0」.
- The Chinese spellings in the table above (「零點九」「九十度」) still read correctly, so they
  remain acceptable; this rule simply means correctly-spaced **digits are an equally valid
  choice**, and the real job is to **judge the intended reading and match the format to it**.
- Whichever form you pick, the surrounding punctuation rules still apply (no `%`, `°`, etc.).

### 3. De-index figures and tables, but **fold the caption's description in**

Two separate things. **(i)** Strip the figure/table **number and label** — the audience
just sees the current slide's image, so refer to it deictically:
- 「Fig. 3 導線長度計算的範例」→「投影片中的圖片為導線長度計算的範例」
- 「如圖 4 所示」→「如同投影片中的圖片所示」
- 「Table 2 ...」→「投影片中的表格為 ...」
- Never say a figure or table number out loud.

**(ii)** Keep the caption's **descriptive content** — do not throw it away. The source
caption usually explains what the image actually shows, and that explanation is exactly
what the narration needs. So **weave the caption's description into the narration of the
slide that carries that image**, merged smoothly with the body text — not dropped in as a
separate sentence and not omitted. A common, natural shape is
「投影片中的圖片…。可以看到，<caption 的內容融進來>。<接回內文>」.

**Fold the caption in right where the figure is introduced.** The body text usually has a
sentence that points at the figure (e.g. 「如圖 2 所示，…」). De-index that sentence to
「投影片中的圖片…」 and fold the caption's description in **at that same sentence, on that
same slide** — do not let the figure's introducing sentence land on one slide while the
caption description ends up on another. The image, its introducing sentence, and its
caption description must all live on one slide and read as one continuous thought.
- Worked example. Body text:「…而讓晶片根本沒辦法製造。」, and the image's source caption is
  「良好擺放（左）與不良擺放（右）的範例。在良好的擺放中，導線較短且幾乎沒有壅塞。在此範例中，
  兩種擺放的面積是相同的」. Fold them together →「…而讓晶片根本沒辦法製造。投影片中的圖片呈現
  了一個 placement 的範例。可以看到，在此範例中，兩種擺放的面積是相同的，但良好的擺放，能讓
  導線較短，而且幾乎沒有 congestion。而實際上，好的 placement，其實是在同時最佳化好幾個目標
  …」. (The caption's facts are spoken; only the 「Fig. N」 label is dropped.)
- The caption content must still obey every other rule above (TTS-safe punctuation, keep
  EDA terms in English such as congestion, de-formalize, etc.).

### 4. Connect slide to slide (承先啟後)

The deck is read aloud as one continuous talk, so the notes must flow in meaning **and**
tone across the `---` slide breaks — never read like a list of disconnected paragraphs.
As you write each slide's note, look back at how the **previous** slide ended and open the
**current** slide so it follows on naturally.

- Open a slide with a **transition connector** that links it to the previous slide's idea,
  instead of starting cold. Use connectors and safe punctuation (only «，»「。」「？」) to
  carry the tone forward — e.g. 「但是，…」「因此，…」「也正因為這樣，…」「那麼，…」
  「除此之外，…」「回到剛剛提到的…」.
- Choose the connector to match the logical relation to the previous slide: contrast
  («但是»、«然而»), consequence («因此»、«所以»), continuation («接著»、«另外»),
  elaboration («也就是說»、«具體來說»).
- Example — previous slide ends 「…對於在很小的面積上容納眾多元件，是很關鍵的。」, next
  slide should not start cold with 「VLSI 實體設計非常複雜，因此發展出一套設計流程…」 but
  rather 「但是，VLSI 實體設計非常複雜，因此，業界發展出一套設計流程…」.
- The opening slide (開場) has nothing before it, so it needs no back-reference; every
  later slide should.

### 5. Note formatting — line breaks

The note is still spoken aloud, so this group is about how the note **text** is laid out, not
about new wording.

- **Break the note into lines for readability.** Do not write a slide's note as one long
  unbroken line. Put a line break at sentence ends and at natural clause boundaries so the
  note reads as a short, scannable block. Separate distinct sub-points with a blank line.

## Done

Report the path of the created file (`OUT`) and stop. Do not do anything beyond these steps.
