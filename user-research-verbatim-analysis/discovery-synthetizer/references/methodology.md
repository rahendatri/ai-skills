# Best practices: discovery synthesis

## Purpose of a discovery synthesis

A discovery synthesis cross-references all research sources produced during
a project (competitive intelligence, data analysis, user interviews) to
produce a structured problem list, ready for prioritization.

The goal is not to summarize each source separately. The goal is to connect
the dots across sources and surface the problems that are most strongly
supported by evidence.

---

## Required context before starting

A synthesis cannot be done without the following:

- The project brief: what problem area is being explored, for which sponsor,
  for which user population
- The north star metric: one single metric the team is trying to impact
- The list of discovery sources: competitive intelligence page, data analysis
  page, interview analysis pages including raw interview notes

Without this context, it is impossible to distinguish relevant problems from
out-of-scope observations. Ask for whatever is missing rather than guessing —
a wrong guess here (especially the north star metric) silently invalidates
every relevance and confidence judgment made later, and the error is
expensive to unwind once a full list has been built on top of it.

---

## Writing good problem statements

- **User-centric framing:** "Users struggle to..." not "The product lacks..."
- **One problem = one root cause.** Do not bundle symptoms into one statement.
  If two symptoms share the same root cause, write one problem. If they have
  different root causes, write two separate problems — even if they surface
  at the same moment in the user journey or came from the same interview.
  Test: would fixing one of them leave the other completely unresolved? If
  yes, they're separate.
- **Apply the 5 Whys:** if a problem statement could be answered with "because
  of another problem", go one level deeper. Stop when you reach a root cause
  the team can actually act on.
- **Be specific:** "Users struggle to understand the pricing breakdown at
  checkout" is a problem. "Users are confused" is not.

---

## Assessing source strength

Not all sources carry the same weight. Each problem should be flagged with
its source(s) and a confidence level:

- **Quantitative data alone:** high confidence if the dataset is large and the
  signal is clear. Flag as **data-validated**.
- **Multiple user interviews (3+) with consistent verbatims:** high
  confidence. Flag as **qualitatively validated**.
- **Cross-source** (data + interviews, competitive intel + interviews, or any
  two source types agreeing): strongest signal. Flag as **cross-validated**.
- **Single interview, a lone board sticky, or an anecdotal observation:** flag
  as **single-source**, needs more thinking before acting on it.

Do not downgrade a problem simply because it appears in only one source
type. A clean quantitative signal on a large dataset is strong evidence on
its own. A single qualitative observation is weak evidence on its own.

When exactly two independent sources corroborate something, be precise
rather than rounding up or down: it's stronger than single-source but it is
not yet the 3+ threshold for high qualitative confidence. Say so explicitly
("two independent, consistent reports — below the 3+ threshold for high
confidence") rather than collapsing it into either neighboring bucket.

---

## Reading interview sources

Prioritize raw interview notes over synthesis pages. Raw notes capture what
users said verbatim. Synthesis pages may have filtered things out. If both
exist, read both and flag any discrepancy between them.

The same logic applies to any other paired raw/synthesized source: a Miro
board full of raw sticky notes versus a written-up summary of that board,
a full data export versus someone's prior analysis write-up on top of it,
etc. When in doubt, go to the rawest version available.

---

## Reading quantitative sources

Don't stop at descriptive statistics ("average time to sell is 23 days").
Segment the data around the north star metric and look for what predicts
movement in it — categories, presence/absence of certain fields, price
bands, whatever the dataset supports. The strongest data-validated problems
usually take the shape "X differs sharply between the fast group and the
slow group," not "here is the distribution of X."

Watch for right-censoring / incomplete resolution in time-based datasets
(e.g. items still active/unsold at the moment of data extraction shouldn't
be treated as having the same "time to sell" as items that have actually
resolved) — conflating the two will bias every downstream average.

---

## Reading board/whiteboard sources (e.g. Miro)

Whiteboard tools often store the visible content (sticky notes, cards) as
nested "foreign" widgets inside a grid/layout container that a naive read of
the container won't expand. Search inside the container explicitly, and
make sure to retrieve *all* of its contents, not a first page or sample —
paginating through a large board is tedious but skipping the tail end is the
single most common way a well-corroborated problem gets mislabeled as
"missing" or "single-source." Card color often carries meaning (e.g. red =
problem, green = positive) and is a useful first pass, but always read the
actual text content — color conventions aren't guaranteed and a real problem
can be filed under an unexpected color.

---

## Output rules

- State a maximum problem count if the user hasn't already given one (default
  to roughly 10–15). Treat it as a ceiling: don't pad the list to reach it,
  and don't quietly exceed it — if a new, well-evidenced problem surfaces
  after the list is full, say explicitly what you'd need to cut to make room.
- Each problem includes: a one-sentence problem statement, the source(s)
  that support it, and a confidence level.
- If a source page is empty or inaccessible, signal it explicitly rather
  than working around it.
- The output is a draft for the PM (or requester) to challenge, not a final
  recommendation. Frame it that way — it should invite pushback, not read as
  a finished decision.
- When a scope exclusion is requested after a list already exists (e.g.
  "exclude category X"), remove affected items, note what was removed and
  why, and check whether the list is still a reasonable size rather than
  leaving an unexplained shorter list.
- When challenged on a specific gap ("didn't we also see problem Y
  somewhere?"), treat it as a strong signal to re-open the relevant
  source(s) rather than defending the existing list. If the challenge is
  right, say so plainly, show the evidence that was missed, and correct the
  list — this is more useful to the requester than a confident-sounding
  defense of an incomplete synthesis.
