# 📊 Full-Cycle Data Warehouse & Analytics Engineering

This project implements a professional **Medallion Architecture** to integrate and analyze fragmented data from CRM and ERP systems. It covers the entire lifecycle: from raw file ingestion to advanced analytical Business insights.

---

## 🏗️ 1. High-Level Architecture
The system architecture ensures data reliability and scalability through a multi-layered approach.

### **The Medallion Framework:**
* **🥉 Bronze Layer (Raw Data):** Ingests raw CSV files from decentralized folders. Uses Batch Processing and Truncate & Insert to preserve a "Source of Truth" with No Transformations.
* **🥈 Silver Layer (Cleaned):** The transformation engine where raw data is cast into structured tables, cleansed, and standardized.
* **🥇 Gold Layer (Business-Ready):** Surfaced via SQL Views in a Star Schema format, optimized for high-performance consumption.



---

## 🧬 2. Data Integration & Lineage
Successful consolidation of cross-functional siloes into a unified analytical environment.

### **Entity Consolidation Logic:**
* **Customer 360:** Merges basic CRM info with ERP-sourced birthdates (`erp_cust_az12`) and geography (`erp_loc_a101`).
* **Product Hierarchy:** Enriches CRM product data with ERP category classifications (`erp_px_cat_g1v2`).
* **Sales Fact:** Centralizes transactional records from `crm_sales_details`.

---

## ⚙️ 3. Exhaustive Data Transformation Process
I implemented a comprehensive suite of transformation techniques to ensure data integrity.

### **Transformation Deep-Dive:**
* **Data Cleansing:** Deduplication (Removing redundant records).
* **Data Filtering:** Isolating relevant business records.
* **Outlier Detection:** Identifying statistical anomalies.
* **Handling Missing/Invalid Values:** Implemented logic to treat NULLs or incorrect entries.
* **Handling Unwanted Spaces:** Trimming and cleaning string data.
* **Data Type Casting:** Ensuring strict schema enforcement.
* **Normalization & Standardization:** Uniform formatting for dates, currencies, and naming conventions.
* **Data Enrichment:** Adding derived columns and calculating business-specific metrics.
* **Data Integration:** Linking disparate keys between CRM and ERP systems.
* **Business Rules & Logic:** Applying complex filtering and conditional logic.
* **Data Aggregations:** Creating pre-calculated summaries for reporting efficiency.

---

## 🥇 4. Data Modeling (Sales Data Mart)
The Gold Layer is modeled as a **Star Schema** to provide a robust foundation for analytics. It consists of **dimension tables** and **fact tables** for specific business metrics.



### **🔹 gold.fact_sales**
* **Purpose:** Stores transactional sales data for analytical purposes.

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `order_number` | NVARCHAR(50) | A unique alphanumeric identifier for each sales order. |
| `product_key` | INT | Surrogate key linking the order to the product dimension table. |
| `customer_key` | INT | Surrogate key linking the order to the customer dimension table. |
| `order_date` | DATE | The date when the order was placed. |
| `shipping_date`| DATE | The date when the order was shipped to the customer. |
| `due_date` | DATE | The date when the order payment was due. |
| `sales_amount` | INT | The total monetary value of the sale for the line item. |
| `quantity` | INT | The number of units of the product ordered. |
| `price` | INT | The price per unit of the product for the line item. |

### **🔹 gold.dim_customers**
* **Purpose:** Stores customer details enriched with demographic and geographic data.

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `customer_key` | INT | Surrogate key uniquely identifying each customer record. |
| `customer_id` | INT | Unique numerical identifier assigned to each customer. |
| `customer_number`| NVARCHAR(50)| Alphanumeric identifier used for tracking and referencing. |
| `first_name` | NVARCHAR(50) | The customer's first name. |
| `last_name` | NVARCHAR(50) | The customer's last name or family name. |
| `country` | NVARCHAR(50) | The country of residence for the customer. |
| `marital_status`| NVARCHAR(50) | The marital status of the customer. |
| `gender` | NVARCHAR(50) | The gender of the customer. |
| `birthdate` | DATE | The date of birth of the customer (YYYY-MM-DD). |
| `create_date` | DATE | The date and time when the record was created. |

