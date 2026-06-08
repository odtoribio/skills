---
name: stock-analysis
description: Run a full fundamental analysis on a stock and deliver a clear buy verdict (Yes / Intermediate / No). Use this whenever the user gives a ticker or company name and wants to know whether it's worth buying, asks "is X a good investment / good buy", "should I buy X", "analyze X stock", "is X overvalued / undervalued", "do a fundamental analysis of X", "value-investing breakdown of X", or mentions evaluating a company against profitability, solidity, valuation, moat, or management. Trigger even when the user just names a company and asks for an opinion on it as an investment, and even if they don't say the words "fundamental analysis." Do NOT use for day-trading, technical/chart analysis, options, or crypto price predictions.
---

# Stock Analysis

Deliver a clear, defensible verdict on whether a stock is worth buying, by running a structured fundamental analysis: 16 quantitative criteria across three blocks (profitability, financial solidity, valuation), then 10 qualitative criteria (moat, management, sector, specific risks), then combining them. This skill encodes a value-investing framework — the goal is a company that is good *and* cheap, not just one or the other.

You are not a licensed financial advisor and this is educational analysis, not investment advice. Always include the short disclaimer at the end of the output.

## The workflow

Work through these steps in order. Don't skip the data step or fabricate numbers — an analysis built on guessed figures is worse than useless.

### 1. Pin down the company and its context
From the ticker or name, confirm the exact company, its ticker, and the exchange. Identify the **sector** and **3–5 comparable peers** in the same sector. This matters because the thresholds for Debt/Equity, ROE, and P/E are only meaningful against same-sector peers — a D/E of 2.5 is alarming for software and normal for a utility.

### 2. Gather the data (web search)
**Anchor the analysis to today's date.** A fundamental verdict is only as good as the data behind it, and financial data goes stale fast — price, P/E, PEG, and intrinsic-value-vs-price can change daily, and a fiscal year or quarter that was current last month may have been superseded. Always pull the *most recent available* figures as of the day the skill runs: the latest reported fiscal year and quarter (TTM where possible), the current share price, and the newest filings. Don't rely on remembered numbers from training — search for them fresh every time, and include current-year terms in your queries (e.g. the actual current year, not a year copied from an old example). State the "as of" date in the output's Sources section so the reader knows how current the verdict is.

Search the web for the figures you need. Good sources, in rough priority: the company's most recent annual report / 10-K and latest quarterly 10-Q (primary), StockAnalysis.com, Morningstar, and the company's investor-relations page. Aim for ~10 years of history (or as much as exists) so you can judge *consistency and trend*, not a single year — but make sure the most recent year/quarter is actually the latest one reported, not an older snapshot a search happened to surface.

Collect: revenue, net income, operating cash flow, free cash flow, EPS, gross/operating/net margins, ROE, ROIC, total assets, total liabilities, debt/equity, current ratio, interest coverage (EBIT ÷ interest), shares outstanding, current P/E, expected growth rate (for PEG), and current price. For valuation you'll also need peer P/E and enough cash-flow data to sketch an intrinsic value.

**Cite each key figure with its source.** Any number you cannot confirm gets marked **UNVERIFIED** in the scorecard — never invent a plausible-looking value. If too much core data is missing to reach a verdict (especially the solidity essentials), say so plainly rather than forcing a conclusion.

### 3. Score the 16 quantitative criteria
Read `references/quantitative.md` for the full definition, the favorable parameter, and the tier (Essential / Recommended) of each criterion. Score each **PASS / PARTIAL / FAIL / UNVERIFIED**, judging trend over the available years and comparing sector-relative metrics against the peers from step 1.

### 4. Apply the quantitative decision rule
From `references/quantitative.md`:
- **Non-negotiable:** the three essential solidity criteria — #9 assets vs. liabilities, #10 debt/equity, #11 current ratio — must pass. A failure here is close to disqualifying on its own, regardless of how good the rest looks.
- **Threshold:** at least **12 of 16** pass, with minimum coverage per block (≥5/8 profitability, all 3 solidity essentials, ≥2/3 valuation).
- Weigh *severity*, not just count: two valuation misses (a bit expensive) are mild; two solidity misses (bankruptcy risk) are severe.

### 5. Score the 10 qualitative criteria
Read `references/qualitative.md`. Score each **FAVORABLE / MIXED / WARNING / UNKNOWN** based on the favorable-vs-warning signals. These are judgments, not thresholds — reason from what the search turned up (shareholder letters, sector trends, competitive position, concentration, litigation).

### 6. Combine and decide
Use the matrix in `references/qualitative.md`: business quality (qualitative) × price-and-numbers (quantitative). Remember the **qualitative veto**: even a 16/16 quantitative company is not a buy if you can't understand the business, management looks dishonest, or there's no durable moat — those good numbers likely won't last.

Map the combined picture to one of three verdicts:
- 🟢 **Yes — worth buying:** passes the quantitative threshold *including* all solidity essentials, *and* the qualitative side is favorable (real moat, trustworthy management, no veto-level red flag). The matrix's "ideal buy" cell.
- 🟠 **Intermediate — watch / conditional:** genuinely mixed. E.g. a great business that's currently expensive (wait for a correction), or strong numbers with one unresolved qualitative concern, or solid but with 2–3 non-solidity misses you'd want to understand first. Most companies land here.
- 🔴 **No — avoid (for now):** fails a solidity essential, falls below the threshold in a way that signals real weakness, is a likely value trap (cheap but deteriorating), or hits a qualitative veto.

When data is too incomplete for confidence, lean toward 🟠 and say what's missing — don't manufacture a 🟢 or 🔴.

## Output format

Present the result using the exact structure in `references/output_format.md` — read that file before writing the verdict. It defines the report layout (headline verdict → short summary → quantitative scorecard → qualitative read → what to watch → sources), the symbol conventions (✅/🟡/❌/⬜ and 🟢/🟡/🔴/⬜), and the rule that the headline color must match the body. Keeping the format in one place means it can be edited without touching the analysis logic here.

## Notes
- If the user pastes their own figures or uploads a 10-K, use those as the primary source and search only to fill gaps; note that you did so.
- Scoping (quantitative-only / qualitative-only requests) and terseness guidance live in `references/output_format.md`.
