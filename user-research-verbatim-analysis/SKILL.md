---
name: user-research-verbatim-analysis
description: >-
  Analyze user-research interview transcripts or verbatims (e.g. a CSV/doc of
  customer interviews) to surface product-discovery insights. Produces a
  locked 4-part output — (1) a table classifying each verbatim as clear,
  actionable feedback vs. vague statements needing follow-up, (2) a
  theme-frequency ranking, (3) the single most frequent plus painful theme
  with supporting quotes, (4) a scoped, actionable recommendation. Use this
  whenever the user shares interview transcripts, customer discovery notes,
  or research verbatims and asks to find themes, pain points, patterns, or
  recommendations — even if they don't use the words "analyze" or "verbatim"
  explicitly (e.g. "here are 10 customer interviews, what should we build?",
  "pull out the key themes from this research", "what's the biggest pain
  point in these calls?"). Also use to turn raw Q&A-style interview
  transcripts into a structured discovery report.
---

# User Research Verbatim Analysis

## Why this skill exists

Raw interview transcripts are noisy: a mix of specific, actionable detail ("I switch between three tools and sometimes double-book") and vague color ("it's stressful"). Treating both as equally strong evidence leads to either over-scoping features off a throwaway comment, or missing a real signal buried in a long transcript. This skill's job is to separate the two, count how often real signal repeats across distinct people, and turn the strongest repeated + painful signal into something a product team can actually act on — rather than a generic summary of "what people said."

## When to use this

Trigger on any request to review interview transcripts, call notes, survey verbatims, or discovery-interview CSVs/docs for themes, pain points, or "what should we build" style questions. This applies across domains — hosts, SaaS users, patients, employees, whatever the interviewee population is — not just Airbnb hosts. It does not require the user to say "classify" or "theme" explicitly; "what's bugging our customers most" or "read these 10 calls and tell me what to prioritize" both qualify.

## Before starting: read the source

Read the full transcript file yourself (view the whole thing — do not sample or skim a truncated preview and extrapolate). If the file is long, view it in full ranges rather than guessing at what the missing middle contains. Every claim in your output must trace back to something actually said in a transcript.

## Step 1: Classify every verbatim into two buckets

Go interview by interview and pull out each distinct pain-point or need statement. Sort each into exactly one of two buckets:

- **Clear feedback**: contains a specific situation, a mechanism, an action already taken, or a concretely described unmet need — enough detail that a PM could scope a feature from it without guessing.
- **Vague / needs clarification**: states an outcome, an emotion, or a general complaint without the underlying mechanism — true, but not yet actionable.

**Example (the calibration case):**
- ❌ Vague: "I have difficulties in validating a transaction." — no detail on what step fails, how often, or why.
- ✅ Clear: "It's difficult to track reservations correctly and I had to note them down manually on my calendar." — names the specific behavior (manual calendar note-taking) and implies a concrete fix (calendar integration).

Watch for statements that sound insightful but are actually just well-phrased vagueness ("the mental load is the heaviest part") — these still belong in the vague column unless a mechanism follows them.

Present this as a markdown table: one row per interviewee, with their clear verbatims (tagged with a short theme label) in one column and their vague verbatims in the other. It's fine and expected for some interviewees to have nothing in the vague column, or vice versa.

## Step 2: Rank themes by frequency

Group the clear-feedback verbatims into themes (name them descriptively, e.g. "cross-platform fragmentation," not "Theme A"). Rank themes by **the number of distinct interviewees who raised them**, not total mention count — one person raising something five times should not outrank five people each raising it once. Present as a ranked table: theme, which interviewees raised it, count.

If two themes tie on interviewee count, do not arbitrarily break the tie — list them as tied and let the pain-intensity evidence in Step 3 help distinguish, or note both as worth investigating.

## Step 3: Identify the most frequent + painful theme

Take the top theme(s) from Step 2 and check whether the frequency leader is also backed by real pain — quote the emotional/cost language interviewees used (time lost, money lost, stress, relationship damage with guests/customers, reputational risk). A theme that's frequent but low-stakes is a weaker candidate than one that's frequent *and* clearly costly — call this out explicitly if it happens, rather than mechanically picking the top row.

Support the selection with 2-4 direct quotes across different interviewees, not just one.

## Step 4: Write one actionable recommendation

For the winning theme, write a single recommendation containing:
- **What to build/change**, in one sentence.
- **Why it matters** — tie back to business impact (retention, review scores, revenue, support cost), not just "users want it."
- **Execution steps** — a numbered list moving from validation/discovery (if the underlying need still has open questions) through MVP scope through pilot/measurement. Steps should be concrete enough to hand to a team, not "do more research" as a whole step.

## Output format — always use this structure

```markdown
## 1. Verbatim Classification — Clear Feedback vs. Vague/Needs Clarification
[table: interviewee | clear feedback (themed) | vague/needs clarification]

## 2. Theme Frequency (by number of distinct interviewees mentioning it)
[ranked table: rank | theme | interviewees | # interviewees]

## 3. Most Frequent + Most Painful Theme
[selection + supporting quotes + brief rationale]

## 4. Recommendation
[what to build, why it matters, numbered execution steps]

---
**Source:** [filename / origin of the transcripts]
**Methodology note / limitation:** [sample size, self-reported nature, qualitative caveat]
**Consistency check:** [one line confirming the table counts match the ranking and the recommendation matches the selected theme]
```

Keep this structure even if the user's request is casual or short — the value of the skill is the discipline of the format, not just the prose. If the user explicitly asks for a different format after seeing this once, follow their new instruction for that turn, but default back to this structure next time this skill is invoked.

## Common pitfalls to avoid

- Don't inflate frequency by counting total mentions instead of distinct interviewees.
- Don't classify a well-written or emotionally resonant quote as "clear feedback" just because it's compelling — check specifically for the mechanism/action, not eloquence.
- Don't let the recommendation drift to a theme that wasn't actually the top-ranked one in Step 2/3 — the consistency check exists to catch this.
- Don't skip the source citation and limitations note — this is qualitative, self-reported data, and the reader needs that framing to weigh the findings correctly.
