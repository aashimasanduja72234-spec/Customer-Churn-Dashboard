# 📉 Customer Churn Analysis Dashboard

A Power BI dashboard built to identify the key drivers of customer churn and surface actionable retention strategies using telecom customer data.

---

## 📌 Project Overview

Customer churn is one of the most critical metrics for subscription-based businesses. This project analyses churn patterns across customer demographics, contract types, service usage, and billing behaviour to help business stakeholders understand *who* is leaving and *why*.

---

## 🎯 Objectives

- Identify the key factors that contribute to customer churn
- Segment churned customers by demographic and behavioural attributes
- Build an interactive Power BI dashboard for business users
- Derive actionable retention recommendations from the data

---

## 🗂️ Data Source

- **Dataset:** Telecom customer data (Excel)
- **Records:** ~7,000 customer rows
- **Key Fields:** Customer ID, Gender, Tenure, Contract Type, Monthly Charges, Total Charges, Internet Service, Tech Support, Churn Label

> *Data was sourced from a publicly available telecom churn dataset and cleaned in Excel prior to modelling.*

---

## 🛠️ Tools & Technologies

| Tool | Purpose |
|---|---|
| **Power BI Desktop** | Dashboard design, visualisation, DAX measures |
| **Microsoft Excel** | Data cleaning, preprocessing, exploratory analysis |
| **DAX** | Custom KPIs, calculated columns, measures |

---

## 🔧 Methodology

### 1. Data Cleaning (Excel)
- Removed duplicates and null values
- Standardised categorical fields (e.g., Yes/No → 1/0 for churn flag)
- Converted `TotalCharges` from text to numeric
- Created an `At Risk` flag for customers on month-to-month contracts with high charges

### 2. Data Modelling (Power BI)
- Loaded cleaned Excel file into Power BI
- Created a date/tenure table for time-based slicing
- Defined relationships between customer fact table and dimension tables

### 3. DAX Measures

```dax
-- Churn Rate
Churn Rate = 
DIVIDE(
    CALCULATE(COUNTROWS(Customers), Customers[Churn] = "Yes"),
    COUNTROWS(Customers)
)

-- Average Monthly Charges (Churned Customers)
Avg Charges Churned = 
CALCULATE(
    AVERAGE(Customers[MonthlyCharges]),
    Customers[Churn] = "Yes"
)

-- Customers at Risk
At Risk Customers = 
CALCULATE(
    COUNTROWS(Customers),
    Customers[Contract] = "Month-to-month",
    Customers[Churn] = "No"
)
```

### 4. Dashboard Design
- KPI cards: Total Customers, Churn Rate, Avg Tenure, Avg Monthly Charges
- Bar charts: Churn by Contract Type, Internet Service, Payment Method
- Donut charts: Churn by Gender, Senior Citizen status
- Slicers: Contract type, Internet service, Gender

---

## 📊 Key Findings

- **Month-to-month contracts** had the highest churn rate (~43%), compared to ~11% for two-year contracts
- Customers with **Fiber Optic internet** churned significantly more than DSL users
- **Senior citizens** had a disproportionately higher churn rate (~41%)
- Customers with **no tech support** were nearly twice as likely to churn
- Higher **monthly charges** strongly correlated with churn — churned customers paid ~$74/month vs ~$61 for retained

---

## 💡 Retention Recommendations

1. **Incentivise longer contracts** — offer discounts to move month-to-month customers to annual plans
2. **Bundle tech support** — especially for senior citizens and Fiber Optic users
3. **Target high-charge segments** — proactive outreach for customers paying above $70/month
4. **Early tenure intervention** — churn risk is highest in the first 12 months; focus onboarding efforts here

---

## 🔗 Back to Portfolio

[← View all projects](https://github.com/aashimasanduja72234-spec/Data-Analytics-portfolio)
