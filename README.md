# -Superstore-Sales-Profit-Analytics
 RLS-Enabled Regional Performance Dashboard | Power BI Capstone Project

 # RLS-Enabled Regional Sales & Profit Analytics

An interactive Power BI dashboard that analyses sales, profit, customers, products and shipping performance for a retail business in India, with **Row-Level Security (RLS)** so each Regional Manager sees only their own region.

## Project overview

- **Domain:** Retail (technology and office supplies)
- **Dataset:** Indian Superstore, 51,284 order lines after cleaning, January 2023 to December 2025
- **Tool:** Microsoft Power BI (Power Query, DAX, Row-Level Security)
- **Headline results:** ₹104.93 Cr sales, ₹12.18 Cr profit, 11.6% margin, 51,236 orders

## Objectives

- Build an interactive Sales & Profit dashboard
- Restrict each Regional Manager to their own region with static RLS
- Use drill-down, drill-through, custom tooltips and bookmarks
- Provide insights across Category, Region, Customer and Product levels

## Repository structure

```
├── dashboard/        Power BI report (.pbix)
├── data/             Source Excel file (Orders and Zone sheets)
├── screenshots/      Dashboard page images
├── docs/             Project report, data dictionary, presentation
└── README.md
```

## Data preparation (Power Query)

- Loaded the Orders and Zone sheets and set correct data types
- Removed the blank Postal Code column and the constant Market column
- Removed 6 invalid rows dated 2012 (51,290 to 51,284 rows)
- Removed duplicates on Row ID and trimmed text columns
- Added a calculated column: `Delivery Days = Duration.Days([Ship Date] - [Order Date])`

## Data model

A **star schema** with `Orders` as the fact table and two dimension tables:

| Relationship | Type |
|---|---|
| Date Table[Date] to Orders[Order Date] | One to many, single direction |
| Zone[Region] to Orders[Region] | One to many, single direction |

The Date Table is a calculated table covering 01-Jan-2023 to 31-Dec-2025.

## DAX measures

```dax
Total Sales       = SUM(Orders[Sales])
Total Profit      = SUM(Orders[Profit])
Profit %          = DIVIDE([Total Profit], [Total Sales], 0)
Total Orders      = DISTINCTCOUNT(Orders[Order ID])
Discount %        = AVERAGE(Orders[Discount])
Avg Delivery Days = AVERAGE(Orders[Delivery Days])
```

## Dashboard pages

| Page | Contents |
|---|---|
| **Sales Overview** | KPI cards, Category and Sub-Category drill-down, sales by state map, monthly trend, top and bottom products |
| **Customer Insights** | Segment contribution, top and bottom customers, region vs customer sales, drill-through to Customer Profile |
| **Product & Discount Impact** | Discount % vs profit scatter plot, product ranking table, delivery time analysis |
| **Region & Manager View** | Region to State to City drill-down, profit by manager, trend by region, bookmark buttons |

## Advanced features

- **Static Row-Level Security:** 5 roles, one per Regional Manager, filtering `Zone[Region Manager]`
- **Bookmarks:** Profit View and Sales View switch the manager chart
- **Drill-through:** Customer Profile and Region Details pages
- **Custom tooltips:** customer and product detail pages on hover
- **Navigation buttons** across all main pages

### RLS roles

| Role | Filter |
|---|---|
| North_Aniket_Sharma | `[Region Manager] = "Aniket Sharma"` |
| East_Yash_Srivastava | `[Region Manager] = "Yash Srivastava"` |
| South_Harish_Deshmukh | `[Region Manager] = "Harish Deshmukh"` |
| West_Pragya_Rathi | `[Region Manager] = "Pragya Rathi"` |
| Central_Nithin_Chaturvedi | `[Region Manager] = "Nithin Chaturvedi"` |

## Key insights

- **Best category:** Technology, with 37.5% of sales and a 14.0% margin; Furniture margin is only 6.9%
- **States:** sales are spread evenly; the top 5 states (Assam, Madhya Pradesh, Kerala, Himachal Pradesh, Tamil Nadu) make only 24% of sales
- **Seasonality:** July to December makes 57% of yearly sales; yearly sales are flat (about -1%)
- **Customers:** Consumer is 51.5% of sales; the top 10 customers make only 2.3% of sales; 84 of 945 customers are unprofitable
- **Discounts:** margin falls from 12.55% (5 to 10% discount) to 10.44% (15 to 20%); Tables - India is the only loss-making product
- **Delivery:** 17.5 days on average in every ship mode; about 19% of orders take over 25 days
- **Regions:** North leads on profit (₹3.69 Cr, manager Aniket Sharma); Central has the best margin (12.6%)

## Business recommendations

1. Grow Technology, which has the best sales and margin
2. Review Furniture and Tables pricing
3. Plan stock and campaigns for August to December
4. Improve delivery performance and audit premium shipping
5. Recover margin in weak territories such as Agra, Hubli, Uttar Pradesh and Karnataka

## Screenshots

| Sales Overview | Customer Insights |
|---|---|
| ![Sales](screenshots/sales.png) | ![Customers](screenshots/customers.png) |

| Product & Discount Impact | Region & Manager View |
|---|---|
| ![Products](screenshots/products.png) | ![Regions](screenshots/regions.png) |

## How to open

1. Install **Power BI Desktop** (free, Windows)
2. Open `dashboard/RLS_Regional_Sales_Profit_Analytics.pbix`
3. If asked, point the data source to `data/Indian_Superstore_Project_Based_Assignment.xlsx`
4. Test security with **Modeling → View as**

## Author

**[Your Name]**
[LinkedIn link] | [Email]
