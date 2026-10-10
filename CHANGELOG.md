# Changelog

## 1.0.4 - 2026-10-10

- Lines never start on the first 3 bars of the loaded history. The chart preview of a publication did not draw a line that began exactly on the first loaded bar (the Yearly Open), although the label was shown.

## 1.0.3 - 2026-10-10

- Line starts are now bar indexes of the chart instead of timestamps: each line begins on the bar where its period started, or on the first loaded bar (at most 4900 bars before the last one) when the period began earlier. This draws long-running levels such as the Yearly Open reliably on every timeframe and in the chart preview of a publication, and avoids TradingView's "too far from the current bar index" error on deep intraday history.

## 1.0.2 - 2026-10-10

- Lines no longer started more than 50 bars before the left edge of the visible chart (replaced in 1.0.3 by bar-index line starts).

## 1.0.1 - 2026-10-10

- Lines now start no earlier than the first loaded candle, so levels whose period began long ago (for example the Yearly Open on an intraday chart) are drawn even when little history is loaded.
- Labels of nearby levels are moved apart by at least 8 bars, so they no longer cover each other when only a few candles are visible.

## 1.0.0 - 2026-10-10

- First release.
- Yearly, Monthly, Weekly and Daily Open (labels `yOpen`, `mOpen`, `wOpen`, `dOpen`), Previous Day High/Low, optional Previous Week and Previous Month High/Low.
- 1 px lines that start on the opening candle (or on the first candle of the previous period) with a short label sitting inside the line.
- Line end: fixed distance (default, 90 bars) or full width; with full width the label sits next to the last candle or at a fixed offset.
- Small/Medium/Large text size (8/10/12, default 10), short or full names, optional price in brackets in the label, adjustable colors, line style and width.
- Labels of levels at the same price are merged, for example `wOpen / dOpen`.
- Labels of nearby levels are moved apart horizontally, with a spacing that follows the zoom level.
- Non-repainting higher-timeframe data (`request.security()` with `lookahead_on` and `[1]`).
