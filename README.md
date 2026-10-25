# Sales Performance Dashboard | Power BI

An interactive Power BI dashboard that analyses sales revenue and quantity across markets, customers and products from **2017 to 2020**, built on a star-schema data model with DAX measures for currency conversion.

![Dashboard Preview](screenshots/dashboard.png)
<img width="904" height="507" alt="Screenshot (14)" src="https://github.com/user-attachments/assets/301ab127-7298-43b2-ab18-55d4a425452a" />


---

## Business Questions Answered

- What is the total revenue and total quantity sold?
- Which markets (cities) generate the most revenue and volume?
- Which customers contribute the most to revenue?
- Which products sell the best?
- How do sales trend over time (year, quarter, month, day)?

---

## Tools Used

| Tool | Purpose |
|------|---------|
| Excel | Source data (5 sheets) |
| Power Query | Loading and cleaning data |
| Power BI Desktop | Data modelling and dashboard design |
| DAX | Measures, including currency conversion |

---

## Dataset

Source file: `sales_.xlsx`

| Table | Type | Rows | Description |
|-------|------|------|-------------|
| `transactions` | Fact | ~150,000 | Order date, product, customer, market, quantity, sales amount, currency |
| `customers` | Dimension | 38 | Customer code, name, type (Brick & Mortar / E-Commerce) |
| `markets` | Dimension | 17 | Market code, city name, zone (North / South / Central) |
| `products` | Dimension | 279 | Product code, product type (Own Brand / Distribution) |
| `date` | Dimension | ~1,100 | Date, year, month name |

**Time period:** October 2017 to June 2020
**Markets covered:** Chennai, Mumbai, Delhi NCR, Bengaluru, Hyderabad, Kochi, Lucknow and others across India

---

## Data Model

Star schema: the `transactions` fact table is connected to the `customers`, `markets`, `products` and `date` dimension tables. All measures are kept in a separate `BaseMeasure` table.

---

## DAX Measures

Measures are stored in the `BaseMeasure` table:

- **Revenue**: total sales amount, with USD transactions converted to INR so all values are in one currency
- **Sales Qty**: total quantity sold

```dax

Revenue = 
SUMX(
    transactions,
    IF(transactions[currency] = "USD",
        transactions[sales_amount] * 75,   -- replace with your conversion rate
        transactions[sales_amount])
)

Sales Qty = SUM(transactions[sales_qty])
```


---

## Dashboard Features

- **KPI cards:** Total Revenue and Total Sales Quantity
- **Revenue by Market:** bar chart, sorted highest to lowest
- **Sales Quantity by Market:** bar chart
- **Revenue by Customer:** bar chart
- **Revenue by Product:** bar chart
- **Revenue Trend:** line chart with drill-down from Year to Quarter, Month and Day
- **Year slicers:** filter the whole page by year

---

## Data Quality Notes

While working with the data, I noticed and handled these issues:

- Hidden carriage-return characters (`\r`) in some text columns, such as currency and product type
- About 1,600 transactions with zero or negative sales amounts
- A small number of transactions recorded in USD, mixed with INR
- Non-Indian market entries (New York, Paris) and a duplicate market name (Bhopal under two codes)

---

## Key Insights


1. **Top market:** [Market name] generates [X]% of total revenue.
2. **Top customer:** [Customer name] is the largest contributor.
3. **Trend:** Revenue [grew / declined] between [year] and [year].
4. **Product mix:** [Insight about top products].

---

## How to Open This Project

1. Download `Sales_Dashboard.pbix` from this repository.
2. Open it in **Power BI Desktop** (free from the Microsoft Store).
3. If prompted, update the data source path to the location of `sales_.xlsx` on your computer (Home → Transform data → Data source settings).

---

## Repository Structure

```
├── README.md
├── data/
│   └── sales_.xlsx
├── powerbi/
│   └── Sales_Dashboard.pbix
└── screenshots/
    └── dashboard.png
```

---

## What I Learned

- Building a star-schema data model in Power BI
- Writing DAX measures for currency conversion
- Designing a clean, interactive dashboard with drill-down and slicers
- Spotting and handling data quality issues before reporting

---

## Contact

Utsavi Saxena
LinkedIn: www.linkedin.com/in/utsavisaxena 
Email: utsavisaxena@gmail.com
