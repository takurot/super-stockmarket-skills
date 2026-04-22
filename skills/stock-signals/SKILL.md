---
name: stock-signals
description: Regime-aware macro scoring for deciding whether the S&P 500 is a buy today using fresh market and macro data. Use when Codex needs to fetch current values for the S&P 500, VIX, FX, gold, oil, Treasury yields, HY spreads, liquidity conditions, and recession gauges; classify the market into one of four regimes; score each signal with fixed thresholds; run contradiction checks; and deliver a source-attributed buy/hold/wait recommendation for US equities.
---

# Stock Signals

## Overview

Use this skill to answer "Is the S&P 500 a buy now?" with a strict, source-attributed framework.
Work from observed data only. Do not add points from intuition, narrative preference, or forecasts.

Read [references/data-sources.md](references/data-sources.md) before collecting data if you need a source map.
Read [references/scorecard.md](references/scorecard.md) for the exact regime rules, precedence, weights, contradictions, action sizing, output contract, and prohibitions.
Read [references/examples.md](references/examples.md) if you need canonical edge cases for regime precedence.

## Workflow

1. Fix the as-of convention before data collection:
   - daily market series: use the most recent completed US market session as the anchor date
   - weekly and monthly macro series: use the latest published release available as of that anchor date
2. Use these standard lookbacks unless a source cadence prevents an exact match:
   - 1 week ago: about 5 trading days for daily market series
   - 1 month ago or `1M`: about 20 trading days for daily market series
   - 3 months ago or `3M`: about 60 trading days for daily market series
   - weekly and monthly macro series: use the nearest published release on or before the anchor-date-equivalent comparison point
3. Collect every required indicator with four timestamps: latest, 1 week ago, 1 month ago, and 3 months ago.
4. Mark any reconstructed or calendar-based approximation as `estimated`; never present it as exact.
5. Record source name and observation date next to every quoted number.
6. Apply cadence-specific freshness checks:
   - daily market series: warn if stale by 2 or more business days versus the anchor date
   - weekly series: warn if older than 10 calendar days
   - monthly series: warn if older than 45 calendar days
7. If a preferred source fails the freshness check, try one fallback source for the same series. If no acceptable fresh reading is available, keep the true date, mark the series as stale, and lower confidence. If the exact concept is unavailable, mark it missing or use an explicitly named proxy.
8. Determine the regime first using the precedence rules in [references/scorecard.md](references/scorecard.md). Do not score indicators before the regime is set.
9. Score each indicator with the exact matrix in [references/scorecard.md](references/scorecard.md).
10. Sum weighted scores, run contradiction checks, and downgrade the final stance by one tier if any contradiction rule triggers.
11. Return the result in the required output order and include explicit confidence.

## Required Inputs

Collect these series unless the user narrows the scope:

- S&P 500
- VIX
- USD/JPY
- AUD/JPY
- Gold
- Crude oil
- US 10Y Treasury yield
- US high-yield spread
- Chicago Fed NFCI
- CNN Fear & Greed
- ISM Manufacturing PMI
- US unemployment rate

If a required series is unavailable, say it is missing, name the proxy if you use one, and explain the impact on confidence.

## Operating Rules

- Prefer current, public, primary sources. Use secondary market-data pages only when a primary source is unavailable or delayed.
- Keep regime selection conservative when the evidence is mixed. If two regimes look plausible, state the selected regime and the runner-up, but still score only the selected regime.
- Treat regime-B oil and gold moves as event-driven only when at least 2 recent, independent reports published within the last 7 calendar days support that interpretation. Otherwise keep `A` and label `B` as `runner-up` or `inference`.
- Say `inference` when you infer the cause from headlines instead of a clearly stated event attribution.
- Treat regime-D yield declines as bearish even if equities have not reacted yet.
- Do not convert missing data into neutral scores.
- Keep `1W` and `3M` observations in the working notes even though the final indicator table only shows `Current` and `1M Ago`.
- Do not infer the user's regular contribution amount. If the baseline monthly amount is unknown, write `通常積立額: 要ユーザー指定`.
- Express the spot-buy suggestion as a percent of the user's normal monthly contribution unless the user specifies another base.
- Use the fixed execution-size mapping in [references/scorecard.md](references/scorecard.md); do not improvise a custom buy size from narrative conviction.

## Output Requirements

Return these sections in this order:

1. Regime verdict with 3 short evidence lines.
2. Indicator table with current value, 1M-ago value, change, score, weight, and weighted score.
3. Total score rounded to 1 decimal place.
4. Consistency-check result with triggered contradictions or `none`.
5. Final stance.
6. Confidence: `High`, `Medium`, or `Low`.
7. Execution guidance:
   - normal monthly contribution
   - recommended action
   - spot-buy sizing as a percent of the normal monthly contribution
   - 3 concrete re-evaluation triggers
   - 3 falsifiers that would overturn the verdict

## Confidence Heuristic

Use `High` when the data set is substantially complete, dates are aligned, no key proxy is needed, and no major contradiction rule triggers.
Use `Medium` when there is limited estimation, one proxy or one stale series, minor date skew, or one notable contradiction.
Use `Low` when key series are missing, multiple proxies are required, date skew is material, or multiple contradictions remain unresolved.
