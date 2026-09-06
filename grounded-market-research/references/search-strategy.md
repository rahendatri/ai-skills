# Scaling search depth to scope

Match the number of searches (and fetches of full pages, not just snippets) to what the user actually needs. Search snippets are often too thin to safely extract a specific grounding excerpt from — when a fact matters, `web_fetch` the source page rather than citing off the snippet alone.

## Quick briefing (5-10 searches)
The user wants a fast, sourced overview — a few paragraphs, not a full report. Still cite every real claim, but don't force the full report structure (Step 4 in SKILL.md) unless they ask for something they'll save or share.

Example triggers: "quickly, how big is the market for X", "give me a sourced take on what's happening in Y right now".

## Standard report (10-20 searches)
Covers market size, a handful of key trends, and the main competitive players. This is the default for a plain "do market research on X" request.

Search across categories, not just repeated variations of one query:
- Market size / forecast: `"[market] market size 2026"`, `"[market] forecast"`
- Trends: `"[market] trends 2026"`
- Competitors: `"[market] key players"`, `"[market] competitive landscape"`
- Recent news: `"[market] news"` (bias toward the last 1-3 months for fast-moving markets)
- Primary sources where they exist: company investor pages, government/statistical agency sites, trade association reports

## Deep / exhaustive report (20+ searches, consider suggest_research)
Multi-jurisdiction comparisons, investment-grade due diligence, or anything the user describes as needing to be thorough or comprehensive. Do the searches you can within the conversation, but also consider offering the background Research tool (if available) for the kind of broad, many-source synthesis that benefits from a dedicated background run — per the tool's own guidance, offer it alongside a direct answer rather than in place of one.

## General search hygiene
- Reformulate rather than repeat: if a query returns nothing useful, change the angle (different terms, a named source, a narrower or broader scope) instead of re-running the same phrasing.
- Prioritize original sources (company filings, statistical agencies, primary research firms, direct company statements) over aggregator or listicle sites — aggregators are fine for orientation but weak as the actual citation.
- For numbers that matter to the conclusion (market size, growth rate, share), try to corroborate with more than one source before treating it as settled; if sources disagree, that disagreement belongs in the report (see SKILL.md Step 4).
- Note publication dates. A "current market size" claim from a 2022 source should be flagged as dated, not presented as current.
