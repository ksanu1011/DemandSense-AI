# DemandSense AI

## Project Goal
Forecast electricity demand using historical PJM energy consumption data.

---

## Workflow

### Step 1: Data Understanding

Dataset:
- PJM_Load_hourly.csv

Shape:
- Rows: 32,896
- Columns: 2

Columns:
- Datetime
- PJM_Load_MW

### Initial Findings

Data Types:
- Datetime → string
- PJM_Load_MW → float64

Missing Values:
- Datetime: 0
- PJM_Load_MW: 0

Statistics:
- Mean Load: 29,766 MW
- Minimum Load: 17,461 MW
- Maximum Load: 54,030 MW

Observations:
- Dataset is clean.
- No missing values.
- Datetime needs conversion.
- Strong variation in load suggests seasonal behavior### Datetime Conversion

Converted Datetime column from string to datetime64.

Reason:
Time-series forecasting requires datetime-aware operations such as:
- Resampling
- Rolling windows
- Lag features
- Seasonal analysis

Status:
✅ Datetime converted### Date Range

Start Date:
1998-04-01 01:00:00

End Date:
2002-01-01 00:00:00

Coverage:
~3.75 years of hourly electricity demand data.

Why this matters:
- Multiple yearly cycles available
- Seasonal patterns can be detected
- Sufficient history for forecasting## Initial Time Series Visualization

Observations:

- Strong seasonal patterns are visible.
- Demand rises and falls in repeating yearly cycles.
- Peak demand reaches approximately 54,000 MW.
- Base demand remains around 18,000–22,000 MW.
- Several high-demand spikes exist.
- No obvious gaps or missing periods are visible.

Conclusion:

Electricity demand is highly seasonal and suitable for time-series forecasting..