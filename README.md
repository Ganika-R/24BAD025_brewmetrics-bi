# BrewMetrics BI

A version-controlled Power BI analytics solution for BrewMetrics Coffee Co.

## Project Overview

BrewMetrics Coffee Co. is a coffee business operating across multiple cities and store formats. This project develops a Power BI dashboard to analyze sales performance, city-wise performance, product trends, and sales patterns over time.

The project also demonstrates version-controlled BI development using Power BI Project files (`.pbip`), Git, GitHub, and GitHub Copilot-assisted DAX development.

## Data Model

The solution uses a star schema consisting of one fact table and four dimension tables.

### Fact Table
- Fact_Sales

### Dimension Tables
- Dim_Date
- Dim_City
- Dim_Product
- Dim_Store_Format

The Fact_Sales table contains transaction-level sales information, while the dimension tables provide descriptive information used for filtering and analysis.

The main relationships are:

- Dim_Date → Fact_Sales
- Dim_City → Fact_Sales
- Dim_Product → Fact_Sales
- Dim_Store_Format → Fact_Sales

All dimension tables use a one-to-many relationship with Fact_Sales.

## DAX Measures

The following measures were developed with assistance from GitHub Copilot:

1. MoM Sales Growth %
2. Running Total Sales
3. City Sales Rank
4. Average Order Value (AOV)

Copilot's suggestions were reviewed, tested, and reworked where necessary. The development process and corrections are documented in `NOTES.md`.

## Dashboard

The BrewMetrics dashboard contains:

- Total Sales KPI
- Monthly sales trend
- City-wise sales comparison
- City sales ranking
- Year/month filtering
- Interactive slicers
- Drill-down analysis

## Key Insights

- Total sales across the four cities are approximately 3.97M.
- Bengaluru has the highest city-level sales at approximately 1.12M, followed by Chennai at approximately 1.05M.
- Coimbatore has the lowest sales among the four cities at approximately 0.82M, showing a noticeable performance gap between the highest- and lowest-performing cities.
- The monthly sales visual shows variation across the available months, allowing seasonal or monthly sales patterns to be identified.

## Tools Used

- Power BI Desktop
- Power BI Project (`.pbip`)
- Power Query
- DAX
- Git
- GitHub
- Visual Studio Code
- GitHub Copilot

## Project Structure

- `24BAD025_BrewMetrics.pbip` - Power BI project file
- `24BAD025_BrewMetrics.Report` - Report definition
- `24BAD025_BrewMetrics.SemanticModel` - Semantic model definition
- `brewmetrics_sales.csv` - Source dataset
- `NOTES.md` - Copilot-assisted DAX development notes
- `REFLECTION.md` - Project reflection
