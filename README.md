 Power BI Sales Dashboard

This repository presents an interactive Power BI Dashboard created using the Sales Forecasting Dataset
 from Kaggle.
The dashboard demonstrates data modeling, advanced DAX, and interactive visualization to analyze sales across customers, products, regions, and operations.

 **Interactive Dashboard Link:** [View on Power BI Service](https://app.powerbi.com/reportEmbed?reportId=3e40924e-45ea-41bb-a361-f06d7ed10db6&autoAuth=true&ctid=2d3194e3-1654-46bd-bae2-ad37ba11b0ae)

[Sales Forecasting Dataset (Kaggle)](https://www.kaggle.com/datasets/rohitsahoo/sales-forecasting)


 Disclaimer

The dataset is completely dummy/artificial, provided by Kaggle for training and educational purposes only.

It does not represent real-world sales transactions.

No YoY (Year over Year) or YTD/MTD comparisons were made, since the dataset does not show meaningful differences between years.

 Dashboard Pages
1. Overview Page

KPIs: Total Sales, Orders Count, Customers, Average Order Value (AOV).

Sales Rolling 12M (line chart by Date).

Top 5 States by Sales.

Sales distribution by Segment.

2. Ship & Operations Page

KPIs: Max Ship Days, Min Ship Days, Avg Ship Days, On-Time %.

Sales by Category and Region.

Avg Ship Days trend (by Month & by Ship Mode).

Sales by Ship Days Band (performance distribution).

3. Sales Trend Page

KPIs: Pareto Sales %, Repeat Customers %, Avg Sales per Order, Avg Sales per Customer.

Top 5 Customers with Largest Contribution.

Sales by Region (line chart).

Count of Sales & Orders by Month.

4. Products Page

KPIs: Product Count, Average Sales per Product.

Sales by Sub-Category & by Category.

Top 5 Products by Sales.

Category-wise Sales Distribution.

DAX Measures

Here are the main DAX measures built to support the dashboard:

-- Total Sales
Total Sales = SUM(Orders[Sales])

-- Orders Count
Orders Count = COUNTROWS(Orders)

-- Customers
Customers = DISTINCTCOUNT(Orders[Customer ID])

-- Average Order Value
AOV = [Total Sales] / [Orders Count]

-- Sales Rolling 12M
Sales Rolling 12M =
CALCULATE(
    [Total Sales],
    DATESINPERIOD('Orders_Data'[Date], MAX('Orders_Data'[Date]), -12, MONTH)
)

-- Sales MTD
Sales MTD = TOTALMTD([Total Sales], 'Orders_Data'[Date])

-- Sales YTD
Sales YTD = TOTALYTD([Total Sales], 'Orders_Data'[Date])

-- Sales LY
Sales LY = CALCULATE([Total Sales], SAMEPERIODLASTYEAR('Orders_Data'[Date]))

-- Pareto Sales %
Pareto Sales % =
DIVIDE([Total Sales], CALCULATE([Total Sales], ALL(Orders)))

-- Repeat Customers %
Repeat Customers % =
DIVIDE(
    CALCULATE(DISTINCTCOUNT(Orders[Customer ID]), FILTER(Orders, Orders[Orders Count] > 1)),
    [Customers]
)

-- On-Time %
On-Time % = AVERAGE(Orders[On Time (Flag)])

-- Top N Customers Sales
TopN Customers Sales =
VAR N = SELECTEDVALUE('Top N'[N], 10)
RETURN
CALCULATE(
    [Total Sales],
    KEEPFILTERS(
        TOPN(N, VALUES(Orders[Customer ID]), [Total Sales], DESC)
    )
)

Dashboard Screenshots
<img width="1074" height="1026" alt="image" src="https://github.com/user-attachments/assets/d9ab9cdf-fc83-4077-a7d0-5c9520298fcf" />
<img width="1060" height="1020" alt="image" src="https://github.com/user-attachments/assets/6639394b-1fa1-483c-a48b-ad20b3596eab" />
<img width="1048" height="1008" alt="image" src="https://github.com/user-attachments/assets/64a7bd44-a1ff-4be2-9b86-13ea7126c9ef" />
<img width="1030" height="1012" alt="image" src="https://github.com/user-attachments/assets/6b52fdf4-7795-435d-8eb5-cb1f95b8bc1b" />


Skills Demonstrated

- Power BI Data Modeling
- Advanced DAX (Rolling, TopN, Time Intelligence, Pareto)
- KPI & Metrics Design
- Interactive Dashboard Storytelling
- Performance Optimization (merging visuals, removing redundancies)

How to Use

- Clone this repository:
git clone https://github.com/YourUsername/Sales-Dashboard-PowerBI.git
- Open the .pbix file in Power BI Desktop.
- Connect to the dataset if needed (or download directly from Kaggle).

 This project is a showcase of Power BI + DAX skills using dummy training data from Kaggle.



