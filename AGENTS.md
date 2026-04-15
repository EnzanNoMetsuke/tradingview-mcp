# AGENTS.md

## Purpose

This project controls TradingView through MCP automation. Safety matters more than speed.

When working with TradingView layouts, treat every chart edit as potentially destructive to a real workflow. Do not assume a successful API response means the correct layout is active.

## TradingView Layout Safety Rules

Only modify the layout explicitly authorized by the user.

For this project, if the user refers to the dedicated AI workspace, the only layout allowed to be modified is `🔬AI` unless the user explicitly authorizes a different layout by name.

Never directly modify any other layout, including `Study: Trend Trader`, unless the user clearly says to do so.

## Required Verification Before Any Chart Edit

Before adding, removing, or changing indicators, drawings, panes, alerts, or layout settings:

1. Switch to the requested layout.
2. Verify the active layout name from the TradingView UI, not only from the MCP `layout_switch` success response.
3. Check for contradictory evidence in the UI, especially the save target or layout label in the top bar.
4. If the UI still references a different layout, stop immediately and do not edit anything.
5. If the active layout is ambiguous, stop and ask the user instead of proceeding.

Do not rely on a single success signal. Confirmation must come from both:

- The layout switch result.
- The visible UI state showing the correct active layout.

## Incident Learning

Past failure mode: the agent called `layout_switch` for `🔬AI`, saw a success response, and proceeded. The UI still showed `Study: Trend Trader` as the active save target. The agent ignored that contradiction and edited the wrong layout.

Preventive rule: contradictory UI evidence always overrides automation success messages.

## Editing Standard

Use the smallest possible change set.

Prefer a compact, non-overlapping swing-trading indicator stack. Avoid indicator clutter and avoid adding multiple studies that answer the same question unless the user explicitly requests it.

When setting up a new trading layout, explain the role of each study before modifying the chart:

- Trend and regime
- Momentum
- Volume confirmation
- Volatility / risk framing

## Fail-Safe Behavior

If there is any uncertainty about which layout is active, do not modify the chart.

If a previous action may have partially changed the wrong layout, disclose that clearly before taking any further action.
