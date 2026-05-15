# Swing Trading Playbook

## Purpose

This file captures the swing-trading framework configured on the `AI` TradingView layout.

The layout is intentionally compact. It uses:

- `Bollinger Bands 20 SMA 2.75`
- `SMA 200`
- `SMA 50`
- `EMA 21` (hidden)
- `Volume`
- `Visible Range Volume Profile 32 rows, 33% value area`
- `RSI 14`
- `ATR 14`

This is a decision framework, not a prediction engine. The goal is to trade only when trend, momentum, participation, and risk all align.

## Indicator Roles

Each indicator has one job:

- `Bollinger Bands 20 SMA 2.75`: visible short-term pullback, extension, and volatility context
- `SMA 200`: primary regime filter
- `SMA 50`: intermediate trend and major pullback support/resistance
- `EMA 21`: hidden short-term pullback reference
- `Volume`: breakout and reversal confirmation
- `Visible Range Volume Profile 32 rows, 33% value area`: visible price-level participation and supply/demand context
- `RSI 14`: momentum quality
- `ATR 14`: volatility-aware stop and sizing framework

Avoid adding overlapping indicators unless there is a specific reason. More indicators usually add noise rather than clarity.

## Core Framework

Use price plus Bollinger Bands and moving averages to decide whether the symbol is trending cleanly enough to trade. Use RSI to filter out weak momentum setups. Use volume and Visible Range Volume Profile to judge whether the move has real participation. Use ATR to frame stops and position size.

Do not treat the layout as a standalone signal generator. The edge comes from taking only the clean setups and skipping everything else.

## Long Playbook

Take the highest-quality long setups when:

- Price is above the `SMA 200`
- `SMA 50` is above the `SMA 200`
- Price is holding above or reclaiming the Bollinger basis

Preferred long entry patterns:

- Pullback entry: price pulls into the Bollinger basis or `SMA 50`, holds, then closes back up
- Breakout entry: price clears a recent swing high with stronger-than-recent volume

Momentum filter for longs:

- Prefer `RSI` above `50`
- Or `RSI` turning higher through the `45-50` zone

Trade management for longs:

- Initial stop goes below the pullback low or roughly `1.0-1.5 ATR` below entry, whichever is farther
- Trail strong trends against the Bollinger basis
- Trail slower swings against the `SMA 50`
- If price loses the Bollinger basis and momentum weakens, reduce
- If price loses the `SMA 50` decisively, assume the swing is likely ending

## Short Playbook

Take shorts only when:

- Price is below the `SMA 200`
- `SMA 50` is below the `SMA 200`
- Price is failing at the Bollinger basis or `SMA 50`

Preferred short entry patterns:

- Failed rally into the Bollinger basis or `SMA 50`
- Breakdown through clear range support with expanding volume

Momentum filter for shorts:

- Prefer `RSI` below `50`
- Or `RSI` failing at the `50` zone and rolling over

Trade management for shorts:

- Initial stop goes above the bounce high or roughly `1.0-1.5 ATR` above entry
- Trail against the Bollinger basis for strong downside trends
- Use the `SMA 50` for slower-moving swings

## When To Skip

Skip the trade when:

- Bollinger basis, `SMA 50`, and `SMA 200` are tangled together
- Price is far extended from the Bollinger basis or outside the bands
- Volume is weak on a supposed breakout or breakdown
- ATR is expanding sharply because of event risk and the stop becomes too wide

Be extra careful with low-volume names and event-driven names. Earnings, FDA events, macro releases, and guidance can invalidate otherwise clean technical structures.

## Risk Rules

Define risk before entry.

Use:

- `position size = dollars willing to lose / stop distance`

ATR helps standardize stop distance across symbols with different volatility. Do not widen a stop after entry just because price moved against the trade.

## Stricter SOP

This is the one-screen operating procedure for actual trade decisions.

### 1. Regime Check

Long bias only if all are true:

- Price above `SMA 200`
- `SMA 50 > SMA 200`
- Price not breaking down through the Bollinger basis

Short bias only if all are true:

- Price below `SMA 200`
- `SMA 50 < SMA 200`
- Price not reclaiming the Bollinger basis

If neither applies: no trade.

### 2. Structure Check

For longs, accept only:

- Pullback into the Bollinger basis or `SMA 50` with a hold
- Breakout above a clear swing high

For shorts, accept only:

- Failed bounce into the Bollinger basis or `SMA 50`
- Breakdown below clear range support

If the chart is messy or rangebound: no trade.

### 3. Momentum Check

For longs:

- `RSI > 50`, or
- `RSI` turns up through `45-50`

For shorts:

- `RSI < 50`, or
- `RSI` fails at `50` and turns down

If momentum disagrees with the setup: no trade.

### 4. Participation Check

For breakouts and breakdowns, volume should be clearly stronger than nearby bars. Visible Range Volume Profile should not show obvious nearby supply/demand directly against the trade. If price is moving but volume is unimpressive, assume the signal is lower quality.

### 5. Risk Check

Set the stop before entry:

- Longs: below the pullback low or `1.0-1.5 ATR` below entry
- Shorts: above the bounce high or `1.0-1.5 ATR` above entry

Size the position from the stop distance. If the required stop makes the position too small or the risk too large: no trade.

### 6. Entry Rule

Enter only after the signal bar closes or after a clean reclaim/break confirms the setup. Avoid anticipatory entries inside noisy bars unless there is a very specific reason.

### 7. Management Rule

For longs:

- Hold while price respects the Bollinger basis
- Reduce if price closes below the Bollinger basis and momentum weakens
- Exit more aggressively if price loses `SMA 50`

For shorts:

- Hold while price stays below the Bollinger basis
- Reduce if price closes back above the Bollinger basis and momentum improves
- Exit more aggressively if price reclaims `SMA 50`

### 8. Hard No-Trade Conditions

Do not trade when:

- The moving averages are tangled
- The setup is extended far from the Bollinger basis or outside the bands
- The setup is driven by thin volume
- ATR is abnormally expanded around an event
- The trade thesis depends on hope instead of structure

## Practical Notes

This framework works best as a trend-following swing process. It is weaker for pure mean-reversion trades and weaker for trying to call exact bottoms or tops.

The cleanest trades usually come from waiting for alignment, not from forcing activity. Missing a move is usually cheaper than entering a bad one.

## Sources

The framework above is an inference built from TradingView's official indicator documentation:

- [Moving Average](https://www.tradingview.com/support/solutions/43000502589-moving-average/)
- [Simple Moving Average](https://www.tradingview.com/support/solutions/43000696841/)
- [Bollinger Bands](https://www.tradingview.com/support/solutions/43000501840/)
- [Relative Strength Index (RSI)](https://www.tradingview.com/support/solutions/43000502338-relative-strength-index-rsi/)
- [Average True Range (ATR)](https://www.tradingview.com/support/solutions/43000501823-average-true-range-atr/)
- [Volume](https://www.tradingview.com/support/solutions/43000591617-volume/)
- [Visible Range Volume Profile](https://www.tradingview.com/support/solutions/43000703076-visible-range-volume-profile/)
