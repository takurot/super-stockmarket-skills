# Stock Signals Examples

Use these examples only to resolve edge cases in regime precedence. They do not replace the scorecard.

## Example 1: Recession concern beats geopolitical shock

- Oil 1M: `+18%`
- US 10Y 1M: `-38 bps`
- ISM Manufacturing: `47.2`
- Unemployment rate versus 3 months ago: `+0.4 pp`
- HY spread: `+35 bps`

Expected regime: `D`
Runner-up: `B`
Reason: recession evidence has higher precedence than event-driven oil moves.

## Example 2: Inflation reacceleration beats geopolitical shock

- Oil 1M: `+19%`
- US 10Y 1M: `+61 bps`
- ISM Manufacturing: `49.8`
- Unemployment rate versus 3 months ago: `+0.1 pp`

Expected regime: `C`
Runner-up: `B`
Reason: rising yields with no recession trigger take precedence over the geopolitical interpretation.

## Example 3: Large yield decline without recession evidence stays out of regime D

- Oil 1M: `-4%`
- US 10Y 1M: `-54 bps`
- ISM Manufacturing: `49.5`
- Unemployment rate versus 3 months ago: `+0.1 pp`
- HY spread: `-12 bps`

Expected regime: `A`
Runner-up: `none`
Reason: a large yield decline alone is not enough for regime `D`; recession evidence must be present.
