Sales Data Analysis (Superstore EDA)

Exploratory Data Analysis (EDA) on the Sample Superstore dataset using Python, Pandas, Matplotlib, and Seaborn. The notebook (sales.ipynb) covers data loading, cleaning, feature engineering, and visualizations to uncover trends in sales, profit, and discounting behavior. 

📌 Overview

This notebook covers a complete EDA workflow on retail sales data:

Loading and inspecting the dataset

Data cleaning

Parsing Order Date and Ship Date

Feature engineering using Delivery Days

Checking missing values and unique categories

Aggregating total sales by product category

Visualizing sales by category

Analyzing profit by category

Examining the impact of discounts on profit

Correlation analysis using a heatmap 


📂 Project Structure

├── sales.ipynb              # Main analysis notebook
├── samplesuperstore.csv     # Dataset
└── README.md

🗂️ Dataset

The notebook expects a CSV file named:

samplesuperstore.csv

For Google Colab:

/content/samplesuperstore.csv

If running locally:

df = pd.read_csv("samplesuperstore.csv")

Typical columns include:

Order Date
Ship Date
Category
Sub-Category
Sales
Profit
Discount
Region

🛠️ Tech Stack / Requirements

Python 3.x

Pandas

NumPy

Matplotlib

Seaborn


Install Dependencies

pip install pandas numpy matplotlib seaborn jupyter

🚀 Usage

1. Clone the repository

git clone https://github.com/<your-username>/<repo-name>.git
cd <repo-name>

2. Place the dataset

Place:

samplesuperstore.csv

in the appropriate directory.

3. Launch Jupyter Notebook

jupyter notebook sales.ipynb

4. Run all cells

Run all notebook cells to reproduce the analysis. 

📊 Key Steps in the Notebook

Step	Description

Data Loading	Reads the CSV into a Pandas DataFrame
Data Inspection	Uses head(), info(), shape, describe()
Date Parsing	Converts Order Date and Ship Date to datetime
Feature Engineering	Calculates Delivery Days
Data Quality Check	Checks unique categories and null values
Sales Aggregation	Calculates total sales by Category
Sales Visualization	Creates bar charts and histograms
Profit Analysis	Uses bar plots and box plots
Discount Impact	Creates a discount vs. profit scatter plot
Correlation Analysis	Creates a correlation matrix and heatmap


📈 Example: Code & Output

1. Load and Inspect the Data

import pandas as pd

df = pd.read_csv("/content/samplesuperstore.csv")
df.info()

Output

<class 'pandas.DataFrame'>
RangeIndex: 200 entries, 0 to 199
Data columns (total 5 columns):
 #   Column      Non-Null Count  Dtype
---  ------      --------------  -----
 0   Order Date  200 non-null    object
 1   Ship Date   200 non-null    object
 2   Category    200 non-null    object
 3   Region      200 non-null    object
 4   Sales       200 non-null    float64

dtypes: float64(1), object(4)
memory usage: 7.9 KB

2. Parse Dates and Create Delivery Days

df['Order Date'] = pd.to_datetime(
    df['Order Date'],
    format="mixed"
)

df['Ship Date'] = pd.to_datetime(
    df['Ship Date'],
    format="mixed"
)

df['Delivery Days'] = (
    df['Ship Date'] - df['Order Date']
).dt.days

df.head()

Output

Order Date  Ship Date         Category          Region   Sales  Delivery Days
0 2023-01-01 2023-01-05        Furniture          West    164.34       4
1 2023-01-04 2023-01-09        Office Supplies    West     68.55       5
2 2023-01-07 2023-01-10        Office Supplies    West     51.77       3
3 2023-01-10 2023-01-15        Furniture          South   265.61       5
4 2023-01-13 2023-01-18        Office Supplies    East    193.44       5

3. Aggregate Sales by Category

category_sales = df.groupby('Category')['Sales'].sum()

category_sales

Output

Category
Furniture          15419.67
Office Supplies    28919.40
Technology         18756.14
Name: Sales, dtype: float64

4. Visualize Sales

import matplotlib.pyplot as plt

category_sales.plot(
    kind='bar',
    figsize=(8,5)
)

plt.title("Sales by Category")
plt.ylabel("Total Sales")
plt.show()

Sales Distribution

import seaborn as sns

plt.figure(figsize=(8,5))

sns.histplot(
    df['Sales'],
    bins=30
)

plt.title("Sales Distribution")
plt.show()

The histogram shows the distribution of individual sale amounts, with most sales concentrated at lower values and a longer tail of higher-value orders. 

5. Profit by Category

sns.barplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit by Category")
plt.show()

sns.boxplot(
    data=df,
    x="Category",
    y="Profit"
)

plt.title("Profit Variation Across Categories")
plt.show()

These plots show profitability and the variation of profit values across categories, including outliers. 

6. Discount vs. Profit

sns.scatterplot(
    data=df,
    x="Discount",
    y="Profit"
)

plt.title("Impact of Discount on Profit")
plt.show()

This helps visualize whether higher discounts are associated with reduced or negative profit. 

7. Correlation Heatmap

numeric_df = df.select_dtypes(include="number")

corr = numeric_df.corr()

sns.heatmap(
    corr,
    annot=True
)

plt.title("Correlation Heatmap")
plt.show()

The heatmap shows relationships between numeric features such as Sales, Profit, Discount, and Quantity. 

📈 Key Insights

Identifies product categories that generate the most sales and profit.

Shows how discounts can reduce or reverse profit margins.

Highlights relationships between sales, profit, discount, and quantity.

Identifies categories with high profit variation and outliers. 


🤝 Contributing

Feel free to fork the repository and submit a pull request with improvements or additional analysis, such as:

Regional breakdowns

Time-series trends

Customer segmentation 


📄 License

This project is open source and available under the MIT License.
