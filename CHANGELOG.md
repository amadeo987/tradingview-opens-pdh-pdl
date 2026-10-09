# Changelog

## 1.0.0 - 2026-10-10

- First release.
- Yearly, Monthly, Weekly and Daily Open (labels `yOpen`, `mOpen`, `wOpen`, `DO`), Previous Day High/Low, optional Previous Week and Previous Month High/Low.
- 1 px lines that start on the opening candle (or on the first candle of the previous period) with a short label sitting inside the line.
- Line end: full width or fixed distance; label position: next to the last candle or a fixed offset.
- Small/Medium/Large text size, short or full names, optional price in the label, adjustable colors, line style and width.
- Labels of levels at the same price are merged, for example `wOpen / DO`.
- Labels of nearby levels are moved apart horizontally, with a spacing that follows the zoom level.
- Non-repainting higher-timeframe data (`request.security()` with `lookahead_on` and `[1]`).
