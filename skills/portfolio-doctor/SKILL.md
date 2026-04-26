---
name: portfolio-doctor
description: Portfolio health check focused on risk, correlation, and diversification. Use when a user wants to understand how their holdings interact, identify concentration risks, or simulate how their portfolio would react to macro shifts.
---

# Portfolio Doctor

## Overview

Use this skill to diagnose a list of holdings. While `stock-signals` looks at the market and `stock-deep-dive` looks at companies, `portfolio-doctor` looks at the *structure* of the user's wealth to ensure they aren't accidentally over-exposed to a single factor.

## Workflow

1. **Exposure Mapping:** Categorize each holding by:
   - Sector (e.g., Tech, Healthcare).
   - Asset Class (e.g., Equity, Fixed Income, Crypto).
   - Style (e.g., Value, Growth, Quality).
   - Geography (e.g., US, Emerging Markets).
2. **Correlation Analysis:**
   - Fetch 1-year historical correlations between the top 5 holdings.
   - Identify "Hidden Clusters" (stocks that move together despite being in different sectors).
3. **Risk Assessment:**
   - Calculate portfolio Beta (sensitivity to the S&P 500).
   - Identify "Concentration Risk" (any single position >15% or sector >30%).
   - Identify "Yield Trap" risk (high dividend stocks with deteriorating fundamentals).
4. **Macro Stress Test:** Simulate impact based on current `stock-signals` Regime:
   - If Regime D (Recession), identify which holdings are most vulnerable.
   - If Regime A (Goldilocks), identify which holdings might be "laggards."
5. **Optimization:** Suggest 2-3 specific actions to improve the "Risk-Adjusted Return."

## Required Inputs

- **Holdings List:** Tickers and their percentage weights (or share counts).
- **Risk Tolerance:** (Conservative, Balanced, Aggressive).
- **Primary Goal:** (Capital Appreciation, Income, Preservation).

## Operating Rules

- Focus on *diversification of risk*, not just diversification of names.
- Flag "Wash Sale" risks or tax implications if the user mentions cost basis.
- Be critical of "over-diversification" (holding 50+ stocks that just mimic an index with higher fees/effort).
- If a user has significant cash, treat it as a "negative beta" asset that reduces overall risk.

## Output Requirements

1. **Portfolio Health Score:** A single number (1-100) based on the user's stated goal.
2. **Exposure Sunburst/Table:** Breakdown by Sector and Style.
3. **The "Danger Zone":** Top 3 risks identified (e.g., "Too much exposure to USD/JPY fluctuations").
4. **Correlation Matrix:** Simplified 3x3 or 5x5 grid of the largest holdings.
5. **Dr. Verdict:** Clear advice (e.g., "Trim Tech, Add Defensive," or "Stay the course").
6. **Specific Rebalancing Suggestions:** "Sell X% of [Ticker] to buy [Ticker/ETF]."

## Confidence Heuristic

- **High:** Full weights provided, all tickers recognized, historical price data available.
- **Medium:** Weights are approximate, or some holdings are niche/illiquid.
- **Low:** Missing weights, or portfolio contains many private/non-standard assets.
