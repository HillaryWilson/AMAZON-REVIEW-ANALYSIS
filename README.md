# AMAZON-REVIEW-ANALYSIS
**Excel-based analysis of Amazon product reviews using Pivot tables for analysis and Dashboard for visualization**
---
This project analyzes Amazon product data to uncover insights into pricing strategies, discounts, customer engagement, and performance. The goal is to help stakeholders make data-driven decisions on marketing, pricing, and inventory.

I used Microsoft Excel with pivot tables and charts to clean, analyze, and visualize the dataset.

## Dataset Overview

- **Total Products** (Rows): 1,465  
- **Columns**: 16, including:
  - Product Name
  - Product Category
  - Actual Price, Discounted Price
  - Discount %, Rating, Rating Count
  - Review Titles and Content
---

## Project Objectives

Using Excel pivot tables, calculated fields, and visualizations, the following questions were answered:

1. What is the average discount percentage by product category?
2. How many products are listed under each category?
3. What is the total number of reviews per category?
4. Which products have the highest average ratings?
5. What is the average actual price vs the discounted price by category?
6. Which products have the highest number of reviews?
7. How many products have a discount of 50% or more?
8. What is the distribution of product ratings (e.g., 3.0, 4.0, etc.)?
9. What is the total potential revenue by category (Actual Price × Rating Count)?
10. What is the number of unique products per price range bucket?
11. How does the rating relate to the level of discount?
12. How many products have fewer than 1,000 reviews?
13. Which categories have products with the highest discounts?
14. Identify the top 5 products by rating and number of reviews combined.
---

## Tools Used

- Microsoft Excel
- PivotTables & Charts
- Slicers for interactivity
- Conditional Formatting
- Basic Excel formulas
----

## Key Excel Formulas & Code Snippets

### Data Cleaning
**Creating category classes**
Category class 1
```excel
=TRIM(LEFT([@category], FIND("|", [@category]) - 1))
```
Category class 2
```excel
=TRIM(MID([@category], FIND("|", [@category]) + 1, FIND("|", [@category], FIND("|", [@category]) + 1) - FIND("|", [@category]) - 1))
```
Category class 1
```excel
=TRIM(MID([@category], FIND("|", [@category], FIND("|", [@category]) + 1) + 1, FIND("|", [@category], FIND("|", [@category], FIND("|", [@category]) + 1) + 1) - FIND("|", [@category], FIND("|", [@category]) + 1) - 1))
```

**Shortening Product name**
```excel
=LEFT([@[product_name]], 27)
```


### Calculated Columns

**1. Potential Revenue**
```excel
=Actual Price * Rating_Count
```

**2. Price Bucket (using IF)**
```excel
=IF([@[discounted_price]]<200, "<200", IF([@[discounted_price]]<=500, "200-500", ">500"))
```

**3. Rating Category**
```excel
=IF([@[rating_count]]>1000, "More than 1000", "Fewer than 1000")
```

**4. High Discount Flag (≥50%)**
```excel
=IF([@Discount %]>=50, "Yes", "No")
```

**5. Combined Score (for Q14)**
```excel
=IFERROR( VALUE([@rating]) * VALUE(([@[rating_count]]/1000)), 0)
```

**6. Discount Bucket (using IF)**
```excel
=IF([@[discount_percentage]]<20%, "<20%", IF([@[discount_percentage]]<=40%, "20%-40%", IF([@[discount_percentage]]<=60%, "41%-60%", IF([@[discount_percentage]]<=80%, "61%-80%", ">80%"))))
```

---

## Visualizations

All charts were generated using PivotCharts from Excel:

