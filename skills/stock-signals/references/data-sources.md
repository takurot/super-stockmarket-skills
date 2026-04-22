# Data Sources

Use current, public data and cite both source name and observation date for every number.

## Preferred Source Map

| Series | Preferred sources | Notes |
| --- | --- | --- |
| S&P 500 | finance market data page, exchange summary page | Use index level, not ETF proxy, unless the index series is unavailable. |
| VIX | Cboe or finance market data page | Use spot VIX level. |
| USD/JPY | finance FX page | Use spot or widely quoted interbank reference. |
| AUD/JPY | finance FX page | Same handling as USD/JPY. |
| Gold | finance commodity page or CME summary | Prefer spot gold or front liquid benchmark, but keep the choice consistent. |
| Crude oil | finance commodity page, CME, or EIA-linked market page | State whether you used WTI or Brent. |
| US 10Y Treasury yield | U.S. Treasury or FRED | Prefer the benchmark 10Y constant maturity or official Treasury yield. |
| HY spread | FRED public HY OAS series or equivalent public spread source | Name the exact HY proxy if the canonical series is unavailable. |
| Chicago Fed NFCI | Chicago Fed | Weekly series; if the latest reading lags market data, flag the date skew. |
| CNN Fear & Greed | CNN | Use the published index level. If CNN is unavailable, use a reputable secondary source that explicitly quotes the CNN reading on the same observation date and label it as a proxy. |
| ISM Manufacturing PMI | ISM | Monthly release; carry forward the latest published level with its release date. |
| US unemployment rate | BLS or FRED | Use headline unemployment rate and compare to 3 months ago in percentage points. |

## Collection Notes

- When only monthly or weekly data exist, keep the latest published value and label the older comparison points as `estimated` only if you interpolate or approximate them.
- When the same concept exists in multiple public forms, prefer the source with stable dates and explicit methodology over a prettier chart.
- When data dates differ materially, preserve the true dates instead of forcing synchronization.
- If a preferred source is stale beyond the skill threshold, try one fallback source for the same concept before accepting the stale reading.
- If an important series is unavailable, use the nearest public proxy and say why it is acceptable.
- Do not switch concepts just to avoid a missing series. For example, do not replace spot VIX with a futures term structure or replace the CNN Fear & Greed index with a different sentiment index unless the substitution is explicitly labeled as a proxy.
- For reconstructed crosses such as `AUD/JPY`, prefer a direct quote. If you must derive it from `AUD/USD` and `USD/JPY`, label the result as `estimated`.
