---
name: stock-picking-cap
description: Fundamental stock analysis skill based on the Competitive Advantage Period (CAP), ROIC, WACC, and Economic Moats. Inspired by Warren Buffett's method to identify Quality Compounders and avoid mirages and value traps. English with technical terms preserved.
---

# Stock Picking — CAP & Moat Analysis

## Objective
Analyze a publicly traded company using the Competitive Advantage Period (CAP) method. Do not stop at the P/E ratio or revenue growth. Determine:
1. Whether the company has a durable competitive advantage (moat / economic moat)
2. Whether its ROIC sustainably exceeds its WACC
3. How long this advantage can resist mean reversion
4. Whether the market under- or over-estimates this duration in the current price
5. **Whether the stock beats the passive alternative (MSCI World) after adjusting for risk**

## Guiding Principles
- **Value creation = ROIC - WACC**, not just rising profits
- **The P/E ratio alone is a poor indicator**: it does not say how long the advantage will last
- **Quality Compounders**: companies that reinvest at high rates for very long periods
- **Mirages**: companies with temporarily high ROIC but no moat (cyclicals, commodities, temporary boosts)
- **Circle of competence**: do not analyze what you do not understand technologically
- **Margin of safety**: even a wonderful company can be a bad investment if the price bakes in an unrealistic CAP
- **No framework is objective**: this tool reduces blind spots but does not eliminate them. Every score, fade rate, and CAP estimate contains subjective judgment. Treat outputs as hypotheses, not facts.
- **Opportunity Cost**: stock-picking only makes sense if the risk/reward asymmetry beats the passive benchmark (MSCI World). A Quality Compounder at fair price is not an opportunity — the market-implied CAP must be significantly shorter than the estimated real CAP. The true test is: "Would I rather own MSCI World at 19x P/E with 8% growth, or this stock?"

---

## 0. Pre-Flight Checks

Before analysing any company, answer these. If uncertain, flag it explicitly in the report.

### Macro Context
| Question | Why It Matters |
|----------|---------------|
| Where are 10-year US Treasury rates? (~4.5% in May 2026) | WACC floor moves with rates. A 5% Rf vs 2% Rf changes the spread dramatically |
| Phase of the economic cycle? (expansion / peak / recession / recovery) | Cyclical companies look brilliant at the peak and terrible at the trough |
| Inflation trend? (rising, peaking, falling) | Pricing power matters most when inflation is high |
| Geopolitical risk relevant to this company? (tariffs, sanctions, supply chain) | Can erase a moat overnight (e.g. Russian assets in 2022) |
| Sector-specific headwind or tailwind? | Regulatory, technological, demographic shifts |

### Self-Awareness (Circle of Competence)
- Do I understand how this company makes money?
- Can I explain its competitive advantage in one sentence to a non-expert?
- Am I analysing this because the data is easy to find (large cap, covered by analysts) or because I genuinely understand the business?
- Is there a technological risk I cannot evaluate? If yes, flag uncertainty explicitly.

### Bias Check
| Bias | Symptom | Remedy |
|------|---------|--------|
| **Confirmation** | "This company is great, let me find data to prove it" | Run the anti-mirage check first |
| **Recency** | "Last quarter was amazing" | Force yourself to look at 10-year data |
| **Home bias** | "I know this brand so it must be good" | Compare with global peers |
| **Narrative** | "AI will change everything" | Quantify: how much revenue comes from the narrative? |
| **Anchoring** | "It was $500 before, now $300, it's cheap" | Calculate implied CAP, ignore the 52-week range |
| **Active management illusion** | "I can pick better than an index" | Run opportunity cost analysis vs MSCI World before concluding |

---

## Analysis Workflow

### Step 1: Fundamental Data Collection
Use `webfetch` and `playwright` to retrieve data on the target company.

**Mandatory data to collect:**
- ROIC over 10 years (GuruFocus, Morningstar, or calculated via NOPAT / Invested Capital)
- ROE, operating margin, net margin over 10 years
- Free Cash Flow and FCF Yield
- Debt / Equity, Net Debt / EBITDA, Interest Coverage
- P/E, P/S, EV/EBITDA current vs 5-year historical
- Revenue and EPS CAGR over 3 and 5 years
- **TAM (Total Addressable Market) and market share trend** — is the market growing or shrinking? Is share rising or falling?

