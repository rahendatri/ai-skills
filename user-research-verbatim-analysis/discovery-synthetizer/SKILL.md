---
name: discovery-synthetizer
description: Cross-references discovery/research sources from a product discovery project (Notion interview transcripts and problem dumps, competitive intelligence decks, Miro user-journey boards, spreadsheets of quantitative data) into one structured, sourced, confidence-rated problem list ready for prioritization. Use whenever the user asks to "synthesize", "consolidate", or "cross-reference" discovery insights, user research, interview findings, or a "problem dump" into a prioritization-ready list — even without the word "synthesis" (e.g. "pull together everything we've learned", "what problems came out of the interviews and data", "check if we missed any problems", "turn this into a final problem list"). Also use to verify a synthesis against a newly added source, or to re-scope (exclude categories) or re-render (e.g. another language) an existing synthesis. Not for single-source summarization — this is specifically for combining multiple sources into one cross-validated output.
---

# Discovery Synthesizer

A discovery synthesis turns scattered research (interviews, data, competitive intel, whiteboards) into one structured, evidence-graded problem list a PM can actually prioritize from. The value isn't summarizing each source — it's finding where sources agree, disagree, or fill each other's gaps, and being honest about which problems are well-evidenced versus speculative.

This skill is a **methodology**, not a template to fill in mechanically. Read `references/methodology.md` in full before starting — it has the complete rules for required context, problem-statement writing, source-strength grading, and output format. This file (SKILL.md) is the workflow: what order to do things in, how to handle the tools involved, and how to handle follow-up requests.

## Why the order of operations matters

Skipping straight to synthesis without the required context (project brief, north star metric, source list) produces a list that looks thorough but can't actually be prioritized — every problem looks equally important because there's no metric to weigh them against. Likewise, skipping straight to synthesis without first pulling *every* source in full (not skimming) means the "cross-validated" labels in the output are unreliable — a problem tagged as single-source might actually have three corroborating mentions the model just didn't read.

## Step 1 — Confirm required context before touching any source

Per the methodology, a synthesis is impossible without: the project brief (problem area + sponsor + user population), the north star metric, and the full list of discovery sources. If the user's request doesn't already contain this (check the conversation — they may have stated it earlier, or a linked doc may state it), ask for it directly rather than guessing or inventing a plausible-sounding brief. A wrong assumption here silently corrupts every problem statement downstream, so it's worth a short back-and-forth up front rather than a full rewrite later.

If the user says "it's in this file" or points at a deck/page, go read it before asking anything else — don't make them repeat information that's already available to you.

## Step 2 — Confirm scope and plan before executing

Once the context is clear, briefly restate what you're about to do (which sources, what structure, what confidence framework) and get a lightweight confirmation before running off to fetch everything — this catches scope misunderstandings (e.g. "only that page" vs "that page and its sub-pages") while they're cheap to fix. Keep this step proportional: a one-paragraph plan is enough, this isn't a formal design doc.

## Step 3 — Pull every source in full, not a sample

For each source type:

- **Notion (interviews, problem dumps, journey syntheses):** Use the Notion MCP tools. Fetch the actual page content, not just a search snippet. If the user says to treat something as a "raw source," read it in full and don't defer to a synthesized/paraphrased version elsewhere, even if one exists and is faster to read — the methodology's whole point is that raw notes can contain things a synthesis filtered out. If both a raw and a synthesized version exist, read both and flag any discrepancy you notice.
- **Spreadsheets (xlsx/csv quantitative data):** Read the file(s) directly with pandas — don't assume a pre-existing "data analysis" write-up exists unless the user points you to one. Look for the actual quantitative signal that bears on the north star metric: segment the data the way the north star suggests (e.g. if the metric is "time to sell," build speed segments and check what predicts them — category, completeness of fields, price, etc.), not just descriptive stats for their own sake. A data-only finding (no interview or anecdote needed) can still be the single strongest problem in the whole list if the pattern is clear and the dataset is large — don't undersell it just because it didn't come from a quote.
- **Slide decks (competitive intelligence, product vision):** Extract with markitdown (see the pptx skill for how). Read for direct competitive gaps (a competitor does X natively/for free, we don't) and for internal tensions (a stated product differentiator that user research suggests isn't working as intended) — both are high-value, easy-to-miss findings.
- **Miro boards (user journey maps, workshop boards):** These often store the real content in "grid"/"grid_text" foreign widgets that a plain SVG read won't expand. Use `canvas_search` with `result_mode: "matches"` and pattern `["re:.+"]` targeting the frame's widget ID, and **paginate through every `next_cursor` until it's null** — stopping partway is the single easiest way to silently miss a well-corroborated problem (see "Common failure modes" below). Sticky note colors are usually meaningful (e.g. red = friction/problem, green = positive, orange/yellow = neutral journey step) — use color as a first-pass filter but read every card's `data-content`, since organizational color conventions vary and a problem can hide in an unexpected color.

