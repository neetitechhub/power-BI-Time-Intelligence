# power-BI-Time-Intelligence
power BI Time Intelligence

**PARALLELPERIOD vs DATEINPERIOD vs SAMEPERIODLASTYEAR**

**1. PARALLELPERIOD(<dates>, <number_of_intervals>, <interval>)**

dates: A column containing dates.
number_of_intervals: The number of intervals to move forward or backward. A positive value moves forward, and a negative value moves backward.
interval: The interval by which to shift the dates. Can be DAY, MONTH, QUARTER, or YEAR.

Sales from the same period in the previous year:
PreviousYearSales = 
CALCULATE(
    [TotalSales],
    PARALLELPERIOD(DateTable[Date], -1, YEAR)
)

**2. DATESINPERIOD(<dates>, <start_date>, <number_of_intervals>, <interval>)**
   
dates: A column containing dates.
start_date: The date that represents the start date.
number_of_intervals: The number of intervals to shift. A positive value looks forward, and a negative value looks backward.
interval: The interval by which to shift the dates. Can be DAY, MONTH, QUARTER, or YEAR.

get sales from the last 12 months:
Last12MonthsSales = 
CALCULATE(
    [TotalSales],
    DATESINPERIOD(DateTable[Date], MAX(DateTable[Date]), -12, MONTH)
)

**3. SAMEPERIODLASTYEAR(<dates>)**

get sales from the same period in the previous year:
PreviousYearSales = 
CALCULATE(
    [TotalSales],
    SAMEPERIODLASTYEAR(DateTable[Date])
)

--------------------------------------------------------------------------------------------------------------------------------------------
Key Differences :

**PARALLELPERIOD:**
Allows shifting by various intervals (day, month, quarter, year).
Useful for comparing specific periods, such as this quarter last year or this month last year.
Flexible in terms of intervals and the number of periods to shift.

**DATESINPERIOD:**
Returns a continuous range of dates starting from a specific date.
Useful for rolling periods, like the last 7 days, last 30 days, or last 12 months.
Requires a start date and can look forward or backward for a specified number of intervals.

**SAMEPERIODLASTYEAR:**
Specifically returns the same period (days, months, quarters) from the previous year.
Simpler syntax for comparing the same period in the previous year.
Less flexible compared to PARALLELPERIOD as it only works for year-over-year comparisons.

**Use Cases :**
PARALLELPERIOD: Ideal for flexible period-over-period comparisons, such as this quarter vs. the same quarter last year, or this month vs. the same month last year.
DATESINPERIOD: Best for creating rolling windows, such as the last 12 months, last 30 days, or last 7 days from a specific date.
SAMEPERIODLASTYEAR: Simplest way to perform year-over-year comparisons, useful when you need to compare metrics from the exact same period in the previous year without additional flexibility.
