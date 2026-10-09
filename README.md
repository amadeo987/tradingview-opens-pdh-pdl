# Opens & Previous Day H/L for TradingView

`[ad] Opens & Previous Day H/L` is a Pine Script v6 indicator that draws the key reference levels many traders watch:

- **Yearly Open (YO)**, **Monthly Open (MO)**, **Weekly Open (WO)** and **Daily Open (DO)**
- **Previous Day High / Low (PDH / PDL)**
- optional **Previous Week High / Low (PWH / PWL)** and **Previous Month High / Low (PMH / PML)**

Every level is a thin 1 px line that starts on the candle where its period opened (for previous highs and lows: where the previous period began). A short text label sits inside the line, so the text looks like a gap in the line instead of a banner on top of the chart.

## How it works

- Period opens and previous highs/lows are requested from the higher timeframe with `request.security()` using the `lookahead_on` + `[1]` pattern. Only values that are already final are used, so levels do not repaint: an open is known as soon as its period starts, and a previous high/low comes from the last completed period.
- The label background uses the chart background color, which cuts the line behind the text. This can be switched off.
- Levels that share a price are merged into one label, for example `WO / DO` on a Monday (the first daily bar of the week has the same open as the week) or `YO / MO / WO / DO` on the first trading day of a year.
- A level is hidden when its period is shorter than the chart timeframe: a weekly chart shows no daily levels, a monthly chart shows only monthly and yearly levels.
- If a period started before the first loaded candle, the line begins at the left edge of the loaded history; the price is still correct because it comes from the higher timeframe.
- The Data Window lists the current value of every level; those plots never change the price scale.
- All drawing happens on the last bar and reuses a fixed set of ten lines and ten labels, so object counts stay low.

## Settings

**Levels** - switch each of the ten levels on or off. Defaults: YO, MO, WO, DO, PDH, PDL on; PWH, PWL, PMH, PML off.

**Lines**
- Line end: `Full width` (the line runs to the right edge of the chart) or `Fixed distance` (it stops a set number of bars after the last candle; the label sits in the middle of that part).
- Fixed distance (bars), line style (solid, dashed, dotted) and line width (default 1).

**Labels**
- Show labels, text size (Small 9, Medium 11, Large 14; default Medium).
- Short names (`DO`, `PDH`, ...) or full names (`Daily Open`, `Prev Day High`, ...).
- Show price in label (off by default).
- Cut the line behind the label (on by default).
- Label position: `Next to last candle` (always on screen) or `Fixed offset` with an offset in bars (needs a right margin of at least that many bars).

**Colors** - Yearly Open, Monthly Open, Weekly Open, Daily Open, previous highs and previous lows. Defaults are orange, pink-red, white, grey, red and blue. The white Weekly Open is easy to read on dark and beige charts; change it if your chart background is white.

## Installation

1. Open the Pine Editor in TradingView.
2. Create a new indicator and paste the contents of [`opens-pdh-pdl.pine`](opens-pdh-pdl.pine).
3. Click **Add to chart**.

## Good to know

- The indicator draws levels only; it has no alerts and gives no trade signals. A level is a reference price, not a prediction or advice.
- Daily, weekly, monthly and yearly boundaries follow the symbol's own sessions and time zone, for example 00:00 UTC for crypto on most exchanges.
- Label positions are measured in bars from the last candle, so the distance on screen depends on your zoom level.
- Labels are filled with the chart background and hide whatever is directly behind them, including candles that are close to the last bar.
- The indicator needs the exchange to provide daily, weekly, monthly and yearly data for the symbol.
- Changing the options of an input in a new version can reset that input on charts that already use the indicator.

## Version

1.0.0 - see [CHANGELOG.md](CHANGELOG.md).

## License

Mozilla Public License 2.0, see [LICENSE](LICENSE).

This is an open-source charting tool, not financial advice.