Do not skip a source or sample it because it looks large or repetitive — a source that's 90% redundant with what you've already read is still worth a full pass, because the 10% that's new is exactly what a synthesis is for. If a listed source is empty or genuinely inaccessible, say so explicitly in the output rather than quietly working around it.

## Step 4 — Cross-reference and write the problem list

Follow `references/methodology.md` for the actual synthesis rules (problem-statement writing, root-cause discipline, confidence grading, max problem count). A few things worth calling out because they're easy to get wrong in practice:

- **Grade confidence honestly, not generously.** Two consistent independent mentions is good but not yet "3+ interviews" high confidence — say so plainly ("below the threshold for high confidence") rather than rounding up. The user is trusting these labels to decide what to act on without more validation.
- **Don't silently merge two problems with different root causes just because they show up in the same part of a journey.** E.g. "agreeing a meetup time/place in advance" and "finding your counterpart precisely once you're both on-site" are different failure points with different fixes, even though both live in the same journey step — keep them as separate line items. If in doubt, ask: would fixing one of these leave the other completely unresolved? If yes, they're separate problems.
- **Cite specific sources per problem**, not a blanket "based on all sources." Every problem statement should let a skeptical reader trace it back to who said what, or which dataset showed what.
- **Respect a hard max on problem count** if the user specifies one (the methodology defaults to 15). When you're at the limit and find a genuinely new, well-evidenced problem, explicitly say what you'd cut to make room rather than silently exceeding the limit or silently dropping the new finding.

## Handling common follow-up requests

Discovery synthesis is rarely one-shot — expect and welcome these follow-ups, and treat each as a request to **revise the existing list**, not start over:

- **"Did we miss anything?" / a new source is added:** Read the new source in full (per Step 3), then check each new finding against the *existing* list before adding it — many "new" findings turn out to be a fresh corroboration of an existing problem (which should bump its confidence level, not create a duplicate line item) rather than something genuinely new. State explicitly which items are additions, which are confidence upgrades to existing items, and which are unchanged.
- **"Exclude category/segment X":** Remove any problem whose evidence is centered on the excluded scope, and briefly check whether removing it drops the list below a reasonable size worth topping up from remaining sources — don't just delete and leave a shorter, unexplained list.
- **"The user thinks something's missing" (a pointed question, not just "check again"):** Take it seriously as a signal you likely under-read a source rather than defending the existing list — re-open the relevant source(s) specifically looking for what they described, and if you find it, explain plainly that it existed but got merged/lost, and fix it. Reflexively defending the prior output erodes trust faster than admitting a miss.
- **"Translate this" / "give me the French/Spanish/etc. version":** Reproduce the same structure, sourcing, and confidence levels — this is a faithful re-render, not a chance to rephrase or re-prioritize. Keep proper nouns, quotes from interviews, and dataset column names in their original language if translating them would lose meaning.
- **Output format preferences stated once (structured, sourced, specific confidence-level framing, etc.):** Apply them for the rest of the conversation without being re-asked each turn.

## Common failure modes to avoid

- **Stopping a paginated read partway through a large source** (Miro boards and long Notion pages are the usual culprits) and treating the partial read as complete — this is the most likely way to produce a confidently wrong "single-source" or "missing" label on a problem that was actually well-corroborated further down.
- **Skipping the required-context step** and inventing a plausible north star metric or brief — this makes every downstream confidence/relevance judgment silently wrong.
- **Treating the Problem Dump / interview synthesis pages as the primary source** instead of the raw interview transcripts when both exist and the user asked for raw — the dump is useful as a cross-check, not a substitute.
- **Doing pure sentiment/vibes analysis on the spreadsheet data** instead of actually segmenting it around the north star metric — "the data shows sellers are unhappy" is not a finding; "sellers in the slowest-selling quintile post 4x fewer repeat listings" is.
- **Padding the problem list to hit a target count**, or conversely trimming well-evidenced problems to look tidier than the evidence supports. The count is a ceiling, not a quota.
