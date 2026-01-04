                                         📊 Full-Cycle Data Warehouse & Analytics Engineering

This project implements a professional Medallion Architecture to integrate and analyze fragmented data from CRM and ERP systems. It covers the entire lifecycle: from raw file ingestion to advanced analytical Business insights.

🏗️ 1. High-Level Architecture
The system architecture ensures data reliability and scalability through a multi-layered approach.

The Medallion Framework:
🥉 Bronze Layer (Raw Data): Ingests raw CSV files from decentralized folders. Uses Batch Processing and Truncate & Insert to preserve a "Source of Truth" with No Transformations.
🥈 Silver Layer (Cleaned): The transformation engine where raw data is cast into structured tables, cleansed, and standardized.
🥇 Gold Layer (Business-Ready): Surfaced via SQL Views in a Star Schema format, optimized for high-performance consumption.

🧬 2. Data Integration & Lineage
Successful consolidation of cross-functional siloes into a unified analytical environment.

Entity Consolidation Logic:
Customer 360: Merges basic CRM info with ERP-sourced birthdates (erp_cust_az12) and geography (erp_loc_a101).
Product Hierarchy: Enriches CRM product data with ERP category classifications (erp_px_cat_g1v2).
Sales Fact: Centralizes transactional records from crm_sales_details.

⚙️ 3. Exhaustive Data Transformation Process
I implemented a comprehensive suite of transformation techniques to ensure data integrity.

Transformation Deep-Dive
Data Cleansing: * Deduplication: Removing redundant records.
Data Filtering: Isolating relevant business records.
Outlier Detection: Identifying statistical anomalies.
Handling Missing/Invalid Values: Implemented logic to treat NULLs or incorrect entries.
Handling Unwanted Spaces: Trimming and cleaning string data.
Data Type Casting: Ensuring strict schema enforcement.
Normalization & Standardization: Uniform formatting for dates, currencies, and naming conventions.
Data Enrichment: Adding derived columns and calculating business-specific metrics.
Data Integration: Linking disparate keys between CRM and ERP systems.
Business Rules & Logic: Applying complex filtering and conditional logic.
Data Aggregations: Creating pre-calculated summaries for reporting efficiency.


🥇 4. Data Modeling (Sales Data Mart)
The Gold Layer is modeled as a Star Schema to provide a robust foundation for analytics.
It is the business-level data representation, structured to support analytical and reporting use cases. It consists of **dimension tables** and **fact tables** for specific business metrics.


gold.fact_sales: The transaction hub with Foreign Keys to dimensions.
- **Purpose:** Stores transactional sales data for analytical purposes.
- **Columns:**
```
| Column Name     | Data Type     | Description                                                                                   |
|-----------------|---------------|-----------------------------------------------------------------------------------------------|
| order_number    | NVARCHAR(50)  | A unique alphanumeric identifier for each sales order (e.g., 'SO54496').                      |
| product_key     | INT           | Surrogate key linking the order to the product dimension table.                               |
| customer_key    | INT           | Surrogate key linking the order to the customer dimension table.                              |
| order_date      | DATE          | The date when the order was placed.                                                           |
| shipping_date   | DATE          | The date when the order was shipped to the customer.                                          |
| due_date        | DATE          | The date when the order payment was due.                                                      |
| sales_amount    | INT           | The total monetary value of the sale for the line item, in whole currency units (e.g., 25).   |
| quantity        | INT           | The number of units of the product ordered for the line item (e.g., 1).                       |
| price           | INT           | The price per unit of the product for the line item, in whole currency units (e.g., 25).      |
```


gold.dim_customers: A comprehensive dimension including marital status, gender, and geographic attributes.
- **Purpose:** Stores customer details enriched with demographic and geographic data.
- **Columns:**
```
| Column Name      | Data Type     | Description                                                                                   |
|------------------|---------------|-----------------------------------------------------------------------------------------------|
| customer_key     | INT           | Surrogate key uniquely identifying each customer record in the dimension table.               |
| customer_id      | INT           | Unique numerical identifier assigned to each customer.                                        |
| customer_number  | NVARCHAR(50)  | Alphanumeric identifier representing the customer, used for tracking and referencing.         |
| first_name       | NVARCHAR(50)  | The customer's first name, as recorded in the system.                                         |
| last_name        | NVARCHAR(50)  | The customer's last name or family name.                                                     |
| country          | NVARCHAR(50)  | The country of residence for the customer (e.g., 'Australia').                               |
| marital_status   | NVARCHAR(50)  | The marital status of the customer (e.g., 'Married', 'Single').                              |
| gender           | NVARCHAR(50)  | The gender of the customer (e.g., 'Male', 'Female', 'n/a').                                  |
| birthdate        | DATE          | The date of birth of the customer, formatted as YYYY-MM-DD (e.g., 1971-10-06).               |
| create_date      | DATE          | The date and time when the customer record was created in the system|
```


