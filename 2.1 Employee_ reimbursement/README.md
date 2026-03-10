# Power BI Employee Reimbursement Analysis

## Project Overview
This project analyzes employee reimbursement data using **Power BI**.  
The dataset contained multiple real-world data issues such as inconsistent text values, missing currency data, and multiple currencies.
The goal of this project was to clean the data, normalize currency values to INR, and create an interactive dashboard to analyze reimbursements by employee and project.

## Dataset Features

The dataset contains the following columns:
- Request_ID
- Employee_ID
- Expense_Type
- Currency
- Amount
- Expense_Date
- Project_Name
- Approval_Status

A separate **Employee Dimension Table** contains employee names and IDs.

---

## Data Cleaning (Power Query)

Several transformations were performed in **Power Query**:

- Corrected spelling and punctuation errors in the **Expense_Type** column
- Standardized **Project_Name** values
- Handled missing values in the **Currency** column
- Created a new column `Currency_Fixed` using conditional logic
- Converted reimbursement amounts into **INR**

Currency normalization logic:

USD → INR (83 exchange rate)  
EUR → INR (90 exchange rate)  
INR → unchanged

---

## Data Model

The model consists of two tables:

Fact Table
fact_reimbursement

Dimension Table
Dim_employee

Relationship:
Dim_employee[Employee_ID] → fact_reimbursement[Employee_ID]

---

## DAX Measures

### Total Reimbursement

```DAX
Total_Reimbursement_INR =
SUM(fact_reimbursement[Amount_INR])
Project B Reimbursement
Project_B_Total =
CALCULATE(
    SUM(fact_reimbursement[Amount_INR]),
    fact_reimbursement[Project_Name] = "Project_B"
)
Declined Requests
Declined_Requests =
CALCULATE(
    COUNT(fact_reimbursement[Request_ID]),
    fact_reimbursement[Approval_Status] = "Declined"
)
```
### Dashboard Features

The Power BI dashboard includes:
KPI Cards
Total Reimbursement Amount
Project B Total
Declined Requests

Visualizations
Bar Chart: Employee vs Reimbursement Amount
Pie Chart: Project-wise Reimbursement Distribution
Interactive Filters
Project slicer
Employee slicer

Key Insights
Total reimbursement amount: ₹607K
Project B reimbursement total: ₹142K
Number of declined reimbursement requests: 2
Project A has the highest reimbursement contribution compared to other projects.

Tools Used
Power BI
Power Query
DAX

Project Files
Power BI Dashboard (.pbix)
Dataset (.xlsx)
Documentation (README)
