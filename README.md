# Sample Superstore – Power Query Data Cleaning

This project uses **Power Query (Power BI / Excel)** to clean and transform the classic *Sample Superstore* dataset, preparing it for analysis and dashboard building.

## 📁 Dataset

The raw data (`samplesuperstore`) contains order-level retail transaction records with fields such as:

- Row ID, Order ID, Order Date, Ship Date, Ship Mode
- Customer ID, Customer Name
- Product, Category, Sub-Category
- Sales, Quantity, Discount, Profit
- (and other standard Superstore columns)

## 🖼️ Output Screenshot

Power Query Editor showing the applied steps and cleaned output:


## 🔧 Transformations Applied (Power Query Steps)<img width="609" height="518" alt="download" src="https://github.com/user-attachments/assets/fb4e5366-9152-486a-bef9-3865be731735" />


The following steps were applied in the Power Query Editor:

| Step | Description |
|------|-------------|
| **Source** | Loaded the raw dataset into Power Query |
| **Promoted Headers** | Set the first row as column headers |
| **Changed Column Type** | Set appropriate data types for initial columns |
| **Changed Type** | Adjusted column types further for consistency |
| **Trimmed Text** | Removed extra spaces from text fields |
| **Inserted Year** | Added a new `Year` column extracted from `Order Date` |
| **Inserted Month** | Added a new `Month` column extracted from `Order Date` |
| **Inserted Quarter** | Added a new `Quarter` column using `Date.QuarterOfYear([Order Date])` |

Example M code used for the Quarter column:

```m
= Table.AddColumn(#"Inserted Month", "Quarter", each Date.QuarterOfYear([Order Date]), Int64.Type)
```

## 🎯 Purpose

These date-based columns (Year, Month, Quarter) enable:
- Time-series trend analysis (yearly/quarterly/monthly sales & profit)
- Easier slicing and filtering in Power BI/Excel dashboards
- Seasonality and growth pattern analysis

## 🛠️ Tools Used

- **Power Query Editor** (Power BI Desktop / Excel)
- Applied Steps panel for reproducible, auditable transformations

## 🚀 How to Use

1. Open the `.pbix` (Power BI) or `.xlsx` (Excel) file included in this repo.
2. Go to **Transform Data** to view/edit the Power Query steps.
3. Click **Close & Apply** to load the cleaned data into the model/report.

## 📌 Next Steps

- Build visuals (sales by quarter, profit by category, etc.)
- Create measures using DAX for KPIs
- Publish dashboard to Power BI Service

---

*Feel free to fork this repo and extend the transformations or dashboards.*
