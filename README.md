# MYSQL-Projects

SUMMARY:
“I cleaned the Layoffs 2022 dataset by creating a staging table, removing duplicates with window functions, standardizing industries and countries, converting dates into proper formats, and handling nulls by deleting rows with no useful information. The result was a clean dataset ready for analysis.”

# 🧹 SQL Data Cleaning Project – Layoffs 2022 Dataset

## 📌 Overview
This project demonstrates a **systematic approach to data cleaning** using SQL on the [Layoffs 2022 dataset](https://www.kaggle.com/datasets/swaptr/layoffs-2022).  
The goal was to transform raw, messy data into a **clean, reliable dataset** ready for analysis, while preserving the original source.

---

## 🎯 Objectives
1. Create a **staging table** to protect raw data.
2. Identify and **remove duplicates** using window functions.
3. **Standardize categorical values** (industries, countries, dates).
4. Handle **null values** intelligently.
5. Drop **unnecessary rows and columns** to finalize the dataset.

---

## 🛠️ Steps Taken

### 1. Create Staging Table
- Copied raw data into a staging table (`layoffs_staging`) to ensure cleaning does not affect the original dataset.
- This follows best practices for safe data handling.

### 2. Remove Duplicates
- Used `ROW_NUMBER()` with `PARTITION BY` across key columns to detect duplicates.
- Created a helper column `row_num` to mark duplicates.
- Deleted rows where `row_num >= 2`.
- Preserved legitimate entries (e.g., multiple layoffs from the same company at different times).

### 3. Standardize Data
- Converted empty strings in `industry` to `NULL`.
- Populated missing industries by matching company names (e.g., Airbnb → Travel).
- Normalized inconsistent values:
  - `"Crypto Currency"`, `"CryptoCurrency"` → `"Crypto"`
  - `"United States."` → `"United States"`
- Converted `date` column from text to proper `DATE` type using `STR_TO_DATE`.

### 4. Handle Null Values
- Analyzed nulls in `total_laid_off`, `percentage_laid_off`, and `funds_raised_millions`.
- Preserved meaningful nulls (e.g., missing funding info).
- Deleted rows where both `total_laid_off` AND `percentage_laid_off` were null (no analytical value).

### 5. Finalize Dataset
- Dropped helper column `row_num`.
- Result: `layoffs_staging2` → clean, standardized, analysis‑ready dataset.

---

## 📊 Key SQL Concepts Used
- **Window Functions**: `ROW_NUMBER()` for duplicate detection.
- **Joins**: Self‑join to populate missing industry values.
- **String Functions**: `TRIM()` for country standardization.
- **Date Conversion**: `STR_TO_DATE()` and `ALTER TABLE` for proper date typing.
- **Conditional Deletes**: Removing rows with useless nulls.

---

## ✅ Outcomes
- Produced a **clean dataset** free of duplicates, inconsistencies, and useless nulls.
- Demonstrated **best practices** in SQL data cleaning:
  - Safe staging environment
  - Structured step‑by‑step cleaning
  - Business‑aware handling of nulls
- Dataset is now ready for **exploratory analysis, dashboards, or machine learning pipelines**.

---

## 🚀 How to Run
1. Download the dataset from Kaggle.
2. Import into your SQL environment (MySQL recommended).
3. Run the provided SQL scripts step by step.
4. Final cleaned table: `world_layoffs.layoffs_staging2`.

## 📂 Repository Structure
