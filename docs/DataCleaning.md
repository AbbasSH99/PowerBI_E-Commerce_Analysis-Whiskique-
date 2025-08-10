# 🧹 Data Cleaning & Transformation – Power BI Project

## 📌 Overview
This document outlines the data preparation and transformation process for my Power BI project, including data import, cleaning, relationship management, and metric creation.

---

## 1. 📥 Data Import & Setup
- Imported CSV tables:
  - **fact_sales** → renamed to `Sales`
  - **dim_products** → renamed to `Products`
  - **dim_customers** → renamed to `Customers`
- Adjusted relationships:
  - Linked `Products` → `Sales` via **Stock Code** (one-to-many)
- Created initial metrics:
  - `Total Rows` (card visual)
  - `Count of Invoice No` (total invoices)

---

## 2. 🧼 Data Cleaning
### Removing Invalid Transactions
- Filtered out rows where **Invoice No** is `NULL` (per business rule).

### Standardizing Customer State Data
- Imported `state_region_mapping` table.
- Used it to standardize state names via a **many-to-many relationship** with `Customers`.

### Product Name Cleanup
- Replaced `"Indoor Pet Camera (Wi-Fi)"` with `"Indoor Pet Camera"` in `Sales`.

---

## 3. 📊 Customer Metrics
- **Number of Customers** → count of unique customers.
- **Customer LTV (avg)** → total sales ÷ total unique customers.

---

## 4. 📦 Quantity & Sales Aggregation
- Duplicated `Sales` → created `Invoice Totals` table.
- Grouped by `Invoice No`:
  - Calculated `Total Quantity` and `Total Sales`.

---

## 5. 🛒 Market Basket Analysis
- Duplicated `Sales` → created `Market Basket` table.
- Established **many-to-many** relationship to analyze product co-purchases.

---

## 6. 🚚 Shipping Cost Analysis (What-if)
### Baseline Shipping
- Added `Shipping Cost` from `Products` to `Sales` using `RELATED()`.
- Created **Shipping (Baseline)** measure:
  - Quantity = 1 → base cost.
  - Quantity > 1 → base cost + 70% cost for each additional item.

### Dynamic What-if Shipping
- Created **Blended Shipping Cost Factor** table for quantity-based cost multipliers.
- Built **Shipping (What-if)** measure using dynamic cost factor.
- Added **Shipping (Difference)** measure.

---

## 7. 📈 Shipping Metrics
- Created running total measures for:
  - Baseline shipping
  - What-if shipping
  - Shipping difference
- Visualized as area chart.

---

## 8. 💰 Revenue & Profit Calculation
- Added **COGS** column → `Landed Cost × Quantity`.
- Created **Profit (Baseline)** → Sales − COGS − Shipping (Baseline).
- Calculated **Profit %** → Profit ÷ Sales.

---

## 📷 Screenshots
*(Insert key screenshots here for better visualization: data model, Power Query steps, DAX formulas, dashboard previews)*

---

## 📂 Full Technical Documentation
For the full detailed step-by-step process, download the **Data Cleaning & Manipulation.docx** file in this repository.