gold.dim_products: A structured hierarchy including category, subcategory, and maintenance status.
- **Purpose:** Provides information about the products and their attributes.
- **Columns:**
```
| Column Name         | Data Type     | Description                                                                                   |
|---------------------|---------------|-----------------------------------------------------------------------------------------------|
| product_key         | INT           | Surrogate key uniquely identifying each product record in the product dimension table.         |
| product_id          | INT           | A unique identifier assigned to the product for internal tracking and referencing.            |
| product_number      | NVARCHAR(50)  | A structured alphanumeric code representing the product, often used for categorization or inventory. |
| product_name        | NVARCHAR(50)  | Descriptive name of the product, including key details such as type, color, and size.         |
| category_id         | NVARCHAR(50)  | A unique identifier for the product's category, linking to its high-level classification.     |
| category            | NVARCHAR(50)  | The broader classification of the product (e.g., Bikes, Components) to group related items.  |
| subcategory         | NVARCHAR(50)  | A more detailed classification of the product within the category, such as product type.      |
| maintenance_required| NVARCHAR(50)  | Indicates whether the product requires maintenance (e.g., 'Yes', 'No').                       |
| cost                | INT           | The cost or base price of the product, measured in monetary units.                            |
| product_line        | NVARCHAR(50)  | The specific product line or series to which the product belongs (e.g., Road, Mountain).      |
| start_date          | DATE          | The date when the product became available for sale or use, stored in|
```

📉 5. Comprehensive Data Analytics Process
The project transitions from engineering to insights through a two-phase analytical roadmap.

Phase I: Exploratory Data Analysis (EDA)
1. Understanding data health and baseline metrics:
2. Database Exploration: Assessing the overall structure and volume.
3. Dimensions Exploration: Validating attribute distributions.
4. Date Exploration: Analyzing business history.
5. Measures Exploration: Identifying "Big Numbers" like total revenue.
6. Magnitude: Visualizing volume and scale.
7. Ranking: Identifying Top N vs. Bottom N performers (Customers and Products).

Phase II: Advanced Analytics
Leveraging the curated data for strategic decision-making: 
7. Change-Over-Time: Detailed trend analysis and growth tracking. 
8. Cumulative Analysis: Running totals and Year-to-Date (YTD) performance. 
9. Performance Analysis: Benchmarking actual performance against business targets. 
10. Part-to-Whole (Proportional): Analyzing category contributions to the total business. 
11. Data Segmentation: Clustering data for targeted marketing and operational focus. 
12. Reporting: Final automated dashboarding for stakeholders.


🏁 6. Final Reporting & Insights (SQL & Tableau)
This final stage of the project involved transforming the data from a storage format into a high-level analytical suite. I developed comprehensive reports in both the SQL layer (for automated logic) and Tableau (for executive visualization).

🗄️ A.SQL Reporting Layer (Gold Views)
I engineered a high-performance reporting layer using specialized SQL views. These views encapsulate complex business logic and serve as the "Single Version of Truth" for all downstream stakeholders and BI tools.

    1-Product Analytical Report (gold.report_products) 📦
I developed a comprehensive view that consolidates product metrics and behavioral data to provide a deep-dive into the product lifecycle.
Core Consolidation: Merges CRM product details with ERP categories, subcategories, and base costs.
Dynamic Segmentation: Implemented logic to automatically categorize products into High-Performers, Mid-Range, or Low-Performers based on total revenue thresholds.
Aggregated Performance Metrics:
Market Reach: Tracks total unique customers and total orders per product.
Sales Volume: Summarizes total quantity sold and total revenue generated.
Lifespan Analysis: Calculates the product lifespan (in months) from the first sale to the most recent.
Advanced KPI Engineering: * Recency: Measures months since the last sale to identify stagnant inventory.
Average Order Revenue (AOR): Calculates the average value per transaction.
Average Monthly Revenue: Standardizes performance over the product's lifespan to identify long-term consistency.
Pricing Accuracy: Derived the Average Selling Price to compare actual transaction values against base costs.

    2-Customer Analytical Report (gold.report_customers) 👥