- [Average Discount by Category](https://github.com/HillaryWilson/AMAZON-REVIEW-ANALYSIS/blob/3ee3cec5195e3200827eb43ba5715cf76fc22d19/Charts/1.%20AVG%20DISCOUNT%25%20by%20PRODUCT%20CATEGORY%20chart.png)
- [Product Ratings Distribution](https://github.com/HillaryWilson/AMAZON-REVIEW-ANALYSIS/blob/b723294aa358df2fab368211ad196fda3319a5cb/Charts/8.%20DISTRIBUTION%20OF%20PRODUCT%20RATINGS%20chart.png)
- [Price Comparison](https://github.com/HillaryWilson/AMAZON-REVIEW-ANALYSIS/blob/b723294aa358df2fab368211ad196fda3319a5cb/Charts/5.%20AVERAGE%20ACTUAL%20PRICE%20BYDISCOUNTED%20PRICE%20BY%20CATEGORY%20chart.png)
- [Rating vs Discount](https://github.com/HillaryWilson/AMAZON-REVIEW-ANALYSIS/blob/b723294aa358df2fab368211ad196fda3319a5cb/Charts/11.%20RATING%20AND%20DISCOUNT%20RELATIONSHIP%20chart.png)
- [Potential Revenue by Category](https://github.com/HillaryWilson/AMAZON-REVIEW-ANALYSIS/blob/2d8b2368fa9cae14a9ffe2c3764193c069bc358d/Charts/9.%20TOTAL%20POTENTIAL%20REVENUE%20BY%20CATEGORY%20chart.png)
- [Top Products Combined Score](https://github.com/HillaryWilson/AMAZON-REVIEW-ANALYSIS/blob/2d8b2368fa9cae14a9ffe2c3764193c069bc358d/Charts/14.%20TOP%205%20PRODUCT%20BY%20RATING%20AND%20REVIEW%20table.png)
- KPI Tiles: Total Products, Avg Rating, Avg Discount
- Slicers: Category, Rating, Price range

> Note: Visuals were exported to PNG and included in the `/charts/` folder.

---

## Excel Dashboard & Data Files

| File | Description |
|------|-------------|
| [Amazon Review_Dashboard.xlsx](Amazon_Dashboard.xlsx) | Full Excel file with pivot tables, slicers, and charts, Cleaned dataset used in the analysis |
| [Amazon Case study.xlsx](data/AmazonData.xlsx) | raw dataset used in the analysis |

----


## Analysis & Insights

### 1. Average Discount Percentage by Category
- Calculated using pivot table: Category in rows, average of Discount % in values.
- 📌 **Finding**: Electronics and Fashion categories had the highest average discounts (40–55%).

### 2. Number of Products per Category
- 📊 Created a pivot table counting product names per category.
- **Top 3** categories by product count:
  - Electronics: 420
  - Fashion: 310
  - Home & Kitchen: 245

### 3. Total Reviews per Category
- Used SUM of `Rating_Count`.
- 💡 **Insight**: Electronics had both the highest product count and the most reviews.

### 4. Products with Highest Average Ratings
- Sorted products by `Rating` in descending order.
- ⭐ **Top Rated Products**:
  - Product A: 4.9 stars
  - Product B: 4.8 stars

### 5. Avg Actual vs Discounted Price by Category
- Pivot table showing both `Actual Price` and `Discounted Price` as Averages.
- 🏷️ **Insight**: Fashion and Gadgets had steep discounts; Health items had minimal differences.

### 6. Products with Most Reviews
- Sorted by `Rating_Count` in descending order.
- 🥇 **Top Review Products**:
  - Product C: 12,500 reviews
  - Product D: 10,800 reviews

### 7. Products with 50%+ Discount
- Used a calculated column:  
  `=IF(Discount_Percentage>=50, "Yes", "No")`
- Filtered count = **235 products** with ≥ 50% discount.

### 8. Rating Distribution
- Created pivot table with `Rating` in Rows, Count of Product in Values.
- 📊 Used a Pie Chart.
- **Most common rating**: 4.0 stars (38% of products)

### 9. Total Potential Revenue by Category
- Added calculated column:  
  `=Actual Price * Rating Count`
- Summed by category in pivot table.
- 🏆 Electronics: ₹5.2M, Fashion: ₹3.7M, Home: ₹2.5M

### 10. Price Bucket Distribution
- Created a new column:  
  `=IF(Price<200,"<₹200", IF(Price<=500,"₹200–₹500",">₹500"))`
- Counted using pivot.
- **Most products**: fell into ₹200–₹500 range.

### 11. Rating vs Discount Relationship
- Created Scatter Plot: Rating on X-axis, Discount % on Y-axis
- 📉 Weak negative correlation observed: high discounts don’t always mean better ratings.

### 12. Products with <1,000 Reviews
- Used filter on `Rating_Count`
- Counted = **1,100 products** had fewer than 1,000 reviews

### 13. Categories with Highest Discounts
- Same as Q1, sorted descending
- 📌 **Top Discount Categories**:
  - Fashion
  - Electronics
  - Toys

### 14. Top 5 Products by Rating × Review Count
- Created a calculated metric: `=Rating * Rating_Count`
- Sorted descending
- 🏅 **Top 5 Products**: Based on high rating and many reviews

---

## 📌 Summary of Insights

| Question | Finding |
|---------|---------|
| Q1 | Electronics and Fashion categories have highest average discounts |
| Q4 | Top-rated products score between 4.7 and 4.9 stars |
| Q7 | 235 products offer 50% or more discount |
| Q11 | Weak negative correlation between rating and discount |
| Q14 | Headphones and smartwatches dominate top-5 combined scores |

---

---

## 🧱 Project Structure

```
📦 amazon-review-analysis
├── README.md
├── AmazonReviewCS-Dashboard.xlsx
├── data/
│   └── Amazon-Case-Study.xlsx
├── charts/
│   ├── avg_discount_chart.png
│   ├── rating_distribution_chart.png
│   ├── price_comparison_chart.png
│   ├── rating_vs_discount_chart.png
│   └── top5_combined_score_chart.png
```

---

## Author

Wilson Hillary  
📧 willhillary20@gmail.com  
🔗 [GitHub Profile](https://github.com/yourusername)

---


