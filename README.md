# B2B-Customer-Analytics-And-Survey-Analysis-Project
A comprehensive data science end-to-end project analyzing B2B customer satisfaction, NPS scores, and purchase likelihood through data cleaning, exploratory analysis, and statistical modeling.

## Overview
This project demonstrates a complete data analytics pipeline from raw data to actionable insights:

1) Data Cleaning & Validation: Python-based ETL with intelligent null handling and outlier detection
2) Exploratory Data Analysis: Comprehensive statistical analysis with correlation and groupby studies
3) Statistical Modeling: OLS Regression with heteroscedasticity testing (R² = 0.748)
4) Interactive Excel: VBA-powered search bar automation for operational use
5) Business Intelligence: Power BI dashboard for executive visualization

Dataset: 1,200 B2B survey responses across 9 industries and 7 countries with 14 features

## Data Pipeline & Methodology (Python Workflow)

The data science pipeline implemented in the Jupyter Notebook follows a structured approach:

### 1. Import Dataset/Libraries & Data Cleaning
**Import Dataset & Libraries:**



<img width="1446" height="761" alt="image" src="https://github.com/user-attachments/assets/0654f5de-834b-4dca-b206-80b183253ed3" />




* **Duplicate Management:** Identification and removal of duplicate records to ensure data integrity.
* **Text Normalization:** Column headers and string data (such as `country`, `industry`, and `free_text_response`) were stripped of leading/trailing whitespaces, and special characters (`-`) in company names were appropriately replaced.
* **Missing Value Imputation:**
  * For the `industry` column, missing fields were tagged as `"Unknown"`.
  * For the `satisfaction_score`, a conditional imputation strategy based on the Net Promoter Score (NPS) was used.
  * For `annual_revenue_usd`, missing financial fields were imputed using the column mean.
* **Data Formatting:** Rounded and converted annual revenue metrics into clean integers for standard formatting.
