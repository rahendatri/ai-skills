---
name: grounded-market-research
description: Conduct deep, multi-source market research and produce a fully source-grounded Markdown, HTML, or slide-deck report where every claim traces back to the exact excerpt and source it came from. Use whenever the user asks for market research, industry/sector analysis, competitive landscape, market sizing (TAM/SAM/SOM), trend analysis, or a research deliverable that needs to be verifiable and traceable to primary sources — even without the words "market research" (e.g. "what's happening in the EV battery space", "how big is the market for X", "who are the competitors in Y", "give me a sourced overview of Z", "turn this into a 5-slide deck for the exec team"). Also covers producing a companion strategy-consulting-style slide deck (max 5 slides, action titles, keyboard-navigable HTML) summarizing a market. Prefer this over ad hoc web searches whenever the user needs a structured, citable deliverable rather than a quick conversational answer.
---

# Grounded Market Research

## Why this skill exists

Market research is only useful if the reader can trust it — and trust comes from being able to check, in seconds, exactly where a claim came from. A report that says "the market is growing 12% annually" with no way to verify it is not much better than a guess. The goal of this skill is to produce research where **every non-obvious claim is traceable to a specific chunk of a specific source**, so the reader never has to take Claude's word for it.

This means two things have to happen together: (1) genuinely deep, multi-source research, and (2) a citation system that survives contact with a skeptical reader — one where clicking a citation actually gets you to the source it was grounded on, not just to a homepage.

**Default reader: someone with five minutes, not fifty.** Unless told otherwise, write for a time-constrained decision-maker who is scanning for a pattern worth acting on, not reading start to finish. This has concrete consequences beyond just "keep it short": the single most important number or pattern in each section should be visually findable without reading the prose around it — pull headline figures out into something scannable (a stat callout, a bolded metric table) rather than burying them in paragraphs, and let a skim of just the bolded terms and pulled-out numbers tell most of the story. Full sentences are still there for whoever wants the detail and the citation trail, but nobody should have to read a paragraph to find the number in it.

## Workflow

### Step 1 — Scope the research

Before searching, nail down what "done" looks like. Check the user's initial prompt against the four scoping elements below. For any element the prompt doesn't already answer, ask about it — if none of the four are answered, ask all four; if the prompt already covers an element clearly, don't ask about it again. Use an elicitation/multiple-choice tool if one is available so the user can tap rather than type; otherwise ask inline in chat.

The four scoping elements:

1. **Subject and boundaries** — a description of the sector, type of activity, and geographical operations to research. This has to be specific enough to search effectively, not just non-empty. "EV industry in France" is specific enough to start from. "Automotive trends in France" is too broad — push back or narrow it (e.g. which vehicle segment, and which part of the value chain: manufacturing, sales, charging infrastructure, financing?).
2. **Language of research** — which language(s) sources should be searched in and the report should be written in. Don't assume the conversation's language is the intended research language (e.g. a request in English about a French market may still want French-language sources or a French-language report) — ask rather than guess.
3. **Depth** — a quick sourced briefing, or an exhaustive report? This determines how many searches to run (see `references/search-strategy.md` for how to scale search volume to scope).
4. **Time window** — a timeframe for the snapshot, or a date range of data to take into account (e.g. "Q1 2024 – Q3 2025").

**Final question — confirm understanding.** This isn't a fifth scoping element — it's a separate, always-asked step. After the four elements above are settled (whether from the initial prompt, from answers just given, or a mix of both), ask one last confirmation question before starting the research. State your understanding of each of the four elements as a short labeled list — one line per element, in the same 1–4 order above, so the user can immediately see which line answers which element and correct just that one if needed — then ask the user to confirm or correct it. For example:

> Before I start, here's what I've got:
> 1. **Subject & boundaries**: EV industry in France (passenger vehicles, sales + charging infrastructure)
> 2. **Language**: French sources, report written in English
> 3. **Depth**: standard report
> 4. **Time window**: 2020 – 2026
>
> Does that match what you're after, or should I adjust anything?

Don't begin Step 2 until the user confirms or corrects this summary.

