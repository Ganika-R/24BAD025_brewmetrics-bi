# Copilot-Assisted DAX Development

## 1. MoM Sales Growth %

### Copilot's initial suggestion

Copilot first suggested a version that calculated CurrentMonthSales using DATEADD with +1 MONTH and PreviousMonthSales using -1 MONTH. It also provided an alternative version that used the current filter context for CurrentSales and DATEADD with -1 MONTH for PreviousSales.

### Correction

The +1 MONTH calculation was not appropriate for the current-month comparison. I used the current filter context for CurrentSales and DATEADD with -1 MONTH for PreviousSales. I also adjusted the date column name to match the actual model column, Dim_Date[date].

### Final measure

MoM Sales Growth % =
VAR CurrentSales = [Total Sales]
VAR PreviousSales =
    CALCULATE(
        [Total Sales],
        DATEADD(Dim_Date[date], -1, MONTH)
    )
RETURN
    DIVIDE(
        CurrentSales - PreviousSales,
        PreviousSales,
        0
    )

### Verification

The measure was tested using the Dim_Date field in a monthly visual to compare the current month's sales with the previous month's sales.

## 2. Running Total Sales

### Copilot's initial suggestion

Copilot suggested using ALLSELECTED(Dim_Date[date]) with FILTER to calculate cumulative sales up to the current date. The suggested measure directly used SUM(Fact_Sales[sales_amount]).

### Correction

I reused the existing [Total Sales] measure instead of repeating the SUM calculation. This makes the measure more consistent with the existing model and avoids duplicating the sales calculation.

### Final measure

Running Total Sales =
CALCULATE(
    [Total Sales],
    FILTER(
        ALLSELECTED(Dim_Date[date]),
        Dim_Date[date] <= MAX(Dim_Date[date])
    )
)

### Verification

The measure was tested in a visual containing Dim_Date[date] and Running Total Sales. The value increased cumulatively as the date progressed.

## 3. City Sales Ranking

### Copilot's initial suggestion

Copilot suggested using RANKX with ALLSELECTED(Dim_City[city]) to rank cities based on [Total Sales]. It used DESC so that the city with the highest sales receives rank 1 and DENSE for consecutive ranking.

### Correction

The suggested RANKX logic was correct for the model. I reused the existing [Total Sales] measure rather than defining SUM(Fact_Sales[sales_amount]) again.

### Final measure

City Sales Rank =
RANKX(
    ALLSELECTED(Dim_City[city]),
    [Total Sales],
    ,
    DESC,
    DENSE
)

### Verification

The measure was tested in a visual containing Dim_City[city], Total Sales, and City Sales Rank. Cities were ranked based on their sales, with rank 1 assigned to the city with the highest sales.

## 4. Average Order Value (AOV)

### Copilot's initial suggestion

Copilot suggested calculating Average Order Value by dividing total sales by the distinct count of sale_id. The suggested measure used SUM(Fact_Sales[sales_amount]) for total sales and DISTINCTCOUNT(Fact_Sales[sale_id]) for the number of orders.

### Correction

The calculation logic was correct. I reused the existing [Total Sales] measure instead of repeating the SUM calculation.

### Final measure

AOV =
DIVIDE(
    [Total Sales],
    DISTINCTCOUNT(Fact_Sales[sale_id])
)

### Verification

The measure was tested in a visual with city and AOV. The value represented the average sales amount per distinct order and changed according to the selected filters.
