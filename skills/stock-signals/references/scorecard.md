# Stock Signals Scorecard

Use this file for the exact scoring and output rules. Do not paraphrase thresholds from memory.

## Regime Classification

Determine the regime before any scoring.

- `A. Normal`: rates, oil, and gold broadly track fundamentals.
- `B. Geopolitical shock / resolution`: oil and gold are primarily moving on risk events.
- `C. Inflation reacceleration`: rising yields and rising oil are bad news.
- `D. Recession concern`: falling yields are bad news and HY widening matters most.

Precedence:

- When multiple regimes look plausible, use `D > C > B > A`.
- Name the runner-up regime if a lower-priority regime also had meaningful evidence.

Decision rules:

1. Select `D` if `ISM Manufacturing < 48` or unemployment rate is at least `0.3 pp` above 3 months ago.
2. Otherwise, select `C` if the `1M` US 10Y change is `>= +50 bps`.
3. Otherwise, select `B` only when the `1M` oil move is above `+15%` or below `-15%` and recent reporting supports an event-driven explanation.
4. Otherwise, select `A`.

Clarifications:

- A `1M` US 10Y decline by itself does not force `D`. Use `D` only when the recession evidence in rule 1 is present.
- In this scorecard, `1M` for daily market series means approximately 20 trading days, not 30 calendar days.
- For regime `B`, require at least 2 recent, independent reports published within the last 7 calendar days that tie the move to a geopolitical risk event or its resolution.
- If `B` is plausible but the event-driven explanation is weak or mixed, keep `A` and label the geopolitical interpretation as `runner-up` or `inference`.

## Required Lookbacks

For every indicator, collect:

- latest
- 1 week ago
- 1 month ago, approximately 20 trading days
- 3 months ago, approximately 60 trading days

For weekly and monthly macro series, use the nearest published release on or before each comparison point.
Mark non-exact lookbacks as `estimated`.

## Indicator Scoring

### S&P 500 trend, weight `1.0`

- `1M >= +3%` and `3M >= +5%` -> `+1`
- `1M between -3% and +3%` and `3M between -5% and +5%` -> `0`
- `1M <= -3%` or `3M <= -5%` -> `-1`
- Divergence case such as `1M +7%` and `3M -10%` -> mark `V-shaped recovery` and score `0`

### VIX, weight `1.0`

- `<= 15` -> `+1`
- `> 15 and <= 20` -> `+1`
- `> 20 and <= 25` -> `0`
- `> 25 and <= 30` -> `-1`
- `> 30` -> `-2`
- If `VIX < 12`, reduce the score from `+1` to `0`

Note: the `> 30` case is still a numeric `-2` score even if it may later be discussed as a contrarian setup.

### USD/JPY and AUD/JPY, weight `0.5` each, capped at combined `+/-1.0`

Use 1-month change:

- `>= +2%` in the pair, meaning yen weakness -> `+0.5`
- between `-2%` and `+2%` -> `0`
- `<= -2%`, meaning yen strength -> `-0.5`

### Gold, weight `0.5`, regime-dependent

Use 1-month change:

- `>= +3%` -> `rise`
- between `-3%` and `+3%` -> `flat`
- `<= -3%` -> `fall`

- Regime `A`: rise -> `-0.5`; flat -> `0`; fall -> `+0.5`
- Regime `B`: event-driven rise -> `-0.5`; event-resolution fall -> `+0.5`; mixed or unclear -> `0`
- Regime `C` or `D`: exclude from scoring, weight `0`

### Oil, weight `0.5`, regime-dependent

Explain the likely reason for the move in one line.

Use 1-month change:

- `>= +5%` -> `rise`
- between `-5%` and `+5%` -> `flat`
- `<= -5%` -> `fall`

- Regime `A`: rise -> `+0.5`; flat -> `0`; fall -> `-0.5`
- Regime `B`: shock-driven oil spike -> `-0.5`; shock resolution with falling oil -> `+0.5`; flat or unclear -> `0`
- Regime `C`: rise -> `-0.5`; flat -> `0`; fall -> `+0.5`
- Regime `D`: exclude from scoring, weight `0`

