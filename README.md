# Opens & Previous Day H/L for TradingView

`[ad] Opens & Previous Day H/L` is a Pine Script v6 indicator that draws the key reference levels many traders watch:

- **Yearly Open (`yOpen`)**, **Monthly Open (`mOpen`)**, **Weekly Open (`wOpen`)** and **Daily Open (`dOpen`)**
- **Previous Day High / Low (PDH / PDL)**
- optional **Previous Week High / Low (PWH / PWL)** and **Previous Month High / Low (PMH / PML)**

Every level is a thin 1 px line that starts on the candle where its period opened (for previous highs and lows: where the previous period began). A short text label sits inside the line, so the text looks like a gap in the line instead of a banner on top of the chart.

## How it works

- Period opens and previous highs/lows are requested from the higher timeframe with `request.security()` using the `lookahead_on` + `[1]` pattern. Only values that are already final are used, so levels do not repaint: an open is known as soon as its period starts, and a previous high/low comes from the last completed period.
- The label background uses the chart background color, which cuts the line behind the text. This can be switched off.
- Levels that share a price are merged into one label, for example `wOpen / dOpen` on a Monday (the first daily bar of the week has the same open as the week) or `yOpen / mOpen / wOpen / dOpen` on the first trading day of a year.
- Labels of levels that are close to each other would cover one another, so they are moved apart horizontally (to the right with Full width, alternately right and left of the middle with Fixed distance). The spacing is calculated from the visible price range and the number of visible bars, so it follows your zoom level.
- A level is hidden when its period is shorter than the chart timeframe: a weekly chart shows no daily levels, a monthly chart shows only monthly and yearly levels.
- Lines start on the bar where their period began. If the period began before the first loaded candle, the line starts at the first loaded candle (and never more than 4900 bars before the last one); the price is still correct because it comes from the higher timeframe.
- The Data Window lists the current value of every level; those plots never change the price scale.
- All drawing happens on the last bar and reuses a fixed set of ten lines and ten labels, so object counts stay low.

## Settings

**Levels** - switch each of the ten levels on or off. Defaults: yOpen, mOpen, wOpen, dOpen, PDH, PDL on; PWH, PWL, PMH, PML off.

**Lines**
- Line end: `Fixed distance` (default; the line stops a set number of bars after the last candle and the label sits in the middle of that part) or `Full width` (the line runs to the right edge of the chart).
- Fixed distance (bars, default 90), line style (solid, dashed, dotted) and line width (default 1).

**Labels**
- Show labels, text size (Small 8, Medium 10, Large 12; default Medium).
- Short names (`yOpen`, `mOpen`, `wOpen`, `dOpen`, `PDH`, ...) or full names (`Yearly Open`, `Daily Open`, `Prev Day High`, ...).
- Show price in label, in brackets, for example `yOpen (87643.3)` (off by default).
- Cut the line behind the label (on by default).
- Avoid overlapping labels (on by default).
- Label position, used only with the Full width line end: `Next to last candle` (always on screen) or `Fixed offset` with an offset in bars (needs a right margin of at least that many bars).

**Colors** - Yearly Open, Monthly Open, Weekly Open, Daily Open, previous highs and previous lows. Defaults: Yearly, Monthly and Weekly Open share one pink-red, Daily Open is grey, previous highs are red and previous lows are blue. Each color can be changed on its own.

## Where to get it

- TradingView: [[ad] Opens & Previous Day H/L](https://www.tradingview.com/script/bj1IB49A-ad-Opens-Previous-Day-H-L/) (open-source publication, add it to a chart with "Add to favorites" / "Use on chart").
- Source code: this repository.

## Installation

1. Open the Pine Editor in TradingView.
2. Create a new indicator and paste the contents of [`opens-pdh-pdl.pine`](opens-pdh-pdl.pine).
3. Click **Add to chart**.

## Good to know

- The indicator draws levels only; it has no alerts and gives no trade signals. A level is a reference price, not a prediction or advice.
- Daily, weekly, monthly and yearly boundaries follow the symbol's own sessions and time zone, for example 00:00 UTC for crypto on most exchanges.
- Label positions and the fixed line length are measured in bars from the last candle, so the distance on screen depends on your zoom level. Keep a right margin of at least the fixed distance to see the whole line.
- Labels are filled with the chart background and hide whatever is directly behind them, including candles that are close to the last bar.
- The indicator needs the exchange to provide daily, weekly, monthly and yearly data for the symbol.
- Changing the options of an input in a new version can reset that input on charts that already use the indicator.

## Version

1.0.4 - see [CHANGELOG.md](CHANGELOG.md).

## License

Mozilla Public License 2.0, see [LICENSE](LICENSE).

This is an open-source charting tool, not financial advice.
