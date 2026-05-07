# stock-picking-cap

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](https://opensource.org/licenses/MIT)
[![Built for: OpenCode & Claude](https://img.shields.io/badge/Built%20for-OpenCode%20%26%20Claude-orange.svg)]()
[![Method: Buffett-Style CAP](https://img.shields.io/badge/Method-Buffett--Style%20CAP-green.svg)]()

**Stock-Picking-CAP** is an AI-native fundamental analysis skill that screens public companies through the lens of Competitive Advantage Period (CAP). It transforms a ticker symbol into a full investment thesis — moat classification, ROIC durability, fade-rate modeling, and implied-CAP valuation — to separate true Quality Compounders from temporary profitability mirages.

---

## The Problem

Most investors look at the same surface-level metrics: rising earnings, low P/E, strong revenue growth. The problem? **Everyone sees that.** The real edge lies in answering a harder question:

> *How long can this company keep generating returns above its cost of capital before competition erodes it?*

This skill guides AI agents through **Competitive Advantage Period (CAP)** analysis — the engine behind Warren Buffett's fortune. It distinguishes:
- **Quality Compounders** (ASML, Mastercard, Hermès) — wide moat, durable ROIC > WACC
- **Mirages / Value Traps** (Maersk, Zoom post-COVID) — temporary profitability with no moat

---

## Key Concepts

| Concept | Definition |
|---------|------------|
| **CAP** | Competitive Advantage Period — how long ROIC stays above WACC |
| **Moat** | Economic advantage protecting the business from competition |
| **Fade Rate** | Speed at which excess ROIC regresses to the mean |
| **Implied CAP** | CAP the market already prices into the current stock price |
| **Quality Compounder** | Company reinvesting at high ROIC for very long periods |

---

## 10-Step Workflow

1. **Pre-Flight Checks** — Macro context, circle of competence, bias audit
2. **Data Collection** — ROIC, WACC, margins, debt, TAM, insider transactions, accounting red flags (10-year history)
3. **Moat Analysis** — Identify type (Network, Brand, Cost, Switching, Scale) and width, detect erosion signals
4. **Profitability & Value Creation** — Verify durable ROIC > WACC with practical WACC estimation
5. **Accounting Red Flag Checklist** — Capitalised expenses, SBC dilution, goodwill, revenue recognition
6. **CAP Estimation** — How many years will the moat hold? Adjust for TAM trajectory
7. **Capital Allocation Assessment** — Buyback effectiveness, M&A track record, dilution, management alignment
8. **Valuation (Implied CAP)** — Does the current price assume a realistic CAP? Scenario analysis across rate environments
9. **Falsification** — Actively try to disprove your own thesis before concluding
10. **Exit Discipline** — Define sell criteria before buying. Know when to hold, trim, or exit

---

## Quick Start

Copy the skill file into your agent's skills directory:

```bash
# OpenCode
mkdir -p ~/.config/opencode/skills/stock-picking-cap
cp skills/stock-picking-cap/SKILL.md ~/.config/opencode/skills/stock-picking-cap/SKILL.md
```

Then invoke:

```
/stock-picking-cap NVDA
```

The agent will collect data, analyze the moat, estimate the CAP, and produce a structured report.

---

## Repository Structure

```
└── skills/
    └── stock-picking-cap/
        └── SKILL.md          # Full skill with prompts, formulas, examples
```

---

## Reference Examples

### Quality Compounders (Wide Moat, Long CAP)

| Company | Moat | ROIC | Est. CAP | Key Risk |
|---------|------|------|----------|----------|
| **ASML** | Patents + Switching Costs | ~47% | 15-20+ yrs | Extreme valuation (694% premium) |
| **Mastercard/Visa** | Network Effect | 40-60% | 15-20+ yrs | Fintech disruption |
| **Hermès** | Brand + Artificial Scarcity | ~23% | 20+ yrs | Luxury cyclicality |
| **Microsoft** | Ecosystem | ~31% | 15-20+ yrs | AI capex, Office maturity |

### Mirages / Value Traps (No Moat, Short CAP)

| Company | Appearance | Reality | Lesson |
|---------|------------|---------|--------|
| **Maersk** | Low P/E, dividends | Commodity shipping, no moat | Don't buy cyclicals at the peak |
| **Zoom (2021)** | ROIC > 100%, COVID boom | No durable moat, free MS/Google competition | Temporary boost ≠ structural advantage |
| **Commodities** | High ROIC during shortages | No pricing power | Mean reversion is inevitable |

### Failed Moats (Survivorship Bias Warning)

| Company | Former Moat | What Killed It |
|---------|-------------|----------------|
| **Kodak** | Brand + Patents | Digital photography |
| **Nokia** | Brand + Scale | iPhone / Android platform shift |
| **IBM** | Switching Costs | Cloud computing |
| **GE** | Brand + Scale | Poor capital allocation, debt |
| **BlackBerry** | Switching Costs | Consumerisation of IT |

---

## Golden Rules

- **Always start with the moat**, never with the P/E.
- **Never recommend without an identifiable moat** for long-term investing.
- **A high P/E is not necessarily expensive** if the CAP is underestimated.
- **A low P/E is not necessarily cheap** if the CAP is zero.
- **Distinguish ROIC (real value creation) from ROE (leverage effect)**.
- **Define exit criteria before you buy.**
- **Run the falsification checklist before every verdict.**

---

## What This Skill Does NOT Do (Limitations)

This is not a complete investment system. It does not replace:
- Reading annual reports (10-K, 20-F)
- Detailed financial statement analysis
- Understanding the competitive dynamics of a specific industry
- Portfolio construction and risk management
- Tax planning for your jurisdiction
- Judgment — the CAP, fade rate, and quality score are estimates, not facts

**Use this skill as a first-pass filter (15 minutes), not as a final conclusion.**

---

## Methodology

### ROIC
```
ROIC = NOPAT / Average Invested Capital
NOPAT = Operating Income × (1 - Tax Rate)
```

### WACC
```
WACC = (E/(D+E)) × Ke + (D/(D+E)) × Kd × (1 - T)
```

### Fade Rate
```
ROIC(t) = WACC + (ROIC_initial - WACC) × (1 - fade_rate)^t
```

**Typical Fade Rates:**

| Moat Type | Fade Rate / Year | Est. CAP |
|-----------|------------------|----------|
| No Moat | 20-30% | 3-5 years |
| Narrow Moat | 10-15% | 5-10 years |
| Wide Moat | 5-8% | 10-20 years |
| Very Strong Wide Moat | 2-5% | 20+ years |

---

## Recommended Data Sources

- [Morningstar](https://www.morningstar.com) — Moat ratings, Fair Value
- [GuruFocus](https://www.gurufocus.com) — Standardized ROIC, GF Score
- [MacroTrends](https://www.macrotrends.net) — 50+ years historical data
- [Yahoo Finance](https://finance.yahoo.com) — Real-time data, basic ratios
- [Seeking Alpha](https://seekingalpha.com) — Analysis, earnings transcripts
- [Koyfin](https://www.koyfin.com) — Pro-grade platform (free tier)

---

## Credits

Methodology inspired by:
- Warren Buffett — *Economic Moats* and *Wonderful Companies*
- Morgan Stanley — Research on Competitive Advantage Period (CAP)
- Morningstar — Framework of the 5 Economic Moat types
- Michael Mauboussin — *Measuring the Moat* (ROIC analysis)

---

Built for AI investing agents by [Antoine Ghigny](https://github.com/antoineghigny)
