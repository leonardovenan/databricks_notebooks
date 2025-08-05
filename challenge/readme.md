# Data Import and Processing Plan

## 📥 Objective

The goal is to:

- Import the provided **Excel file** into the **local database**.
- Clean up the data.
- Ensure phone numbers are consistent by **converting them into a pure string of digits**, without any symbols.
- Split records (using **SQL queries**) that contain **multiple RFIDs** (separated by `"|"`) into individual records.
- After cleaning and splitting, import the data into the **Customer** and **Vehicle** tables.

---

## 🧠 Business Logic

### 1. No Payment Token
This likely indicates an **old customer** who is no longer being billed, suggesting their account is probably expired.

### 2. “Active” ARMStatus with Past Dates
If a record has an `Active` **ARMStatus** but the **ARM LastBillDate** or **ARM Expires** date is in the past, it’s likely an **expired monthly pass**.

### 3. Truly Active Customers
Focus on customers with an **ARM Expires** date in the future to identify those who are still actively using the service.

---

## ⚙️ Requirements for SQL Scripts (SQL Server)

The scripts should:

- ✅ Import the **cleaned data** into **temporary or staging tables**.
- 🧹 Perform **data transformation** to:
  - Ensure phone numbers are **pure digit strings**.
  - Split records that contain multiple RFIDs into individual entries.
- 📤 Insert the **processed data** into the appropriate `Customer` and `Vehicle` tables.
- 🛡️ Be structured for **easy execution**, with proper **error handling** and **logging** to track progress.

