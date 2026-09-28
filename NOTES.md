# Copilot-Assisted DAX Development

## 1. MoM Sales Growth %

### Copilot's initial suggestion
Copilot first suggested calculating CurrentMonthSales using DATEADD with +1 MONTH and PreviousMonthSales using -1 MONTH.

### Correction
The +1 MONTH calculation was not appropriate for the current-month comparison. I used the current filter context for CurrentSales and DATEADD with -1 MONTH for PreviousSales.

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
