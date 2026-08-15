# Ghana SuperMart — Sales Performance Dashboard
A sales performance dashboard built for Ghana SuperMart, an 8-store retail chain across Ghana — transforming a single messy 2023–2024 transaction file into a clean data model and an interactive Power BI report the executive team can use to track revenue, cost, and quantity performance across stores, categories, and products.

## Table of Contents
- [Overview](#overview)
- [Project Brief & Problem Statement](#Project-Brief-&-Problem-Statement)
- [Data Pipeline & Architecture](#Data-Pipeline-&-Architecture)
- [Data Model & Relationships](#Data-Model-&-Relationships)
- [Core DAX Measures & Formulas](#Core-DAX-Measures-&-Formulas)
- [Dashboards & Visualizations](#Dashboards-&-Visualizations)
- [Key Business Insights](#Key-Business-Insights)
- [Strategic Recommendations](#Strategic-Recommendations)
- [Tech Stack](#Tech-Stack)
- Author

## Overview
Ghana SuperMart's leadership handed over a single, massive, unstructured sales file spanning 2023–2024 with no clean way to see how the business was actually performing. 

This project establishes a robust business intelligence framework by structuring flat operational files into an optimized relational Star Schema, applying ETL transformations in Power Query, and building intuitive visuals that enable retail executives to track high-level KPIs, unit volume economics, store performance, and product trends. 

## Project Brief & Problem Statement
### Problem Statement
Ghana SuperMart lacked a centralized view of its financial and sales performance. Decisions were traditionally made based on raw intuition and flat spreadsheets, making it difficult to analyze store efficiency, track category margins, optimize inventory movement, and identify unprofitable operations. 

### Project Objectives
•	Centralize Financial Visibility: Consolidate raw transaction logs to track cumulative revenue, costs, and profit across all retail branches. 
•	Category & Product Intelligence: Isolate top-selling product categories and evaluate exact sales performance and unit volume per product. 
•	Store & Regional Analytics: Analyze branch performance across 8 retail stores in Ghana to identify operational leaders and laggards. 
•	Demographic & Segment Tracking: Profile customer segments and geographic locations to support localized marketing and stocking strategies. 

## Data Pipeline & Architecture
[ Raw Flat File ] ➔ [ Power Query ETL ] ➔ [ Star Schema Data Model ] ➔ [ Interactive Power BI Report ]

## Power Query ETL Steps
The raw transactional dataset (Ghana_SuperMart_Master_Data.csv) was normalized into 1 Fact Table and 3 Dimension Tables using Power Query to enforce data integrity and improve query performance:

customer_dim
<img width="1366" height="768" alt="Customer_dim" src="https://github.com/user-attachments/assets/69d695bf-076d-48da-99a7-bd772a1587fc" />

product_vim
<img width="1366" height="768" alt="Product_dim" src="https://github.com/user-attachments/assets/9f5d2055-0317-43f4-9f17-ea392f3813b9" />

store_dim
<img width="1366" height="768" alt="Store_dim" src="https://github.com/user-attachments/assets/04bcebe7-7f53-4302-982d-041f95e51920" />

fact_sales
<img width="1366" height="768" alt="Fact_sales" src="https://github.com/user-attachments/assets/470f6dc1-386f-4f78-8b48-287ac5bbe46c" />

•	Data Hygiene: Renamed base query to Fact_Sales and duplicated source queries for dimensional breakdown. 
•	Primary Key Enforcement: Applied Remove Duplicates on ID headers across dimension queries (StoreID, ProductID, CustomerID) to guarantee key uniqueness. 
•	Column Selection: Kept specific dimensional attributes using Remove Other Columns for lean dimension tables. 
•	Normalization: Stripped descriptive text columns (StoreName, City, Region, ProductName, Category, CustomerName, etc.) out of Fact_Sales using Remove Columns to lean out the central transaction record. 

## Data Model & Relationships
The model follows a classic Star Schema centered around the transactional fact table, configured with one-to-many (1:*) single-direction filter relationships:

<img width="1010" height="492" alt="GhM Data Model" src="https://github.com/user-attachments/assets/5b38bea8-fdf8-4de7-b78c-4750a5dbc489" />

•	Fact_Sales: Stores central transactional metrics (SalesID, Quantity, TotalAmount, Date) linked via foreign keys (StoreID, ProductID, CustomerID). 
•	Store_dim: Contains store branch lookup attributes (StoreName, City, Region).
•	Product_dim: Details product specifications (ProductName, Category, BasePrice).
•	Customer_dim: Tracks customer attributes (CustomerName, Gender, CustomerSegment).

## Dashboards & Visualizations
## Dashboard — Financial Performance & Category Analysis
A single-page, interactive report featuring dynamic bookmark toggle buttons (Revenue, Orders, Quantity) that allow executives to switch between financial, transaction, and volume perspectives without changing pages.

#### Core Visual Matrix (Dynamic Views):
- Trend Line Chart: Tracks monthly performance over time (e.g., Revenue by Month peaking in April and May, dipping in February).
- Store Ranking Bar Chart: Horizontal bar chart ranking all 8 store locations (led by Kumasi City Mart at GH₵62K, down to Accra Mall SuperMart at GH₵41K).
- Category Breakdown Bar Chart: Compares performance across product categories (Beverages leading at GH₵148K, followed by Apparel at GH₵134K, Food at GH₵88K, Personal Care at GH₵25K, and Snacks at GH₵4K).
- Product Ranking Bar Chart: Detailed bar chart ranking individual items (led by Kente Print Shirt at GH₵134K, Club Beer 6-pack at GH₵53K, and Milo Cocoa Powder at GH₵40K).

## Key Business Insights
### Financial Performance
•	Operating Loss: Total Revenue is GH₵399.3K against Total Cost of GH₵413.5K, generating a net loss of -GH₵14.3K (-3.6% net margin). 
•	Negative Unit Economics: On average, every transaction costs the business GH₵5.68 more than it yields (GH₵159.72 revenue vs. GH₵165.40 cost per order across 2,500 orders). 

### Operational & Inventory Intelligence
- Volume Heavyweights: Beverages and Food dominate retail volume, driving 10.0K out of 13.8K total units sold (72% of total inventory moved).
- Balanced Store Sales: Kumasi City Mart leads store volume (1,888 units), while Accra Mall SuperMart trails lowest (1,451 units) — demonstrating a balanced volume spread across branches.
- Single Product Outlier: The Kente Print Shirt accounts for approximately 96% of Apparel category sales (1,151 units) and is the single highest-selling product across the entire retail chain.
- Local Product Preference: High-volume sales are heavily concentrated in local staple goods including Shito Pepper Sauce, Gari, Palm Oil, Alomo Bitters, and FanMilk Yoghurt.

## Strategic Recommendations
- Audit Cost & Pricing Architecture: Immediately re-examine base supplier prices and retail markups to fix the negative unit margin (-GH₵5.68 per order).
- Leverage High-Volume Staples: Protect supply chains for local staples (Food & Beverages) to retain retail foot traffic.
- Expand Cultural Apparel Line: Investigate adding culturally distinctive products similar to the Kente Print Shirt given its massive market demand.
- Address Capital Branch Performance: Investigate stock availability, pricing, or footfall issues at Accra Mall SuperMart to lift unit sales in the capital. 

## Tech Stack
- Data Transformation: Power Query (M Language)
- Data Modeling & Analytics: Microsoft Power BI Desktop, DAX
- Design & Visual Layout: Dynamic Toggle Buttons, Slicers, Star Schema Layout 
















