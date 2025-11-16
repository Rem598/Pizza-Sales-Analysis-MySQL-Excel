# 🍕 Pizza Sales Analysis (MySQL & Excel)

## 🎯 Problem Statement

The goal of this project was to move beyond raw sales metrics to develop a **data-driven strategy for optimizing menu performance and operational efficiency** for a pizza business. The analysis focuses on identifying peak sales periods, best/worst-selling items, and key customer behavior (size, category preferences).

**Tools Used:** **MySQL** (Querying & Aggregation), **Microsoft Excel** (Data Visualization & Dashboard)

---

## 🗃️ Dataset Overview

The dataset contains a year's worth of transactional data. The analysis utilizes these key fields to drive insights:

* **pizza_name:** Standardized pizza name (e.g., "The Classic Deluxe")
* **pizza_category:** Category (e.g., Meat, Veggie, Classic)
* **pizza_size:** Size (Small, Medium, Large)
* **quantity, unit_price, total_price**
* **order_date & order_time:** Crucial for trend and peak-hour analysis.

[Dataset Source: Download from Google Drive](https://drive.google.com/drive/folders/1ecpBALfFUMSK-GOnk-X4nZhC_uK18zih)

---

## 🧠 Detailed SQL for Business KPIs

The core of this project focused on crafting queries to answer strategic business questions, including calculating essential metrics and trends.

### Key Financial Metrics

```sql
-- Total Revenue
SELECT SUM(total_price) AS total_revenue FROM pizza_sales.sales;

-- Average Order Value = Total Revenue / Total Orders
SELECT SUM(total_price) / COUNT(DISTINCT order_id) AS average_order_value FROM pizza_sales.sales;

-- Total Pizzas Sold
SELECT SUM(quantity) AS total_pizza_sold
FROM pizza_sales.sales;

-- Average Pizzas Per Order
SELECT SUM(quantity) / COUNT(DISTINCT order_id) AS avg_pizza_per_order
FROM pizza_sales.sales;


## Operational Efficiency: Daily & Hourly Trends

-- Daily Trend for Orders
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders
FROM pizza_sales.sales
GROUP BY DATENAME(DW, order_date);

## Menu Strategy: Top & Bottom Performers

-- Top 5 Bestselling Pizzas (by volume)
SELECT pizza_name, SUM(quantity) AS total_sold
FROM pizza_sales.sales
GROUP BY pizza_name
ORDER BY total_sold DESC
LIMIT 5;

-- Percentage of Sales by Pizza Category
SELECT pizza_category, 
       SUM(total_price) * 100.0 / (SELECT SUM(total_price) FROM pizza_sales.sales) AS percentage
FROM pizza_sales.sales
GROUP BY pizza_category;


-- Percentage of Sales by Pizza Size
SELECT pizza_size, 
       SUM(total_price) * 100.0 / (SELECT SUM(total_price) FROM pizza_sales.sales) AS percentage
FROM pizza_sales.sales
GROUP BY pizza_size;
```
## 📊 Dashboard & Visualizations
The final analysis was summarized in an Excel dashboard to provide clear, immediate understanding of the results.

Pizza Sales Dashboard Overview
![Dashboard](https://github.com/Rem598/Pizza-Sales-Analysis-MySQL-Excel/blob/main/pizza.jpg)

## 💡 Key Insights & Recommendations
The analysis identified actionable findings that can directly influence menu pricing and resource allocation:

- Revenue Optimization: Large-sized pizzas consistently brought in the highest overall revenue, confirming their importance to the bottom line.

- Menu Strategy: Classic and Supreme categories dominate sales volume, requiring prioritization in ingredient inventory and menu visibility.

- Staffing Efficiency: Analysis of the daily and hourly trend data (included in the full SQL script) allows for optimizing staffing schedules to meet peak demand periods.
