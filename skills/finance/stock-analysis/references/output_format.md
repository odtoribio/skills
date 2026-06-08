# Output format

Lead with the verdict so it's the first thing the reader sees, then the short summary, then the supporting detail. Use this exact structure:

```
## [COMPANY] ([TICKER]) — Verdict: 🟢 YES / 🟠 INTERMEDIATE / 🔴 NO

**[One- to three-sentence summary of the decision and the single biggest reason for it.]**

### Why this verdict
[One short paragraph (~3–6 sentences) in plain language: the decisive factors. Lead with what drove the call — e.g. "Solid, cheap, and a clear moat" or "Great business but priced for perfection" or "Fails liquidity and carries heavy customer concentration." This is the narrative version of the verdict.]

### Quantitative scorecard ([X] / 16 passed)
| # | Criterion | Result | Note |
|---|-----------|--------|------|
| 1 | Revenue | ✅ PASS | brief evidence + figure |
| ... | ... | ... | ... |
Solidity essentials (9–11): [✅ all pass / ❌ fails #N]
Block coverage: Profitability X/8 · Solidity X/5 · Valuation X/3

### Qualitative read
| # | Point | Signal | Note |
|---|-------|--------|------|
| 1 | Durable advantage | 🟢 Favorable | brief reasoning |
| ... | ... | ... | ... |
Moat: [type(s) / none] · Management: [read] · Veto flag: [none / which one]

### What to watch
[2–4 bullets: the things that would change the verdict, or what to monitor if buying / waiting.]

### Sources
[State the "as of" date of the analysis (today's date) and the most recent fiscal period used. List the key sources, with what each provided. Flag any UNVERIFIED figures here.]

---
*Educational analysis, not investment advice. Thresholds are general guides that vary by sector and market conditions. Verify figures against primary sources (10-K) and consider a certified financial advisor before investing.*
```

## Symbol conventions

Use these consistently so the report reads the same way every time:
- **Quantitative results:** ✅ PASS · 🟡 PARTIAL · ❌ FAIL · ⬜ UNVERIFIED
- **Qualitative signals:** 🟢 Favorable · 🟡 Mixed · 🔴 Warning · ⬜ Unknown

The headline verdict color (🟢 / 🟠 / 🔴) must match the body of the analysis — never show a green headline over a scorecard full of failures.

## Scoping

- If the user asks only for the quantitative side, or only the qualitative side, run just that block and give a verdict scoped to it (drop the section that wasn't run).
- Keep evidence notes terse — a figure or a phrase, not a paragraph. Depth lives in the structure, not in long prose.
