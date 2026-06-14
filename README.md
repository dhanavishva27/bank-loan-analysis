# 🏦 Bank Loan Performance Analysis
### End-to-End Data Analytics Project | Finance Domain


## 📌 Project Overview

This project delivers a comprehensive **Bank Loan Performance Analysis** built on real-world financial data. The goal was to help stakeholders monitor loan portfolio health, identify risk segments, and track KPIs across loan applications, funded amounts, and repayment behaviour — through an interactive, multi-page Power BI dashboard validated against MS SQL Server queries.

---

## 🎯 Business Problem

A bank needs visibility into:
- How many loans are being applied for, approved, and funded each month?
- What percentage of loans are performing well (Good) vs. defaulting (Bad)?
- Which states, loan purposes, and borrower profiles carry the most risk?
- Are interest rates and debt-to-income ratios within acceptable ranges?

---

## 🗂️ Project Workflow

```
Raw Data (CSV)
     │
     ▼
MS SQL Server ──► SQL Queries (KPI Validation)
     │
     ▼
Power BI (Data Model + DAX)
     │
     ▼
3-Page Interactive Dashboard
```

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| MS SQL Server | Database creation, data import, KPI querying |
| SQL (T-SQL) | Data extraction, aggregation, validation |
| Power BI Desktop | Data modelling, DAX measures, dashboard design |
| DAX | KPI calculations, time intelligence, MoM trends |
| Power Query | Data cleaning and transformation |

---

## 📊 Dashboards Built

### 1. Summary Dashboard — KPI Overview
Tracks high-level loan performance metrics at a glance.

**KPIs included:**
- Total Loan Applications (with MoM & MTD)
- Total Funded Amount
- Total Amount Received
- Average Interest Rate
- Average Debt-to-Income (DTI) Ratio

**Good Loan vs Bad Loan Analysis:**

| Metric | Good Loan | Bad Loan |
|---|---|---|
| Status | Fully Paid / Current | Charged Off |
| KPIs tracked | Applications, Funded Amount, Amount Received | Applications, Funded Amount, Amount Received |

---

### 2. Overview Dashboard — Trend & Segment Analysis
Deep-dive into patterns across time, geography, and borrower segments.

**Visuals included:**
- Monthly trend line chart (loan applications over time)
- Regional map — loan distribution by US state
- Loan term breakdown (36 months vs 60 months)
- Loan purpose analysis (debt consolidation, car, education, etc.)
- Home ownership breakdown (rent, own, mortgage)
- Dynamic field parameters for interactive switching

---

### 3. Details Dashboard — Row-Level Audit View
A granular table view for auditing individual customer loan records.

**Features:**
- Full grid of customer-level data
- Interactive slicers for filtering by grade, purpose, state
- Enables drill-down into specific loan records for compliance review

---

## 🔍 SQL Queries — Key Metrics Calculated

```sql
-- Total Loan Applications
SELECT COUNT(id) AS Total_Loan_Applications FROM bank_loan_data;

-- Total Funded Amount
SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data;

-- Total Amount Received
SELECT SUM(total_payment) AS Total_Amount_Received FROM bank_loan_data;

-- Average Interest Rate
SELECT ROUND(AVG(int_rate) * 100, 2) AS Avg_Interest_Rate FROM bank_loan_data;

-- Average DTI
SELECT ROUND(AVG(dti) * 100, 2) AS Avg_DTI FROM bank_loan_data;

-- Good Loan Percentage
SELECT
  (COUNT(CASE WHEN loan_status IN ('Fully Paid','Current') THEN id END) * 100.0)
  / COUNT(id) AS Good_Loan_Percentage
FROM bank_loan_data;

-- Bad Loan Percentage
SELECT
  (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0)
  / COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data;

-- Monthly Trend (MTD)
SELECT
  MONTH(issue_date) AS Month,
  DATENAME(MONTH, issue_date) AS Month_Name,
  COUNT(id) AS Total_Loan_Applications,
  SUM(loan_amount) AS Total_Funded_Amount,
  SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date);
```

---

## 📐 Data Model

- **Star schema** with a dedicated `Date` table for accurate time intelligence
- Relationships established between fact table and date dimension
- DAX measures created for MoM change, MTD, and YTD calculations

---

## ✅ Data Validation

All Power BI dashboard figures were **cross-validated** against SQL query outputs to ensure 100% accuracy before final delivery. This step ensures that the DAX measures and SQL aggregations are in agreement.

---

## 💡 Key Insights

- **Good loans** account for the majority of the portfolio — confirming healthy credit approval standards
- **Debt consolidation** is the most common loan purpose, representing the largest share of funded amounts
- **Charged Off** loans are concentrated in specific states and longer loan terms (60 months)
- **Average interest rate** varies significantly by loan grade — Grade A borrowers enjoy the lowest rates
- **DTI ratio** is a strong predictor of loan status — higher DTI correlates with higher charge-off risk

---

## 📁 Repository Structure

```
bank-loan-analysis/
│
├── SQL/
│   └── bank_loan_queries.sql       # All KPI queries used in the project
│
├── PowerBI/
│   └── bank_loan_dashboard.pbix    # Power BI report file
│
├── Data/
│   └── financial_loan.csv          # Raw dataset
│
├── Screenshots/
│   ├── summary_dashboard.png
│   ├── overview_dashboard.png
│   └── details_dashboard.png
│
└── README.md
```

---

## 🚀 How to Run This Project

1. **SQL Setup**
   - Install MS SQL Server Management Studio (SSMS)
   - Create a new database: `bank_loan_db`
   - Import `financial_loan.csv` using the import wizard
   - Run queries from `SQL/bank_loan_queries.sql`

2. **Power BI Setup**
   - Open `PowerBI/bank_loan_dashboard.pbix` in Power BI Desktop
   - Update the SQL Server connection string to your local server
   - Refresh the data

---

## 👤 Author

**Dhanavishva S**
B.E. — Artificial Intelligence & Data Science | PSNACET

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0077B5?style=flat-square&logo=linkedin)](https://www.linkedin.com/in/dhanavishva)
[![GitHub](https://img.shields.io/badge/GitHub-Follow-181717?style=flat-square&logo=github)](https://github.com/dhanavishva)

---

## 📄 Acknowledgement

Project inspired by the end-to-end Bank Loan Analysis tutorial covering MS SQL Server and Power BI for the finance domain.
