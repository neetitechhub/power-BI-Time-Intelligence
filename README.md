# power-BI-Time-Intelligence
power BI Time Intelligence

**PARALLELPERIOD vs DATEINPERIOD vs SAMEPERIODLASTYEAR vs DATESBETWEEN vs DATE ADD**

**1. PARALLELPERIOD(<Dates>, <Number of Intervals>, <Interval>)**

it is used to return a table that contains a column of dates that represent a parallel period in a previous or future time period relative to the given date column.

**dates:** A column containing dates.

**number_of_intervals:** The number of intervals to move forward or backward. A positive value moves forward, and a negative value moves backward.

**interval:** The interval by which to shift the dates. Can be DAY, MONTH, QUARTER, or YEAR.

Sales from the same period in the previous year:

PreviousYearSales = 
CALCULATE(
    [TotalSales],
    PARALLELPERIOD(DateTable[Date], -1, YEAR)
)

**2. DATEINPERIOD(<Dates>, <StartDate>, <NumberOfIntervals>, <Interval>)**

it returns a single-column table of dates shifted from the first date in the given dates column. It returns all the dates in a period, based on a specified date, number of intervals, and interval type.

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

**Key Differences**

**Context:**

PARALLELPERIOD is used to compare parallel periods. For example, comparing this year to the same period last year.
DATESINPERIOD is used to retrieve a range of dates based on a specific start date and interval. For example, getting the last 30 days from a specific date.

**Behavior:**

**PARALLELPERIOD** returns dates in the same period (e.g., same months, same days) shifted by a specified number of intervals.

**DATESINPERIOD** returns a continuous range of dates starting from a specified date and includes a specified number of intervals.

**Use Cases**

**PARALLELPERIOD:** Useful for year-over-year (YoY), quarter-over-quarter (QoQ), or month-over-month (MoM) comparisons.

**DATESINPERIOD:** Useful for rolling periods like the last 7 days, last 30 days, last 12 months, etc.

**3. SAMEPERIODLASTYEAR(<dates>)**

It shifts the context to the exact same period in the previous year. It’s particularly useful for year-over-year comparisons.

get sales from the same period in the previous year:

PreviousYearSales = 
CALCULATE(
    [TotalSales],
    SAMEPERIODLASTYEAR(DateTable[Date])
)

**4.DATESBETWEEN**
It is used to return a table containing a contiguous set of dates that are between the specified start and end dates. This function is useful for creating custom date ranges that can be used in various calculations and analyses.

**DATESBETWEEN(<dates>, <start_date>, <end_date>)**

**dates:** A column containing dates.

**start_date:** The start date.

**end_date:** The end date.

Get sales between two specific dates:

SalesBetweenDates = 
CALCULATE(
    [TotalSales],
    DATESBETWEEN(DateTable[Date], DATE(2023, 1, 1), DATE(2023, 12, 31))
)

**5.DATEADD**

The DATEADD function in DAX is used to shift a set of dates by a specified number of intervals. It can move the dates forward or backward in time and is commonly used for time intelligence calculations.

DATEADD(<dates>, <number_of_intervals>, <interval>)

**dates:** A column containing dates.

**number_of_intervals:** The number of intervals to shift the dates. A positive value moves forward in time, and a negative value moves backward in time.

**interval:** The interval to shift by. This can be DAY, MONTH, QUARTER, or YEAR.

**Examples:**
1. Comparing Sales to the Same Period Last Month
2. Comparing Sales to the Same Period Last Quarter

PreviousMonthSales = 
CALCULATE(
    [TotalSales],
    DATEADD(DateTable[Date], -1, MONTH)
)

PreviousQuarterSales = 
CALCULATE(
    [TotalSales],
    DATEADD(DateTable[Date], -1, QUARTER)
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

**DATESBETWEEN:**  Returns all dates within the specified start and end dates.

**Use Cases :**

**PARALLELPERIOD:** Ideal for flexible period-over-period comparisons, such as this quarter vs. the same quarter last year, or this month vs. the same month last year.

**DATESINPERIOD:** Best for creating rolling windows, such as the last 12 months, last 30 days, or last 7 days from a specific date.

**SAMEPERIODLASTYEAR:** Simplest way to perform year-over-year comparisons, useful when you need to compare metrics from the exact same period in the previous year without additional flexibility.

**DATESBETWEEN:** Use Case: Fixed periods, like the sales between two specific dates.

**DATEAD:** used in visuals to compare current performance against the previous month, quarter, or year, providing valuable insights for analysis.
