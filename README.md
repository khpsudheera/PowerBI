# PowerBI
Power Query Data Transformations
# Power Query Data Transformations – Step-by-Step Approach

This repository documents the end-to-end Power Query transformations performed as part of the **Codebasics – Power Query Practice Exercise (Chapter 5)**. The objective was to clean, structure, and prepare transactional data for analysis using Power BI.

---

## 📌 Datasets Used

* `fact_transactions_2022`
* `fact_transactions_2023`
* `dim_merchants`
* `pivoted_dim_category`
* `dim_date`

---

## 🧩 Task 1: Data Cleaning – dim_merchants

**Objective:** Clean and standardize merchant information.

**Steps performed:**

1. Split the `Merchant` column using the delimiter `-` to separate merchant name and industry details.
2. Renamed the newly created column to **Industry Segment**.
3. Trimmed leading and trailing spaces from the `Industry Segment` column.
4. Removed parentheses `(` and `)` by extracting values using **Text Between Delimiters**.
5. Removed duplicate merchant records where the same merchant appeared with different IDs.

---

## 🧩 Task 2: Extract Date Information – dim_date

**Objective:** Break down the date into usable attributes.

**Steps performed:**

1. Extracted **Year** from the Date column.
2. Extracted **Month Name** from the Date column.
3. Extracted **Day Name** from the Date column.
4. Created separate columns for Year, Month Name, and Day Name.

---

## 🧩 Task 3: Unpivot Category Table

**Objective:** Reshape category data for proper merging.

**Steps performed:**

1. Cleaned unnecessary rows and headers in `pivoted_dim_category`.
2. Selected category columns and applied **Unpivot Columns**.
3. Renamed the resulting columns appropriately.
4. Renamed the final table to **dim_category**.

---

## 🧩 Task 4: Filtering Unwanted Data

**Objective:** Focus analysis on significant transactions.

**Steps performed:**

1. Applied a filter on `Debit_Amount` to keep values **greater than or equal to 100**.
2. Applied the same filtering logic to both `fact_transactions_2022` and `fact_transactions_2023`.

---

## 🧩 Task 5: Append Tables

**Objective:** Combine multi-year transaction data.

**Steps performed:**

1. Appended `fact_transactions_2023` to `fact_transactions_2022` using **Append Queries as New**.
2. Stored the combined result in a new table named **fact_transactions**.

---

## 🧩 Task 6: Merge Tables

**Objective:** Enrich transaction data with descriptive attributes.

**Steps performed:**

1. Merged `fact_transactions` with `dim_category` using **CategoryID** (Left Outer Join).
2. Expanded and added **CategoryName** to the fact table.
3. Merged `fact_transactions` with `dim_merchants` using **MerchantID** (Left Outer Join).
4. Expanded and added **Merchant** name to the fact table.

---

## 🧩 Task 7: Adding Conditional Column

**Objective:** Categorize transactions by value.

**Steps performed:**

1. Added a conditional column named **Transaction Category**.
2. Defined rules:

   * Debit Amount < 1000 → **Low**
   * Debit Amount ≥ 1000 → **High**

---

## 🧩 Task 8: Sorting and Grouping

**Objective:** Analyze total transaction amount per merchant.

**Steps performed:**

1. Duplicated the `fact_transactions` table to preserve transaction-level data.
2. Grouped data by **Merchant**.
3. Calculated **Sum of Debit_Amount** as `total_transaction_amount`.
4. Sorted merchants in **descending order** based on total transaction amount.

---

## ✅ Final Outcome

* Cleaned and standardized dimension tables
* Unified multi-year transaction data
* Enriched fact table with merchant and category details
* Created transaction-level and aggregated insights ready for analysis

---

### 📌  This project demonstrates practical Power Query skills including cleaning, filtering, appending, merging, unpivoting, grouping, and conditional logic.
