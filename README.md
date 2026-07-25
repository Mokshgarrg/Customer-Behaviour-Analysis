# Customer Behavior Dashboard — Retail Shopping Behavior Analysis

### Tools Used: Python (Data Cleaning), Microsoft SQL Server (Querying), Power BI (Dashboard)

## Problem Statement

A retail company wants to understand its customers' shopping behavior — who they are, what they buy, how much they spend, and whether they stay loyal — in order to improve sales, satisfaction, and retention. This project analyzes customer transaction data end-to-end: cleaning and preparing the raw data in Python, answering key business questions with SQL Server queries, and visualizing the results in an interactive Power BI dashboard.

The dataset contains 3,900 customer records with 18 fields, including Age, Gender, Item Purchased, Category, Purchase Amount, Review Rating, Subscription Status, Shipping Type, Discount Applied, Previous Purchases, Payment Method, and Frequency of Purchases.

## Steps Followed

### 1. Data Cleaning & Feature Engineering (Python)
- Loaded the raw CSV (3,900 rows, 18 columns) and inspected structure and data types.
- Imputed missing **Review Rating** values (37 missing) using the median rating within each product category, rather than a single overall median, to preserve category-specific differences.
- Renamed columns to snake_case (e.g., `customer_id`, `purchase_amount`) for consistency across Python and SQL.
- Engineered an **age_group** feature by splitting customer Age into 4 equal-sized quartile bins using `qcut`, labeled Young Adult, Adult, Middle-aged, and Senior.
- Converted the textual **Frequency of Purchases** field (e.g., "Weekly", "Fortnightly") into a numeric scale representing days between purchases, to support quantitative analysis.

### 2. Database Integration & SQL Querying (MS SQL Server)
The cleaned data was loaded into MS SQL Server, and the following business questions were answered:

| # | Business Question | Key Finding |
|---|---|---|
| 1 | Total revenue by male vs. female customers | Male: $157,890 · Female: $75,191 |
| 2 | Customers who used a discount but still spent above average | 839 customers (average purchase amount: $59.76) |
| 3 | Top 5 products by average review rating | Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.79) |
| 4 | Average purchase amount: Standard vs. Express shipping | Express: $60.48 · Standard: $58.46 |
| 5 | Average spend & total revenue: subscribers vs. non-subscribers | Non-subscribers: 2,847 customers, $59.87 avg, $170,436 total · Subscribers: 1,053 customers, $59.49 avg, $62,645 total |
| 6 | Top 5 products by discount-application rate | Hat (50.0%), Sneakers (49.66%), Coat (49.07%), Sweater (48.17%), Pants (47.37%) |
| 7 | Customer segmentation by previous purchases (New / Repeating / Loyal) | Loyal: 3,116 · Repeating: 701 · New: 83 |
| 8 | Top 3 most purchased products within each category | e.g., Clothing → Blouse, Pants, Shirt; Footwear → Sandals, Shoes, Sneakers; Accessories → Jewelry, Belt, Sunglasses; Outerwear → Jacket, Coat |
| 9 | Subscription status among repeat buyers (5+ previous purchases) | No: 2,583 · Yes: 980 |
| 10 | Revenue contribution by age group | Young Adult (18–31): $62,143 · Adult (44–57): $59,197 · Middle-aged (31–44): $55,978 · Senior (57–70): $55,763 |

*(Full SQL scripts for all 10 queries are included in the repository.)*

### 3. Power BI Dashboard
- Built a single-page **Customer Behavior Dashboard** with:
  - **KPI cards**: Number of Customers, Average Purchase Amount, Average Review Rating.
  - **Donut chart**: % of Customers by Subscription Status.
  - **Bar charts**: Revenue by Category and Sales (count) by Category.
  - **Bar charts**: Revenue by Age Group and Sales (count) by Age Group.
  - **Slicers**: Subscription Status, Gender, Category, and Shipping Type for interactive filtering.
- Applied a consistent purple/pink color theme and rounded-panel layout for a clean, professional look.

## Dashboard Screenshot

![Customer Behavior Dashboard]([images/dashboard.png](https://github.com/user-attachments/assets/c051c0f7-6a88-4317-b951-aaa56a2d2ed8)

## Insights

### Overall
- **Total Customers:** 3.9K
- **Average Purchase Amount:** $59.76
- **Average Review Rating:** 3.75
- **27%** of customers are subscribed; **73%** are not.

### Revenue & Sales by Category
Clothing leads in both revenue and units sold, followed by Accessories, Footwear, and Outerwear — indicating Clothing is the core revenue driver and highest-volume category.

### Revenue & Sales by Age Group
Young Adults (18–31) generate the highest revenue and sales volume, followed by Adults (44–57), while Middle-aged (31–44) and Senior (57–70) customers contribute comparably lower but still substantial revenue — showing demand is fairly spread across age groups with a slight skew toward younger customers.

### Gender
Male customers generated significantly more total revenue ($157,890) than female customers ($75,191), despite the dataset containing more male customers overall (2,652 male vs. 1,248 female).

### Loyalty & Subscriptions
The vast majority of customers (3,116 of 3,900) fall into the "Loyal" segment based on purchase history, but only 27% are subscribed — and among repeat buyers with 5+ previous purchases, non-subscribers still outnumber subscribers (2,583 vs. 980). This suggests an opportunity to convert loyal, repeat customers into subscribers.

### Discounts
839 customers used a discount yet still spent above the average purchase amount, showing that discounting doesn't always signal price-sensitive behavior. Products like Hats, Sneakers, and Coats rely most heavily on discounts to sell (highest discount-application rates).

### Shipping
Customers using Express shipping spend slightly more on average ($60.48) than those using Standard shipping ($58.46), suggesting a modest willingness to pay more when opting for faster delivery.
