# Retail Sales Exploratory Data Analysis (EDA)
**Oasis Infobyte Data Analytics Internship — Level 1, Task 1**

![Python](https://img.shields.io/badge/Python-3.12-blue.svg)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-orange.svg)
![Seaborn](https://img.shields.io/badge/Seaborn-Visualization-green.svg)
![Status](https://img.shields.io/badge/Status-Completed%20%26%20Verified-brightgreen.svg)

---

## 1. Project Overview
This project presents an end-to-end **Exploratory Data Analysis (EDA)** on retail transaction data conducted for the Oasis Infobyte Data Analytics Internship (Level 1, Task 1). 

The primary objective is to evaluate transactional sales trends, demographic customer purchasing behavior, and product category performance to derive actionable retail business intelligence and inventory planning recommendations.

---

## 2. Dataset Architecture & Schema

- **File Location:** `data/retail_sales_dataset.csv`
- **Total Records:** 1,000 transactions
- **Total Attributes:** 9 columns
- **Temporal Range:** January 1, 2023 to January 1, 2024
- **Total Gross Revenue:** 456,000 (Monetary units unspecified in dataset)

### Data Dictionary

| Column Name | Data Type | Description |
| :--- | :--- | :--- |
| `Transaction ID` | Integer | Unique identifier for each retail transaction (1 to 1,000) |
| `Date` | Datetime | Date of sale (formatted as `YYYY-MM-DD`) |
| `Customer ID` | Object | Unique customer identifier |
| `Gender` | Object | Customer biological gender (`Female`, `Male`) |
| `Age` | Integer | Customer age (ranging from 18 to 64 years) |
| `Product Category`| Object | Broad product classification (`Beauty`, `Clothing`, `Electronics`) |
| `Quantity` | Integer | Units purchased per transaction (1 to 4 units) |
| `Price per Unit` | Integer | Price per single unit (ranging from 25 to 500) |
| `Total Amount` | Integer | Total transaction revenue (`Quantity × Price per Unit`) |

---

## 3. Repository Structure

```plaintext
DataAnalytics-L1-EDARetailSales/
├── data/
│   └── retail_sales_dataset.csv            # Original retail transactions dataset
├── notebooks/
│   ├── Retail_Sales_Analysis_Final.ipynb   # Executed, refactored, verified notebook
│   ├── Retail_Sales_Analysis.ipynb         # Original notebook
│   └── Retail_Sales_Analysis_Backup.ipynb  # Preserved backup of original notebook
├── outputs/
│   ├── charts/                             # High-resolution exported PNG visualizations
│   │   ├── 01_monthly_revenue_trend.png
│   │   ├── 02_quarterly_revenue_trend.png
│   │   ├── 03_customer_age_distribution.png
│   │   ├── 04_revenue_by_age_group.png
│   │   ├── 05_gender_analysis.png
│   │   ├── 06_category_revenue.png
│   │   └── 07_correlation_heatmap.png
│   └── reports/                            # Analytical documentation and reports
├── README.md                               # Project documentation and executive summary
└── requirements.txt                        # Python environment dependencies
```

---

## 4. Environment Setup & Execution Guide

### Prerequisites
- Python 3.10+ (Tested on Python 3.12)
- JupyterLab / Jupyter Notebook / VS Code Jupyter Extension

### Installation & Execution
1. **Clone the repository:**
   ```bash
   git clone https://github.com/your-username/DataAnalytics-L1-EDARetailSales.git
   cd DataAnalytics-L1-EDARetailSales
   ```
2. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```
3. **Launch Jupyter:**
   ```bash
   jupyter notebook notebooks/Retail_Sales_Analysis_Final.ipynb
   ```
4. Run all cells sequentially to reproduce calculations, charts, and validation assertions.

---

## 5. Key Analytical Findings

### A. Data Hygiene & Validation
- **Missing Values:** Exactly 0 missing values across all 1,000 records.
- **Duplicate Records:** 0 duplicate rows detected.
- **Date Parsing:** 100% of date strings parsed successfully into `datetime64[ns]`.
- **Arithmetic Integrity:** Verified that `Total Amount == Quantity * Price per Unit` for 1,000 out of 1,000 records (0 mismatches).

### B. Descriptive Statistical Summary
| Metric | Age | Quantity | Price per Unit | Total Amount |
| :--- | :---: | :---: | :---: | :---: |
| **Mean** | 41.39 | 2.51 | 179.89 | 456.00 |
| **Median** | 42.00 | 3.00 | 50.00 | 135.00 |
| **Mode** | 43.00 | 4.00 | 50.00 | 50.00 |
| **Std Dev** | 13.68 | 1.13 | 189.68 | 560.00 |

*Statistical Note:* `Total Amount` and `Price per Unit` exhibit strong right-skewness (Mean >> Median), driven by premium products (prices up to 500) and multi-unit transactions (up to 2,000 total).

### C. Time-Series Sales Trajectory
- **Peak Monthly Sales:** **May 2023** generated the highest monthly revenue of **53,150** (114 transactions).
- **Lowest Full Month:** **September 2023** was the lowest full month at **23,620** (65 transactions).
- **Quarterly Performance:**
  - `Q1 2023`: 108,500
  - `Q2 2023`: 123,735
  - `Q3 2023`: 96,045
  - `Q4 2023`: **126,190** (Peak Quarter, surging **+31.39%** over Q3 2023)
  - `Q1 2024`: 1,530 (*Partial period*: captures only January 1, 2024)

### D. Customer Demographics & Segment Analysis
Age grouping was established using 5 non-overlapping left-inclusive bins (`[18, 26, 36, 46, 56, 101]` with `right=False`):

| Age Cohort | Transaction Count | Volume Share | Total Revenue | Revenue Share | Average Order Value (AOV) |
| :---: | :---: | :---: | :---: | :---: | :---: |
| **18–25** | 169 | 16.90% | 84,550 | 18.54% | **500.30** (Highest) |
| **26–35** | 205 | 20.50% | 98,480 | 21.60% | 480.39 |
| **36–45** | 202 | 20.20% | 91,870 | 20.15% | 454.80 |
| **46–55** | **229** | **22.90%** | **100,690** | **22.08%** | 439.69 |
| **56+** | 195 | 19.50% | 80,410 | 17.63% | 412.36 |
| **Total** | **1,000** | **100.0%** | **456,000** | **100.0%** | **456.00** |

- **Core Segment:** The **46–55 age group** is the primary revenue engine (100,690; 22.08% of total revenue).
- **High-Ticket Segment:** Young adults aged **18–25** achieve the highest average transaction value (500.30).

### E. Gender Breakdown
| Gender | Transactions | Transaction Share | Total Revenue | Revenue Share | Average Order Value |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Female** | 510 | 51.0% | 232,840 | 51.06% | 456.55 |
| **Male** | 490 | 49.0% | 223,160 | 48.94% | 455.43 |

Purchasing volume and spend are balanced evenly across genders with virtually identical basket sizes.

### F. Product Category Performance
| Product Category | Transactions | Units Sold | Total Revenue | Revenue Share | Average Order Value |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Electronics** | 342 | 849 | **156,905** | **34.41%** | 458.79 |
| **Clothing** | **351** | **894** | 155,580 | 34.12% | 443.25 |
| **Beauty** | 307 | 771 | 143,515 | 31.47% | **467.48** |

- Electronics leads in revenue, Clothing leads in transaction and unit volume, and Beauty leads in Average Order Value.

### G. Correlation Analysis
- **Price per Unit vs. Total Amount (+0.85):** Strong positive correlation; product price is the dominant driver of transaction size.
- **Quantity vs. Total Amount (+0.37):** Moderate positive correlation.
- **Age vs. Total Amount (-0.06):** Negligible linear association.
- **Age vs. Quantity (-0.02):** No meaningful relationship between customer age and basket unit size.

---

## 6. Strategic Business Recommendations

1. **Targeted Engagement for Core Cohorts (Ages 26–55):**  
   Customers between 26 and 55 account for **63.8% of total revenue (291,040)**. Retail marketing should prioritize targeted loyalty rewards and personalized campaigns for these mature demographics.
2. **Product Bundling for Multi-Unit Baskets:**  
   All top transactions (2,000 value) are 4-unit purchases. Implementing bundle promotions (e.g., "Buy 3, Get 1 at 50% off") will encourage shoppers to scale up unit purchases.
3. **Mid-Year Promotional Calendar:**  
   Address the seasonal revenue dip observed in Q3 (September trough of 23,620) through mid-season clearance events or back-to-school promotional campaigns.
4. **Cross-Selling Beauty & Fashion:**  
   Because Beauty exhibits the highest Average Order Value (467.48) but lower unit volume, bundle Beauty products with Clothing accessories to elevate overall category conversion.

---

## 7. Crucial Project & Dataset Limitations

1. **Absence of Individual Product SKUs:**  
   The dataset provides high-level categories (`Beauty`, `Clothing`, `Electronics`) but **omits individual product names or item codes**. Therefore, an individual "Top 10 Products" analysis cannot be conducted without fabricating non-existent data. Instead, the analysis truthfully analyzes the **Top 10 Highest-Value Transactions**.
2. **Unspecified Currency:**  
   The source dataset does not specify a currency symbol (e.g., USD, INR, EUR); values are presented purely as numerical monetary units.
3. **Partial January 2024 Coverage:**  
   January 2024 contains only 2 transaction records from January 1, 2024 (1,530 revenue). It represents a partial window and should not be treated as a complete operational month.
4. **Channel & Geographic Data:**  
   The dataset lacks geographic store location, sales channel (online vs. physical brick-and-mortar), and payment method indicators.

---

## 8. Verification & Reconciliation Matrix

All metrics have been verified programmatically via assertions in `Retail_Sales_Analysis_Final.ipynb`:

| Test Assertion | Target Value | Verified Result | Status |
| :--- | :---: | :---: | :---: |
| Total Record Count | 1,000 | 1,000 | **PASSED** |
| Total Gross Revenue | 456,000 | 456,000 | **PASSED** |
| Product Category Revenue Sum | 456,000 | 456,000 | **PASSED** |
| Gender Revenue Sum | 456,000 | 456,000 | **PASSED** |
| Age Cohort Revenue Sum | 456,000 | 456,000 | **PASSED** |
| Age Cohort Transaction Sum | 1,000 | 1,000 | **PASSED** |
| Missing Value Count | 0 | 0 | **PASSED** |
| Duplicate Record Count | 0 | 0 | **PASSED** |
| Arithmetic Discrepancies | 0 | 0 | **PASSED** |
| Invalid Datetime Conversions | 0 | 0 | **PASSED** |

---

## 9. Author & License
- **Author:** Kathiravan K  
- **Internship:** Oasis Infobyte Data Analytics Internship (Level 1, Task 1)  
- **License:** Open source for academic and portfolio demonstration.

