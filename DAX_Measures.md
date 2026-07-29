# DAX Measures Documentation

This document contains all DAX measures used in the Power BI dashboard for the `atlantic_music_data` dataset.

---

## 1. Total Unique Songs

Counts the exact number of distinct tracks on the chart, ensuring duplicates aren't counted twice.

```dax
Total Unique Songs = 
DISTINCTCOUNT('atlantic_music_data'[song])
```

**Formatting:** Whole Number

---

## 2. Total Unique Artists

Counts the exact number of distinct artists appearing on the chart.

```dax
Total Unique Artists = 
DISTINCTCOUNT('atlantic_music_data'[artist])
```

**Formatting:** Whole Number

---

## 3. Average Rank

Calculates the mean chart position. Invert this on your line chart so that a lower number (e.g., Rank 1) shows at the top.

```dax
Average Rank = 
AVERAGE('atlantic_music_data'[position])
```

**Formatting:** Decimal Number (2 decimal places)

---

## 4. Average Popularity

Averages the 0–100 popularity score assigned by the platform.

```dax
Average Popularity = 
AVERAGE('atlantic_music_data'[popularity])
```

**Formatting:** Decimal Number (2 decimal places)

---

## 5. Days on Chart

Calculates the total number of unique days a specific song or artist has appeared on the playlist. This is the measure used in the Filter pane for "Top N" logic.

```dax
Days on Chart = 
DISTINCTCOUNT('atlantic_music_data'[date])
```

**Formatting:** Whole Number

---

## 6. Rank Volatility (Stability Index)

Measures how much a song's rank bounces around. A lower score means the song is stable at its current rank; a higher score means it is highly volatile.

```dax
Rank Volatility = 
STDEV.P('atlantic_music_data'[position])
```

**Formatting:** Decimal Number (1–2 decimal places)

---

## 7. Explicit Content Share %

Calculates the percentage of tracks flagged as explicit compared to the total number of tracks.

```dax
Explicit Content % = 
VAR ExplicitCount = CALCULATE(
    COUNTROWS('atlantic_music_data'), 
    'atlantic_music_data'[is_explicit] == TRUE()
)
VAR TotalCount = COUNTROWS('atlantic_music_data')
RETURN
DIVIDE(ExplicitCount, TotalCount, 0)
```

**Formatting:** Percentage (1–2 decimal places)

---

## Summary Table

| # | Measure Name | Type | Formatting |
|---|---|---|---|
| 1 | Total Unique Songs | DISTINCTCOUNT | Whole Number |
| 2 | Total Unique Artists | DISTINCTCOUNT | Whole Number |
| 3 | Average Rank | AVERAGE | Decimal (2 dp) |
| 4 | Average Popularity | AVERAGE | Decimal (2 dp) |
| 5 | Days on Chart | DISTINCTCOUNT | Whole Number |
| 6 | Rank Volatility | STDEV.P | Decimal (1-2 dp) |
| 7 | Explicit Content % | CALCULATE + DIVIDE | Percentage |

---

*Table: `atlantic_music_data`*
