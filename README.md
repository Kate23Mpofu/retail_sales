# 🛒 Retail Sales Data Analysis

A full end-to-end data analysis project covering data cleaning and interactive Power BI dashboards, built on a synthetic retail sales dataset of 76,500 rows.

---

## 📌 Project Overview

This project simulates a real-world data analyst workflow:

1. **Raw messy data** → clean, analysis-ready dataset
2. **Excel** for data cleaning and transformation
3. **Power BI** for interactive dashboards and visual storytelling

The dataset represents retail transactions across 10 South African cities, 7 product categories, and 3 years (2022–2024).

---

## 🗂️ Repository Structure
 
```
retail-sales-analysis/
│
├── power BI/
│   ├── [retail_sales_visualizations.pbit]             # Power BI dashboard file
│   └── [Dashboard screenshots]            # Screenshots of each dashboard page
│
├── retail_sales_analysis.xls              # Excel analysis file
├── retail_sales_cleaned.xls               # Cleaned dataset
├── retail_sales_messy.csv                 # Original raw dataset 
├── Retail_Sales_Findings_Report.pdf      # Report with findings
└── README.md
```
 
---

## 🧹 Data Cleaning (Excel)

The raw dataset contained **12+ types of data quality issues**, all resolved in Excel before loading into Power BI.

| Issue | Volume | Fix Applied |
|---|---|---|
| Duplicate rows | ~1,500 | Removed, kept first occurrence |
| Missing values | 4,500–7,500 per column | Replaced with `N/A` or `Unknown` |
| Mixed category casing | ~14% of rows | Standardised to Title Case |
| Gender typos (`M`, `FEMALE`, `N/A`) | ~4% of rows | Mapped to canonical values |
| Mixed date formats | ~9% of rows | Standardised to `dd/mm/yyyy` |
| Invalid dates (`00/00/0000`, future) | ~500 rows | Replaced with `N/A` |
| Negative/zero quantities & prices | ~2% of rows | Nullified |
| Currency prefix in total (`R99.99`) | ~2% of rows | Stripped to numeric |
| Ages & ratings out of valid range | ~3–5% of rows | Replaced with `N/A` |
| City/region mismatches | ~3% of rows | Re-derived from city lookup |
| Trailing whitespace | ~4–8% of rows | Trimmed |
| total_amount formula mismatches | ~4% of rows | Recalculated |

### Date Column
The date column was the most complex. It contained three coexisting formats introduced by Excel's auto-parsing. The cleaning formula used:

```excel
=IF(TRIM(Q2)="not a date","N/A",IF(TRIM(Q2)="N/A","N/A",IF(TRIM(Q2)="","N/A",
  IF(ISNUMBER(Q2),
    IF(OR(TEXT(Q2,"dd/mm/yyyy")="00/00/0000",VALUE(LEFT(TEXT(Q2,"dd/mm/yyyy"),2))>31,
       VALUE(MID(TEXT(Q2,"dd/mm/yyyy"),4,2))>12,VALUE(RIGHT(TEXT(Q2,"dd/mm/yyyy"),4))>2026),
    "N/A",TEXT(Q2,"dd/mm/yyyy")),
    IF(OR(TRIM(Q2)="00/00/0000",VALUE(LEFT(TRIM(Q2),2))>31,
       VALUE(MID(TRIM(Q2),4,2))>12,VALUE(RIGHT(TRIM(Q2),4))>2026),
    "N/A",TRIM(Q2))))))
```

After standardisation, **Text to Columns** was used to convert text dates into proper Excel date serials, enabling `DAY()`, `MONTH()`, `YEAR()` and `TEXT(...,"dddd")` extraction.

---

## 📊 Power BI Dashboard

The dashboard is structured across **2 pages**:

### Page 1 — Sales Overview
- 📈 Total Revenue by Month (line chart)
- 📊 Top Categories By Orders (bar chart)
- 🗺️ Revenue by Region (map)
- 🏆 Sales Performance vs Sales Quality by Rep (line & clustered column chart)
- KPI Cards: Total Revenue | Total Transactions | Avg Order Value | Avg Rating

### Page 2 — Customer & Operations
- 👥 Age Group vs Average Spend
- 🔄 Return Rate by Category
- ⚤ Gender vs Average Spend
- 💳 Payment Method Split (donut)
- 📅 Revenue by Day of Week

---

## 💡 Key Business Questions Answered

1. What is the total revenue trend month over month?
2. Which product category generates the most revenue?
3. Which age group spends the most on average?
4. Which region has the highest return rate?
5. What is the most popular payment method?
6. Which day of the week has the most transactions?
7. Is there a gender difference in average spend?
8. Which category has the highest return rate?

---

## 🔍 Key Findings

> See the full `Retail_Sales_Findings_Report.docx` for detailed findings.

- **Sports** was the best-performing product category
- **Eastern Cape** generated the most revenue across all cities
- The **18–24 age group** had the highest spent
- **Tuesday** was the busiest transaction day of the week
- Return rates were highest in **Toys**, suggesting a need for quality review

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Microsoft Excel | Data cleaning and transformation |
| Power BI Desktop | Interactive dashboards and visualisation |

---

## 📁 Dataset

The dataset was synthetically generated to simulate a realistic messy retail environment. It is **not real customer data**.

- **Rows:** 76,500
- **Columns:** 19
- **Period:** January 2022 – December 2024
- **Geography:** South Africa (10 cities, 9 provinces)

---

## 👤 Author

**Tendai**
[https://www.linkedin.com/in/tendai-teremuka-235693273/]
The project is not perfect because I am still learning.