### Step 2 — Gather sources and capture the grounding chunk as you go

Use `references/search-strategy.md` to decide how many searches to run and how to spread them across categories. Cover, as relevant: market size/forecast reports, industry associations, company filings/earnings calls, trade press, analyst notes, and recent news. Favor primary and original sources (company filings, government/statistical agency data, original research firms) over aggregators, and prioritize recent sources for anything fast-moving.

**The critical discipline**: the moment you find a fact worth using, capture these together, not just the fact:
1. The claim, in your own words
2. The specific short excerpt (verbatim, under 15 words) or precise data point that grounds it
3. The source's title, publisher, URL, and date
4. Where in the source it appears, if the source exposes it (page number, section/heading, or paragraph position) — this is what Step 3's inline citations will point to

Do this capture as you research, not from memory afterward — reconstructing "which source said what" after 20 searches is exactly how citations get mismatched or invented. If you're not confident which source a fact came from, don't use it.

### Step 3 — Write the report

Use `assets/report_template.md` as the default structure. Write the report itself in the language chosen in Step 1 — headings, prose, and section names all switch, not just the sourced claims. Each section has a distinct job — don't let content bleed across sections (e.g. a specific player's product gap belongs in Unmet Market Gaps, not Competitive Landscape; a shifting compliance deadline belongs in Regulatory & Risk Factors, not Key Drivers).

**Inline citation mechanic** (this is the core of the skill): every claim that isn't common knowledge gets a citation immediately after it, in the form `(Publisher, Year — location)`, where "location" is whatever Step 2 captured — a page number, a section heading, or, if the source has no visible structure, a short positional description like "opening paragraph." The whole parenthetical is itself a hyperlink straight to the source URL — that's what makes it clickable proof, not just a label. For example, in Markdown: `The global market was valued at roughly $42B in 2025 ([McKinsey Europe, 2025 — p. 12](https://example.com/report)).` In HTML: `The global market was valued at roughly $42B in 2025 <a href="https://example.com/report">(McKinsey Europe, 2025 — p. 12)</a>.`

Where a fact is genuinely common knowledge or something you're stating as your own synthesis/judgment rather than a sourced fact, don't force a citation onto it — over-citing obvious statements clutters the report and dilutes the citations that matter.

Close the report with a **Sources** section: a plain, deduplicated list of every source cited — one entry per source even if it's cited several times in the body — giving its title, publisher, date, and link. The location and grounding excerpt already live inline with each citation in the body, so this list doesn't repeat them; it exists purely so a reader can see the full set of sources at a glance.

Where sources conflict on a figure or claim, say so explicitly in the text and cite both, e.g. `Estimates range from $38B (Source A, 2025) to $45B (Source B, 2025) depending on methodology.` rather than silently picking one — this is part of being trustworthy, not a formatting nicety.

### Step 4 — Verify before delivering

Before finalizing, do a pass specifically checking:
- Does every inline citation resolve to a working link, and does every source cited in the body also appear in the closing Sources list (and vice versa)?
- Are there contradictions between sections (e.g. a growth rate stated one way in the summary and another way in the body)?
- Is the tone even-handed — no unsupported editorializing, and any genuinely contested points presented as contested?

### Step 5 — Deliver

For a request that reads as wanting a quick, conversational answer, it's fine to answer inline in the chat — reserve the full report structure for requests that clearly want a deliverable.

