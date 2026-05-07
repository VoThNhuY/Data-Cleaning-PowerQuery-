# 📊 Power Query Data Transformation
## 📋 Project Overview
- The goal of this project is to turn a messy Excel sales report into a clean, professional Star Schema data model, using Power Query to fix formatting issues and restructure the data so it can be easily used for charts and reports.
- **The Problem**:
  - Country names and codes were combined into a single column.
  - There were many empty cells (null).
  - Sales data was spread across 12 monthly columns (Wide format), making it hard to analyze trends.

### 📂 Dataset
- **`raw_data`**: The [original dataset](https://github.com/VoThNhuY/Data-Cleaning-PowerQuery-/blob/main/raw_data.csv) before any transformations.
- **`cleaned_data`**: The [final dataset](https://github.com/VoThNhuY/Data-Cleaning-PowerQuery-/blob/main/clean_data.xlsx) after Power Query processing.

## 📸 Visual Comparison
**Before Cleaning:**
<img width="625" height="83" alt="image" src="https://github.com/user-attachments/assets/5b16ee32-129e-4c99-915c-051d8c471828" />


**After Cleaning:**
<img width="1920" height="823" alt="image" src="https://github.com/user-attachments/assets/b5aa74d0-de4c-4e48-8697-90bee127eeda" /> 
<img width="1917" height="824" alt="image" src="https://github.com/user-attachments/assets/20316728-14fc-4f1a-bb31-b14388a6429e" />

## 🛠️ Cleaning Process
**1. Split Columns**
- **Task**: The Country column looked like this: _**GBR|United Kingdom**_.
- **Action**: Using **Split Column** feature with the delimiter |.
- **Result**: Having two clear columns: **CountryCode** and **CountryName**.

**2. Fix Missing Data**
- **Task**: Many months had no data, showing as **null**.
- **Action**: Using **Replace Values** to change all **_null_** values to **0**.
- **Result**: This ensures calculations like "Total Sales" work correctly.

**3. Change Table Structure (Unpivot)**
- **Task**: Monthly data was **horizontal** (January, February, etc., were columns).
- **Action**: Using the **Unpivot Other Columns** feature.
- **Result**: The table is now vertical (Long format). I created two new columns: **Month** and **Quantity**.

**4. Add Business Logic**
- **Task**: Label months where sales were zero.
- **Action**: Adding a Conditional Column called **Note**
<img width="1145" height="468" alt="image" src="https://github.com/user-attachments/assets/f937fa6c-0ae5-4173-a73e-354640faae70" />

  
## 🏗️Data Model (Star Schema)
To make the report run faster, split the data into two tables:
- **Country Table (Dimension)**: Contains a unique list of **CountryCode** and **CountryName**.
- **Sales Table (Fact)**: Contains the transactions (CountryCode, Month, Quantity, and Note).
- **Relationship**: I linked these two tables using the CountryCode column (One-to-Many relationship).
  <img width="719" height="319" alt="image" src="https://github.com/user-attachments/assets/ea2a0bc4-5ae7-4886-bb46-abacb9913861" />

## 📈Final Result
- **Clean Data**: No more null values or messy columns.
- **Ready for Reports**: The data is now perfect for creating dashboards in Power BI or Excel Pivot Tables.
- **Automated:** Just click "Refresh" to process new data instantly.