### **🔹 gold.dim_products**
* **Purpose:** Provides information about the products and their attributes.

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `product_key` | INT | Surrogate key uniquely identifying each product record. |
| `product_id` | INT | Unique identifier for internal tracking and referencing. |
| `product_number` | NVARCHAR(50) | Structured alphanumeric code for categorization. |
| `product_name` | NVARCHAR(50) | Descriptive name of the product. |
| `category_id` | NVARCHAR(50) | Linking to high-level classification. |
| `category` | NVARCHAR(50) | The broader classification of the product. |
| `subcategory` | NVARCHAR(50) | Detailed classification within the category. |
| `maintenance_required`| NVARCHAR(50)| Indicates if the product requires maintenance. |
| `cost` | INT | The cost or base price of the product. |
| `product_line` | NVARCHAR(50) | Specific product line (e.g., Road, Mountain). |
| `start_date` | DATE | Date when the product became available. |

---

## 📉 5. Comprehensive Data Analytics Process
The project transitions from engineering to insights through a two-phase analytical roadmap.

### **Phase I: Exploratory Data Analysis (EDA)**
1.  **Database Exploration:** Assessing the overall structure and volume.
2.  **Dimensions Exploration:** Validating attribute distributions.
3.  **Date Exploration:** Analyzing business history.
4.  **Measures Exploration:** Identifying "Big Numbers" like total revenue.
5.  **Magnitude:** Visualizing volume and scale.
6.  **Ranking:** Identifying Top N vs. Bottom N performers.

### **Phase II: Advanced Analytics**
7.  **Change-Over-Time:** Detailed trend analysis and growth tracking.
8.  **Cumulative Analysis:** Running totals and Year-to-Date (YTD) performance.
9.  **Performance Analysis:** Benchmarking actual performance against business targets.
10. **Part-to-Whole (Proportional):** Analyzing category contributions to the total business.
11. **Data Segmentation:** Clustering data for targeted marketing and operational focus.
12. **Reporting:** Final automated dashboarding for stakeholders.

---

## 🏁 6. Final Reporting & Insights (SQL & Tableau)
Transforming storage data into a high-level analytical suite via SQL layers and Tableau visualization.

### **🗄️ A. SQL Reporting Layer (Gold Views)**
High-performance reporting views serving as the "Single Version of Truth."

1.  **Product Analytical Report (`gold.report_products`)**
    * **Core Consolidation:** Merges CRM product details with ERP categories/costs.
    * **Dynamic Segmentation:** Automatically categorizes products into High, Mid, or Low Performers.
    * **KPI Engineering:** Tracks Market Reach, Sales Volume, Lifespan Analysis, Recency, AOR, and Pricing Accuracy.

2.  **Customer Analytical Report (`gold.report_customers`)**
    * **Consolidation:** Integrates CRM profiles with ERP geographic and demographic data.
    * **Intelligence:** Embedded logic for Age Grouping and Customer Lifetime Value (CLV).

### **🎨 B. Tableau Dashboard Development**
Professional design lifecycle followed: **Analyze Requirements → Build Data Source → Build Charts → Build Dashboards.**

* **💰 Sales Dashboard:** Financial performance, YoY comparisons, Max/Min indicators, and Weekly Trends.
* **👥 Customer Dashboard:** Behavioral segmentation, Executive KPIs, and VIP Customer Analysis.

---

## 🛠️ Tech Stack & Technical Proficiencies

### **Database Engineering (SQL Server)**
* **Architecture:** Medallion Framework (Bronze, Silver, Gold).
* **Object Development:** Stored Procedures, SQL Views, DDL/DML.
* **Modeling:** Star Schema, SCD Type 1, Batch Processing.
* **Cleaning:** Regex parsing, deduplication, and outlier handling.

### **Business Intelligence & Visualization (Tableau)**
* **Lifecycle:** Requirements → Data Optimization → Chart Engineering → UI Layout.
* **Analytics:** YoY Growth, Parameter-Driven Logic, Reference Lines.
* **UI/UX:** Nested Containers, Customized Tooltips, Navigation Buttons.

### **Methodology**
* **Lifecycle:** End-to-End ETL/ELT.
* **Strategy:** User Story Mapping.
* **Documentation:** Data Cataloging and Logic Mapping.

---
**📫 Let's Connect!**
*Created by [Your Name]*