**Strategic data to collect:**
- Business model: segments, revenue sources, geographies, key customers
- Market share and competitive position
- Recent news (6-12 months): competition, regulation, disruption
- Morningstar rating if available (Moat: Wide / Narrow / None, Fair Value, Uncertainty)
- **Capital allocation history** — major acquisitions, buybacks, dividends, dilution trends
- **Insider transactions** — are executives buying or selling? At what prices?
- **Accounting red flags** — see accounting checklist below

**Priority sources (free):**
1. `morningstar.com` — Economic Moat, Fair Value Estimate, fundamental data
2. `gurufocus.com` — Standardized ROIC, GF Score, 15+ years historical data
3. `macrotrends.net` — 50+ years historical data, long-term trends
4. `finance.yahoo.com` — Real-time data, news, basic ratios
5. `seekingalpha.com` — Detailed analysis, earnings call transcripts
6. Company Investor Relations site — Annual reports, presentations
7. `simplywall.st` — Quick fair value visualization via simplified DCF
8. `koyfin.com` — Pro platform with free tier, advanced screeners

**If a site is blocked by `webfetch`**, use `playwright` to navigate and capture the content: navigate to the page, wait for rendering, then extract text or take a snapshot.

---

### Step 2: Moat (Economic Moat) Analysis
Identify and classify the competitive advantage using the Morningstar framework:

| Type | Description | Examples |
|------|-------------|----------|
| **Network Effect** | Value increases as more users join | Visa, Mastercard, Microsoft, Meta |
| **Intangible Assets** | Brands, patents, licenses, know-how | Hermès, ASML, Coca-Cola, Nike |
| **Cost Advantage** | Economies of scale, optimized processes | Walmart, Costco |
| **Switching Costs** | High costs to change suppliers | SAP, Salesforce, ASML (30-year machines) |
| **Efficient Scale** | Limited markets, natural monopolies | Utilities, airports, local cement |

**Key questions to ask:**
- What type of moat protects the company?
- What are the concrete barriers to entry?
- Are serious competitors threatening this advantage?
- Can customers leave easily?
- Can the company raise prices without losing significant customers?
- Does the company get stronger as it grows?

**Width evaluation:**
- **Wide Moat**: Durable advantage 10-20+ years (ASML, Visa, Hermès, Microsoft)
- **Narrow Moat**: Advantage 5-10 years (Zoom, some regional banks)
- **No Moat**: Mean reversion in 3-5 years (Maersk, steel, commoditized retail)

**Moat erosion signals (check these carefully):**
- Revenue growth outpacing earnings growth (pricing power weakening)
- Customer concentration increasing
- Competitor entry with comparable quality at lower price
- Regulatory changes removing barriers to entry
- Technology shift that bypasses the company's advantage
- Patent cliff approaching without pipeline to replace
- **Voluntary catalogue price cuts to defend market share (price war initiated)** — a company that cuts its own list prices unilaterally is signalling pricing power erosion

---

### Step 3: Profitability and Value Creation
Verify that the company is truly creating economic value.

**Essential formulas:**
```
NOPAT = Operating Income × (1 - Tax Rate)
Invested Capital = Total Assets - Accounts Payable - Excess Cash
ROIC = NOPAT / Average Invested Capital

WACC = (E/(D+E)) × Ke + (D/(D+E)) × Kd × (1 - T)
Ke (Cost of Equity) = Rf + β × (Rm - Rf)  [CAPM]
```

**Golden rule:**
- ROIC > WACC → Value creation
- ROIC < WACC → Value destruction
- ROIC = WACC → No marginal value created

**ROIC quality thresholds:**
| Level | ROIC |
|-------|------|
| Exceptional | > 25% |
| Excellent | 15-25% |
| Good | 10-15% |
| Average | 5-10% |
| Weak | < 5% |

**Checks:**
- ROIC > WACC for 5-10 consecutive years?
- ROIC trend: stable, rising, or declining?
- Comparison with sector peers
- Is ROIC higher than ROE? (otherwise leverage is artificially boosting returns)
- **Is ROIC adjusted for goodwill?** If a company made large acquisitions, goodwill inflates assets and ROIC looks lower. If you exclude goodwill, does ROIC look suspiciously high? (implies acquisitions destroyed value)

**Practical WACC estimation reference (May 2026):**
| Component | Method | Typical Range |
|-----------|--------|---------------|
| Risk-free rate (Rf) | 10-year US Treasury yield | ~4.5% (check current) |
| Equity risk premium (Rm - Rf) | Historical US equity premium | 4-6% |
| Beta (β) | 5-year monthly vs S&P 500 | 0.8 (defensive) to 1.4 (volatile) |
| Cost of Equity (Ke) | Rf + β × ERP | 8-12% for most large caps |
| Pre-tax cost of debt (Kd) | Yield on outstanding bonds | Rf + 1-3% spread |
| Tax rate (T) | Effective rate from filings | 15-30% depending on jurisdiction |

