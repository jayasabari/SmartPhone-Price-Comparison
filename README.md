# 📱 Smartphone Price Comparison
 Power BI + SQL Data Analysis Project

## 📌 Project Information

| Item | Details |
|---|---|
| **Project Title** | Smartphone Price Comparison |
| **Industry** | Consumer Electronics / Smartphone Retail (India) |
| **Dataset Name** | `smartphone_price_comparision_edited.csv` |
| **Dataset Source** | Smartphone Price Comparison dataset |
| **Database Name** | `smartphone` |
| **Table Name** | `smartphone_price_comparison` (the table loaded into Power BI) |

**Problem Statement**

The Indian smartphone market has many brands, models, price points and retail channels. Buyers, retailers and brand managers need a clear, data-backed view of how brands compare on price, discount, customer rating and sales volume, and how these vary by city, retailer and specification. Without a consolidated view, pricing and stocking decisions rely on guesswork.

**Project Objectives**

- Compare smartphone brands on selling price, MRP, discount and customer rating.
- Identify the best-selling brands, cities, retailers and launch years by units sold.
- Understand how operating system, RAM and other specifications relate to price and sales.
- Build an interactive Power BI dashboard so stakeholders can filter and explore the data themselves.

**Proposed Solution / Business Questions**

Clean and analyse the data with SQL, then model and visualise it in Power BI. The project aims to answer:

1. Which brands sell the most units, and what is each brand's share of total units?
2. How do average selling price and average discount differ across brands?
3. Which cities and retailers contribute the most units?
4. How do customer ratings vary by brand, launch year and city?
5. How does price vary with RAM and operating system?
6. Is there a visible relationship between price, rating and units sold?

---

## 🛠️ Tools & Technologies

- **MySQL** – database setup and SQL analysis
- **SQL** – data cleaning, transformation and analysis queries
- **Power BI Desktop** – data modeling and dashboard development
- **DAX** – measures such as Total Units Sold, Average Selling Price, Average Customer Rating and Average Discount %
- **CSV** – source data format

---

## 📖 Project Overview

This project analyses smartphone pricing and sales in the **consumer electronics / smartphone retail** industry. The dataset covers 10 brands, 80 models, 10 Indian cities and 6 retail channels, with prices in INR.

The goal is to turn raw product and sales records into insight about pricing, discounting, customer satisfaction and demand. **SQL (MySQL)** is used to store, clean and query the data. **Power BI** is used to model the data and build an interactive, four-page dashboard on top of it.

The expected business value is a clearer, shared view of the market. Retailers can see which brands and channels drive volume. Brands can benchmark price, discount and rating against competitors. Buyers can compare options. The findings describe this dataset only and are not claims about the real market.

---

## 🎯 Project Objectives

- Analyse brand-wise sales volume and market share.
- Compare average selling price and discount across brands.
- Evaluate customer ratings by brand, launch year and city.
- Study sales by city, retailer, operating system and launch year.
- Examine the effect of RAM on selling price.
- Deliver an interactive Power BI dashboard with slicers and KPIs.

---

## 🗂️ Dataset Information

| Property | Value |
|---|---|
| **Rows** | 5,000 |
| **Columns** | 20 |
| **Missing values** | None |
| **Duplicate Product IDs** | None |
| **Brands / Models** | 10 brands / 80 models (8 models per brand) |
| **Cities / Retailers / Colors** | 10 / 6 / 9 |
| **Launch years** | 2022 – 2026 |
| **Currency** | Indian Rupee (INR) |

**Columns**

| Column | Description |
|---|---|
| `Product_ID` | Unique product identifier (PHN00001 – PHN05000) |
| `Brand` | Smartphone brand (Samsung, Xiaomi, Apple, OnePlus, Vivo, Realme, OPPO, Motorola, Google, Nothing) |
| `Model` | Phone model name |
| `Launch_Year` | Year of launch |
| `Operating_System` | Android or iOS |
| `Network_Type` | Network capability flag (Yes / No) |
| `RAM_GB` | RAM size in GB (4 – 24) |
| `Storage_GB` | Internal storage in GB (64 – 1024) |
| `Battery_mAh` | Battery capacity (3,000 – 6,000 mAh) |
| `Screen_Size_Inches` | Display size (6.1 – 6.9 in) |
| `Rear_Camera_MP` | Rear camera resolution (8 – 200 MP) |
| `MRP_INR` | Maximum retail price |
| `Selling_Price_INR` | Actual selling price |
| `Discount_Percent` | Discount offered (0 – 30 %) |
| `Customer_Rating` | Customer rating (2.5 – 5.0) |
| `Color` | Phone colour |
| `Retailer` | Sales channel (Amazon India, Flipkart, Croma, Reliance Digital, Brand Store, Local Retailer) |
| `City` | City of sale |
| `Units_Sold` | Units sold (1 – 500 per record) |
| `Warranty_Months` | Warranty period in months (6 – 24) |

---

## 🔄 Project Workflow

**Industry Selection → Problem Identification → Dataset Collection → MySQL Database Setup → Data Cleaning & Transformation Using SQL → SQL Data Analysis → Power BI Data Modeling → Dashboard Development → Insights & Recommendations**

---

## 🧮 SQL Analysis

**Database setup (`SQL/smartphone_comparision_SQL.sql`)**