A "Customer 360" analytical view that consolidates demographic and geographic data for precision targeting.
Consolidation: Integrates CRM profiles with ERP geographic data (Country/Region) and demographic details (Age, Gender, Marital Status).
Intelligence: Features embedded logic for Age Grouping and Customer Lifetime Value (CLV) indicators.
Actionable Insights: Enables instant segmentation and trend analysis at the database level, ensuring fast, consistent reporting in Tableau.

    -Final Delivered Reports:
By embedding this logic into SQL views, I created two primary reporting pillars:
Full Product Report: Providing automated insights into which categories drive the highest Average Order Revenue and which products are approaching the end of their lifecycle (Recency).
Full Customer Report: Delivering detailed drill-downs into customer demographics and historical trends to drive targeted business strategies.


🎨 B. Tableau Dashboard Development
Using the SQL Gold Views as a high-performance data source, I transformed analytical logic into a suite of interactive dashboards. I followed a professional design lifecycle—from requirement analysis to container-based layout—to ensure the final product delivers actionable business intelligence.

 .The Design Lifecycle
Step 1: Analyze Requirements 
Translated user stories into technical KPIs and drew physical mockups to plan a balanced visual hierarchy.
Step 2: Build Data Source 
Connected Tableau to the SQL Reporting Views and optimized data types for time-series and geographic analysis.
Step 3: Build Charts 
Engineered numerous Calculated Fields for Year-over-Year (YoY) comparisons and trend detection.
Refined visuals by cleaning axes, removing grid lines, and designing custom representative tooltips.
Step 4: Build Dashboards 
Structured layouts using Nested Containers for precise alignment.
Implemented Navigation Buttons for seamless movement between dashboards, along with global filters and interactive legends.

    🖥️ Final Deliverables
1. Sales Dashboard 💰 This dashboard provides a comprehensive view of financial performance and inventory movement.
Interactive Controls: Utilizes Year Parameters and dynamic filters to shift the entire analytical context.
Advanced KPI Suite:
Sales KPI: Current vs. Previous Year (PY) comparison with % Difference, monthly trends, and automated Max/Min indicators.
Quantities KPI: Current vs. PY comparison with % Difference and monthly volume tracking.
Avg Cost per Product KPI: Current vs. PY comparison with % Difference, monthly average price trends, and Max/Min highlights.
Core Analytical Charts:
Sub-category Analysis: A dual-metric comparison of Sales vs. Average Prices for both Current and Previous years.
Weekly Trends: Sales and Average Price fluctuations across months, featuring Average Reference Lines to identify performance outliers.

2. Customer Dashboard 👥 Following the same high-standard schema as the Sales dashboard, this view focuses on behavioral segmentation.
Executive KPIs: Tracking Total Customers, Total Orders, and Sales per Customer with YoY variance.
Distribution & Behavior:
Customer Distribution: Charting the number of orders per customer to identify engagement levels.
VIP Customer Analysis: A detailed breakdown of top-tier customers based on Sales, Orders, and Quantities, including their Last Order Date for recency tracking.
Interactivity: Full drill-down capabilities allowing users to navigate from high-level segments to specific VIP customer profiles.

    🛡️ Key Achievement
Successfully bridged the gap between raw backend data and frontend executive decision-making by creating a "Single Version of Truth" that is both visually professional and technically robust.


🛠️ Tech Stack & Technical Proficiencies

Database Engineering (SQL Server)
Architecture: Medallion Framework (Bronze, Silver, Gold) implemented via T-SQL.
Object Development: Advanced Stored Procedures for automated ETL, SQL Views for reporting, and DDL/DML for schema management.
Data Modeling: Dimensional Modeling (Star Schema) consisting of optimized Fact and Dimension tables.
Engineering Techniques: * SCD Type 1 implementation for dimension management.
Batch Processing and Truncate & Insert strategies.
Data Integration: Merging disparate CRM and ERP data sources into a "Single Version of Truth."
Data Cleaning: Regex-based file parsing, deduplication, and handling of statistical outliers.

Business Intelligence & Visualization (Tableau)
Dashboard Lifecycle: Full-cycle development: Requirements Analysis → Data Source Optimization → Chart Engineering → Container-based Layout.
Advanced Analytics: * Time-Series Analysis: Year-over-Year (YoY) growth, weekly trends, and monthly performance tracking.
Parameter-Driven Logic: Dynamic Year selection and interactive filtering.
Statistical Features: Average reference lines and automated Max/Min value detection.
UI/UX Design: Container nesting for balanced layouts, customized representative tooltips, navigation buttons, and interactive legends.

Methodology & Project Management
Lifecycle: End-to-End ETL/ELT best practices.
Strategy: User Story Mapping to align technical development with business stakeholder requirements.
Documentation: Data Cataloging and logic mapping for the Gold Reporting Layer.