### US 10Y Treasury yield, weight `1.0`, regime-dependent

- Regime `A`: lower yield -> `+1`; higher yield -> `-1`
- Regime `B`: exclude from scoring, weight `0`; still use the series for regime selection and contradiction checks
- Regime `C`: lower yield -> `+1`; higher yield -> `-2`
- Regime `D`: lower yield -> `-1`; higher yield -> `+0.5`

Absolute-level adjustment:

Apply this adjustment only when the US 10Y series is actively scored in regimes `A`, `C`, or `D`.

- yield `> 5.0%` -> additional `-1`
- yield `< 3.5%` -> additional `+1`

### HY spread, weight `1.5`

Absolute level first:

- `< 3.0%` -> `+1`, but warn about reversal risk
- `3.0% to 4.0%` -> start from `+1`
- `4.0% to 5.0%` -> `0`
- `5.0% to 7.0%` -> `-1`
- `> 7.0%` -> `-2`

Direction adjustment versus 1 month ago:

- narrowed by at least `20 bps` -> additional `+0.5`
- widened by at least `20 bps` -> additional `-0.5`

### Chicago Fed NFCI, weight `1.5`

- `< -0.5` -> `+2`
- `>= -0.5` and `< 0` -> `+1`
- `>= 0` and `< +0.5` -> `-1`
- `>= +0.5` -> `-2`

### CNN Fear & Greed, weight `0.5`

- `0 to 24` -> `+1`
- `25 to 74` -> `0`
- `75 to 100` -> `-1`

## Final Score Bands

Approximate total range: `-10` to `+10`

- `>= +5.0` -> `strong buy`
- `+2.0 to +4.9` -> `normal buy / keep DCA`
- `-1.9 to +1.9` -> `neutral / keep DCA only`
- `-4.9 to -2.0` -> `wait / consider reducing or pausing DCA`
- `<= -5.0` -> `clear downtrend / wait`

## Contradiction Checks

If any item below triggers, downgrade the final verdict by one band.

1. `VIX < 20` while `NFCI > 0`
2. `S&P 500 1M >= +3%` while HY spreads widened by at least `20 bps` over 1 month
3. `S&P 500 1M >= +3%`, gold `1M >= +3%`, and `VIX 1M <= -10%`
4. `US 10Y 1M <= -25 bps`, `S&P 500 1M >= +3%`, and the selected regime is `A` or `B`
5. `Fear & Greed > 80` and `VIX < 15`

Use the same `1M` convention here as above: approximately 20 trading days for daily market series.

## Execution Mapping

Map the final verdict to action size mechanically:

- `strong buy` -> `推奨アクション: keep DCA + spot buy`; spot-buy size `100%` of the user's normal monthly contribution
- `normal buy / keep DCA` -> `推奨アクション: keep DCA + modest spot buy`; spot-buy size `50%`
- `neutral / keep DCA only` -> `推奨アクション: keep DCA only`; spot-buy size `0%`
- `wait / consider reducing or pausing DCA` -> `推奨アクション: wait on spot buys; DCA policy depends on the user's stated preference`; spot-buy size `0%`
- `clear downtrend / wait` -> `推奨アクション: wait`; spot-buy size `0%`

## Required Output Shape

1. Regime classification: `A/B/C/D` plus 3 evidence lines
2. Indicator table

| Indicator | Current | 1M Ago | Change | Score | Weight | Weighted Score |

3. Total score, rounded to 1 decimal place
4. Consistency-check result
5. Final verdict
6. Confidence: `High`, `Medium`, `Low`
7. Execution guidance:
   - `通常積立額`
   - `推奨アクション`
   - `スポット買い比率`
   - `次回再判定トリガー` with 3 concrete conditions
   - `反証条件` with 3 concrete conditions

## Prohibitions

- No intuition-based scoring
- No forecast-based scoring
- No single-stock discussion
- No converting missing data into sideways or neutral
- No hedged conclusion such as "short term X, medium term Y" that avoids a final stance