**WACC by company type (estimate):**
| Type | Typical WACC |
|------|-------------|
| Large cap, low debt, stable (MSFT, V) | 8-10% |
| Large cap, some debt or volatility (META, GOOGL) | 9-11% |
| Mid cap, high growth | 10-13% |
| Small cap, high debt, cyclical | 12-16% |

**Note on WACC sensitivity:** A 1% difference in WACC changes the valuation significantly. Always check whether your conclusion holds if WACC is 1% higher or lower. If the verdict flips, your margin of safety is too thin.

---

### Step 3.5: Accounting Red Flag Checklist

Run this before trusting any financial metric. A single red flag does not disqualify a company, but 2+ without explanation means proceed with extreme caution.

| Red Flag | How to detect | Example |
|----------|--------------|---------|
| **Capitalised expenses** | R&D or customer acquisition costs growing as % of revenue while being capitalised instead of expensed | Software companies capitalising sales commissions |
| **Revenue recognition abuse** | Receivables growing faster than revenue (customers not paying) or unbilled receivables piling up | Premature recognition before delivery |
| **Goodwill ballooning** | Large acquisitions followed by goodwill impairments. If goodwill > 30% of equity, check past M&A track record | write-downs that destroy book value |
| **Stock-based compensation** | SBC > 10% of revenue or growing faster than revenue. Adjust FCF and diluted EPS for SBC | Unprofitable tech companies paying with options |
| **Related-party transactions** | Significant revenue from or expenses to related entities | Enron, Wirecard |
| **Pension assumption tricks** | Unrealistic discount rates or expected returns on pension assets | Older industrial companies |
| **Share dilution** | Share count growing consistently. Calculate cumulative dilution over 5 years | Companies that keep acquiring with stock |
| **Off-balance-sheet debt** | Operating leases, factoring of receivables, guarantees | Retail with massive lease obligations |
| **Auditor changes / restatements** | Multiple auditor changes or historical restatements | Reliable predictor of problems |
| **Insider selling patterns** | C-suite selling > 10x their buying over 12 months | Best leading indicator of overvaluation |
| **One-time items / provision reversals** | Revenue or earnings inflated by non-recurring items (legal settlements, provision writebacks, 340B adjustments). Compare reported vs adjusted figures. | Pharma companies with 340B program adjustments, banks with reserve releases |

---

### Step 4: Real CAP and Fade Rate Estimation
The **Competitive Advantage Period (CAP)** is the duration during which ROIC stays above WACC before regressing to the mean.

**Typical fade rates by moat type:**
| Moat Type | Fade Rate / Year | Est. CAP |
|-----------|------------------|----------|
| No Moat | 20-30% | 3-5 years |
| Narrow Moat | 10-15% | 5-10 years |
| Wide Moat | 5-8% | 10-20 years |
| Very Strong Wide Moat | 2-5% | 20+ years |

**Fade rate formula:**
```
ROIC(t) = WACC + (ROIC_initial - WACC) × (1 - fade_rate)^t
```

**Estimation method:**
1. Identify the moat type and width
2. Choose a fade rate consistent with sector history
3. Calculate how many years until excess ROIC drops to near zero
4. Cross-check with the company's actual history (has its ROIC already started declining?)

**TAM integration:** A company with a wide moat but a shrinking TAM (e.g., linear TV, print media, combustion engines) will see its ROIC regress faster regardless of moat strength. Always adjust the fade rate upward if the market is structurally declining.

**Scenario analysis (required):**
| Scenario | WACC assumption | Implied CAP | Verdict if this scenario happens |
|----------|----------------|-------------|----------------------------------|
| Base case (current rates) | ~10% | ? | ? |
| Rising rates (Rf = 6%) | ~12% | ? | ? |
| Falling rates (Rf = 3%) | ~8% | ? | ? |
| Recession (revenue -20%) | ~11% | ? | ? |

If the implied CAP under the rising-rate or recession scenario is < 5 years, the investment thesis is fragile.

---

### Step 5: Capital Allocation Assessment

Management quality is not a vague concept. Evaluate with concrete metrics:

