# Super Stockmarket Skills

A skill set for Gemini CLI designed to provide quantitative and objective investment decisions for the S&P 500 based on fresh market data and macroeconomic indicators.

## Overview

This project provides a **rigorous scoring framework** based on observed market data and macro indicators, moving beyond "intuition" or "forecasts." By classifying the current market environment into one of four "Regimes," it applies specific evaluation logic tailored to the prevailing context, ensuring consistent and attributed investment stances.

## Key Features

- **Autonomous Regime Classification**: Dynamically identifies the market environment (Normal, Geopolitical Shock, Inflation Reacceleration, or Recession Concern).
- **Multi-Source Indicator Analysis**: Integrates data from the S&P 500, VIX, FX (USD/JPY, AUD/JPY), Gold, Crude Oil, US 10Y Yields, HY Spreads, NFCI, and Fear & Greed.
- **Quantitative Scoring**: Applies weighted scores to each indicator, resulting in a total score between -10 and +10 for objective decision-making.
- **Consistency & Contradiction Checks**: Detects market "dislocations" (e.g., divergence between credit and equity markets) to refine the final verdict.
- **Actionable Guidance**: Delivers specific execution steps, including spot-buy sizing, re-evaluation triggers, and falsifiers.

## Repository Structure

```text
.
├── prompts/
│   └── stock-signals.md      # System prompt defining the skill's behavior
└── skills/
    └── stock-signals/
        ├── SKILL.md          # Gemini CLI skill definition
        ├── agents/           # Agent configurations
        └── references/       # In-depth logic and reference documents
            ├── data-sources.md   # Recommended primary and fallback sources
            ├── scorecard.md      # Exact thresholds, weights, and scoring rules
            └── examples.md       # Canonical edge cases for regime precedence
```

## Usage

Register this skill with your Gemini CLI to start using it.

### Installation

```bash
# Register the skill (adjust the path as necessary for your environment)
gemini skill add ./skills/stock-signals
```

### Example Command

Simply ask about the current market stance, and the agent will handle data collection and analysis.

```bash
gemini ask "Is the S&P 500 a buy today?"
```

## The Core Framework

### 1. Regime Classification
The analysis begins by determining the market regime using the following precedence:
- **D. Recession Concern**: Triggered by weak ISM Manufacturing or rising unemployment.
- **C. Inflation Reacceleration**: Triggered by a sharp rise in yields acting as a headwind.
- **B. Geopolitical Shock**: Triggered by event-driven spikes or drops in Oil and Gold.
- **A. Normal**: Default regime where rates and commodities track fundamentals.

### 2. Scoring & Verdicts
Indicators are scored based on their 1-month changes or absolute levels. The final stance is derived from the weighted sum:
- **>= +5.0**: Strong Buy
- **+2.0 to +4.9**: Normal Buy / Keep DCA
- **-1.9 to +1.9**: Neutral / Keep DCA Only
- **-4.9 to -2.0**: Wait / Consider pausing DCA
- **<= -5.0**: Clear Downtrend / Wait

## Important Notes

- **Not Financial Advice**: This tool is for informational purposes only. All investment decisions should be made at your own discretion.
- **Data Freshness**: The framework requires source-attributed and time-stamped data to ensure high-confidence results.
- **Fact-Based**: Scoring is based strictly on *observed facts* and current values, never on subjective intuition or forecasts.
