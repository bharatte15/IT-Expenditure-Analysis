# IT-Expenditure-Analysis

> **Interactive Power BI report with KPI tracking, cost analysis, region/department breakdowns, trend analysis, and actionable insights for IT budget optimization.**

---

## 📊 IT Expenditure Analysis Dashboard

**Developed in Power BI | End-to-End Data Analytics Project**

This project provides a complete analysis of Enterprise IT Expenditure across Departments, Sub-Categories, Vendors, and Approval Statuses. 
The dashboard delivers actionable insights by comparing **Actual Spend vs Planned Budget**, tracking budget variance, and highlighting major cost drivers across the organization.

---

## 🎯 Project Overview

The objective of this dashboard is to help organizations:
* **Understand Spend Distribution:** Track where the IT budget is being allocated across business functions.
* **Identify Top Cost Drivers:** Pinpoint high-spend vendors (AWS, Databricks, Snowflake) and sub-categories.
* **Audit Approval Statuses:** Monitor over-budget flags, approved variances, and within-budget compliance.
* **Budget Variance Tracking:** Compare `Actual Spend` against `Planned Budget` to identify overruns.
* **Cost Optimization:** Uncover actionable opportunities for operational efficiency and license rationalization.

This is a **3-page interactive Power BI report** designed for leadership-level review and operational deep dives.

---

## 📁 Dataset Details

The analysis is powered by a structured dataset containing **1,000 transaction records**:

| Field Name | Description |
| :--- | :--- |
| **`Expense_ID`** | Unique transaction reference key (e.g., `EXP-10000`) |
| **`Date`** | Transaction date (spanning 2024–2026) |
| **`Department`** | Business unit (*Software Engineering, Data & Analytics, IT Support, Cybersecurity, Cloud & Infra*) |
| **`Category`** | Cost classification (*Cloud & Hosting*) |
| **`Sub_Category`** | Specific IT asset or tool (*AWS Compute, Databricks, Snowflake, Jira, Docker*) |
| **`Vendor_Name`** | Service provider (*Amazon Web Services, Fivetran, Microsoft, Atlassian*) |
| **`Planned_Budget`** | Allocated budget target |
| **`Actual_Spend`** | Actual incurred cost |
| **`Approval_Status`** | Governance status (*Approved within Budget, Approved with Variance, Over-budget Flag*) |

> A custom `DateTable` dimension is integrated into the star schema to support time-intelligence functions.

---

## 📑 Report Pages

### 📌 Page 1 – Global Overview
*Designed for executive decision-makers.*

* **KPI Summary Cards:** Total Actual Spend, Total Planned Budget, Budget Variance, and Variance %
* **Spend by Department:** Clustered bar chart highlighting top-spending organizational units
* **Spend Distribution by Approval Status:** Donut chart auditing budget compliance across transactions
* **Top Sub-Categories & Vendors:** Ranked bar chart showcasing major software and infrastructure expenses
* **Monthly Expenditure Trend:** Multi-line chart comparing Actual Spend vs Planned Budget over time

---

### 📌 Page 2 – Operational Deep Dive Analysis
*Designed for operational managers and department leads.*

* **Detailed Transaction Matrix:** Granular line-item audit by Department $\rightarrow$ Sub-Category $\rightarrow$ Vendor
* **Vendor Spend Ranking:** Comprehensive breakdown of vendor concentration
* **Interactive Slicer Panel:** Dynamic filters for Department, Approval Status, Sub-Category, and Date Range
* **Variance Highlighting:** Conditional formatting identifying over-budget line items

---

### 📌 Page 3 – Key Insights & Recommendations
*Designed for executive presentations and business strategy reviews.*

#### 💡 Key Insights
1. **Software Engineering & Data Analytics Lead Spend:** Software Engineering ($9.12M) and Data & Analytics ($8.71M) consume the largest portion of the budget.
2. **Over-Budget Risk Concentration:** Approximately 29.4% of total spend ($12.21M across 258 transactions) was flagged as over-budget.
3. **Cloud & SaaS Dominance:** High dependency on cloud compute and analytics platforms (AWS, Databricks, Snowflake) drives recurring costs.
4. **Overall Budget Variance:** Total actual spend exceeded total planned budget by **+$2.15M (+5.46% variance)** across the measured period.

#### 💡 Strategic Recommendations
1. **Vendor Rationalization & SaaS Consolidation:** Audit redundant developer licenses (IDEs, CI/CD tools) and negotiate volume discounts with major cloud vendors.
2. **Automated Budget Guardrails:** Implement real-time budget thresholds and alerts before expenditure reaches the `Over-budget Flag` tier.
3. **Departmental Governance:** Focus cost-containment initiatives on Software Engineering and Data & Analytics units.
4. **Forecast Model Refinement:** Re-align monthly planning targets using rolling historical averages to reduce variance.

---

## 🛠️ Tools & Technologies Used

* **Power BI Desktop:** Data modeling, star schema design, interactive visualizations
* **Power Query Editor:** Data cleaning, data type casting, and schema transformations
* **DAX (Data Analysis Expressions):** Measures for variance, percentages, dynamic aggregations, and time-intelligence
* **Python (Pandas / Matplotlib):** Exploratory data analysis (EDA) and data validation
* **Excel / CSV:** Primary dataset source

---

## 🔢 Key DAX Measures

```dax
// 1. Total Financial Aggregations
Total Actual Spend = SUM('IT_Expenditure_Dataset'[Actual_Spend])

Total Planned Budget = SUM('IT_Expenditure_Dataset'[Planned_Budget])

// 2. Budget Variance Calculations
Budget Variance = [Total Actual Spend] - [Total Planned Budget]

Variance Percentage = DIVIDE([Budget Variance], [Total Planned Budget], 0)

// 3. Over-Budget Tracking
Over Budget Spend = 
CALCULATE(
    [Total Actual Spend], 
    'IT_Expenditure_Dataset'[Approval_Status] = "Over-budget Flag"
)

// 4. Time Intelligence (YoY Metrics)
Actual Spend LY = 
CALCULATE(
    [Total Actual Spend], 
    SAMEPERIODLASTYEAR('DateTable'[Date])
)

YoY Spend Growth % = 
DIVIDE([Total Actual Spend] - [Actual Spend LY], [Actual Spend LY], 0)