| Metric | What it measures | Good signal | Bad signal |
|--------|-----------------|-------------|------------|
| **Incremental ROIC** | Return on new investments | > 15% | < WACC |
| **Buyback effectiveness** | Buybacks at good prices? | Buybacks when P/E < 15 or price < book value | Buybacks at ATH prices |
| **Dilution** | Net change in shares outstanding | Shares declining (net buyback) | Shares increasing 2%+ annually |
| **Dividend sustainability** | Payout ratio | < 50% of FCF | > 80% of FCF or funded by debt |
| **M&A track record** | Acquisitions over 10 years | Small bolt-on, high ROIC | Large transformative, goodwill impairments |
| **Cash efficiency** | Cash as % of market cap | < 10% (reinvested or returned) | > 20% (lazy balance sheet) |
| **Compensation alignment** | CEO pay vs shareholder return | CEO owns > 5% of shares, pay tied to ROIC | High fixed pay, golden parachutes, stock gift programs |

**Red flags in capital allocation:**
- Issuing shares to fund operations (serial diluter)
- Buying back shares while net debt is rising
- Acquiring unrelated businesses (empire building)
- Holding excess cash for years without plan (Berkshire Hathaway problem)
- Dividend cut shortly after buyback program (signalling failure)
- **Dividend growing while FCF does not cover it** — check FCF payout ratio annually. Growing dividend + negative FCF coverage = debt-funded illusion, not shareholder return

---

### Step 6: Valuation (Implied CAP)
The market anticipates a certain competitive advantage duration in the current price. You must back it out to find anomalies.

**Simplified Implied CAP method (inverse DCF approach):**
```
Value = NOPAT × [1 - (1+g)^n / (1+WACC)^n] / (WACC - g) + Terminal Value
```
Solve for **n** (number of CAP years) based on the current market price.

**Practical alternative approach:**
- Compare current P/E with Morningstar Fair Value
- Compare FCF Yield with required return
- If the current price implies a 5-year CAP but fundamental analysis suggests 20 years → **undervalued**
- If the current price implies a 25-year CAP but analysis suggests 8 years → **overvalued**

**Valuation sanity checks:**
| Check | If true | Danger |
|-------|---------|--------|
| P/E > 50x | Implied CAP > 20 years even with strong growth | Any moat erosion crushes returns |
| FCF Yield < 2% | Implied CAP near infinite | Even a small rate rise destroys value |
| EV/EBITDA > 30x | Market pricing perfection | No room for error |
| Price/Book > 20x | Extreme premium to assets | Capital-light businesses can justify this, but check |

**Reference examples:**
- **Microsoft (2020)**: P/E ~30, market anticipated a short CAP. Result: stock doubled in 4 years because CAP was underestimated.
- **ASML (2026)**: 694% premium above fair value, market anticipates an extremely long CAP that may be unrealistic.

**Capex adjustment for abnormal periods:**
When capex > 50% of Operating Cash Flow, P/FCF becomes misleading (company is investing massively for future growth). Use P/Operating CF instead, or normalize capex over 5-10 years.

**Dividend coverage check:**
Verify the dividend is covered by Free Cash Flow. A growing dividend not covered by FCF = debt-funded illusion. FCF Payout Ratio: < 50% healthy, > 80% dangerous.

---

### Step 7: Opportunity Cost Analysis vs Passive Benchmark

A Quality Compounder can be a great investment — but not necessarily better than MSCI World. This step forces explicit comparison before any buy/sell decision.

**MSCI World reference metrics (as of May 2026):**
| Metric | MSCI World |
|--------|------------|
| P/E (TTM) | ~19x |
| EPS CAGR (5y) | ~8% |
| PEG Ratio | ~2.4 |
| FCF Yield | ~2.5% |
| Dividend Yield | ~2.0% |
| ROIC (avg) | ~15% |
| Beta | 1.0 |
| Expected annual return (5-10y) | ~8-10% |

**Comparison table:**
| Metric | Stock | MSCI World | Gap | Interpretation |
|--------|-------|------------|-----|----------------|
| **PEG Ratio** | PER ÷ EPS CAGR | 2.4 | [X] | < 1 means better growth efficiency |
| **FCF Yield** | FCF / Market Cap | 2.5% | [X] | Higher = better cash return |
| **Expected return 5-10y** | Est. CAGR + Div Yield | ~8-10% | [X] | Based on estimated CAP fade |
| **Dividend Yield** | Div / Price | 2.0% | [X] | Cash return comparison |
| **ROIC** | NOPAT / Invested Capital | ~15% | [X] | Business quality |
| **Risk (Beta)** | 5y monthly | 1.0 | [X] | Relative volatility |
| **CAP-adjusted expected return** | CAGR × (CAP_est ÷ CAP_implied) + Div Yield | ~8-10% | [X] | Anomaly-adjusted view |

