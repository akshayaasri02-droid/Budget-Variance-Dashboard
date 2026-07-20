# Budget-Variance-Dashboard
# Budget vs Actual Spending Analysis (2021–2023)

A Power BI dashboard I built to analyse budget vs actual spending across six departments over three years. It covers variance by department, a ranked view of the biggest drivers, and a forecast.

## Executive summary

Actual spending was 890M against a budget of 795M, so an overrun of 95M, about 12% over plan. All six departments came in over budget, not just one or two. Marketing had the largest variance at around 19.9M, then HR at 18.1M and Sales at 16.6M.

The thing I found most interesting was how consistent it was. Variance stayed positive in almost every month across all three years. Spending never really dropped back under budget at any point. The forecast suggests this carries on into early 2024.

Because it's a steady pattern and not a one-off spike, I'd read this as a budgeting/planning issue rather than a sudden cost problem. A mid-year reforecast seems sensible, plus closer review of Marketing, HR and Sales since those three make up most of the total variance.

Note: the dataset is synthetic (made for practice), so the numbers aren't from a real company. The approach is the same as I'd use on real data though.

## What's in the dashboard

- KPI cards for total budget, total actual, variance and variance %
- Variance by department, colour coded so over-budget shows red
- A budget status indicator that classifies the position (currently "Significantly Over Budget")
- A top drivers table showing the three departments contributing most to the overrun
- Monthly variance trend with a forecast

## How I built it

The raw file had around 10,000 rows of transaction level data with budget and actual amounts by department, category and region.

I cleaned it in Power Query first, removed the duplicate records, dealt with a few missing values, and pulled month and year out of the date column. I also had to create a proper month-year column, because plotting it by day was far too noisy to see any trend, and using just month names meant all three years got merged together. That part took a few attempts to get right.

For the analysis I used DAX measures rather than calculated columns so everything responds to filters:

- Variance and Variance % as the base measures
- YTD Variance using time intelligence
- Month-over-month variance change
- A budget status measure using SWITCH to classify against thresholds
- A department ranking using RANKX, which drives the top drivers table

The forecast is Power BI's built-in forecasting on the monthly series. Since the data is synthetic there isn't much real seasonality in it, so I've included it more to show the method than to make any claim about an actual trend.

## Tools

Power BI Desktop — Power Query for cleaning, DAX for the measures. Source data was an Excel file.

## What I'd do next

With real data I'd want to add a driver analysis splitting volume vs rate effects, and a drill-through page for each department. This dataset doesn't have a units/quantity column so I couldn't do the volume split properly, and I'd rather leave it out than fake it.iver breakdown separating volume effects from rate effects, and a drill-through page per department for detail. Those need columns this synthetic set doesn't include, so I've left them as next steps rather than forcing them.