```sql
create database smartphone;
use smartphone;

select * from smartphone_price_comparison;
```

- A MySQL database named `smartphone` is created and selected.
- The dataset is stored in the table `smartphone_price_comparison`, and `SELECT *` is used to verify that the data loaded correctly.

**SQL concepts for further analysis on this table:** `SELECT`, `WHERE`, `GROUP BY`, `ORDER BY`, aggregate functions (`SUM`, `AVG`, `COUNT`), and window functions (`RANK`).

```sql
-- Total units sold and market share by brand
SELECT Brand,
       SUM(Units_Sold) AS total_units,
       ROUND(SUM(Units_Sold) * 100.0 / SUM(SUM(Units_Sold)) OVER (), 2) AS share_pct
FROM smartphone_price_comparison
GROUP BY Brand
ORDER BY total_units DESC;

-- Average selling price, discount and rating by brand
SELECT Brand,
       ROUND(AVG(Selling_Price_INR), 2) AS avg_price,
       ROUND(AVG(Discount_Percent), 2)  AS avg_discount,
       ROUND(AVG(Customer_Rating), 2)   AS avg_rating
FROM smartphone_price_comparison
GROUP BY Brand
ORDER BY avg_price DESC;

-- Units sold by city
SELECT City, SUM(Units_Sold) AS total_units
FROM smartphone_price_comparison
GROUP BY City
ORDER BY total_units DESC;
```

> The three queries above are the analysis queries behind the dashboard's brand, price and city views. Add them to your SQL file if you ran them.

---

## 📊 Power BI Dashboard

The report (`PowerBI/smartphone_price_comparision.pbix`) has **4 pages**, each with a title banner, custom icons, and a sunset smartphone background image. It is built on one data table (`smartphone_price_comparison`) plus a measures table (`Dax functions`).

**Data model & DAX**

- Data loaded from the cleaned CSV into a single table, plus a dedicated measures table named `Dax functions`.
- DAX measures used in the visuals: **Total Units Sold**, **Average Selling Price**, **Average Customer Rating**, **Average Discount %**.

**Dashboard pages and visuals**

| Page | Visuals |
|---|---|
| **1. Market Overview** | Four KPI cards by brand (Total Units Sold, Average Selling Price, Average Customer Rating, Average Discount %); column chart of units by brand; donut chart of average selling price by brand; bar chart of units by operating system; dropdown slicers for **City**, **Brand** and **Color** |
| **2. Sales Performance** | Cards for total units sold and average selling price; pie chart of units by brand; stacked column chart of units by retailer and brand; bar chart of units by city; **Year** tile slicer (2022 – 2026) |
| **3. Pricing and Discount** | Bar chart of average selling price by brand; pie chart of average selling price by RAM (GB); combo chart of average discount % (columns) and total units sold (line) by brand; table of Brand, Model, Sum of MRP, Average Selling Price and Average Discount % |
| **4. Product Specs and Customer Rating** | Scatter chart of average selling price vs. average customer rating by brand (bubble size = units sold); card for average customer rating; matrix of average rating by brand and launch year; table of customer rating by city; brand tile slicer |

**Key features:** interactive slicers and cross-filtering, KPI cards, custom icons and shapes, and a consistent layout across all four pages.

---

## 🔍 Data Analysis & Visualization

- **KPI Analysis** – total units, average price, rating and discount.
- **Comparison Analysis** – brand vs. brand on price, discount, rating and units.
- **Category-wise Analysis** – by operating system, RAM, retailer and colour.
- **Time-based Analysis** – units and ratings by launch year.
- **Relationship Analysis** – rating vs. price vs. units (scatter chart).
- **Distribution Analysis** – share of units by brand and share of price by RAM.

---

**Recommendations (based on the above)**

- Stock depth on Samsung, Xiaomi and Apple models, and on 8 GB and 12 GB variants, given where unit volume concentrates.
- Since ratings and discounts barely differ between brands, differentiation in this dataset comes mainly from price tier and volume rather than satisfaction or discount depth.
- Investigate lower-volume cities such as Delhi for growth potential.

---

## 🖼️ Power BI Dashboard Screenshots

### 1. Market Overview

![Market Overview](Visualizations/market_overview.png)

### 2. Sales Performance

![Sales Performance](Visualizations/sales_performance.png)

### 3. Pricing and Discount

![Pricing and Discount](Visualizations/pricing_and_discount.png)

### 4. Product Specs and Customer Rating

![Product Specs and Customer Rating](Visualizations/product_specs_and_customer_rating.png)

---

## 📁 Project Folder Structure

```text
Smartphone_Price_Comparison/
│
├── README.md
│
├── Dataset/
│   ├── Original.xlsx
│   └── smartphone_price_comparision_edited.csv
│
├── SQL/
│   └── smartphone_comparision_SQL.sql
│
├── PowerBI/
│   └── smartphone_price_comparision.pbix
│
└── Visualizations/
    ├── market_overview.png
    ├── sales_performance.png
    ├── pricing_and_discount.png
    └── product_specs_and_customer_rating.png
```

---

## 👤 Author

| | |
|---|---|
| **Name** | JAYASABARI |
| **Student ID** | AF05321014 |
| **Organization** | Anudip Foundation |
| **Course** | DBA_AI |
| **Batch Code** | ANP-D7635 |