**CAP-adjusted expected return formula (opportunity lens):**
```
E[Return] = CAGR_EPS × (CAP_estimated ÷ CAP_implied) + Div_Yield
```
- If CAGR_EPS = 20%, CAP_est = 15y, CAP_implied = 5y, Div = 4%
- E[Return] = 20% × (15/5) + 4% = **64%/yr implied** (market is so wrong that reversion to fair value produces this return)
- If CAP_implied ≈ CAP_est, then E[Return] ≈ CAGR + Div = ~24% (still beats MSCI World but less extreme)

**Decision rule:**
| Alpha expected vs MSCI World | Verdict |
|------------------------------|---------|
| > 3%/year over 5+ years | **Genuine opportunity** — worth the stock-picking risk |
| 1-3%/year over 5+ years | **Marginal** — only if high conviction on moat durability |
| < 1%/year | **Not worth it** — buy MSCI World instead |
| Negative | **Sell / avoid** — the passive portfolio beats this pick |

**Portfolio framing (correct framing):**
Stock-picking is not a binary choice (100% stock vs 100% MSCI World). It is a **marginal decision**: for the portion of my portfolio allocated to active stock-picking (say 10-20%), does this specific stock earn that allocation better than just putting it into MSCI World?

**Final required question:** *"For the fraction of my portfolio dedicated to stock-picking, is the expected alpha of this stock (vs MSCI World) large enough to compensate for the concentration risk and analysis time?"* The answer must be quantitative.

A Quality Compounder with expected alpha > 3%/year justifies its allocation. Alpha < 1%/year does not — better to put that portion into MSCI World and keep it simple.

---

### Step 8: Quality Score and Verdict
Rate the company on a scale of 1 to 5 for each criterion, total out of 30.

| Criterion | 5 (Excellent) | 1 (Weak) |
|-----------|---------------|----------|
| **Moat Durability** | Wide moat, unassailable (Visa, Hermès) | No moat (Maersk) |
| **ROIC vs WACC** | ROIC > 25%, WACC < 8%, large spread | ROIC < WACC |
| **Historical Consistency** | ROIC stable > 15% over 10 years | Extreme ROIC volatility |
| **Pricing Power** | Prices rise > inflation without volume loss | Prices set by the market |
| **Capital Intensity** | Very low capital needs (software, networks) | Very high intensity (shipping, steel) |
| **Management Quality** | Exemplary capital allocation, transparency, ownership | Dilutive decisions, opacity |

**Score interpretation:**
- **25-30**: Exceptional Quality Compounder
- **20-24**: Good quality, worth studying closely
- **15-19**: Average quality, watch valuation
- **< 15**: Avoid for the long term

**Final verdict:**
- **Quality Compounder**: Buy if the price bakes in a realistic or underestimated CAP **and** the stock beats MSCI World on expected risk-adjusted return
- **Mirage / Value Trap**: Avoid despite appearances (low P/E, temporary growth)
- **Uncertain**: Wait for more visibility on the moat or valuation
- **Better off in MSCI World**: The stock may be fine, but not enough to justify active management

---

### Step 9: Falsification (Try to Prove Yourself Wrong)

Before concluding, actively try to disprove the investment thesis. Answer each:

1. **What specific event would make this ROIC drop by 50%?** (new competitor, tech shift, regulation)
2. **If I could short this stock with 2x leverage, would I?** (if yes, don't buy)
3. **What would a sceptical analyst say in 3 bullet points?** (write them)
4. **Am I confusing a great company with a great stock?** (great company + high price = bad investment)
5. **Is the TAM growing or shrinking?** (moat on a shrinking market is worthless)
6. **What happens if rates go back to 6%?** (would the valuation collapse?)
7. **Has this moat ever been tested in a recession?** (2008, 2020, 2022)
8. **Is the CEO's incentive aligned with long-term shareholders?** (check their stock ownership vs options grants)
9. **Would I still pick this stock over MSCI World if my analysis is 30% wrong?** (margin of safety on the opportunity cost)

If any answer reveals a vulnerability you cannot quantify, reduce position size or skip.

---

### Step 10: When to Sell (Exit Discipline)

The hardest part of investing. Define exit criteria **before** buying.

**Definite sells (act immediately):**
- [ ] Moat erosion confirmed (core product losing share, new competitor winning, switching costs falling)
- [ ] ROIC < WACC for 2 consecutive years (value destruction)
- [ ] CEO change to someone without capital allocation track record
- [ ] Accounting fraud or restatement discovered
- [ ] Stock exceeds 150% of estimated fair value (CAP now overpriced in the price)
- [ ] Thesis-breaking event (regulation bans the business model, key patent invalidated)

**Evaluate sells (review with fresh analysis):**
- [ ] Stock reaches fair value (take partial profits: 30-50% of position)
- [ ] Better opportunity with higher margin of safety appears (relative value swap)
- [ ] Position exceeds 15% of portfolio (rebalance for risk management)
- [ ] Management starts making dilutive or empire-building acquisitions
- [ ] Share count increases > 3% annually (stealth dilution)

**Do NOT sell for these reasons:**
- Stock dropped 20% (if thesis is intact, buy more)
- Macro news is scary (recessions are buying opportunities for compounders)
- Earnings miss one quarter (look through the noise)
- "It's gone up too much" (let your winners run if CAP is still underestimated)

---

## Research Delegation Prompts

### Prompt 1: Data Collection
```
Research and collect for [TICKER/COMPANY]:
1. Key financial data over 10 years: ROIC, ROE, operating margin, net margin, debt/equity, FCF, EPS
2. Business model: segments, revenue sources, geographies, representative customers
3. Competitive advantage: moat type per Morningstar, width, durability
4. Recent news (6-12 months): competition, regulation, technological disruption
5. Morningstar rating if available (Moat, Fair Value, Uncertainty, Rating)
6. Valuation data: P/E, P/S, EV/EBITDA, FCF Yield, dividend yield
7. TAM (Total Addressable Market) and market share trajectory
8. Capital allocation history: buybacks, dividends, M&A, dilution
9. Insider transactions over the last 12 months
10. Accounting red flags: check capitalised expenses, goodwill, SBC, dilution, receivables trend

Sources: morningstar.com, gurufocus.com, macrotrends.net, finance.yahoo.com, seekingalpha.com, company investor relations.

Summarize as factual bullet points. Do not interpret, just collect.
```

### Prompt 2: Moat Analysis
```
Analyze the competitive advantage of [COMPANY] based on collected data:
- What type of moat protects the company? (Network Effect, Intangible Assets, Cost Advantage, Switching Costs, Efficient Scale)
- What are the concrete and quantifiable barriers to entry?
- Are serious competitors threatening this advantage? Which ones?
- Can customers leave easily? What would be the switching costs?
- Can the company raise prices without losing significant customers?
- Does the company get stronger as it grows?
- Are there recent signs of moat erosion?
- Is the TAM growing or shrinking?

Give a clear assessment: Wide Moat / Narrow Moat / No Moat, with detailed justification.
```

### Prompt 3: Valuation Analysis
```
Evaluate the current valuation of [COMPANY] at the current price [PRICE]:
- Current P/E vs 5-year historical and sector median
- Current FCF Yield
- Morningstar Fair Value or other reliable reference
- P/S and EV/EBITDA vs peers
- What Implied CAP does the market anticipate at the current price? (compare with fair value)
- Scenario analysis: how does valuation change if WACC is 2% higher (rising rates)?
- Insider transactions: are executives buying or selling?

Conclude: overvalued, fairly valued, or undervalued relative to fundamental quality and estimated CAP.
```

### Prompt 4: Anti-Mirage Check
```
Check whether [COMPANY] could be a mirage / value trap:
- Is the currently high ROIC due to a favorable economic cycle?
- Does the company operate in a commodity business (prices set by the market)?
- Has there been a recent temporary boost (pandemic, war, shortage)?
- Is competition arriving with similar or cheaper products?
- Does the company need to reinvest massively to maintain profitability?
- Are current earnings sustainable without exceptional market conditions?
- Is the TAM growing or shrinking?
- Does the company have pricing power that has been tested in a downturn?
- Are there accounting red flags (capitalised expenses, SBC dilution, goodwill)?

If 2+ answers are positive, classify as a potential mirage.
```

### Prompt 5: Opportunity Cost vs MSCI World
```
Compare [COMPANY] at current price [PRICE] against MSCI World:

Stock metrics to use:
- P/E: [X] | EPS CAGR 5y: [X]% | PEG: [X]
- FCF Yield: [X]% | Div Yield: [X]%
- ROIC: [X]% | Beta: [X]
- CAP estimated: [X]y | CAP implied by price: [X]y

MSCI World reference:
- P/E: ~19x | EPS CAGR 5y: ~8% | PEG: ~2.4
- FCF Yield: ~2.5% | Div Yield: ~2.0%
- ROIC: ~15% | Beta: 1.0
- Expected return 5-10y: ~8-10%

Calculate:
1. PEG ratio comparison (lower = better)
2. CAP-adjusted expected return: CAGR × (CAP_est ÷ CAP_implied) + Div Yield
3. Alpha expected vs MSCI World: [E[Return_stock] - E[Return_MSCI]]
4. Risk-adjusted comparison: does the stock compensate enough for its higher specific risk?

Apply decision rule:
- Alpha > 3%/y → genuine opportunity
- Alpha 1-3%/y → marginal, requires high conviction
- Alpha < 1%/y → recommend MSCI World instead

Conclude: is this stock worth the active management risk vs a passive world index?
```

---

## Mandatory Output Format

Produce a structured markdown report with the following sections:

```markdown
# Analysis [TICKER] — [Company Name]
Date: [DATE]

## Executive Summary
- Verdict: [Quality Compounder / Mirage / Value Trap / Uncertain / Better off in MSCI World]
- Quality Score: [XX/30]
- Recommendation: [Buy / Watch / Wait / Avoid]
- Current Price: [X] | Reference Fair Value: [X] | Margin of Safety: [X]%
- Opportunity Cost Verdict: [Beats MSCI World / Matches MSCI World / Worse than MSCI World]
- Suggested position size: [X]% of portfolio (based on conviction: 5-40%)

## 0. Pre-Flight Checks
- Macro context: [rates, cycle, inflation, geopolitical]
- Circle of competence: [understood / uncertain / outside]
- Bias check: [any biases identified]

## 1. Profile and Business Model
[Concise description of segments, geographies, economic model]
- TAM: [$X] and market share: [X]%

## 2. Moat Analysis
- Identified type: [Network / Brand / Cost / Switching / Scale / Combination]
- Width: [Wide / Narrow / None]
- Estimated durability: [X] years
- Barriers to entry: [Concrete list]
- Identified threats: [List]
- Moat erosion signals: [List or none]

## 3. Profitability and Value Creation
- 5-year average ROIC: [X]% | 10-year average ROIC: [X]%
- Estimated WACC: [X]% (with assumptions: Rf, beta, ERP)
- ROIC-WACC spread: [X]% (average)
- ROIC trend: [Stable / Rising / Declining]
- Average operating margin: [X]%
- Free Cash Flow Yield: [X]%
- Accounting red flags: [List or clean]

## 4. Capital Allocation Assessment
- Buyback effectiveness: [Good / Neutral / Poor]
- Dilution / buyback net: [X]% annual change in shares
- M&A track record: [Good / Neutral / Poor]
- Cash efficiency: [X]% cash / market cap
- Management alignment: [Insider ownership X%, compensation structure]

## 5. Competitive Advantage Period (CAP)
- Estimated real CAP: [X] years
- Estimated fade rate: [X]% per year
- Implied CAP (market): [X] years
- Anomaly: [Market underestimates / Market overestimates / Fair]
- Scenario check: [Does verdict hold under rising rates / recession?]

## 6. Valuation
- Current P/E: [X] vs 5-year historical: [X]
- P/S: [X] | EV/EBITDA: [X]
- FCF Yield: [X]%
- Morningstar Fair Value: [X]
- Dividend Yield: [X]%
- Insider activity: [Buying / Neutral / Selling]

## 7. Opportunity Cost vs MSCI World
| Metric | Stock | MSCI World | Gap |
|--------|-------|------------|-----|
| P/E | [X] | ~19x | [X] |
| EPS CAGR 5y | [X]% | ~8% | [X] |
| PEG Ratio | [X] | ~2.4 | [X] |
| FCF Yield | [X]% | ~2.5% | [X] |
| Div Yield | [X]% | ~2.0% | [X] |
| ROIC | [X]% | ~15% | [X] |
| Beta | [X] | 1.0 | [X] |
| CAP-adjusted E[Return] | [X]% | ~8-10% | [X] |
- Alpha expected vs MSCI World: [X]%/year
- Verdict: [Genuine opportunity (alpha > 3%) / Marginal (1-3%) / Not worth it (< 1%)]

## 8. Falsification
- What would break the thesis: [List]
- Would I short this stock? [Yes / No]
- Sceptic's case: [3 bullet points]
- Would I still pick this over MSCI World if my analysis is 30% wrong? [Yes / No]

## 9. Risks and Red Flags
- [Risk 1]
- [Risk 2]
- [Risk 3]

## 10. Exit Criteria
- Sell if: [specific conditions]

## 11. Conclusion and Thesis
[Synthesis: why buy, wait, or avoid. Explicit reference to CAP, moat, and opportunity cost vs MSCI World. Answer: "Why this stock instead of MSCI World?"]
```

---

## References and Examples

### Quality Compounders (Wide Moat, Long CAP)
| Company | Moat | ROIC | Est. CAP | Key Risk |
|---------|------|------|----------|----------|
| **ASML** | Patents + Switching Costs | ~47% | 15-20+ yrs | Extreme valuation (694% premium) |
| **Mastercard** | Network Effect | ~63% | 15-20 yrs | Fintech, account-to-account payments |
| **Visa** | Network Effect | ~40% | 15-20+ yrs | Alternative network competition |
| **Hermès** | Brand (artificial scarcity) | ~23% | 20+ yrs | Luxury cyclicality, geopolitics |
| **Microsoft** | Network + Switching + Brand | ~31% | 15-20+ yrs | Massive AI capex, Office maturity |

### Mirages / Value Traps (No Moat or Short CAP)
| Company | Appearance | Reality | Lesson |
|---------|------------|---------|--------|
| **Maersk** | Low P/E, dividends | Commodity shipping, no moat | Don't buy cyclicals at the peak |
| **Zoom (2021)** | ROIC > 100%, boom | No durable moat, free MS/Google competition | Temporary boost ≠ structural advantage |
| **Shipping/Commodities** | High ROIC during shortages | No pricing power | Mean reversion is inevitable |

### Opportunity Cost Examples (Stock vs MSCI World)
| Company | Year | P/E | vs MSCI P/E | Alpha Result | Lesson |
|---------|------|-----|-------------|-------------|--------|
| **Microsoft** | 2020 | ~30x | ~1.5x MSCI | Outperformed 4x | CAP was underestimated |
| **Novo Nordisk** | 2026 | ~13x | ~0.7x MSCI | ? | CAP anomaly: market prices 5y for a 20y moat |
| **ASML** | 2026 | ~45x | ~2.4x MSCI | ? | CAP may be overestimated despite wide moat |
| **Zoom** | 2021 | ~200x | ~10x MSCI | -80% | Mirage: premium moat vanished |

### Failed Moats (Survivorship Bias Warning)
These companies all had Wide Moats at their peak. The lesson: moats are not permanent.

| Company | Former Moat | What Killed It | Year of Collapse |
|---------|-------------|----------------|------------------|
| **Kodak** | Brand + Patents (film photography) | Digital photography (technology shift) | 2000-2012 |
| **Nokia** | Brand + Scale (mobile phones) | iPhone / Android (platform shift) | 2007-2013 |
| **IBM** | Switching Costs (enterprise IT) | Cloud computing (architecture shift) | 2012-2020 |
| **GE** | Brand + Scale (conglomerate) | Poor capital allocation, debt, complexity | 2008-2018 |
| **BlackBerry** | Switching Costs (enterprise mobile) | iPhone / Android (consumerisation of IT) | 2008-2013 |
| **Xerox** | Patents + Brand (copiers) | Digital documents (category death) | 1990-2010 |

**Checklist to avoid the next fallen moat:**
- Is the company's product threatened by a technology that did not exist 10 years ago?
- Does the company's competitive advantage rely on something that could be made obsolete?
- Would a well-funded startup with a clean sheet of paper do it differently?
- Is the company's management investing in the future or defending the past?

---

## Strict Usage Rules
1. **Always start with the business model and the moat**, never with the P/E ratio or stock price.
2. **Never recommend a company without an identifiable moat** for long-term investment (10+ years).
3. **Always compare estimated real CAP with market-implied CAP** — that is where the anomaly lies.
4. **Always compare opportunity vs MSCI World before recommending.** If expected alpha < 2%/year, recommend MSCI World instead.
5. **If data is insufficient**, explicitly ask what is missing rather than guessing or extrapolating.
6. **For complex technology companies**, verify they are within your circle of competence. Otherwise, flag uncertainty.
7. **Do not rely on the latest quarter's earnings alone** — look at 5 to 10 years of history.
8. **Distinguish operational value creation (ROIC) from leverage effect (ROE)** — prefer ROIC.
9. **A high P/E is not necessarily expensive** if the CAP is underestimated. A low P/E is not necessarily cheap if the CAP is zero.
10. **Define exit criteria before buying.**
11. **Run the falsification checklist before every final verdict.**
12. **Run the accounting red flag checklist before trusting any financial metric.**
