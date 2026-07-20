# Budget-Variance-Dashboard
# Budget vs Actual Spending Analysis (2021–2023)

A Power BI dashboard analysing budget-versus-actual spending across six departments over a three-year period, with variance breakdowns, driver ranking, and a forward forecast.

---

## Executive summary

Across 2021–2023, actual spending came in at 890M against a budget of 795M — an overrun of 95M, or about 12% over plan. The overspend isn't isolated to one area: all six departments finished over budget. Marketing was the biggest contributor at roughly 19.9M of variance, followed by HR (18.1M) and Sales (16.6M).

What stood out most was the consistency. Variance stayed positive in essentially every month across all three years — spending never dipped back under budget, even briefly. The forecast projects this pattern continuing into early 2024.

Given that the overrun is persistent rather than a one-off, I'd treat it as a planning problem more than a one-time cost spike. A mid-year reforecast would be sensible, along with tighter spend review on the three largest drivers (Marketing, HR, Sales), since those three alone account for the bulk of the total variance.

*Note: this dataset is synthetic, generated for analysis practice, so the figures don't reflect a real company. The methods and the dashboard, however, are built the same way I'd approach real budget data.*

---

## What the dashboard shows

- **Headline KPIs** — total budget, total actual, total variance, and variance as a percentage of budget.
- **Variance by department** — a ranked bar chart, colour-coded so anything over budget reads red at a glance.
- **Budget status** — a single indicator that classifies the overall position (here, "Significantly Over Budget") based on the variance percentage.
- **Top drivers** — a ranked table surfacing the three departments contributing most to the overrun.
- **Variance over time** — a monthly trend across the full period, with a forecast extending the line forward.

## How I built it

The data started as ~10,000 transaction-level rows with budget and actual amounts by department, category, and region. I cleaned it in Power Query first — removed duplicate records, handled a handful of missing values, and derived a proper month-level date field so the time series would sort and forecast correctly (the raw daily data was too noisy to read as a trend).

The analysis runs on a set of DAX measures rather than pre-calculated columns, so everything responds to filtering:

- **Variance** and **Variance %** as the base measures.
- **YTD Variance** using time-intelligence, to show accumulation within each year.
- **Month-over-month variance change**, to see whether the gap is widening or narrowing.
- A **budget status** measure using `SWITCH` to classify the position against thresholds.
- A **department ranking** using `RANKX` to drive the top-drivers table automatically.

The forecast uses Power BI's built-in forecasting on the monthly series. As the underlying data is synthetic, the seasonal signal is limited — I've kept the forecast in as a demonstration of the technique rather than a claim about a real trend.

## Tools

Power BI Desktop (Power Query for cleaning, DAX for measures), built from an Excel source file.

## What I'd add next

With real data, the natural extensions would be a driver breakdown separating volume effects from rate effects, and a drill-through page per department for detail. Those need columns this synthetic set doesn't include, so I've left them as next steps rather than forcing them.
What I'd add next

With real data, the natural extensions would be a driver breakdown separating volume effects from rate effects, and a drill-through page per department for detail. Those need columns this synthetic set doesn't include, so I've left them as next steps rather than forcing them.