**Markdown delivery** (default when the user doesn't specify): create it as a `.md` file rather than dumping a huge wall of text into the chat, following `/mnt/skills/public/md` conventions if present.

**HTML delivery** (when the user asks for HTML, or wants something polished to view or share as a standalone page): build a single self-contained `.html` file — CSS and any script inline, no external dependencies. This is a document meant to be read closely, not a marketing page, so keep the design in service of legibility: a clear type scale, generous line-height and comfortable line length (under ~75ch) for body paragraphs, and restrained color use. Each inline citation is itself the link: wrap the parenthetical citation text in `<a href="SOURCE_URL" target="_blank" rel="noopener">`, so a click jumps straight to the original source — no intermediate table or anchor to hunt through. Close with the compact Sources list (title, publisher/date, link) from Step 3, given real `<table>` or list structure with each URL as an actual `<a href>`. Avoid generic AI-report tells (see `/mnt/skills/public/frontend-design/SKILL.md` if present for what to avoid) — this should read like it was designed for this specific report, not a generic template.

**Slide-deck delivery** (when the user asks for slides, a deck, or something to present): this is a companion artifact, not a replacement for the full report — it condenses to the single most decision-relevant points and leans on the underlying report for the complete Sources list. Build it as a self-contained `.html` file too (see `assets/slides_template.html` for a working starting point), following strategy-consulting conventions:

- **5 slides maximum.** The limit is the point — it forces picking only what a decision-maker actually needs, not everything the research turned up. A typical shape: cover → market sizing → drivers → competitive landscape or gaps → the opportunity/recommendation. Combine or drop slides rather than exceeding five.
- **Action titles, not topic labels.** Every slide's headline is a full sentence stating the takeaway — "Regulation, not battery volume, is the near-term growth driver," not "Demand Drivers." Someone who only reads the five headlines in sequence should walk away with the report's actual argument.
- **One idea per slide, evidence underneath.** The headline makes the claim; the slide body (a stat row, a short bulleted list, a compact table) is what proves it. Don't let a slide carry two unrelated points.
- **Three bullets per slide, hard cap — and lead with the figure, not the sentence.** This is an executive digest: someone giving it 30 seconds should get the point without reading full sentences. Whenever a real number backs the point (a date, a percentage, a dollar figure), reuse the `stat-row`/`stat-card` pattern from the Market Sizing convention — a large bold value with a short caption underneath — instead of writing a prose bullet with the number buried mid-sentence. Only fall back to a plain short-phrase bullet (still a phrase, not a full sentence) when the point genuinely has no number to lead with. If a section seems to need more than three points, that's a sign to cut to the three most decision-relevant rather than shrinking text to fit more in.
- **Citations stay, just compressed.** Keep the same parenthetical citations on claims, as a small footnote line at the bottom of each slide, rather than reproducing the full Sources list — note in the deck (e.g. in the footer of the closing slide) that the complete source list lives in the companion report.
- **Keyboard-navigable, not just clickable.** This is a hard requirement, not a nice-to-have: arrow keys (and Home/End) must move between slides, the current slide must be announced to assistive tech (an `aria-live` region), each slide needs `role="group"` with an `aria-label` identifying its position ("Slide 2 of 5: ..."), and there must be a visible focus indicator — a mouse-only deck doesn't satisfy this. The template handles this; preserve it rather than removing the JS "because the deck looks fine without it."

## Copyright discipline (non-negotiable)

Sourced research is especially prone to copyright problems because it's tempting to lean on long quotes for "proof." Don't. This skill's citation mechanism gives verifiability through the *link and a short excerpt*, not through reproducing source text at length:
- Grounding excerpts must stay under 15 words, verbatim, and each source gets at most one such excerpt used as a quote.
- The location detail inside each inline citation (see Step 3) is factual metadata (page, section, paragraph) — it identifies where the excerpt sits, it doesn't add more quoted text. Don't drift into describing or summarizing the surrounding content there; that's not what it's for.
- Everything else — the claim itself, the surrounding analysis — must be in your own words.
- Never chain multiple quotes from the same source, even short ones.
- Never reproduce a source's paragraph structure or walk through it point-by-point as a substitute for original analysis.

## A note on tone and rigor

Market research readers are often making real decisions with this. Stay neutral and non-promotional — describe what sources say, flag disagreement between them, and avoid confident claims the sources don't actually support. If the available sources are thin on some angle the user asked about, say so plainly rather than filling the gap with plausible-sounding but unsourced material.

See `references/search-strategy.md` for guidance on scaling search depth to the scope of the request, `assets/report_template.md` for a ready-to-copy Markdown skeleton, `assets/report_template.html` for a ready-to-copy standalone HTML skeleton with inline hyperlinked citations and a Sources list already in place, and `assets/slides_template.html` for the companion slide-deck skeleton with keyboard navigation and accessibility wiring already built.
