---
name: stock-deep-dive
description: Bottom-up fundamental analysis for individual equities. Use when the user needs a deep dive into a specific company's financial health, competitive moat, growth catalysts, and valuation (DCF/Multiples) to decide if it is a high-quality investment regardless of macro conditions.
---

# Stock Deep Dive

## Overview

Use this skill to analyze a single ticker in depth. This is a bottom-up complement to `stock-signals`. It focuses on whether a company is a "quality" business and if its current price offers a margin of safety.

## Workflow

1. **Financial Snapshot:** Collect the last 4 quarters and last 3 years of:
   - Revenue growth and Net Income trends.
   - Operating Margins (expanding or contracting?).
   - Free Cash Flow (FCF) and FCF Margin.
   - Debt-to-Equity and Current Ratio.
2. **Moat & Business Model Analysis:**
   - Identify the primary revenue drivers.
   - Evaluate the "Moat" (Switching costs, Network effect, Cost advantage, or Intangibles).
   - Rate the moat: Wide, Narrow, or None.
3. **Valuation:**
   - Calculate or fetch current P/E, P/S, and EV/EBITDA.
   - Compare these to the 5-year historical average and industry peers.
   - Perform a simplified 2-stage DCF if cash flows are predictable.
4. **Risk & Catalysts:**
   - Identify 3 near-term catalysts (e.g., upcoming product launch, earnings).
   - Identify 3 primary risks (e.g., regulatory, competitive, macro sensitivity).
5. **Synthesis:** Combine fundamentals and valuation into a "Quality vs. Price" matrix.

## Required Inputs

- **Ticker Symbol** (e.g., AAPL, TSLA)
- **Investment Horizon** (Default: 3-5 years)
- **Reference Currency** (Default: USD)

## Operating Rules

- Prioritize primary financial statements (SEC filings for US stocks).
- Always compare metrics against at least 2 direct industry competitors.
- If the company is pre-profit, focus on unit economics and cash burn/runway.
- Distinguish between "Cyclical" and "Secular" growth.
- Do not rely solely on "Analyst Price Targets"; build an independent view based on data.

## Output Requirements

1. **Executive Summary:** 1-sentence bull case and 1-sentence bear case.
2. **The "Quality" Scorecard:** (1-10 scale for Profitability, Growth, and Solvency).
3. **Moat Verdict:** Description of the competitive advantage.
4. **Valuation Map:**
   - Current Price vs. Estimated Fair Value.
   - Margin of Safety (%).
5. **Peer Comparison Table:** Ticker vs. Peer A vs. Peer B (Margins, Growth, P/E).
6. **Final Verdict:** Strong Buy / Buy / Hold / Avoid.

## Confidence Heuristic

- **High:** Clean financials, predictable cash flows, clear moat, and peer data available.
- **Medium:** High growth but inconsistent profits, or changing competitive landscape.
- **Low:** Turnaround stories, highly speculative industries, or missing/opaque financial data.
